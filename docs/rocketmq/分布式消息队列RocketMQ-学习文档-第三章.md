
# 分布式消息队列RocketMQ学习文档

> 本文资料来源：尚硅谷 | 本文发表时RocketMQ的版本：`v4.9.2` | 本资料是第三章内容，本文档总共有四章。

<hr/>

> 文章目录：
<ul>
<li><a target="_blank" href="https://hello-blogger-ui.blogspot.com/2021/10/rocketmq.html">分布式消息队列RocketMQ-学习文档-第一章</a></li>
<li><a target="_blank" href="https://hello-blogger-ui.blogspot.com/2021/10/rocketmq_29.html">分布式消息队列RocketMQ-学习文档-第二章</a></li>
<li><a target="_blank" href="https://hello-blogger-ui.blogspot.com/2021/10/rocketmq_62.html">分布式消息队列RocketMQ-学习文档-第三章</a></li>
<li><a target="_blank" href="https://hello-blogger-ui.blogspot.com/2021/10/rocketmq_32.html">分布式消息队列RocketMQ-学习文档-第四章</a></li>
</ul>


## 第3章 RocketMQ工作原理

### 一、消息的生产

#### 1、消息的生产过程

Producer可以将消息写入到某Broker中的某Queue中，其经历了如下过程：

* Producer发送消息之前，会先向NameServer发出获取<font color="#0000FF">消息Topic的路由信息</font>的请求
* NameServer返回该Topic的<font color="#0000FF">路由表</font>及<font color="#0000FF">Broker列表</font>
* Producer根据代码中指定的Queue选择策略，从Queue列表中选出一个队列，用于后续存储消息
* Produer对消息做一些特殊处理，例如，消息本身超过4M，则会对其进行压缩
* Producer向选择出的Queue所在的Broker发出RPC请求，将消息发送到选择出的Queue

> 路由表：实际是一个Map，key为Topic名称，value是一个QueueData实例列表。QueueData并不是一个Queue对应一个QueueData，而是一个Broker中该Topic的所有Queue对应一个QueueData。即，只要涉及到该Topic的Broker，一个Broker对应一个QueueData。QueueData中包含brokerName。简单来说，路由表的key为Topic名称，value则为所有涉及该Topic的BrokerName列表。
> Broker列表：其实际也是一个Map。key为brokerName，value为BrokerData。一个Broker对应一个BrokerData实例，对吗？不对。一套brokerName名称相同的Master-Slave小集群对应一个BrokerData。BrokerData中包含brokerName及一个map。该map的key为brokerId，value为该broker对应的地址。brokerId为0表示该broker为Master，非0表示Slave。

#### 2、Queue选择算法

对于无序消息，其Queue选择算法，也称为消息投递算法，常见的有两种：

##### ①、轮询算法

默认选择算法。该算法保证了每个Queue中可以均匀的获取到消息。

> 该算法存在一个问题：由于某些原因，在某些Broker上的Queue可能投递延迟较严重。从而导致Producer的缓存队列中出现较大的消息积压，影响消息的投递性能。

##### ②、最小投递延迟算法

该算法会统计每次消息投递的时间延迟，然后根据统计出的结果将消息投递到时间延迟最小的Queue。如果延迟相同，则采用轮询算法投递。该算法可以有效提升消息的投递性能。

> 该算法也存在一个问题：消息在Queue上的分配不均匀。投递延迟小的Queue其可能会存在大量的消息。而对该Queue的消费者压力会增大，降低消息的消费能力，可能会导致MQ中消息的堆积。

### 二、消息的存储

RocketMQ中的消息存储在本地文件系统中，这些相关文件默认在当前用户主目录下的store目录中。

![](https://pic.imgdb.cn/item/617ae5b02ab3f51d916b1975.jpg){width="6.106944444444444in" height="2.073611111111111in"}

* abort：该文件在Broker启动后会自动创建，正常关闭Broker，该文件会自动消失。若在没有启动Broker的情况下，发现这个文件是存在的，则说明之前Broker的关闭是非正常关闭。
* checkpoint：其中存储着commitlog、consumequeue、index文件的最后刷盘时间戳 
* commitlog：其中存放着commitlog文件，而消息是写在commitlog文件中的
* config：存放着Broker运行期间的一些配置数据
* consumequeue：其中存放着consumequeue文件，队列就存放在这个目录中
* index：其中存放着消息索引文件indexFile
* lock：运行期间使用到的全局资源锁

#### 1、commitlog文件

> 说明：在很多资料中 目录中的文件简单就称为 文件。但在源码中，该文件被命名为mappedFile。

##### ①、目录与文件

commitlog目录中存放着很多的mappedFile文件，当前Broker中的所有消息都是落盘到这些mappedFile文件中的。mappedFile文件大小为1G（小于等于1G），文件名由20位十进制数构成，表示当前文件的第一条消息的起始位移偏移量。

> 第一个文件名一定是20位0构成的。因为第一个文件的第一条消息的偏移量commitlog offset为0
> 当第一个文件放满时，则会自动生成第二个文件继续存放消息。假设第一个文件大小是1073741820字节（1G = 1073741824字节），则第二个文件名就是00000000001073741824。
> 以此类推，第n个文件名应该是前n-1个文件大小之和。
> 一个Broker中所有mappedFile文件的commitlog offset是连续的

需要注意的是，一个Broker中仅包含一个commitlog目录，所有的mappedFile文件都是存放在该目录中的。即无论当前Broker中存放着多少Topic的消息，这些消息都是被顺序写入到了mappedFile文件中的。也就是说，这些消息在Broker中存放时并没有被按照Topic进行分类存放。

> mappedFile文件是顺序读写的文件，所有其访问效率很高
> 无论是SSD磁盘还是SATA磁盘，通常情况下，顺序存取效率都会高于随机存取。

##### ②、消息单元

![](https://pic.imgdb.cn/item/617aed852ab3f51d916f3ea4.jpg){width="6.106944444444444in" height="2.1881944444444446in"}

mappedFile文件内容由一个个的<font color="#00CED1">消息单元</font>构成。每个消息单元中包含消息总长度MsgLen、消息的物理位置physicalOffset、消息体内容Body、消息体长度BodyLength、消息主题Topic、Topic长度TopicLength、消息生产者BornHost、消息发送时间戳BornTimestamp、消息所在的队列QueueId、消息在Queue中存储的偏移量QueueOffset等近20余项消息相关属性。

> 需要注意到，消息单元中是包含 相关属性的。所以，我们在后续的学习中，就需要十分留意commitlog与queue间的关系是什么？
> 一个mappedFile文件中第m+1个消息单元的commitlog offset偏移量
> L(m+1) = L(m) + MsgLen(m) (m >= 0)

#### 2、consumequeue

![](https://pic.imgdb.cn/item/617aee362ab3f51d916f91cf.jpg){width="6.106944444444444in" height="4.011805555555555in"}

##### ①、目录与文件

![](https://pic.imgdb.cn/item/617aee682ab3f51d916fa882.jpg){width="6.106944444444444in" height="5.366666666666666in"}

为了提高效率，会为每个Topic在\~/store/consumequeue中创建一个目录，目录名为Topic名称。在该Topic目录下，会再为每个该Topic的Queue建立一个目录，目录名为queueId。每个目录中存放着若干consumequeue文件，consumequeue文件是commitlog的索引文件，可以根据consumequeue定位到具体的消息。

consumequeue文件名也由20位数字构成，表示当前文件的第一个索引条目的起始位移偏移量。与mappedFile文件名不同的是，其后续文件名是固定的。因为consumequeue文件大小是固定不变的。

##### ②、索引条目

![](https://pic.imgdb.cn/item/617aeea62ab3f51d916fcf18.jpg){width="3.8868055555555556in" height="2.011111111111111in"}

每个consumequeue文件可以包含30w个索引条目，每个索引条目包含了三个消息重要属性：消息在mappedFile文件中的偏移量CommitLog Offset、消息长度、消息Tag的hashcode值。这三个属性占20个字节，所以每个文件的大小是固定的30w \* 20字节。

> 一个consumequeue文件中所有消息的Topic一定是相同的。但每条消息的Tag可能是不同的

#### 3、对文件的读写

![](https://pic.imgdb.cn/item/617aeefd2ab3f51d91700b7c.jpg){width="6.106944444444444in" height="3.3243055555555556in"}

##### ①、消息写入

一条消息进入到Broker后经历了以下几个过程才最终被持久化。

* Broker根据queueId，获取到该消息对应索引条目要在consumequeue目录中的写入偏移量，即QueueOffset
* 将queueId、queueOffset等数据，与消息一起封装为消息单元
* 将消息单元写入到commitlog
* 同时，形成消息索引条目
* 将消息索引条目分发到相应的consumequeue

##### ②、消息拉取

当Consumer来拉取消息时会经历以下几个步骤：

* Consumer获取到其要消费消息所在Queue的消费偏移量offset ，计算出其要消费消息的消息offset

> 消费offset即消费进度，consumer对某个Queue的消费offset，即消费到了该Queue的第几条消息
> 消息offset = 消费offset + 1

* Consumer向Broker发送拉取请求，其中会包含其要拉取消息的Queue、消息offset及消息Tag。
* Broker计算在该consumequeue中的queueOffset。

> queueOffset = 消息offset * 20字节

* 从该queueOffset处开始向后查找第一个指定Tag的索引条目。
* 解析该索引条目的前8个字节，即可定位到该消息在commitlog中的commitlog offset 
* 从对应commitlog offset中读取消息单元，并发送给Consumer

##### ③、性能提升

RocketMQ中，无论是消息本身还是消息索引，都是存储在磁盘上的。其不会影响消息的消费吗？当然不会。其实RocketMQ的性能在目前的MQ产品中性能是非常高的。因为系统通过一系列相关机制大大提升了性能。

首先，RocketMQ对文件的读写操作是通过mmap零拷贝进行的，将对文件的操作转化为直接对内存地址进行操作，从而极大地提高了文件的读写效率。

其次，consumequeue中的数据是顺序存放的，还引入了PageCache的预读取机制，使得对consumequeue文件的读取几乎接近于内存读取，即使在有消息堆积情况下也不会影响性能。

> PageCache机制，页缓存机制，是OS对文件的缓存机制，用于加速对文件的读写操作。一般来说，程序对文件进行顺序读写的速度几乎接近于内存读写速度，主要原因是由于OS使用PageCache机制对读写访问操作进行性能优化，将一部分的内存用作PageCache。
>
> * 写操作：OS会先将数据写入到PageCache中，随后会以异步方式由pdflush（page dirty flush)内核线程将Cache中的数据刷盘到物理磁盘
> * 读操作：若用户要读取数据，其首先会从PageCache中读取，若没有命中，则OS在从物理磁盘上加载该数据到PageCache的同时，也会顺序对其相邻数据块中的数据进行预读取。

RocketMQ中可能会影响性能的是对commitlog文件的读取。因为对commitlog文件来说，读取消息时会产生大量的随机访问，而随机访问会严重影响性能。不过，如果选择合适的系统IO调度算法，比如设置调度算法为Deadline（采用SSD固态硬盘的话），随机读的性能也会有所提升。

#### 4、与Kafka的对比

RocketMQ的很多思想来源于Kafka，其中commitlog与consumequeue就是。

RocketMQ中的commitlog目录与consumequeue的结合就类似于Kafka中的partition分区目录。

> Kafka中的Topic的消息被分割为一个或多个partition。partition是一个物理概念，对应到系统上就是topic目录下的一个或多个目录。每个partition中包含的文件称为segment，是具体存放消息的文件。
> Kafka中消息存放的目录结构是：topic目录下有partition目录，partition目录下有segment文件
> Kafka中没有二级分类标签Tag这个概念
> Kafka中无需索引文件。因为生产者是将消息直接写在了partition中的，消费者也是直接从partition中读取数据的

### 三、indexFile

除了通过通常的指定Topic进行消息消费外，RocketMQ还提供了根据key进行消息查询的功能。该查询是通过store目录中的index子目录中的indexFile进行索引实现的快速查询。当然，这个indexFile中的索引数据是在包含了key的消息被发送到Broker时写入的。如果消息中没有包含key，则不会写入。

#### 1、索引条目结构

每个Broker中会包含一组indexFile，每个indexFile都是以一个时间戳命名的（这个indexFile被创建时的时间戳）。每个indexFile文件由三部分构成：indexHeader，slots槽位，indexes索引数据。每个indexFile文件中包含500w个slot槽。而每个slot槽又可能会挂载很多的index索引单元。

![](https://pic.imgdb.cn/item/617af1ee2ab3f51d91722179.jpg){width="3.865972222222222in" height="1.4590277777777778in"}

indexHeader固定40个字节，其中存放着如下数据：

![](https://pic.imgdb.cn/item/617af20e2ab3f51d91723081.jpg){width="6.106944444444444in" height="1.542361111111111in"}

* beginTimestamp：该indexFile中第一条消息的存储时间
* endTimestamp：该indexFile中最后一条消息存储时间
* beginPhyoffset：该indexFile中第一条消息在commitlog中的偏移量commitlog offset
* endPhyoffset：该indexFile中最后一条消息在commitlog中的偏移量commitlog offset
* hashSlotCount：已经填充有index的slot数量（并不是每个slot槽下都挂载有index索引单元，这里统计的是所有挂载了index索引单元的slot槽的数量）
* indexCount：该indexFile中包含的索引单元个数（统计出当前indexFile中所有slot槽下挂载的所有index索引单元的数量之和）

indexFile中最复杂的是Slots与Indexes间的关系。在实际存储时，Indexes是在Slots后面的，但为了便于理解，将它们的关系展示为如下形式：

![](https://pic.imgdb.cn/item/617af2bd2ab3f51d91728a7d.jpg){width="6.106944444444444in" height="4.2625in"}

key的hash值 % 500w 的结果即为slot槽位，然后将该slot值修改为该index索引单元的indexNo，根据这个indexNo可以计算出该index单元在indexFile中的位置。不过，该取模结果的重复率是很高的，为了解决该问题，在每个index索引单元中增加了preIndexNo，用于指定该slot中当前index索引单元的前一个index索引单元。而slot中始终存放的是其下最新的index索引单元的indexNo，这样的话，只要找到了slot就可以找到其最新的index索引单元，而通过这个index索引单元就可以找到其之前的所有index索引单元。

> indexNo是一个在indexFile中的流水号，从0开始依次递增。即在一个indexFile中所有indexNo是以此递增的。indexNo在index索引单元中是没有体现的，其是通过indexes中依次数出来的。

index索引单元默写20个字节，其中存放着以下四个属性：

![](https://pic.imgdb.cn/item/617af31b2ab3f51d9172baa0.jpg){width="6.106944444444444in" height="1.854861111111111in"}

* keyHash：消息中指定的业务key的hash值
* phyOffset：当前key对应的消息在commitlog中的偏移量commitlog offset
* timeDiff：当前key对应消息的存储时间与当前indexFile创建时间的时间差
* preIndexNo：当前slot下当前index索引单元的前一个index索引单元的indexNo

#### 2、indexFile的创建

indexFile的文件名为当前文件被创建时的时间戳。这个时间戳有什么用处呢？

根据业务key进行查询时，查询条件除了key之外，还需要指定一个要查询的时间戳，表示要查询不大于该时间戳的最新的消息，即查询指定时间戳之前存储的最新消息。这个时间戳文件名可以简化查询，提高查询效率。具体后面会详细讲解。

indexFile文件是何时创建的？其创建的条件（时机）有两个：

* 当第一条带key的消息发送来后，系统发现没有indexFile，此时会创建第一个indexFile文件
* 当一个indexFile中挂载的index索引单元数量超出2000w个时，会创建新的indexFile。当带key的消息发送到来后，系统会找到最新的indexFile，并从其indexHeader的最后4字节中读取到indexCount。若indexCount >= 2000w时，会创建新的indexFile。

> 由于可以推算出，一个indexFile的最大大小是：(40 + 500w * 4 + 2000w * 20)字节

#### 3、查询流程

当消费者通过业务key来查询相应的消息时，其需要经过一个相对较复杂的查询流程。不过，在分析查询流程之前，首先要清楚几个定位计算式子：

```txt
计算指定消息key的slot槽位序号：
slot槽位序号 = key的hash % 500w (式子1)

计算槽位序号为n的slot在indexFile中的起始位置：
slot(n)位置 = 40 + (n - 1) * 4 (式子2)

计算indexNo为m的index在indexFile中的位置：
index(m)位置 = 40 + 500w * 4 + (m - 1) * 20 (式子3)
```

> 40为indexFile中indexHeader的字节数
> 500w * 4 是所有slots所占的字节数

##### 具体查询流程如下：

![](https://pic.imgdb.cn/item/617bb1b02ab3f51d91009a09.jpg){width="6.106944444444444in" height="3.5118055555555556in"}

### 四、消息的消费

消费者从Broker中获取消息的方式有两种：pull拉取方式和push推动方式。消费者组对于消息消费的模式又分为两种：集群消费Clustering和广播消费Broadcasting。

#### 1、获取消费类型

##### ①、拉取式消费

Consumer主动从Broker中拉取消息，主动权由Consumer控制。一旦获取了批量消息，就会启动消费过程。不过，该方式的实时性较弱，即Broker中有了新的消息时消费者并不能及时发现并消费。

> 由于拉取时间间隔是由用户指定的，所以在设置该间隔时需要注意平稳：间隔太短，空请求比例会增加；间隔太长，消息的实时性太差

##### ②、推送式消费

该模式下Broker收到数据后会主动推送给Consumer。该获取方式一般实时性较高。

该获取方式是典型的<font color="#00FFFF">发布-订阅</font>模式，即Consumer向其关联的Queue注册了监听器，一旦发现有新的消息到来就会触发回调的执行，回调方法是Consumer去Queue中拉取消息。而这些都是基于Consumer与Broker间的长连接的。长连接的维护是需要消耗系统资源的。

##### ③、对比

* pull：需要应用去实现对关联Queue的遍历，实时性差；但便于应用控制消息的拉取 
* push：封装了对关联Queue的遍历，实时性强，但会占用较多的系统资源

#### 2、消费模式

##### ①、广播消费

![](https://pic.imgdb.cn/item/617bb3672ab3f51d9101da3c.jpg){width="5.825694444444444in" height="3.5743055555555556in"}

广播消费模式下，相同Consumer Group的每个Consumer实例都接收同一个Topic的全量消息。即每条消息都会被发送到Consumer Group中的<font color="#00FFFF">每个</font>Consumer。

##### ②、集群消费

![](https://pic.imgdb.cn/item/617bb3b92ab3f51d9102208c.jpg){width="5.804861111111111in" height="3.490972222222222in"}

集群消费模式下，相同Consumer Group的每个Consumer实例<font color="#00FFFF">平均分摊</font>同一个Topic的消息。即每条消息只会被发送到Consumer Group中的<font color="#00FFFF">某个</font>Consumer。

##### ③、消息进度保存

* 广播模式：消费进度保存在consumer端。因为广播模式下consumer group中每个consumer都会消费所有消息，但它们的消费进度是不同。所以consumer各自保存各自的消费进度。
* 集群模式：消费进度保存在broker中。consumer group中的所有consumer共同消费同一个Topic中的消息，同一条消息只会被消费一次。消费进度会参与到了消费的负载均衡中，故消费进度是需要共享的。下图是broker中存放的各个Topic的各个Queue的消费进度。

![](https://pic.imgdb.cn/item/617bb4352ab3f51d910279d5.jpg){width="6.106944444444444in" height="3.9805555555555556in"}

#### 3、Rebalance机制

Rebalance机制讨论的前提是：集群消费。

##### ①、什么是Rebalance

Rebalance即再均衡，指的是，将一个Topic下的多个Queue在同一个Consumer Group中的多个Consumer间进行重新分配的过程。

![](https://pic.imgdb.cn/item/617bb48d2ab3f51d9102bd39.jpg){width="6.106944444444444in" height="3.1680555555555556in"}

Rebalance机制的本意是为了提升消息的<font color="#00FFFF">并行消费能力</font>。例如，一个Topic下5个队列，在只有1个消费者的情况下，这个消费者将负责消费这5个队列的消息。如果此时我们增加一个消费者，那么就可以给其中一个消费者分配2个队列，给另一个分配3个队列，从而提升消息的并行消费能力。

##### ②、Rebalance限制

由于一个队列最多分配给一个消费者，因此当某个消费者组下的消费者实例数量大于队列的数量时，多余的消费者实例将分配不到任何队列。

##### ③、Rebalance危害

Rebalance的在提升消费能力的同时，也带来一些问题：

<font color="#FF0000">消费暂停</font>：在只有一个Consumer时，其负责消费所有队列；在新增了一个Consumer后会触发Rebalance的发生。此时原Consumer就需要暂停部分队列的消费，等到这些队列分配给新的Consumer后，这些暂停消费的队列才能继续被消费。

<font color="#FF0000">消费重复</font>：Consumer 在消费新分配给自己的队列时，必须接着之前Consumer 提交的消费进度的offset继续消费。然而默认情况下，offset是异步提交的，这个异步性导致提交到Broker的offset与Consumer实际消费的消息并不一致。这个不一致的差值就是可能会重复消费的消息。

> 同步提交： consumer提交了其消费完毕的一批消息的offset给broker后，需要等待broker的成功ACK。当收到ACK后，consumer才会继续获取并消费下一批消息。在等待ACK期间，consumer是阻塞的。
> 异步提交：consumer提交了其消费完毕的一批消息的offset给broker后，不需要等待broker的成功ACK。consumer可以直接获取并消费下一批消息。
> 对于一次性读取消息的数量，需要根据具体业务场景选择一个相对均衡的是很有必要的。因为数量过大，系统性能提升了，但产生重复消费的消息数量可能会增加；数量过小，系统性能会下降，但被重复消费的消息数量可能会减少。



<font color="#FF0000">消费突刺</font>：由于Rebalance可能导致重复消费，如果需要重复消费的消息过多，或者因为Rebalance暂停时间过长从而导致积压了部分消息。那么有可能会导致在Rebalance结束之后瞬间需要消费很多消息。

##### ④、Rebalance产生的原因

导致Rebalance产生的原因，无非就两个：消费者所订阅Topic的Queue数量发生变化，或消费者组中消费者的数量发生变化。

> 1）Queue数量发生变化的场景：
>
> * Broker扩容或缩容
> * Broker升级运维
> * Broker与NameServer间的网络异常
> * Queue扩容或缩容
>   2）消费者数量发生变化的场景：
> * Consumer Group扩容或缩容
> * Consumer升级运维
> * Consumer与NameServer间网络异常


##### ⑤、Rebalance过程

在Broker中维护着多个Map集合，这些集合中动态存放着当前Topic中Queue的信息、Consumer Group 中Consumer实例的信息。一旦发现消费者所订阅的Queue数量发生变化，或消费者组中消费者的数量发生变化，立即向Consumer Group中的每个实例发出Rebalance通知。

> TopicConfigManager：key是topic名称，value是TopicConfig。TopicConfig中维护着该Topic中所有Queue的数据。
> ConsumerManager：key是Consumser Group Id，value是ConsumerGroupInfo。ConsumerGroupInfo中维护着该Group中所有Consumer实例数据。
> ConsumerOffsetManager：key为Topic与订阅该Topic的Group的组合,即topic@group，value是一个内层Map。内层Map的key为QueueId，内层Map的value为该Queue的消费进度offset。

##### ⑥、与Kafka对比

在Kafka中，一旦发现出现了Rebalance条件，Broker会调用Group Coordinator来完成Rebalance。Coordinator是Broker中的一个进程。Coordinator会在Consumer Group中选出一个Group Leader。由这个Leader根据自己本身组情况完成Partition分区的再分配。这个再分配结果会上报给Coordinator，并由Coordinator同步给Group中的所有Consumer实例。

Kafka中的Rebalance是由Consumer Leader完成的。而RocketMQ中的Rebalance是由每个Consumer自身完成的，Group中不存在Leader。

#### 4、Queue分配算法

一个Topic中的Queue只能由Consumer Group中的一个Consumer进行消费，而一个Consumer可以同时消费多个Queue中的消息。那么Queue与Consumer间的配对关系是如何确定的，即Queue要分配给哪个Consumer进行消费，也是有算法策略的。常见的有四种策略。这些策略是通过在创建Consumer时的构造器传进去的。

##### ①、平均分配策略

![](https://pic.imgdb.cn/item/617bb6ff2ab3f51d9104cb00.jpg){width="4.345833333333333in" height="3.1680555555555556in"}

该算法是要根据avg = QueueCount / ConsumerCount 的计算结果进行分配的。如果能够整除，则按顺序将avg个Queue逐个分配Consumer；如果不能整除，则将多余出的Queue按照Consumer顺序逐个分配。

> 该算法即，先计算好每个Consumer应该分得几个Consumer，然后再依次将这些数量的Queue逐个分配给Consumer。

##### ②、环形平均策略

![](https://pic.imgdb.cn/item/617bb7cd2ab3f51d91057ab1.jpg){width="5.950694444444444in" height="5.022916666666666in"}

环形平均算法是指，根据消费者的顺序，依次在由queue队列组成的环形图中逐个分配。

> 该算法不用事先计算每个Consumer需要分配几个Queue，直接一个一个分即可。

##### ③、一致性hash策略

![](https://pic.imgdb.cn/item/617bb8492ab3f51d9105ea1d.jpg){width="4.73125in" height="4.470833333333333in"}

该算法会将consumer的hash值作为Node节点存放到hash环上，然后将queue的hash值也放到hash环上，通过顺时针方向，距离queue最近的那个consumer就是该queue要分配的consumer。

> 该算法存在的问题：分配不均。

##### ④、同机房策略

![](https://pic.imgdb.cn/item/617bb8912ab3f51d91063c77.jpg){width="6.106944444444444in" height="3.4493055555555556in"}

该算法会根据queue的部署机房位置和consumer的位置，过滤出当前consumer相同机房的queue。然后按照平均分配策略或环形平均策略对同机房queue进行分配。如果没有同机房queue，则按照平均分配策略或环形平均策略对所有queue进行分配。

##### ⑤、对比

一致性hash算法存在的问题：两种平均分配策略的分配效率较高，一致性hash策略的较低。因为一致性hash算法较复杂。另外，一致性hash策略分配的结果也很大可能上存在不平均的情况。

一致性hash算法存在的意义：其可以有效减少由于消费者组扩容或缩容所带来的大量的Rebalance。

![](https://pic.imgdb.cn/item/617bb8de2ab3f51d910673c9.jpg){width="6.106944444444444in" height="6.179861111111111in"}

致性hash算法的应用场景：Consumer数量变化较频繁的场景。

##### ⑥、至少一次原则

RocketMQ有一个原则：每条消息必须要被成功消费一次。

那么什么是成功消费呢？Consumer在消费完消息后会向其消费进度记录器提交其消费消息的offset，offset被成功记录到记录器中，那么这条消费就被成功消费了。

> 什么是消费进度记录器？
> 对于广播消费模式来说， Consumer本身就是消费进度记录器。
> 对于集群消费模式来说， Broker是消费进度记录器。

### 五、订阅关系的一致性

订阅关系的一致性指的是，同一个消费者组（Group ID相同）下所有Consumer实例所订阅的Topic与Tag及对消息的处理逻辑必须完全一致。否则，消息消费的逻辑就会混乱，甚至导致消息丢失。

#### 1、正确订阅关系

多个消费者组订阅了多个Topic，并且每个消费者组里的多个消费者实例的订阅关系保持了一致。

![](https://pic.imgdb.cn/item/617bbb182ab3f51d91084e70.jpg){width="4.960416666666666in" height="4.158333333333333in"}

#### 2、错误订阅关系

一个消费者组订阅了多个Topic，但是该消费者组里的多个Consumer实例的订阅关系并没有保持一致。

![](https://pic.imgdb.cn/item/617bbb422ab3f51d91087541.jpg){width="5.741666666666666in" height="2.323611111111111in"}

##### ①、订阅了不同Topic

该例中的错误在于，同一个消费者组中的两个Consumer实例订阅了不同的Topic。

Consumer实例1-1：（订阅了topic为jodie_test_A，tag为所有的消息）

```java
Properties properties = new Properties();
properties.put(PropertyKeyConst.GROUP_ID, "GID_jodie_test_1");
Consumer consumer = ONSFactory.createConsumer(properties);
consumer.subscribe("jodie_test_A", "*", new MessageListener() {
    public Action consume(Message message, ConsumeContext context) {
    System.out.println(message.getMsgID());
    return Action.CommitMessage;
    }
});
```

Consumer实例1-2：（订阅了topic为jodie_test_B，tag为所有的消息）

```java
Properties properties = new Properties();
properties.put(PropertyKeyConst.GROUP_ID, "GID_jodie_test_1");
Consumer consumer = ONSFactory.createConsumer(properties);
consumer.subscribe("jodie_test_B", "*", new MessageListener() {
    public Action consume(Message message, ConsumeContext context) {
    System.out.println(message.getMsgID());
    return Action.CommitMessage;
    }
});
```

##### ②、订阅了不同Tag

该例中的错误在于，同一个消费者组中的两个Consumer订阅了相同Topic的不同Tag。

Consumer实例2-1：（订阅了topic为jodie_test_A，tag为TagA的消息）

```java
Properties properties = new Properties();
properties.put(PropertyKeyConst.GROUP_ID, "GID_jodie_test_2");
Consumer consumer = ONSFactory.createConsumer(properties);
consumer.subscribe("jodie_test_A", "TagA", new MessageListener() {
    public Action consume(Message message, ConsumeContext context) {
    System.out.println(message.getMsgID());
    return Action.CommitMessage;
    }
});

```

Consumer实例2-2：（订阅了topic为jodie_test_A，tag为所有的消息）

```java
Properties properties = new Properties();
properties.put(PropertyKeyConst.GROUP_ID, "GID_jodie_test_2");
Consumer consumer = ONSFactory.createConsumer(properties);
consumer.subscribe("jodie_test_A", "*", new MessageListener() {
    public Action consume(Message message, ConsumeContext context) {
    System.out.println(message.getMsgID());
    return Action.CommitMessage;
    }
});
```

##### ③、订阅了不同数量的Topic

该例中的错误在于，同一个消费者组中的两个Consumer订阅了不同数量的Topic。

Consumer实例3-1：（该Consumer订阅了两个Topic）

```java
Properties properties = new Properties();
properties.put(PropertyKeyConst.GROUP_ID, "GID_jodie_test_3");
Consumer consumer = ONSFactory.createConsumer(properties);
consumer.subscribe("jodie_test_A", "TagA", new MessageListener() {
    public Action consume(Message message, ConsumeContext context) {
    System.out.println(message.getMsgID());
    return Action.CommitMessage;
    }
});
consumer.subscribe("jodie_test_B", "TagB", new MessageListener() {
    public Action consume(Message message, ConsumeContext context) {
    System.out.println(message.getMsgID());
    return Action.CommitMessage;
    }
});

```

Consumer实例3-2：（该Consumer订阅了一个Topic）

```java
Properties properties = new Properties();
properties.put(PropertyKeyConst.GROUP_ID, "GID_jodie_test_3");
Consumer consumer = ONSFactory.createConsumer(properties);
consumer.subscribe("jodie_test_A", "TagB", new MessageListener() {
    public Action consume(Message message, ConsumeContext context) {
    System.out.println(message.getMsgID());
    return Action.CommitMessage;
    }
});
```

### 六、offset管理

> 这里的offset指的是Consumer的消费进度offset。

消费进度offset是用来记录每个Queue的不同消费组的消费进度的。根据消费进度记录器的不同，可以
分为两种模式：本地模式和远程模式。

#### 1、offset本地管理模式

当消费模式为<font color="#00FFFF">广播消费</font>时，offset使用本地模式存储。因为每条消息会被所有的消费者消费，每个消费者管理自己的消费进度，各个消费者之间不存在消费进度的交集。

Consumer在广播消费模式下offset相关数据以json的形式持久化到Consumer本地磁盘文件中，默认文件路径为当前用户主目录下的<font color="#00FFFF">.rocketmq_offsets/\${clientId}/\${group}/Offsets.json</font> 。

其中\${clientId}为当前消费者id，默认为ip\@DEFAULT；\${group}为消费者组名称。

#### 2、offset远程管理模式

当消费模式为集群消费时，offset使用远程模式管理。因为所有Cosnumer实例对消息采用的是均衡消费，所有Consumer共享Queue的消费进度。

Consumer在集群消费模式下offset相关数据以json的形式持久化到Broker磁盘文件中，文件路径为当前用户主目录下的store/config/consumerOffset.json 。

Broker启动时会加载这个文件，并写入到一个双层Map（ConsumerOffsetManager）。外层map的key为topic\@group，value为内层map。内层map的key为queueId，value为offset。当发生Rebalance时，新的Consumer会从该Map中获取到相应的数据来继续消费。

集群模式下offset采用远程管理模式，主要是为了保证Rebalance机制。

#### 3、offset用途

消费者是如何从最开始持续消费消息的？消费者要消费的第一条消息的起始位置是用户自己通过consumer.setConsumeFromWhere()方法指定的。

在Consumer启动后，其要消费的第一条消息的起始位置常用的有三种，这三种位置可以通过枚举类型常量设置。这个枚举类型为ConsumeFromWhere。

![](https://pic.imgdb.cn/item/617bbe932ab3f51d910beca0.jpg){width="6.106944444444444in" height="5.220833333333333in"}

> CONSUME_FROM_LAST_OFFSET：从queue的当前最后一条消息开始消费
> CONSUME_FROM_FIRST_OFFSET：从queue的第一条消息开始消费
> CONSUME_FROM_TIMESTAMP：从指定的具体时间戳位置的消息开始消费。这个具体时间戳是通过另外一个语句指定的 。
> consumer.setConsumeTimestamp(“20210701080000”) yyyyMMddHHmmss

当消费完一批消息后，Consumer会提交其消费进度offset给Broker，Broker在收到消费进度后会将其更新到那个双层Map（ConsumerOffsetManager）及consumerOffset.json文件中，然后向该Consumer进行ACK，而ACK内容中包含三项数据：当前消费队列的最小offset（minOffset）、最大offset（maxOffset）、及下次消费的起始offset（nextBeginOffset）。

#### 4、重试队列

![](https://pic.imgdb.cn/item/617bbeff2ab3f51d910c48ff.jpg){width="6.106944444444444in" height="4.866666666666666in"}

当rocketMQ对消息的消费出现异常时，会将发生异常的消息的offset提交到Broker中的重试队列。系统在发生消息消费异常时会为当前的topic\@group创建一个重试队列，该队列以%RETRY%开头，到达重试时间后进行消费重试。

#### 5、offset的同步提交与异步提交

集群消费模式下，Consumer消费完消息后会向Broker提交消费进度offset，其提交方式分为两种：

同步提交：消费者在消费完一批消息后会向broker提交这些消息的offset，然后等待broker的成功响应。若在等待超时之前收到了成功响应，则继续读取下一批消息进行消费（从ACK中获取nextBeginOffset）。若没有收到响应，则会重新提交，直到获取到响应。而在这个等待过程中，消费者是阻塞的。其严重影响了消费者的吞吐量。

异步提交：消费者在消费完一批消息后向broker提交offset，但无需等待Broker的成功响应，可以继续读取并消费下一批消息。这种方式增加了消费者的吞吐量。但需要注意，broker在收到提交的offset后，还是会向消费者进行响应的。可能还没有收到ACK，此时Consumer会从Broker中直接获取nextBeginOffset。

### 七、消费幂等

#### 1、什么是消费幂等

当出现消费者对某条消息重复消费的情况时，重复消费的结果与消费一次的结果是相同的，并且多次消费并未对业务系统产生任何负面影响，那么这个消费过程就是消费幂等的。

> 幂等：若某操作执行多次与执行一次对系统产生的影响是相同的，则称该操作是幂等的。

在互联网应用中，尤其在网络不稳定的情况下，消息很有可能会出现重复发送或重复消费。如果重复的消息可能会影响业务处理，那么就应该对消息做幂等处理。

#### 2、消息重复的场景分析

什么情况下可能会出现消息被重复消费呢？最常见的有以下三种情况：

##### ①、发送时消息重复

当一条消息已被成功发送到Broker并完成持久化，此时出现了网络闪断，从而导致Broker对Producer应答失败。 如果此时Producer意识到消息发送失败并尝试再次发送消息，此时Broker中就可能会出现两条内容相同并且Message ID也相同的消息，那么后续Consumer就一定会消费两次该消息。

##### ②、消费时消息重复

消息已投递到Consumer并完成业务处理，当Consumer给Broker反馈应答时网络闪断，Broker没有接收到消费成功响应。为了保证消息至少被消费一次的原则，Broker将在网络恢复后再次尝试投递之前已被处理过的消息。此时消费者就会收到与之前处理过的内容相同、Message ID也相同的消息。

##### ③、Rebalance时消息重复

当Consumer Group中的Consumer数量发生变化时，或其订阅的Topic的Queue数量发生变化时，会触发Rebalance，此时Consumer可能会收到曾经被消费过的消息。

#### 3、通用解决方案

##### ①、两要素

幂等解决方案的设计中涉及到两项要素：幂等令牌，与唯一性处理。只要充分利用好这两要素，就可以设计出好的幂等解决方案。

* 幂等令牌：是生产者和消费者两者中的既定协议，通常指具备唯⼀业务标识的字符串。例如，订单号、流水号。一般由Producer随着消息一同发送来的。
* 唯一性处理：服务端通过采用⼀定的算法策略，保证同⼀个业务逻辑不会被重复执行成功多次。例如，对同一笔订单的多次支付操作，只会成功一次。

##### ②、解决方案

对于常见的系统，幂等性操作的通用性解决方案是：

* 1.  首先通过缓存去重。在缓存中如果已经存在了某幂等令牌，则说明本次操作是重复性操作；若缓存没有命中，则进入下一步。

* 2.  在唯一性处理之前，先在数据库中查询幂等令牌作为索引的数据是否存在。若存在，则说明本次操作为重复性操作；若不存在，则进入下一步。

* 3.  在同一事务中完成三项操作：唯一性处理后，将幂等令牌写入到缓存，并将幂等令牌作为唯一索引的数据写入到DB中。

> 第1步已经判断过是否是重复性操作了，为什么第2步还要再次判断？能够进入第 2步，说明已经不是重复操作了，第2次判断是否重复？
> 当然不重复。一般缓存中的数据是具有有效期的。缓存中数据的有效期一旦过期，就是发生缓存穿透，使请求直接就到达了DBMS。

##### ③、解决方案举例

以支付场景为例：

* 1.当支付请求到达后，首先在Redis缓存中却获取key为支付流水号的缓存value。若value不空，则说明本次支付是重复操作，业务系统直接返回调用侧重复支付标识；若value为空，则进入下一步操作

* 2.到DBMS中根据支付流水号查询是否存在相应实例。若存在，则说明本次支付是重复操作，业务系统直接返回调用侧重复支付标识；若不存在，则说明本次操作是首次操作，进入下一步完成唯一性处理

* 3.在分布式事务中完成三项操作：

> ①、完成支付任务
> ②、将当前支付流水号作为key，任意字符串作为value，通过set(key, value, expireTime)将数据写入到Redis缓存
> ③、将当前支付流水号作为主键，与其它相关数据共同写入到DBMS

#### 4、消费幂等的实现

消费幂等的解决方案很简单：为消息指定不会重复的唯一标识。因为Message ID有可能出现重复的情况，所以真正安全的幂等处理，不建议以Message ID作为处理依据。最好的方式是以业务唯一标识作为幂等处理的关键依据，而业务的唯一标识可以通过消息Key设置。

以支付场景为例，可以将消息的Key设置为订单号，作为幂等处理的依据。具体代码示例如下：

```java
Message message = new Message();
message.setKey("ORDERID_100");
SendResult sendResult = producer.send(message);
```

消费者收到消息时可以根据消息的Key即订单号来实现消费幂等：

```java
consumer.registerMessageListener(new MessageListenerConcurrently() {
    @Override
    public ConsumeConcurrentlyStatus consumeMessage(List<MessageExt>
    msgs,
    ConsumeConcurrentlyContext
    context) {
    for(MessageExt msg:msgs){
        String key = msg.getKeys();
        // 根据业务唯一标识Key做幂等处理
        // ……
    }
    return ConsumeConcurrentlyStatus.CONSUME_SUCCESS;
    }
});

```

> RocketMQ能够保证消息不丢失，但不能保证消息不重复。

### 八、消息堆积与消费延迟

#### 1、概念

消息处理流程中，如果Consumer的消费速度跟不上Producer的发送速度，MQ中未处理的消息会越来越多（进的多出的少），这部分消息就被称为堆积消息。消息出现堆积进而会造成消息的消费延迟。以下场景需要重点关注消息堆积和消费延迟问题：

* 业务系统上下游能力不匹配造成的持续堆积，且无法自行恢复。
* 业务系统对消息的消费实时性要求较高，即使是短暂的堆积造成的消费延迟也无法接受。

#### 2、产生原因分析

![](https://pic.imgdb.cn/item/617bc4c12ab3f51d9111a0d2.jpg){width="6.106944444444444in" height="2.647222222222222in"}

Consumer使用长轮询Pull模式消费消息时，分为以下两个阶段：

##### ①、消息拉取

Consumer通过长轮询Pull模式批量拉取的方式从服务端获取消息，将拉取到的消息缓存到本地缓冲队列中。对于拉取式消费，在内网环境下会有很高的吞吐量，所以这一阶段一般不会成为消息堆积的瓶颈。

> 一个单线程单分区的低规格主机(Consumer，4C8G)，其可达到几万的TPS。如果是多个分区多个线程，则可以轻松达到几十万的TPS。

##### ②、消息消费

Consumer将本地缓存的消息提交到消费线程中，使用业务消费逻辑对消息进行处理，处理完毕后获取到一个结果。这是真正的消息消费过程。此时Consumer的消费能力就完全依赖于消息的消费耗时和消费并发度了。如果由于业务处理逻辑复杂等原因，导致处理单条消息的耗时较长，则整体的消息吞吐量肯定不会高，此时就会导致Consumer本地缓冲队列达到上限，停止从服务端拉取消息。

##### ③、结论

消息堆积的主要瓶颈在于客户端的消费能力，而消费能力由<font color="#0000FF">消费耗时</font>和<font color="#0000FF">消费并发度</font>决定。注意，消费耗时的优先级要高于消费并发度。即在保证了<font color="#0000FF">消费耗时</font>的合理性前提下，再考虑消费并发度问题。

#### 3、消费耗时

影响消息处理时长的主要因素是代码逻辑。而代码逻辑中可能会影响处理时长代码主要有两种类型：<font color="#0000FF">CPU内部计算型代码</font>和<font color="#0000FF">外部I/O操作型代码</font>。

通常情况下代码中如果没有复杂的递归和循环的话，内部计算耗时相对外部I/O操作来说几乎可以忽略。所以外部IO型代码是影响消息处理时长的主要症结所在。

> 外部IO操作型代码举例：
>
> * 读写外部数据库，例如对远程MySQL的访问
> * 读写外部缓存系统，例如对远程Redis的访问
> * 下游系统调用，例如Dubbo的RPC远程调用，Spring Cloud的对下游系统的Http接口调用

> 关于下游系统调用逻辑需要进行提前梳理，掌握每个调用操作预期的耗时，这样做是为了能够判断消费逻辑中IO操作的耗时是否合理。通常消息堆积是由于下游系统出现了<font color="#0000FF">服务异常</font>或<font color="#0000FF">达到了DBMS容量限制</font>，导致消费耗时增加。

> 服务异常，并不仅仅是系统中出现的类似500这样的代码错误，而可能是更加隐蔽的问题。例如，网络带宽问题。

> 达到了DBMS容量限制，其也会引发消息的消费耗时增加。


#### 4、消费并发度

一般情况下，消费者端的消费并发度由单节点线程数和节点数量共同决定，其值为<font color="#0000FF">单节点线程数</font> * <font color="#0000FF">节点数量</font>。不过，通常需要优先调整单节点的线程数，若单机硬件资源达到了上限，则需要通过横向扩展来提高消费并发度。

> 单节点线程数，即单个Consumer所包含的线程数量

> 节点数量，即Consumer Group所包含的Consumer数量

> 对于普通消息、延时消息及事务消息，并发度计算都是 <font color="#0000FF">单节点线程数</font> * <font color="#0000FF">节点数量</font> 。但对于顺序消息则是不同的。顺序消息的消费并发度等于 <font color="#0000FF">Topic的Queue分区数量</font> 。

> 1）全局顺序消息：该类型消息的Topic只有一个Queue分区。其可以保证该Topic的所有消息被顺序消费。为了保证这个全局顺序性，Consumer Group中在同一时刻只能有一个Consumer的一个线程进行消费。所以其并发度为1。

> 2）分区顺序消息：该类型消息的Topic有多个Queue分区。其仅可以保证该Topic的每个Queue分区中的消息被顺序消费，不能保证整个Topic中消息的顺序消费。为了保证这个分区顺序性，每个Queue分区中的消息在Consumer Group中的同一时刻只能有一个Consumer的一个线程进行消费。即，在同一时刻最多会出现多个Queue分蘖有多个Consumer的多个线程并行消费。所以其并发度为Topic的分区数量。

#### 5、单机线程数计算

对于一台主机中线程池中线程数的设置需要谨慎，不能盲目直接调大线程数，设置过大的线程数反而会带来大量的线程切换的开销。<font color="#0000FF">理想环境下单节点的最优线程数计算模型为：C \*（T1 + T2）/ T1</font>。

* C：CPU内核数
* T1：CPU内部逻辑计算耗时
* T2：外部IO操作耗时

![](media/image223.png){width="5.2083333333333336e-2in" height="0.19791666666666666in"}

> 最优线程数= C *（T1+T2）/T1=C*T1/T1+C*T2/T1=C+C*T2/T1

> 注意，该计算出的数值是理想状态下的理论数据，在生产环境中，不建议直接使用。而是根据当前环境，先设置一个比该值小的数值然后观察其压测效果，然后再根据效果逐步调大线程数，直至找到在该环境中性能最佳时的值。

#### 6、如何避免

为了避免在业务使用时出现非预期的消息堆积和消费延迟问题，需要在前期设计阶段对整个业务逻辑进行完善的排查和梳理。其中最重要的就是<font color="#0000FF">梳理消息的消费耗时</font>和<font color="#0000FF">设置消息消费的并发度</font>。

##### ①、梳理消息的消费耗时

通过压测获取消息的消费耗时，并对耗时较高的操作的代码逻辑进行分析。梳理消息的消费耗时需要关注以下信息：

* 消息消费逻辑的计算复杂度是否过高，代码是否存在无限循环和递归等缺陷。
* 消息消费逻辑中的I/O操作是否是必须的，能否用本地缓存等方案规避。
* 消费逻辑中的复杂耗时的操作是否可以做异步化处理。如果可以，是否会造成逻辑错乱。

##### ②、设置消费并发度

对于消息消费并发度的计算，可以通过以下两步实施：

* 逐步调大单个Consumer节点的线程数，并观测节点的系统指标，得到单个节点最优的消费线程数和消息吞吐量。
* 根据上下游链路的<font color="#0000FF">流量峰值</font>计算出需要设置的节点数

> 节点数=流量峰值/单个节点消息吞吐量

### 九、消息的清理

消息被消费过后会被清理掉吗？不会的。

消息是被顺序存储在commitlog文件的，且消息大小不定长，所以消息的清理是不可能以消息为单位进行清理的，而是以commitlog文件为单位进行清理的。否则会急剧下降清理效率，并实现逻辑复杂。

commitlog文件存在一个<font color="#0000FF">过期时间</font>，默认为72小时，即三天。除了用户手动清理外，在以下情况下也会被自动清理，无论文件中的消息是否被消费过：

* 文件过期，且到达<font color="#0000FF">清理时间点</font>（默认为凌晨4点）后，自动清理过期文件
* 文件过期，且磁盘空间占用率已达<font color="#0000FF">过期清理警戒线</font>（默认75%）后，无论是否达到清理时间点，都会自动清理过期文件
* 磁盘占用率达到<font color="#0000FF">清理警戒线</font>（默认85%）后，开始按照设定好的规则清理文件，无论是否过期。默认会从最老的文件开始清理
* 磁盘占用率达到<font color="#0000FF">系统危险警戒线</font>（默认90%）后，Broker将拒绝消息写入

> 需要注意以下几点：
> 1）对于RocketMQ系统来说，删除一个1G大小的文件，是一个压力巨大的IO操作。在删除过程中，系统性能会骤然下降。所以，其默认清理时间点为凌晨4点，访问量最小的时间。也正因如果，我们要保障磁盘空间的空闲率，不要使系统出现在其它时间点删除commitlog文件的情况。
> 2）官方建议RocketMQ服务的Linux文件系统采用ext4。因为对于文件删除操作，ext4要比ext3性能更好

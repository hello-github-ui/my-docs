<section class="normal markdown-section">
<div id="content">
<h1>15. Hystrix 超时和 Ribbon Clients</h1>
<div><ins class="adsbygoogle" style="display:block; text-align:center;" data-ad-layout="in-article" data-ad-format="fluid" data-ad-client="ca-pub-6108808167664152" data-ad-slot="6964403648"></ins>
<script>
(adsbygoogle = window.adsbygoogle || []).push({});
</script></div>
<div><p>使用包装 Ribbon clients 的 Hystrix 命令时，要确保将 Hystrix 超时配置为长于配置的 Ribbon 超时，包括可能进行的任何可能的重试。例如，如果您的 Ribbon 连接超时为一秒且 Ribbon client 可能会重试请求三次，那么 Hystrix 超时应该略大于三秒。</p>
<h2 id="如何包含-hystrix-仪表板"><a href="#netflix-hystrix-dashboard-starter" id="netflix-hystrix-dashboard-starter"></a> 15.1 如何包含 Hystrix 仪表板</h2>
<p>要在项目中包含 Hystrix 仪表板，请使用带有 group <code>org.springframework.cloud</code>和 artifact id <code>spring-cloud-starter-netflix-hystrix-dashboard</code>的 starter。有关使用当前 Spring Cloud Release Train 设置 build 系统的详细信息，请参阅<a href="https://projects.spring.io/spring-cloud/" target="_blank" rel="noopener noreferrer">Spring Cloud 项目页面</a>。</p>
<p>要 run Hystrix 仪表板使用<code>@EnableHystrixDashboard</code>注释 Spring Boot main class。然后，您访问<code>/hystrix</code>并将仪表板指向 Hystrix client application 中的单个实例<code>/hystrix.stream</code>端点。</p>
<blockquote><p>当连接到使用 HTTPS 的<code>/hystrix.stream</code>端点时，JVM 必须信任服务器使用的证书。如果证书不受信任，则必须__ortort 将证书导入 order 中的 JVM，以便 Hystrix 仪表板成功连接到流端点。</p>
</blockquote>
<h2 id="turbine"><a href="#_turbine" id="_turbine"></a> 15.2 Turbine</h2>
<p>查看单个实例 Hystrix 数据在系统整体运行状况方面不是很有用。 <a href="https://github.com/Netflix/Turbine" target="_blank" rel="noopener noreferrer">涡轮</a>是一个 application，它将所有相关的<code>/hystrix.stream</code> endpoints 聚合为<code>/turbine.stream</code>组合，以便在 Hystrix 仪表板中使用。个别实例位于 Eureka。 Running Turbine 就像使用<code>@EnableTurbine</code> annotation(e.g. 使用 spring-cloud-starter-netflix-turbine 设置 classpath)注释主 class 一样简单。来自<a href="https://github.com/Netflix/Turbine/wiki/Configuration-(1.x)" target="_blank" rel="noopener noreferrer">Turbine 1 维基</a>的所有记录的 configuration properties 都适用。唯一的区别是<code>turbine.instanceUrlSuffix</code>不需要 port 前置，因为这是自动处理的，除非<code>turbine.instanceInsertPort=false</code>。</p>
<blockquote><p>默认情况下，Turbine 通过查找 Eureka 中的<code>hostName</code>和<code>port</code>条目，然后将<code>/hystrix.stream</code>附加到其上来查找已注册实例上的<code>/hystrix.stream</code>端点。如果实例的元数据包含<code>management.port</code>，则将使用它来代替<code>/hystrix.stream</code>端点的<code>port</code> value。默认情况下，元数据条目<code>management.port</code>等于<code>management.port</code> configuration property，但可以通过以下 configuration 覆盖它：</p>
</blockquote>
<pre><code class="language-">eureka:
  instance:
    metadata-map:
      management.port: ${management.port:8081}
</code></pre>
<p>configuration key <code>turbine.appConfig</code>是_tureine 将用于查找实例的 eureka serviceIds 列表。然后使用类似于以下内容的 URL 在 Hystrix 仪表板中使用 turbine 流：<code>http://my.turbine.sever:8080/turbine.stream?cluster=CLUSTERNAME</code>(如果 name 是“default”，则可以省略 cluster 参数)。 <code>cluster</code>参数必须_匹配<code>turbine.aggregator.clusterConfig</code>中的条目。从 eureka 返回的值是大写的，因此如果在 Eureka 中注册了一个名为“customers”的应用程序，我们希望这个 example 能够正常工作：</p>
<pre><code class="language-">turbine:
  aggregator:
    clusterConfig: CUSTOMERS
  appConfig: customers
</code></pre>
<p>如果需要自定义 Turbine 应使用哪些 cluster 名称(您不希望在<code>turbine.aggregator.clusterConfig</code> configuration 中 store cluster 名称)，请提供<code>TurbineClustersProvider</code>类型的 bean。</p>
<p><code>clusterName</code>可以通过<code>turbine.clusterNameExpression</code>中的 SPEL 表达式自定义，其根目录是<code>InstanceInfo</code>的实例。默认的 value 是<code>appName</code>，这意味着 Eureka serviceId _end up 为 cluster key(i.e.<code>InstanceInfo</code> for customers 的<code>appName</code>为“CUSTOMERS”)。另一个 example 将是<code>turbine.clusterNameExpression=aSGName</code>，它将从 AWS ASG name 获取 cluster name。另一个例子：</p>
<pre><code class="language-">turbine:
  aggregator:
    clusterConfig: SYSTEM,USER
  appConfig: customers,stores,ui,admin
  clusterNameExpression: metadata['cluster']
</code></pre>
<p>在这种情况下，来自 4 个服务的 cluster name 是从其元数据 map 中提取的，并且应该具有包含“SYSTEM”和“USER”的值。</p>
<p>要为所有应用程序使用“默认”cluster，您需要 string 文字表达式(带单引号，如果它也在 YAML 中，则使用 double 引号进行转义)：</p>
<pre><code class="language-">turbine:
  appConfig: customers,stores
  clusterNameExpression: "'default'"
</code></pre>
<p>Spring Cloud 提供<code>spring-cloud-starter-netflix-turbine</code>，它具有获取 Turbine 服务器 running 所需的所有依赖项。只需创建一个 Spring Boot application 并使用<code>@EnableTurbine</code>注释它。</p>
<blockquote><p>默认情况下 Spring Cloud 允许 Turbine 使用 host 和 port 允许每个 host，每个 cluster 允许多个进程。如果您希望 Turbine 中内置的本机 Netflix 行为不允许每个 host 的多个进程，每个 cluster(实例 id 的 key 是主机名)，则设置 property <code>turbine.combineHostPort=false</code>。</p>
</blockquote>
<h2 id="turbine-stream"><a href="#_turbine_stream" id="_turbine_stream"></a> 15.3 Turbine Stream</h2>
<p>在某些环境中(在 PaaS 设置中为 e.g. )，从所有分布式 Hystrix 命令中提取 metrics 的经典 Turbine model 不起作用。在这种情况下，您可能希望让 Hystrix 命令将 metrics 推送到 Turbine，而 Spring Cloud 可以通过消息传递启用它。您只需要在 client 上添加一个依赖项<code>spring-cloud-netflix-hystrix-stream</code>和您选择的<code>spring-cloud-starter-stream-*</code>(有关代理的详细信息，请参阅 Spring Cloud Stream 文档，以及如何配置 client 凭据，但它应该是开箱即用的当地经纪人)。</p>
<p>在服务器端只需创建一个 Spring Boot application 并使用<code>@EnableTurbineStream</code>注释它，默认情况下它将出现在 port 8989 上(将 Hystrix 仪表板指向该 port，任何路径)。您可以使用<code>server.port</code>或<code>turbine.stream.port</code>自定义 port。如果 classpath 上也有<code>spring-boot-starter-web</code>和<code>spring-boot-starter-actuator</code>，则可以通过提供不同的<code>management.port</code>在单独的 port(默认情况下为 Tomcat)上打开 Actuator endpoints。</p>
<p>然后，您可以将 Hystrix 仪表板指向 Turbine Stream Server 而不是单个 Hystrix 流。如果 Turbine Stream 在 myhost 上 port 8989 上运行，则将<code>http://myhost:8989</code>放在 Hystrix 仪表板的流输入字段中。电路将以各自的 serviceId 为前缀，后跟一个点，然后是电路 name。</p>
<p>Spring Cloud 提供<code>spring-cloud-starter-netflix-turbine-stream</code>，它具有获取 Turbine Stream 服务器所需的所有依赖项运行 - 只需添加您选择的 Stream binder，e.g. <code>spring-cloud-starter-stream-rabbit</code>。你需要 Java 8 来运行应用程序，因为它是 Netty-based。</p>
<p>Turbine Stream 服务器还支持<code>cluster</code>参数。与 Turbine 服务器不同，Turbine Stream 使用 eureka serviceIds 作为 cluster 名称，这些不可配置。</p>
<p>如果 Turbine Stream 服务器在<code>my.turbine.server</code>上 port 8989 上运行并且您的环境中有两个 eureka serviceIds <code>customers</code>和<code>products</code>，则 Turbine Stream 服务器上将提供以下 URL。 <code>default</code>和空 cluster name 将提供 Turbine Stream 服务器接收的所有 metrics。</p>
<pre><code class="language-">http://my.turbine.sever:8989/turbine.stream?cluster=customers
http://my.turbine.sever:8989/turbine.stream?cluster=products
http://my.turbine.sever:8989/turbine.stream?cluster=default
http://my.turbine.sever:8989/turbine.stream
</code></pre>
<p>因此，您可以将 eureka serviceIds 用作 Turbine 仪表板(或任何兼容的仪表板)的 cluster 名称。您不需要为 Turbine Stream 服务器配置<code>turbine.appConfig</code>，<code>turbine.clusterNameExpression</code>和<code>turbine.aggregator.clusterConfig</code>等任何 properties。</p>
<blockquote><p>Turbine Stream 服务器使用 Spring Cloud Stream 从配置的输入 channel 收集所有 metrics。这意味着它不会从每个实例主动收集 Hystrix metrics。它只能提供已经由每个实例收集到输入 channel 中的 metrics。</p>
</blockquote>
</div>
</div>
</section>
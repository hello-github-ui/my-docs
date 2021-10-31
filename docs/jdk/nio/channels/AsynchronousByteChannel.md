<div class="contentContainer"> 
   <div class="description"> 
    <ul class="blockList"> 
     <li class="blockList"> 
      <dl> 
       <dt>
         All Superinterfaces: 
       </dt> 
       <dd> 
        <span><a href="../../../java/nio/channels/AsynchronousChannel.html" title="java.nio.channels中的接口">AsynchronousChannel</a> ， <a href="../../../java/lang/AutoCloseable.html" title="java.lang中的接口">AutoCloseable</a> ， <a href="../../../java/nio/channels/Channel.html" title="java.nio.channels中的接口">Channel</a> ， <a href="../../../java/io/Closeable.html" title="java.io中的接口">Closeable</a></span> 
       </dd> 
      </dl> 
      <dl> 
       <dt>
        所有已知实现类：
       </dt> 
       <dd> 
        <span><a href="../../../java/nio/channels/AsynchronousSocketChannel.html" title="java.nio.channels中的类">AsynchronousSocketChannel</a></span> 
       </dd> 
      </dl> 
      <hr> <br> <pre>public interface <span class="typeNameLabel">AsynchronousByteChannel</span>
extends <a href="../../../java/nio/channels/AsynchronousChannel.html" title="interface in java.nio.channels">AsynchronousChannel</a></pre> 
      <div class="block"> 
       <span>一个可以读写字节的异步通道。</span> 
       <p> <span>某些频道在任何给定的时间可能不允许多于一个读或写。</span> <span>如果线程在先前的读取操作完成之前调用读取方法，那么将抛出一个<a href="../../../java/nio/channels/ReadPendingException.html" title="java.nio.channels中的类"><code>ReadPendingException</code></a> 。</span> <span>类似地，如果在先前写入完成之前调用了写入方法，则抛出<a href="../../../java/nio/channels/WritePendingException.html" title="java.nio.channels中的类"><code>WritePendingException</code></a> 。</span> <span>其他类型的I / O操作是否可以与读取操作同时进行取决于通道的类型。</span> </p> 
       <p> <span>请注意， <a href="../../../java/nio/ByteBuffer.html" title="java.nio中的类"><code>ByteBuffers</code></a>对于多个并发线程不能使用。</span> <span>当启动读或写操作时，必须注意确保在操作完成之前不访问缓冲区。</span> </p> 
      </div> 
      <dl> 
       <dt> 
        <span class="simpleTagLabel">从以下版本开始：</span> 
       </dt> 
       <dd>
         1.7 
       </dd> 
       <dt> 
        <span class="seeLabel">另请参见：</span> 
       </dt> 
       <dd> 
        <a href="../../../java/nio/channels/Channels.html#newInputStream-java.nio.channels.AsynchronousByteChannel-"><code>Channels.newInputStream(AsynchronousByteChannel)</code></a> ， 
        <a href="../../../java/nio/channels/Channels.html#newOutputStream-java.nio.channels.AsynchronousByteChannel-"><code>Channels.newOutputStream(AsynchronousByteChannel)</code></a> 
       </dd> 
      </dl> </li> 
    </ul> 
   </div> 
   <div class="summary"> 
    <ul class="blockList"> 
     <li class="blockList"> 
      <!-- ========== METHOD SUMMARY =========== --> 
      <ul class="blockList"> 
       <li class="blockList"><a name="method.summary"> 
         <!--   --> </a> <h3>方法摘要</h3> 
        <table class="memberSummary" border="0" cellpadding="3" cellspacing="0" summary="Method Summary table, listing methods, and an explanation"> 
         <caption> 
          <span id="t0" class="activeTableTab"><span>所有方法</span><span class="tabEnd">&nbsp;</span></span> 
          <span id="t2" class="tableTab"><span><a href="javascript:show(2);">接口方法</a></span><span class="tabEnd">&nbsp;</span></span> 
          <span id="t3" class="tableTab"><span><a href="javascript:show(4);">抽象方法</a></span><span class="tabEnd">&nbsp;</span></span> 
         </caption> 
         <tbody> 
          <tr> 
           <th class="colFirst" scope="col">Modifier and Type</th> 
           <th class="colLast" scope="col">Method and Description</th> 
          </tr> 
          <tr id="i0" class="altColor"> 
           <td class="colFirst"><code><a href="../../../java/util/concurrent/Future.html" title="interface in java.util.concurrent">Future</a>&lt;<a href="../../../java/lang/Integer.html" title="class in java.lang">Integer</a>&gt;</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../../java/nio/channels/AsynchronousByteChannel.html#read-java.nio.ByteBuffer-">read</a></span>(<a href="../../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;dst)</code> 
            <div class="block">
              从该通道读取到给定缓冲区的字节序列。 
            </div> </td> 
          </tr> 
          <tr id="i1" class="rowColor"> 
           <td class="colFirst"><code>&lt;A&gt;&nbsp;void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../../java/nio/channels/AsynchronousByteChannel.html#read-java.nio.ByteBuffer-A-java.nio.channels.CompletionHandler-">read</a></span>(<a href="../../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;dst, A&nbsp;attachment, <a href="../../../java/nio/channels/CompletionHandler.html" title="interface in java.nio.channels">CompletionHandler</a>&lt;<a href="../../../java/lang/Integer.html" title="class in java.lang">Integer</a>,? super A&gt;&nbsp;handler)</code> 
            <div class="block">
              从该通道读取到给定缓冲区的字节序列。 
            </div> </td> 
          </tr> 
          <tr id="i2" class="altColor"> 
           <td class="colFirst"><code><a href="../../../java/util/concurrent/Future.html" title="interface in java.util.concurrent">Future</a>&lt;<a href="../../../java/lang/Integer.html" title="class in java.lang">Integer</a>&gt;</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../../java/nio/channels/AsynchronousByteChannel.html#write-java.nio.ByteBuffer-">write</a></span>(<a href="../../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;src)</code> 
            <div class="block">
              从给定的缓冲区向该通道写入一个字节序列。 
            </div> </td> 
          </tr> 
          <tr id="i3" class="rowColor"> 
           <td class="colFirst"><code>&lt;A&gt;&nbsp;void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../../java/nio/channels/AsynchronousByteChannel.html#write-java.nio.ByteBuffer-A-java.nio.channels.CompletionHandler-">write</a></span>(<a href="../../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;src, A&nbsp;attachment, <a href="../../../java/nio/channels/CompletionHandler.html" title="interface in java.nio.channels">CompletionHandler</a>&lt;<a href="../../../java/lang/Integer.html" title="class in java.lang">Integer</a>,? super A&gt;&nbsp;handler)</code> 
            <div class="block">
              从给定的缓冲区向该通道写入一个字节序列。 
            </div> </td> 
          </tr> 
         </tbody> 
        </table> 
        <ul class="blockList"> 
         <li class="blockList"><a name="methods.inherited.from.class.java.nio.channels.AsynchronousChannel"> 
           <!--   --> </a> <h3>Methods inherited from interface&nbsp;java.nio.channels.<a href="../../../java/nio/channels/AsynchronousChannel.html" title="interface in java.nio.channels">AsynchronousChannel</a></h3> <code><a href="../../../java/nio/channels/AsynchronousChannel.html#close--">close</a></code></li> 
        </ul> 
        <ul class="blockList"> 
         <li class="blockList"><a name="methods.inherited.from.class.java.nio.channels.Channel"> 
           <!--   --> </a> <h3>Methods inherited from interface&nbsp;java.nio.channels.<a href="../../../java/nio/channels/Channel.html" title="interface in java.nio.channels">Channel</a></h3> <code><a href="../../../java/nio/channels/Channel.html#isOpen--">isOpen</a></code></li> 
        </ul> </li> 
      </ul> </li> 
    </ul> 
   </div> 
   <div class="details"> 
    <ul class="blockList"> 
     <li class="blockList"> 
      <!-- ============ METHOD DETAIL ========== --> 
      <ul class="blockList"> 
       <li class="blockList"><a name="method.detail"> 
         <!--   --> </a> <h3>方法详细信息</h3> <a name="read-java.nio.ByteBuffer-java.lang.Object-java.nio.channels.CompletionHandler-"> 
         <!--   --> </a><a name="read-java.nio.ByteBuffer-A-java.nio.channels.CompletionHandler-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>read</h4> <pre>&lt;A&gt;&nbsp;void&nbsp;read(<a href="../../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;dst,
              A&nbsp;attachment,
              <a href="../../../java/nio/channels/CompletionHandler.html" title="interface in java.nio.channels">CompletionHandler</a>&lt;<a href="../../../java/lang/Integer.html" title="class in java.lang">Integer</a>,? super A&gt;&nbsp;handler)</pre> 
          <div class="block"> 
           <span>从该通道读取到给定缓冲区的字节序列。</span> 
           <p> <span>该方法启动异步读取操作，以从该通道读取到给定缓冲器中的字节序列。</span> <span><code>handler</code>参数是在读取操作完成（或失败）时调用的完成处理程序。</span> <span>传递给完成处理程序的结果是读取的字节数或<code>-1</code>如果由于通道已达到流出端，则不能读取字节。</span> </p> 
           <p> <span>读取操作可以从通道读取<i>r</i>个字节，其中<i>r</i>是缓冲器中剩余的字节数，即在<code>dst.remaining()</code>读取时为dst.remaining()。</span> <span>其中<i>r</i>为0，读操作立即完成，结果为<code>0</code>而不启动I / O操作。</span> </p> 
           <p> <span>假设读取长度为<i>n</i>的字节序列，其中<tt>88416675767076</tt> <tt>&lt;</tt> <i>n</i> <tt>&lt;=</tt> <i>r</i> 。</span> <span>该字节序列将被传送到缓冲器中，使序列中的第一个字节处于索引<i>p</i> ，最后一个字节处于索引<i>p</i> <tt>+</tt> <i>n</i> <tt>-</tt> <tt>1</tt> ，其中<i>p</i>是执行读取时缓冲区的位置。</span> <span>完成后，缓冲区的位置将等于<i>p</i> <tt>+</tt> <i>n</i> ;</span> <span>其限制将不会改变。</span> </p> 
           <p> <span>缓冲区不能安全地被多个并发线程使用，因此在操作完成之前，请注意不要访问缓冲区。</span> </p> 
           <p> <span>可以随时调用此方法。</span> <span>某些渠道类型在任何给定时间可能不允许多于一个读取。</span> <span>如果线程在先前的读取操作完成之前启动了读取操作，那么将抛出一个<a href="../../../java/nio/channels/ReadPendingException.html" title="java.nio.channels中的类"><code>ReadPendingException</code></a> 。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数类型</span> 
           </dt> 
           <dd> 
            <code>A</code> - 
            <code>A</code>的类型 
           </dd> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>dst</code> - 要传输字节的缓冲区 
           </dd> 
           <dd> 
            <span><code>attachment</code> - 要附加到I / O操作的对象;</span> 
            <span>可以是<code>null</code></span> 
           </dd> 
           <dd> 
            <code>handler</code> - 完成处理程序 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../../java/lang/IllegalArgumentException.html" title="class in java.lang">IllegalArgumentException</a></code> - 如果缓冲区是只读的 
           </dd> 
           <dd> 
            <code><a href="../../../java/nio/channels/ReadPendingException.html" title="class in java.nio.channels">ReadPendingException</a></code> - 如果通道不允许多于一个读取未完成，并且以前的读取尚未完成 
           </dd> 
           <dd> 
            <span><code><a href="../../../java/nio/channels/ShutdownChannelGroupException.html" title="class in java.nio.channels">ShutdownChannelGroupException</a></code> -如果信道与相关联<a href="../../../java/nio/channels/AsynchronousChannelGroup.html" title="java.nio.channels中的类"><code>group</code></a>已终止</span> 
           </dd> 
          </dl> </li> 
        </ul> <a name="read-java.nio.ByteBuffer-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>read</h4> <pre><a href="../../../java/util/concurrent/Future.html" title="interface in java.util.concurrent">Future</a>&lt;<a href="../../../java/lang/Integer.html" title="class in java.lang">Integer</a>&gt;&nbsp;read(<a href="../../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;dst)</pre> 
          <div class="block"> 
           <span>从该通道读取到给定缓冲区的字节序列。</span> 
           <p> <span>该方法启动异步读取操作，以从该通道读取到给定缓冲器中的字节序列。</span> <span>该方法的行为方式与<a href="../../../java/nio/channels/AsynchronousByteChannel.html#read-java.nio.ByteBuffer-A-java.nio.channels.CompletionHandler-"><code>read(ByteBuffer,Object,CompletionHandler)</code></a>方法完全相同，不同之处在于，该方法不是指定完成处理程序，而是返回一个<code>Future</code>待处理结果的<code>Future</code> 。</span> <span><code>Future</code>的<a href="../../../java/util/concurrent/Future.html#get--"><code>get</code></a>方法返回读取的字节数或<code>-1</code>如果没有字节可以读取，因为通道已经达到流终止。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>dst</code> - 要传输字节的缓冲区 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             代表操作结果的未来 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../../java/lang/IllegalArgumentException.html" title="class in java.lang">IllegalArgumentException</a></code> - 如果缓冲区是只读的 
           </dd> 
           <dd> 
            <code><a href="../../../java/nio/channels/ReadPendingException.html" title="class in java.nio.channels">ReadPendingException</a></code> - 如果通道不允许多个读取未完成，并且以前的读取尚未完成 
           </dd> 
          </dl> </li> 
        </ul> <a name="write-java.nio.ByteBuffer-java.lang.Object-java.nio.channels.CompletionHandler-"> 
         <!--   --> </a><a name="write-java.nio.ByteBuffer-A-java.nio.channels.CompletionHandler-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>write</h4> <pre>&lt;A&gt;&nbsp;void&nbsp;write(<a href="../../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;src,
               A&nbsp;attachment,
               <a href="../../../java/nio/channels/CompletionHandler.html" title="interface in java.nio.channels">CompletionHandler</a>&lt;<a href="../../../java/lang/Integer.html" title="class in java.lang">Integer</a>,? super A&gt;&nbsp;handler)</pre> 
          <div class="block"> 
           <span>从给定的缓冲区向该通道写入一个字节序列。</span> 
           <p> <span>该方法启动异步写入操作，以从给定的缓冲区向该通道写入字节序列。</span> <span><code>handler</code>参数是在写操作完成（或失败）时调用的完成处理程序。</span> <span>传递给完成处理程序的结果是写入的字节数。</span> </p> 
           <p> <span>写入操作可以写入<i>r</i>字节到通道，其中<i>r</i>是缓冲区中剩余的字节数，即在<code>src.remaining()</code>写入时为src.remaining()。</span> <span>其中<i>r</i>为0，写操作立即完成，结果为<code>0</code>而不启动I / O操作。</span> </p> 
           <p> <span>假设写入长度为<i>n</i>的字节序列，其中<tt>0</tt> <tt>&lt;</tt> <i>n</i> <tt>&lt;=</tt> <i>r</i> 。</span> <span>该字节序列将从索引<i>p</i>开始从缓冲区传送，其中<i>p</i>是执行写入时的缓冲区的位置;</span> <span>写入的最后一个字节的索引将为<i>p</i> <tt>+</tt> <i>n</i> <tt>-</tt> <tt>1</tt> 。</span> <span>完成后，缓冲区的位置将等于<i>p</i> <tt>+</tt> <i>n</i> ;</span> <span>其限制将不会改变。</span> </p> 
           <p> <span>缓冲区不能安全地被多个并发线程使用，因此在操作完成之前，请注意不要访问缓冲区。</span> </p> 
           <p> <span>可以随时调用此方法。</span> <span>某些频道类型可能不允许在任何给定时间多出一个写入。</span> <span>如果线程在先前写入操作完成之前启动写入操作，则会抛出<a href="../../../java/nio/channels/WritePendingException.html" title="java.nio.channels中的类"><code>WritePendingException</code></a> 。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数类型</span> 
           </dt> 
           <dd> 
            <code>A</code> - 
            <code>A</code>的类型 
           </dd> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>src</code> - 要检索字节的缓冲区 
           </dd> 
           <dd> 
            <span><code>attachment</code> - 要附加到I / O操作的对象;</span> 
            <span>可以是<code>null</code></span> 
           </dd> 
           <dd> 
            <code>handler</code> - 完成处理程序对象 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../../java/nio/channels/WritePendingException.html" title="class in java.nio.channels">WritePendingException</a></code> - 如果通道不允许多个写入未完成，并且以前的写入尚未完成 
           </dd> 
           <dd> 
            <span><code><a href="../../../java/nio/channels/ShutdownChannelGroupException.html" title="class in java.nio.channels">ShutdownChannelGroupException</a></code> -如果信道与相关联<a href="../../../java/nio/channels/AsynchronousChannelGroup.html" title="java.nio.channels中的类"><code>group</code></a>已终止</span> 
           </dd> 
          </dl> </li> 
        </ul> <a name="write-java.nio.ByteBuffer-"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>write</h4> <pre><a href="../../../java/util/concurrent/Future.html" title="interface in java.util.concurrent">Future</a>&lt;<a href="../../../java/lang/Integer.html" title="class in java.lang">Integer</a>&gt;&nbsp;write(<a href="../../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;src)</pre> 
          <div class="block"> 
           <span>从给定的缓冲区向该通道写入一个字节序列。</span> 
           <p> <span>该方法启动异步写入操作，以从给定的缓冲区向该通道写入字节序列。</span> <span>该方法的行为方式与<a href="../../../java/nio/channels/AsynchronousByteChannel.html#write-java.nio.ByteBuffer-A-java.nio.channels.CompletionHandler-"><code>write(ByteBuffer,Object,CompletionHandler)</code></a>方法完全相同，不同的是，该方法不是指定完成处理程序，而是返回一个<code>Future</code>待处理结果的<code>Future</code> 。</span> <span><code>Future</code>的<a href="../../../java/util/concurrent/Future.html#get--"><code>get</code></a>方法返回写入的字节数。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>src</code> - 要检索字节的缓冲区 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             代表操作结果的未来 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../../java/nio/channels/WritePendingException.html" title="class in java.nio.channels">WritePendingException</a></code> - 如果通道不允许多个写入未完成，并且以前的写入尚未完成 
           </dd> 
          </dl> </li> 
        </ul> </li> 
      </ul> </li> 
    </ul> 
   </div> 
  </div>
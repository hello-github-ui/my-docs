<div class="contentContainer"> 
   <div class="description"> 
    <ul class="blockList"> 
     <li class="blockList"> 
      <dl> 
       <dt>
         All Superinterfaces: 
       </dt> 
       <dd> 
        <span><a href="../../../java/lang/AutoCloseable.html" title="java.lang中的接口">AutoCloseable</a> ， <a href="../../../java/nio/channels/Channel.html" title="java.nio.channels中的接口">Channel</a> ， <a href="../../../java/io/Closeable.html" title="java.io中的接口">Closeable</a> ， <a href="../../../java/nio/channels/WritableByteChannel.html" title="java.nio.channels中的接口">WritableByteChannel</a></span> 
       </dd> 
      </dl> 
      <dl> 
       <dt>
        所有已知实现类：
       </dt> 
       <dd> 
        <span><a href="../../../java/nio/channels/DatagramChannel.html" title="java.nio.channels中的类">DatagramChannel</a> ， <a href="../../../java/nio/channels/FileChannel.html" title="java.nio.channels中的类">FileChannel</a> ， <a href="../../../java/nio/channels/Pipe.SinkChannel.html" title="java.nio.channels中的类">Pipe.SinkChannel</a> ， <a href="../../../java/nio/channels/SocketChannel.html" title="java.nio.channels中的类">SocketChannel</a></span> 
       </dd> 
      </dl> 
      <hr> <br> <pre>public interface <span class="typeNameLabel">GatheringByteChannel</span>
extends <a href="../../../java/nio/channels/WritableByteChannel.html" title="interface in java.nio.channels">WritableByteChannel</a></pre> 
      <div class="block"> 
       <span>可以从缓冲区序列中写入字节的通道。</span> 
       <p> <span><i>采集</i>写入操作在单个调用中写入一个或多个缓冲器序列中的一个或多个字节序列。</span> <span>在实现网络协议或文件格式时，收集写入通常很有用，例如，将数据分组到由一个或多个固定长度的标题后跟可变长度的主体组成的段中。</span> <span>类似的<i>散射</i>读操作都在定义<a href="../../../java/nio/channels/ScatteringByteChannel.html" title="java.nio.channels中的接口"><code>ScatteringByteChannel</code></a>接口。</span> </p> 
      </div> 
      <dl> 
       <dt> 
        <span class="simpleTagLabel">从以下版本开始：</span> 
       </dt> 
       <dd>
         1.4 
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
           <td class="colFirst"><code>long</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../../java/nio/channels/GatheringByteChannel.html#write-java.nio.ByteBuffer:A-">write</a></span>(<a href="../../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>[]&nbsp;srcs)</code> 
            <div class="block">
              从给定的缓冲区向该通道写入一系列字节。 
            </div> </td> 
          </tr> 
          <tr id="i1" class="rowColor"> 
           <td class="colFirst"><code>long</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../../java/nio/channels/GatheringByteChannel.html#write-java.nio.ByteBuffer:A-int-int-">write</a></span>(<a href="../../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>[]&nbsp;srcs, int&nbsp;offset, int&nbsp;length)</code> 
            <div class="block">
              从给定缓冲区的子序列将一个字节序列写入该通道。 
            </div> </td> 
          </tr> 
         </tbody> 
        </table> 
        <ul class="blockList"> 
         <li class="blockList"><a name="methods.inherited.from.class.java.nio.channels.WritableByteChannel"> 
           <!--   --> </a> <h3>Methods inherited from interface&nbsp;java.nio.channels.<a href="../../../java/nio/channels/WritableByteChannel.html" title="interface in java.nio.channels">WritableByteChannel</a></h3> <code><a href="../../../java/nio/channels/WritableByteChannel.html#write-java.nio.ByteBuffer-">write</a></code></li> 
        </ul> 
        <ul class="blockList"> 
         <li class="blockList"><a name="methods.inherited.from.class.java.nio.channels.Channel"> 
           <!--   --> </a> <h3>Methods inherited from interface&nbsp;java.nio.channels.<a href="../../../java/nio/channels/Channel.html" title="interface in java.nio.channels">Channel</a></h3> <code><a href="../../../java/nio/channels/Channel.html#close--">close</a>, <a href="../../../java/nio/channels/Channel.html#isOpen--">isOpen</a></code></li> 
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
         <!--   --> </a> <h3>方法详细信息</h3> <a name="write-java.nio.ByteBuffer:A-int-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>write</h4> <pre>long&nbsp;write(<a href="../../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>[]&nbsp;srcs,
           int&nbsp;offset,
           int&nbsp;length)
    throws <a href="../../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>从给定缓冲区的子序列将一个字节序列写入该通道。</span> 
           <p> <span>尝试写入<i>r</i>个字节到该通道，其中<i>r</i>是给定缓冲区数组的指定子序列中剩余的总字节数，也就是说，</span> </p> 
           <blockquote> 
            <span><pre> srcs[offset].remaining()
     + srcs[offset+1].remaining()
     + ... + srcs[offset+length-1].remaining()</pre></span> 
           </blockquote> 
           <span>在此方法被调用的时刻。</span> 
           <p> <span>假设写入长度为<i>n</i>的字节序列，其中<tt>0</tt> <tt>&lt;=</tt> <i>n</i> <tt>&lt;=</tt> <i>r</i> 。</span> <span>直到该序列的第一个<tt>srcs[offset].remaining()</tt>字节从缓冲器<tt>srcs[offset]</tt>写入，直到下一个<tt>srcs[offset+1].remaining()</tt>字节从缓冲器<tt>srcs[offset+1]</tt>写入，等等，直到写入整个字节序列。</span> <span>尽可能多的字节从每个缓冲区写入，因此除了最后更新的缓冲区之外，每个更新的缓冲区的最终位置被保证等于该缓冲区的限制。</span> </p> 
           <p> <span>除非另有规定，写入操作将仅在写入所有<i>r个</i>请求的字节后才会返回。</span> <span>某些类型的通道取决于它们的状态，可能仅写入一些字节，或者可能只写入一些字节。</span> <span>例如，在非阻塞模式下的套接字通道不能再写入比套接字输出缓冲区中的任何字节更多的字节。</span> </p> 
           <p> <span>可以随时调用此方法。</span> <span>但是，如果另一个线程已经在该通道上启动了写入操作，那么此方法的调用将阻塞，直到第一个操作完成。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>srcs</code> - 要检索字节的缓冲区 
           </dd> 
           <dd> 
            <span><code>offset</code> - 要检索字节的第一个缓冲区的缓冲区中的偏移量;</span> 
            <span>必须是非负数，不得大于<tt>srcs.length</tt></span> 
           </dd> 
           <dd> 
            <span><code>length</code> - 要访问的最大缓冲区数;</span> 
            <span>必须是非负数，不得大于<tt>srcs.length</tt> - <tt>offset</tt></span> 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             写入的字节数，可能为零 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../../java/lang/IndexOutOfBoundsException.html" title="class in java.lang">IndexOutOfBoundsException</a></code> - 如果 
            <tt>offset</tt>和 
            <tt>length</tt>参数的前提条件不成立 
           </dd> 
           <dd> 
            <code><a href="../../../java/nio/channels/NonWritableChannelException.html" title="class in java.nio.channels">NonWritableChannelException</a></code> - 如果这个频道没有开放写作 
           </dd> 
           <dd> 
            <code><a href="../../../java/nio/channels/ClosedChannelException.html" title="class in java.nio.channels">ClosedChannelException</a></code> - 如果此通道关闭 
           </dd> 
           <dd> 
            <code><a href="../../../java/nio/channels/AsynchronousCloseException.html" title="class in java.nio.channels">AsynchronousCloseException</a></code> - 如果另一个线程在写操作正在进行时关闭此通道 
           </dd> 
           <dd> 
            <code><a href="../../../java/nio/channels/ClosedByInterruptException.html" title="class in java.nio.channels">ClosedByInterruptException</a></code> - 如果另一个线程在写操作正在进行时中断当前线程，从而关闭通道并设置当前线程的中断状态 
           </dd> 
           <dd> 
            <code><a href="../../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生其他I / O错误 
           </dd> 
          </dl> </li> 
        </ul> <a name="write-java.nio.ByteBuffer:A-"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>write</h4> <pre>long&nbsp;write(<a href="../../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>[]&nbsp;srcs)
    throws <a href="../../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>从给定的缓冲区向该通道写入一系列字节。</span> 
           <p> <span>调用此方法的形式为<tt>c.write(srcs)的</tt>行为方式与调用完全相同</span> </p> 
           <blockquote> 
            <span><pre> c.write(srcs, 0, srcs.length);</pre></span> 
           </blockquote> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>srcs</code> - 要检索字节的缓冲区 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             写入的字节数，可能为零 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../../java/nio/channels/NonWritableChannelException.html" title="class in java.nio.channels">NonWritableChannelException</a></code> - 如果这个频道没有开放写作 
           </dd> 
           <dd> 
            <code><a href="../../../java/nio/channels/ClosedChannelException.html" title="class in java.nio.channels">ClosedChannelException</a></code> - 如果此频道关闭 
           </dd> 
           <dd> 
            <code><a href="../../../java/nio/channels/AsynchronousCloseException.html" title="class in java.nio.channels">AsynchronousCloseException</a></code> - 如果另一个线程在写操作正在进行时关闭此通道 
           </dd> 
           <dd> 
            <code><a href="../../../java/nio/channels/ClosedByInterruptException.html" title="class in java.nio.channels">ClosedByInterruptException</a></code> - 如果另一个线程在写操作正在进行时中断当前线程，从而关闭通道并设置当前线程的中断状态 
           </dd> 
           <dd> 
            <code><a href="../../../java/io/IOException.html" title="class in java.io">IOException</a></code> - If some other I/O error occurs 
           </dd> 
          </dl> </li> 
        </ul> </li> 
      </ul> </li> 
    </ul> 
   </div> 
  </div>
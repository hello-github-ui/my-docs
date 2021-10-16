<div class="contentContainer"> 
   <div class="description"> 
    <ul class="blockList"> 
     <li class="blockList"> 
      <dl> 
       <dt>
         All Superinterfaces: 
       </dt> 
       <dd> 
        <span><a href="../../../java/lang/AutoCloseable.html" title="java.lang中的接口">AutoCloseable</a> ， <a href="../../../java/io/Closeable.html" title="java.io中的接口">Closeable</a></span> 
       </dd> 
      </dl> 
      <dl> 
       <dt>
         All Known Subinterfaces: 
       </dt> 
       <dd> 
        <span><a href="../../../java/nio/channels/AsynchronousByteChannel.html" title="java.nio.channels中的接口">AsynchronousByteChannel</a> ， <a href="../../../java/nio/channels/AsynchronousChannel.html" title="java.nio.channels中的接口">AsynchronousChannel</a> ， <a href="../../../java/nio/channels/ByteChannel.html" title="java.nio.channels中的接口">ByteChannel</a> ， <a href="../../../java/nio/channels/GatheringByteChannel.html" title="java.nio.channels中的接口">GatheringByteChannel</a> ， <a href="../../../java/nio/channels/InterruptibleChannel.html" title="java.nio.channels中的接口">InterruptibleChannel</a> ， <a href="../../../java/nio/channels/MulticastChannel.html" title="java.nio.channels中的接口">MulticastChannel</a> ， <a href="../../../java/nio/channels/NetworkChannel.html" title="java.nio.channels中的接口">NetworkChannel</a> ， <a href="../../../java/nio/channels/ReadableByteChannel.html" title="java.nio.channels中的接口">ReadableByteChannel</a> ， <a href="../../../java/nio/channels/ScatteringByteChannel.html" title="java.nio.channels中的接口">ScatteringByteChannel</a> ， <a href="../../../java/nio/channels/SeekableByteChannel.html" title="java.nio.channels中的接口">SeekableByteChannel</a> ， <a href="../../../java/nio/channels/WritableByteChannel.html" title="java.nio.channels中的接口">WritableByteChannel</a></span> 
       </dd> 
      </dl> 
      <dl> 
       <dt>
        所有已知实现类：
       </dt> 
       <dd> 
        <span><a href="../../../java/nio/channels/spi/AbstractInterruptibleChannel.html" title="java.nio.channels.spi中的类">AbstractInterruptibleChannel</a> ， <a href="../../../java/nio/channels/spi/AbstractSelectableChannel.html" title="java.nio.channels.spi中的类">AbstractSelectableChannel</a> ， <a href="../../../java/nio/channels/AsynchronousFileChannel.html" title="java.nio.channels中的类">AsynchronousFileChannel</a> ， <a href="../../../java/nio/channels/AsynchronousServerSocketChannel.html" title="java.nio.channels中的类">AsynchronousServerSocketChannel</a> ， <a href="../../../java/nio/channels/AsynchronousSocketChannel.html" title="java.nio.channels中的类">AsynchronousSocketChannel</a> ， <a href="../../../java/nio/channels/DatagramChannel.html" title="java.nio.channels中的类">DatagramChannel</a> ， <a href="../../../java/nio/channels/FileChannel.html" title="java.nio.channels中的类">FileChannel</a> ， <a href="../../../java/nio/channels/Pipe.SinkChannel.html" title="java.nio.channels中的类">Pipe.SinkChannel</a> ， <a href="../../../java/nio/channels/Pipe.SourceChannel.html" title="java.nio.channels中的类">Pipe.SourceChannel</a> ， <a href="../../../java/nio/channels/SelectableChannel.html" title="java.nio.channels中的类">SelectableChannel</a> ， <a href="../../../java/nio/channels/ServerSocketChannel.html" title="java.nio.channels中的类">ServerSocketChannel</a> ， <a href="../../../java/nio/channels/SocketChannel.html" title="java.nio.channels中的类">SocketChannel</a></span> 
       </dd> 
      </dl> 
      <hr> <br> <pre>public interface <span class="typeNameLabel">Channel</span>
extends <a href="../../../java/io/Closeable.html" title="interface in java.io">Closeable</a></pre> 
      <div class="block"> 
       <span>I / O操作的联系。</span> 
       <p> <span>信道表示与诸如硬件设备，文件，网络套接字或能够执行一个或多个不同I / O操作（例如读取或写入）的程序组件的实体的开放连接。</span> </p> 
       <p> <span>通道是打开的还是关闭的。</span> <span>一个通道在创建时打开，一旦关闭，它仍然关闭。</span> <span>一旦通道关闭，任何尝试调用I / O操作将导致抛出<a href="../../../java/nio/channels/ClosedChannelException.html" title="java.nio.channels中的类"><code>ClosedChannelException</code></a> 。</span> <span>频道是否打开可以通过调用其<a href="../../../java/nio/channels/Channel.html#isOpen--"><code>isOpen</code></a>方法进行测试。</span> </p> 
       <p> <span>一般来说，通道旨在为多线程访问安全，如扩展和实现此接口的接口和类的规范中所述。</span> </p> 
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
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../../java/nio/channels/Channel.html#close--">close</a></span>()</code> 
            <div class="block">
              关闭此频道。 
            </div> </td> 
          </tr> 
          <tr id="i1" class="rowColor"> 
           <td class="colFirst"><code>boolean</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../../java/nio/channels/Channel.html#isOpen--">isOpen</a></span>()</code> 
            <div class="block">
              告诉这个频道是否开放。 
            </div> </td> 
          </tr> 
         </tbody> 
        </table> </li> 
      </ul> </li> 
    </ul> 
   </div> 
   <div class="details"> 
    <ul class="blockList"> 
     <li class="blockList"> 
      <!-- ============ METHOD DETAIL ========== --> 
      <ul class="blockList"> 
       <li class="blockList"><a name="method.detail"> 
         <!--   --> </a> <h3>方法详细信息</h3> <a name="isOpen--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>isOpen</h4> <pre>boolean&nbsp;isOpen()</pre> 
          <div class="block">
            告诉这个频道是否开放。 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd> 
            <tt>true</tt>如果，只有这个频道是开放的 
           </dd> 
          </dl> </li> 
        </ul> <a name="close--"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>close</h4> <pre>void&nbsp;close()
    throws <a href="../../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>关闭此频道。</span> 
           <p> <span>通道关闭后，进一步尝试调用I / O操作将导致抛出<a href="../../../java/nio/channels/ClosedChannelException.html" title="java.nio.channels中的类"><code>ClosedChannelException</code></a> 。</span> </p> 
           <p> <span>如果此通道已经关闭，则调用此方法不起作用。</span> </p> 
           <p> <span>可以随时调用此方法。</span> <span>然而，如果一些其他线程已经调用了它，那么另一个调用将阻塞，直到第一个调用完成，之后它将不起作用。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">Specified by:</span> 
           </dt> 
           <dd> 
            <code><a href="../../../java/lang/AutoCloseable.html#close--">close</a></code>中的 
            <code><a href="../../../java/lang/AutoCloseable.html" title="interface in java.lang">AutoCloseable</a></code> 
           </dd> 
           <dt> 
            <span class="overrideSpecifyLabel">Specified by:</span> 
           </dt> 
           <dd> 
            <code><a href="../../../java/io/Closeable.html#close--">close</a></code>在接口 
            <code><a href="../../../java/io/Closeable.html" title="interface in java.io">Closeable</a></code> 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../../java/io/IOException.html" title="class in java.io">IOException</a></code> - If an I/O error occurs 
           </dd> 
          </dl> </li> 
        </ul> </li> 
      </ul> </li> 
    </ul> 
   </div> 
  </div>
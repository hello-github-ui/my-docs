<div class="contentContainer"> 
   <div class="description"> 
    <ul class="blockList"> 
     <li class="blockList"> 
      <dl> 
       <dt>
         All Superinterfaces: 
       </dt> 
       <dd> 
        <span><a href="../../../java/lang/AutoCloseable.html" title="java.lang中的接口">AutoCloseable</a> ， <a href="../../../java/nio/channels/Channel.html" title="java.nio.channels中的接口">Channel</a> ， <a href="../../../java/io/Closeable.html" title="java.io中的接口">Closeable</a> ， <a href="../../../java/nio/channels/ReadableByteChannel.html" title="java.nio.channels中的接口">ReadableByteChannel</a> ， <a href="../../../java/nio/channels/WritableByteChannel.html" title="java.nio.channels中的接口">WritableByteChannel</a></span> 
       </dd> 
      </dl> 
      <dl> 
       <dt>
         All Known Subinterfaces: 
       </dt> 
       <dd> 
        <span><a href="../../../java/nio/channels/SeekableByteChannel.html" title="java.nio.channels中的接口">SeekableByteChannel</a></span> 
       </dd> 
      </dl> 
      <dl> 
       <dt>
        所有已知实现类：
       </dt> 
       <dd> 
        <span><a href="../../../java/nio/channels/DatagramChannel.html" title="java.nio.channels中的类">DatagramChannel</a> ， <a href="../../../java/nio/channels/FileChannel.html" title="java.nio.channels中的类">FileChannel</a> ， <a href="../../../java/nio/channels/SocketChannel.html" title="java.nio.channels中的类">SocketChannel</a></span> 
       </dd> 
      </dl> 
      <hr> <br> <pre>public interface <span class="typeNameLabel">ByteChannel</span>
extends <a href="../../../java/nio/channels/ReadableByteChannel.html" title="interface in java.nio.channels">ReadableByteChannel</a>, <a href="../../../java/nio/channels/WritableByteChannel.html" title="interface in java.nio.channels">WritableByteChannel</a></pre> 
      <div class="block"> 
       <span>一个可以读写字节的通道。</span> 
       <span>这个界面简单地统一了<a href="../../../java/nio/channels/ReadableByteChannel.html" title="java.nio.channels中的接口"><code>ReadableByteChannel</code></a>和<a href="../../../java/nio/channels/WritableByteChannel.html" title="java.nio.channels中的接口"><code>WritableByteChannel</code></a> ;</span> 
       <span>它没有指定任何新的操作。</span> 
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
        <ul class="blockList"> 
         <li class="blockList"><a name="methods.inherited.from.class.java.nio.channels.ReadableByteChannel"> 
           <!--   --> </a> <h3>Methods inherited from interface&nbsp;java.nio.channels.<a href="../../../java/nio/channels/ReadableByteChannel.html" title="interface in java.nio.channels">ReadableByteChannel</a></h3> <code><a href="../../../java/nio/channels/ReadableByteChannel.html#read-java.nio.ByteBuffer-">read</a></code></li> 
        </ul> 
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
  </div>
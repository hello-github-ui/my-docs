<div class="contentContainer"> 
   <div class="description"> 
    <ul class="blockList"> 
     <li class="blockList"> 
      <dl> 
       <dt>
         All Superinterfaces: 
       </dt> 
       <dd> 
        <span><a href="../../../java/lang/AutoCloseable.html" title="java.lang中的接口">AutoCloseable</a> ， <a href="../../../java/nio/channels/Channel.html" title="java.nio.channels中的接口">Channel</a> ， <a href="../../../java/io/Closeable.html" title="java.io中的接口">Closeable</a></span> 
       </dd> 
      </dl> 
      <dl> 
       <dt>
         All Known Subinterfaces: 
       </dt> 
       <dd> 
        <span><a href="../../../java/nio/channels/AsynchronousByteChannel.html" title="java.nio.channels中的接口">AsynchronousByteChannel</a></span> 
       </dd> 
      </dl> 
      <dl> 
       <dt>
        所有已知实现类：
       </dt> 
       <dd> 
        <span><a href="../../../java/nio/channels/AsynchronousFileChannel.html" title="java.nio.channels中的类">AsynchronousFileChannel</a> ， <a href="../../../java/nio/channels/AsynchronousServerSocketChannel.html" title="java.nio.channels中的类">AsynchronousServerSocketChannel</a> ， <a href="../../../java/nio/channels/AsynchronousSocketChannel.html" title="java.nio.channels中的类">AsynchronousSocketChannel</a></span> 
       </dd> 
      </dl> 
      <hr> <br> <pre>public interface <span class="typeNameLabel">AsynchronousChannel</span>
extends <a href="../../../java/nio/channels/Channel.html" title="interface in java.nio.channels">Channel</a></pre> 
      <div class="block"> 
       <span>支持异步I / O操作的通道。</span> 
       <span>异步I / O操作通常采用以下两种形式之一：</span> 
       <ol> 
        <li><pre>  <span><a href="../../../java/util/concurrent/Future.html" title="interface in java.util.concurrent"><code>Future</code></a>&lt;V&gt; <em>operation</em>(<em>...</em>)</span> </pre></li> 
        <li><pre>  <span>void <em>operation</em>(<em>...</em> A attachment, <a href="../../../java/nio/channels/CompletionHandler.html" title="interface in java.nio.channels"><code>CompletionHandler</code></a>&lt;V,? super A&gt; handler)</span> </pre></li> 
       </ol> 
       <span>其中<i>操作</i>是I / O操作的名称（例如读或写）， <i>V</i>是I / O操作的结果类型， <i>A</i>是附加到I / O操作以提供上下文的对象的类型消耗结果。</span> 
       <span>对于无<em>状态</em> <code>CompletionHandler</code>用于消耗许多I / O操作的结果的情况， <code>CompletionHandler</code>很重要。</span> 
       <p> <span>在第一种形式中，由<a href="../../../java/util/concurrent/Future.html" title="java.util.concurrent中的接口"><code>Future</code></a>接口定义的方法可用于检查操作是否已经完成，等待其完成，并检索结果。</span> <span>在第二种形式中，一个<a href="../../../java/nio/channels/CompletionHandler.html" title="java.nio.channels中的接口"><code>CompletionHandler</code></a>被调用它何时完成或失败来消耗I / O操作的结果。</span> </p> 
       <p> <span>实现此接口的通道<em>异步关闭</em> ：如果通道上的I / O操作未完成，并且调用通道的<a href="../../../java/nio/channels/AsynchronousChannel.html#close--"><code>close</code></a>方法，则I / O操作将失败，但<code>AsynchronousCloseException</code> <a href="../../../java/nio/channels/AsynchronousCloseException.html" title="java.nio.channels中的类">除外</a> 。</span> </p> 
       <p> <span>异步通道可以安全地被多个并发线程使用。</span> <span>一些通道实现可以支持并发读取和写入，但是在任何给定时间可能不允许多于一个读取和一个写入操作。</span> </p> 
       <h2> <span>消除</span> </h2> 
       <p> <span><code>Future</code>接口定义了取消执行的<a href="../../../java/util/concurrent/Future.html#cancel-boolean-"><code>cancel</code></a>方法。</span> <span>这将导致所有线程等待I / O操作的结果抛出<a href="../../../java/util/concurrent/CancellationException.html" title="java.util.concurrent中的类"><code>CancellationException</code></a> 。</span> <span>是否可以取消基础I / O操作是高度实现具体的，因此未指定。</span> <span>如果取消离开通道或其连接的实体处于不一致的状态，则该通道将被置于实现特定的<em>错误状态</em> ，以防止进一步尝试启动<i>类似于</i>已取消操作的I / O操作。</span> <span>例如，如果读取操作被取消，但实现不能保证字节没有从通道读取，那么它将通道置于错误状态;</span> <span>进一步尝试启动<code>read</code>操作会引起未指定的运行时异常。</span> <span>同样，如果一个写操作将被取消，但执行不能保证字节还没有被写入通道，然后随后尝试启动<code>write</code>将失败，未指定的运行时异常。</span> </p> 
       <p> <span>在<a href="../../../java/util/concurrent/Future.html#cancel-boolean-"><code>cancel</code></a>方法调用<code>mayInterruptIfRunning</code>参数设置为<code>true</code>下，I / O操作可能会由于关闭通道而中断。</span> <span>在这种情况下，等待I / O操作结果的所有线程都抛出<code>CancellationException</code>以及任何其他在通道上未完成的I / O操作，并且异常<a href="../../../java/nio/channels/AsynchronousCloseException.html" title="java.nio.channels中的类"><code>AsynchronousCloseException</code></a> 。</span> </p> 
       <p> <span>在调用<code>cancel</code>方法以取消读取或写入操作的情况下，建议丢弃在I / O操作中使用的所有缓冲区，或注意确保在通道保持打开状态时不访问缓冲区。</span> </p> 
      </div> 
      <dl> 
       <dt> 
        <span class="simpleTagLabel">从以下版本开始：</span> 
       </dt> 
       <dd>
         1.7 
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
           <td class="colLast"><code><span class="memberNameLink"><a href="../../../java/nio/channels/AsynchronousChannel.html#close--">close</a></span>()</code> 
            <div class="block">
              关闭此频道。 
            </div> </td> 
          </tr> 
         </tbody> 
        </table> 
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
         <!--   --> </a> <h3>方法详细信息</h3> <a name="close--"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>close</h4> <pre>void&nbsp;close()
    throws <a href="../../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>关闭此频道。</span> 
           <p> <span>此通道上的任何未完成的异步<a href="../../../java/nio/channels/AsynchronousCloseException.html" title="java.nio.channels中的类">操作</a>将完成，但<code>AsynchronousCloseException</code> <a href="../../../java/nio/channels/AsynchronousCloseException.html" title="java.nio.channels中的类">除外</a> 。</span> <span>在关闭通道后，进一步尝试启动异步I / O操作，立即完成原因<a href="../../../java/nio/channels/ClosedChannelException.html" title="java.nio.channels中的类"><code>ClosedChannelException</code></a> 。</span> </p> 
           <p> <span>该方法的行为与<code>Channel</code>接口的<a href="../../../java/nio/channels/Channel.html" title="java.nio.channels中的接口">规定</a>完全相同。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">Specified by:</span> 
           </dt> 
           <dd> 
            <code><a href="../../../java/lang/AutoCloseable.html#close--">close</a></code>在界面 
            <code><a href="../../../java/lang/AutoCloseable.html" title="interface in java.lang">AutoCloseable</a></code> 
           </dd> 
           <dt> 
            <span class="overrideSpecifyLabel">Specified by:</span> 
           </dt> 
           <dd> 
            <code><a href="../../../java/nio/channels/Channel.html#close--">close</a></code>中的 
            <code><a href="../../../java/nio/channels/Channel.html" title="interface in java.nio.channels">Channel</a></code> 
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
            <code><a href="../../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生I / O错误 
           </dd> 
          </dl> </li> 
        </ul> </li> 
      </ul> </li> 
    </ul> 
   </div> 
  </div>
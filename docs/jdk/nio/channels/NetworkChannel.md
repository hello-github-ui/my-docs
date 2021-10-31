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
        <span><a href="../../../java/nio/channels/MulticastChannel.html" title="java.nio.channels中的接口">MulticastChannel</a></span> 
       </dd> 
      </dl> 
      <dl> 
       <dt>
        所有已知实现类：
       </dt> 
       <dd> 
        <span><a href="../../../java/nio/channels/AsynchronousServerSocketChannel.html" title="java.nio.channels中的类">AsynchronousServerSocketChannel</a> ， <a href="../../../java/nio/channels/AsynchronousSocketChannel.html" title="java.nio.channels中的类">AsynchronousSocketChannel</a> ， <a href="../../../java/nio/channels/DatagramChannel.html" title="java.nio.channels中的类">DatagramChannel</a> ， <a href="../../../java/nio/channels/ServerSocketChannel.html" title="java.nio.channels中的类">ServerSocketChannel</a> ， <a href="../../../java/nio/channels/SocketChannel.html" title="java.nio.channels中的类">SocketChannel</a></span> 
       </dd> 
      </dl> 
      <hr> <br> <pre>public interface <span class="typeNameLabel">NetworkChannel</span>
extends <a href="../../../java/nio/channels/Channel.html" title="interface in java.nio.channels">Channel</a></pre> 
      <div class="block"> 
       <span>到网络插座的通道。</span> 
       <p> <span>实现此接口的通道是通向网络套接字的通道。</span> <span>该<a href="../../../java/nio/channels/NetworkChannel.html#bind-java.net.SocketAddress-"><code>bind</code></a>方法用于套接字绑定到本地<a href="../../../java/net/SocketAddress.html" title="java.net中的类"><code>address</code></a> ，所述<a href="../../../java/nio/channels/NetworkChannel.html#getLocalAddress--"><code>getLocalAddress</code></a>方法返回套接字绑定到地址， <a href="../../../java/nio/channels/NetworkChannel.html#setOption-java.net.SocketOption-T-"><code>setOption</code></a>种<a href="../../../java/nio/channels/NetworkChannel.html#getOption-java.net.SocketOption-"><code>getOption</code></a>方法用于设置和查询套接字选项。</span> <span>此接口的实现应指定其支持的套接字选项。</span> </p> 
       <p> <span><a href="../../../java/nio/channels/NetworkChannel.html#bind-java.net.SocketAddress-">指定</a>不另外具有值返回值的<a href="../../../java/nio/channels/NetworkChannel.html#bind-java.net.SocketAddress-"><code>bind</code></a>和<a href="../../../java/nio/channels/NetworkChannel.html#setOption-java.net.SocketOption-T-"><code>setOption</code></a>方法来返回调用它们的网络通道。</span> <span>这允许方法调用被链接。</span> <span>该接口的实现应该专门化返回类型，以便可以链接实现类上的方法调用。</span> </p> 
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
           <td class="colFirst"><code><a href="../../../java/nio/channels/NetworkChannel.html" title="interface in java.nio.channels">NetworkChannel</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../../java/nio/channels/NetworkChannel.html#bind-java.net.SocketAddress-">bind</a></span>(<a href="../../../java/net/SocketAddress.html" title="class in java.net">SocketAddress</a>&nbsp;local)</code> 
            <div class="block">
              将通道的套接字绑定到本地地址。 
            </div> </td> 
          </tr> 
          <tr id="i1" class="rowColor"> 
           <td class="colFirst"><code><a href="../../../java/net/SocketAddress.html" title="class in java.net">SocketAddress</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../../java/nio/channels/NetworkChannel.html#getLocalAddress--">getLocalAddress</a></span>()</code> 
            <div class="block">
              返回此通道的套接字所绑定的套接字地址。 
            </div> </td> 
          </tr> 
          <tr id="i2" class="altColor"> 
           <td class="colFirst"><code>&lt;T&gt;&nbsp;T</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../../java/nio/channels/NetworkChannel.html#getOption-java.net.SocketOption-">getOption</a></span>(<a href="../../../java/net/SocketOption.html" title="interface in java.net">SocketOption</a>&lt;T&gt;&nbsp;name)</code> 
            <div class="block">
              返回套接字选项的值。 
            </div> </td> 
          </tr> 
          <tr id="i3" class="rowColor"> 
           <td class="colFirst"><code>&lt;T&gt;&nbsp;<a href="../../../java/nio/channels/NetworkChannel.html" title="interface in java.nio.channels">NetworkChannel</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../../java/nio/channels/NetworkChannel.html#setOption-java.net.SocketOption-T-">setOption</a></span>(<a href="../../../java/net/SocketOption.html" title="interface in java.net">SocketOption</a>&lt;T&gt;&nbsp;name, T&nbsp;value)</code> 
            <div class="block">
              设置套接字选项的值。 
            </div> </td> 
          </tr> 
          <tr id="i4" class="altColor"> 
           <td class="colFirst"><code><a href="../../../java/util/Set.html" title="interface in java.util">Set</a>&lt;<a href="../../../java/net/SocketOption.html" title="interface in java.net">SocketOption</a>&lt;?&gt;&gt;</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../../java/nio/channels/NetworkChannel.html#supportedOptions--">supportedOptions</a></span>()</code> 
            <div class="block">
              返回此通道支持的一组套接字选项。 
            </div> </td> 
          </tr> 
         </tbody> 
        </table> 
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
         <!--   --> </a> <h3>方法详细信息</h3> <a name="bind-java.net.SocketAddress-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>bind</h4> <pre><a href="../../../java/nio/channels/NetworkChannel.html" title="interface in java.nio.channels">NetworkChannel</a>&nbsp;bind(<a href="../../../java/net/SocketAddress.html" title="class in java.net">SocketAddress</a>&nbsp;local)
             throws <a href="../../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>将通道的套接字绑定到本地地址。</span> 
           <p> <span>该方法用于在套接字和本地地址之间建立关联。</span> <span>一旦建立关联，则套接字保持绑定，直到通道关闭。</span> <span>如果<code>local</code>参数的值为<code>null</code>则套接字将被绑定到自动分配的地址。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>local</code> - 绑定套接字的地址，或 
            <code>null</code>将套接字绑定到自动分配的套接字地址 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             这个频道 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../../java/nio/channels/AlreadyBoundException.html" title="class in java.nio.channels">AlreadyBoundException</a></code> - 如果套接字已经绑定 
           </dd> 
           <dd> 
            <code><a href="../../../java/nio/channels/UnsupportedAddressTypeException.html" title="class in java.nio.channels">UnsupportedAddressTypeException</a></code> - 如果不支持给定地址的类型 
           </dd> 
           <dd> 
            <code><a href="../../../java/nio/channels/ClosedChannelException.html" title="class in java.nio.channels">ClosedChannelException</a></code> - 如果通道关闭 
           </dd> 
           <dd> 
            <code><a href="../../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生其他I / O错误 
           </dd> 
           <dd> 
            <span><code><a href="../../../java/lang/SecurityException.html" title="class in java.lang">SecurityException</a></code> - 如果安装了一个安全管理器，并且它拒绝了未指定的权限。</span> 
            <span>此接口的实现应指定任何所需的权限。</span> 
           </dd> 
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <a href="../../../java/nio/channels/NetworkChannel.html#getLocalAddress--"><code>getLocalAddress()</code></a> 
           </dd> 
          </dl> </li> 
        </ul> <a name="getLocalAddress--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>getLocalAddress</h4> <pre><a href="../../../java/net/SocketAddress.html" title="class in java.net">SocketAddress</a>&nbsp;getLocalAddress()
                       throws <a href="../../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>返回此通道的套接字所绑定的套接字地址。</span> 
           <p> <span>通道为Internet协议套接字地址的<a href="../../../java/nio/channels/NetworkChannel.html#bind-java.net.SocketAddress-"><code>bound</code></a> ，则此方法的返回值为<a href="../../../java/net/InetSocketAddress.html" title="java.net中的类"><code>InetSocketAddress</code></a> 。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             套接字绑定的套接字地址，如果通道的套接字未绑定， 
            <code>null</code> 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../../java/nio/channels/ClosedChannelException.html" title="class in java.nio.channels">ClosedChannelException</a></code> - 如果通道关闭 
           </dd> 
           <dd> 
            <code><a href="../../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生I / O错误 
           </dd> 
          </dl> </li> 
        </ul> <a name="setOption-java.net.SocketOption-java.lang.Object-"> 
         <!--   --> </a><a name="setOption-java.net.SocketOption-T-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>setOption</h4> <pre>&lt;T&gt;&nbsp;<a href="../../../java/nio/channels/NetworkChannel.html" title="interface in java.nio.channels">NetworkChannel</a>&nbsp;setOption(<a href="../../../java/net/SocketOption.html" title="interface in java.net">SocketOption</a>&lt;T&gt;&nbsp;name,
                             T&nbsp;value)
                      throws <a href="../../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block">
            设置套接字选项的值。 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数类型</span> 
           </dt> 
           <dd> 
            <code>T</code> - 套接字选项值的类型 
           </dd> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>name</code> - 套接字选项 
           </dd> 
           <dd> 
            <span><code>value</code> - 套接字选项的值。</span> 
            <span>值为<code>null</code>可能是某些套接字选项的有效值。</span> 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             这个频道 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../../java/lang/UnsupportedOperationException.html" title="class in java.lang">UnsupportedOperationException</a></code> - 如果此通道不支持套接字选项 
           </dd> 
           <dd> 
            <code><a href="../../../java/lang/IllegalArgumentException.html" title="class in java.lang">IllegalArgumentException</a></code> - 如果该值不是此套接字选项的有效值 
           </dd> 
           <dd> 
            <code><a href="../../../java/nio/channels/ClosedChannelException.html" title="class in java.nio.channels">ClosedChannelException</a></code> - 如果此通道关闭 
           </dd> 
           <dd> 
            <code><a href="../../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生I / O错误 
           </dd> 
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <span><a href="../../../java/net/StandardSocketOptions.html" title="java.net中的类"><code>StandardSocketOptions</code></a></span> 
           </dd> 
          </dl> </li> 
        </ul> <a name="getOption-java.net.SocketOption-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>getOption</h4> <pre>&lt;T&gt;&nbsp;T&nbsp;getOption(<a href="../../../java/net/SocketOption.html" title="interface in java.net">SocketOption</a>&lt;T&gt;&nbsp;name)
         throws <a href="../../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block">
            返回套接字选项的值。 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数类型</span> 
           </dt> 
           <dd> 
            <code>T</code> - 套接字选项值的类型 
           </dd> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>name</code> - 套接字选项 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd> 
            <span>套接字选项的值。</span> 
            <span>值为<code>null</code>可能是某些套接字选项的有效值。</span> 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../../java/lang/UnsupportedOperationException.html" title="class in java.lang">UnsupportedOperationException</a></code> - 如果此通道不支持套接字选项 
           </dd> 
           <dd> 
            <code><a href="../../../java/nio/channels/ClosedChannelException.html" title="class in java.nio.channels">ClosedChannelException</a></code> - 如果此通道关闭 
           </dd> 
           <dd> 
            <code><a href="../../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生I / O错误 
           </dd> 
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <span><a href="../../../java/net/StandardSocketOptions.html" title="java.net中的类"><code>StandardSocketOptions</code></a></span> 
           </dd> 
          </dl> </li> 
        </ul> <a name="supportedOptions--"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>supportedOptions</h4> <pre><a href="../../../java/util/Set.html" title="interface in java.util">Set</a>&lt;<a href="../../../java/net/SocketOption.html" title="interface in java.net">SocketOption</a>&lt;?&gt;&gt;&nbsp;supportedOptions()</pre> 
          <div class="block"> 
           <span>返回此通道支持的一组套接字选项。</span> 
           <p> <span>即使通道关闭后，此方法仍将继续返回该选项。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             A set of the socket options supported by this channel 
           </dd> 
          </dl> </li> 
        </ul> </li> 
      </ul> </li> 
    </ul> 
   </div> 
  </div>
<div class="contentContainer"> 
   <ul class="inheritance"> 
    <li><a href="../../java/lang/Object.html" title="class in java.lang">java.lang.Object</a></li> 
    <li> 
     <ul class="inheritance"> 
      <li><a href="../../java/nio/Buffer.html" title="class in java.nio">java.nio.Buffer</a></li> 
      <li> 
       <ul class="inheritance"> 
        <li>java.nio.IntBuffer</li> 
       </ul> </li> 
     </ul> </li> 
   </ul> 
   <div class="description"> 
    <ul class="blockList"> 
     <li class="blockList"> 
      <dl> 
       <dt>
         All Implemented Interfaces: 
       </dt> 
       <dd> 
        <span><a href="../../java/lang/Comparable.html" title="java.lang中的接口">Comparable</a> &lt; <a href="../../java/nio/IntBuffer.html" title="java.nio中的类">IntBuffer</a> &gt;</span> 
       </dd> 
      </dl> 
      <hr> <br> <pre>public abstract class <span class="typeNameLabel">IntBuffer</span>
extends <a href="../../java/nio/Buffer.html" title="class in java.nio">Buffer</a>
implements <a href="../../java/lang/Comparable.html" title="interface in java.lang">Comparable</a>&lt;<a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a>&gt;</pre> 
      <div class="block"> 
       <span>一个int缓冲区</span> 
       <p> <span>该类定义了int缓冲区中的四类操作：</span> </p> 
       <ul> 
        <li><p> <span>绝对和相对的<a href="../../java/nio/IntBuffer.html#get--"><code><i>get</i></code></a>和<a href="../../java/nio/IntBuffer.html#put-int-"><code><i>put</i></code></a>读写单个int的方法;</span> </p></li> 
        <li><p> <span>相对<a href="../../java/nio/IntBuffer.html#get-int:A-"><code><i>bulk get</i></code></a>方法将连续的ints序列从该缓冲区传输到数组中;</span> <span>和</span> </p></li> 
        <li><p> <span>相对<a href="../../java/nio/IntBuffer.html#put-int:A-"><code><i>bulk put</i></code></a>方法，将int数组或其他int缓冲区的连续序列传输到此缓冲区中;</span> <span>和</span> </p></li> 
        <li><p> <span>方法<a href="../../java/nio/IntBuffer.html#compact--"><code>compacting</code></a> ， <a href="../../java/nio/IntBuffer.html#duplicate--"><code>duplicating</code></a>和<a href="../../java/nio/IntBuffer.html#slice--"><code>slicing</code></a> INT缓冲区。</span> </p></li> 
       </ul> 
       <p> <span>Int缓冲区可以由<a href="../../java/nio/IntBuffer.html#allocate-int-"><code><i>allocation</i></code></a>创建，该缓冲区为缓冲区的内容分配空间， <a href="../../java/nio/IntBuffer.html#wrap-int:A-">89424995934805</a>将现有的int数组<a href="../../java/nio/IntBuffer.html#wrap-int:A-">分配</a>到缓冲区中，或通过创建现有字节缓冲区的<a href="ByteBuffer.html#views"><i>view</i></a> 。</span> </p> 
       <p> <span>像一个字节缓冲区一样，int缓冲区是<a href="ByteBuffer.html#direct"><i>direct</i> or <i>non-direct</i></a> 。</span> <span>通过<tt>此类的wrap</tt>方法创建的int缓冲区将是非直接的。</span> <span>作为字节缓冲区视图创建的int缓冲区将是直接的，只有当字节缓冲区本身是直接的。</span> <span>int缓冲区是否直接可以通过调用<a href="../../java/nio/IntBuffer.html#isDirect--"><code>isDirect</code></a>方法来确定。</span> </p> 
       <p> <span>指定此类中没有值返回值的方法返回调用它们的缓冲区。</span> <span>这允许方法调用被链接。</span> </p> 
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
          <span id="t1" class="tableTab"><span><a href="javascript:show(1);">静态方法</a></span><span class="tabEnd">&nbsp;</span></span> 
          <span id="t2" class="tableTab"><span><a href="javascript:show(2);">接口方法</a></span><span class="tabEnd">&nbsp;</span></span> 
          <span id="t3" class="tableTab"><span><a href="javascript:show(4);">抽象方法</a></span><span class="tabEnd">&nbsp;</span></span> 
          <span id="t4" class="tableTab"><span><a href="javascript:show(8);">具体的方法</a></span><span class="tabEnd">&nbsp;</span></span> 
         </caption> 
         <tbody> 
          <tr> 
           <th class="colFirst" scope="col">Modifier and Type</th> 
           <th class="colLast" scope="col">Method and Description</th> 
          </tr> 
          <tr id="i0" class="altColor"> 
           <td class="colFirst"><code>static <a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/IntBuffer.html#allocate-int-">allocate</a></span>(int&nbsp;capacity)</code> 
            <div class="block">
              分配一个新的int缓冲区。 
            </div> </td> 
          </tr> 
          <tr id="i1" class="rowColor"> 
           <td class="colFirst"><code>int[]</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/IntBuffer.html#array--">array</a></span>()</code> 
            <div class="block">
              返回支持此缓冲区的int数组 
             <i>（可选操作）</i> 。 
            </div> </td> 
          </tr> 
          <tr id="i2" class="altColor"> 
           <td class="colFirst"><code>int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/IntBuffer.html#arrayOffset--">arrayOffset</a></span>()</code> 
            <div class="block">
              返回该缓冲区的缓冲区的第一个元素的背衬数组中的偏移量 
             <i>（可选操作）</i> 。 
            </div> </td> 
          </tr> 
          <tr id="i3" class="rowColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/IntBuffer.html#asReadOnlyBuffer--">asReadOnlyBuffer</a></span>()</code> 
            <div class="block">
              创建一个新的只读int缓冲区，共享此缓冲区的内容。 
            </div> </td> 
          </tr> 
          <tr id="i4" class="altColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/IntBuffer.html#compact--">compact</a></span>()</code> 
            <div class="block"> 
             <i>压缩</i>此缓冲区 
             <i>（可选操作）</i> 。 
            </div> </td> 
          </tr> 
          <tr id="i5" class="rowColor"> 
           <td class="colFirst"><code>int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/IntBuffer.html#compareTo-java.nio.IntBuffer-">compareTo</a></span>(<a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a>&nbsp;that)</code> 
            <div class="block">
              将此缓冲区与另一个缓冲区进行比较。 
            </div> </td> 
          </tr> 
          <tr id="i6" class="altColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/IntBuffer.html#duplicate--">duplicate</a></span>()</code> 
            <div class="block">
              创建一个共享此缓冲区内容的新int缓冲区。 
            </div> </td> 
          </tr> 
          <tr id="i7" class="rowColor"> 
           <td class="colFirst"><code>boolean</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/IntBuffer.html#equals-java.lang.Object-">equals</a></span>(<a href="../../java/lang/Object.html" title="class in java.lang">Object</a>&nbsp;ob)</code> 
            <div class="block">
              告诉这个缓冲区是否等于另一个对象。 
            </div> </td> 
          </tr> 
          <tr id="i8" class="altColor"> 
           <td class="colFirst"><code>abstract int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/IntBuffer.html#get--">get</a></span>()</code> 
            <div class="block">
              相对 
             <i>获取</i>方法。 
            </div> </td> 
          </tr> 
          <tr id="i9" class="rowColor"> 
           <td class="colFirst"><code>abstract int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/IntBuffer.html#get-int-">get</a></span>(int&nbsp;index)</code> 
            <div class="block">
              绝对 
             <i>获取</i>方法。 
            </div> </td> 
          </tr> 
          <tr id="i10" class="altColor"> 
           <td class="colFirst"><code><a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/IntBuffer.html#get-int:A-">get</a></span>(int[]&nbsp;dst)</code> 
            <div class="block">
              相对批量 
             <i>获取</i>方法。 
            </div> </td> 
          </tr> 
          <tr id="i11" class="rowColor"> 
           <td class="colFirst"><code><a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/IntBuffer.html#get-int:A-int-int-">get</a></span>(int[]&nbsp;dst, int&nbsp;offset, int&nbsp;length)</code> 
            <div class="block">
              相对批量 
             <i>获取</i>方法。 
            </div> </td> 
          </tr> 
          <tr id="i12" class="altColor"> 
           <td class="colFirst"><code>boolean</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/IntBuffer.html#hasArray--">hasArray</a></span>()</code> 
            <div class="block">
              告诉这个缓冲区是否由可访问的int数组支持。 
            </div> </td> 
          </tr> 
          <tr id="i13" class="rowColor"> 
           <td class="colFirst"><code>int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/IntBuffer.html#hashCode--">hashCode</a></span>()</code> 
            <div class="block">
              返回此缓冲区的当前哈希码。 
            </div> </td> 
          </tr> 
          <tr id="i14" class="altColor"> 
           <td class="colFirst"><code>abstract boolean</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/IntBuffer.html#isDirect--">isDirect</a></span>()</code> 
            <div class="block">
              告诉这个int缓冲区是否直接。 
            </div> </td> 
          </tr> 
          <tr id="i15" class="rowColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/nio/ByteOrder.html" title="class in java.nio">ByteOrder</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/IntBuffer.html#order--">order</a></span>()</code> 
            <div class="block">
              检索此缓冲区的字节顺序。 
            </div> </td> 
          </tr> 
          <tr id="i16" class="altColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/IntBuffer.html#put-int-">put</a></span>(int&nbsp;i)</code> 
            <div class="block">
              相对 
             <i>放置</i>法 
             <i>（可选操作）</i> 。 
            </div> </td> 
          </tr> 
          <tr id="i17" class="rowColor"> 
           <td class="colFirst"><code><a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/IntBuffer.html#put-int:A-">put</a></span>(int[]&nbsp;src)</code> 
            <div class="block">
              相对大容量 
             <i>put</i>方法 
             <i>（可选操作）</i> 。 
            </div> </td> 
          </tr> 
          <tr id="i18" class="altColor"> 
           <td class="colFirst"><code><a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/IntBuffer.html#put-int:A-int-int-">put</a></span>(int[]&nbsp;src, int&nbsp;offset, int&nbsp;length)</code> 
            <div class="block">
              相对大容量 
             <i>put</i>方法 
             <i>（可选操作）</i> 。 
            </div> </td> 
          </tr> 
          <tr id="i19" class="rowColor"> 
           <td class="colFirst"><code><a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/IntBuffer.html#put-java.nio.IntBuffer-">put</a></span>(<a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a>&nbsp;src)</code> 
            <div class="block">
              相对大容量 
             <i>put</i>方法 
             <i>（可选操作）</i> 。 
            </div> </td> 
          </tr> 
          <tr id="i20" class="altColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/IntBuffer.html#put-int-int-">put</a></span>(int&nbsp;index, int&nbsp;i)</code> 
            <div class="block">
              绝对 
             <i>put</i>方法 
             <i>（可选操作）</i> 。 
            </div> </td> 
          </tr> 
          <tr id="i21" class="rowColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/IntBuffer.html#slice--">slice</a></span>()</code> 
            <div class="block">
              创建一个新的int缓冲区，其内容是此缓冲区内容的共享子序列。 
            </div> </td> 
          </tr> 
          <tr id="i22" class="altColor"> 
           <td class="colFirst"><code><a href="../../java/lang/String.html" title="class in java.lang">String</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/IntBuffer.html#toString--">toString</a></span>()</code> 
            <div class="block">
              返回一个汇总此缓冲区状态的字符串。 
            </div> </td> 
          </tr> 
          <tr id="i23" class="rowColor"> 
           <td class="colFirst"><code>static <a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/IntBuffer.html#wrap-int:A-">wrap</a></span>(int[]&nbsp;array)</code> 
            <div class="block">
              将int数组包装到缓冲区中。 
            </div> </td> 
          </tr> 
          <tr id="i24" class="altColor"> 
           <td class="colFirst"><code>static <a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/IntBuffer.html#wrap-int:A-int-int-">wrap</a></span>(int[]&nbsp;array, int&nbsp;offset, int&nbsp;length)</code> 
            <div class="block">
              将int数组包装到缓冲区中。 
            </div> </td> 
          </tr> 
         </tbody> 
        </table> 
        <ul class="blockList"> 
         <li class="blockList"><a name="methods.inherited.from.class.java.nio.Buffer"> 
           <!--   --> </a> <h3>Methods inherited from class&nbsp;java.nio.<a href="../../java/nio/Buffer.html" title="class in java.nio">Buffer</a></h3> <code><a href="../../java/nio/Buffer.html#capacity--">capacity</a>, <a href="../../java/nio/Buffer.html#clear--">clear</a>, <a href="../../java/nio/Buffer.html#flip--">flip</a>, <a href="../../java/nio/Buffer.html#hasRemaining--">hasRemaining</a>, <a href="../../java/nio/Buffer.html#isReadOnly--">isReadOnly</a>, <a href="../../java/nio/Buffer.html#limit--">limit</a>, <a href="../../java/nio/Buffer.html#limit-int-">limit</a>, <a href="../../java/nio/Buffer.html#mark--">mark</a>, <a href="../../java/nio/Buffer.html#position--">position</a>, <a href="../../java/nio/Buffer.html#position-int-">position</a>, <a href="../../java/nio/Buffer.html#remaining--">remaining</a>, <a href="../../java/nio/Buffer.html#reset--">reset</a>, <a href="../../java/nio/Buffer.html#rewind--">rewind</a></code></li> 
        </ul> 
        <ul class="blockList"> 
         <li class="blockList"><a name="methods.inherited.from.class.java.lang.Object"> 
           <!--   --> </a> <h3>Methods inherited from class&nbsp;java.lang.<a href="../../java/lang/Object.html" title="class in java.lang">Object</a></h3> <code><a href="../../java/lang/Object.html#clone--">clone</a>, <a href="../../java/lang/Object.html#finalize--">finalize</a>, <a href="../../java/lang/Object.html#getClass--">getClass</a>, <a href="../../java/lang/Object.html#notify--">notify</a>, <a href="../../java/lang/Object.html#notifyAll--">notifyAll</a>, <a href="../../java/lang/Object.html#wait--">wait</a>, <a href="../../java/lang/Object.html#wait-long-">wait</a>, <a href="../../java/lang/Object.html#wait-long-int-">wait</a></code></li> 
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
         <!--   --> </a> <h3>方法详细信息</h3> <a name="allocate-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>allocate</h4> <pre>public static&nbsp;<a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a>&nbsp;allocate(int&nbsp;capacity)</pre> 
          <div class="block"> 
           <span>分配一个新的int缓冲区。</span> 
           <p> <span>新缓冲区的位置将为零，其限制将为其容量，其标记将不定义，并且其每个元素将被初始化为零。</span> <span>它将有一个<a href="../../java/nio/IntBuffer.html#array--"><code>backing array</code></a> ，其<a href="../../java/nio/IntBuffer.html#arrayOffset--"><code>array offset</code></a>将为零。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>capacity</code> - 新的缓冲区的容量，在ints 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             新的int缓冲区 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/IllegalArgumentException.html" title="class in java.lang">IllegalArgumentException</a></code> - 如果 
            <tt>capacity</tt>是负整数 
           </dd> 
          </dl> </li> 
        </ul> <a name="wrap-int:A-int-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>wrap</h4> <pre>public static&nbsp;<a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a>&nbsp;wrap(int[]&nbsp;array,
                             int&nbsp;offset,
                             int&nbsp;length)</pre> 
          <div class="block"> 
           <span>将int数组包装到缓冲区中。</span> 
           <p> <span>新的缓冲区将由给定的int数组支持;</span> <span>也就是说，对缓冲区的修改将导致数组被修改，反之亦然。</span> <span>新增缓存的容量将为<tt>array.length</tt> ，其位置将为<tt>offset</tt> ，其限制将为<tt>offset + length</tt> ，其标记将不定。</span> <span>其<a href="../../java/nio/IntBuffer.html#array--"><code>backing array</code></a>将是给定的数组，其<a href="../../java/nio/IntBuffer.html#arrayOffset--"><code>array offset</code></a>将为零。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>array</code> - 将返回新缓冲区的数组 
           </dd> 
           <dd> 
            <span><code>offset</code> - 要使用的子阵列的偏移量;</span> 
            <span>必须是非负数，不得大于<tt>array.length</tt> 。</span> 
            <span>新缓冲区的位置将被设置为此值。</span> 
           </dd> 
           <dd> 
            <span><code>length</code> - 要使用的子阵列的长度;</span> 
            <span>必须是非负数，不得大于<tt>array.length - offset</tt> 。</span> 
            <span>新缓冲区的限制将设置为<tt>offset + length</tt> 。</span> 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             新的int缓冲区 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/IndexOutOfBoundsException.html" title="class in java.lang">IndexOutOfBoundsException</a></code> - 如果 
            <tt>offset</tt>和 
            <tt>length</tt>参数的前提条件不成立 
           </dd> 
          </dl> </li> 
        </ul> <a name="wrap-int:A-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>wrap</h4> <pre>public static&nbsp;<a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a>&nbsp;wrap(int[]&nbsp;array)</pre> 
          <div class="block"> 
           <span>将int数组包装到缓冲区中。</span> 
           <p> <span>新的缓冲区将由给定的int数组支持;</span> <span>也就是说，对缓冲区的修改将导致数组被修改，反之亦然。</span> <span>新缓冲区的容量和限制将为<tt>array.length</tt> ，其位置将为零，其标记将不定。</span> <span>它的<a href="../../java/nio/IntBuffer.html#array--"><code>backing array</code></a>将是给定的数组，其<a href="../../java/nio/IntBuffer.html#arrayOffset--"><code>array offset&gt;</code></a>将为零。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>array</code> - 将返回此缓冲区的数组 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             新的int缓冲区 
           </dd> 
          </dl> </li> 
        </ul> <a name="slice--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>slice</h4> <pre>public abstract&nbsp;<a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a>&nbsp;slice()</pre> 
          <div class="block"> 
           <span>创建一个新的int缓冲区，其内容是此缓冲区内容的共享子序列。</span> 
           <p> <span>新缓冲区的内容将从此缓冲区的当前位置开始。</span> <span>对这个缓冲区内容的更改将在新的缓冲区中可见，反之亦然;</span> <span>两个缓冲区的位置，极限和标记值将是独立的。</span> </p> 
           <p> <span>新缓冲区的位置将为零，其容量和限制将是此缓冲区中剩余的int数，其标记将不定义。</span> <span>如果只有这个缓冲区是直接的，并且只有当这个缓冲区是只读的时，这个缓冲区将是只读的。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             新的int缓冲区 
           </dd> 
          </dl> </li> 
        </ul> <a name="duplicate--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>duplicate</h4> <pre>public abstract&nbsp;<a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a>&nbsp;duplicate()</pre> 
          <div class="block"> 
           <span>创建一个共享此缓冲区内容的新int缓冲区。</span> 
           <p> <span>新缓冲区的内容将是这个缓冲区的内容。</span> <span>对这个缓冲区内容的更改将在新的缓冲区中可见，反之亦然;</span> <span>两个缓冲区的位置，极限和标记值将是独立的。</span> </p> 
           <p> <span>新缓冲区的容量，限制，位置和标记值将与此缓冲区的容量，限制，位置和标记值相同。</span> <span>如果只有这个缓冲区是直接的，并且只有当这个缓冲区是只读的时，这个缓冲区将是只读的。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             新的int缓冲区 
           </dd> 
          </dl> </li> 
        </ul> <a name="asReadOnlyBuffer--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>asReadOnlyBuffer</h4> <pre>public abstract&nbsp;<a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a>&nbsp;asReadOnlyBuffer()</pre> 
          <div class="block"> 
           <span>创建一个新的只读int缓冲区，共享此缓冲区的内容。</span> 
           <p> <span>新缓冲区的内容将是这个缓冲区的内容。</span> <span>这个缓冲区内容的更改将在新的缓冲区中显示;</span> <span>然而，新的缓冲区本身将是只读的，不允许修改共享内容。</span> <span>两个缓冲区的位置，极限和标记值将是独立的。</span> </p> 
           <p> <span>新缓冲区的容量，限制，位置和标记值将与此缓冲区的容量，限制，位置和标记值相同。</span> </p> 
           <p> <span>如果此缓冲区本身是只读的，则该方法的行为与<a href="../../java/nio/IntBuffer.html#duplicate--"><code>duplicate</code></a>方法完全相同。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             新的只读int缓冲区 
           </dd> 
          </dl> </li> 
        </ul> <a name="get--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>get</h4> <pre>public abstract&nbsp;int&nbsp;get()</pre> 
          <div class="block"> 
           <span>相对<i>获取</i>方法。</span> 
           <span>在此缓冲区的当前位置读取int，然后增加位置。</span> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             int在缓冲区的当前位置 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/nio/BufferUnderflowException.html" title="class in java.nio">BufferUnderflowException</a></code> - 如果缓冲区的当前位置不小于其限制 
           </dd> 
          </dl> </li> 
        </ul> <a name="put-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>put</h4> <pre>public abstract&nbsp;<a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a>&nbsp;put(int&nbsp;i)</pre> 
          <div class="block"> 
           <span>相对<i>放置</i>法<i>（可选操作）</i> 。</span> 
           <p> <span>将给定的int写入到当前位置的缓冲区中，然后增加位置。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>i</code> - 
            <code>i</code>的int 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             这个缓冲区 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/nio/BufferOverflowException.html" title="class in java.nio">BufferOverflowException</a></code> - 如果此缓冲区的当前位置不小于其限制 
           </dd> 
           <dd> 
            <code><a href="../../java/nio/ReadOnlyBufferException.html" title="class in java.nio">ReadOnlyBufferException</a></code> - 如果此缓冲区为只读 
           </dd> 
          </dl> </li> 
        </ul> <a name="get-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>get</h4> <pre>public abstract&nbsp;int&nbsp;get(int&nbsp;index)</pre> 
          <div class="block"> 
           <span>绝对<i>获取</i>方法。</span> 
           <span>读取给定索引的int。</span> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>index</code> - 从中读取的索引 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             在给定索引的int 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/IndexOutOfBoundsException.html" title="class in java.lang">IndexOutOfBoundsException</a></code> - 如果 
            <tt>index</tt>为负数或不小于缓冲区限制 
           </dd> 
          </dl> </li> 
        </ul> <a name="put-int-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>put</h4> <pre>public abstract&nbsp;<a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a>&nbsp;put(int&nbsp;index,
                              int&nbsp;i)</pre> 
          <div class="block"> 
           <span>绝对<i>put</i>方法<i>（可选操作）</i> 。</span> 
           <p> <span>将给定的int写入给定索引的缓冲区。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>index</code> - 将写入int的索引 
           </dd> 
           <dd> 
            <code>i</code> - 要写入的int值 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             这个缓冲区 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/IndexOutOfBoundsException.html" title="class in java.lang">IndexOutOfBoundsException</a></code> - 如果 
            <tt>index</tt>为负数或不小于缓冲区限制 
           </dd> 
           <dd> 
            <code><a href="../../java/nio/ReadOnlyBufferException.html" title="class in java.nio">ReadOnlyBufferException</a></code> - 如果此缓冲区是只读的 
           </dd> 
          </dl> </li> 
        </ul> <a name="get-int:A-int-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>get</h4> <pre>public&nbsp;<a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a>&nbsp;get(int[]&nbsp;dst,
                     int&nbsp;offset,
                     int&nbsp;length)</pre> 
          <div class="block"> 
           <span>相对批量<i>获取</i>方法。</span> 
           <p> <span>此方法将int从此缓冲区传输到给定的目标数组。</span> <span>如果缓冲区中剩余的内容少于满足请求所需的int，那么就不会<tt>传输</tt> <tt>任何</tt> <tt>内部文件</tt> ，并抛出一个<a href="../../java/nio/BufferUnderflowException.html" title="java.nio中的类"><code>BufferUnderflowException</code></a> ，否则，将<a href="../../java/nio/BufferUnderflowException.html" title="java.nio中的类">返回<code>BufferUnderflowException</code></a> 。</span> </p> 
           <p> <span>否则，该方法将<tt>length</tt> int从此缓冲区复制到给定的数组中，从该缓冲区的当前位置开始，并在数组中给定的偏移量。</span> <span>此缓冲区的位置然后增加<tt>length</tt> 。</span> </p> 
           <p> <span>换句话说，这种src.get(dst,&nbsp;off,&nbsp;len)形式的方法的<tt>调用</tt>与循环完全相同</span> </p> 
           <pre>  <span><code> for (int i = off; i &lt; off + len; i++) dst[i] = src.get(): </code></span> </pre> 
           <span>除了它首先检查这个缓冲区中是否有足够的int，并且它可能更有效率。</span> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>dst</code> - 要写入int的数组 
           </dd> 
           <dd> 
            <span><code>offset</code> - 要写入的第一个int的数组中的偏移量;</span> 
            <span>必须是非负数，不得大于<tt>dst.length</tt></span> 
           </dd> 
           <dd> 
            <span><code>length</code> - 要写入给定数组的最大int数;</span> 
            <span>必须是非负数，不得大于<tt>dst.length - offset</tt></span> 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             这个缓冲区 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/nio/BufferUnderflowException.html" title="class in java.nio">BufferUnderflowException</a></code> - 如果该缓冲区中剩余的内容不足 
            <tt>length</tt> 
           </dd> 
           <dd> 
            <code><a href="../../java/lang/IndexOutOfBoundsException.html" title="class in java.lang">IndexOutOfBoundsException</a></code> - 如果 
            <tt>offset</tt>和 
            <tt>length</tt>参数的前提条件不成立 
           </dd> 
          </dl> </li> 
        </ul> <a name="get-int:A-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>get</h4> <pre>public&nbsp;<a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a>&nbsp;get(int[]&nbsp;dst)</pre> 
          <div class="block"> 
           <span>相对批量<i>获取</i>方法。</span> 
           <p> <span>此方法将int从此缓冲区传输到给定的目标数组。</span> <span>调用此方法的形式为<tt>src.get(a)的</tt>行为方式与调用完全相同</span> </p> 
           <pre>  <span>src.get(a, 0, a.length)</span> </pre> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>dst</code> - 目的地阵列 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             这个缓冲区 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/nio/BufferUnderflowException.html" title="class in java.nio">BufferUnderflowException</a></code> - 如果此缓冲区中剩余的内容不足 
            <tt>length</tt> 
           </dd> 
          </dl> </li> 
        </ul> <a name="put-java.nio.IntBuffer-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>put</h4> <pre>public&nbsp;<a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a>&nbsp;put(<a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a>&nbsp;src)</pre> 
          <div class="block"> 
           <span>相对大容量<i>put</i>方法<i>（可选操作）</i> 。</span> 
           <p> <span>该方法将给定源缓冲区中剩余的int传输到此缓冲区。</span> <span>如果源缓冲区中剩余的内容多于此缓冲区，也就是说，如果<tt>src.remaining()</tt> <tt>&gt;</tt> <tt>remaining()</tt> ，则不会传输任何int，并抛出一个<a href="../../java/nio/BufferOverflowException.html" title="java.nio中的类"><code>BufferOverflowException</code></a> 。</span> </p> 
           <p> <span>否则，该方法将<i>n</i> = <tt>src.remaining()</tt> int从给定缓冲区复制到此缓冲区，从每个缓冲区的当前位置开始。</span> <span>然后将两个缓冲器的位置递增<i>n</i> 。</span> </p> 
           <p> <span>换句话说，调用此方法的形式<tt>dst.put(src)</tt>具有与循环完全相同的效果</span> </p> 
           <pre>  <span>while (src.hasRemaining())
         dst.put(src.get());</span> </pre> 
           <span>除了它首先检查这个缓冲区中是否有足够的空间，并且它可能更有效率。</span> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <span><code>src</code> - 要读取int的源缓冲区;</span> 
            <span>不能是这个缓冲区</span> 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             这个缓冲区 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/nio/BufferOverflowException.html" title="class in java.nio">BufferOverflowException</a></code> - 如果源缓冲区中剩余的int的缓冲区空间不足 
           </dd> 
           <dd> 
            <code><a href="../../java/lang/IllegalArgumentException.html" title="class in java.lang">IllegalArgumentException</a></code> - 如果源缓冲区是这个缓冲区 
           </dd> 
           <dd> 
            <code><a href="../../java/nio/ReadOnlyBufferException.html" title="class in java.nio">ReadOnlyBufferException</a></code> - 如果这个缓冲区是只读的 
           </dd> 
          </dl> </li> 
        </ul> <a name="put-int:A-int-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>put</h4> <pre>public&nbsp;<a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a>&nbsp;put(int[]&nbsp;src,
                     int&nbsp;offset,
                     int&nbsp;length)</pre> 
          <div class="block"> 
           <span>相对大容量<i>put</i>方法<i>（可选操作）</i> 。</span> 
           <p> <span>此方法将ints从给定的源数组传输到这个缓冲区。</span> <span>如果从数组中复制的内容多于保留在此缓冲区中的内容，也就是说，如果<tt>length</tt> <tt>&gt;</tt> <tt>remaining()</tt> ， <tt>则不</tt> <tt>传输</tt> int，并抛出<a href="../../java/nio/BufferOverflowException.html" title="java.nio中的类"><code>BufferOverflowException</code></a> 。</span> </p> 
           <p> <span>否则，该方法将<tt>length</tt> int从给定的数组复制到此缓冲区中，从阵列中的给定偏移量和此缓冲区的当前位置开始。</span> <span>此缓冲区的位置然后增加<tt>length</tt> 。</span> </p> 
           <p> <span>换句话说，调用此方法的形式<tt>dst.put(src,&nbsp;off,&nbsp;len)</tt>具有与循环完全相同的效果</span> </p> 
           <pre>  <span><code> for (int i = off; i &lt; off + len; i++) dst.put(a[i]); </code></span> </pre> 
           <span>除了它首先检查这个缓冲区中是否有足够的空间，并且它可能更有效率。</span> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>src</code> - 要读取int的数组 
           </dd> 
           <dd> 
            <span><code>offset</code> - 要读取的第一个int的数组中的偏移量;</span> 
            <span>必须是非负数，不得大于<tt>array.length</tt></span> 
           </dd> 
           <dd> 
            <span><code>length</code> - 要从给定数组读取的int数;</span> 
            <span>必须是非负数，不得大于<tt>array.length - offset</tt></span> 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             这个缓冲区 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/nio/BufferOverflowException.html" title="class in java.nio">BufferOverflowException</a></code> - 如果此缓冲区空间不足 
           </dd> 
           <dd> 
            <code><a href="../../java/lang/IndexOutOfBoundsException.html" title="class in java.lang">IndexOutOfBoundsException</a></code> - 如果 
            <tt>offset</tt>和 
            <tt>length</tt>参数的前提条件不成立 
           </dd> 
           <dd> 
            <code><a href="../../java/nio/ReadOnlyBufferException.html" title="class in java.nio">ReadOnlyBufferException</a></code> - 如果此缓冲区是只读的 
           </dd> 
          </dl> </li> 
        </ul> <a name="put-int:A-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>put</h4> <pre>public final&nbsp;<a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a>&nbsp;put(int[]&nbsp;src)</pre> 
          <div class="block"> 
           <span>相对大容量<i>put</i>方法<i>（可选操作）</i> 。</span> 
           <p> <span>此方法将给定源int数组的整个内容传输到此缓冲区。</span> <span>调用此方法的形式为<tt>dst.put(a)的</tt>行为方式与调用完全相同</span> </p> 
           <pre>  <span>dst.put(a, 0, a.length)</span> </pre> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>src</code> - 源数组 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             这个缓冲区 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/nio/BufferOverflowException.html" title="class in java.nio">BufferOverflowException</a></code> - 如果此缓冲区空间不足 
           </dd> 
           <dd> 
            <code><a href="../../java/nio/ReadOnlyBufferException.html" title="class in java.nio">ReadOnlyBufferException</a></code> - 如果此缓冲区是只读的 
           </dd> 
          </dl> </li> 
        </ul> <a name="hasArray--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>hasArray</h4> <pre>public final&nbsp;boolean&nbsp;hasArray()</pre> 
          <div class="block"> 
           <span>告诉这个缓冲区是否由可访问的int数组支持。</span> 
           <p> <span>如果此方法返回<tt>true，</tt>则可以安全地调用<a href="../../java/nio/IntBuffer.html#array--"><code>array</code></a>和<a href="../../java/nio/IntBuffer.html#arrayOffset--"><code>arrayOffset</code></a>方法。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">Specified by:</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/nio/Buffer.html#hasArray--">hasArray</a></code>在 
            <code><a href="../../java/nio/Buffer.html" title="class in java.nio">Buffer</a></code> 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd> 
            <tt>true</tt>如果且仅当此缓冲区由数组支持并且不是只读的 
           </dd> 
          </dl> </li> 
        </ul> <a name="array--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>array</h4> <pre>public final&nbsp;int[]&nbsp;array()</pre> 
          <div class="block"> 
           <span>返回支持此缓冲区的int数组<i>（可选操作）</i> 。</span> 
           <p> <span>对此缓冲区内容的修改将导致返回的数组的内容被修改，反之亦然。</span> </p> 
           <p> <span>在调用此方法之前调用<a href="../../java/nio/IntBuffer.html#hasArray--"><code>hasArray</code></a>方法，以确保此缓冲区具有可访问的后台阵列。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">Specified by:</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/nio/Buffer.html#array--">array</a></code>在 
            <code><a href="../../java/nio/Buffer.html" title="class in java.nio">Buffer</a></code> 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             支持这个缓冲区的数组 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/nio/ReadOnlyBufferException.html" title="class in java.nio">ReadOnlyBufferException</a></code> - 如果此缓冲区由数组支持但是只读 
           </dd> 
           <dd> 
            <code><a href="../../java/lang/UnsupportedOperationException.html" title="class in java.lang">UnsupportedOperationException</a></code> - 如果此缓冲区不由可访问阵列支持 
           </dd> 
          </dl> </li> 
        </ul> <a name="arrayOffset--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>arrayOffset</h4> <pre>public final&nbsp;int&nbsp;arrayOffset()</pre> 
          <div class="block"> 
           <span>返回该缓冲区的缓冲区的第一个元素的背衬数组中的偏移量<i>（可选操作）</i> 。</span> 
           <p> <span>如果此缓冲区由数组支持，则缓冲区<i>p</i>对应于数组索引<i>p</i> + <tt>arrayOffset()</tt> 。</span> </p> 
           <p> <span>在调用此方法之前调用<a href="../../java/nio/IntBuffer.html#hasArray--"><code>hasArray</code></a>方法，以确保此缓冲区具有可访问的后台阵列。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">Specified by:</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/nio/Buffer.html#arrayOffset--">arrayOffset</a></code>在 
            <code><a href="../../java/nio/Buffer.html" title="class in java.nio">Buffer</a></code> 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             缓冲区的第一个元素的缓冲区数组中的偏移量 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/nio/ReadOnlyBufferException.html" title="class in java.nio">ReadOnlyBufferException</a></code> - 如果此缓冲区由数组支持但是只读 
           </dd> 
           <dd> 
            <code><a href="../../java/lang/UnsupportedOperationException.html" title="class in java.lang">UnsupportedOperationException</a></code> - 如果此缓冲区不由可访问阵列支持 
           </dd> 
          </dl> </li> 
        </ul> <a name="compact--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>compact</h4> <pre>public abstract&nbsp;<a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a>&nbsp;compact()</pre> 
          <div class="block"> 
           <span><i>压缩</i>此缓冲区<i>（可选操作）</i> 。</span> 
           <p> <span>缓冲区当前位置与其限制（如果有的话）之间的int被复制到缓冲区的开头。</span> <span>也就是说，索引<i>p</i> = <tt>position()</tt>处的int被复制到索引零，索引<i>p</i> + 1处的int被复制到索引1，等等，直到索引<tt>limit()-1</tt>的int被复制到索引<i>n</i> = <tt>limit()</tt> - <tt>1</tt> - <i>p</i> 。</span> <span>然后将缓冲区的位置设置为<i>n + 1</i> ，并将其限制设置为其容量。</span> <span>标记如果被定义，则被丢弃。</span> </p> 
           <p> <span>缓冲区的位置设置为复制的int数，而不是为零，因此可以通过调用另一个相对<i>put</i>方法来立即调用此方法。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             这个缓冲区 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/nio/ReadOnlyBufferException.html" title="class in java.nio">ReadOnlyBufferException</a></code> - 如果此缓冲区是只读的 
           </dd> 
          </dl> </li> 
        </ul> <a name="isDirect--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>isDirect</h4> <pre>public abstract&nbsp;boolean&nbsp;isDirect()</pre> 
          <div class="block">
            告诉这个int缓冲区是否直接。 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">Specified by:</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/nio/Buffer.html#isDirect--">isDirect</a></code>在类 
            <code><a href="../../java/nio/Buffer.html" title="class in java.nio">Buffer</a></code> 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd> 
            <tt>true</tt>如果，只有这个缓冲区是直接的 
           </dd> 
          </dl> </li> 
        </ul> <a name="toString--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>toString</h4> <pre>public&nbsp;<a href="../../java/lang/String.html" title="class in java.lang">String</a>&nbsp;toString()</pre> 
          <div class="block">
            返回一个汇总此缓冲区状态的字符串。 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/Object.html#toString--">toString</a></code>在 
            <code><a href="../../java/lang/Object.html" title="class in java.lang">Object</a></code> 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             摘要字符串 
           </dd> 
          </dl> </li> 
        </ul> <a name="hashCode--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>hashCode</h4> <pre>public&nbsp;int&nbsp;hashCode()</pre> 
          <div class="block"> 
           <span>返回此缓冲区的当前哈希码。</span> 
           <p> <span>int缓冲区的哈希码仅取决于其剩余的元素;</span> <span>也就是说，元素从<tt>position()</tt>到，并包括元素在<tt>limit()</tt> - <tt>1</tt> 。</span> </p> 
           <p> <span>因为缓冲区哈希码是内容依赖的，所以使用缓冲区作为哈希映射或类似数据结构中的密钥是不合适的，除非知道它们的内容不会改变。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/Object.html#hashCode--">hashCode</a></code>在 
            <code><a href="../../java/lang/Object.html" title="class in java.lang">Object</a></code> 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             这个缓冲区的当前哈希码 
           </dd> 
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <a href="../../java/lang/Object.html#equals-java.lang.Object-"><code>Object.equals(java.lang.Object)</code></a> ， 
            <a href="../../java/lang/System.html#identityHashCode-java.lang.Object-"><code>System.identityHashCode(java.lang.Object)</code></a> 
           </dd> 
          </dl> </li> 
        </ul> <a name="equals-java.lang.Object-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>equals</h4> <pre>public&nbsp;boolean&nbsp;equals(<a href="../../java/lang/Object.html" title="class in java.lang">Object</a>&nbsp;ob)</pre> 
          <div class="block"> 
           <span>告诉这个缓冲区是否等于另一个对象。</span> 
           <p> <span>两个int缓冲区相等，如果只有</span> </p> 
           <ol> 
            <li><p> <span>它们具有相同的元素类型，</span> </p></li> 
            <li><p> <span>他们有相同数量的剩余元素，和</span> </p></li> 
            <li><p> <span>独立于其起始位置的剩余元素的两个序列是相等的。</span> </p></li> 
           </ol> 
           <p> <span>int缓冲区不等于任何其他类型的对象。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/Object.html#equals-java.lang.Object-">equals</a></code>在 
            <code><a href="../../java/lang/Object.html" title="class in java.lang">Object</a></code> 
           </dd> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>ob</code> - 要比较此缓冲区的对象 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd> 
            <tt>true</tt>如果，并且只有这个缓冲区等于给定的对象 
           </dd> 
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <span><a href="../../java/lang/Object.html#hashCode--"><code>Object.hashCode()</code></a> ， <a href="../../java/util/HashMap.html" title="java.util中的类"><code>HashMap</code></a></span> 
           </dd> 
          </dl> </li> 
        </ul> <a name="compareTo-java.nio.IntBuffer-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>compareTo</h4> <pre>public&nbsp;int&nbsp;compareTo(<a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a>&nbsp;that)</pre> 
          <div class="block"> 
           <span>将此缓冲区与另一个缓冲区进行比较。</span> 
           <p> <span>通过将词汇的剩余元素的序列进行比较来比较两个int缓冲区，而不考虑其相应缓冲区内每个序列的起始位置。</span> <span>对<code>int</code>元素进行比较，仿佛通过调用<a href="../../java/lang/Integer.html#compare-int-int-"><code>Integer.compare(int,int)</code></a> 。</span> </p> 
           <p> <span>int缓冲区不能与任何其他类型的对象相媲美。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">Specified by:</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/Comparable.html#compareTo-T-">compareTo</a></code>在接口 
            <code><a href="../../java/lang/Comparable.html" title="interface in java.lang">Comparable</a>&lt;<a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a>&gt;</code> 
           </dd> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>that</code> - 要比较的对象。 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             负整数，零或正整数，因为此缓冲区小于，等于或大于给定的缓冲区 
           </dd> 
          </dl> </li> 
        </ul> <a name="order--"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>order</h4> <pre>public abstract&nbsp;<a href="../../java/nio/ByteOrder.html" title="class in java.nio">ByteOrder</a>&nbsp;order()</pre> 
          <div class="block"> 
           <span>检索此缓冲区的字节顺序。</span> 
           <p> <span>通过分配或通过包装现有<tt>int</tt>阵列创建的int缓冲区的字节顺序是<a href="../../java/nio/ByteOrder.html#nativeOrder--"><code>native order</code></a>底层硬件。</span> <span>作为字节缓冲区的<a href="ByteBuffer.html#views">view</a>创建的int缓冲区的字节顺序是创建<a href="ByteBuffer.html#views">视图</a>时的字节缓冲区的字节顺序。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             这个缓冲区的字节顺序 
           </dd> 
          </dl> </li> 
        </ul> </li> 
      </ul> </li> 
    </ul> 
   </div> 
  </div>
<div class="contentContainer"> 
   <ul class="inheritance"> 
    <li><a href="../../java/lang/Object.html" title="class in java.lang">java.lang.Object</a></li> 
    <li> 
     <ul class="inheritance"> 
      <li>java.nio.Buffer</li> 
     </ul> </li> 
   </ul> 
   <div class="description"> 
    <ul class="blockList"> 
     <li class="blockList"> 
      <dl> 
       <dt>
        已知直接子类：
       </dt> 
       <dd> 
        <span><a href="../../java/nio/ByteBuffer.html" title="java.nio中的类">ByteBuffer</a> ， <a href="../../java/nio/CharBuffer.html" title="java.nio中的类">CharBuffer</a> ， <a href="../../java/nio/DoubleBuffer.html" title="java.nio中的类">DoubleBuffer</a> ， <a href="../../java/nio/FloatBuffer.html" title="java.nio中的类">FloatBuffer</a> ， <a href="../../java/nio/IntBuffer.html" title="java.nio中的类">IntBuffer</a> ， <a href="../../java/nio/LongBuffer.html" title="java.nio中的类">LongBuffer</a> ， <a href="../../java/nio/ShortBuffer.html" title="java.nio中的类">ShortBuffer</a></span> 
       </dd> 
      </dl> 
      <hr> <br> <pre>public abstract class <span class="typeNameLabel">Buffer</span>
extends <a href="../../java/lang/Object.html" title="class in java.lang">Object</a></pre> 
      <div class="block"> 
       <span>用于特定原始类型的数据的容器。</span> 
       <p> <span>缓冲器是特定原始类型的元素的线性有限序列。</span> <span>除了其内容，缓冲区的基本属性是其容量，限制和位置：</span> </p> 
       <blockquote> 
        <span><p> A buffer's <i>capacity</i> is the number of elements it contains. The capacity of a buffer is never negative and never changes. </p> <p> A buffer's <i>limit</i> is the index of the first element that should not be read or written. A buffer's limit is never negative and is never greater than its capacity. </p> <p> A buffer's <i>position</i> is the index of the next element to be read or written. A buffer's position is never negative and is never greater than its limit. </p></span> 
       </blockquote> 
       <p> <span>每个非布尔基元类型都有这个类的一个子类。</span> </p> 
       <h2> <span>传输数据</span> </h2> 
       <p> <span>该类的每个子类定义了两类<i>get</i>和<i>put</i>操作：</span> </p> 
       <blockquote> 
        <span><p> <i>Relative</i> operations read or write one or more elements starting at the current position and then increment the position by the number of elements transferred. If the requested transfer exceeds the limit then a relative <i>get</i> operation throws a <a href="../../java/nio/BufferUnderflowException.html" title="class in java.nio"><code>BufferUnderflowException</code></a> and a relative <i>put</i> operation throws a <a href="../../java/nio/BufferOverflowException.html" title="class in java.nio"><code>BufferOverflowException</code></a>; in either case, no data is transferred. </p> <p> <i>Absolute</i> operations take an explicit element index and do not affect the position. Absolute <i>get</i> and <i>put</i> operations throw an <a href="../../java/lang/IndexOutOfBoundsException.html" title="class in java.lang"><code>IndexOutOfBoundsException</code></a> if the index argument exceeds the limit. </p></span> 
       </blockquote> 
       <p> <span>当然，数据也可以通过相对于当前位置的相应通道的I / O操作被传送到或者从缓冲器传出。</span> </p> 
       <h2> <span>标记和重置</span> </h2> 
       <p> <span>当调用<a href="../../java/nio/Buffer.html#reset--"><code>reset</code></a>方法时，缓冲区的<i>标记</i>是其位置将被重置的索引。</span> <span>标记并不总是定义，但是当它被定义时，它不会是负的，并且永远不会大于位置。</span> <span>如果标记被定义，则当位置或极限被调整为小于标记的值时，它被丢弃。</span> <span>如果未定义标记，则调用<a href="../../java/nio/Buffer.html#reset--"><code>reset</code></a>方法将导致抛出<a href="../../java/nio/InvalidMarkException.html" title="java.nio中的类"><code>InvalidMarkException</code></a> 。</span> </p> 
       <h2> <span>不变量</span> </h2> 
       <p> <span>标记，位置，极限和容量值的以下不变量保持不变：</span> </p> 
       <blockquote> 
        <span><tt>0</tt> <tt>&lt;=</tt> <i>mark</i> <tt>&lt;=</tt> <i>position</i> <tt>&lt;=</tt> <i>limit</i> <tt>&lt;=</tt> <i>capacity</i></span> 
       </blockquote> 
       <p> <span>新创建的缓冲区始终具有零位置和未定义的标记。</span> <span>初始限制可以为零，或者可以是取决于缓冲器的类型和构造方式的某些其他值。</span> <span>新分配的缓冲区的每个元素被初始化为零。</span> </p> 
       <h2> <span>清理，翻转和倒带</span> </h2> 
       <p> <span>除了访问位置，限制和容量值以及标记和重置的方法之外，此类还定义了缓冲区上的以下操作：</span> </p> 
       <ul> 
        <li><p> <span><a href="../../java/nio/Buffer.html#clear--"><code>clear()</code></a>使缓冲区准备好信道读取或相对<i>放置</i>操作的一个新的序列：它设置了限制的能力和位置为零。</span> </p></li> 
        <li><p> <span><a href="../../java/nio/Buffer.html#flip--"><code>flip()</code></a>使缓冲区准备好新的通道写入或相对<i>获取操作</i>序列：它将限制设置为当前位置，然后将位置设置为零。</span> </p></li> 
        <li><p> <span><a href="../../java/nio/Buffer.html#rewind--"><code>rewind()</code></a>使缓冲区准备好重新读取已经包含的数据：它保持限制不变，并将位置设置为零。</span> </p></li> 
       </ul> 
       <h2> <span>只读缓冲区</span> </h2> 
       <p> <span>每个缓冲区都是可读的，但并不是每个缓冲区都是可写的。</span> <span>每个缓冲区类的变异方法被指定为<i>可选操作</i> ，当在只读缓冲区上调用时，它将抛出一个<a href="../../java/nio/ReadOnlyBufferException.html" title="java.nio中的类"><code>ReadOnlyBufferException</code></a> 。</span> <span>只读缓冲区不允许更改其内容，但其标记，位置和限制值是可变的。</span> <span>缓冲区是否为只读可以通过调用其<a href="../../java/nio/Buffer.html#isReadOnly--"><code>isReadOnly</code></a>方法来<a href="../../java/nio/Buffer.html#isReadOnly--">确定</a> 。</span> </p> 
       <h2> <span>线程安全</span> </h2> 
       <p> <span>缓冲区不能安全地被多个并发线程使用。</span> <span>如果一个缓冲区被多个线程使用，则应该通过适当的同步来控制对缓冲区的访问。</span> </p> 
       <h2> <span>调用链接</span> </h2> 
       <p> <span>指定此类中没有值返回值的方法返回调用它们的缓冲区。</span> <span>这允许方法调用被链接;</span> <span>例如，语句序列</span> </p> 
       <blockquote> 
        <span><pre> b.flip();
 b.position(23);
 b.limit(42);</pre></span> 
       </blockquote> 
       <span>可以由单一，更紧凑的语句替代</span> 
       <blockquote> 
        <span><pre> b.flip().position(23).limit(42);</pre></span> 
       </blockquote> 
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
          <span id="t4" class="tableTab"><span><a href="javascript:show(8);">具体的方法</a></span><span class="tabEnd">&nbsp;</span></span> 
         </caption> 
         <tbody> 
          <tr> 
           <th class="colFirst" scope="col">Modifier and Type</th> 
           <th class="colLast" scope="col">Method and Description</th> 
          </tr> 
          <tr id="i0" class="altColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/lang/Object.html" title="class in java.lang">Object</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/Buffer.html#array--">array</a></span>()</code> 
            <div class="block">
              返回支持此缓冲区的数组 
             <i>（可选操作）</i> 。 
            </div> </td> 
          </tr> 
          <tr id="i1" class="rowColor"> 
           <td class="colFirst"><code>abstract int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/Buffer.html#arrayOffset--">arrayOffset</a></span>()</code> 
            <div class="block">
              返回该缓冲区的缓冲区的第一个元素的背衬数组中的偏移量 
             <i>（可选操作）</i> 。 
            </div> </td> 
          </tr> 
          <tr id="i2" class="altColor"> 
           <td class="colFirst"><code>int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/Buffer.html#capacity--">capacity</a></span>()</code> 
            <div class="block">
              返回此缓冲区的容量。 
            </div> </td> 
          </tr> 
          <tr id="i3" class="rowColor"> 
           <td class="colFirst"><code><a href="../../java/nio/Buffer.html" title="class in java.nio">Buffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/Buffer.html#clear--">clear</a></span>()</code> 
            <div class="block">
              清除此缓冲区。 
            </div> </td> 
          </tr> 
          <tr id="i4" class="altColor"> 
           <td class="colFirst"><code><a href="../../java/nio/Buffer.html" title="class in java.nio">Buffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/Buffer.html#flip--">flip</a></span>()</code> 
            <div class="block">
              翻转这个缓冲区。 
            </div> </td> 
          </tr> 
          <tr id="i5" class="rowColor"> 
           <td class="colFirst"><code>abstract boolean</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/Buffer.html#hasArray--">hasArray</a></span>()</code> 
            <div class="block">
              告诉这个缓冲区是否由可访问的数组支持。 
            </div> </td> 
          </tr> 
          <tr id="i6" class="altColor"> 
           <td class="colFirst"><code>boolean</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/Buffer.html#hasRemaining--">hasRemaining</a></span>()</code> 
            <div class="block">
              告诉当前位置和极限之间是否存在任何元素。 
            </div> </td> 
          </tr> 
          <tr id="i7" class="rowColor"> 
           <td class="colFirst"><code>abstract boolean</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/Buffer.html#isDirect--">isDirect</a></span>()</code> 
            <div class="block">
              告诉这个缓冲区是否为 
             <a href="ByteBuffer.html#direct"><i>direct</i></a> 。 
            </div> </td> 
          </tr> 
          <tr id="i8" class="altColor"> 
           <td class="colFirst"><code>abstract boolean</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/Buffer.html#isReadOnly--">isReadOnly</a></span>()</code> 
            <div class="block">
              告知这个缓冲区是否是只读的。 
            </div> </td> 
          </tr> 
          <tr id="i9" class="rowColor"> 
           <td class="colFirst"><code>int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/Buffer.html#limit--">limit</a></span>()</code> 
            <div class="block">
              返回此缓冲区的限制。 
            </div> </td> 
          </tr> 
          <tr id="i10" class="altColor"> 
           <td class="colFirst"><code><a href="../../java/nio/Buffer.html" title="class in java.nio">Buffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/Buffer.html#limit-int-">limit</a></span>(int&nbsp;newLimit)</code> 
            <div class="block">
              设置此缓冲区的限制。 
            </div> </td> 
          </tr> 
          <tr id="i11" class="rowColor"> 
           <td class="colFirst"><code><a href="../../java/nio/Buffer.html" title="class in java.nio">Buffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/Buffer.html#mark--">mark</a></span>()</code> 
            <div class="block">
              将此缓冲区的标记设置在其位置。 
            </div> </td> 
          </tr> 
          <tr id="i12" class="altColor"> 
           <td class="colFirst"><code>int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/Buffer.html#position--">position</a></span>()</code> 
            <div class="block">
              返回此缓冲区的位置。 
            </div> </td> 
          </tr> 
          <tr id="i13" class="rowColor"> 
           <td class="colFirst"><code><a href="../../java/nio/Buffer.html" title="class in java.nio">Buffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/Buffer.html#position-int-">position</a></span>(int&nbsp;newPosition)</code> 
            <div class="block">
              设置这个缓冲区的位置。 
            </div> </td> 
          </tr> 
          <tr id="i14" class="altColor"> 
           <td class="colFirst"><code>int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/Buffer.html#remaining--">remaining</a></span>()</code> 
            <div class="block">
              返回当前位置和限制之间的元素数。 
            </div> </td> 
          </tr> 
          <tr id="i15" class="rowColor"> 
           <td class="colFirst"><code><a href="../../java/nio/Buffer.html" title="class in java.nio">Buffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/Buffer.html#reset--">reset</a></span>()</code> 
            <div class="block">
              将此缓冲区的位置重置为先前标记的位置。 
            </div> </td> 
          </tr> 
          <tr id="i16" class="altColor"> 
           <td class="colFirst"><code><a href="../../java/nio/Buffer.html" title="class in java.nio">Buffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/Buffer.html#rewind--">rewind</a></span>()</code> 
            <div class="block">
              倒带这个缓冲区。 
            </div> </td> 
          </tr> 
         </tbody> 
        </table> 
        <ul class="blockList"> 
         <li class="blockList"><a name="methods.inherited.from.class.java.lang.Object"> 
           <!--   --> </a> <h3>Methods inherited from class&nbsp;java.lang.<a href="../../java/lang/Object.html" title="class in java.lang">Object</a></h3> <code><a href="../../java/lang/Object.html#clone--">clone</a>, <a href="../../java/lang/Object.html#equals-java.lang.Object-">equals</a>, <a href="../../java/lang/Object.html#finalize--">finalize</a>, <a href="../../java/lang/Object.html#getClass--">getClass</a>, <a href="../../java/lang/Object.html#hashCode--">hashCode</a>, <a href="../../java/lang/Object.html#notify--">notify</a>, <a href="../../java/lang/Object.html#notifyAll--">notifyAll</a>, <a href="../../java/lang/Object.html#toString--">toString</a>, <a href="../../java/lang/Object.html#wait--">wait</a>, <a href="../../java/lang/Object.html#wait-long-">wait</a>, <a href="../../java/lang/Object.html#wait-long-int-">wait</a></code></li> 
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
         <!--   --> </a> <h3>方法详细信息</h3> <a name="capacity--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>capacity</h4> <pre>public final&nbsp;int&nbsp;capacity()</pre> 
          <div class="block">
            返回此缓冲区的容量。 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             这个缓冲区的容量 
           </dd> 
          </dl> </li> 
        </ul> <a name="position--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>position</h4> <pre>public final&nbsp;int&nbsp;position()</pre> 
          <div class="block">
            返回此缓冲区的位置。 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             这个缓冲区的位置 
           </dd> 
          </dl> </li> 
        </ul> <a name="position-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>position</h4> <pre>public final&nbsp;<a href="../../java/nio/Buffer.html" title="class in java.nio">Buffer</a>&nbsp;position(int&nbsp;newPosition)</pre> 
          <div class="block"> 
           <span>设置这个缓冲区的位置。</span> 
           <span>如果标记被定义并且大于新位置，则它被丢弃。</span> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <span><code>newPosition</code> - 新的位置值;</span> 
            <span>必须是非负数，不得大于当前限制</span> 
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
            <code><a href="../../java/lang/IllegalArgumentException.html" title="class in java.lang">IllegalArgumentException</a></code> - 如果newPosition的 
            <tt>前提条件</tt>不成立 
           </dd> 
          </dl> </li> 
        </ul> <a name="limit--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>limit</h4> <pre>public final&nbsp;int&nbsp;limit()</pre> 
          <div class="block">
            返回此缓冲区的限制。 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             这个缓冲区的极限 
           </dd> 
          </dl> </li> 
        </ul> <a name="limit-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>limit</h4> <pre>public final&nbsp;<a href="../../java/nio/Buffer.html" title="class in java.nio">Buffer</a>&nbsp;limit(int&nbsp;newLimit)</pre> 
          <div class="block"> 
           <span>设置此缓冲区的限制。</span> 
           <span>如果位置大于新的限制，那么它被设置为新的限制。</span> 
           <span>如果标记被定义并且大于新限制，则它被丢弃。</span> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <span><code>newLimit</code> - 新限制值;</span> 
            <span>必须是非负数，不大于此缓冲区的容量</span> 
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
            <code><a href="../../java/lang/IllegalArgumentException.html" title="class in java.lang">IllegalArgumentException</a></code> - 如果newLimit的 
            <tt>前提条件</tt>不成立 
           </dd> 
          </dl> </li> 
        </ul> <a name="mark--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>mark</h4> <pre>public final&nbsp;<a href="../../java/nio/Buffer.html" title="class in java.nio">Buffer</a>&nbsp;mark()</pre> 
          <div class="block">
            将此缓冲区的标记设置在其位置。 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             这个缓冲区 
           </dd> 
          </dl> </li> 
        </ul> <a name="reset--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>reset</h4> <pre>public final&nbsp;<a href="../../java/nio/Buffer.html" title="class in java.nio">Buffer</a>&nbsp;reset()</pre> 
          <div class="block"> 
           <span>将此缓冲区的位置重置为先前标记的位置。</span> 
           <p> <span>调用此方法既不会更改也不丢弃该标记的值。</span> </p> 
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
            <code><a href="../../java/nio/InvalidMarkException.html" title="class in java.nio">InvalidMarkException</a></code> - 如果标记尚未设置 
           </dd> 
          </dl> </li> 
        </ul> <a name="clear--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>clear</h4> <pre>public final&nbsp;<a href="../../java/nio/Buffer.html" title="class in java.nio">Buffer</a>&nbsp;clear()</pre> 
          <div class="block"> 
           <span>清除此缓冲区。</span> 
           <span>位置设置为零，限制设置为容量，标记被丢弃。</span> 
           <p> <span>在使用一系列通道读取或<i>放置</i>操作填充此缓冲区之前调用此方法。</span> <span>例如：</span> </p> 
           <blockquote> 
            <span><pre> buf.clear();     // Prepare buffer for reading
 in.read(buf);    // Read data</pre></span> 
           </blockquote> 
           <p> <span>这个方法实际上并不会清除缓冲区中的数据，但是它被命名为它的确是因为它最常用于情况也是如此。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             这个缓冲区 
           </dd> 
          </dl> </li> 
        </ul> <a name="flip--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>flip</h4> <pre>public final&nbsp;<a href="../../java/nio/Buffer.html" title="class in java.nio">Buffer</a>&nbsp;flip()</pre> 
          <div class="block"> 
           <span>翻转这个缓冲区。</span> 
           <span>该限制设置为当前位置，然后将该位置设置为零。</span> 
           <span>如果标记被定义，则它被丢弃。</span> 
           <p> <span>在通道读取或<i>放置</i>操作的序列之后，调用此方法来准备一系列通道写入或相对<i>获取</i>操作。</span> <span>例如：</span> </p> 
           <blockquote> 
            <span><pre> buf.put(magic);    // Prepend header
 in.read(buf);      // Read data into rest of buffer
 buf.flip();        // Flip buffer
 out.write(buf);    // Write header + data to channel</pre></span> 
           </blockquote> 
           <p> <span>当将数据从一个地方传输到另一个<a href="../../java/nio/ByteBuffer.html#compact--">地址</a>时，该方法通常与<a href="../../java/nio/ByteBuffer.html#compact--"><code>compact</code></a>方法结合使用。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             这个缓冲区 
           </dd> 
          </dl> </li> 
        </ul> <a name="rewind--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>rewind</h4> <pre>public final&nbsp;<a href="../../java/nio/Buffer.html" title="class in java.nio">Buffer</a>&nbsp;rewind()</pre> 
          <div class="block"> 
           <span>倒带这个缓冲区。</span> 
           <span>位置设置为零，标记被丢弃。</span> 
           <p> <span>在通道写入或<i>获取</i>操作的序列之前调用此方法，假设已经设置了相应的限制。</span> <span>例如：</span> </p> 
           <blockquote> 
            <span><pre> out.write(buf);    // Write remaining data
 buf.rewind();      // Rewind buffer
 buf.get(array);    // Copy data into array</pre></span> 
           </blockquote> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             这个缓冲区 
           </dd> 
          </dl> </li> 
        </ul> <a name="remaining--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>remaining</h4> <pre>public final&nbsp;int&nbsp;remaining()</pre> 
          <div class="block">
            返回当前位置和限制之间的元素数。 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             此缓冲区中剩余的元素数 
           </dd> 
          </dl> </li> 
        </ul> <a name="hasRemaining--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>hasRemaining</h4> <pre>public final&nbsp;boolean&nbsp;hasRemaining()</pre> 
          <div class="block">
            告诉当前位置和极限之间是否存在任何元素。 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd> 
            <tt>true</tt>如果，并且只有在此缓冲区中至少有一个元素 
           </dd> 
          </dl> </li> 
        </ul> <a name="isReadOnly--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>isReadOnly</h4> <pre>public abstract&nbsp;boolean&nbsp;isReadOnly()</pre> 
          <div class="block">
            告知这个缓冲区是否是只读的。 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd> 
            <tt>true</tt>如果，只有这个缓冲区是只读的 
           </dd> 
          </dl> </li> 
        </ul> <a name="hasArray--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>hasArray</h4> <pre>public abstract&nbsp;boolean&nbsp;hasArray()</pre> 
          <div class="block"> 
           <span>告诉这个缓冲区是否由可访问的数组支持。</span> 
           <p> <span>如果此方法返回<tt>true，</tt>则可以安全地调用<a href="../../java/nio/Buffer.html#array--"><code>array</code></a>和<a href="../../java/nio/Buffer.html#arrayOffset--"><code>arrayOffset</code></a>方法。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd> 
            <tt>true</tt>如果并且只有这个缓冲区由数组支持并且不是只读的 
           </dd> 
           <dt> 
            <span class="simpleTagLabel">从以下版本开始：</span> 
           </dt> 
           <dd>
             1.6 
           </dd> 
          </dl> </li> 
        </ul> <a name="array--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>array</h4> <pre>public abstract&nbsp;<a href="../../java/lang/Object.html" title="class in java.lang">Object</a>&nbsp;array()</pre> 
          <div class="block"> 
           <span>返回支持此缓冲区的数组<i>（可选操作）</i> 。</span> 
           <p> <span>该方法旨在使阵列支持的缓冲区更有效地传递到本地代码。</span> <span>具体的子类为此方法提供了更强类型的返回值。</span> </p> 
           <p> <span>对此缓冲区内容的修改将导致返回的数组的内容被修改，反之亦然。</span> </p> 
           <p> <span>在调用此方法之前调用<a href="../../java/nio/Buffer.html#hasArray--"><code>hasArray</code></a>方法，以确保此缓冲区具有可访问的后台阵列。</span> </p> 
          </div> 
          <dl> 
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
            <code><a href="../../java/lang/UnsupportedOperationException.html" title="class in java.lang">UnsupportedOperationException</a></code> - 如果此缓冲区未由可访问阵列支持 
           </dd> 
           <dt> 
            <span class="simpleTagLabel">从以下版本开始：</span> 
           </dt> 
           <dd>
             1.6 
           </dd> 
          </dl> </li> 
        </ul> <a name="arrayOffset--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>arrayOffset</h4> <pre>public abstract&nbsp;int&nbsp;arrayOffset()</pre> 
          <div class="block"> 
           <span>返回该缓冲区的缓冲区的第一个元素的背衬数组中的偏移量<i>（可选操作）</i> 。</span> 
           <p> <span>如果此缓冲区由数组支持，那么缓冲位置<i>p</i>对应于数组索引<i>p</i> + <tt>arrayOffset()</tt> 。</span> </p> 
           <p> <span>在调用此方法之前调用<a href="../../java/nio/Buffer.html#hasArray--"><code>hasArray</code></a>方法，以确保此缓冲区具有可访问的后备数组。</span> </p> 
          </div> 
          <dl> 
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
           <dt> 
            <span class="simpleTagLabel">从以下版本开始：</span> 
           </dt> 
           <dd>
             1.6 
           </dd> 
          </dl> </li> 
        </ul> <a name="isDirect--"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>isDirect</h4> <pre>public abstract&nbsp;boolean&nbsp;isDirect()</pre> 
          <div class="block">
            告诉这个缓冲区是否是 
           <a href="ByteBuffer.html#direct"><i>direct</i></a> 。 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd> 
            <tt>true</tt>如果，只有这个缓冲区是直接的 
           </dd> 
           <dt> 
            <span class="simpleTagLabel">从以下版本开始：</span> 
           </dt> 
           <dd>
             1.6 
           </dd> 
          </dl> </li> 
        </ul> </li> 
      </ul> </li> 
    </ul> 
   </div> 
  </div>
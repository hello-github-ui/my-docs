<div class="contentContainer"> 
   <ul class="inheritance"> 
    <li><a href="../../java/lang/Object.html" title="class in java.lang">java.lang.Object</a></li> 
    <li> 
     <ul class="inheritance"> 
      <li><a href="../../java/nio/Buffer.html" title="class in java.nio">java.nio.Buffer</a></li> 
      <li> 
       <ul class="inheritance"> 
        <li>java.nio.ByteBuffer</li> 
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
        <span><a href="../../java/lang/Comparable.html" title="java.lang中的接口">Comparable</a> &lt; <a href="../../java/nio/ByteBuffer.html" title="java.nio中的类">ByteBuffer</a> &gt;</span> 
       </dd> 
      </dl> 
      <dl> 
       <dt>
        已知直接子类：
       </dt> 
       <dd> 
        <span><a href="../../java/nio/MappedByteBuffer.html" title="java.nio中的类">MappedByteBuffer</a></span> 
       </dd> 
      </dl> 
      <hr> <br> <pre>public abstract class <span class="typeNameLabel">ByteBuffer</span>
extends <a href="../../java/nio/Buffer.html" title="class in java.nio">Buffer</a>
implements <a href="../../java/lang/Comparable.html" title="interface in java.lang">Comparable</a>&lt;<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&gt;</pre> 
      <div class="block"> 
       <span>一个字节缓冲区。</span> 
       <p> <span>这个类在字节缓冲区中定义了六类操作：</span> </p> 
       <ul> 
        <li><p> <span>绝对和相对<a href="../../java/nio/ByteBuffer.html#get--"><code><i>get</i></code></a>和<a href="../../java/nio/ByteBuffer.html#put-byte-"><code><i>put</i></code></a>读写单字节的方法;</span> </p></li> 
        <li><p> <span>相对<a href="../../java/nio/ByteBuffer.html#get-byte:A-"><code><i>bulk get</i></code></a>方法将连续的字节序列从该缓冲区传输到数组中;</span> </p></li> 
        <li><p> <span>相对<a href="../../java/nio/ByteBuffer.html#put-byte:A-"><code><i>bulk put</i></code></a>方法，将字节数组或其他字节缓冲区的连续字节序列传输到此缓冲区中;</span> </p></li> 
        <li><p> <span>绝对和相对<a href="../../java/nio/ByteBuffer.html#getChar--"><code><i>get</i></code></a>和<a href="../../java/nio/ByteBuffer.html#putChar-char-"><code><i>put</i></code></a>方法，读取和写入其他原始类型的值，将它们转换为特定字节顺序的字节序列;</span> </p></li> 
        <li><p> <span>用于创建<i><a href="#views">view buffers的</a></i>方法，其允许将字节缓冲器视为包含某些其他原始类型的值的缓冲器;</span> <span>和</span> </p></li> 
        <li><p> <span>方法<a href="../../java/nio/ByteBuffer.html#compact--"><code>compacting</code></a> ， <a href="../../java/nio/ByteBuffer.html#duplicate--"><code>duplicating</code></a>和<a href="../../java/nio/ByteBuffer.html#slice--"><code>slicing</code></a>一个字节的缓冲区。</span> </p></li> 
       </ul> 
       <p> <span>字节缓冲区可以由<a href="../../java/nio/ByteBuffer.html#allocate-int-"><code><i>allocation</i></code></a>创建，它为缓冲区的内容分配空间，或者通过<a href="../../java/nio/ByteBuffer.html#wrap-byte:A-"><code><i>wrapping</i></code></a>将现有的字节数组<a href="../../java/nio/ByteBuffer.html#wrap-byte:A-">分配</a>到缓冲区中。</span> <span><a name="direct"></a></span> </p> 
       <h2> <span>直接<i>与</i>非直接缓冲区</span> </h2> 
       <p> <span>字节缓冲区是<i>直接</i> <i>或非直接的</i> 。</span> <span>给定一个直接字节缓冲区，Java虚拟机将尽力在其上直接执行本地I / O操作。</span> <span>也就是说，它将尝试避免在每次调用其中一个底层操作系统的本机I / O操作之前（或之后）将缓冲区的内容复制到（或从）中间缓冲区。</span> </p> 
       <p> <span>可以通过调用<a href="../../java/nio/ByteBuffer.html#allocateDirect-int-">此类的<code>allocateDirect</code></a>工厂方法来创建直接字节缓冲区。</span> <span>此方法返回的缓冲区通常比非直接缓冲区具有更高的分配和释放成本。</span> <span>直接缓冲区的内容可能驻留在正常的垃圾回收堆之外，因此它们对应用程序的内存占用的影响可能不明显。</span> <span>因此，建议直接缓冲区主要用于受基础系统本机I / O操作影响的大型长寿命缓冲区。</span> <span>一般来说，最好只在产生程序性能可测量的增益时才分配直接缓冲区。</span> </p> 
       <p> <span>直接字节缓冲区也可以由文件的<a href="../../java/nio/channels/FileChannel.html#map-java.nio.channels.FileChannel.MapMode-long-long-"><code>mapping</code></a>直接创建到内存区域。</span> <span>Java平台的实现可以可选地支持通过JNI从本地代码创建直接字节缓冲器。</span> <span>如果这些缓冲区之一的实例指的是存储器的不可访问的区域，则访问该区域的尝试将不会改变缓冲区的内容，并且将导致在访问时或之后的某个未指定的异常时间。</span> </p> 
       <p> <span>字节缓冲区是直接还是非直接可以通过调用其<a href="../../java/nio/ByteBuffer.html#isDirect--"><code>isDirect</code></a>方法来<a href="../../java/nio/ByteBuffer.html#isDirect--">确定</a> 。</span> <span>提供了这种方法，使得可以在性能关键代码中进行显式缓冲区管理。</span> <span><a name="bin"></a></span> </p> 
       <h2> <span>访问二进制数据</span> </h2> 
       <p> <span>该类定义了用于读取和写入所有其他原始类型的值的方法，但<tt>boolean</tt>除外。</span> <span>原始值根据缓冲区的当前字节顺序转换为（或从）字节序列，可以通过<a href="../../java/nio/ByteBuffer.html#order--"><code>order</code></a>方法检索和修改。</span> <span>特定字节顺序由<a href="../../java/nio/ByteOrder.html" title="java.nio中的类"><code>ByteOrder</code></a>类的实例表示。</span> <span>字节缓冲区的初始顺序始终为<a href="../../java/nio/ByteOrder.html#BIG_ENDIAN"><code>BIG_ENDIAN</code></a> 。</span> </p> 
       <p> <span>对于访问异构二进制数据，即不同类型的值序列，该类定义了每个类型的绝对和相对<i>get</i>和<i>put</i>方法族。</span> <span>例如，对于32位浮点值，此类定义：</span> </p> 
       <blockquote> 
        <span><pre> float  <a href="../../java/nio/ByteBuffer.html#getFloat--"><code>getFloat()</code></a>
 float  <a href="../../java/nio/ByteBuffer.html#getFloat-int-"><code>getFloat(int index)</code></a>
  void  <a href="../../java/nio/ByteBuffer.html#putFloat-float-"><code>putFloat(float f)</code></a>
  void  <a href="../../java/nio/ByteBuffer.html#putFloat-int-float-"><code>putFloat(int index, float f)</code></a></pre></span> 
       </blockquote> 
       <p> <span>相应的方法被用于类型<tt><tt><tt><tt>char，short，int，long</tt></tt></tt></tt>和<tt>double</tt>限定。</span> <span>绝对<i>get</i>和<i>put</i>方法的索引参数是以字节为单位，而不是读取或写入的类型。</span> <span><a name="views"></a></span> </p> 
       <p> <span>对于访问同构二进制数据，即相同类型的值的序列，此类定义可以创建给定字节缓冲区的<i>视图</i>的方法。</span> <span><i>视图缓冲区</i>只是另一个缓冲区，其内容由字节缓冲区支持。</span> <span>对字节缓冲区内容的更改将在视图缓冲区中可见，反之亦然;</span> <span>两个缓冲区的位置，极限和标记值是独立的。</span> <span>例如， <a href="../../java/nio/ByteBuffer.html#asFloatBuffer--"><code>asFloatBuffer</code></a>方法创建了由调用该方法的字节缓冲区支持的<a href="../../java/nio/FloatBuffer.html" title="java.nio中的类"><code>FloatBuffer</code></a>类的实例。</span> <span>相应的视图创建方法的各类<tt><tt><tt><tt>char，short，int，long</tt></tt></tt></tt>和<tt>double</tt>限定。</span> </p> 
       <p> <span>与上述类型特定的<i>get</i>和<i>put</i>方法相比，查看缓冲区有三个重要的优点：</span> </p> 
       <ul> 
        <li><p> <span>视图缓冲区的索引不是以字节为单位，而是根据其值的类型特定大小;</span> </p></li> 
        <li><p> <span>视图缓冲器提供相对的批量<i>获取</i>和<i>放置</i>方法，该方法可以在缓冲区和数组之间传递连续序列值或者相同类型的其他缓冲区;</span> <span>和</span> </p></li> 
        <li><p> <span>视图缓冲区可能会更有效率，因为只有当它的后备字节缓冲区是直接的时才是直接的。</span> </p></li> 
       </ul> 
       <p> <span>在创建视图时，视图缓冲区的字节顺序被固定为其字节缓冲区的字节顺序。</span> </p> 
       <h2> <span>调用链接</span> </h2> 
       <p> <span>指定此类中没有值返回值的方法返回调用它们的缓冲区。</span> <span>这允许方法调用被链接。</span> <span>语句序列</span> </p> 
       <blockquote> 
        <span><pre> bb.putInt(0xCAFEBABE);
 bb.putShort(3);
 bb.putShort(45);</pre></span> 
       </blockquote> 
       <span>例如，可以用单个语句来替换</span> 
       <blockquote> 
        <span><pre> bb.putInt(0xCAFEBABE).putShort(3).putShort(45);</pre></span> 
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
           <td class="colFirst"><code>static <a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#allocate-int-">allocate</a></span>(int&nbsp;capacity)</code> 
            <div class="block">
              分配一个新的字节缓冲区。 
            </div> </td> 
          </tr> 
          <tr id="i1" class="rowColor"> 
           <td class="colFirst"><code>static <a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#allocateDirect-int-">allocateDirect</a></span>(int&nbsp;capacity)</code> 
            <div class="block">
              分配一个新的直接字节缓冲区。 
            </div> </td> 
          </tr> 
          <tr id="i2" class="altColor"> 
           <td class="colFirst"><code>byte[]</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#array--">array</a></span>()</code> 
            <div class="block">
              返回支持此缓冲区的字节数组 
             <i>（可选操作）</i> 。 
            </div> </td> 
          </tr> 
          <tr id="i3" class="rowColor"> 
           <td class="colFirst"><code>int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#arrayOffset--">arrayOffset</a></span>()</code> 
            <div class="block">
              返回该缓冲区的缓冲区的第一个元素的背衬数组中的偏移量 
             <i>（可选操作）</i> 。 
            </div> </td> 
          </tr> 
          <tr id="i4" class="altColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/nio/CharBuffer.html" title="class in java.nio">CharBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#asCharBuffer--">asCharBuffer</a></span>()</code> 
            <div class="block">
              创建一个字节缓冲区作为char缓冲区的视图。 
            </div> </td> 
          </tr> 
          <tr id="i5" class="rowColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/nio/DoubleBuffer.html" title="class in java.nio">DoubleBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#asDoubleBuffer--">asDoubleBuffer</a></span>()</code> 
            <div class="block">
              将此字节缓冲区的视图创建为双缓冲区。 
            </div> </td> 
          </tr> 
          <tr id="i6" class="altColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/nio/FloatBuffer.html" title="class in java.nio">FloatBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#asFloatBuffer--">asFloatBuffer</a></span>()</code> 
            <div class="block">
              将此字节缓冲区的视图创建为浮动缓冲区。 
            </div> </td> 
          </tr> 
          <tr id="i7" class="rowColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#asIntBuffer--">asIntBuffer</a></span>()</code> 
            <div class="block">
              将此字节缓冲区的视图创建为int缓冲区。 
            </div> </td> 
          </tr> 
          <tr id="i8" class="altColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/nio/LongBuffer.html" title="class in java.nio">LongBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#asLongBuffer--">asLongBuffer</a></span>()</code> 
            <div class="block">
              将此字节缓冲区的视图创建为长缓冲区。 
            </div> </td> 
          </tr> 
          <tr id="i9" class="rowColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#asReadOnlyBuffer--">asReadOnlyBuffer</a></span>()</code> 
            <div class="block">
              创建一个新的只读字节缓冲区，共享此缓冲区的内容。 
            </div> </td> 
          </tr> 
          <tr id="i10" class="altColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/nio/ShortBuffer.html" title="class in java.nio">ShortBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#asShortBuffer--">asShortBuffer</a></span>()</code> 
            <div class="block">
              将此字节缓冲区的视图创建为短缓冲区。 
            </div> </td> 
          </tr> 
          <tr id="i11" class="rowColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#compact--">compact</a></span>()</code> 
            <div class="block"> 
             <i>压缩</i>此缓冲区 
             <i>（可选操作）</i> 。 
            </div> </td> 
          </tr> 
          <tr id="i12" class="altColor"> 
           <td class="colFirst"><code>int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#compareTo-java.nio.ByteBuffer-">compareTo</a></span>(<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;that)</code> 
            <div class="block">
              将此缓冲区与另一个缓冲区进行比较。 
            </div> </td> 
          </tr> 
          <tr id="i13" class="rowColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#duplicate--">duplicate</a></span>()</code> 
            <div class="block">
              创建一个新的字节缓冲区，共享此缓冲区的内容。 
            </div> </td> 
          </tr> 
          <tr id="i14" class="altColor"> 
           <td class="colFirst"><code>boolean</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#equals-java.lang.Object-">equals</a></span>(<a href="../../java/lang/Object.html" title="class in java.lang">Object</a>&nbsp;ob)</code> 
            <div class="block">
              告诉这个缓冲区是否等于另一个对象。 
            </div> </td> 
          </tr> 
          <tr id="i15" class="rowColor"> 
           <td class="colFirst"><code>abstract byte</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#get--">get</a></span>()</code> 
            <div class="block">
              相对 
             <i>获取</i>方法。 
            </div> </td> 
          </tr> 
          <tr id="i16" class="altColor"> 
           <td class="colFirst"><code><a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#get-byte:A-">get</a></span>(byte[]&nbsp;dst)</code> 
            <div class="block">
              相对批量 
             <i>获取</i>方法。 
            </div> </td> 
          </tr> 
          <tr id="i17" class="rowColor"> 
           <td class="colFirst"><code><a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#get-byte:A-int-int-">get</a></span>(byte[]&nbsp;dst, int&nbsp;offset, int&nbsp;length)</code> 
            <div class="block">
              相对批量 
             <i>获取</i>方法。 
            </div> </td> 
          </tr> 
          <tr id="i18" class="altColor"> 
           <td class="colFirst"><code>abstract byte</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#get-int-">get</a></span>(int&nbsp;index)</code> 
            <div class="block">
              绝对 
             <i>获取</i>方法。 
            </div> </td> 
          </tr> 
          <tr id="i19" class="rowColor"> 
           <td class="colFirst"><code>abstract char</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#getChar--">getChar</a></span>()</code> 
            <div class="block">
              读取char值的相对 
             <i>get</i>方法。 
            </div> </td> 
          </tr> 
          <tr id="i20" class="altColor"> 
           <td class="colFirst"><code>abstract char</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#getChar-int-">getChar</a></span>(int&nbsp;index)</code> 
            <div class="block">
              绝对 
             <i>获取</i>方法来读取一个char值。 
            </div> </td> 
          </tr> 
          <tr id="i21" class="rowColor"> 
           <td class="colFirst"><code>abstract double</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#getDouble--">getDouble</a></span>()</code> 
            <div class="block">
              读取双重值的相对 
             <i>get</i>方法。 
            </div> </td> 
          </tr> 
          <tr id="i22" class="altColor"> 
           <td class="colFirst"><code>abstract double</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#getDouble-int-">getDouble</a></span>(int&nbsp;index)</code> 
            <div class="block">
              绝对 
             <i>获取</i>读取双重值的方法。 
            </div> </td> 
          </tr> 
          <tr id="i23" class="rowColor"> 
           <td class="colFirst"><code>abstract float</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#getFloat--">getFloat</a></span>()</code> 
            <div class="block">
              读取浮点值的相对 
             <i>get</i>方法。 
            </div> </td> 
          </tr> 
          <tr id="i24" class="altColor"> 
           <td class="colFirst"><code>abstract float</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#getFloat-int-">getFloat</a></span>(int&nbsp;index)</code> 
            <div class="block">
              用于读取浮点值的绝对 
             <i>get</i>方法。 
            </div> </td> 
          </tr> 
          <tr id="i25" class="rowColor"> 
           <td class="colFirst"><code>abstract int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#getInt--">getInt</a></span>()</code> 
            <div class="block">
              用于读取int值的相对 
             <i>get</i>方法。 
            </div> </td> 
          </tr> 
          <tr id="i26" class="altColor"> 
           <td class="colFirst"><code>abstract int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#getInt-int-">getInt</a></span>(int&nbsp;index)</code> 
            <div class="block">
              用于读取int值的绝对 
             <i>get</i>方法。 
            </div> </td> 
          </tr> 
          <tr id="i27" class="rowColor"> 
           <td class="colFirst"><code>abstract long</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#getLong--">getLong</a></span>()</code> 
            <div class="block">
              读取长值的相对 
             <i>get</i>方法。 
            </div> </td> 
          </tr> 
          <tr id="i28" class="altColor"> 
           <td class="colFirst"><code>abstract long</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#getLong-int-">getLong</a></span>(int&nbsp;index)</code> 
            <div class="block">
              绝对 
             <i>获取</i>读取长值的方法。 
            </div> </td> 
          </tr> 
          <tr id="i29" class="rowColor"> 
           <td class="colFirst"><code>abstract short</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#getShort--">getShort</a></span>()</code> 
            <div class="block">
              相对 
             <i>获取</i>方法读取一个简短的值。 
            </div> </td> 
          </tr> 
          <tr id="i30" class="altColor"> 
           <td class="colFirst"><code>abstract short</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#getShort-int-">getShort</a></span>(int&nbsp;index)</code> 
            <div class="block">
              绝对 
             <i>获取</i>读取一个简短值的方法。 
            </div> </td> 
          </tr> 
          <tr id="i31" class="rowColor"> 
           <td class="colFirst"><code>boolean</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#hasArray--">hasArray</a></span>()</code> 
            <div class="block">
              告诉这个缓冲区是否由可访问的字节数组支持。 
            </div> </td> 
          </tr> 
          <tr id="i32" class="altColor"> 
           <td class="colFirst"><code>int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#hashCode--">hashCode</a></span>()</code> 
            <div class="block">
              返回此缓冲区的当前哈希码。 
            </div> </td> 
          </tr> 
          <tr id="i33" class="rowColor"> 
           <td class="colFirst"><code>abstract boolean</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#isDirect--">isDirect</a></span>()</code> 
            <div class="block">
              告诉这个字节缓冲区是否是直接的。 
            </div> </td> 
          </tr> 
          <tr id="i34" class="altColor"> 
           <td class="colFirst"><code><a href="../../java/nio/ByteOrder.html" title="class in java.nio">ByteOrder</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#order--">order</a></span>()</code> 
            <div class="block">
              检索此缓冲区的字节顺序。 
            </div> </td> 
          </tr> 
          <tr id="i35" class="rowColor"> 
           <td class="colFirst"><code><a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#order-java.nio.ByteOrder-">order</a></span>(<a href="../../java/nio/ByteOrder.html" title="class in java.nio">ByteOrder</a>&nbsp;bo)</code> 
            <div class="block">
              修改缓冲区的字节顺序。 
            </div> </td> 
          </tr> 
          <tr id="i36" class="altColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#put-byte-">put</a></span>(byte&nbsp;b)</code> 
            <div class="block">
              相对 
             <i>放置</i>法 
             <i>（可选操作）</i> 。 
            </div> </td> 
          </tr> 
          <tr id="i37" class="rowColor"> 
           <td class="colFirst"><code><a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#put-byte:A-">put</a></span>(byte[]&nbsp;src)</code> 
            <div class="block">
              相对大容量 
             <i>put</i>方法 
             <i>（可选操作）</i> 。 
            </div> </td> 
          </tr> 
          <tr id="i38" class="altColor"> 
           <td class="colFirst"><code><a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#put-byte:A-int-int-">put</a></span>(byte[]&nbsp;src, int&nbsp;offset, int&nbsp;length)</code> 
            <div class="block">
              相对大容量 
             <i>put</i>方法 
             <i>（可选操作）</i> 。 
            </div> </td> 
          </tr> 
          <tr id="i39" class="rowColor"> 
           <td class="colFirst"><code><a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#put-java.nio.ByteBuffer-">put</a></span>(<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;src)</code> 
            <div class="block">
              相对大容量 
             <i>put</i>方法 
             <i>（可选操作）</i> 。 
            </div> </td> 
          </tr> 
          <tr id="i40" class="altColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#put-int-byte-">put</a></span>(int&nbsp;index, byte&nbsp;b)</code> 
            <div class="block">
              绝对 
             <i>put</i>方法 
             <i>（可选操作）</i> 。 
            </div> </td> 
          </tr> 
          <tr id="i41" class="rowColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#putChar-char-">putChar</a></span>(char&nbsp;value)</code> 
            <div class="block">
              写入char值的相对 
             <i>put</i>方法 
             <i>（可选操作）</i> 。 
            </div> </td> 
          </tr> 
          <tr id="i42" class="altColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#putChar-int-char-">putChar</a></span>(int&nbsp;index, char&nbsp;value)</code> 
            <div class="block">
              用于写入char值的绝对 
             <i>put</i>方法 
             <i>（可选操作）</i> 。 
            </div> </td> 
          </tr> 
          <tr id="i43" class="rowColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#putDouble-double-">putDouble</a></span>(double&nbsp;value)</code> 
            <div class="block">
              写入double值的相对 
             <i>put</i>方法 
             <i>（可选操作）</i> 。 
            </div> </td> 
          </tr> 
          <tr id="i44" class="altColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#putDouble-int-double-">putDouble</a></span>(int&nbsp;index, double&nbsp;value)</code> 
            <div class="block">
              用于写入双精度值的绝对 
             <i>put</i>方法 
             <i>（可选操作）</i> 。 
            </div> </td> 
          </tr> 
          <tr id="i45" class="rowColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#putFloat-float-">putFloat</a></span>(float&nbsp;value)</code> 
            <div class="block">
              编写浮点值的相对 
             <i>put</i>方法 
             <i>（可选操作）</i> 。 
            </div> </td> 
          </tr> 
          <tr id="i46" class="altColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#putFloat-int-float-">putFloat</a></span>(int&nbsp;index, float&nbsp;value)</code> 
            <div class="block">
              用于写入浮点值的绝对 
             <i>put</i>方法 
             <i>（可选操作）</i> 。 
            </div> </td> 
          </tr> 
          <tr id="i47" class="rowColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#putInt-int-">putInt</a></span>(int&nbsp;value)</code> 
            <div class="block">
              编写int值的相对 
             <i>put</i>方法 
             <i>（可选操作）</i> 。 
            </div> </td> 
          </tr> 
          <tr id="i48" class="altColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#putInt-int-int-">putInt</a></span>(int&nbsp;index, int&nbsp;value)</code> 
            <div class="block">
              用于写入int值的绝对 
             <i>put</i>方法 
             <i>（可选操作）</i> 。 
            </div> </td> 
          </tr> 
          <tr id="i49" class="rowColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#putLong-int-long-">putLong</a></span>(int&nbsp;index, long&nbsp;value)</code> 
            <div class="block">
              绝对 
             <i>put</i>方法写入一个长的值 
             <i>（可选操作）</i> 。 
            </div> </td> 
          </tr> 
          <tr id="i50" class="altColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#putLong-long-">putLong</a></span>(long&nbsp;value)</code> 
            <div class="block">
              写入长值的相对 
             <i>put</i>方法 
             <i>（可选操作）</i> 。 
            </div> </td> 
          </tr> 
          <tr id="i51" class="rowColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#putShort-int-short-">putShort</a></span>(int&nbsp;index, short&nbsp;value)</code> 
            <div class="block">
              绝对 
             <i>put</i>方法写入一个简短的值 
             <i>（可选操作）</i> 。 
            </div> </td> 
          </tr> 
          <tr id="i52" class="altColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#putShort-short-">putShort</a></span>(short&nbsp;value)</code> 
            <div class="block">
              写入一个短值的相对 
             <i>放置</i>方法 
             <i>（可选操作）</i> 。 
            </div> </td> 
          </tr> 
          <tr id="i53" class="rowColor"> 
           <td class="colFirst"><code>abstract <a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#slice--">slice</a></span>()</code> 
            <div class="block">
              创建一个新的字节缓冲区，其内容是此缓冲区内容的共享子序列。 
            </div> </td> 
          </tr> 
          <tr id="i54" class="altColor"> 
           <td class="colFirst"><code><a href="../../java/lang/String.html" title="class in java.lang">String</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#toString--">toString</a></span>()</code> 
            <div class="block">
              返回一个汇总此缓冲区状态的字符串。 
            </div> </td> 
          </tr> 
          <tr id="i55" class="rowColor"> 
           <td class="colFirst"><code>static <a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#wrap-byte:A-">wrap</a></span>(byte[]&nbsp;array)</code> 
            <div class="block">
              将一个字节数组包装到缓冲区中。 
            </div> </td> 
          </tr> 
          <tr id="i56" class="altColor"> 
           <td class="colFirst"><code>static <a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteBuffer.html#wrap-byte:A-int-int-">wrap</a></span>(byte[]&nbsp;array, int&nbsp;offset, int&nbsp;length)</code> 
            <div class="block">
              将一个字节数组包装到缓冲区中。 
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
         <!--   --> </a> <h3>方法详细信息</h3> <a name="allocateDirect-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>allocateDirect</h4> <pre>public static&nbsp;<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;allocateDirect(int&nbsp;capacity)</pre> 
          <div class="block"> 
           <span>分配一个新的直接字节缓冲区。</span> 
           <p> <span>新缓冲区的位置将为零，其限制将为其容量，其标记将不定义，并且其每个元素将被初始化为零。</span> <span>是否有一个<a href="../../java/nio/ByteBuffer.html#hasArray--"><code>backing array</code></a>是未指定的。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>capacity</code> - 新的缓冲区的容量，以字节为单位 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             新的字节缓冲区 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/IllegalArgumentException.html" title="class in java.lang">IllegalArgumentException</a></code> - 如果 
            <tt>capacity</tt>是负整数 
           </dd> 
          </dl> </li> 
        </ul> <a name="allocate-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>allocate</h4> <pre>public static&nbsp;<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;allocate(int&nbsp;capacity)</pre> 
          <div class="block"> 
           <span>分配一个新的字节缓冲区。</span> 
           <p> <span>新缓冲区的位置将为零，其限制将为其容量，其标记将不定义，并且其每个元素将被初始化为零。</span> <span>它将有一个<a href="../../java/nio/ByteBuffer.html#array--"><code>backing array</code></a> ，其<a href="../../java/nio/ByteBuffer.html#arrayOffset--"><code>array offset</code></a>将为零。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>capacity</code> - 新的缓冲区的容量，以字节为单位 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             新的字节缓冲区 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/IllegalArgumentException.html" title="class in java.lang">IllegalArgumentException</a></code> - 如果 
            <tt>capacity</tt>是负整数 
           </dd> 
          </dl> </li> 
        </ul> <a name="wrap-byte:A-int-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>wrap</h4> <pre>public static&nbsp;<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;wrap(byte[]&nbsp;array,
                              int&nbsp;offset,
                              int&nbsp;length)</pre> 
          <div class="block"> 
           <span>将一个字节数组包装到缓冲区中。</span> 
           <p> <span>新的缓冲区将由给定的字节数组支持;</span> <span>也就是说，对缓冲区的修改将导致数组被修改，反之亦然。</span> <span>新增的缓冲区容量将为<tt>array.length</tt> ，其位置将为<tt>offset</tt> ，其限制将为<tt>offset + length</tt> ，其标志将不明确。</span> <span>它的<a href="../../java/nio/ByteBuffer.html#array--"><code>backing array</code></a>将是给定的数组，其<a href="../../java/nio/ByteBuffer.html#arrayOffset--"><code>array offset</code></a>将为零。</span> </p> 
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
             新的字节缓冲区 
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
        </ul> <a name="wrap-byte:A-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>wrap</h4> <pre>public static&nbsp;<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;wrap(byte[]&nbsp;array)</pre> 
          <div class="block"> 
           <span>将一个字节数组包装到缓冲区中。</span> 
           <p> <span>新的缓冲区将由给定的字节数组支持;</span> <span>也就是说，对缓冲区的修改将导致数组被修改，反之亦然。</span> <span>新缓冲区的容量和限制将为<tt>array.length</tt> ，其位置将为零，其标志将不确定。</span> <span>其<a href="../../java/nio/ByteBuffer.html#array--"><code>backing array</code></a>将是给定的数组，其<a href="../../java/nio/ByteBuffer.html#arrayOffset--"><code>array offset&gt;</code></a>将为零。</span> </p> 
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
             新的字节缓冲区 
           </dd> 
          </dl> </li> 
        </ul> <a name="slice--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>slice</h4> <pre>public abstract&nbsp;<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;slice()</pre> 
          <div class="block"> 
           <span>创建一个新的字节缓冲区，其内容是此缓冲区内容的共享子序列。</span> 
           <p> <span>新缓冲区的内容将从此缓冲区的当前位置开始。</span> <span>对这个缓冲区内容的更改将在新的缓冲区中可见，反之亦然;</span> <span>两个缓冲区的位置，极限和标记值将是独立的。</span> </p> 
           <p> <span>新缓冲区的位置将为零，其容量和限制将是此缓冲区中剩余的字节数，其标记将不定义。</span> <span>如果只有这个缓冲区是直接的，并且只有当这个缓冲区是只读的时，这个缓冲区将是只读的。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             新的字节缓冲区 
           </dd> 
          </dl> </li> 
        </ul> <a name="duplicate--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>duplicate</h4> <pre>public abstract&nbsp;<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;duplicate()</pre> 
          <div class="block"> 
           <span>创建一个新的字节缓冲区，共享此缓冲区的内容。</span> 
           <p> <span>新缓冲区的内容将是这个缓冲区的内容。</span> <span>对这个缓冲区内容的更改将在新的缓冲区中可见，反之亦然;</span> <span>两个缓冲区的位置，极限和标记值将是独立的。</span> </p> 
           <p> <span>新缓冲区的容量，限制，位置和标记值将与此缓冲区的容量，限制，位置和标记值相同。</span> <span>如果只有这个缓冲区是直接的，并且只有当这个缓冲区是只读的时，这个缓冲区将是只读的。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             新的字节缓冲区 
           </dd> 
          </dl> </li> 
        </ul> <a name="asReadOnlyBuffer--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>asReadOnlyBuffer</h4> <pre>public abstract&nbsp;<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;asReadOnlyBuffer()</pre> 
          <div class="block"> 
           <span>创建一个新的只读字节缓冲区，共享此缓冲区的内容。</span> 
           <p> <span>新缓冲区的内容将是这个缓冲区的内容。</span> <span>这个缓冲区内容的更改将在新的缓冲区中显示;</span> <span>然而，新的缓冲区本身将是只读的，不允许修改共享内容。</span> <span>两个缓冲区的位置，极限和标记值将是独立的。</span> </p> 
           <p> <span>新缓冲区的容量，限制，位置和标记值将与此缓冲区的容量，限制，位置和标记值相同。</span> </p> 
           <p> <span>如果此缓冲区本身是只读的，则该方法的行为与<a href="../../java/nio/ByteBuffer.html#duplicate--"><code>duplicate</code></a>方法完全相同。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             新的只读字节缓冲区 
           </dd> 
          </dl> </li> 
        </ul> <a name="get--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>get</h4> <pre>public abstract&nbsp;byte&nbsp;get()</pre> 
          <div class="block"> 
           <span>相对<i>获取</i>方法。</span> 
           <span>读取该缓冲区当前位置的字节，然后增加位置。</span> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             缓冲区当前位置的字节 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/nio/BufferUnderflowException.html" title="class in java.nio">BufferUnderflowException</a></code> - 如果缓冲区的当前位置不小于其限制 
           </dd> 
          </dl> </li> 
        </ul> <a name="put-byte-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>put</h4> <pre>public abstract&nbsp;<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;put(byte&nbsp;b)</pre> 
          <div class="block"> 
           <span>相对<i>放置</i>法<i>（可选操作）</i> 。</span> 
           <p> <span>将给定字节写入当前位置的缓冲区，然后增加位置。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>b</code> - 要写入的字节 
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
            <code><a href="../../java/nio/ReadOnlyBufferException.html" title="class in java.nio">ReadOnlyBufferException</a></code> - 如果此缓冲区是只读的 
           </dd> 
          </dl> </li> 
        </ul> <a name="get-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>get</h4> <pre>public abstract&nbsp;byte&nbsp;get(int&nbsp;index)</pre> 
          <div class="block"> 
           <span>绝对<i>获取</i>方法。</span> 
           <span>读取给定索引处的字节。</span> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>index</code> - 读取字节的索引 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             给定索引的字节 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/IndexOutOfBoundsException.html" title="class in java.lang">IndexOutOfBoundsException</a></code> - 如果 
            <tt>index</tt>为负数或不小于缓冲区限制 
           </dd> 
          </dl> </li> 
        </ul> <a name="put-int-byte-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>put</h4> <pre>public abstract&nbsp;<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;put(int&nbsp;index,
                               byte&nbsp;b)</pre> 
          <div class="block"> 
           <span>绝对<i>put</i>方法<i>（可选操作）</i> 。</span> 
           <p> <span>将给定字节写入给定索引的缓冲区。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>index</code> - 要写入字节的索引 
           </dd> 
           <dd> 
            <code>b</code> - 要写入的字节值 
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
        </ul> <a name="get-byte:A-int-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>get</h4> <pre>public&nbsp;<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;get(byte[]&nbsp;dst,
                      int&nbsp;offset,
                      int&nbsp;length)</pre> 
          <div class="block"> 
           <span>相对批量<i>获取</i>方法。</span> 
           <p> <span>此方法将字节从此缓冲区传输到给定的目标数组。</span> <span>如果缓冲区中剩余的字节比满足请求所需的字节少，也就是说，如果<tt>length</tt> <tt>&gt;</tt> <tt>remaining()</tt> ， <tt>则不</tt> <tt>传输</tt>任何字节并抛出<a href="../../java/nio/BufferUnderflowException.html" title="java.nio中的类"><code>BufferUnderflowException</code></a> 。</span> </p> 
           <p> <span>否则，该方法将<tt>length</tt>字节从该缓冲区复制到给定的数组中，从该缓冲区的当前位置开始，并在数组中给定的偏移量。</span> <span>然后将该缓冲区的位置增加<tt>length</tt> 。</span> </p> 
           <p> <span>换句话说，调用此方法的形式<tt>src.get(dst,&nbsp;off,&nbsp;len)</tt>具有与循环完全相同的效果</span> </p> 
           <pre>  <span><code> for (int i = off; i &lt; off + len; i++) dst[i] = src.get(): </code></span> </pre> 
           <span>除了它首先检查这个缓冲区中是否有足够的字节，并且它可能更有效率。</span> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>dst</code> - 要写入字节的数组 
           </dd> 
           <dd> 
            <span><code>offset</code> - 要写入的第一个字节的数组中的偏移量;</span> 
            <span>必须是非负数，不得大于<tt>dst.length</tt></span> 
           </dd> 
           <dd> 
            <span><code>length</code> - 要写入给定数组的最大字节数;</span> 
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
            <code><a href="../../java/nio/BufferUnderflowException.html" title="class in java.nio">BufferUnderflowException</a></code> - 如果此缓冲区中剩余少于 
            <tt>length</tt>个字节 
           </dd> 
           <dd> 
            <code><a href="../../java/lang/IndexOutOfBoundsException.html" title="class in java.lang">IndexOutOfBoundsException</a></code> - 如果 
            <tt>offset</tt>和 
            <tt>length</tt>参数的前提条件不成立 
           </dd> 
          </dl> </li> 
        </ul> <a name="get-byte:A-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>get</h4> <pre>public&nbsp;<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;get(byte[]&nbsp;dst)</pre> 
          <div class="block"> 
           <span>相对批量<i>获取</i>方法。</span> 
           <p> <span>此方法将字节从此缓冲区传输到给定的目标数组。</span> <span>调用此方法的形式为<tt>src.get(a)的</tt>行为方式与调用完全相同</span> </p> 
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
            <code><a href="../../java/nio/BufferUnderflowException.html" title="class in java.nio">BufferUnderflowException</a></code> - 如果此缓冲区中 
            <tt>剩余的</tt>字节少于 
            <tt>length</tt>个字节 
           </dd> 
          </dl> </li> 
        </ul> <a name="put-java.nio.ByteBuffer-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>put</h4> <pre>public&nbsp;<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;put(<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;src)</pre> 
          <div class="block"> 
           <span>相对大容量<i>put</i>方法<i>（可选操作）</i> 。</span> 
           <p> <span>此方法将给定源缓冲区中剩余的字节传输到此缓冲区。</span> <span>如果源缓冲区中剩余的字节多于此缓冲区，即<tt>src.remaining()</tt> <tt>&gt;</tt> <tt>remaining()</tt> ，则不会传输任何字节，并抛出<a href="../../java/nio/BufferOverflowException.html" title="java.nio中的类"><code>BufferOverflowException</code></a> 。</span> </p> 
           <p> <span>否则，该方法将<i>n</i> = <tt>src.remaining()</tt>个字节从给定缓冲区复制到此缓冲区中，从每个缓冲区的当前位置开始。</span> <span>然后将两个缓冲器的位置递增<i>n</i> 。</span> </p> 
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
            <span><code>src</code> - 读取字节的源缓冲区;</span> 
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
            <code><a href="../../java/nio/BufferOverflowException.html" title="class in java.nio">BufferOverflowException</a></code> - 如果此缓冲区中的源缓冲区中剩余字节的空间不足 
           </dd> 
           <dd> 
            <code><a href="../../java/lang/IllegalArgumentException.html" title="class in java.lang">IllegalArgumentException</a></code> - 如果源缓冲区是这个缓冲区 
           </dd> 
           <dd> 
            <code><a href="../../java/nio/ReadOnlyBufferException.html" title="class in java.nio">ReadOnlyBufferException</a></code> - 如果此缓冲区是只读的 
           </dd> 
          </dl> </li> 
        </ul> <a name="put-byte:A-int-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>put</h4> <pre>public&nbsp;<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;put(byte[]&nbsp;src,
                      int&nbsp;offset,
                      int&nbsp;length)</pre> 
          <div class="block"> 
           <span>相对大容量<i>put</i>方法<i>（可选操作）</i> 。</span> 
           <p> <span>此方法将字节从给定的源数组传输到此缓冲区。</span> <span>如果要从数组中复制的字节多于保留在此缓冲区中的字节数，也就是说，如果<tt>length</tt> <tt>&gt;</tt> <tt>remaining()</tt> ，则不会传输任何字节，并抛出<a href="../../java/nio/BufferOverflowException.html" title="java.nio中的类"><code>BufferOverflowException</code></a> 。</span> </p> 
           <p> <span>否则，该方法将给定数组中的<tt>length</tt>个字节复制到此缓冲区中，从阵列中的给定偏移量和该缓冲区的当前位置开始。</span> <span>此缓冲区的位置然后增加<tt>length</tt> 。</span> </p> 
           <p> <span>换言之，所述表格<tt>dst.put(src,&nbsp;off,&nbsp;len)</tt>的这种方法的调用具有完全一样的环相同的效果</span> </p> 
           <pre>  <span><code> for (int i = off; i &lt; off + len; i++) dst.put(a[i]); </code></span> </pre> 
           <span>除了它首先检查这个缓冲区中是否有足够的空间，并且它可能更有效率。</span> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>src</code> - 要读取字节的数组 
           </dd> 
           <dd> 
            <span><code>offset</code> - 要读取的第一个字节的数组内的偏移量;</span> 
            <span>必须是非负数，不得大于<tt>array.length</tt></span> 
           </dd> 
           <dd> 
            <span><code>length</code> - 要从给定数组读取的字节数;</span> 
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
            <code><a href="../../java/nio/BufferOverflowException.html" title="class in java.nio">BufferOverflowException</a></code> - 如果此缓冲区中没有足够的空间 
           </dd> 
           <dd> 
            <code><a href="../../java/lang/IndexOutOfBoundsException.html" title="class in java.lang">IndexOutOfBoundsException</a></code> - 如果 
            <tt>offset</tt>和 
            <tt>length</tt>参数的前提条件不成立 
           </dd> 
           <dd> 
            <code><a href="../../java/nio/ReadOnlyBufferException.html" title="class in java.nio">ReadOnlyBufferException</a></code> - 如果这个缓冲区是只读的 
           </dd> 
          </dl> </li> 
        </ul> <a name="put-byte:A-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>put</h4> <pre>public final&nbsp;<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;put(byte[]&nbsp;src)</pre> 
          <div class="block"> 
           <span>相对大容量<i>put</i>方法<i>（可选操作）</i> 。</span> 
           <p> <span>此方法将给定源字节数组的整个内容传输到此缓冲区。</span> <span>调用此方法的形式为<tt>dst.put(a)的</tt>行为方式与调用完全相同</span> </p> 
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
           <span>告诉这个缓冲区是否由可访问的字节数组支持。</span> 
           <p> <span>如果此方法返回<tt>true，</tt>则可以安全地调用<a href="../../java/nio/ByteBuffer.html#array--"><code>array</code></a>和<a href="../../java/nio/ByteBuffer.html#arrayOffset--"><code>arrayOffset</code></a>方法。</span> </p> 
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
         <li class="blockList"> <h4>array</h4> <pre>public final&nbsp;byte[]&nbsp;array()</pre> 
          <div class="block"> 
           <span>返回支持此缓冲区的字节数组<i>（可选操作）</i> 。</span> 
           <p> <span>对此缓冲区内容的修改将导致返回的数组的内容被修改，反之亦然。</span> </p> 
           <p> <span>在调用此方法之前调用<a href="../../java/nio/ByteBuffer.html#hasArray--"><code>hasArray</code></a>方法，以确保此缓冲区具有可访问的后台阵列。</span> </p> 
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
           <p> <span>如果此缓冲区由数组支持，则缓冲区位置<i>p</i>对应于数组索引<i>p</i> + <tt>arrayOffset()</tt> 。</span> </p> 
           <p> <span>在调用此方法之前调用<a href="../../java/nio/ByteBuffer.html#hasArray--"><code>hasArray</code></a>方法，以确保此缓冲区具有可访问的后台阵列。</span> </p> 
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
         <li class="blockList"> <h4>compact</h4> <pre>public abstract&nbsp;<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;compact()</pre> 
          <div class="block"> 
           <span><i>压缩</i>此缓冲区<i>（可选操作）</i> 。</span> 
           <p> <span>缓冲区当前位置与其限制（如果有的话）之间的字节被复制到缓冲区的开头。</span> <span>也就是说，索引<i>p</i> = <tt>position()</tt>的字节被复制到索引零，索引<i>p</i> + 1处的字节被复制到索引1，等等，直到索引<tt>limit()-1</tt>的字节被复制到索引<i>n</i> = <tt>limit()</tt> - <tt>1</tt> - <i>p</i> 。</span> <span>然后将缓冲区的位置设置为<i>n + 1</i> ，并将其限制设置为其容量。</span> <span>标记如果被定义，则被丢弃。</span> </p> 
           <p> <span>缓冲区的位置设置为复制的字节数，而不是零，因此可以通过调用另一个相对<i>put</i>方法来立即调用此方法。</span> </p> 
           <p> <span>在写入不完整的情况下从缓冲区写入数据后调用此方法。</span> <span>例如，以下循环通过缓冲区将字节从一个通道复制到另一个通道<tt>buf</tt> ：</span> </p> 
           <blockquote> 
            <span><pre><code>
   buf.clear();          // Prepare buffer for use
   while (in.read(buf) &gt;= 0 || buf.position != 0) {
       buf.flip();
       out.write(buf);
       buf.compact();    // In case of partial write
   }
 </code></pre></span> 
           </blockquote> 
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
            <code><a href="../../java/nio/ReadOnlyBufferException.html" title="class in java.nio">ReadOnlyBufferException</a></code> - 如果这个缓冲区是只读的 
           </dd> 
          </dl> </li> 
        </ul> <a name="isDirect--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>isDirect</h4> <pre>public abstract&nbsp;boolean&nbsp;isDirect()</pre> 
          <div class="block">
            告诉这个字节缓冲区是否是直接的。 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">Specified by:</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/nio/Buffer.html#isDirect--">isDirect</a></code>在 
            <code><a href="../../java/nio/Buffer.html" title="class in java.nio">Buffer</a></code>类 
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
            <code><a href="../../java/lang/Object.html#toString--">toString</a></code>在类 
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
           <p> <span>字节缓冲区的哈希码仅取决于其剩余的元素;</span> <span>也就是说，从<tt>position()</tt>到元素，并包括元素在<tt>limit()</tt> - <tt>1</tt> 。</span> </p> 
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
           <p> <span>两个字节的缓冲区是相等的，</span> </p> 
           <ol> 
            <li><p> <span>它们具有相同的元素类型，</span> </p></li> 
            <li><p> <span>他们有相同数量的剩余元素，和</span> </p></li> 
            <li><p> <span>独立于其起始位置的剩余元素的两个序列是相等的。</span> </p></li> 
           </ol> 
           <p> <span>字节缓冲区不等于任何其他类型的对象。</span> </p> 
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
            <tt>true</tt>如果，且仅当此缓冲区等于给定对象时 
           </dd> 
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <span><a href="../../java/lang/Object.html#hashCode--"><code>Object.hashCode()</code></a> ， <a href="../../java/util/HashMap.html" title="java.util中的类"><code>HashMap</code></a></span> 
           </dd> 
          </dl> </li> 
        </ul> <a name="compareTo-java.nio.ByteBuffer-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>compareTo</h4> <pre>public&nbsp;int&nbsp;compareTo(<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;that)</pre> 
          <div class="block"> 
           <span>将此缓冲区与另一个缓冲区进行比较。</span> 
           <p> <span>通过以字面的方式比较其剩余元素的序列来比较两个字节缓冲区，而不考虑其相应缓冲器内每个序列的起始位置。</span> <span>对<code>byte</code>元素进行比较，仿佛通过调用<a href="../../java/lang/Byte.html#compare-byte-byte-"><code>Byte.compare(byte,byte)</code></a> 。</span> </p> 
           <p> <span>一个字节缓冲区不能与任何其他类型的对象相媲美。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">Specified by:</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/Comparable.html#compareTo-T-">compareTo</a></code>在接口 
            <code><a href="../../java/lang/Comparable.html" title="interface in java.lang">Comparable</a>&lt;<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&gt;</code> 
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
        <ul class="blockList"> 
         <li class="blockList"> <h4>order</h4> <pre>public final&nbsp;<a href="../../java/nio/ByteOrder.html" title="class in java.nio">ByteOrder</a>&nbsp;order()</pre> 
          <div class="block"> 
           <span>检索此缓冲区的字节顺序。</span> 
           <p> <span>读取或写入多字节值时使用字节顺序，当创建作为此字节缓冲区视图的缓冲区时使用。</span> <span>新创建的字节缓冲区的顺序始终为<a href="../../java/nio/ByteOrder.html#BIG_ENDIAN"><code>BIG_ENDIAN</code></a> 。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             这个缓冲区的字节顺序 
           </dd> 
          </dl> </li> 
        </ul> <a name="order-java.nio.ByteOrder-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>order</h4> <pre>public final&nbsp;<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;order(<a href="../../java/nio/ByteOrder.html" title="class in java.nio">ByteOrder</a>&nbsp;bo)</pre> 
          <div class="block">
            修改缓冲区的字节顺序。 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>bo</code> - 新字节顺序， 
            <a href="../../java/nio/ByteOrder.html#BIG_ENDIAN"><code>BIG_ENDIAN</code></a>或 
            <a href="../../java/nio/ByteOrder.html#LITTLE_ENDIAN"><code>LITTLE_ENDIAN</code></a> 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             这个缓冲区 
           </dd> 
          </dl> </li> 
        </ul> <a name="getChar--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>getChar</h4> <pre>public abstract&nbsp;char&nbsp;getChar()</pre> 
          <div class="block"> 
           <span>读取char值的相对<i>get</i>方法。</span> 
           <p> <span>在此缓冲区的当前位置读取接下来的两个字节，根据当前字节顺序将它们组合成一个char值，然后将位置递增2。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             缓冲区当前位置的char值 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/nio/BufferUnderflowException.html" title="class in java.nio">BufferUnderflowException</a></code> - 如果此缓冲区中剩余少于两个字节 
           </dd> 
          </dl> </li> 
        </ul> <a name="putChar-char-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>putChar</h4> <pre>public abstract&nbsp;<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;putChar(char&nbsp;value)</pre> 
          <div class="block"> 
           <span>写入char值的相对<i>put</i>方法<i>（可选操作）</i> 。</span> 
           <p> <span>将当前字节顺序中包含给定char值的两个字节写入此缓冲区中的当前位置，然后将位置递增2。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>value</code> - 要写入的char值 
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
            <code><a href="../../java/nio/BufferOverflowException.html" title="class in java.nio">BufferOverflowException</a></code> - 如果此缓冲区中剩余少于两个字节 
           </dd> 
           <dd> 
            <code><a href="../../java/nio/ReadOnlyBufferException.html" title="class in java.nio">ReadOnlyBufferException</a></code> - 如果此缓冲区是只读的 
           </dd> 
          </dl> </li> 
        </ul> <a name="getChar-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>getChar</h4> <pre>public abstract&nbsp;char&nbsp;getChar(int&nbsp;index)</pre> 
          <div class="block"> 
           <span>绝对<i>获取</i>方法来读取一个char值。</span> 
           <p> <span>在给定索引处读取两个字节，根据当前字节顺序将它们组合成一个char值。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>index</code> - 从中读取字节的索引 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             给定索引处的char值 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/IndexOutOfBoundsException.html" title="class in java.lang">IndexOutOfBoundsException</a></code> - 如果 
            <tt>index</tt>为负数或不小于缓冲区限制，则减1 
           </dd> 
          </dl> </li> 
        </ul> <a name="putChar-int-char-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>putChar</h4> <pre>public abstract&nbsp;<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;putChar(int&nbsp;index,
                                   char&nbsp;value)</pre> 
          <div class="block"> 
           <span>用于写入char值的绝对<i>put</i>方法<i>（可选操作）</i> 。</span> 
           <p> <span>将给定的char值的两个字节以当前字节顺序写入给定索引的缓冲区。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>index</code> - 要写入字节的索引 
           </dd> 
           <dd> 
            <code>value</code> - 要写入的char值 
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
            <tt>index</tt>为负数或不小于缓冲区限制，则减去1 
           </dd> 
           <dd> 
            <code><a href="../../java/nio/ReadOnlyBufferException.html" title="class in java.nio">ReadOnlyBufferException</a></code> - 如果这个缓冲区是只读的 
           </dd> 
          </dl> </li> 
        </ul> <a name="asCharBuffer--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>asCharBuffer</h4> <pre>public abstract&nbsp;<a href="../../java/nio/CharBuffer.html" title="class in java.nio">CharBuffer</a>&nbsp;asCharBuffer()</pre> 
          <div class="block"> 
           <span>创建一个字节缓冲区作为char缓冲区的视图。</span> 
           <p> <span>新缓冲区的内容将从此缓冲区的当前位置开始。</span> <span>对这个缓冲区内容的更改将在新的缓冲区中可见，反之亦然;</span> <span>两个缓冲区的位置，极限和标记值将是独立的。</span> </p> 
           <p> <span>新缓冲区的位置将为零，其容量和限制将是此缓冲区中剩余的字节数除以2，其标记将不定义。</span> <span>如果只有这个缓冲区是直接的，并且只有当这个缓冲区是只读的时，这个缓冲区将是只读的。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             一个新的char缓冲区 
           </dd> 
          </dl> </li> 
        </ul> <a name="getShort--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>getShort</h4> <pre>public abstract&nbsp;short&nbsp;getShort()</pre> 
          <div class="block"> 
           <span>相对<i>获取</i>方法读取一个简短的值。</span> 
           <p> <span>在该缓冲区的当前位置读取接下来的两个字节，根据当前字节顺序将它们组合成一个短值，然后将位置递增2。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             缓冲区当前位置的短值 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/nio/BufferUnderflowException.html" title="class in java.nio">BufferUnderflowException</a></code> - 如果此缓冲区中剩余少于两个字节 
           </dd> 
          </dl> </li> 
        </ul> <a name="putShort-short-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>putShort</h4> <pre>public abstract&nbsp;<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;putShort(short&nbsp;value)</pre> 
          <div class="block"> 
           <span>写入一个短值的相对<i>放置</i>方法<i>（可选操作）</i> 。</span> 
           <p> <span>以当前字节顺序将包含给定短值的两个字节写入此缓冲区，然后将位置递增2。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>value</code> - 
            <code>value</code>的短价值 
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
            <code><a href="../../java/nio/BufferOverflowException.html" title="class in java.nio">BufferOverflowException</a></code> - 如果该缓冲区中剩余少于两个字节 
           </dd> 
           <dd> 
            <code><a href="../../java/nio/ReadOnlyBufferException.html" title="class in java.nio">ReadOnlyBufferException</a></code> - 如果此缓冲区为只读 
           </dd> 
          </dl> </li> 
        </ul> <a name="getShort-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>getShort</h4> <pre>public abstract&nbsp;short&nbsp;getShort(int&nbsp;index)</pre> 
          <div class="block"> 
           <span>绝对<i>获取</i>读取一个简短值的方法。</span> 
           <p> <span>在给定索引处读取两个字节，根据当前字节顺序将它们组合成一个短值。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>index</code> - 读取字节的索引 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             给定指数的短期价值 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/IndexOutOfBoundsException.html" title="class in java.lang">IndexOutOfBoundsException</a></code> - 如果 
            <tt>index</tt>为负数或不小于缓冲区限制，则减1 
           </dd> 
          </dl> </li> 
        </ul> <a name="putShort-int-short-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>putShort</h4> <pre>public abstract&nbsp;<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;putShort(int&nbsp;index,
                                    short&nbsp;value)</pre> 
          <div class="block"> 
           <span>绝对<i>put</i>方法写入一个简短的值<i>（可选操作）</i> 。</span> 
           <p> <span>以给定的索引将包含给定短值的两个字节以当前字节顺序写入此缓冲区。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>index</code> - 将写入字节的索引 
           </dd> 
           <dd> 
            <code>value</code> - 
            <code>value</code>的短价值 
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
            <tt>index</tt>为负值或不小于缓冲区限制，则减1 
           </dd> 
           <dd> 
            <code><a href="../../java/nio/ReadOnlyBufferException.html" title="class in java.nio">ReadOnlyBufferException</a></code> - 如果这个缓冲区是只读的 
           </dd> 
          </dl> </li> 
        </ul> <a name="asShortBuffer--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>asShortBuffer</h4> <pre>public abstract&nbsp;<a href="../../java/nio/ShortBuffer.html" title="class in java.nio">ShortBuffer</a>&nbsp;asShortBuffer()</pre> 
          <div class="block"> 
           <span>将此字节缓冲区的视图创建为短缓冲区。</span> 
           <p> <span>新缓冲区的内容将从此缓冲区的当前位置开始。</span> <span>对这个缓冲区内容的更改将在新的缓冲区中可见，反之亦然;</span> <span>两个缓冲区的位置，极限和标记值将是独立的。</span> </p> 
           <p> <span>新缓冲区的位置将为零，其容量和限制将是此缓冲区中剩余的字节数除以2，其标记将不定义。</span> <span>如果只有这个缓冲区是直接的，并且只有当这个缓冲区是只读的时，这个缓冲区将是只读的。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             一个新的缓冲区 
           </dd> 
          </dl> </li> 
        </ul> <a name="getInt--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>getInt</h4> <pre>public abstract&nbsp;int&nbsp;getInt()</pre> 
          <div class="block"> 
           <span>用于读取int值的相对<i>get</i>方法。</span> 
           <p> <span>在该缓冲区的当前位置读取接下来的四个字节，根据当前字节顺序将它们组合成一个int值，然后将位置递增四。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             缓冲区当前位置的int值 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/nio/BufferUnderflowException.html" title="class in java.nio">BufferUnderflowException</a></code> - 如果该缓冲区中剩余少于四个字节 
           </dd> 
          </dl> </li> 
        </ul> <a name="putInt-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>putInt</h4> <pre>public abstract&nbsp;<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;putInt(int&nbsp;value)</pre> 
          <div class="block"> 
           <span>编写int值的相对<i>put</i>方法<i>（可选操作）</i> 。</span> 
           <p> <span>以当前字节顺序将包含给定int值的四个字节写入当前位置的缓冲区，然后将位置递增四。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>value</code> - 要写入的int值 
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
            <code><a href="../../java/nio/BufferOverflowException.html" title="class in java.nio">BufferOverflowException</a></code> - 如果此缓冲区中剩余少于四个字节 
           </dd> 
           <dd> 
            <code><a href="../../java/nio/ReadOnlyBufferException.html" title="class in java.nio">ReadOnlyBufferException</a></code> - 如果这个缓冲区是只读的 
           </dd> 
          </dl> </li> 
        </ul> <a name="getInt-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>getInt</h4> <pre>public abstract&nbsp;int&nbsp;getInt(int&nbsp;index)</pre> 
          <div class="block"> 
           <span>用于读取int值的绝对<i>get</i>方法。</span> 
           <p> <span>在给定索引处读取四个字节，根据当前字节顺序将它们组合成一个int值。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>index</code> - 读取字节的索引 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             给定索引处的int值 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/IndexOutOfBoundsException.html" title="class in java.lang">IndexOutOfBoundsException</a></code> - 如果 
            <tt>index</tt>为负数或不小于缓冲区限制，则减去3 
           </dd> 
          </dl> </li> 
        </ul> <a name="putInt-int-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>putInt</h4> <pre>public abstract&nbsp;<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;putInt(int&nbsp;index,
                                  int&nbsp;value)</pre> 
          <div class="block"> 
           <span>用于写入int值的绝对<i>put</i>方法<i>（可选操作）</i> 。</span> 
           <p> <span>以给定的索引将包含给定int值的四个字节以当前字节顺序写入此缓冲区。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>index</code> - 要写入字节的索引 
           </dd> 
           <dd> 
            <code>value</code> - 要写入的int值 
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
            <tt>index</tt>为负数或不小于缓冲区限制，则减去3 
           </dd> 
           <dd> 
            <code><a href="../../java/nio/ReadOnlyBufferException.html" title="class in java.nio">ReadOnlyBufferException</a></code> - 如果此缓冲区是只读的 
           </dd> 
          </dl> </li> 
        </ul> <a name="asIntBuffer--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>asIntBuffer</h4> <pre>public abstract&nbsp;<a href="../../java/nio/IntBuffer.html" title="class in java.nio">IntBuffer</a>&nbsp;asIntBuffer()</pre> 
          <div class="block"> 
           <span>将此字节缓冲区的视图创建为int缓冲区。</span> 
           <p> <span>新缓冲区的内容将从此缓冲区的当前位置开始。</span> <span>对这个缓冲区内容的更改将在新的缓冲区中可见，反之亦然;</span> <span>两个缓冲区的位置，极限和标记值将是独立的。</span> </p> 
           <p> <span>新缓冲区的位置将为零，其容量和限制将是该缓冲区中剩余的字节数除以4，其标记将不定义。</span> <span>如果只有这个缓冲区是直接的，并且只有当这个缓冲区是只读的时，这个缓冲区将是只读的。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             一个新的int缓冲区 
           </dd> 
          </dl> </li> 
        </ul> <a name="getLong--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>getLong</h4> <pre>public abstract&nbsp;long&nbsp;getLong()</pre> 
          <div class="block"> 
           <span>读取长值的相对<i>get</i>方法。</span> 
           <p> <span>在该缓冲区的当前位置读取接下来的八个字节，根据当前字节顺序将它们组合成一个长的值，然后将位置增加八位。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             缓冲区当前位置的长值 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/nio/BufferUnderflowException.html" title="class in java.nio">BufferUnderflowException</a></code> - 如果此缓冲区中剩余少于8个字节 
           </dd> 
          </dl> </li> 
        </ul> <a name="putLong-long-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>putLong</h4> <pre>public abstract&nbsp;<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;putLong(long&nbsp;value)</pre> 
          <div class="block"> 
           <span>写入长值的相对<i>put</i>方法<i>（可选操作）</i> 。</span> 
           <p> <span>以当前字节顺序将包含给定长值的八个字节写入当前位置的缓冲区，然后将位置递增8。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>value</code> - 
            <code>value</code>的长的价值 
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
            <code><a href="../../java/nio/BufferOverflowException.html" title="class in java.nio">BufferOverflowException</a></code> - 如果此缓冲区中剩余少于八个字节 
           </dd> 
           <dd> 
            <code><a href="../../java/nio/ReadOnlyBufferException.html" title="class in java.nio">ReadOnlyBufferException</a></code> - 如果此缓冲区是只读的 
           </dd> 
          </dl> </li> 
        </ul> <a name="getLong-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>getLong</h4> <pre>public abstract&nbsp;long&nbsp;getLong(int&nbsp;index)</pre> 
          <div class="block"> 
           <span>绝对<i>获取</i>读取长值的方法。</span> 
           <p> <span>在给定索引处读取八个字节，根据当前字节顺序将它们组合成一个长整型值。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>index</code> - 读取字节的索引 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             给定指数的长期价值 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/IndexOutOfBoundsException.html" title="class in java.lang">IndexOutOfBoundsException</a></code> - 如果 
            <tt>index</tt>为负数或不小于缓冲区限制，则为负数 
           </dd> 
          </dl> </li> 
        </ul> <a name="putLong-int-long-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>putLong</h4> <pre>public abstract&nbsp;<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;putLong(int&nbsp;index,
                                   long&nbsp;value)</pre> 
          <div class="block"> 
           <span>绝对<i>put</i>方法写入一个长的值<i>（可选操作）</i> 。</span> 
           <p> <span>以给定的索引将包含给定long值的八个字节以当前字节顺序写入此缓冲区。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>index</code> - 要写入字节的索引 
           </dd> 
           <dd> 
            <code>value</code> - 
            <code>value</code>的长的价值 
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
            <tt>index</tt>是负数或不小于缓冲区的限制，则减去7 
           </dd> 
           <dd> 
            <code><a href="../../java/nio/ReadOnlyBufferException.html" title="class in java.nio">ReadOnlyBufferException</a></code> - 如果这个缓冲区是只读的 
           </dd> 
          </dl> </li> 
        </ul> <a name="asLongBuffer--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>asLongBuffer</h4> <pre>public abstract&nbsp;<a href="../../java/nio/LongBuffer.html" title="class in java.nio">LongBuffer</a>&nbsp;asLongBuffer()</pre> 
          <div class="block"> 
           <span>将此字节缓冲区的视图创建为长缓冲区。</span> 
           <p> <span>新缓冲区的内容将从此缓冲区的当前位置开始。</span> <span>对这个缓冲区内容的更改将在新的缓冲区中可见，反之亦然;</span> <span>两个缓冲区的位置，极限和标记值将是独立的。</span> </p> 
           <p> <span>新缓冲区的位置将为零，其容量和限制将是该缓冲区中剩余的字节数除以8，其标记将不定义。</span> <span>如果只有这个缓冲区是直接的，并且只有当这个缓冲区是只读的时，这个缓冲区将是只读的。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             一个新的长缓冲区 
           </dd> 
          </dl> </li> 
        </ul> <a name="getFloat--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>getFloat</h4> <pre>public abstract&nbsp;float&nbsp;getFloat()</pre> 
          <div class="block"> 
           <span>读取浮点值的相对<i>get</i>方法。</span> 
           <p> <span>在该缓冲区的当前位置读取接下来的四个字节，根据当前字节顺序将它们组合成一个浮点值，然后将位置递增四。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             缓冲区当前位置的浮点值 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/nio/BufferUnderflowException.html" title="class in java.nio">BufferUnderflowException</a></code> - 如果此缓冲区中剩余少于四个字节 
           </dd> 
          </dl> </li> 
        </ul> <a name="putFloat-float-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>putFloat</h4> <pre>public abstract&nbsp;<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;putFloat(float&nbsp;value)</pre> 
          <div class="block"> 
           <span>编写浮点值的相对<i>put</i>方法<i>（可选操作）</i> 。</span> 
           <p> <span>以当前字节顺序将包含给定浮点值的四个字节写入此缓冲区中的当前位置，然后将位置递增四。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>value</code> - 要写入的浮点值 
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
            <code><a href="../../java/nio/BufferOverflowException.html" title="class in java.nio">BufferOverflowException</a></code> - 如果此缓冲区中剩余少于四个字节 
           </dd> 
           <dd> 
            <code><a href="../../java/nio/ReadOnlyBufferException.html" title="class in java.nio">ReadOnlyBufferException</a></code> - 如果此缓冲区是只读的 
           </dd> 
          </dl> </li> 
        </ul> <a name="getFloat-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>getFloat</h4> <pre>public abstract&nbsp;float&nbsp;getFloat(int&nbsp;index)</pre> 
          <div class="block"> 
           <span>用于读取浮点值的绝对<i>get</i>方法。</span> 
           <p> <span>在给定索引处读取四个字节，根据当前字节顺序将它们组合成一个浮点值。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>index</code> - 读取字节的索引 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             给定索引处的浮点值 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/IndexOutOfBoundsException.html" title="class in java.lang">IndexOutOfBoundsException</a></code> - 如果 
            <tt>index</tt>为负数或不小于缓冲区限制，则减去3 
           </dd> 
          </dl> </li> 
        </ul> <a name="putFloat-int-float-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>putFloat</h4> <pre>public abstract&nbsp;<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;putFloat(int&nbsp;index,
                                    float&nbsp;value)</pre> 
          <div class="block"> 
           <span>用于写入浮点值的绝对<i>put</i>方法<i>（可选操作）</i> 。</span> 
           <p> <span>以给定的索引将包含给定浮点值的四个字节以当前字节顺序写入此缓冲区。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>index</code> - 将写入字节的索引 
           </dd> 
           <dd> 
            <code>value</code> - 要写入的浮点值 
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
            <tt>index</tt>为负数或不小于缓冲区限制，则减去3 
           </dd> 
           <dd> 
            <code><a href="../../java/nio/ReadOnlyBufferException.html" title="class in java.nio">ReadOnlyBufferException</a></code> - 如果此缓冲区是只读的 
           </dd> 
          </dl> </li> 
        </ul> <a name="asFloatBuffer--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>asFloatBuffer</h4> <pre>public abstract&nbsp;<a href="../../java/nio/FloatBuffer.html" title="class in java.nio">FloatBuffer</a>&nbsp;asFloatBuffer()</pre> 
          <div class="block"> 
           <span>将此字节缓冲区的视图创建为浮动缓冲区。</span> 
           <p> <span>新缓冲区的内容将从此缓冲区的当前位置开始。</span> <span>对这个缓冲区内容的更改将在新的缓冲区中可见，反之亦然;</span> <span>两个缓冲区的位置，极限和标记值将是独立的。</span> </p> 
           <p> <span>新缓冲区的位置将为零，其容量和限制将是该缓冲区中剩余的字节数除以4，其标记将不定义。</span> <span>如果只有这个缓冲区是直接的，并且只有当这个缓冲区是只读的时，这个缓冲区将是只读的。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             一个新的浮动缓冲区 
           </dd> 
          </dl> </li> 
        </ul> <a name="getDouble--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>getDouble</h4> <pre>public abstract&nbsp;double&nbsp;getDouble()</pre> 
          <div class="block"> 
           <span>读取双重值的相对<i>get</i>方法。</span> 
           <p> <span>在该缓冲区的当前位置读取接下来的八个字节，根据当前字节顺序将它们组合成双精度值，然后将位置递增八。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             缓冲区当前位置的double值 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/nio/BufferUnderflowException.html" title="class in java.nio">BufferUnderflowException</a></code> - 如果此缓冲区中剩余少于8个字节 
           </dd> 
          </dl> </li> 
        </ul> <a name="putDouble-double-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>putDouble</h4> <pre>public abstract&nbsp;<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;putDouble(double&nbsp;value)</pre> 
          <div class="block"> 
           <span>写入double值的相对<i>put</i>方法<i>（可选操作）</i> 。</span> 
           <p> <span>以当前字节顺序将包含给定双值的八个字节写入当前位置的缓冲区，然后将位置递增8。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>value</code> - 要写入的双重值 
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
            <code><a href="../../java/nio/BufferOverflowException.html" title="class in java.nio">BufferOverflowException</a></code> - 如果此缓冲区中剩余少于8个字节 
           </dd> 
           <dd> 
            <code><a href="../../java/nio/ReadOnlyBufferException.html" title="class in java.nio">ReadOnlyBufferException</a></code> - 如果这个缓冲区是只读的 
           </dd> 
          </dl> </li> 
        </ul> <a name="getDouble-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>getDouble</h4> <pre>public abstract&nbsp;double&nbsp;getDouble(int&nbsp;index)</pre> 
          <div class="block"> 
           <span>绝对<i>获取</i>读取双重值的方法。</span> 
           <p> <span>在给定索引处读取八个字节，根据当前字节顺序将它们组合成双精度值。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>index</code> - 读取字节的索引 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             给定指数的双重值 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/IndexOutOfBoundsException.html" title="class in java.lang">IndexOutOfBoundsException</a></code> - 如果 
            <tt>index</tt>为负数或不小于缓冲区限制，则减去7 
           </dd> 
          </dl> </li> 
        </ul> <a name="putDouble-int-double-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>putDouble</h4> <pre>public abstract&nbsp;<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a>&nbsp;putDouble(int&nbsp;index,
                                     double&nbsp;value)</pre> 
          <div class="block"> 
           <span>用于写入双精度值的绝对<i>put</i>方法<i>（可选操作）</i> 。</span> 
           <p> <span>以给定的索引将包含给定双值的八个字节以当前字节顺序写入此缓冲区。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>index</code> - 要写入字节的索引 
           </dd> 
           <dd> 
            <code>value</code> - 要写入的双重值 
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
            <tt>index</tt>为负数或不小于缓冲区限制，则减去7 
           </dd> 
           <dd> 
            <code><a href="../../java/nio/ReadOnlyBufferException.html" title="class in java.nio">ReadOnlyBufferException</a></code> - 如果此缓冲区为只读 
           </dd> 
          </dl> </li> 
        </ul> <a name="asDoubleBuffer--"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>asDoubleBuffer</h4> <pre>public abstract&nbsp;<a href="../../java/nio/DoubleBuffer.html" title="class in java.nio">DoubleBuffer</a>&nbsp;asDoubleBuffer()</pre> 
          <div class="block"> 
           <span>将此字节缓冲区的视图创建为双缓冲区。</span> 
           <p> <span>新缓冲区的内容将从此缓冲区的当前位置开始。</span> <span>对这个缓冲区内容的更改将在新的缓冲区中可见，反之亦然;</span> <span>两个缓冲区的位置，极限和标记值将是独立的。</span> </p> 
           <p> <span>新缓冲区的位置将为零，其容量和限制将是该缓冲区中剩余的字节数除以8，其标记将不定义。</span> <span>如果只有这个缓冲区是直接的，并且只有当这个缓冲区是只读的时，这个缓冲区将是只读的。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             一个新的双缓冲区 
           </dd> 
          </dl> </li> 
        </ul> </li> 
      </ul> </li> 
    </ul> 
   </div> 
  </div>
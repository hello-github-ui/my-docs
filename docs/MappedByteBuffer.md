<div class="contentContainer"> 
   <ul class="inheritance"> 
    <li><a href="../../java/lang/Object.html" title="class in java.lang">java.lang.Object</a></li> 
    <li> 
     <ul class="inheritance"> 
      <li><a href="../../java/nio/Buffer.html" title="class in java.nio">java.nio.Buffer</a></li> 
      <li> 
       <ul class="inheritance"> 
        <li><a href="../../java/nio/ByteBuffer.html" title="class in java.nio">java.nio.ByteBuffer</a></li> 
        <li> 
         <ul class="inheritance"> 
          <li>java.nio.MappedByteBuffer</li> 
         </ul> </li> 
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
      <hr> <br> <pre>public abstract class <span class="typeNameLabel">MappedByteBuffer</span>
extends <a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a></pre> 
      <div class="block"> 
       <span>直接字节缓冲器，其内容是文件的存储器映射区域。</span> 
       <p> <span>映射的字节缓冲区是通过<a href="../../java/nio/channels/FileChannel.html#map-java.nio.channels.FileChannel.MapMode-long-long-"><code>FileChannel.map</code></a>方法创建的。</span> <span>此类扩展了具有特定于内存映射文件区域的操作的<a href="../../java/nio/ByteBuffer.html" title="java.nio中的类"><code>ByteBuffer</code></a>类。</span> </p> 
       <p> <span>映射字节缓冲区及其表示的文件映射在缓冲区本身被垃圾回收之前保持有效。</span> </p> 
       <p> <span>映射字节缓冲区的内容可以随时更改，例如，如果该程序或其他映射文件的对应区域的内容被更改。</span> <span>这种变化是否发生，何时发生，是操作系统依赖的，因此是未指定的。</span> <span><a name="inaccess"></a></span> </p> 
       <p> <span>映射字节缓冲区的全部或部分可能在任何时候变得无法访问，例如映射文件被截断。</span> <span>访问映射字节缓冲区的不可访问区域的尝试不会更改缓冲区的内容，并将导致在访问时或稍后的时候抛出未指定的异常。</span> <span>因此，强烈建议您采取适当的预防措施，以避免该程序或同时运行的程序对映射文件进行操作，但读取或写入文件的内容除外。</span> </p> 
       <p> <span>映射的字节缓冲区的行为与普通的直接字节缓冲区不同。</span> </p> 
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
          <span id="t4" class="tableTab"><span><a href="javascript:show(8);">具体的方法</a></span><span class="tabEnd">&nbsp;</span></span> 
         </caption> 
         <tbody> 
          <tr> 
           <th class="colFirst" scope="col">Modifier and Type</th> 
           <th class="colLast" scope="col">Method and Description</th> 
          </tr> 
          <tr id="i0" class="altColor"> 
           <td class="colFirst"><code><a href="../../java/nio/MappedByteBuffer.html" title="class in java.nio">MappedByteBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/MappedByteBuffer.html#force--">force</a></span>()</code> 
            <div class="block">
              强制将此缓冲区内容的任何更改写入包含映射文件的存储设备。 
            </div> </td> 
          </tr> 
          <tr id="i1" class="rowColor"> 
           <td class="colFirst"><code>boolean</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/MappedByteBuffer.html#isLoaded--">isLoaded</a></span>()</code> 
            <div class="block">
              告诉这个缓冲区的内容是否驻留在物理内存中。 
            </div> </td> 
          </tr> 
          <tr id="i2" class="altColor"> 
           <td class="colFirst"><code><a href="../../java/nio/MappedByteBuffer.html" title="class in java.nio">MappedByteBuffer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/MappedByteBuffer.html#load--">load</a></span>()</code> 
            <div class="block">
              将此缓冲区的内容加载到物理内存中。 
            </div> </td> 
          </tr> 
         </tbody> 
        </table> 
        <ul class="blockList"> 
         <li class="blockList"><a name="methods.inherited.from.class.java.nio.ByteBuffer"> 
           <!--   --> </a> <h3>Methods inherited from class&nbsp;java.nio.<a href="../../java/nio/ByteBuffer.html" title="class in java.nio">ByteBuffer</a></h3> <code><a href="../../java/nio/ByteBuffer.html#allocate-int-">allocate</a>, <a href="../../java/nio/ByteBuffer.html#allocateDirect-int-">allocateDirect</a>, <a href="../../java/nio/ByteBuffer.html#array--">array</a>, <a href="../../java/nio/ByteBuffer.html#arrayOffset--">arrayOffset</a>, <a href="../../java/nio/ByteBuffer.html#asCharBuffer--">asCharBuffer</a>, <a href="../../java/nio/ByteBuffer.html#asDoubleBuffer--">asDoubleBuffer</a>, <a href="../../java/nio/ByteBuffer.html#asFloatBuffer--">asFloatBuffer</a>, <a href="../../java/nio/ByteBuffer.html#asIntBuffer--">asIntBuffer</a>, <a href="../../java/nio/ByteBuffer.html#asLongBuffer--">asLongBuffer</a>, <a href="../../java/nio/ByteBuffer.html#asReadOnlyBuffer--">asReadOnlyBuffer</a>, <a href="../../java/nio/ByteBuffer.html#asShortBuffer--">asShortBuffer</a>, <a href="../../java/nio/ByteBuffer.html#compact--">compact</a>, <a href="../../java/nio/ByteBuffer.html#compareTo-java.nio.ByteBuffer-">compareTo</a>, <a href="../../java/nio/ByteBuffer.html#duplicate--">duplicate</a>, <a href="../../java/nio/ByteBuffer.html#equals-java.lang.Object-">equals</a>, <a href="../../java/nio/ByteBuffer.html#get--">get</a>, <a href="../../java/nio/ByteBuffer.html#get-byte:A-">get</a>, <a href="../../java/nio/ByteBuffer.html#get-byte:A-int-int-">get</a>, <a href="../../java/nio/ByteBuffer.html#get-int-">get</a>, <a href="../../java/nio/ByteBuffer.html#getChar--">getChar</a>, <a href="../../java/nio/ByteBuffer.html#getChar-int-">getChar</a>, <a href="../../java/nio/ByteBuffer.html#getDouble--">getDouble</a>, <a href="../../java/nio/ByteBuffer.html#getDouble-int-">getDouble</a>, <a href="../../java/nio/ByteBuffer.html#getFloat--">getFloat</a>, <a href="../../java/nio/ByteBuffer.html#getFloat-int-">getFloat</a>, <a href="../../java/nio/ByteBuffer.html#getInt--">getInt</a>, <a href="../../java/nio/ByteBuffer.html#getInt-int-">getInt</a>, <a href="../../java/nio/ByteBuffer.html#getLong--">getLong</a>, <a href="../../java/nio/ByteBuffer.html#getLong-int-">getLong</a>, <a href="../../java/nio/ByteBuffer.html#getShort--">getShort</a>, <a href="../../java/nio/ByteBuffer.html#getShort-int-">getShort</a>, <a href="../../java/nio/ByteBuffer.html#hasArray--">hasArray</a>, <a href="../../java/nio/ByteBuffer.html#hashCode--">hashCode</a>, <a href="../../java/nio/ByteBuffer.html#isDirect--">isDirect</a>, <a href="../../java/nio/ByteBuffer.html#order--">order</a>, <a href="../../java/nio/ByteBuffer.html#order-java.nio.ByteOrder-">order</a>, <a href="../../java/nio/ByteBuffer.html#put-byte-">put</a>, <a href="../../java/nio/ByteBuffer.html#put-byte:A-">put</a>, <a href="../../java/nio/ByteBuffer.html#put-byte:A-int-int-">put</a>, <a href="../../java/nio/ByteBuffer.html#put-java.nio.ByteBuffer-">put</a>, <a href="../../java/nio/ByteBuffer.html#put-int-byte-">put</a>, <a href="../../java/nio/ByteBuffer.html#putChar-char-">putChar</a>, <a href="../../java/nio/ByteBuffer.html#putChar-int-char-">putChar</a>, <a href="../../java/nio/ByteBuffer.html#putDouble-double-">putDouble</a>, <a href="../../java/nio/ByteBuffer.html#putDouble-int-double-">putDouble</a>, <a href="../../java/nio/ByteBuffer.html#putFloat-float-">putFloat</a>, <a href="../../java/nio/ByteBuffer.html#putFloat-int-float-">putFloat</a>, <a href="../../java/nio/ByteBuffer.html#putInt-int-">putInt</a>, <a href="../../java/nio/ByteBuffer.html#putInt-int-int-">putInt</a>, <a href="../../java/nio/ByteBuffer.html#putLong-int-long-">putLong</a>, <a href="../../java/nio/ByteBuffer.html#putLong-long-">putLong</a>, <a href="../../java/nio/ByteBuffer.html#putShort-int-short-">putShort</a>, <a href="../../java/nio/ByteBuffer.html#putShort-short-">putShort</a>, <a href="../../java/nio/ByteBuffer.html#slice--">slice</a>, <a href="../../java/nio/ByteBuffer.html#toString--">toString</a>, <a href="../../java/nio/ByteBuffer.html#wrap-byte:A-">wrap</a>, <a href="../../java/nio/ByteBuffer.html#wrap-byte:A-int-int-">wrap</a></code></li> 
        </ul> 
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
         <!--   --> </a> <h3>方法详细信息</h3> <a name="isLoaded--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>isLoaded</h4> <pre>public final&nbsp;boolean&nbsp;isLoaded()</pre> 
          <div class="block"> 
           <span>告诉这个缓冲区的内容是否驻留在物理内存中。</span> 
           <p> <span>返回值为<tt>true</tt>意味着该缓冲区中的所有数据很可能驻留在物理内存中，因此可能会被访问，而不会导致任何虚拟内存页面错误或I / O操作。</span> <span><tt>false</tt>的返回值并不一定意味着缓冲区的内容不会驻留在物理内存中。</span> </p> 
           <p> <span>返回的值是一个提示，而不是一个保证，因为底层操作系统可能会在调用此方法时返回一些缓冲区的数据。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd> 
            <tt>true</tt>如果这个缓冲区的内容很可能驻留在物理内存中 
           </dd> 
          </dl> </li> 
        </ul> <a name="load--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>load</h4> <pre>public final&nbsp;<a href="../../java/nio/MappedByteBuffer.html" title="class in java.nio">MappedByteBuffer</a>&nbsp;load()</pre> 
          <div class="block"> 
           <span>将此缓冲区的内容加载到物理内存中。</span> 
           <p> <span>这种方法尽最大努力确保当它返回时，该缓冲区的内容驻留在物理内存中。</span> <span>调用此方法可能会导致一些页面错误和I / O操作发生。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             这个缓冲区 
           </dd> 
          </dl> </li> 
        </ul> <a name="force--"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>force</h4> <pre>public final&nbsp;<a href="../../java/nio/MappedByteBuffer.html" title="class in java.nio">MappedByteBuffer</a>&nbsp;force()</pre> 
          <div class="block"> 
           <span>强制将此缓冲区内容的任何更改写入包含映射文件的存储设备。</span> 
           <p> <span>如果映射到此缓冲区的文件驻留在本地存储设备上，那么当此方法返回时，将保证自从创建缓冲区以来所做的所有更改，或自上次调用该方法后，都将被写入该设备。</span> </p> 
           <p> <span>如果文件不在本地设备上，则不会提供此类保证。</span> </p> 
           <p> <span>如果此缓冲区没有映射到读/写模式（ <a href="../../java/nio/channels/FileChannel.MapMode.html#READ_WRITE"><code>FileChannel.MapMode.READ_WRITE</code></a> ），则调用此方法将不起作用。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             这个缓冲区 
           </dd> 
          </dl> </li> 
        </ul> </li> 
      </ul> </li> 
    </ul> 
   </div> 
  </div>
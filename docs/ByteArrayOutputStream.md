<div class="contentContainer"> 
   <ul class="inheritance"> 
    <li><a href="../../java/lang/Object.html" title="class in java.lang">java.lang.Object</a></li> 
    <li> 
     <ul class="inheritance"> 
      <li><a href="../../java/io/OutputStream.html" title="class in java.io">java.io.OutputStream</a></li> 
      <li> 
       <ul class="inheritance"> 
        <li>java.io.ByteArrayOutputStream</li> 
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
        <span><a href="../../java/io/Closeable.html" title="java.io中的接口">Closeable</a> ， <a href="../../java/io/Flushable.html" title="java.io中的接口">Flushable</a> ， <a href="../../java/lang/AutoCloseable.html" title="java.lang中的接口">AutoCloseable</a></span> 
       </dd> 
      </dl> 
      <hr> <br> <pre>public class <span class="typeNameLabel">ByteArrayOutputStream</span>
extends <a href="../../java/io/OutputStream.html" title="class in java.io">OutputStream</a></pre> 
      <div class="block"> 
       <span>该类实现了将数据写入字节数组的输出流。</span> 
       <span>当数据写入缓冲区时，缓冲区会自动增长。</span> 
       <span>数据可以使用<code>toByteArray()</code>和<code>toString()</code> 。</span> 
       <p> <span>关闭<tt>ByteArrayOutputStream</tt>没有任何效果。</span> <span>该流中的方法可以在流关闭后调用，而不生成<tt>IOException</tt> 。</span> </p> 
      </div> 
      <dl> 
       <dt> 
        <span class="simpleTagLabel">从以下版本开始：</span> 
       </dt> 
       <dd>
         JDK1.0 
       </dd> 
      </dl> </li> 
    </ul> 
   </div> 
   <div class="summary"> 
    <ul class="blockList"> 
     <li class="blockList"> 
      <!-- =========== FIELD SUMMARY =========== --> 
      <ul class="blockList"> 
       <li class="blockList"><a name="field.summary"> 
         <!--   --> </a> <h3>Field Summary</h3> 
        <table class="memberSummary" border="0" cellpadding="3" cellspacing="0" summary="Field Summary table, listing fields, and an explanation"> 
         <caption> 
          <span>Fields</span> 
          <span class="tabEnd">&nbsp;</span> 
         </caption> 
         <tbody> 
          <tr> 
           <th class="colFirst" scope="col">Modifier and Type</th> 
           <th class="colLast" scope="col">Field and Description</th> 
          </tr> 
          <tr class="altColor"> 
           <td class="colFirst"><code>protected byte[]</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/ByteArrayOutputStream.html#buf">buf</a></span></code> 
            <div class="block">
              存储数据的缓冲区。 
            </div> </td> 
          </tr> 
          <tr class="rowColor"> 
           <td class="colFirst"><code>protected int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/ByteArrayOutputStream.html#count">count</a></span></code> 
            <div class="block">
              缓冲区中有效字节的数量。 
            </div> </td> 
          </tr> 
         </tbody> 
        </table> </li> 
      </ul> 
      <!-- ======== CONSTRUCTOR SUMMARY ======== --> 
      <ul class="blockList"> 
       <li class="blockList"><a name="constructor.summary"> 
         <!--   --> </a> <h3>构造方法摘要</h3> 
        <table class="memberSummary" border="0" cellpadding="3" cellspacing="0" summary="Constructor Summary table, listing constructors, and an explanation"> 
         <caption> 
          <span>构造方法</span> 
          <span class="tabEnd">&nbsp;</span> 
         </caption> 
         <tbody> 
          <tr> 
           <th class="colOne" scope="col">Constructor and Description</th> 
          </tr> 
          <tr class="altColor"> 
           <td class="colOne"><code><span class="memberNameLink"><a href="../../java/io/ByteArrayOutputStream.html#ByteArrayOutputStream--">ByteArrayOutputStream</a></span>()</code> 
            <div class="block">
              创建一个新的字节数组输出流。 
            </div> </td> 
          </tr> 
          <tr class="rowColor"> 
           <td class="colOne"><code><span class="memberNameLink"><a href="../../java/io/ByteArrayOutputStream.html#ByteArrayOutputStream-int-">ByteArrayOutputStream</a></span>(int&nbsp;size)</code> 
            <div class="block">
              创建一个新的字节数组输出流，具有指定大小的缓冲区容量（以字节为单位）。 
            </div> </td> 
          </tr> 
         </tbody> 
        </table> </li> 
      </ul> 
      <!-- ========== METHOD SUMMARY =========== --> 
      <ul class="blockList"> 
       <li class="blockList"><a name="method.summary"> 
         <!--   --> </a> <h3>方法摘要</h3> 
        <table class="memberSummary" border="0" cellpadding="3" cellspacing="0" summary="Method Summary table, listing methods, and an explanation"> 
         <caption> 
          <span id="t0" class="activeTableTab"><span>所有方法</span><span class="tabEnd">&nbsp;</span></span> 
          <span id="t2" class="tableTab"><span><a href="javascript:show(2);">接口方法</a></span><span class="tabEnd">&nbsp;</span></span> 
          <span id="t4" class="tableTab"><span><a href="javascript:show(8);">具体的方法</a></span><span class="tabEnd">&nbsp;</span></span> 
          <span id="t6" class="tableTab"><span><a href="javascript:show(32);">弃用的方法</a></span><span class="tabEnd">&nbsp;</span></span> 
         </caption> 
         <tbody> 
          <tr> 
           <th class="colFirst" scope="col">Modifier and Type</th> 
           <th class="colLast" scope="col">Method and Description</th> 
          </tr> 
          <tr id="i0" class="altColor"> 
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/ByteArrayOutputStream.html#close--">close</a></span>()</code> 
            <div class="block">
              关闭 
             <tt>ByteArrayOutputStream</tt>没有任何效果。 
            </div> </td> 
          </tr> 
          <tr id="i1" class="rowColor"> 
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/ByteArrayOutputStream.html#reset--">reset</a></span>()</code> 
            <div class="block">
              将此字节数组输出流的 
             <code>count</code>字段重置为零，以便丢弃输出流中当前累积的所有输出。 
            </div> </td> 
          </tr> 
          <tr id="i2" class="altColor"> 
           <td class="colFirst"><code>int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/ByteArrayOutputStream.html#size--">size</a></span>()</code> 
            <div class="block">
              返回缓冲区的当前大小。 
            </div> </td> 
          </tr> 
          <tr id="i3" class="rowColor"> 
           <td class="colFirst"><code>byte[]</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/ByteArrayOutputStream.html#toByteArray--">toByteArray</a></span>()</code> 
            <div class="block">
              创建一个新分配的字节数组。 
            </div> </td> 
          </tr> 
          <tr id="i4" class="altColor"> 
           <td class="colFirst"><code><a href="../../java/lang/String.html" title="class in java.lang">String</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/ByteArrayOutputStream.html#toString--">toString</a></span>()</code> 
            <div class="block">
              使用平台的默认字符集将缓冲区内容转换为字符串解码字节。 
            </div> </td> 
          </tr> 
          <tr id="i5" class="rowColor"> 
           <td class="colFirst"><code><a href="../../java/lang/String.html" title="class in java.lang">String</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/ByteArrayOutputStream.html#toString-int-">toString</a></span>(int&nbsp;hibyte)</code> 
            <div class="block"> 
             <span><span class="deprecatedLabel">已弃用</span></span> 
             <div class="block"> 
              <span><span class="deprecationComment">此方法无法将字节正确转换为字符。</span></span> 
              <span><span class="deprecationComment">从JDK 1.1的，要做到这一点的优选方法是通过<code>toString(String enc)</code>方法，它需要一个编码名称参数，或<code>toString()</code>方法，它使用平台的默认字符编码。</span></span> 
             </div> 
            </div> </td> 
          </tr> 
          <tr id="i6" class="altColor"> 
           <td class="colFirst"><code><a href="../../java/lang/String.html" title="class in java.lang">String</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/ByteArrayOutputStream.html#toString-java.lang.String-">toString</a></span>(<a href="../../java/lang/String.html" title="class in java.lang">String</a>&nbsp;charsetName)</code> 
            <div class="block"> 
             <span>通过使用命名的<a href="../../java/nio/charset/Charset.html" title="java.nio.charset中的类"><code>charset</code></a>解码字节，将缓冲区的内容转换为字符串。</span> 
            </div> </td> 
          </tr> 
          <tr id="i7" class="rowColor"> 
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/ByteArrayOutputStream.html#write-byte:A-int-int-">write</a></span>(byte[]&nbsp;b, int&nbsp;off, int&nbsp;len)</code> 
            <div class="block">
              从指定的字节数组写入 
             <code>len</code>字节，从偏移量为 
             <code>off</code>开始，输出到这个字节数组输出流。 
            </div> </td> 
          </tr> 
          <tr id="i8" class="altColor"> 
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/ByteArrayOutputStream.html#write-int-">write</a></span>(int&nbsp;b)</code> 
            <div class="block">
              将指定的字节写入此字节数组输出流。 
            </div> </td> 
          </tr> 
          <tr id="i9" class="rowColor"> 
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/ByteArrayOutputStream.html#writeTo-java.io.OutputStream-">writeTo</a></span>(<a href="../../java/io/OutputStream.html" title="class in java.io">OutputStream</a>&nbsp;out)</code> 
            <div class="block">
              将此字节数组输出流的完整内容写入指定的输出流参数，就像使用 
             <code>out.write(buf, 0, count)</code>调用输出流的写入方法 
             <code>out.write(buf, 0, count)</code> 。 
            </div> </td> 
          </tr> 
         </tbody> 
        </table> 
        <ul class="blockList"> 
         <li class="blockList"><a name="methods.inherited.from.class.java.io.OutputStream"> 
           <!--   --> </a> <h3>Methods inherited from class&nbsp;java.io.<a href="../../java/io/OutputStream.html" title="class in java.io">OutputStream</a></h3> <code><a href="../../java/io/OutputStream.html#flush--">flush</a>, <a href="../../java/io/OutputStream.html#write-byte:A-">write</a></code></li> 
        </ul> 
        <ul class="blockList"> 
         <li class="blockList"><a name="methods.inherited.from.class.java.lang.Object"> 
           <!--   --> </a> <h3>Methods inherited from class&nbsp;java.lang.<a href="../../java/lang/Object.html" title="class in java.lang">Object</a></h3> <code><a href="../../java/lang/Object.html#clone--">clone</a>, <a href="../../java/lang/Object.html#equals-java.lang.Object-">equals</a>, <a href="../../java/lang/Object.html#finalize--">finalize</a>, <a href="../../java/lang/Object.html#getClass--">getClass</a>, <a href="../../java/lang/Object.html#hashCode--">hashCode</a>, <a href="../../java/lang/Object.html#notify--">notify</a>, <a href="../../java/lang/Object.html#notifyAll--">notifyAll</a>, <a href="../../java/lang/Object.html#wait--">wait</a>, <a href="../../java/lang/Object.html#wait-long-">wait</a>, <a href="../../java/lang/Object.html#wait-long-int-">wait</a></code></li> 
        </ul> </li> 
      </ul> </li> 
    </ul> 
   </div> 
   <div class="details"> 
    <ul class="blockList"> 
     <li class="blockList"> 
      <!-- ============ FIELD DETAIL =========== --> 
      <ul class="blockList"> 
       <li class="blockList"><a name="field.detail"> 
         <!--   --> </a> <h3>字段详细信息</h3> <a name="buf"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>buf</h4> <pre>protected&nbsp;byte[] buf</pre> 
          <div class="block">
            存储数据的缓冲区。 
          </div> </li> 
        </ul> <a name="count"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>count</h4> <pre>protected&nbsp;int count</pre> 
          <div class="block">
            缓冲区中有效字节的数量。 
          </div> </li> 
        </ul> </li> 
      </ul> 
      <!-- ========= CONSTRUCTOR DETAIL ======== --> 
      <ul class="blockList"> 
       <li class="blockList"><a name="constructor.detail"> 
         <!--   --> </a> <h3>构造方法详细信息</h3> <a name="ByteArrayOutputStream--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>ByteArrayOutputStream</h4> <pre>public&nbsp;ByteArrayOutputStream()</pre> 
          <div class="block"> 
           <span>创建一个新的字节数组输出流。</span> 
           <span>缓冲区容量最初为32字节，但如果需要，其容量会增加。</span> 
          </div> </li> 
        </ul> <a name="ByteArrayOutputStream-int-"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>ByteArrayOutputStream</h4> <pre>public&nbsp;ByteArrayOutputStream(int&nbsp;size)</pre> 
          <div class="block">
            创建一个新的字节数组输出流，具有指定大小的缓冲区容量（以字节为单位）。 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>size</code> - 初始尺寸。 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/IllegalArgumentException.html" title="class in java.lang">IllegalArgumentException</a></code> - 如果大小为负数。 
           </dd> 
          </dl> </li> 
        </ul> </li> 
      </ul> 
      <!-- ============ METHOD DETAIL ========== --> 
      <ul class="blockList"> 
       <li class="blockList"><a name="method.detail"> 
         <!--   --> </a> <h3>方法详细信息</h3> <a name="write-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>write</h4> <pre>public&nbsp;void&nbsp;write(int&nbsp;b)</pre> 
          <div class="block">
            将指定的字节写入此字节数组输出流。 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">Specified by:</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/OutputStream.html#write-int-">write</a></code>在 
            <code><a href="../../java/io/OutputStream.html" title="class in java.io">OutputStream</a></code> 
           </dd> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>b</code> - 要写入的字节。 
           </dd> 
          </dl> </li> 
        </ul> <a name="write-byte:A-int-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>write</h4> <pre>public&nbsp;void&nbsp;write(byte[]&nbsp;b,
                  int&nbsp;off,
                  int&nbsp;len)</pre> 
          <div class="block">
            写入 
           <code>len</code>从指定的字节数组以偏移字节 
           <code>off</code>该字节数组输出流。 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/OutputStream.html#write-byte:A-int-int-">write</a></code>在类别 
            <code><a href="../../java/io/OutputStream.html" title="class in java.io">OutputStream</a></code> 
           </dd> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>b</code> - 数据。 
           </dd> 
           <dd> 
            <code>off</code> - 数据中的起始偏移量。 
           </dd> 
           <dd> 
            <code>len</code> - 要写入的字节数。 
           </dd> 
          </dl> </li> 
        </ul> <a name="writeTo-java.io.OutputStream-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>writeTo</h4> <pre>public&nbsp;void&nbsp;writeTo(<a href="../../java/io/OutputStream.html" title="class in java.io">OutputStream</a>&nbsp;out)
             throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block">
            将此字节数组输出流的完整内容写入指定的输出流参数，就像使用 
           <code>out.write(buf, 0, count)</code>调用输出流的写入方法 
           <code>out.write(buf, 0, count)</code> 。 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>out</code> - 要写入数据的输出流。 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生I / O错误。 
           </dd> 
          </dl> </li> 
        </ul> <a name="reset--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>reset</h4> <pre>public&nbsp;void&nbsp;reset()</pre> 
          <div class="block"> 
           <span>将此字节数组输出流的<code>count</code>字段重置为零，以便丢弃输出流中当前累积的所有输出。</span> 
           <span>可以再次使用输出流，重用已经分配的缓冲区空间。</span> 
          </div> 
          <dl> 
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <a href="../../java/io/ByteArrayInputStream.html#count"><code>ByteArrayInputStream.count</code></a> 
           </dd> 
          </dl> </li> 
        </ul> <a name="toByteArray--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>toByteArray</h4> <pre>public&nbsp;byte[]&nbsp;toByteArray()</pre> 
          <div class="block"> 
           <span>创建一个新分配的字节数组。</span> 
           <span>其大小是此输出流的当前大小，缓冲区的有效内容已被复制到其中。</span> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             该输出流的当前内容，作为字节数组。 
           </dd> 
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <a href="../../java/io/ByteArrayOutputStream.html#size--"><code>size()</code></a> 
           </dd> 
          </dl> </li> 
        </ul> <a name="size--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>size</h4> <pre>public&nbsp;int&nbsp;size()</pre> 
          <div class="block">
            返回缓冲区的当前大小。 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd> 
            <code>count</code>字段的值，这是此输出流中有效字节的数量。 
           </dd> 
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <a href="../../java/io/ByteArrayOutputStream.html#count"><code>count</code></a> 
           </dd> 
          </dl> </li> 
        </ul> <a name="toString--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>toString</h4> <pre>public&nbsp;<a href="../../java/lang/String.html" title="class in java.lang">String</a>&nbsp;toString()</pre> 
          <div class="block"> 
           <span>使用平台的默认字符集将缓冲区内容转换为字符串解码字节。</span> 
           <span>新的<tt>String</tt>的长度是字符集的函数，因此可能不等于缓冲区的大小。</span> 
           <p> <span>该方法总是使用默认替换字符串替换格式错误的输入和不可映射的字符序列，用于平台的默认字符集。</span> <span>当需要更多的解码过程控制时，应使用<a href="../../java/nio/charset/CharsetDecoder.html" title="java.nio.charset中的类">CharsetDecoder</a>类。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/Object.html#toString--">toString</a></code>在类别 
            <code><a href="../../java/lang/Object.html" title="class in java.lang">Object</a></code> 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             从缓冲区的内容中解码字符串。 
           </dd> 
           <dt> 
            <span class="simpleTagLabel">从以下版本开始：</span> 
           </dt> 
           <dd>
             JDK1.1 
           </dd> 
          </dl> </li> 
        </ul> <a name="toString-java.lang.String-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>toString</h4> <pre>public&nbsp;<a href="../../java/lang/String.html" title="class in java.lang">String</a>&nbsp;toString(<a href="../../java/lang/String.html" title="class in java.lang">String</a>&nbsp;charsetName)
                throws <a href="../../java/io/UnsupportedEncodingException.html" title="class in java.io">UnsupportedEncodingException</a></pre> 
          <div class="block"> 
           <span>通过使用命名的<a href="../../java/nio/charset/Charset.html" title="java.nio.charset中的类"><code>charset</code></a>解码字节将缓冲区的内容转换为字符串。</span> 
           <span>新的<tt>String</tt>的长度是字符集的函数，因此可能不等于字节数组的长度。</span> 
           <p> <span>此方法总是用此字符集的默认替换字符串替换格式错误的输入和不可映射字符序列。</span> <span>当需要更多的解码过程控制时，应使用<a href="../../java/nio/charset/CharsetDecoder.html" title="java.nio.charset中的类"><code>CharsetDecoder</code></a>类。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <span><code>charsetName</code> - 支持的名称<a href="../../java/nio/charset/Charset.html" title="java.nio.charset中的类"><code>charset</code></a></span> 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             从缓冲区的内容中解码字符串。 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/UnsupportedEncodingException.html" title="class in java.io">UnsupportedEncodingException</a></code> - 如果不支持命名的字符集 
           </dd> 
           <dt> 
            <span class="simpleTagLabel">从以下版本开始：</span> 
           </dt> 
           <dd>
             JDK1.1 
           </dd> 
          </dl> </li> 
        </ul> <a name="toString-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>toString</h4> <pre><a href="../../java/lang/Deprecated.html" title="annotation in java.lang">@Deprecated</a>
public&nbsp;<a href="../../java/lang/String.html" title="class in java.lang">String</a>&nbsp;toString(int&nbsp;hibyte)</pre> 
          <div class="block"> 
           <span><span class="deprecatedLabel">已弃用</span></span> 
           <span><span class="deprecationComment">此方法无法将字节正确转换为字符。</span></span> 
           <span><span class="deprecationComment">从JDK 1.1的，要做到这一点的优选方法是通过<code>toString(String enc)</code>方法，它需要一个编码名称参数，或<code>toString()</code>方法，它使用平台的默认字符编码。</span></span> 
          </div> 
          <div class="block"> 
           <span>创建一个新分配的字符串。</span> 
           <span>其大小是输出流的当前大小，并且缓冲区的有效内容已被复制到其中。</span> 
           <span>结果字符串中的每个字符<i>c</i>由字节数组中的相应元素<i>b</i>构成，使得：</span> 
           <blockquote> 
            <span><pre>     c == (char)(((hibyte &amp; 0xff) &lt;&lt; 8) | (b &amp; 0xff))
 </pre></span> 
           </blockquote> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>hibyte</code> - 每个生成的Unicode字符的高字节。 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             输出流的当前内容，作为一个字符串。 
           </dd> 
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <a href="../../java/io/ByteArrayOutputStream.html#size--"><code>size()</code></a> ， 
            <a href="../../java/io/ByteArrayOutputStream.html#toString-java.lang.String-"><code>toString(String)</code></a> ， 
            <a href="../../java/io/ByteArrayOutputStream.html#toString--"><code>toString()</code></a> 
           </dd> 
          </dl> </li> 
        </ul> <a name="close--"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>close</h4> <pre>public&nbsp;void&nbsp;close()
           throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>关闭<tt>ByteArrayOutputStream</tt>没有任何效果。</span> 
           <span>该流中的方法可以在流关闭后调用，而不生成<tt>IOException</tt> 。</span> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">Specified by:</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/Closeable.html#close--">close</a></code>在界面 
            <code><a href="../../java/io/Closeable.html" title="interface in java.io">Closeable</a></code> 
           </dd> 
           <dt> 
            <span class="overrideSpecifyLabel">Specified by:</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/AutoCloseable.html#close--">close</a></code>在界面 
            <code><a href="../../java/lang/AutoCloseable.html" title="interface in java.lang">AutoCloseable</a></code> 
           </dd> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/OutputStream.html#close--">close</a></code>在 
            <code><a href="../../java/io/OutputStream.html" title="class in java.io">OutputStream</a></code> 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生I / O错误。 
           </dd> 
          </dl> </li> 
        </ul> </li> 
      </ul> </li> 
    </ul> 
   </div> 
  </div>
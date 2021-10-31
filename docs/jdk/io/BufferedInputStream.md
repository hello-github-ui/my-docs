<div class="contentContainer"> 
   <ul class="inheritance"> 
    <li><a href="../../java/lang/Object.html" title="class in java.lang">java.lang.Object</a></li> 
    <li> 
     <ul class="inheritance"> 
      <li><a href="../../java/io/InputStream.html" title="class in java.io">java.io.InputStream</a></li> 
      <li> 
       <ul class="inheritance"> 
        <li><a href="../../java/io/FilterInputStream.html" title="class in java.io">java.io.FilterInputStream</a></li> 
        <li> 
         <ul class="inheritance"> 
          <li>java.io.BufferedInputStream</li> 
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
        <span><a href="../../java/io/Closeable.html" title="java.io中的接口">Closeable</a> ， <a href="../../java/lang/AutoCloseable.html" title="java.lang中的接口">AutoCloseable</a></span> 
       </dd> 
      </dl> 
      <hr> <br> <pre>public class <span class="typeNameLabel">BufferedInputStream</span>
extends <a href="../../java/io/FilterInputStream.html" title="class in java.io">FilterInputStream</a></pre> 
      <div class="block"> 
       <span>A <code>BufferedInputStream</code>为另一个输入流添加了功能，即缓冲输入和支持<code>mark</code>和<code>reset</code>方法的功能。</span> 
       <span>当创建<code>BufferedInputStream</code>时，将创建一个内部缓冲区数组。</span> 
       <span>当从流中读取或跳过字节时，内部缓冲区将根据需要从所包含的输入流中重新填充，一次有多个字节。</span> 
       <span><code>mark</code>操作会记住输入流中的一点，并且<code>reset</code>操作会导致从最近的<code>mark</code>操作之后读取的所有字节在从包含的输入流中取出新的字节之前重新读取。</span> 
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
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedInputStream.html#buf">buf</a></span></code> 
            <div class="block">
              存储数据的内部缓冲区数组。 
            </div> </td> 
          </tr> 
          <tr class="rowColor"> 
           <td class="colFirst"><code>protected int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedInputStream.html#count">count</a></span></code> 
            <div class="block">
              索引一大于缓冲区中最后一个有效字节的索引。 
            </div> </td> 
          </tr> 
          <tr class="altColor"> 
           <td class="colFirst"><code>protected int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedInputStream.html#marklimit">marklimit</a></span></code> 
            <div class="block"> 
             <code>mark</code>方法调用后，最大超前允许，后续调用 
             <code>reset</code>方法失败。 
            </div> </td> 
          </tr> 
          <tr class="rowColor"> 
           <td class="colFirst"><code>protected int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedInputStream.html#markpos">markpos</a></span></code> 
            <div class="block"> 
             <code>pos</code>字段在最后一个 
             <code>mark</code>方法被调用时的值。 
            </div> </td> 
          </tr> 
          <tr class="altColor"> 
           <td class="colFirst"><code>protected int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedInputStream.html#pos">pos</a></span></code> 
            <div class="block">
              缓冲区中的当前位置。 
            </div> </td> 
          </tr> 
         </tbody> 
        </table> 
        <ul class="blockList"> 
         <li class="blockList"><a name="fields.inherited.from.class.java.io.FilterInputStream"> 
           <!--   --> </a> <h3>Fields inherited from class&nbsp;java.io.<a href="../../java/io/FilterInputStream.html" title="class in java.io">FilterInputStream</a></h3> <code><a href="../../java/io/FilterInputStream.html#in">in</a></code></li> 
        </ul> </li> 
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
           <td class="colOne"><code><span class="memberNameLink"><a href="../../java/io/BufferedInputStream.html#BufferedInputStream-java.io.InputStream-">BufferedInputStream</a></span>(<a href="../../java/io/InputStream.html" title="class in java.io">InputStream</a>&nbsp;in)</code> 
            <div class="block">
              创建一个 
             <code>BufferedInputStream</code>并保存其参数，输入流 
             <code>in</code> ，供以后使用。 
            </div> </td> 
          </tr> 
          <tr class="rowColor"> 
           <td class="colOne"><code><span class="memberNameLink"><a href="../../java/io/BufferedInputStream.html#BufferedInputStream-java.io.InputStream-int-">BufferedInputStream</a></span>(<a href="../../java/io/InputStream.html" title="class in java.io">InputStream</a>&nbsp;in, int&nbsp;size)</code> 
            <div class="block">
              创建 
             <code>BufferedInputStream</code>具有指定缓冲区大小，并保存其参数，输入流 
             <code>in</code> ，供以后使用。 
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
         </caption> 
         <tbody> 
          <tr> 
           <th class="colFirst" scope="col">Modifier and Type</th> 
           <th class="colLast" scope="col">Method and Description</th> 
          </tr> 
          <tr id="i0" class="altColor"> 
           <td class="colFirst"><code>int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedInputStream.html#available--">available</a></span>()</code> 
            <div class="block">
              返回从该输入流中可以读取（或跳过）的字节数的估计值，而不会被下一次调用此输入流的方法阻塞。 
            </div> </td> 
          </tr> 
          <tr id="i1" class="rowColor"> 
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedInputStream.html#close--">close</a></span>()</code> 
            <div class="block">
              关闭此输入流并释放与流相关联的任何系统资源。 
            </div> </td> 
          </tr> 
          <tr id="i2" class="altColor"> 
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedInputStream.html#mark-int-">mark</a></span>(int&nbsp;readlimit)</code> 
            <div class="block">
              见的总承包 
             <code>mark</code>的方法 
             <code>InputStream</code> 。 
            </div> </td> 
          </tr> 
          <tr id="i3" class="rowColor"> 
           <td class="colFirst"><code>boolean</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedInputStream.html#markSupported--">markSupported</a></span>()</code> 
            <div class="block">
              测试这个输入流是否支持 
             <code>mark</code>和 
             <code>reset</code>方法。 
            </div> </td> 
          </tr> 
          <tr id="i4" class="altColor"> 
           <td class="colFirst"><code>int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedInputStream.html#read--">read</a></span>()</code> 
            <div class="block">
              见 
             <code>read</code>法 
             <code>InputStream</code>的一般合同。 
            </div> </td> 
          </tr> 
          <tr id="i5" class="rowColor"> 
           <td class="colFirst"><code>int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedInputStream.html#read-byte:A-int-int-">read</a></span>(byte[]&nbsp;b, int&nbsp;off, int&nbsp;len)</code> 
            <div class="block">
              从给定的偏移开始，将字节输入流中的字节读入指定的字节数组。 
            </div> </td> 
          </tr> 
          <tr id="i6" class="altColor"> 
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedInputStream.html#reset--">reset</a></span>()</code> 
            <div class="block">
              见 
             <code>reset</code>法 
             <code>InputStream</code>的一般合同。 
            </div> </td> 
          </tr> 
          <tr id="i7" class="rowColor"> 
           <td class="colFirst"><code>long</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedInputStream.html#skip-long-">skip</a></span>(long&nbsp;n)</code> 
            <div class="block">
              见 
             <code>skip</code>法 
             <code>InputStream</code>的一般合同。 
            </div> </td> 
          </tr> 
         </tbody> 
        </table> 
        <ul class="blockList"> 
         <li class="blockList"><a name="methods.inherited.from.class.java.io.FilterInputStream"> 
           <!--   --> </a> <h3>Methods inherited from class&nbsp;java.io.<a href="../../java/io/FilterInputStream.html" title="class in java.io">FilterInputStream</a></h3> <code><a href="../../java/io/FilterInputStream.html#read-byte:A-">read</a></code></li> 
        </ul> 
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
      <!-- ============ FIELD DETAIL =========== --> 
      <ul class="blockList"> 
       <li class="blockList"><a name="field.detail"> 
         <!--   --> </a> <h3>字段详细信息</h3> <a name="buf"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>buf</h4> <pre>protected volatile&nbsp;byte[] buf</pre> 
          <div class="block"> 
           <span>存储数据的内部缓冲区数组。</span> 
           <span>必要时，可以用不同大小的另一个阵列代替。</span> 
          </div> </li> 
        </ul> <a name="count"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>count</h4> <pre>protected&nbsp;int count</pre> 
          <div class="block"> 
           <span>索引一大于缓冲区中最后一个有效字节的索引。</span> 
           <span>此值始终在<code>0</code>到<code>buf.length</code> ;</span> 
           <span>元素<code>buf[0]</code>至<code>buf[count-1]</code>包含从底层输入流获得的缓冲输入数据。</span> 
          </div> </li> 
        </ul> <a name="pos"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>pos</h4> <pre>protected&nbsp;int pos</pre> 
          <div class="block"> 
           <span>缓冲区中的当前位置。</span> 
           <span>这是从<code>buf</code>数组读取的下一个字符的索引。</span> 
           <p> <span>此值始终在<code>0</code>到<code>count</code> 。</span> <span>如果小于<code>count</code> ，那么<code>buf[pos]</code>是作为输入提供的下一个字节;</span> <span>如果等于<code>count</code> ，那么接下来的<code>read</code>或<code>skip</code>操作将需要从包含的输入流读取更多的字节。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <a href="../../java/io/BufferedInputStream.html#buf"><code>buf</code></a> 
           </dd> 
          </dl> </li> 
        </ul> <a name="markpos"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>markpos</h4> <pre>protected&nbsp;int markpos</pre> 
          <div class="block"> 
           <span><code>pos</code>字段在最后一个<code>mark</code>方法被调用时的值。</span> 
           <p> <span>此值始终在<code>-1</code>到<code>pos</code> 。</span> <span>如果输入流中没有标记位置，则此字段为<code>-1</code> 。</span> <span>如果在输入流中有一个标记的位置，那么<code>buf[markpos]</code>是<code>reset</code>操作后作为输入提供的第一个字节。</span> <span>如果<code>markpos</code>不是<code>-1</code> ，然后从位置的所有字节<code>buf[markpos]</code>通过<code>buf[pos-1]</code>必须保留在缓冲器阵列中（尽管它们可以被移动到缓冲器阵列中的另一个处，与适当的调整的值<code>count</code> ， <code>pos</code>和<code>markpos</code> ）;</span> <span>除非<code>pos</code>和<code>markpos</code>之间的<code>markpos</code>超过<code>marklimit</code> 。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <a href="../../java/io/BufferedInputStream.html#mark-int-"><code>mark(int)</code></a> ， 
            <a href="../../java/io/BufferedInputStream.html#pos"><code>pos</code></a> 
           </dd> 
          </dl> </li> 
        </ul> <a name="marklimit"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>marklimit</h4> <pre>protected&nbsp;int marklimit</pre> 
          <div class="block"> 
           <span>读取的最大的一个电话后，允许提前<code>mark</code>后续调用方法之前<code>reset</code>方法失败。</span> 
           <span>每当之间的差别<code>pos</code>和<code>markpos</code>超过<code>marklimit</code> ，则标记可以被设置下降<code>markpos</code>到<code>-1</code> 。</span> 
          </div> 
          <dl> 
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <a href="../../java/io/BufferedInputStream.html#mark-int-"><code>mark(int)</code></a> ， 
            <a href="../../java/io/BufferedInputStream.html#reset--"><code>reset()</code></a> 
           </dd> 
          </dl> </li> 
        </ul> </li> 
      </ul> 
      <!-- ========= CONSTRUCTOR DETAIL ======== --> 
      <ul class="blockList"> 
       <li class="blockList"><a name="constructor.detail"> 
         <!--   --> </a> <h3>构造方法详细信息</h3> <a name="BufferedInputStream-java.io.InputStream-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>BufferedInputStream</h4> <pre>public&nbsp;BufferedInputStream(<a href="../../java/io/InputStream.html" title="class in java.io">InputStream</a>&nbsp;in)</pre> 
          <div class="block"> 
           <span>创建一个<code>BufferedInputStream</code>并保存其参数，输入流<code>in</code>供以后使用。</span> 
           <span>内部缓冲区数组创建并存储在<code>buf</code> 。</span> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>in</code> - 底层输入流。 
           </dd> 
          </dl> </li> 
        </ul> <a name="BufferedInputStream-java.io.InputStream-int-"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>BufferedInputStream</h4> <pre>public&nbsp;BufferedInputStream(<a href="../../java/io/InputStream.html" title="class in java.io">InputStream</a>&nbsp;in,
                           int&nbsp;size)</pre> 
          <div class="block"> 
           <span>创建具有<code>BufferedInputStream</code>缓冲区大小的BufferedInputStream，并保存其参数，输入流<code>in</code>供以后使用。</span> 
           <span>长度为<code>size</code>的内部缓冲区阵列被创建并存储在<code>buf</code> 。</span> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>in</code> - 底层输入流。 
           </dd> 
           <dd> 
            <code>size</code> - 缓冲区大小。 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/IllegalArgumentException.html" title="class in java.lang">IllegalArgumentException</a></code> - 如果 
            <code>size &lt;= 0</code> 。 
           </dd> 
          </dl> </li> 
        </ul> </li> 
      </ul> 
      <!-- ============ METHOD DETAIL ========== --> 
      <ul class="blockList"> 
       <li class="blockList"><a name="method.detail"> 
         <!--   --> </a> <h3>方法详细信息</h3> <a name="read--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>read</h4> <pre>public&nbsp;int&nbsp;read()
         throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block">
            见 
           <code>read</code>法 
           <code>InputStream</code>的一般合同。 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/FilterInputStream.html#read--">read</a></code>在 
            <code><a href="../../java/io/FilterInputStream.html" title="class in java.io">FilterInputStream</a></code> 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             数据的下一个字节，如果达到流的末尾， 
            <code>-1</code> 。 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果此输入流已通过调用其 
            <a href="../../java/io/BufferedInputStream.html#close--"><code>close()</code></a>方法已关闭，或发生I / O错误。 
           </dd> 
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <a href="../../java/io/FilterInputStream.html#in"><code>FilterInputStream.in</code></a> 
           </dd> 
          </dl> </li> 
        </ul> <a name="read-byte:A-int-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>read</h4> <pre>public&nbsp;int&nbsp;read(byte[]&nbsp;b,
                int&nbsp;off,
                int&nbsp;len)
         throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>从给定的偏移开始，将字节输入流中的字节读入指定的字节数组。</span> 
           <p> <span>该方法执行<code><a href="../../java/io/InputStream.html" title="class in java.io"><code>InputStream</code></a></code>类对应的<code><a href="../../java/io/InputStream.html#read-byte:A-int-int-"><code>read</code></a></code>方法的一般合同。</span> <span>作为一个额外的方便，它尝试通过重复调用基础流的<code>read</code>方法来读取尽可能多的字节。</span> <span>此迭代<code>read</code>继续，直至<code>read</code>条件之一为止：</span> </p> 
           <ul> 
            <li> <span>指定的字节数已被读取，</span> </li> 
            <li> <span>底层流的<code>read</code>方法返回<code>-1</code> ，表示文件结尾，或</span> </li> 
            <li> <span>底层流的<code>available</code>方法返回零，表示进一步的输入请求将阻塞。</span> </li> 
           </ul> 
           <span>如果基础流上的第一个<code>read</code>返回<code>-1</code>以指示文件结束，则此方法返回<code>-1</code> 。</span> 
           <span>否则，此方法返回实际读取的字节数。</span> 
           <p> <span>鼓励这个类的子类，但不是必需的，尝试以相同的方式读取尽可能多的字节。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/FilterInputStream.html#read-byte:A-int-int-">read</a></code>在 
            <code><a href="../../java/io/FilterInputStream.html" title="class in java.io">FilterInputStream</a></code> 
           </dd> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>b</code> - 目的缓冲区。 
           </dd> 
           <dd> 
            <code>off</code> - 开始存储字节的偏移量。 
           </dd> 
           <dd> 
            <code>len</code> - 要读取的最大字节数。 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             读取的字节数，或 
            <code>-1</code>如果流已到达）。 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果此输入流已通过调用其 
            <a href="../../java/io/BufferedInputStream.html#close--"><code>close()</code></a>方法关闭，或发生I / O错误。 
           </dd> 
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <a href="../../java/io/FilterInputStream.html#in"><code>FilterInputStream.in</code></a> 
           </dd> 
          </dl> </li> 
        </ul> <a name="skip-long-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>skip</h4> <pre>public&nbsp;long&nbsp;skip(long&nbsp;n)
          throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block">
            见的总承包 
           <code>skip</code>的方法 
           <code>InputStream</code> 。 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/FilterInputStream.html#skip-long-">skip</a></code>在 
            <code><a href="../../java/io/FilterInputStream.html" title="class in java.io">FilterInputStream</a></code> 
           </dd> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>n</code> - 要跳过的字节数。 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             实际跳过的字节数。 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果流不支持查询，或者如果此输入流已通过调用其 
            <a href="../../java/io/BufferedInputStream.html#close--"><code>close()</code></a>方法关闭，或发生I / O错误。 
           </dd> 
          </dl> </li> 
        </ul> <a name="available--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>available</h4> <pre>public&nbsp;int&nbsp;available()
              throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>返回从该输入流中可以读取（或跳过）的字节数的估计值，而不会被下一次调用此输入流的方法阻塞。</span> 
           <span>下一个调用可能是同一个线程或另一个线程。</span> 
           <span>这个多个字节的单个读取或跳过将不会被阻塞，但可以读取或跳过较少的字节。</span> 
           <p> <span>该方法返回缓冲区（ <code>count&nbsp;- pos</code> ）中要读取的剩余字节数和调用<a href="../../java/io/FilterInputStream.html#in"><code>in</code></a> .available（）的结果。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/FilterInputStream.html#available--">available</a></code>在 
            <code><a href="../../java/io/FilterInputStream.html" title="class in java.io">FilterInputStream</a></code> 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             可以从该输入流中读取（或跳过）的字节数，而不阻塞。 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果此输入流已通过调用其 
            <a href="../../java/io/BufferedInputStream.html#close--"><code>close()</code></a>方法关闭，或发生I / O错误。 
           </dd> 
          </dl> </li> 
        </ul> <a name="mark-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>mark</h4> <pre>public&nbsp;void&nbsp;mark(int&nbsp;readlimit)</pre> 
          <div class="block">
            见的总承包 
           <code>mark</code>的方法 
           <code>InputStream</code> 。 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/FilterInputStream.html#mark-int-">mark</a></code>在类别 
            <code><a href="../../java/io/FilterInputStream.html" title="class in java.io">FilterInputStream</a></code> 
           </dd> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>readlimit</code> - 标记位置无效之前可以读取的最大字节数限制。 
           </dd> 
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <a href="../../java/io/BufferedInputStream.html#reset--"><code>reset()</code></a> 
           </dd> 
          </dl> </li> 
        </ul> <a name="reset--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>reset</h4> <pre>public&nbsp;void&nbsp;reset()
           throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>见的总承包<code>reset</code>的方法<code>InputStream</code> 。</span> 
           <p> <span>如果<code>markpos</code>是<code>-1</code> （没有设置标记或标记已被无效），则抛出<code>IOException</code> 。</span> <span>否则， <code>pos</code>设置等于<code>markpos</code> 。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/FilterInputStream.html#reset--">reset</a></code>在类别 
            <code><a href="../../java/io/FilterInputStream.html" title="class in java.io">FilterInputStream</a></code> 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果该流未被标记，或者如果该标记已被无效，或通过调用其 
            <a href="../../java/io/BufferedInputStream.html#close--"><code>close()</code></a>方法已关闭流或发生I / O错误。 
           </dd> 
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <a href="../../java/io/BufferedInputStream.html#mark-int-"><code>mark(int)</code></a> 
           </dd> 
          </dl> </li> 
        </ul> <a name="markSupported--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>markSupported</h4> <pre>public&nbsp;boolean&nbsp;markSupported()</pre> 
          <div class="block"> 
           <span>测试此输入流是否支持<code>mark</code>和<code>reset</code>方法。</span> 
           <span><code>markSupported</code>方法<code>BufferedInputStream</code>返回<code>true</code> 。</span> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/FilterInputStream.html#markSupported--">markSupported</a></code>在 
            <code><a href="../../java/io/FilterInputStream.html" title="class in java.io">FilterInputStream</a></code> 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             一个 
            <code>boolean</code>指示这种流类型是否支持 
            <code>mark</code>和 
            <code>reset</code>方法。 
           </dd> 
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <a href="../../java/io/InputStream.html#mark-int-"><code>InputStream.mark(int)</code></a> ， 
            <a href="../../java/io/InputStream.html#reset--"><code>InputStream.reset()</code></a> 
           </dd> 
          </dl> </li> 
        </ul> <a name="close--"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>close</h4> <pre>public&nbsp;void&nbsp;close()
           throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>关闭此输入流并释放与流相关联的任何系统资源。</span> 
           <span>一旦流已关闭，进一步的read（），available（），reset（）或skip（）调用将抛出IOException异常。</span> 
           <span>关闭以前关闭的流无效。</span> 
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
            <code><a href="../../java/io/FilterInputStream.html#close--">close</a></code>在 
            <code><a href="../../java/io/FilterInputStream.html" title="class in java.io">FilterInputStream</a></code> 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生I / O错误。 
           </dd> 
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <a href="../../java/io/FilterInputStream.html#in"><code>FilterInputStream.in</code></a> 
           </dd> 
          </dl> </li> 
        </ul> </li> 
      </ul> </li> 
    </ul> 
   </div> 
  </div>
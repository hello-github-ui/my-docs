<div class="contentContainer"> 
   <ul class="inheritance"> 
    <li><a href="../../java/lang/Object.html" title="class in java.lang">java.lang.Object</a></li> 
    <li> 
     <ul class="inheritance"> 
      <li><a href="../../java/io/InputStream.html" title="class in java.io">java.io.InputStream</a></li> 
      <li> 
       <ul class="inheritance"> 
        <li>java.io.ByteArrayInputStream</li> 
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
      <hr> <br> <pre>public class <span class="typeNameLabel">ByteArrayInputStream</span>
extends <a href="../../java/io/InputStream.html" title="class in java.io">InputStream</a></pre> 
      <div class="block"> 
       <span>A <code>ByteArrayInputStream</code>包含一个内部缓冲区，其中包含可以从流中读取的字节。</span> 
       <span>内部计数器跟踪<code>read</code>方法要提供的下一个字节。</span> 
       <p> <span>关闭<tt>ByteArrayInputStream</tt>没有任何效果。</span> <span>在关闭流之后，可以调用此类中的方法，而不生成<tt>IOException</tt> 。</span> </p> 
      </div> 
      <dl> 
       <dt> 
        <span class="simpleTagLabel">从以下版本开始：</span> 
       </dt> 
       <dd>
         JDK1.0 
       </dd> 
       <dt> 
        <span class="seeLabel">另请参见：</span> 
       </dt> 
       <dd> 
        <span><a href="../../java/io/StringBufferInputStream.html" title="java.io中的类"><code>StringBufferInputStream</code></a></span> 
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
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/ByteArrayInputStream.html#buf">buf</a></span></code> 
            <div class="block">
              由数据流的创建者提供的字节数组。 
            </div> </td> 
          </tr> 
          <tr class="rowColor"> 
           <td class="colFirst"><code>protected int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/ByteArrayInputStream.html#count">count</a></span></code> 
            <div class="block">
              索引一大于输入流缓冲区中的最后一个有效字符。 
            </div> </td> 
          </tr> 
          <tr class="altColor"> 
           <td class="colFirst"><code>protected int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/ByteArrayInputStream.html#mark">mark</a></span></code> 
            <div class="block">
              流中当前标记的位置。 
            </div> </td> 
          </tr> 
          <tr class="rowColor"> 
           <td class="colFirst"><code>protected int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/ByteArrayInputStream.html#pos">pos</a></span></code> 
            <div class="block">
              从输入流缓冲区读取的下一个字符的索引。 
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
           <td class="colOne"><code><span class="memberNameLink"><a href="../../java/io/ByteArrayInputStream.html#ByteArrayInputStream-byte:A-">ByteArrayInputStream</a></span>(byte[]&nbsp;buf)</code> 
            <div class="block">
              创建一个 
             <code>ByteArrayInputStream</code> ，使其使用 
             <code>buf</code>作为其缓冲区数组。 
            </div> </td> 
          </tr> 
          <tr class="rowColor"> 
           <td class="colOne"><code><span class="memberNameLink"><a href="../../java/io/ByteArrayInputStream.html#ByteArrayInputStream-byte:A-int-int-">ByteArrayInputStream</a></span>(byte[]&nbsp;buf, int&nbsp;offset, int&nbsp;length)</code> 
            <div class="block">
              创建 
             <code>ByteArrayInputStream</code>使用 
             <code>buf</code>作为其缓冲器阵列。 
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
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/ByteArrayInputStream.html#available--">available</a></span>()</code> 
            <div class="block">
              返回可从此输入流读取（或跳过）的剩余字节数。 
            </div> </td> 
          </tr> 
          <tr id="i1" class="rowColor"> 
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/ByteArrayInputStream.html#close--">close</a></span>()</code> 
            <div class="block">
              关闭 
             <tt>ByteArrayInputStream</tt>没有任何效果。 
            </div> </td> 
          </tr> 
          <tr id="i2" class="altColor"> 
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/ByteArrayInputStream.html#mark-int-">mark</a></span>(int&nbsp;readAheadLimit)</code> 
            <div class="block">
              设置流中当前标记的位置。 
            </div> </td> 
          </tr> 
          <tr id="i3" class="rowColor"> 
           <td class="colFirst"><code>boolean</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/ByteArrayInputStream.html#markSupported--">markSupported</a></span>()</code> 
            <div class="block">
              测试 
             <code>InputStream</code>是否支持标记/复位。 
            </div> </td> 
          </tr> 
          <tr id="i4" class="altColor"> 
           <td class="colFirst"><code>int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/ByteArrayInputStream.html#read--">read</a></span>()</code> 
            <div class="block">
              从该输入流读取下一个数据字节。 
            </div> </td> 
          </tr> 
          <tr id="i5" class="rowColor"> 
           <td class="colFirst"><code>int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/ByteArrayInputStream.html#read-byte:A-int-int-">read</a></span>(byte[]&nbsp;b, int&nbsp;off, int&nbsp;len)</code> 
            <div class="block">
              将 
             <code>len</code>字节的数据读入此输入流中的字节数组。 
            </div> </td> 
          </tr> 
          <tr id="i6" class="altColor"> 
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/ByteArrayInputStream.html#reset--">reset</a></span>()</code> 
            <div class="block">
              将缓冲区重置为标记位置。 
            </div> </td> 
          </tr> 
          <tr id="i7" class="rowColor"> 
           <td class="colFirst"><code>long</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/ByteArrayInputStream.html#skip-long-">skip</a></span>(long&nbsp;n)</code> 
            <div class="block">
              从此输入流跳过 
             <code>n</code>个字节的输入。 
            </div> </td> 
          </tr> 
         </tbody> 
        </table> 
        <ul class="blockList"> 
         <li class="blockList"><a name="methods.inherited.from.class.java.io.InputStream"> 
           <!--   --> </a> <h3>Methods inherited from class&nbsp;java.io.<a href="../../java/io/InputStream.html" title="class in java.io">InputStream</a></h3> <code><a href="../../java/io/InputStream.html#read-byte:A-">read</a></code></li> 
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
         <li class="blockList"> <h4>buf</h4> <pre>protected&nbsp;byte[] buf</pre> 
          <div class="block"> 
           <span>由数据流的创建者提供的字节数组。</span> 
           <span>元素<code>buf[0]</code>至<code>buf[count-1]</code>是唯一可以从流中读取的字节;</span> 
           <span>元素<code>buf[pos]</code>是要读取的下一个字节。</span> 
          </div> </li> 
        </ul> <a name="pos"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>pos</h4> <pre>protected&nbsp;int pos</pre> 
          <div class="block"> 
           <span>从输入流缓冲区读取的下一个字符的索引。</span> 
           <span>该值应始终为非负数，不得大于<code>count</code>的值。</span> 
           <span>要从输入流缓冲区读取的下一个字节将为<code>buf[pos]</code> 。</span> 
          </div> </li> 
        </ul> <a name="mark"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>mark</h4> <pre>protected&nbsp;int mark</pre> 
          <div class="block"> 
           <span>流中当前标记的位置。</span> 
           <span>当构造时，ByteArrayInputStream对象在默认情况下标记为零。</span> 
           <span>它们可以通过<code>mark()</code>方法标记在缓冲区内的另一个位置。</span> 
           <span>目前的缓冲区位置由<code>reset()</code>方法设置。</span> 
           <p> <span>如果没有设置标记，则标记的值是传递给构造函数的偏移量（如果没有提供偏移量，则为0）。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="simpleTagLabel">从以下版本开始：</span> 
           </dt> 
           <dd>
             JDK1.1 
           </dd> 
          </dl> </li> 
        </ul> <a name="count"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>count</h4> <pre>protected&nbsp;int count</pre> 
          <div class="block"> 
           <span>索引一大于输入流缓冲区中的最后一个有效字符。</span> 
           <span>该值应始终为非负数，不得大于<code>buf</code>的长度。</span> 
           <span>它大于<code>buf</code>中可以从输入流缓冲区读取的最后一个字节的位置。</span> 
          </div> </li> 
        </ul> </li> 
      </ul> 
      <!-- ========= CONSTRUCTOR DETAIL ======== --> 
      <ul class="blockList"> 
       <li class="blockList"><a name="constructor.detail"> 
         <!--   --> </a> <h3>构造方法详细信息</h3> <a name="ByteArrayInputStream-byte:A-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>ByteArrayInputStream</h4> <pre>public&nbsp;ByteArrayInputStream(byte[]&nbsp;buf)</pre> 
          <div class="block"> 
           <span>创建一个<code>ByteArrayInputStream</code> ，使其使用<code>buf</code>作为其缓冲区数组。</span> 
           <span>缓冲区数组不被复制。</span> 
           <span>的初始值<code>pos</code>是<code>0</code>和的初始值<code>count</code>是长度<code>buf</code> 。</span> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>buf</code> - 输入缓冲区。 
           </dd> 
          </dl> </li> 
        </ul> <a name="ByteArrayInputStream-byte:A-int-int-"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>ByteArrayInputStream</h4> <pre>public&nbsp;ByteArrayInputStream(byte[]&nbsp;buf,
                            int&nbsp;offset,
                            int&nbsp;length)</pre> 
          <div class="block"> 
           <span>创建<code>ByteArrayInputStream</code>使用<code>buf</code>作为其缓冲器阵列。</span> 
           <span>的初始值<code>pos</code>是<code>offset</code>和的初始值<code>count</code>是的最小<code>offset+length</code>和<code>buf.length</code> 。</span> 
           <span>缓冲区数组不被复制。</span> 
           <span>缓冲区的标记设置为指定的偏移量。</span> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>buf</code> - 输入缓冲区。 
           </dd> 
           <dd> 
            <code>offset</code> - 要读取的第一个字节的缓冲区中的偏移量。 
           </dd> 
           <dd> 
            <code>length</code> - 从缓冲区读取的最大字节数。 
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
         <li class="blockList"> <h4>read</h4> <pre>public&nbsp;int&nbsp;read()</pre> 
          <div class="block"> 
           <span>从该输入流读取下一个数据字节。</span> 
           <span>值字节返回为<code>int</code> ，范围为<code>0</code>至<code>255</code> 。</span> 
           <span>如果没有字节可用，因为流已经到达，则返回值<code>-1</code> 。</span> 
           <p> <span>这个<code>read</code>方法无法阻止。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">Specified by:</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/InputStream.html#read--">read</a></code>在 
            <code><a href="../../java/io/InputStream.html" title="class in java.io">InputStream</a></code> 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             数据的下一个字节，如果已经达到流的末尾， 
            <code>-1</code> 。 
           </dd> 
          </dl> </li> 
        </ul> <a name="read-byte:A-int-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>read</h4> <pre>public&nbsp;int&nbsp;read(byte[]&nbsp;b,
                int&nbsp;off,
                int&nbsp;len)</pre> 
          <div class="block"> 
           <span>从此输入流读取最多<code>len</code>字节的数据到一个字节数组。</span> 
           <span>如果<code>pos</code>等于<code>count</code> ，则返回<code>-1</code>以指示文件结束。</span> 
           <span>否则，读取的字节数为<code>k</code>等于<code>len</code>和<code>count-pos</code>中的较小<code>count-pos</code> 。</span> 
           <span>如果<code>k</code>为正，则字节<code>buf[pos]</code>通过<code>buf[pos+k-1]</code>被复制到<code>b[off]</code>通过<code>b[off+k-1]</code>中所执行的方式<code>System.arraycopy</code> 。</span> 
           <span>值<code>k</code>被添加到<code>pos</code>并返回<code>k</code> 。</span> 
           <p> <span>这个<code>read</code>方法不能阻止。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/InputStream.html#read-byte:A-int-int-">read</a></code>在 
            <code><a href="../../java/io/InputStream.html" title="class in java.io">InputStream</a></code> 
           </dd> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>b</code> - 读取数据的缓冲区。 
           </dd> 
           <dd> 
            <code>off</code> - 目标数组中的起始偏移量 
            <code>b</code> 
           </dd> 
           <dd> 
            <code>len</code> - 读取的最大字节数。 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             读取到缓冲区的总字节数，如果没有更多的数据，因为已经到达流的末尾， 
            <code>-1</code> 。 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/NullPointerException.html" title="class in java.lang">NullPointerException</a></code> - 如果 
            <code>b</code>是 
            <code>null</code> 。 
           </dd> 
           <dd> 
            <code><a href="../../java/lang/IndexOutOfBoundsException.html" title="class in java.lang">IndexOutOfBoundsException</a></code> - 如果 
            <code>off</code>为负数，则 
            <code>len</code>为负数，或 
            <code>len</code>大于 
            <code>b.length - off</code> 
           </dd> 
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <a href="../../java/io/InputStream.html#read--"><code>InputStream.read()</code></a> 
           </dd> 
          </dl> </li> 
        </ul> <a name="skip-long-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>skip</h4> <pre>public&nbsp;long&nbsp;skip(long&nbsp;n)</pre> 
          <div class="block"> 
           <span>从此输入流跳过<code>n</code>个字节的输入。</span> 
           <span>如果达到输入流的结尾，则可能会跳过更少的字节。</span> 
           <span>要跳过的字节的实际数字为<code>k</code>等于<code>n</code>和<code>count-pos</code>中的较小<code>count-pos</code> 。</span> 
           <span>值<code>k</code>被添加到<code>pos</code> ，返回<code>k</code> 。</span> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/InputStream.html#skip-long-">skip</a></code>在 
            <code><a href="../../java/io/InputStream.html" title="class in java.io">InputStream</a></code> 
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
          </dl> </li> 
        </ul> <a name="available--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>available</h4> <pre>public&nbsp;int&nbsp;available()</pre> 
          <div class="block"> 
           <span>返回可从此输入流读取（或跳过）的剩余字节数。</span> 
           <p> <span>返回的值为<code>count&nbsp;- pos</code> ，这是从输入缓冲区读取的剩余字节数。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/InputStream.html#available--">available</a></code>在类别 
            <code><a href="../../java/io/InputStream.html" title="class in java.io">InputStream</a></code> 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             可以从该输入流中读取（或跳过）而不阻塞的剩余字节数。 
           </dd> 
          </dl> </li> 
        </ul> <a name="markSupported--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>markSupported</h4> <pre>public&nbsp;boolean&nbsp;markSupported()</pre> 
          <div class="block"> 
           <span>测试<code>InputStream</code>是否支持标记/复位。</span> 
           <span>该<code>markSupported</code>的方法<code>ByteArrayInputStream</code>总是返回<code>true</code> 。</span> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/InputStream.html#markSupported--">markSupported</a></code>在 
            <code><a href="../../java/io/InputStream.html" title="class in java.io">InputStream</a></code> 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd> 
            <span><code>true</code>如果这个流实例支持标记和重置方法;</span> 
            <span><code>false</code>否则。</span> 
           </dd> 
           <dt> 
            <span class="simpleTagLabel">从以下版本开始：</span> 
           </dt> 
           <dd>
             JDK1.1 
           </dd> 
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <a href="../../java/io/InputStream.html#mark-int-"><code>InputStream.mark(int)</code></a> ， 
            <a href="../../java/io/InputStream.html#reset--"><code>InputStream.reset()</code></a> 
           </dd> 
          </dl> </li> 
        </ul> <a name="mark-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>mark</h4> <pre>public&nbsp;void&nbsp;mark(int&nbsp;readAheadLimit)</pre> 
          <div class="block"> 
           <span>设置流中当前标记的位置。</span> 
           <span>当构造时，ByteArrayInputStream对象在默认情况下标记为零。</span> 
           <span>它们可以通过此方法标记在缓冲区内的另一个位置。</span> 
           <p> <span>如果没有设置标记，则标记的值是传递给构造函数的偏移量（如果没有提供偏移量，则为0）。</span> </p> 
           <p> <span>注意：这个班的<code>readAheadLimit</code>没有意义。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/InputStream.html#mark-int-">mark</a></code>在类别 
            <code><a href="../../java/io/InputStream.html" title="class in java.io">InputStream</a></code> 
           </dd> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>readAheadLimit</code> - 标记位置无效之前可以读取的最大字节数限制。 
           </dd> 
           <dt> 
            <span class="simpleTagLabel">从以下版本开始：</span> 
           </dt> 
           <dd>
             JDK1.1 
           </dd> 
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <a href="../../java/io/InputStream.html#reset--"><code>InputStream.reset()</code></a> 
           </dd> 
          </dl> </li> 
        </ul> <a name="reset--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>reset</h4> <pre>public&nbsp;void&nbsp;reset()</pre> 
          <div class="block"> 
           <span>将缓冲区重置为标记位置。</span> 
           <span>标记位置为0，除非在构造函数中指定了另一个位置或者指定了一个偏移量。</span> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/InputStream.html#reset--">reset</a></code>在 
            <code><a href="../../java/io/InputStream.html" title="class in java.io">InputStream</a></code> 
           </dd> 
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <span><a href="../../java/io/InputStream.html#mark-int-"><code>InputStream.mark(int)</code></a> ， <a href="../../java/io/IOException.html" title="java.io中的类"><code>IOException</code></a></span> 
           </dd> 
          </dl> </li> 
        </ul> <a name="close--"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>close</h4> <pre>public&nbsp;void&nbsp;close()
           throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>关闭<tt>ByteArrayInputStream</tt>没有任何效果。</span> 
           <span>在关闭流之后，可以调用此类中的方法，而不生成<tt>IOException</tt> 。</span> 
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
            <code><a href="../../java/io/InputStream.html#close--">close</a></code>在 
            <code><a href="../../java/io/InputStream.html" title="class in java.io">InputStream</a></code> 
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
<div class="contentContainer"> 
   <ul class="inheritance"> 
    <li><a href="../../java/lang/Object.html" title="class in java.lang">java.lang.Object</a></li> 
    <li> 
     <ul class="inheritance"> 
      <li><a href="../../java/io/Reader.html" title="class in java.io">java.io.Reader</a></li> 
      <li> 
       <ul class="inheritance"> 
        <li>java.io.BufferedReader</li> 
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
        <span><a href="../../java/io/Closeable.html" title="java.io中的接口">Closeable</a> ， <a href="../../java/lang/AutoCloseable.html" title="java.lang中的接口">AutoCloseable</a> ， <a href="../../java/lang/Readable.html" title="java.lang中的接口">Readable</a></span> 
       </dd> 
      </dl> 
      <dl> 
       <dt>
        已知直接子类：
       </dt> 
       <dd> 
        <span><a href="../../java/io/LineNumberReader.html" title="java.io中的类">LineNumberReader</a></span> 
       </dd> 
      </dl> 
      <hr> <br> <pre>public class <span class="typeNameLabel">BufferedReader</span>
extends <a href="../../java/io/Reader.html" title="class in java.io">Reader</a></pre> 
      <div class="block"> 
       <span>从字符输入流读取文本，缓冲字符，以提供字符，数组和行的高效读取。</span> 
       <p> <span>可以指定缓冲区大小，或者可以使用默认大小。</span> <span>默认值足够大，可用于大多数用途。</span> </p> 
       <p> <span>通常，由读取器做出的每个读取请求将引起对底层字符或字节流的相应读取请求。</span> <span>因此，建议将BufferedReader包装在其read（）操作可能昂贵的读取器上，例如FileReaders和InputStreamReaders。</span> <span>例如，</span> </p> 
       <pre>  <span>BufferedReader in
   = new BufferedReader(new FileReader("foo.in"));</span> </pre> 
       <span>将缓冲指定文件的输入。</span> 
       <span>没有缓冲，每次调用read（）或readLine（）可能会导致从文件中读取字节，转换成字符，然后返回，这可能非常低效。</span> 
       <p> <span>使用DataInputStreams进行文本输入的程序可以通过用适当的BufferedReader替换每个DataInputStream进行本地化。</span> </p> 
      </div> 
      <dl> 
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
        <span><a href="../../java/io/FileReader.html" title="java.io中的类"><code>FileReader</code></a> ， <a href="../../java/io/InputStreamReader.html" title="java.io中的类"><code>InputStreamReader</code></a> ， <a href="../../java/nio/file/Files.html#newBufferedReader-java.nio.file.Path-java.nio.charset.Charset-"><code>Files.newBufferedReader(java.nio.file.Path, java.nio.charset.Charset)</code></a></span> 
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
        <ul class="blockList"> 
         <li class="blockList"><a name="fields.inherited.from.class.java.io.Reader"> 
           <!--   --> </a> <h3>Fields inherited from class&nbsp;java.io.<a href="../../java/io/Reader.html" title="class in java.io">Reader</a></h3> <code><a href="../../java/io/Reader.html#lock">lock</a></code></li> 
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
           <td class="colOne"><code><span class="memberNameLink"><a href="../../java/io/BufferedReader.html#BufferedReader-java.io.Reader-">BufferedReader</a></span>(<a href="../../java/io/Reader.html" title="class in java.io">Reader</a>&nbsp;in)</code> 
            <div class="block">
              创建使用默认大小的输入缓冲区的缓冲字符输入流。 
            </div> </td> 
          </tr> 
          <tr class="rowColor"> 
           <td class="colOne"><code><span class="memberNameLink"><a href="../../java/io/BufferedReader.html#BufferedReader-java.io.Reader-int-">BufferedReader</a></span>(<a href="../../java/io/Reader.html" title="class in java.io">Reader</a>&nbsp;in, int&nbsp;sz)</code> 
            <div class="block">
              创建使用指定大小的输入缓冲区的缓冲字符输入流。 
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
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedReader.html#close--">close</a></span>()</code> 
            <div class="block">
              关闭流并释放与之相关联的任何系统资源。 
            </div> </td> 
          </tr> 
          <tr id="i1" class="rowColor"> 
           <td class="colFirst"><code><a href="../../java/util/stream/Stream.html" title="interface in java.util.stream">Stream</a>&lt;<a href="../../java/lang/String.html" title="class in java.lang">String</a>&gt;</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedReader.html#lines--">lines</a></span>()</code> 
            <div class="block">
              返回一个 
             <code>Stream</code> ，其元素是从这个 
             <code>BufferedReader</code>读取的行。 
            </div> </td> 
          </tr> 
          <tr id="i2" class="altColor"> 
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedReader.html#mark-int-">mark</a></span>(int&nbsp;readAheadLimit)</code> 
            <div class="block">
              标记流中的当前位置。 
            </div> </td> 
          </tr> 
          <tr id="i3" class="rowColor"> 
           <td class="colFirst"><code>boolean</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedReader.html#markSupported--">markSupported</a></span>()</code> 
            <div class="block">
              告诉这个流是否支持mark（）操作。 
            </div> </td> 
          </tr> 
          <tr id="i4" class="altColor"> 
           <td class="colFirst"><code>int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedReader.html#read--">read</a></span>()</code> 
            <div class="block">
              读一个字符 
            </div> </td> 
          </tr> 
          <tr id="i5" class="rowColor"> 
           <td class="colFirst"><code>int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedReader.html#read-char:A-int-int-">read</a></span>(char[]&nbsp;cbuf, int&nbsp;off, int&nbsp;len)</code> 
            <div class="block">
              将字符读入数组的一部分。 
            </div> </td> 
          </tr> 
          <tr id="i6" class="altColor"> 
           <td class="colFirst"><code><a href="../../java/lang/String.html" title="class in java.lang">String</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedReader.html#readLine--">readLine</a></span>()</code> 
            <div class="block">
              读一行文字。 
            </div> </td> 
          </tr> 
          <tr id="i7" class="rowColor"> 
           <td class="colFirst"><code>boolean</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedReader.html#ready--">ready</a></span>()</code> 
            <div class="block">
              告诉这个流是否准备好被读取。 
            </div> </td> 
          </tr> 
          <tr id="i8" class="altColor"> 
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedReader.html#reset--">reset</a></span>()</code> 
            <div class="block">
              将流重置为最近的标记。 
            </div> </td> 
          </tr> 
          <tr id="i9" class="rowColor"> 
           <td class="colFirst"><code>long</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedReader.html#skip-long-">skip</a></span>(long&nbsp;n)</code> 
            <div class="block">
              跳过字符 
            </div> </td> 
          </tr> 
         </tbody> 
        </table> 
        <ul class="blockList"> 
         <li class="blockList"><a name="methods.inherited.from.class.java.io.Reader"> 
           <!--   --> </a> <h3>Methods inherited from class&nbsp;java.io.<a href="../../java/io/Reader.html" title="class in java.io">Reader</a></h3> <code><a href="../../java/io/Reader.html#read-char:A-">read</a>, <a href="../../java/io/Reader.html#read-java.nio.CharBuffer-">read</a></code></li> 
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
      <!-- ========= CONSTRUCTOR DETAIL ======== --> 
      <ul class="blockList"> 
       <li class="blockList"><a name="constructor.detail"> 
         <!--   --> </a> <h3>构造方法详细信息</h3> <a name="BufferedReader-java.io.Reader-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>BufferedReader</h4> <pre>public&nbsp;BufferedReader(<a href="../../java/io/Reader.html" title="class in java.io">Reader</a>&nbsp;in,
                      int&nbsp;sz)</pre> 
          <div class="block">
            创建使用指定大小的输入缓冲区的缓冲字符输入流。 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>in</code> - 阅读器 
           </dd> 
           <dd> 
            <code>sz</code> - 输入缓冲区大小 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/IllegalArgumentException.html" title="class in java.lang">IllegalArgumentException</a></code> - 如果 
            <code>sz &lt;= 0</code> 
           </dd> 
          </dl> </li> 
        </ul> <a name="BufferedReader-java.io.Reader-"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>BufferedReader</h4> <pre>public&nbsp;BufferedReader(<a href="../../java/io/Reader.html" title="class in java.io">Reader</a>&nbsp;in)</pre> 
          <div class="block">
            创建使用默认大小的输入缓冲区的缓冲字符输入流。 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>in</code> - 读者 
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
            读一个字符 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/Reader.html#read--">read</a></code>在 
            <code><a href="../../java/io/Reader.html" title="class in java.io">Reader</a></code> 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             字符读取，作为0到65535（ 
            <tt>0x00-0xffff</tt> ）范围内的整数，如果已经达到流的结尾，则为-1。 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生I / O错误 
           </dd> 
          </dl> </li> 
        </ul> <a name="read-char:A-int-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>read</h4> <pre>public&nbsp;int&nbsp;read(char[]&nbsp;cbuf,
                int&nbsp;off,
                int&nbsp;len)
         throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>将字符读入数组的一部分。</span> 
           <p> <span>该方法执行<code><a href="../../java/io/Reader.html" title="class in java.io"><code>Reader</code></a></code>类的相应<code><a href="../../java/io/Reader.html#read-char:A-int-int-"><code>read</code></a></code>方法的一般合同。</span> <span>作为一个额外的方便，它尝试通过重复调用基础流的<code>read</code>方法来读取尽可能多的字符。</span> <span>这个迭代<code>read</code>继续，直到下列条件之一成立：</span> </p> 
           <ul> 
            <li> <span>指定的字符数已被读取，</span> </li> 
            <li> <span>底层流的<code>read</code>方法返回<code>-1</code> ，表示文件结尾，或</span> </li> 
            <li> <span>底层流的<code>ready</code>方法返回<code>false</code> ，表示进一步的输入请求将阻塞。</span> </li> 
           </ul> 
           <span>如果底层流上的第一个<code>read</code>返回<code>-1</code>以指示文件结束，则此方法返回<code>-1</code> 。</span> 
           <span>否则，此方法返回实际读取的字符数。</span> 
           <p> <span>鼓励这个类的子类，但不是必需的，尝试以相同的方式读取尽可能多的字符。</span> </p> 
           <p> <span>通常这种方法从这个流的字符缓冲区中获取字符，并根据需要从底层流中填充它。</span> <span>但是，如果缓冲区为空，则该标记无效，并且所请求的长度至少与缓冲区一样大，则该方法将直接从基础流中读取字符到给定的数组中。</span> <span>因此冗余<code>BufferedReader</code>将不会不必要地复制数据。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">Specified by:</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/Reader.html#read-char:A-int-int-">read</a></code>在类别 
            <code><a href="../../java/io/Reader.html" title="class in java.io">Reader</a></code> 
           </dd> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>cbuf</code> - 目的缓冲区 
           </dd> 
           <dd> 
            <code>off</code> - 开始存储字符的偏移量 
           </dd> 
           <dd> 
            <code>len</code> - 要读取的最大字符数 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             读取的字符数，如果已经达到流的结尾，则为-1 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生I / O错误 
           </dd> 
          </dl> </li> 
        </ul> <a name="readLine--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>readLine</h4> <pre>public&nbsp;<a href="../../java/lang/String.html" title="class in java.lang">String</a>&nbsp;readLine()
                throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>读一行文字。</span> 
           <span>一行被视为由换行符（'\ n'），回车符（'\ r'）中的任何一个或随后的换行符终止。</span> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             包含行的内容的字符串，不包括任何行终止字符，如果已达到流的末尾，则为null 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生I / O错误 
           </dd> 
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <a href="../../java/nio/file/Files.html#readAllLines-java.nio.file.Path-java.nio.charset.Charset-"><code>Files.readAllLines(java.nio.file.Path, java.nio.charset.Charset)</code></a> 
           </dd> 
          </dl> </li> 
        </ul> <a name="skip-long-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>skip</h4> <pre>public&nbsp;long&nbsp;skip(long&nbsp;n)
          throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block">
            跳过字符 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/Reader.html#skip-long-">skip</a></code>在 
            <code><a href="../../java/io/Reader.html" title="class in java.io">Reader</a></code> 
           </dd> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>n</code> - 要跳过的字符数 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             实际跳过的字符数 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/IllegalArgumentException.html" title="class in java.lang">IllegalArgumentException</a></code> - 如果 
            <code>n</code>为负数。 
           </dd> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生I / O错误 
           </dd> 
          </dl> </li> 
        </ul> <a name="ready--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>ready</h4> <pre>public&nbsp;boolean&nbsp;ready()
              throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>告诉这个流是否准备好被读取。</span> 
           <span>如果缓冲区不为空，或者底层字符流准备就绪，则缓冲字符流就绪。</span> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/Reader.html#ready--">ready</a></code>在类别 
            <code><a href="../../java/io/Reader.html" title="class in java.io">Reader</a></code> 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd> 
            <span>如果下一个read（）保证不阻止输入，则为True，否则为false。</span> 
            <span>请注意，返回false并不能保证下一次读取将被阻止。</span> 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生I / O错误 
           </dd> 
          </dl> </li> 
        </ul> <a name="markSupported--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>markSupported</h4> <pre>public&nbsp;boolean&nbsp;markSupported()</pre> 
          <div class="block">
            告诉这个流是否支持mark（）操作。 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/Reader.html#markSupported--">markSupported</a></code>在 
            <code><a href="../../java/io/Reader.html" title="class in java.io">Reader</a></code> 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             当且仅当此流支持标记操作时才为真。 
           </dd> 
          </dl> </li> 
        </ul> <a name="mark-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>mark</h4> <pre>public&nbsp;void&nbsp;mark(int&nbsp;readAheadLimit)
          throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>标记流中的当前位置。</span> 
           <span>对reset（）的后续调用将尝试将流重新定位到此位置。</span> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/Reader.html#mark-int-">mark</a></code>在 
            <code><a href="../../java/io/Reader.html" title="class in java.io">Reader</a></code> 
           </dd> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <span><code>readAheadLimit</code> - 限制仍然保留标记时可能读取的字符数。</span> 
            <span>在读取字符到此限制或超出之后，尝试重新设置流可能会失败。</span> 
            <span>大于输入缓冲区大小的限制值将导致新的缓冲区被分配，其大小不小于limit。</span> 
            <span>因此，应谨慎使用大量值。</span> 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/IllegalArgumentException.html" title="class in java.lang">IllegalArgumentException</a></code> - 如果 
            <code>readAheadLimit &lt; 0</code> 
           </dd> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生I / O错误 
           </dd> 
          </dl> </li> 
        </ul> <a name="reset--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>reset</h4> <pre>public&nbsp;void&nbsp;reset()
           throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block">
            将流重置为最近的标记。 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/Reader.html#reset--">reset</a></code>在 
            <code><a href="../../java/io/Reader.html" title="class in java.io">Reader</a></code> 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果流未被标记，或者标记已被无效 
           </dd> 
          </dl> </li> 
        </ul> <a name="close--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>close</h4> <pre>public&nbsp;void&nbsp;close()
           throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span class="descfrmTypeLabel">描述从类别： <code><a href="../../java/io/Reader.html#close--">Reader</a></code>复制</span> 
          </div> 
          <div class="block"> 
           <span>关闭流并释放与之相关联的任何系统资源。</span> 
           <span>一旦流已关闭，进一步的read（），ready（），mark（），reset（）或skip（）调用将抛出IOException。</span> 
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
            <span class="overrideSpecifyLabel">Specified by:</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/Reader.html#close--">close</a></code>在 
            <code><a href="../../java/io/Reader.html" title="class in java.io">Reader</a></code> 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生I / O错误 
           </dd> 
          </dl> </li> 
        </ul> <a name="lines--"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>lines</h4> <pre>public&nbsp;<a href="../../java/util/stream/Stream.html" title="interface in java.util.stream">Stream</a>&lt;<a href="../../java/lang/String.html" title="class in java.lang">String</a>&gt;&nbsp;lines()</pre> 
          <div class="block"> 
           <span>返回一个<code>Stream</code> ，其元素是从这个<code>BufferedReader</code>读取的行。</span> 
           <span><a href="../../java/util/stream/Stream.html" title="java.util.stream中的接口"><code>Stream</code></a>是懒惰的人群，即只读在<a href="../util/stream/package-summary.html#StreamOps">terminal stream operation</a>期间。</span> 
           <p> <span>在执行终端流操作期间，读取器不能被操作。</span> <span>否则，终端流操作的结果未定义。</span> </p> 
           <p> <span>在执行终端流操作之后，不能保证读取器将处于从其读取下一个字符或行的特定位置。</span> </p> 
           <p> <span>如果在<a href="../../java/io/IOException.html" title="java.io中的类">访问底层BufferedReader</a>时抛出<code>BufferedReader</code> ，它将被包裹在<a href="../../java/io/UncheckedIOException.html" title="java.io中的类"><code>UncheckedIOException</code>中</a> ，这将从导致读取的<code>Stream</code>方法抛出。</span> <span>如果在关闭的BufferedReader中调用该方法，则此方法将返回一个Stream。</span> <span>该流的任何操作需要在关闭之后从BufferedReader读取，将导致抛出UncheckedIOException异常。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             一个 
            <code>Stream&lt;String&gt;</code>提供了这个 
            <code>BufferedReader</code>的文本行 
           </dd> 
           <dt> 
            <span class="simpleTagLabel">从以下版本开始：</span> 
           </dt> 
           <dd>
             1.8 
           </dd> 
          </dl> </li> 
        </ul> </li> 
      </ul> </li> 
    </ul> 
   </div> 
  </div>
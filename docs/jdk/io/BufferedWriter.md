<div class="header"> 
   <div class="subTitle">
     compact1, compact2, compact3 
   </div> 
   <div class="subTitle">
     java.io 
   </div> 
   <h2 title="Class BufferedWriter" class="title">Class BufferedWriter</h2> 
  </div>
<div class="contentContainer"> 
   <ul class="inheritance"> 
    <li><a href="../../java/lang/Object.html" title="class in java.lang">java.lang.Object</a></li> 
    <li> 
     <ul class="inheritance"> 
      <li><a href="../../java/io/Writer.html" title="class in java.io">java.io.Writer</a></li> 
      <li> 
       <ul class="inheritance"> 
        <li>java.io.BufferedWriter</li> 
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
        <span><a href="../../java/io/Closeable.html" title="java.io中的接口">Closeable</a> ， <a href="../../java/io/Flushable.html" title="java.io中的接口">Flushable</a> ， <a href="../../java/lang/Appendable.html" title="java.lang中的接口">Appendable</a> ， <a href="../../java/lang/AutoCloseable.html" title="java.lang中的接口">AutoCloseable</a></span> 
       </dd> 
      </dl> 
      <hr> <br> <pre>public class <span class="typeNameLabel">BufferedWriter</span>
extends <a href="../../java/io/Writer.html" title="class in java.io">Writer</a></pre> 
      <div class="block"> 
       <span>将文本写入字符输出流，缓冲字符，以提供单个字符，数组和字符串的高效写入。</span> 
       <p> <span>可以指定缓冲区大小，或者可以接受默认大小。</span> <span>默认值足够大，可用于大多数用途。</span> </p> 
       <p> <span>提供了一个newLine（）方法，它使用平台自己的系统属性<tt>line.separator</tt>定义的行分隔符概念。</span> <span>并非所有平台都使用换行符（'\ n'）来终止行。</span> <span>因此，调用此方法来终止每个输出行，因此优选直接写入换行符。</span> </p> 
       <p> <span>一般来说，Writer将其输出立即发送到底层字符或字节流。</span> <span>除非需要提示输出，否则建议将BufferedWriter包装在其write（）操作可能很昂贵的Writer上，例如FileWriters和OutputStreamWriters。</span> <span>例如，</span> </p> 
       <pre>  <span>PrintWriter out
   = new PrintWriter(new BufferedWriter(new FileWriter("foo.out")));</span> </pre> 
       <span>将缓冲PrintWriter的输出到文件。</span> 
       <span>没有缓冲，每次调用print（）方法都会使字符转换为字节，然后立即写入文件，这可能非常低效。</span> 
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
        <span><a href="../../java/io/PrintWriter.html" title="java.io中的类"><code>PrintWriter</code></a> ， <a href="../../java/io/FileWriter.html" title="java.io中的类"><code>FileWriter</code></a> ， <a href="../../java/io/OutputStreamWriter.html" title="java.io中的类"><code>OutputStreamWriter</code></a> ， <a href="../../java/nio/file/Files.html#newBufferedWriter-java.nio.file.Path-java.nio.charset.Charset-java.nio.file.OpenOption...-"><code>Files.newBufferedWriter(java.nio.file.Path, java.nio.charset.Charset, java.nio.file.OpenOption...)</code></a></span> 
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
         <li class="blockList"><a name="fields.inherited.from.class.java.io.Writer"> 
           <!--   --> </a> <h3>Fields inherited from class&nbsp;java.io.<a href="../../java/io/Writer.html" title="class in java.io">Writer</a></h3> <code><a href="../../java/io/Writer.html#lock">lock</a></code></li> 
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
           <td class="colOne"><code><span class="memberNameLink"><a href="../../java/io/BufferedWriter.html#BufferedWriter-java.io.Writer-">BufferedWriter</a></span>(<a href="../../java/io/Writer.html" title="class in java.io">Writer</a>&nbsp;out)</code> 
            <div class="block">
              创建使用默认大小的输出缓冲区的缓冲字符输出流。 
            </div> </td> 
          </tr> 
          <tr class="rowColor"> 
           <td class="colOne"><code><span class="memberNameLink"><a href="../../java/io/BufferedWriter.html#BufferedWriter-java.io.Writer-int-">BufferedWriter</a></span>(<a href="../../java/io/Writer.html" title="class in java.io">Writer</a>&nbsp;out, int&nbsp;sz)</code> 
            <div class="block">
              创建一个新的缓冲字符输出流，使用给定大小的输出缓冲区。 
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
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedWriter.html#close--">close</a></span>()</code> 
            <div class="block">
              关闭流，先刷新。 
            </div> </td> 
          </tr> 
          <tr id="i1" class="rowColor"> 
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedWriter.html#flush--">flush</a></span>()</code> 
            <div class="block">
              刷新流。 
            </div> </td> 
          </tr> 
          <tr id="i2" class="altColor"> 
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedWriter.html#newLine--">newLine</a></span>()</code> 
            <div class="block">
              写一行行分隔符。 
            </div> </td> 
          </tr> 
          <tr id="i3" class="rowColor"> 
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedWriter.html#write-char:A-int-int-">write</a></span>(char[]&nbsp;cbuf, int&nbsp;off, int&nbsp;len)</code> 
            <div class="block">
              写入字符数组的一部分。 
            </div> </td> 
          </tr> 
          <tr id="i4" class="altColor"> 
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedWriter.html#write-int-">write</a></span>(int&nbsp;c)</code> 
            <div class="block">
              写一个字符 
            </div> </td> 
          </tr> 
          <tr id="i5" class="rowColor"> 
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedWriter.html#write-java.lang.String-int-int-">write</a></span>(<a href="../../java/lang/String.html" title="class in java.lang">String</a>&nbsp;s, int&nbsp;off, int&nbsp;len)</code> 
            <div class="block">
              写一个字符串的一部分。 
            </div> </td> 
          </tr> 
         </tbody> 
        </table> 
        <ul class="blockList"> 
         <li class="blockList"><a name="methods.inherited.from.class.java.io.Writer"> 
           <!--   --> </a> <h3>Methods inherited from class&nbsp;java.io.<a href="../../java/io/Writer.html" title="class in java.io">Writer</a></h3> <code><a href="../../java/io/Writer.html#append-char-">append</a>, <a href="../../java/io/Writer.html#append-java.lang.CharSequence-">append</a>, <a href="../../java/io/Writer.html#append-java.lang.CharSequence-int-int-">append</a>, <a href="../../java/io/Writer.html#write-char:A-">write</a>, <a href="../../java/io/Writer.html#write-java.lang.String-">write</a></code></li> 
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
         <!--   --> </a> <h3>构造方法详细信息</h3> <a name="BufferedWriter-java.io.Writer-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>BufferedWriter</h4> <pre>public&nbsp;BufferedWriter(<a href="../../java/io/Writer.html" title="class in java.io">Writer</a>&nbsp;out)</pre> 
          <div class="block">
            创建使用默认大小的输出缓冲区的缓冲字符输出流。 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>out</code> - 作家 
           </dd> 
          </dl> </li> 
        </ul> <a name="BufferedWriter-java.io.Writer-int-"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>BufferedWriter</h4> <pre>public&nbsp;BufferedWriter(<a href="../../java/io/Writer.html" title="class in java.io">Writer</a>&nbsp;out,
                      int&nbsp;sz)</pre> 
          <div class="block">
            创建一个新的缓冲字符输出流，使用给定大小的输出缓冲区。 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>out</code> - 作家 
           </dd> 
           <dd> 
            <code>sz</code> - 输出缓冲区大小，正整数 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/IllegalArgumentException.html" title="class in java.lang">IllegalArgumentException</a></code> - 如果 
            <code>sz &lt;= 0</code> 
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
         <li class="blockList"> <h4>write</h4> <pre>public&nbsp;void&nbsp;write(int&nbsp;c)
           throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block">
            写一个字符 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/Writer.html#write-int-">write</a></code>在 
            <code><a href="../../java/io/Writer.html" title="class in java.io">Writer</a></code> 
           </dd> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>c</code> - int指定要写入的字符 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生I / O错误 
           </dd> 
          </dl> </li> 
        </ul> <a name="write-char:A-int-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>write</h4> <pre>public&nbsp;void&nbsp;write(char[]&nbsp;cbuf,
                  int&nbsp;off,
                  int&nbsp;len)
           throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>写入字符数组的一部分。</span> 
           <p> <span>通常，此方法将给定数组中的字符存储到此流的缓冲区中，根据需要将缓冲区刷新到底层流。</span> <span>然而，如果请求的长度至少与缓冲区一样大，那么这个方法将刷新缓冲区，并将字符直接写入底层流。</span> <span>因此冗余<code>BufferedWriter</code>将不会不必要地复制数据。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">Specified by:</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/Writer.html#write-char:A-int-int-">write</a></code>在 
            <code><a href="../../java/io/Writer.html" title="class in java.io">Writer</a></code> 
           </dd> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>cbuf</code> - 一个字符数组 
           </dd> 
           <dd> 
            <code>off</code> - 开始读取字符的偏移量 
           </dd> 
           <dd> 
            <code>len</code> - 要写入的 
            <code>len</code>数 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生I / O错误 
           </dd> 
          </dl> </li> 
        </ul> <a name="write-java.lang.String-int-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>write</h4> <pre>public&nbsp;void&nbsp;write(<a href="../../java/lang/String.html" title="class in java.lang">String</a>&nbsp;s,
                  int&nbsp;off,
                  int&nbsp;len)
           throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>写一个字符串的一部分。</span> 
           <p> <span>如果<tt>len</tt>参数的值为负，则不会写入任何字符。</span> <span>这与superclass中的这种方法的<a href="../../java/io/Writer.html#write-java.lang.String-int-int-">规范相反</a> ， <a href="../../java/lang/IndexOutOfBoundsException.html" title="java.lang中的类">superclass</a>要求抛出一个<a href="../../java/lang/IndexOutOfBoundsException.html" title="java.lang中的类"><code>IndexOutOfBoundsException</code></a> 。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/Writer.html#write-java.lang.String-int-int-">write</a></code>在 
            <code><a href="../../java/io/Writer.html" title="class in java.io">Writer</a></code> 
           </dd> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>s</code> - 要写入的字符串 
           </dd> 
           <dd> 
            <code>off</code> - 开始读取字符的偏移量 
           </dd> 
           <dd> 
            <code>len</code> - 要写入的字符数 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生I / O错误 
           </dd> 
          </dl> </li> 
        </ul> <a name="newLine--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>newLine</h4> <pre>public&nbsp;void&nbsp;newLine()
             throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>写一行行分隔符。</span> 
           <span>行分隔符字符串由系统属性<tt>line.separator</tt>定义，并不一定是单个换行符（'\ n'）字符。</span> 
          </div> 
          <dl> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生I / O错误 
           </dd> 
          </dl> </li> 
        </ul> <a name="flush--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>flush</h4> <pre>public&nbsp;void&nbsp;flush()
           throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block">
            刷新流。 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">Specified by:</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/Flushable.html#flush--">flush</a></code>在界面 
            <code><a href="../../java/io/Flushable.html" title="interface in java.io">Flushable</a></code> 
           </dd> 
           <dt> 
            <span class="overrideSpecifyLabel">Specified by:</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/Writer.html#flush--">flush</a></code>在 
            <code><a href="../../java/io/Writer.html" title="class in java.io">Writer</a></code> 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生I / O错误 
           </dd> 
          </dl> </li> 
        </ul> <a name="close--"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>close</h4> <pre>public&nbsp;void&nbsp;close()
           throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span class="descfrmTypeLabel">描述从类别： <code><a href="../../java/io/Writer.html#close--">Writer</a></code>复制</span> 
          </div> 
          <div class="block"> 
           <span>关闭流，先刷新。</span> 
           <span>一旦流已关闭，进一步的write（）或flush（）调用将导致抛出IOException。</span> 
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
            <code><a href="../../java/io/Writer.html#close--">close</a></code>在 
            <code><a href="../../java/io/Writer.html" title="class in java.io">Writer</a></code> 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生I / O错误 
           </dd> 
          </dl> </li> 
        </ul> </li> 
      </ul> </li> 
    </ul> 
   </div> 
  </div>
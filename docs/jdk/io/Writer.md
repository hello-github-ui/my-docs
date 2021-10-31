<div class="contentContainer"> 
   <ul class="inheritance"> 
    <li><a href="../../java/lang/Object.html" title="class in java.lang">java.lang.Object</a></li> 
    <li> 
     <ul class="inheritance"> 
      <li>java.io.Writer</li> 
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
      <dl> 
       <dt>
        已知直接子类：
       </dt> 
       <dd> 
        <span><a href="../../java/io/BufferedWriter.html" title="java.io中的类">BufferedWriter</a> ， <a href="../../java/io/CharArrayWriter.html" title="java.io中的类">CharArrayWriter</a> ， <a href="../../java/io/FilterWriter.html" title="java.io中的类">FilterWriter</a> ， <a href="../../java/io/OutputStreamWriter.html" title="java.io中的类">OutputStreamWriter</a> ， <a href="../../java/io/PipedWriter.html" title="java.io中的类">PipedWriter</a> ， <a href="../../java/io/PrintWriter.html" title="java.io中的类">PrintWriter</a> ， <a href="../../java/io/StringWriter.html" title="java.io中的类">StringWriter</a></span> 
       </dd> 
      </dl> 
      <hr> <br> <pre>public abstract class <span class="typeNameLabel">Writer</span>
extends <a href="../../java/lang/Object.html" title="class in java.lang">Object</a>
implements <a href="../../java/lang/Appendable.html" title="interface in java.lang">Appendable</a>, <a href="../../java/io/Closeable.html" title="interface in java.io">Closeable</a>, <a href="../../java/io/Flushable.html" title="interface in java.io">Flushable</a></pre> 
      <div class="block"> 
       <span>用于写入字符流的抽象类。</span> 
       <span>子类必须实现的唯一方法是write（char []，int，int），flush（）和close（）。</span> 
       <span>然而，大多数子类将覆盖这里定义的一些方法，以便提供更高的效率，附加的功能或两者。</span> 
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
        <span><a href="../../java/io/Writer.html" title="java.io中的类"><code>Writer</code></a> ， <a href="../../java/io/BufferedWriter.html" title="java.io中的类"><code>BufferedWriter</code></a> ， <a href="../../java/io/CharArrayWriter.html" title="java.io中的类"><code>CharArrayWriter</code></a> ， <a href="../../java/io/FilterWriter.html" title="java.io中的类"><code>FilterWriter</code></a> ， <a href="../../java/io/OutputStreamWriter.html" title="java.io中的类"><code>OutputStreamWriter</code></a> ， <a href="../../java/io/FileWriter.html" title="java.io中的类"><code>FileWriter</code></a> ， <a href="../../java/io/PipedWriter.html" title="java.io中的类"><code>PipedWriter</code></a> ， <a href="../../java/io/PrintWriter.html" title="java.io中的类"><code>PrintWriter</code></a> ， <a href="../../java/io/StringWriter.html" title="java.io中的类"><code>StringWriter</code></a> ， <a href="../../java/io/Reader.html" title="java.io中的类"><code>Reader</code></a></span> 
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
           <td class="colFirst"><code>protected <a href="../../java/lang/Object.html" title="class in java.lang">Object</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/Writer.html#lock">lock</a></span></code> 
            <div class="block">
              用于同步此流上的操作的对象。 
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
           <th class="colFirst" scope="col">Modifier</th> 
           <th class="colLast" scope="col">Constructor and Description</th> 
          </tr> 
          <tr class="altColor"> 
           <td class="colFirst"><code>protected </code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/Writer.html#Writer--">Writer</a></span>()</code> 
            <div class="block">
              创建一个新的人物流作家，其关键部分将在作者本身上同步。 
            </div> </td> 
          </tr> 
          <tr class="rowColor"> 
           <td class="colFirst"><code>protected </code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/Writer.html#Writer-java.lang.Object-">Writer</a></span>(<a href="../../java/lang/Object.html" title="class in java.lang">Object</a>&nbsp;lock)</code> 
            <div class="block">
              创建一个新的字符流写入器，其关键部分将在给定对象上进行同步。 
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
          <span id="t3" class="tableTab"><span><a href="javascript:show(4);">抽象方法</a></span><span class="tabEnd">&nbsp;</span></span> 
          <span id="t4" class="tableTab"><span><a href="javascript:show(8);">具体的方法</a></span><span class="tabEnd">&nbsp;</span></span> 
         </caption> 
         <tbody> 
          <tr> 
           <th class="colFirst" scope="col">Modifier and Type</th> 
           <th class="colLast" scope="col">Method and Description</th> 
          </tr> 
          <tr id="i0" class="altColor"> 
           <td class="colFirst"><code><a href="../../java/io/Writer.html" title="class in java.io">Writer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/Writer.html#append-char-">append</a></span>(char&nbsp;c)</code> 
            <div class="block">
              将指定的字符附加到此作者。 
            </div> </td> 
          </tr> 
          <tr id="i1" class="rowColor"> 
           <td class="colFirst"><code><a href="../../java/io/Writer.html" title="class in java.io">Writer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/Writer.html#append-java.lang.CharSequence-">append</a></span>(<a href="../../java/lang/CharSequence.html" title="interface in java.lang">CharSequence</a>&nbsp;csq)</code> 
            <div class="block">
              将指定的字符序列附加到此作者。 
            </div> </td> 
          </tr> 
          <tr id="i2" class="altColor"> 
           <td class="colFirst"><code><a href="../../java/io/Writer.html" title="class in java.io">Writer</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/Writer.html#append-java.lang.CharSequence-int-int-">append</a></span>(<a href="../../java/lang/CharSequence.html" title="interface in java.lang">CharSequence</a>&nbsp;csq, int&nbsp;start, int&nbsp;end)</code> 
            <div class="block">
              将指定字符序列的子序列附加到此作者。 
            </div> </td> 
          </tr> 
          <tr id="i3" class="rowColor"> 
           <td class="colFirst"><code>abstract void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/Writer.html#close--">close</a></span>()</code> 
            <div class="block">
              关闭流，先刷新。 
            </div> </td> 
          </tr> 
          <tr id="i4" class="altColor"> 
           <td class="colFirst"><code>abstract void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/Writer.html#flush--">flush</a></span>()</code> 
            <div class="block">
              刷新流。 
            </div> </td> 
          </tr> 
          <tr id="i5" class="rowColor"> 
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/Writer.html#write-char:A-">write</a></span>(char[]&nbsp;cbuf)</code> 
            <div class="block">
              写入一个字符数组。 
            </div> </td> 
          </tr> 
          <tr id="i6" class="altColor"> 
           <td class="colFirst"><code>abstract void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/Writer.html#write-char:A-int-int-">write</a></span>(char[]&nbsp;cbuf, int&nbsp;off, int&nbsp;len)</code> 
            <div class="block">
              写入字符数组的一部分。 
            </div> </td> 
          </tr> 
          <tr id="i7" class="rowColor"> 
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/Writer.html#write-int-">write</a></span>(int&nbsp;c)</code> 
            <div class="block">
              写一个字符 
            </div> </td> 
          </tr> 
          <tr id="i8" class="altColor"> 
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/Writer.html#write-java.lang.String-">write</a></span>(<a href="../../java/lang/String.html" title="class in java.lang">String</a>&nbsp;str)</code> 
            <div class="block">
              写一个字符串 
            </div> </td> 
          </tr> 
          <tr id="i9" class="rowColor"> 
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/Writer.html#write-java.lang.String-int-int-">write</a></span>(<a href="../../java/lang/String.html" title="class in java.lang">String</a>&nbsp;str, int&nbsp;off, int&nbsp;len)</code> 
            <div class="block">
              写一个字符串的一部分。 
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
      <!-- ============ FIELD DETAIL =========== --> 
      <ul class="blockList"> 
       <li class="blockList"><a name="field.detail"> 
         <!--   --> </a> <h3>字段详细信息</h3> <a name="lock"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>lock</h4> <pre>protected&nbsp;<a href="../../java/lang/Object.html" title="class in java.lang">Object</a> lock</pre> 
          <div class="block"> 
           <span>用于同步此流上的操作的对象。</span> 
           <span>为了效率，字符流对象可以使用自身以外的对象来保护关键部分。</span> 
           <span>因此，子类应该使用此字段中的对象而不是<tt>this</tt>或同步方法。</span> 
          </div> </li> 
        </ul> </li> 
      </ul> 
      <!-- ========= CONSTRUCTOR DETAIL ======== --> 
      <ul class="blockList"> 
       <li class="blockList"><a name="constructor.detail"> 
         <!--   --> </a> <h3>构造方法详细信息</h3> <a name="Writer--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>Writer</h4> <pre>protected&nbsp;Writer()</pre> 
          <div class="block">
            创建一个新的人物流作家，其关键部分将在作者本身上同步。 
          </div> </li> 
        </ul> <a name="Writer-java.lang.Object-"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>Writer</h4> <pre>protected&nbsp;Writer(<a href="../../java/lang/Object.html" title="class in java.lang">Object</a>&nbsp;lock)</pre> 
          <div class="block">
            创建一个新的字符流写入器，其关键部分将在给定对象上进行同步。 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>lock</code> - 要同步的对象 
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
           <span>写一个字符</span> 
           <span>要写入的字符包含在给定整数值的16个低位中;</span> 
           <span>16个高位被忽略。</span> 
           <p> <span>旨在支持高效单字符输出的子类应该覆盖此方法。</span> </p> 
          </div> 
          <dl> 
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
        </ul> <a name="write-char:A-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>write</h4> <pre>public&nbsp;void&nbsp;write(char[]&nbsp;cbuf)
           throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block">
            写入一个字符数组。 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>cbuf</code> - 要写入的字符数组 
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
         <li class="blockList"> <h4>write</h4> <pre>public abstract&nbsp;void&nbsp;write(char[]&nbsp;cbuf,
                           int&nbsp;off,
                           int&nbsp;len)
                    throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block">
            写入字符数组的一部分。 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>cbuf</code> - 
            <code>cbuf</code>数组 
           </dd> 
           <dd> 
            <code>off</code> - 从中开始编写字符的偏移量 
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
        </ul> <a name="write-java.lang.String-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>write</h4> <pre>public&nbsp;void&nbsp;write(<a href="../../java/lang/String.html" title="class in java.lang">String</a>&nbsp;str)
           throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block">
            写一个字符串 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>str</code> - 要写入的字符串 
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
         <li class="blockList"> <h4>write</h4> <pre>public&nbsp;void&nbsp;write(<a href="../../java/lang/String.html" title="class in java.lang">String</a>&nbsp;str,
                  int&nbsp;off,
                  int&nbsp;len)
           throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block">
            写一个字符串的一部分。 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>str</code> - 字符串 
           </dd> 
           <dd> 
            <code>off</code> - 开始编写字符的偏移量 
           </dd> 
           <dd> 
            <code>len</code> - 要写入的 
            <code>len</code>数 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/IndexOutOfBoundsException.html" title="class in java.lang">IndexOutOfBoundsException</a></code> - 如果 
            <tt>off</tt>为负数，或 
            <tt>len</tt>为负数，或 
            <tt>off+len</tt>为负数或大于给定字符串的长度 
           </dd> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生I / O错误 
           </dd> 
          </dl> </li> 
        </ul> <a name="append-java.lang.CharSequence-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>append</h4> <pre>public&nbsp;<a href="../../java/io/Writer.html" title="class in java.io">Writer</a>&nbsp;append(<a href="../../java/lang/CharSequence.html" title="interface in java.lang">CharSequence</a>&nbsp;csq)
              throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>将指定的字符序列附加到此作者。</span> 
           <p> <span>调用此方法的形式<tt>out.append(csq)的</tt>行为方式与调用完全相同</span> </p> 
           <pre>  <span>out.write(csq.toString())</span> </pre> 
           <p> <span>取决于<tt>toString</tt>字符序列<tt>csq</tt>本说明书中，整个序列可以不追加。</span> <span>例如，调用字符缓冲区的<tt>toString</tt>方法将返回一个子序列，其内容取决于缓冲区的位置和限制。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">Specified by:</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/Appendable.html#append-java.lang.CharSequence-">append</a></code>在界面 
            <code><a href="../../java/lang/Appendable.html" title="interface in java.lang">Appendable</a></code> 
           </dd> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <span><code>csq</code> - 要追加的字符序列。</span> 
            <span>如果<tt>csq</tt>是<tt>null</tt> ，那么四个字符<tt>"null"</tt>被附加到该写入器。</span> 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             这位作家 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生I / O错误 
           </dd> 
           <dt> 
            <span class="simpleTagLabel">从以下版本开始：</span> 
           </dt> 
           <dd>
             1.5 
           </dd> 
          </dl> </li> 
        </ul> <a name="append-java.lang.CharSequence-int-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>append</h4> <pre>public&nbsp;<a href="../../java/io/Writer.html" title="class in java.io">Writer</a>&nbsp;append(<a href="../../java/lang/CharSequence.html" title="interface in java.lang">CharSequence</a>&nbsp;csq,
                     int&nbsp;start,
                     int&nbsp;end)
              throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>将指定字符序列的子序列附加到此作者。</span> 
           <span><tt>Appendable</tt> 。</span> 
           <p> <span>形式的这种方法的调用时<tt>out.append(csq, start, end)</tt> <tt>csq</tt>是完全相同的方式调用不<tt>null</tt>的行为</span> </p> 
           <pre>  <span>out.write(csq.subSequence(start, end).toString())</span> </pre> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">Specified by:</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/Appendable.html#append-java.lang.CharSequence-int-int-">append</a></code>在界面 
            <code><a href="../../java/lang/Appendable.html" title="interface in java.lang">Appendable</a></code> 
           </dd> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <span><code>csq</code> - 追加子序列的字符序列。</span> 
            <span>如果<tt>csq</tt>是<tt>null</tt> ，则会附加<tt>字符</tt> ，如果<tt>csq</tt>包含四个字符<tt>"null"</tt> 。</span> 
           </dd> 
           <dd> 
            <code>start</code> - 子序列中第一个字符的索引 
           </dd> 
           <dd> 
            <code>end</code> - 子序列中最后一个字符后面的字符的索引 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             这位作家 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/IndexOutOfBoundsException.html" title="class in java.lang">IndexOutOfBoundsException</a></code> - 如果 
            <tt>start</tt>或 
            <tt>end</tt>为负数，则 
            <tt>start</tt>大于 
            <tt>end</tt> ，或 
            <tt>end</tt>大于 
            <tt>csq.length()</tt> 
           </dd> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生I / O错误 
           </dd> 
           <dt> 
            <span class="simpleTagLabel">从以下版本开始：</span> 
           </dt> 
           <dd>
             1.5 
           </dd> 
          </dl> </li> 
        </ul> <a name="append-char-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>append</h4> <pre>public&nbsp;<a href="../../java/io/Writer.html" title="class in java.io">Writer</a>&nbsp;append(char&nbsp;c)
              throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>将指定的字符附加到此作者。</span> 
           <p> <span>对这种形式out.append(c)的这种方法的<tt>调用</tt>与<tt>调用的</tt>方式完全相同</span> </p> 
           <pre>  <span>out.write(c)</span> </pre> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">Specified by:</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/Appendable.html#append-char-">append</a></code>在界面 
            <code><a href="../../java/lang/Appendable.html" title="interface in java.lang">Appendable</a></code> 
           </dd> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>c</code> - 要追加的16位字符 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             这位作家 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生I / O错误 
           </dd> 
           <dt> 
            <span class="simpleTagLabel">从以下版本开始：</span> 
           </dt> 
           <dd>
             1.5 
           </dd> 
          </dl> </li> 
        </ul> <a name="flush--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>flush</h4> <pre>public abstract&nbsp;void&nbsp;flush()
                    throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>刷新流。</span> 
           <span>如果流已经从缓冲区中的各种write（）方法保存了任何字符，请将它们立即写入到其预期目的地。</span> 
           <span>然后，如果该目的地是另一个字符或字节流，请将其刷新。</span> 
           <span>因此，一个flush（）调用将刷新Writers和OutputStreams链中的所有缓冲区。</span> 
           <p> <span>如果此流的预期目标是由底层操作系统（例如文件）提供的抽象，那么刷新流仅保证先前写入流的字节传递到操作系统进行写入;</span> <span>它并不保证它们实际上被写入物理设备，如磁盘驱动器。</span> </p> 
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
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生I / O错误 
           </dd> 
          </dl> </li> 
        </ul> <a name="close--"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>close</h4> <pre>public abstract&nbsp;void&nbsp;close()
                    throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
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
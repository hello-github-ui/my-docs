<div class="contentContainer"> 
   <ul class="inheritance"> 
    <li><a href="../../java/lang/Object.html" title="class in java.lang">java.lang.Object</a></li> 
    <li> 
     <ul class="inheritance"> 
      <li><a href="../../java/io/Writer.html" title="class in java.io">java.io.Writer</a></li> 
      <li> 
       <ul class="inheritance"> 
        <li><a href="../../java/io/OutputStreamWriter.html" title="class in java.io">java.io.OutputStreamWriter</a></li> 
        <li> 
         <ul class="inheritance"> 
          <li>java.io.FileWriter</li> 
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
        <span><a href="../../java/io/Closeable.html" title="java.io中的接口">Closeable</a> ， <a href="../../java/io/Flushable.html" title="java.io中的接口">Flushable</a> ， <a href="../../java/lang/Appendable.html" title="java.lang中的接口">Appendable</a> ， <a href="../../java/lang/AutoCloseable.html" title="java.lang中的接口">AutoCloseable</a></span> 
       </dd> 
      </dl> 
      <hr> <br> <pre>public class <span class="typeNameLabel">FileWriter</span>
extends <a href="../../java/io/OutputStreamWriter.html" title="class in java.io">OutputStreamWriter</a></pre> 
      <div class="block"> 
       <span>方便课写字符文件。</span> 
       <span>该类的构造函数假定默认字符编码和默认字节缓冲区大小是可以接受的。</span> 
       <span>要自己指定这些值，请在FileOutputStream上构造一个OutputStreamWriter。</span> 
       <p> <span>文件是否可用或可能被创建取决于底层平台。</span> <span>特别是某些平台允许一次只能打开一个文件来写入一个<tt>FileWriter</tt> （或其他文件写入对象）。</span> <span>在这种情况下，如果所涉及的文件已经打开，则此类中的构造函数将失败。</span> </p> 
       <p> <span><code>FileWriter</code>是用于写入字符流。</span> <span>要编写原始字节流，请考虑使用<code>FileOutputStream</code> 。</span> </p> 
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
        <span><a href="../../java/io/OutputStreamWriter.html" title="java.io中的类"><code>OutputStreamWriter</code></a> ， <a href="../../java/io/FileOutputStream.html" title="java.io中的类"><code>FileOutputStream</code></a></span> 
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
           <td class="colOne"><code><span class="memberNameLink"><a href="../../java/io/FileWriter.html#FileWriter-java.io.File-">FileWriter</a></span>(<a href="../../java/io/File.html" title="class in java.io">File</a>&nbsp;file)</code> 
            <div class="block">
              给一个File对象构造一个FileWriter对象。 
            </div> </td> 
          </tr> 
          <tr class="rowColor"> 
           <td class="colOne"><code><span class="memberNameLink"><a href="../../java/io/FileWriter.html#FileWriter-java.io.File-boolean-">FileWriter</a></span>(<a href="../../java/io/File.html" title="class in java.io">File</a>&nbsp;file, boolean&nbsp;append)</code> 
            <div class="block">
              给一个File对象构造一个FileWriter对象。 
            </div> </td> 
          </tr> 
          <tr class="altColor"> 
           <td class="colOne"><code><span class="memberNameLink"><a href="../../java/io/FileWriter.html#FileWriter-java.io.FileDescriptor-">FileWriter</a></span>(<a href="../../java/io/FileDescriptor.html" title="class in java.io">FileDescriptor</a>&nbsp;fd)</code> 
            <div class="block">
              构造与文件描述符关联的FileWriter对象。 
            </div> </td> 
          </tr> 
          <tr class="rowColor"> 
           <td class="colOne"><code><span class="memberNameLink"><a href="../../java/io/FileWriter.html#FileWriter-java.lang.String-">FileWriter</a></span>(<a href="../../java/lang/String.html" title="class in java.lang">String</a>&nbsp;fileName)</code> 
            <div class="block">
              构造一个给定文件名的FileWriter对象。 
            </div> </td> 
          </tr> 
          <tr class="altColor"> 
           <td class="colOne"><code><span class="memberNameLink"><a href="../../java/io/FileWriter.html#FileWriter-java.lang.String-boolean-">FileWriter</a></span>(<a href="../../java/lang/String.html" title="class in java.lang">String</a>&nbsp;fileName, boolean&nbsp;append)</code> 
            <div class="block">
              构造一个FileWriter对象，给出一个带有布尔值的文件名，表示是否附加写入的数据。 
            </div> </td> 
          </tr> 
         </tbody> 
        </table> </li> 
      </ul> 
      <!-- ========== METHOD SUMMARY =========== --> 
      <ul class="blockList"> 
       <li class="blockList"><a name="method.summary"> 
         <!--   --> </a> <h3>方法摘要</h3> 
        <ul class="blockList"> 
         <li class="blockList"><a name="methods.inherited.from.class.java.io.OutputStreamWriter"> 
           <!--   --> </a> <h3>Methods inherited from class&nbsp;java.io.<a href="../../java/io/OutputStreamWriter.html" title="class in java.io">OutputStreamWriter</a></h3> <code><a href="../../java/io/OutputStreamWriter.html#close--">close</a>, <a href="../../java/io/OutputStreamWriter.html#flush--">flush</a>, <a href="../../java/io/OutputStreamWriter.html#getEncoding--">getEncoding</a>, <a href="../../java/io/OutputStreamWriter.html#write-char:A-int-int-">write</a>, <a href="../../java/io/OutputStreamWriter.html#write-int-">write</a>, <a href="../../java/io/OutputStreamWriter.html#write-java.lang.String-int-int-">write</a></code></li> 
        </ul> 
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
         <!--   --> </a> <h3>构造方法详细信息</h3> <a name="FileWriter-java.lang.String-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>FileWriter</h4> <pre>public&nbsp;FileWriter(<a href="../../java/lang/String.html" title="class in java.lang">String</a>&nbsp;fileName)
           throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block">
            构造一个给定文件名的FileWriter对象。 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>fileName</code> - String系统相关的文件名。 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果命名文件存在但是是一个目录而不是常规文件，则不存在但不能创建，或由于任何其他原因无法打开 
           </dd> 
          </dl> </li> 
        </ul> <a name="FileWriter-java.lang.String-boolean-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>FileWriter</h4> <pre>public&nbsp;FileWriter(<a href="../../java/lang/String.html" title="class in java.lang">String</a>&nbsp;fileName,
                  boolean&nbsp;append)
           throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block">
            构造一个FileWriter对象，给出一个带有布尔值的文件名，表示是否附加写入的数据。 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>fileName</code> - String系统相关的文件名。 
           </dd> 
           <dd> 
            <code>append</code> - boolean如果是 
            <code>true</code> ，那么数据将被写入文件的末尾而不是开头。 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果命名文件存在，但是是一个目录而不是常规文件，不存在但不能创建，或由于任何其他原因无法打开 
           </dd> 
          </dl> </li> 
        </ul> <a name="FileWriter-java.io.File-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>FileWriter</h4> <pre>public&nbsp;FileWriter(<a href="../../java/io/File.html" title="class in java.io">File</a>&nbsp;file)
           throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block">
            给一个File对象构造一个FileWriter对象。 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>file</code> - 要写入的File对象。 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果文件存在但是是一个目录而不是常规文件，不存在但不能创建，或由于任何其他原因无法打开 
           </dd> 
          </dl> </li> 
        </ul> <a name="FileWriter-java.io.File-boolean-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>FileWriter</h4> <pre>public&nbsp;FileWriter(<a href="../../java/io/File.html" title="class in java.io">File</a>&nbsp;file,
                  boolean&nbsp;append)
           throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>给一个File对象构造一个FileWriter对象。</span> 
           <span>如果第二个参数是<code>true</code> ，则字节将写入文件的末尾而不是开头。</span> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>file</code> - 要写入的File对象 
           </dd> 
           <dd> 
            <code>append</code> - 如果 
            <code>true</code> ，则字节将被写入文件的末尾而不是开头 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果文件存在但是是一个目录而不是常规文件，则不存在但不能创建，或由于任何其他原因无法打开 
           </dd> 
           <dt> 
            <span class="simpleTagLabel">从以下版本开始：</span> 
           </dt> 
           <dd>
             1.4 
           </dd> 
          </dl> </li> 
        </ul> <a name="FileWriter-java.io.FileDescriptor-"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>FileWriter</h4> <pre>public&nbsp;FileWriter(<a href="../../java/io/FileDescriptor.html" title="class in java.io">FileDescriptor</a>&nbsp;fd)</pre> 
          <div class="block">
            构造与文件描述符关联的FileWriter对象。 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>fd</code> - 要写入的FileDescriptor对象。 
           </dd> 
          </dl> </li> 
        </ul> </li> 
      </ul> </li> 
    </ul> 
   </div> 
  </div>
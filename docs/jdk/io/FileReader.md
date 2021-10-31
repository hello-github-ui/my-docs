<div class="contentContainer"> 
   <ul class="inheritance"> 
    <li><a href="../../java/lang/Object.html" title="class in java.lang">java.lang.Object</a></li> 
    <li> 
     <ul class="inheritance"> 
      <li><a href="../../java/io/Reader.html" title="class in java.io">java.io.Reader</a></li> 
      <li> 
       <ul class="inheritance"> 
        <li><a href="../../java/io/InputStreamReader.html" title="class in java.io">java.io.InputStreamReader</a></li> 
        <li> 
         <ul class="inheritance"> 
          <li>java.io.FileReader</li> 
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
        <span><a href="../../java/io/Closeable.html" title="java.io中的接口">Closeable</a> ， <a href="../../java/lang/AutoCloseable.html" title="java.lang中的接口">AutoCloseable</a> ， <a href="../../java/lang/Readable.html" title="java.lang中的接口">Readable</a></span> 
       </dd> 
      </dl> 
      <hr> <br> <pre>public class <span class="typeNameLabel">FileReader</span>
extends <a href="../../java/io/InputStreamReader.html" title="class in java.io">InputStreamReader</a></pre> 
      <div class="block"> 
       <span>阅读字符文件的便利课。</span> 
       <span>该类的构造函数假定默认字符编码和默认字节缓冲区大小是适当的。</span> 
       <span>要自己指定这些值，请在FileInputStream上构造一个InputStreamReader。</span> 
       <p> <span><code>FileReader</code>是用于读取字符流。</span> <span>要读取原始字节流，请考虑使用<code>FileInputStream</code> 。</span> </p> 
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
        <span><a href="../../java/io/InputStreamReader.html" title="java.io中的类"><code>InputStreamReader</code></a> ， <a href="../../java/io/FileInputStream.html" title="java.io中的类"><code>FileInputStream</code></a></span> 
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
           <td class="colOne"><code><span class="memberNameLink"><a href="../../java/io/FileReader.html#FileReader-java.io.File-">FileReader</a></span>(<a href="../../java/io/File.html" title="class in java.io">File</a>&nbsp;file)</code> 
            <div class="block">
              创建一个新的 
             <tt>FileReader</tt> ，给出 
             <tt>File</tt>读取。 
            </div> </td> 
          </tr> 
          <tr class="rowColor"> 
           <td class="colOne"><code><span class="memberNameLink"><a href="../../java/io/FileReader.html#FileReader-java.io.FileDescriptor-">FileReader</a></span>(<a href="../../java/io/FileDescriptor.html" title="class in java.io">FileDescriptor</a>&nbsp;fd)</code> 
            <div class="block">
              创建一个新的 
             <tt>FileReader</tt> ，给定 
             <tt>FileDescriptor</tt>读取。 
            </div> </td> 
          </tr> 
          <tr class="altColor"> 
           <td class="colOne"><code><span class="memberNameLink"><a href="../../java/io/FileReader.html#FileReader-java.lang.String-">FileReader</a></span>(<a href="../../java/lang/String.html" title="class in java.lang">String</a>&nbsp;fileName)</code> 
            <div class="block">
              创建一个新的 
             <tt>FileReader</tt> ，给定要读取的文件的名称。 
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
         <li class="blockList"><a name="methods.inherited.from.class.java.io.InputStreamReader"> 
           <!--   --> </a> <h3>Methods inherited from class&nbsp;java.io.<a href="../../java/io/InputStreamReader.html" title="class in java.io">InputStreamReader</a></h3> <code><a href="../../java/io/InputStreamReader.html#close--">close</a>, <a href="../../java/io/InputStreamReader.html#getEncoding--">getEncoding</a>, <a href="../../java/io/InputStreamReader.html#read--">read</a>, <a href="../../java/io/InputStreamReader.html#read-char:A-int-int-">read</a>, <a href="../../java/io/InputStreamReader.html#ready--">ready</a></code></li> 
        </ul> 
        <ul class="blockList"> 
         <li class="blockList"><a name="methods.inherited.from.class.java.io.Reader"> 
           <!--   --> </a> <h3>Methods inherited from class&nbsp;java.io.<a href="../../java/io/Reader.html" title="class in java.io">Reader</a></h3> <code><a href="../../java/io/Reader.html#mark-int-">mark</a>, <a href="../../java/io/Reader.html#markSupported--">markSupported</a>, <a href="../../java/io/Reader.html#read-char:A-">read</a>, <a href="../../java/io/Reader.html#read-java.nio.CharBuffer-">read</a>, <a href="../../java/io/Reader.html#reset--">reset</a>, <a href="../../java/io/Reader.html#skip-long-">skip</a></code></li> 
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
         <!--   --> </a> <h3>构造方法详细信息</h3> <a name="FileReader-java.lang.String-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>FileReader</h4> <pre>public&nbsp;FileReader(<a href="../../java/lang/String.html" title="class in java.lang">String</a>&nbsp;fileName)
           throws <a href="../../java/io/FileNotFoundException.html" title="class in java.io">FileNotFoundException</a></pre> 
          <div class="block">
            创建一个新的 
           <tt>FileReader</tt> ，给定要读取的文件的名称。 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>fileName</code> - 要读取的文件的名称 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/FileNotFoundException.html" title="class in java.io">FileNotFoundException</a></code> - 如果命名文件不存在，是一个目录，而不是常规文件，或者由于某些其他原因无法打开读取。 
           </dd> 
          </dl> </li> 
        </ul> <a name="FileReader-java.io.File-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>FileReader</h4> <pre>public&nbsp;FileReader(<a href="../../java/io/File.html" title="class in java.io">File</a>&nbsp;file)
           throws <a href="../../java/io/FileNotFoundException.html" title="class in java.io">FileNotFoundException</a></pre> 
          <div class="block">
            创建一个新的 
           <tt>FileReader</tt> ，给定 
           <tt>File</tt>读取。 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>file</code> - 要阅读的 
            <tt>File</tt> 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/FileNotFoundException.html" title="class in java.io">FileNotFoundException</a></code> - 如果文件不存在，是一个目录而不是常规文件，或者由于某些其他原因无法打开阅读。 
           </dd> 
          </dl> </li> 
        </ul> <a name="FileReader-java.io.FileDescriptor-"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>FileReader</h4> <pre>public&nbsp;FileReader(<a href="../../java/io/FileDescriptor.html" title="class in java.io">FileDescriptor</a>&nbsp;fd)</pre> 
          <div class="block">
            创建一个新的 
           <tt>FileReader</tt> ，给予 
           <tt>FileDescriptor从中</tt>读取。 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>fd</code> - 要读取的FileDescriptor 
           </dd> 
          </dl> </li> 
        </ul> </li> 
      </ul> </li> 
    </ul> 
   </div> 
  </div>
<div class="contentContainer"> 
   <ul class="inheritance"> 
    <li><a href="../../java/lang/Object.html" title="class in java.lang">java.lang.Object</a></li> 
    <li> 
     <ul class="inheritance"> 
      <li><a href="../../java/io/InputStream.html" title="class in java.io">java.io.InputStream</a></li> 
      <li> 
       <ul class="inheritance"> 
        <li>java.io.FileInputStream</li> 
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
      <hr> <br> <pre>public class <span class="typeNameLabel">FileInputStream</span>
extends <a href="../../java/io/InputStream.html" title="class in java.io">InputStream</a></pre> 
      <div class="block"> 
       <span>A <code>FileInputStream</code>从文件系统中的文件获取输入字节。</span> 
       <span>什么文件可用取决于主机环境。</span> 
       <p> <span><code>FileInputStream</code>用于读取诸如图像数据的原始字节流。</span> <span>要阅读字符串，请考虑使用<code>FileReader</code> 。</span> </p> 
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
        <span><a href="../../java/io/File.html" title="java.io中的类"><code>File</code></a> ， <a href="../../java/io/FileDescriptor.html" title="java.io中的类"><code>FileDescriptor</code></a> ， <a href="../../java/io/FileOutputStream.html" title="java.io中的类"><code>FileOutputStream</code></a> ， <a href="../../java/nio/file/Files.html#newInputStream-java.nio.file.Path-java.nio.file.OpenOption...-"><code>Files.newInputStream(java.nio.file.Path, java.nio.file.OpenOption...)</code></a></span> 
       </dd> 
      </dl> </li> 
    </ul> 
   </div> 
   <div class="summary"> 
    <ul class="blockList"> 
     <li class="blockList"> 
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
           <td class="colOne"><code><span class="memberNameLink"><a href="../../java/io/FileInputStream.html#FileInputStream-java.io.File-">FileInputStream</a></span>(<a href="../../java/io/File.html" title="class in java.io">File</a>&nbsp;file)</code> 
            <div class="block">
              通过打开与实际文件的连接创建一个 
             <code>FileInputStream</code> ，该文件由文件系统中的 
             <code>File</code>对象 
             <code>file</code>命名。 
            </div> </td> 
          </tr> 
          <tr class="rowColor"> 
           <td class="colOne"><code><span class="memberNameLink"><a href="../../java/io/FileInputStream.html#FileInputStream-java.io.FileDescriptor-">FileInputStream</a></span>(<a href="../../java/io/FileDescriptor.html" title="class in java.io">FileDescriptor</a>&nbsp;fdObj)</code> 
            <div class="block">
              创建 
             <code>FileInputStream</code>通过使用文件描述符 
             <code>fdObj</code> ，其表示在文件系统中的现有连接到一个实际的文件。 
            </div> </td> 
          </tr> 
          <tr class="altColor"> 
           <td class="colOne"><code><span class="memberNameLink"><a href="../../java/io/FileInputStream.html#FileInputStream-java.lang.String-">FileInputStream</a></span>(<a href="../../java/lang/String.html" title="class in java.lang">String</a>&nbsp;name)</code> 
            <div class="block">
              通过打开与实际文件的连接来创建一个 
             <code>FileInputStream</code> ，该文件由文件系统中的路径名 
             <code>name</code>命名。 
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
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/FileInputStream.html#available--">available</a></span>()</code> 
            <div class="block">
              返回从此输入流中可以读取（或跳过）的剩余字节数的估计值，而不会被下一次调用此输入流的方法阻塞。 
            </div> </td> 
          </tr> 
          <tr id="i1" class="rowColor"> 
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/FileInputStream.html#close--">close</a></span>()</code> 
            <div class="block">
              关闭此文件输入流并释放与流相关联的任何系统资源。 
            </div> </td> 
          </tr> 
          <tr id="i2" class="altColor"> 
           <td class="colFirst"><code>protected void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/FileInputStream.html#finalize--">finalize</a></span>()</code> 
            <div class="block">
              确保当这个文件输入流的 
             <code>close</code>方法没有更多的引用时被调用。 
            </div> </td> 
          </tr> 
          <tr id="i3" class="rowColor"> 
           <td class="colFirst"><code><a href="../../java/nio/channels/FileChannel.html" title="class in java.nio.channels">FileChannel</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/FileInputStream.html#getChannel--">getChannel</a></span>()</code> 
            <div class="block"> 
             <span>返回与此文件输入流相关联的唯一的<a href="../../java/nio/channels/FileChannel.html" title="java.nio.channels中的类"><code>FileChannel</code></a>对象。</span> 
            </div> </td> 
          </tr> 
          <tr id="i4" class="altColor"> 
           <td class="colFirst"><code><a href="../../java/io/FileDescriptor.html" title="class in java.io">FileDescriptor</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/FileInputStream.html#getFD--">getFD</a></span>()</code> 
            <div class="block">
              返回表示与此 
             <code>FileInputStream</code>正在使用的文件系统中实际文件的连接的 
             <code>FileDescriptor</code>对象。 
            </div> </td> 
          </tr> 
          <tr id="i5" class="rowColor"> 
           <td class="colFirst"><code>int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/FileInputStream.html#read--">read</a></span>()</code> 
            <div class="block">
              从该输入流读取一个字节的数据。 
            </div> </td> 
          </tr> 
          <tr id="i6" class="altColor"> 
           <td class="colFirst"><code>int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/FileInputStream.html#read-byte:A-">read</a></span>(byte[]&nbsp;b)</code> 
            <div class="block">
              从该输入流读取最多 
             <code>b.length</code>个字节的数据为字节数组。 
            </div> </td> 
          </tr> 
          <tr id="i7" class="rowColor"> 
           <td class="colFirst"><code>int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/FileInputStream.html#read-byte:A-int-int-">read</a></span>(byte[]&nbsp;b, int&nbsp;off, int&nbsp;len)</code> 
            <div class="block">
              从该输入流读取最多 
             <code>len</code>字节的数据为字节数组。 
            </div> </td> 
          </tr> 
          <tr id="i8" class="altColor"> 
           <td class="colFirst"><code>long</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/FileInputStream.html#skip-long-">skip</a></span>(long&nbsp;n)</code> 
            <div class="block">
              跳过并从输入流中丢弃 
             <code>n</code>字节的数据。 
            </div> </td> 
          </tr> 
         </tbody> 
        </table> 
        <ul class="blockList"> 
         <li class="blockList"><a name="methods.inherited.from.class.java.io.InputStream"> 
           <!--   --> </a> <h3>Methods inherited from class&nbsp;java.io.<a href="../../java/io/InputStream.html" title="class in java.io">InputStream</a></h3> <code><a href="../../java/io/InputStream.html#mark-int-">mark</a>, <a href="../../java/io/InputStream.html#markSupported--">markSupported</a>, <a href="../../java/io/InputStream.html#reset--">reset</a></code></li> 
        </ul> 
        <ul class="blockList"> 
         <li class="blockList"><a name="methods.inherited.from.class.java.lang.Object"> 
           <!--   --> </a> <h3>Methods inherited from class&nbsp;java.lang.<a href="../../java/lang/Object.html" title="class in java.lang">Object</a></h3> <code><a href="../../java/lang/Object.html#clone--">clone</a>, <a href="../../java/lang/Object.html#equals-java.lang.Object-">equals</a>, <a href="../../java/lang/Object.html#getClass--">getClass</a>, <a href="../../java/lang/Object.html#hashCode--">hashCode</a>, <a href="../../java/lang/Object.html#notify--">notify</a>, <a href="../../java/lang/Object.html#notifyAll--">notifyAll</a>, <a href="../../java/lang/Object.html#toString--">toString</a>, <a href="../../java/lang/Object.html#wait--">wait</a>, <a href="../../java/lang/Object.html#wait-long-">wait</a>, <a href="../../java/lang/Object.html#wait-long-int-">wait</a></code></li> 
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
         <!--   --> </a> <h3>构造方法详细信息</h3> <a name="FileInputStream-java.lang.String-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>FileInputStream</h4> <pre>public&nbsp;FileInputStream(<a href="../../java/lang/String.html" title="class in java.lang">String</a>&nbsp;name)
                throws <a href="../../java/io/FileNotFoundException.html" title="class in java.io">FileNotFoundException</a></pre> 
          <div class="block"> 
           <span>通过打开与实际文件的连接创建一个<code>FileInputStream</code>文件，该文件由文件系统中的路径名<code>name</code>命名。</span> 
           <span>创建一个新的<code>FileDescriptor</code>对象来表示此文件连接。</span> 
           <p> <span>首先，如果有一个安全管理器，它的<code>checkRead</code>方法被调用与<code>name</code>参数作为其参数。</span> </p> 
           <p> <span>如果命名文件不存在，则是一个目录而不是常规文件，或者由于某些其他原因无法打开读取，因此抛出一个<code>FileNotFoundException</code> 。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>name</code> - 与系统相关的文件名。 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/FileNotFoundException.html" title="class in java.io">FileNotFoundException</a></code> - 如果文件不存在，是一个目录而不是常规文件，或者由于某些其他原因无法打开阅读。 
           </dd> 
           <dd> 
            <code><a href="../../java/lang/SecurityException.html" title="class in java.lang">SecurityException</a></code> - 如果安全管理器存在，并且其 
            <code>checkRead</code>方法拒绝对该文件的读取访问。 
           </dd> 
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <a href="../../java/lang/SecurityManager.html#checkRead-java.lang.String-"><code>SecurityManager.checkRead(java.lang.String)</code></a> 
           </dd> 
          </dl> </li> 
        </ul> <a name="FileInputStream-java.io.File-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>FileInputStream</h4> <pre>public&nbsp;FileInputStream(<a href="../../java/io/File.html" title="class in java.io">File</a>&nbsp;file)
                throws <a href="../../java/io/FileNotFoundException.html" title="class in java.io">FileNotFoundException</a></pre> 
          <div class="block"> 
           <span>通过打开与实际文件的连接创建一个<code>FileInputStream</code> ，该文件由文件系统中的<code>File</code>对象<code>file</code>命名。</span> 
           <span>创建一个新的<code>FileDescriptor</code>对象来表示此文件连接。</span> 
           <p> <span>首先，如果有一个安全管理器，它的<code>checkRead</code>方法<code>file</code>参数表示的路径作为参数来调用。</span> </p> 
           <p> <span>如果命名文件不存在，则是一个目录而不是常规文件，或者由于某些其他原因无法打开读取，因此抛出一个<code>FileNotFoundException</code> 。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>file</code> - 要打开阅读的文件。 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/FileNotFoundException.html" title="class in java.io">FileNotFoundException</a></code> - 如果文件不存在，是一个目录而不是常规文件，或者由于某些其他原因无法打开阅读。 
           </dd> 
           <dd> 
            <code><a href="../../java/lang/SecurityException.html" title="class in java.lang">SecurityException</a></code> - 如果安全管理器存在，并且其 
            <code>checkRead</code>方法拒绝对该文件的读取访问。 
           </dd> 
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <a href="../../java/io/File.html#getPath--"><code>File.getPath()</code></a> ， 
            <a href="../../java/lang/SecurityManager.html#checkRead-java.lang.String-"><code>SecurityManager.checkRead(java.lang.String)</code></a> 
           </dd> 
          </dl> </li> 
        </ul> <a name="FileInputStream-java.io.FileDescriptor-"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>FileInputStream</h4> <pre>public&nbsp;FileInputStream(<a href="../../java/io/FileDescriptor.html" title="class in java.io">FileDescriptor</a>&nbsp;fdObj)</pre> 
          <div class="block"> 
           <span>创建<code>FileInputStream</code>通过使用文件描述符<code>fdObj</code> ，其表示在文件系统中的现有连接到一个实际的文件。</span> 
           <p> <span>如果有安全管理器，则调用其<code>checkRead</code>方法，文件描述符<code>fdObj</code>作为参数，以查看是否可以读取文件描述符。</span> <span>如果文件描述符被拒绝读访问，则抛出一个<code>SecurityException</code> 。</span> </p> 
           <p> <span>如果<code>fdObj</code>为null，则抛出<code>NullPointerException</code> 。</span> </p> 
           <p> <span>如果<code>fdObj</code>是<a href="../../java/io/FileDescriptor.html#valid--"><code>invalid</code>，</a>那么这个构造函数不会抛出<a href="../../java/io/FileDescriptor.html#valid--">异常</a> 。</span> <span>但是，如果在结果流上调用方法来尝试流上的I / O，则会抛出一个<code>IOException</code> 。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>fdObj</code> - 要打开阅读的文件描述符。 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/SecurityException.html" title="class in java.lang">SecurityException</a></code> - 如果安全管理器存在，并且其 
            <code>checkRead</code>方法拒绝对 
            <code>checkRead</code>读取访问。 
           </dd> 
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <a href="../../java/lang/SecurityManager.html#checkRead-java.io.FileDescriptor-"><code>SecurityManager.checkRead(java.io.FileDescriptor)</code></a> 
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
           <span>从该输入流读取一个字节的数据。</span> 
           <span>如果没有输入可用，此方法将阻止。</span> 
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
             数据的下一个字节，如果达到文件的末尾， 
            <code>-1</code> 。 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生I / O错误。 
           </dd> 
          </dl> </li> 
        </ul> <a name="read-byte:A-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>read</h4> <pre>public&nbsp;int&nbsp;read(byte[]&nbsp;b)
         throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>从该输入流读取最多<code>b.length</code>字节的数据到字节数组。</span> 
           <span>此方法将阻塞，直到某些输入可用。</span> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/InputStream.html#read-byte:A-">read</a></code>在 
            <code><a href="../../java/io/InputStream.html" title="class in java.io">InputStream</a></code>类 
           </dd> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>b</code> - 读取数据的缓冲区。 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             读入缓冲区的总字节数，如果没有更多的数据，因为文件的结尾已经到达， 
            <code>-1</code> 。 
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
            <a href="../../java/io/InputStream.html#read-byte:A-int-int-"><code>InputStream.read(byte[], int, int)</code></a> 
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
           <span>从该输入流读取最多<code>len</code>字节的数据为字节数组。</span> 
           <span>如果<code>len</code>不为零，该方法将阻塞，直到某些输入可用;</span> 
           <span>否则，不会读取字节，并返回<code>0</code> 。</span> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/InputStream.html#read-byte:A-int-int-">read</a></code>在类 
            <code><a href="../../java/io/InputStream.html" title="class in java.io">InputStream</a></code> 
           </dd> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>b</code> - 读取数据的缓冲区。 
           </dd> 
           <dd> 
            <code>off</code> - 目标数组 
            <code>b</code>的起始偏移量 
           </dd> 
           <dd> 
            <code>len</code> - 读取的最大字节数。 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             读取到缓冲区的总字节数，如果没有更多的数据，因为文件的结尾已经到达， 
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
            <code>off</code>为负数， 
            <code>len</code>为负数，或 
            <code>len</code>为大于 
            <code>b.length - off</code> 
           </dd> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生I / O错误 
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
         <li class="blockList"> <h4>skip</h4> <pre>public&nbsp;long&nbsp;skip(long&nbsp;n)
          throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>跳过并从输入流中丢弃<code>n</code>个字节的数据。</span> 
           <p> <span>由于各种原因， <code>skip</code>方法可能会跳过一些较小数量的字节，可能是<code>0</code> 。</span> <span>如果<code>n</code>为负，则该方法将尝试向后跳。</span> <span>如果后台文件不支持其当前位置的向后跳过，则会抛出<code>IOException</code> 。</span> <span>返回实际跳过的字节数。</span> <span>如果它向前跳，它返回一个正值。</span> <span>如果它向后跳，它返回一个负值。</span> </p> 
           <p> <span>该方法可能会跳过比后备文件中剩余的字节更多的字节。</span> <span>这不会产生异常，并且跳过的字节数可能包括超出后台文件的EOF的一些字节数。</span> <span>尝试在跳过结束后从流中读取将导致-1表示文件的结尾。</span> </p> 
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
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果n为负，如果流不支持查询，或者发生I / O错误。 
           </dd> 
          </dl> </li> 
        </ul> <a name="available--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>available</h4> <pre>public&nbsp;int&nbsp;available()
              throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>返回从此输入流中可以读取（或跳过）的剩余字节数的估计值，而不会被下一次调用此输入流的方法阻塞。</span> 
           <span>当文件位置超出EOF时返回0。</span> 
           <span>下一个调用可能是同一个线程或另一个线程。</span> 
           <span>这个多个字节的单个读取或跳过将不会被阻塞，但可以读取或跳过较少的字节。</span> 
           <p> <span>在某些情况下，非阻塞读取（或跳过）在缓慢时可能会被阻止，例如在慢速网络中读取大文件时。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/InputStream.html#available--">available</a></code>在 
            <code><a href="../../java/io/InputStream.html" title="class in java.io">InputStream</a></code> 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             可以从该输入流中读取（或跳过）而不阻塞的剩余字节数的估计。 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果此文件输入流已通过调用 
            <code>close</code>关闭或发生I / O错误。 
           </dd> 
          </dl> </li> 
        </ul> <a name="close--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>close</h4> <pre>public&nbsp;void&nbsp;close()
           throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>关闭此文件输入流并释放与流相关联的任何系统资源。</span> 
           <p> <span>如果该流具有相关联的信道，则该信道也被关闭。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">Specified by:</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/Closeable.html#close--">close</a></code>在接口 
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
            <code><a href="../../java/io/InputStream.html" title="class in java.io">InputStream</a></code>类 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生I / O错误。 
           </dd> 
          </dl> </li> 
        </ul> <a name="getFD--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>getFD</h4> <pre>public final&nbsp;<a href="../../java/io/FileDescriptor.html" title="class in java.io">FileDescriptor</a>&nbsp;getFD()
                           throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block">
            返回 
           <code>FileDescriptor</code>对象，表示与该FileInputStream正在使用的文件系统中的实际文件的 
           <code>FileInputStream</code> 。 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             与此流关联的文件描述符对象。 
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
            <span><a href="../../java/io/FileDescriptor.html" title="java.io中的类"><code>FileDescriptor</code></a></span> 
           </dd> 
          </dl> </li> 
        </ul> <a name="getChannel--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>getChannel</h4> <pre>public&nbsp;<a href="../../java/nio/channels/FileChannel.html" title="class in java.nio.channels">FileChannel</a>&nbsp;getChannel()</pre> 
          <div class="block"> 
           <span>返回与此文件输入流相关联的唯一<a href="../../java/nio/channels/FileChannel.html" title="java.nio.channels中的类"><code>FileChannel</code></a>对象。</span> 
           <p> <span>返回通道的初始<a href="../../java/nio/channels/FileChannel.html#position--"><code>position</code></a>将等于从文件读取的字节数到目前为止。</span> <span>从该流读取字节将增加通道的位置。</span> <span>通过显式地或通过阅读来改变频道的位置将会改变这个流的文件位置。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             与此文件输入流关联的文件通道 
           </dd> 
           <dt> 
            <span class="simpleTagLabel">从以下版本开始：</span> 
           </dt> 
           <dd>
             1.4 
           </dd> 
          </dl> </li> 
        </ul> <a name="finalize--"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>finalize</h4> <pre>protected&nbsp;void&nbsp;finalize()
                 throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block">
            确保当没有更多的引用时，调用此文件输入流的 
           <code>close</code>方法。 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/Object.html#finalize--">finalize</a></code>在 
            <code><a href="../../java/lang/Object.html" title="class in java.lang">Object</a></code>类 
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
            <a href="../../java/io/FileInputStream.html#close--"><code>close()</code></a> 
           </dd> 
          </dl> </li> 
        </ul> </li> 
      </ul> </li> 
    </ul> 
   </div> 
  </div>
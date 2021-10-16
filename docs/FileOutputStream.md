<div class="contentContainer"> 
   <ul class="inheritance"> 
    <li><a href="../../java/lang/Object.html" title="class in java.lang">java.lang.Object</a></li> 
    <li> 
     <ul class="inheritance"> 
      <li><a href="../../java/io/OutputStream.html" title="class in java.io">java.io.OutputStream</a></li> 
      <li> 
       <ul class="inheritance"> 
        <li>java.io.FileOutputStream</li> 
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
      <hr> <br> <pre>public class <span class="typeNameLabel">FileOutputStream</span>
extends <a href="../../java/io/OutputStream.html" title="class in java.io">OutputStream</a></pre> 
      <div class="block"> 
       <span>文件输出流是用于将数据写入到输出流<code>File</code>或一个<code>FileDescriptor</code> 。</span> 
       <span>文件是否可用或可能被创建取决于底层平台。</span> 
       <span>特别是某些平台允许一次只能打开一个文件来写入一个<tt>FileOutputStream</tt> （或其他文件写入对象）。</span> 
       <span>在这种情况下，如果所涉及的文件已经打开，则此类中的构造函数将失败。</span> 
       <p> <span><code>FileOutputStream</code>用于写入诸如图像数据的原始字节流。</span> <span>对于写入字符流，请考虑使用<code>FileWriter</code> 。</span> </p> 
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
        <span><a href="../../java/io/File.html" title="java.io中的类"><code>File</code></a> ， <a href="../../java/io/FileDescriptor.html" title="java.io中的类"><code>FileDescriptor</code></a> ， <a href="../../java/io/FileInputStream.html" title="java.io中的类"><code>FileInputStream</code></a> ， <a href="../../java/nio/file/Files.html#newOutputStream-java.nio.file.Path-java.nio.file.OpenOption...-"><code>Files.newOutputStream(java.nio.file.Path, java.nio.file.OpenOption...)</code></a></span> 
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
           <td class="colOne"><code><span class="memberNameLink"><a href="../../java/io/FileOutputStream.html#FileOutputStream-java.io.File-">FileOutputStream</a></span>(<a href="../../java/io/File.html" title="class in java.io">File</a>&nbsp;file)</code> 
            <div class="block">
              创建文件输出流以写入由指定的 
             <code>File</code>对象表示的文件。 
            </div> </td> 
          </tr> 
          <tr class="rowColor"> 
           <td class="colOne"><code><span class="memberNameLink"><a href="../../java/io/FileOutputStream.html#FileOutputStream-java.io.File-boolean-">FileOutputStream</a></span>(<a href="../../java/io/File.html" title="class in java.io">File</a>&nbsp;file, boolean&nbsp;append)</code> 
            <div class="block">
              创建文件输出流以写入由指定的 
             <code>File</code>对象表示的文件。 
            </div> </td> 
          </tr> 
          <tr class="altColor"> 
           <td class="colOne"><code><span class="memberNameLink"><a href="../../java/io/FileOutputStream.html#FileOutputStream-java.io.FileDescriptor-">FileOutputStream</a></span>(<a href="../../java/io/FileDescriptor.html" title="class in java.io">FileDescriptor</a>&nbsp;fdObj)</code> 
            <div class="block">
              创建文件输出流以写入指定的文件描述符，表示与文件系统中实际文件的现有连接。 
            </div> </td> 
          </tr> 
          <tr class="rowColor"> 
           <td class="colOne"><code><span class="memberNameLink"><a href="../../java/io/FileOutputStream.html#FileOutputStream-java.lang.String-">FileOutputStream</a></span>(<a href="../../java/lang/String.html" title="class in java.lang">String</a>&nbsp;name)</code> 
            <div class="block">
              创建文件输出流以指定的名称写入文件。 
            </div> </td> 
          </tr> 
          <tr class="altColor"> 
           <td class="colOne"><code><span class="memberNameLink"><a href="../../java/io/FileOutputStream.html#FileOutputStream-java.lang.String-boolean-">FileOutputStream</a></span>(<a href="../../java/lang/String.html" title="class in java.lang">String</a>&nbsp;name, boolean&nbsp;append)</code> 
            <div class="block">
              创建文件输出流以指定的名称写入文件。 
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
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/FileOutputStream.html#close--">close</a></span>()</code> 
            <div class="block">
              关闭此文件输出流并释放与此流相关联的任何系统资源。 
            </div> </td> 
          </tr> 
          <tr id="i1" class="rowColor"> 
           <td class="colFirst"><code>protected void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/FileOutputStream.html#finalize--">finalize</a></span>()</code> 
            <div class="block">
              清理与文件的连接，并确保当没有更多的引用此流时，将调用此文件输出流的 
             <code>close</code>方法。 
            </div> </td> 
          </tr> 
          <tr id="i2" class="altColor"> 
           <td class="colFirst"><code><a href="../../java/nio/channels/FileChannel.html" title="class in java.nio.channels">FileChannel</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/FileOutputStream.html#getChannel--">getChannel</a></span>()</code> 
            <div class="block"> 
             <span>返回与此文件输出流相关联的唯一的<a href="../../java/nio/channels/FileChannel.html" title="java.nio.channels中的类"><code>FileChannel</code></a>对象。</span> 
            </div> </td> 
          </tr> 
          <tr id="i3" class="rowColor"> 
           <td class="colFirst"><code><a href="../../java/io/FileDescriptor.html" title="class in java.io">FileDescriptor</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/FileOutputStream.html#getFD--">getFD</a></span>()</code> 
            <div class="block">
              返回与此流相关联的文件描述符。 
            </div> </td> 
          </tr> 
          <tr id="i4" class="altColor"> 
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/FileOutputStream.html#write-byte:A-">write</a></span>(byte[]&nbsp;b)</code> 
            <div class="block">
              将 
             <code>b.length</code>个字节从指定的字节数组写入此文件输出流。 
            </div> </td> 
          </tr> 
          <tr id="i5" class="rowColor"> 
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/FileOutputStream.html#write-byte:A-int-int-">write</a></span>(byte[]&nbsp;b, int&nbsp;off, int&nbsp;len)</code> 
            <div class="block">
              将 
             <code>len</code>字节从位于偏移量 
             <code>off</code>的指定字节数组写入此文件输出流。 
            </div> </td> 
          </tr> 
          <tr id="i6" class="altColor"> 
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/FileOutputStream.html#write-int-">write</a></span>(int&nbsp;b)</code> 
            <div class="block">
              将指定的字节写入此文件输出流。 
            </div> </td> 
          </tr> 
         </tbody> 
        </table> 
        <ul class="blockList"> 
         <li class="blockList"><a name="methods.inherited.from.class.java.io.OutputStream"> 
           <!--   --> </a> <h3>Methods inherited from class&nbsp;java.io.<a href="../../java/io/OutputStream.html" title="class in java.io">OutputStream</a></h3> <code><a href="../../java/io/OutputStream.html#flush--">flush</a></code></li> 
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
         <!--   --> </a> <h3>构造方法详细信息</h3> <a name="FileOutputStream-java.lang.String-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>FileOutputStream</h4> <pre>public&nbsp;FileOutputStream(<a href="../../java/lang/String.html" title="class in java.lang">String</a>&nbsp;name)
                 throws <a href="../../java/io/FileNotFoundException.html" title="class in java.io">FileNotFoundException</a></pre> 
          <div class="block"> 
           <span>创建文件输出流以指定的名称写入文件。</span> 
           <span>创建一个新的<code>FileDescriptor</code>对象来表示此文件连接。</span> 
           <p> <span>首先，如果有一个安全管理器，它的<code>checkWrite</code>方法<code>name</code>作为参数来调用。</span> </p> 
           <p> <span>如果文件存在但是是一个目录而不是常规文件，不存在但不能创建，或者由于任何其他原因无法打开，那么抛出一个<code>FileNotFoundException</code> 。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>name</code> - 与系统相关的文件名 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/FileNotFoundException.html" title="class in java.io">FileNotFoundException</a></code> - 如果文件存在但是是一个目录而不是常规文件，不存在但不能创建，或者由于任何其他原因无法打开 
           </dd> 
           <dd> 
            <code><a href="../../java/lang/SecurityException.html" title="class in java.lang">SecurityException</a></code> - 如果安全管理器存在，并且其 
            <code>checkWrite</code>方法拒绝对该文件的写入访问。 
           </dd> 
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <a href="../../java/lang/SecurityManager.html#checkWrite-java.lang.String-"><code>SecurityManager.checkWrite(java.lang.String)</code></a> 
           </dd> 
          </dl> </li> 
        </ul> <a name="FileOutputStream-java.lang.String-boolean-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>FileOutputStream</h4> <pre>public&nbsp;FileOutputStream(<a href="../../java/lang/String.html" title="class in java.lang">String</a>&nbsp;name,
                        boolean&nbsp;append)
                 throws <a href="../../java/io/FileNotFoundException.html" title="class in java.io">FileNotFoundException</a></pre> 
          <div class="block"> 
           <span>创建文件输出流以指定的名称写入文件。</span> 
           <span>如果第二个参数是<code>true</code> ，则字节将写入文件的末尾而不是开头。</span> 
           <span>创建一个新的<code>FileDescriptor</code>对象来表示此文件连接。</span> 
           <p> <span>首先，如果有一个安全管理员，它的<code>checkWrite</code>方法是以<code>name</code>作为参数来调用的。</span> </p> 
           <p> <span>如果文件存在但是是一个目录而不是常规文件，不存在但不能创建，或者由于任何其他原因无法打开，那么抛出一个<code>FileNotFoundException</code> 。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>name</code> - 与系统相关的文件名 
           </dd> 
           <dd> 
            <code>append</code> - 如果是 
            <code>true</code> ，那么字节将被写入文件的末尾，而不是开头 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/FileNotFoundException.html" title="class in java.io">FileNotFoundException</a></code> - 如果文件存在但是是一个目录而不是常规文件，不存在但不能创建，或由于任何其他原因无法打开。 
           </dd> 
           <dd> 
            <code><a href="../../java/lang/SecurityException.html" title="class in java.lang">SecurityException</a></code> - 如果安全管理器存在，并且其 
            <code>checkWrite</code>方法拒绝对该文件的写入访问。 
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
            <a href="../../java/lang/SecurityManager.html#checkWrite-java.lang.String-"><code>SecurityManager.checkWrite(java.lang.String)</code></a> 
           </dd> 
          </dl> </li> 
        </ul> <a name="FileOutputStream-java.io.File-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>FileOutputStream</h4> <pre>public&nbsp;FileOutputStream(<a href="../../java/io/File.html" title="class in java.io">File</a>&nbsp;file)
                 throws <a href="../../java/io/FileNotFoundException.html" title="class in java.io">FileNotFoundException</a></pre> 
          <div class="block"> 
           <span>创建文件输出流以写入由指定的<code>File</code>对象表示的文件。</span> 
           <span>创建一个新的<code>FileDescriptor</code>对象来表示此文件连接。</span> 
           <p> <span>首先，如果有一个安全管理器，它的<code>checkWrite</code>方法被调用与由<code>file</code>参数表示的路径作为其参数。</span> </p> 
           <p> <span>如果文件存在但是是一个目录而不是常规文件，则不存在但不能创建，或者由于任何其他原因无法打开，因此抛出<code>FileNotFoundException</code> 。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>file</code> - 要打开的文件进行写入。 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/FileNotFoundException.html" title="class in java.io">FileNotFoundException</a></code> - 如果文件存在但是是一个目录而不是常规文件，不存在但不能创建，或由于任何其他原因无法打开 
           </dd> 
           <dd> 
            <code><a href="../../java/lang/SecurityException.html" title="class in java.lang">SecurityException</a></code> - 如果安全管理器存在，并且其 
            <code>checkWrite</code>方法拒绝对该文件的写入访问。 
           </dd> 
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <span><a href="../../java/io/File.html#getPath--"><code>File.getPath()</code></a> ， <a href="../../java/lang/SecurityException.html" title="java.lang中的类"><code>SecurityException</code></a> ， <a href="../../java/lang/SecurityManager.html#checkWrite-java.lang.String-"><code>SecurityManager.checkWrite(java.lang.String)</code></a></span> 
           </dd> 
          </dl> </li> 
        </ul> <a name="FileOutputStream-java.io.File-boolean-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>FileOutputStream</h4> <pre>public&nbsp;FileOutputStream(<a href="../../java/io/File.html" title="class in java.io">File</a>&nbsp;file,
                        boolean&nbsp;append)
                 throws <a href="../../java/io/FileNotFoundException.html" title="class in java.io">FileNotFoundException</a></pre> 
          <div class="block"> 
           <span>创建文件输出流以写入由指定的<code>File</code>对象表示的文件。</span> 
           <span>如果第二个参数是<code>true</code> ，则字节将被写入文件的末尾而不是开头。</span> 
           <span>创建一个新的<code>FileDescriptor</code>对象来表示此文件连接。</span> 
           <p> <span>首先，如果有一个安全管理器，则调用其<code>checkWrite</code>方法，其中以<code>file</code>参数表示的路径作为参数。</span> </p> 
           <p> <span>如果文件存在但是是一个目录而不是常规文件，不存在但不能创建，或者由于任何其他原因无法打开，那么将抛出一个<code>FileNotFoundException</code> 。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>file</code> - 要打开的文件写入。 
           </dd> 
           <dd> 
            <code>append</code> - 如果 
            <code>true</code> ，则字节将被写入文件的末尾而不是开头 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/FileNotFoundException.html" title="class in java.io">FileNotFoundException</a></code> - 如果文件存在但是是一个目录而不是常规文件，不存在但不能创建，或由于任何其他原因无法打开 
           </dd> 
           <dd> 
            <code><a href="../../java/lang/SecurityException.html" title="class in java.lang">SecurityException</a></code> - 如果安全管理器存在，并且其 
            <code>checkWrite</code>方法拒绝对该文件的写入访问。 
           </dd> 
           <dt> 
            <span class="simpleTagLabel">从以下版本开始：</span> 
           </dt> 
           <dd>
             1.4 
           </dd> 
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <span><a href="../../java/io/File.html#getPath--"><code>File.getPath()</code></a> ， <a href="../../java/lang/SecurityException.html" title="java.lang中的类"><code>SecurityException</code></a> ， <a href="../../java/lang/SecurityManager.html#checkWrite-java.lang.String-"><code>SecurityManager.checkWrite(java.lang.String)</code></a></span> 
           </dd> 
          </dl> </li> 
        </ul> <a name="FileOutputStream-java.io.FileDescriptor-"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>FileOutputStream</h4> <pre>public&nbsp;FileOutputStream(<a href="../../java/io/FileDescriptor.html" title="class in java.io">FileDescriptor</a>&nbsp;fdObj)</pre> 
          <div class="block"> 
           <span>创建文件输出流以写入指定的文件描述符，表示与文件系统中实际文件的现有连接。</span> 
           <p> <span>首先，如果有一个安全管理器，它的<code>checkWrite</code>方法被调用与文件描述符<code>fdObj</code>参数作为其参数。</span> </p> 
           <p> <span>如果<code>fdObj</code>为null，则抛出<code>NullPointerException</code> 。</span> </p> 
           <p> <span>如果<code>fdObj</code>是<a href="../../java/io/FileDescriptor.html#valid--"><code>invalid</code>，</a>这个构造函数不会抛出<a href="../../java/io/FileDescriptor.html#valid--">异常</a> 。</span> <span>但是，如果在结果流上调用方法来尝试流上的I / O，则会抛出一个<code>IOException</code> 。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>fdObj</code> - 要打开来写入的文件描述符 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/SecurityException.html" title="class in java.lang">SecurityException</a></code> - 如果安全管理器存在，并且其 
            <code>checkWrite</code>方法拒绝对 
            <code>checkWrite</code>写入访问 
           </dd> 
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <a href="../../java/lang/SecurityManager.html#checkWrite-java.io.FileDescriptor-"><code>SecurityManager.checkWrite(java.io.FileDescriptor)</code></a> 
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
         <li class="blockList"> <h4>write</h4> <pre>public&nbsp;void&nbsp;write(int&nbsp;b)
           throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>将指定的字节写入此文件输出流。</span> 
           <span>实现<code>write</code>方法<code>OutputStream</code> 。</span> 
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
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生I / O错误。 
           </dd> 
          </dl> </li> 
        </ul> <a name="write-byte:A-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>write</h4> <pre>public&nbsp;void&nbsp;write(byte[]&nbsp;b)
           throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block">
            将 
           <code>b.length</code>字节从指定的字节数组写入此文件输出流。 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/OutputStream.html#write-byte:A-">write</a></code>在 
            <code><a href="../../java/io/OutputStream.html" title="class in java.io">OutputStream</a></code> 
           </dd> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>b</code> - 数据。 
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
            <a href="../../java/io/OutputStream.html#write-byte:A-int-int-"><code>OutputStream.write(byte[], int, int)</code></a> 
           </dd> 
          </dl> </li> 
        </ul> <a name="write-byte:A-int-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>write</h4> <pre>public&nbsp;void&nbsp;write(byte[]&nbsp;b,
                  int&nbsp;off,
                  int&nbsp;len)
           throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block">
            从位于偏移量 
           <code>off</code>的指定字节数组写入 
           <code>len</code>字节到该文件输出流。 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/OutputStream.html#write-byte:A-int-int-">write</a></code>在 
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
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></code> - 如果发生I / O错误。 
           </dd> 
          </dl> </li> 
        </ul> <a name="close--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>close</h4> <pre>public&nbsp;void&nbsp;close()
           throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>关闭此文件输出流并释放与此流相关联的任何系统资源。</span> 
           <span>此文件输出流可能不再用于写入字节。</span> 
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
        </ul> <a name="getFD--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>getFD</h4> <pre>public final&nbsp;<a href="../../java/io/FileDescriptor.html" title="class in java.io">FileDescriptor</a>&nbsp;getFD()
                           throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block">
            返回与此流相关联的文件描述符。 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd> 
            <code>FileDescriptor</code>对象，表示与该 
            <code>FileOutputStream</code>对象正在使用的文件系统中的文件的 
            <code>FileOutputStream</code> 。 
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
           <span>返回与此文件输出流相关联的唯一的<a href="../../java/nio/channels/FileChannel.html" title="java.nio.channels中的类"><code>FileChannel</code></a>对象。</span> 
           <p> <span>返回通道的初始<a href="../../java/nio/channels/FileChannel.html#position--"><code>position</code></a>将等于写入文件的字节数，除非该流是附加模式，在这种情况下，它将等于文件的大小。</span> <span>将字节写入此流将相应地增加通道的位置。</span> <span>通过显式地或通过写入来更改频道的位置将会改变这个流的文件位置。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             与此文件输出流关联的文件通道 
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
            清除与文件的连接，并确保当没有对此流的更多引用时，调用此文件输出流的 
           <code>close</code>方法。 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/Object.html#finalize--">finalize</a></code>在 
            <code><a href="../../java/lang/Object.html" title="class in java.lang">Object</a></code> 
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
            <a href="../../java/io/FileInputStream.html#close--"><code>FileInputStream.close()</code></a> 
           </dd> 
          </dl> </li> 
        </ul> </li> 
      </ul> </li> 
    </ul> 
   </div> 
  </div>
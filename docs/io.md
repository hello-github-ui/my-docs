<div class="header"> 
   <h1 title="Package" class="title">Package&nbsp;java.io</h1> 
   <div class="docSummary"> 
    <div class="block">
      通过数据流，序列化和文件系统提供系统输入和输出。 
    </div> 
   </div> 
   <p>See:&nbsp;<a href="#package.description">描述</a></p> 
  </div>
  <div class="contentContainer"> 
   <ul class="blockList"> 
    <li class="blockList"> 
     <table class="typeSummary" border="0" cellpadding="3" cellspacing="0" summary="Interface Summary table, listing interfaces, and an explanation"> 
      <caption> 
       <span>接口摘要</span> 
       <span class="tabEnd">&nbsp;</span> 
      </caption> 
      <tbody> 
       <tr> 
        <th class="colFirst" scope="col">接口</th> 
        <th class="colLast" scope="col">描述</th> 
       </tr> 
      </tbody> 
      <tbody> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/Closeable.html" title="interface in java.io">Closeable</a></td> 
        <td class="colLast"> 
         <div class="block">
           A 
          <code>Closeable</code>是可以关闭的数据的源或目的地。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/DataInput.html" title="interface in java.io">DataInput</a></td> 
        <td class="colLast"> 
         <div class="block"> 
          <code>DataInput</code>接口提供从二进制流读取字节，并从其中重建任何Java基元类型的数据。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/DataOutput.html" title="interface in java.io">DataOutput</a></td> 
        <td class="colLast"> 
         <div class="block"> 
          <code>DataOutput</code>接口提供将数据从任何Java基本类型转换为一系列字节，并将这些字节写入二进制流。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/Externalizable.html" title="interface in java.io">Externalizable</a></td> 
        <td class="colLast"> 
         <div class="block">
           只有Externalizable实例的类的身份才能写入序列化流中，并且该类负责保存和恢复其实例的内容。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/FileFilter.html" title="interface in java.io">FileFilter</a></td> 
        <td class="colLast"> 
         <div class="block">
           抽象路径名的过滤器。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/FilenameFilter.html" title="interface in java.io">FilenameFilter</a></td> 
        <td class="colLast"> 
         <div class="block">
           用于实现此接口的类的实例用于过滤文件名。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/Flushable.html" title="interface in java.io">Flushable</a></td> 
        <td class="colLast"> 
         <div class="block">
           A 
          <tt>Flushable</tt>是可以刷新的数据的目的地。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/ObjectInput.html" title="interface in java.io">ObjectInput</a></td> 
        <td class="colLast"> 
         <div class="block">
           ObjectInput扩展了DataInput接口以包含对象的读取。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/ObjectInputValidation.html" title="interface in java.io">ObjectInputValidation</a></td> 
        <td class="colLast"> 
         <div class="block">
           回调界面允许验证图中的对象。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/ObjectOutput.html" title="interface in java.io">ObjectOutput</a></td> 
        <td class="colLast"> 
         <div class="block">
           ObjectOutput扩展了DataOutput接口，包括写入对象。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/ObjectStreamConstants.html" title="interface in java.io">ObjectStreamConstants</a></td> 
        <td class="colLast"> 
         <div class="block">
           写入对象序列化流的常量。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/Serializable.html" title="interface in java.io">Serializable</a></td> 
        <td class="colLast"> 
         <div class="block">
           类的序列化由实现java.io.Serializable接口的类启用。 
         </div> </td> 
       </tr> 
      </tbody> 
     </table> </li> 
    <li class="blockList"> 
     <table class="typeSummary" border="0" cellpadding="3" cellspacing="0" summary="Class Summary table, listing classes, and an explanation"> 
      <caption> 
       <span>类摘要</span> 
       <span class="tabEnd">&nbsp;</span> 
      </caption> 
      <tbody> 
       <tr> 
        <th class="colFirst" scope="col">类</th> 
        <th class="colLast" scope="col">描述</th> 
       </tr> 
      </tbody> 
      <tbody> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/BufferedInputStream.html" title="class in java.io">BufferedInputStream</a></td> 
        <td class="colLast"> 
         <div class="block">
           A 
          <code>BufferedInputStream</code>为另一个输入流添加了功能，即缓冲输入和支持 
          <code>mark</code>和 
          <code>reset</code>方法的功能。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/BufferedOutputStream.html" title="class in java.io">BufferedOutputStream</a></td> 
        <td class="colLast"> 
         <div class="block">
           该类实现缓冲输出流。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/BufferedReader.html" title="class in java.io">BufferedReader</a></td> 
        <td class="colLast"> 
         <div class="block">
           从字符输入流读取文本，缓冲字符，以提供字符，数组和行的高效读取。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/BufferedWriter.html" title="class in java.io">BufferedWriter</a></td> 
        <td class="colLast"> 
         <div class="block">
           将文本写入字符输出流，缓冲字符，以提供单个字符，数组和字符串的高效写入。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/ByteArrayInputStream.html" title="class in java.io">ByteArrayInputStream</a></td> 
        <td class="colLast"> 
         <div class="block">
           A 
          <code>ByteArrayInputStream</code>包含一个内部缓冲区，其中包含可以从流中读取的字节。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/ByteArrayOutputStream.html" title="class in java.io">ByteArrayOutputStream</a></td> 
        <td class="colLast"> 
         <div class="block">
           该类实现了将数据写入字节数组的输出流。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/CharArrayReader.html" title="class in java.io">CharArrayReader</a></td> 
        <td class="colLast"> 
         <div class="block">
           该类实现了一个字符缓冲区，可以用作字符输入流。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/CharArrayWriter.html" title="class in java.io">CharArrayWriter</a></td> 
        <td class="colLast"> 
         <div class="block">
           该类实现了可以用作Writer的字符缓冲区。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/Console.html" title="class in java.io">Console</a></td> 
        <td class="colLast"> 
         <div class="block">
           访问与当前Java虚拟机关联的基于字符的控制台设备（如果有的话）的方法。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/DataInputStream.html" title="class in java.io">DataInputStream</a></td> 
        <td class="colLast"> 
         <div class="block">
           数据输入流允许应用程序以独立于机器的方式从底层输入流读取原始Java数据类型。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/DataOutputStream.html" title="class in java.io">DataOutputStream</a></td> 
        <td class="colLast"> 
         <div class="block">
           数据输出流使应用程序以便携式方式将原始Java数据类型写入输出流。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/File.html" title="class in java.io">File</a></td> 
        <td class="colLast"> 
         <div class="block">
           文件和目录路径名的抽象表示。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/FileDescriptor.html" title="class in java.io">FileDescriptor</a></td> 
        <td class="colLast"> 
         <div class="block">
           文件描述符类的实例用作表示打开文件，开放套接字或其他字节源或信宿的底层机器特定结构的不透明句柄。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/FileInputStream.html" title="class in java.io">FileInputStream</a></td> 
        <td class="colLast"> 
         <div class="block">
           A 
          <code>FileInputStream</code>从文件系统中的文件获取输入字节。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/FileOutputStream.html" title="class in java.io">FileOutputStream</a></td> 
        <td class="colLast"> 
         <div class="block">
           文件输出流是用于将数据写入到输出流 
          <code>File</code>或一个 
          <code>FileDescriptor</code> 。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/FilePermission.html" title="class in java.io">FilePermission</a></td> 
        <td class="colLast"> 
         <div class="block">
           此类表示访问文件或目录。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/FileReader.html" title="class in java.io">FileReader</a></td> 
        <td class="colLast"> 
         <div class="block">
           阅读字符文件的便利课。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/FileWriter.html" title="class in java.io">FileWriter</a></td> 
        <td class="colLast"> 
         <div class="block">
           方便课写字符文件。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/FilterInputStream.html" title="class in java.io">FilterInputStream</a></td> 
        <td class="colLast"> 
         <div class="block">
           A 
          <code>FilterInputStream</code>包含一些其他输入流，它用作其基本的数据源，可能会沿着路径转换数据或提供附加功能。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/FilterOutputStream.html" title="class in java.io">FilterOutputStream</a></td> 
        <td class="colLast"> 
         <div class="block">
           这个类是过滤输出流的所有类的超类。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/FilterReader.html" title="class in java.io">FilterReader</a></td> 
        <td class="colLast"> 
         <div class="block">
           用于读取过滤后的字符流的抽象类。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/FilterWriter.html" title="class in java.io">FilterWriter</a></td> 
        <td class="colLast"> 
         <div class="block">
           用于编写过滤后的字符流的抽象类。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/InputStream.html" title="class in java.io">InputStream</a></td> 
        <td class="colLast"> 
         <div class="block">
           这个抽象类是表示输入字节流的所有类的超类。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/InputStreamReader.html" title="class in java.io">InputStreamReader</a></td> 
        <td class="colLast"> 
         <div class="block"> 
          <span>InputStreamReader是从字节流到字符流的桥梁：它读取字节，并使用指定的<code>charset</code>将其解码为<a href="../../java/nio/charset/Charset.html" title="java.nio.charset中的类">字符</a> 。</span> 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/LineNumberInputStream.html" title="class in java.io">LineNumberInputStream</a></td> 
        <td class="colLast">Deprecated 
         <div class="block"> 
          <span class="deprecationComment">该类错误地假定字节充分表示字符。</span> 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/LineNumberReader.html" title="class in java.io">LineNumberReader</a></td> 
        <td class="colLast"> 
         <div class="block">
           缓冲字符输入流，跟踪行号。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/ObjectInputStream.html" title="class in java.io">ObjectInputStream</a></td> 
        <td class="colLast"> 
         <div class="block">
           ObjectInputStream反序列化先前使用ObjectOutputStream编写的原始数据和对象。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/ObjectInputStream.GetField.html" title="class in java.io">ObjectInputStream.GetField</a></td> 
        <td class="colLast"> 
         <div class="block">
           提供对从输入流读取的持久性字段的访问。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/ObjectOutputStream.html" title="class in java.io">ObjectOutputStream</a></td> 
        <td class="colLast"> 
         <div class="block">
           ObjectOutputStream将Java对象的原始数据类型和图形写入OutputStream。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/ObjectOutputStream.PutField.html" title="class in java.io">ObjectOutputStream.PutField</a></td> 
        <td class="colLast"> 
         <div class="block">
           提供对要写入ObjectOutput的持久字段的编程访问。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/ObjectStreamClass.html" title="class in java.io">ObjectStreamClass</a></td> 
        <td class="colLast"> 
         <div class="block">
           序列化的类的描述符。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/ObjectStreamField.html" title="class in java.io">ObjectStreamField</a></td> 
        <td class="colLast"> 
         <div class="block">
           Serializable类的Serializable字段的描述。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/OutputStream.html" title="class in java.io">OutputStream</a></td> 
        <td class="colLast"> 
         <div class="block">
           这个抽象类是表示字节输出流的所有类的超类。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/OutputStreamWriter.html" title="class in java.io">OutputStreamWriter</a></td> 
        <td class="colLast"> 
         <div class="block"> 
          <span>OutputStreamWriter是字符的桥梁流以字节流：向其写入的字符编码成使用指定的字节<a href="../../java/nio/charset/Charset.html" title="java.nio.charset中的类"><code>charset</code></a> 。</span> 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/PipedInputStream.html" title="class in java.io">PipedInputStream</a></td> 
        <td class="colLast"> 
         <div class="block"> 
          <span>管道输入流应连接到管道输出流;</span> 
          <span>管道输入流然后提供写入管道输出流的任何数据字节。</span> 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/PipedOutputStream.html" title="class in java.io">PipedOutputStream</a></td> 
        <td class="colLast"> 
         <div class="block">
           管道输出流可以连接到管道输入流以创建通信管道。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/PipedReader.html" title="class in java.io">PipedReader</a></td> 
        <td class="colLast"> 
         <div class="block">
           流水字符输入流。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/PipedWriter.html" title="class in java.io">PipedWriter</a></td> 
        <td class="colLast"> 
         <div class="block">
           流水字符输出流。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/PrintStream.html" title="class in java.io">PrintStream</a></td> 
        <td class="colLast"> 
         <div class="block">
           A 
          <code>PrintStream</code>将功能添加到另一个输出流，即能够方便地打印各种数据值的表示。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/PrintWriter.html" title="class in java.io">PrintWriter</a></td> 
        <td class="colLast"> 
         <div class="block">
           将对象的格式表示打印到文本输出流。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/PushbackInputStream.html" title="class in java.io">PushbackInputStream</a></td> 
        <td class="colLast"> 
         <div class="block">
           A 
          <code>PushbackInputStream</code>将功能添加到另一个输入流，即可以“推回”或“未读”一个字节。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/PushbackReader.html" title="class in java.io">PushbackReader</a></td> 
        <td class="colLast"> 
         <div class="block">
           一个字符流读取器，允许将字符推回到流中。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/RandomAccessFile.html" title="class in java.io">RandomAccessFile</a></td> 
        <td class="colLast"> 
         <div class="block">
           该类的实例支持读取和写入随机访问文件。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/Reader.html" title="class in java.io">Reader</a></td> 
        <td class="colLast"> 
         <div class="block">
           用于读取字符流的抽象类。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/SequenceInputStream.html" title="class in java.io">SequenceInputStream</a></td> 
        <td class="colLast"> 
         <div class="block">
           A 
          <code>SequenceInputStream</code>表示其他输入流的逻辑级联。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/SerializablePermission.html" title="class in java.io">SerializablePermission</a></td> 
        <td class="colLast"> 
         <div class="block">
           这个类用于Serializable权限。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/StreamTokenizer.html" title="class in java.io">StreamTokenizer</a></td> 
        <td class="colLast"> 
         <div class="block"> 
          <code>StreamTokenizer</code>类接收输入流并将其解析为“令牌”，允许一次读取一个令牌。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/StringBufferInputStream.html" title="class in java.io">StringBufferInputStream</a></td> 
        <td class="colLast">Deprecated 
         <div class="block"> 
          <span class="deprecationComment">此类不会将字符正确转换为字节。</span> 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/StringReader.html" title="class in java.io">StringReader</a></td> 
        <td class="colLast"> 
         <div class="block">
           一个字符流，其源是一个字符串。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/StringWriter.html" title="class in java.io">StringWriter</a></td> 
        <td class="colLast"> 
         <div class="block">
           在字符串缓冲区中收集其输出的字符流，然后可以用于构造字符串。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/Writer.html" title="class in java.io">Writer</a></td> 
        <td class="colLast"> 
         <div class="block">
           用于写入字符流的抽象类。 
         </div> </td> 
       </tr> 
      </tbody> 
     </table> </li> 
    <li class="blockList"> 
     <table class="typeSummary" border="0" cellpadding="3" cellspacing="0" summary="Exception Summary table, listing exceptions, and an explanation"> 
      <caption> 
       <span>异常摘要</span> 
       <span class="tabEnd">&nbsp;</span> 
      </caption> 
      <tbody> 
       <tr> 
        <th class="colFirst" scope="col">异常</th> 
        <th class="colLast" scope="col">描述</th> 
       </tr> 
      </tbody> 
      <tbody> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/CharConversionException.html" title="class in java.io">CharConversionException</a></td> 
        <td class="colLast"> 
         <div class="block">
           字符转换异常的基类。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/EOFException.html" title="class in java.io">EOFException</a></td> 
        <td class="colLast"> 
         <div class="block">
           表示在输入过程中意外地到达文件结束或流结束。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/FileNotFoundException.html" title="class in java.io">FileNotFoundException</a></td> 
        <td class="colLast"> 
         <div class="block">
           指示尝试打开由指定路径名表示的文件失败。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/InterruptedIOException.html" title="class in java.io">InterruptedIOException</a></td> 
        <td class="colLast"> 
         <div class="block">
           表示I / O操作已中断。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/InvalidClassException.html" title="class in java.io">InvalidClassException</a></td> 
        <td class="colLast"> 
         <div class="block">
           当序列化运行时检测到类中的以下问题之一时抛出。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/InvalidObjectException.html" title="class in java.io">InvalidObjectException</a></td> 
        <td class="colLast"> 
         <div class="block">
           表示一个或多个反序列化对象失败的验证测试。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/IOException.html" title="class in java.io">IOException</a></td> 
        <td class="colLast"> 
         <div class="block">
           表示发生某种类型的I / O异常。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/NotActiveException.html" title="class in java.io">NotActiveException</a></td> 
        <td class="colLast"> 
         <div class="block">
           序列化或反序列化不活动时抛出。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/NotSerializableException.html" title="class in java.io">NotSerializableException</a></td> 
        <td class="colLast"> 
         <div class="block">
           抛出一个实例需要一个Serializable接口。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/ObjectStreamException.html" title="class in java.io">ObjectStreamException</a></td> 
        <td class="colLast"> 
         <div class="block">
           对象流类别特有的所有异常的超类。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/OptionalDataException.html" title="class in java.io">OptionalDataException</a></td> 
        <td class="colLast"> 
         <div class="block">
           表示由于未读原始数据导致的对象读取操作失败的异常，或属于流中序列化对象的数据的结束。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/StreamCorruptedException.html" title="class in java.io">StreamCorruptedException</a></td> 
        <td class="colLast"> 
         <div class="block">
           当从对象流读取的控制信息违反内部一致性检查时抛出。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/SyncFailedException.html" title="class in java.io">SyncFailedException</a></td> 
        <td class="colLast"> 
         <div class="block">
           发出同步操作失败的信号。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/UncheckedIOException.html" title="class in java.io">UncheckedIOException</a></td> 
        <td class="colLast"> 
         <div class="block"> 
          <span>包装一个<a href="../../java/io/IOException.html" title="java.io中的类"><code>IOException</code></a>与未检查的异常。</span> 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/UnsupportedEncodingException.html" title="class in java.io">UnsupportedEncodingException</a></td> 
        <td class="colLast"> 
         <div class="block">
           字符编码不支持。 
         </div> </td> 
       </tr> 
       <tr class="rowColor"> 
        <td class="colFirst"><a href="../../java/io/UTFDataFormatException.html" title="class in java.io">UTFDataFormatException</a></td> 
        <td class="colLast"> 
         <div class="block">
           表示 
          <a href="DataInput.html#modified-utf-8">modified UTF-8</a>格式的格式不正确的字符串已被读入数据输入流或任何实现数据输入接口的类。 
         </div> </td> 
       </tr> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/WriteAbortedException.html" title="class in java.io">WriteAbortedException</a></td> 
        <td class="colLast"> 
         <div class="block">
           指示在写入操作期间抛出ObjectStreamExceptions之一。 
         </div> </td> 
       </tr> 
      </tbody> 
     </table> </li> 
    <li class="blockList"> 
     <table class="typeSummary" border="0" cellpadding="3" cellspacing="0" summary="Error Summary table, listing errors, and an explanation"> 
      <caption> 
       <span>Error Summary</span> 
       <span class="tabEnd">&nbsp;</span> 
      </caption> 
      <tbody> 
       <tr> 
        <th class="colFirst" scope="col">Error</th> 
        <th class="colLast" scope="col">描述</th> 
       </tr> 
      </tbody> 
      <tbody> 
       <tr class="altColor"> 
        <td class="colFirst"><a href="../../java/io/IOError.html" title="class in java.io">IOError</a></td> 
        <td class="colLast"> 
         <div class="block">
           当出现严重I / O错误时抛出。 
         </div> </td> 
       </tr> 
      </tbody> 
     </table> </li> 
   </ul> 
   <a name="package.description"> 
    <!--   --> </a> 
   <h2 title="Package java.io Description">Package java.io Description</h2> 
   <div class="block"> 
    <span>通过数据流，序列化和文件系统提供系统输入和输出。</span> 
    <span>除非另有说明，否则在此包中的任何类或接口中将null参数传递给构造函数或方法将导致抛出<tt>NullPointerException</tt> 。</span> 
    <h2> <span>包装规格</span> </h2> 
    <ul> 
     <li> <span><a href="../../../platform/serialization/spec/serialTOC.html">Java Object Serialization Specification</a></span> </li> 
    </ul> 
    <h2> <span>相关文档</span> </h2> 
    <span>有关概述，教程，示例，指南和工具文档，请参阅：</span> 
    <ul> 
     <li> <span><a href="../../../technotes/guides/serialization">Serialization Enhancements</a></span> </li> 
    </ul> 
   </div> 
   <dl> 
    <dt> 
     <span class="simpleTagLabel">从以下版本开始：</span> 
    </dt> 
    <dd>
      JDK1.0 
    </dd> 
   </dl> 
  </div>
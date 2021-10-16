<div class="contentContainer"> 
   <ul class="inheritance"> 
    <li><a href="../../java/lang/Object.html" title="class in java.lang">java.lang.Object</a></li> 
    <li> 
     <ul class="inheritance"> 
      <li><a href="../../java/io/OutputStream.html" title="class in java.io">java.io.OutputStream</a></li> 
      <li> 
       <ul class="inheritance"> 
        <li><a href="../../java/io/FilterOutputStream.html" title="class in java.io">java.io.FilterOutputStream</a></li> 
        <li> 
         <ul class="inheritance"> 
          <li>java.io.BufferedOutputStream</li> 
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
        <span><a href="../../java/io/Closeable.html" title="java.io中的接口">Closeable</a> ， <a href="../../java/io/Flushable.html" title="java.io中的接口">Flushable</a> ， <a href="../../java/lang/AutoCloseable.html" title="java.lang中的接口">AutoCloseable</a></span> 
       </dd> 
      </dl> 
      <hr> <br> <pre>public class <span class="typeNameLabel">BufferedOutputStream</span>
extends <a href="../../java/io/FilterOutputStream.html" title="class in java.io">FilterOutputStream</a></pre> 
      <div class="block"> 
       <span>该类实现缓冲输出流。</span> 
       <span>通过设置这样的输出流，应用程序可以向底层输出流写入字节，而不必为写入的每个字节导致底层系统的调用。</span> 
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
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedOutputStream.html#buf">buf</a></span></code> 
            <div class="block">
              存储数据的内部缓冲区。 
            </div> </td> 
          </tr> 
          <tr class="rowColor"> 
           <td class="colFirst"><code>protected int</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedOutputStream.html#count">count</a></span></code> 
            <div class="block">
              缓冲区中有效字节的数量。 
            </div> </td> 
          </tr> 
         </tbody> 
        </table> 
        <ul class="blockList"> 
         <li class="blockList"><a name="fields.inherited.from.class.java.io.FilterOutputStream"> 
           <!--   --> </a> <h3>Fields inherited from class&nbsp;java.io.<a href="../../java/io/FilterOutputStream.html" title="class in java.io">FilterOutputStream</a></h3> <code><a href="../../java/io/FilterOutputStream.html#out">out</a></code></li> 
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
           <td class="colOne"><code><span class="memberNameLink"><a href="../../java/io/BufferedOutputStream.html#BufferedOutputStream-java.io.OutputStream-">BufferedOutputStream</a></span>(<a href="../../java/io/OutputStream.html" title="class in java.io">OutputStream</a>&nbsp;out)</code> 
            <div class="block">
              创建一个新的缓冲输出流，以将数据写入指定的底层输出流。 
            </div> </td> 
          </tr> 
          <tr class="rowColor"> 
           <td class="colOne"><code><span class="memberNameLink"><a href="../../java/io/BufferedOutputStream.html#BufferedOutputStream-java.io.OutputStream-int-">BufferedOutputStream</a></span>(<a href="../../java/io/OutputStream.html" title="class in java.io">OutputStream</a>&nbsp;out, int&nbsp;size)</code> 
            <div class="block">
              创建一个新的缓冲输出流，以便以指定的缓冲区大小将数据写入指定的底层输出流。 
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
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedOutputStream.html#flush--">flush</a></span>()</code> 
            <div class="block">
              刷新缓冲输出流。 
            </div> </td> 
          </tr> 
          <tr id="i1" class="rowColor"> 
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedOutputStream.html#write-byte:A-int-int-">write</a></span>(byte[]&nbsp;b, int&nbsp;off, int&nbsp;len)</code> 
            <div class="block">
              从指定的字节数组写入 
             <code>len</code>个字节，从偏移 
             <code>off</code>开始到缓冲的输出流。 
            </div> </td> 
          </tr> 
          <tr id="i2" class="altColor"> 
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/io/BufferedOutputStream.html#write-int-">write</a></span>(int&nbsp;b)</code> 
            <div class="block">
              将指定的字节写入缓冲的输出流。 
            </div> </td> 
          </tr> 
         </tbody> 
        </table> 
        <ul class="blockList"> 
         <li class="blockList"><a name="methods.inherited.from.class.java.io.FilterOutputStream"> 
           <!--   --> </a> <h3>Methods inherited from class&nbsp;java.io.<a href="../../java/io/FilterOutputStream.html" title="class in java.io">FilterOutputStream</a></h3> <code><a href="../../java/io/FilterOutputStream.html#close--">close</a>, <a href="../../java/io/FilterOutputStream.html#write-byte:A-">write</a></code></li> 
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
            存储数据的内部缓冲区。 
          </div> </li> 
        </ul> <a name="count"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>count</h4> <pre>protected&nbsp;int count</pre> 
          <div class="block"> 
           <span>缓冲区中有效字节的数量。</span> 
           <span>此值始终在<tt>0</tt>到<tt>buf.length之间</tt> ;</span> 
           <span>元素<tt>buf[0]</tt>至<tt>buf[count-1]</tt>包含有效的字节数据。</span> 
          </div> </li> 
        </ul> </li> 
      </ul> 
      <!-- ========= CONSTRUCTOR DETAIL ======== --> 
      <ul class="blockList"> 
       <li class="blockList"><a name="constructor.detail"> 
         <!--   --> </a> <h3>构造方法详细信息</h3> <a name="BufferedOutputStream-java.io.OutputStream-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>BufferedOutputStream</h4> <pre>public&nbsp;BufferedOutputStream(<a href="../../java/io/OutputStream.html" title="class in java.io">OutputStream</a>&nbsp;out)</pre> 
          <div class="block">
            创建一个新的缓冲输出流，以将数据写入指定的底层输出流。 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>out</code> - 底层输出流。 
           </dd> 
          </dl> </li> 
        </ul> <a name="BufferedOutputStream-java.io.OutputStream-int-"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>BufferedOutputStream</h4> <pre>public&nbsp;BufferedOutputStream(<a href="../../java/io/OutputStream.html" title="class in java.io">OutputStream</a>&nbsp;out,
                            int&nbsp;size)</pre> 
          <div class="block">
            创建一个新的缓冲输出流，以便以指定的缓冲区大小将数据写入指定的底层输出流。 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>out</code> - 底层输出流。 
           </dd> 
           <dd> 
            <code>size</code> - 缓冲区大小。 
           </dd> 
           <dt> 
            <span class="throwsLabel">异常</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/IllegalArgumentException.html" title="class in java.lang">IllegalArgumentException</a></code> - 如果大小&lt;= 0。 
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
            将指定的字节写入缓冲的输出流。 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/FilterOutputStream.html#write-int-">write</a></code>在 
            <code><a href="../../java/io/FilterOutputStream.html" title="class in java.io">FilterOutputStream</a></code> 
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
        </ul> <a name="write-byte:A-int-int-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>write</h4> <pre>public&nbsp;void&nbsp;write(byte[]&nbsp;b,
                  int&nbsp;off,
                  int&nbsp;len)
           throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>从指定的字节数组写入<code>len</code>个字节，从偏移<code>off</code>开始到缓冲的输出流。</span> 
           <p> <span>通常，该方法将给定数组的字节存储到此流的缓冲区中，根据需要将缓冲区刷新到底层输出流。</span> <span>然而，如果请求的长度至少与此流的缓冲区一样大，那么这个方法将刷新缓冲区并将字节直接写入底层的输出流。</span> <span>因此冗余<code>BufferedOutputStream</code>不会不必要地复制数据。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/FilterOutputStream.html#write-byte:A-int-int-">write</a></code>在 
            <code><a href="../../java/io/FilterOutputStream.html" title="class in java.io">FilterOutputStream</a></code> 
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
           <dt> 
            <span class="seeLabel">另请参见：</span> 
           </dt> 
           <dd> 
            <a href="../../java/io/FilterOutputStream.html#write-int-"><code>FilterOutputStream.write(int)</code></a> 
           </dd> 
          </dl> </li> 
        </ul> <a name="flush--"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>flush</h4> <pre>public&nbsp;void&nbsp;flush()
           throws <a href="../../java/io/IOException.html" title="class in java.io">IOException</a></pre> 
          <div class="block"> 
           <span>刷新缓冲输出流。</span> 
           <span>这将强制任何缓冲输出字节写入底层输出流。</span> 
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
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/io/FilterOutputStream.html#flush--">flush</a></code>在 
            <code><a href="../../java/io/FilterOutputStream.html" title="class in java.io">FilterOutputStream</a></code> 
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
            <a href="../../java/io/FilterOutputStream.html#out"><code>FilterOutputStream.out</code></a> 
           </dd> 
          </dl> </li> 
        </ul> </li> 
      </ul> </li> 
    </ul> 
   </div> 
  </div>
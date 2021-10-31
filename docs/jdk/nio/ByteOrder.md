<div class="contentContainer"> 
   <ul class="inheritance"> 
    <li><a href="../../java/lang/Object.html" title="class in java.lang">java.lang.Object</a></li> 
    <li> 
     <ul class="inheritance"> 
      <li>java.nio.ByteOrder</li> 
     </ul> </li> 
   </ul> 
   <div class="description"> 
    <ul class="blockList"> 
     <li class="blockList"> 
      <hr> <br> <pre>public final class <span class="typeNameLabel">ByteOrder</span>
extends <a href="../../java/lang/Object.html" title="class in java.lang">Object</a></pre> 
      <div class="block">
        字节顺序的类型安全枚举。 
      </div> 
      <dl> 
       <dt> 
        <span class="simpleTagLabel">从以下版本开始：</span> 
       </dt> 
       <dd>
         1.4 
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
           <td class="colFirst"><code>static <a href="../../java/nio/ByteOrder.html" title="class in java.nio">ByteOrder</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteOrder.html#BIG_ENDIAN">BIG_ENDIAN</a></span></code> 
            <div class="block">
              常量表示大字节字节顺序。 
            </div> </td> 
          </tr> 
          <tr class="rowColor"> 
           <td class="colFirst"><code>static <a href="../../java/nio/ByteOrder.html" title="class in java.nio">ByteOrder</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteOrder.html#LITTLE_ENDIAN">LITTLE_ENDIAN</a></span></code> 
            <div class="block">
              常量表示小端字节顺序。 
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
          <span id="t1" class="tableTab"><span><a href="javascript:show(1);">静态方法</a></span><span class="tabEnd">&nbsp;</span></span> 
          <span id="t2" class="tableTab"><span><a href="javascript:show(2);">接口方法</a></span><span class="tabEnd">&nbsp;</span></span> 
          <span id="t4" class="tableTab"><span><a href="javascript:show(8);">具体的方法</a></span><span class="tabEnd">&nbsp;</span></span> 
         </caption> 
         <tbody> 
          <tr> 
           <th class="colFirst" scope="col">Modifier and Type</th> 
           <th class="colLast" scope="col">Method and Description</th> 
          </tr> 
          <tr id="i0" class="altColor"> 
           <td class="colFirst"><code>static <a href="../../java/nio/ByteOrder.html" title="class in java.nio">ByteOrder</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteOrder.html#nativeOrder--">nativeOrder</a></span>()</code> 
            <div class="block">
              检索底层平台的本机字节顺序。 
            </div> </td> 
          </tr> 
          <tr id="i1" class="rowColor"> 
           <td class="colFirst"><code><a href="../../java/lang/String.html" title="class in java.lang">String</a></code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../java/nio/ByteOrder.html#toString--">toString</a></span>()</code> 
            <div class="block">
              构造描述此对象的字符串。 
            </div> </td> 
          </tr> 
         </tbody> 
        </table> 
        <ul class="blockList"> 
         <li class="blockList"><a name="methods.inherited.from.class.java.lang.Object"> 
           <!--   --> </a> <h3>Methods inherited from class&nbsp;java.lang.<a href="../../java/lang/Object.html" title="class in java.lang">Object</a></h3> <code><a href="../../java/lang/Object.html#clone--">clone</a>, <a href="../../java/lang/Object.html#equals-java.lang.Object-">equals</a>, <a href="../../java/lang/Object.html#finalize--">finalize</a>, <a href="../../java/lang/Object.html#getClass--">getClass</a>, <a href="../../java/lang/Object.html#hashCode--">hashCode</a>, <a href="../../java/lang/Object.html#notify--">notify</a>, <a href="../../java/lang/Object.html#notifyAll--">notifyAll</a>, <a href="../../java/lang/Object.html#wait--">wait</a>, <a href="../../java/lang/Object.html#wait-long-">wait</a>, <a href="../../java/lang/Object.html#wait-long-int-">wait</a></code></li> 
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
         <!--   --> </a> <h3>字段详细信息</h3> <a name="BIG_ENDIAN"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>BIG_ENDIAN</h4> <pre>public static final&nbsp;<a href="../../java/nio/ByteOrder.html" title="class in java.nio">ByteOrder</a> BIG_ENDIAN</pre> 
          <div class="block"> 
           <span>常量表示大字节字节顺序。</span> 
           <span>按照这个顺序，多字节值的字节从最高有效位到最低有效位排序。</span> 
          </div> </li> 
        </ul> <a name="LITTLE_ENDIAN"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>LITTLE_ENDIAN</h4> <pre>public static final&nbsp;<a href="../../java/nio/ByteOrder.html" title="class in java.nio">ByteOrder</a> LITTLE_ENDIAN</pre> 
          <div class="block"> 
           <span>常量表示小端字节顺序。</span> 
           <span>按照这个顺序，多字节值的字节从最低有效到最高有序排序。</span> 
          </div> </li> 
        </ul> </li> 
      </ul> 
      <!-- ============ METHOD DETAIL ========== --> 
      <ul class="blockList"> 
       <li class="blockList"><a name="method.detail"> 
         <!--   --> </a> <h3>方法详细信息</h3> <a name="nativeOrder--"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>nativeOrder</h4> <pre>public static&nbsp;<a href="../../java/nio/ByteOrder.html" title="class in java.nio">ByteOrder</a>&nbsp;nativeOrder()</pre> 
          <div class="block"> 
           <span>检索底层平台的本机字节顺序。</span> 
           <p> <span>定义了这种方法，使得性能敏感的Java代码可以以与硬件相同的字节顺序分配直接缓冲区。</span> <span>当使用这种缓冲区时，本地代码库通常更有效率。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             运行此Java虚拟机的硬件的本机字节顺序 
           </dd> 
          </dl> </li> 
        </ul> <a name="toString--"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>toString</h4> <pre>public&nbsp;<a href="../../java/lang/String.html" title="class in java.lang">String</a>&nbsp;toString()</pre> 
          <div class="block"> 
           <span>构造描述此对象的字符串。</span> 
           <p> <span>该方法返回<tt><code>BIG_ENDIAN</code></tt>的字符串<a href="../../java/nio/ByteOrder.html#BIG_ENDIAN">"BIG_ENDIAN"</a>和<tt><code>LITTLE_ENDIAN</code></tt>的<a href="../../java/nio/ByteOrder.html#LITTLE_ENDIAN">"LITTLE_ENDIAN"</a> 。</span> </p> 
          </div> 
          <dl> 
           <dt> 
            <span class="overrideSpecifyLabel">重写：</span> 
           </dt> 
           <dd> 
            <code><a href="../../java/lang/Object.html#toString--">toString</a></code>在 
            <code><a href="../../java/lang/Object.html" title="class in java.lang">Object</a></code> 
           </dd> 
           <dt> 
            <span class="returnLabel">结果</span> 
           </dt> 
           <dd>
             The specified string 
           </dd> 
          </dl> </li> 
        </ul> </li> 
      </ul> </li> 
    </ul> 
   </div> 
  </div>
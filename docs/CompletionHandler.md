<div class="contentContainer"> 
   <div class="description"> 
    <ul class="blockList"> 
     <li class="blockList"> 
      <dl> 
       <dt> 
        <span class="paramLabel">参数类型</span> 
       </dt> 
       <dd> 
        <code>V</code> - I / O操作的结果类型 
       </dd> 
       <dd> 
        <code>A</code> - 附加到I / O操作的对象的类型 
       </dd> 
      </dl> 
      <hr> <br> <pre>public interface <span class="typeNameLabel">CompletionHandler&lt;V,A&gt;</span></pre> 
      <div class="block"> 
       <span>用于消除异步I / O操作结果的处理程序。</span> 
       <p> <span>在此包中定义的异步通道允许指定完成处理程序以消耗异步操作的结果。</span> <span>当I / O操作成功完成时，将调用<a href="../../../java/nio/channels/CompletionHandler.html#completed-V-A-"><code>completed</code></a>方法。</span> <span>如果I / O操作失败，则调用<a href="../../../java/nio/channels/CompletionHandler.html#failed-java.lang.Throwable-A-"><code>failed</code></a>方法。</span> <span>这些方法的实现应该及时完成，以避免将调用线程调度到其他完成处理程序。</span> </p> 
      </div> 
      <dl> 
       <dt> 
        <span class="simpleTagLabel">从以下版本开始：</span> 
       </dt> 
       <dd>
         1.7 
       </dd> 
      </dl> </li> 
    </ul> 
   </div> 
   <div class="summary"> 
    <ul class="blockList"> 
     <li class="blockList"> 
      <!-- ========== METHOD SUMMARY =========== --> 
      <ul class="blockList"> 
       <li class="blockList"><a name="method.summary"> 
         <!--   --> </a> <h3>方法摘要</h3> 
        <table class="memberSummary" border="0" cellpadding="3" cellspacing="0" summary="Method Summary table, listing methods, and an explanation"> 
         <caption> 
          <span id="t0" class="activeTableTab"><span>所有方法</span><span class="tabEnd">&nbsp;</span></span> 
          <span id="t2" class="tableTab"><span><a href="javascript:show(2);">接口方法</a></span><span class="tabEnd">&nbsp;</span></span> 
          <span id="t3" class="tableTab"><span><a href="javascript:show(4);">抽象方法</a></span><span class="tabEnd">&nbsp;</span></span> 
         </caption> 
         <tbody> 
          <tr> 
           <th class="colFirst" scope="col">Modifier and Type</th> 
           <th class="colLast" scope="col">Method and Description</th> 
          </tr> 
          <tr id="i0" class="altColor"> 
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../../java/nio/channels/CompletionHandler.html#completed-V-A-">completed</a></span>(<a href="../../../java/nio/channels/CompletionHandler.html" title="type parameter in CompletionHandler">V</a>&nbsp;result, <a href="../../../java/nio/channels/CompletionHandler.html" title="type parameter in CompletionHandler">A</a>&nbsp;attachment)</code> 
            <div class="block">
              操作完成后调用。 
            </div> </td> 
          </tr> 
          <tr id="i1" class="rowColor"> 
           <td class="colFirst"><code>void</code></td> 
           <td class="colLast"><code><span class="memberNameLink"><a href="../../../java/nio/channels/CompletionHandler.html#failed-java.lang.Throwable-A-">failed</a></span>(<a href="../../../java/lang/Throwable.html" title="class in java.lang">Throwable</a>&nbsp;exc, <a href="../../../java/nio/channels/CompletionHandler.html" title="type parameter in CompletionHandler">A</a>&nbsp;attachment)</code> 
            <div class="block">
              当操作失败时调用。 
            </div> </td> 
          </tr> 
         </tbody> 
        </table> </li> 
      </ul> </li> 
    </ul> 
   </div> 
   <div class="details"> 
    <ul class="blockList"> 
     <li class="blockList"> 
      <!-- ============ METHOD DETAIL ========== --> 
      <ul class="blockList"> 
       <li class="blockList"><a name="method.detail"> 
         <!--   --> </a> <h3>方法详细信息</h3> <a name="completed-java.lang.Object-java.lang.Object-"> 
         <!--   --> </a><a name="completed-V-A-"> 
         <!--   --> </a> 
        <ul class="blockList"> 
         <li class="blockList"> <h4>completed</h4> <pre>void&nbsp;completed(<a href="../../../java/nio/channels/CompletionHandler.html" title="type parameter in CompletionHandler">V</a>&nbsp;result,
               <a href="../../../java/nio/channels/CompletionHandler.html" title="type parameter in CompletionHandler">A</a>&nbsp;attachment)</pre> 
          <div class="block">
            操作完成后调用。 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>result</code> - I / O操作的结果。 
           </dd> 
           <dd> 
            <code>attachment</code> - 启动时附加到I / O操作的对象。 
           </dd> 
          </dl> </li> 
        </ul> <a name="failed-java.lang.Throwable-java.lang.Object-"> 
         <!--   --> </a><a name="failed-java.lang.Throwable-A-"> 
         <!--   --> </a> 
        <ul class="blockListLast"> 
         <li class="blockList"> <h4>failed</h4> <pre>void&nbsp;failed(<a href="../../../java/lang/Throwable.html" title="class in java.lang">Throwable</a>&nbsp;exc,
            <a href="../../../java/nio/channels/CompletionHandler.html" title="type parameter in CompletionHandler">A</a>&nbsp;attachment)</pre> 
          <div class="block">
            当操作失败时调用。 
          </div> 
          <dl> 
           <dt> 
            <span class="paramLabel">参数</span> 
           </dt> 
           <dd> 
            <code>exc</code> - 表示I / O操作失败的原因的例外 
           </dd> 
           <dd> 
            <code>attachment</code> - 启动时附加到I / O操作的对象。 
           </dd> 
          </dl> </li> 
        </ul> </li> 
      </ul> </li> 
    </ul> 
   </div> 
  </div>
<section class="normal markdown-section">
                                
                                <p><a id="deployment"></a></p>
<h1 id="六、部署-spring-boot-应用程序">六、部署 Spring Boot 应用程序</h1>
<p>Spring Boot 的可执行 jar 是现成的，适用于大多数流行的云 PaaS（Platform-as-a-Service，平台即服务）提供商。这些提供商往往要求你「自带容器」。它们负责管理应用程序进程（而不是 Java 应用程序），因此它们需要一个中间层，使你的应用程序适应云概念中的运行进程。</p>
<p>有两个流行的云提供商 Heroku 和 Cloud Foundry 采用了 buildpack 方式。buildpack 将你部署的代码包装在启动应用程序所需的环境中。它可能是一个用于调用 <code>java</code> 的 JDK、一个内嵌 Web 服务器或一个完整的应用程序服务器。buildpack 是可插拔的，但理想情况下，你应尽可能少地进行自定义。其减少了不受控制的功能数，最大限度地减少了开发和生产环境之间的差异。</p>
<p>理想情况下，你的应用程序（比如一个 Spring Boot 可执行 jar）打包了运行所需的所有内容。</p>
<p>在本节中，我们将使用「<a href="getting-started.html">起步</a>」章节中开发的一个<a href="getting-started.html#getting-started-first-application">简单应用程序</a>作为范例，并将其运行在云中。</p>
<p><strong>待续</strong></p>
<footer class="page-footer"><span class="copyright">felord.cn</span>&nbsp; &nbsp; <a href="http://beian.miit.gov.cn/" class="copyright-links" target="_blank" rel="nofollow">豫ICP备19038867号-1</a><span class="footer-modification">File Modify:
2019-10-16 21:49:43
</span></footer>
                                
                                </section>
<section class="normal markdown-section">
                                
                                <p><strong>作者</strong></p>
<ul>
<li>Phillip Webb</li>
<li>Dave Syer</li>
<li>Josh Long</li>
<li>Stéphane Nicoll</li>
<li>Rob Winch</li>
<li>Andy Wilkinson</li>
<li>Marcel Overdijk</li>
<li>Christian Dupuis</li>
<li>Sébastien Deleuze</li>
<li>Michael Simons</li>
<li>Vedran Pavić</li>
<li>Jay Bryant</li>
<li>Madhura Bhave</li>
</ul>
<p><strong>译者</strong></p>
<ul>
<li><a href="https://github.com/oopsguy" target="_blank">Oopsguy</a></li>
</ul>
<hr>
<p><strong>2.1.5.RELEASE</strong>（前半部分为 1.5.9.RELEASE 的内容，之后会更新）</p>
<p>Copyright © 2012-2018</p>
<hr>
<p>在不对副本收取任何费用且每个副本都包含版权声明的情况下，您可以将本文档的副本分发给他人，无论是印刷形式还是电子发行形式。</p>
<p><a id="boot-documentation"></a></p>
<h1 id="i、spring-boot-文档">I、Spring Boot 文档</h1>
<p>本节将简要介绍 Spring Boot 参考文档，可以看作是本文档内容的概述。您可以以线性方式阅读此参考指南，如果您不感兴趣，可以跳过该部分。</p>
<p><a id="boot-documentation-about"></a></p>
<h2 id="1、关于文档">1、关于文档</h2>
<p>Spring Boot 参考指南提供了 <a href="https://docs.spring.io/spring-boot/docs/2.1.1.RELEASE/reference/html" target="_blank">html</a>、<a href="https://docs.spring.io/spring-boot/docs/2.1.1.RELEASE/reference/pdf/spring-boot-reference.pdf" target="_blank">pdf</a> 和 <a href="https://docs.spring.io/spring-boot/docs/2.1.1.RELEASE/reference/epub/spring-boot-reference.epub" target="_blank">epub</a> 格式的文档。最新的副本可在<a href="https://docs.spring.io/spring-boot/docs/current/reference" target="_blank">docs.spring.io/spring-boot/docs/current/reference</a> 获取。</p>
<p>在不对副本收取任何费用且每个副本都包含版权声明的情况下，您可以将本文档的副本分发给他人，无论是印刷形式还是电子发行形式。</p>
<p><a id="boot-documentation-getting-help"></a></p>
<h2 id="2、获取帮助">2、获取帮助</h2>
<p>如果您在使用 Spring Boot 时遇到了麻烦，可参考以下指南。</p>
<ul>
<li>尝试 <a href="howto.md">How-to</a>  —— 最常见问题的解决方案都在这里。</li>
<li>学习 Spring 基础  ——  Spring Boot 是建立在多个 Spring 项目之上, 请查看 <a href="https://spring.io/" target="_blank">spring.io</a> 网站以获取更多参考文档。如果您是刚刚开始使用 Spring, 请尝试其中一个<a href="https://spring.io/guides" target="_blank">指南</a>。</li>
<li>提问问题 —— 我们时刻关注着 <a href="https://stackoverflow.com/" target="_blank">stackoverflow.com</a> 上有关 <code>spring-boot</code> 标签相关的问题。</li>
<li>在 <a href="https://github.com/spring-projects/spring-boot/issues" target="_blank">github.com/spring-projects/spring-boot/issues</a> 报告 Spring Boot 的 bug。</li>
</ul>
<blockquote>
<p>Spring Boot 是全部开源的，包括文档！如果您发现文档中存在错误了，或者您想改进它们，请<a href="https://github.com/spring-projects/spring-boot/tree/v2.1.1.RELEASE" target="_blank">参与我们</a>。</p>
</blockquote>
<p><a id="boot-documentation-first-steps"></a></p>
<h2 id="3、起步">3、起步</h2>
<p>如果您是刚开始使用 Spring Boot，或者对 Spring 大体有个印象, <a href="page/getting-started.md">您可以从这里开始学习</a>!</p>
<ul>
<li><strong>从零开始</strong>： <a href="getting-started.html#getting-started-introducing-spring-boot">概述</a> | <a href="getting-started.html#getting-started-system-requirements">要求</a> | <a href="getting-started.html#getting-started-installing-spring-boot">安装</a></li>
<li><strong>教程</strong>： <a href="getting-started.html">第 1 部分</a> | <a href="getting-started.html#getting-started-first-application-code">第 2 部分</a></li>
<li><strong>运行您的例子</strong>： 第 1 部分 | 第 2 部分</li>
</ul>
<p><a id="_working_with_spring_boot"></a></p>
<h2 id="4、使用-spring-boot">4、使用 Spring Boot</h2>
<p>准备开始使用 Spring Boot 了? <a href="using-spring-boot.html">立即上手</a>。</p>
<ul>
<li><strong>构建系统</strong>：Maven | Gradle | Ant | Starter</li>
<li><strong>最佳实践</strong>：代码结构 | @Configuration | @EnableAutoConfiguration | Bean 与依赖注入</li>
<li><strong>运行代码</strong>：IDE | 打包 | Maven | Gradle</li>
<li><strong>打包应用</strong>：生产环境下的 jar</li>
<li><strong>Spring Boot CLI</strong>：使用 CLI</li>
</ul>
<p><a id="_learning_about_spring_boot_features"></a></p>
<h2 id="5、了解-spring-boot-新特性">5、了解 Spring Boot 新特性</h2>
<p>需要更多关于 Spring Boot 核心特性？<a href="boot-features.md">Spring 特性</a>!</p>
<ul>
<li><strong>核心特性</strong>：SpringApplication | 外部配置 | Profile | 日志</li>
<li><strong>Web 应用程序</strong>：MVC | 嵌入式容器</li>
<li><strong>使用数据</strong>：SQL | NO-SQL</li>
<li><strong>消息传递</strong>：概述 | JMS</li>
<li><strong>测试</strong>：概述 | Boot Applications | 实用工具</li>
<li><strong>延伸</strong>：Auto-configuration | @Conditions</li>
</ul>
<p><a id="_moving_to_production"></a></p>
<h2 id="6、生产环境">6、生产环境</h2>
<p>您如果准备将 Spring Boot 应用推送至生产环境，或许会对以下内容感兴趣。</p>
<ul>
<li><strong>管理端点</strong>：概述 | 自定义</li>
<li><strong>连接方式</strong>：HTTP | JMX | SSH</li>
<li><strong>监控</strong>：度量 | 审计 | 追踪 | 流程</li>
</ul>
<p><a id="_advanced_topics"></a></p>
<h2 id="7、高级内容">7、高级内容</h2>
<p>最后，我们为高级用户提供了几个主题。</p>
<ul>
<li><strong>部署 Spring Boot 应用</strong>：云部署 | OS 服务</li>
<li><strong>构建工具插件</strong>：Maven | Gradle</li>
<li><strong>附录</strong>：Application Properties | Auto-configuration 类 | 可执行 Jar </li>
</ul>
<footer class="page-footer"><span class="copyright">felord.cn</span>&nbsp; &nbsp; <a href="http://beian.miit.gov.cn/" class="copyright-links" target="_blank" rel="nofollow">豫ICP备19038867号-1</a><span class="footer-modification">File Modify:
2019-10-16 21:49:43
</span></footer>
                                
                                </section>
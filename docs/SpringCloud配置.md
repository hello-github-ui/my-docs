<div id="content">
<h1>Part II. Spring Cloud 配置</h1>
<div><ins class="adsbygoogle" style="display:block; text-align:center;" data-ad-layout="in-article" data-ad-format="fluid" data-ad-client="ca-pub-6108808167664152" data-ad-slot="6964403648"></ins>
<script>
(adsbygoogle = window.adsbygoogle || []).push({});
</script></div>
<div><p><strong>Edgware.SR5</strong></p>
<p>Spring Cloud Config 为分布式系统中的外部化 configuration 提供服务器和 client-side 支持。使用 Config Server，您可以在所有环境中管理 applications 的外部 properties。 client 和 server map 的概念与 Spring <code>Environment</code>和<code>PropertySource</code>抽象相同，因此它们非常适合 Spring applications，但可以与任何语言的任何 application running 一起使用。当一个 application 通过部署管道从 dev 转到 test 并进入 production 时，你可以管理这些环境之间的 configuration，并确保 applications 具有迁移时运行所需的一切。服务器存储后端的默认 implementation 使用 git，因此它可以轻松支持 configuration 环境的标签版本，并且可以访问各种用于管理内容的工具。添加备用 implementations 并使用 Spring configuration 插入它们很容易。</p>
</div>
</div>

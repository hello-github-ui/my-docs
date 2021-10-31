<section class="normal markdown-section">
                                
                                <p><a id="using-boot"></a></p>
<h1 id="三、使用-spring-boot">三、使用 Spring Boot</h1>
<p>本章节将详细介绍如何使用 Spring Boot。它覆盖了诸如构建系统、自动配置和如何运行应用等主题。我们还介绍一些 Spring Boot 最佳实践。虽然 Spring Boot 并没有什么特别（它只是另一个您可以使用的类库），但仍然有一些建议可以让您的开发工作变得更加容易。</p>
<p>如果您是刚开始使用 Spring Boot，那么在深入本部分之前，您应该先阅读<a href="#getting-started">入门部分</a>。</p>
<p><a id="using-boot-build-systems"></a></p>
<h2 id="13、构建系统">13、构建系统</h2>
<p>强烈推荐您选择一个支持<a href="#using-boot-dependency-management">依赖管理</a>的构建系统, 您可以使用它将 artifact 发布到 Maven Central 仓库。我们建议您选择 Maven 或者 Gradle。虽然可以让 Spring Boot 与其它构建系统（如 Ant）配合工作，但它们不会得到特别好的支持。</p>
<p><a id="using-boot-dependency-management"></a></p>
<h3 id="131、依赖管理">13.1、依赖管理</h3>
<p>每一次 Spring Boot 发行都提供了一个它所支持的依赖清单。实际上，您不需要为构建配置提供任何依赖的版本，因为 Spring Boot 已经帮您管理这些了。当您升级 Spring Boot 时，这些依赖也将以一致的方式进行升级。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>如果您觉得有必要，您仍然可以指定一个版本并覆盖 Spring Boot 所推荐的。</p>
</blockquote>
<p>该清单包含了全部可以与 Spring Boot 一起使用的 spring 模块以及第三方类库，可作为标准<a href="#using-boot-maven-without-a-parent">材料清单（<code>spring-boot-dependencies</code>）</a>，并且可以与 <a href="#using-boot-maven-parent-pom">Maven</a> 和 <a href="#using-boot-gradle">Gradle</a> 一起使用。</p>
<p><strong>警告</strong></p>
<blockquote>
<p>Spring Boot 的每一次发行都会基于一个 Spring Framework 版本，因此我们<strong>强烈</strong>建议您不要指定指定它的版本。</p>
</blockquote>
<p><a id="using-boot-maven"></a></p>
<h3 id="132、maven">13.2、Maven</h3>
<p>Maven 用户可以继承 <code>spring-boot-starter-parent</code> 项目以获取合适的默认值，父项目提供了以下功能：</p>
<ul>
<li>Java 1.8 作为默认编译器级别。</li>
<li>源代码使用 UTF-8 编码。</li>
<li><a href="#using-boot-dependency-management">依赖管理部分</a>继承自 <code>spring-boot-dependencies</code> 的 POM，允许您省略常见依赖的 <code><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>version</span><span class="token punctuation">&gt;</span></span></code> 标签。</li>
<li>合理的<a href="https://maven.apache.org/plugins/maven-resources-plugin/examples/filter.html" target="_blank">资源过滤</a>。</li>
<li>合适的插件配置（<a href="http://www.mojohaus.org/exec-maven-plugin/" target="_blank">exec plugin</a>、<a href="https://github.com/ktoso/maven-git-commit-id-plugin" target="_blank">Git commit ID</a>、<a href="https://maven.apache.org/plugins/maven-shade-plugin/" target="_blank">shade</a>）。</li>
<li>针对 <code>application.properties</code> 和 <code>application.yml</code> 资源的合理过滤，包括特定 profile 的文件（例如 <code>application-foo.properties</code> 和 <code>application-foo.yml</code>）</li>
</ul>
<p>注意：由于 <code>application.properties</code> 和 <code>application.yml</code> 文件接受 Spring 风格的占位符（<code>${​...}</code>），因此 Maven 过滤改为使用 <code>@..@</code> 占位符（您可以使用 Maven 的 <code>resource.delimiter</code> 属性重写它）</p>
<p><a id="using-boot-maven-parent-pom"></a></p>
<h4 id="1321、继承-starter-parent">13.2.1、继承 Starter Parent</h4>
<p>要将项目配置继承 <code>spring-boot-starter-parent</code>，只需要按以下方式设置 <code>parent</code>：</p>
<pre class="language-"><code class="lang-xml"><span class="token comment">&lt;!-- 从 Spring Boot 继承默认配置 --&gt;</span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>parent</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>groupId</span><span class="token punctuation">&gt;</span></span>org.springframework.boot<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>groupId</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>artifactId</span><span class="token punctuation">&gt;</span></span>spring-boot-starter-parent<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>artifactId</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>version</span><span class="token punctuation">&gt;</span></span>2.0.0.RELEASE<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>version</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>parent</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<p><strong>注意</strong></p>
<blockquote>
<p>您只需要在此依赖上指定 Spring Boot 的版本号。如果您要导入其它 starter，则可以放心地省略版本号。</p>
</blockquote>
<p>通过该设置，您还可以重写自己项目中的配置属性来覆盖个别依赖。例如，要升级到另一个 Spring Data 发行版本，您需要将以下内容添加到 <code>pom.xml</code> 文件中。</p>
<pre class="language-"><code class="lang-xml"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>properties</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>spring-data-releasetrain.version</span><span class="token punctuation">&gt;</span></span>Fowler-SR2<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>spring-data-releasetrain.version</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>properties</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<p><strong>提示</strong></p>
<blockquote>
<p>查看 <a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-dependencies/pom.xml" target="_blank"><code>spring-boot-dependencies</code> pom</a> 以获取受支持的属性清单。</p>
</blockquote>
<p><a id="using-boot-maven-without-a-parent"></a></p>
<h4 id="1322、不使用父-pom">13.2.2、不使用父 POM</h4>
<p>不是每个人都喜欢从 <code>spring-boot-starter-parent</code> 继承 POM。您可能需要使用自己公司标准的父 POM，或者您可能只是希望明确地声明所有 Maven 配置。</p>
<p>如果您不想使用 <code>spring-boot-starter-parent</code>，则仍然可以通过使用 <code>scope=import</code> 依赖来获得依赖管理（但不是插件管理）的好处：</p>
<pre class="language-"><code class="lang-xml"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependencyManagement</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependencies</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependency</span><span class="token punctuation">&gt;</span></span>
            <span class="token comment">&lt;!-- 从 Spring Boot 导入依赖管理 --&gt;</span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>groupId</span><span class="token punctuation">&gt;</span></span>org.springframework.boot<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>groupId</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>artifactId</span><span class="token punctuation">&gt;</span></span>spring-boot-dependencies<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>artifactId</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>version</span><span class="token punctuation">&gt;</span></span>2.0.0.RELEASE<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>version</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>type</span><span class="token punctuation">&gt;</span></span>pom<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>type</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>scope</span><span class="token punctuation">&gt;</span></span>import<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>scope</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependency</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependencies</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependencyManagement</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<p>如上所述，上述示例设置不会让您使用属性来覆盖个别依赖。要达到相同的目的，需要在 <code>spring-boot-dependencies</code> 项<strong>之前</strong>在项目的 <code>dependencyManagement</code> 中添加一项。例如，要升级到另一个 Spring Data 发行版，您可以将以下元素添加到 <code>pom.xml</code>中：</p>
<pre class="language-"><code class="lang-xml"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependencyManagement</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependencies</span><span class="token punctuation">&gt;</span></span>
        <span class="token comment">&lt;!-- 覆盖 Spring Boot 提供的 Spring Data --&gt;</span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependency</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>groupId</span><span class="token punctuation">&gt;</span></span>org.springframework.data<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>groupId</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>artifactId</span><span class="token punctuation">&gt;</span></span>spring-data-releasetrain<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>artifactId</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>version</span><span class="token punctuation">&gt;</span></span>Fowler-SR2<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>version</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>type</span><span class="token punctuation">&gt;</span></span>pom<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>type</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>scope</span><span class="token punctuation">&gt;</span></span>import<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>scope</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependency</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependency</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>groupId</span><span class="token punctuation">&gt;</span></span>org.springframework.boot<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>groupId</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>artifactId</span><span class="token punctuation">&gt;</span></span>spring-boot-dependencies<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>artifactId</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>version</span><span class="token punctuation">&gt;</span></span>2.0.0.RELEASE<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>version</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>type</span><span class="token punctuation">&gt;</span></span>pom<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>type</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>scope</span><span class="token punctuation">&gt;</span></span>import<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>scope</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependency</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependencies</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependencyManagement</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<p><strong>注意</strong></p>
<blockquote>
<p>以上示例中，我们指定了一个 <strong>BOM</strong>，但是任何的依赖类型都可以用这个方法来重写。</p>
</blockquote>
<p><a id="using-boot-maven-plugin"></a></p>
<h4 id="1323、使用-spring-boot-maven-插件">13.2.3、使用 Spring Boot Maven 插件</h4>
<p>Spring Boot 包括了一个 <a href="#build-tool-plugins-maven-plugin">Maven 插件</a>，它可以将项目打包成一个可执行 jar。如果要使用它，请将插件添加到您的 <code><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>plugins</span><span class="token punctuation">&gt;</span></span></code> 中：</p>
<pre class="language-"><code class="lang-xml"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>build</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>plugins</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>plugin</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>groupId</span><span class="token punctuation">&gt;</span></span>org.springframework.boot<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>groupId</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>artifactId</span><span class="token punctuation">&gt;</span></span>spring-boot-maven-plugin<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>artifactId</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>plugin</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>plugins</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>build</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<p><strong>注意</strong></p>
<blockquote>
<p>如果您使用了 Spring Boot starter 的父 pom，则只需要添加插件。除非您要修改父级中定义的设置，否则不需要进行配置。</p>
</blockquote>
<p><a id="using-boot-gradle"></a></p>
<h3 id="133、gradle">13.3、Gradle</h3>
<p>要了解如何使用 Spring Boot 和 Gradle，请参阅 Spring Boot 的 Gradle 插件文档：</p>
<ul>
<li>参考文档（<a href="https://docs.spring.io/spring-boot/docs/2.0.0.RELEASE/gradle-plugin/reference/html" target="_blank">HTML</a> 与 <a href="https://docs.spring.io/spring-boot/docs/2.0.0.RELEASE/gradle-plugin/reference/pdf/spring-boot-gradle-plugin-reference.pdf" target="_blank">PDF</a>）</li>
<li><a href="https://docs.spring.io/spring-boot/docs/2.0.0.RELEASE/gradle-plugin/api" target="_blank">API</a></li>
</ul>
<p><a id="using-boot-ant"></a></p>
<h3 id="134、ant">13.4、Ant</h3>
<p>可以使用 Apache Ant+Ivy 构建 Spring Boot 项目。<code>spring-boot-antlib</code> AntLib 模块也可以帮助 Ant 创建可执行 jar 文件。</p>
<p>要声明依赖，可参考以下一个典型的 <code>ivy.xml</code> 文件内容：</p>
<pre class="language-"><code class="lang-xml"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>ivy-module</span> <span class="token attr-name">version</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>2.0<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>info</span> <span class="token attr-name">organisation</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>org.springframework.boot<span class="token punctuation">"</span></span> <span class="token attr-name">module</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>spring-boot-sample-ant<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>configurations</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>conf</span> <span class="token attr-name">name</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>compile<span class="token punctuation">"</span></span> <span class="token attr-name">description</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>everything needed to compile this module<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>conf</span> <span class="token attr-name">name</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>runtime<span class="token punctuation">"</span></span> <span class="token attr-name">extends</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>compile<span class="token punctuation">"</span></span> <span class="token attr-name">description</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>everything needed to run this module<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>configurations</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependencies</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependency</span> <span class="token attr-name">org</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>org.springframework.boot<span class="token punctuation">"</span></span> <span class="token attr-name">name</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>spring-boot-starter<span class="token punctuation">"</span></span>
            <span class="token attr-name">rev</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>${spring-boot.version}<span class="token punctuation">"</span></span> <span class="token attr-name">conf</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>compile<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependencies</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>ivy-module</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<p>一个典型的 <code>build.xml</code> 大概是这样：</p>
<pre class="language-"><code class="lang-xml"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>project</span>
    <span class="token attr-name"><span class="token namespace">xmlns:</span>ivy</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>antlib:org.apache.ivy.ant<span class="token punctuation">"</span></span>
    <span class="token attr-name"><span class="token namespace">xmlns:</span>spring-boot</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>antlib:org.springframework.boot.ant<span class="token punctuation">"</span></span>
    <span class="token attr-name">name</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>myapp<span class="token punctuation">"</span></span> <span class="token attr-name">default</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>build<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>

    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>property</span> <span class="token attr-name">name</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>spring-boot.version<span class="token punctuation">"</span></span> <span class="token attr-name">value</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>2.0.0.RELEASE<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>

    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>target</span> <span class="token attr-name">name</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>resolve<span class="token punctuation">"</span></span> <span class="token attr-name">description</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>--&gt; retrieve dependencies with ivy<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span><span class="token namespace">ivy:</span>retrieve</span> <span class="token attr-name">pattern</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>lib/[conf]/[artifact]-[type]-[revision].[ext]<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>target</span><span class="token punctuation">&gt;</span></span>

    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>target</span> <span class="token attr-name">name</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>classpaths<span class="token punctuation">"</span></span> <span class="token attr-name">depends</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>resolve<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>path</span> <span class="token attr-name">id</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>compile.classpath<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>fileset</span> <span class="token attr-name">dir</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>lib/compile<span class="token punctuation">"</span></span> <span class="token attr-name">includes</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>*.jar<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>path</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>target</span><span class="token punctuation">&gt;</span></span>

    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>target</span> <span class="token attr-name">name</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>init<span class="token punctuation">"</span></span> <span class="token attr-name">depends</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>classpaths<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>mkdir</span> <span class="token attr-name">dir</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>build/classes<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>target</span><span class="token punctuation">&gt;</span></span>

    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>target</span> <span class="token attr-name">name</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>compile<span class="token punctuation">"</span></span> <span class="token attr-name">depends</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>init<span class="token punctuation">"</span></span> <span class="token attr-name">description</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>compile<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>javac</span> <span class="token attr-name">srcdir</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>src/main/java<span class="token punctuation">"</span></span> <span class="token attr-name">destdir</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>build/classes<span class="token punctuation">"</span></span> <span class="token attr-name">classpathref</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>compile.classpath<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>target</span><span class="token punctuation">&gt;</span></span>

    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>target</span> <span class="token attr-name">name</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>build<span class="token punctuation">"</span></span> <span class="token attr-name">depends</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>compile<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span><span class="token namespace">spring-boot:</span>exejar</span> <span class="token attr-name">destfile</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>build/myapp.jar<span class="token punctuation">"</span></span> <span class="token attr-name">classes</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>build/classes<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span><span class="token namespace">spring-boot:</span>lib</span><span class="token punctuation">&gt;</span></span>
                <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>fileset</span> <span class="token attr-name">dir</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>lib/runtime<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span><span class="token namespace">spring-boot:</span>lib</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span><span class="token namespace">spring-boot:</span>exejar</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>target</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>project</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<p><strong>提示</strong></p>
<blockquote>
<p>如果您不想使用 <code>spring-boot-antlib</code> 模块，请参阅第 84.10 节：<a href="https://docs.spring.io/spring-boot/docs/2.0.0.RELEASE/reference/htmlsingle/#howto-build-an-executable-archive-with-ant" target="_blank"><strong>使用 Ant 构建可执行归档文件</strong></a>，无需使用 <code>spring-boot-antlib</code>。</p>
</blockquote>
<p><a id="using-boot-starter"></a></p>
<h3 id="135、starter">13.5、Starter</h3>
<p>Starter 是一组惯例依赖描述资源，可以包含在应用中。从 starter 中，您可以获得所需的所有 Spring 和相关技术的一站式支持，无须通过示例代码和复制粘贴来获取依赖。比如，如果您要使用 Spring 和 JPA 进行数据库访问，那么只需要在项目中包含 <code>spring-boot-starter-data-jpa</code> 依赖项即可。</p>
<p>starter 包含了许多您需要用于使项目快速启动和运行，并且需要一组受支持的可传递依赖关系的依赖。</p>
<hr>
<p><strong>命名含义</strong></p>
<p>官方的所有 starter 都遵循类似的命名规则：<code>spring-boot-starter-*</code>，其中 <code>*</code> 是特定类型的应用。这个命名结构旨在帮助您找到 starter。许多 IDE 中 Maven 集成允许您按名称搜索依赖。例如，安装了 Eclipse 或者 STS 插件后，您可以简单地在 POM 编辑器中按下 <code>ctrl-space</code> 并输入 <strong>spring-boot-starter</strong> 来获取完整的列表。</p>
<p>正如<a href="#boot-features-custom-starter"><strong>创建自己的 starter</strong></a> 章节所述，第三方的 starter 命名不应该以 <code>spring-boot</code> 开头，因为它是官方 Spring Boot 构件所保留的规则。例如，有一个第三方 starter 项目叫做 <code>thirdpartyproject</code>，它通常会命名为 <code>thirdpartyproject-spring-boot-starter</code>。</p>
<hr>
<p>Spring Boot 在 <code>org.springframework.boot</code> group 下提供了以下应用 starter：</p>
<p><strong>表 13.1、Spring Boot 应用类 Starter</strong></p>
<table>
<thead>
<tr>
<th style="text-align:left">名称</th>
<th style="text-align:left">描述</th>
<th style="text-align:center">POM</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left"><code>spring-boot-starter</code></td>
<td style="text-align:left">核心 starter，包含自动配置支持、日志和 YAML</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-activemq</code></td>
<td style="text-align:left">提供 JMS 消息支持，使用 Apache ActiveMQ</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-activemq/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-amqp</code></td>
<td style="text-align:left">提供 Spring AMQP 与 Rabbit MQ 支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-amqp/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-aop</code></td>
<td style="text-align:left">提供 Spring AOP 与 AspectJ 面向切面编程支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-aop/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-artemis</code></td>
<td style="text-align:left">提供 JMS 消息服务支持，使用 Apache Artemis</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-artemis/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-batch</code></td>
<td style="text-align:left">提供 Spring Batch 支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-batch/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-cache</code></td>
<td style="text-align:left">提供 Spring Framework 缓存支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-cache/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-cloud-connectors</code></td>
<td style="text-align:left">使用 Spring Cloud Connectors 简单连接到类似 Cloud Foundry 和 Heroku 等云平台</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-cloud-connectors/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-data-cassandra</code></td>
<td style="text-align:left">提供对 Cassandra 分布式数据库和 Spring Data Cassandra 的支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-data-cassandra/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-data-cassandra-reactive</code></td>
<td style="text-align:left">提供对 Cassandra 分布式数据库和 Spring Data Cassandra Reactive 的支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-data-cassandra-reactive/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-data-couchbase</code></td>
<td style="text-align:left">提供对 Couchbase 面向文档数据库和 Spring Data Couchbase 的支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-data-couchbase/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-data-couchbase-reactive</code></td>
<td style="text-align:left">提供对 Couchbase 面向文档数据库和 Spring Data Couchbase Reactive 的支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-data-couchbase-reactive/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-data-elasticsearch</code></td>
<td style="text-align:left">提供对 Elasticseach 搜索与分析引擎和 Spring Data Elasticsearch 的支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-data-elasticsearch/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-data-jpa</code></td>
<td style="text-align:left">提供 Spring Data JPA 与 Hibernate 的支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-data-jpa/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-data-ldap</code></td>
<td style="text-align:left">提供对 Spring Data LDAP 的支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-data-ldap/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-data-mongodb</code></td>
<td style="text-align:left">提供对 MongoDB 面向文档数据库和 Spring Data MongoDB 的支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-data-mongodb/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-data-mongodb-reactive</code></td>
<td style="text-align:left">提供对 MongoDB 面向文档数据库和 Spring Data MongoDB Reactive 的支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-data-mongodb-reactive/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-data-neo4j</code></td>
<td style="text-align:left">提供对 Neo4j 图数据库与 SPring Data Neo4j 的支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-data-neo4j/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-data-redis</code></td>
<td style="text-align:left">提供对 Redis 键值数据存储、Spring Data Redis 和 Lettuce 客户端的支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-data-redis/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-data-redis-reactive</code></td>
<td style="text-align:left">提供对 Redis 键值数据存储、Spring Data Redis Reactive 和 Lettuce 客户端的支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-data-redis-reactive/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-data-rest</code></td>
<td style="text-align:left">提供使用 Spring Data REST 通过 REST 暴露 Spring Data 资源库的支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-data-rest/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-data-solr</code></td>
<td style="text-align:left">提供对 Apache Solr 搜索平台与 Spring Data Solr 的支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-data-solr/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-freemarker</code></td>
<td style="text-align:left">提供使用 Freemakrer 视图构建 MVC web 应用的支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-freemarker/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-groovy-templates</code></td>
<td style="text-align:left">提供使用 Groovy 模板视图构建 MVC web 应用的支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-groovy-templates/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-hateoas</code></td>
<td style="text-align:left">提供使用 Spring MVC 与Spring HATEOAS 构建基于超媒体的 RESTful web 应用的支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-hateoas/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-integration</code></td>
<td style="text-align:left">提供对 Spring Integration 的支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-integration/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-jdbc</code></td>
<td style="text-align:left">提供 JDBC 与 Tomcat JDBC 连接池的支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-jdbc/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-jersey</code></td>
<td style="text-align:left">提供对使用 JAX-RS 与 Jersey 构建 RESTful web 应用的支持。<a href="https://docs.spring.io/spring-boot/docs/2.0.0.RELEASE/reference/htmlsingle/#spring-boot-starter-web" target="_blank"><code>spring-boot-starter-web</code></a> 的替代方案</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-jersey/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-jooq</code></td>
<td style="text-align:left">提供对使用 JOOQ 访问 SQL 数据库的支持。<a href="https://docs.spring.io/spring-boot/docs/2.0.0.RELEASE/reference/htmlsingle/#spring-boot-starter-data-jpa" target="_blank"><code>spring-boot-starter-data-jpa</code></a> 或 <a href="https://docs.spring.io/spring-boot/docs/2.0.0.RELEASE/reference/htmlsingle/#spring-boot-starter-jdbc" target="_blank"><code>spring-boot-starter-jdbc</code></a> 的替代方案</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-jooq/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-json</code></td>
<td style="text-align:left">提供了读写 json 的支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-json/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-jta-atomikos</code></td>
<td style="text-align:left">提供 Atomikos JTA 事务支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-jta-atomikos/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-jta-bitronix</code></td>
<td style="text-align:left">提供 Bitronix JTA 事务支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-jta-bitronix/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-jta-narayana</code></td>
<td style="text-align:left">提供 Narayana JTA 支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-jta-narayana/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-mail</code></td>
<td style="text-align:left">提供使用　Java Mail 与 Spring Framework 的邮件发送支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-mail/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-mustache</code></td>
<td style="text-align:left">提供使用 Mustache 视图构建 web 应用的支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-mustache/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-quartz</code></td>
<td style="text-align:left">Quartz 支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-quartz/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-security</code></td>
<td style="text-align:left">Spring Security 支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-security/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-test</code></td>
<td style="text-align:left">提供包含了 JUnit、Hamcrest 与 Mockito 类库的 Spring Boot 单元测试支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-test/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-thymeleaf</code></td>
<td style="text-align:left">提供使用 Thymeleaf 视图构建 MVC web 应用的支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-thymeleaf/pom.xml" target="_blank">pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-validation</code></td>
<td style="text-align:left">提供 Hibernate Validator 与 Java Bean Validation 的支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-validation/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-web</code></td>
<td style="text-align:left">提供使用 Spring MVC 构建 web（包含 RESTful）应用的支持，使用 Tomcat 作为默认嵌入式容器</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-web/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-web-services</code></td>
<td style="text-align:left">Spring Web Services 支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-web-services/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-webflux</code></td>
<td style="text-align:left">提供使用 Spring Framework 的 Reactive Web 支持构建 WebFlux 应用的支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-webflux/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-websocket</code></td>
<td style="text-align:left">提供使用 Spring Framework 的 WebSocket 支持构建 WebSocket 应用的支持</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-websocket/pom.xml" target="_blank">Pom</a></td>
</tr>
</tbody>
</table>
<p>除了应用 starter，以下 starter 可用于添加<a href="https://docs.spring.io/spring-boot/docs/2.0.0.RELEASE/reference/htmlsingle/#production-ready" target="_blank">生产就绪</a>特性：</p>
<p><strong>表 13.2、Spring Boot 生产类 starter</strong></p>
<table>
<thead>
<tr>
<th style="text-align:left">名称</th>
<th style="text-align:left">描述</th>
<th style="text-align:center">POM</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left"><code>spring-boot-starter-actuator</code></td>
<td style="text-align:left">Spring Boot 的 Actuator 支持，其提供了生产就绪功能，帮助您监控和管理应用</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-actuator/pom.xml" target="_blank">Pom</a></td>
</tr>
</tbody>
</table>
<p>最后，Spring Boot 还包含以下 starter，如果您想要排除或切换特定技术，可以使用以下 starter：</p>
<p><strong>表 13.3、Spring Boot 技术类 starter</strong></p>
<table>
<thead>
<tr>
<th style="text-align:left">名称</th>
<th style="text-align:left">描述</th>
<th style="text-align:center">POM</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left"><code>spring-boot-starter-jetty</code></td>
<td style="text-align:left">使用 Jetty 作为嵌入式 servlet 容器。可代替 <a href="https://docs.spring.io/spring-boot/docs/2.0.0.RELEASE/reference/htmlsingle/#spring-boot-starter-tomcat" target="_blank"><code>spring-boot-starter-tomcat</code></a></td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-jetty/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-log4j2</code></td>
<td style="text-align:left">使用 Log4j2 作为日志组件。可代替 <a href="https://docs.spring.io/spring-boot/docs/2.0.0.RELEASE/reference/htmlsingle/#spring-boot-starter-logging" target="_blank"><code>spring-boot-starter-logging</code></a></td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-log4j2/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-logging</code></td>
<td style="text-align:left">使用 Logback 作为日志组件，此 starter 为默认的日志 starter</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-logging/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-reactor-netty</code></td>
<td style="text-align:left">使用 Reactor Netty 作为内嵌响应式 HTTP 服务器</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-reactor-netty/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-tomcat</code></td>
<td style="text-align:left">使用 Tomcat 作为嵌入式 servlet 容器，此为 <a href="https://docs.spring.io/spring-boot/docs/2.0.0.RELEASE/reference/htmlsingle/#spring-boot-starter-web" target="_blank"><code>spring-boot-starter-web</code></a> 默认的 servlet 容器 starter</td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-tomcat/pom.xml" target="_blank">Pom</a></td>
</tr>
<tr>
<td style="text-align:left"><code>spring-boot-starter-undertow</code></td>
<td style="text-align:left">使用 Undertow 作为嵌入式 servlet 容器，可代替 <a href="https://docs.spring.io/spring-boot/docs/2.0.0.RELEASE/reference/htmlsingle/#spring-boot-starter-tomcat" target="_blank"><code>spring-boot-starter-tomcat</code></a></td>
<td style="text-align:center"><a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-undertow/pom.xml" target="_blank">Pom</a></td>
</tr>
</tbody>
</table>
<p><strong>提示</strong></p>
<blockquote>
<p>有关其它社区贡献的 starter 列表，请参阅 GitHub 上的 <code>spring-boot-starters</code> 模块中的 <a href="https://github.com/spring-projects/spring-boot/tree/master/spring-boot-project/spring-boot-starters/README.adoc" target="_blank">README 文件</a>。</p>
</blockquote>
<p><a id="using-boot-structuring-your-code"></a></p>
<h2 id="14、组织代码">14、组织代码</h2>
<p>Spring Boot 不需要任何特定的代码布局，但是有一些最佳实践是很有用的。</p>
<p><a id="using-boot-using-the-default-package"></a></p>
<h3 id="141、使用-default-包">14.1、使用 default 包</h3>
<p>当一个类没有 <code>package</code> 声明时，它就被认为是在 <strong>default</strong> 包中。通常不鼓励使用 <strong>default 包</strong>，应该避免使用。对于使用 <code>@ComponentScan</code>、<code>@EntityScan</code> 或者 <code>@SpringBootApplication</code> 注解的 Spring Boot 应用，这样可能会导致特殊问题发生，因为每一个 jar 中的每一个类将会被读取到。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>我们建议您使用 Java 推荐的包命名约定，并使用域名的反向形式命名（例如  <code>com.example.project</code>）。</p>
</blockquote>
<p><a id="using-boot-locating-the-main-class"></a></p>
<h3 id="142、定位主应用类">14.2、定位主应用类</h3>
<p>我们通常建议您将主应用类放在其它类之上的根包中， <code>@EnableAutoConfiguration</code> 注解通常放在主类上，它隐式定义了某些项目的 <strong>包搜索</strong>的基准起点。例如，如果您在编写一个 JPA 应用程序，则被 <code>@EnableAutoConfiguration</code> 注解的类所属的包将被用于搜索标记有 <code>@Entity</code> 注解的类。</p>
<p>使用根包还可以允许使用没有指定 <code>basePackage</code> 属性的 <code>@ComponentScan</code> 注解。如果您的主类在根包中，也可以使用 <code>@SpringBootApplication</code> 注解。</p>
<p>以下是一个经典的包结构：</p>
<pre class="language-"><code>com
 +- example
     +- myapplication
         +- Application.java
         |
         +- customer
         |   +- Customer.java
         |   +- CustomerController.java
         |   +- CustomerService.java
         |   +- CustomerRepository.java
         |
         +- order
             +- Order.java
             +- OrderController.java
             +- OrderService.java
             +- OrderRepository.java
</code></pre><p><code>Application.java</code> 文件声明了 <code>main</code> 方法，附带了 <code>@Configuration</code> 注解。</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">package</span> <span class="token namespace">com<span class="token punctuation">.</span>example<span class="token punctuation">.</span>myapplication</span><span class="token punctuation">;</span>

<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>boot</span><span class="token punctuation">.</span><span class="token class-name">SpringApplication</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>boot<span class="token punctuation">.</span>autoconfigure</span><span class="token punctuation">.</span><span class="token class-name">EnableAutoConfiguration</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>context<span class="token punctuation">.</span>annotation</span><span class="token punctuation">.</span><span class="token class-name">ComponentScan</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>context<span class="token punctuation">.</span>annotation</span><span class="token punctuation">.</span><span class="token class-name">Configuration</span><span class="token punctuation">;</span>

<span class="token annotation punctuation">@Configuration</span>
<span class="token annotation punctuation">@EnableAutoConfiguration</span>
<span class="token annotation punctuation">@ComponentScan</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">Application</span> <span class="token punctuation">{</span>

    <span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">main</span><span class="token punctuation">(</span><span class="token class-name">String</span><span class="token punctuation">[</span><span class="token punctuation">]</span> args<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token class-name">SpringApplication</span><span class="token punctuation">.</span><span class="token function">run</span><span class="token punctuation">(</span><span class="token class-name">Application</span><span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">,</span> args<span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p><a id="using-boot-configuration-classes"></a></p>
<h2 id="15、配置类">15、配置类</h2>
<p>Spring Boot 支持基于 Java 的配置。虽然可以在 <code>SpringApplication</code> 中使用 XML 配置源，但我们通常建议主配置源为 <code>@Configuration</code> 类。通常，一个很好的选择是将定义了 <code>main</code> 方法的类作为 <code>@Configuration</code>。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>许多 Spring 的 XML 配置示例已经在 Internet 上发布了。如果可能的话，您无论如何都应该尝试着使用等效的基于 Java 的配置方式，搜索 <code>Enable*</code> 注解可以帮到您不少忙。</p>
</blockquote>
<p><a id="using-boot-importing-configuration"></a></p>
<h3 id="151、导入额外的配置类">15.1、导入额外的配置类</h3>
<p>你不需要把所有的 <code>@Configuration</code> 放在一个类中。<code>@Import</code> 注解可用于导入其他配置类。或者，您可以使用 <code>@ComponentScan</code> 自动扫描所有 Spring 组件，包括 <code>@Configuration</code> 类。</p>
<p><a id="using-boot-importing-xml-configuration"></a></p>
<h3 id="152、导入-xml-配置">15.2、导入 XML 配置</h3>
<p>如果您一定要使用基于 XML 的配置，我们建议您仍然使用 <code>@Configuration</code> 类。您可以使用 <code>@ImportResource</code> 注解来加载 XML 配置文件。</p>
<p><a id="using-boot-auto-configuration"></a></p>
<h2 id="16、自动配置">16、自动配置</h2>
<p>Spring Boot 自动配置尝试根据您添加的 jar 依赖自动配置 Spring 应用。例如，如果 classpath 下存在 HSQLDB，并且您没有手动配置任何数据库连接 bean，那么 Spring Boot 将自动配置一个内存数据库。</p>
<p>您需要通过将 <code>@EnableAutoConfiguration</code> 或者 <code>@SpringBootApplication</code> 注解添加到其中一个 <code>@Configuration</code> 类之上以启用自动配置。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>您应该仅添加一个 <code>@EnableAutoConfiguration</code> 注解。我们通常建议您将其添加到主 <code>@Configuration</code> 类中。</p>
</blockquote>
<p><a id="using-boot-replacing-auto-configuration"></a></p>
<h3 id="161、平滑替换自动配置">16.1、平滑替换自动配置</h3>
<p>自动配置是非入侵的，您可以随时定义自己的配置来代替自动配置的特定部分。例如，如果您添加了自己的 <code>DataSource</code> bean，默认的嵌入式数据库支持将不会自动配置。</p>
<p>如果您需要了解当前正在应用的自动配置，以及为什么使用，请使用 <code>--debug</code> 开关启动应用。这样做可以为核心 logger 启用调试日志，并记录到控制台。</p>
<p><a id="using-boot-disabling-specific-auto-configuration"></a></p>
<h3 id="162、禁用指定的自动配置类">16.2、禁用指定的自动配置类</h3>
<p>如果您发现在正在使用不需要的自动配置类，可以通过使用 <code>@EnableAutoConfiguration</code> 的 <code>exclude</code> 属性来禁用它们。</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>boot<span class="token punctuation">.</span>autoconfigure</span><span class="token punctuation">.</span>*<span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>boot<span class="token punctuation">.</span>autoconfigure<span class="token punctuation">.</span>jdbc</span><span class="token punctuation">.</span>*<span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>context<span class="token punctuation">.</span>annotation</span><span class="token punctuation">.</span>*<span class="token punctuation">;</span>

<span class="token annotation punctuation">@Configuration</span>
<span class="token annotation punctuation">@EnableAutoConfiguration</span><span class="token punctuation">(</span>exclude<span class="token operator">=</span><span class="token punctuation">{</span><span class="token class-name">DataSourceAutoConfiguration</span><span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">}</span><span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyConfiguration</span> <span class="token punctuation">{</span>
<span class="token punctuation">}</span>
</code></pre>
<p>如果类不在 classpath 下，您可以使用注解的 <code>excludeName</code> 属性并指定完全类名。最后，您还可以通过 <code>spring.autoconfigure.exclude</code> property 控制要排除的自动配置类列表。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>您可以同时使用注解和 property 定义排除项</p>
</blockquote>
<p><a id="using-boot-spring-beans-and-dependency-injection"></a></p>
<h2 id="17、spring-bean-与依赖注入">17、Spring Bean 与依赖注入</h2>
<p>您可以自由使用任何标准的 Spring Framework 技术来定义您的 bean 以及它们注入的依赖。我们发现使用 <code>@ComponentScan</code> 来寻找 bean 和结合 <code>@Autowired</code> 构造器注入可以很好地工作。</p>
<p>如果您按照上述的建议（将应用类放在根包中）来组织代码，则可以添加无参的 <code>@ComponentScan</code>。所有应用组件（<code>@Component</code>、<code>@Service</code>、<code>@Repository</code>、<code>@Controller</code> 等）将自动注册为 Spring Bean。</p>
<p>以下是一个 <code>@Service</code> Bean，其使用构造注入方式获取一个必需的 <code>RiskAssessor</code> bean。</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">package</span> <span class="token namespace">com<span class="token punctuation">.</span>example<span class="token punctuation">.</span>service</span><span class="token punctuation">;</span>

<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>beans<span class="token punctuation">.</span>factory<span class="token punctuation">.</span>annotation</span><span class="token punctuation">.</span><span class="token class-name">Autowired</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>stereotype</span><span class="token punctuation">.</span><span class="token class-name">Service</span><span class="token punctuation">;</span>

<span class="token annotation punctuation">@Service</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">DatabaseAccountService</span> <span class="token keyword">implements</span> <span class="token class-name">AccountService</span> <span class="token punctuation">{</span>

    <span class="token keyword">private</span> <span class="token keyword">final</span> <span class="token class-name">RiskAssessor</span> riskAssessor<span class="token punctuation">;</span>

    <span class="token annotation punctuation">@Autowired</span>
    <span class="token keyword">public</span> <span class="token class-name">DatabaseAccountService</span><span class="token punctuation">(</span><span class="token class-name">RiskAssessor</span> riskAssessor<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>riskAssessor <span class="token operator">=</span> riskAssessor<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token comment">// ...</span>

<span class="token punctuation">}</span>
</code></pre>
<p>如果 bean 中只有一个构造方法，您可以忽略掉 <code>@Autowired</code> 注解。</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Service</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">DatabaseAccountService</span> <span class="token keyword">implements</span> <span class="token class-name">AccountService</span> <span class="token punctuation">{</span>

    <span class="token keyword">private</span> <span class="token keyword">final</span> <span class="token class-name">RiskAssessor</span> riskAssessor<span class="token punctuation">;</span>

    <span class="token keyword">public</span> <span class="token class-name">DatabaseAccountService</span><span class="token punctuation">(</span><span class="token class-name">RiskAssessor</span> riskAssessor<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>riskAssessor <span class="token operator">=</span> riskAssessor<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token comment">// ...</span>

<span class="token punctuation">}</span>
</code></pre>
<p><strong>提示</strong></p>
<blockquote>
<p>请注意，构造注入允许 <code>riskAssessor</code> 字段被修饰为 <code>final</code>，这表示以后它不能被更改。</p>
</blockquote>
<p><a id="using-boot-using-springbootapplication-annotation"></a></p>
<h2 id="18、使用-springbootapplication-注解">18、使用 @SpringBootApplication 注解</h2>
<p>很多 Spring Boot 开发者总是使用 <code>@Configuration</code>、<code>@EnableAutoConfiguration</code> 和 <code>@ComponentScan</code> 注解标记在主类上。由于 这些注解经常一起使用（特别是如果您遵循上述的<a href="#using-boot-structuring-your-code">最佳实践</a>）。Spring Boot 提供了一个更方便的 <code>@SpringBootApplication</code> 注解可用来替代这个组合。</p>
<p><code>@SpringBootApplication</code> 注解相当于使用 <code>@Configuration</code>、<code>@EnableAutoConfiguration</code> 和 <code>@ComponentScan</code> 及他们的默认属性：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">package</span> <span class="token namespace">com<span class="token punctuation">.</span>example<span class="token punctuation">.</span>myapplication</span><span class="token punctuation">;</span>

<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>boot</span><span class="token punctuation">.</span><span class="token class-name">SpringApplication</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>boot<span class="token punctuation">.</span>autoconfigure</span><span class="token punctuation">.</span><span class="token class-name">SpringBootApplication</span><span class="token punctuation">;</span>

<span class="token annotation punctuation">@SpringBootApplication</span> <span class="token comment">// 相当于使用 @Configuration @EnableAutoConfiguration @ComponentScan</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">Application</span> <span class="token punctuation">{</span>

    <span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">main</span><span class="token punctuation">(</span><span class="token class-name">String</span><span class="token punctuation">[</span><span class="token punctuation">]</span> args<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token class-name">SpringApplication</span><span class="token punctuation">.</span><span class="token function">run</span><span class="token punctuation">(</span><span class="token class-name">Application</span><span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">,</span> args<span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p><strong>注意</strong></p>
<blockquote>
<p><code>@SpringBootApplication</code> 还提供了别名来自定义 <code>@EnableAutoConfiguration</code> 和 <code>@ComponentScan</code> 的属性。</p>
</blockquote>
<p><a id="using-boot-running-your-application"></a></p>
<h2 id="19、运行您的应用">19、运行您的应用</h2>
<p>将应用程序打包成 <code>jar</code> 可执行文件并使用嵌入式 HTTP 服务器的最大有点之一就是可以按照您想使用的其它方式来运行应用。调试 Spring Boot 也是很简单，您不需要任何特殊的 IDE 插件或者扩展。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>本章节仅涵盖基于　jar　的打包方式，如果您选择将应用打包为　war　文件，则应该参考您的服务器和　IDE　文档。</p>
</blockquote>
<p><a id="using-boot-running-your-application"></a></p>
<h3 id="191、使用-ide-运行">19.1、使用 IDE 运行</h3>
<p>您可以使用 IDE 运行 Spring Boot应用，就像运行一个简单的 Java 应用程序一样，但是首先您需要导入项目，导入步骤取决于您的 IDE 和构建系统。大多数 IDE 可以直接导入 Maven 项目，例如 Eclipse 用户可以从 <code>File</code> 菜单中选择 <code>Import</code> ​ → <code>Existing Maven Projects</code>。</p>
<p>如果您无法将项目直接导入到 IDE 中，则可以使用构建插件生成 IDE 元数据（metadata）。Maven 包含了 <a href="https://maven.apache.org/plugins/maven-eclipse-plugin/" target="_blank">Eclipse</a> 和 <a href="https://maven.apache.org/plugins/maven-idea-plugin/" target="_blank">IDEA</a> 的插件,Gradle 也为<a href="https://docs.gradle.org/4.2.1/userguide/userguide.html" target="_blank">各种 IDE</a> 提供了插件。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>如果您不小心运行了两次 web 应用，您将看到一个 <strong>Port already in use</strong> （端口已经被使用）错误。STS 用户可以使用 <code>Relaunch</code> 按钮运行以确保现有的任何实例都已关闭，而不是使用 Run 按钮。</p>
</blockquote>
<p><a id="using-boot-running-as-a-packaged-application"></a></p>
<h3 id="192、作为打包应用运行">19.2、作为打包应用运行</h3>
<p>如果您使用 Spring Boot Maven 或者 Gradle 插件创建可执行 jar，可以使用 <code>java -jar</code> 命令运行应用。例如：</p>
<pre class="language-"><code class="lang-bash">$ java -jar target/myapplication-0.0.1-SNAPSHOT.jar
</code></pre>
<p>也可以在运行打包应用程序时开启远程调试支持。该功能允许您将调试器附加到打包的应用中。</p>
<pre class="language-"><code class="lang-bash">$ java -Xdebug -Xrunjdwp:server<span class="token operator">=</span>y,transport<span class="token operator">=</span>dt_socket,address<span class="token operator">=</span><span class="token number">8000</span>,suspend<span class="token operator">=</span>n <span class="token punctuation">\</span>
       -jar target/myapplication-0.0.1-SNAPSHOT.jar
</code></pre>
<p><a id="using-boot-running-with-the-maven-plugin"></a></p>
<h3 id="193、使用-maven-插件">19.3、使用 Maven 插件</h3>
<p>Spring Boot Maven 插件包含一个可用于快速编译和运行应用程序的 <code>run</code> goal。应用程序以快速形式运行，就像在 IDE 中一样。以下示例展示了运行 Spring Boot 应用程序的典型 Maven 命令：</p>
<pre class="language-"><code class="lang-bash">$ mvn spring-boot:run
</code></pre>
<p>您可能还想使用 <code>MAVEN_OPTS</code> 操作系统环境变量，如下例所示：</p>
<pre class="language-"><code class="lang-bash">$ <span class="token builtin class-name">export</span> <span class="token assign-left variable">MAVEN_OPTS</span><span class="token operator">=</span>-Xmx1024m
</code></pre>
<p><a id="using-boot-running-with-the-gradle-plugin"></a></p>
<h3 id="194、使用-gradle-插件">19.4、使用 Gradle 插件</h3>
<p>Spring Boot Gradle 插件包含一个 <code>bootRun</code> 任务，可用于以快速形式运行应用程序。每当应用 <code>org.springframework.boot</code> 和 java 插件时都会添加 <code>bootRun</code> 任务：</p>
<pre class="language-"><code class="lang-bash">$ gradle bootRun
</code></pre>
<p>您可能还想使用 <code>JAVA_OPTS</code> 操作系统环境变量：</p>
<pre class="language-"><code class="lang-bash">$ <span class="token builtin class-name">export</span> <span class="token assign-left variable">JAVA_OPTS</span><span class="token operator">=</span>-Xmx1024m
</code></pre>
<p><a id="using-boot-hot-swapping"></a></p>
<h3 id="195、热交换">19.5、热交换</h3>
<p>由于 Spring Boot 应用程序只是普通的 Java 应用程序，因此 JVM 热插拔是可以开箱即用。JVM 热插拔在可替换字节码方面有所限制。想要更完整的解决方案，可以使用 <a href="https://zeroturnaround.com/software/jrebel/" target="_blank">JRebel</a>。</p>
<p><code>spring-boot-devtools</code> 模块包含了对快速重新启动应用程序的支持。有关详细信息，请参阅本章后面的<a href="#using-boot-devtools">第 20 章：开发人员工具</a>部分以及<a href="#howto-hotswapping">热插拔的 How-to 部分</a>。</p>
<p><a id="using-boot-devtools"></a></p>
<h2 id="20、开发者工具">20、开发者工具</h2>
<p>Spring Boot 包含了一套工具，可以使应用开发体验更加愉快。<code>spring-boot-devtools</code> 模块可包含在任何项目中，以提供额外的开发时（development-time）功能。要启用 devtools 支持，只需要将模块依赖添加到您的构建配置中即可：</p>
<p><strong>Maven</strong></p>
<pre class="language-"><code class="lang-xml"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependencies</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependency</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>groupId</span><span class="token punctuation">&gt;</span></span>org.springframework.boot<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>groupId</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>artifactId</span><span class="token punctuation">&gt;</span></span>spring-boot-devtools<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>artifactId</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>optional</span><span class="token punctuation">&gt;</span></span>true<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>optional</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependency</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependencies</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<p><strong>Gradle</strong></p>
<pre class="language-"><code class="lang-xml">dependencies {
    compile("org.springframework.boot:spring-boot-devtools")
}
</code></pre>
<p><strong>注意</strong></p>
<blockquote>
<p>当运行完全打包的应用时，开发者工具将会自动禁用。如果您的应用使用了 <code>java -jar</code> 方式或者特殊的类加载器启动，那么它会被认为是一个<strong>生产级别应用</strong>。将 Maven 的依赖标记为可选或者在 Gradle 中使用 <code>compileOnly</code> 是防止您的项目被其他模块使用时 devtools 被应用到其它模块的最佳方法。</p>
</blockquote>
<p><strong>提示</strong></p>
<blockquote>
<p>重新打包的归档默认情况下不包含 devtools。如果要使用<a href="#using-boot-devtools-remote">某些远程 devtools 功能</a>, 你需要禁用 <code>excludeDevtools</code> 构建属性以把 devtools 包含进来。该属性支持 Maven 和 Gradle 插件。</p>
</blockquote>
<p><a id="using-boot-devtools-property-defaults"></a></p>
<h3 id="201、property-默认值">20.1、Property 默认值</h3>
<p>Spring Boot 所支持的一些库使用了缓存来提高性能。例如，<a href="#boot-features-spring-mvc-template-engines">模板引擎</a>将缓存编译后的模板，以避免重复解析模板文件。此外，Spring MVC 可以在服务静态资源时添加 HTTP 缓存头。</p>
<p>虽然缓存在生产中非常有用，但它在开发过程可能会产生相反的效果，让您不能及时看到刚才在应用中作出的更改。因此，<code>spring-boot-devtools</code> 将默认禁用这些缓存选项。</p>
<p>一般是在 <code>application.properties</code> 文件中设置缓存选项。例如，Thymeleaf 提供了 <code>spring.thymeleaf.cache</code> 属性。您不需要手动设置这些属性，<code>spring-boot-devtools</code> 会自动应用合适的开发时（development-time）配置。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>有关应用属性的完整列表，请参阅 <a href="https://github.com/spring-projects/spring-boot/tree/v2.0.1.RELEASE/spring-boot-project/spring-boot-devtools/src/main/java/org/springframework/boot/devtools/env/DevToolsPropertyDefaultsPostProcessor.java" target="_blank">DevToolsPropertyDefaultsPostProcessor</a>。</p>
</blockquote>
<p><a id="using-boot-devtools-restart"></a></p>
<h3 id="202、自动重启">20.2、自动重启</h3>
<p>使用 <code>spring-boot-devtools</code> 的应用在 classpath 下的文件发生更改时会自动重启。这对于使用 IDE 工作而言可能是一个非常棒的功能，因为它为代码变更提供了非常块的反馈环。默认情况下，将监视 classpath 指向的所有文件夹。请注意，某些资源（如静态资源和视图模板）<a href="using-boot-devtools-restart-exclude">不需要重启应用</a>。</p>
<hr>
<p><strong>触发重启</strong></p>
<p>当 DevTools 监视 classpath 资源时，触发重启的唯一方式是更新 classpath。使 classpath 更新的方式取决于您使用的 IDE。在 Eclipse 中，保存修改的文件将更新 classpath，从而触发重启。在 IntelliJ IDEA 中，构建项目（<code>Build -&gt; Make Project</code>) 将产生相同的效果。</p>
<hr>
<p><strong>注意</strong></p>
<blockquote>
<p>只要 forking 被开启，您可以使用受支持的构建工具（如 Maven 或 Gradle）来启用应用，因为 DevTools 需要隔离应用类加载器才能正常运行。默认情况下，当在 classpath 下检测到 DevTools 时，Gradle 和 Maven 会这么做。</p>
</blockquote>
<p><strong>提示</strong></p>
<blockquote>
<p>自动重启功能与 LiveReload（实时重载）一起使用效果更棒。<a href="#using-boot-devtools-livereload">阅读 LiveReload 章节</a>以获取更多信息。如果您使用 JRebel，自动重启将会被禁用，以支持动态类重载，但其他 devtools 功能（如 LiveReload 和 property 覆盖）仍然可以使用。</p>
</blockquote>
<p><strong>注意</strong></p>
<blockquote>
<p>DevTools 依赖于应用上下文的关闭钩子，以在重启期间关闭自己。如果禁用了关闭钩子（<code>SpringApplication.setRegisterShutdownHook(false)</code>），它将不能正常工作。</p>
</blockquote>
<p><strong>注意</strong></p>
<blockquote>
<p>当 classpath 下的内容发生更改，决定是否触发重启时，DevTools 会自动忽略名为 <code>spring-boot</code>、<code>spring-boot-devtools</code>、<code>spring-boot-autoconfigure</code>、<code>spring-boot-actuator</code> 和 <code>spring-boot-starter</code> 的项目。</p>
</blockquote>
<p><strong>注意</strong></p>
<blockquote>
<p>DevTools 需要自定义 <code>ApplicationContext</code> 使用到的 <code>ResourceLoader</code>。如果您的应用已经提供了一个，它将被包装起来，因为不支持在 <code>ApplicationContext</code> 上直接覆盖 <code>getResource</code> 方法。</p>
</blockquote>
<hr>
<p><strong>重启（Restart）与重载（Reload）</strong></p>
<p>Spring Boot 通过使用两个类加载器来提供了重启技术。不改变的类（例如，第三方 jar）被加载到 <strong>base</strong> 类加载器中。经常处于开发状态的类被加载到 <strong>restart</strong> 类加载器中。当应用重启时，<strong>restart</strong> 类加载器将被丢弃，并重新创建一个新的。这种方式意味着应用重启比<strong>冷启动</strong>要快得多，因为省去 <strong>base</strong> 类加载器的处理步骤，并且可以直接使用。</p>
<p>如果您觉得重启还不够快，或者遇到类加载问题，您可以考虑如 ZeroTurnaround 的 <a href="https://zeroturnaround.com/software/jrebel/" target="_blank">JRebel</a> 等工具。他们是通过在加载类时重写类来加快重新加载。</p>
<hr>
<p><a id="using-boot-devtools-restart-logging-condition-delta"></a></p>
<h4 id="2021、条件评估变更日志">20.2.1、条件评估变更日志</h4>
<p>默认情况下，每次应用重启时，都会记录显示条件评估增量的报告。该报告展示了在您进行更改（如添加或删除 bean 以及设置配置属性）时对应用自动配置所作出的更改。</p>
<p>要禁用报告的日志记录，请设置以下属性：</p>
<pre class="language-"><code class="lang-properties"><span class="token attr-name">spring.devtools.restart.log-condition-evaluation-delta</span><span class="token punctuation">=</span><span class="token attr-value">false</span>
</code></pre>
<p><a id="using-boot-devtools-restart-exclude"></a></p>
<h4 id="2022、排除资源">20.2.2、排除资源</h4>
<p>某些资源在更改时不一定需要触发重启。例如，Thymeleaf 模板可以实时编辑。默认情况下，更改 <code>/META-INF/maven</code>、<code>/META-INF/resources</code>、<code>/resources</code>、<code>/static</code>、<code>/public</code> 或者 <code>/templates</code> 不会触发重启，但会触发 <a href="#using-boot-devtools-livereload">LiveReload</a>。如果您想自定义排除项，可以使用 <code>spring.devtools.restart.exclude</code> 属性。例如，仅排除 <code>/static</code> 和 <code>/public</code>，您可以设置以下内容：</p>
<pre class="language-"><code class="lang-properties"><span class="token attr-name">spring.devtools.restart.exclude</span><span class="token punctuation">=</span><span class="token attr-value">static/**,public/**</span>
</code></pre>
<p><strong>提示</strong></p>
<blockquote>
<p>如果要保留这些默认值并<strong>添加</strong>其他排除项 ，请改用 <code>spring.devtools.restart.additional-exclude</code> 属性。</p>
</blockquote>
<p><a id="using-boot-devtools-restart-additional-paths"></a></p>
<h4 id="2023、监视附加路径">20.2.3、监视附加路径</h4>
<p>如果您想在对不在 classpath 下的文件进行修改时重启或重载应用，请使用 <code>spring.devtools.restart.additional-paths</code> 属性来配置监视其他路径的更改情况。您可以使用<a href="#using-boot-devtools-restart-exclude">上述</a>的 <code>spring.devtools.restart.exclude</code> 属性来控制附加路径下的文件被修改时是否触发重启或只是 <a href="#using-boot-devtools-livereload">LiveReload</a>。</p>
<p><a id="using-boot-devtools-restart-disable"></a></p>
<h4 id="2024、禁用重启">20.2.4、禁用重启</h4>
<p>您如果不想使用重启功能，可以使用 <code>spring.devtools.restart.enabled</code> 属性来禁用它。一般情况下，您可以在 <code>application.properties</code> 中设置此属性（重启类加载器仍将被初始化，但不会监视文件更改）。</p>
<p>如果您需要<strong>完全</strong>禁用重启支持（例如，可能它不适用于某些类库），您需要在调用 <code>SpringApplication.run(​...)</code> 之前将 System 属性 <code>spring.devtools.restart.enabled System</code> 设置为 <code>false</code>。例如：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">main</span><span class="token punctuation">(</span><span class="token class-name">String</span><span class="token punctuation">[</span><span class="token punctuation">]</span> args<span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token class-name">System</span><span class="token punctuation">.</span><span class="token function">setProperty</span><span class="token punctuation">(</span><span class="token string">"spring.devtools.restart.enabled"</span><span class="token punctuation">,</span> <span class="token string">"false"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token class-name">SpringApplication</span><span class="token punctuation">.</span><span class="token function">run</span><span class="token punctuation">(</span><span class="token class-name">MyApp</span><span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">,</span> args<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>
<p><a id="using-boot-devtools-restart-triggerfile"></a></p>
<h4 id="2025、使用触发文件">20.2.5、使用触发文件</h4>
<p>如果您使用 IDE 进行开发，并且时时刻刻在编译更改的文件，或许您只是希望在特定的时间内触发重启。为此，您可以使用<strong>触发文件</strong>，这是一个特殊文件，您想要触发重启检查时，必须修改它。更改文件只会触发检查，只有在 Devtools 检查到它需要做某些操作时才会触发重启，可以手动更新触发文件，也可以通过 IDE 插件更新。</p>
<p>要使用触发文件，请设置 <code>spring.devtools.restart.trigger-file</code> 属性指向触发文件的路径。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>您也许想将 <code>spring.devtools.restart.trigger-file</code> 设置成一个<a href="#using-boot-devtools-globalsettings">全局配置</a>，以使得所有的项目都能应用此方式。</p>
</blockquote>
<p><a id="using-boot-devtools-customizing-classload"></a></p>
<h4 id="2026、自定义重启类加载器">20.2.6、自定义重启类加载器</h4>
<p>正如之前的<a href="#using-spring-boot-restart-vs-reload">重启和重载</a>部分所述，重启功能是通过使用两个类加载器来实现的。对于大多数应用而言，这种方式很好，然而，有时可能会导致类加载出现问题。</p>
<p>默认情况下，IDE 中任何打开的项目将使用 <strong>restart</strong> 类加载器加载，任何常规的 <code>.jar</code> 文件将使用 <strong>base</strong> 类加载器加载。您如果开发的是多模块项目，而不是每一个模块都导入到 IDE 中，则可能需要自定义。为此，您可以创建一个 <code>META-INF/spring-devtools.properties</code> 文件。</p>
<p><code>spring-devtools.properties</code> 文件可以包含以 <code>restart.exclude.</code> 和 <code>restart.include.</code> 为前缀的属性。<code>include</code> 元素是加载到 <strong>restart</strong> 类加载器的项，<code>exclude</code> 元素是加载到 <strong>base</strong> 类加载器的项。属性值是一个应用到 classpath 的正则表达式。例如：</p>
<pre class="language-"><code class="lang-properties"><span class="token attr-name">restart.exclude.companycommonlibs</span><span class="token punctuation">=</span><span class="token attr-value">/mycorp-common-[\\w-]+\.jar</span>
<span class="token attr-name">restart.include.projectcommon</span><span class="token punctuation">=</span><span class="token attr-value">/mycorp-myproj-[\\w-]+\.jar</span>
</code></pre>
<p><strong>注意</strong></p>
<blockquote>
<p>所有属性键名必须是唯一的。只要有一个属性以 <code>restart.include.</code> 或 <code>restart.exclude.</code> 开头，它将会被考虑。</p>
</blockquote>
<p><strong>提示</strong></p>
<blockquote>
<p>classpath 下的所有 <code>META-INF/spring-devtools.properties</code> 文件将被加载，您可以将它们打包进工程或者类库中为项目所用。</p>
</blockquote>
<p><a id="using-boot-devtools-known-restart-limitations"></a></p>
<h4 id="2027、已知限制">20.2.7、已知限制</h4>
<p>重新启动功能对使用标准 <code>ObjectInputStream</code> 反序列化的对象无效。您如果需要反序列化数据，可能需要使用 Spring 的 <code>ConfigurableObjectInputStream</code> 配合 <code>Thread.currentThread().getContextClassLoader()</code>。</p>
<p>遗憾的是，一些第三方类库在没有考虑上下文类加载器的情况下使用了反序列化。您如果遇到此问题，需要向原作者提交修复请求。</p>
<p><a id="using-boot-devtools-livereload"></a></p>
<h3 id="203、livereload">20.3、LiveReload</h3>
<p><code>spring-boot-devtools</code> 模块包括了一个内嵌 LiveReload 服务器，它可在资源发生更改时触发浏览器刷新。您可以从 <a href="http://livereload.com/extensions/" target="_blank">livereload.com</a> 上免费获取 Chrome、Firefox 和 Safari 平台下对应的 LiveReload 浏览器扩展程序。</p>
<p>如果您不想在应用运行时启动 LiveReload 服务器，可以将 <code>spring.devtools.livereload.enabled</code> 属性设置为 <code>false</code>。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>您一次只能运行一个 LiveReload 服务器。在启动应用之前，请确保没有其他 LiveReload 服务器正在运行。如果在 IDE 中启动了多个应用，那么只有第一个应用的 LiveReload 生效。</p>
</blockquote>
<p><a id="using-boot-devtools-globalsettings"></a></p>
<h3 id="204、全局设置">20.4、全局设置</h3>
<p>您可以通过在 <code>$HOME</code> 目录中添加名为 <code>.spring-boot-devtools.properties</code> 的文件来配置全局 devtools 设置（请注意，文件名以“.”开头）。在此文件中添加的任何属性将应用到您的计算机上<strong>所有</strong>使用了 devtools 的 Spring Boot 应用。例如，始终使用<a href="#using-boot-devtools-restart-triggerfile">触发文件</a>来配置重启功能，您可以添加以下内容：</p>
<p><strong>~/.spring-boot-devtools.properties.</strong></p>
<pre class="language-"><code>spring.devtools.reload.trigger-file=.reloadtrigger
</code></pre><p><strong>注意</strong></p>
<blockquote>
<p>在 <code>.spring-boot-devtools.properties</code> 中激活的 profile 将不会影响指定 profile 的配置文件的加载。</p>
</blockquote>
<p><a id="using-boot-devtools-remote"></a></p>
<h3 id="205、远程应用">20.5、远程应用</h3>
<p>Spring Boot 开发者工具不局限于本地开发。在远程运行应用时也可以使用许多功能。远程支持功能是可选的，如果要启用，您需要确保在重新打包归档文件时包含 <code>devtools</code>：</p>
<pre class="language-"><code class="lang-xml"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>build</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>plugins</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>plugin</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>groupId</span><span class="token punctuation">&gt;</span></span>org.springframework.boot<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>groupId</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>artifactId</span><span class="token punctuation">&gt;</span></span>spring-boot-maven-plugin<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>artifactId</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>configuration</span><span class="token punctuation">&gt;</span></span>
                <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>excludeDevtools</span><span class="token punctuation">&gt;</span></span>false<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>excludeDevtools</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>configuration</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>plugin</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>plugins</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>build</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<p>之后您需要设置一个 <code>spring.devtools.remote.secret</code> 属性，如下：</p>
<pre class="language-"><code>spring.devtools.remote.secret=mysecret
</code></pre><p><strong>警告</strong></p>
<blockquote>
<p>在远程应用上启用 <code>spring-boot-devtools</code> 是存在安全隐患的。您不应该在生产部署时启用它。</p>
</blockquote>
<p>远程 devtools 支持分为两部分：接受请求连接的服务器端端点和在 IDE 中运行的客户端应用。当设置了 <code>spring.devtools.remote.secret</code> 属性时，服务器组件将自动启用。客户端组件必须手启用。</p>
<p><a id="_running_the_remote_client_application"></a></p>
<h4 id="2051、运行远程客户端应用">20.5.1、运行远程客户端应用</h4>
<p>假设远程客户端应用运行在 IDE 中。您需要在与要连接的远程项目相同的 classpath 下运行 <code>org.springframework.boot.devtools.RemoteSpringApplication</code>。把要连接的远程 URL 作为必须参数传入。</p>
<p>例如，如果您使用的是 Eclipse 或 STS，并且有一个名为 <code>my-app</code> 的项目已部署到了 Cloud Foundry，则可以执行以下操作：</p>
<ul>
<li>在 <code>Run</code> 菜单中选择选择 <code>Run Configurations...</code>​。</li>
<li>创建一个新的 <code>Java Application</code> launch configuration。</li>
<li>浏览 <code>my-app</code> 项目。</li>
<li>使用 <code>org.springframework.boot.devtools.RemoteSpringApplication</code> 作为主类。</li>
<li>将 <code>https://myapp.cfapps.io</code> 作为 <code>程序参数</code> （或者任何远程 URL）传入。</li>
</ul>
<p>运行的远程客户端将如下所示：</p>
<pre class="language-"><code>  .   ____          _                                              __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _          ___               _      \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` |        | _ \___ _ __  ___| |_ ___ \ \ \ \
 \\/  ___)| |_)| | | | | || (_| []::::::[]   / -_) '  \/ _ \  _/ -_) ) ) ) )
  '  |____| .__|_| |_|_| |_\__, |        |_|_\___|_|_|_\___/\__\___|/ / / /
 =========|_|==============|___/===================================/_/_/_/
 :: Spring Boot Remote :: 2.1.1.RELEASE

2015-06-10 18:25:06.632  INFO 14938 --- [           main] o.s.b.devtools.RemoteSpringApplication   : Starting RemoteSpringApplication on pwmbp with PID 14938 (/Users/pwebb/projects/spring-boot/code/spring-boot-devtools/target/classes started by pwebb in /Users/pwebb/projects/spring-boot/code/spring-boot-samples/spring-boot-sample-devtools)
2015-06-10 18:25:06.671  INFO 14938 --- [           main] s.c.a.AnnotationConfigApplicationContext : Refreshing org.springframework.context.annotation.AnnotationConfigApplicationContext@2a17b7b6: startup date [Wed Jun 10 18:25:06 PDT 2015]; root of context hierarchy
2015-06-10 18:25:07.043  WARN 14938 --- [           main] o.s.b.d.r.c.RemoteClientConfiguration    : The connection to http://localhost:8080 is insecure. You should use a URL starting with 'https://'.
2015-06-10 18:25:07.074  INFO 14938 --- [           main] o.s.b.d.a.OptionalLiveReloadServer       : LiveReload server is running on port 35729
2015-06-10 18:25:07.130  INFO 14938 --- [           main] o.s.b.devtools.RemoteSpringApplication   : Started RemoteSpringApplication in 0.74 seconds (JVM running for 1.105)
</code></pre><p><strong>注意</strong></p>
<blockquote>
<p>由于远程客户端与实际应用使用的是同一个 classpath，因此可以直接读取应用的 properties。这也是 <code>spring.devtools.remote.secret</code> 属性为什么能被读取和传递给服务器进行身份验证的原因。</p>
</blockquote>
<p><strong>提示</strong></p>
<blockquote>
<p>建议使用 <code>https://</code> 作为连接协议，以便加密传输并防止密码被拦截。</p>
</blockquote>
<p><strong>提示</strong></p>
<blockquote>
<p>如果您需要通过代理来访问远程应用，请配置 <code>spring.devtools.remote.proxy.host</code> 和 <code>spring.devtools.remote.proxy.port</code> 属性。</p>
</blockquote>
<p><a id="using-boot-devtools-remote-update"></a></p>
<h4 id="2052、远程更新">20.5.2、远程更新</h4>
<p>远程客户端使用了与<a href="#using-boot-devtools-restart">本地重启</a>相同的方式来监控应用 classpath 下发生的更改。任何更新的资源将被推送到远程应用和触发重启（<strong>如果要求</strong>）。如果您正在迭代一个使用了本地没有的云服务的功能，这可能会非常有用。通常远程更新和重启比完全重新构建和部署的周期要快得多。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>文件只有在远程客户端运行时才被监控。如果您在启动远程客户端之前更改了文件，文件将不会被推送到远程服务器。</p>
</blockquote>
<p><a id="using-boot-packaging-for-production"></a></p>
<h2 id="21、打包生产应用">21、打包生产应用</h2>
<p>可执行 jar 可用于生产部署，它们是独立（self-contained，独立、自包含）的，同样也适合云部署。</p>
<p>针对其他<strong>生产就绪</strong>功能，比如健康、审计和 REST 或者 JMX 端点度量，可以添加 <code>spring-boot-actuator</code>。有关这方面的详细信息，请参见 <a href="#production-ready">第五部分：“Spring Boot Actuator：生产就绪功能”</a>。</p>
<p><a id="using-boot-whats-next"></a></p>
<h2 id="22、下一步">22、下一步</h2>
<p>您现在应该知道如何使用 Spring Boot 以及应该遵循哪些最佳实践。接下来您可以深入地了解 <a href="#boot-features">Spring Boot 功能</a>，或者您也可以跳过下一部分直接阅读<a href="h#production-ready">“生产就绪功能”</a>方面的内容。</p>
<footer class="page-footer"><span class="copyright">felord.cn</span>&nbsp; &nbsp; <a href="http://beian.miit.gov.cn/" class="copyright-links" target="_blank" rel="nofollow">豫ICP备19038867号-1</a><span class="footer-modification">File Modify:
2019-10-16 21:49:43
</span></footer>
                                
                                </section>
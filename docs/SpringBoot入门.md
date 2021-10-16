<section class="normal markdown-section">
                                
                                <p><a id="getting-started"></a></p>
<h1 id="二、入门">二、入门</h1>
<p>如果您是刚开始使用 Spring Boot，或者对 Spring 有点印象，那么这部分内容是为您准备的！在这里我们将给出基本的“是什么？”、“怎么做？”、“为什么？”这类问题的答案。这是一份友好的 Spring Boot 简介和安装说明。当我们在讨论一些核心原理之后，我们将构建第一个 Spring Boot 应用。</p>
<p><a id="getting-started-introducing-spring-boot"></a></p>
<h2 id="8、spring-boot-简介">8、Spring Boot 简介</h2>
<p>使用 Spring Boot 可以很容易地创建出能直接运行的独立的、生产级别的基于 Spring 的应用。我们对 Spring 平台和第三方类库有自己的考虑，因此您可以从最基本的开始。大多数 Spring Boot 应用只需要很少的 Spring 配置。</p>
<p>您可以使用 Spring Boot 来创建一个可以使用 <code>java -jar</code> 命令来运行或者基于传统的 war 包部署的应用程序。我们还提供了一个用于运行 spring scripts 的命令行工具。</p>
<p>我们的主要目标是：</p>
<ul>
<li>为所有 Spring Boot 开发提供一个更快、更全面的入门体验。</li>
<li>坚持自我虽好，但当需求出现偏离，您需要能迅速摆脱出来。</li>
<li>提供大量非功能性特性相关项目（例如：内嵌服务器、安全、指标、健康检查、外部配置)。</li>
<li>绝对没有代码生成，也不要求 XML 配置。</li>
</ul>
<p><a id="getting-started-system-requirements"></a></p>
<h2 id="9、系统要求">9、系统要求</h2>
<p>默认情况下，Spring Boot 1.5.4.RELEASE 需要 <a href="https://www.java.com/" target="_blank">Java 7</a> 和 Spring Framework 4.3.9.RELEASE 或者更高版本。您可以通过其他配置使 Java 6 配合 Spring Boot。更多详细信息，请参见<a href="howto.md#howto-use-java-6">第 84.11节，“如何使用 Java 6”</a>。Spring Boot 为 Maven（3.2+），和 Gradle 2（2.9 或者更高版本）和 Gradle 3 提供了显式构建支持。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>虽然您可以在 Java 6 或者 Java 7 上使用 Spring Boot，但我们还是强烈推荐您使用 Java 8。</p>
</blockquote>
<p><a id="_servlet_containers"></a></p>
<h3 id="91、servlet-容器">9.1、Servlet 容器</h3>
<p>支持以下嵌入式容器开箱即用：</p>
<table>
<thead>
<tr>
<th style="text-align:left">名称</th>
<th style="text-align:left">Servlet 版本</th>
<th style="text-align:left">Java 版本</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left">Tomcat 8</td>
<td style="text-align:left">3.1</td>
<td style="text-align:left">Java 7+</td>
</tr>
<tr>
<td style="text-align:left">Tomcat 7</td>
<td style="text-align:left">3.0</td>
<td style="text-align:left">Java 6+</td>
</tr>
<tr>
<td style="text-align:left">Jetty 9.3</td>
<td style="text-align:left">3.1</td>
<td style="text-align:left">Java 8+</td>
</tr>
<tr>
<td style="text-align:left">Jetty 9.2</td>
<td style="text-align:left">3.1</td>
<td style="text-align:left">Java 7+</td>
</tr>
<tr>
<td style="text-align:left">Jetty 8</td>
<td style="text-align:left">3.0</td>
<td style="text-align:left">Java 6+</td>
</tr>
<tr>
<td style="text-align:left">Undertow 1.3</td>
<td style="text-align:left">3.1</td>
<td style="text-align:left">Java 7+</td>
</tr>
</tbody>
</table>
<p>您可以将 Spring Boot 应用部署到任何一个 Servlet 3.0+ 兼容容器中。</p>
<p><a id="getting-started-installing-spring-boot"></a></p>
<h2 id="10、安装-spring-boot">10、安装 Spring Boot</h2>
<p>Spring Boot 可以与<strong>经典</strong>的 Java 开发工具一起使用或者作为命令行工具安装。无论如何，您将需要 <a href="https://www.java.com/" target="_blank">Java SDK 1.6</a> 或者更高版本。在开始之前您应该检查 Java 的安装情况：</p>
<pre class="language-"><code class="lang-bash">$ java -version
</code></pre>
<p>如果您是 Java 开发新手，或者您只想尝试使用 Spring Boot，您可能需要首先尝试使用 <a href="#getting-started-installing-the-cli">Spring Boot CLI</a>，否则请阅读经典的安装说明。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>虽然 Spring Boot 支持 Java 1.6，但是如果可以，您应该考虑使用最新的 Java 版本。</p>
</blockquote>
<p><a id="getting-started-installation-instructions-for-java"></a></p>
<h3 id="101、针对-java-开发人员的安装说明">10.1、针对 Java 开发人员的安装说明</h3>
<p>您可以跟使用任何标准 Java 库的方式一样使用 Spring Boot。只需要在 classpath 下包含相应的 <code>spring-boot-*.jar</code> 文件即可。Spring Boot 不需要任何专用的工具来集成，因此您可以使用任何 IDE 或者文本编辑器，并且 Spring Boot 应用也没什么特殊之处，因此可以像任何其它 Java 程序一样运行和调试。</p>
<p>虽然您可以复制 Spring Boot 的 jar 文件，但我们通常建议您使用支持依赖管理的构建工具（比如 Maven 或者 Gradle）。</p>
<p><a id="getting-started-maven-installation"></a></p>
<h3 id="1011、使用-maven-安装">10.1.1、使用 Maven 安装</h3>
<p>Spring Boot 兼容 Apache Maven 3.2 或更高版本。如果您还没有安装 Maven，可以到 <a href="https://maven.apache.org/" target="_blank">maven.apache.org</a> 上按照说明进行操作。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>在许多操作系统上，可以通过软件包管理器来安装 Maven。如果您是 OSX Homebrew 用户，请尝试使用 <code>brew install maven</code>。Ubuntu 用户可以运行 <code>sudo apt-get install maven</code>。</p>
</blockquote>
<p>Spring Boot 依赖使用到了 <code>org.springframework.boot</code> <code>groupId</code>。通常，您的 Maven POM 文件将从 <code>spring-boot-starter-parent</code> 项目继承，并声明一个或多个 <a href="using-boot-starter.md">Starter</a> 依赖。Spring Boot 还提供了一个可选的 <a href="#build-tool-plugins-maven-plugin">Maven 插件</a>来创建可执行 jar。</p>
<p>这是一个典型的 <code>pom.xml</code> 文件：</p>
<pre class="language-"><code class="lang-xml"><span class="token prolog">&lt;?xml version="1.0" encoding="UTF-8"?&gt;</span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>project</span> <span class="token attr-name">xmlns</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>http://maven.apache.org/POM/4.0.0<span class="token punctuation">"</span></span> <span class="token attr-name"><span class="token namespace">xmlns:</span>xsi</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>http://www.w3.org/2001/XMLSchema-instance<span class="token punctuation">"</span></span>
    <span class="token attr-name"><span class="token namespace">xsi:</span>schemaLocation</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>modelVersion</span><span class="token punctuation">&gt;</span></span>4.0.0<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>modelVersion</span><span class="token punctuation">&gt;</span></span>

    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>groupId</span><span class="token punctuation">&gt;</span></span>com.example<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>groupId</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>artifactId</span><span class="token punctuation">&gt;</span></span>myproject<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>artifactId</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>version</span><span class="token punctuation">&gt;</span></span>0.0.1-SNAPSHOT<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>version</span><span class="token punctuation">&gt;</span></span>

    <span class="token comment">&lt;!-- Inherit defaults from Spring Boot --&gt;</span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>parent</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>groupId</span><span class="token punctuation">&gt;</span></span>org.springframework.boot<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>groupId</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>artifactId</span><span class="token punctuation">&gt;</span></span>spring-boot-starter-parent<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>artifactId</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>version</span><span class="token punctuation">&gt;</span></span>1.5.9.RELEASE<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>version</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>parent</span><span class="token punctuation">&gt;</span></span>

    <span class="token comment">&lt;!-- Add typical dependencies for a web application --&gt;</span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependencies</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependency</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>groupId</span><span class="token punctuation">&gt;</span></span>org.springframework.boot<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>groupId</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>artifactId</span><span class="token punctuation">&gt;</span></span>spring-boot-starter-web<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>artifactId</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependency</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependencies</span><span class="token punctuation">&gt;</span></span>

    <span class="token comment">&lt;!-- Package as an executable jar --&gt;</span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>build</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>plugins</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>plugin</span><span class="token punctuation">&gt;</span></span>
                <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>groupId</span><span class="token punctuation">&gt;</span></span>org.springframework.boot<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>groupId</span><span class="token punctuation">&gt;</span></span>
                <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>artifactId</span><span class="token punctuation">&gt;</span></span>spring-boot-maven-plugin<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>artifactId</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>plugin</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>plugins</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>build</span><span class="token punctuation">&gt;</span></span>

<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>project</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<p><strong>提示</strong></p>
<blockquote>
<p><code>spring-boot-starter-parent</code> 是一个使用 Spring Boot 的好方式，但它并不是任何时候都适用。有时您可能需要继承不同的父 POM，或者您不喜欢我们的默认配置。请参见<a href="#using-boot-maven-without-a-parent">第 13.2.2 节, “使用不带父 POM 的 Spring Boot”</a> 作为的替代方案，其使用了 <code>import</code> Scope。</p>
</blockquote>
<p><a id="getting-started-gradle-installation"></a></p>
<h3 id="1012、使用-gradle-安装">10.1.2、使用 Gradle 安装</h3>
<p>Spring Boot 兼容 Gradle 2 (2.9 或者更高版本)和 Gradle 3。如果您还没有安装 Gradle，您可以按照 <a href="http://www.gradle.org/" target="_blank">www.gradle.org/</a> 上的说明进行操作。</p>
<p>Spring Boot 依赖 <code>org.springframework.boot</code> <code>group</code>。通常，您的项目将声明一个或者多个 <a href="using-boot-starter.md">Starter</a> 的依赖。Spring Boot 提供了一个有用的 <a href="#build-tool-plugins-gradle-plugin">Gradle 插件</a>，可用于简化依赖声明和创建可执行 jar 文件。</p>
<p><strong>Gradle Wrapper</strong></p>
<blockquote>
<p>当您许需要构建项目时，Gradle Wrapper 提供了一个用于获取 Gradle 的好方法。它是由小脚本和库组成，您在提交的同时，您的代码将引导构建流程。更多详细信息，请参阅 <a href="https://docs.gradle.org/2.14.1/userguide/gradle_wrapper.html" target="_blank">docs.gradle.org/2.14.1/userguide/gradle_wrapper.html</a>。</p>
</blockquote>
<p>这是一个典型的 <code>build.gradle</code> 文件：</p>
<pre class="language-"><code class="lang-groovy">plugins <span class="token punctuation">{</span>
    id <span class="token string">'org.springframework.boot'</span> version <span class="token string">'1.5.4.RELEASE'</span>
    id <span class="token string">'java'</span>
<span class="token punctuation">}</span>


jar <span class="token punctuation">{</span>
    baseName <span class="token operator">=</span> <span class="token string">'myproject'</span>
    version <span class="token operator">=</span>  <span class="token string">'0.0.1-SNAPSHOT'</span>
<span class="token punctuation">}</span>

repositories <span class="token punctuation">{</span>
    <span class="token function">jcenter</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
<span class="token punctuation">}</span>

dependencies <span class="token punctuation">{</span>
    <span class="token function">compile</span><span class="token punctuation">(</span><span class="token string">"org.springframework.boot:spring-boot-starter-web"</span><span class="token punctuation">)</span>
    <span class="token function">testCompile</span><span class="token punctuation">(</span><span class="token string">"org.springframework.boot:spring-boot-starter-test"</span><span class="token punctuation">)</span>
<span class="token punctuation">}</span>
</code></pre>
<p><a id="getting-started-installing-the-cli"></a></p>
<h3 id="102、安装-spring-boot-cli">10.2、安装 Spring Boot CLI</h3>
<p>Spring Boot CLI 是一个命令行工具，如果您想使用 Spring 快速搭建原型，可以选择它。它允许您运行 <a href="http://groovy.codehaus.org/" target="_blank">Groovy</a> 脚本，这意味着您有可以有类 Java 语法且没有太多样板的代码。</p>
<p>您不需要使用 CLI 来配合 Spring Boot，但它确实是一个入门 Spring 应用的最快方式。</p>
<p><a id="getting-started-manual-cli-installation"></a></p>
<h4 id="1021、手动安装">10.2.1、手动安装</h4>
<p>您可以从 Spring 软件仓库中下载 Spring CLI 发行版：</p>
<ul>
<li><a href="https://repo.spring.io/release/org/springframework/boot/spring-boot-cli/1.5.9.RELEASE/spring-boot-cli-1.5.9.RELEASE-bin.zip" target="_blank">spring-boot-cli-1.5.9.RELEASE-bin.zip</a></li>
<li><a href="https://repo.spring.io/release/org/springframework/boot/spring-boot-cli/1.5.9.RELEASE/spring-boot-cli-1.5.9.RELEASE-bin.tar.gz" target="_blank">spring-boot-cli-1.5.9.RELEASE-bin.tar.gz</a></li>
</ul>
<p><a href="https://repo.spring.io/snapshot/org/springframework/boot/spring-boot-cli/" target="_blank">最新的快照发行版</a>也是可用的。</p>
<p>下载之后，请按照解压缩归档文件中的 <a href="https://raw.github.com/spring-projects/spring-boot/v1.5.9.RELEASE/spring-boot-cli/src/main/content/INSTALL.txt" target="_blank">INSTALL.txt</a> 说明进行操作。总之：在 <code>.zip</code> 文件的 <code>bin/</code> 目录中有一个 spring 脚本（在 Windows 下为 <code>spring.bat</code>），或者也可以使用 <code>java -jar</code> 配合 <code>.jar</code> 文件（该脚本可以帮助您确保 classpath 设置正确）。</p>
<p><a id="getting-started-sdkman-cli-installation"></a></p>
<h4 id="1022、使用-sdkman-安装">10.2.2、使用 SDKMAN! 安装</h4>
<p>SDKMAN!（软件开发包管理器）用于管理二进制 SDK 的多个版本，包括 Groovy 和 Spring Boot CLI。从 <a href="http://sdkman.io/" target="_blank">sdkman.io</a> 获取 SDKMAN! 并安装 Spring Boot：</p>
<pre class="language-"><code class="lang-bash">$ sdk <span class="token function">install</span> springboot
$ spring --version
Spring Boot v1.5.9.RELEASE
</code></pre>
<p>如果您正在为 CLI 开发功能，并希望够能轻松地访问刚创建的版本，请参照以下指令。</p>
<pre class="language-"><code class="lang-bash">$ sdk <span class="token function">install</span> springboot dev /path/to/spring-boot/spring-boot-cli/target/spring-boot-cli-1.5.9.RELEASE-bin/spring-1.5.9.RELEASE/
$ sdk default springboot dev
$ spring --version
Spring CLI v1.5.9.RELEASE
</code></pre>
<p>以上操作将会安装一个名为 <code>dev</code> 的 <code>spring</code> 的本地实例。它指向您的目标构建位置，因此每次重新构建 Spring Boot 时，spring 都是最新的。</p>
<p>您可以这样做来相关信息：</p>
<pre class="language-"><code class="lang-bash">$ sdk <span class="token function">ls</span> springboot

<span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span>
Available Springboot Versions
<span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span>
<span class="token operator">&gt;</span> + dev
* <span class="token number">1.5</span>.9.RELEASE

<span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span>
+ - <span class="token builtin class-name">local</span> version
* - installed
<span class="token operator">&gt;</span> - currently <span class="token keyword">in</span> use
<span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span><span class="token operator">==</span>
</code></pre>
<p><a id="getting-started-homebrew-cli-installation"></a></p>
<h4 id="1023、使用-osx-homebrew-安装">10.2.3、使用 OSX Homebrew 安装</h4>
<p>如果您是在 Mac 上工作并且使用了 <a href="http://brew.sh/" target="_blank">Homebrew</a>，您安装 Spring Boot CLI 需要做的:</p>
<pre class="language-"><code class="lang-bash">$ brew tap pivotal/tap
$ brew <span class="token function">install</span> springboot
</code></pre>
<p>Homebrew 将会把 spring 安装在 <code>/usr/local/bin</code>。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>如果您没有看到执行流程, 您安装的 brew 可能已经过期了。执行 <code>brew update</code> 并重新尝试。</p>
</blockquote>
<p><a id="getting-started-macports-cli-installation"></a></p>
<h4 id="1024、使用-macports-安装">10.2.4、使用 MacPorts 安装</h4>
<p>如果您是在 Mac 上工作并且使用了 <a href="https://www.macports.org/" target="_blank">MacPorts</a>，您安装 Spring Boot CLI 所需要做的:</p>
<pre class="language-"><code class="lang-bash">$ <span class="token function">sudo</span> port <span class="token function">install</span> spring-boot-cli
</code></pre>
<p><a id="getting-started-cli-command-line-completion"></a></p>
<h4 id="1025、命令行完成">10.2.5、命令行完成</h4>
<p>Spring Boot CLI 为 <a href="https://en.wikipedia.org/wiki/Bash_%28Unix_shell%29" target="_blank">BASH</a> 和 <a href="https://en.wikipedia.org/wiki/Zsh" target="_blank">zsh</a> 提供了命令完成脚本。您可以在任何 shell 中执行此脚本 (也称为 <code>spring</code>），或将其放在您个人或系统范围的 bash 中完成初始化。在 Debian 系统上，系统范围的脚本位于 <code>/shell-completion/bash</code> 中，当新的 shell 启动时，该目录中的所有脚本将被执行。要手动运行脚本, 例如：您已经使用 SDKMAN! 安装了</p>
<pre class="language-"><code class="lang-bash">$ <span class="token builtin class-name">.</span> ~/.sdkman/candidates/springboot/current/shell-completion/bash/spring
$ spring <span class="token operator">&lt;</span>HIT TAB HERE<span class="token operator">&gt;</span>
  grab  <span class="token builtin class-name">help</span>  jar  run  <span class="token builtin class-name">test</span>  version
</code></pre>
<p><strong>注意</strong></p>
<blockquote>
<p>如果您使用 Homebrew 或者 MacPorts 安装了 Spring Boot CLI，则命令行完成脚本将自动注册到您的 shell 中。</p>
</blockquote>
<p><a id="getting-started-cli-example"></a></p>
<h3 id="1026、快速入门-spring-cli-示例">10.2.6、快速入门 Spring CLI 示例</h3>
<p>这是一个非常简单的 web 应用程序，可以用于测试您的安装情况。创建一个名为 <code>app.groovy</code> 的文件：</p>
<pre class="language-"><code class="lang-groovy"><span class="token annotation punctuation">@RestController</span>
<span class="token keyword">class</span> <span class="token class-name">ThisWillActuallyRun</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@RequestMapping</span><span class="token punctuation">(</span><span class="token string">"/"</span><span class="token punctuation">)</span>
    String <span class="token function">home</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token string">"Hello World!"</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>之后在 shell 中运行它：</p>
<pre class="language-"><code class="lang-bash">$ spring run app.groovy
</code></pre>
<p><strong>注意</strong></p>
<blockquote>
<p>第一次运行应用的时候需要一些时间，因为需要下载依赖。后续运行将会更快。</p>
</blockquote>
<p>在您喜欢的浏览器中打开 localhost:8080，您应该会看到以下输出：</p>
<pre class="language-"><code>Hello World!
</code></pre><p><a id="getting-started-upgrading-from-an-earlier-version"></a></p>
<h2 id="103、升级旧版-spring-boot">10.3、升级旧版 Spring Boot</h2>
<p>如果您想从旧版的 Spring Boot 升级到此版本，请查看<a href="https://github.com/spring-projects/spring-boot/wiki" target="_blank">项目 wiki</a> 上托管的 <strong>release notes（发行说明）</strong>。您将会找到升级说明以及每个版本的<strong>新特性和注意事项</strong>列表。</p>
<p>要升级现有的 CLI，请使用相应的包管理器命令（例如 <code>brew upgrade</code>） 或者, 如果您手动安装了 CLI，请按照<a href="#getting-started-manual-cli-installation">标准说明</a>，记得更新您的 <code>PATH</code> 环境变量以删除任何旧的引用。</p>
<p><a id="getting-started-first-application"></a></p>
<h2 id="11、开发第一个-spring-boot-应用">11、开发第一个 Spring Boot 应用</h2>
<p>让我们使用 Java 开发一个简单的 <strong>Hello World!</strong> web 应用程序，以便体现 Spring Boot 的一些关键特性。我们将使用 Maven 构建该项目，因为大多数 IDE 都支持它。</p>
<p><strong>提示</strong></p>
<blockquote>
<p><a href="https://spring.io/" target="_blank">spring.io</a> 网站上有许多使用 Spring Boot 的<strong>入门指南</strong>，如果您正在寻找具体问题的解决方案，可先从上面寻找。您可以到 <a href="https://start.spring.io/" target="_blank">start.spring.io</a> 使用依赖搜索功能选择 <code>web</code> starter 来快速完成以下步骤。它将自动生成一个新的项目结构，以便您可以<a href="#getting-started-first-application-code">立即开始编码</a>。<a href="https://github.com/spring-io/initializr" target="_blank">查看文档了解更多信息</a>。</p>
</blockquote>
<p>在开始之前，打开终端检查您是否安装了符合要求的 Java 版本和 Maven 版本。</p>
<pre class="language-"><code class="lang-bash">$ java -version
java version <span class="token string">"1.7.0_51"</span>
Java<span class="token punctuation">(</span>TM<span class="token punctuation">)</span> SE Runtime Environment <span class="token punctuation">(</span>build <span class="token number">1.7</span>.0_51-b13<span class="token punctuation">)</span>
Java HotSpot<span class="token punctuation">(</span>TM<span class="token punctuation">)</span> <span class="token number">64</span>-Bit Server VM <span class="token punctuation">(</span>build <span class="token number">24.51</span>-b03, mixed mode<span class="token punctuation">)</span>
</code></pre>
<pre class="language-"><code class="lang-bash">$ mvn -v
Apache Maven <span class="token number">3.2</span>.3 <span class="token punctuation">(</span>33f8c3e1027c3ddde99d3cdebad2656a31e8fdf4<span class="token punctuation">;</span> <span class="token number">2014</span>-08-11T13:58:10-07:00<span class="token punctuation">)</span>
Maven home: /Users/user/tools/apache-maven-3.1.1
Java version: <span class="token number">1.7</span>.0_51, vendor: Oracle Corporation
</code></pre>
<p><strong>提示</strong></p>
<blockquote>
<p>此示例需要在您自己的文件夹中创建，后续的步骤说明假设您已经创建了这个文件夹，它是您的<strong>当前目录</strong>。</p>
</blockquote>
<p><a id="getting-started-first-application-pom"></a></p>
<h3 id="111-创建-pom">11.1 创建 POM</h3>
<p>我们先要创建一个 Maven <code>pom.xml</code> 文件。<code>pom.xml</code> 是用于构建项目的<strong>配方</strong>。打开您最喜欢的编辑器并添加一下内容：</p>
<pre class="language-"><code class="lang-xml"><span class="token prolog">&lt;?xml version="1.0" encoding="UTF-8"?&gt;</span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>project</span> <span class="token attr-name">xmlns</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>http://maven.apache.org/POM/4.0.0<span class="token punctuation">"</span></span> <span class="token attr-name"><span class="token namespace">xmlns:</span>xsi</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>http://www.w3.org/2001/XMLSchema-instance<span class="token punctuation">"</span></span>
    <span class="token attr-name"><span class="token namespace">xsi:</span>schemaLocation</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>modelVersion</span><span class="token punctuation">&gt;</span></span>4.0.0<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>modelVersion</span><span class="token punctuation">&gt;</span></span>

    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>groupId</span><span class="token punctuation">&gt;</span></span>com.example<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>groupId</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>artifactId</span><span class="token punctuation">&gt;</span></span>myproject<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>artifactId</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>version</span><span class="token punctuation">&gt;</span></span>0.0.1-SNAPSHOT<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>version</span><span class="token punctuation">&gt;</span></span>

    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>parent</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>groupId</span><span class="token punctuation">&gt;</span></span>org.springframework.boot<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>groupId</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>artifactId</span><span class="token punctuation">&gt;</span></span>spring-boot-starter-parent<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>artifactId</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>version</span><span class="token punctuation">&gt;</span></span>1.5.9.RELEASE<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>version</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>parent</span><span class="token punctuation">&gt;</span></span>

    <span class="token comment">&lt;!-- Additional lines to be added here... --&gt;</span>

<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>project</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<p>这应该会给您生成一个工作版本，您可以通过运行 <code>mvn package</code> 来测试它（此时您可以忽略 <strong>jar will be empty - no content was marked for inclusion!</strong> 警告信息)。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>此时，您可以将项目导入 IDE（大部分的现代 Java IDE 都内置 Maven 支持）。为了简单起见，我们将继续在这个例子中使用纯文本编辑器。</p>
</blockquote>
<p><a id="getting-started-first-application-dependencies"></a></p>
<h3 id="112、添加-classpath-依赖">11.2、添加 Classpath 依赖</h3>
<p>Spring Boot 提供了多个 “Starter”，可以让您方便地将 jar 添加到 classpath 下。我们的示例应用已经在 POM 的 <code>parent</code> 部分使用了 <code>spring-boot-starter-parent</code>。<code>spring-boot-starter-parent</code> 是一个特殊 Starter，它提供了有用的 Maven 默认配置。此外它还提供了<a href="#using-boot-dependency-management">依赖管理</a>功能，您可以忽略这些依赖的版本（<code>version</code>）标签。</p>
<p>其他 Starter 只提供在开发特定应用时可能需要到的依赖。由于我们正在开发一个 web 应用，因此我们将添加一个 <code>spring-boot-starter-web</code> 依赖 ， 但在此之前，让我们来看看目前拥有的。</p>
<pre class="language-"><code>mvn dependency:tree

[INFO] com.example:myproject:jar:0.0.1-SNAPSHOT
</code></pre><p><code>mvn dependency:tree</code> 命令以树的形式打印项目的依赖。您可以看到 <code>spring-boot-starter-parent</code> 本身不提供依赖。我们可以在 <code>parent</code> 下方立即编辑 <code>pom.xml</code> 并添加 <code>spring-boot-starter-web</code> 依赖：</p>
<pre class="language-"><code class="lang-xml"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependencies</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependency</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>groupId</span><span class="token punctuation">&gt;</span></span>org.springframework.boot<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>groupId</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>artifactId</span><span class="token punctuation">&gt;</span></span>spring-boot-starter-web<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>artifactId</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependency</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependencies</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<p>如果您再次运行 <code>mvn dependency:tree</code>，将会看到现在有许多附加的依赖，包括了 Tomcat web 服务器和 Spring Boot 本身。</p>
<p><a id="getting-started-first-application-code"></a></p>
<h3 id="113、编码">11.3、编码</h3>
<p>要完成我们的应用，我们需要创建一个 Java 文件。默认情况下，Maven 将从 <code>src/main/java</code> 目录下编译源代码，因此您需要创建该文件夹结构，之后添加一个名为 <code>src/main/java/Example.java</code> 的文件：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>boot</span><span class="token punctuation">.</span>*<span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>boot<span class="token punctuation">.</span>autoconfigure</span><span class="token punctuation">.</span>*<span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>web<span class="token punctuation">.</span>bind<span class="token punctuation">.</span>annotation</span><span class="token punctuation">.</span>*<span class="token punctuation">;</span>

<span class="token annotation punctuation">@RestController</span>
<span class="token annotation punctuation">@EnableAutoConfiguration</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">Example</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@RequestMapping</span><span class="token punctuation">(</span><span class="token string">"/"</span><span class="token punctuation">)</span>
    <span class="token class-name">String</span> <span class="token function">home</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> <span class="token string">"Hello World!"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">main</span><span class="token punctuation">(</span><span class="token class-name">String</span><span class="token punctuation">[</span><span class="token punctuation">]</span> args<span class="token punctuation">)</span> <span class="token keyword">throws</span> <span class="token class-name">Exception</span> <span class="token punctuation">{</span>
        <span class="token class-name">SpringApplication</span><span class="token punctuation">.</span><span class="token function">run</span><span class="token punctuation">(</span><span class="token class-name">Example</span><span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">,</span> args<span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>虽然没有多少代码，但它仍然做了很多事情。让我们看看里面重要的部分。</p>
<p><a id="getting-started-first-application-annotations"></a></p>
<h4 id="1131、restcontroller-与-requestmapping-注解">11.3.1、@RestController 与 @RequestMapping 注解</h4>
<p><code>Example</code> 类中的第一个注解是 <code>@RestController</code>，该注解被称作 stereotype 注解。它能为代码阅读者提供一些提示，对于 Spring 而言，这个类具有特殊作用。在本示例中，我们的类是一个 web <code>@Controller</code>，因此 Spring 在处理传入的 web 请求时会考虑它。</p>
<p><code>@RequestMapping</code> 注解提供了 <strong>routing</strong>（路由）信息。它告诉 Spring，任何具有路径为 <code>/</code> 的 HTTP 请求都应映射到 <code>home</code> 方法。<code>@RestController</code> 注解告知 Spring 渲染结果字符串直接返回给调用者。</p>
<p><strong>提示</strong></p>
<blockquote>
<p><code>@RestController</code> 和 <code>@RequestMapping</code> 是 Spring MVC 注解（它们不是 Spring Boot 特有的）。有关更多详细信息，请参阅 Spring 参考文档中的 <a href="https://docs.spring.io/spring/docs/5.0.4.RELEASE/spring-framework-reference/web.html#mvc" target="_blank">MVC 章节</a></p>
</blockquote>
<p><a id="getting-started-first-application-auto-configuration"></a></p>
<h4 id="1132、enableautoconfiguration-注解">11.3.2、@EnableAutoConfiguration 注解</h4>
<p>第二个类级别注解是 <code>@EnableAutoConfiguration</code>。此注解告知 Spring Boot 根据您添加的 jar 依赖来“猜测”您想如何配置 Spring 并进行自动配置，由于 <code>spring-boot-starter-web</code> 添加了 Tomcat 和 Spring MVC，auto-configuration（自动配置）将假定您要开发 web 应用并相应设置了 Spring。</p>
<blockquote>
<p><strong>Starter 与自动配置</strong> <br> Auto-configuration 被设计与 Starter 配合使用，但这两个概念并不是直接相关的。您可以自由选择 starter 之外的 jar 依赖，Spring Boot 仍然会自动配置您的应用程序。</p>
</blockquote>
<p><a id="getting-started-first-application-main-method"></a></p>
<h4 id="1133、main-方法">11.3.3、main 方法</h4>
<p>应用的最后一部分是 <code>main</code> 方法。这只是一个标准方法，其遵循 Java 规范中定义的应用程序入口点。我们的 main 方法通过调用 <code>run</code> 来委托 Spring Boot 的 <code>SpringApplication</code> 类，<code>SpringApplication</code> 类将引导我们的应用，启动 Spring，然后启动自动配置的 Tomcat web 服务器。我们需要将 <code>Example.class</code>  作为一个参数传递给 <code>run</code> 方法来告知 <code>SpringApplication</code>，它是 Spring 主组件。同时还传递 <code>args</code> 数组以暴露所有命令行参数。</p>
<p><a id="getting-started-first-application-run"></a></p>
<h3 id="114、运行示例">11.4、运行示例</h3>
<p>此时，我们的应用应该是可以工作了。由于您使用了 <code>spring-boot-starter-parent</code> POM，因此您可以使用 <code>run</code> 来启动应用程序。在根目录下输入 <code>mvn spring-boot:run</code> 以启动应用：</p>
<pre class="language-"><code>$ mvn spring-boot:run

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::  (v2.0.0.RELEASE)
....... . . .
....... . . . (log output here)
....... . . .
........ Started Example in 2.222 seconds (JVM running for 6.514)
</code></pre><p>如果您用浏览器打开了 <a href="http://localhost:8080/" target="_blank"><code>localhost:8080</code></a>，您应该会看到以下输出：</p>
<pre class="language-"><code>Hello World!
</code></pre><p>要平滑退出程序，请按 <code>ctrl+c</code>。</p>
<p><a id="getting-started-first-application-executable-jar"></a></p>
<h3 id="115、创建可执行-jar">11.5、创建可执行 jar</h3>
<p>我们通过创建一个完全自包含（self-contained）的可执行 jar 文件完成了示例。该 jar 文件可以在生产环境中运行。可执行 jar（有时又称为 <code>fat jars</code>）是包含了编译后的类以及代码运行时所需要相关的 jar 依赖的归档文件。</p>
<hr>
<p><strong>可执行 jar 与 Java</strong></p>
<p>Java 不提供任何标准方式来加载嵌套的 jar 文件（比如本身包含在 jar 中的 jar 文件）。如果您想分发自包含的应用，这可能是个问题。</p>
<p>为了解决此问题，许多开发人员使用了 <strong>uber</strong> jar，uber jar 从所有应用的依赖中打包所有的类到一个归档中。这种方法的问题在于，您很难看出应用程序实际上使用到了哪些库。如果在多个 jar 中使用了相同的文件名（但内容不同），这也可能产生问题。</p>
<p>Spring Boot 采用了<a href="#executable-jar">不同方方式</a>，可以直接对 jar 进行嵌套。 </p>
<hr>
<p>要创建可执行 jar，我们需要将 <code>spring-boot-maven-plugin</code> 添加到 <code>pom.xml</code> 文件中。在 <code>dependencies</code> 下方插入以下配置：</p>
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
<p><code>spring-boot-starter-parent</code> POM 包含了 <code><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>executions</span><span class="token punctuation">&gt;</span></span></code> 配置，用于绑定 <code>repackage</code> 。如果您没有使用父 POM，您需要自己声明此配置。有关详细的信息，请参阅<a href="https://docs.spring.io/spring-boot/docs/2.0.0.RELEASE/maven-plugin/usage.html" target="_blank">插件文档</a>。</p>
</blockquote>
<p>保存 <code>pom.xml</code> 并在命令行中运行 <code>mvn package</code>：</p>
<pre class="language-"><code>$ mvn package

[INFO] Scanning for projects...
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] Building myproject 0.0.1-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] .... ..
[INFO] --- maven-jar-plugin:2.4:jar (default-jar) @ myproject ---
[INFO] Building jar: /Users/developer/example/spring-boot-example/target/myproject-0.0.1-SNAPSHOT.jar
[INFO]
[INFO] --- spring-boot-maven-plugin:2.0.0.RELEASE:repackage (default) @ myproject ---
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
</code></pre><p>如果您浏览 <code>target</code> 目录，您应该会看到 <code>myproject-0.0.1-SNAPSHOT.jar</code>。该文件的大小大约为 10 MB。如果您想要查看里面的内容，可以使用 <code>jar tvf</code>：</p>
<pre class="language-"><code class="lang-bash">$ jar tvf target/myproject-0.0.1-SNAPSHOT.jar
</code></pre>
<p>您应该还会在 <code>target</code> 目录中看到一个名为 <code>myproject-0.0.1-SNAPSHOT.jar.original</code> 的较小文件。这是在 Spring Boot 重新打包之前由 Maven 所创建的原始 jar 文件。</p>
<p>使用 <code>java -jar</code> 命令运行该应用：</p>
<pre class="language-"><code>$ java -jar target/myproject-0.0.1-SNAPSHOT.jar

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::  (v2.0.0.RELEASE)
....... . . .
....... . . . (log output here)
....... . . .
........ Started Example in 2.536 seconds (JVM running for 2.864)
</code></pre><p>跟之前一样, 要平滑退出应用，请按 <code>ctrl-c</code>。</p>
<p><a id="getting-started-whats-next"></a></p>
<h2 id="12、下一步">12、下一步</h2>
<p>希望您在本章节学到了一些 Spring Boot 的基础知识，并且开始编写自己的应用。如果您是一名面向任务（task-oriented）的开发人员，您可能想跳过 <a href="https://spring.io/" target="_blank">spring.io</a> 而直接阅读一些能解决<strong>如何使用 Spring 来解决？</strong> 这类问题的<a href="https://spring.io/guides/" target="_blank">入门指南</a>，此外我们还有 Spring Boot 专门的 <a href="#howto">How-to</a> 参考文档。</p>
<p><a href="https://github.com/spring-projects/spring-boot" target="_blank">Spring Boot 仓库</a>还有很多您可以运行的<a href="https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-samples" target="_blank">示例</a>。示例与其余部分的代码是独立的（也就是说，您不需要构建其他的代码来运行或使用示例）。</p>
<p>接下来阅读的是第三部：<a href="#using-boot">使用 Spring Boot</a>。如果您真的感到厌倦了，可以跳过该部分直接阅读 <a href="#boot-features">Spring Boot 特性</a>。</p>
<footer class="page-footer"><span class="copyright">felord.cn</span>&nbsp; &nbsp; <a href="http://beian.miit.gov.cn/" class="copyright-links" target="_blank" rel="nofollow">豫ICP备19038867号-1</a><span class="footer-modification">File Modify:
2019-10-16 21:49:43
</span></footer>
                                
                                </section>
<section class="normal markdown-section">
                                
                                <p><a id="boot-features"></a></p>
<h1 id="四、spring-boot-特性">四、Spring Boot 特性</h1>
<p>本部分将介绍 Spring Boot 相关的细节内容。在这里，您可以学习到可能需要使用和自定义的主要功能。您如果还没有做好充分准备，可能需要阅读<a href="#getting-started">第二部分：入门</a>和<a href="#using-boot">第三部分：使用 Spring Boot</a>，以便打下前期基础。</p>
<p><a id="boot-features-spring-application"></a></p>
<h2 id="23、springapplication">23、SpringApplication</h2>
<p><code>SpringApplication</code> 类提供了一种可通过运行 <code>main()</code> 方法来启动 Spring 应用的简单方式。多数情况下，您只需要委托给静态的 <code>SpringApplication.run</code> 方法：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">main</span><span class="token punctuation">(</span><span class="token class-name">String</span><span class="token punctuation">[</span><span class="token punctuation">]</span> args<span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token class-name">SpringApplication</span><span class="token punctuation">.</span><span class="token function">run</span><span class="token punctuation">(</span><span class="token class-name">MySpringConfiguration</span><span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">,</span> args<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>
<p>当应用启动时，您应该会看到类似以下的内容输出：</p>
<pre class="language-"><code>  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::   v2.1.1.RELEASE

2013-07-31 00:08:16.117  INFO 56603 --- [           main] o.s.b.s.app.SampleApplication            : Starting SampleApplication v0.1.0 on mycomputer with PID 56603 (/apps/myapp.jar started by pwebb)
2013-07-31 00:08:16.166  INFO 56603 --- [           main] ationConfigServletWebServerApplicationContext : Refreshing org.springframework.boot.web.servlet.context.AnnotationConfigServletWebServerApplicationContext@6e5a8246: startup date [Wed Jul 31 00:08:16 PDT 2013]; root of context hierarchy
2014-03-04 13:09:54.912  INFO 41370 --- [           main] .t.TomcatServletWebServerFactory : Server initialized with port: 8080
2014-03-04 13:09:56.501  INFO 41370 --- [           main] o.s.b.s.app.SampleApplication            : Started SampleApplication in 2.992 seconds (JVM running for 3.658)
</code></pre><p>默认情况下，将显示 <code>INFO</code> 级别的日志信息，包括一些应用启动相关信息。如果您需要修改 <code>INFO</code> 日志级别，请参考 <a href="#boot-features-custom-log-levels">26.4 部分：日志等级</a>。</p>
<p><a id="boot-features-startup-failure"></a></p>
<h3 id="231、启动失败">23.1、启动失败</h3>
<p>如果您的应用无法启动，注册的 <code>FailureAnalyzers</code> 可能会提供有相关的错误信息和解决问题的具体方法。例如，如果您在已经被占用的 <code>8080</code> 端口上启动了一个 web 应用，会看到类似以下的错误信息：</p>
<pre class="language-"><code>***************************
APPLICATION FAILED TO START
***************************

Description:

Embedded servlet container failed to start. Port 8080 was already in use.

Action:

Identify and stop the process that's listening on port 8080 or configure this application to listen on another port.
</code></pre><p><strong>注意</strong></p>
<blockquote>
<p>Spring Boot 提供了许多的 <code>FailureAnalyzer</code> 实现，您也可以<a href="#howto-failure-analyzer">添加自己的实现</a>。</p>
</blockquote>
<p>如果没有失败分析器能够处理的异常，您仍然可以显示完整的条件报告以便更好地了解出现的问题。为此，您需要针对 <code>org.springframework.boot.autoconfigure.logging.ConditionEvaluationReportLoggingListener</code> <a href="#boot-features-external-config">启用 <code>debug</code> 属性</a>或者<a href="#boot-features-custom-log-levels">开启 <code>DEBUG</code> 日志</a>。</p>
<p>例如，如果您使用 <code>java -jar</code> 运行应用，可以按以下方式启用 <code>debug</code> 属性：</p>
<pre class="language-"><code>$ java -jar myproject-0.0.1-SNAPSHOT.jar --debug
</code></pre><p><a id="boot-features-banner"></a></p>
<h3 id="232、自定义-banner">23.2、自定义 banner</h3>
<p>可以通过在 classpath 下添加一个 <code>banner.txt</code> 文件，或者将 <code>spring.banner.location</code> 属性指向该文件的位置来更改启动时打印的 banner。如果文件采用了非 UTF-8 编码，您可以设置 <code>spring.banner.charset</code> 来解决。除了文本文件，您还可以将 <code>banner.gif</code>、<code>banner.jpg</code> 或者 <code>banner.png</code> 图片文件添加到 classpath 下，或者设置 <code>spring.banner.image.location</code> 属性。指定的图片将会被转换成 ASCII 形式并打印在 banner 文本上方。</p>
<p>您可以在 <code>banner.txt</code> 文件中使用以下占位符：</p>
<table>
<thead>
<tr>
<th>变量</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>${application.version}</code></td>
<td>您的应用版本号，声明在 <code>MANIFEST.MF</code> 中。例如，<code>Implementation-Version: 1.0</code> 将被打印为 <code>1.0</code>。</td>
</tr>
<tr>
<td><code>${application.formatted-version}</code></td>
<td>您的应用版本号，声明在 <code>MANIFEST.MF</code> 中，格式化之后打印（用括号括起来，以 <code>v</code> 为前缀），例如 (<code>v1.0</code>)。</td>
</tr>
<tr>
<td><code>${spring-boot.version}</code></td>
<td>您使用的 Spring Boot 版本。例如 <code>2.1.1.RELEASE.</code>。</td>
</tr>
<tr>
<td><code>${spring-boot.formatted-version}</code></td>
<td>您使用的 Spring Boot 版本格式化之后显示（用括号括起来，以 <code>v</code> 为前缀）。例如 (<code>v2.1.1.RELEASE</code>)。</td>
</tr>
<tr>
<td><code>${Ansi.NAME}</code>（或 <code>${AnsiColor.NAME}</code>、<br><code>${AnsiBackground.NAME}</code>、<br><code>${AnsiStyle.NAME}</code>）</td>
<td>其中 <code>NAME</code> 是 ANSI 转义码的名称。有关详细信息，请参阅 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.1.RELEASE/spring-boot-project/spring-boot/src/main/java/org/springframework/boot/ansi/AnsiPropertySource.java" target="_blank">AnsiPropertySource</a>。</td>
</tr>
<tr>
<td><code>${application.title}</code></td>
<td>您的应用标题，声明在 <code>MANIFEST.MF</code> 中，例如 <code>Implementation-Title: MyApp</code> 打印为 <code>MyApp</code>。</td>
</tr>
</tbody>
</table>
<p><strong>提示</strong></p>
<blockquote>
<p>如果您想以编程的方式生成 banner，可以使用 <code>SpringApplication.setBanner(​...)</code> 方法。使用 <code>org.springframework.boot.Banner</code> 接口并实现自己的 <code>printBanner()</code> 方法。</p>
</blockquote>
<p>您还可以使用 <code>spring.main.banner-mode</code> 属性来确定是否必须在 <code>System.out</code>（<code>console</code>）上打印 banner，还是使用日志记录器（<code>log</code>）或者都不打印（<code>off</code>）。</p>
<p>打印的 banner 被注册名为 <code>springBootBanner</code> 的单例 bean。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>YAML 将 <code>off</code> 映射为 <code>false</code>，因此如果要禁用应用程序 banner，请确保属性添加引号。</p>
</blockquote>
<pre class="language-"><code class="lang-yaml"><span class="token key atrule">spring</span><span class="token punctuation">:</span>
    <span class="token key atrule">main</span><span class="token punctuation">:</span>
        <span class="token key atrule">banner-mode</span><span class="token punctuation">:</span> <span class="token string">"off"</span>
</code></pre>
<p><a id="boot-features-customizing-spring-application"></a></p>
<h3 id="233、自定义-springapplication">23.3、自定义 SpringApplication</h3>
<p>如果 <code>SpringApplication</code> 的默认设置不符合您的想法，您可以创建本地实例进行定制化。例如，要关闭 banner，您可以这样：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">main</span><span class="token punctuation">(</span><span class="token class-name">String</span><span class="token punctuation">[</span><span class="token punctuation">]</span> args<span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token class-name">SpringApplication</span> app <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">SpringApplication</span><span class="token punctuation">(</span><span class="token class-name">MySpringConfiguration</span><span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    app<span class="token punctuation">.</span><span class="token function">setBannerMode</span><span class="token punctuation">(</span><span class="token class-name">Banner</span><span class="token punctuation">.</span><span class="token class-name">Mode</span><span class="token punctuation">.</span>OFF<span class="token punctuation">)</span><span class="token punctuation">;</span>
    app<span class="token punctuation">.</span><span class="token function">run</span><span class="token punctuation">(</span>args<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>
<p><strong>注意</strong></p>
<blockquote>
<p>传入 <code>SpringApplication</code> 的构造参数是 spring bean 的配置源。大多情况下是引用 <code>@Configuration</code> 类，但您也可以引用 XML 配置或者被扫描的包。</p>
</blockquote>
<p>也可以使用 <code>application.properties</code> 文件配置 <code>SpringApplication</code>。有关详细信息，请参见<a href="#boot-features-external-config">第 24 章：外部化配置</a>。</p>
<p>关于配置选项的完整列表，请参阅 <a href="https://docs.spring.io/spring-boot/docs/2.1.1.RELEASE/api/org/springframework/boot/SpringApplication.html" target="_blank">SpringApplication Javadoc</a>。</p>
<p><a id="boot-features-customizing-spring-application"></a></p>
<h3 id="234、fluent-builder-api">23.4、Fluent Builder API</h3>
<p>如果您需要构建一个有层级关系的 <code>ApplicationContext</code>（具有父/子关系的多上下文），或者偏向使用 <strong>fluent</strong>（流式）构建器 API，可以使用 <code>SpringApplicationBuilder</code>。</p>
<p><code>SpringApplicationBuilder</code> 允许您链式调用多个方法，包括能创建出具有层次结构的 <code>parent</code> 和 <code>child</code> 方法。</p>
<p>例如：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">new</span> <span class="token class-name">SpringApplicationBuilder</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
        <span class="token punctuation">.</span><span class="token function">sources</span><span class="token punctuation">(</span><span class="token class-name">Parent</span><span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">)</span>
        <span class="token punctuation">.</span><span class="token function">child</span><span class="token punctuation">(</span><span class="token class-name">Application</span><span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">)</span>
        <span class="token punctuation">.</span><span class="token function">bannerMode</span><span class="token punctuation">(</span><span class="token class-name">Banner</span><span class="token punctuation">.</span><span class="token class-name">Mode</span><span class="token punctuation">.</span>OFF<span class="token punctuation">)</span>
        <span class="token punctuation">.</span><span class="token function">run</span><span class="token punctuation">(</span>args<span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p><strong>注意</strong></p>
<blockquote>
<p>创建层级的 <code>ApplicationContext</code> 时有部分限制，比如 Web 组件<strong>必须</strong>包含在子上下文中，并且相同的 <code>Environment</code> 将作用于父子上下文。有关详细信息，请参阅 <a href="https://docs.spring.io/spring-boot/docs/2.1.1.RELEASE/api/org/springframework/boot/builder/SpringApplicationBuilder.html" target="_blank">SpringApplicationBuilder Javadoc</a>。</p>
</blockquote>
<p><a id="boot-features-application-events-and-listeners"></a></p>
<h3 id="235、应用程序事件与监听器">23.5、应用程序事件与监听器</h3>
<p>除了常见的 Spring Framework 事件，比如 <a href="https://docs.spring.io/spring/docs/5.1.3.RELEASE/javadoc-api/org/springframework/context/event/ContextRefreshedEvent.html" target="_blank"><code>ContextRefreshedEvent</code></a>，<code>SpringApplication</code> 还会发送其他应用程序事件。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>在 <code>ApplicationContext</code> 创建之前，实际上触发了一些事件，因此您不能像 <code>@Bean</code> 一样注册监听器。您可以通过 <code>SpringApplication.addListeners(​...)</code> 或者 <code>SpringApplicationBuilder.listeners(...​)</code> 方法注册它们。如果您希望无论应用使用何种创建方式都能自动注册这些监听器，您都可以将 <code>META-INF/spring.factories</code> 文件添加到项目中，并使用 <code>org.springframework.context.ApplicationListener</code> 属性键指向您的监听器。比如：<code>org.springframework.context.ApplicationListener=com.example.project.MyListener</code></p>
</blockquote>
<p>当您运行应用时，应用程序事件将按照以下顺序发送：</p>
<ol>
<li>在开始应用开始运行但还没有进行任何处理时（除了注册监听器和初始化器[initializer]），将发送 <code>ApplicationStartingEvent</code>。</li>
<li>当 <code>Environment</code> 被上下文使用，但是在上下文创建之前，将发送 <code>ApplicationEnvironmentPreparedEvent</code>。</li>
<li>在开始刷新之前，bean 定义被加载之后发送 <code>ApplicationPreparedEvent</code>。</li>
<li>在上下文刷新之后且所有的应用和命令行运行器（command-line runner）被调用之前发送 <code>ApplicationStartedEvent</code>。</li>
<li>在应用程序和命令行运行器（command-line runner）被调用之后，将发出 <code>ApplicationReadyEvent</code>，该事件用于通知应用已经准备处理请求。</li>
<li>如果启动时发生异常，将发送 <code>ApplicationFailedEvent</code>。</li>
</ol>
<p><strong>提示</strong></p>
<blockquote>
<p>您可能不会经常使用应用程序事件，但了解他们的存在还是很有必要的。在框架内部，Spring Boot 使用这些事件来处理各种任务。</p>
</blockquote>
<p>应用程序事件发送使用了 Spring Framework 的事件发布机制。该部分机制确保在子上下文中发布给监听器的事件也会发布给所有祖先上下文中的监听器。因此，如果您的应用程序使用有层级结构的 SpringApplication 实例，则监听器可能会收到同种类型应用程序事件的多个实例。</p>
<p>为了让监听器能够区分其上下文事件和后代上下文事件，您应该注入其应用程序上下文，然后将注入的上下文与事件的上下文进行比较。可以通过实现 <code>ApplicationContextAware</code> 来注入上下文，如果监听器是 bean，则使用 <code>@Autowired</code> 注入上下文。</p>
<p><a id="boot-features-web-environment"></a></p>
<h3 id="236、web-环境">23.6、Web 环境</h3>
<p><code>SpringApplication</code> 试图为您创建正确类型的 <code>ApplicationContext</code>。确定 <code>WebApplicationType</code> 的算法非常简单：</p>
<ul>
<li>如果存在 Spring MVC，则使用 <code>AnnotationConfigServletWebServerApplicationContext</code></li>
<li>如果 Spring MVC 不存在且存在 Spring WebFlux，则使用 <code>AnnotationConfigReactiveWebServerApplicationContext</code></li>
<li>否则，使用 <code>AnnotationConfigApplicationContext</code></li>
</ul>
<p>这意味着如果您在同一个应用程序中使用了 Spring MVC 和 Spring WebFlux 中的新 <code>WebClient</code>，默认情况下将使用 Spring MVC。您可以通过调用 <code>setWebApplicationType(WebApplicationType)</code> 修改默认行为。</p>
<p>也可以调用 <code>setApplicationContextClass(...)</code> 来完全控制 <code>ApplicationContext</code> 类型。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>在 JUnit 测试中使用 <code>SpringApplication</code> 时，通常需要调用 <code>setWebApplicationType(WebApplicationType.NONE)</code>。</p>
</blockquote>
<p><a id="boot-features-application-arguments"></a></p>
<h3 id="237、访问应用程序参数">23.7、访问应用程序参数</h3>
<p>如果您需要访问从 <code>SpringApplication.run(​...)</code> 传入的应用程序参数，可以注入一个 <code>org.springframework.boot.ApplicationArguments</code> bean。<code>ApplicationArguments</code> 接口提供了访问原始 <code>String[]</code> 参数以及解析后的 <code>option</code> 和 <code>non-option</code> 参数的方法：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>boot</span><span class="token punctuation">.</span>*<span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>beans<span class="token punctuation">.</span>factory<span class="token punctuation">.</span>annotation</span><span class="token punctuation">.</span>*<span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>stereotype</span><span class="token punctuation">.</span>*<span class="token punctuation">;</span>

<span class="token annotation punctuation">@Component</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyBean</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@Autowired</span>
    <span class="token keyword">public</span> <span class="token class-name">MyBean</span><span class="token punctuation">(</span><span class="token class-name">ApplicationArguments</span> args<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">boolean</span> debug <span class="token operator">=</span> args<span class="token punctuation">.</span><span class="token function">containsOption</span><span class="token punctuation">(</span><span class="token string">"debug"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token class-name">List</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">String</span><span class="token punctuation">&gt;</span></span> files <span class="token operator">=</span> args<span class="token punctuation">.</span><span class="token function">getNonOptionArgs</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token comment">// if run with "--debug logfile.txt" debug=true, files=["logfile.txt"]</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p><strong>提示</strong></p>
<blockquote>
<p>Spring Boot 还向 Spring <code>Environment</code> 注册了一个 <code>CommandLinePropertySource</code>。这允许您可以使用 <code>@Value</code> 注解注入单个应用参数。</p>
</blockquote>
<p><a id="boot-features-command-line-runner"></a></p>
<h3 id="238、使用-applicationrunner-或-applicationrunner">23.8、使用 ApplicationRunner 或 ApplicationRunner</h3>
<p>如果您需要在 SpringApplication 启动时运行一些代码，可以实现 <code>ApplicationRunner</code> 或者 <code>CommandLineRunner</code> 接口。这两个接口的工作方式是一样的，都提供了一个单独的 <code>run</code> 方法，它将在 <code>SpringApplication.run(​...)</code> 完成之前调用。</p>
<p><code>CommandLineRunner</code> 接口提供了访问应用程序字符串数组形式参数的方法，而 <code>ApplicationRunner</code> 则使用了上述的 <code>ApplicationArguments</code> 接口。以下示例展示 <code>CommandLineRunner</code> 和 <code>run</code> 方法的使用：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>boot</span><span class="token punctuation">.</span>*<span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>stereotype</span><span class="token punctuation">.</span>*<span class="token punctuation">;</span>

<span class="token annotation punctuation">@Component</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyBean</span> <span class="token keyword">implements</span> <span class="token class-name">CommandLineRunner</span> <span class="token punctuation">{</span>

    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">run</span><span class="token punctuation">(</span><span class="token class-name">String</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span> args<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment">// Do something...</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>如果您定义了多个 <code>CommandLineRunner</code> 或者 <code>ApplicationRunner</code> bean，则必须指定调用顺序，您可以实现 <code>org.springframework.core.Ordered</code> 接口，也可以使用 <code>org.springframework.core.annotation.Order</code> 注解解决顺序问题。</p>
<p><a id="boot-features-application-exit"></a></p>
<h3 id="239、应用程序退出">23.9、应用程序退出</h3>
<p>每个 <code>SpringApplication</code> 注册了一个 JVM 关闭钩子，以确保 <code>ApplicationContext</code> 在退出时可以优雅关闭。所有标准的 Spring 生命周期回调（比如 <code>DisposableBean</code> 接口，或者 <code>@PreDestroy</code> 注解）都可以使用。</p>
<p>此外，如果希望在调用 <code>SpringApplication.exit()</code> 时返回特定的退出码，则 bean 可以实现 <code>org.springframework.boot.ExitCodeGenerator</code> 接口。之后退出码将传递给 <code>System.exit()</code> 以将其作为状态码返回，如示例所示：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@SpringBootApplication</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">ExitCodeApplication</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@Bean</span>
    <span class="token keyword">public</span> <span class="token class-name">ExitCodeGenerator</span> <span class="token function">exitCodeGenerator</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> <span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">-&gt;</span> <span class="token number">42</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">main</span><span class="token punctuation">(</span><span class="token class-name">String</span><span class="token punctuation">[</span><span class="token punctuation">]</span> args<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token class-name">System</span><span class="token punctuation">.</span><span class="token function">exit</span><span class="token punctuation">(</span><span class="token class-name">SpringApplication</span>
                <span class="token punctuation">.</span><span class="token function">exit</span><span class="token punctuation">(</span><span class="token class-name">SpringApplication</span><span class="token punctuation">.</span><span class="token function">run</span><span class="token punctuation">(</span><span class="token class-name">ExitCodeApplication</span><span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">,</span> args<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>此外，<code>ExitCodeGenerator</code> 接口可以通过异常实现。遇到这类异常时，Spring Boot 将返回实现的 <code>getExitCode()</code> 方法提供的退出码。</p>
<p><a id="boot-features-application-admin"></a></p>
<h3 id="2310、管理功能">23.10、管理功能</h3>
<p>可以通过指定 <code>spring.application.admin.enabled</code> 属性来为应用程序启用管理相关的功能。其将在 <code>MBeanServer</code> 平台上暴露 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.1.RELEASE/spring-boot-project/spring-boot/src/main/java/org/springframework/boot/admin/SpringApplicationAdminMXBean.java" target="_blank"><code>SpringApplicationAdminMXBean</code></a>。您可以使用此功能来远程管理 Spring Boot 应用。该功能对服务包装器的实现也是非常有用的。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>如果您想知道应用程序在哪一个 HTTP 端口上运行，请使用 <code>local.server.port</code> 键获取该属性。</p>
</blockquote>
<p><strong>注意</strong></p>
<blockquote>
<p>启用此功能时请小心，因为 MBean 暴露了关闭应用程序的方法。</p>
</blockquote>
<p><a id="boot-features-external-config"></a></p>
<h2 id="24、外部化配置">24、外部化配置</h2>
<p>Spring Boot 可以让您的配置外部化，以便可以在不同环境中使用相同的应用程序代码。您可以使用 properties 文件、YAML 文件、环境变量或者命令行参数来外部化配置。可以使用 <code>@Value</code> 注解将属性值直接注入到 bean 中，可通过 Spring 的 <code>Environment</code> 访问，或者通过 <code>@ConfigurationProperties</code> 绑定到<a href="#boot-features-external-config-typesafe-configuration-properties">结构化对象</a>。</p>
<p>Spring Boot 使用了一个非常特别的 <code>PropertySource</code> 指令，用于智能覆盖默认值。属性将按照以下顺序处理：</p>
<ol>
<li>在您的主目录（当 devtools 被激活，则为 <code>~/.spring-boot-devtools.properties</code> ）中的 <a href="#using-boot-devtools-globalsettings">Devtools 全局设置属性</a>。</li>
<li>在测试中使用到的 <code>@TestPropertySource</code> 注解。</li>
<li>在测试中使用到的 <code>properties</code> 属性，可以是 <a href="https://docs.spring.io/spring-boot/docs/2.1.1.RELEASE/api/org/springframework/boot/test/context/SpringBootTest.html" target="_blank"><code>@SpringBootTest</code></a> 和<a href="#boot-features-testing-spring-boot-applications-testing-autoconfigured-tests">用于测试应用程序某部分的测试注解</a>。</li>
<li>命令行参数。</li>
<li>来自 <code>SPRING_APPLICATION_JSON</code> 的属性（嵌入在环境变量或者系统属性【system propert】中的内联 JSON）。</li>
<li><code>ServletConfig</code> 初始化参数。</li>
<li><code>ServletContext</code> 初始化参数。</li>
<li>来自 <code>java:comp/env</code> 的 JNDI 属性。</li>
<li>Java 系统属性（<code>System.getProperties()</code>）。</li>
<li>操作系统环境变量。</li>
<li>只有 <code>random.*</code> 属性的 <code>RandomValuePropertySource</code>。</li>
<li>在已打包的 jar 外部的<a href="#boot-features-external-config-profile-specific-properties">指定 profile 的应用属性文件</a>（<code>application-{profile}.properties</code> 和 YAML 变量）。</li>
<li>在已打包的 jar 内部的<a href="#boot-features-external-config-profile-specific-properties">指定 profile 的应用属性文件</a>（<code>application-{profile}.properties</code> 和 YAML 变量）。</li>
<li>在已打包的 jar 外部的应用属性文件（<code>application.properties</code> 和 YAML 变量）。</li>
<li>在已打包的 jar 内部的应用属性文件（<code>application.properties</code> 和 YAML 变量）。</li>
<li>在 <code>@Configuration</code> 类上的 <code>@PropertySource</code> 注解。</li>
<li>默认属性（使用 <code>SpringApplication.setDefaultProperties</code> 指定）。</li>
</ol>
<p>举个例子，假设开发的 <code>@Component</code> 使用了 <code>name</code> 属性，可以这样：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>stereotype</span><span class="token punctuation">.</span>*<span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>beans<span class="token punctuation">.</span>factory<span class="token punctuation">.</span>annotation</span><span class="token punctuation">.</span>*<span class="token punctuation">;</span>

<span class="token annotation punctuation">@Component</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyBean</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@Value</span><span class="token punctuation">(</span><span class="token string">"${name}"</span><span class="token punctuation">)</span>
    <span class="token keyword">private</span> <span class="token class-name">String</span> name<span class="token punctuation">;</span>

    <span class="token comment">// ...</span>

<span class="token punctuation">}</span>
</code></pre>
<p>在您的应用程序的 classpath 中（比如在 jar 中），您可以有一个 <code>application.properties</code>，它为 <code>name</code> 提供了一个合适的默认属性值。当在新环境中运行时，您可以在 jar 外面提供一个 <code>application.properties</code> 来覆盖 <code>name</code>。对于一次性测试，您可以使用命令行指定形式启动（比如 <code>java -jar app.jar --name="Spring"</code>）。</p>
<p><strong>提示</strong></p>
<blockquote>

`SPRING_APPLICATION_JSON` 属性可以在命令行中提供一个环境变量。比如在 UN*X shell 中：

```
$ SPRING_APPLICATION_JSON='{"acme":{"name":"test"}}' java -jar myapp.jar
```

在此示例中，您可以在 Spring `Environment` 中使用 `acme.name=test`，也可以在系统属性（System property）中将 JSON 作为 `spring.application.json` 属性提供：

```
$ java -Dspring.application.json='{"name":"test"}' -jar myapp.jar
```

或者以命令行参数形式：

```
$ java -jar myapp.jar --spring.application.json='{"name":"test"}'
```

或者将 JSON 作为一个 JNDI 变量：`java:comp/env/spring.application.json`。

</blockquote>

<p><a id="boot-features-external-config-random-values"></a></p>
<h3 id="241、配置随机值">24.1、配置随机值</h3>
<p><code>RandomValuePropertySource</code> 对于随机值注入非常有用（比如在保密场景或者测试用例中)。它可以产生 integer、long、uuid 和 string。如下示例：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">my.secret</span><span class="token attr-value"><span class="token punctuation">=</span>${random.value}</span>
<span class="token constant">my.number</span><span class="token attr-value"><span class="token punctuation">=</span>${random.int}</span>
<span class="token constant">my.bignumber</span><span class="token attr-value"><span class="token punctuation">=</span>${random.long}</span>
<span class="token constant">my.uuid</span><span class="token attr-value"><span class="token punctuation">=</span>${random.uuid}</span>
<span class="token constant">my.number.less.than.ten</span><span class="token attr-value"><span class="token punctuation">=</span>${random.int(10)}</span>
<span class="token constant">my.number.in.range</span><span class="token attr-value"><span class="token punctuation">=</span>${random.int[1024,65536]}</span>
</code></pre>
<p><code>random.int*</code> 语法为 <code>OPEN value (,max) CLOSE</code>，<code>OPEN,CLOSE</code> 可为任意字符，<code>value,max</code> 为整数。如果使用了 <code>max</code>，<code>value</code> 则为最小值，<code>max</code> 为最大值。</p>
<p><a id="boot-features-external-config-command-line-args"></a></p>
<h3 id="242、访问命令行属性">24.2、访问命令行属性</h3>
<p>默认情况下，<code>SpringApplication</code> 将所有命令行选项参数（即以 <code>--</code> 开头的参数，比如 <code>--server.port=9000</code>）转换为属性，并将它们添加到 Spring <code>Environment</code> 中。如之前所述，命令行属性始终优先于其他属性源。</p>
<p>如果您不希望将命令行属性添加到 <code>Environment</code>，可以使用 <code>SpringApplication.setAddCommandLineProperties(false)</code> 来禁用它们。</p>
<p><a id="boot-features-external-config-application-property-files"></a></p>
<h3 id="243、应用程序属性文件">24.3、应用程序属性文件</h3>
<p><code>SpringApplication</code> 从以下位置的 <code>application.properties</code> 文件中加载属性（properties），并将它们添加到 Spring <code>Environment</code> 中：</p>
<ol>
<li>当前目录的 <code>/config</code> 子目录</li>
<li>当前目录</li>
<li>classpath 上的 <code>/config</code> 包</li>
<li>classpath 根路径</li>
</ol>
<p>列表按序号优先级排序，序号越小，优先级越高。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>您还可以使用 <a href="#boot-features-external-config-yaml">YAML（.yml）</a>文件来替代 <strong>.properties</strong>。</p>
</blockquote>
<p>如果您不喜欢 <code>application.properties</code> 作为配置文件名，则可以通过指定 <code>spring.config.name</code> 环境属性来切换到另一个文件名。您还可以使用 <code>spring.config.location</code> 环境属性来引用一个显式位置（以逗号分隔的目录位置或文件路径列表）。以下示例展示了如何指定其他文件名：</p>
<pre class="language-"><code>$ java -jar myproject.jar --spring.config.name=myproject
</code></pre><p>以下示例展示了如何指定两个位置：</p>
<pre class="language-"><code>$ java -jar myproject.jar --spring.config.location=classpath:/default.properties,classpath:/override.properties
</code></pre><p><strong>警告</strong></p>
<blockquote>
<p><code>spring.config.name</code> 和 <code>spring.config.location</code> 在程序启动早期就用来确定哪些文件必须加载，因此必须将它们定义为环境属性（通常是 OS 环境变量、系统属性或命令行参数）。</p>
</blockquote>
<p>如果 <code>spring.config.location</code> 包含目录（而不是文件），则它们应该以 <code>/</code> 结尾（并且在运行期间，在加载之前追加从 <code>spring.config.name</code> 生成的名称，包括指定 profile 的文件名）。 <code>spring.config.location</code> 中指定的文件按原样使用，不支持指定 profile 形式，并且可被任何指定 profile 的文件的属性所覆盖。</p>
<p>配置位置以相反的顺序搜索。默认情况下，配置的位置为 <code>classpath:/,classpath:/config/,file:./,file:./config/</code>。生成的搜索顺序如下：</p>
<ol>
<li><code>file:./config/</code></li>
<li><code>file:./</code></li>
<li><code>classpath:/config/</code></li>
<li><code>classpath:/</code></li>
</ol>
<p>使用了 <code>spring.config.location</code> 配置自定义配置位置时，默认位置配置将被替代。例如，如果 <code>spring.config.location</code> 配置为 <code>classpath:/custom-config/,file:./custom-config/</code>，搜索顺序将变为以下：</p>
<ol>
<li><code>file:./custom-config/</code></li>
<li><code>classpath:custom-config/</code></li>
</ol>
<p>或者，当使用 <code>spring.config.additional-location</code> 配置自定义配置位置时，除了使用默认位置外，还会使用它们。这些其他（additional）位置将在默认位置之前搜索。例如，如果将其他位置配置为 <code>classpath:/custom-config/,file:./custom-config/</code>，则搜索顺序将变为以下内容：</p>
<ol>
<li><code>file:./custom-config/</code></li>
<li><code>classpath:custom-config/</code></li>
<li><code>file:./config/</code></li>
<li><code>file:./</code></li>
<li><code>classpath:/config/</code></li>
<li><code>classpath:/</code></li>
</ol>
<p>该搜索顺序允许您在一个配置文件中指定默认值，然后有选择地覆盖另一个配置文件中的值。您可以在 <code>application.properties</code>（或您使用 <code>spring.config.name</code> 指定的其他文件）中的某个默认位置为应用程序提供默认值。之后，在运行时，这些默认值将被自定义位置中的某个文件所覆盖。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>如果您使用的是环境变量而不是系统属性，大部分操作系统都不允许使用 <code>.</code> 分隔的键名，但您可以使用下划线来代替（例如，使用 <code>SPRING_CONFIG_NAME</code> 而不是 <code>spring.config.name</code>）。</p>
</blockquote>
<p><strong>注意</strong></p>
<blockquote>
<p>如果应用程序在容器中运行，则可以使用 JNDI 属性（<code>java:comp/env</code>）或 servlet 上下文初始化参数来代替环境变量或系统属性。</p>
</blockquote>
<p><a id="boot-features-external-config-profile-specific-properties"></a></p>
<h3 id="244、特定-profile-的属性文件">24.4、特定 Profile 的属性文件</h3>
<p>除 <code>application.properties</code> 文件外，还可以使用以下命名约定定义特定 profile 的属性文件：<code>application-{profile}.properties</code>。<code>Environment</code> 有一组默认配置文件（默认情况下为 <code>default</code>），如果未设置激活的（active）profile，则使用这些配置文件。换句话说，如果没有显式激活 profile，则会加载 <code>application-default.properties</code> 中的属性。</p>
<p>特定 profile 的属性文件从与标准 <code>application.properties</code> 相同的位置加载，特定 profile 的属性文件无论是否在打包的 jar 内部，都始终覆盖非特定文件。</p>
<p>如果指定了多个配置文件，则应用 last-wins 策略（优先采取最后一个）。例如，<code>spring.profiles.active</code> 属性指定的配置文件是在使用 <code>SpringApplication</code> API 配置的配置文件之后添加的，因此优先应用。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>如果在 <code>spring.config.location</code> 中指定了文件，则不考虑这些文件的特定 profile 形式。如果您还想使用特定 profile 的属性文件，请在 <code>spring.config.location</code> 中使用目录形式。</p>
</blockquote>
<p><a id="boot-features-external-config-placeholders-in-properties"></a></p>
<h3 id="245、属性中的占位符">24.5、属性中的占位符</h3>
<p><code>application.properties</code> 中的值在使用时通过现有的 <code>Environment</code> 进行过滤，因此您可以返回之前定义的值（例如，从系统属性）。</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">app.name</span><span class="token attr-value"><span class="token punctuation">=</span>MyApp</span>
<span class="token constant">app.description</span><span class="token attr-value"><span class="token punctuation">=</span>${app.name} is a Spring Boot application</span>
</code></pre>
<p><strong>提示</strong></p>
<blockquote>
<p>您还可以使用此技术创建现有 Spring Boot 属性的<strong>简短</strong>形式。有关详细信息，请参见<a href="hwo-to.md#howto-use-short-command-line-arguments">第 77.4 章节：使用<strong>简短</strong>命令行参数</a>。</p>
</blockquote>
<p><a id="boot-features-encrypting-properties"></a></p>
<h3 id="246、加密属性">24.6、加密属性</h3>
<p>Spring Boot 没有为加密属性值提供任何内置支持，然而，它提供了修改 Spring <code>Environment</code> 包含的值所必需的钩子。<code>EnvironmentPostProcessor</code> 接口允许您在应用程序启动之前操作 <code>Environment</code>。有关详细信息，请参见<a href="how-to.md#howto-customize-the-environment-or-application-context">第 76.3 章节：在启动前自定义 Environment 或 ApplicationContext</a>。</p>
<p>如果您正在寻找一种可用于存储凭据和密码的安全方法，<a href="https://cloud.spring.io/spring-cloud-vault/" target="_blank">Spring Cloud Vault</a> 项目支持在 <a href="https://www.vaultproject.io/" target="_blank">HashiCorp Vault</a> 中存储外部化配置。</p>
<p><a id="boot-features-external-config-yaml"></a></p>
<h3 id="247、使用-yaml-代替属性文件">24.7、使用 YAML 代替属性文件</h3>
<p><a href="http://yaml.org/" target="_blank">YAML</a> 是 JSON 的超集，是一个可用于指定层级配置数据的便捷格式。只要在 classpath 上有 <a href="http://www.snakeyaml.org/" target="_blank">SnakeYAML</a> 库，<code>SpringApplication</code> 类就会自动支持 YAML 作为属性文件（properties）的替代。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>如果使用 <strong>starter</strong>，则 <code>spring-boot-starter</code> 会自动提供 SnakeYAML。</p>
</blockquote>
<p><a id="boot-features-external-config-loading-yaml"></a></p>
<h4 id="2471、加载-yaml">24.7.1、加载 YAML</h4>
<p>Spring Framework 提供了两个便捷类，可用于加载 YAML 文档。<code>YamlPropertiesFactoryBean</code> 将 YAML 加载为 <code>Properties</code>，<code>YamlMapFactoryBean</code> 将 YAML 加载为 <code>Map</code>。</p>
<p>例如以下 YAML 文档：</p>
<pre class="language-"><code class="lang-yaml"><span class="token key atrule">environments</span><span class="token punctuation">:</span>
  <span class="token key atrule">dev</span><span class="token punctuation">:</span>
    <span class="token key atrule">url</span><span class="token punctuation">:</span> http<span class="token punctuation">:</span>//dev.example.com
    <span class="token key atrule">name</span><span class="token punctuation">:</span> Developer Setup
  <span class="token key atrule">prod</span><span class="token punctuation">:</span>
    <span class="token key atrule">url</span><span class="token punctuation">:</span> http<span class="token punctuation">:</span>//another.example.com
    <span class="token key atrule">name</span><span class="token punctuation">:</span> My Cool App
</code></pre>
<p>前面的示例将转换为以下属性（properties）：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">environments.dev.url</span><span class="token attr-value"><span class="token punctuation">=</span>http://dev.example.com</span>
<span class="token constant">environments.dev.name</span><span class="token attr-value"><span class="token punctuation">=</span>Developer Setup</span>
<span class="token constant">environments.prod.url</span><span class="token attr-value"><span class="token punctuation">=</span>http://another.example.com</span>
<span class="token constant">environments.prod.name</span><span class="token attr-value"><span class="token punctuation">=</span>My Cool App</span>
</code></pre>
<p>YAML 列表表示带有 <code>[index]</code> 下标引用的属性键。例如以下 YAML：</p>
<pre class="language-"><code class="lang-yaml"><span class="token key atrule">my</span><span class="token punctuation">:</span>
<span class="token key atrule">servers</span><span class="token punctuation">:</span>
  <span class="token punctuation">-</span> dev.example.com
  <span class="token punctuation">-</span> another.example.com
</code></pre>
<p>以上示例将转成以下属性：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">my.servers[0]</span><span class="token attr-value"><span class="token punctuation">=</span>dev.example.com</span>
<span class="token constant">my.servers[1]</span><span class="token attr-value"><span class="token punctuation">=</span>another.example.com</span>
</code></pre>
<p>要使用 Spring Boot 的 <code>Binder</code> 工具来绑定这样配置到属性（这是 <code>@ConfigurationProperties</code> 所做的），你需要在目标 bean 中有一个 <code>java.util.List</code>（或 <code>Set</code>）类型的属性，你需要为其提供一个 setter 或者使用可变值初始化它。 例如，以下示例展示将上述的配置与属性绑定：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@ConfigurationProperties</span><span class="token punctuation">(</span>prefix<span class="token operator">=</span><span class="token string">"my"</span><span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">Config</span> <span class="token punctuation">{</span>

    <span class="token keyword">private</span> <span class="token class-name">List</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">String</span><span class="token punctuation">&gt;</span></span> servers <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">ArrayList</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">String</span><span class="token punctuation">&gt;</span></span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

    <span class="token keyword">public</span> <span class="token class-name">List</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">String</span><span class="token punctuation">&gt;</span></span> <span class="token function">getServers</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> <span class="token keyword">this</span><span class="token punctuation">.</span>servers<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<p><a id="boot-features-external-config-exposing-yaml-to-spring"></a></p>
<h4 id="2472、在-spring-environment-中将-yaml-暴露为属性">24.7.2、在 Spring Environment 中将 YAML 暴露为属性</h4>
<p><code>YamlPropertySourceLoader</code> 类可用于在 Spring <code>Environment</code> 中将 YAML 暴露为 <code>PropertySource</code>。这样做可以让您使用带占位符语法的 <code>@Value</code> 注解来访问 YAML 属性。</p>
<p><a id="boot-features-external-config-multi-profile-yaml"></a></p>
<h4 id="2473、多-profile-yaml-文档">24.7.3、多 profile YAML 文档</h4>
<p>您可以使用 <code>spring.profiles</code> key 在单个文件中指定多个特定 profile 的 YAML 文档，以指示文档何时应用，如下所示：</p>
<pre class="language-"><code class="lang-yaml"><span class="token key atrule">server</span><span class="token punctuation">:</span>
  <span class="token key atrule">address</span><span class="token punctuation">:</span> 192.168.1.100
<span class="token punctuation">---</span>
<span class="token key atrule">spring</span><span class="token punctuation">:</span>
  <span class="token key atrule">profiles</span><span class="token punctuation">:</span> development
<span class="token key atrule">server</span><span class="token punctuation">:</span>
  <span class="token key atrule">address</span><span class="token punctuation">:</span> 127.0.0.1
<span class="token punctuation">---</span>
<span class="token key atrule">spring</span><span class="token punctuation">:</span>
  <span class="token key atrule">profiles</span><span class="token punctuation">:</span> production &amp; eu<span class="token punctuation">-</span>central
<span class="token key atrule">server</span><span class="token punctuation">:</span>
  <span class="token key atrule">address</span><span class="token punctuation">:</span> 192.168.1.120
</code></pre>
<p>在前面示例中，如果 <code>development</code> profile 处于激活状态，则 <code>server.address</code> 属性得值为 <code>127.0.0.1</code>。 同样，如果 <code>production</code> 和 <code>eu-central</code> profile 处于激活状态，则 <code>server.address</code> 属性的值为 <code>192.168.1.120</code>。如果未激活 <code>development</code>、<code>production</code> 或 <code>eu-central</code> profile，则该属性的值为 <code>192.168.1.100</code>。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>因此，<code>spring.profiles</code> 可以包含一个简单的 profile 名称（例如 <code>production</code>）或一个 profile 表达式。profile 表达式允许表达更复杂的 profile 逻辑，例如 <code>production &amp; (eu-central | eu-west)</code>。有关详细信息，请查阅<a href="https://docs.spring.io/spring/docs/5.1.3.RELEASE/spring-framework-reference/core.html#beans-definition-profiles-java" target="_blank">参考指南</a>。</p>
</blockquote>
<p>如果在应用程序上下文启动时没有显式激活，则激活默认 profile。因此，在以下 YAML 中，我们为 <code>spring.security.user.password</code> 设置了一个值，该值<strong>仅</strong>在 <code>default</code> profile 中可用：</p>
<pre class="language-"><code class="lang-yaml"><span class="token key atrule">server</span><span class="token punctuation">:</span>
  <span class="token key atrule">port</span><span class="token punctuation">:</span> <span class="token number">8000</span>
<span class="token punctuation">---</span>
<span class="token key atrule">spring</span><span class="token punctuation">:</span>
  <span class="token key atrule">profiles</span><span class="token punctuation">:</span> default
  <span class="token key atrule">security</span><span class="token punctuation">:</span>
    <span class="token key atrule">user</span><span class="token punctuation">:</span>
      <span class="token key atrule">password</span><span class="token punctuation">:</span> weak
</code></pre>
<p>然而，在以下示例中，始终设置密码，因为它未附加到任何 profile，如果需要更改，必须在所有其他 profile 中显式重置：</p>
<pre class="language-"><code class="lang-yaml"><span class="token key atrule">server</span><span class="token punctuation">:</span>
  <span class="token key atrule">port</span><span class="token punctuation">:</span> <span class="token number">8000</span>
<span class="token key atrule">spring</span><span class="token punctuation">:</span>
  <span class="token key atrule">security</span><span class="token punctuation">:</span>
    <span class="token key atrule">user</span><span class="token punctuation">:</span>
      <span class="token key atrule">password</span><span class="token punctuation">:</span> weak
</code></pre>
<p>使用 <code>spring.profiles</code> 元素来指定 Spring profile 可以选择通过使用 <code>!</code> 字符来取反（否定）。如果为单个文档指定了否定和非否定的 profile，则至少一个非否定的 profile 必须匹配，没有否定的 profile 可以匹配。</p>
<p><a id="boot-features-external-config-yaml-shortcomings"></a></p>
<h4 id="2474、yaml-的缺点">24.7.4、YAML 的缺点</h4>
<p>无法使用 <code>@PropertySource</code> 注解加载 YAML 文件。因此，如果您需要以这种方式加载值，请使用属性文件（properties）。</p>
<p><a id="boot-features-external-config-typesafe-configuration-properties"></a></p>
<h3 id="248、类型安全的配置属性">24.8、类型安全的配置属性</h3>
<p>使用 <code>@Value("${property}")</code> 注解来注入配置属性有时会很麻烦，特别是如果您使用了多个属性或者您的数据本质上是分层结构。Spring Boot 提供了另一种使用属性的方法，该方法使用强类型的 bean 来管理和验证应用程序的配置，如下所示：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">package</span> <span class="token namespace">com<span class="token punctuation">.</span>example</span><span class="token punctuation">;</span>

<span class="token keyword">import</span> <span class="token namespace">java<span class="token punctuation">.</span>net</span><span class="token punctuation">.</span><span class="token class-name">InetAddress</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">java<span class="token punctuation">.</span>util</span><span class="token punctuation">.</span><span class="token class-name">ArrayList</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">java<span class="token punctuation">.</span>util</span><span class="token punctuation">.</span><span class="token class-name">Collections</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">java<span class="token punctuation">.</span>util</span><span class="token punctuation">.</span><span class="token class-name">List</span><span class="token punctuation">;</span>

<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>boot<span class="token punctuation">.</span>context<span class="token punctuation">.</span>properties</span><span class="token punctuation">.</span><span class="token class-name">ConfigurationProperties</span><span class="token punctuation">;</span>

<span class="token annotation punctuation">@ConfigurationProperties</span><span class="token punctuation">(</span><span class="token string">"acme"</span><span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">AcmeProperties</span> <span class="token punctuation">{</span>

    <span class="token keyword">private</span> <span class="token keyword">boolean</span> enabled<span class="token punctuation">;</span>

    <span class="token keyword">private</span> <span class="token class-name">InetAddress</span> remoteAddress<span class="token punctuation">;</span>

    <span class="token keyword">private</span> <span class="token keyword">final</span> <span class="token class-name">Security</span> security <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">Security</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

    <span class="token keyword">public</span> <span class="token keyword">boolean</span> <span class="token function">isEnabled</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span> <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span> <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">setEnabled</span><span class="token punctuation">(</span><span class="token keyword">boolean</span> enabled<span class="token punctuation">)</span> <span class="token punctuation">{</span> <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span> <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token class-name">InetAddress</span> <span class="token function">getRemoteAddress</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span> <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span> <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">setRemoteAddress</span><span class="token punctuation">(</span><span class="token class-name">InetAddress</span> remoteAddress<span class="token punctuation">)</span> <span class="token punctuation">{</span> <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span> <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token class-name">Security</span> <span class="token function">getSecurity</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span> <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span> <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">class</span> <span class="token class-name">Security</span> <span class="token punctuation">{</span>

        <span class="token keyword">private</span> <span class="token class-name">String</span> username<span class="token punctuation">;</span>

        <span class="token keyword">private</span> <span class="token class-name">String</span> password<span class="token punctuation">;</span>

        <span class="token keyword">private</span> <span class="token class-name">List</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">String</span><span class="token punctuation">&gt;</span></span> roles <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">ArrayList</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token punctuation">&gt;</span></span><span class="token punctuation">(</span><span class="token class-name">Collections</span><span class="token punctuation">.</span><span class="token function">singleton</span><span class="token punctuation">(</span><span class="token string">"USER"</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

        <span class="token keyword">public</span> <span class="token class-name">String</span> <span class="token function">getUsername</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span> <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span> <span class="token punctuation">}</span>

        <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">setUsername</span><span class="token punctuation">(</span><span class="token class-name">String</span> username<span class="token punctuation">)</span> <span class="token punctuation">{</span> <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span> <span class="token punctuation">}</span>

        <span class="token keyword">public</span> <span class="token class-name">String</span> <span class="token function">getPassword</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span> <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span> <span class="token punctuation">}</span>

        <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">setPassword</span><span class="token punctuation">(</span><span class="token class-name">String</span> password<span class="token punctuation">)</span> <span class="token punctuation">{</span> <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span> <span class="token punctuation">}</span>

        <span class="token keyword">public</span> <span class="token class-name">List</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">String</span><span class="token punctuation">&gt;</span></span> <span class="token function">getRoles</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span> <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span> <span class="token punctuation">}</span>

        <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">setRoles</span><span class="token punctuation">(</span><span class="token class-name">List</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">String</span><span class="token punctuation">&gt;</span></span> roles<span class="token punctuation">)</span> <span class="token punctuation">{</span> <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span> <span class="token punctuation">}</span>

    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<p>前面的 POJO 定义了以下属性：</p>
<ul>
<li><code>acme.enabled</code>，默认值为 <code>false</code>。</li>
<li><code>acme.remote-address</code>，可以从 String 强制转换的类型。</li>
<li><code>acme.security.username</code>，内嵌一个 <strong>security</strong> 对象，其名称由属性名称决定。特别是，返回类型根本没有使用，可能是 <code>SecurityProperties</code>。</li>
<li><code>acme.security.password</code>。</li>
<li><code>acme.security.roles</code>，String 集合。</li>
</ul>
<p><strong>注意</strong></p>
<blockquote>

getter 和 setter 通常是必需的，因为绑定是通过标准的 Java Bean 属性描述符来完成，就像在 Spring MVC 中一样。以下情况可以省略 setter：

- Map，只要它们要初始化，就需要一个 getter 但不一定需要setter，因为它们可以被 binder 修改。
- 集合和数组可以通过一个索引（通常使用 YAML）或使用单个逗号分隔值（属性）进行访问。最后一种情况必须使用 setter。我们建议始终为此类型添加 setter。如果初始化集合，请确保它是可变的（如上例所示）。
- 如果初始化嵌套的 POJO 属性（如前面示例中的 `Security` 字段），则不需要 setter。如果您希望 binder 使用其默认构造函数动态创建实例，则需要一个 setter。

有些人可能会使用 Project Lombok 来自动生成 getter 和 setter。请确保 Lombok 不为此类型生成任何特定构造函数，因为容器会自动使用它来实例化对象。

最后，考虑到标准 Java Bean 属性，不支持对静态属性的绑定。

</blockquote>

<p><strong>提示</strong></p>
<blockquote>
<p>另请参阅 <a href="#boot-features-external-config-vs-value">@Value 和 @ConfigurationProperties 之间的差异</a>。</p>
</blockquote>
<p>您还需要列出要在 <code>@EnableConfigurationProperties</code> 注解中注册的属性类，如下所示：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Configuration</span>
<span class="token annotation punctuation">@EnableConfigurationProperties</span><span class="token punctuation">(</span><span class="token class-name">AcmeProperties</span><span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyConfiguration</span> <span class="token punctuation">{</span>
<span class="token punctuation">}</span>
</code></pre>
<p><strong>注意</strong></p>
<blockquote>

当以这种方式注册 `@ConfigurationProperties` bean 时，bean 具有一个固定格式的名称：`<prefix>-<fqn>`，其中 `<prefix>` 是 `@ConfigurationProperties` 注解中指定的环境 key 前缀，`<fqn>` 是 bean 的完全限定类名。如果注解未提供任何前缀，则仅使用 bean 的完全限定类名。

上面示例中的 bean 名称为 `acme-com.example.AcmeProperties`。

</fqn></prefix></fqn></prefix></blockquote>

<p>即使前面的配置为 <code>AcmeProperties</code> 创建了一个 bean，我们也建议 <code>@ConfigurationProperties</code> 只处理环境（environment），特别是不要从上下文中注入其他 bean。话虽如此，<code>@EnableConfigurationProperties</code> 注解也会自动应用到您的项目，以便从 <code>Environment</code> 配置使用了 <code>@ConfigurationProperties</code> 注解的所有<strong>现有</strong>的 bean。您可以通过确保 <code>AcmeProperties</code> 已经是一个 bean 来快捷生成 <code>MyConfiguration</code>，如下所示：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Component</span>
<span class="token annotation punctuation">@ConfigurationProperties</span><span class="token punctuation">(</span>prefix<span class="token operator">=</span><span class="token string">"acme"</span><span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">AcmeProperties</span> <span class="token punctuation">{</span>

    <span class="token comment">// ... see the preceding example</span>

<span class="token punctuation">}</span>
</code></pre>
<p>这种配置风格特别适用于 <code>SpringApplication</code> 外部 YAML 配置，如下所示：</p>
<pre class="language-"><code class="lang-yaml"><span class="token comment"># application.yml</span>

<span class="token key atrule">acme</span><span class="token punctuation">:</span>
    <span class="token key atrule">remote-address</span><span class="token punctuation">:</span> 192.168.1.1
    <span class="token key atrule">security</span><span class="token punctuation">:</span>
        <span class="token key atrule">username</span><span class="token punctuation">:</span> admin
        <span class="token key atrule">roles</span><span class="token punctuation">:</span>
          <span class="token punctuation">-</span> USER
          <span class="token punctuation">-</span> ADMIN

<span class="token comment"># additional configuration as required</span>
</code></pre>
<p>要使用 <code>@ConfigurationProperties</code> bean，您可以使用与其他 bean 相同的方式注入它们，如下所示：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Service</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyService</span> <span class="token punctuation">{</span>

    <span class="token keyword">private</span> <span class="token keyword">final</span> <span class="token class-name">AcmeProperties</span> properties<span class="token punctuation">;</span>

    <span class="token annotation punctuation">@Autowired</span>
    <span class="token keyword">public</span> <span class="token class-name">MyService</span><span class="token punctuation">(</span><span class="token class-name">AcmeProperties</span> properties<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>properties <span class="token operator">=</span> properties<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

     <span class="token comment">//...</span>

    <span class="token annotation punctuation">@PostConstruct</span>
    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">openConnection</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token class-name">Server</span> server <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">Server</span><span class="token punctuation">(</span><span class="token keyword">this</span><span class="token punctuation">.</span>properties<span class="token punctuation">.</span><span class="token function">getRemoteAddress</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token comment">// ...</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p><strong>提示</strong></p>
<blockquote>
<p>使用 <code>@ConfigurationProperties</code> 还可以生成元数据文件，IDE 可以通过这些文件来为您自己的 key 提供自动完成功能。有关详细信息，请参阅<a href="https://docs.spring.io/spring-boot/docs/2.1.1.RELEASE/reference/htmlsingle/#configuration-metadata" target="_blank">附录 B：配置元数据</a>。</p>
</blockquote>
<p><a id="boot-features-external-config-3rd-party-configuration"></a></p>
<h4 id="2481、第三方配置">24.8.1、第三方配置</h4>
<p><code>@ConfigurationProperties</code> 除了可以使用来注解类之外，您还可以在公共的 @Bean 方法上使用。当您想要将属性绑定到您掌控之外的第三方组件时，这样做特别有用。</p>
<p>要使用 <code>Environment</code> 属性配置 bean，请将 <code>@ConfigurationProperties</code> 添加到 bean 注册上，如下所示：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@ConfigurationProperties</span><span class="token punctuation">(</span>prefix <span class="token operator">=</span> <span class="token string">"another"</span><span class="token punctuation">)</span>
<span class="token annotation punctuation">@Bean</span>
<span class="token keyword">public</span> <span class="token class-name">AnotherComponent</span> <span class="token function">anotherComponent</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
<span class="token punctuation">}</span>
</code></pre>
<p>使用 <code>another</code> 前缀定义的所有属性都使用与前面的 <code>AcmeProperties</code> 示例类似的方式映射到 <code>AnotherComponent</code> bean。</p>
<p><a id="boot-features-external-config-relaxed-binding"></a></p>
<h4 id="2482、宽松绑定">24.8.2、宽松绑定</h4>
<p>Spring Boot 使用一些宽松的规则将 <code>Environment</code> 属性绑定到 <code>@ConfigurationProperties</code> bean，因此 <code>Environment</code> 属性名不需要和 bean 属性名精确匹配。常见的示例包括使用了 <code>-</code> 符号分割的环境属性（例如，<code>context-path</code> 绑定到 <code>contextPath</code>）和大写环境属性（例如，<code>PORT</code> 绑定到 <code>port</code>）。</p>
<p>如下 <code>@ConfigurationProperties</code> 类：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@ConfigurationProperties</span><span class="token punctuation">(</span>prefix<span class="token operator">=</span><span class="token string">"acme.my-project.person"</span><span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">OwnerProperties</span> <span class="token punctuation">{</span>

    <span class="token keyword">private</span> <span class="token class-name">String</span> firstName<span class="token punctuation">;</span>

    <span class="token keyword">public</span> <span class="token class-name">String</span> <span class="token function">getFirstName</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> <span class="token keyword">this</span><span class="token punctuation">.</span>firstName<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">setFirstName</span><span class="token punctuation">(</span><span class="token class-name">String</span> firstName<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>firstName <span class="token operator">=</span> firstName<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>在上述示例中，同样可以使用以下属性名称：</p>
<p><strong>表 24.1、宽松绑定</strong></p>
<table>
<thead>
<tr>
<th>属性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>acme.my-project.person.first-name</code></td>
<td>Kebab 风格（短横线命名），建议在 <code>.properties</code> 和 <code>.yml</code> 文件中使用。</td>
</tr>
<tr>
<td><code>acme.myProject.person.firstName</code></td>
<td>标准驼峰式风格。</td>
</tr>
<tr>
<td><code>acme.my_project.person.first_name</code></td>
<td>下划线表示法，<code>.properties</code> 和 <code>.yaml</code> 文件中的另外一种格式。</td>
</tr>
<tr>
<td><code>ACME_MYPROJECT_PERSON_FIRSTNAME</code></td>
<td>大写风格，当使用系统环境变量时推荐使用该风格。</td>
</tr>
</tbody>
</table>
<p><strong>注意</strong></p>
<blockquote>
<p>注解的 <code>prefix</code> 值必须是 kebab (短横线命名)风格（小写并用 <code>-</code> 分隔，例如 <code>acme.my-project.person</code>）。</p>
</blockquote>
<p><strong>表 24.2、每种属性源（property source）的宽松绑定规则</strong></p>
<table>
<thead>
<tr>
<th>属性源</th>
<th>简单类型</th>
<th>列表集合类型</th>
</tr>
</thead>
<tbody>
<tr>
<td>properties 文件</td>
<td>驼峰式、短横线式或下划线式</td>
<td>标准列表语法使用 <code>[]</code> 或逗号分隔值</td>
</tr>
<tr>
<td>YAML 文件</td>
<td>驼峰式、短横线式或者下划线式</td>
<td>标准 YAML 列表语法或者逗号分隔值</td>
</tr>
<tr>
<td>环境变量</td>
<td>大写并且以下划线作为定界符，<code>_</code> 不能放在属性名之间使用</td>
<td>数字值两边使用下划线连接，例如 <code>MY_ACME_1_OTHER = my.acme[1].other</code></td>
</tr>
<tr>
<td>系统属性</td>
<td>驼峰式、短横线式或者下划线式</td>
<td>标准列表语法使用 <code>[]</code> 或逗号分隔值</td>
</tr>
</tbody>
</table>
<p><strong>提示</strong></p>
<blockquote>
<p>我们建议，属性尽可能以小写的短横线格式存储，比如 <code>my.property-name=acme</code>。</p>
</blockquote>
<p>当绑定到 <code>Map</code> 属性时，如果 key 包含除小写字母数字字符或 <code>-</code> 以外的任何内容，则需要使用括号表示法来保留原始值。如果 key 没有使用 <code>[]</code> 包裹，则里面的任何非字母数字字符或 <code>-</code> 的字符都将被删除。例如，将以下属性绑定到一个 <code>Map</code>：</p>
<pre class="language-"><code class="lang-yaml"><span class="token key atrule">acme</span><span class="token punctuation">:</span>
  <span class="token key atrule">map</span><span class="token punctuation">:</span>
    "<span class="token punctuation">[</span>/key1<span class="token punctuation">]</span>"<span class="token punctuation">:</span> value1
    "<span class="token punctuation">[</span>/key2<span class="token punctuation">]</span>"<span class="token punctuation">:</span> value2
    <span class="token key atrule">/key3</span><span class="token punctuation">:</span> value3
</code></pre>
<p>上面的属性将绑定到一个 <code>Map</code> 上，其中 <code>/key1</code>，<code>/key2</code> 和 <code>key3</code> 作为 map 的 key。</p>
<p><a id="boot-features-external-config-complex-type-merge"></a></p>
<h4 id="2483、合并复杂类型">24.8.3、合并复杂类型</h4>
<p>当列表集合（list）在多个地方配置时，整个列表集合将被替换。</p>
<p>例如，假设带有 <code>name</code> 和 <code>description</code> 属性的 <code>MyPojo</code> 对象默认为 <code>null</code>。以下示例中，<code>AcmeProperties</code> 暴露了一个 <code>MyPojo</code> 对象列表集合：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@ConfigurationProperties</span><span class="token punctuation">(</span><span class="token string">"acme"</span><span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">AcmeProperties</span> <span class="token punctuation">{</span>

    <span class="token keyword">private</span> <span class="token keyword">final</span> <span class="token class-name">List</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">MyPojo</span><span class="token punctuation">&gt;</span></span> list <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">ArrayList</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token punctuation">&gt;</span></span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

    <span class="token keyword">public</span> <span class="token class-name">List</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">MyPojo</span><span class="token punctuation">&gt;</span></span> <span class="token function">getList</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> <span class="token keyword">this</span><span class="token punctuation">.</span>list<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>配置可以如下：</p>
<pre class="language-"><code class="lang-yaml"><span class="token key atrule">acme</span><span class="token punctuation">:</span>
  <span class="token key atrule">list</span><span class="token punctuation">:</span>
    <span class="token punctuation">-</span> <span class="token key atrule">name</span><span class="token punctuation">:</span> my name
      <span class="token key atrule">description</span><span class="token punctuation">:</span> my description
<span class="token punctuation">---</span>
<span class="token key atrule">spring</span><span class="token punctuation">:</span>
  <span class="token key atrule">profiles</span><span class="token punctuation">:</span> dev
<span class="token key atrule">acme</span><span class="token punctuation">:</span>
  <span class="token key atrule">list</span><span class="token punctuation">:</span>
    <span class="token punctuation">-</span> <span class="token key atrule">name</span><span class="token punctuation">:</span> my another name
</code></pre>
<p>如果 <code>dev</code> 配置文件未激活，则 <code>AcmeProperties.list</code> 只包含一条 <code>MyPojo</code> 条目，如之前所述。但是，如果激活了 <code>dev</code> 配置文件，列表集合仍然只包含一个条目（<code>name</code> 属性值为 <code>my another name</code>，<code>description</code> 为 <code>null</code>）。此配置不会向列表集合中添加第二个 <code>MyPojo</code> 实例，也不会合并条目。</p>
<p>在多个配置文件中指定一个 <code>List</code> 时，最高优先级（并且只有一个）的列表集合将被使用。可做如下配置：</p>
<pre class="language-"><code class="lang-yaml"><span class="token key atrule">acme</span><span class="token punctuation">:</span>
  <span class="token key atrule">list</span><span class="token punctuation">:</span>
    <span class="token punctuation">-</span> <span class="token key atrule">name</span><span class="token punctuation">:</span> my name
      <span class="token key atrule">description</span><span class="token punctuation">:</span> my description
    <span class="token punctuation">-</span> <span class="token key atrule">name</span><span class="token punctuation">:</span> another name
      <span class="token key atrule">description</span><span class="token punctuation">:</span> another description
<span class="token punctuation">---</span>
<span class="token key atrule">spring</span><span class="token punctuation">:</span>
  <span class="token key atrule">profiles</span><span class="token punctuation">:</span> dev
<span class="token key atrule">acme</span><span class="token punctuation">:</span>
  <span class="token key atrule">list</span><span class="token punctuation">:</span>
    <span class="token punctuation">-</span> <span class="token key atrule">name</span><span class="token punctuation">:</span> my another name
</code></pre>
<p>在前面示例中，如果 <code>dev</code> 配置文件处于活动状态，则 <code>AcmeProperties.list</code> 包含一个 <code>MyPojo</code> 条目（<code>name</code> 为 <code>my another name</code>，<code>description</code> 为 <code>null</code>）。对于 YAML 而言，逗号分隔的列表和YAML 列表同样会完全覆盖列表集合的内容。</p>
<p>对于 <code>Map</code> 属性，您可以绑定来自多个源中提取的属性值。但是，对于多个源中的相同属性，则使用高优先级最高的属性。以下示例从 <code>AcmeProperties</code> 暴露了一个 <code>Map<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>String,</span> <span class="token attr-name">MyPojo</span><span class="token punctuation">&gt;</span></span></code>：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@ConfigurationProperties</span><span class="token punctuation">(</span><span class="token string">"acme"</span><span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">AcmeProperties</span> <span class="token punctuation">{</span>

    <span class="token keyword">private</span> <span class="token keyword">final</span> <span class="token class-name">Map</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">String</span><span class="token punctuation">,</span> <span class="token class-name">MyPojo</span><span class="token punctuation">&gt;</span></span> map <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">HashMap</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token punctuation">&gt;</span></span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

    <span class="token keyword">public</span> <span class="token class-name">Map</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">String</span><span class="token punctuation">,</span> <span class="token class-name">MyPojo</span><span class="token punctuation">&gt;</span></span> <span class="token function">getMap</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> <span class="token keyword">this</span><span class="token punctuation">.</span>map<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>可以考虑以下配置：</p>
<pre class="language-"><code class="lang-yaml"><span class="token key atrule">acme</span><span class="token punctuation">:</span>
  <span class="token key atrule">map</span><span class="token punctuation">:</span>
    <span class="token key atrule">key1</span><span class="token punctuation">:</span>
      <span class="token key atrule">name</span><span class="token punctuation">:</span> my name 1
      <span class="token key atrule">description</span><span class="token punctuation">:</span> my description 1
<span class="token punctuation">---</span>
<span class="token key atrule">spring</span><span class="token punctuation">:</span>
  <span class="token key atrule">profiles</span><span class="token punctuation">:</span> dev
<span class="token key atrule">acme</span><span class="token punctuation">:</span>
  <span class="token key atrule">map</span><span class="token punctuation">:</span>
    <span class="token key atrule">key1</span><span class="token punctuation">:</span>
      <span class="token key atrule">name</span><span class="token punctuation">:</span> dev name 1
    <span class="token key atrule">key2</span><span class="token punctuation">:</span>
      <span class="token key atrule">name</span><span class="token punctuation">:</span> dev name 2
      <span class="token key atrule">description</span><span class="token punctuation">:</span> dev description 2
</code></pre>
<p>如果 <code>dev</code> 配置文件未激活，则 <code>AcmeProperties.map</code> 只包含一个带 <code>key1</code> key 的条目（<code>name</code> 为 <code>my name 1</code>，<code>description</code> 为 <code>my description 1</code>）。但是，如果激活了 dev 配置文件，则 <code>map</code> 将包含两个条目， key 分别为 <code>key1</code>（<code>name</code> 为 <code>dev name 1</code> 和 <code>description</code> 为 <code>my description 1</code>）和 <code>key2</code>（<code>name</code> 为 <code>dev name 2</code> 和 <code>description</code> 为 <code>dev description 2</code>）。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>前面的合并规则适用于所有不同属性源的属性，而不仅仅是 YAML 文件。</p>
</blockquote>
<p><a id="boot-features-external-config-conversion"></a></p>
<h4 id="2484、属性转换">24.8.4、属性转换</h4>
<p>当外部应用程序属性（application properties） 绑定到 <code>@ConfigurationProperties</code> bean 时，Spring Boot 会尝试将其属性强制转换为正确的类型。如果需要自定义类型转换，可以提供 <code>ConversionService</code> bean（名为 <code>conversionService</code> 的 bean）或自定义属性编辑器（通过 <code>CustomEditorConfigurer</code> bean）或自定义转换器（带有注解为 <code>@ConfigurationPropertiesBinding</code> 的 bean 定义）。</p>
<p><strong>注意</strong></p>
<p>由于该 bean 在应用程序生命周期早期就被请求 ，因此请限制 <code>ConversionService</code> 使用的依赖。您在创建时可能无法完全初始化所需的依赖。如果配置 key 为非强制需要，您可能希望重命名自定义的 <code>ConversionService</code>，并仅依赖于使用 <code>@ConfigurationPropertiesBinding</code> 限定的自定义转换器。</p>
<p><a id="boot-features-external-config-conversion-duration"></a></p>
<h5 id="转换-duration">转换 duration</h5>
<p>Spring Boot 支持持续时间（duration）表达。如果您暴露一个 <code>java.time.Duration</code> 属性，则可以在应用程序属性中使用以下格式：</p>
<ul>
<li>常规 <code>long</code> 表示（除非指定 <code>@DurationUnit</code>，否则使用毫秒作为默认单位）</li>
<li><a href="https://docs.oracle.com/javase/8/docs/api//java/time/Duration.html#parse-java.lang.CharSequence-" target="_blank"><code>java.util.Duration</code></a> 使用的标准 ISO-8601 格式</li>
<li>一种更易读的格式，值和单位在一起（例如 <code>10s</code> 表示 10 秒）</li>
</ul>
<p>思考以下示例：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@ConfigurationProperties</span><span class="token punctuation">(</span><span class="token string">"app.system"</span><span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">AppSystemProperties</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@DurationUnit</span><span class="token punctuation">(</span><span class="token class-name">ChronoUnit</span><span class="token punctuation">.</span>SECONDS<span class="token punctuation">)</span>
    <span class="token keyword">private</span> <span class="token class-name">Duration</span> sessionTimeout <span class="token operator">=</span> <span class="token class-name">Duration</span><span class="token punctuation">.</span><span class="token function">ofSeconds</span><span class="token punctuation">(</span><span class="token number">30</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

    <span class="token keyword">private</span> <span class="token class-name">Duration</span> readTimeout <span class="token operator">=</span> <span class="token class-name">Duration</span><span class="token punctuation">.</span><span class="token function">ofMillis</span><span class="token punctuation">(</span><span class="token number">1000</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

    <span class="token keyword">public</span> <span class="token class-name">Duration</span> <span class="token function">getSessionTimeout</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> <span class="token keyword">this</span><span class="token punctuation">.</span>sessionTimeout<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">setSessionTimeout</span><span class="token punctuation">(</span><span class="token class-name">Duration</span> sessionTimeout<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>sessionTimeout <span class="token operator">=</span> sessionTimeout<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token class-name">Duration</span> <span class="token function">getReadTimeout</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> <span class="token keyword">this</span><span class="token punctuation">.</span>readTimeout<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">setReadTimeout</span><span class="token punctuation">(</span><span class="token class-name">Duration</span> readTimeout<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>readTimeout <span class="token operator">=</span> readTimeout<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>指定一个会话超时时间为 30 秒，使用 <code>30</code>、<code>PT30S</code> 和 <code>30s</code> 等形式都是可以的。读取超时时间设置为 500ms，可以采用以下任何一种形式：<code>500</code>、<code>PT0.5S</code> 和 <code>500ms</code>。</p>
<p>您也可以使用任何支持的单位来标识：</p>
<ul>
<li><code>ns</code> 为纳秒</li>
<li><code>us</code> 为微秒</li>
<li><code>ms</code> 为毫秒</li>
<li><code>s</code> 为秒</li>
<li><code>m</code> 为分钟</li>
<li><code>h</code> 为小时</li>
<li><code>d</code> 为天</li>
</ul>
<p>默认单位是毫秒，可以使用 <code>@DurationUnit</code> 配合上面的单位示例重写。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>要从先前仅使用 <code>Long</code> 来表示持续时间的版本进行升级，如果切换到 <code>Duration</code> 时不是毫秒，请定义单位（使用 <code>@DurationUnit</code>）。这样做可以提供透明的升级路径，同时支持更丰富的格式。</p>
</blockquote>
<p><a id="boot-features-external-config-conversion-datasize"></a></p>
<h5 id="转换-data-size">转换 Data Size</h5>
<p>Spring Framework 有一个 <code>DataSize</code> 值类型，允许以字节表示大小。如果暴露一个 <code>DataSize</code> 属性，则可以在应用程序属性中使用以下格式：</p>
<ul>
<li>常规的 <code>Long</code> 表示（使用字节作为默认单位，除非指定了 <code>@DataSizeUnit</code>）</li>
<li>更具有可读性的格式，值和单位在一起（例如 <code>10MB</code> 表示 <code>10</code> 兆字节）</li>
</ul>
<p>请思考以下示例：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@ConfigurationProperties</span><span class="token punctuation">(</span><span class="token string">"app.io"</span><span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">AppIoProperties</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@DataSizeUnit</span><span class="token punctuation">(</span><span class="token class-name">DataUnit</span><span class="token punctuation">.</span>MEGABYTES<span class="token punctuation">)</span>
    <span class="token keyword">private</span> <span class="token class-name">DataSize</span> bufferSize <span class="token operator">=</span> <span class="token class-name">DataSize</span><span class="token punctuation">.</span><span class="token function">ofMegabytes</span><span class="token punctuation">(</span><span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

    <span class="token keyword">private</span> <span class="token class-name">DataSize</span> sizeThreshold <span class="token operator">=</span> <span class="token class-name">DataSize</span><span class="token punctuation">.</span><span class="token function">ofBytes</span><span class="token punctuation">(</span><span class="token number">512</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

    <span class="token keyword">public</span> <span class="token class-name">DataSize</span> <span class="token function">getBufferSize</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> <span class="token keyword">this</span><span class="token punctuation">.</span>bufferSize<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">setBufferSize</span><span class="token punctuation">(</span><span class="token class-name">DataSize</span> bufferSize<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>bufferSize <span class="token operator">=</span> bufferSize<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token class-name">DataSize</span> <span class="token function">getSizeThreshold</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> <span class="token keyword">this</span><span class="token punctuation">.</span>sizeThreshold<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">setSizeThreshold</span><span class="token punctuation">(</span><span class="token class-name">DataSize</span> sizeThreshold<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>sizeThreshold <span class="token operator">=</span> sizeThreshold<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>要指定 10 兆字节的缓冲大小，使用 <code>10</code> 和 <code>10MB</code> 是等效的。256 字节的大小可以指定为 <code>256</code> 或 <code>256B</code>。</p>
<p>您也可以使用任何支持的单位：</p>
<ul>
<li><code>B</code> 表示字节</li>
<li><code>KB</code> 为千字节</li>
<li><code>MB</code> 为兆字节</li>
<li><code>GB</code> 为千兆字节</li>
<li><code>TB</code> 为兆兆字节</li>
</ul>
<p>默认单位是字节，可以使用 <code>@DataSizeUnit</code> 配合上面的示例单位重写。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>要从先前仅使用 <code>Long</code> 来表示大小的版本进行升级，请确保在切换到 <code>DataSize</code> 不是字节的情况下定义单位（使用 <code>@DataSizeUnit</code>）。这样做可以提供透明的升级路径，同时支持更丰富的格式。</p>
</blockquote>
<p><a id="boot-features-external-config-validation"></a></p>
<h4 id="2485、configurationproperties-验证">24.8.5、@ConfigurationProperties 验证</h4>
<p>只要使用了 Spring 的 <code>@Validated</code> 注解，Spring Boot 就会尝试验证 <code>@ConfigurationProperties</code> 类。您可以直接在配置类上使用 JSR-303 <code>javax.validation</code> 约束注解。为此，请确保 JSR-303 实现在 classpath 上，然后将约束注解添加到字段上，如下所示：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@ConfigurationProperties</span><span class="token punctuation">(</span>prefix<span class="token operator">=</span><span class="token string">"acme"</span><span class="token punctuation">)</span>
<span class="token annotation punctuation">@Validated</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">AcmeProperties</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@NotNull</span>
    <span class="token keyword">private</span> <span class="token class-name">InetAddress</span> remoteAddress<span class="token punctuation">;</span>

    <span class="token comment">// ... getters and setters</span>

<span class="token punctuation">}</span>
</code></pre>
<p><strong>提示</strong></p>
<blockquote>
<p>您还可以通过使用 <code>@Validated</code> 注解创建配置属性的 <code>@Bean</code> 方法来触发验证。</p>
</blockquote>
<p>虽然绑定时也会验证嵌套属性，但最好的做法还是将关联字段注解上 <code>@Valid</code>。这可确保即使未找到嵌套属性也会触发验证。以下示例基于前面的 <code>AcmeProperties</code> 示例：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@ConfigurationProperties</span><span class="token punctuation">(</span>prefix<span class="token operator">=</span><span class="token string">"acme"</span><span class="token punctuation">)</span>
<span class="token annotation punctuation">@Validated</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">AcmeProperties</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@NotNull</span>
    <span class="token keyword">private</span> <span class="token class-name">InetAddress</span> remoteAddress<span class="token punctuation">;</span>

    <span class="token annotation punctuation">@Valid</span>
    <span class="token keyword">private</span> <span class="token keyword">final</span> <span class="token class-name">Security</span> security <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">Security</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

    <span class="token comment">// ... getters and setters</span>

    <span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">class</span> <span class="token class-name">Security</span> <span class="token punctuation">{</span>

        <span class="token annotation punctuation">@NotEmpty</span>
        <span class="token keyword">public</span> <span class="token class-name">String</span> username<span class="token punctuation">;</span>

        <span class="token comment">// ... getters and setters</span>

    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>您还可以通过创建一个名为 <code>configurationPropertiesValidator</code> 的 bean 定义来添加自定义 Spring <code>Validator</code>。应该将 <code>@Bean</code> 方法声明为 <code>static</code>。配置属性验证器在应用程序生命周期的早期创建，将 <code>@Bean</code> 方法声明为 <code>static</code> 可以无需实例化 <code>@Configuration</code> 类来创建 bean。这样做可以避免早期实例化可能导致的意外问题。这里有一个<a href="https://github.com/spring-projects/spring-boot/tree/v2.1.1.RELEASE/spring-boot-samples/spring-boot-sample-property-validation" target="_blank">属性验证示例</a>，讲解了如何设置。</p>
<p><strong>提示</strong></p>
<blockquote>
<p><code>spring-boot-actuator</code> 模块包括一个暴露所有 <code>@ConfigurationProperties</code> bean 的端点。可将 Web 浏览器指向 <code>/actuator/configprops</code> 或使用等效的 JMX 端点。有关详细信息，请参阅<a href="#production-ready-endpoints">生产就绪功能</a>部分。</p>
</blockquote>
<p><a id="boot-features-external-config-vs-value"></a></p>
<h4 id="2486、configurationproperties-与-value-对比">24.8.6、@ConfigurationProperties 与 @Value 对比</h4>
<p><code>@Value</code> 注解是核心容器功能，它不提供与类型安全配置属性相同的功能。下表总结了 <code>@ConfigurationProperties</code> 和 <code>@Value</code> 支持的功能：</p>
<table>
<thead>
<tr>
<th>功能</th>
<th><code>@ConfigurationProperties</code></th>
<th><code>@Value</code></th>
</tr>
</thead>
<tbody>
<tr>
<td><a href="#boot-features-external-config-relaxed-binding">宽松绑定</a></td>
<td>是</td>
<td>否</td>
</tr>
<tr>
<td><a href="#configuration-metadata">元数据支持</a></td>
<td>是</td>
<td>否</td>
</tr>
<tr>
<td><code>SpEL</code> 表达式</td>
<td>否</td>
<td>是</td>
</tr>
</tbody>
</table>
<p>如果您要为自己的组件定义一组配置 key，我们建议您将它们分组到使用 <code>@ConfigurationProperties</code> 注解的 POJO 中。您应该知道，由于 <code>@Value</code> 不支持宽松绑定，因此如果您需要通过环境变量来提供值，它并不是一个好的选择。</p>
<p>最后，虽然您可以在 <code>@Value</code> 中编写 <code>SpEL</code> 表达式，但来自应用程序属性文件的此类表达式并不会被处理。</p>
<p><a id="boot-features-profiles"></a></p>
<h2 id="25、profile">25、Profile</h2>
<p>Spring Profile 提供了一种应用程序配置部分隔离并使其仅在特定环境中可用的方法。可以使用 <code>@Profile</code> 来注解任何 <code>@Component</code> 或 <code>@Configuration</code> 以指定何时加载它，如下所示：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Configuration</span>
<span class="token annotation punctuation">@Profile</span><span class="token punctuation">(</span><span class="token string">"production"</span><span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">ProductionConfiguration</span> <span class="token punctuation">{</span>

    <span class="token comment">// ...</span>

<span class="token punctuation">}</span>
</code></pre>
<p>您可以使用 <code>spring.profiles.active</code> <code>Environment</code> 属性指定哪些配置文件处于激活状态。您可以使用本章前面介绍的任何方法指定属性。例如，您可以将其包含在 <code>application.properties</code> 中，如下所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.profiles.active</span><span class="token attr-value"><span class="token punctuation">=</span>dev,hsqldb</span>
</code></pre>
<p>您还可以在命令行上使用以下开关指定它：<code>--spring.profiles.active=dev,hsqldb</code>。</p>
<p><a id="boot-features-adding-active-profiles"></a></p>
<h3 id="251、添加激活-profile">25.1、添加激活 Profile</h3>
<p><code>spring.profiles.active</code> 属性遵循与其他属性相同的排序规则：应用优先级最高的 <code>PropertySource</code>。这意味着您可以在 <code>application.properties</code> 中指定激活配置文件，然后使用命令行开关<strong>替换</strong>它们。</p>
<p>有时，将特定 profile 的属性<strong>添加</strong>到激活配置文件而不是替换它们，这种方式也是很有用的。<code>spring.profiles.include</code> 属性可无条件地添加激活配置文件。<code>SpringApplication</code> 入口还有一个 Java API，用于设置其他 profile（即，在 <code>spring.profiles.active</code> 属性激活的 profile 之上）。请参阅SpringApplication 中的 <code>setAdditionalProfiles()</code> 方法。</p>
<p>例如，当使用开关 <code>--spring.profiles.active=prod</code> 运行有以下属性的应用程序时，<code>proddb</code> 和 <code>prodmq</code> 配置文件也会被激活：</p>
<pre class="language-"><code class="lang-yaml"><span class="token punctuation">---</span>
<span class="token key atrule">my.property</span><span class="token punctuation">:</span> fromyamlfile
<span class="token punctuation">---</span>
<span class="token key atrule">spring.profiles</span><span class="token punctuation">:</span> prod
<span class="token key atrule">spring.profiles.include</span><span class="token punctuation">:</span>
  <span class="token punctuation">-</span> proddb
  <span class="token punctuation">-</span> prodmq
</code></pre>
<p><strong>注意</strong></p>
<blockquote>
<p>请记住，可以在 YAML 文档中定义 <code>spring.profiles</code> 属性，以确定此特定文档何时包含在配置中。有关更多详细信息，请参见第 77.7 章节：<a href="howto.md#howto-change-configuration-depending-on-the-environment">根据环境更改配置</a>。</p>
</blockquote>
<p><a id="boot-features-programmatically-setting-profiles"></a></p>
<h3 id="252、以编程方式设置-profile">25.2、以编程方式设置 Profile</h3>
<p>您可以在应用程序运行之前以编程方式通过调用 <code>SpringApplication.setAdditionalProfiles(...)</code> 设置激活 profile。也可以使用 Spring 的 <code>ConfigurableEnvironment</code> 接口激活 profile。</p>
<p><a id="boot-features-profile-specific-configuration"></a></p>
<h3 id="253、特定-profile-的配置文件">25.3、特定 Profile 的配置文件</h3>
<p>特定 profile 的 <code>application.properties</code>（或 <code>application.yml</code>）和通过 <code>@ConfigurationProperties</code> 引用的文件被当做文件并加载。有关详细信息，请参见<a href="#boot-features-external-config-profile-specific-properties">第 24.4 章节：特定 Profile 的属性文件</a>。</p>
<p><a id="boot-features-logging"></a></p>
<h2 id="26、日志记录">26、日志记录</h2>
<p>Spring Boot 使用 <a href="https://commons.apache.org/logging" target="_blank">Commons Logging</a> 记录所有内部日志，但开放日志的底层实现。其为 <a href="https://docs.oracle.com/javase/8/docs/api//java/util/logging/package-summary.html" target="_blank">Java Util Logging
</a>、<a href="https://logging.apache.org/log4j/2.x/" target="_blank">Log4J2</a> 和 <a href="http://logback.qos.ch/" target="_blank">Logback</a> 提供了默认配置。在每种情况下，日志记录器都预先配置为使用控制台输出，并且还提供可选的文件输出。</p>
<p>默认情况下，如果您使用了 <strong>Starter</strong>，则使用 Logback 进行日志记录。还包括合适的 Logback 路由，以确保在使用 Java Util Logging、Commons Logging、Log4J 或 SLF4J 的依赖库都能正常工作。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>Java 有很多日志框架可供使用。如果以上列表让您感到困惑，请不要担心。通常，您不需要更改日志依赖，并且 Spring Boot 提供的默认配置可以保证日志正常工作。</p>
</blockquote>
<p><a id="boot-features-logging-format"></a></p>
<h3 id="261、日志格式">26.1、日志格式</h3>
<p>Spring Boot 默认日志输出类似于以下示例：</p>
<pre class="language-"><code>2014-03-05 10:57:51.112  INFO 45469 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet Engine: Apache Tomcat/7.0.52
2014-03-05 10:57:51.253  INFO 45469 --- [ost-startStop-1] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2014-03-05 10:57:51.253  INFO 45469 --- [ost-startStop-1] o.s.web.context.ContextLoader            : Root WebApplicationContext: initialization completed in 1358 ms
2014-03-05 10:57:51.698  INFO 45469 --- [ost-startStop-1] o.s.b.c.e.ServletRegistrationBean        : Mapping servlet: 'dispatcherServlet' to [/]
2014-03-05 10:57:51.702  INFO 45469 --- [ost-startStop-1] o.s.b.c.embedded.FilterRegistrationBean  : Mapping filter: 'hiddenHttpMethodFilter' to: [/*]
</code></pre><p>输出以下项：</p>
<ul>
<li>日期和时间：毫秒精度，易于排序。</li>
<li>日志级别：<code>ERROR</code>、<code>WARN</code>、<code>INFO</code>、<code>DEBUG</code> 或 <code>TRACE</code>。</li>
<li>进程 ID。</li>
<li>一个 <code>---</code> 分隔符，用于区分实际日志内容的开始。</li>
<li>线程名称：在方括号中（可能会截断控制台输出）。</li>
<li>日志记录器名称：这通常是源类名称（通常为缩写）。</li>
<li>日志内容。</li>
</ul>
<p><strong>注意</strong></p>
<blockquote>
<p>Logback 没有 <code>FATAL</code> 级别。该级别映射到 <code>ERROR</code>。</p>
</blockquote>
<p><a id="boot-features-logging-console-output"></a></p>
<h3 id="262、控制台输出">26.2、控制台输出</h3>
<p>默认日志配置会在写入时将消息回显到控制台。默认情况下，会记录 <code>ERROR</code>、<code>WARN</code> 和 <code>INFO</code> 级别的日志。您还可以通过使用 <code>--debug</code> 标志启动应用程序来启用<strong>调试</strong>模式。</p>
<pre class="language-"><code class="lang-bash">$ java -jar myapp.jar --debug
</code></pre>
<p><strong>注意</strong></p>
<blockquote>
<p>您还可以在 <code>application.properties</code> 中指定 <code>debug=true</code>。</p>
</blockquote>
<p>启用调试模式后，核心日志记录器（内嵌容器、Hibernate 和 Spring Boot）将被配置为输出更多日志信息。启用调试模式不会将应用程序配置为使用 <code>DEBUG</code> 级别记录所有日志内容。</p>
<p>或者，您可以通过使用 <code>--trace</code> 标志（或在 <code>application.properties</code> 中的设置 <code>trace=true</code>）启动应用程序来启用<strong>跟踪</strong>模式。这样做可以为选择的核心日志记录器（内嵌容器、Hibernate 模式生成和整个 Spring 组合）启用日志追踪。</p>
<p><a id="boot-features-logging-color-coded-output"></a></p>
<h3 id="2621、着色输出">26.2.1、着色输出</h3>
<p>如果您的终端支持 ANSI，则可以使用颜色输出来提高可读性。您可以将 <code>spring.output.ansi.enabled</code> 设置为<a href="https://docs.spring.io/spring-boot/docs/2.1.1.RELEASE/api/org/springframework/boot/ansi/AnsiOutput.Enabled.html" target="_blank">受支持的值</a>以覆盖自动检测。</p>
<p>可使用 <code>％clr</code> 转换字配置颜色编码。最简单形式是，转换器根据日志级别对输出进行着色，如下所示：</p>
<pre class="language-"><code>%clr(%5p)
</code></pre><p>下表描述日志级别与颜色的映射关系：</p>
<table>
<thead>
<tr>
<th>级别</th>
<th>颜色</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>FATAL</code></td>
<td>红（Red）</td>
</tr>
<tr>
<td><code>ERROR</code></td>
<td>红（Red）</td>
</tr>
<tr>
<td><code>WARN</code></td>
<td>黄（Yellow）</td>
</tr>
<tr>
<td><code>INFO</code></td>
<td>绿（Green）</td>
</tr>
<tr>
<td><code>DEBUG</code></td>
<td>绿（Green）</td>
</tr>
<tr>
<td><code>TRACE</code></td>
<td>绿（Green）</td>
</tr>
</tbody>
</table>
<p>或者，您可以通过将其作为转换选项指定应使用的颜色或样式。例如，要将文本变为黄色，请使用以下设置：</p>
<pre class="language-"><code>%clr(%d{yyyy-MM-dd HH:mm:ss.SSS}){yellow}
</code></pre><p>支持以下颜色和样式：</p>
<ul>
<li><code>blue</code></li>
<li><code>cyan</code></li>
<li><code>faint</code></li>
<li><code>green</code></li>
<li><code>magenta</code></li>
<li><code>red</code></li>
<li><code>yellow</code></li>
</ul>
<p><a id="boot-features-logging-file-output"></a></p>
<h3 id="263、文件输出">26.3、文件输出</h3>
<p>默认情况下，Spring Boot 仅记录到控制台，不会写入日志文件。想除了控制台输出之外还要写入日志文件，则需要设置 <code>logging.file</code> 或 <code>logging.path</code> 属性（例如，在 <code>application.properties</code> 中）。</p>
<p>下表展示了如何与 <code>logging.*</code> 属性一起使用：</p>
<p><strong>表 26.1、Logging 属性</strong></p>
<table>
<thead>
<tr>
<th><code>logging.file</code></th>
<th><code>logging.path</code></th>
<th>示例</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr>
<td>（无）</td>
<td>（无）</td>
<td></td>
<td>仅在控制台输出</td>
</tr>
<tr>
<td>指定文件</td>
<td>(无)</td>
<td><code>my.log</code></td>
<td>写入指定的日志文件。名称可以是绝对位置或相对于当前目录。</td>
</tr>
<tr>
<td>（无）</td>
<td>指定目录</td>
<td><code>/var/log</code></td>
<td>将 <code>spring.log</code> 写入指定的目录。名称可以是绝对位置或相对于当前目录。</td>
</tr>
</tbody>
</table>
<p>日志文件在达到 10MB 时会轮转，并且与控制台输出一样，默认情况下会记录 <code>ERROR</code>、<code>WARN</code> 和 <code>INFO</code> 级别的内容。可以使用 <code>logging.file.max-size</code> 属性更改大小限制。除非已设置 <code>logging.file.max-history</code> 属性，否则以前轮转的文件将无限期归档。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>日志记录系统在应用程序生命周期的早期开始初始化。因此，通过 <code>@PropertySource</code> 注解加载的属性文件中是找不到日志属性的。</p>
</blockquote>
<p><strong>提示</strong></p>
<blockquote>
<p>日志属性独立于实际的日志底层。因此，spring Boot 不管理特定的配置 key（例如 Logback 的 <code>logback.configurationFile</code>）。</p>
</blockquote>
<p><a id="boot-features-custom-log-levels"></a></p>
<h3 id="264、日志等级">26.4、日志等级</h3>
<p>所有受支持的日志记录系统都可以使用 <code>logging.level.<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>logger-name</span><span class="token punctuation">&gt;</span></span>=<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>level</span><span class="token punctuation">&gt;</span></span></code> 来设置 Spring <code>Environment</code> 中的记录器等级（例如，在 <code>application.properties</code> 中）。其中 <code>level</code> 是 TRACE、DEBUG、INFO、WARN、ERROR、FATAL 和 OFF 其中之一。可以使用 <code>logging.level.root</code> 配置 <code>root</code> 记录器。</p>
<p>以下示例展示了 <code>application.properties</code> 中默认的日志记录设置：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">logging.level.root</span><span class="token attr-value"><span class="token punctuation">=</span>WARN</span>
<span class="token constant">logging.level.org.springframework.web</span><span class="token attr-value"><span class="token punctuation">=</span>DEBUG</span>
<span class="token constant">logging.level.org.hibernate</span><span class="token attr-value"><span class="token punctuation">=</span>ERROR</span>
</code></pre>
<p><a id="boot-features-custom-log-groups"></a></p>
<h3 id="265、日志组">26.5、日志组</h3>
<p>将相关记录器组合在一起以便可以同时配置，这通常很有用。例如，您可以更改<strong>所有</strong> Tomcat 相关记录器的日志记录级别，但您无法轻松记住顶层的包名。</p>
<p>为了解决这个问题，Spring Boot 允许您在 Spring <code>Environment</code> 中定义日志记录组。例如，以下通过将 <strong>tomcat</strong> 组添加到 <code>application.properties</code> 来定义 <strong>tomcat</strong> 组：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">logging.group.tomcat</span><span class="token attr-value"><span class="token punctuation">=</span>org.apache.catalina, org.apache.coyote, org.apache.tomcat</span>
</code></pre>
<p>定义后，您可以使用一行配置来更改组中所有记录器的级别：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">logging.level.tomcat</span><span class="token attr-value"><span class="token punctuation">=</span>TRACE</span>
</code></pre>
<p>Spring Boot 包含以下预定义的日志记录组，可以直接使用：</p>
<table>
<thead>
<tr>
<th>名称</th>
<th>日志记录器</th>
</tr>
</thead>
<tbody>
<tr>
<td>web</td>
<td><code>org.springframework.core.codec</code>、<code>org.springframework.http</code>、<code>org.springframework.web</code></td>
</tr>
<tr>
<td>sql</td>
<td><code>org.springframework.jdbc.core</code>、<code>org.hibernate.SQL</code></td>
</tr>
</tbody>
</table>
<p><a id="boot-features-custom-log-configuration"></a></p>
<h3 id="266、自定义日志配置">26.6、自定义日志配置</h3>
<p>可以通过在 classpath 中引入适合的库来激活各种日志记录系统，并且可以通过在 classpath 的根目录中或在以下 Spring <code>Environment</code> 属性指定的位置提供合适的配置文件来进一步自定义：<code>logging.config</code>。</p>
<p>您可以使用 <code>org.springframework.boot.logging.LoggingSystem</code> 系统属性强制 Spring Boot 使用特定的日志记录系统。该值应该是一个实现了 <code>LoggingSystem</code> 的类的完全限定类名。您还可以使用 <code>none</code> 值完全禁用 Spring Boot 的日志记录配置。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>由于日志记录在创建 <code>ApplicationContext</code> 之前初始化，因此无法在 Spring <code>@Configuration</code> 文件中控制来自 <code>@PropertySources</code> 的日志记录。更改日志记录系统或完全禁用它的唯一方法是通过系统属性设置。</p>
</blockquote>
<p>根据您的日志记录系统，将加载以下文件：</p>
<table>
<thead>
<tr>
<th>日志记录系统</th>
<th>文件</th>
</tr>
</thead>
<tbody>
<tr>
<td>Logback</td>
<td><code>logback-spring.xml</code>、<code>logback-spring.groovy</code>、<code>logback.xml</code> 或者 <code>logback.groovy</code></td>
</tr>
<tr>
<td>Log4j2</td>
<td><code>log4j2-spring.xml</code> 或者 <code>log4j2.xml</code></td>
</tr>
<tr>
<td>JDK（Java Util Logging）</td>
<td><code>logging.properties</code></td>
</tr>
</tbody>
</table>
<p><strong>注意</strong></p>
<blockquote>
<p>如果可能，我们建议您使用 <code>-spring</code> 的形式来配置日志记录（比如 <code>logback-spring.xml</code> 而不是 <code>logback.xml</code>）。如果使用标准的配置位置，Spring 无法完全控制日志初始化。</p>
</blockquote>
<p><strong>警告</strong></p>
<blockquote>
<p>Java Util Logging 存在已知的类加载问题，这些问题在以<strong>可执行 jar</strong> 运行时会触发。如果可能的话，我们建议您在使用<strong>可执行 jar</strong> 方式运行时避免使用它。</p>
</blockquote>
<p>为了进行自定义，部分其他属性会从 Spring <code>Environment</code> 传输到 System 属性，如下表所述：</p>
<table>
<thead>
<tr>
<th>Spring Environment</th>
<th>系统属性</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>logging.exception-conversion-word</code></td>
<td><code>LOG_EXCEPTION_CONVERSION_WORD</code></td>
<td>记录异常时使用的转换字。</td>
</tr>
<tr>
<td><code>logging.file</code></td>
<td><code>LOG_FILE</code></td>
<td>如果已定义，则在默认日志配置中使用它。</td>
</tr>
<tr>
<td><code>logging.file.max-size</code></td>
<td><code>LOG_FILE_MAX_SIZE</code></td>
<td>最大日志文件大小（如果启用了 LOG_FILE）。（仅支持默认的 Logback 设置。）</td>
</tr>
<tr>
<td><code>logging.file.max-history</code></td>
<td><code>LOG_FILE_MAX_HISTORY</code></td>
<td>要保留的归档日志文件最大数量（如果启用了 LOG_FILE）。（仅支持默认的 Logback 设置。）</td>
</tr>
<tr>
<td><code>logging.path</code></td>
<td><code>LOG_PATH</code></td>
<td>如果已定义，则在默认日志配置中使用它。</td>
</tr>
<tr>
<td><code>logging.pattern.console</code></td>
<td><code>CONSOLE_LOG_PATTERN</code></td>
<td>要在控制台上使用的日志模式（stdout）。（仅支持默认的 Logback 设置。）</td>
</tr>
<tr>
<td><code>logging.pattern.dateformat</code></td>
<td><code>LOG_DATEFORMAT_PATTERN</code></td>
<td>日志日期格式的 Appender 模式。（仅支持默认的 Logback 设置。）</td>
</tr>
<tr>
<td><code>logging.pattern.file</code></td>
<td><code>FILE_LOG_PATTERN</code></td>
<td>要在文件中使用的日志模式（如果启用了 <code>LOG_FILE</code>）。（仅支持默认的 Logback 设置。）</td>
</tr>
<tr>
<td><code>logging.pattern.level</code></td>
<td><code>LOG_LEVEL_PATTERN</code></td>
<td>渲染日志级别时使用的格式（默认值为 <code>％5p</code>）。（仅支持默认的 Logback 设置。）</td>
</tr>
<tr>
<td><code>PID</code></td>
<td><code>PID</code></td>
<td>当前进程 ID（如果可能，则在未定义为 OS 环境变量时发现）。</td>
</tr>
</tbody>
</table>
<p>所有受支持的日志记录系统在解析其配置文件时都可以参考系统属性。有关示例，请参阅 <code>spring-boot.jar</code> 中的默认配置：</p>
<ul>
<li><a href="https://github.com/spring-projects/spring-boot/tree/v2.1.1.RELEASE/spring-boot-project/spring-boot/src/main/resources/org/springframework/boot/logging/logback/defaults.xml" target="_blank">Logback</a></li>
<li><a href="https://github.com/spring-projects/spring-boot/tree/v2.1.1.RELEASE/spring-boot-project/spring-boot/src/main/resources/org/springframework/boot/logging/log4j2/log4j2.xml" target="_blank">Log4j 2</a></li>
<li><a href="https://github.com/spring-projects/spring-boot/tree/v2.1.1.RELEASE/spring-boot-project/spring-boot/src/main/resources/org/springframework/boot/logging/java/logging-file.properties" target="_blank">Java Util logging</a></li>
</ul>
<p><strong>提示</strong></p>
<blockquote>
<p>如果要在日志记录属性中使用占位符，则应使用 <a href="#boot-features-external-config-placeholders-in-properties">Spring Boot 的语法</a>，而不是使用底层框架的语法。值得注意的是，如果使用 Logback，则应使用 <code>:</code> 作为属性名称与其默认值之间的分隔符，而不是使用 <code>:-</code>。</p>
</blockquote>
<p><strong>提示</strong></p>
<blockquote>

您可以通过仅覆盖 `LOG_LEVEL_PATTERN`（或带 Logback 的 `logging.pattern.level`）将 MDC 和其他特别的内容添加到日志行。例如，如果使用 `logging.pattern.level=user:%X{user} %5p`，则默认日志格式包含 **user** MDC 项（如果存在），如下所示:

```
2015-09-30 12:30:04.031 user:someone INFO 22174 --- [  nio-8080-exec-0] demo.Controller
Handling authenticated request
```

</blockquote>

<p><a id="boot-features-logback-extensions"></a></p>
<h3 id="267、logback-扩展">26.7、Logback 扩展</h3>
<p>Spring Boot 包含许多 Logback 扩展，可用于进行高级配置。您可以在 <code>logback-spring.xml</code> 配置文件中使用这些扩展。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>由于标准的 logback.xml 配置文件加载过早，因此无法在其中使用扩展。您需要使用 <code>logback-spring.xml</code> 或定义 <code>logging.config</code> 属性。</p>
</blockquote>
<p><strong>警告</strong></p>
<blockquote>
<p>扩展不能与 Logback 的<a href="http://logback.qos.ch/manual/configuration.html#autoScan" target="_blank">配置扫描</a>一起使用。如果尝试这样做，更改配置文件会导致发生类似以下错误日志：</p>
</blockquote>
<pre class="language-"><code>ERROR in ch.qos.logback.core.joran.spi.Interpreter@4:71 - no applicable action for [springProperty], current ElementPath is [[configuration][springProperty]]
ERROR in ch.qos.logback.core.joran.spi.Interpreter@4:71 - no applicable action for [springProfile], current ElementPath is [[configuration][springProfile]]
</code></pre><p><a id="_profile_specific_configuration"></a></p>
<h3 id="2671、特定-profile-配置">26.7.1、特定 Profile 配置</h3>
<p><code><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>springProfile</span><span class="token punctuation">&gt;</span></span></code> 标签允许您根据激活的 Spring profile 选择性地包含或排除配置部分。在 <code><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>configuration</span><span class="token punctuation">&gt;</span></span></code> 元素中的任何位置都支持配置 profile。使用 <code>name</code> 属性指定哪个 proifle 接受配置。<code><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>springProfile</span><span class="token punctuation">&gt;</span></span></code> 标记可以包含简单的 proifle 名称（例如 <code>staging</code>）或 profile 表达式。profile 表达式允许表达更复杂的 profile 逻辑，例如 <code>production &amp; (eu-central | eu-west)</code>。有关详细信息，请查阅<a href="https://docs.spring.io/spring/docs/5.1.3.RELEASE/spring-framework-reference/core.html#beans-definition-profiles-java" target="_blank">参考指南</a>。以下清单展示了三个示例 profile：</p>
<pre class="language-"><code class="lang-xml"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>springProfile</span> <span class="token attr-name">name</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>staging<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
    <span class="token comment">&lt;!-- configuration to be enabled when the "staging" profile is active --&gt;</span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>springProfile</span><span class="token punctuation">&gt;</span></span>

<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>springProfile</span> <span class="token attr-name">name</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>dev | staging<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
    <span class="token comment">&lt;!-- configuration to be enabled when the "dev" or "staging" profiles are active --&gt;</span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>springProfile</span><span class="token punctuation">&gt;</span></span>

<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>springProfile</span> <span class="token attr-name">name</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>!production<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
    <span class="token comment">&lt;!-- configuration to be enabled when the "production" profile is not active --&gt;</span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>springProfile</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<p><a id="_environment_properties"></a></p>
<h3 id="2672、环境属性">26.7.2、环境属性</h3>
<p>使用 <code><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>springProperty</span><span class="token punctuation">&gt;</span></span></code> 标记可以让您暴露 Spring 环境（<code>Environment</code>）中的属性，以便在 Logback 中使用。如果在 Logback 配置中访问来自 <code>application.properties</code> 文件的值，这样做很有用。标签的工作方式与 Logback 的标准 <code><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>property</span><span class="token punctuation">&gt;</span></span></code> 标签类似。但是，您可以指定属性（来自 <code>Environment</code>）的 <code>source</code>，而不是指定直接的 <code>value</code>。如果需要将属性存储在 <code>local</code> 范围以外的其他位置，则可以使用 <code>scope</code> 属性。如果需要回退值（如果未在 <code>Environment</code> 中设置该属性），则可以使用 <code>defaultValue</code> 属性。以下示例展示了如何暴露属性以便在 Logback 中使用：</p>
<pre class="language-"><code class="lang-xml"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>springProperty</span> <span class="token attr-name">scope</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>context<span class="token punctuation">"</span></span> <span class="token attr-name">name</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>fluentHost<span class="token punctuation">"</span></span> <span class="token attr-name">source</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>myapp.fluentd.host<span class="token punctuation">"</span></span>
        <span class="token attr-name">defaultValue</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>localhost<span class="token punctuation">"</span></span><span class="token punctuation">/&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>appender</span> <span class="token attr-name">name</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>FLUENT<span class="token punctuation">"</span></span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>ch.qos.logback.more.appenders.DataFluentAppender<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>remoteHost</span><span class="token punctuation">&gt;</span></span>${fluentHost}<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>remoteHost</span><span class="token punctuation">&gt;</span></span>
    ...
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>appender</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<p><strong>注意</strong></p>
<blockquote>
<p>必须以 kebab 风格（短横线小写风格）指定 <code>source</code>（例如 <code>my.property-name</code>）。但可以使用宽松规则将属性添加到 <code>Environment</code> 中。</p>
</blockquote>
<p><a id="boot-features-json"></a></p>
<h2 id="27、json">27、JSON</h2>
<p>Spring Boot 为三个 JSON 映射库提供了内置集成：</p>
<ul>
<li>GSON</li>
<li>Jackson</li>
<li>JSON-B</li>
</ul>
<p>Jackson 是首选和默认的库。</p>
<p><a id="boot-features-json-jackson"></a></p>
<h2 id="271、jackson">27.1、Jackson</h2>
<p>Spring Boot 提供了 Jackson 的自动配置，Jackson 是 <code>spring-boot-starter-json</code> 的一部分。当 Jackson 在 classpath 上时，会自动配置 <code>ObjectMapper</code> bean。Spring Boot 提供了几个配置属性来<a href="howto.md#howto-customize-the-jackson-objectmapper">自定义 <code>ObjectMapper</code> 的配置</a>。</p>
<p><a id="boot-features-json-gson"></a></p>
<h2 id="272、gson">27.2、Gson</h2>
<p>Spring Boot 提供 Gson 的自动配置。当 Gson 在 classpath 上时，会自动配置 <code>Gson</code> bean。Spring Boot 提供了几个 <code>spring.gson.*</code> 配置属性来自定义配置。为了获得更多控制，可以使用一个或多个 <code>GsonBuilderCustomizer</code> bean。</p>
<p><a id="boot-features-json-json-b"></a></p>
<h2 id="273、json-b">27.3、JSON-B</h2>
<p>Spring Boot 提供了 JSON-B 的自动配置。当 JSON-B API 和实现在 classpath 上时，将自动配置 <code>Jsonb</code> bean。首选的 JSON-B 实现是 Apache Johnzon，它提供了依赖管理。</p>
<p><a id="boot-features-developing-web-applications"></a></p>
<h2 id="28、开发-web-应用程序">28、开发 Web 应用程序</h2>
<p>Spring Boot 非常适合用于开发 web 应用程序。您可以使用嵌入式 Tomcat、Jetty 或者 Undertow 来创建一个独立（self-contained）的 HTTP 服务器。大多数 web 应用程序使用 <code>spring-boot-starter-web</code> 模块来快速搭建和运行，您也可以选择使用 <code>spring-boot-starter-webflux</code> 模块来构建响应式（reactive） web 应用程序。</p>
<p>如果您尚未开发过 Spring Boot web 应用程序，则可以按照<a href="#getting-started-first-application">入门</a>章节中的“Hello World!”示例进行操作。</p>
<p><a id="boot-features-spring-mvc"></a></p>
<h3 id="281、spring-web-mvc-框架">28.1、Spring Web MVC 框架</h3>
<p><a href="https://docs.spring.io/spring/docs/5.1.3.RELEASE/spring-framework-reference/web.html#mvc" target="_blank">Spring Web MVC 框架</a>（通常简称“Spring MVC”）是一个富<strong>模型-视图-控制器</strong>的 web 框架。Spring MVC 允许您创建 <code>@Controller</code> 或者 <code>@RestController</code> bean 来处理传入的 HTTP 请求。控制器中的方法通过 <code>@RequestMapping</code> 注解映射到 HTTP。</p>
<p>以下是一个使用了 <code>@RestController</code> 来响应 JSON 数据的典型示例：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@RestController</span>
<span class="token annotation punctuation">@RequestMapping</span><span class="token punctuation">(</span>value<span class="token operator">=</span><span class="token string">"/users"</span><span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyRestController</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@RequestMapping</span><span class="token punctuation">(</span>value<span class="token operator">=</span><span class="token string">"/{user}"</span><span class="token punctuation">,</span> method<span class="token operator">=</span><span class="token class-name">RequestMethod</span><span class="token punctuation">.</span>GET<span class="token punctuation">)</span>
    <span class="token keyword">public</span> <span class="token class-name">User</span> <span class="token function">getUser</span><span class="token punctuation">(</span><span class="token annotation punctuation">@PathVariable</span> <span class="token class-name">Long</span> user<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment">// ...</span>
    <span class="token punctuation">}</span>

    <span class="token annotation punctuation">@RequestMapping</span><span class="token punctuation">(</span>value<span class="token operator">=</span><span class="token string">"/{user}/customers"</span><span class="token punctuation">,</span> method<span class="token operator">=</span><span class="token class-name">RequestMethod</span><span class="token punctuation">.</span>GET<span class="token punctuation">)</span>
    <span class="token class-name">List</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">Customer</span><span class="token punctuation">&gt;</span></span> <span class="token function">getUserCustomers</span><span class="token punctuation">(</span><span class="token annotation punctuation">@PathVariable</span> <span class="token class-name">Long</span> user<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment">// ...</span>
    <span class="token punctuation">}</span>

    <span class="token annotation punctuation">@RequestMapping</span><span class="token punctuation">(</span>value<span class="token operator">=</span><span class="token string">"/{user}"</span><span class="token punctuation">,</span> method<span class="token operator">=</span><span class="token class-name">RequestMethod</span><span class="token punctuation">.</span>DELETE<span class="token punctuation">)</span>
    <span class="token keyword">public</span> <span class="token class-name">User</span> <span class="token function">deleteUser</span><span class="token punctuation">(</span><span class="token annotation punctuation">@PathVariable</span> <span class="token class-name">Long</span> user<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment">// ...</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>Spring MVC 是 Spring Framework 核心的一部分，详细介绍可参考其<a href="https://docs.spring.io/spring/docs/5.1.3.RELEASE/spring-framework-reference/web.html#mvc" target="_blank">参考文档</a>。<a href="https://spring.io/guides" target="_blank">spring.io/guides</a> 还提供了几个 Spring MVC 相关的指南。</p>
<p><a id="boot-features-spring-mvc-auto-configuration"></a></p>
<h4 id="2811、spring-mvc-自动配置">28.1.1、Spring MVC 自动配置</h4>
<p>Spring Boot 提供了适用于大多数 Spring MVC 应用的自动配置（auto-configuration）。</p>
<p>自动配置在 Spring 默认功能上添加了以下功能：</p>
<ul>
<li>引入 <code>ContentNegotiatingViewResolver</code> 和 <code>BeanNameViewResolver</code> bean。</li>
<li>支持服务静态资源，包括对 WebJar 的支持（<a href="#boot-features-spring-mvc-static-content">见下文</a>）。</li>
<li>自动注册 <code>Converter</code>、<code>GenericConverter</code> 和 <code>Formatter</code> bean。</li>
<li>支持 <code>HttpMessageConverter</code>（见<a href="#boot-features-spring-mvc-message-converters">下文</a>）。</li>
<li>自动注册 <code>MessageCodesResolver</code>（见<a href="#boot-features-spring-message-codes">下文</a>）。</li>
<li>支持静态 index.html。</li>
<li>支持自定义 Favicon （见<a href="#boot-features-spring-mvc-favicon">下文</a>）。</li>
<li>自动使用 <code>ConfigurableWebBindingInitializer</code> bean（见<a href="#boot-features-spring-mvc-web-binding-initializer">下文</a>）。</li>
</ul>
<p>如果您想保留 Spring Boot MVC 的功能，并且需要添加其他 <a href="https://docs.spring.io/spring/docs/5.1.3.RELEASE/spring-framework-reference/web.html#mvc" target="_blank">MVC 配置</a>（interceptor、formatter 和视图控制器等），可以添加自己的 <code>WebMvcConfigurerAdapter</code> 类型的 <code>@Configuration</code> 类，但<strong>不能</strong>带 <code>@EnableWebMvc</code> 注解。如果您想自定义 <code>RequestMappingHandlerMapping</code>、<code>RequestMappingHandlerAdapter</code> 或者 <code>ExceptionHandlerExceptionResolver</code> 实例，可以声明一个 <code>WebMvcRegistrationsAdapter</code> 实例来提供这些组件。</p>
<p>如果您想完全掌控 Spring MVC，可以添加自定义注解了 <code>@EnableWebMvc</code> 的 @Configuration 配置类。</p>
<p><a id="boot-features-spring-mvc-message-converters"></a></p>
<h4 id="2812、httpmessageconverters">28.1.2、HttpMessageConverters</h4>
<p>Spring MVC 使用 <code>HttpMessageConverter</code> 接口来转换 HTTP 的请求和响应。开箱即用功能包含了合适的默认值，比如对象可以自动转换为 JSON（使用 Jackson 库）或者 XML（优先使用 Jackson XML 扩展，其次为 JAXB）。字符串默认使用 <code>UTF-8</code> 编码。</p>
<p>如果您需要添加或者自定义转换器（converter），可以使用 Spring Boot 的 <code>HttpMessageConverters</code> 类：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>boot<span class="token punctuation">.</span>autoconfigure<span class="token punctuation">.</span>web</span><span class="token punctuation">.</span><span class="token class-name">HttpMessageConverters</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>context<span class="token punctuation">.</span>annotation</span><span class="token punctuation">.</span>*<span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>http<span class="token punctuation">.</span>converter</span><span class="token punctuation">.</span>*<span class="token punctuation">;</span>

<span class="token annotation punctuation">@Configuration</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyConfiguration</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@Bean</span>
    <span class="token keyword">public</span> <span class="token class-name">HttpMessageConverters</span> <span class="token function">customConverters</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token class-name">HttpMessageConverter</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token operator">?</span><span class="token punctuation">&gt;</span></span> additional <span class="token operator">=</span> <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
        <span class="token class-name">HttpMessageConverter</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token operator">?</span><span class="token punctuation">&gt;</span></span> another <span class="token operator">=</span> <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
        <span class="token keyword">return</span> <span class="token keyword">new</span> <span class="token class-name">HttpMessageConverters</span><span class="token punctuation">(</span>additional<span class="token punctuation">,</span> another<span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>上下文中的所有 <code>HttpMessageConverter</code> bean 都将被添加到转换器列表中。您也可以用这种方式来覆盖默认转换器。</p>
<p><a id="boot-features-json-components"></a></p>
<h4 id="2813、自定义-json-serializer-和-deserializer">28.1.3、自定义 JSON Serializer 和 Deserializer</h4>
<p>如果您使用 Jackson 序列化和反序列化 JSON 数据，可能需要自己编写 <code>JsonSerializer</code> 和 <code>JsonDeserializer</code> 类。自定义序列化器（serializer）的做法通常是通过<a href="https://github.com/FasterXML/jackson-docs/wiki/JacksonHowToCustomSerializers" target="_blank">一个模块来注册 Jackson</a>， 然而 Spring Boot 提供了一个备选的 <code>@JsonComponent</code> 注解，它可以更加容易地直接注册 Spring Bean。</p>
<p>您可以直接在 <code>JsonSerializer</code> 或者 <code>JsonDeserializer</code> 实现上使用 <code>@JsonComponent</code> 注解。您也可以在将序列化器/反序列化器（deserializer）作为内部类的类上使用。例如：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">import</span> <span class="token namespace">java<span class="token punctuation">.</span>io</span><span class="token punctuation">.</span>*<span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">com<span class="token punctuation">.</span>fasterxml<span class="token punctuation">.</span>jackson<span class="token punctuation">.</span>core</span><span class="token punctuation">.</span>*<span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">com<span class="token punctuation">.</span>fasterxml<span class="token punctuation">.</span>jackson<span class="token punctuation">.</span>databind</span><span class="token punctuation">.</span>*<span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>boot<span class="token punctuation">.</span>jackson</span><span class="token punctuation">.</span>*<span class="token punctuation">;</span>

<span class="token annotation punctuation">@JsonComponent</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">Example</span> <span class="token punctuation">{</span>

    <span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">class</span> <span class="token class-name">Serializer</span> <span class="token keyword">extends</span> <span class="token class-name">JsonSerializer</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">SomeObject</span><span class="token punctuation">&gt;</span></span> <span class="token punctuation">{</span>
        <span class="token comment">// ...</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">class</span> <span class="token class-name">Deserializer</span> <span class="token keyword">extends</span> <span class="token class-name">JsonDeserializer</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">SomeObject</span><span class="token punctuation">&gt;</span></span> <span class="token punctuation">{</span>
        <span class="token comment">// ...</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p><code>ApplicationContext</code> 中所有的 <code>@JsonComponent</code> bean 将被自动注册到 Jackson 中，由于 <code>@JsonComponent</code> 使用 <code>@Component</code> 注解标记，因此组件扫描（component-scanning）规则将对其生效。</p>
<p>Spring Boot 还提供了 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.1.RELEASE/spring-boot-project/spring-boot/src/main/java/org/springframework/boot/jackson/JsonObjectSerializer.java" target="_blank">JsonObjectSerializer</a> 和 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.1.RELEASE/spring-boot-project/spring-boot/src/main/java/org/springframework/boot/jackson/JsonObjectDeserializer.java" target="_blank">JsonObjectDeserializer</a> 基类，它们在序列化对象时为标准的 Jackson 版本提供了有用的替代方案。有关详细信息，请参阅 Javadoc 中的 <a href="https://docs.spring.io/spring-boot/docs/2.1.1.RELEASE/api/org/springframework/boot/jackson/JsonObjectSerializer.html" target="_blank">JsonObjectSerializer</a> 和 <a href="https://docs.spring.io/spring-boot/docs/2.1.1.RELEASE/api/org/springframework/boot/jackson/JsonObjectDeserializer.html" target="_blank">JsonObjectDeserializer</a>。</p>
<p><a id="boot-features-spring-message-codes"></a></p>
<h4 id="2814、messagecodesresolver">28.1.4、MessageCodesResolver</h4>
<p>Spring MVC 有一个从绑定错误中生成错误码的策略，用于渲染错误信息：<code>MessageCodesResolver</code>。如果您设置了 <code>spring.mvc.message-codes-resolver.format</code> 属性值为 <code>PREFIX_ERROR_CODE</code> 或 <code>POSTFIX_ERROR_CODE</code>，Spring Boot 将为你创建该策略（请参阅 <a href="https://docs.spring.io/spring/docs/5.1.3.RELEASE/javadoc-api/org/springframework/validation/DefaultMessageCodesResolver.Format.html" target="_blank">DefaultMessageCodesResolver.Format</a> 中的枚举）。</p>
<p><a id="boot-features-spring-mvc-static-content"></a></p>
<h4 id="2815、静态内容">28.1.5、静态内容</h4>
<p>默认情况下，Spring Boot 将在 classpath 或者 <code>ServletContext</code> 根目录下从名为 <code>/static</code> （<code>/public</code>、<code>/resources</code> 或 <code>/META-INF/resources</code>）目录中服务静态内容。它使用了 Spring MVC 的 <code>ResourceHttpRequestHandler</code>，因此您可以通过添加自己的 <code>WebMvcConfigurerAdapter</code> 并重写 <code>addResourceHandlers</code> 方法来修改此行为。</p>
<p>在一个独立的（stand-alone） web 应用程序中，来自容器的默认 servlet 也是被启用的，并充当一个回退支援，Spring 决定不处理 <code>ServletContext</code> 根目录下的静态资源，容器的默认 servlet 也将会处理。大多情况下，这是不会发生的（除非您修改了默认的 MVC 配置），因为 Spring 始终能通过 <code>DispatcherServlet</code> 来处理请求。</p>
<p>默认情况下，资源被映射到 <code>/**</code>，但可以通过 <code>spring.mvc.static-path-pattern</code> 属性调整。比如，将所有资源重定位到 <code>/resources/**</code>：</p>
<pre class="language-"><code>spring.mvc.static-path-pattern=/resources/**
</code></pre><p>您还可以使用 <code>spring.resources.static-locations</code> 属性来自定义静态资源的位置（使用一个目录位置列表替换默认值）。根 Servlet context path <code>/</code> 自动作为一个 location 添加进来。</p>
<p>除了上述提到的<strong>标准</strong>静态资源位置之外，还有一种特殊情况是用于 <a href="https://www.webjars.org/" target="_blank">Webjar 内容</a>。如果以 Webjar 格式打包，则所有符合 <code>/webjars/**</code> 的资源都将从 jar 文件中服务。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>如果您的应用程序要包成 jar，请不要使用 <code>src/main/webapp</code> 目录。虽然此目录是一个通用标准，但它<strong>只</strong>适用于 war 打包，如果生成的是一个 jar，它将被绝大多数的构建工具所忽略。</p>
</blockquote>
<p>Spring Boot 还支持 Spring MVC 提供的高级资源处理功能，允许使用例如静态资源缓存清除（cache busting）或者 Webjar 版本无关 URL。</p>
<p>要使用 Webjar 版本无关 URL 功能，只需要添加 <code>webjars-locator-core</code> 依赖。然后声明您的 Webjar，以 jQuery 为例，添加的 <code>"/webjars/jquery/dist/jquery.min.js"</code> 将变成 <code>"/webjars/jquery/x.y.z/dist/jquery.min.js"</code>，其中 <code>x.y.z</code> 是 Webjar 的版本。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>如果您使用 JBoss，则需要声明 <code>webjars-locator-jboss-vfs</code> 依赖，而不是 <code>webjars-locator-core</code>，否则所有 Webjar 将被解析成 <code>404</code>。</p>
</blockquote>
<p>要使用缓存清除功能，以下配置为所有静态资源配置了一个缓存清除方案，实际上是在 URL 上添加了一个内容哈希，例如 <code><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>link</span> <span class="token attr-name">href</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>/css/spring-2a2d595e6ed9a0b24f027f2b63b134d6.css<span class="token punctuation">"</span></span><span class="token punctuation">/&gt;</span></span></code>：</p>
<pre class="language-"><code>pring.resources.chain.strategy.content.enabled=true
spring.resources.chain.strategy.content.paths=/**
</code></pre><p><strong>注意</strong></p>
<blockquote>
<p>模板中的资源链接在运行时被重写，这得益于 <code>ResourceUrlEncodingFilter</code> 为 Thymeleaf 和 FreeMarker 自动配置。在使用 JSP 时，您应该手动声明此过滤器。其他模板引擎现在还不会自动支持，但可以与自定义模板宏（macro）/helper 和 <a href="https://docs.spring.io/spring/docs/5.1.3.RELEASE/javadoc-api/org/springframework/web/servlet/resource/ResourceUrlProvider.html" target="_blank"><code>ResourceUrlProvider</code></a> 结合使用。</p>
</blockquote>
<p>当使用例如 Javascript 模块加载器动态加载资源时，重命名文件是不可选的。这也是为什么支持其他策略并且可以组合使用的原因。<strong>fixed</strong>策略将在 URL 中添加一个静态版本字符串，而不是更改文件名：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.resources.chain.strategy.content.enabled</span><span class="token attr-value"><span class="token punctuation">=</span>true</span>
<span class="token constant">spring.resources.chain.strategy.content.paths</span><span class="token attr-value"><span class="token punctuation">=</span>/**</span>
<span class="token constant">spring.resources.chain.strategy.fixed.enabled</span><span class="token attr-value"><span class="token punctuation">=</span>true</span>
<span class="token constant">spring.resources.chain.strategy.fixed.paths</span><span class="token attr-value"><span class="token punctuation">=</span>/js/lib/</span>
<span class="token constant">spring.resources.chain.strategy.fixed.version</span><span class="token attr-value"><span class="token punctuation">=</span>v12</span>
</code></pre>
<p>使用此配置，JavaScript 模块定位在 <code>"/js/lib/"</code> 下使用固定版本策略（<code>"/v12/js/lib/mymodule.js"</code>），而其他资源仍使用内容策略（<code><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>link</span> <span class="token attr-name">href</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>/css/spring-2a2d595e6ed9a0b24f027f2b63b134d6.css<span class="token punctuation">"</span></span><span class="token punctuation">/&gt;</span></span></code>）。</p>
<p>有关更多支持选项，请参阅 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.1.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/web/ResourceProperties.java" target="_blank">ResourceProperties</a>。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>该功能已经在一个专门的<a href="https://spring.io/blog/2014/07/24/spring-framework-4-1-handling-static-web-resources" target="_blank">博客文章</a>和 Spring 框架的<a href="https://docs.spring.io/spring/docs/5.1.3.RELEASE/spring-framework-reference/web.html#mvc-config-static-resources" target="_blank">参考文档</a>中进行了详细描述。</p>
</blockquote>
<p><a id="boot-features-spring-mvc-welcome-page"></a></p>
<h4 id="2816、欢迎页面">28.1.6、欢迎页面</h4>
<p>Spring Boot 支持静态和模板化的欢迎页面。它首先在配置的静态内容位置中查找 <code>index.html</code> 文件。如果找不到，则查找 <code>index</code> 模板。如果找到其中任何一个，它将自动用作应用程序的欢迎页面。</p>
<p><a id="boot-features-spring-mvc-favicon"></a></p>
<h4 id="2817、自定义-favicon">28.1.7、自定义 Favicon</h4>
<p>Spring Boot 在配置的静态内容位置和根 classpath 中查找 <code>favicon.ico</code>（按顺序）。如果该文件存在，则将被自动用作应用程序的 favicon。</p>
<p><a id="boot-features-spring-mvc-pathmatch"></a></p>
<h4 id="2818、路径匹配与内容协商">28.1.8、路径匹配与内容协商</h4>
<p>Spring MVC 可以通过查看请求路径并将其与应用程序中定义的映射相匹配，将传入的 HTTP 请求映射到处理程序（例如 Controller 方法上的 <code>@GetMapping</code> 注解）。</p>
<p>Spring Boot 默认选择禁用后缀模式匹配，这意味着像 <code>"GET /projects/spring-boot.json"</code> 这样的请求将不会与 <code>@GetMapping("/projects/spring-boot")</code> 映射匹配。这被视为是 <a href="https://docs.spring.io/spring/docs/5.1.3.RELEASE/spring-framework-reference/web.html#mvc-ann-requestmapping-suffix-pattern-match" target="_blank">Spring MVC 应用程序的最佳实践</a>。此功能在过去对于 HTTP 客户端没有发送正确的 <strong>Accept</strong> 请求头的情况还是很有用的，我们需要确保将正确的内容类型发送给客户端。如今，内容协商（Content Negotiation）更加可靠。</p>
<p>还有其他方法可以处理 HTTP 客户端发送不一致 <strong>Accept</strong> 请求头问题。我们可以使用查询参数来确保像 <code>"GET /projects/spring-boot?format=json"</code> 这样的请求映射到 <code>@GetMapping("/projects/spring-boot")</code>，而不是使用后缀匹配：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.mvc.contentnegotiation.favor-parameter</span><span class="token attr-value"><span class="token punctuation">=</span>true</span>

<span class="token comment"># We can change the parameter name, which is "format" by default:</span>
<span class="token comment"># spring.mvc.contentnegotiation.parameter-name=myparam</span>

<span class="token comment"># We can also register additional file extensions/media types with:</span>
<span class="token constant">spring.mvc.contentnegotiation.media-types.markdown</span><span class="token attr-value"><span class="token punctuation">=</span>text/markdown</span>
</code></pre>
<p>如果您了解相关注意事项并仍希望应用程序使用后缀模式匹配，则需要以下配置：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.mvc.contentnegotiation.favor-path-extension</span><span class="token attr-value"><span class="token punctuation">=</span>true</span>
<span class="token constant">spring.mvc.pathmatch.use-suffix-pattern</span><span class="token attr-value"><span class="token punctuation">=</span>true</span>
</code></pre>
<p>或者，不打开所有后缀模式，仅打开支持已注册的后缀模式更加安全：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.mvc.contentnegotiation.favor-path-extension</span><span class="token attr-value"><span class="token punctuation">=</span>true</span>
<span class="token constant">spring.mvc.pathmatch.use-registered-suffix-pattern</span><span class="token attr-value"><span class="token punctuation">=</span>true</span>

<span class="token comment"># You can also register additional file extensions/media types with:</span>
<span class="token comment"># spring.mvc.contentnegotiation.media-types.adoc=text/asciidoc</span>
</code></pre>
<p><a id="boot-features-spring-mvc-web-binding-initializer"></a></p>
<h4 id="2819、configurablewebbindinginitializer">28.1.9、ConfigurableWebBindingInitializer</h4>
<p>Spring MVC 使用一个 <code>WebBindingInitializer</code> 为特定的请求初始化 <code>WebDataBinder</code>。如果您创建了自己的 <code>ConfigurableWebBindingInitializer</code> <code>@Bean</code>，Spring Boot 将自动配置 Spring MVC 使用它。</p>
<p><a id="boot-features-spring-mvc-template-engines"></a></p>
<h4 id="28110、模板引擎">28.1.10、模板引擎</h4>
<p>除了 REST web 服务之外，您还可以使用 Spring MVC 来服务动态 HTML 内容。Spring MVC 支持多种模板技术，包括 Thymeleaf、FreeMarker 和 JSP。当然，许多其他模板引擎也有自己的 Spring MVC 集成。</p>
<p>Spring Boot 包含了以下的模板引擎的自动配置支持：</p>
<ul>
<li><a href="https://freemarker.apache.org/docs/" target="_blank">FreeMarker</a></li>
<li><a href="http://docs.groovy-lang.org/docs/next/html/documentation/template-engines.html#_the_markuptemplateengine" target="_blank">Groovy</a></li>
<li><a href="http://www.thymeleaf.org/" target="_blank">Thymeleaf</a></li>
<li><a href="https://mustache.github.io/" target="_blank">Mustache</a></li>
</ul>
<p><strong>提示</strong></p>
<blockquote>
<p>如果可以，请尽量避免使用 JSP，当使用了内嵌 servlet 容器，会有几个<a href="#boot-features-jsp-limitations">已知限制</a>。</p>
</blockquote>
<p>当您使用这些模板引擎的其中一个并附带了默认配置时，您的模板将从 <code>src/main/resources/templates</code> 自动获取。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>IntelliJ IDEA 根据您运行应用程序的方式来对 classpath 进行不同的排序。在 IDE 中通过 main 方法来运行应用程序将导致与使用 Maven 或 Gradle 或来以 jar 包方式引用程序的排序有所不同，可能会导致 Spring Boot 找不到 classpath 中的模板。如果您碰到到此问题，可以重新排序 IDE 的 classpath 来放置模块的 classes 和 resources 到首位。或者，您可以配置模板前缀来搜索 classpath 中的每一个 <code>templates</code> 目录，比如：<code>classpath*:/templates/</code>。 </p>
</blockquote>
<p><a id="boot-features-error-handling"></a></p>
<h4 id="28111、错误处理">28.1.11、错误处理</h4>
<p>默认情况下，Spring Boot 提供了一个使用了比较合理的方式来处理所有错误的 <code>/error</code> 映射，其在 servlet 容器中注册了一个<strong>全局</strong>错误页面。对于机器客户端而言，它将产生一个包含错误、HTTP 状态和异常消息的 JSON 响应。对于浏览器客户端而言，将以 HTML 格式呈现相同数据的 <strong>whitelabel</strong> 错误视图（可添加一个解析到 <code>error</code> 的 <code>View</code> 进行自定义）。要完全替换默认行为，您可以实现 <code>ErrorController</code> 并注册该类型的 bean，或者简单地添加一个类型为 <code>ErrorAttributes</code> 的 bean 来替换内容，但继续使用现用机制。</p>
<p><strong>提示</strong></p>
<blockquote>
<p><code>BasicErrorController</code> 可以作为自定义 <code>ErrorController</code> 的基类，这非常有用，尤其是在您想添加一个新的内容类型（默认专门处理 <code>text/html</code>，并为其他内容提供后备）处理器的情况下。要做到这点，您只需要继承 <code>BasicErrorController</code> 并添加一个带有 <code>produces</code> 属性的 <code>@RequestMapping</code> 注解的公共方法，之后创建一个新类型的 bean。</p>
</blockquote>
<p>您还可以定义一个带有 <code>@ControllerAdvice</code> 注解的类来自定义为特定控制器或异常类型返回的 JSON 文档：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@ControllerAdvice</span><span class="token punctuation">(</span>basePackageClasses <span class="token operator">=</span> <span class="token class-name">AcmeController</span><span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">AcmeControllerAdvice</span> <span class="token keyword">extends</span> <span class="token class-name">ResponseEntityExceptionHandler</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@ExceptionHandler</span><span class="token punctuation">(</span><span class="token class-name">YourException</span><span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">)</span>
    <span class="token annotation punctuation">@ResponseBody</span>
    <span class="token class-name">ResponseEntity</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token operator">?</span><span class="token punctuation">&gt;</span></span> <span class="token function">handleControllerException</span><span class="token punctuation">(</span><span class="token class-name">HttpServletRequest</span> request<span class="token punctuation">,</span> <span class="token class-name">Throwable</span> ex<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token class-name">HttpStatus</span> status <span class="token operator">=</span> <span class="token function">getStatus</span><span class="token punctuation">(</span>request<span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">return</span> <span class="token keyword">new</span> <span class="token class-name">ResponseEntity</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token punctuation">&gt;</span></span><span class="token punctuation">(</span><span class="token keyword">new</span> <span class="token class-name">CustomErrorType</span><span class="token punctuation">(</span>status<span class="token punctuation">.</span><span class="token function">value</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">,</span> ex<span class="token punctuation">.</span><span class="token function">getMessage</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">,</span> status<span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">private</span> <span class="token class-name">HttpStatus</span> <span class="token function">getStatus</span><span class="token punctuation">(</span><span class="token class-name">HttpServletRequest</span> request<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token class-name">Integer</span> statusCode <span class="token operator">=</span> <span class="token punctuation">(</span><span class="token class-name">Integer</span><span class="token punctuation">)</span> request<span class="token punctuation">.</span><span class="token function">getAttribute</span><span class="token punctuation">(</span><span class="token string">"javax.servlet.error.status_code"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">if</span> <span class="token punctuation">(</span>statusCode <span class="token operator">==</span> <span class="token keyword">null</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token keyword">return</span> <span class="token class-name">HttpStatus</span><span class="token punctuation">.</span>INTERNAL_SERVER_ERROR<span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
        <span class="token keyword">return</span> <span class="token class-name">HttpStatus</span><span class="token punctuation">.</span><span class="token function">valueOf</span><span class="token punctuation">(</span>statusCode<span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>以上示例中，如果同包下定义的控制器 <code>AcmeController</code> 抛出了 <code>YourException</code>，则将使用 <code>CustomerErrorType</code> 类型的 POJO 来代替 <code>ErrorAttributes</code> 做 JSON 呈现。</p>
<p><a id="boot-features-error-handling-custom-error-pages"></a></p>
<h5 id="281111、自定义错误页面">28.1.11.1、自定义错误页面</h5>
<p>如果您想在自定义的 HTML 错误页面上显示给定的状态码，请将文件添加到 <code>/error</code> 文件夹中。错误页面可以是静态 HTML（添加在任意静态资源文件夹下) 或者使用模板构建。文件的名称应该是确切的状态码或者一个序列掩码。</p>
<p>例如，要将 <code>404</code> 映射到一个静态 HTML 文件，文件夹结构可以如下：</p>
<pre class="language-"><code>src/
 +- main/
     +- java/
     |   + <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>source</span> <span class="token attr-name">code</span><span class="token punctuation">&gt;</span></span>
     +- resources/
         +- public/
             +- error/
             |   +- 404.html
             +- <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>other</span> <span class="token attr-name">public</span> <span class="token attr-name">assets</span><span class="token punctuation">&gt;</span></span>
</code></pre><p>使用 FreeMarker 模板来映射所有 <code>5xx</code> 错误，文件夹的结构如下：</p>
<pre class="language-"><code>src/
 +- main/
     +- java/
     |   + <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>source</span> <span class="token attr-name">code</span><span class="token punctuation">&gt;</span></span>
     +- resources/
         +- templates/
             +- error/
             |   +- 5xx.ftl
             +- <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>other</span> <span class="token attr-name">templates</span><span class="token punctuation">&gt;</span></span>
</code></pre><p>对于更复杂的映射，您还通过可以添加实现了 <code>ErrorViewResolver</code> 接口的 bean 来处理：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyErrorViewResolver</span> <span class="token keyword">implements</span> <span class="token class-name">ErrorViewResolver</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@Override</span>
    <span class="token keyword">public</span> <span class="token class-name">ModelAndView</span> <span class="token function">resolveErrorView</span><span class="token punctuation">(</span><span class="token class-name">HttpServletRequest</span> request<span class="token punctuation">,</span>
            <span class="token class-name">HttpStatus</span> status<span class="token punctuation">,</span> <span class="token class-name">Map</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">String</span><span class="token punctuation">,</span> <span class="token class-name">Object</span><span class="token punctuation">&gt;</span></span> model<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment">// Use the request or status to optionally return a ModelAndView</span>
        <span class="token keyword">return</span> <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>您还可以使用常规的 Spring MVC 功能，比如 <a href="https://docs.spring.io/spring/docs/5.1.3.RELEASE/spring-framework-reference/web.html#mvc-exceptionhandlers" target="_blank"><code>@ExceptionHandler</code> 方法</a>和 <a href="https://docs.spring.io/spring/docs/5.1.3.RELEASE/spring-framework-reference/web.html#mvc-ann-controller-advice" target="_blank">@ControllerAdvice</a><code>。之后，ErrorController</code> 将能接收任何未处理的异常。</p>
<p><a id="boot-features-error-handling-mapping-error-pages-without-mvc"></a></p>
<h5 id="281112、映射到-spring-mvc-之外的错误页面">28.1.11.2、映射到 Spring MVC 之外的错误页面</h5>
<p>对于不使用 Spring MVC 的应用程序，您可以使用 <code>ErrorPageRegistrar</code> 接口来直接注册 <code>ErrorPages</code>。抽象部分直接与底层的内嵌 servlet 容器一起工作，即使您没有 Spring MVC <code>DispatcherServlet</code> 也能使用。</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Bean</span>
<span class="token keyword">public</span> <span class="token class-name">ErrorPageRegistrar</span> <span class="token function">errorPageRegistrar</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">{</span>
    <span class="token keyword">return</span> <span class="token keyword">new</span> <span class="token class-name">MyErrorPageRegistrar</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token comment">// ...</span>

<span class="token keyword">private</span> <span class="token keyword">static</span> <span class="token keyword">class</span> <span class="token class-name">MyErrorPageRegistrar</span> <span class="token keyword">implements</span> <span class="token class-name">ErrorPageRegistrar</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@Override</span>
    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">registerErrorPages</span><span class="token punctuation">(</span><span class="token class-name">ErrorPageRegistry</span> registry<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        registry<span class="token punctuation">.</span><span class="token function">addErrorPages</span><span class="token punctuation">(</span><span class="token keyword">new</span> <span class="token class-name">ErrorPage</span><span class="token punctuation">(</span><span class="token class-name">HttpStatus</span><span class="token punctuation">.</span>BAD_REQUEST<span class="token punctuation">,</span> <span class="token string">"/400"</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p><strong>注意</strong></p>
<blockquote>
<p>如果您注册了一个 <code>ErrorPage</code>，它的路径最终由一个 <code>Filter</code>（例如，像一些非 Spring web 框架一样，比如 Jersey 和 Wicket）处理，则必须将 Filter 显式注册为一个 <code>ERROR</code> dispatcher，如下示例：</p>
</blockquote>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Bean</span>
<span class="token keyword">public</span> <span class="token class-name">FilterRegistrationBean</span> <span class="token function">myFilter</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token class-name">FilterRegistrationBean</span> registration <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">FilterRegistrationBean</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    registration<span class="token punctuation">.</span><span class="token function">setFilter</span><span class="token punctuation">(</span><span class="token keyword">new</span> <span class="token class-name">MyFilter</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
    registration<span class="token punctuation">.</span><span class="token function">setDispatcherTypes</span><span class="token punctuation">(</span><span class="token class-name">EnumSet</span><span class="token punctuation">.</span><span class="token function">allOf</span><span class="token punctuation">(</span><span class="token class-name">DispatcherType</span><span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token keyword">return</span> registration<span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>
<p>请注意，默认的 <code>FilterRegistrationBean</code> 不包含 <code>ERROR</code> 调度器（dispatcher）类型。</p>
<p><strong>当心</strong>：当部署到 servlet 容器时，Spring Boot 使用其错误页面过滤器会将有错误状态的请求转发到相应的错误页面。如果尚未提交响应，则只能将请求转发到正确的错误页面。默认情况下，WebSphere Application Server 8.0 及更高版本在成功完成 servlet 的 service 方法后提交响应。您应该将 <code>com.ibm.ws.webcontainer.invokeFlushAfterService</code> 设置为 <code>false</code> 来禁用此行为。</p>
<p><a id="boot-features-spring-hateoas"></a></p>
<h4 id="28112、spring-hateoas">28.1.12、Spring HATEOAS</h4>
<p>如果您想开发一个使用超媒体（hypermedia）的 RESTful API，Spring Boot 提供的 Spring HATEOAS 自动配置在大多数应用程序都工作得非常好。自动配置取代了 <code>@EnableHypermediaSupport</code> 的需要，并注册了一些 bean，以便能轻松构建基于超媒体的应用程序，其包括了一个 <code>LinkDiscoverers</code> （用于客户端支持）和一个用于配置将响应正确呈现的 <code>ObjectMapper</code>。<code>ObjectMapper</code> 可以通过设置 <code>spring.jackson.*</code> 属性或者 <code>Jackson2ObjectMapperBuilder</code> bean （如果存在）自定义。</p>
<p>您可以使用 <code>@EnableHypermediaSupport</code> 来控制 Spring HATEOAS 的配置。请注意，这使得上述的自定义 ObjectMapper 被禁用。</p>
<p><a id="boot-features-cors"></a></p>
<h4 id="28113、cors-支持">28.1.13、CORS 支持</h4>
<p><a href="https://en.wikipedia.org/wiki/Cross-origin_resource_sharing" target="_blank">跨域资源共享</a>（Cross-origin resource sharing，CORS）是<a href="https://caniuse.com/#feat=cors" target="_blank">大多数浏览器</a>实现的一个 <a href="https://www.w3.org/TR/cors/" target="_blank">W3C 规范</a>，其可允许您以灵活的方式指定何种跨域请求可以被授权，而不是使用一些不太安全和不太强大的方式（比如 IFRAME 或者 JSONP）。</p>
<p>Spring MVC 从 4.2 版本起开始<a href="https://docs.spring.io/spring/docs/5.1.3.RELEASE/spring-framework-reference/web.html#cors" target="_blank">支持 CORS</a>。您可在 Spring Boot 应用程序中使用 <a href="https://docs.spring.io/spring/docs/5.1.3.RELEASE/spring-framework-reference/web.html#controller-method-cors-configuration" target="_blank"><code>@CrossOrigin</code></a> 注解配置<a href="https://docs.spring.io/spring/docs/5.1.3.RELEASE/spring-framework-reference/web.html#controller-method-cors-configuration" target="_blank">控制器方法启用 CORS</a>。还可以通过注册一个 WebMvcConfigurer bean 并自定义 <code>addCorsMappings(CorsRegistry)</code> 方法来定义<a href="https://docs.spring.io/spring/docs/5.1.3.RELEASE/spring-framework-reference/web.html#global-cors-configuration" target="_blank">全局 CORS 配置</a>：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Configuration</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyConfiguration</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@Bean</span>
    <span class="token keyword">public</span> <span class="token class-name">WebMvcConfigurer</span> <span class="token function">corsConfigurer</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> <span class="token keyword">new</span> <span class="token class-name">WebMvcConfigurer</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token annotation punctuation">@Override</span>
            <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">addCorsMappings</span><span class="token punctuation">(</span><span class="token class-name">CorsRegistry</span> registry<span class="token punctuation">)</span> <span class="token punctuation">{</span>
                registry<span class="token punctuation">.</span><span class="token function">addMapping</span><span class="token punctuation">(</span><span class="token string">"/api/**"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            <span class="token punctuation">}</span>
        <span class="token punctuation">}</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<p><a id="boot-features-webflux"></a></p>
<h3 id="282、spring-webflux-框架">28.2、Spring WebFlux 框架</h3>
<p>Spring WebFlux 是 Spring Framework 5.0 中新引入的一个响应式 Web 框架。与 Spring MVC 不同，它不需要 Servlet API，完全异步且无阻塞，并通过 <a href="http://www.reactive-streams.org/" target="_blank">Reactor 项目</a>实现<a href="http://www.reactive-streams.org/" target="_blank">响应式流（Reactive Streams）</a>规范。</p>
<p>Spring WebFlux 有两个版本：函数式和基于注解。基于注解的方式非常接近 Spring MVC 模型，如下所示：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@RestController</span>
<span class="token annotation punctuation">@RequestMapping</span><span class="token punctuation">(</span><span class="token string">"/users"</span><span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyRestController</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@GetMapping</span><span class="token punctuation">(</span><span class="token string">"/{user}"</span><span class="token punctuation">)</span>
    <span class="token keyword">public</span> <span class="token class-name">Mono</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">User</span><span class="token punctuation">&gt;</span></span> <span class="token function">getUser</span><span class="token punctuation">(</span><span class="token annotation punctuation">@PathVariable</span> <span class="token class-name">Long</span> user<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment">// ...</span>
    <span class="token punctuation">}</span>

    <span class="token annotation punctuation">@GetMapping</span><span class="token punctuation">(</span><span class="token string">"/{user}/customers"</span><span class="token punctuation">)</span>
    <span class="token keyword">public</span> <span class="token class-name">Flux</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">Customer</span><span class="token punctuation">&gt;</span></span> <span class="token function">getUserCustomers</span><span class="token punctuation">(</span><span class="token annotation punctuation">@PathVariable</span> <span class="token class-name">Long</span> user<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment">// ...</span>
    <span class="token punctuation">}</span>

    <span class="token annotation punctuation">@DeleteMapping</span><span class="token punctuation">(</span><span class="token string">"/{user}"</span><span class="token punctuation">)</span>
    <span class="token keyword">public</span> <span class="token class-name">Mono</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">User</span><span class="token punctuation">&gt;</span></span> <span class="token function">deleteUser</span><span class="token punctuation">(</span><span class="token annotation punctuation">@PathVariable</span> <span class="token class-name">Long</span> user<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment">// ...</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p><strong>WebFlux.fn</strong> 为函数式调用方式，它将路由配置与请求处理分开，如下所示：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Configuration</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">RoutingConfiguration</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@Bean</span>
    <span class="token keyword">public</span> <span class="token class-name">RouterFunction</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">ServerResponse</span><span class="token punctuation">&gt;</span></span> <span class="token function">monoRouterFunction</span><span class="token punctuation">(</span><span class="token class-name">UserHandler</span> userHandler<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> <span class="token function">route</span><span class="token punctuation">(</span><span class="token function">GET</span><span class="token punctuation">(</span><span class="token string">"/{user}"</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">and</span><span class="token punctuation">(</span><span class="token function">accept</span><span class="token punctuation">(</span>APPLICATION_JSON<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">,</span> userHandler<span class="token operator">:</span><span class="token operator">:</span><span class="token function">getUser</span><span class="token punctuation">)</span>
                <span class="token punctuation">.</span><span class="token function">andRoute</span><span class="token punctuation">(</span><span class="token function">GET</span><span class="token punctuation">(</span><span class="token string">"/{user}/customers"</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">and</span><span class="token punctuation">(</span><span class="token function">accept</span><span class="token punctuation">(</span>APPLICATION_JSON<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">,</span> userHandler<span class="token operator">:</span><span class="token operator">:</span><span class="token function">getUserCustomers</span><span class="token punctuation">)</span>
                <span class="token punctuation">.</span><span class="token function">andRoute</span><span class="token punctuation">(</span><span class="token function">DELETE</span><span class="token punctuation">(</span><span class="token string">"/{user}"</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">and</span><span class="token punctuation">(</span><span class="token function">accept</span><span class="token punctuation">(</span>APPLICATION_JSON<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">,</span> userHandler<span class="token operator">:</span><span class="token operator">:</span><span class="token function">deleteUser</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>

<span class="token annotation punctuation">@Component</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">UserHandler</span> <span class="token punctuation">{</span>

    <span class="token keyword">public</span> <span class="token class-name">Mono</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">ServerResponse</span><span class="token punctuation">&gt;</span></span> <span class="token function">getUser</span><span class="token punctuation">(</span><span class="token class-name">ServerRequest</span> request<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment">// ...</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token class-name">Mono</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">ServerResponse</span><span class="token punctuation">&gt;</span></span> <span class="token function">getUserCustomers</span><span class="token punctuation">(</span><span class="token class-name">ServerRequest</span> request<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment">// ...</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token class-name">Mono</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">ServerResponse</span><span class="token punctuation">&gt;</span></span> <span class="token function">deleteUser</span><span class="token punctuation">(</span><span class="token class-name">ServerRequest</span> request<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment">// ...</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<p>WebFlux 是 Spring Framework 的一部分，详细信息可查看其<a href="https://docs.spring.io/spring/docs/5.1.3.RELEASE/spring-framework-reference/web-reactive.html#webflux-fn" target="_blank">参考文档</a>。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>您可以根据需要定义尽可能多的 <code>RouterFunction</code> bean 来模块化路由定义。如果需要设定优先级，Bean 可以指定顺序。</p>
</blockquote>
<p>首先，将 <code>spring-boot-starter-webflux</code> 模块添加到您的应用程序中。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>在应用程序中同时添加 <code>spring-boot-starter-web</code> 和 <code>spring-boot-starter-webflux</code> 模块会导致Spring Boot 自动配置 Spring MVC，而不是使用 WebFlux。这样做的原因是因为许多 Spring 开发人员将 <code>spring-boot-starter-webflux</code> 添加到他们的 Spring MVC 应用程序中只是为了使用响应式 <code>WebClient</code>。 您仍然可以通过设置 <code>SpringApplication.setWebApplicationType(WebApplicationType.REACTIVE)</code> 来强制执行您选择的应用程序类型。</p>
</blockquote>
<p><a id="boot-features-webflux-auto-configuration"></a></p>
<h4 id="2821、spring-webflux-自动配置">28.2.1、Spring WebFlux 自动配置</h4>
<p>Spring Boot 为 Spring WebFlux 提供自动配置，适用于大多数应用程序。</p>
<p>自动配置在 Spring 的默认基础上添加了以下功能：</p>
<ul>
<li>为 <code>HttpMessageReader</code> 和 <code>HttpMessageWriter</code> 实例配置编解码器（<a href="#boot-features-webflux-httpcodecs">稍后将介绍</a>）。</li>
<li>支持提供静态资源，包括对 WebJars 的支持（<a href="https://docs.spring.io/spring-boot/docs/2.1.1.RELEASE/reference/htmlsingle/#boot-features-spring-mvc-static-content" target="_blank">后面将介绍</a>）。</li>
</ul>
<p>如果你要保留 Spring Boot WebFlux 功能并且想要添加其他 <a href="https://docs.spring.io/spring/docs/5.1.3.RELEASE/spring-framework-reference/web.html#web-reactive" target="_blank">WebFlux 配置</a>，可以添加自己的 <code>@Configuration</code> 类，类型为 <code>WebFluxConfigurer</code>，但不包含 <code>@EnableWebFlux</code>。</p>
<p>如果您想完全控制 Spring WebFlux，可以将 <code>@EnableWebFlux</code> 注解到自己的 @Configuration。</p>
<p><a id="boot-features-webflux-httpcodecs"></a></p>
<h4 id="2822、使用-httpmessagereader-和-httpmessagewriter-作为-http-编解码器">28.2.2、使用 HttpMessageReader 和 HttpMessageWriter 作为 HTTP 编解码器</h4>
<p>Spring WebFlux 使用 <code>HttpMessageReader</code> 和 <code>HttpMessageWriter</code> 接口来转换 HTTP 的请求和响应。它们通过检测 classpath 中可用的类库，配置了 <code>CodecConfigurer</code> 生成合适的默认值。</p>
<p>Spring Boot 通过使用 <code>CodecCustomizer</code> 实例加强定制。例如，<code>spring.jackson.*</code> 配置 key 应用于 Jackson 编解码器。</p>
<p>如果需要添加或自定义编解码器，您可以创建一个自定义的 <code>CodecCustomizer</code> 组件，如下所示：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>boot<span class="token punctuation">.</span>web<span class="token punctuation">.</span>codec</span><span class="token punctuation">.</span><span class="token class-name">CodecCustomizer</span><span class="token punctuation">;</span>

<span class="token annotation punctuation">@Configuration</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyConfiguration</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@Bean</span>
    <span class="token keyword">public</span> <span class="token class-name">CodecCustomizer</span> <span class="token function">myCodecCustomizer</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> codecConfigurer <span class="token operator">-&gt;</span> <span class="token punctuation">{</span>
            <span class="token comment">// ...</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>您还可以利用 <a href="#boot-features-json-components">Boot 的自定义 JSON 序列化器和反序列化器</a>。</p>
<p><a id="boot-features-webflux-static-content"></a></p>
<h4 id="2823、静态内容">28.2.3、静态内容</h4>
<p>默认情况下，Spring Boot 将在 classpath 或者 <code>ServletContext</code> 根目录下从名为 <code>/static</code> （<code>/public</code>、<code>/resources</code> 或 <code>/META-INF/resources</code>）目录中服务静态内容。它使用了 Spring WebFlux 的 <code>ResourceWebHandler</code>，因此您可以通过添加自己的 <code>WebFluxConfigurer</code> 并重写 <code>addResourceHandlers</code> 方法来修改此行为。</p>
<p>默认情况下，资源被映射到 <code>/**</code>，但可以通过 <code>spring.webflux.static-path-pattern</code> 属性调整。比如，将所有资源重定位到 <code>/resources/**</code>：</p>
<pre class="language-"><code>spring.webflux.static-path-pattern=/resources/**
</code></pre><p>您还可以使用 <code>spring.resources.static-locations</code> 属性来自定义静态资源的位置（使用一个目录位置列表替换默认值），如果这样做，默认的欢迎页面检测会切换到您自定义的位置。因此，如果启动时有任何其中一个位置存在 <code>index.html</code>，那么它将是应用程序的主页。</p>
<p>除了上述提到的<strong>标准</strong>静态资源位置之外，还有一种特殊情况是用于 <a href="https://www.webjars.org/" target="_blank">Webjar 内容</a>。如果以 Webjar 格式打包，则所有符合 <code>/webjars/**</code> 的资源都将从 jar 文件中服务。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>Spring WebFlux 应用程序并不严格依赖于 Servlet API，因此它们不能作为 war 文件部署，也不能使用 <code>src/main/webapp</code> 目录。</p>
</blockquote>
<p><a id="boot-features-webflux-template-engines"></a></p>
<h4 id="2824、模板引擎">28.2.4、模板引擎</h4>
<p>除了 REST web 服务之外，您还可以使用 Spring WebFlux 来服务动态 HTML 内容。Spring WebFlux 支持多种模板技术，包括 Thymeleaf、FreeMarker 和 Mustache。</p>
<p>Spring Boot 包含了以下的模板引擎的自动配置支持：</p>
<ul>
<li><a href="https://freemarker.apache.org/docs/" target="_blank">FreeMarker</a></li>
<li><a href="http://www.thymeleaf.org/" target="_blank">Thymeleaf</a></li>
<li><a href="https://mustache.github.io/" target="_blank">Mustache</a></li>
</ul>
<p>当您使用这些模板引擎的其中一个并附带了默认配置时，您的模板将从 <code>src/main/resources/templates</code> 自动获取。</p>
<p><a id="boot-features-webflux-error-handling"></a></p>
<h4 id="2825、错误处理">28.2.5、错误处理</h4>
<p>Spring Boot 提供了一个 <code>WebExceptionHandler</code>，它以合理的方式处理所有错误。它在处理顺序中的位置紧接在 WebFlux 提供的处理程序之前，这些处理器排序是最后的。对于机器客户端，它会生成一个 JSON 响应，其中包含错误详情、HTTP 状态和异常消息。对于浏览器客户端，有一个 <strong>whitelabel</strong> 错误处理程序，它以 HTML 格式呈现同样的数据。您还可以提供自己的 HTML 模板来显示错误（<a href="#boot-features-webflux-error-handling-custom-error-pages">请参阅下一节</a>）。</p>
<p>自定义此功能的第一步通常会沿用现有机制，但替换或扩充了错误内容。为此，您可以添加 <code>ErrorAttributes</code> 类型的 bean。</p>
<p>想要更改错误处理行为，可以实现 <code>ErrorWebExceptionHandler</code> 并注册该类型的 bean。因为 <code>WebExceptionHandler</code> 是一个非常底层的异常处理器，所以 Spring Boot 还提供了一个方便的 <code>AbstractErrorWebExceptionHandler</code> 来让你以 WebFlux 的方式处理错误，如下所示：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">CustomErrorWebExceptionHandler</span> <span class="token keyword">extends</span> <span class="token class-name">AbstractErrorWebExceptionHandler</span> <span class="token punctuation">{</span>

    <span class="token comment">// Define constructor here</span>

    <span class="token annotation punctuation">@Override</span>
    <span class="token keyword">protected</span> <span class="token class-name">RouterFunction</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">ServerResponse</span><span class="token punctuation">&gt;</span></span> <span class="token function">getRoutingFunction</span><span class="token punctuation">(</span><span class="token class-name">ErrorAttributes</span> errorAttributes<span class="token punctuation">)</span> <span class="token punctuation">{</span>

        <span class="token keyword">return</span> <span class="token class-name">RouterFunctions</span>
                <span class="token punctuation">.</span><span class="token function">route</span><span class="token punctuation">(</span>aPredicate<span class="token punctuation">,</span> aHandler<span class="token punctuation">)</span>
                <span class="token punctuation">.</span><span class="token function">andRoute</span><span class="token punctuation">(</span>anotherPredicate<span class="token punctuation">,</span> anotherHandler<span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>要获得更完整的功能，您还可以直接继承 <code>DefaultErrorWebExceptionHandler</code> 并覆盖相关方法。</p>
<p><a id="boot-features-webflux-error-handling-custom-error-pages"></a></p>
<h5 id="28251、自定义错误页面">28.2.5.1、自定义错误页面</h5>
<p>如果您想在自定义的 HTML 错误页面上显示给定的状态码，请将文件添加到 <code>/error</code> 文件夹中。错误页面可以是静态 HTML（添加在任意静态资源文件夹下) 或者使用模板构建。文件的名称应该是确切的状态码或者一个序列掩码。</p>
<p>例如，要将 <code>404</code> 映射到一个静态 HTML 文件，文件夹结构可以如下：</p>
<pre class="language-"><code>src/
 +- main/
     +- java/
     |   + <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>source</span> <span class="token attr-name">code</span><span class="token punctuation">&gt;</span></span>
     +- resources/
         +- public/
             +- error/
             |   +- 404.html
             +- <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>other</span> <span class="token attr-name">public</span> <span class="token attr-name">assets</span><span class="token punctuation">&gt;</span></span>
</code></pre><p>使用 Mustache 模板来映射所有 <code>5xx</code> 错误，文件夹的结构如下：</p>
<pre class="language-"><code>src/
 +- main/
     +- java/
     |   + <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>source</span> <span class="token attr-name">code</span><span class="token punctuation">&gt;</span></span>
     +- resources/
         +- templates/
             +- error/
             |   +- 5xx.mustache
             +- <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>other</span> <span class="token attr-name">templates</span><span class="token punctuation">&gt;</span></span>
</code></pre><p><a id="boot-features-webflux-web-filters"></a></p>
<h4 id="2826、web-过滤器">28.2.6、Web 过滤器</h4>
<p>Spring WebFlux 提供了一个 <code>WebFilter</code> 接口，可以通过实现该接口来过滤 HTTP 请求/响应消息交换。在应用程序上下文中找到的 WebFilter bean 将自动用于过滤每个消息交换。</p>
<p>如果过滤器的执行顺序很重要，则可以实现 <code>Ordered</code> 接口或使用 <code>@Order</code> 注解来指定顺序。Spring Boot 自动配置可能为您配置了几个 Web 过滤器。执行此操作时，将使用下表中的顺序：</p>
<table>
<thead>
<tr>
<th>Web 过滤器</th>
<th>顺序</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>MetricsWebFilter</code></td>
<td><code>Ordered.HIGHEST_PRECEDENCE + 1</code></td>
</tr>
<tr>
<td><code>WebFilterChainProxy</code>（Spring Security）</td>
<td><code>-100</code></td>
</tr>
<tr>
<td><code>HttpTraceWebFilter</code></td>
<td><code>Ordered.LOWEST_PRECEDENCE - 10</code></td>
</tr>
</tbody>
</table>
<p><a id="boot-features-jersey"></a></p>
<h3 id="283、jax-rs-与-jersey">28.3、JAX-RS 与 Jersey</h3>
<p>如果您喜欢 JAX-RS 编程模型的 REST 端点，则可以使用一个实现来替代 Spring MVC。<a href="https://jersey.github.io/" target="_blank">Jersey</a> 和 <a href="https://cxf.apache.org/" target="_blank">Apache CXF</a> 都能开箱即用。CXF 要求在应用程序上下文中以 <code>@Bean</code> 的方式将它注册为一个 <code>Servlet</code> 或者 <code>Filter</code>。Jersey 有部分原生 Spring 支持，所以我们也在 starter 中提供了与 Spring Boot 整合的自动配置支持。</p>
<p>要使用 Jersey，只需要将 <code>spring-boot-starter-jersey</code> 作为依赖引入，然后您需要一个 <code>ResourceConfig</code> 类型的 <code>@Bean</code>，您可以在其中注册所有端点：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Component</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">JerseyConfig</span> <span class="token keyword">extends</span> <span class="token class-name">ResourceConfig</span> <span class="token punctuation">{</span>

    <span class="token keyword">public</span> <span class="token class-name">JerseyConfig</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token function">register</span><span class="token punctuation">(</span><span class="token class-name">Endpoint</span><span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p><strong>警告</strong></p>
<blockquote>
<p>Jersey 对于扫描可执行归档文件的支持是相当有限的。例如，它无法扫描一个<a href="#deployment-install">完整的可执行 jar 文件</a>中的端点，同样，当运行一个可执行的 war 文件时，它也无法扫描包中 <code>WEB-INF/classes</code> 下的端点。为了避免该限制，您不应该使用 <code>packages</code> 方法，应该使用上述的 <code>register</code> 方法来单独注册每一个端点。</p>
</blockquote>
<p>您可以注册任意数量实现了 <code>ResourceConfigCustomizer</code> 的 bean，以实现更高级的定制化。</p>
<p>所有注册的端点都应注解了 <code>@Components</code> 并具有 HTTP 资源注解（ <code>@GET</code> 等），例如：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Component</span>
<span class="token annotation punctuation">@Path</span><span class="token punctuation">(</span><span class="token string">"/hello"</span><span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">Endpoint</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@GET</span>
    <span class="token keyword">public</span> <span class="token class-name">String</span> <span class="token function">message</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> <span class="token string">"Hello"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>由于 <code>Endpoint</code> 是一个 Spring <code>@Component</code>，它的生命周期由 Spring 管理，您可以使用 <code>@Autowired</code> 注入依赖并使用 <code>@Value</code> 注入外部配置。默认情况下，Jersey servlet 将被注册并映射到 <code>/*</code>。您可以通过将 <code>@ApplicationPath</code> 添加到 <code>ResourceConfig</code> 来改变此行为。</p>
<p>默认情况下，Jersey 在 <code>ServletRegistrationBean</code> 类型的 <code>@Bean</code> 中被设置为一个名为 <code>jerseyServletRegistration</code> 的 Servlet。默认情况下，该 servlet 将被延迟初始化，您可以使用 <code>spring.jersey.servlet.load-on-startup</code> 自定义。您可以禁用或通过创建一个自己的同名 bean 来覆盖该 bean。您还可以通过设置 <code>spring.jersey.type=filter</code> 使用过滤器替代 servlet（该情况下， 替代或覆盖 <code>@Bean</code> 的为<code>jerseyFilterRegistration</code>）。该过滤器有一个 <code>@Order</code>，您可以使用 <code>spring.jersey.filter.order</code> 设置。可以使用 <code>spring.jersey.init.*</code> 指定一个 map 类型的 property 以给定 servlet 和过滤器的初始化参数。</p>
<p>这里有一个 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.1.RELEASE/spring-boot-samples/spring-boot-sample-jersey" target="_blank">Jersey 示例</a>，您可以解如何设置。</p>
<p><a id="boot-features-embedded-container"></a></p>
<h3 id="284、内嵌-servlet-容器支持">28.4、内嵌 Servlet 容器支持</h3>
<p>Spring Boot 包含了对内嵌 <a href="https://tomcat.apache.org/" target="_blank">Tomcat</a>、<a href="https://www.eclipse.org/jetty/" target="_blank">Jetty</a> 和 <a href="http://undertow.io/" target="_blank">Undertow</a> 服务器的支持。大部分开发人员只需简单地使用对应的 Starter 来获取完整的配置实例。默认情况下，内嵌服务器将监听 <code>8080</code> 上的 HTTP 请求。</p>
<p><strong>警告</strong></p>
<blockquote>
<p>如果您选择在 <a href="https://www.centos.org/" target="_blank">CentOS</a> 使用 Tomcat，请注意，默认情况下，临时目录用于储存编译后的 JSP、上传的文件等。当您的应用程序运行时发生了故障，该目录可能会被 <code>tmpwatch</code> 删除。为了避免出现该情况，您可能需要自定义 <code>tmpwatch</code> 配置，使 <code>tomcat.*</code>目录不被删除，或者配置 <code>server.tomcat.basedir</code> 让 Tomcat 使用其他位置。</p>
</blockquote>
<p><a id="boot-features-embedded-container-servlets-filters-listeners"></a></p>
<h4 id="2841、servlet、filter-与-listener">28.4.1、Servlet、Filter 与 Listener</h4>
<p>使用内嵌 servlet 容器时，您可以使用 Spring bean 或者扫描方式来注册 Servlet 规范中的 Servlet、Filter 和所有监听器（比如 <code>HttpSessionListener</code>）。</p>
<p><a id="boot-features-embedded-container-servlets-filters-listeners-beans"></a></p>
<h5 id="28411、将-servlet、filter-和-listener-注册为-spring-bean">28.4.1.1、将 Servlet、Filter 和 Listener 注册为 Spring Bean</h5>
<p>任何 <code>Servlet</code>、<code>Filter</code> 或 <code>*Listener</code> 的 Spring bean 实例都将被注册到内嵌容器中。如果您想引用 <code>application.properties</code> 中的某个值，这可能会特别方便。</p>
<p>默认情况下，如果上下文只包含单个 Servlet，它将映射到 <code>/</code>。在多个 Servlet bean 的情况下，bean 的名称将用作路径的前缀。Filter 将映射到 <code>/*</code>。</p>
<p>如果基于约定配置的映射不够灵活，您可以使用 <code>ServletRegistrationBean</code>、<code>FilterRegistrationBean</code> 和 <code>ServletListenerRegistrationBean</code> 类来完全控制。</p>
<p>Spring Boot 附带了许多可以定义 Filter bean 的自动配置。以下是部分过滤器及其执行顺序的（顺序值越低，优先级越高）：</p>
<table>
<thead>
<tr>
<th>Servlet Filter</th>
<th>顺序</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>OrderedCharacterEncodingFilter</code></td>
<td><code>Ordered.HIGHEST_PRECEDENCE</code></td>
</tr>
<tr>
<td><code>WebMvcMetricsFilter</code></td>
<td><code>Ordered.HIGHEST_PRECEDENCE + 1</code></td>
</tr>
<tr>
<td><code>ErrorPageFilter</code></td>
<td><code>Ordered.HIGHEST_PRECEDENCE + 1</code></td>
</tr>
<tr>
<td><code>HttpTraceFilter</code></td>
<td><code>Ordered.LOWEST_PRECEDENCE - 10</code></td>
</tr>
</tbody>
</table>
<p>通常 Filter bean 无序放置也是安全的。</p>
<p>如果需要指定顺序，则应避免在 <code>Ordered.HIGHEST_PRECEDENCE</code> 顺序点配置读取请求体的过滤器，因为它的字符编码可能与应用程序的字符编码配置不一致。如果一个 Servlet 过滤器包装了请求，则应使用小于或等于 <code>OrderedFilter.REQUEST_WRAPPER_FILTER_MAX_ORDER</code>的顺序点对其进行配置。</p>
<p><a id="boot-features-embedded-container-context-initializer"></a></p>
<h4 id="2842、servlet-上下文初始化">28.4.2、Servlet 上下文初始化</h4>
<p>内嵌 servlet 容器不会直接执行 Servlet 3.0+ 的 <code>javax.servlet.ServletContainerInitializer</code> 接口或 Spring 的 <code>org.springframework.web.WebApplicationInitializer</code> 接口。这是一个有意的设计决策，旨在降低在 war 内运行时第三方类库产生的风险，防止破坏 Sring Boot 应用程序。</p>
<p>如果您需要在 Spring Boot 应用程序中执行 servlet 上下文初始化，则应注册一个实现了 <code>org.springframework.boot.context.embedded.ServletContextInitializer</code> 接口的 bean。<code>onStartup</code> 方法提供了针对 <code>ServletContext</code> 的访问入口，如果需要，它可以容易作为现有 <code>WebApplicationInitializer</code> 的适配器。</p>
<p><a id="boot-features-embedded-container-servlets-filters-listeners-scanning"></a></p>
<h5 id="28421、扫描-servlet、filter-和-listener">28.4.2.1、扫描 Servlet、Filter 和 Listener</h5>
<p>使用内嵌容器时，可以使用 <code>@ServletComponentScan</code> 启用带 <code>@WebServlet</code>、<code>@WebFilter</code> 和 <code>@WebListener</code> 注解的类自动注册。</p>
<p><strong>提示</strong></p>
<p><code>@ServletComponentScan</code> 在独立（standalone）容器中不起作用，因容器将使用内置发现机制来代替。</p>
<p><a id="boot-features-embedded-container-application-context"></a></p>
<h4 id="2843、servletwebserverapplicationcontext">28.4.3、ServletWebServerApplicationContext</h4>
<p>Spring Boot 底层使用了一个不同的 <code>ApplicationContext</code> 类型来支持内嵌 servlet。<code>ServletWebServerApplicationContext</code> 是一个特殊 <code>WebApplicationContext</code> 类型，它通过搜索单个 <code>ServletWebServerFactory</code> bean 来引导自身。通常，<code>TomcatServletWebServerFactory</code>、 <code>JettyServletWebServerFactory</code> 或者 <code>UndertowServletWebServerFactory</code> 中的一个将被自动配置。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>通常，你不需要知道这些实现类。大部分应用程序会自动配置，并为您创建合适的 <code>ApplicationContext</code> 和 <code>ServletWebServerFactory</code>。</p>
</blockquote>
<p><a id="boot-features-customizing-embedded-containers"></a></p>
<h5 id="2844、自定义内嵌-servlet-容器">28.4.4、自定义内嵌 Servlet 容器</h5>
<p>可以使用 Spring <code>Environment</code> 属性来配置通用的 servlet 容器设置。通常，您可以在 <code>application.properties</code> 文件中定义这些属性。</p>
<p>通用的服务器设置包括：</p>
<ul>
<li>网络设置：监听 HTTP 请求的端口（<code>server.port</code>），绑定接口地址到 <code>server.address</code> 等。</li>
<li>会话设置：是否持久会话（<code>server.session.persistence</code>）、session 超时（<code>server.session.timeout</code>）、会话数据存放位置（<code>server.session.store-dir</code>）和 session-cookie 配置（<code>server.session.cookie.*</code>）。</li>
<li>错误管理：错误页面位置（<code>server.error.path</code>）等。</li>
<li><a href="#howto-configure-ssl">SSL</a></li>
<li><a href="#how-to-enable-http-response-compression">HTTP 压缩</a></li>
</ul>
<p>Spring Boot 尽可能暴露通用的设置，但并不总是都可以。针对这些情况，专用的命名空间为特定的服务器提供了自定义功能（请参阅 <code>server.tomcat</code> 和 <code>server.undertow</code>）。例如，您可以使用内嵌 servlet 容器的特定功能来配置<a href="#howto-configure-accesslogs">访问日志</a>。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>有关完整的内容列表，请参阅 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.1.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/web/ServerProperties.java" target="_blank">ServerProperties</a> 类。</p>
</blockquote>
<p><a id="boot-features-programmatic-embedded-container-customization"></a></p>
<h6 id="28441、以编程方式自定义">28.4.4.1、以编程方式自定义</h6>
<p>如果您需要以编程的方式配置内嵌 servlet 容器，可以注册一个是实现了 <code>WebServerFactoryCustomizer</code> 接口的 Spring bean。<code>WebServerFactoryCustomizer</code> 提供了对 <code>ConfigurableServletWebServerFactory</code> 的访问入口，其中包含了许多自定义 setter 方法。以下示例使用了编程方式来设置端口：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>boot<span class="token punctuation">.</span>web<span class="token punctuation">.</span>server</span><span class="token punctuation">.</span><span class="token class-name">WebServerFactoryCustomizer</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>boot<span class="token punctuation">.</span>web<span class="token punctuation">.</span>servlet<span class="token punctuation">.</span>server</span><span class="token punctuation">.</span><span class="token class-name">ConfigurableServletWebServerFactory</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>stereotype</span><span class="token punctuation">.</span><span class="token class-name">Component</span><span class="token punctuation">;</span>

<span class="token annotation punctuation">@Component</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">CustomizationBean</span> <span class="token keyword">implements</span> <span class="token class-name">WebServerFactoryCustomizer</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">ConfigurableServletWebServerFactory</span><span class="token punctuation">&gt;</span></span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@Override</span>
    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">customize</span><span class="token punctuation">(</span><span class="token class-name">ConfigurableServletWebServerFactory</span> server<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        server<span class="token punctuation">.</span><span class="token function">setPort</span><span class="token punctuation">(</span><span class="token number">9000</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p><strong>注意</strong></p>
<blockquote>
<p><code>TomcatServletWebServerFactory</code>、<code>JettyServletWebServerFactory</code> 和 <code>UndertowServletWebServerFactory</code> 是 ConfigurableServletWebServerFactory 的具体子类，它们分别为 Tomcat、Jetty 和 Undertow 提供了额外的自定义 setter 方法。</p>
</blockquote>
<p><a id="boot-features-customizing-configurableservletwebserverfactory-directly"></a></p>
<h6 id="28442、直接自定义-configurableservletwebserverfactory">28.4.4.2、直接自定义 ConfigurableServletWebServerFactory</h6>
<p>如果上述的自定义方式太局限，您可以自己注册 <code>TomcatServletWebServerFactory</code>、<code>JettyServletWebServerFactory</code> 或 <code>UndertowServletWebServerFactory</code> bean。</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Bean</span>
<span class="token keyword">public</span> <span class="token class-name">ConfigurableServletWebServerFactory</span> <span class="token function">webServerFactory</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token class-name">TomcatServletWebServerFactory</span> factory <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">TomcatServletWebServerFactory</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    factory<span class="token punctuation">.</span><span class="token function">setPort</span><span class="token punctuation">(</span><span class="token number">9000</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    factory<span class="token punctuation">.</span><span class="token function">setSessionTimeout</span><span class="token punctuation">(</span><span class="token number">10</span><span class="token punctuation">,</span> <span class="token class-name">TimeUnit</span><span class="token punctuation">.</span>MINUTES<span class="token punctuation">)</span><span class="token punctuation">;</span>
    factory<span class="token punctuation">.</span><span class="token function">addErrorPages</span><span class="token punctuation">(</span><span class="token keyword">new</span> <span class="token class-name">ErrorPage</span><span class="token punctuation">(</span><span class="token class-name">HttpStatus</span><span class="token punctuation">.</span>NOT_FOUND<span class="token punctuation">,</span> <span class="token string">"/notfound.html"</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token keyword">return</span> factory<span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>
<p>Setter 方法提供了许多配置选项。还有几个 <strong>hook</strong> 保护方法供您深入定制。有关详细信息，请参阅<a href="https://docs.spring.io/spring-boot/docs/2.1.1.RELEASE/api/org/springframework/boot/web/servlet/server/ConfigurableServletWebServerFactory.html" target="_blank">源码文档</a>。</p>
<p><a id="boot-features-jsp-limitations"></a></p>
<h4 id="2845、jsp-局限">28.4.5、JSP 局限</h4>
<p>当运行使用了内嵌 servlet 容器的 Spring Boot 应用程序时（打包为可执行归档文件），JSP 支持将存在一些限制。</p>
<ul>
<li>如果您使用 war 打包，在 Jetty 和 Tomcat 中可以正常工作，使用 <code>java -jar</code> 启动时，可执行的 war 可正常使用，并且还可以部署到任何标准容器。使用可执行 jar 时不支持 JSP。</li>
<li>Undertow 不支持 JSP。</li>
<li>创建自定义的 error.jsp 页面不会覆盖默认<a href="#boot-features-error-handling">错误处理</a>视图，应该使用<a href="#boot-features-error-handling-custom-error-pages">自定义错误页面</a>来代替。</li>
</ul>
<p>这里有一个 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.1.RELEASE/spring-boot-samples/spring-boot-sample-web-jsp" target="_blank">JSP 示例</a>，您可以了解到如何配置。</p>
<p><a id="boot-features-reactive-server"></a></p>
<h3 id="285、内嵌响应式服务器支持">28.5、内嵌响应式服务器支持</h3>
<p>Spring Boot 包括对以下内嵌响应式 Web 服务器的支持：Reactor Netty、Tomcat、Jetty 和 Undertow。大多数开发人员使用对应的 <strong>Starter</strong> 来获取一个完全配置的实例。默认情况下，内嵌服务器在 8080 端口上监听 HTTP 请求。</p>
<p><a id="boot-features-reactive-server-resources"></a></p>
<h3 id="286、响应式服务器资源配置">28.6、响应式服务器资源配置</h3>
<p>在自动配置 Reactor Netty 或 Jetty 服务器时，Spring Boot 将创建特定的 bean 为服务器实例提供 HTTP 资源：<code>ReactorResourceFactory</code> 或 <code>JettyResourceFactory</code>。</p>
<p>默认情况下，这些资源也将与 Reactor Netty 和 Jetty 客户端共享以获得最佳性能，具体如下：</p>
<ul>
<li>用于服务器和客户端的的相同技术</li>
<li>客户端实例使用了 Spring Boot 自动配置的 <code>WebClient.Builder</code> bean 构建。</li>
</ul>
<p>开发人员可以通过提供自定义的 <code>ReactorResourceFactory</code> 或 <code>JettyResourceFactory</code> bean 来重写 Jetty 和 Reactor Netty 的资源配置 —— 将应用于客户端和服务器。</p>
<p>您可以在 <a href="#boot-features-webclient-runtime">WebClient Runtime</a> 章节中了解有关客户端资源配置的更多内容。</p>
<p><a id="boot-features-security"></a></p>
<h2 id="29、安全">29、安全</h2>
<p>默认情况下，如果 <a href="https://projects.spring.io/spring-security/" target="_blank">Spring Security</a> 在 classpath 上，则 Web 应用程序是受保护的。Spring Boot 依赖 Spring Security 的内容协商策略来确定是使用 <code>httpBasic</code> 还是 <code>formLogin</code>。要给 Web 应用程序添加方法级别的安全保护，可以使用 <code>@EnableGlobalMethodSecurity</code> 注解设置。有关更多其他信息，您可以在 <a href="https://docs.spring.io/spring-security/site/docs/5.1.2.RELEASE/reference/htmlsingle#jc-method" target="_blank">Spring Security 参考指南</a>中找到。</p>
<p>默认的 <code>UserDetailsS​​ervice</code> 只有一个用户。用户名为 <code>user</code>，密码是随机的，在应用程序启动时会以 INFO 级别打印出来，如下所示：</p>
<pre class="language-"><code>Using generated security password: 78fa095d-3f4c-48b1-ad50-e24c31d5cf35
</code></pre><p><strong>注意</strong></p>
<blockquote>
<p>如果您对日志配置进行微调，请确保将 <code>org.springframework.boot.autoconfigure.security</code> 的级别设置为 <code>INFO</code>。否则，默认密码不会打印出来。</p>
</blockquote>
<p>您可以通过提供 <code>spring.security.user.name</code> 和 <code>spring.security.user.password</code> 来更改用户名和密码。</p>
<p>您在 Web 应用程序中默认会获得以下基本功能：</p>
<ul>
<li>一个 <code>UserDetailsS​​ervice</code>（或 WebFlux 应用程序中的 <code>ReactiveUserDetailsS​​ervice</code>）bean，采用内存存储形式，有一个自动生成密码的用户（有关用户属性，请参阅 <a href="https://docs.spring.io/spring-boot/docs/2.1.1.RELEASE/api/org/springframework/boot/autoconfigure/security/SecurityProperties.User.html" target="_blank"><code>SecurityProperties.User</code></a>）。</li>
<li>用于整个应用程序（如果 actuator 在 classpath 上，则包括 actuator 端点）基于表单登录或 HTTP Basic 认证（取决于 Content-Type）。</li>
<li>一个用于发布身份验证事件的 <code>DefaultAuthenticationEventPublisher</code>。</li>
</ul>
<p>您可以通过为其添加一个 bean 来提供不同的 <code>AuthenticationEventPublisher</code>。</p>
<p><a id="boot-features-security-mvc"></a></p>
<h3 id="291、mvc-安全">29.1、MVC 安全</h3>
<p>默认的安全配置在 <code>SecurityAutoConfiguration</code> 和 <code>UserDetailsS​​erviceAutoConfiguration</code> 中实现。 <code>SecurityAutoConfiguration</code> 导入用于 Web 安全的 <code>SpringBootWebSecurityConfiguration</code>，<code>UserDetailsS​​erviceAutoConfiguration</code> 配置身份验证，这同样适用于非 Web 应用程序。要完全关闭默认的 Web 应用程序安全配置，可以添加 <code>WebSecurityConfigurerAdapter</code> 类型的 bean（这样做不会禁用 <code>UserDetailsS​​ervice</code> 配置或 Actuator 的安全保护）。</p>
<p>要同时关闭 <code>UserDetailsS​​ervice</code> 配置，您可以添加 <code>UserDetailsS​​ervice</code>、<code>AuthenticationProvider</code> 或 <code>AuthenticationManager</code> 类型的 bean。<a href="https://github.com/spring-projects/spring-boot/tree/v2.1.1.RELEASE/spring-boot-samples/" target="_blank">Spring Boot 示例</a>中有几个使用了安全保护的应用程序，他们或许可以帮助到您。</p>
<p>可以通过添加自定义 <code>WebSecurityConfigurerAdapter</code> 来重写访问规则。Spring Boot 提供了便捷方法，可用于重写 actuator 端点和静态资源的访问规则。<code>EndpointRequest</code> 可用于创建一个基于 <code>management.endpoints.web.base-path</code> 属性的 <code>RequestMatcher</code>。<code>PathRequest</code> 可用于为常用位置中的资源创建一个 <code>RequestMatcher</code>。</p>
<p><a id="boot-features-security-webflux"></a></p>
<h3 id="292、webflux-安全">29.2、WebFlux 安全</h3>
<p>与 Spring MVC 应用程序类似，您可以通过添加 <code>spring-boot-starter-security</code> 依赖来保护 WebFlux 应用程序。默认的安全配置在 <code>ReactiveSecurityAutoConfiguration</code> 和 <code>UserDetailsServiceAutoConfiguration</code> 中实现。<code>ReactiveSecurityAutoConfiguration</code> 导入用于 Web 安全的 <code>WebFluxSecurityConfiguration</code>，<code>UserDetailsServiceAutoConfiguration</code> 配置身份验证，这同样适用于非 Web 应用程序。要完全关闭默认的 Web 应用程序安全配置，可以添加 <code>WebFilterChainProxy</code> 类型的 bean（这样做不会禁用 <code>UserDetailsS​​ervice</code> 配置或 Actuator 的安全保护）。</p>
<p>要同时关闭 <code>UserDetailsS​​ervice</code> 配置，您可以添加 <code>ReactiveUserDetailsService</code> 或 <code>ReactiveAuthenticationManager</code> 类型的 bean。</p>
<p>可以通过添加自定义 <code>SecurityWebFilterChain</code> 来重写访问规则。Spring Boot 提供了便捷方法，可用于重写 actuator 端点和静态资源的访问规则。<code>EndpointRequest</code> 可用于创建一个基于 <code>management.endpoints.web.base-path</code> 属性的 <code>ServerWebExchangeMatcher</code>。</p>
<p><code>PathRequest</code> 可用于为常用位置中的资源创建一个 <code>ServerWebExchangeMatcher</code>。</p>
<p>例如，您可以通过添加以下内容来自定义安全配置：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Bean</span>
<span class="token keyword">public</span> <span class="token class-name">SecurityWebFilterChain</span> <span class="token function">springSecurityFilterChain</span><span class="token punctuation">(</span><span class="token class-name">ServerHttpSecurity</span> http<span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">return</span> http
        <span class="token punctuation">.</span><span class="token function">authorizeExchange</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
            <span class="token punctuation">.</span><span class="token function">matchers</span><span class="token punctuation">(</span><span class="token class-name">PathRequest</span><span class="token punctuation">.</span><span class="token function">toStaticResources</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">atCommonLocations</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">permitAll</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
            <span class="token punctuation">.</span><span class="token function">pathMatchers</span><span class="token punctuation">(</span><span class="token string">"/foo"</span><span class="token punctuation">,</span> <span class="token string">"/bar"</span><span class="token punctuation">)</span>
                <span class="token punctuation">.</span><span class="token function">authenticated</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">and</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
            <span class="token punctuation">.</span><span class="token function">formLogin</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">and</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
        <span class="token punctuation">.</span><span class="token function">build</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>
<p><a id="boot-features-security-oauth2"></a></p>
<h3 id="293、oauth2">29.3、OAuth2</h3>
<p><a href="https://oauth.net/2/" target="_blank">OAuth2</a> 是 Spring 支持的一种广泛使用的授权框架。</p>
<p><a id="boot-features-security-oauth2-client"></a></p>
<h4 id="2931、客户端">29.3.1、客户端</h4>
<p>如果您的 classpath 上有 <code>spring-security-oauth2-client</code>，则可以利用一些自动配置来轻松设置 <code>OAuth2/Open ID Connect 客户端。该配置使用</code>OAuth2ClientProperties` 的属性。相同的属性适用于 servlet 和响应式应用程序。</p>
<p>您可以在 <code>spring.security.oauth2.client</code> 前缀下注册多个 OAuth2 客户端和提供者（provider），如下所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.security.oauth2.client.registration.my-client-1.client-id</span><span class="token attr-value"><span class="token punctuation">=</span>abcd</span>
<span class="token constant">spring.security.oauth2.client.registration.my-client-1.client-secret</span><span class="token attr-value"><span class="token punctuation">=</span>password</span>
<span class="token constant">spring.security.oauth2.client.registration.my-client-1.client-name</span><span class="token attr-value"><span class="token punctuation">=</span>Client for user scope</span>
<span class="token constant">spring.security.oauth2.client.registration.my-client-1.provider</span><span class="token attr-value"><span class="token punctuation">=</span>my-oauth-provider</span>
<span class="token constant">spring.security.oauth2.client.registration.my-client-1.scope</span><span class="token attr-value"><span class="token punctuation">=</span>user</span>
<span class="token constant">spring.security.oauth2.client.registration.my-client-1.redirect-uri-template</span><span class="token attr-value"><span class="token punctuation">=</span>http://my-redirect-uri.com</span>
<span class="token constant">spring.security.oauth2.client.registration.my-client-1.client-authentication-method</span><span class="token attr-value"><span class="token punctuation">=</span>basic</span>
<span class="token constant">spring.security.oauth2.client.registration.my-client-1.authorization-grant-type</span><span class="token attr-value"><span class="token punctuation">=</span>authorization_code</span>

<span class="token constant">spring.security.oauth2.client.registration.my-client-2.client-id</span><span class="token attr-value"><span class="token punctuation">=</span>abcd</span>
<span class="token constant">spring.security.oauth2.client.registration.my-client-2.client-secret</span><span class="token attr-value"><span class="token punctuation">=</span>password</span>
<span class="token constant">spring.security.oauth2.client.registration.my-client-2.client-name</span><span class="token attr-value"><span class="token punctuation">=</span>Client for email scope</span>
<span class="token constant">spring.security.oauth2.client.registration.my-client-2.provider</span><span class="token attr-value"><span class="token punctuation">=</span>my-oauth-provider</span>
<span class="token constant">spring.security.oauth2.client.registration.my-client-2.scope</span><span class="token attr-value"><span class="token punctuation">=</span>email</span>
<span class="token constant">spring.security.oauth2.client.registration.my-client-2.redirect-uri-template</span><span class="token attr-value"><span class="token punctuation">=</span>http://my-redirect-uri.com</span>
<span class="token constant">spring.security.oauth2.client.registration.my-client-2.client-authentication-method</span><span class="token attr-value"><span class="token punctuation">=</span>basic</span>
<span class="token constant">spring.security.oauth2.client.registration.my-client-2.authorization-grant-type</span><span class="token attr-value"><span class="token punctuation">=</span>authorization_code</span>

<span class="token constant">spring.security.oauth2.client.provider.my-oauth-provider.authorization-uri</span><span class="token attr-value"><span class="token punctuation">=</span>http://my-auth-server/oauth/authorize</span>
<span class="token constant">spring.security.oauth2.client.provider.my-oauth-provider.token-uri</span><span class="token attr-value"><span class="token punctuation">=</span>http://my-auth-server/oauth/token</span>
<span class="token constant">spring.security.oauth2.client.provider.my-oauth-provider.user-info-uri</span><span class="token attr-value"><span class="token punctuation">=</span>http://my-auth-server/userinfo</span>
<span class="token constant">spring.security.oauth2.client.provider.my-oauth-provider.user-info-authentication-method</span><span class="token attr-value"><span class="token punctuation">=</span>header</span>
<span class="token constant">spring.security.oauth2.client.provider.my-oauth-provider.jwk-set-uri</span><span class="token attr-value"><span class="token punctuation">=</span>http://my-auth-server/token_keys</span>
<span class="token constant">spring.security.oauth2.client.provider.my-oauth-provider.user-name-attribute</span><span class="token attr-value"><span class="token punctuation">=</span>name</span>
</code></pre>
<p>对于支持 <a href="https://openid.net/specs/openid-connect-discovery-1_0.html" target="_blank">OpenID Connect 发现</a>的 OpenID Connect 提供者，可以进一步简化配置。需要使用 <code>issuer-uri</code> 配置提供者，<code>issuer-uri</code> 是其 Issuer Identifier 的 URI。例如，如果提供的 <code>issuer-uri</code> 是 “<a href="https://example.com”，则将对" target="_blank">https://example.com”，则将对</a> “<a href="https://example.com/.well-known/openid-configuration”" target="_blank">https://example.com/.well-known/openid-configuration”</a> 发起一个 <code>OpenID Provider Configuration Request</code>。期望结果是一个 <code>OpenID Provider Configuration Response</code>。以下示例展示了如何使用 <code>issuer-uri</code> 配置一个 OpenID Connect Provider：</p>
<pre class="language-"><code>spring.security.oauth2.client.provider.oidc-provider.issuer-uri=https://dev-123456.oktapreview.com/oauth2/default/
</code></pre><p>默认情况下，Spring Security 的 <code>OAuth2LoginAuthenticationFilter</code> 仅处理与 <code>/login/oauth2/code/*</code> 相匹配的 URL。如果要自定义 <code>redirect-uri</code> 以使用其他匹配模式，则需要提供配置以处理该自定义模式。例如，对于 servlet 应用程序，您可以添加类似于以下 <code>WebSecurityConfigurerAdapter</code>：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">OAuth2LoginSecurityConfig</span> <span class="token keyword">extends</span> <span class="token class-name">WebSecurityConfigurerAdapter</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@Override</span>
    <span class="token keyword">protected</span> <span class="token keyword">void</span> <span class="token function">configure</span><span class="token punctuation">(</span><span class="token class-name">HttpSecurity</span> http<span class="token punctuation">)</span> <span class="token keyword">throws</span> <span class="token class-name">Exception</span> <span class="token punctuation">{</span>
        http
            <span class="token punctuation">.</span><span class="token function">authorizeRequests</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
                <span class="token punctuation">.</span><span class="token function">anyRequest</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">authenticated</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
                <span class="token punctuation">.</span><span class="token function">and</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
            <span class="token punctuation">.</span><span class="token function">oauth2Login</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
                <span class="token punctuation">.</span><span class="token function">redirectionEndpoint</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
                    <span class="token punctuation">.</span><span class="token function">baseUri</span><span class="token punctuation">(</span><span class="token string">"/custom-callback"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<p><a id="boot-features-security-oauth2-common-providers"></a></p>
<p><strong>OAuth2 客户端注册常见的提供者</strong></p>
<p>对于常见的 OAuth2 和 OpenID 提供者（provider），包括 Google、Github、Facebook 和 Okta，我们提供了一组提供者默认设置（分别是 <code>google</code>、<code>github</code>、<code>facebook</code> 和 <code>okta</code>）。</p>
<p>如果您不需要自定义这些提供者，则可以将 <code>provider</code> 属性设置为您需要推断默认值的属性。此外，如果客户端注册的 key 与默认支持的提供者匹配，则 Spring Boot 也会推断出来。</p>
<p>换而言之，以下示例中的两个配置使用了 Google 提供者：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.security.oauth2.client.registration.my-client.client-id</span><span class="token attr-value"><span class="token punctuation">=</span>abcd</span>
<span class="token constant">spring.security.oauth2.client.registration.my-client.client-secret</span><span class="token attr-value"><span class="token punctuation">=</span>password</span>
<span class="token constant">spring.security.oauth2.client.registration.my-client.provider</span><span class="token attr-value"><span class="token punctuation">=</span>google</span>

<span class="token constant">spring.security.oauth2.client.registration.google.client-id</span><span class="token attr-value"><span class="token punctuation">=</span>abcd</span>
<span class="token constant">spring.security.oauth2.client.registration.google.client-secret</span><span class="token attr-value"><span class="token punctuation">=</span>password</span>
</code></pre>
<p><a id="boot-features-security-oauth2-server"></a></p>
<h4 id="2932、资源服务器">29.3.2、资源服务器</h4>
<p>如果在 classpath 上有 <code>spring-security-oauth2-resource-server</code>，只要指定了 JWK Set URI 或 OIDC Issuer URI，Spring Boot 就可以设置 OAuth2 资源服务器，如下所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.security.oauth2.resourceserver.jwt.jwk-set-uri</span><span class="token attr-value"><span class="token punctuation">=</span>https://example.com/oauth2/default/v1/keys</span>
</code></pre>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.security.oauth2.resourceserver.jwt.issuer-uri</span><span class="token attr-value"><span class="token punctuation">=</span>https://dev-123456.oktapreview.com/oauth2/default/</span>
</code></pre>
<p>相同的属性适用于 servlet 和响应式应用程序。</p>
<p>或者，您可以为 servlet 应用程序定义自己的 <code>JwtDecoder</code> bean，或为响应式应用程序定义 <code>ReactiveJwtDecoder</code>。</p>
<p><a id="_authorization_server"></a></p>
<h4 id="2933、授权服务器">29.3.3、授权服务器</h4>
<p>目前，Spring Security 没有提供 OAuth 2.0 授权服务器实现。但此功能可从 <a href="https://projects.spring.io/spring-security-oauth/" target="_blank">Spring Security OAuth</a> 项目获得，该项目最终会被 Spring Security 所取代。在此之前，您可以使用 <code>spring-security-oauth2-autoconfigure</code> 模块轻松设置 OAuth 2.0 授权服务器，请参阅其<a href="https://docs.spring.io/spring-security-oauth2-boot" target="_blank">文档</a>以获取详细信息。</p>
<p><a id="boot-features-security-actuator"></a></p>
<h3 id="294、actuator-安全">29.4、Actuator 安全</h3>
<p>出于安全考虑，默认情况下禁用除 <code>/health</code> 和 <code>/info</code> 之外的所有 actuator。可用 <code>management.endpoints.web.exposure.include</code> 属性启用 actuator。</p>
<p>如果 Spring Security 位于 classpath 上且没有其他 <code>WebSecurityConfigurerAdapter</code>，则除了 <code>/health</code> 和 <code>/info</code> 之外的所有 actuator 都由 Spring Boot 自动配置保护。如果您定义了自定义 <code>WebSecurityConfigurerAdapter</code>，则 Spring Boot 自动配置将不再生效，您可以完全控制 actuator 的访问规则。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>在设置 <code>management.endpoints.web.exposure.include</code> 之前，请确保暴露的 actuator 没有包含敏感信息和 <code>/</code> 或被防火墙保护亦或受 Spring Security 之类的保护。</p>
</blockquote>
<p><a id="boot-features-security-csrf"></a></p>
<h4 id="2941、跨站请求伪造保护">29.4.1、跨站请求伪造保护</h4>
<p>由于 Spring Boot 依赖 Spring Security 的默认值配置，因此默认情况下会启用 CSRF 保护。这意味着当使用默认安全配置时，需要 <code>POST</code>（shutdown 和 loggers 端点）、<code>PUT</code> 或 <code>DELETE</code> 的 actuator 端点将返回 403 禁止访问错误。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>我们建议仅在创建非浏览器客户端使用的服务时才完全禁用 CSRF 保护。</p>
</blockquote>
<p>有关 CSRF 保护的其他信息，请参阅 <a href="https://docs.spring.io/spring-security/site/docs/5.1.2.RELEASE/reference/htmlsingle#csrf" target="_blank">Spring Security 参考指南</a>。</p>
<p><a id="boot-features-sql"></a></p>
<h2 id="30、使用-sql-数据库">30、使用 SQL 数据库</h2>
<p><a href="https://projects.spring.io/spring-framework/" target="_blank">Spring Framework</a> 为 SQL 数据库提供了广泛的支持。从直接使用 <code>JdbcTemplate</code> 进行 JDBC 访问到完全的<strong>对象关系映射</strong>（object relational mapping）技术，比如 Hibernate。<a href="https://projects.spring.io/spring-data/" target="_blank">Spring Data</a> 提供了更多级别的功能，直接从接口创建的 <code>Repository</code> 实现，并使用了约定从方法名生成查询。</p>
<p><a id="boot-features-configure-datasource"></a></p>
<h3 id="301、配置数据源">30.1、配置数据源</h3>
<p>Java 的 <code>javax.sql.DataSource</code> 接口提供了一个使用数据库连接的标准方法。通常，数据源使用 <code>URL</code> 和一些凭据信息来建立数据库连接。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>查看 <a href="#howto-configure-a-datasource">How-to</a> 部分获取更多高级示例，通常您可以完全控制数据库的配置。</p>
</blockquote>
<p><a id="boot-features-embedded-database-support"></a></p>
<h4 id="3011、内嵌数据库支持">30.1.1、内嵌数据库支持</h4>
<p>使用内嵌内存数据库来开发应用程序非常方便的。显然，内存数据库不提供持久存储。在应用启动时，您需要填充数据库，并在应用程序结束时丢弃数据。</p>
<p><strong>提示</strong></p>
<blockquote>
<p><strong>How-to</strong> 部分包含了<a href="#howto-database-initialization">如何初始化数据库</a>方面的内容。</p>
</blockquote>
<p>Spring Boot 可以自动配置内嵌 <a href="http://www.h2database.com/" target="_blank">H2</a>、<a href="http://hsqldb.org/" target="_blank">HSQL</a> 和 <a href="https://db.apache.org/derby/" target="_blank">Derby</a> 数据库。您不需要提供任何连接 URL，只需为您想要使用的内嵌数据库引入特定的构建依赖。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>如果您在测试中使用此功能，您可能会注意到，无论使用了多少应用程序上下文，整个测试套件都会重复使用相同的数据库。如果您想确保每个上下文都有一个单独的内嵌数据库，则应该将 <code>spring.datasource.generate-unique-name</code> 设置为 <code>true</code>。</p>
</blockquote>
<p>以下是 POM 依赖示例：</p>
<pre class="language-"><code class="lang-xml"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependency</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>groupId</span><span class="token punctuation">&gt;</span></span>org.springframework.boot<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>groupId</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>artifactId</span><span class="token punctuation">&gt;</span></span>spring-boot-starter-data-jpa<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>artifactId</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependency</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependency</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>groupId</span><span class="token punctuation">&gt;</span></span>org.hsqldb<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>groupId</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>artifactId</span><span class="token punctuation">&gt;</span></span>hsqldb<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>artifactId</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>scope</span><span class="token punctuation">&gt;</span></span>runtime<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>scope</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependency</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<p><strong>注意</strong></p>
<blockquote>
<p>要自动配置内嵌数据库，您需要一个 <code>spring-jdbc</code> 依赖。在这个例子中，它是通过 <code>spring-boot-starter-data-jpa</code> 引入。</p>
</blockquote>
<p><strong>提示</strong></p>
<blockquote>
<p>如果出于某些原因，您需要配置内嵌数据库的连接 URL，则应注意确保禁用数据库的自动关闭功能。如果您使用 H2，则应该使用 <code>DB_CLOSE_ON_EXIT=FALSE</code> 来设置。如果您使用 <code>HSQLDB</code>，则确保不使用 <code>shutdown=true</code>。禁用数据库的自动关闭功能允许 Spring Boot 控制数据库何时关闭，从而确保一旦不再需要访问数据库时就触发。</p>
</blockquote>
<p><a id="boot-features-connect-to-production-database"></a></p>
<h4 id="3012、连接生产数据库">30.1.2、连接生产数据库</h4>
<p>生产数据库连接也可以使用使用 <code>DataSource</code> 自动配置。Spring Boot 使用以下算法来选择一个特定的实现：</p>
<ul>
<li>出于性能和并发性的考虑，我们更喜欢 <a href="https://github.com/brettwooldridge/HikariCP" target="_blank">HikariCP</a> 连接池。如果 HikariCP 可用，我们总是选择它。</li>
<li>否则，如果 Tomcat 池 <code>DataSource</code> 可用，我们将使用它。</li>
<li>如果 HikariCP 和 Tomcat 池数据源不可用，但 <a href="https://commons.apache.org/proper/commons-dbcp/" target="_blank">Commons DBCP</a> 可用，我们将使用它。</li>
</ul>
<p>如果您使用了 <code>spring-boot-starter-jdbc</code> 或者 <code>spring-boot-starter-data-jpa</code> starter，您将自动得到 <code>HikariCP</code> 依赖。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>您完全可以绕过该算法，并通过 <code>spring.datasource.type</code> 属性指定要使用的连接池。如果您在 Tomcat 容器中运行应用程序，默认提供 <code>tomcat-jdbc</code>，这点尤其重要。</p>
</blockquote>
<p><strong>提示</strong></p>
<blockquote>
<p>可以手动配置其他连接池。如果您定义了自己的 <code>DataSource</code> bean，则自动配置将不会触发。</p>
</blockquote>
<p>数据源配置由 <code>spring.datasource.*</code> 中的外部属性所控制。例如，您可以在 <code>application.properties</code> 中声明以下部分：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.datasource.url</span><span class="token attr-value"><span class="token punctuation">=</span>jdbc:mysql://localhost/test</span>
<span class="token constant">spring.datasource.username</span><span class="token attr-value"><span class="token punctuation">=</span>dbuser</span>
<span class="token constant">spring.datasource.password</span><span class="token attr-value"><span class="token punctuation">=</span>dbpass</span>
<span class="token constant">spring.datasource.driver-class-name</span><span class="token attr-value"><span class="token punctuation">=</span>com.mysql.jdbc.Driver</span>
</code></pre>
<p><strong>注意</strong></p>
<blockquote>
<p>您至少应该使用 <code>spring.datasource.url</code> 属性来指定 URL，否则 Spring Boot 将尝试自动配置内嵌数据库。</p>
</blockquote>
<p><strong>提示</strong></p>
<blockquote>
<p>通常您不需要指定 <code>driver-class-name</code>，因为 Spring boot 可以从 <code>url</code> 推导出大多数数据库。</p>
</blockquote>
<p><strong>注意</strong></p>
<blockquote>
<p>对于要创建的池 <code>DataSource</code>，我们需要能够验证有效的 <code>Driver</code> 类是否可用，因此我们在使用之前进行检查。例如，如果您设置了 <code>spring.datasource.driver-class-name=com.mysql.jdbc.Driver</code>，那么该类必须可加载。</p>
</blockquote>
<p>有关更多支持选项，请参阅 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.1.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/jdbc/DataSourceProperties.java" target="_blank">DataSourceProperties</a>。这些都是标准选项，与实际的实现无关。还可以使用各自的前缀（<code>spring.datasource.hikari.*</code>、<code>spring.datasource.tomcat.*</code> 和 <code>spring.datasource.dbcp2.*</code>）微调实现特定的设置。请参考您现在使用的连接池实现的文档来获取更多信息。</p>
<p>例如，如果你使用 <a href="https://tomcat.apache.org/tomcat-8.0-doc/jdbc-pool.html#Common_Attributes" target="_blank">Tomcat 连接池</a>，则可以自定义许多其他设置，如下：</p>
<pre class="language-"><code class="lang-ini"><span class="token comment"># Number of ms to wait before throwing an exception if no connection is available.</span>
<span class="token constant">spring.datasource.tomcat.max-wait</span><span class="token attr-value"><span class="token punctuation">=</span>10000</span>

<span class="token comment"># Maximum number of active connections that can be allocated from this pool at the same time.</span>
<span class="token constant">spring.datasource.tomcat.max-active</span><span class="token attr-value"><span class="token punctuation">=</span>50</span>

<span class="token comment"># Validate the connection before borrowing it from the pool.</span>
<span class="token constant">spring.datasource.tomcat.test-on-borrow</span><span class="token attr-value"><span class="token punctuation">=</span>true</span>
</code></pre>
<p><a id="boot-features-connecting-to-a-jndi-datasource"></a></p>
<h4 id="3013、连接-jndi-数据源">30.1.3、连接 JNDI 数据源</h4>
<p>如果要将 Spring Boot 应用程序部署到应用服务器（Application Server）上，您可能想使用应用服务器的内置功能和 JNDI 访问方式来配置和管理数据源。</p>
<p><code>spring.datasource.jndi-name</code> 属性可作为 <code>spring.datasource.url</code>、<code>spring.datasource.username</code> 和 <code>spring.datasource.password</code> 属性的替代方法，用于从特定的 JNDI 位置访问 <code>DataSource</code>。例如，<code>application.properties</code> 中的以下部分展示了如何访问 JBoss AS 定义的 <code>DataSource</code>：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.datasource.jndi-name</span><span class="token attr-value"><span class="token punctuation">=</span>java:jboss/datasources/customers</span>
</code></pre>
<p><a id="boot-features-using-jdbc-template"></a></p>
<h3 id="302、使用-jdbctemplate">30.2、使用 JdbcTemplate</h3>
<p>Spring 的 <code>JdbcTemplate</code> 和 <code>NamedParameterJdbcTemplate</code> 类是自动配置的，您可以使用 <code>@Autowire</code> 将它们直接注入您的 bean 中：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>beans<span class="token punctuation">.</span>factory<span class="token punctuation">.</span>annotation</span><span class="token punctuation">.</span><span class="token class-name">Autowired</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>jdbc<span class="token punctuation">.</span>core</span><span class="token punctuation">.</span><span class="token class-name">JdbcTemplate</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>stereotype</span><span class="token punctuation">.</span><span class="token class-name">Component</span><span class="token punctuation">;</span>

<span class="token annotation punctuation">@Component</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyBean</span> <span class="token punctuation">{</span>

    <span class="token keyword">private</span> <span class="token keyword">final</span> <span class="token class-name">JdbcTemplate</span> jdbcTemplate<span class="token punctuation">;</span>

    <span class="token annotation punctuation">@Autowired</span>
    <span class="token keyword">public</span> <span class="token class-name">MyBean</span><span class="token punctuation">(</span><span class="token class-name">JdbcTemplate</span> jdbcTemplate<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>jdbcTemplate <span class="token operator">=</span> jdbcTemplate<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token comment">// ...</span>

<span class="token punctuation">}</span>
</code></pre>
<p>您可以使用 <code>spring.jdbc.template.*</code> 属性来自定义一些 template 的属性，如下：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.jdbc.template.max-rows</span><span class="token attr-value"><span class="token punctuation">=</span>500</span>
</code></pre>
<p><strong>注意</strong></p>
<blockquote>
<p><code>NamedParameterJdbcTemplate</code> 在底层重用了相同的 <code>JdbcTemplate</code> 实例。如果定义了多个 <code>JdbcTemplate</code> 且没有声明 primary 主候选，则不会自动配置 <code>NamedParameterJdbcTemplate</code>。</p>
</blockquote>
<p><a id="boot-features-jpa-and-spring-data"></a></p>
<h3 id="303、jpa-与-spring-data-jpa">30.3、JPA 与 Spring Data JPA</h3>
<p>Java Persistence API（Java 持久化 API）是一项标准技术，可让您将对象<strong>映射</strong>到关系数据库。<code>spring-boot-starter-data-jpa</code> POM 提供了一个快速起步的方法。它提供了以下关键依赖：</p>
<ul>
<li><strong>Hibernate</strong>  ——  最受欢迎的 JPA 实现之一。</li>
<li><strong>Spring Data JPA</strong> ——  可以轻松地实现基于 JPA 的资源库。</li>
<li><strong>Spring ORM</strong>  ——  Spring Framework 的核心 ORM 支持</li>
</ul>
<p><strong>提示</strong></p>
<blockquote>
<p>我们不会在这里介绍太多关于 JPA 或者 <a href="https://projects.spring.io/spring-data/" target="_blank">Spring Data</a> 的相关内容。您可以在 <a href="https://spring.io/" target="_blank">spring.io</a> 上查看<a href="https://spring.io/guides/gs/accessing-data-jpa/" target="_blank">使用 JPA 访问数据</a>，获取阅读 <a href="https://projects.spring.io/spring-data-jpa/" target="_blank">Spring Data JPA</a> 和 <a href="https://hibernate.org/orm/documentation/" target="_blank">Hibernate</a> 的参考文档。</p>
</blockquote>
<p><a id="boot-features-jpa-and-spring-data"></a></p>
<h4 id="3031、实体类">30.3.1、实体类</h4>
<p>通常，JPA <strong>Entity</strong>（实体）类是在 <code>persistence.xml</code> 文件中指定的。使用了 Spring Boot，该文件将不是必需的，可以使用 <strong>Entity Scanning</strong>（实体扫描）来代替。默认情况下，将搜索主配置类（使用了 <code>@EnableAutoConfiguration</code> 或 <code>@SpringBootApplication</code> 注解）下面的所有包。</p>
<p>任何用了 <code>@Entity</code>、<code>@Embeddable</code> 或者 <code>@MappedSuperclass</code> 注解的类将被考虑。一个典型的实体类如下：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">package</span> <span class="token namespace">com<span class="token punctuation">.</span>example<span class="token punctuation">.</span>myapp<span class="token punctuation">.</span>domain</span><span class="token punctuation">;</span>

<span class="token keyword">import</span> <span class="token namespace">java<span class="token punctuation">.</span>io</span><span class="token punctuation">.</span><span class="token class-name">Serializable</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">javax<span class="token punctuation">.</span>persistence</span><span class="token punctuation">.</span>*<span class="token punctuation">;</span>

<span class="token annotation punctuation">@Entity</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">City</span> <span class="token keyword">implements</span> <span class="token class-name">Serializable</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@Id</span>
    <span class="token annotation punctuation">@GeneratedValue</span>
    <span class="token keyword">private</span> <span class="token class-name">Long</span> id<span class="token punctuation">;</span>

    <span class="token annotation punctuation">@Column</span><span class="token punctuation">(</span>nullable <span class="token operator">=</span> <span class="token boolean">false</span><span class="token punctuation">)</span>
    <span class="token keyword">private</span> <span class="token class-name">String</span> name<span class="token punctuation">;</span>

    <span class="token annotation punctuation">@Column</span><span class="token punctuation">(</span>nullable <span class="token operator">=</span> <span class="token boolean">false</span><span class="token punctuation">)</span>
    <span class="token keyword">private</span> <span class="token class-name">String</span> state<span class="token punctuation">;</span>

    <span class="token comment">// ... additional members, often include @OneToMany mappings</span>

    <span class="token keyword">protected</span> <span class="token class-name">City</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment">// no-args constructor required by JPA spec</span>
        <span class="token comment">// this one is protected since it shouldn't be used directly</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token class-name">City</span><span class="token punctuation">(</span><span class="token class-name">String</span> name<span class="token punctuation">,</span> <span class="token class-name">String</span> state<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>name <span class="token operator">=</span> name<span class="token punctuation">;</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>state <span class="token operator">=</span> state<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token class-name">String</span> <span class="token function">getName</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> <span class="token keyword">this</span><span class="token punctuation">.</span>name<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token class-name">String</span> <span class="token function">getState</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> <span class="token keyword">this</span><span class="token punctuation">.</span>state<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token comment">// ... etc</span>

<span class="token punctuation">}</span>
</code></pre>
<p><strong>提示</strong></p>
<blockquote>
<p>您可以使用 <code>@EntityScan</code> 注解自定义实体类的扫描位置。请参见<a href="https://docs.spring.io/spring-boot/docs/2.1.1.RELEASE/reference/htmlsingle/#howto-separate-entity-definitions-from-spring-configuration" target="_blank">84.4、从 Spring configuration 配置中分离 @Entity 定义</a>章节。</p>
</blockquote>
<p><a id="boot-features-spring-data-jpa-repositories"></a></p>
<h4 id="3032、spring-data-jpa-资源库">30.3.2、Spring Data JPA 资源库</h4>
<p><a href="https://projects.spring.io/spring-data-jpa/" target="_blank">Spring Data JPA</a> 资源库（repository）是接口，您可以定义用于访问数据。JAP 查询是根据您的方法名自动创建。例如，<code>CityRepository</code> 接口可以声明 <code>findAllByState(String state)</code> 方法来查找指定状态下的所有城市。</p>
<p>对于更加复杂的查询，您可以使用 Spring Data 的 <a href="https://docs.spring.io/spring-data/jpa/docs/current/api/org/springframework/data/jpa/repository/Query.html" target="_blank"><code>Query</code></a> 注解</p>
<p>Spring Data 资源库通常继承自 <a href="https://docs.spring.io/spring-data/commons/docs/current/api/org/springframework/data/repository/Repository.html" target="_blank">Repository</a> 或者 <a href="https://docs.spring.io/spring-data/commons/docs/current/api/org/springframework/data/repository/CrudRepository.html" target="_blank">CrudRepository</a> 接口。如果您使用了自动配置，则将从包含主配置类（使用了 <code>@EnableAutoConfiguration</code> 或 <code>@SpringBootApplication</code> 注解）的包中搜索资源库：</p>
<p>以下是一个典型的 Spring Data 资源库接口定义：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">package</span> <span class="token namespace">com<span class="token punctuation">.</span>example<span class="token punctuation">.</span>myapp<span class="token punctuation">.</span>domain</span><span class="token punctuation">;</span>

<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>data<span class="token punctuation">.</span>domain</span><span class="token punctuation">.</span>*<span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>data<span class="token punctuation">.</span>repository</span><span class="token punctuation">.</span>*<span class="token punctuation">;</span>

<span class="token keyword">public</span> <span class="token keyword">interface</span> <span class="token class-name">CityRepository</span> <span class="token keyword">extends</span> <span class="token class-name">Repository</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">City</span><span class="token punctuation">,</span> <span class="token class-name">Long</span><span class="token punctuation">&gt;</span></span> <span class="token punctuation">{</span>

    <span class="token class-name">Page</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">City</span><span class="token punctuation">&gt;</span></span> <span class="token function">findAll</span><span class="token punctuation">(</span><span class="token class-name">Pageable</span> pageable<span class="token punctuation">)</span><span class="token punctuation">;</span>

    <span class="token class-name">City</span> <span class="token function">findByNameAndStateAllIgnoringCase</span><span class="token punctuation">(</span><span class="token class-name">String</span> name<span class="token punctuation">,</span> <span class="token class-name">String</span> state<span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token punctuation">}</span>
</code></pre>
<p>Spring Data JPA 资源库支持三种不同的引导模式：default、deferred 和 lazy。要启用延迟或懒惰引导，请将 <code>spring.data.jpa.repositories.bootstrap-mode</code> 分别设置为 <code>deferred</code> 或 <code>lazy</code>。使用延迟或延迟引导时，自动配置的 <code>EntityManagerFactoryBuilder</code> 将使用上下文的异步任务执行器（如果有）作为引导程序执行器。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>我们几乎没有接触到 Spring Data JPA 的表面内容。有关详细信息，请查阅 <a href="https://docs.spring.io/spring-data/jpa/docs/current/reference/html/" target="_blank">Spring Data JPA 参考文档</a>。</p>
</blockquote>
<p><a id="boot-features-creating-and-dropping-jpa-databases"></a></p>
<h4 id="3033、创建和删除-jpa-数据库">30.3.3、创建和删除 JPA 数据库</h4>
<p>默认情况下，<strong>仅</strong>当您使用了内嵌数据库（H2、HSQL 或 Derby）时才会自动创建 JPA 数据库。您可以使用 <code>spring.jpa.*</code> 属性显式配置 JPA 设置。例如，要创建和删除表，您可以将以下内容添加到 <code>application.properties</code> 中：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.jpa.hibernate.ddl-auto</span><span class="token attr-value"><span class="token punctuation">=</span>create-drop</span>
</code></pre>
<p><strong>注意</strong></p>
<blockquote>
<p>关于上述功能，Hibernate 自己的内部属性名称（如果您记住更好）为 <code>hibernate.hbm2ddl.auto</code>。您可以使用 <code>spring.jpa.properties.*</code>（在添加到实体管理器之前，该前缀将被删除）来将 Hibernate 原生属性一同设置：</p>
</blockquote>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.jpa.properties.hibernate.globally_quoted_identifiers</span><span class="token attr-value"><span class="token punctuation">=</span>true</span>
</code></pre>
<p>上面示例中将 <code>true</code> 值设置给 <code>hibernate.globally_quoted_identifiers</code> 属性，该属性将传给 Hibernate 实体管理器。</p>
<p>默认情况下，DDL 执行（或验证）将延迟到 <code>ApplicationContext</code> 启动后。还有一个 <code>spring.jpa.generate-ddl</code> 标志，如果 Hibernate 自动配置是激活的，那么它将不会被使用，因为 <code>ddl-auto</code> 设置更细粒度。</p>
<p><a id="boot-features-jpa-in-web-environment"></a></p>
<h4 id="3034、在视图中打开-entitymanager">30.3.4、在视图中打开 EntityManager</h4>
<p>如果您正在运行 web 应用程序，Spring Boot 将默认注册 <a href="https://docs.spring.io/spring/docs/5.1.3.RELEASE/javadoc-api/org/springframework/orm/jpa/support/OpenEntityManagerInViewInterceptor.html" target="_blank"><code>OpenEntityManagerInViewInterceptor</code></a> 用于<strong>在视图中打开 EntityManager</strong> 模式，即运允许在 web 视图中延迟加载。如果您不想开启这个行为，则应在 <code>application.properties</code> 中将 <code>spring.jpa.open-in-view</code> 设置为 <code>false</code>。</p>
<p><a id="boot-features-data-jdbc"></a></p>
<h3 id="304、spring-data-jdbc">30.4、Spring Data JDBC</h3>
<p>Spring Data 包含了对 JDBC 资源库的支持，并将自动为 <code>CrudRepository</code> 上的方法生成 SQL。对于更高级的查询，它提供了 <code>@Query</code> 注解。</p>
<p>当 classpath 下存在必要的依赖时，Spring Boot 将自动配置 Spring Data 的 JDBC 资源库。可以通过添加单个 <code>spring-boot-starter-data-jdbc</code> 依赖引入到项目中。如有必要，可通过在应用程序中添加 <code>@EnableJdbcRepositories</code> 注解或 <code>JdbcConfiguration</code> 子类来控制 Spring Data JDBC 的配置。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>有关 Spring Data JDBC 的完整详细信息，请参阅<a href="https://projects.spring.io/spring-data-jdbc/" target="_blank">参考文档</a>。</p>
</blockquote>
<p><a id="boot-features-sql-h2-console"></a></p>
<h3 id="305、使用-h2-的-web-控制台">30.5、使用 H2 的 Web 控制台</h3>
<p><a href="http://www.h2database.com/" target="_blank">H2 数据库</a>提供了一个<a href="http://www.h2database.com/html/quickstart.html#h2_console" target="_blank">基于浏览器的控制台</a>，Spring Boot 可以为您自动配置。当满足以下条件时，控制台将自动配置：</p>
<ul>
<li>您开发的是一个基于 servlet 的 web 应用程序</li>
<li><code>com.h2database:h2</code> 在 classpath 上</li>
<li>您使用了 <a href="#using-boot-devtools">Spring Boot 的开发者工具</a></li>
</ul>
<p><strong>提示</strong></p>
<blockquote>
<p>如果您不使用 Spring Boot 的开发者工具，但仍希望使用 H2 的控制台，则可以通过将 <code>spring.h2.console.enabled</code> 属性设置为 <code>true</code> 来实现。</p>
</blockquote>
<p><strong>注意</strong></p>
<blockquote>
<p>H2 控制台仅用于开发期间，因此应注意确保 <code>spring.h2.console.enabled</code> 在生产环境中<strong>没有</strong>设置为 <code>true</code>。</p>
</blockquote>
<p><a id="boot-features-sql-h2-console-custom-path"></a></p>
<h4 id="3051、更改-h2-控制台的路径">30.5.1、更改 H2 控制台的路径</h4>
<p>默认情况下，控制台的路径为 <code>/h2-console</code>。你可以使用 <code>spring.h2.console.path</code> 属性来自定义控制台的路径。</p>
<p><a id="boot-features-jooq"></a></p>
<h3 id="306、使用-jooq">30.6、使用 jOOQ</h3>
<p>Java 面向对象查询（<a href="http://www.jooq.org/" target="_blank">Java Object Oriented Querying，jOOQ</a>）是一款广受欢迎的产品，出自 <a href="http://www.datageekery.com/" target="_blank">Data Geekery</a>，它可以通过数据库生成 Java 代码，并允许您使用流式 API 来构建类型安全的 SQL 查询。商业版和开源版都可以与 Spring Boot 一起使用。</p>
<p><a id="_code_generation"></a></p>
<h4 id="3061、代码生成">30.6.1、代码生成</h4>
<p>要使用 jOOQ 的类型安全查询，您需要从数据库模式生成 Java 类。您可以按照 <a href="https://www.jooq.org/doc/3.11.7/manual-single-page/#jooq-in-7-steps-step3" target="_blank">jOOQ 用户手册</a>中的说明进行操作。如果您使用了 <code>jooq-codegen-maven</code> 插件，并且还使用了 <code>spring-boot-starter-parent</code> 父 POM，则可以安全地省略掉插件的 <code><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>version</span><span class="token punctuation">&gt;</span></span></code> 标签。您还可以使用 Spring Boot 定义的版本变量（例如 <code>h2.version</code>）来声明插件的数据库依赖。以下是一个示例：</p>
<pre class="language-"><code class="lang-xml"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>plugin</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>groupId</span><span class="token punctuation">&gt;</span></span>org.jooq<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>groupId</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>artifactId</span><span class="token punctuation">&gt;</span></span>jooq-codegen-maven<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>artifactId</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>executions</span><span class="token punctuation">&gt;</span></span>
        ...
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>executions</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependencies</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependency</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>groupId</span><span class="token punctuation">&gt;</span></span>com.h2database<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>groupId</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>artifactId</span><span class="token punctuation">&gt;</span></span>h2<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>artifactId</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>version</span><span class="token punctuation">&gt;</span></span>${h2.version}<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>version</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependency</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependencies</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>configuration</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>jdbc</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>driver</span><span class="token punctuation">&gt;</span></span>org.h2.Driver<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>driver</span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>url</span><span class="token punctuation">&gt;</span></span>jdbc:h2:~/yourdatabase<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>url</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>jdbc</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>generator</span><span class="token punctuation">&gt;</span></span>
            ...
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>generator</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>configuration</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>plugin</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<p><a id="_using_dslcontext"></a></p>
<h4 id="3062、使用-dslcontext">30.6.2、使用 DSLContext</h4>
<p>jOOQ 提供的流式 API 是通过 <code>org.jooq.DSLContext</code> 接口初始化的。Spring Boot 将自动配置一个 <code>DSLContext</code> 作为 Spring Bean，并且将其连接到应用程序的 <code>DataSource</code>。<code>要使用 DSLContext</code>，您只需要 <code>@Autowire</code> 它：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Component</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">JooqExample</span> <span class="token keyword">implements</span> <span class="token class-name">CommandLineRunner</span> <span class="token punctuation">{</span>

    <span class="token keyword">private</span> <span class="token keyword">final</span> <span class="token class-name">DSLContext</span> create<span class="token punctuation">;</span>

    <span class="token annotation punctuation">@Autowired</span>
    <span class="token keyword">public</span> <span class="token class-name">JooqExample</span><span class="token punctuation">(</span><span class="token class-name">DSLContext</span> dslContext<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>create <span class="token operator">=</span> dslContext<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p><strong>提示</strong></p>
<blockquote>
<p>jOOQ 手册建议使用名为 <code>create</code> 的变量来保存 <code>DSLContext</code>。</p>
</blockquote>
<p>您可以使用 <code>DSLContext</code> 构建查询：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">public</span> <span class="token class-name">List</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">GregorianCalendar</span><span class="token punctuation">&gt;</span></span> <span class="token function">authorsBornAfter1980</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">return</span> <span class="token keyword">this</span><span class="token punctuation">.</span>create<span class="token punctuation">.</span><span class="token function">selectFrom</span><span class="token punctuation">(</span>AUTHOR<span class="token punctuation">)</span>
        <span class="token punctuation">.</span><span class="token function">where</span><span class="token punctuation">(</span>AUTHOR<span class="token punctuation">.</span>DATE_OF_BIRTH<span class="token punctuation">.</span><span class="token function">greaterThan</span><span class="token punctuation">(</span><span class="token keyword">new</span> <span class="token class-name">GregorianCalendar</span><span class="token punctuation">(</span><span class="token number">1980</span><span class="token punctuation">,</span> <span class="token number">0</span><span class="token punctuation">,</span> <span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">)</span>
        <span class="token punctuation">.</span><span class="token function">fetch</span><span class="token punctuation">(</span>AUTHOR<span class="token punctuation">.</span>DATE_OF_BIRTH<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>
<p><a id="_jooq_sql_dialect"></a></p>
<h4 id="3063、jooq-sql-方言">30.6.3、jOOQ SQL 方言</h4>
<p>除非配置了 <code>spring.jooq.sql-dialect</code> 属性，否则 Spring Boot 会自动判定用于数据源的 SQL 方言。如果 Spring Boot 无法检测到方言，则使用 <code>DEFAULT</code>。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>Spring Boot 只能自动配置 jOOQ 开源版本支持的方言。</p>
</blockquote>
<p><a id="_customizing_jooq"></a></p>
<h4 id="3064、自定义-jooq">30.6.4、自定义 jOOQ</h4>
<p>可通过定义自己的 <code>@Bean</code> 来实现更高级的功能，这些自定义将在创建 jOOQ <code>Configuration</code> 时使用。您可以为以下 jOOQ 类型定义 bean：</p>
<ul>
<li><code>ConnectionProvider</code></li>
<li><code>ExecutorProvider</code></li>
<li><code>TransactionProvider</code></li>
<li><code>RecordMapperProvider</code></li>
<li><code>RecordUnmapperProvider</code></li>
<li><code>RecordListenerProvider</code></li>
<li><code>ExecuteListenerProvider</code></li>
<li><code>VisitListenerProvider</code></li>
<li><code>TransactionListenerProvider</code></li>
</ul>
<p>如果要完全控制 jOOQ 配置，您可以创建自己的 <code>org.jooq.Configuration</code> <code>@Bean</code>。</p>
<p><a id="boot-features-nosql"></a></p>
<h2 id="31、使用-nosql-技术">31、使用 NoSQL 技术</h2>
<p>Spring Data 提供了其他项目，可以帮助您访问各种 NoSQL 技术，包括 <a href="https://projects.spring.io/spring-data-mongodb/" target="_blank">MongoDB</a>、<a href="https://projects.spring.io/spring-data-neo4j/" target="_blank">Neo4J</a>、<a href="https://github.com/spring-projects/spring-data-elasticsearch/" target="_blank">Elasticsearch</a>、<a href="https://projects.spring.io/spring-data-solr/" target="_blank">Solr</a>、<a href="https://projects.spring.io/spring-data-redis/" target="_blank">Redis</a>、<a href="https://projects.spring.io/spring-data-gemfire/" target="_blank">Gemfire</a>、<a href="https://projects.spring.io/spring-data-cassandra/" target="_blank">Cassandra</a>、<a href="https://projects.spring.io/spring-data-couchbase/" target="_blank">Couchbase</a> 和 <a href="https://projects.spring.io/spring-data-ldap/" target="_blank">LDAP</a>。Spring Boot 为 Redis、MongoDB、Neo4j、Elasticsearch、Solr、Cassandra、Couchbase 和 LDAP 提供了自动配置。您也可以使用其他项目，但您需要自行配置他们。请参阅 <a href="https://projects.spring.io/spring-data" target="_blank">projects.spring.io/spring-data</a> 中相应的参考文档。</p>
<p><a id="boot-features-redis"></a></p>
<h3 id="311、redis">31.1、Redis</h3>
<p><a href="http://redis.io/" target="_blank">Redis</a> 是一个集缓存、消息代理和键值存储等丰富功能的数据库。Spring Boot 为 <a href="https://github.com/lettuce-io/lettuce-core/" target="_blank">Lettuce</a> 和 <a href="https://github.com/xetorthio/jedis/" target="_blank">Jedis 客户端类库</a>提供了基本自动配置，<a href="https://github.com/spring-projects/spring-data-redis" target="_blank">Spring Data Redis</a> 为他们提供了上层抽象。</p>
<p>使用 <code>spring-boot-starter-data-redis</code> starter 可方便地引入相关依赖。默认情况下，它使用 <a href="https://github.com/lettuce-io/lettuce-core/" target="_blank">Lettuce</a>。该 starter 可处理传统应用程序和响应式应用程序。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>我们还提供了一个 <code>spring-boot-starter-data-redis-reactive</code> starter，以便与其他带有响应式支持的存储保持一致。</p>
</blockquote>
<p><a id="boot-features-connecting-to-redis"></a></p>
<h4 id="3111、连接-redis">31.1.1、连接 Redis</h4>
<p>您可以像所有 Spring Bean 一样注入自动配置的 <code>RedisConnectionFactory</code>、<code>StringRedisTemplate</code> 或普通的 <code>RedisTemplate</code> 实例。默认情况下，实例将尝试在 <code>localhost:6379</code> 上连接 Redis 服务器，以下是 bean 示例：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Component</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyBean</span> <span class="token punctuation">{</span>

    <span class="token keyword">private</span> <span class="token class-name">StringRedisTemplate</span> template<span class="token punctuation">;</span>

    <span class="token annotation punctuation">@Autowired</span>
    <span class="token keyword">public</span> <span class="token class-name">MyBean</span><span class="token punctuation">(</span><span class="token class-name">StringRedisTemplate</span> template<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>template <span class="token operator">=</span> template<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token comment">// ...</span>

<span class="token punctuation">}</span>
</code></pre>
<p><strong>提示</strong></p>
<blockquote>
<p>您还可以注册任意数量个实现了 <code>LettuceClientConfigurationBuilderCustomizer</code> 的 bean，以进行更高级的自定义。如果你使用 Jedis，则可以使用 <code>JedisClientConfigurationBuilderCustomizer</code>。</p>
</blockquote>
<p>如果您添加了自己的任何一个自动配置类型的 <code>@Bean</code>，它将替换默认设置（除了 <code>RedisTemplate</code>，由于排除是基于 bean 名称，而 <code>redisTemplate</code> 不是它的类型）。默认情况下，如果 <code>commons-pool2</code> 在 classpath 上，您将获得一个连接池工厂。</p>
<p><a id="boot-features-mongodb"></a></p>
<h3 id="312、mongodb">31.2、MongoDB</h3>
<p><a href="https://www.mongodb.com/" target="_blank">MongoDB</a> 是一个开源的 NoSQL 文档数据库，其使用了类似 JSON 的模式（schema）来替代传统基于表的关系数据。Spring Boot 为 MongoDB 提供了几种便利的使用方式，包括 <code>spring-boot-starter-data-mongodb</code> 和 <code>spring-boot-starter-data-mongodb-reactive</code> starter。</p>
<p><a id="boot-features-connecting-to-mongodb"></a></p>
<h4 id="3121、连接-mongodb-数据库">31.2.1、连接 MongoDB 数据库</h4>
<p>您可以注入一个自动配置的 <code>org.springframework.data.mongodb.MongoDbFactory</code> 来访问 Mongo 数据库。默认情况下，该实例将尝试在 <code>mongodb://localhost/test</code> 上连接 MongoDB 服务器，以下示例展示了如何连接到 MongoDB 数据库：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>data<span class="token punctuation">.</span>mongodb</span><span class="token punctuation">.</span><span class="token class-name">MongoDbFactory</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">com<span class="token punctuation">.</span>mongodb</span><span class="token punctuation">.</span>DB<span class="token punctuation">;</span>

<span class="token annotation punctuation">@Component</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyBean</span> <span class="token punctuation">{</span>

    <span class="token keyword">private</span> <span class="token keyword">final</span> <span class="token class-name">MongoDbFactory</span> mongo<span class="token punctuation">;</span>

    <span class="token annotation punctuation">@Autowired</span>
    <span class="token keyword">public</span> <span class="token class-name">MyBean</span><span class="token punctuation">(</span><span class="token class-name">MongoDbFactory</span> mongo<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>mongo <span class="token operator">=</span> mongo<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token comment">// ...</span>

    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">example</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token class-name">DB</span> db <span class="token operator">=</span> mongo<span class="token punctuation">.</span><span class="token function">getDb</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token comment">// ...</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>您可以通过设置 <code>spring.data.mongodb.uri</code> 属性来更改 URL 和配置其他设置，如<strong>副本集</strong>（replica set）：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.data.mongodb.uri</span><span class="token attr-value"><span class="token punctuation">=</span>mongodb://user:secret@mongo1.example.com:12345,mongo2.example.com:23456/test</span>
</code></pre>
<p>另外，只要您使用了 Mongo 2.x，请指定 <code>host</code>/<code>port</code>。比如，您可能要在 <code>application.properties</code> 中声明以下内容：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.data.mongodb.host</span><span class="token attr-value"><span class="token punctuation">=</span>mongoserver</span>
<span class="token constant">spring.data.mongodb.port</span><span class="token attr-value"><span class="token punctuation">=</span>27017</span>
</code></pre>
<p>如果您已经定义了自己的 <code>MongoClient</code>，它将被用于自动配置合适的 <code>MongoDbFactory</code>。支持 <code>com.mongodb.MongoClient</code> 和 <code>com.mongodb.client.MongoClient</code>。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>如果您使用 Mongo 3.0 Java 驱动，则不支持 <code>spring.data.mongodb.host</code> 和 <code>spring.data.mongodb.port</code>。这种情况下，应该使用 <code>spring.data.mongodb.uri</code> 来提供所有配置。</p>
</blockquote>
<p><strong>提示</strong></p>
<blockquote>
<p>如果未指定 <code>spring.data.mongodb.port</code>，则使用默认值 <code>27017</code>。您可以将上述示例中的改行配置删除掉。</p>
</blockquote>
<p><strong>提示</strong></p>
<blockquote>
<p>如果您不使用 Spring Data Mongo，则可以注入 <code>com.mongodb.MongoClient</code> bean 来代替 <code>MongoDbFactory</code>。如果要完全控制建立 MongoDB 连接，您还可以声明自己的 <code>MongoDbFactory</code> 或者 <code>MongoClient</code> bean。</p>
</blockquote>
<p><strong>注意</strong></p>
<blockquote>
<p>如果您使用的是响应式驱动，则 SSL 需要 Netty。 如果 Netty 可用且 factory 尚未自定义，则自动配置会自动配置此 factory。</p>
</blockquote>
<p><a id="boot-features-mongo-template"></a></p>
<h4 id="3122、mongotemplate">31.2.2、MongoTemplate</h4>
<p><a href="https://projects.spring.io/spring-data-mongodb/" target="_blank">Spring Data Mongo</a> 提供了一个 <a href="https://docs.spring.io/spring-data/mongodb/docs/current/api/org/springframework/data/mongodb/core/MongoTemplate.html" target="_blank"><code>MongoTemplate</code></a> 类，它的设计与 Spring 的 <code>JdbcTemplate</code> 非常相似。与 <code>JdbcTemplate</code> 一样，Spring Boot 会自动配置一个 bean，以便您能注入模板：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>beans<span class="token punctuation">.</span>factory<span class="token punctuation">.</span>annotation</span><span class="token punctuation">.</span><span class="token class-name">Autowired</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>data<span class="token punctuation">.</span>mongodb<span class="token punctuation">.</span>core</span><span class="token punctuation">.</span><span class="token class-name">MongoTemplate</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>stereotype</span><span class="token punctuation">.</span><span class="token class-name">Component</span><span class="token punctuation">;</span>

<span class="token annotation punctuation">@Component</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyBean</span> <span class="token punctuation">{</span>

    <span class="token keyword">private</span> <span class="token keyword">final</span> <span class="token class-name">MongoTemplate</span> mongoTemplate<span class="token punctuation">;</span>

    <span class="token annotation punctuation">@Autowired</span>
    <span class="token keyword">public</span> <span class="token class-name">MyBean</span><span class="token punctuation">(</span><span class="token class-name">MongoTemplate</span> mongoTemplate<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>mongoTemplate <span class="token operator">=</span> mongoTemplate<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token comment">// ...</span>

<span class="token punctuation">}</span>
</code></pre>
<p>更多详细信息，参照 <a href="https://docs.spring.io/spring-data/mongodb/docs/current/api/org/springframework/data/mongodb/core/MongoOperations.html" target="_blank"><code>MongoOperations</code></a> Javadoc。</p>
<p><a id="boot-features-spring-data-mongo-repositories"></a></p>
<h4 id="3123、spring-data-mongodb-资源库">31.2.3、Spring Data MongoDB 资源库</h4>
<p>Spring Data 包含了对 MongoDB 资源库（repository）的支持。与之前讨论的 JPA 资源库一样，基本原理是根据方法名称自动构建查询。</p>
<p>事实上，Spring Data JPA 和 Spring Data MongoDB 共享通用的底层代码，因此你可以拿之前提到的 JPA 示例作为基础，假设 <code>City</code> 现在是一个 Mongo 数据类，而不是一个 JPA <code>@Entity</code>，他们方式工作相同：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">package</span> <span class="token namespace">com<span class="token punctuation">.</span>example<span class="token punctuation">.</span>myapp<span class="token punctuation">.</span>domain</span><span class="token punctuation">;</span>

<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>data<span class="token punctuation">.</span>domain</span><span class="token punctuation">.</span>*<span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>data<span class="token punctuation">.</span>repository</span><span class="token punctuation">.</span>*<span class="token punctuation">;</span>

<span class="token keyword">public</span> <span class="token keyword">interface</span> <span class="token class-name">CityRepository</span> <span class="token keyword">extends</span> <span class="token class-name">Repository</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">City</span><span class="token punctuation">,</span> <span class="token class-name">Long</span><span class="token punctuation">&gt;</span></span> <span class="token punctuation">{</span>

    <span class="token class-name">Page</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">City</span><span class="token punctuation">&gt;</span></span> <span class="token function">findAll</span><span class="token punctuation">(</span><span class="token class-name">Pageable</span> pageable<span class="token punctuation">)</span><span class="token punctuation">;</span>

    <span class="token class-name">City</span> <span class="token function">findByNameAndStateAllIgnoringCase</span><span class="token punctuation">(</span><span class="token class-name">String</span> name<span class="token punctuation">,</span> <span class="token class-name">String</span> state<span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token punctuation">}</span>
</code></pre>
<p><strong>提示</strong></p>
<blockquote>
<p>您可以使用 <code>@EntityScan</code> 注解来自定义文档扫描位置。</p>
</blockquote>
<p><strong>提示</strong></p>
<blockquote>
<p>有关 Spring Data MongoDB 的完整详细内容，包括其丰富的对象关系映射技术，请参考其<a href="https://projects.spring.io/spring-data-mongodb/" target="_blank">参考文档</a>。</p>
</blockquote>
<p><a id="boot-features-mongo-embedded"></a></p>
<h4 id="3124、内嵌-mongo">31.2.4、内嵌 Mongo</h4>
<p>Spring Boot 提供了<a href="https://github.com/flapdoodle-oss/de.flapdoodle.embed.mongo" target="_blank">内嵌 Mongo</a> 的自动配置。要在 Spring Boot 应用程序中使用它，请添加依赖 <code>de.flapdoodle.embed:de.flapdoodle.embed.mongo</code>。</p>
<p>可以使用 <code>spring.data.mongodb.port</code> 属性来配置 Mongo 的监听端口。如果想随机分配空闲端口，请把值设置为 0。<code>MongoAutoConfiguration</code> 创建的 <code>MongoClient</code> 将自动配置随机分配的端口。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>如果您不配置一个自定义端口，内嵌支持将默认使用一个随机端口（而不是 27017）。</p>
</blockquote>
<p>如果您的 classpath 上有 SLF4J，Mongo 产生的输出将自动路由到名为 <code>org.springframework.boot.autoconfigure.mongo.embedded.EmbeddedMongo</code> 的 logger。</p>
<p>您可以声明自己的 <code>IMongodConfig</code> 和 <code>IRuntimeConfig</code> bean 来控制 Mongo 实例的配置和日志路由。</p>
<p><a id="boot-features-neo4j"></a></p>
<h3 id="313、neo4j">31.3、Neo4j</h3>
<p><a href="http://neo4j.com/" target="_blank">Neo4j</a> 是一个开源的 NoSQL 图形数据库，它使用了一个节点由关系连接的富数据模型，比传统 RDBMS 的方式更适合连接大数据。Spring Boot 为 Neo4j 提供了便捷引入方式，包括 <code>spring-boot-starter-data-neo4j</code> starter。</p>
<p><a id="boot-features-connecting-to-neo4j"></a></p>
<h4 id="3131、连接-neo4j-数据库">31.3.1、连接 Neo4j 数据库</h4>
<p>您可以像任何 Spring Bean 一样注入一个自动配置的 <code>org.neo4j.ogm.session.Session</code>。默认情况下， 该实例将尝试使用在 <code>localhost:7687</code> 上使用 Bolt 协议连接到 Neo4j 服务器，以下示例展示了如何注入 一个 Neo4j <code>Session</code>：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Component</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyBean</span> <span class="token punctuation">{</span>

    <span class="token keyword">private</span> <span class="token keyword">final</span> <span class="token class-name">Session</span> session<span class="token punctuation">;</span>

    <span class="token annotation punctuation">@Autowired</span>
    <span class="token keyword">public</span> <span class="token class-name">MyBean</span><span class="token punctuation">(</span><span class="token class-name">Session</span> session<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>session <span class="token operator">=</span> session<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token comment">// ...</span>

<span class="token punctuation">}</span>
</code></pre>
<p>您可以通过配置 <code>spring.data.neo4j.*</code> 属性来设置 uri 和凭据：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.data.neo4j.uri</span><span class="token attr-value"><span class="token punctuation">=</span>bolt://my-server:7687</span>
<span class="token constant">spring.data.neo4j.username</span><span class="token attr-value"><span class="token punctuation">=</span>neo4j</span>
<span class="token constant">spring.data.neo4j.password</span><span class="token attr-value"><span class="token punctuation">=</span>secret</span>
</code></pre>
<p>您可以通过添加自己的 <code>org.neo4j.ogm.config.Configuration</code> @Bean 来完全控制 session 创建。此外，添加 <code>SessionFactory</code> 类型的 @Bean 会禁用自动配置，因此您可以掌控所有。</p>
<p><a id="boot-features-connecting-to-neo4j-embedded"></a></p>
<h4 id="3132、使用内嵌模式">31.3.2、使用内嵌模式</h4>
<p>如果您将 <code>org.neo4j:neo4j-ogm-embedded-driver</code> 添加到应用程序的依赖中，Spring Boot 将自动配置一个进程内内嵌的 Neo4j 实例，当您的应用程序关闭时，该实例将不会保留任何数据。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>内嵌 Neo4j OGM 驱动本身不提供 Neo4j 您必须自己声明 <code>org.neo4j:neo4j</code> 依赖，请参考 <a href="https://neo4j.com/docs/ogm-manual/current/reference/#reference:getting-started" target="_blank">Neo4j OGM 文档</a> 获取兼容版本列表。</p>
</blockquote>
<p>当 classpath 上有多个驱动时，内嵌驱动优先于其他驱动。您可以通过设置 <code>spring.data.neo4j.embedded.enabled=false</code> 来显式禁用内嵌模式。</p>
<p>如果内嵌驱动和 Neo4j 内核如上所述位于 classpath 上，则 <a href="#boot-features-testing-spring-boot-applications-testing-autoconfigured-neo4j-test">Data Neo4j 测试</a> 会自动使用内嵌 Neo4j 实例。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>您可以通过在配置中提供数据库文件路径来为内嵌模式启用持久化，例如：<code>spring.data.neo4j.uri=file://var/tmp/graph.db</code>。</p>
</blockquote>
<p><a id="boot-features-neo4j-ogm-session"></a></p>
<h4 id="3133、neo4jsession">31.3.3、Neo4jSession</h4>
<p>默认情况下，如果您正在运行 Web 应用程序，会话（session）将被绑定到当前请求的整个处理线程（即 <strong>Open Session in View</strong> 模式）。如果不希望此行为，您可以在 <code>application.properties</code> 中添加以下内容：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.data.neo4j.open-in-view</span><span class="token attr-value"><span class="token punctuation">=</span>false</span>
</code></pre>
<p><a id="boot-features-spring-data-neo4j-repositories"></a></p>
<h4 id="3134、spring-data-neo4j-资源库">31.3.4、Spring Data Neo4j 资源库</h4>
<p>Spring Data 包括了对 Neo4j 资源库的支持。</p>
<p>Spring Data Neo4j 与 Spring Data JPA 共享相同的通用底层代码，因此您可以直接把之前的 JPA 示例作为基础，假设 <code>City</code> 现在是一个 Neo4j OGM <code>@NodeEntity</code>，而不是一个 JPA <code>@Entity</code>，并且资源库抽象以相同的方式工作：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">package</span> <span class="token namespace">com<span class="token punctuation">.</span>example<span class="token punctuation">.</span>myapp<span class="token punctuation">.</span>domain</span><span class="token punctuation">;</span>

<span class="token keyword">import</span> <span class="token namespace">java<span class="token punctuation">.</span>util</span><span class="token punctuation">.</span><span class="token class-name">Optional</span><span class="token punctuation">;</span>

<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>data<span class="token punctuation">.</span>neo4j<span class="token punctuation">.</span>repository</span><span class="token punctuation">.</span>*<span class="token punctuation">;</span>

<span class="token keyword">public</span> <span class="token keyword">interface</span> <span class="token class-name">CityRepository</span> <span class="token keyword">extends</span> <span class="token class-name">Neo4jRepository</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">City</span><span class="token punctuation">,</span> <span class="token class-name">Long</span><span class="token punctuation">&gt;</span></span> <span class="token punctuation">{</span>

    <span class="token class-name">Optional</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">City</span><span class="token punctuation">&gt;</span></span> <span class="token function">findOneByNameAndState</span><span class="token punctuation">(</span><span class="token class-name">String</span> name<span class="token punctuation">,</span> <span class="token class-name">String</span> state<span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token punctuation">}</span>
</code></pre>
<p><code>spring-boot-starter-data-neo4j</code> starter 支持资源库和事务管理。您可以在 <code>@Configuration</code> bean 上分别使用 <code>@EnableNeo4jRepositories</code> 和 <code>@EntityScan</code> 来自定义位置以查找资源库和实体。</p>
<p><strong>提示</strong></p>
<p>有关 Spring Data Neo4j 的完整详细信息，包括其对象映射技术，请参阅<a href="https://projects.spring.io/spring-data-neo4j/" target="_blank">参考文档</a>。</p>
<p><a id="boot-features-gemfire"></a></p>
<h3 id="314、gemfire">31.4、Gemfire</h3>
<p><a href="https://github.com/spring-projects/spring-data-gemfire" target="_blank">Spring Data Gemfire</a> 提供了便捷的 Spring 整合工具，用于访问 <a href="https://pivotal.io/big-data/pivotal-gemfire#details" target="_blank">Pivotal Gemfire</a> 数据管理平台。        <code>spring-boot-starter-data-gemfire</code> starter 包含了相关依赖。目前没有针对 Gemfire 的自动配置支持，但您可以使用一个<a href="https://github.com/spring-projects/spring-data-gemfire/blob/master/src/main/java/org/springframework/data/gemfire/repository/config/EnableGemfireRepositories.java" target="_blank">单独的注解（@EnableGemfireRepositories）</a>来启用 Spring Data 资源库。</p>
<p><a id="boot-features-solr"></a></p>
<h3 id="315、solr">31.5、Solr</h3>
<p><a href="https://lucene.apache.org/solr/" target="_blank">Apache Solr</a> 是一个搜素引擎。Spring Boot 为 Solr 5 客户端类库提供了基本的自动配置，并且 <a href="https://github.com/spring-projects/spring-data-solr" target="_blank">Spring Data Solr</a> 为其提供给了顶层抽象。相关的依赖包含在了 <code>spring-boot-starter-data-solr</code> starter 中。</p>
<p><a id="boot-features-solr"></a></p>
<h4 id="3151、连接-solr">31.5.1、连接 Solr</h4>
<p>您可以像其他 Spring Bean 一样注入一个自动配置的 <code>SolrClient</code> 实例。默认情况下，该实例将尝试通过 <a href="http://localhost:8983/solr" target="_blank"><code>localhost:8983/solr</code></a> 连接到服务器，以下示例展示了如何注入一个 Solr bean：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Component</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyBean</span> <span class="token punctuation">{</span>

    <span class="token keyword">private</span> <span class="token class-name">SolrClient</span> solr<span class="token punctuation">;</span>

    <span class="token annotation punctuation">@Autowired</span>
    <span class="token keyword">public</span> <span class="token class-name">MyBean</span><span class="token punctuation">(</span><span class="token class-name">SolrClient</span> solr<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>solr <span class="token operator">=</span> solr<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token comment">// ...</span>

<span class="token punctuation">}</span>
</code></pre>
<p>如果您添加了自己的 <code>SolrClient</code> 类型的 <code>@Bean</code>，它将替换掉默认配置。</p>
<p><a id="boot-features-spring-data-solr-repositories"></a></p>
<h4 id="3152、spring-data-solr-资源库">31.5.2、Spring Data Solr 资源库</h4>
<p>Spring Data 包含了对 Apache Solr 资源库的支持。与之前讨论的 JPA 资源库一样，基本原理是根据方法名称自动构造查询。</p>
<p>事实上，Spring Data JPA 和 Spring Data Solr 共享了相同的通用底层代码，因此您可以使用之前的 JPA 示例作为基础，假设 <code>City</code> 现在是一个 <code>@SolrDocument</code> 类，而不是一个 JPA <code>@Entity</code>，它的工作方式相同。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>有关 Spring Data Solr 的完整详细内容，请参考其<a href="https://projects.spring.io/spring-data-solr/" target="_blank">参考文档</a>。</p>
</blockquote>
<p><a id="boot-features-elasticsearch"></a></p>
<h3 id="316、elasticsearch">31.6、Elasticsearch</h3>
<p><a href="https://www.elastic.co/products/elasticsearch" target="_blank">Elasticsearch</a> 是一个开源、分布式、RESTful 的实时搜索分析引擎。Spring Boot 为 Elasticsearch 提供了基本的自动配置。</p>
<p>Spring Boot 支持以下 HTTP 客户端：</p>
<ul>
<li>官方 Java <strong>Low Level（低级）</strong> 和 <strong>High Level（高级）</strong> REST 客户端</li>
<li><a href="https://github.com/searchbox-io/Jest" target="_blank">Jest</a></li>
</ul>
<p><a href="https://github.com/spring-projects/spring-data-elasticsearch" target="_blank">Spring Data Elasticsearch</a> 依旧使用传输客户端，您可以使用 <code>spring-boot-starter-data-elasticsearch</code> starter 引入使用它。</p>
<p><a id="boot-features-connecting-to-elasticsearch-rest"></a></p>
<h4 id="3161、使用-rest-客户端连接-elasticsearch">31.6.1、使用 REST 客户端连接 Elasticsearch</h4>
<p>Elasticsearch 提供了两个可用于查询集群的 <a href="https://www.elastic.co/guide/en/elasticsearch/client/java-rest/current/index.html" target="_blank">REST 客户端</a>：<strong>Low Level（低级）</strong> 和 <strong>High Level（高级）</strong>。</p>
<p>如果您的 classpath 上存在 <code>org.elasticsearch.client:elasticsearch-rest-client</code> 依赖，则 Spring Boot 将自动配置并注册默认目标为 <a href="http://localhost:9200/" target="_blank"><code>localhost:9200</code></a> 的 <code>RestClient</code> bean。您可以进一步调整 <code>RestClient</code> 的配置，如下所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.elasticsearch.rest.uris</span><span class="token attr-value"><span class="token punctuation">=</span>http://search.example.com:9200</span>
<span class="token constant">spring.elasticsearch.rest.username</span><span class="token attr-value"><span class="token punctuation">=</span>user</span>
<span class="token constant">spring.elasticsearch.rest.password</span><span class="token attr-value"><span class="token punctuation">=</span>secret</span>
</code></pre>
<p>您还可以注册实现任意数量的 <code>RestClientBuilderCustomizer</code> bean，以进行更高级的自定义。要完全控制注册流程，请定义 <code>RestClient</code> bean。</p>
<p>如果你 classpath 上有 <code>org.elasticsearch.client:elasticsearch-rest-high-level-client</code> 依赖，Spring Boot 将自动配置一个 <code>RestHighLevelClient</code>，它包装了所有现有的 <code>RestClient</code> bean，重用其 HTTP 配置。</p>
<p><a id="boot-features-connecting-to-elasticsearch-jest"></a></p>
<h4 id="3162、使用-jest-连接-elasticsearch">31.6.2、使用 Jest 连接 Elasticsearch</h4>
<p>如果您的 classpath 上存在 <code>Jest</code>，则可以注入一个默认目标为 <a href="http://localhost:9200/" target="_blank"><code>localhost:9200</code></a> 的自动配置 <code>JestClient</code>。您还可以进一步调整客户端配置：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.elasticsearch.jest.uris</span><span class="token attr-value"><span class="token punctuation">=</span>http://search.example.com:9200</span>
<span class="token constant">spring.elasticsearch.jest.read-timeout</span><span class="token attr-value"><span class="token punctuation">=</span>10000</span>
<span class="token constant">spring.elasticsearch.jest.username</span><span class="token attr-value"><span class="token punctuation">=</span>user</span>
<span class="token constant">spring.elasticsearch.jest.password</span><span class="token attr-value"><span class="token punctuation">=</span>secret</span>
</code></pre>
<p>您还可以注册任何数量实现了 <code>HttpClientConfigBuilderCustomizer</code> 的 bean，以进行更加高级的自定义。以下示例调整了其他 HTTP 设置：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">static</span> <span class="token keyword">class</span> <span class="token class-name">HttpSettingsCustomizer</span> <span class="token keyword">implements</span> <span class="token class-name">HttpClientConfigBuilderCustomizer</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@Override</span>
    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">customize</span><span class="token punctuation">(</span><span class="token class-name">HttpClientConfig</span><span class="token punctuation">.</span><span class="token class-name">Builder</span> builder<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        builder<span class="token punctuation">.</span><span class="token function">maxTotalConnection</span><span class="token punctuation">(</span><span class="token number">100</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">defaultMaxTotalConnectionPerRoute</span><span class="token punctuation">(</span><span class="token number">5</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>要完全控制注册流程，请定义一个 <code>JestClient</code> bean。</p>
<p><a id="boot-features-connecting-to-elasticsearch-spring-data"></a></p>
<h4 id="3163、使用-spring-data-连接-elasticsearch">31.6.3、使用 Spring Data 连接 Elasticsearch</h4>
<p>要连接 Elasticsearch，您必须提供一个或多个群集节点的地址。可以通过将 <code>spring.data.elasticsearch.cluster-nodes</code> 属性设置为以逗号分隔的 <code>host:port</code> 列表来指定地址。使用此配置，可以像其他 Spring bean 一样注入 <code>ElasticsearchTemplate</code> 或 <code>TransportClient</code>，如下所示：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Component</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyBean</span> <span class="token punctuation">{</span>

    <span class="token keyword">private</span> <span class="token keyword">final</span> <span class="token class-name">ElasticsearchTemplate</span> template<span class="token punctuation">;</span>

    <span class="token keyword">public</span> <span class="token class-name">MyBean</span><span class="token punctuation">(</span><span class="token class-name">ElasticsearchTemplate</span> template<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>template <span class="token operator">=</span> template<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token comment">// ...</span>

<span class="token punctuation">}</span>
</code></pre>
<p>如果您添加了自己的 <code>ElasticsearchTemplate</code> 或者 <code>TransportClient</code> <code>@Bean</code>，则其将替代默认配置。</p>
<p><a id="boot-features-spring-data-elasticsearch-repositories"></a></p>
<h4 id="3164、spring-data-elasticsearch-资源库">31.6.4、Spring Data Elasticsearch 资源库</h4>
<p>Spring Data 包含了对 Elasticsearch 资源库的支持，与之前讨论的 JPA 资源库一样，其原理是根据方法名称自动构造查询。</p>
<p>事实上，Spring Data JPA 与 Spring Data Elasticsearch 共享了相同的通用底层代码，因此您可以使用之前的 JPA 示例作为基础，假设 <code>City</code> 此时是一个 Elasticsearch <code>@Document</code> 类，而不是一个 JPA <code>@Entity</code>，它以相同的方式工作。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>有关 Spring Data Elasticsearch 的完整详细内容，请参阅其<a href="https://docs.spring.io/spring-data/elasticsearch/docs/" target="_blank">参考文档</a>。</p>
</blockquote>
<p><a id="boot-features-cassandra"></a></p>
<h3 id="317、cassandra">31.7、Cassandra</h3>
<p><a href="https://cassandra.apache.org/" target="_blank">Cassandra</a> 是一个开源的分布式数据库管理系统，旨在处理商用服务器上的大量数据。Spring Boot 为 Cassandra 提供了自动配置，且 <a href="https://github.com/spring-projects/spring-data-cassandra" target="_blank">Spring Data Cassandra</a> 为其提供了顶层抽象。相关依赖包含在 <code>spring-boot-starter-data-cassandra</code> starter 中。</p>
<p><a id="boot-features-connecting-to-cassandra"></a></p>
<h4 id="3171、连接-cassandra">31.7.1、连接 Cassandra</h4>
<p>您可以像其他 Spring Bean 一样注入一个自动配置的 <code>CassandraTemplate</code> 或 Cassandra <code>Session</code> 实例。<code>spring.data.cassandra.*</code> 属性可用于自定义连接。通常，您会提供 <code>keyspace-name</code> 和 <code>contact-points</code>属性：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.data.cassandra.keyspace-name</span><span class="token attr-value"><span class="token punctuation">=</span>mykeyspace</span>
<span class="token constant">spring.data.cassandra.contact-points</span><span class="token attr-value"><span class="token punctuation">=</span>cassandrahost1,cassandrahost2</span>
</code></pre>
<p>您还可以注册任意数量实现了 ClusterBuilderCustomizer 的 bean，以进行更高级的自定义。</p>
<p>以下代码展示了如何注入一个 Cassandra bean：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Component</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyBean</span> <span class="token punctuation">{</span>

    <span class="token keyword">private</span> <span class="token class-name">CassandraTemplate</span> template<span class="token punctuation">;</span>

    <span class="token annotation punctuation">@Autowired</span>
    <span class="token keyword">public</span> <span class="token class-name">MyBean</span><span class="token punctuation">(</span><span class="token class-name">CassandraTemplate</span> template<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>template <span class="token operator">=</span> template<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token comment">// ...</span>

<span class="token punctuation">}</span>
</code></pre>
<p>如果您添加了自己的类的为 <code>@CassandraTemplate</code> 的 <code>@Bean</code>，则其将替代默认值。</p>
<p><a id="boot-features-spring-data-cassandra-repositories"></a></p>
<h4 id="3172、spring-data-cassandra-资源库">31.7.2、Spring Data Cassandra 资源库</h4>
<p>Spring Data 包含了基本的 Cassandra 资源库支持。目前，其限制要比之前讨论的 JPA 资源库要多，并且需要在 finder 方法上使用 <code>@Query</code> 注解。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>有关 Spring Data Cassandra 的完整详细内容，请参阅其<a href="https://docs.spring.io/spring-data/cassandra/docs/" target="_blank">参考文档</a>。</p>
</blockquote>
<p><a id="boot-features-couchbase"></a></p>
<h3 id="318、couchbase">31.8、Couchbase</h3>
<p><a href="https://www.couchbase.com/" target="_blank">Couchbase</a> 是一个开源、分布式多模型的 NoSQL 面向文档数据库，其针对交互式应用程序做了优化。Spring Boot 为 Couchbase 提供了自动配置，且 <a href="https://github.com/spring-projects/spring-data-couchbase" target="_blank">Spring Data Couchbase</a> 为其提供了顶层抽象。相关的依赖包含在了 <code>spring-boot-starter-data-couchbase</code> starter 中。</p>
<p><a id="boot-features-connecting-to-couchbase"></a></p>
<h4 id="3181、连接-couchbase">31.8.1、连接 Couchbase</h4>
<p>您可以通过添加 Couchbase SDK 和一些配置来轻松获取 <code>Bucket</code> 和 <code>Cluster</code>。<code>spring.couchbase.*</code> 属性可用于自定义连接。通常您会配置 bootstrap host、bucket name 和 password：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.couchbase.bootstrap-hosts</span><span class="token attr-value"><span class="token punctuation">=</span>my-host-1,192.168.1.123</span>
<span class="token constant">spring.couchbase.bucket.name</span><span class="token attr-value"><span class="token punctuation">=</span>my-bucket</span>
<span class="token constant">spring.couchbase.bucket.password</span><span class="token attr-value"><span class="token punctuation">=</span>secret</span>
</code></pre>
<blockquote>
<p>您<strong>至少</strong>需要提供 bootstrap host，这种情况下，bucket name 为 <code>default</code> 且 password 为空字符串。或者，您可以定义自己的 <code>org.springframework.data.couchbase.config.CouchbaseConfigurer</code> @Bean 来控制整个配置。</p>
</blockquote>
<p>也可以自定义一些 <code>CouchbaseEnvironment</code> 设置。例如，以下配置修改了打开一个新 <code>Bucket</code> 的超时时间和开启了 SSL 支持：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.couchbase.env.timeouts.connect</span><span class="token attr-value"><span class="token punctuation">=</span>3000</span>
<span class="token constant">spring.couchbase.env.ssl.key-store</span><span class="token attr-value"><span class="token punctuation">=</span>/location/of/keystore.jks</span>
<span class="token constant">spring.couchbase.env.ssl.key-store-password</span><span class="token attr-value"><span class="token punctuation">=</span>secret</span>
</code></pre>
<p>查看 <code>spring.couchbase.env.*</code> 获取更多详细内容。</p>
<p><a id="boot-features-spring-data-couchbase-repositories"></a></p>
<h4 id="3182、spring-data-couchbase-资源库">31.8.2、Spring Data Couchbase 资源库</h4>
<p>Spring Data 包含了 Couchbase 资源库支持。有关 Spring Data Couchbase 的完整详细信息，请参阅其<a href="https://docs.spring.io/spring-data/couchbase/docs/current/reference/html/" target="_blank">参考文档</a>。</p>
<p>您可以像使用其他 Spring Bean 一样注入自动配置的 <code>CouchbaseTemplate</code> 实例，前提是有一个默认的<code>CouchbaseConfigurer</code>（当您启用 Couchbase 支持时会发生这种情况，如之前所述）。</p>
<p>以下示例展示了如何注入一个 Couchbase bean：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Component</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyBean</span> <span class="token punctuation">{</span>

    <span class="token keyword">private</span> <span class="token keyword">final</span> <span class="token class-name">CouchbaseTemplate</span> template<span class="token punctuation">;</span>

    <span class="token annotation punctuation">@Autowired</span>
    <span class="token keyword">public</span> <span class="token class-name">MyBean</span><span class="token punctuation">(</span><span class="token class-name">CouchbaseTemplate</span> template<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>template <span class="token operator">=</span> template<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token comment">// ...</span>

<span class="token punctuation">}</span>
</code></pre>
<p>您可以在自己的配置中定义以下几个 bean，以覆盖自动配置提供的配置：</p>
<ul>
<li>一个名为 <code>couchbaseTemplate</code> 的 <code>CouchbaseTemplate</code> @Bean</li>
<li>一个名为 <code>couchbaseIndexManager</code> 的 <code>IndexManager</code> @Bean</li>
<li>一个名为 <code>couchbaseCustomConversions</code> 的 <code>CustomConversions</code> @Bean</li>
</ul>
<p>为了避免在自己的配置中硬编码这些名称，您可以重用 Spring Data Couchbase 提供的 <code>BeanNames</code>，例如，您可以自定义转换器，如下：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Configuration</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">SomeConfiguration</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@Bean</span><span class="token punctuation">(</span><span class="token class-name">BeanNames</span><span class="token punctuation">.</span>COUCHBASE_CUSTOM_CONVERSIONS<span class="token punctuation">)</span>
    <span class="token keyword">public</span> <span class="token class-name">CustomConversions</span> <span class="token function">myCustomConversions</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> <span class="token keyword">new</span> <span class="token class-name">CustomConversions</span><span class="token punctuation">(</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token comment">// ...</span>

<span class="token punctuation">}</span>
</code></pre>
<p><strong>提示</strong></p>
<p>如果您想要安全绕开 Spring Data Couchbase 的自动配置，请提供自己的 <code>org.springframework.data.couchbase.config.AbstractCouchbaseDataConfiguration</code> 实现。</p>
<p><a id="boot-features-ldap"></a></p>
<h3 id="319、ldap">31.9、LDAP</h3>
<p><a href="https://en.wikipedia.org/wiki/Lightweight_Directory_Access_Protocol" target="_blank">LDAP</a>（Lightweight Directory Access Protocol，轻量级目录访问协议）是一个开放、厂商中立的行业标准应用协议，其通过 IP 网络访问和维护分布式目录信息服务。Spring Boot 为兼容 LDAP 服务器提供了自动配置，以及支持从 <a href="https://www.ldap.com/unboundid-ldap-sdk-for-java" target="_blank">UnboundID</a> 内嵌内存式 LDAP 服务器。</p>
<p><a href="https://github.com/spring-projects/spring-data-ldap" target="_blank">Spring Data LDAP</a> 提供了 LDAP 抽象。相关依赖包含在了 <code>spring-boot-starter-data-ldap</code> starter 中。</p>
<p><a id="boot-features-ldap-connecting"></a></p>
<h4 id="3191、连接-ldap-服务器">31.9.1、连接 LDAP 服务器</h4>
<p>要连接 LDAP 服务器，请确保您已经声明了 <code>spring-boot-starter-data-ldap</code> starter 或者 <code>spring-ldap-core</code> 依赖，然后在 <code>application.properties</code> 声明服务器的 URL：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.ldap.urls</span><span class="token attr-value"><span class="token punctuation">=</span>ldap://myserver:1235</span>
<span class="token constant">spring.ldap.username</span><span class="token attr-value"><span class="token punctuation">=</span>admin</span>
<span class="token constant">spring.ldap.password</span><span class="token attr-value"><span class="token punctuation">=</span>secret</span>
</code></pre>
<p>如果需要自定义连接设置，您可以使用 <code>spring.ldap.base</code> 和 <code>spring.ldap.base-environment</code> 属性。</p>
<p><code>LdapContextSource</code> 将根据这些设置自动配置。如果您需要自定义它，例如使用一个 <code>PooledContextSource</code>，则仍然可以注入自动配置的 <code>LdapContextSource</code>。确保将自定义的 <code>ContextSource</code> 标记为 <code>@Primary</code>，以便自动配置的 <code>LdapTemplate</code> 能使用它。</p>
<p><a id="boot-features-ldap-spring-data-repositories"></a></p>
<h4 id="3192、spring-data-ldap-资源库">31.9.2、Spring Data LDAP 资源库</h4>
<p>Spring Data 包含了 LDAP 资源库支持。有关 Spring Data LDAP 的完整详细信息，请参阅其<a href="https://docs.spring.io/spring-data/ldap/docs/1.0.x/reference/html/" target="_blank">参考文档</a>。</p>
<p>您还可以像其他 Spring Bean 一样注入一个自动配置的 <code>LdapTemplate</code> 实例：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Component</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyBean</span> <span class="token punctuation">{</span>

    <span class="token keyword">private</span> <span class="token keyword">final</span> <span class="token class-name">LdapTemplate</span> template<span class="token punctuation">;</span>

    <span class="token annotation punctuation">@Autowired</span>
    <span class="token keyword">public</span> <span class="token class-name">MyBean</span><span class="token punctuation">(</span><span class="token class-name">LdapTemplate</span> template<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>template <span class="token operator">=</span> template<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token comment">// ...</span>

<span class="token punctuation">}</span>
</code></pre>
<p><a id="boot-features-ldap-embedded"></a></p>
<h4 id="3193、内嵌内存式-ldap-服务器">31.9.3、内嵌内存式 LDAP 服务器</h4>
<p>为了测试目的，Spring Boot 支持从 <a href="https://www.ldap.com/unboundid-ldap-sdk-for-java" target="_blank">UnboundID</a> 自动配置一个内存式 LDAP 服务器。要配置服务器，请添加 <code>com.unboundid:unboundid-ldapsdk</code> 依赖并声明一个 <code>base-dn</code> 属性：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.ldap.embedded.base-dn</span><span class="token attr-value"><span class="token punctuation">=</span>dc=spring,dc=io</span>
</code></pre>
<p><strong>注意</strong></p>
<blockquote>

可以定义多个 `base-dn` 值，但是，由于名称包含逗号，存在歧义，因此必须使用正确的符号来定义它们。

在 yaml 文件中，您可以使用 yaml 列表表示法：

```yaml
spring.ldap.embedded.base-dn:
  - dc=spring,dc=io
  - dc=pivotal,dc=io
```

在属性文件中，必须使用索引方式：

```ini
spring.ldap.embedded.base-dn[0]=dc=spring,dc=io
spring.ldap.embedded.base-dn[1]=dc=pivotal,dc=io
```

</blockquote>

<p>默认情况下，服务器将在一个随机端口上启动，并触发常规的 LDAP 支持（不需要指定 <code>spring.ldap.urls</code> 属性）。</p>
<p>如果您的 classpath 上存在一个 <code>schema.ldif</code> 文件，其将用于初始化服务器。如果您想从不同的资源中加载脚本，可以使用 <code>spring.ldap.embedded.ldif</code> 属性。</p>
<p>默认情况下，将使用一个标准模式（schema）来校验 <code>LDIF</code> 文件。您可以使用 <code>spring.ldap.embedded.validation.enabled</code> 属性来关闭所有校验。如果您有自定义的属性，则可以使用 <code>spring.ldap.embedded.validation.schema</code> 来定义自定义属性类型或者对象类。</p>
<p><a id="boot-features-influxdb"></a></p>
<h3 id="3110、influxdb">31.10、InfluxDB</h3>
<p><a href="https://www.influxdata.com/" target="_blank">InfluxDB</a> 是一个开源时列数据库，其针对运营监控、应用程序指标、物联网传感器数据和实时分析等领域中的时间序列数据在速度、高可用存储和检索方面进行了优化。</p>
<p><a id="boot-features-connecting-to-influxdb"></a></p>
<h4 id="31101、连接-influxdb">31.10.1、连接 InfluxDB</h4>
<p>Spring Boot 自动配置 <code>InfluxDB</code> 实例，前提是 <code>Influxdb-java</code> 客户端在 classpath 上并且设置了数据库的 URL，如下所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.influx.url</span><span class="token attr-value"><span class="token punctuation">=</span>HTTP://172.0.0.1:8086</span>
</code></pre>
<p>如果与 InfluxDB 的连接需要用户和密码，则可以相应地设置 <code>spring.influx.user</code> 和 <code>spring.influx.password</code> 属性。</p>
<p>InfluxDB 依赖于 OkHttp。如果你需要调整 <code>InfluxDB</code> 在底层使用的 http 客户端，则可以注册一个 <code>InfluxDbOkHttpClientBuilderProvider</code> bean。</p>
<p><a id="boot-features-caching"></a></p>
<h2 id="32、缓存">32、缓存</h2>
<p>Spring Framework 支持以透明的方式向应用程序添加缓存。从本质上讲，将缓存应用于方法上，根据缓存数据减少方法的执行次数。缓存逻辑是透明的，不会对调用者造成任何干扰。通过 <code>@EnableCaching</code> 注解启用缓存支持，Spring Boot 就会自动配置缓存设置。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>有关更多详细信息，请查看 Spring Framework 参考文档的<a href="https://docs.spring.io/spring/docs/5.1.3.RELEASE/spring-framework-reference/integration.html#cache" target="_blank">相关部分</a>。</p>
</blockquote>
<p>简而言之，为服务添加缓存的操作就像在其方法中添加注解一样简单，如下所示：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>cache<span class="token punctuation">.</span>annotation</span><span class="token punctuation">.</span><span class="token class-name">Cacheable</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>stereotype</span><span class="token punctuation">.</span><span class="token class-name">Component</span><span class="token punctuation">;</span>

<span class="token annotation punctuation">@Component</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MathService</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@Cacheable</span><span class="token punctuation">(</span><span class="token string">"piDecimals"</span><span class="token punctuation">)</span>
    <span class="token keyword">public</span> <span class="token keyword">int</span> <span class="token function">computePiDecimal</span><span class="token punctuation">(</span><span class="token keyword">int</span> i<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment">// ...</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>此示例展示了如何在代价可能高昂的操作上使用缓存。在调用 <code>computePiDecimal</code> 之前，缓存支持会在 <code>piDecimals</code> 缓存中查找与 <code>i</code> 参数匹配的项。如果找到，则缓存中的内容会立即返回给调用者，并不会调用该方法。否则，将调用该方法，并在返回值之前更新缓存。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>您还可以使用标准 JSR-107（JCache）注解（例如 <code>@CacheResult</code>）。但是，我们强烈建议您<strong>不要</strong>将 Spring Cache 和 JCache 注解混合使用。</p>
</blockquote>
<p>如果您不添加任何指定的缓存库，Spring Boot 会自动配置一个使用并发 map 的 <a href="#boot-features-caching-provider-simple">simple provider</a>。当需要缓存时（例如前面示例中的 <code>piDecimals</code>），该 simple provider 会为您创建缓存。不推荐将 simple provider 用于生产环境，但它非常适合入门并帮助您了解这些功能。当您决定使用缓存提供者时，请务必阅读其文档以了解如何配置应用程序。几乎所有提供者都要求您显式配置应用程序中使用的每个缓存。有些提供了自定义 <code>spring.cache.cache-names</code> 属性以定义默认缓存。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>还可以透明地<a href="https://docs.spring.io/spring/docs/5.1.3.RELEASE/spring-framework-reference/integration.html#cache-annotations-put" target="_blank">更新</a>或<a href="https://docs.spring.io/spring/docs/5.1.3.RELEASE/spring-framework-reference/integration.html#cache-annotations-evict" target="_blank">回收</a>缓存中的数据。</p>
</blockquote>
<p><a id="boot-features-caching-provider"></a></p>
<h3 id="321、支持的缓存提供者">32.1、支持的缓存提供者</h3>
<p>缓存抽象不提供存储实现，其依赖于 <code>org.springframework.cache.Cache</code> 和 <code>org.springframework.cache.CacheManager</code> 接口实现的抽象。</p>
<p>如果您未定义 <code>CacheManager</code> 类型的 bean 或名为 <code>cacheResolver</code> 的 <code>CacheResolver</code>（请参阅 <a href="https://docs.spring.io/spring/docs/5.1.3.RELEASE/javadoc-api/org/springframework/cache/annotation/CachingConfigurer.html" target="_blank"><code>CachingConfigurer</code></a>），则 Spring Boot 会尝试检测以下提供者（按序号顺序）：</p>
<ol>
<li><a href="#boot-features-caching-provider-generic">Generic</a></li>
<li><a href="#boot-features-caching-provider-jcache">JCache (JSR-107)</a>(EhCache 3、Hazelcast、Infinispan 或其他)</li>
<li><a href="#boot-features-caching-provider-ehcache2">EhCache 2.x</a></li>
<li><a href="#boot-features-caching-provider-hazelcast">Hazelcast</a></li>
<li><a href="#boot-features-caching-provider-infinispan">Infinispan</a></li>
<li><a href="#boot-features-caching-provider-couchbase">Couchbase</a></li>
<li><a href="#boot-features-caching-provider-redis">Redis</a>
8 <a href="#boot-features-caching-provider-caffeine">Caffeine</a></li>
<li><a href="#boot-features-caching-provider-simple">Simple</a></li>
</ol>
<p><strong>提示</strong></p>
<blockquote>
<p>也可以通过设置 <code>spring.cache.type</code> 属性来强制指定缓存提供者。如果您需要在某些环境（比如测试）中<a href="#boot-features-caching-provider-none">完全禁用缓存</a>，请使用此属性。</p>
</blockquote>
<p><strong>提示</strong></p>
<blockquote>
<p>使用 <code>spring-boot-starter-cache</code> starter 快速添加基本的缓存依赖。starter 引入了 <code>spring-context-support</code>。如果手动添加依赖，则必须包含 <code>spring-context-support</code> 才能使用 JCache、EhCache 2.x 或 Guava 支持。</p>
</blockquote>
<p>如果通过 Spring Boot 自动配置 <code>CacheManager</code>，则可以通过暴露一个实现了 <code>CacheManagerCustomizer</code> 接口的 bean，在完全初始化之前进一步调整其配置。以下示例设置了一个 flag，表示应将 null 值传递给底层 map：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Bean</span>
<span class="token keyword">public</span> <span class="token class-name">CacheManagerCustomizer</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">ConcurrentMapCacheManager</span><span class="token punctuation">&gt;</span></span> <span class="token function">cacheManagerCustomizer</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">return</span> <span class="token keyword">new</span> <span class="token class-name">CacheManagerCustomizer</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">ConcurrentMapCacheManager</span><span class="token punctuation">&gt;</span></span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token annotation punctuation">@Override</span>
        <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">customize</span><span class="token punctuation">(</span><span class="token class-name">ConcurrentMapCacheManager</span> cacheManager<span class="token punctuation">)</span> <span class="token punctuation">{</span>
            cacheManager<span class="token punctuation">.</span><span class="token function">setAllowNullValues</span><span class="token punctuation">(</span><span class="token boolean">false</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">}</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>
<p><strong>注意</strong></p>
<blockquote>
<p>在前面示例中，需要一个自动配置的 <code>ConcurrentMapCacheManager</code>。如果不是这种情况（您提供了自己的配置或自动配置了不同的缓存提供者），则根本不会调用 customizer。您可以拥有多个 customizer，也可以使用 <code>@Order</code> 或 <code>Ordered</code> 来排序它们。</p>
</blockquote>
<p><a id="boot-features-caching-provider-generic"></a></p>
<h4 id="3211、generic">32.1.1、Generic</h4>
<p>如果上下文定义了<strong>至少</strong>一个 <code>org.springframework.cache.Cache</code> bean，则使用 Generic 缓存。将创建一个包装所有该类型 bean 的 <code>CacheManager</code>。</p>
<p><a id="boot-features-caching-provider-jcache"></a></p>
<h4 id="3212、jcache-jsr-107">32.1.2、JCache (JSR-107)</h4>
<p><a href="https://jcp.org/en/jsr/detail?id=107" target="_blank">JCache</a> 通过 classpath 上的 <code>javax.cache.spi.CachingProvider</code>（即 classpath 上存在符合 JSR-107 的缓存库）来引导，<code>jCacheCacheManager</code> 由 <code>spring-boot-starter-cache</code> starter 提供。您可以使用各种兼容库，Spring Boot 为 Ehcache 3、Hazelcast 和 Infinispan 提供依赖管理。您还可以添加任何其他兼容库。</p>
<p>可能存在多个提供者，在这种情况下必须明确指定提供者。即使 JSR-107 标准没有强制规定一个定义配置文件位置的标准化方法，Spring Boot 也会尽其所能设置一个包含实现细节的缓存，如下所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token comment"># 存在多个 provider 才需要这样做</span>
<span class="token constant">spring.cache.jcache.provider</span><span class="token attr-value"><span class="token punctuation">=</span>com.acme.MyCachingProvider</span>
<span class="token constant">spring.cache.jcache.config</span><span class="token attr-value"><span class="token punctuation">=</span>classpath:acme.xml</span>
</code></pre>
<p><strong>注意</strong></p>
<blockquote>
<p>当缓存库同时提供原生实现和 JSR-107 支持时，Spring Boot 更倾向 JSR-107 支持，因此当您切换到不同的 JSR-107 实现时，还可以使用相同的功能。</p>
</blockquote>
<p><strong>提示</strong></p>
<blockquote>
<p>Spring Boot 对 <a href="#boot-features-hazelcast">Hazelcast</a> 的支持一般。如果有一个 <code>HazelcastInstance</code> 可用，它也会自动为 <code>CacheManager</code> 复用，除非指定了 <code>spring.cache.jcache.config</code> 属性。</p>
</blockquote>
<p>有两种方法可以自定义底层的 <code>javax.cache.cacheManager</code>：</p>
<ul>
<li>可以通过设置 <code>spring.cache.cache-names</code> 属性在启动时创建缓存。如果定义了自定义 <code>javax.cache.configuration.Configuration</code> bean，则会使用它来自定义。</li>
<li>使用 <code>CacheManager</code> 的引用调用 <code>org.springframework.boot.autoconfigure.cache.JCacheManagerCustomizer</code> bean 以进行完全自定义。</li>
</ul>
<p><strong>提示</strong></p>
<blockquote>
<p>如果定义了一个标准的 <code>javax.cache.CacheManager</code> bean，它将自动包装进一个抽象所需的 <code>org.springframework.cache.CacheManager</code> 实现中，而不会应用自定义配置。</p>
</blockquote>
<p><a id="boot-features-caching-provider-ehcache2"></a></p>
<h4 id="3213、ehcache-2x">32.1.3、EhCache 2.x</h4>
<p>如果可以在 classpath 的根目录中找到名为 <code>ehcache.xml</code> 的文件，则使用 EhCache 2.x。如果找到 EhCache 2.x，则使用 <code>spring-boot-starter-cache</code> starter 提供的 <code>EhCacheCacheManager</code> 来启动缓存管理器。还可以提供其他配置文件，如下所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.cache.ehcache.config</span><span class="token attr-value"><span class="token punctuation">=</span>classpath:config/another-config.xml</span>
</code></pre>
<p><a id="boot-features-caching-provider-hazelcast"></a></p>
<h4 id="3214、hazelcast">32.1.4、Hazelcast</h4>
<p>Spring Boot 对 <a href="#boot-features-hazelcast">Hazelcast</a> 的支持一般。如果自动配置了一个 <code>HazelcastInstance</code>，它将自动包装进 <code>CacheManager</code> 中。</p>
<p><a id="boot-features-caching-provider-infinispan"></a></p>
<h4 id="3215、infinispan">32.1.5、Infinispan</h4>
<p><a href="http://infinispan.org/" target="_blank">Infinispan</a> 没有默认的配置文件位置，因此必须明确指定。否则将使用默认配置引导。</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.cache.infinispan.config</span><span class="token attr-value"><span class="token punctuation">=</span>infinispan.xml</span>
</code></pre>
<p>可以通过设置 <code>spring.cache.cache-names</code> 属性在启动时创建缓存。如果定义了自定义 <code>ConfigurationBuilder</code> bean，则它将用于自定义缓存。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>Infinispan 在 Spring Boot 中的支持仅限于内嵌模式，非常简单。如果你想要更多选项，你应该使用官方的 Infinispan Spring Boot starter。有关更多详细信息，请参阅 <a href="https://github.com/infinispan/infinispan-spring-boot" target="_blank">Infinispan 文档</a>。</p>
</blockquote>
<p><a id="boot-features-caching-provider-couchbase"></a></p>
<h4 id="3216、couchbase">32.1.6、Couchbase</h4>
<p>如果 <a href="https://www.couchbase.com/" target="_blank">Couchbase</a> Java 客户端和 <code>couchbase-spring-cache</code> 实现可用且已经<a href="#boot-features-couchbase">配置</a>了 Couchbase，则应用程序会自动配置一个 <code>CouchbaseCacheManager</code>。也可以通过设置 <code>spring.cache.cache-names</code> 属性在启动时创建其他缓存。这些缓存在自动配置的 Bucket 上操作。您<strong>还</strong>可以使用 customizer 在其他 <code>Bucket</code> 上创建缓存。假设您需要在 <strong>main</strong> <code>Bucket</code> 上有两个缓存（<code>cache1</code> 和 <code>cache2</code>），并且 <strong>another</strong> <code>Bucket</code> 有一个过期时间为 2 秒的缓存（<code>cache3</code>）。您可以通过配置创建这两个缓存，如下所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.cache.cache-names</span><span class="token attr-value"><span class="token punctuation">=</span>cache1,cache2</span>
</code></pre>
<p>然后，您可以定义一个 <code>@Configuration</code> 类来配置其他 <code>Bucket</code> 和 <code>cache3</code> 缓存，如下所示：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Configuration</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">CouchbaseCacheConfiguration</span> <span class="token punctuation">{</span>

    <span class="token keyword">private</span> <span class="token keyword">final</span> <span class="token class-name">Cluster</span> cluster<span class="token punctuation">;</span>

    <span class="token keyword">public</span> <span class="token class-name">CouchbaseCacheConfiguration</span><span class="token punctuation">(</span><span class="token class-name">Cluster</span> cluster<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>cluster <span class="token operator">=</span> cluster<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token annotation punctuation">@Bean</span>
    <span class="token keyword">public</span> <span class="token class-name">Bucket</span> <span class="token function">anotherBucket</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> <span class="token keyword">this</span><span class="token punctuation">.</span>cluster<span class="token punctuation">.</span><span class="token function">openBucket</span><span class="token punctuation">(</span><span class="token string">"another"</span><span class="token punctuation">,</span> <span class="token string">"secret"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token annotation punctuation">@Bean</span>
    <span class="token keyword">public</span> <span class="token class-name">CacheManagerCustomizer</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">CouchbaseCacheManager</span><span class="token punctuation">&gt;</span></span> <span class="token function">cacheManagerCustomizer</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> c <span class="token operator">-&gt;</span> <span class="token punctuation">{</span>
            c<span class="token punctuation">.</span><span class="token function">prepareCache</span><span class="token punctuation">(</span><span class="token string">"cache3"</span><span class="token punctuation">,</span> <span class="token class-name">CacheBuilder</span><span class="token punctuation">.</span><span class="token function">newInstance</span><span class="token punctuation">(</span><span class="token function">anotherBucket</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span>
                    <span class="token punctuation">.</span><span class="token function">withExpiration</span><span class="token punctuation">(</span><span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>此示例配置复用了通过自动配置创建的 <code>Cluster</code>。</p>
<p><a id="boot-features-caching-provider-redis"></a></p>
<h4 id="3217、redis">32.1.7、Redis</h4>
<p>如果 <a href="http://redis.io/" target="_blank">Redis</a> 可用并已经配置，则应用程序会自动配置一个 <code>RedisCacheManager</code>。通过设置 <code>spring.cache.cache-names</code> 属性可以在启动时创建其他缓存，并且可以使用 <code>spring.cache.redis.*</code> 属性配置缓存默认值。例如，以下配置创建 <code>cache1</code> 和 <code>cache2</code> 缓存，他们的<strong>有效时间</strong>为 10 分钟：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.cache.cache-names</span><span class="token attr-value"><span class="token punctuation">=</span>cache1,cache2</span>
<span class="token constant">spring.cache.redis.time-to-live</span><span class="token attr-value"><span class="token punctuation">=</span>600000</span>
</code></pre>
<p><strong>注意</strong></p>
<blockquote>
<p>默认情况下，会添加一个 key 前缀，这样做是因为如果两个单独的缓存使用了相同的键，Redis 不支持重叠 key，而缓存也不能返回无效值。如果您创建自己的 <code>RedisCacheManager</code>，我们强烈建议您启用此设置。</p>
</blockquote>
<p><strong>提示</strong></p>
<blockquote>
<p>您可以通过添加自己的 <code>RedisCacheConfiguration</code> <code>@Bean</code> 来完全控制配置。如果您想自定义序列化策略，这种方式可能很有用。</p>
</blockquote>
<p><a id="boot-features-caching-provider-caffeine"></a></p>
<h4 id="3218、caffeine">32.1.8、Caffeine</h4>
<p><a href="https://github.com/ben-manes/caffeine" target="_blank">Caffeine</a> 是一个使用了 Java 8 重写 Guava 缓存，用于取代 Guava 支持的缓存库。如果 Caffeine 存在，则应用程序会自动配置一个 <code>CaffeineCacheManager</code>（由 <code>spring-boot-starter-cache</code> starter 提供）。可以通过设置 <code>spring.cache.cache-names</code> 属性在启动时创建缓存，并且可以通过以下方式之一（按序号顺序）自定义缓存：</p>
<ol>
<li>一个由 <code>spring.cache.caffeine.spec</code> 定义的缓存规范</li>
<li>一个已定义的 <code>com.github.benmanes.caffeine.cache.CaffeineSpec</code> bean</li>
<li>一个已定义的 <code>com.github.benmanes.caffeine.cache.Caffeine</code> bean</li>
</ol>
<p>例如，以下配置创建 <code>cache1</code> 和 <code>cache2</code> 缓存，最大大小为 500，<strong>有效时间</strong> 为 10 分钟：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.cache.cache-names</span><span class="token attr-value"><span class="token punctuation">=</span>cache1,cache2</span>
<span class="token constant">spring.cache.caffeine.spec</span><span class="token attr-value"><span class="token punctuation">=</span>maximumSize=500,expireAfterAccess=600s</span>
</code></pre>
<p>如果定义了 <code>com.github.benmanes.caffeine.cache.CacheLoader</code> bean，它将自动与 <code>CaffeineCacheManager</code> 关联。由于 <code>CacheLoader</code> 将与缓存管理器管理的<strong>所有</strong>缓存相关联，因此必须将其定义为 <code>CacheLoader<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>Object,</span> <span class="token attr-name">Object</span><span class="token punctuation">&gt;</span></span></code>。自动配置会忽略所有其他泛型类型。</p>
<p><a id="boot-features-caching-provider-simple"></a></p>
<h4 id="3219、simple">32.1.9、Simple</h4>
<p>如果找不到其他提供者，则配置使用一个 <code>ConcurrentHashMap</code> 作为缓存存储的简单实现。如果您的应用程序中没有缓存库，则该项为默认值。默认情况下，会根据需要创建缓存，但您可以通过设置 <code>cache-names</code> 属性来限制可用缓存的列表。例如，如果只需要 <code>cache1</code> 和 <code>cache2</code> 缓存，请按如下设置 <code>cache-names</code> 属性：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.cache.cache-names</span><span class="token attr-value"><span class="token punctuation">=</span>cache1,cache2</span>
</code></pre>
<p>如果这样做了，并且您的应用程序使用了未列出的缓存，则运行时在它需要缓存时会触发失败，但在启动时则不会。这类似于<strong>真实</strong>缓存提供者在使用未声明的缓存时触发的行为方式。</p>
<p><a id="boot-features-caching-provider-none"></a></p>
<h4 id="32110、none">32.1.10、None</h4>
<p>当配置中存在 <code>@EnableCaching</code> 时，也需要合适的缓存配置。如果需要在某些环境中完全禁用缓存，请将缓存类型强制设置为 <code>none</code> 以使用 no-op 实现，如下所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.cache.type</span><span class="token attr-value"><span class="token punctuation">=</span>none</span>
</code></pre>
<p><a id="boot-features-messaging"></a></p>
<h2 id="33、消息传递">33、消息传递</h2>
<p>Spring Framework 为消息传递系统集成提供了广泛的支持，从使用 <code>JmsTemplate</code> 简化 JMS API 的使用到异步接收消息的完整基础设施。Spring AMQP 为高级消息队列协议（Advanced Message Queuing Protocol，AMQP）提供了类似的功能集合。Spring Boot 还为 <code>RabbitTemplate</code> 和 RabbitMQ 提供自动配置选项。Spring WebSocket 本身包含了对 STOMP 消息传递的支持，Spring Boot 通过 starter 和少量自动配置即可支持它。Spring Boot 同样支持 Apache Kafka。</p>
<p><a id="boot-features-jms"></a></p>
<h3 id="331、jms">33.1、JMS</h3>
<p><code>javax.jms.ConnectionFactory</code> 接口提供了一种创建 <code>javax.jms.Connection</code> 的标准方法，可与 JMS broker（代理）进行交互。虽然 Spring 需要一个 <code>ConnectionFactory</code> 来与 JMS 一同工作，但是您通常不需要自己直接使用它，而是可以依赖更高级别的消息传递抽象。（有关详细信息，请参阅 Spring Framework 参考文档的<a href="https://docs.spring.io/spring/docs/5.1.3.RELEASE/spring-framework-reference/integration.html#jms" target="_blank">相关部分</a>。）Spring Boot 还会自动配置发送和接收消息所需的基础设施。</p>
<p><a id="boot-features-activemq"></a></p>
<h4 id="3311、activemq-支持">33.1.1、ActiveMQ 支持</h4>
<p>当 <a href="http://activemq.apache.org/" target="_blank">ActiveMQ</a> 在 classpath 上可用时，Spring Boot 也可以配置一个 <code>ConnectionFactory</code>。如果 broker 存在，则会自动启动并配置一个内嵌式 broker（前提是未通过配置指定 broder URL）。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>如果使用 <code>spring-boot-starter-activemq</code>，则提供了连接到 ActiveMQ 实例必须依赖或内嵌一个 ActiveMQ 实例，以及与 JMS 集成的 Spring 基础设施。</p>
</blockquote>
<p>ActiveMQ 配置由 <code>spring.activemq.*</code> 中的外部配置属性控制。例如，您可以在 <code>application.properties</code> 中声明以下部分：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.activemq.broker-url</span><span class="token attr-value"><span class="token punctuation">=</span>tcp://192.168.1.210:9876</span>
<span class="token constant">spring.activemq.user</span><span class="token attr-value"><span class="token punctuation">=</span>admin</span>
<span class="token constant">spring.activemq.password</span><span class="token attr-value"><span class="token punctuation">=</span>secret</span>
</code></pre>
<p>默认情况下，<code>CachingConnectionFactory</code> 将原生的 <code>ConnectionFactory</code> 使用可由 <code>spring.jms.*</code> 中的外部配置属性控制的合理设置包装起来：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.jms.cache.session-cache-size</span><span class="token attr-value"><span class="token punctuation">=</span>5</span>
</code></pre>
<p>如果您更愿意使用原生池，则可以通过向 <code>org.messaginghub:pooled-jms</code> 添加一个依赖并相应地配置 <code>JmsPoolConnectionFactory</code> 来实现，如下所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.activemq.pool.enabled</span><span class="token attr-value"><span class="token punctuation">=</span>true</span>
<span class="token constant">spring.activemq.pool.max-connections</span><span class="token attr-value"><span class="token punctuation">=</span>50</span>
</code></pre>
<p><strong>提示</strong></p>
<blockquote>
<p>有关更多支持的选项，请参阅 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.1.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/jms/activemq/ActiveMQProperties.java" target="_blank"><code>ActiveMQProperties</code></a>。您还可以注册多个实现了 <code>ActiveMQConnectionFactoryCustomizer</code> 的的 bean，以进行更高级的自定义。</p>
</blockquote>
<p>默认情况下，ActiveMQ 会创建一个 destination（目标）（如果它尚不存在），以便根据提供的名称解析 destination。</p>
<p><a id="boot-features-artemis"></a></p>
<h4 id="3312、artemis-支持">33.1.2、Artemis 支持</h4>
<p>Spring Boot 可以在检测到 <a href="http://activemq.apache.org/artemis/" target="_blank">Artemis</a> 在 classpath 上可用时自动配置一个 <code>ConnectionFactory</code>。如果存在 broker，则会自动启动并配置一个内嵌 broker（除非已明确设置 mode 属性）。支持的 mode 为 <code>embedded</code>（明确表示需要一个内嵌 broker，如果 broker 在 classpath 上不可用则发生错误）和 <code>native</code>（使用 netty 传输协议连接到 broker）。配置后者后，Spring Boot 会使用默认设置配置一个 <code>ConnectionFactory</code>，该 <code>ConnectionFactory</code> 连接到在本地计算机上运行的 broker。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>如果使用了 <code>spring-boot-starter-artemis</code>，则会提供连接到现有的 Artemis 实例的必须依赖，以及与 JMS 集成的Spring 基础设施。将 <code>org.apache.activemq:artemis-jms-server</code> 添加到您的应用程序可让您使用内嵌模式。</p>
</blockquote>
<p>Artemis 配置由 <code>spring.artemis.*</code> 中的外部配置属性控制。例如，您可以在 <code>application.properties</code> 中声明以下部分：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.artemis.mode</span><span class="token attr-value"><span class="token punctuation">=</span>native</span>
<span class="token constant">spring.artemis.host</span><span class="token attr-value"><span class="token punctuation">=</span>192.168.1.210</span>
<span class="token constant">spring.artemis.port</span><span class="token attr-value"><span class="token punctuation">=</span>9876</span>
<span class="token constant">spring.artemis.user</span><span class="token attr-value"><span class="token punctuation">=</span>admin</span>
<span class="token constant">spring.artemis.password</span><span class="token attr-value"><span class="token punctuation">=</span>secret</span>
</code></pre>
<p>内嵌 broker 时，您可以选择是否要启用持久化并列出应该可用的 destination。可以将这些指定为以逗号分隔的列表，以使用默认选项创建它们，也可以定义类型为 <code>org.apache.activemq.artemis.jms.server.config.JMSQueueConfiguration</code> 或 <code>org.apache.activemq.artemis.jms.server.config.TopicConfiguration</code> 的 bean，分别用于高级队列和 topic（主题）配置。</p>
<p>默认情况下，<code>CachingConnectionFactory</code> 将原生的 <code>ConnectionFactory</code> 使用可由 <code>spring.jms.*</code> 中的外部配置属性控制的合理设置包装起来：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.jms.cache.session-cache-size</span><span class="token attr-value"><span class="token punctuation">=</span>5</span>
</code></pre>
<p>如果您更愿意使用原生池，则可以通过向 <code>org.messaginghub:pooled-jms</code> 添加一个依赖并相应地配置 <code>JmsPoolConnectionFactory</code> 来实现，如下所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.artemis.pool.enabled</span><span class="token attr-value"><span class="token punctuation">=</span>true</span>
<span class="token constant">spring.artemis.pool.max-connections</span><span class="token attr-value"><span class="token punctuation">=</span>50</span>
</code></pre>
<p>有关更多支持的选项，请参阅 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.1.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/jms/artemis/ArtemisProperties.java" target="_blank"><code>ArtemisProperties</code></a>。</p>
<p>不涉及 JNDI 查找，使用 Artemis 配置中的 <code>name</code> 属性或通过配置提供的名称来解析目标（destination）名称。</p>
<p><a id="boot-features-jms-jndi"></a></p>
<h4 id="3313、使用-jndi-connectionfactory">33.1.3、使用 JNDI ConnectionFactory</h4>
<p>如果您在应用程序服务器中运行应用程序，Spring Boot 会尝试使用 JNDI 找到 JMS <code>ConnectionFactory</code>。默认情况下，将检查 <code>java:/JmsXA</code> 和 <code>java:/XAConnectionFactory</code> 这两个位置。如果需要指定其他位置，可以使用 <code>spring.jms.jndi-name</code> 属性，如下所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.jms.jndi-name</span><span class="token attr-value"><span class="token punctuation">=</span>java:/MyConnectionFactory</span>
</code></pre>
<p><a id="boot-features-using-jms-sending"></a></p>
<h4 id="3314、发送消息">33.1.4、发送消息</h4>
<p>Spring 的 <code>JmsTemplate</code> 是自动配置的，你可以直接将它注入到你自己的 bean 中，如下所示：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>beans<span class="token punctuation">.</span>factory<span class="token punctuation">.</span>annotation</span><span class="token punctuation">.</span><span class="token class-name">Autowired</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>jms<span class="token punctuation">.</span>core</span><span class="token punctuation">.</span><span class="token class-name">JmsTemplate</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>stereotype</span><span class="token punctuation">.</span><span class="token class-name">Component</span><span class="token punctuation">;</span>

<span class="token annotation punctuation">@Component</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyBean</span> <span class="token punctuation">{</span>

    <span class="token keyword">private</span> <span class="token keyword">final</span> <span class="token class-name">JmsTemplate</span> jmsTemplate<span class="token punctuation">;</span>

    <span class="token annotation punctuation">@Autowired</span>
    <span class="token keyword">public</span> <span class="token class-name">MyBean</span><span class="token punctuation">(</span><span class="token class-name">JmsTemplate</span> jmsTemplate<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>jmsTemplate <span class="token operator">=</span> jmsTemplate<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token comment">// ...</span>

<span class="token punctuation">}</span>
</code></pre>
<p><strong>注意</strong></p>
<blockquote>
<p><code>JmsMessagingTemplate</code> 可以以类似的方式注入。如果定义了 <code>DestinationResolver</code> 或 <code>MessageConverter</code> bean，它将自动关联到自动配置的 <code>JmsTemplate</code>。</p>
</blockquote>
<p><a id="boot-features-using-jms-receiving"></a></p>
<h4 id="3315、接收消息">33.1.5、接收消息</h4>
<p>当存在 JMS 基础设施时，可以使用 <code>@JmsListener</code> 对任何 bean 进行注解以创建监听器（listener）端点。如果未定义 <code>JmsListenerContainerFactory</code>，则会自动配置一个默认的（factory）。如果定义了 <code>DestinationResolver</code> 或 <code>MessageConverter</code> bean，它将自动关联到默认的 factory。</p>
<p>默认情况下，默认 factory 是具有事务特性的。如果您在存在有 <code>JtaTransactionManager</code> 的基础设施中运行，则默认情况下它与监听器容器相关联。如果不是，则 <code>sessionTransacted</code> flag 将为启用（enabled）。在后一种情况下，您可以通过在监听器方法（或其委托）上添加 <code>@Transactional</code>，将本地数据存储事务与传入消息的处理相关联。这确保了在本地事务完成后传入消息能被告知。这还包括了发送已在同一 JMS 会话上执行的响应消息。</p>
<p>以下组件在 <code>someQueue</code> destination 上创建一个监听器端点：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Component</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyBean</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@JmsListener</span><span class="token punctuation">(</span>destination <span class="token operator">=</span> <span class="token string">"someQueue"</span><span class="token punctuation">)</span>
    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">processMessage</span><span class="token punctuation">(</span><span class="token class-name">String</span> content<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment">// ...</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p><strong>提示</strong></p>
<blockquote>
<p>有关更多详细信息，请参阅 <a href="https://docs.spring.io/spring/docs/5.1.3.RELEASE/javadoc-api/org/springframework/jms/annotation/EnableJms.html" target="_blank"><code>@EnableJms</code> 的 Javadoc</a>。</p>
</blockquote>
<p>如果需要创建更多 <code>JmsListenerContainerFactory</code> 实例或覆盖缺省值，Spring Boot 会提供一个 <code>DefaultJmsListenerContainerFactoryConfigurer</code>，您可以使用它来初始化 <code>DefaultJmsListenerContainerFactory</code>，其设置与自动配置的 factory 设置相同。</p>
<p>例如，以下示例暴露了另一个使用特定 <code>MessageConverter</code> 的 factory：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Configuration</span>
<span class="token keyword">static</span> <span class="token keyword">class</span> <span class="token class-name">JmsConfiguration</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@Bean</span>
    <span class="token keyword">public</span> <span class="token class-name">DefaultJmsListenerContainerFactory</span> <span class="token function">myFactory</span><span class="token punctuation">(</span>
            <span class="token class-name">DefaultJmsListenerContainerFactoryConfigurer</span> configurer<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token class-name">DefaultJmsListenerContainerFactory</span> factory <span class="token operator">=</span>
                <span class="token keyword">new</span> <span class="token class-name">DefaultJmsListenerContainerFactory</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        configurer<span class="token punctuation">.</span><span class="token function">configure</span><span class="token punctuation">(</span>factory<span class="token punctuation">,</span> <span class="token function">connectionFactory</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        factory<span class="token punctuation">.</span><span class="token function">setMessageConverter</span><span class="token punctuation">(</span><span class="token function">myMessageConverter</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">return</span> factory<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>然后，您可以在任何 <code>@JmsListener</code> 注解的方法中使用该 factory，如下所示：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Component</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyBean</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@JmsListener</span><span class="token punctuation">(</span>destination <span class="token operator">=</span> <span class="token string">"someQueue"</span><span class="token punctuation">,</span> containerFactory<span class="token operator">=</span><span class="token string">"myFactory"</span><span class="token punctuation">)</span>
    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">processMessage</span><span class="token punctuation">(</span><span class="token class-name">String</span> content<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment">// ...</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p><a id="boot-features-amqp"></a></p>
<h3 id="332、amqp">33.2、AMQP</h3>
<p>高级消息队列协议（Advanced Message Queuing Protocol，AMQP）是一个平台无关，面向消息中间件的连接级协议。Spring AMQP 项目将核心 Spring 概念应用于基于 AMQP 消息传递解决方案的开发。Spring Boot 为通过 RabbitMQ 使用 AMQP 提供了一些快捷方法，包括 <code>spring-boot-starter-amqp</code> starter。</p>
<p><a id="boot-features-rabbitmq"></a></p>
<h4 id="3321、rabbitmq-支持">33.2.1、RabbitMQ 支持</h4>
<p><a href="https://www.rabbitmq.com/" target="_blank">RabbitMQ</a> 是一个基于 AMQP 协议的轻量级、可靠、可扩展且可移植的消息代理。Spring 使用 RabbitMQ 通过 AMQP 协议进行通信。</p>
<p>RabbitMQ 配置由 <code>spring.rabbitmq.*</code> 中的外部配置属性控制。例如，您可以在 <code>application.properties</code> 中声明以下部分：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.rabbitmq.host</span><span class="token attr-value"><span class="token punctuation">=</span>localhost</span>
<span class="token constant">spring.rabbitmq.port</span><span class="token attr-value"><span class="token punctuation">=</span>5672</span>
<span class="token constant">spring.rabbitmq.username</span><span class="token attr-value"><span class="token punctuation">=</span>admin</span>
<span class="token constant">spring.rabbitmq.password</span><span class="token attr-value"><span class="token punctuation">=</span>secret</span>
</code></pre>
<p>如果上下文中存在 <code>ConnectionNameStrategy</code> bean，它将自动用于命名由自动配置的 <code>ConnectionFactory</code> 所创建的连接。有关更多支持的选项，请参阅 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.1.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/amqp/RabbitProperties.java" target="_blank">RabbitProperties</a>。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>有关详细信息，请参阅<a href="https://spring.io/blog/2010/06/14/understanding-amqp-the-protocol-used-by-rabbitmq/" target="_blank">理解 AMQP、RabbitMQ 使用的协议</a>。</p>
</blockquote>
<p><a id="boot-features-using-amqp-sending"></a></p>
<h4 id="3322、发送消息">33.2.2、发送消息</h4>
<p>Spring 的 <code>AmqpTemplate</code> 和 <code>AmqpAdmin</code> 是自动配置的，您可以将它们直接注入自己的 bean 中，如下所示：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>amqp<span class="token punctuation">.</span>core</span><span class="token punctuation">.</span><span class="token class-name">AmqpAdmin</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>amqp<span class="token punctuation">.</span>core</span><span class="token punctuation">.</span><span class="token class-name">AmqpTemplate</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>beans<span class="token punctuation">.</span>factory<span class="token punctuation">.</span>annotation</span><span class="token punctuation">.</span><span class="token class-name">Autowired</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>stereotype</span><span class="token punctuation">.</span><span class="token class-name">Component</span><span class="token punctuation">;</span>

<span class="token annotation punctuation">@Component</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyBean</span> <span class="token punctuation">{</span>

    <span class="token keyword">private</span> <span class="token keyword">final</span> <span class="token class-name">AmqpAdmin</span> amqpAdmin<span class="token punctuation">;</span>
    <span class="token keyword">private</span> <span class="token keyword">final</span> <span class="token class-name">AmqpTemplate</span> amqpTemplate<span class="token punctuation">;</span>

    <span class="token annotation punctuation">@Autowired</span>
    <span class="token keyword">public</span> <span class="token class-name">MyBean</span><span class="token punctuation">(</span><span class="token class-name">AmqpAdmin</span> amqpAdmin<span class="token punctuation">,</span> <span class="token class-name">AmqpTemplate</span> amqpTemplate<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>amqpAdmin <span class="token operator">=</span> amqpAdmin<span class="token punctuation">;</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>amqpTemplate <span class="token operator">=</span> amqpTemplate<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token comment">// ...</span>

<span class="token punctuation">}</span>
</code></pre>
<p><strong>注意</strong></p>
<blockquote>
<p>RabbitMessagingTemplate 可以以类似的方式注入。如果定义了 <code>MessageConverter</code> bean，它将自动关联到自动配置的 <code>AmqpTemplate</code>。</p>
</blockquote>
<p>如有必要，所有定义为 bean 的 <code>org.springframework.amqp.core.Queue</code> 都会自动在 RabbitMQ 实例上声明相应的队列。</p>
<p>要重试操作，可以在 <code>AmqpTemplate</code> 上启用重试（例如，在 broker 连接丢失的情况下）：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.rabbitmq.template.retry.enabled</span><span class="token attr-value"><span class="token punctuation">=</span>true</span>
<span class="token constant">spring.rabbitmq.template.retry.initial-interval</span><span class="token attr-value"><span class="token punctuation">=</span>2s</span>
</code></pre>
<p>默认情况下禁用重试。您还可以通过声明 <code>RabbitRetryTemplateCustomizer</code> bean 以编程方式自定义 <code>RetryTemplate</code>。</p>
<p><a id="boot-features-using-amqp-receiving"></a></p>
<h4 id="3323、接收消息">33.2.3、接收消息</h4>
<p>当 Rabbit 基础设施存在时，可以使用 <code>@RabbitListener</code> 注解任何 bean 以创建监听器端点。如果未定义 <code>RabbitListenerContainerFactory</code>，则会自动配置一个默认的 <code>SimpleRabbitListenerContainerFactory</code>，您可以使用 <code>spring.rabbitmq.listener.type</code> 属性切换到一个直接容器。如果定义了 <code>MessageConverter</code> 或 <code>MessageRecoverer</code> bean，它将自动与默认 factory 关联。</p>
<p>以下示例组件在 <code>someQueue</code> 队列上创建一个侦听监听器端点：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Component</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyBean</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@RabbitListener</span><span class="token punctuation">(</span>queues <span class="token operator">=</span> <span class="token string">"someQueue"</span><span class="token punctuation">)</span>
    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">processMessage</span><span class="token punctuation">(</span><span class="token class-name">String</span> content<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment">// ...</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p><strong>提示</strong></p>
<blockquote>
<p>有关更多详细信息，请参阅 <a href="https://docs.spring.io/spring-amqp/docs/current/api/org/springframework/amqp/rabbit/annotation/EnableRabbit.html" target="_blank"><code>@EnableRabbit</code> 的 Javadoc</a>。</p>
</blockquote>
<p>如果需要创建更多 <code>RabbitListenerContainerFactory</code> 实例或覆盖缺省值，Spring Boot 提供了一个 <code>SimpleRabbitListenerContainerFactoryConfigurer</code> 和一个 <code>DirectRabbitListenerContainerFactoryConfigurer</code>，您可以使用它来初始化 <code>SimpleRabbitListenerContainerFactory</code> 和 <code>DirectRabbitListenerContainerFactory</code>，其设置与使用自动配置的 factory 相同。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>这两个 bean 与您选择的容器类型没有关系，它们通过自动配置暴露。</p>
</blockquote>
<p>例如，以下配置类暴露了另一个使用特定 <code>MessageConverter</code> 的 factory：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Configuration</span>
<span class="token keyword">static</span> <span class="token keyword">class</span> <span class="token class-name">RabbitConfiguration</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@Bean</span>
    <span class="token keyword">public</span> <span class="token class-name">SimpleRabbitListenerContainerFactory</span> <span class="token function">myFactory</span><span class="token punctuation">(</span>
            <span class="token class-name">SimpleRabbitListenerContainerFactoryConfigurer</span> configurer<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token class-name">SimpleRabbitListenerContainerFactory</span> factory <span class="token operator">=</span>
                <span class="token keyword">new</span> <span class="token class-name">SimpleRabbitListenerContainerFactory</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        configurer<span class="token punctuation">.</span><span class="token function">configure</span><span class="token punctuation">(</span>factory<span class="token punctuation">,</span> connectionFactory<span class="token punctuation">)</span><span class="token punctuation">;</span>
        factory<span class="token punctuation">.</span><span class="token function">setMessageConverter</span><span class="token punctuation">(</span><span class="token function">myMessageConverter</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">return</span> factory<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>然后，您可以在任何 <code>@RabbitListener</code> 注解的方法中使用该 factory，如下所示：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Component</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyBean</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@RabbitListener</span><span class="token punctuation">(</span>queues <span class="token operator">=</span> <span class="token string">"someQueue"</span><span class="token punctuation">,</span> containerFactory<span class="token operator">=</span><span class="token string">"myFactory"</span><span class="token punctuation">)</span>
    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">processMessage</span><span class="token punctuation">(</span><span class="token class-name">String</span> content<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment">// ...</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>您可以启用重试机制来处理监听器的异常抛出情况。默认情况下使用 <code>RejectAndDontRequeueRecoverer</code>，但您可以定义自己的 <code>MessageRecoverer</code>。如果 broker 配置了重试机制，当重试次数耗尽时，则拒绝消息并将其丢弃或路由到死信（dead-letter）exchange 中。默认情况下重试机制为禁用。您还可以通过声明 <code>RabbitRetryTemplateCustomizer</code> bean 以编程方式自定义 <code>RetryTemplate</code>。</p>
<p><strong>重要</strong></p>
<blockquote>
<p>默认情况下，如果禁用重试并且监听器异常抛出，则会无限期地重试传递。您可以通过两种方式修改此行为：将 <code>defaultRequeueRejected</code> 属性设置为 <code>false</code>，以便尝试零重传或抛出 <code>AmqpRejectAndDontRequeueException</code> 以指示拒绝该消息。后者是启用重试并且达到最大传递尝试次数时使用的机制。</p>
</blockquote>
<p><a id="boot-features-kafka"></a></p>
<h3 id="333、apache-kafka-支持">33.3、Apache Kafka 支持</h3>
<p>通过提供 <code>spring-kafka</code> 项目的自动配置来支持 <a href="https://kafka.apache.org/" target="_blank">Apache Kafka</a>。</p>
<p>Kafka 配置由 <code>spring.kafka.*</code> 中的外部配置属性控制。例如，您可以在 <code>application.properties</code> 中声明以下部分：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.kafka.bootstrap-servers</span><span class="token attr-value"><span class="token punctuation">=</span>localhost:9092</span>
<span class="token constant">spring.kafka.consumer.group-id</span><span class="token attr-value"><span class="token punctuation">=</span>myGroup</span>
</code></pre>
<p><strong>提示</strong></p>
<blockquote>
<p>要在启动时创建主题（topic），请添加 <code>NewTopic</code> 类型的 Bean。如果主题已存在，则忽略该 bean。</p>
</blockquote>
<p>有关更多支持的选项，请参阅 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.1.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/kafka/KafkaProperties.java" target="_blank"><code>KafkaProperties</code></a>。</p>
<p><a id="boot-features-kafka-sending-a-message"></a></p>
<h4 id="3331、发送消息">33.3.1、发送消息</h4>
<p>Spring 的 <code>KafkaTemplate</code> 是自动配置的，您可以直接在自己的 bean 中装配它，如下所示：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Component</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyBean</span> <span class="token punctuation">{</span>

    <span class="token keyword">private</span> <span class="token keyword">final</span> <span class="token class-name">KafkaTemplate</span> kafkaTemplate<span class="token punctuation">;</span>

    <span class="token annotation punctuation">@Autowired</span>
    <span class="token keyword">public</span> <span class="token class-name">MyBean</span><span class="token punctuation">(</span><span class="token class-name">KafkaTemplate</span> kafkaTemplate<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>kafkaTemplate <span class="token operator">=</span> kafkaTemplate<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token comment">// ...</span>

<span class="token punctuation">}</span>
</code></pre>
<p><strong>注意</strong></p>
<blockquote>
<p>如果定义了属性 <code>spring.kafka.producer.transaction-id-prefix</code>，则会自动配置一个 <code>KafkaTransactionManager</code>。此外，如果定义了 <code>RecordMessageConverter</code> bean，它将自动关联到自动配置的 <code>KafkaTemplate</code>。</p>
</blockquote>
<p><a id="boot-features-kafka-receiving-a-message"></a></p>
<h4 id="3332、接收消息">33.3.2、接收消息</h4>
<p>当存在 Apache Kafka 基础设施时，可以使用 <code>@KafkaListener</code> 注解任何 bean 以创监听器端点。如果未定义 <code>KafkaListenerContainerFactory</code>，则会使用 <code>spring.kafka.listener.*</code> 中定义的 key 自动配置一个默认的 factory。</p>
<p>以下组件在 <code>someTopic</code> topic 上创建一个监听器端点：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Component</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyBean</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@KafkaListener</span><span class="token punctuation">(</span>topics <span class="token operator">=</span> <span class="token string">"someTopic"</span><span class="token punctuation">)</span>
    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">processMessage</span><span class="token punctuation">(</span><span class="token class-name">String</span> content<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment">// ...</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>如果定义了 <code>KafkaTransactionManager</code> bean，它将自动关联到容器 factory。同样，如果定义了 <code>RecordMessageConverter</code>、<code>ErrorHandler</code> 或 <code>AfterRollbackProcessor</code> bean，它将自动关联到默认的 factory。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>自定义 <code>ChainedKafkaTransactionManager</code> 必须标记为 <code>@Primary</code>，因为它通常引用自动配置的 <code>KafkaTransactionManager</code> bean。</p>
</blockquote>
<p><a id="boot-features-kafka-streams"></a></p>
<h3 id="3333、kafka-stream">33.3.3、Kafka Stream</h3>
<p>Spring for Apache Kafka 提供了一个工厂 bean 来创建 <code>StreamsBuilder</code> 对象并管理其 stream（流）的生命周期。只要 <code>kafka-streams</code> 在 classpath 上并且通过 <code>@EnableKafkaStreams</code> 注解启用了 Kafka Stream，Spring Boot 就会自动配置所需的 <code>KafkaStreamsConfiguration</code> bean。</p>
<p>启用 Kafka Stream 意味着必须设置应用程序 id 和引导服务器（bootstrap server）。可以使用 <code>spring.kafka.streams.application-id</code> 配置前者，如果未设置则默认为 <code>spring.application.name</code>。后者可以全局设置或专门为 stream 而重写。</p>
<p>使用专用 properties 可以设置多个其他属性，可以使用 <code>spring.kafka.streams.properties</code> 命名空间设置其他任意 Kafka 属性。有关更多信息，另请参见<a href="#boot-features-kafka-extra-props">第 33.3.4 节：其他 Kafka 属性</a>。</p>
<p>要使用 factory bean，只需将 <code>StreamsBuilder</code> 装配到您的 <code>@Bean</code> 中，如下所示：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Configuration</span>
<span class="token annotation punctuation">@EnableKafkaStreams</span>
<span class="token keyword">static</span> <span class="token keyword">class</span> <span class="token class-name">KafkaStreamsExampleConfiguration</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@Bean</span>
    <span class="token keyword">public</span> <span class="token class-name">KStream</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">Integer</span><span class="token punctuation">,</span> <span class="token class-name">String</span><span class="token punctuation">&gt;</span></span> <span class="token function">kStream</span><span class="token punctuation">(</span><span class="token class-name">StreamsBuilder</span> streamsBuilder<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token class-name">KStream</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">Integer</span><span class="token punctuation">,</span> <span class="token class-name">String</span><span class="token punctuation">&gt;</span></span> stream <span class="token operator">=</span> streamsBuilder<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token string">"ks1In"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        stream<span class="token punctuation">.</span><span class="token function">map</span><span class="token punctuation">(</span><span class="token punctuation">(</span>k<span class="token punctuation">,</span> v<span class="token punctuation">)</span> <span class="token operator">-&gt;</span> <span class="token keyword">new</span> <span class="token class-name">KeyValue</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token punctuation">&gt;</span></span><span class="token punctuation">(</span>k<span class="token punctuation">,</span> v<span class="token punctuation">.</span><span class="token function">toUpperCase</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token keyword">to</span><span class="token punctuation">(</span><span class="token string">"ks1Out"</span><span class="token punctuation">,</span>
                <span class="token class-name">Produced</span><span class="token punctuation">.</span><span class="token keyword">with</span><span class="token punctuation">(</span><span class="token class-name">Serdes</span><span class="token punctuation">.</span><span class="token class-name">Integer</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token keyword">new</span> <span class="token class-name">JsonSerde</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token punctuation">&gt;</span></span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">return</span> stream<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>默认情况下，由其创建的 <code>StreamBuilder</code> 对象管理的流会自动启动。您可以使用 <code>spring.kafka.streams.auto-startup</code> 属性自定义此行为。</p>
<p><a id="boot-features-kafka-extra-props"></a></p>
<h3 id="3334、其他-kafka-属性">33.3.4、其他 Kafka 属性</h3>
<p>自动配置支持的属性可在<a href="#common-application-properties">附录 A、常见应用程序属性</a>中找到。请注意，在大多数情况下，这些属性（连接符或驼峰命名）直接映射到 Apache Kafka 点连形式属性。有关详细信息，请参阅 Apache Kafka 文档。</p>
<p>这些属性中的前几个适用于所有组件（生产者【producer】、使用者【consumer】、管理者【admin】和流【stream】），但如果您希望使用不同的值，则可以在组件级别指定。Apache Kafka 重要性（优先级）属性设定为 HIGH、MEDIUM 或 LOW。Spring Boot 自动配置支持所有 HIGH 重要性属性，一些选择的 MEDIUM 和 LOW 属性，以及所有没有默认值的属性。</p>
<p>只有 Kafka 支持的属性的子集可以直接通过 <code>KafkaProperties</code> 类获得。如果您希望使用不受支持的其他属性配置生产者或消费者，请使用以下属性：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.kafka.properties.prop.one</span><span class="token attr-value"><span class="token punctuation">=</span>first</span>
<span class="token constant">spring.kafka.admin.properties.prop.two</span><span class="token attr-value"><span class="token punctuation">=</span>second</span>
<span class="token constant">spring.kafka.consumer.properties.prop.three</span><span class="token attr-value"><span class="token punctuation">=</span>third</span>
<span class="token constant">spring.kafka.producer.properties.prop.four</span><span class="token attr-value"><span class="token punctuation">=</span>fourth</span>
<span class="token constant">spring.kafka.streams.properties.prop.five</span><span class="token attr-value"><span class="token punctuation">=</span>fifth</span>
</code></pre>
<p>这将常见的 <code>prop.one</code> Kafka 属性设置为 <code>first</code>（适用于生产者、消费者和管理者），<code>prop.two</code> 管理者属性为 <code>second</code>，<code>prop.three</code> 消费者属性为 <code>third</code>，<code>prop.four</code> 生产者属性为 <code>fourth</code>，<code>prop.five</code> 流属性为 <code>fifth</code>。</p>
<p>您还可以按如下方式配置 Spring Kafka <code>JsonDeserializer</code>：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.kafka.consumer.value-deserializer</span><span class="token attr-value"><span class="token punctuation">=</span>org.springframework.kafka.support.serializer.JsonDeserializer</span>
<span class="token constant">spring.kafka.consumer.properties.spring.json.value.default.type</span><span class="token attr-value"><span class="token punctuation">=</span>com.example.Invoice</span>
<span class="token constant">spring.kafka.consumer.properties.spring.json.trusted.packages</span><span class="token attr-value"><span class="token punctuation">=</span>com.example,org.acme</span>
</code></pre>
<p>同样，您可以禁用 <code>JsonSerializer</code> 在 header 中发送类型信息的默认行为：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.kafka.producer.value-serializer</span><span class="token attr-value"><span class="token punctuation">=</span>org.springframework.kafka.support.serializer.JsonSerializer</span>
<span class="token constant">spring.kafka.producer.properties.spring.json.add.type.headers</span><span class="token attr-value"><span class="token punctuation">=</span>false</span>
</code></pre>
<p><strong>重要</strong></p>
<blockquote>
<p>以这种方式设置的属性将覆盖 Spring Boot 明确支持的任何配置项。</p>
</blockquote>
<p><a id="boot-features-resttemplate"></a></p>
<h2 id="34、使用-resttemplate-调用-rest-服务">34、使用 <code>RestTemplate</code> 调用 REST 服务</h2>
<p>如果您的应用程序需要调用远程 REST 服务，这可以使用 Spring Framework 的 <a href="https://docs.spring.io/spring/docs/5.1.3.RELEASE/javadoc-api/org/springframework/web/client/RestTemplate.html" target="_blank"><code>RestTemplate</code></a> 类。由于 <code>RestTemplate</code> 实例在使用之前通常需要进行自定义，因此 Spring Boot 不提供任何自动配置的 <code>RestTemplate</code> bean。但是，它会自动配置 <code>RestTemplateBuilder</code>，可在需要时创建 <code>RestTemplate</code> 实例。自动配置的 <code>RestTemplateBuilder</code> 确保将合适的 <code>HttpMessageConverters</code> 应用于 <code>RestTemplate</code> 实例。</p>
<p>以下代码展示了一个典型示例：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Service</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyService</span> <span class="token punctuation">{</span>

    <span class="token keyword">private</span> <span class="token keyword">final</span> <span class="token class-name">RestTemplate</span> restTemplate<span class="token punctuation">;</span>

    <span class="token keyword">public</span> <span class="token class-name">MyService</span><span class="token punctuation">(</span><span class="token class-name">RestTemplateBuilder</span> restTemplateBuilder<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>restTemplate <span class="token operator">=</span> restTemplateBuilder<span class="token punctuation">.</span><span class="token function">build</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token class-name">Details</span> <span class="token function">someRestCall</span><span class="token punctuation">(</span><span class="token class-name">String</span> name<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> <span class="token keyword">this</span><span class="token punctuation">.</span>restTemplate<span class="token punctuation">.</span><span class="token function">getForObject</span><span class="token punctuation">(</span><span class="token string">"/{name}/details"</span><span class="token punctuation">,</span> <span class="token class-name">Details</span><span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">,</span> name<span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p><strong>提示</strong></p>
<blockquote>
<p><code>RestTemplateBuilder</code> 包含许多可用于快速配置 ·RestTemplate· 的方法。例如，要添加 BASIC auth 支持，可以使用 <code>builder.basicAuthentication("user", "password").build()</code>。</p>
</blockquote>
<p><a id="boot-features-resttemplate-customization"></a></p>
<h3 id="341、自定义-resttemplate">34.1、自定义 RestTemplate</h3>
<p><code>RestTemplate</code> 自定义有三种主要方法，具体取决于您希望自定义的程度。</p>
<p>要想自定义的范围尽可能地窄，请注入自动配置的 <code>RestTemplateBuilder</code>，然后根据需要调用其方法。每个方法调用都返回一个新的 <code>RestTemplateBuilder</code> 实例，因此自定义只会影响当前构建器。</p>
<p>要在应用程序范围内添加自定义配置，请使用 <code>RestTemplateCustomizer</code> bean。所有这些 bean 都会自动注册到自动配置的 <code>RestTemplateBuilder</code>，并应用于使用它构建的所有模板。</p>
<p>以下示例展示了一个 customizer，它为除 <code>192.168.0.5</code> 之外的所有主机配置代理：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">static</span> <span class="token keyword">class</span> <span class="token class-name">ProxyCustomizer</span> <span class="token keyword">implements</span> <span class="token class-name">RestTemplateCustomizer</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@Override</span>
    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">customize</span><span class="token punctuation">(</span><span class="token class-name">RestTemplate</span> restTemplate<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token class-name">HttpHost</span> proxy <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">HttpHost</span><span class="token punctuation">(</span><span class="token string">"proxy.example.com"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token class-name">HttpClient</span> httpClient <span class="token operator">=</span> <span class="token class-name">HttpClientBuilder</span><span class="token punctuation">.</span><span class="token function">create</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
                <span class="token punctuation">.</span><span class="token function">setRoutePlanner</span><span class="token punctuation">(</span><span class="token keyword">new</span> <span class="token class-name">DefaultProxyRoutePlanner</span><span class="token punctuation">(</span>proxy<span class="token punctuation">)</span> <span class="token punctuation">{</span>

                    <span class="token annotation punctuation">@Override</span>
                    <span class="token keyword">public</span> <span class="token class-name">HttpHost</span> <span class="token function">determineProxy</span><span class="token punctuation">(</span><span class="token class-name">HttpHost</span> target<span class="token punctuation">,</span>
                            <span class="token class-name">HttpRequest</span> request<span class="token punctuation">,</span> <span class="token class-name">HttpContext</span> context<span class="token punctuation">)</span>
                            <span class="token keyword">throws</span> <span class="token class-name">HttpException</span> <span class="token punctuation">{</span>
                        <span class="token keyword">if</span> <span class="token punctuation">(</span>target<span class="token punctuation">.</span><span class="token function">getHostName</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">equals</span><span class="token punctuation">(</span><span class="token string">"192.168.0.5"</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
                            <span class="token keyword">return</span> <span class="token keyword">null</span><span class="token punctuation">;</span>
                        <span class="token punctuation">}</span>
                        <span class="token keyword">return</span> <span class="token keyword">super</span><span class="token punctuation">.</span><span class="token function">determineProxy</span><span class="token punctuation">(</span>target<span class="token punctuation">,</span> request<span class="token punctuation">,</span> context<span class="token punctuation">)</span><span class="token punctuation">;</span>
                    <span class="token punctuation">}</span>

                <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">build</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        restTemplate<span class="token punctuation">.</span><span class="token function">setRequestFactory</span><span class="token punctuation">(</span>
                <span class="token keyword">new</span> <span class="token class-name">HttpComponentsClientHttpRequestFactory</span><span class="token punctuation">(</span>httpClient<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>最后，最极端（也很少使用）的选择是创建自己的 <code>RestTemplateBuilder</code> bean。这样做会关闭 <code>RestTemplateBuilder</code> 的自动配置，并阻止使用任何 <code>RestTemplateCustomizer</code> bean。</p>
<p><a id="boot-features-webclient"></a></p>
<h2 id="35、使用-webclient-调用-rest-服务">35、使用 <code>WebClient</code> 调用 REST 服务</h2>
<p>如果在 classpath 上存在 Spring WebFlux，则还可以选择使用 <code>WebClient</code> 来调用远程 REST 服务。与 <code>RestTemplate</code> 相比，该客户端更具函数式风格并且完全响应式。您可以在 <a href="https://docs.spring.io/spring/docs/5.1.3.RELEASE/spring-framework-reference/web-reactive.html#webflux-client" target="_blank">Spring Framework 文档的相关部分</a>中了解有关 <code>WebClient</code> 的更多信息。</p>
<p>Spring Boot 为您创建并预配置了一个 <code>WebClient.Builder</code>。强烈建议将其注入您的组件中并使用它来创建 <code>WebClient</code> 实例。Spring Boot 配置该构建器以共享 HTTP 资源，以与服务器相同的方式反射编解码器设置（请参阅 <a href="#boot-features-webflux-httpcodecs">WebFlux HTTP 编解码器自动配置</a>）等。</p>
<p>以下代码是一个典型示例：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Service</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyService</span> <span class="token punctuation">{</span>

    <span class="token keyword">private</span> <span class="token keyword">final</span> <span class="token class-name">WebClient</span> webClient<span class="token punctuation">;</span>

    <span class="token keyword">public</span> <span class="token class-name">MyService</span><span class="token punctuation">(</span><span class="token class-name">WebClient</span><span class="token punctuation">.</span><span class="token class-name">Builder</span> webClientBuilder<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>webClient <span class="token operator">=</span> webClientBuilder<span class="token punctuation">.</span><span class="token function">baseUrl</span><span class="token punctuation">(</span><span class="token string">"http://example.org"</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">build</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token class-name">Mono</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">Details</span><span class="token punctuation">&gt;</span></span> <span class="token function">someRestCall</span><span class="token punctuation">(</span><span class="token class-name">String</span> name<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> <span class="token keyword">this</span><span class="token punctuation">.</span>webClient<span class="token punctuation">.</span><span class="token function">get</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">uri</span><span class="token punctuation">(</span><span class="token string">"/{name}/details"</span><span class="token punctuation">,</span> name<span class="token punctuation">)</span>
                        <span class="token punctuation">.</span><span class="token function">retrieve</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">bodyToMono</span><span class="token punctuation">(</span><span class="token class-name">Details</span><span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p><a id="boot-features-webclient-runtime"></a></p>
<h3 id="351、webclient-运行时">35.1、WebClient 运行时</h3>
<p>Spring Boot 将自动检测用于驱动 <code>WebClient</code> 的 <code>ClientHttpConnector</code>，具体取决于应用程序 classpath 上可用的类库。目前支持 Reactor Netty 和 Jetty RS 客户端。</p>
<p>默认情况下 <code>spring-boot-starter-webflux</code> starter 依赖于 <code>io.projectreactor.netty:reactor-netty</code>，它包含了服务器和客户端的实现。如果您选择将 <code>Jetty</code> 用作响应式服务器，则应添加 Jetty Reactive HTTP 客户端库依赖项 <code>org.eclipse.jetty:jetty-reactive-httpclient</code>。服务器和客户端使用相同的技术具有一定优势，因为它会自动在客户端和服务器之间共享 HTTP 资源。</p>
<p>开发人员可以通过提供自定义的 <code>ReactorResourceFactory</code> 或 <code>JettyResourceFactory</code> bean 来覆盖 Jetty 和 Reactor Netty 的资源配置 —— 这将同时应用于客户端和服务器。</p>
<p>如果您只希望覆盖客户端选项，则可以定义自己的 <code>ClientHttpConnector</code> bean 并完全控制客户端配置。</p>
<p>您可以在 <a href="https://docs.spring.io/spring/docs/5.1.3.RELEASE/spring-framework-reference/web-reactive.html#webflux-client-builder" target="_blank">Spring Framework 参考文档中了解有关 <code>WebClient</code> 配置选项的更多信息</a>。</p>
<p><a id="boot-features-webclient-customization"></a></p>
<h3 id="352、自定义-webclient">35.2、自定义 WebClient</h3>
<p><code>WebClient</code> 自定义有三种主要方法，具体取决于您希望自定义的程度。</p>
<p>要想自定义的范围尽可能地窄，请注入自动配置的 <code>WebClient.Builder</code>，然后根据需要调用其方法。<code>WebClient.Builder</code> 实例是有状态的：构建器上的任何更改都会影响到之后所有使用它创建的客户端。如果要使用相同的构建器创建多个客户端，可以考虑使用 <code>WebClient.Builder other = builder.clone();</code> 的方式克隆构建器。</p>
<p>要在应用程序范围内对所有 <code>WebClient.Builder</code> 实例添加自定义，可以声明 <code>WebClientCustomizer</code> bean 并在注入点局部更改 <code>WebClient.Builder</code>。</p>
<p>最后，您可以回退到原始 API 并使用 <code>WebClient.create()</code>。在这种情况下，不会应用自动配置或 <code>WebClientCustomizer</code>。</p>
<p><a id="boot-features-validation"></a></p>
<h2 id="36、验证">36、验证</h2>
<p>只要 classpath 上存在 JSR-303 实现（例如 Hibernate 验证器），就会自动启用 Bean Validation 1.1 支持的方法验证功能。这允许 bean 方法在其参数和/或返回值上使用 <code>javax.validation</code> 约束进行注解。带有此类注解方法的目标类需要在类级别上使用 <code>@Validated</code> 进行注解，以便搜索其内联约束注解的方法。</p>
<p>例如，以下服务触发第一个参数的验证，确保其大小在 8 到 10 之间：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Service</span>
<span class="token annotation punctuation">@Validated</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyBean</span> <span class="token punctuation">{</span>

    <span class="token keyword">public</span> <span class="token class-name">Archive</span> <span class="token function">findByCodeAndAuthor</span><span class="token punctuation">(</span><span class="token annotation punctuation">@Size</span><span class="token punctuation">(</span>min <span class="token operator">=</span> <span class="token number">8</span><span class="token punctuation">,</span> max <span class="token operator">=</span> <span class="token number">10</span><span class="token punctuation">)</span> <span class="token class-name">String</span> code<span class="token punctuation">,</span>
            <span class="token class-name">Author</span> author<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p><a id="boot-features-email"></a></p>
<h2 id="37、发送邮件">37、发送邮件</h2>
<p>Spring Framework 提供了一个使用 <code>JavaMailSender</code> 接口发送电子邮件的简单抽象，Spring Boot 为其提供了自动配置以及一个 starter 模块。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>有关如何使用 <code>JavaMailSender</code> 的详细说明，请参阅<a href="https://docs.spring.io/spring/docs/5.1.3.RELEASE/spring-framework-reference/integration.html#mail" target="_blank">参考文档</a>。</p>
</blockquote>
<p>如果 <code>spring.mail.host</code> 和相关库（由 <code>spring-boot-starter-mail</code> 定义）可用，则创建默认的 <code>JavaMailSender</code>（如果不存在）。可以通过 <code>spring.mail</code> 命名空间中的配置项进一步自定义发件人。有关更多详细信息，请参阅 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.1.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/mail/MailProperties.java" target="_blank"><code>MailProperties</code></a>。</p>
<p>特别是，某些默认超时时间的值是无限的，您可能想更改它以避免线程被无响应的邮件服务器阻塞，如下示例所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.mail.properties.mail.smtp.connectiontimeout</span><span class="token attr-value"><span class="token punctuation">=</span>5000</span>
<span class="token constant">spring.mail.properties.mail.smtp.timeout</span><span class="token attr-value"><span class="token punctuation">=</span>3000</span>
<span class="token constant">spring.mail.properties.mail.smtp.writetimeout</span><span class="token attr-value"><span class="token punctuation">=</span>5000</span>
</code></pre>
<p>也可以使用 JNDI 中的现有 <code>Session</code> 配置一个 <code>JavaMailSender</code>：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.mail.jndi-name</span><span class="token attr-value"><span class="token punctuation">=</span>mail/Session</span>
</code></pre>
<p>设置 <code>jndi-name</code> 时，它优先于所有其他与 <code>Session</code> 相关的设置。</p>
<p><a id="boot-features-jta"></a></p>
<h2 id="38、jta-分布式事务">38、JTA 分布式事务</h2>
<p>Spring Boot 通过使用 <a href="http://www.atomikos.com/" target="_blank">Atomikos</a> 或 <a href="https://github.com/bitronix/btm" target="_blank">Bitronix</a> 嵌入式事务管理器来支持跨多个 XA 资源的分布式 JTA 事务。部署在某些 Java EE 应用服务器（Application Server）上也支持 JTA 事务。</p>
<p>当检测到 JTA 环境时，Spring 的 <code>JtaTransactionManager</code> 将用于管理事务。自动配置的 JMS、DataSource 和 JPA bean 已升级为支持 XA 事务。您可以使用标准的 Spring 方式（例如 <code>@Transactional</code>）来使用分布式事务。如果您处于 JTA 环境中并且仍想使用本地事务，则可以将 <code>spring.jta.enabled</code> 属性设置为 <code>false</code> 以禁用 JTA 自动配置。</p>
<p><a id="boot-features-jta-atomikos"></a></p>
<h3 id="381、使用-atomikos-事务管理器">38.1、使用 Atomikos 事务管理器</h3>
<p><a href="https://www.atomikos.com/" target="_blank">Atomikos</a> 是一个流行的开源事务管理器，可以嵌入到 Spring Boot 应用程序中。您可以使用 <code>spring-boot-starter-jta-atomikos</code> starter 来获取相应的 Atomikos 库。Spring Boot 自动配置 Atomikos 并确保将合适的依赖设置应用于 Spring bean，以确保启动和关闭顺序正确。</p>
<p>默认情况下，Atomikos 事务日志将写入应用程序主目录（应用程序 jar 文件所在的目录）中的 <code>transaction-logs</code> 目录。您可以通过在 <code>application.properties</code> 文件中设置 <code>spring.jta.log-dir</code> 属性来自定义此目录的位置。也可用 <code>spring.jta.atomikos.properties</code> 开头的属性来自定义 Atomikos <code>UserTransactionServiceImp</code>。有关完整的详细信息，请参阅 <a href="https://docs.spring.io/spring-boot/docs/2.1.1.RELEASE/api/org/springframework/boot/jta/atomikos/AtomikosProperties.html" target="_blank">AtomikosProperties Javadoc</a>。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>为确保多个事务管理器可以安全地协调相同的资源管理器，必须为每个 Atomikos 实例配置唯一 ID。默认情况下，此 ID 是运行 Atomikos 的计算机的 IP 地址。在生产环境中要确保唯一性，应为应用程序的每个实例配置 <code>spring.jta.transaction-manager-id</code> 属性，并使用不同的值。</p>
</blockquote>
<p><a id="boot-features-jta-bitronix"></a></p>
<h3 id="382、使用-bitronix-事务管理器">38.2、使用 Bitronix 事务管理器</h3>
<p><a href="https://github.com/bitronix/btm" target="_blank">Bitronix</a> 是一个流行的开源 JTA 事务管理器实现。您可以使用 <code>spring-boot-starter-jta-bitronix</code> starter 为您的项目添加合适的 Bitronix 依赖。与 Atomikos 一样，Spring Boot 会自动配置 Bitronix 并对 bean 进行后处理（post-processes），以确保启动和关闭顺序正确。</p>
<p>默认情况下，Bitronix 事务日志文件（<code>part1.btm</code> 和 <code>part2.btm</code>）将写入应用程序主目录中的 <code>transaction-logs</code> 目录。您可以通过设置 <code>spring.jta.log-dir</code> 属性来自定义此目录的位置。以 <code>spring.jta.bitronix.properties</code> 开头的属性绑定到了 <code>bitronix.tm.Configuration</code> bean，允许完全自定义。有关详细信息，请参阅 <a href="https://github.com/bitronix/btm/wiki/Transaction-manager-configuration" target="_blank">Bitronix 文档</a>。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>为确保多个事务管理器能够安全地协调相同的资源管理器，必须为每个 Bitronix 实例配置唯一的 ID。默认情况下，此 ID 是运行 Bitronix 的计算机的 IP 地址。生产环境要确保唯一性，应为应用程序的每个实例配置 <code>spring.jta.transaction-manager-id</code> 属性，并使用不同的值。</p>
</blockquote>
<p><a id="boot-features-jta-javaee"></a></p>
<h3 id="383、使用-java-ee-管理的事务管理器">38.3、使用 Java EE 管理的事务管理器</h3>
<p>如果将 Spring Boot 应用程序打包为 <code>war</code> 或 <code>ear</code> 文件并将其部署到 Java EE 应用程序服务器，则可以使用应用程序服务器的内置事务管理器。Spring Boot 尝试通过查找常见的 JNDI 位置（<code>java:comp/UserTransaction</code>、<code>java:comp/TransactionManager</code> 等）来自动配置事务管理器。如果使用应用程序服务器提供的事务服务，通常还需要确保所有资源都由服务器管理并通过 JNDI 暴露。Spring Boot 尝试通过在 JNDI 路径（<code>java:/JmsXA</code> 或 <code>java:/JmsXA</code>）中查找 <code>ConnectionFactory</code> 来自动配置 JMS，并且可以使用 <a href="#boot-features-connecting-to-a-jndi-datasource"><code>spring.datasource.jndi-name</code> 属性</a>来配置 <code>DataSource</code>。</p>
<p><a id="boot-features-jta-mixed-jms"></a></p>
<h3 id="384、混合使用-xa-与非-xa-jms-连接">38.4、混合使用 XA 与非 XA JMS 连接</h3>
<p>使用 JTA 时，主 JMS <code>ConnectionFactory</code> bean 可识别 XA 并参与分布式事务。在某些情况下，您可能希望使用非 XA <code>ConnectionFactory</code> 处理某些 JMS 消息。例如，您的 JMS 处理逻辑可能需要比 XA 超时时间更长的时间。</p>
<p>如果要使用非 XA <code>ConnectionFactory</code>，可以注入 <code>nonXaJmsConnectionFactory</code> bean 而不是 <code>@Primary</code> <code>jmsConnectionFactory</code> bean。为了保持一致性，提供的 <code>jmsConnectionFactory</code> bean 还需要使用 <code>xaJmsConnectionFactory</code> 别名。</p>
<p>以下示例展示了如何注入 <code>ConnectionFactory</code> 实例：</p>
<pre class="language-"><code class="lang-java"><span class="token comment">// Inject the primary (XA aware) ConnectionFactory</span>
<span class="token annotation punctuation">@Autowired</span>
<span class="token keyword">private</span> <span class="token class-name">ConnectionFactory</span> defaultConnectionFactory<span class="token punctuation">;</span>

<span class="token comment">// Inject the XA aware ConnectionFactory (uses the alias and injects the same as above)</span>
<span class="token annotation punctuation">@Autowired</span>
<span class="token annotation punctuation">@Qualifier</span><span class="token punctuation">(</span><span class="token string">"xaJmsConnectionFactory"</span><span class="token punctuation">)</span>
<span class="token keyword">private</span> <span class="token class-name">ConnectionFactory</span> xaConnectionFactory<span class="token punctuation">;</span>

<span class="token comment">// Inject the non-XA aware ConnectionFactory</span>
<span class="token annotation punctuation">@Autowired</span>
<span class="token annotation punctuation">@Qualifier</span><span class="token punctuation">(</span><span class="token string">"nonXaJmsConnectionFactory"</span><span class="token punctuation">)</span>
<span class="token keyword">private</span> <span class="token class-name">ConnectionFactory</span> nonXaConnectionFactory<span class="token punctuation">;</span>
</code></pre>
<p><a id="boot-features-jta-supporting-alternative-embedded"></a></p>
<h3 id="385、支持嵌入式事务管理器">38.5、支持嵌入式事务管理器</h3>
<p><a href="https://github.com/spring-projects/spring-boot/tree/v2.1.1.RELEASE/spring-boot-project/spring-boot/src/main/java/org/springframework/boot/jms/XAConnectionFactoryWrapper.java" target="_blank"><code>XAConnectionFactoryWrapper</code></a> 和 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.1.RELEASE/spring-boot-project/spring-boot/src/main/java/org/springframework/boot/jdbc/XADataSourceWrapper.java" target="_blank"><code>XADataSourceWrapper</code></a> 接口可用于支持其他嵌入式事务管理器。接口负责包装 <code>XAConnectionFactory</code> 和 <code>XADataSource</code> bean，并将它们公开为普通的 <code>ConnectionFactory</code> 和 <code>DataSource</code> bean，它们透明地加入分布式事务。<code>DataSource</code> 和 JMS 自动配置使用 JTA 变体，前提是您需要有一个 <code>JtaTransactionManager</code> bean 和在 <code>ApplicationContext</code> 中注册有的相应 XA 包装器（wrapper） bean。</p>
<p><a href="https://github.com/spring-projects/spring-boot/tree/v2.1.1.RELEASE/spring-boot-project/spring-boot/src/main/java/org/springframework/boot/jta/bitronix/BitronixXAConnectionFactoryWrapper.java" target="_blank">BitronixXAConnectionFactoryWrapper</a> 和 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.1.RELEASE/spring-boot-project/spring-boot/src/main/java/org/springframework/boot/jta/bitronix/BitronixXADataSourceWrapper.java" target="_blank">BitronixXADataSourceWrapper</a> 为如何编写 XA 包装器提供了很好示例。</p>
<p><a id="boot-features-hazelcast"></a></p>
<h2 id="39、hazelcast">39、Hazelcast</h2>
<p>如果 <a href="https://hazelcast.com/" target="_blank">Hazelcast</a> 在 classpath 上并有合适的配置，则 Spring Boot 会自动配置一个可以在应用程序中注入的 <code>HazelcastInstance</code>。</p>
<p>如果定义了 <code>com.hazelcast.config.Config</code> bean，则 Spring Boot 会使用它。如果您的配置定义了实例名称，Spring Boot 会尝试查找现有的实例，而不是创建新实例。</p>
<p>您还可以通过配置指定要使用的 <code>hazelcast.xml</code> 配置文件，如下所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.hazelcast.config</span><span class="token attr-value"><span class="token punctuation">=</span>classpath:config/my-hazelcast.xml</span>
</code></pre>
<p>否则，Spring Boot 会尝试从默认位置查找 Hazelcast 配置：工作目录或 classpath 根目录中的 <code>hazelcast.xml</code> 。我们还检查是否设置了 <code>hazelcast.config</code> 系统属性。有关更多详细信息，请参阅 <a href="http://docs.hazelcast.org/docs/latest/manual/html-single/" target="_blank">Hazelcast 文档</a>。</p>
<p>如果 classpath 中存在 <code>hazelcast-client</code>，则 Spring Boot 会首先尝试通过检查以下配置项来创建客户端：</p>
<ul>
<li>存在 <code>com.hazelcast.client.config.ClientConfig</code> bean。</li>
<li><code>spring.hazelcast.config</code> 属性定义的配置文件。</li>
<li>存在 <code>hazelcast.client.config</code> 系统属性。</li>
<li>工作目录中或 classpath 根目录下的 <code>hazelcast-client.xml</code>。</li>
</ul>
<p><strong>注意</strong></p>
<blockquote>
<p>Spring Boot 还为 Hazelcast 提供了<a href="#boot-features-caching-provider-hazelcast">缓存支持</a>。如果启用了缓存，<code>HazelcastInstance</code> 将自动包装在 <code>CacheManager</code> 实现中。</p>
</blockquote>
<p><a id="boot-features-quartz"></a></p>
<h2 id="40、quartz-调度器">40、Quartz 调度器</h2>
<p>Spring Boot 提供了几种使用 <a href="http://www.quartz-scheduler.org/" target="_blank">Quartz 调度器</a>的便捷方式，它们来自 <code>spring-boot-starter-quartz</code> starter。如果 Quartz 可用，则 Spring Boot 将自动配置 <code>Scheduler</code>（通过 <code>SchedulerFactoryBean</code> 抽象）。</p>
<p>自动选取以下类型的 Bean 并将其与 <code>Scheduler</code> 关联起来：</p>
<ul>
<li><code>JobDetail</code>：定义一个特定的 job。可以使用 <code>JobBuilder</code> API 构建 <code>JobDetail</code> 实例。</li>
<li><code>Calendar</code>。</li>
<li><code>Trigger</code>：定义何时触发 job。</li>
</ul>
<p>默认使用内存存储方式的 <code>JobStore</code>。 但如果应用程序中有 <code>DataSource</code> bean，并且配置了 <code>spring.quartz.job-store-type</code> 属性，则可以配置基于 JDBC 的存储，如下所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.quartz.job-store-type</span><span class="token attr-value"><span class="token punctuation">=</span>jdbc</span>
</code></pre>
<p>使用 JDBC 存储时，可以在启动时初始化 schema（表结构），如下所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.quartz.jdbc.initialize-schema</span><span class="token attr-value"><span class="token punctuation">=</span>always</span>
</code></pre>
<p><strong>警告</strong></p>
<blockquote>
<p>默认将使用 Quartz 库提供的标准脚本检测并初始化数据库。这些脚本会删除现有表，在每次重启时删除所有触发器。可以通过设置 <code>spring.quartz.jdbc.schema</code> 属性来提供自定义脚本。</p>
</blockquote>
<p>要让 Quartz 使用除应用程序主 <code>DataSource</code> 之外的 <code>DataSource</code>，请声明一个 <code>DataSource</code> bean，使用 <code>@QuartzDataSource</code> 注解其 <code>@Bean</code> 方法。这样做可确保 <code>SchedulerFactoryBean</code> 和 schema 初始化都使用 Quartz 指定的 <code>DataSource</code>。</p>
<p>默认情况下，配置创建的 job 不会覆盖已从持久 job 存储读取的已注册的 job。要启用覆盖现有的 job 定义，请设置 <code>spring.quartz.overwrite-existing-jobs</code> 属性。</p>
<p>Quartz 调取器配置可以使用 <code>spring.quartz</code> 属性和 <code>SchedulerFactoryBeanCustomizer</code> bean 进行自定义，它们允许以编程方式的 SchedulerFactoryBean 自定义。可以使用 <code>spring.quartz.properties.*</code> 自定义高级 Quartz 配置属性。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>需要强调的是，<code>Executor</code> bean 与调度程序没有关联，因为 Quartz 提供了通过 <code>spring.quartz.properties</code> 配置调度器的方法。如果需要自定义执行器，请考虑实现 <code>SchedulerFactoryBeanCustomizer</code>。</p>
</blockquote>
<p>job 可以定义 <code>setter</code> 以注入数据映射属性。也可以以类似的方式注入常规的 bean，如下所示：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">SampleJob</span> <span class="token keyword">extends</span> <span class="token class-name">QuartzJobBean</span> <span class="token punctuation">{</span>

    <span class="token keyword">private</span> <span class="token class-name">MyService</span> myService<span class="token punctuation">;</span>

    <span class="token keyword">private</span> <span class="token class-name">String</span> name<span class="token punctuation">;</span>

    <span class="token comment">// Inject "MyService" bean</span>
    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">setMyService</span><span class="token punctuation">(</span><span class="token class-name">MyService</span> myService<span class="token punctuation">)</span> <span class="token punctuation">{</span> <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span> <span class="token punctuation">}</span>

    <span class="token comment">// Inject the "name" job data property</span>
    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">setName</span><span class="token punctuation">(</span><span class="token class-name">String</span> name<span class="token punctuation">)</span> <span class="token punctuation">{</span> <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span> <span class="token punctuation">}</span>

    <span class="token annotation punctuation">@Override</span>
    <span class="token keyword">protected</span> <span class="token keyword">void</span> <span class="token function">executeInternal</span><span class="token punctuation">(</span><span class="token class-name">JobExecutionContext</span> context<span class="token punctuation">)</span>
            <span class="token keyword">throws</span> <span class="token class-name">JobExecutionException</span> <span class="token punctuation">{</span>
        <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p><a id="boot-features-task-execution-scheduling"></a></p>
<h2 id="41、任务执行与调度">41、任务执行与调度</h2>
<p>在上下文中没有 <code>Executor</code> bean 的情况下，Spring Boot 会自动配置一个有合理默认值的 <code>ThreadPoolTask​​Executor</code>，它可以自动与异步任务执行（<code>@EnableAsync</code>）和 Spring MVC 异步请求处理相关联。</p>
<p><strong>提示</strong></p>
<blockquote>

如果您在上下文中定义了自定义 `Executor`，则常规任务执行（即 `@EnableAsync`）将透明地使用它，但不会配置 Spring MVC 支持，因为它需要 `AsyncTaskExecutor` 实现（名为 `applicationTaskExecutor`）。根据您的目标安排，您可以将 `Executor` 更改为 `ThreadPoolTask​​Executor`，或者定义 `Executor的ThreadPoolTask​​Executor` 和 `AsyncConfigurer` 来包装自定义的 `Executor`。

您可以使用自动配置的 `TaskExecutorBuilder` 来轻松创建实例，以复制默认的自动配置。

</blockquote>

<p>线程池使用 8 个核心线程，可根据负载情况增加和减少。可以使用 <code>spring.task.execution</code> 命名空间对这些默认设置进行微调，如下所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.task.execution.pool.max-threads</span><span class="token attr-value"><span class="token punctuation">=</span>16</span>
<span class="token constant">spring.task.execution.pool.queue-capacity</span><span class="token attr-value"><span class="token punctuation">=</span>100</span>
<span class="token constant">spring.task.execution.pool.keep-alive</span><span class="token attr-value"><span class="token punctuation">=</span>10s</span>
</code></pre>
<p>这会将线程池更改为使用有界队列，在队列满（100 个任务）时，线程池将增加到最多 16 个线程。当线程在闲置10 秒（而不是默认的 60 秒）时回收线程，池的收缩更为明显。</p>
<p>如果需要与调度任务执行（<code>@EnableScheduling</code>）相关联，可以自动配置一个 <code>ThreadPoolTaskScheduler</code>。默认情况下，线程池使用一个线程，可以使用 <code>spring.task.scheduling</code> 命名空间对这些设置进行微调。</p>
<p>如果需要创建自定义执行器或调度器，则在上下文中可以使用 <code>TaskExecutorBuilder</code> bean 和 <code>TaskSchedulerBuilder</code> bean。</p>
<p><a id="boot-features-integration"></a></p>
<h2 id="42、spring-integration">42、Spring Integration</h2>
<p>Spring Boot 为 <a href="https://projects.spring.io/spring-integration/" target="_blank">Spring Integration</a> 提供了一些便捷的使用方式，它们包含在 <code>spring-boot-starter-integration</code> starter 中。Spring Integration 为消息传递以及其他传输（如 HTTP、TCP 等）提供了抽象。如果 classpath 上存在 Spring Integration，则 Spring Boot 会通过 <code>@EnableIntegration</code> 注解对其进行初始化。</p>
<p>Spring Boot 还配置了一些由其他 Spring Integration 模块触发的功能。如果 <code>spring-integration-jmx</code> 也在 classpath 上，则消息处理统计信息将通过 JMX 发布。如果 <code>spring-integration-jdbc</code> 可用，则可以在启动时创建默认数据库模式，如下所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.integration.jdbc.initialize-schema</span><span class="token attr-value"><span class="token punctuation">=</span>always</span>
</code></pre>
<p>有关更多详细信息，请参阅 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.2.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/integration/IntegrationAutoConfiguration.java" target="_blank">IntegrationAutoConfiguration</a> 和 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.2.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/integration/IntegrationProperties.java" target="_blank">IntegrationProperties</a> 类。</p>
<p>默认情况下，如果存在 Micrometer <code>meterRegistry</code> bean，则 Micrometer 将管理 Spring Integration 的指标。如果您希望使用旧版 Spring Integration 度量，请将 <code>DefaultMetricsFactory</code> bean 添加到应用程序上下文中。</p>
<p><a id="boot-features-session"></a></p>
<h2 id="43、spring-session">43、Spring Session</h2>
<p>Spring Boot 为各种数据存储提供 <a href="https://projects.spring.io/spring-session/" target="_blank">Spring Session</a> 自动配置。在构建 Servlet Web 应用程序时，可以自动配置以下存储：</p>
<ul>
<li>JDBC</li>
<li>Redis</li>
<li>Hazelcast</li>
<li>MongoDB</li>
</ul>
<p>构建响应式 Web 应用程序时，可以自动配置以下存储：</p>
<ul>
<li>Redis</li>
<li>MongoDB</li>
</ul>
<p>如果 classpath 上存在单个 Spring Session 模块，则 Spring Boot 会自动使用该存储实现。如果您有多个实现，则必须选择要用于存储会话的 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.2.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/session/StoreType.java" target="_blank"><code>StoreType</code></a>。 例如，要使用 JDBC 作为后端存储，您可以按如下方式配置应用程序：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.session.store-type</span><span class="token attr-value"><span class="token punctuation">=</span>jdbc</span>
</code></pre>
<p><strong>提示</strong></p>
<blockquote>
<p>可以将 <code>store-type</code> 设置为 <code>none</code> 来禁用 Spring Session。</p>
</blockquote>
<p>每个 store 都有自己的额外设置。例如，可以为 JDBC 存储定制表的名称，如下所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.session.jdbc.table-name</span><span class="token attr-value"><span class="token punctuation">=</span>SESSIONS</span>
</code></pre>
<p>可以使用 <code>spring.session.timeout</code> 属性来设置会话的超时时间。如果未设置该属性，则自动配置将使用 <code>server.servlet.session.timeout</code> 的值。</p>
<p><a id="boot-features-jmx"></a></p>
<h2 id="44、通过-jmx-监控和管理">44、通过 JMX 监控和管理</h2>
<p>Java Management Extensions（JMX，Java 管理扩展）提供了一种监视和管理应用程序的标准机制。默认情况下，Spring Boot 会创建一个 ID 为 <code>mbeanServer</code> 的 <code>MBeanServer</code> bean，并暴露使用 Spring JMX 注解（<code>@ManagedResource</code>、<code>@ManagedAttribute</code> 或 <code>@ManagedOperation</code>）的 bean。</p>
<p>有关更多详细信息，请参阅 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.2.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/jmx/JmxAutoConfiguration.java" target="_blank"><code>JmxAutoConfiguration</code></a> 类。</p>
<p><a id="boot-features-testing"></a></p>
<h2 id="45、测试">45、测试</h2>
<p><a id="boot-features-websockets"></a></p>
<h2 id="46、websocket">46、WebSocket</h2>
<p>Spring Boot 为内嵌式 Tomcat、Jetty 和 Undertow 提供了 WebSocket 自动配置。如果将 war 文件部署到独立容器，则 Spring Boot 假定容器负责配置其 WebSocket 支持。</p>
<p>Spring Framework 为 MVC Web 应用程序提供了<a href="https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/web.html#websocket" target="_blank">丰富的 WebSocket 支持</a>，可以通过 <code>spring-boot-starter-websocket</code> 模块轻松访问。</p>
<p>WebSocket 支持也可用于<a href="https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/web-reactive.html#webflux-websocket" target="_blank">响应式 Web 应用程序</a>，并且引入 WebSocket API 以及 <code>spring-boot-starter-webflux</code>：</p>
<pre class="language-"><code class="lang-xml"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependency</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>groupId</span><span class="token punctuation">&gt;</span></span>javax.websocket<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>groupId</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>artifactId</span><span class="token punctuation">&gt;</span></span>javax.websocket-api<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>artifactId</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependency</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<p><a id="boot-features-webservices"></a></p>
<h2 id="47、web-service">47、Web Service</h2>
<p>Spring Boot 提供 Web Service 自动配置，因此您要做的就是定义 <code>Endpoints</code>。</p>
<p>可以使用 <code>spring-boot-starter-webservices</code> 模块轻松访问 <a href="https://docs.spring.io/spring-ws/docs/3.0.6.RELEASE/reference/" target="_blank">Spring Web Service 功能</a>。</p>
<p>可以分别为 WSDL 和 XSD 自动创建 <code>SimpleWsdl11Definition</code> 和 <code>SimpleXsdSchema</code> bean。为此，请配置其位置，如下所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.webservices.wsdl-locations</span><span class="token attr-value"><span class="token punctuation">=</span>classpath:/wsdl</span>
</code></pre>
<p><a id="boot-features-webservices-template"></a></p>
<h3 id="471、使用-webservicetemplate-调用-web-service">47.1、使用 <code>WebServiceTemplate</code> 调用 Web Service</h3>
<p>如果您需要从应用程序调用远程 Web 服务，则可以使用 <code>WebServiceTemplate</code> 类。由于 <code>WebServiceTemplate</code> 实例在使用之前通常需要进行自定义，因此 Spring Boot 不提供任何自动配置的 <code>WebServiceTemplate</code> bean。但是，它会自动配置 <code>WebServiceTemplateBuilder</code>，可在需要创建 <code>WebServiceTemplate</code> 实例时使用。</p>
<p>以下代码为一个典型示例：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Service</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyService</span> <span class="token punctuation">{</span>

    <span class="token keyword">private</span> <span class="token keyword">final</span> <span class="token class-name">WebServiceTemplate</span> webServiceTemplate<span class="token punctuation">;</span>

    <span class="token keyword">public</span> <span class="token class-name">MyService</span><span class="token punctuation">(</span><span class="token class-name">WebServiceTemplateBuilder</span> webServiceTemplateBuilder<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>webServiceTemplate <span class="token operator">=</span> webServiceTemplateBuilder<span class="token punctuation">.</span><span class="token function">build</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token class-name">DetailsResp</span> <span class="token function">someWsCall</span><span class="token punctuation">(</span><span class="token class-name">DetailsReq</span> detailsReq<span class="token punctuation">)</span> <span class="token punctuation">{</span>
         <span class="token keyword">return</span> <span class="token punctuation">(</span><span class="token class-name">DetailsResp</span><span class="token punctuation">)</span> <span class="token keyword">this</span><span class="token punctuation">.</span>webServiceTemplate<span class="token punctuation">.</span><span class="token function">marshalSendAndReceive</span><span class="token punctuation">(</span>detailsReq<span class="token punctuation">,</span> <span class="token keyword">new</span> <span class="token class-name">SoapActionCallback</span><span class="token punctuation">(</span>ACTION<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>默认情况下，<code>WebServiceTemplateBuilder</code> 使用 classpath 上的可用 HTTP 客户端库检测合适的基于 HTTP 的 <code>WebServiceMessageSender</code>。您还可以按如下方式自定义读取和连接的超时时间：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Bean</span>
<span class="token keyword">public</span> <span class="token class-name">WebServiceTemplate</span> <span class="token function">webServiceTemplate</span><span class="token punctuation">(</span><span class="token class-name">WebServiceTemplateBuilder</span> builder<span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">return</span> builder<span class="token punctuation">.</span><span class="token function">messageSenders</span><span class="token punctuation">(</span><span class="token keyword">new</span> <span class="token class-name">HttpWebServiceMessageSenderBuilder</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
            <span class="token punctuation">.</span><span class="token function">setConnectTimeout</span><span class="token punctuation">(</span><span class="token number">5000</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">setReadTimeout</span><span class="token punctuation">(</span><span class="token number">2000</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">build</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">build</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>
<p><a id="boot-features-developing-auto-configuration"></a></p>
<h2 id="49、创建自己的自动配置">49、创建自己的自动配置</h2>
<p>如果您在公司负责开发公共类库，或者如果您在开发一个开源或商业库，您可能希望开发自己的自动配置。自动配置类可以捆绑在外部 jar 中，他仍然可以被 Spring Boot 获取。</p>
<p>自动配置可以与提供自动配置代码的 starter 以及您将使用的类库库相关联。我们首先介绍构建自己的自动配置需要了解的内容，然后我们将继续介绍<a href="#boot-features-custom-starter">创建自定义 starter 所需的步骤</a>。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>这里有一个<a href="https://github.com/snicoll-demos/spring-boot-master-auto-configuration" target="_blank">演示项目</a>展示了如何逐步创建 starter。</p>
</blockquote>
<p><a id="boot-features-understanding-auto-configured-beans"></a></p>
<h3 id="491、理解自定配置-bean">49.1、理解自定配置 Bean</h3>
<p>在内部，自动配置使用了标准的 <code>@Configuration</code> 类来实现。<code>@Conditional</code> 注解用于约束何时应用自动配置。通常，自动配置类使用 <code>@ConditionalOnClass</code> 和 <code>@ConditionalOnMissingBean</code> 注解。这可确保仅在找到相关类时以及未声明您自己的 <code>@Configuration</code> 时才应用自动配置。</p>
<p>您可以浏览 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure" target="_blank"><code>spring-boot-autoconfigure</code></a> 的源代码，以查看 Spring 提供的 <code>@Configuration</code> 类（请参阅 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/resources/META-INF/spring.factories" target="_blank"><code>META-INF/spring.factories</code></a> 文件）。</p>
<p><a id="boot-features-locating-auto-configuration-candidates"></a></p>
<h3 id="492、找到候选的自动配置">49.2、找到候选的自动配置</h3>
<p>Spring Boot 会检查已发布 jar 中是否存在 <code>META-INF/spring.factories</code> 文件。该文件应列出 <code>EnableAutoConfiguration</code> key 下的配置类，如下所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">org.springframework.boot.autoconfigure.EnableAutoConfiguration</span><span class="token attr-value"><span class="token punctuation">=</span>\</span>
com.mycorp.libx.autoconfigure.LibXAutoConfiguration,\
com.mycorp.libx.autoconfigure.LibXWebAutoConfiguration
</code></pre>
<p><strong>注意</strong></p>
<blockquote>
<p><strong>必须</strong>以这种方式加载自动配置。确保它们在特定的包空间中定义，并且它们不能是组件扫描的目标。此外，自动配置类不应启用组件扫描以查找其他组件。应该使用特定的<code>@Imports</code> 来代替。</p>
</blockquote>
<p>如果需要按特定顺序应用配置，则可以使用 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/AutoConfigureAfter.java" target="_blank"><code>@AutoConfigureAfter</code></a> 或 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/AutoConfigureBefore.java" target="_blank"><code>@AutoConfigureBefore</code></a> 注解。例如，如果您提供特定于 Web 的配置，则可能需要在<code>WebMvcAutoConfiguration</code> 之后应用您的类。</p>
<p>如果您想排序某些不应该彼此直接了解的自动配置，您也可以使用 <code>@AutoConfigureOrder</code>。该注解与常规 <code>@Order</code> 注解有相同的语义，但它为自动配置类提供了专用顺序。</p>
<p><a id="boot-features-condition-annotations"></a></p>
<h3 id="493、条件注解">49.3、条件注解</h3>
<p>您几乎总希望在自动配置类中包含一个或多个 <code>@Conditional</code> 注解。<code>@ConditionalOnMissingBean</code> 是一个常用的注解，其允许开发人员在对您的默认值不满意用于覆盖自动配置。</p>
<p>Spring Boot 包含许多 <code>@Conditional</code> 注解，您可以通过注解 <code>@Configuration</code> 类或单独的 <code>@Bean</code> 方法在您自己的代码中复用它们。这些注解包括：</p>
<ul>
<li><a href="#boot-features-class-conditions">第 49.3.1 节，类条件</a></li>
<li><a href="#boot-features-bean-conditions">第 49.3.2 节，Bean 条件</a></li>
<li><a href="#boot-features-property-conditions">第 49.3.3 节，属性条件</a></li>
<li><a href="#boot-features-resource-conditions">第 49.3.4 节，资源条件</a></li>
<li><a href="#boot-features-web-application-conditions">第 49.3.5 节，Web 应用程序条件</a></li>
<li><a href="#boot-features-spel-conditions">第 49.3.6 节，SpEL 表达式条件</a></li>
</ul>
<p><a id="boot-features-class-conditions"></a></p>
<h4 id="4931、类条件">49.3.1、类条件</h4>
<p><code>@ConditionalOnClass</code> 和 <code>@ConditionalOnMissingClass</code> 注解允许根据特定类的是否存在来包含 <code>@Configuration</code> 类。由于使用 <a href="http://asm.ow2.org/" target="_blank">ASM</a> 解析注解元数据，您可以使用 <code>value</code> 属性来引用真实类，即使该类实际上可能不会出现在正在运行的应用程序的 classpath 中。如果您希望使用 <code>String</code> 值来指定类名，也可以使用 <code>name</code> 属性。</p>
<p>此机制不会以相同的方式应用于返回类型是条件的目标的 <code>@Bean</code> 方法：在方法上的条件应用之前，JVM 将加载类和可能处理的方法引用，如果找不到类，将发生失败。</p>
<p>要处理这种情况，可以使用单独的 <code>@Configuration</code> 类来隔离条件，如下所示：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Configuration</span>
<span class="token comment">// Some conditions</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyAutoConfiguration</span> <span class="token punctuation">{</span>

    <span class="token comment">// Auto-configured beans</span>

    <span class="token annotation punctuation">@Configuration</span>
    <span class="token annotation punctuation">@ConditionalOnClass</span><span class="token punctuation">(</span><span class="token class-name">EmbeddedAcmeService</span><span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">)</span>
    <span class="token keyword">static</span> <span class="token keyword">class</span> <span class="token class-name">EmbeddedConfiguration</span> <span class="token punctuation">{</span>

        <span class="token annotation punctuation">@Bean</span>
        <span class="token annotation punctuation">@ConditionalOnMissingBean</span>
        <span class="token keyword">public</span> <span class="token class-name">EmbeddedAcmeService</span> <span class="token function">embeddedAcmeService</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span> <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span> <span class="token punctuation">}</span>

    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p><strong>提示</strong></p>
<blockquote>
<p>如果使用 <code>@ConditionalOnClass</code> 或 <code>@ConditionalOnMissingClass</code> 作为元注解的一部分来组成自己的组合注解，则必须使用 <code>name</code> 来引用类，在这种情况将不作处理。</p>
</blockquote>
<p><a id="boot-features-bean-conditions"></a></p>
<h4 id="4932、bean-条件">49.3.2、Bean 条件</h4>
<p><code>@ConditionalOnBean</code> 和 <code>@ConditionalOnMissingBean</code> 注解允许根据特定 bean 是否存在来包含 bean。您可以使用 <code>value</code> 属性按类型或使用 <code>name</code> 来指定 bean。<code>search</code> 属性允许您限制在搜索 bean 时应考虑的 <code>ApplicationContext</code> 层次结构。</p>
<p>放置在 <code>@Bean</code> 方法上时，目标类型默认为方法的返回类型，如下所示：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Configuration</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyAutoConfiguration</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@Bean</span>
    <span class="token annotation punctuation">@ConditionalOnMissingBean</span>
    <span class="token keyword">public</span> <span class="token class-name">MyService</span> <span class="token function">myService</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span> <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span> <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>在前面的示例中，如果 <code>ApplicationContext</code> 中不包含 <code>MyService</code> 类型的 bean，则将创建 <code>myService</code> bean。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>您需要非常小心地添加 bean 定义的顺序，因为这些条件是根据到目前为止已处理的内容进行计算的。因此，我们建议在自动配置类上仅使用 <code>@ConditionalOnBean</code> 和 <code>@ConditionalOnMissingBean</code> 注解（因为这些注解保证在添加所有用户定义的 bean 定义后加载）。</p>
</blockquote>
<p><strong>注意</strong></p>
<blockquote>
<p><code>@ConditionalOnBean</code> 和 <code>@ConditionalOnMissingBean</code> 不会阻止创建 <code>@Configuration</code> 类。在类级别使用这些条件并使用注解标记每个包含 <code>@Bean</code> 方法的唯一区别是，如果条件不匹配，前者会阻止将 <code>@Configuration</code> 类注册为 bean。</p>
</blockquote>
<p><a id="boot-features-property-conditions"></a></p>
<h4 id="4933、属性条件">49.3.3、属性条件</h4>
<p><code>@ConditionalOnProperty</code> 注解允许基于 Spring Environment 属性包含配置。使用 <code>prefix</code> 和 <code>name</code> 属性指定需要检查的属性。默认情况下，匹配存在且不等于 <code>false</code> 的所有属性。您还可以使用 <code>havingValue</code> 和 <code>matchIfMissing</code> 属性创建更高级的检查。</p>
<p><a id="boot-features-resource-conditions"></a></p>
<h4 id="4934、资源条件">49.3.4、资源条件</h4>
<p><code>@ConditionalOnResource</code> 注解仅允许在存在特定资源时包含配置。可以使用常用的 Spring 约定来指定资源，如下所示：<code>file:/home/user/test.dat</code>。</p>
<p><a id="boot-features-web-application-conditions"></a></p>
<h4 id="4935、web-应用程序条件">49.3.5、Web 应用程序条件</h4>
<p><code>@ConditionalOnWebApplication</code> 和 <code>@ConditionalOnNotWebApplication</code> 注解在应用程序为 <strong>Web 应用程序</strong>的情况下是否包含配置。Web 应用程序是使用 Spring <code>WebApplicationContext</code>，定义一个 <code>session</code> 范围或具有 <code>StandardServletEnvironment</code> 的任何应用程序。</p>
<p><a id="boot-features-spel-conditions"></a></p>
<h4 id="4936、spel-表达式条件">49.3.6、SpEL 表达式条件</h4>
<p><code>@ConditionalOnExpression</code> 注解允许根据 <a href="https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#expressions" target="_blank">SpEL 表达式</a>的结果包含配置。</p>
<p><a id="boot-features-test-autoconfig"></a></p>
<h4 id="494、测试自动配置">49.4、测试自动配置</h4>
<p>自动配置可能受许多因素的影响：用户配置（<code>@Bean</code> 定义和 <code>Environment</code> 自定义）、条件评估（存在特定的类库）等。具体而言，每个测试都应该创建一个定义良好的 <code>ApplicationContext</code>，它表示这些自定义的组合。<code>ApplicationContextRunner</code> 提供了一个好的实现方法。</p>
<p><code>ApplicationContextRunner</code> 通常被定义为测试类的一个字段，用于收集基本的通用配置。以下示例确保始终调用 <code>UserServiceAutoConfiguration</code>：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">private</span> <span class="token keyword">final</span> <span class="token class-name">ApplicationContextRunner</span> contextRunner <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">ApplicationContextRunner</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
        <span class="token punctuation">.</span><span class="token function">withConfiguration</span><span class="token punctuation">(</span><span class="token class-name">AutoConfigurations</span><span class="token punctuation">.</span><span class="token function">of</span><span class="token punctuation">(</span><span class="token class-name">UserServiceAutoConfiguration</span><span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p><strong>提示</strong></p>
<blockquote>
<p>如果必须定义多个自动配置，则无需按照与运行应用程序时完全相同的顺序调用它们的声明。</p>
</blockquote>
<p>每个测试都可以使用 runner 来表示特定的用例。例如，下面的示例调用用户配置（<code>UserConfiguration</code>）并检查自动配置是否正确退回。调用 <code>run</code> 提供了一个可以与 <code>Assert4J</code> 一起使用的回调上下文。</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Test</span>
<span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">defaultServiceBacksOff</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">this</span><span class="token punctuation">.</span>contextRunner<span class="token punctuation">.</span><span class="token function">withUserConfiguration</span><span class="token punctuation">(</span><span class="token class-name">UserConfiguration</span><span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">)</span>
            <span class="token punctuation">.</span><span class="token function">run</span><span class="token punctuation">(</span><span class="token punctuation">(</span>context<span class="token punctuation">)</span> <span class="token operator">-&gt;</span> <span class="token punctuation">{</span>
                <span class="token function">assertThat</span><span class="token punctuation">(</span>context<span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">hasSingleBean</span><span class="token punctuation">(</span><span class="token class-name">UserService</span><span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
                <span class="token function">assertThat</span><span class="token punctuation">(</span>context<span class="token punctuation">.</span><span class="token function">getBean</span><span class="token punctuation">(</span><span class="token class-name">UserService</span><span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">isSameAs</span><span class="token punctuation">(</span>
                        context<span class="token punctuation">.</span><span class="token function">getBean</span><span class="token punctuation">(</span><span class="token class-name">UserConfiguration</span><span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">myUserService</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token annotation punctuation">@Configuration</span>
<span class="token keyword">static</span> <span class="token keyword">class</span> <span class="token class-name">UserConfiguration</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@Bean</span>
    <span class="token keyword">public</span> <span class="token class-name">UserService</span> <span class="token function">myUserService</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> <span class="token keyword">new</span> <span class="token class-name">UserService</span><span class="token punctuation">(</span><span class="token string">"mine"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>也可以轻松自定义 <code>Environment</code>，如下所示：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Test</span>
<span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">serviceNameCanBeConfigured</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">this</span><span class="token punctuation">.</span>contextRunner<span class="token punctuation">.</span><span class="token function">withPropertyValues</span><span class="token punctuation">(</span><span class="token string">"user.name=test123"</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">run</span><span class="token punctuation">(</span><span class="token punctuation">(</span>context<span class="token punctuation">)</span> <span class="token operator">-&gt;</span> <span class="token punctuation">{</span>
        <span class="token function">assertThat</span><span class="token punctuation">(</span>context<span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">hasSingleBean</span><span class="token punctuation">(</span><span class="token class-name">UserService</span><span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token function">assertThat</span><span class="token punctuation">(</span>context<span class="token punctuation">.</span><span class="token function">getBean</span><span class="token punctuation">(</span><span class="token class-name">UserService</span><span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">getName</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">isEqualTo</span><span class="token punctuation">(</span><span class="token string">"test123"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>
<p>runner 还可用于展示 <code>ConditionEvaluationReport</code>。报告可以在 <code>INFO</code> 或 <code>DEBUG</code> 级别下打印。以下示例展示如何使用 <code>ConditionEvaluationReportLoggingListener</code> 在自动配置测试中打印报表。</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Test</span>
<span class="token keyword">public</span> <span class="token keyword">void</span> autoConfigTest <span class="token punctuation">{</span>
    <span class="token class-name">ConditionEvaluationReportLoggingListener</span> initializer <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">ConditionEvaluationReportLoggingListener</span><span class="token punctuation">(</span>
            <span class="token class-name">LogLevel</span><span class="token punctuation">.</span>INFO<span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token class-name">ApplicationContextRunner</span> contextRunner <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">ApplicationContextRunner</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
            <span class="token punctuation">.</span><span class="token function">withInitializer</span><span class="token punctuation">(</span>initializer<span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">run</span><span class="token punctuation">(</span><span class="token punctuation">(</span>context<span class="token punctuation">)</span> <span class="token operator">-&gt;</span> <span class="token punctuation">{</span>
                    <span class="token comment">// Do something...</span>
            <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>
<p><a id="_simulating_a_web_context"></a></p>
<h4 id="4941、模拟一个-web-上下文">49.4.1、模拟一个 Web 上下文</h4>
<p>如果需要测试一个仅在 Servlet 或响应式 Web 应用程序上下文中运行的自动配置，请分别使用 <code>WebApplicationContextRunner</code> 或 <code>ReactiveWebApplicationContextRunner</code>。</p>
<p><a id="_overriding_the_classpath"></a></p>
<h4 id="4942、覆盖-classpath">49.4.2、覆盖 Classpath</h4>
<p>还可以测试在运行时不存在特定类和/或包时发生的情况。 Spring Boot附带了一个可以由跑步者轻松使用的FilteredClassLoader。 在以下示例中，我们声明如果UserService不存在，则会正确禁用自动配置：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Test</span>
<span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">serviceIsIgnoredIfLibraryIsNotPresent</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">this</span><span class="token punctuation">.</span>contextRunner<span class="token punctuation">.</span><span class="token function">withClassLoader</span><span class="token punctuation">(</span><span class="token keyword">new</span> <span class="token class-name">FilteredClassLoader</span><span class="token punctuation">(</span><span class="token class-name">UserService</span><span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">)</span><span class="token punctuation">)</span>
            <span class="token punctuation">.</span><span class="token function">run</span><span class="token punctuation">(</span><span class="token punctuation">(</span>context<span class="token punctuation">)</span> <span class="token operator">-&gt;</span> <span class="token function">assertThat</span><span class="token punctuation">(</span>context<span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">doesNotHaveBean</span><span class="token punctuation">(</span><span class="token string">"userService"</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>
<p><a id="boot-features-custom-starter"></a></p>
<h3 id="495、创建自己的-starter">49.5、创建自己的 Starter</h3>
<p>一个完整的 Spring Boot starter 类库可能包含以下组件：</p>
<ul>
<li><code>autoconfigure</code> 模块，包含自动配置代码。</li>
<li><code>starter</code> 模块，它提供对 <code>autoconfigure</code> 模块依赖关系以及类库和常用的其他依赖关系。简而言之，添加 starter 应该提供该库开始使用所需的一切。</li>
</ul>
<p><strong>提示</strong></p>
<blockquote>
<p>如果您不想将这两个模块分开，则可以将自动配置代码和依赖关系管理组合在一个模块中。</p>
</blockquote>
<p><a id="boot-features-custom-starter-naming"></a></p>
<h4 id="4951、命名">49.5.1、命名</h4>
<p>您应该确保为您的 starter 提供一个合适的命名空间。即使您使用其他 Maven <code>groupId</code>，也不要使用 <code>spring-boot</code> 作为模块名称的开头。我们可能会为您以后自动配置的内容提供官方支持。</p>
<p>根据经验，您应该在 starter 后命名一个组合模块。例如，假设您正在为 <strong>acme</strong> 创建一个 starter，并且您将自动配置模块命名为 <code>acme-spring-boot-autoconfigure</code>，将 starter 命名为 <code>acme-spring-boot-starter</code>。如果您只有一个组合这两者的模块，请将其命名为 <code>acme-spring-boot-starter</code>。</p>
<p>此外，如果您的 starter 提供配置 key，请为它们使用唯一的命名空间。尤其是，不要将您的 key 包含在 Spring Boot 使用的命名空间中（例如 <code>server</code>、<code>management</code>、<code>spring</code> 等）。如果您使用了相同的命名空间，我们将来可能会以破坏您的模块的方式来修改这些命名空间。</p>
<p>确<a href="#configuration-metadata-annotation-processor">保触发元数据生成</a>，以便为您的 key 提供 IDE 帮助。您可能想查看生成的元数据（<code>META-INF/spring-configuration-metadata.json</code>）以确保您的 key 记录是否正确。</p>
<p><a id="boot-features-custom-starter-module-autoconfigure"></a></p>
<h4 id="4952、autoconfigure-模块">49.5.2、<code>autoconfigure</code> 模块</h4>
<p><code>autoconfigure</code> 模块包含类库开始使用所需的所有内容。它还可以包含配置 key 定义（例如 <code>@ConfigurationProperties</code>）和任何可用于进一步自定义组件初始化方式的回调接口。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>您应该将类库的依赖项标记为可选，以便您可以更轻松地在项目中包含 <code>autoconfigure</code> 模块。如果以这种方式执行，则不提供类库，默认情况下，Spring Boot 将会退出。</p>
</blockquote>
<p>Spring Boot 使用注解处理器来收集元数据文件（<code>META-INF/spring-autoconfigure-metadata.properties</code>）中自动配置的条件。如果该文件存在，则用于快速过滤不匹配的自动配置，缩短启动时间。建议在包含自动配置的模块中添加以下依赖项：</p>
<pre class="language-"><code class="lang-xml"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependency</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>groupId</span><span class="token punctuation">&gt;</span></span>org.springframework.boot<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>groupId</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>artifactId</span><span class="token punctuation">&gt;</span></span>spring-boot-autoconfigure-processor<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>artifactId</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>optional</span><span class="token punctuation">&gt;</span></span>true<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>optional</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependency</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<p>使用 Gradle 4.5 及更早版本时，应在 <code>compileOnly</code> 配置中声明依赖项，如下所示：</p>
<pre class="language-"><code class="lang-groovy">dependencies <span class="token punctuation">{</span>
    compileOnly <span class="token string">"org.springframework.boot:spring-boot-autoconfigure-processor"</span>
<span class="token punctuation">}</span>
</code></pre>
<p>使用 Gradle 4.6 及更高版本时，应在 <code>annotationProcessor</code> 配置中声明依赖项，如下所示：</p>
<pre class="language-"><code class="lang-groovy">dependencies <span class="token punctuation">{</span>
    annotationProcessor <span class="token string">"org.springframework.boot:spring-boot-autoconfigure-processor"</span>
<span class="token punctuation">}</span>
</code></pre>
<p><a id="boot-features-custom-starter-module-starter"></a></p>
<h4 id="4953、starter-模块">49.5.3、Starter 模块</h4>
<p>starter 真的是一个空 jar。它的唯一目的是为使用类库提供必要的依赖项。您可以将其视为使用类库的一切基础。</p>
<p>不要对添加 starter 的项目抱有假设想法。如果您自动配置的库经常需要其他 starter，请一并声明它们。如果可选依赖项的数量很多，则提供一组适当的默认依赖项可能很难，因为您本应该避免包含对常用库的使用不必要的依赖项。换而言之，您不应该包含可选的依赖项。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>无论哪种方式，您的 starter 必须直接或间接引用核心 Spring Boot starter（<code>spring-boot-starter</code>）（如果您的 starter 依赖于另一个 starter ，则无需添加它）。如果只使用自定义 starter 创建项目，则 Spring Boot 的核心功能将通过存在的核心 starter 来实现。</p>
</blockquote>
<p><a id="boot-features-kotlin"></a></p>
<h2 id="50、kotlin-支持">50、Kotlin 支持</h2>
<p><a href="https://kotlinlang.org/" target="_blank">Kotlin</a> 是一种针对 JVM（和其他平台）的静态类型语言，它可编写出简洁而优雅的代码，同时提供与使用 Java 编写的现有库的<a href="https://kotlinlang.org/docs/reference/java-interop.html" target="_blank">互操作性</a>。</p>
<p>Spring Boot 通过利用其他 Spring 项目（如 Spring Framework、Spring Data 和 Reactor）的支持来提供 Kotlin 支持。有关更多信息，请参阅 <a href="https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/languages.html#kotlin" target="_blank">Spring Framework Kotlin 支持文档</a>。</p>
<p>开始学习 Spring Boot 和 Kotlin 最简单方法是遵循这个<a href="https://spring.io/guides/tutorials/spring-boot-kotlin/" target="_blank">全面教程</a>。您可以通过 <a href="https://start.spring.io/#!language=kotlin" target="_blank">start.spring.io</a> 创建新的 Kotlin 项目。如果您需要支持，请免费加入 <a href="http://slack.kotlinlang.org/" target="_blank">Kotlin Slack</a> 的 #spring 频道或使用 <a href="https://stackoverflow.com/questions/tagged/spring+kotlin" target="_blank">Stack Overflow</a> 上的 <code>spring</code> 和 <code>kotlin</code> 标签提问。</p>
<p><a id="boot-features-kotlin-requirements"></a></p>
<h3 id="501、要求">50.1、要求</h3>
<p>Spring Boot 支持 Kotlin 1.2.x。要使用 Kotlin，classpath 下必须存在 <code>org.jetbrains.kotlin:kotlin-stdlib</code> 和 <code>org.jetbrains.kotlin:kotlin-reflect</code>。也可以使用 <code>kotlin-stdlib</code> 的变体 <code>kotlin-stdlib-jdk7</code> 和 <code>kotlin-stdlib-jdk8</code>。</p>
<p>由于 <a href="https://discuss.kotlinlang.org/t/classes-final-by-default/166" target="_blank">Kotlin 类默认为 final</a>，因此您可能需要配置 <a href="https://kotlinlang.org/docs/reference/compiler-plugins.html#spring-support" target="_blank">kotlin-spring</a> 插件以自动打开 <code>Spring-annotated</code> 类，以便可以代理它们。</p>
<p>在 Kotlin 中序列化/反序列化 JSON 数据需要使用 <a href="https://github.com/FasterXML/jackson-module-kotlin" target="_blank">Jackson 的 Kotlin 模块</a>。在 classpath 中找到它时会自动注册。如果 Jackson 和 Kotlin 存在但 Jackson Kotlin 模块不存在，则会记录警告消息。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>如果在 <a href="https://start.spring.io/#!language=kotlin" target="_blank">start.spring.io</a> 上创建 Kotlin 项目，则默认提供这些依赖项和插件。</p>
</blockquote>
<p><a id="boot-features-kotlin-null-safety"></a></p>
<h3 id="502、null-安全">50.2、Null 安全</h3>
<p>Kotlin 的一个关键特性是 <a href="https://kotlinlang.org/docs/reference/null-safety.html" target="_blank">null 安全</a>。它在编译时处理空值，而不是将问题推迟到运行时并遇到 <code>NullPointerException</code>。这有助于消除常见的错误来源，而无需支付像 <code>Optional</code> 这样的包装器的成本。Kotlin 还允许使用有可空值的，如 <a href="http://www.baeldung.com/kotlin-null-safety" target="_blank">Kotlin null 安全综合指南</a>中所述。</p>
<p>虽然 Java 不允许在其类型系统中表示 null 安全，但 Spring Framework、Spring Data 和 Reactor 现在通过易于使用的工具的注解提供其 API 的安全性。默认情况下，Kotlin 中使用的 Java API 类型被识别为放宽空检查的<a href="https://kotlinlang.org/docs/reference/java-interop.html#null-safety-and-platform-types" target="_blank">平台类型</a>。<a href="https://kotlinlang.org/docs/reference/java-interop.html#jsr-305-support" target="_blank">Kotlin 对 JSR 305 注解的支持</a>与可空注解相结合，为 Kotlin 中 Spring API 相关的代码提供了空安全。</p>
<p>可以通过使用以下选项添加 <code>-Xjsr305</code> 编译器标志来配置 JSR 305 检查：<code>-Xjsr305={strict|warn|ignore}</code>。默认行为与 <code>-Xjsr305=warn</code> 相同。在从 Spring API 推断出的 Kotlin 类型中需要考虑 null 安全的 <code>strict</code> 值，但是应该使用 Spring API 可空声明甚至可以在次要版本之间发展并且将来可能添加更多检查的方案。</p>
<p><strong>警告</strong></p>
<blockquote>
<p>尚不支持泛型类型参数、<code>varargs</code> 和数组元素可空性。有关最新信息，请参见 <a href="https://jira.spring.io/browse/SPR-15942" target="_blank">SPR-15942</a>。另请注意，Spring Boot 自己的 API <a href="https://github.com/spring-projects/spring-boot/issues/10712" target="_blank">尚未注解</a>。</p>
</blockquote>
<p><a id="boot-features-kotlin-api"></a></p>
<h3 id="503、kotlin-api">50.3、Kotlin API</h3>
<p><a id="boot-features-kotlin-api-runapplication"></a></p>
<h4 id="5031、runapplication">50.3.1、runApplication</h4>
<p>Spring Boot 提供了使用 <code>runApplication<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>MyApplication</span><span class="token punctuation">&gt;</span></span>(*args)</code> 运行应用程序的惯用方法，如下所示：</p>
<pre class="language-"><code class="lang-kotlin"><span class="token keyword">import</span> org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>boot<span class="token punctuation">.</span>autoconfigure<span class="token punctuation">.</span>SpringBootApplication
<span class="token keyword">import</span> org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>boot<span class="token punctuation">.</span>runApplication

<span class="token annotation builtin">@SpringBootApplication</span>
<span class="token keyword">class</span> MyApplication

<span class="token keyword">fun</span> <span class="token function">main</span><span class="token punctuation">(</span>args<span class="token operator">:</span> Array<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    runApplication<span class="token operator">&lt;</span>MyApplication<span class="token operator">&gt;</span><span class="token punctuation">(</span><span class="token operator">*</span>args<span class="token punctuation">)</span>
<span class="token punctuation">}</span>
</code></pre>
<p>这是 <code>SpringApplication.run(MyApplication::class.java, *args)</code> 的替代方式。它还允许自定义应用程序，如下所示：</p>
<pre class="language-"><code class="lang-kotlin">runApplication<span class="token operator">&lt;</span>MyApplication<span class="token operator">&gt;</span><span class="token punctuation">(</span><span class="token operator">*</span>args<span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token function">setBannerMode</span><span class="token punctuation">(</span>OFF<span class="token punctuation">)</span>
<span class="token punctuation">}</span>
</code></pre>
<p><a id="boot-features-kotlin-api-extensions"></a></p>
<h4 id="5032、扩展">50.3.2、扩展</h4>
<p>Kotlin <a href="https://kotlinlang.org/docs/reference/extensions.html" target="_blank">扩展</a>提供了使用附加功能扩展现有类的能力。Spring Boot Kotlin API 利用这些扩展为现有 API 添加新的 Kotlin 特定便利。</p>
<p>提供的 <code>TestRestTemplate</code> 扩展类似于 Spring Framework 为 <code>RestOperations</code> 提供的。除此之外，扩展使得利用 Kotlin reified 类型参数变为可能。</p>
<p><a id="boot-features-kotlin-dependency-management"></a></p>
<h3 id="504、依赖管理">50.4、依赖管理</h3>
<p>为了避免在 classpath 上混合不同版本的 Kotlin 依赖项，提供了以下 Kotlin 依赖项的依赖项管理：</p>
<ul>
<li><code>kotlin-reflect</code></li>
<li><code>kotlin-runtime</code></li>
<li><code>kotlin-stdlib</code></li>
<li><code>kotlin-stdlib-jdk7</code></li>
<li><code>kotlin-stdlib-jdk8</code></li>
<li><code>kotlin-stdlib-jre7</code></li>
<li><code>kotlin-stdlib-jre8</code></li>
</ul>
<p>使用 Maven，可以通过 <code>kotlin.version</code> 属性自定义 Kotlin 版本，并为 <code>kotlin-maven-plugin</code> 提供插件管理。使用 Gradle，Spring Boot 插件会自动将 <code>kotlin.version</code> 与 Kotlin 插件的版本保一致。</p>
<p><a id="boot-features-kotlin-configuration-properties"></a></p>
<h3 id="505、configurationproperties">50.5、<code>@ConfigurationProperties</code></h3>
<p><code>@ConfigurationProperties</code> 目前仅适用于 <code>lateinit</code> 或可空的 <code>var</code> 属性（建议使用前者），因为<a href="https://github.com/spring-projects/spring-boot/issues/8762" target="_blank">尚不支持</a>由构造函数初始化的不可变类。</p>
<pre class="language-"><code class="lang-kotlin"><span class="token annotation builtin">@ConfigurationProperties</span><span class="token punctuation">(</span><span class="token string">"example.kotlin"</span><span class="token punctuation">)</span>
<span class="token keyword">class</span> KotlinExampleProperties <span class="token punctuation">{</span>

    <span class="token keyword">lateinit</span> <span class="token keyword">var</span> name<span class="token operator">:</span> String

    <span class="token keyword">lateinit</span> <span class="token keyword">var</span> description<span class="token operator">:</span> String

    <span class="token keyword">val</span> myService <span class="token operator">=</span> <span class="token function">MyService</span><span class="token punctuation">(</span><span class="token punctuation">)</span>

    <span class="token keyword">class</span> MyService <span class="token punctuation">{</span>

        <span class="token keyword">lateinit</span> <span class="token keyword">var</span> apiToken<span class="token operator">:</span> String

        <span class="token keyword">lateinit</span> <span class="token keyword">var</span> uri<span class="token operator">:</span> URI

    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p><strong>提示</strong></p>
<blockquote>
<p>要使用注解处理器生成<a href="#configuration-metadata-annotation-processor">您自己的元数据</a>，应使用 <code>spring-boot-configuration-processor</code> 依赖<a href="https://kotlinlang.org/docs/reference/kapt.html" target="_blank">配置 <code>kapt</code></a>。</p>
</blockquote>
<p><a id="boot-features-kotlin-testing"></a></p>
<h3 id="506、测试">50.6、测试</h3>
<p>虽然可以使用 JUnit 4（<code>spring-boot-starter-test</code> 提供的默认配置）来测试 Kotlin 代码，但建议使用 JUnit 5。JUnit 5 允许测试类实例化一次，并在所有类的测试中复用。这使得可以在非静态方法上使用 <code>@BeforeAll</code> 和 <code>@AfterAll</code> 注解，这非常适合 Kotlin。</p>
<p>要使用 JUnit 5，请从 <code>spring-boot-starter-test</code> 中排除 <code>junit:junit</code> 依赖项，然后添加 JUnit 5 依赖项，并相应地配置 Maven 或 Gradle 插件。有关更多详细信息，请参阅 <a href="https://junit.org/junit5/docs/current/user-guide/#dependency-metadata-junit-jupiter-samples" target="_blank">JUnit 5 文档</a>。您还需要<a href="https://junit.org/junit5/docs/current/user-guide/#writing-tests-test-instance-lifecycle-changing-default" target="_blank">将测试实例生命周期切换为 <strong>per-class</strong></a>。</p>
<p>为了模拟 Kotlin 类，建议使用 <a href="https://mockk.io/" target="_blank">Mockk</a>。如果需要 Mockk 等效的 Mockito 特定的 <a href="boot-features-testing-spring-boot-applications-mocking-beans"><code>@MockBean</code> 和 <code>@SpyBean</code> 注解</a>，则可以使用 <a href="https://github.com/Ninja-Squad/springmockk" target="_blank">SpringMockK</a>，它提供类似的 <code>@MockkBean</code> 和 <code>@SpykBean</code> 注解。</p>
<p><a id="boot-features-kotlin-resources"></a></p>
<h3 id="507、资源">50.7、资源</h3>
<p><a id="boot-features-kotlin-resources-further-reading"></a></p>
<h4 id="5071、进阶阅读">50.7.1、进阶阅读</h4>
<ul>
<li><a href="https://kotlinlang.org/docs/reference/" target="_blank">Kotlin 语言参考</a></li>
<li><a href="http://slack.kotlinlang.org/" target="_blank">Kotlin Slack</a>（有专用的 #spring 频道）</li>
<li><a href="https://stackoverflow.com/questions/tagged/spring+kotlin" target="_blank">Stackoverflow 上 <code>spring</code> 和 <code>kotlin</code> 标签</a></li>
<li><a href="https://try.kotlinlang.org/" target="_blank">在浏览器中尝试 Kotlin</a></li>
<li><a href="https://blog.jetbrains.com/kotlin/" target="_blank">Kotlin 博客</a></li>
<li><a href="https://kotlin.link/" target="_blank">Awesome Kotlin</a></li>
<li><a href="https://spring.io/guides/tutorials/spring-boot-kotlin/" target="_blank">教程：使用 Spring Boot 和 Kotlin 构建 Web 应用程序</a></li>
<li><a href="https://spring.io/blog/2016/02/15/developing-spring-boot-applications-with-kotlin" target="_blank">使用 Kotlin 开发 Spring Boot 应用程序</a></li>
<li><a href="https://spring.io/blog/2016/03/20/a-geospatial-messenger-with-kotlin-spring-boot-and-postgresql" target="_blank">使用 Kotlin、Spring Boot 和 PostgreSQL 开发地理信使</a></li>
<li><a href="https://spring.io/blog/2017/01/04/introducing-kotlin-support-in-spring-framework-5-0" target="_blank">在 Spring Framework 5.0 中引入 Kotlin 支持</a></li>
<li><a href="https://spring.io/blog/2017/08/01/spring-framework-5-kotlin-apis-the-functional-way" target="_blank">Spring Framework 5 Kotlin API 实现函数式</a></li>
</ul>
<p><a id="boot-features-kotlin-resources-examples"></a></p>
<h4 id="5072、示例">50.7.2、示例</h4>
<ul>
<li><a href="https://github.com/sdeleuze/spring-boot-kotlin-demo" target="_blank">spring-boot-kotlin-demo</a>：常规的 Spring Boot + Spring Data JPA 项目</li>
<li><a href="https://github.com/mixitconf/mixit" target="_blank">mixit</a>：Spring Boot 2 + WebFlux + Reactive Spring Data MongoDB</li>
<li><a href="https://github.com/sdeleuze/spring-kotlin-fullstack" target="_blank">spring-kotlin-fullstack</a>：WebFlux Kotlin 全栈示例，在前端使用 Kotlin2js 代替 JavaScript 和 TypeScript</li>
<li><a href="https://github.com/spring-petclinic/spring-petclinic-kotlin" target="_blank">spring-petclinic-kotlin</a>：Spring PetClinic 示例应用的 Kotlin 版本</li>
<li><a href="https://github.com/sdeleuze/spring-kotlin-deepdive" target="_blank">spring-kotlin-deepdive</a>：将Boot 1.0 + Java 逐步迁移到 Boot 2.0 + Kotlin</li>
</ul>
<p><a id="boot-features-whats-next"></a></p>
<h2 id="51、下一步">51、下一步</h2>
<p>如果您想了解本节中讨论的任何类目的更多信息，可以查看 <a href="https://docs.spring.io/spring-boot/docs/2.1.3.RELEASE/api" target="_blank">Spring Boot API 文档</a>，也可以直接浏览<a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE" target="_blank">源代码</a>。如果您有具体问题，请查看 <a href="howto.md">how-to</a> 部分。</p>
<p>如果您对 Spring Boot 的核心功能感到满意，可以继续阅读有关生产就绪功能的内容。</p>
<footer class="page-footer"><span class="copyright">felord.cn</span>&nbsp; &nbsp; <a href="http://beian.miit.gov.cn/" class="copyright-links" target="_blank" rel="nofollow">豫ICP备19038867号-1</a><span class="footer-modification">File Modify:
2019-10-16 21:49:43
</span></footer>
                                
                                </section>
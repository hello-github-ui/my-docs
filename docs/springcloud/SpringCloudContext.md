<section class="normal markdown-section">
<div id="content">
<h1>2. Spring Cloud Context：Application Context Services</h1>
<div><ins class="adsbygoogle" style="display:block; text-align:center;" data-ad-layout="in-article" data-ad-format="fluid" data-ad-client="ca-pub-6108808167664152" data-ad-slot="6964403648"></ins>
<script>
(adsbygoogle = window.adsbygoogle || []).push({});
</script></div>
<div><p>Spring Boot 对于如何使用 Spring 构建 application 有一个自以为是的观点：例如，它具有 common configuration 文件的常规位置，_comnd management 和监视任务的 endpoints。 Spring Cloud 构建于此之上，并添加了一些 features，可能系统中的所有组件都会使用或偶尔需要。</p>
<h2 id="bootstrap-application-context"><a href="#_the_bootstrap_application_context" id="_the_bootstrap_application_context"></a> 2.1 Bootstrap Application Context</h2>
<p>Spring Cloud application 通过 creating“bootstrap”context 来操作，它是主 application 的 parent context。它开箱即用，它负责从外部源加载 configuration properties，并解密本地外部 configuration files 中的 properties。这两个上下文共享一个<code>Environment</code>，它是任何 Spring application 的外部 properties 的源。 Bootstrap properties(不是<code>bootstrap.properties</code>，但是在引导阶段加载的 properties)以高优先级添加，因此默认情况下它们不能被 local configuration 覆盖。</p>
<p>bootstrap context 使用不同的约定来查找外部 configuration 而不是主 application context，因此使用<code>bootstrap.yml</code>而不是<code>application.yml</code>(或<code>.properties</code>)，保持 bootstrap 和 main context 的外部 configuration 很好地分开。 例：</p>
<p><strong>bootstrap.yml.</strong></p>
<pre><code class="language-">spring:
  application:
    name: foo
  cloud:
    config:
      uri: ${SPRING_CONFIG_URI:http://localhost:8888}
</code></pre>
<p>如果您的 application 需要来自服务器的任何 application-specific configuration，那么设置<code>spring.application.name</code>(在<code>bootstrap.yml</code>或<code>application.yml</code>中)是一个很好的 idea。</p>
<p>您可以通过在 System properties 中设置<code>spring.cloud.bootstrap.enabled=false</code>(e.g. )来完全禁用 bootstrap process。</p>
<h2 id="application-context-层次结构"><a href="#_application_context_hierarchies" id="_application_context_hierarchies"></a> 2.2 Application Context 层次结构</h2>
<p>如果从<code>SpringApplication</code>或<code>SpringApplicationBuilder</code> build application context，则将 Bootstrap context 作为 parent 添加到该 context。它是 Spring 的一个 feature，child 上下文从它们的 parent 继承 property 源和 profiles，所以“main”application context 将包含额外的 property 源，相比之下 building 相同的 context 没有 Spring Cloud Config。额外的 property 来源是：</p>
<ul>
<li>
<p>“bootstrap”：如果在 Bootstrap context 中找到任何<code>PropertySourceLocators</code>，则可选<code>CompositePropertySource</code>具有高优先级，并且它们具有 non-empty properties。 example 将是 Spring Cloud Config Server 的 properties。有关如何自定义此 property 源的内容的说明，请参阅<a href="multi__spring_cloud_context_application_context_services.html#customizing-bootstrap-property-sources">下面</a>。</p>
</li>
<li>
<p>“applicationConfig：[18]”(和朋友，如果 Spring profiles 是 active)。如果你有一个<code>bootstrap.yml</code>(或 properties)，那么这些 properties 用于配置 Bootstrap context，然后在设置 parent 时将它们添加到 child context。它们的优先级低于<code>application.yml</code>(或 properties)以及添加到 child 的任何其他 property 源，作为 creating Spring Boot application 的 process 的正常部分。有关如何自定义这些 property 源的内容的说明，请参阅<a href="multi__spring_cloud_context_application_context_services.html#customizing-bootstrap-properties">下面</a>。</p>
</li>
</ul>
<p>由于 property 源的_ororder 规则，“bootstrap”条目优先，但请注意，这些条目不包含来自<code>bootstrap.yml</code>的任何数据，它具有非常低的优先级，但可用于设置默认值。</p>
<p>您可以通过简单地设置您创建的任何<code>ApplicationContext</code>的 parent context 来扩展 context 层次结构 e.g. 使用自己的接口，或使用<code>SpringApplicationBuilder</code>方便方法(<code>parent()</code>，<code>child()</code>和<code>sibling()</code>)。 bootstrap context 将是您自己创建的最高级祖先的 parent。层次结构中的每个 context 都有自己的“bootstrap”property 源(可能为空)，以避免无意中将值从 parents 降级到它们的后代。如果存在 Config Server，层次结构中的每个 context(原则上)也可以具有不同的<code>spring.application.name</code>，因此具有不同的 remote property 源。正常的 Spring application context 行为规则适用于 property 解决方案：来自 child context 的 properties 覆盖 parent，name 和 property source name 中的 properties(如果 child 有一个 property 源与 parent 具有相同的 name，来自 parent 不包含在 child 中。</p>
<p>请注意，<code>SpringApplicationBuilder</code>允许您在整个层次结构中共享<code>Environment</code>，但这不是默认值。因此，特别是兄弟情境不需要具有相同的 profiles 或 property 源，即使它们将与 parent 共享 common 事物。</p>
<h2 id="更改-bootstrap-properties-的位置"><a href="#customizing-bootstrap-properties" id="customizing-bootstrap-properties"></a> 2.3 更改 Bootstrap Properties 的位置</h2>
<p><code>bootstrap.yml</code>(或<code>.properties</code>)位置可以使用<code>spring.cloud.bootstrap.name</code>(默认“bootstrap”)或<code>spring.cloud.bootstrap.location</code>(默认为空)e.g 指定。在 System properties 中。那些 properties 的行为类似于具有相同 name 的<code>spring.config.*</code>变体，实际上它们用于通过在<code>Environment</code>中设置 properties 来设置 bootstrap <code>ApplicationContext</code>。如果有 active profile(来自<code>spring.profiles.active</code>或通过 context 中的<code>Environment</code> API，你是 building)，那么 profile 中的 properties 也将被加载，就像在常规的 Spring Boot 应用程序中一样，e.g. 来自<code>bootstrap-development.properties</code>的“发展”profile。</p>
<h2 id="覆盖-remote-properties-的值"><a href="#overriding-bootstrap-properties" id="overriding-bootstrap-properties"></a> 2.4 覆盖 Remote Properties 的值</h2>
<p>由 bootstrap context 添加到 application 的 property 源通常是“remote”(来自 Config Server 的 e.g. )，默认情况下，除了命令 line 之外，它们不能在本地重写。如果要允许 applications 使用自己的 System properties 或 config files 覆盖 remote properties，则 remote property 源必须通过设置<code>spring.cloud.config.allowOverride=true</code>来授予它权限(它不能在本地设置它)。一旦设置了 flag，就会有一些更细粒度的设置来控制 remote properties 相对于 System properties 的位置和 application 的本地 configuration：<code>spring.cloud.config.overrideNone=true</code>以覆盖任何本地 property 源，如果只有 System properties 和 env vars 应该覆盖<code>spring.cloud.config.overrideSystemProperties=false</code> remote 设置，但不是本地配置 files。</p>
<h2 id="自定义-bootstrap-configuration"><a href="#_customizing_the_bootstrap_configuration" id="_customizing_the_bootstrap_configuration"></a> 2.5 自定义 Bootstrap Configuration</h2>
<p>可以通过在 key <code>org.springframework.cloud.bootstrap.BootstrapConfiguration</code>下向<code>/META-INF/spring.factories</code>添加条目来训练 bootstrap context 以执行任何操作。这是 Spring <code>@Configuration</code> classes 的 comma-separated 列表，它将用于创建 context。您可以在此处创建任何希望可用于主 application context 以进行自动装配的 beans，并且<code>@Beans</code>类型的<code>@Beans</code>还有一个特殊的 contract。如果要控制启动顺序(默认 order 是“last”)，Class 可以用<code>@Order</code>标记。</p>
<blockquote><p>添加自定义<code>BootstrapConfiguration</code>时要小心，你添加的 classes 错误地不是<code>@ComponentScanned</code>到你的“main”application context 中，可能不需要它们。对或<code>@SpringBootApplication</code>带注释的 configuration classes 尚未涵盖的 boot configuration classes 使用单独的包 name。</p>
</blockquote>
<p>引导程序 process _end 通过将初始化程序注入主<code>SpringApplication</code>实例(i.e.正常 Spring Boot 启动顺序，无论它是作为独立应用程序运行还是部署在 application 服务器中)。首先从<code>spring.factories</code>中找到的 classes 创建 bootstrap context，然后在启动之前将类型<code>@Beans</code>添加到主<code>SpringApplication</code>。</p>
<h2 id="自定义-bootstrap-property-sources"><a href="#customizing-bootstrap-property-sources" id="customizing-bootstrap-property-sources"></a> 2.6 自定义 Bootstrap Property Sources</h2>
<p>bootstrap process 添加的外部 configuration 的默认 property 源是 Config Server，但您可以通过将<code>PropertySourceLocator</code>类型的 beans 添加到 bootstrap context(通过<code>spring.factories</code>)来添加其他源。例如，您可以使用它来插入来自不同服务器或数据库的其他 properties。</p>
<p>作为示例，请考虑以下简单的自定义定位器：</p>
<pre><code class="language-">@Configuration
public class CustomPropertySourceLocator implements PropertySourceLocator {

    @Override
    public PropertySource&lt;?&gt; locate(Environment environment) {
        return new MapPropertySource("customProperty",
                Collections.&lt;String, Object&gt;singletonMap("property.from.sample.custom.source", "worked as intended"));
    }

}
</code></pre>
<p>传入的<code>Environment</code>是要创建的<code>ApplicationContext</code>的<code>Environment</code>，i.e。我们正在提供额外的 property 来源的那个。它已经有了正常的 Spring Boot-provided property 源，因此您可以使用它们来查找特定于此<code>Environment</code>的 property 源(e.g. 通过在<code>spring.application.name</code>上键入它，就像在默认的 Config Server property 源定位器中所做的那样)。</p>
<p>如果在其中创建带有此 class 的 jar，然后添加包含以下内容的<code>META-INF/spring.factories</code>：</p>
<pre><code class="language-">org.springframework.cloud.bootstrap.BootstrapConfiguration=sample.custom.CustomPropertySourceLocator
</code></pre>
<p>然后“customProperty”<code>PropertySource</code>将显示在任何 application 中，其 class 路径上包含 jar。</p>
<h2 id="logging-configuration"><a href="#_logging_configuration" id="_logging_configuration"></a> 2.7 Logging Configuration</h2>
<p>如果你打算使用 Spring Boot 来配置 log 设置，你应该将这个 configuration 放在`bootstrap。[72]中，如果你希望它适用于所有的 events。</p>
<h2 id="环境变化"><a href="#_environment_changes" id="_environment_changes"></a> 2.8 环境变化</h2>
<p>application 将侦听<code>EnvironmentChangeEvent</code>并以几种标准方式对更改作出反应(用户可以正常方式将<code>ApplicationListeners</code>添加为<code>@Beans</code>)。当观察到<code>EnvironmentChangeEvent</code>时，它将有一个已更改的 key 值列表，application 将使用这些值：</p>
<ul>
<li>
<p>Re-bind context 中的任何<code>@ConfigurationProperties</code> beans</p>
</li>
<li>
<p>为<code>logging.level.*</code>中的任何 properties 设置 logger 级别</p>
</li>
</ul>
<p>请注意，Config Client 默认情况下不会轮询<code>Environment</code>中的更改，通常我们不建议使用这种方法来检测更改(尽管您可以使用<code>@Scheduled</code> annotation 进行设置)。如果你有一个 scaled-out client application，那么最好将<code>EnvironmentChangeEvent</code>播放到所有实例，而不是让它们轮询更改(e.g. 使用<a href="https://github.com/spring-cloud/spring-cloud-bus" target="_blank" rel="noopener noreferrer">Spring Cloud Bus</a>)。</p>
<p><code>EnvironmentChangeEvent</code>涵盖了大型的 class 刷新用例，因为你实际上可以对<code>Environment</code>进行更改并发布 event(这些 API 是公共的，部分是核心 Spring)。您可以通过访问<code>/configprops</code>端点(正常 Spring Boot Actuator feature)来验证更改是否绑定到<code>@ConfigurationProperties</code> beans。例如，<code>DataSource</code>可以在运行时更改<code>maxPoolSize</code>(Spring Boot 创建的默认<code>DataSource</code>是<code>@ConfigurationProperties</code> bean)并动态增加容量。 Re-binding <code>@ConfigurationProperties</code>不包括另一个大的 class 用例，你需要更多控制刷新，以及你需要在整个<code>ApplicationContext</code>上进行原子更改。为了解决这些问题，我们有<code>@RefreshScope</code>。</p>
<h2 id="刷新范围"><a href="#_refresh_scope" id="_refresh_scope"></a> 2.9 刷新范围</h2>
<p>当 configuration 更改时，标记为<code>@RefreshScope</code>的 Spring <code>@Bean</code>将得到特殊处理。这解决了有状态 beans 的问题，它们只在初始化时才会注入 configuration。例如，如果<code>DataSource</code>在通过<code>Environment</code>更改数据库 URL 时具有打开的连接，我们可能希望这些连接的持有者能够完成他们正在做的事情。然后在下一个 time 有人借用池中的连接时，他会使用新 URL 获取一个连接。</p>
<p>刷新范围 beans 是在使用它们时初始化的惰性代理(i.e.当调用方法时)，并且范围充当初始化值的缓存。要在下一个方法调用上强制 bean 到 re-initialize，您只需要使其缓存条目无效。</p>
<p><code>RefreshScope</code>是 context 中的 bean，它有一个公共方法<code>refreshAll()</code>，通过清除目标缓存来刷新范围内的所有 beans。还有一个<code>refresh(String)</code>方法可以通过 name 刷新单个 bean。此功能在<code>/refresh</code>端点(通过 HTTP 或 JMX)中公开。</p>
<blockquote><p><code>@RefreshScope</code>(在技术上)在<code>@Configuration</code> class 上工作，但它可能会导致令人惊讶的行为：e.g. 它不**意味着该 class 中定义的所有<code>@Beans</code>本身都是<code>@RefreshScope</code>。具体来说，任何依赖于那些 beans 的东西都不能依赖它们在启动刷新时被更新，除非它本身在<code>@RefreshScope</code>(它将在刷新时重建它的依赖 re-injected，此时它们将是 re-initialized 来自刷新<code>@Configuration</code>)。</p>
</blockquote>
<h2 id="加密和解密"><a href="#_encryption_and_decryption" id="_encryption_and_decryption"></a> 2.10 加密和解密</h2>
<p>Spring Cloud 有一个<code>Environment</code> pre-processor 用于在本地解密 property 值。它遵循与 Config Server 相同的规则，并通过<code>encrypt.*</code>具有相同的外部 configuration。因此，您可以使用<code>{cipher}*</code>形式的加密值和 long 作为 long，因为它们将在主 application context 获得<code>Environment</code>之前被解密。要在 application 中使用加密 features，您需要在 classpath(Maven co-ordinates“org.springframework.security:spring-security-rsa”)中包含 Spring Security RSA，并且还需要 JVM 中的全强度 JCE extensions。</p>
<p>如果由于“非法 key 大小”而得到 exception 并且您使用的是 Sun 的 JDK，则需要安装 Java Cryptography Extension(JCE)Unlimited Strength Jurisdiction Policy Files。有关更多信息，请参阅以下链接：</p>
<ul>
<li>
<p><a href="http://www.oracle.com/technetwork/java/javase/downloads/jce-6-download-429243.html" target="_blank" rel="noopener noreferrer">Java 6 JCE</a></p>
</li>
<li>
<p><a href="http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html" target="_blank" rel="noopener noreferrer">Java 7 JCE</a></p>
</li>
<li>
<p><a href="http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html" target="_blank" rel="noopener noreferrer">Java 8 JCE</a></p>
</li>
</ul>
<p>将 files 提取到 JDK/jre/lib/security 文件夹中(无论你使用哪个 version JRE/JDK x64/x86)。</p>
<h2 id="endpoints"><a href="#_endpoints" id="_endpoints"></a> 2.11 Endpoints</h2>
<p>对于 Spring Boot Actuator application，还有一些额外的 management endpoints：</p>
<ul>
<li>
<p>POST 到<code>/env</code>以更新<code>Environment</code>并重新绑定<code>@ConfigurationProperties</code>和 log 级别</p>
</li>
<li>
<p><code>/refresh</code>为 re-loading boot strap context 并刷新<code>@RefreshScope</code> beans</p>
</li>
<li>
<p><code>/restart</code>用于关闭<code>ApplicationContext</code>并重新启动它(默认情况下禁用)</p>
</li>
<li>
<p><code>/pause</code>和<code>/resume</code>用于调用<code>Lifecycle</code>方法(<code>ApplicationContext</code>上<code>stop()</code>和<code>start()</code>)</p>
</li>
</ul>
<blockquote><p>如果禁用<code>/restart</code>端点，则<code>/pause</code>和<code>/resume</code> endpoints 也将被禁用，因为它们只是<code>/restart</code>的一个特例。</p>
</blockquote>
</div>
</div>
</section>
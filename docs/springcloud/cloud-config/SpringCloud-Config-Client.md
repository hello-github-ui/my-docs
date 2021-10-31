<section class="normal markdown-section">
<div id="content">
<h1>10. Spring Cloud Config Client</h1>
<div><ins class="adsbygoogle" style="display:block; text-align:center;" data-ad-layout="in-article" data-ad-format="fluid" data-ad-client="ca-pub-6108808167664152" data-ad-slot="6964403648"></ins>
<script>
(adsbygoogle = window.adsbygoogle || []).push({});
</script></div>
<div><p>Spring Boot application 可以立即利用 Spring 配置服务器(或 application 开发人员提供的其他外部 property 源)，它还将获取一些与<code>Environment</code> change events 相关的其他有用的 features。</p>
<h2 id="config-first-bootstrap"><a href="#config-first-bootstrap" id="config-first-bootstrap"></a> 10.1 Config First Bootstrap</h2>
<p>这是在 classpath 上具有 Spring Cloud Config Client 的任何 application 的默认行为。当 config client 启动时，它会绑定到 Config Server(通过 bootstrap configuration property <code>spring.cloud.config.uri</code>)并使用 remote property 源初始化 Spring <code>Environment</code>。</p>
<p>最终结果是，所有想要使用配置服务器的 client 应用程序需要<code>bootstrap.yml</code>(或环境变量)，服务器地址在<code>spring.cloud.config.uri</code>(默认为“http://localhost:8888”)。</p>
<h2 id="discovery-first-bootstrap"><a href="#discovery-first-bootstrap" id="discovery-first-bootstrap"></a> 10.2 Discovery First Bootstrap</h2>
<p>如果您正在使用`DiscoveryClient implementation，例如 Spring Cloud Netflix 和 Eureka Service Discovery 或 Spring Cloud Consul(Spring Cloud Zookeeper 尚不支持此功能)，那么您可以将 Config Server 注册到 Discovery Service，如果您愿意，但在默认的“Config First”模式下，clients 将无法利用注册。</p>
<p>如果您更喜欢使用<code>DiscoveryClient</code>来定位配置服务器，可以通过设置<code>spring.cloud.config.discovery.enabled=true</code>(默认为“false”)来实现。最终结果是 client 应用程序都需要具有适当发现 configuration 的<code>bootstrap.yml</code>(或环境变量)。对于 example，使用 Spring Cloud Netflix，您需要定义 Eureka 服务器地址 e.g. 在<code>eureka.client.serviceUrl.defaultZone</code>。使用此选项的价格是启动时额外的网络往返，以查找服务注册。好处是 Config Server 可以将 co-ordinates 更改为 long，因为 Discovery Service 是一个固定点。默认服务 ID 是“configserver”，但您可以使用<code>spring.cloud.config.discovery.serviceId</code>在 client 上更改它(在服务器上以通常的方式更改服务，e.g. 通过设置<code>spring.application.name</code>)。</p>
<p>发现 client implementations 都支持某种元数据 map(e.g. 对于 Eureka 我们有<code>eureka.instance.metadataMap</code>)。可能需要在其服务注册元数据中配置 Config Server 的一些其他 properties，以便 clients 可以正确连接。如果使用 HTTP Basic 保护配置服务器，则可以将凭据配置为“用户名”和“密码”。如果 Config Server 有 context 路径，则可以设置“configPath”。 例如，对于 Eureka client 的配置服务器：</p>
<p><strong>bootstrap.yml.</strong></p>
<pre><code class="language-">eureka:
  instance:
    ...
    metadataMap:
      user: osufhalskjrtl
      password: lviuhlszvaorhvlo5847
      configPath: /config
</code></pre>
<h2 id="配置-client-快速失败"><a href="#config-client-fail-fast" id="config-client-fail-fast"></a> 10.3 配置 Client 快速失败</h2>
<p>在某些情况下，如果服务无法连接到配置服务器，则可能需要失败启动服务。如果这是所需的行为，请设置 bootstrap configuration property <code>spring.cloud.config.failFast=true</code>，client 将以 Exception 停止。</p>
<h2 id="配置-client-重试"><a href="#config-client-retry" id="config-client-retry"></a> 10.4 配置 Client 重试</h2>
<p>如果您希望应用程序启动时配置服务器偶尔可用，您可以要求它在发生故障后继续尝试。首先需要设置<code>spring.cloud.config.failFast=true</code>，然后需要将<code>spring-retry</code>和<code>spring-boot-starter-aop</code>添加到 classpath。默认行为是重试 6 次，初始退避间隔为 1000 毫秒，指数乘数为 1.1，用于后续退避。您可以使用<code>spring.cloud.config.retry.*</code> configuration properties 配置这些 properties(和其他)。</p>
<blockquote><p>要完全控制重试，请添加<code>@Bean</code>类型<code>RetryOperationsInterceptor</code>，其 id 为“configServerRetryInterceptor”。 Spring Retry 有一个<code>RetryInterceptorBuilder</code>，可以很容易地创建一个。</p>
</blockquote>
<h2 id="查找-remote-configuration-资源"><a href="#_locating_remote_configuration_resources" id="_locating_remote_configuration_resources"></a> 10.5 查找 Remote Configuration 资源</h2>
<p>Config Service 从<code>/{name}/{profile}/{label}</code>提供 property 源，其中 client 应用程序中的默认绑定是</p>
<ul>
<li>
<p>“name”= <code>${spring.application.name}</code></p>
</li>
<li>
<p>“profile”= <code>${spring.profiles.active}</code>(实际<code>Environment.getActiveProfiles()</code>)</p>
</li>
<li>
<p>“label”=“ master”</p>
</li>
</ul>
<p>所有这些都可以通过设置<code>spring.cloud.config.*</code>(其中<code>*</code>是“name”，“ profile”或“label”)来覆盖。 “标签”对于回滚到以前版本的 configuration 非常有用;使用默认的 Config Server implementation，它可以是 git 标签，branch name 或 commit id。 Label 也可以作为 comma-separated 列表提供，在这种情况下，列表中的项目将被尝试 on-by-one，直到成功。这在处理 feature 分支时非常有用，例如，当您可能希望将 config 标签与分支对齐时，可以将其设置为可选(e.g. <code>spring.cloud.config.label=myfeature,develop</code>)。</p>
<h2 id="安全"><a href="#_security_2" id="_security_2"></a> 10.6 安全</h2>
<p>如果您在服务器上使用 HTTP Basic 安全性，则 clients 只需要知道密码(如果不是默认值，则使用用户名)。您可以通过配置服务器 URI 或通过单独的用户名和密码 properties，e.g 来实现。</p>
<p><strong>bootstrap.yml.</strong></p>
<pre><code class="language-">spring:
  cloud:
    config:
     uri: https://user:[emailprotected]
</code></pre>
<p>要么</p>
<p><strong>bootstrap.yml.</strong></p>
<pre><code class="language-">spring:
  cloud:
    config:
     uri: https://myconfig.mycompany.com
     username: user
     password: secret
</code></pre>
<p><code>spring.cloud.config.password</code>和<code>spring.cloud.config.username</code>值会覆盖 URI 中提供的任何内容。</p>
<p>如果您在 Cloud Foundry 上部署应用程序，那么提供密码的最佳方式是通过服务凭据 e.g. 在 URI 中，从那以后它甚至不需要在配置文件中。本地工作的 example 和 Cloud Foundry 上名为“configserver”的 user-provided 服务：</p>
<p><strong>bootstrap.yml.</strong></p>
<pre><code class="language-">spring:
  cloud:
    config:
     uri: ${vcap.services.configserver.credentials.uri:http://user:[emailprotected]:8888}
</code></pre>
<p>如果你使用另一种形式的安全性，你可能需要<a href="multi__spring_cloud_config_client.html#custom-rest-template">提供 RestTemplate</a>到<code>ConfigServicePropertySourceLocator</code>(e.g. 通过在 bootstrap context 中抓取它并注入一个)。</p>
<h3 id="健康指标"><a href="#_health_indicator_3" id="_health_indicator_3"></a> 10.6.1 健康指标</h3>
<p>Config Client 提供 Spring Boot 运行状况指示器，尝试从 Config Server 加载 configuration。可以通过设置<code>health.config.enabled=false</code>来禁用运行状况指示器。出于性能原因，还会缓存响应。要生存的默认缓存 time 是 5 分钟。要更改该 value，请设置<code>health.config.time-to-live</code> property(以毫秒为单位)。</p>
<h3 id="提供自定义-resttemplate"><a href="#custom-rest-template" id="custom-rest-template"></a> 10.6.2 提供自定义 RestTemplate</h3>
<p>在某些情况下，您可能需要自定义从 client 对配置服务器发出的请求。通常，这涉及传递特殊的<code>Authorization</code> headers 以验证对服务器的请求。要提供自定义<code>RestTemplate</code>，请按照以下步骤操作。</p>
<ul>
<li>使用<code>PropertySourceLocator</code>的 implementation 创建一个新的 configuration bean。</li>
</ul>
<p><strong>CustomConfigServiceBootstrapConfiguration.java.</strong></p>
<pre><code class="language-">@Configuration
public class CustomConfigServiceBootstrapConfiguration {
    @Bean
    public ConfigServicePropertySourceLocator configServicePropertySourceLocator() {
        ConfigClientProperties clientProperties = configClientProperties();
       ConfigServicePropertySourceLocator configServicePropertySourceLocator =  new ConfigServicePropertySourceLocator(clientProperties);
        configServicePropertySourceLocator.setRestTemplate(customRestTemplate(clientProperties));
        return configServicePropertySourceLocator;
    }
}
</code></pre>
<ul>
<li>在<code>resources/META-INF</code>中创建一个名为<code>spring.factories</code>的文件并指定自定义 configuration。</li>
</ul>
<p><strong>spring.factories.</strong></p>
<pre><code class="language-">org.springframework.cloud.bootstrap.BootstrapConfiguration = com.my.config.client.CustomConfigServiceBootstrapConfiguration
</code></pre>
<h3 id="vault"><a href="#_vault" id="_vault"></a> 10.6.3 Vault</h3>
<p>当使用 Vault 作为配置服务器的后端时，client 将需要为服务器提供令牌以从 Vault 检索值。通过在<code>bootstrap.yml</code>中设置<code>spring.cloud.config.token</code>，可以在 client 中提供此标记。</p>
<p><strong>bootstrap.yml.</strong></p>
<pre><code class="language-">spring:
  cloud:
    config:
      token: YourVaultToken
</code></pre>
<h2 id="vault-1"><a href="#_vault_2" id="_vault_2"></a> 10.7 Vault</h2>
<h3 id="vault-中的嵌套键"><a href="#_nested_keys_in_vault" id="_nested_keys_in_vault"></a> 10.7.1 Vault 中的嵌套键</h3>
<p>Vault 支持将密钥嵌套在 Vault 中存储的 value 中。例如</p>
<p><code>echo -n '{"appA": {"secret": "appAsecret"}, "bar": "baz"}' | vault write secret/myapp -</code></p>
<p>此命令将向您的 Vault 写入 JSON object。要在 Spring 中访问这些值，您将使用传统的 dot(.) annotation。例如</p>
<pre><code class="language-">@Value("${appA.secret}")
String name = "World";
</code></pre>
<p>上面的 code 会将<code>name</code>变量设置为<code>appAsecret</code>。</p>
</div>
</div>
</section>
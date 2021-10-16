<section class="normal markdown-section">
<div id="content">
<h1>11. 服务发现：Eureka Clients</h1>
<div><ins class="adsbygoogle" style="display:block; text-align:center;" data-ad-layout="in-article" data-ad-format="fluid" data-ad-client="ca-pub-6108808167664152" data-ad-slot="6964403648"></ins>
<script>
(adsbygoogle = window.adsbygoogle || []).push({});
</script></div>
<div><p>Service Discovery 是基于微服务的 architecture 的 key 原则之一。尝试手动配置每个 client 或某种形式的约定可能非常难以做到并且可能非常脆弱。 Eureka 是 Netflix 服务发现服务器和 Client。可以配置和部署服务器以使其具有高可用性，每个服务器将注册服务的 state 复制到其他服务器。</p>
<h2 id="如何包含-eureka-client"><a href="#netflix-eureka-client-starter" id="netflix-eureka-client-starter"></a> 11.1 如何包含 Eureka Client</h2>
<p>要在项目中包含 Eureka Client，请使用带有 group <code>org.springframework.cloud</code>和 artifact id <code>spring-cloud-starter-netflix-eureka-client</code>的 starter。有关使用当前 Spring Cloud Release Train 设置 build 系统的详细信息，请参阅<a href="https://projects.spring.io/spring-cloud/" target="_blank" rel="noopener noreferrer">Spring Cloud 项目页面</a>。</p>
<h2 id="注册-eureka"><a href="#_registering_with_eureka" id="_registering_with_eureka"></a> 11.2 注册 Eureka</h2>
<p>当 client 向 Eureka 注册时，它提供 meta-data 自身，例如 host 和 port，运行状况指示器 URL，主页等.Eureka 从属于服务的每个实例接收心跳消息。如果心跳故障超过可配置的时间表，则通常会从注册表中删除该实例。</p>
<p>Example eureka client：</p>
<pre><code class="language-">@Configuration
@ComponentScan
@EnableAutoConfiguration
@RestController
public class Application {

    @RequestMapping("/")
    public String home() {
        return "Hello world";
    }

    public static void main(String[] args) {
        new SpringApplicationBuilder(Application.class).web(true).run(args);
    }

}
</code></pre>
<p>(i.e.完全正常 Spring Boot 应用程序)。通过 class 路径上的<code>spring-cloud-starter-netflix-eureka-client</code>，您的 application 将自动注册 Eureka 服务器。 Configuration 是定位 Eureka 服务器所必需的。 例：</p>
<p><strong>application.yml.</strong></p>
<pre><code class="language-">eureka:
  client:
    serviceUrl:
      defaultZone: http://localhost:8761/eureka/
</code></pre>
<p>其中“defaultZone”是一个 magic string fallback value，它为任何不表达首选项的 client 提供服务 URL(i.e.它是一个有用的默认值)。</p>
<p>从<code>Environment</code>获取的默认 application name(服务 ID)，virtual host 和 non-secure port 分别是<code>${spring.application.name}</code>，<code>${spring.application.name}</code>和<code>${server.port}</code>。</p>
<p>在 classpath 上有<code>spring-cloud-starter-netflix-eureka-client</code>使得 app 成为 Eureka“实例”(i.e.它自己注册)和“client”(i.e.它可以查询注册表以查找其他服务)。实例行为由<code>eureka.instance.*</code> configuration 键驱动，但是如果确保 application 具有<code>spring.application.name</code>(这是 Eureka 服务 ID 或 VIP 的默认值)，则默认值将正常。</p>
<p>有关可配置选项的更多详细信息，请参见<a href="https://github.com/spring-cloud/spring-cloud-netflix/tree/master/spring-cloud-netflix-eureka-client/src/main/java/org/springframework/cloud/netflix/eureka/EurekaInstanceConfigBean.java" target="_blank" rel="noopener noreferrer">EurekaInstanceConfigBean</a>和<a href="https://github.com/spring-cloud/spring-cloud-netflix/tree/master/spring-cloud-netflix-eureka-client/src/main/java/org/springframework/cloud/netflix/eureka/EurekaClientConfigBean.java" target="_blank" rel="noopener noreferrer">EurekaClientConfigBean</a>。</p>
<p>要禁用 Eureka Discovery Client，您可以将<code>eureka.client.enabled</code>设置为<code>false</code>。</p>
<h2 id="使用-eureka-server-进行身份验证"><a href="#_authenticating_with_the_eureka_server" id="_authenticating_with_the_eureka_server"></a> 11.3 使用 Eureka Server 进行身份验证</h2>
<p>如果其中一个<code>eureka.client.serviceUrl.defaultZone</code> URL 中嵌入了凭据(卷曲样式，如<code>http://user:[email protected]:8761/eureka</code>)，则 HTTP 基本身份验证将自动添加到 eureka client。对于更复杂的需求，您可以在其中创建<code>@Bean</code>类型的<code>DiscoveryClientOptionalArgs</code>和 inject <code>ClientFilter</code>实例，所有这些实例都将应用于 calls 从 client 到服务器。</p>
<blockquote><p>由于 Eureka 中存在限制，因此无法支持 per-server 基本身份验证凭据，因此仅使用找到的第一个集合。</p>
</blockquote>
<h2 id="状态页面和健康指标"><a href="#_status_page_and_health_indicator" id="_status_page_and_health_indicator"></a> 11.4 状态页面和健康指标</h2>
<p>Eureka 实例的状态页面和运行状况指示器分别默认为“/info”和“/health”，它们是 Spring Boot Actuator application 中有用 endpoints 的默认位置。如果使用 non-default context 路径或 servlet 路径(e.g. <code>server.servletPath=/foo</code>)，则需要更改这些，即使对于 Actuator application 也是如此示例：</p>
<p><strong>application.yml.</strong></p>
<pre><code class="language-">eureka:
  instance:
    statusPageUrlPath: ${server.servletPath}/info
    healthCheckUrlPath: ${server.servletPath}/health
</code></pre>
<p>这些链接显示在 clients 消耗的元数据中，并在某些情况下用于决定是否向 application 发送请求，因此如果它们准确，则会有所帮助。</p>
<blockquote><p>在 Dalston 中，还需要在更改 management context 路径时设置状态和运行状况检查 URL。在 Edgware 中删除了此要求。</p>
</blockquote>
<h2 id="注册安全-application"><a href="#_registering_a_secure_application" id="_registering_a_secure_application"></a> 11.5 注册安全 Application</h2>
<p>如果您希望通过 HTTPS 联系您的应用，则可以分别在<code>EurekaInstanceConfig</code>，即<code>eureka.instance.[nonSecurePortEnabled,securePortEnabled]=[false,true]</code>中设置两个标记。这将使 Eureka 发布实例信息，显示对安全通信的明确偏好。对于以这种方式配置的服务，Spring Cloud <code>DiscoveryClient</code>将始终 return 以<code>https</code>开头的 URI，Eureka(本机)实例信息将具有安全的运行状况检查 URL。</p>
<p>由于 Eureka 在内部工作的方式，它仍将发布状态和主页的 non-secure URL，除非您也明确覆盖这些 URL。您可以使用占位符来配置 eureka 实例 URL，e.g.</p>
<p><strong>application.yml.</strong></p>
<pre><code class="language-">eureka:
  instance:
    statusPageUrl: https://${eureka.hostname}/info
    healthCheckUrl: https://${eureka.hostname}/health
    homePageUrl: https://${eureka.hostname}/
</code></pre>
<p>(请注意，<code>${eureka.hostname}</code>是仅在 Eureka 的更高版本中可用的本机占位符.您也可以使用 Spring 占位符实现相同的功能，e.g. 使用<code>${eureka.instance.hostName}</code> .)</p>
<blockquote><p>如果您的应用程序在代理后运行，并且 SSL 终止在代理中(e.g. 如果您在 Cloud Foundry 或其他平台中作为服务运行)，则需要确保代理“转发”headers 被拦截和处理通过 application。 Spring Boot 应用程序中的嵌入式 Tomcat 容器如果具有'X-Forwarded - *`headers 的显式 configuration，则会自动执行此操作。这个错误的标志是你的应用程序呈现给自己的链接是错误的(错误的 host，port 或协议)。</p>
</blockquote>
<h2 id="eureka-的健康检查"><a href="#_eureka_s_health_checks" id="_eureka_s_health_checks"></a> 11.6 Eureka 的健康检查</h2>
<p>默认情况下，Eureka 使用 client 心跳来确定 client 是否已启动。除非另有说明，否则 Discovery Client 不会传播 Spring Boot Actuator 的 application 的当前运行状况检查状态。这意味着在成功注册后 Eureka 将始终宣布 application 处于'UP'state 状态。通过启用 Eureka 运行状况检查可以更改此行为，从而将 application 状态传播到 Eureka。因此，除了'UP'之外，其他每个 application 都不会向 state 中的 application 发送流量。</p>
<p><strong>application.yml.</strong></p>
<pre><code class="language-">eureka:
  client:
    healthcheck:
      enabled: true
</code></pre>
<blockquote><p><code>eureka.client.healthcheck.enabled=true</code>只应在<code>application.yml</code>中设置。在<code>bootstrap.yml</code>中设置 value 会导致不良副作用，例如在 eureka 中注册<code>UNKNOWN</code>状态。</p>
</blockquote>
<p>如果您需要对健康检查进行更多控制，可以考虑实施自己的<code>com.netflix.appinfo.HealthCheckHandler</code>。</p>
<h2 id="实例和-clients-的-117-eureka-元数据"><a href="#实例和-clients-的-117-eureka-元数据" id="实例和-clients-的-117-eureka-元数据"></a><span id="_eureka_metadata_for_instances_and_clients">实例和 Clients 的</span> 11.7 Eureka 元数据</h2>
<p>值得花一点时间了解 Eureka 元数据的工作方式，因此您可以在平台中使用它。有关于主机名，IP 地址，port numbers，状态页和运行状况检查等内容的标准元数据。这些发布在服务注册表中，并由 clients 用于以直接的方式联系服务。可以将其他元数据添加到<code>eureka.instance.metadataMap</code>中的实例注册中，这可以在 remote clients 中访问，但通常不会更改 client 的行为，除非它了解元数据的含义。下面介绍了几个特殊情况，其中 Spring Cloud 已经为元数据 map 赋予了意义。</p>
<h3 id="在-cloud-foundry-上使用-eureka"><a href="#_using_eureka_on_cloud_foundry" id="_using_eureka_on_cloud_foundry"></a> 11.7.1 在 Cloud Foundry 上使用 Eureka</h3>
<p>Cloud Foundry 有一个 global router，以便同一个应用程序的所有实例具有相同的主机名(在具有类似 architecture 的其他 PaaS 解决方案中也是如此)。这不一定是使用 Eureka 的障碍，但是如果你使用 router(推荐，甚至是强制性的，取决于你的平台的设置方式)，你需要显式设置主机名和 port numbers(安全或 non-secure)所以他们使用 router。您可能还想使用实例元数据，以便区分 client 上的实例(自定义负载均衡器中的 e.g. )。默认情况下，<code>eureka.instance.instanceId</code>是<code>vcap.application.instance_id</code>。例如：</p>
<p><strong>application.yml.</strong></p>
<pre><code class="language-">eureka:
  instance:
    hostname: ${vcap.application.uris[0]}
    nonSecurePort: 80
</code></pre>
<p>根据在 Cloud Foundry 实例中设置安全规则的方式，您可以注册并使用 host VM 的 IP 地址直接 service-to-service calls。 Pivotal Web Services(<a href="https://run.pivotal.io" target="_blank" rel="noopener noreferrer">PWS</a>)上尚未提供此 feature。</p>
<h3 id="在-aws-上使用-eureka"><a href="#_using_eureka_on_aws" id="_using_eureka_on_aws"></a> 11.7.2 在 AWS 上使用 Eureka</h3>
<p>如果计划将 application 部署到 AWS 云，则必须将 Eureka 实例配置为支持 AWS，这可以通过以下方式自定义<a href="https://github.com/spring-cloud/spring-cloud-netflix/tree/master/spring-cloud-netflix-eureka-client/src/main/java/org/springframework/cloud/netflix/eureka/EurekaInstanceConfigBean.java" target="_blank" rel="noopener noreferrer">EurekaInstanceConfigBean</a>来完成：</p>
<pre><code class="language-">@Bean
@Profile("!default")
public EurekaInstanceConfigBean eurekaInstanceConfig(InetUtils inetUtils) {
  EurekaInstanceConfigBean b = new EurekaInstanceConfigBean(inetUtils);
  AmazonInfo info = AmazonInfo.Builder.newBuilder().autoBuild("eureka");
  b.setDataCenterInfo(info);
  return b;
}
</code></pre>
<h3 id="更改-eureka-实例-id"><a href="#_changing_the_eureka_instance_id" id="_changing_the_eureka_instance_id"></a> 11.7.3 更改 Eureka 实例 ID</h3>
<p>一个 vanilla Netflix Eureka 实例注册的 ID 等于其 host name(i.e.每个 host 只有一个服务)。 Spring Cloud Eureka 提供了一个合理的默认值，如下所示：<code>${spring.cloud.client.hostname}:${spring.application.name}:${spring.application.instance_id:${server.port}}}</code>。对于 example <code>myhost:myappname:8080</code>。</p>
<p>使用 Spring Cloud，您可以通过在<code>eureka.instance.instanceId</code>中提供唯一标识符来覆盖它。例如：</p>
<p><strong>application.yml.</strong></p>
<pre><code class="language-">eureka:
  instance:
    instanceId: ${spring.application.name}:${vcap.application.instance_id:${spring.application.instance_id:${random.value}}}
</code></pre>
<p>有了这个元数据，并且在 localhost 上部署了多个服务实例，随机 value 将在那里启动以使该实例唯一。在 Cloud Foundry 中，<code>vcap.application.instance_id</code>将在 Spring Boot application 中自动填充，因此不需要随机 value。</p>
<h2 id="使用-eurekaclient"><a href="#_using_the_eurekaclient" id="_using_the_eurekaclient"></a> 11.8 使用 EurekaClient</h2>
<p>一旦您拥有了一个发现客户端的应用程序，您就可以使用它来发现<a href="multi_spring-cloud-eureka-server.html">Eureka Server</a>中的服务实例。一种方法是使用原生<code>com.netflix.discovery.EurekaClient</code>(而不是 Spring Cloud <code>DiscoveryClient</code>)，e.g.</p>
<pre><code class="language-">@Autowired
private EurekaClient discoveryClient;

public String serviceUrl() {
    InstanceInfo instance = discoveryClient.getNextServerFromEureka("STORES", false);
    return instance.getHomePageUrl();
}
</code></pre>
<blockquote><p>不要在<code>@PostConstruct</code>方法或<code>@Scheduled</code>方法中使用<code>EurekaClient</code>(或者可能尚未启动的任何地方)。它在<code>SmartLifecycle</code>(带有<code>phase=0</code>)中初始化，因此最早可以依赖它可用的是另一个具有更高相位的<code>SmartLifecycle</code>。</p>
</blockquote>
<h3 id="没有-jersey-的-eurekaclient"><a href="#_eurekaclient_without_jersey" id="_eurekaclient_without_jersey"></a> 11.8.1 没有 Jersey 的 EurekaClient</h3>
<p>默认情况下，EurekaClient 使用 Jersey 进行 HTTP 通信。如果您希望避免来自 Jersey 的依赖项，则可以将其从依赖项中排除。 Spring Cloud 将根据 Spring <code>RestTemplate</code>自动配置 transport client。</p>
<pre><code class="language-xm">&lt;dependency&gt;
    &lt;groupId&gt;org.springframework.cloud&lt;/groupId&gt;
    &lt;artifactId&gt;spring-cloud-starter-eureka&lt;/artifactId&gt;
    &lt;exclusions&gt;
        &lt;exclusion&gt;
            &lt;groupId&gt;com.sun.jersey&lt;/groupId&gt;
            &lt;artifactId&gt;jersey-client&lt;/artifactId&gt;
        &lt;/exclusion&gt;
        &lt;exclusion&gt;
            &lt;groupId&gt;com.sun.jersey&lt;/groupId&gt;
            &lt;artifactId&gt;jersey-core&lt;/artifactId&gt;
        &lt;/exclusion&gt;
        &lt;exclusion&gt;
            &lt;groupId&gt;com.sun.jersey.contribs&lt;/groupId&gt;
            &lt;artifactId&gt;jersey-apache-client4&lt;/artifactId&gt;
        &lt;/exclusion&gt;
    &lt;/exclusions&gt;
&lt;/dependency&gt;
</code></pre>
<h2 id="原生-netflix-eurekaclient-的替代品"><a href="#_alternatives_to_the_native_netflix_eurekaclient" id="_alternatives_to_the_native_netflix_eurekaclient"></a> 11.9 原生 Netflix EurekaClient 的替代品</h2>
<p>您不必使用原始 Netflix <code>EurekaClient</code>，通常在某种 wrapper 后面使用它会更方便。 Spring Cloud 支持<a href="multi_spring-cloud-feign.html">假装</a>(REST 客户端构建器)，并且<a href="multi_spring-cloud-ribbon.html">Spring RestTemplate</a>使用逻辑 Eureka 服务标识符(VIP)而不是物理 URL。要使用固定的物理服务器列表配置 Ribbon，您只需将<code>&lt;client&gt;.ribbon.listOfServers</code>设置为 comma-separated 物理地址(或主机名)列表，其中<code>&lt;client&gt;</code>是 client 的 ID。</p>
<p>您还可以使用<code>org.springframework.cloud.client.discovery.DiscoveryClient</code>为发现客户端提供一个简单的 API，该 API 不是特定于 Netflix，e.g.</p>
<pre><code class="language-">@Autowired
private DiscoveryClient discoveryClient;

public String serviceUrl() {
    List&lt;ServiceInstance&gt; list = discoveryClient.getInstances("STORES");
    if (list != null &amp;&amp; list.size() &gt; 0 ) {
        return list.get(0).getUri();
    }
    return null;
}
</code></pre>
<h2 id="为什么注册服务这么慢"><a href="#_why_is_it_so_slow_to_register_a_service" id="_why_is_it_so_slow_to_register_a_service"></a> 11.10 为什么注册服务这么慢？</h2>
<p>作为一个实例还涉及到注册表的周期性心跳(通过 client 的<code>serviceUrl</code>)，默认持续时间为 30 秒。服务器不可供 clients 发现，直到实例，服务器和 client 在其本地缓存中都具有相同的元数据(因此它可能需要 3 个心跳)。您可以使用<code>eureka.instance.leaseRenewalIntervalInSeconds</code>更改周期，这将加速 process 连接到其他服务的 process。在 production 中，最好坚持使用默认值，因为服务器内部有一些计算可以对租约续订期做出假设。</p>
<h2 id="区域"><a href="#_zones" id="_zones"></a> 11.11 区域</h2>
<p>如果您已将 Eureka clients 部署到多个 zones，那么您可能希望这些 clients 在另一个 zone 中尝试服务之前利用同一 zone 内的服务。为此，您需要正确配置 Eureka clients。</p>
<p>首先，您需要确保将 Eureka 服务器部署到每个 zone 并且它们是彼此的对等体。有关详细信息，请参阅<a href="multi_spring-cloud-eureka-server.html#spring-cloud-eureka-server-zones-and-regions">区域和地区</a>部分。</p>
<p>接下来，您需要告诉 Eureka 您的服务所在的区域。您可以使用<code>metadataMap</code> property 执行此操作。对于 example，如果将<code>service 1</code>部署到<code>zone 1</code>和<code>zone 2</code>，则需要在<code>service 1</code>中设置以下 Eureka properties</p>
<p><strong>Zone 1</strong>中的服务 1</p>
<pre><code class="language-">eureka.instance.metadataMap.zone = zone1
eureka.client.preferSameZoneEureka = true
</code></pre>
<p><strong>Zone 2</strong>中的服务 1</p>
<pre><code class="language-">eureka.instance.metadataMap.zone = zone2
eureka.client.preferSameZoneEureka = true
</code></pre>
</div>
</div>
</section>
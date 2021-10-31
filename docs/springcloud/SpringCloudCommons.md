<section class="normal markdown-section">
<div id="content">
<h1>3. Spring Cloud Commons：Common Abstractions</h1>
<div><ins class="adsbygoogle" style="display:block; text-align:center;" data-ad-layout="in-article" data-ad-format="fluid" data-ad-client="ca-pub-6108808167664152" data-ad-slot="6964403648"></ins>
<script>
(adsbygoogle = window.adsbygoogle || []).push({});
</script></div>
<div><p>服务发现，负载平衡和断路器等模式适用于所有 Spring Cloud clients 都可以使用的 common 抽象层，独立于 implementation(e.g. 发现通过 Eureka 或 Consul)。</p>
<h2 id="enablediscoveryclient"><a href="#__enablediscoveryclient" id="__enablediscoveryclient"></a> 3.1 @EnableDiscoveryClient</h2>
<p>Commons 提供<code>@EnableDiscoveryClient</code> annotation。这将通过<code>META-INF/spring.factories</code>查找<code>DiscoveryClient</code>接口的 implementations。 _ Discovery Client 的实现将在<code>org.springframework.cloud.client.discovery.EnableDiscoveryClient</code> key 下为<code>spring.factories</code>添加 configuration class。 <code>DiscoveryClient</code> __mplementations 的示例：<a href="https://cloud.spring.io/spring-cloud-netflix/" target="_blank" rel="noopener noreferrer">Spring Cloud Netflix Eureka</a>，<a href="https://cloud.spring.io/spring-cloud-consul/" target="_blank" rel="noopener noreferrer">Spring Cloud Consul Discovery</a>和<a href="https://cloud.spring.io/spring-cloud-zookeeper/" target="_blank" rel="noopener noreferrer">Spring Cloud Zookeeper Discovery</a>。</p>
<p>默认情况下，<code>DiscoveryClient</code>的_i实现 auto-register 本地 Spring Boot 服务器与 remote 发现服务器。可以通过在<code>@EnableDiscoveryClient</code>中设置<code>autoRegister=false</code>来禁用此功能。</p>
<blockquote><p>不再需要使用<code>@EnableDiscoveryClient</code>。只需在 classpath 上使用<code>DiscoveryClient</code> implementation 就可以使 Spring Boot application 向服务发现服务器注册。</p>
</blockquote>
<h3 id="健康指标"><a href="#_health_indicator" id="_health_indicator"></a> 3.1.1 健康指标</h3>
<p>Commons _创建一个 Spring Boot <code>HealthIndicator</code>，<code>DiscoveryClient</code> __mplement 可以通过实现<code>DiscoveryHealthIndicator</code>来参与。要禁用复合<code>HealthIndicator</code> set <code>spring.cloud.discovery.client.composite-indicator.enabled=false</code>。基于<code>DiscoveryClient</code>的泛型<code>HealthIndicator</code>是 auto-configured(</p>
<h2 id="serviceregistry"><a href="#_serviceregistry" id="_serviceregistry"></a> 3.2 ServiceRegistry</h2>
<p>Commons _now 提供<code>ServiceRegistry</code>接口，提供<code>register(Registration)</code>和<code>deregister(Registration)</code>等方法，允许您提供自定义注册服务。 <code>Registration</code>是标记界面。</p>
<pre><code class="language-">@Configuration
@EnableDiscoveryClient(autoRegister=false)
public class MyConfiguration {
    private ServiceRegistry registry;

    public MyConfiguration(ServiceRegistry registry) {
        this.registry = registry;
    }

    // called via some external process, such as an event or a custom actuator endpoint
    public void register() {
        Registration registration = constructRegistration();
        this.registry.register(registration);
    }
}
</code></pre>
<p>每个<code>ServiceRegistry</code> implementation 都有自己的<code>Registry</code> implementation。</p>
<ul>
<li>
<p><code>ZookeeperRegistration</code>与<code>ZookeeperServiceRegistry</code>一起使用</p>
</li>
<li>
<p><code>EurekaRegistration</code>与<code>EurekaServiceRegistry</code>一起使用</p>
</li>
<li>
<p><code>ConsulRegistration</code>与<code>ConsulServiceRegistry</code>一起使用</p>
</li>
</ul>
<p>如果您使用<code>ServiceRegistry</code>接口，则需要为正在使用的<code>ServiceRegistry</code> implementation 传递正确的<code>Registry</code> implementation。</p>
<h3 id="serviceregistry-auto-registration"><a href="#_serviceregistry_auto_registration" id="_serviceregistry_auto_registration"></a> 3.2.1 ServiceRegistry Auto-Registration</h3>
<p>默认情况下，<code>ServiceRegistry</code> implementation 将运行服务。要禁用该行为，有两种方法。您可以将<code>@EnableDiscoveryClient(autoRegister=false)</code>设置为永久禁用 auto-registration。您还可以设置<code>spring.cloud.service-registry.auto-registration.enabled=false</code>以通过 configuration 禁用该行为。</p>
<h3 id="service-registry-actuator-端点"><a href="#_service_registry_actuator_endpoint" id="_service_registry_actuator_endpoint"></a> 3.2.2 Service Registry Actuator 端点</h3>
<p>Commons 提供<code>/service-registry</code> actuator 端点。此端点依赖于 Spring Application Context 中的<code>Registration</code> bean。通过 GET 调用<code>/service-registry/instance-status</code>将_return <code>Registration</code>的状态。使用<code>String</code>正文对相同端点的 POST 会将当前<code>Registration</code>的状态更改为新的 value。请参阅您正在使用的<code>ServiceRegistry</code> implementation 的文档，其中包含用于更新状态的允许值以及为状态恢复的值。</p>
<h2 id="spring-resttemplate-作为负载均衡器-client"><a href="#_spring_resttemplate_as_a_load_balancer_client" id="_spring_resttemplate_as_a_load_balancer_client"></a> 3.3 Spring RestTemplate 作为负载均衡器 Client</h2>
<p><code>RestTemplate</code>可以自动配置为使用 ribbon。要创建负载均衡<code>RestTemplate</code>创建<code>RestTemplate</code> <code>@Bean</code>并使用<code>@LoadBalanced</code>限定符。</p>
<blockquote><p>不再通过 auto configuration 创建<code>RestTemplate</code> bean。它必须由单独的 applications 创建。</p>
</blockquote>
<pre><code class="language-">@Configuration
public class MyConfiguration {

    @LoadBalanced
    @Bean
    RestTemplate restTemplate() {
        return new RestTemplate();
    }
}

public class MyClass {
    @Autowired
    private RestTemplate restTemplate;

    public String doOtherStuff() {
        String results = restTemplate.getForObject("http://stores/stores", String.class);
        return results;
    }
}
</code></pre>
<p>URI 需要使用虚拟 host name(即 service name，而不是 host name)。 Ribbon client 用于创建完整的物理地址。有关如何设置<code>RestTemplate</code>的详细信息，请参阅<a href="https://github.com/spring-cloud/spring-cloud-netflix/blob/master/spring-cloud-netflix-core/src/main/java/org/springframework/cloud/netflix/ribbon/RibbonAutoConfiguration.java" target="_blank" rel="noopener noreferrer">RibbonAutoConfiguration</a>。</p>
<h3 id="重试失败的请求"><a href="#_retrying_failed_requests" id="_retrying_failed_requests"></a> 3.3.1 重试失败的请求</h3>
<p>可以将负载平衡<code>RestTemplate</code>配置为重试失败的请求。默认情况下，此逻辑被禁用，您可以通过将<a href="https://github.com/spring-projects/spring-retry" target="_blank" rel="noopener noreferrer">Spring 重试</a>添加到 application 的 classpath 来启用它。负载平衡<code>RestTemplate</code>将支持与重试失败请求相关的一些 Ribbon configuration 值。如果您想在 class 路径上使用 Spring Retry 禁用重试逻辑，则可以设置<code>spring.cloud.loadbalancer.retry.enabled=false</code>。您可以使用的 properties 是<code>client.ribbon.MaxAutoRetries</code>，<code>client.ribbon.MaxAutoRetriesNextServer</code>和<code>client.ribbon.OkToRetryOnAllOperations</code>。有关 properties 的作用的说明，请参阅<a href="https://github.com/Netflix/ribbon/wiki/Getting-Started#the-properties-file-sample-clientproperties" target="_blank" rel="noopener noreferrer">Ribbon 文档</a>。</p>
<p>如果要在重试中实现<code>BackOffPolicy</code>，则需要创建类型的 bean，并</p>
<pre><code class="language-">@Configuration
public class MyConfiguration {
    @Bean
    LoadBalancedBackOffPolicyFactory backOffPolciyFactory() {
        return new LoadBalancedBackOffPolicyFactory() {
            @Override
            public BackOffPolicy createBackOffPolicy(String service) {
        		return new ExponentialBackOffPolicy();
        	}
        };
    }
}
</code></pre>
<blockquote><p>上面示例中的<code>client</code>应替换为 Ribbon client 的 name。</p>
</blockquote>
<p>如果要在重试中添加一个或多个<code>RetryListener</code>，则需要创建类型的 bean，并_返回要用于给定服务的<code>RetryListener</code> array。</p>
<pre><code class="language-">@Configuration
public class MyConfiguration {
    @Bean
    LoadBalancedRetryListenerFactory retryListenerFactory() {
        return new LoadBalancedRetryListenerFactory() {
            @Override
            public RetryListener[] createRetryListeners(String service) {
                return new RetryListener[]{new RetryListener() {
                    @Override
                    public &lt;T, E extends Throwable&gt; boolean open(RetryContext context, RetryCallback&lt;T, E&gt; callback) {
                        //TODO Do you business...
                        return true;
                    }

                    @Override
                     public &lt;T, E extends Throwable&gt; void close(RetryContext context, RetryCallback&lt;T, E&gt; callback, Throwable throwable) {
                        //TODO Do you business...
                    }

                    @Override
                    public &lt;T, E extends Throwable&gt; void onError(RetryContext context, RetryCallback&lt;T, E&gt; callback, Throwable throwable) {
                        //TODO Do you business...
                    }
                }};
            }
        };
    }
}
</code></pre>
<h2 id="多个-resttemplate-objects"><a href="#_multiple_resttemplate_objects" id="_multiple_resttemplate_objects"></a> 3.4 多个 RestTemplate objects</h2>
<p>如果你想要一个非负载均衡的<code>RestTemplate</code>，那么创建一个<code>RestTemplate</code> bean 并 inject 它正常。要在创建<code>@Bean</code>时使用<code>@LoadBalanced</code>限定符来访问负载均衡<code>RestTemplate</code>。</p>
<blockquote><p>请注意下面 example 中 plain <code>RestTemplate</code>声明上的<code>@Primary</code> annotation，以消除不合格的<code>@Autowired</code>注入的歧义。</p>
</blockquote>
<pre><code class="language-">@Configuration
public class MyConfiguration {

    @LoadBalanced
    @Bean
    RestTemplate loadBalanced() {
        return new RestTemplate();
    }

    @Primary
    @Bean
    RestTemplate restTemplate() {
        return new RestTemplate();
    }
}

public class MyClass {
    @Autowired
    private RestTemplate restTemplate;

    @Autowired
    @LoadBalanced
    private RestTemplate loadBalanced;

    public String doOtherStuff() {
        return loadBalanced.getForObject("http://stores/stores", String.class);
    }

    public String doStuff() {
        return restTemplate.getForObject("http://example.com", String.class);
    }
}
</code></pre>
<blockquote><p>如果您看到<code>java.lang.IllegalArgumentException: Can not set org.springframework.web.client.RestTemplate field com.my.app.Foo.restTemplate to com.sun.proxy.$Proxy89</code>之类的错误，请尝试注入<code>RestOperations</code>或设置<code>spring.aop.proxyTargetClass=true</code>。</p>
</blockquote>
<h2 id="忽略网络接口"><a href="#ignore-network-interfaces" id="ignore-network-interfaces"></a> 3.5 忽略网络接口</h2>
<p>有时忽略某些命名的网络接口是有用的，因此可以从 Service Discovery 注册中排除它们(例如，在 Docker 容器中运行)。可以设置正则表达式列表，这将导致忽略所需的网络接口。以下 configuration 将忽略“docker0”接口和所有以“veth”开头的接口。</p>
<p><strong>application.yml.</strong></p>
<pre><code class="language-">spring:
  cloud:
    inetutils:
      ignoredInterfaces:
        - docker0
        - veth.*
</code></pre>
<p>您还可以使用正则表达式列表强制仅使用指定的网络地址：</p>
<p><strong>bootstrap.yml.</strong></p>
<pre><code class="language-">spring:
  cloud:
    inetutils:
      preferredNetworks:
        - 192.168
        - 10.0
</code></pre>
<p>您还可以强制仅使用站点本地地址。有关详细信息，请参阅<a href="https://docs.oracle.com/javase/8/docs/api/java/net/Inet4Address.html#isSiteLocalAddress--" target="_blank" rel="noopener noreferrer">Inet4Address.html.isSiteLocalAddress()</a>什么是站点本地地址。</p>
<p><strong>application.yml.</strong></p>
<pre><code class="language-">spring:
  cloud:
    inetutils:
      useOnlySiteLocalInterfaces: true
</code></pre>
<h2 id="http-client-factories"><a href="#http-clients" id="http-clients"></a> 3.6 HTTP Client Factories</h2>
<p>Spring Cloud Commons _provides beans for creating Apache HTTP clients(<code>ApacheHttpClientFactory</code>)以及 OK HTTP clients(<code>OkHttpClientFactory</code>)。只有在 classpath 上有 OK HTTP jar 时才会创建<code>OkHttpClientFactory</code> bean。另外，Spring Cloud Commons _provides beans 用于创建 clients 使用的连接_manage，<code>ApacheHttpClientConnectionManagerFactory</code>用于 Apache HTTP client，<code>OkHttpClientConnectionPoolFactory</code>用于 OK HTTP client。如果要自定义在下游项目中创建 HTTP clients 的方式，可以提供自己的 beans 实现。您还可以通过将<code>spring.cloud.httpclientfactories.apache.enabled</code>或<code>spring.cloud.httpclientfactories.ok.enabled</code>设置为<code>false</code>来禁用这些 beans 的创建。</p>
</div>
</div>
</section>
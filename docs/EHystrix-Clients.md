<section class="normal markdown-section">
<div id="content">
<h1>13. 断路器：Hystrix Clients</h1>
<div><ins class="adsbygoogle" style="display:block; text-align:center;" data-ad-layout="in-article" data-ad-format="fluid" data-ad-client="ca-pub-6108808167664152" data-ad-slot="6964403648"></ins>
<script>
(adsbygoogle = window.adsbygoogle || []).push({});
</script></div>
<div><p>Netflix 创建了一个名为<a href="https://github.com/Netflix/Hystrix" target="_blank" rel="noopener noreferrer">Hystrix</a>的 library，它实现了<a href="http://martinfowler.com/bliki/CircuitBreaker.html" target="_blank" rel="noopener noreferrer">断路器 pattern</a>。在微服务 architecture 中，拥有多层服务 calls 是常见的。</p>
<p><a href="" id="d0e3357"></a></p>
<p><strong>图 1_.微服务图</strong></p>
<p><img src="https://www.docs4dev.com/images/spring-cloud/Edgware.SR5/Hystrix.jpg" alt="Hystrix"></p>
<p>较低级别服务中的服务故障可能导致级联故障一直到用户。 calls 到特定服务大于<code>circuitBreaker.requestVolumeThreshold</code>(默认值：20 个请求)且故障百分比大于<code>circuitBreaker.errorThresholdPercentage</code>(默认值：&gt; 50％)在由<code>metrics.rollingStats.timeInMilliseconds</code>定义的滚动窗口中(默认值：10 秒)，电路打开并且呼叫没有。在出现错误和开路的情况下，开发人员可以提供后备。</p>
<p><a href="" id="d0e3377"></a></p>
<p><strong>图 1_.Hystrix 后备防止级联故障</strong></p>
<p><img src="https://www.docs4dev.com/images/spring-cloud/Edgware.SR5/HystrixFallback.jpg" alt="HystrixFallback"></p>
<p>有一个开放的电路可以阻止级联故障，并允许不堪重负或失败的服务 time 来治愈。回退可以是另一个 Hystrix 保护调用，静态数据或理智的空 value。回退可能会被链接，因此第一个回退会使一些其他业务调用反过来又回到静态数据。</p>
<h2 id="如何包含-hystrix"><a href="#netflix-hystrix-starter" id="netflix-hystrix-starter"></a> 13.1 如何包含 Hystrix</h2>
<p>要在项目中包含 Hystrix，请使用带有 group <code>org.springframework.cloud</code>和 artifact id <code>spring-cloud-starter-netflix-hystrix</code>的 starter。有关使用当前 Spring Cloud Release Train 设置 build 系统的详细信息，请参阅<a href="https://projects.spring.io/spring-cloud/" target="_blank" rel="noopener noreferrer">Spring Cloud 项目页面</a>。</p>
<p>Example boot app：</p>
<pre><code class="language-">@SpringBootApplication
@EnableCircuitBreaker
public class Application {

    public static void main(String[] args) {
        new SpringApplicationBuilder(Application.class).web(true).run(args);
    }

}

@Component
public class StoreIntegration {

    @HystrixCommand(fallbackMethod = "defaultStores")
    public Object getStores(Map&lt;String, Object&gt; parameters) {
        //do stuff that might fail
    }

    public Object defaultStores(Map&lt;String, Object&gt; parameters) {
        return /* something useful */;
    }
}
</code></pre>
<p><code>@HystrixCommand</code>由名为<a href="https://github.com/Netflix/Hystrix/tree/master/hystrix-contrib/hystrix-javanica" target="_blank" rel="noopener noreferrer">“爪哇”</a>的 Netflix contrib library 提供。 Spring Cloud 在连接到 Hystrix 断路器的代理中自动将 Spring beans 与注释包装在一起。断路器计算何时打开和关闭电路，以及在发生故障时该怎么做。</p>
<p>要配置<code>@HystrixCommand</code>，您可以将<code>commandProperties</code>属性与<code>@HystrixProperty</code> 注释列表一起使用。有关详细信息，请参阅<a href="https://github.com/Netflix/Hystrix/tree/master/hystrix-contrib/hystrix-javanica#configuration" target="_blank" rel="noopener noreferrer">这里</a>。有关 properties 的详细信息，请参阅<a href="https://github.com/Netflix/Hystrix/wiki/Configuration" target="_blank" rel="noopener noreferrer">Hystrix wiki</a>。</p>
<h2 id="传播安全-context-或使用-spring-scopes"><a href="#_propagating_the_security_context_or_using_spring_scopes" id="_propagating_the_security_context_or_using_spring_scopes"></a> 13.2 传播安全 Context 或使用 Spring Scopes</h2>
<p>如果您希望某些线程 local context 传播到<code>@HystrixCommand</code>，则默认声明将不起作用，因为它在线程池中执行该命令(如果超时)。您可以使用某些 configuration 切换 Hystrix 以使用与调用者相同的线程，或者通过要求它使用不同的“隔离策略”来直接在 annotation 中。例如：</p>
<pre><code class="language-">@HystrixCommand(fallbackMethod = "stubMyService",
    commandProperties = {
      @HystrixProperty(name="execution.isolation.strategy", value="SEMAPHORE")
    }
)
...
</code></pre>
<p>如果您使用<code>@SessionScope</code>或<code>@RequestScope</code>，则同样适用。您将知道何时需要执行此操作，因为运行时 exception 表示无法找到作用域 context。</p>
<p>您还可以选择将<code>hystrix.shareSecurityContext</code> property 设置为<code>true</code>。这样做会自动配置 Hystrix 并发策略插件 hook，它将<code>SecurityContext</code>从主线程传输到 Hystrix 命令使用的那个。 Hystrix 不允许注册多个 hystrix 并发策略，因此可以通过将自己的<code>HystrixConcurrencyStrategy</code>声明为 Spring bean 来获得扩展机制。 Spring Cloud 将在 Spring context 中查找 implementation 并将其包装在自己的插件中。</p>
<h2 id="健康指标"><a href="#_health_indicator_4" id="_health_indicator_4"></a> 13.3 健康指标</h2>
<p>连接断路器的 state 也暴露在调用 application 的<code>/health</code>端点中。</p>
<pre><code class="language-">{
    "hystrix": {
        "openCircuitBreakers": [
            "StoreIntegration::getStoresByLocationLink"
        ],
        "status": "CIRCUIT_OPEN"
    },
    "status": "UP"
}
</code></pre>
<h2 id="hystrix-metrics-stream"><a href="#_hystrix_metrics_stream" id="_hystrix_metrics_stream"></a> 13.4 Hystrix Metrics Stream</h2>
<p>要启用 Hystrix metrics 流，请包含对<code>spring-boot-starter-actuator</code>的依赖关系。这会将<code>/hystrix.stream</code>公开为 management 端点。</p>
<pre><code class="language-xm">&lt;dependency&gt;
        &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;
        &lt;artifactId&gt;spring-boot-starter-actuator&lt;/artifactId&gt;
    &lt;/dependency&gt;
</code></pre>
</div>
</div>
</section>
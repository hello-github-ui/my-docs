<section class="normal markdown-section">
                                
                                <p><a id="production-ready"></a></p>
<h1 id="五、spring-boot-actuator-生产就绪功能">五、Spring Boot Actuator: 生产就绪功能</h1>
<p>Spring Boot 包含许多其他功能，可帮助你在将应用程序推送到生产环境时监控和管理应用程序。你可以选择使用 HTTP 端点或 JMX 来管理和监控应用程序。审计、健康和指标收集也可以自动应用于你的应用程序。</p>
<p><a id="production-ready-enabling"></a></p>
<h2 id="52、启用生产就绪功能">52、启用生产就绪功能</h2>
<p><a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator" target="_blank"><code>spring-boot-actuator</code></a> 模块提供了 Spring Boot 的所有生产就绪功能。启用这些功能的最简单方法是添加 <code>spring-boot-starter-actuator</code> starter 到依赖中。</p>
<blockquote>

**Actuator 的定义**

Actuator 是制造术语，指的是用于移动或控制某物的机械装置。Actuator 可以通过一个小的变化产生大量的运动。

</blockquote>

<p>要将 actuator 添加到基于 Maven 的项目，请添加以下 starter 依赖项：</p>
<pre class="language-"><code class="lang-xml"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependencies</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependency</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>groupId</span><span class="token punctuation">&gt;</span></span>org.springframework.boot<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>groupId</span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>artifactId</span><span class="token punctuation">&gt;</span></span>spring-boot-starter-actuator<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>artifactId</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependency</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependencies</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<p>对于 Gradle，请使用以下声明：</p>
<pre class="language-"><code class="lang-groovy">dependencies <span class="token punctuation">{</span>
    <span class="token function">compile</span><span class="token punctuation">(</span><span class="token string">"org.springframework.boot:spring-boot-starter-actuator"</span><span class="token punctuation">)</span>
<span class="token punctuation">}</span>
</code></pre>
<p><a id="production-ready-endpoints"></a></p>
<h2 id="53、端点">53、端点</h2>
<p>通过 Actuator 端点，你可以监控应用程序并与之交互。Spring Boot 包含许多内置端点，也允许你添加自己的端点。例如，<code>health</code> 端点提供基本的应用程序健康信息。</p>
<p>可以<a href="#production-ready-endpoints-enabling-endpoints">启用或禁用</a>每个端点。它可控制当其 bean 存在于应用程序上下文中是否创建端点。要进行远程访问，必须<a href="#production-ready-endpoints-exposing-endpoints">通过 JMX 或 HTTP 暴露端点</a>。大多数应用程序选择 HTTP 方式，端点的 ID 以及 <code>/actuator</code> 的前缀映射到一个 URL。例如，默认情况下，<code>health</code> 端点映射到 <code>/actuator/health</code>。</p>
<p>可以使用以下与技术无关的端点：</p>
<table>
<thead>
<tr>
<th>ID</th>
<th>描述</th>
<th style="text-align:center">默认启用</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>auditevents</code></td>
<td>暴露当前应用程序的审计事件信息。</td>
<td style="text-align:center">是</td>
</tr>
<tr>
<td><code>beans</code></td>
<td>显示应用程序中所有 Spring bean 的完整列表。</td>
<td style="text-align:center">是</td>
</tr>
<tr>
<td><code>caches</code></td>
<td>暴露可用的缓存。</td>
<td style="text-align:center">是</td>
</tr>
<tr>
<td><code>conditions</code></td>
<td>显示在配置和自动配置类上评估的条件以及它们匹配或不匹配的原因。</td>
<td style="text-align:center">是</td>
</tr>
<tr>
<td><code>configprops</code></td>
<td>显示所有 <code>@ConfigurationProperties</code> 的校对清单。</td>
<td style="text-align:center">是</td>
</tr>
<tr>
<td><code>env</code></td>
<td>暴露 Spring <code>ConfigurableEnvironment</code> 中的属性。</td>
<td style="text-align:center">是</td>
</tr>
<tr>
<td><code>flyway</code></td>
<td>显示已应用的 Flyway 数据库迁移。</td>
<td style="text-align:center">是</td>
</tr>
<tr>
<td><code>health</code></td>
<td>显示应用程序健康信息</td>
<td style="text-align:center">是</td>
</tr>
<tr>
<td><code>httptrace</code></td>
<td>显示 HTTP 追踪信息（默认情况下，最后 100 个 HTTP 请求/响应交换）。</td>
<td style="text-align:center">是</td>
</tr>
<tr>
<td><code>info</code></td>
<td>显示应用程序信息。</td>
<td style="text-align:center">是</td>
</tr>
<tr>
<td><code>integrationgraph</code></td>
<td>显示 Spring Integration 图。</td>
<td style="text-align:center">是</td>
</tr>
<tr>
<td><code>loggers</code></td>
<td>显示和修改应用程序中日志记录器的配置。</td>
<td style="text-align:center">是</td>
</tr>
<tr>
<td><code>liquibase</code></td>
<td>显示已应用的 Liquibase 数据库迁移。</td>
<td style="text-align:center">是</td>
</tr>
<tr>
<td><code>metrics</code></td>
<td>显示当前应用程序的指标度量信息。</td>
<td style="text-align:center">是</td>
</tr>
<tr>
<td><code>mappings</code></td>
<td>显示所有 <code>@RequestMapping</code> 路径的整理清单。</td>
<td style="text-align:center">是</td>
</tr>
<tr>
<td><code>scheduledtasks</code></td>
<td>显示应用程序中的调度任务。</td>
<td style="text-align:center">是</td>
</tr>
<tr>
<td><code>sessions</code></td>
<td>允许从 Spring Session 支持的会话存储中检索和删除用户会话。当使用 Spring Session 的响应式 Web 应用程序支持时不可用。</td>
<td style="text-align:center">是</td>
</tr>
<tr>
<td><code>shutdown</code></td>
<td>正常关闭应用程序。</td>
<td style="text-align:center">否</td>
</tr>
<tr>
<td><code>threaddump</code></td>
<td>执行线程 dump。</td>
<td style="text-align:center">是</td>
</tr>
</tbody>
</table>
<p>如果你的应用程序是 Web 应用程序（Spring MVC、Spring WebFlux 或 Jersey），则可以使用以下附加端点：</p>
<table>
<thead>
<tr>
<th>ID</th>
<th>描述</th>
<th style="text-align:center">默认启用</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>heapdump</code></td>
<td>返回一个 <code>hprof</code> 堆 dump 文件。</td>
<td style="text-align:center">是</td>
</tr>
<tr>
<td><code>jolokia</code></td>
<td>通过 HTTP 暴露 JMX bean（当 Jolokia 在 classpath 上时，不适用于 WebFlux）。</td>
<td style="text-align:center">是</td>
</tr>
<tr>
<td><code>logfile</code></td>
<td>返回日志文件的内容（如果已设置 <code>logging.file</code> 或 <code>logging.path</code> 属性）。支持使用 HTTP <code>Range</code> 头来检索部分日志文件的内容。</td>
<td style="text-align:center">是</td>
</tr>
<tr>
<td><code>prometheus</code></td>
<td>以可以由 Prometheus 服务器抓取的格式暴露指标。</td>
<td style="text-align:center">是</td>
</tr>
</tbody>
</table>
<p>想了解有关 Actuator 端点及其请求和响应格式的更多信息，请参阅单独的 API 文档（<a href="https://docs.spring.io/spring-boot/docs/2.1.3.RELEASE/actuator-api//html" target="_blank">HTML</a> 或 <a href="https://docs.spring.io/spring-boot/docs/2.1.3.RELEASE/actuator-api//pdf/spring-boot-actuator-web-api.pdf" target="_blank">PDF</a>）。</p>
<p><a id="production-ready-endpoints-enabling-endpoints"></a></p>
<h3 id="531、启用端点">53.1、启用端点</h3>
<p>默认情况下，Actuator 启用除 <code>shutdown</code> 之外的所有端点。要配置端点的启用，请使用其 <code>management.endpoint.<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>id</span><span class="token punctuation">&gt;</span></span>.enabled</code> 属性。以下示例展示了如何启用关闭端点：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.endpoint.shutdown.enabled</span><span class="token attr-value"><span class="token punctuation">=</span>true</span>
</code></pre>
<p>如果你希望端点启用是选择性加入而不是选择性退出，请将 <code>management.endpoints.enabled-by-default</code> 属性设置为 <code>false</code>，并使用各个端点的 <code>enabled</code> 属性重新加入。以下示例启用 <code>info</code> 端点并禁用所有其他端点：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.endpoints.enabled-by-default</span><span class="token attr-value"><span class="token punctuation">=</span>false</span>
<span class="token constant">management.endpoint.info.enabled</span><span class="token attr-value"><span class="token punctuation">=</span>true</span>
</code></pre>
<p><strong>注意</strong></p>
<blockquote>
<p>已完全从应用程序上下文中删除已禁用的端点。如果只想更改端点所暴露的技术，请改用 <a href="#production-ready-endpoints-exposing-endpoints"><code>include</code> 和 <code>exclude</code> 属性</a>。</p>
</blockquote>
<p><a id="production-ready-endpoints-exposing-endpoints"></a></p>
<h3 id="532、暴露端点">53.2、暴露端点</h3>
<p>由于端点可能包含敏感信息，因此应仔细考虑何时暴露它们。下表显示了内置端点和默认暴露情况：</p>
<table>
<thead>
<tr>
<th>ID</th>
<th>JMX</th>
<th style="text-align:center">Web</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>auditevents</code></td>
<td>是</td>
<td style="text-align:center">否</td>
</tr>
<tr>
<td><code>beans</code></td>
<td>是</td>
<td style="text-align:center">否</td>
</tr>
<tr>
<td><code>caches</code></td>
<td>是</td>
<td style="text-align:center">否</td>
</tr>
<tr>
<td><code>conditions</code></td>
<td>是</td>
<td style="text-align:center">否</td>
</tr>
<tr>
<td><code>configprops</code></td>
<td>是</td>
<td style="text-align:center">否</td>
</tr>
<tr>
<td><code>env</code></td>
<td>是</td>
<td style="text-align:center">否</td>
</tr>
<tr>
<td><code>flyway</code></td>
<td>是</td>
<td style="text-align:center">否</td>
</tr>
<tr>
<td><code>health</code></td>
<td>是</td>
<td style="text-align:center">是</td>
</tr>
<tr>
<td><code>heapdump</code></td>
<td>N/A</td>
<td style="text-align:center">否</td>
</tr>
<tr>
<td><code>httptrace</code></td>
<td>是</td>
<td style="text-align:center">否</td>
</tr>
<tr>
<td><code>info</code></td>
<td>是</td>
<td style="text-align:center">是</td>
</tr>
<tr>
<td><code>integrationgraph</code></td>
<td>是</td>
<td style="text-align:center">否</td>
</tr>
<tr>
<td><code>jolokia</code></td>
<td>N/A</td>
<td style="text-align:center">否</td>
</tr>
<tr>
<td><code>logfile</code></td>
<td>N/A</td>
<td style="text-align:center">否</td>
</tr>
<tr>
<td><code>loggers</code></td>
<td>是</td>
<td style="text-align:center">否</td>
</tr>
<tr>
<td><code>liquibase</code></td>
<td>是</td>
<td style="text-align:center">否</td>
</tr>
<tr>
<td><code>metrics</code></td>
<td>是</td>
<td style="text-align:center">否</td>
</tr>
<tr>
<td><code>mappings</code></td>
<td>是</td>
<td style="text-align:center">否</td>
</tr>
<tr>
<td><code>prometheus</code></td>
<td>N/A</td>
<td style="text-align:center">否</td>
</tr>
<tr>
<td><code>scheduledtasks</code></td>
<td>是</td>
<td style="text-align:center">否</td>
</tr>
<tr>
<td><code>sessions</code></td>
<td>是</td>
<td style="text-align:center">否</td>
</tr>
<tr>
<td><code>shutdown</code></td>
<td>是</td>
<td style="text-align:center">否</td>
</tr>
<tr>
<td><code>threaddump</code></td>
<td>是</td>
<td style="text-align:center">否</td>
</tr>
</tbody>
</table>
<p>要更改暴露的端点，请使用以下特定的 <code>include</code> 和 <code>exclude</code> 属性：</p>
<table>
<thead>
<tr>
<th>属性</th>
<th>默认</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>management.endpoints.jmx.exposure.exclude</code></td>
<td></td>
</tr>
<tr>
<td><code>management.endpoints.jmx.exposure.include</code></td>
<td><code>*</code></td>
</tr>
<tr>
<td><code>management.endpoints.web.exposure.exclude</code></td>
<td></td>
</tr>
<tr>
<td><code>management.endpoints.web.exposure.include</code></td>
<td><code>info, health</code></td>
</tr>
</tbody>
</table>
<p><code>include</code> 属性列出了暴露的端点的 ID。<code>exclude</code> 属性列出了不应暴露的端点的 ID。<code>exclude</code> 属性优先于 <code>include</code> 属性。可以使用端点 ID 列表配置 <code>include</code> 和 <code>exclude</code> 属性。</p>
<p>例如，要停止通过 JMX 暴露所有端点并仅暴露 <code>health</code> 和 <code>info</code> 端点，请使用以下属性：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.endpoints.jmx.exposure.include</span><span class="token attr-value"><span class="token punctuation">=</span>health,info</span>
</code></pre>
<p><code>*</code> 可用于选择所有端点。例如，要通过 HTTP 暴露除 <code>env</code> 和 <code>beans</code> 之外的所有端点，请使用以下属性：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.endpoints.web.exposure.include</span><span class="token attr-value"><span class="token punctuation">=</span>*</span>
<span class="token constant">management.endpoints.web.exposure.exclude</span><span class="token attr-value"><span class="token punctuation">=</span>env,beans</span>
</code></pre>
<p><strong>注意</strong></p>
<blockquote>

`*` 在 YAML 中具有特殊含义，因此如果要包含（或排除）所有端点，请务必添加引号，如下所示：

```yaml
management:
  endpoints:
    web:
      exposure:
        include: "*"
```

</blockquote>

<p><strong>注意</strong></p>
<blockquote>
<p>如果你的应用程序是公开的，我们强烈建议你也<a href="#production-ready-endpoints-security">保护你的端点</a>。</p>
</blockquote>
<p><strong>提示</strong></p>
<blockquote>
<p>如果要在暴露端点时实现自己的策略，可以注册一个 <code>EndpointFilter</code> bean。</p>
</blockquote>
<p><a id="production-ready-endpoints-security"></a></p>
<h3 id="533、保护-http-端点">53.3、保护 HTTP 端点</h3>
<p>你应该像保护所有其他敏感 URL 一样注意保护 HTTP 端点。如果存在 Spring Security，则默认使用 Spring Security 的内容协商策略来保护端点。例如，如果你希望为 HTTP 端点配置自定义安全策略，只允许具有特定角色身份的用户访问它们，Spring Boot 提供了方便的 <code>RequestMatcher</code> 对象，可以与 Spring Security 结合使用。</p>
<p>典型的 Spring Security 配置可能如下：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Configuration</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">ActuatorSecurity</span> <span class="token keyword">extends</span> <span class="token class-name">WebSecurityConfigurerAdapter</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@Override</span>
    <span class="token keyword">protected</span> <span class="token keyword">void</span> <span class="token function">configure</span><span class="token punctuation">(</span><span class="token class-name">HttpSecurity</span> http<span class="token punctuation">)</span> <span class="token keyword">throws</span> <span class="token class-name">Exception</span> <span class="token punctuation">{</span>
        http<span class="token punctuation">.</span><span class="token function">requestMatcher</span><span class="token punctuation">(</span><span class="token class-name">EndpointRequest</span><span class="token punctuation">.</span><span class="token function">toAnyEndpoint</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">authorizeRequests</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
                <span class="token punctuation">.</span><span class="token function">anyRequest</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">hasRole</span><span class="token punctuation">(</span><span class="token string">"ENDPOINT_ADMIN"</span><span class="token punctuation">)</span>
                <span class="token punctuation">.</span><span class="token function">and</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
            <span class="token punctuation">.</span><span class="token function">httpBasic</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>上面的示例使用 <code>EndpointRequest.toAnyEndpoint()</code> 将请求与所有端点进行匹配，然后确保所有端点都具有 <code>ENDPOINT_ADMIN</code> 角色。<code>EndpointRequest</code> 上还提供了其他几种匹配器方法。有关详细信息，请参阅 API 文档（<a href="https://docs.spring.io/spring-boot/docs/2.1.3.RELEASE/actuator-api//html" target="_blank">HTML</a>或 <a href="https://docs.spring.io/spring-boot/docs/2.1.3.RELEASE/actuator-api//pdf/spring-boot-actuator-web-api.pdf" target="_blank">PDF</a>）。</p>
<p>如果应用程序部署在有防火墙的环境，你可能希望无需身份验证即可访问所有 Actuator 端点。你可以通过更改 <code>management.endpoints.web.exposure.include</code> 属性来执行此操作，如下所示：</p>
<p><strong>application.properties</strong></p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.endpoints.web.exposure.include</span><span class="token attr-value"><span class="token punctuation">=</span>*</span>
</code></pre>
<p>此外，如果存在 Spring Security，则需要添加自定义安全配置，以允许对端点进行未经身份验证的访问，如下所示：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Configuration</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">ActuatorSecurity</span> <span class="token keyword">extends</span> <span class="token class-name">WebSecurityConfigurerAdapter</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@Override</span>
    <span class="token keyword">protected</span> <span class="token keyword">void</span> <span class="token function">configure</span><span class="token punctuation">(</span><span class="token class-name">HttpSecurity</span> http<span class="token punctuation">)</span> <span class="token keyword">throws</span> <span class="token class-name">Exception</span> <span class="token punctuation">{</span>
        http<span class="token punctuation">.</span><span class="token function">requestMatcher</span><span class="token punctuation">(</span><span class="token class-name">EndpointRequest</span><span class="token punctuation">.</span><span class="token function">toAnyEndpoint</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">authorizeRequests</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
            <span class="token punctuation">.</span><span class="token function">anyRequest</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">permitAll</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p><a id="production-ready-endpoints-caching"></a></p>
<h3 id="534、配置端点">53.4、配置端点</h3>
<p>端点对不带参数读取操作的响应自动缓存。要配置端点缓存响应的时间长度，请使用其 <code>cache.time-to-live</code> 属性。以下示例将beans端点缓存的生存时间设置为10秒：</p>
<p><strong>application.properties</strong></p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.endpoint.beans.cache.time-to-live</span><span class="token attr-value"><span class="token punctuation">=</span>10s</span>
</code></pre>
<p><strong>注意</strong></p>
<blockquote>
<p>前缀 <code>management.endpoint.<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>name</span><span class="token punctuation">&gt;</span></span></code> 用于唯一标识配置的端点。</p>
</blockquote>
<p><strong>注意</strong></p>
<blockquote>
<p>在进行一个身份验证 HTTP 请求时，<code>Principal</code> 被视为端点的输入，因此不会缓存响应。</p>
</blockquote>
<p><a id="production-ready-endpoints-hypermedia"></a></p>
<h3 id="535、actuator-web-端点超媒体">53.5、Actuator Web 端点超媒体</h3>
<p>添加 <strong>discovery page</strong>，其包含指向所有端点的链接。默认情况下，<strong>discovery page</strong> 在 <code>/actuator</code> 上可访问。</p>
<p>配置一个自定义管理上下文（management context）路径时，<strong>discovery page</strong> 会自动从 <code>/actuator</code> 移动到管理上下文的根目录。例如，如果管理上下文路径是 <code>/management</code>，则可以从 <code>/management</code> 获取 discovery page。当管理上下文路径设置为 <code>/</code> 时，将禁用发现页面以防止与其他映射冲突。</p>
<p><a id="production-ready-endpoints-cors"></a></p>
<h3 id="536、跨域支持">53.6、跨域支持</h3>
<p><a href="https://en.wikipedia.org/wiki/Cross-origin_resource_sharing" target="_blank">跨源资源共享</a>（CORS）是一个 <a href="https://www.w3.org/TR/cors/" target="_blank">W3C 规范</a>，允许你以灵活的方式指定授权的跨域请求类型。如果你使用 Spring MVC 或 Spring WebFlux，则可以配置 Actuator 的 Web 端点以支持此类方案。</p>
<p>默认情况下 CORS 支持被禁用，仅在设置了 <code>management.endpoints.web.cors.allowed-origins</code> 属性后才启用 CORS 支持。以下配置允许来自 <code>example.com</code> 域的 GET 和 POST 调用：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.endpoints.web.cors.allowed-origins</span><span class="token attr-value"><span class="token punctuation">=</span>http://example.com</span>
<span class="token constant">management.endpoints.web.cors.allowed-methods</span><span class="token attr-value"><span class="token punctuation">=</span>GET,POST</span>
</code></pre>
<p><strong>提示</strong></p>
<blockquote>
<p>有关选项的完整列表，请参阅 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator-autoconfigure/src/main/java/org/springframework/boot/actuate/autoconfigure/endpoint/web/CorsEndpointProperties.java" target="_blank">CorsEndpointProperties</a>。</p>
</blockquote>
<p><a id="production-ready-endpoints-custom"></a></p>
<h3 id="537、实现自定义端点">53.7、实现自定义端点</h3>
<p>如果你添加一个使用了 <code>@Endpoint</code> 注解的 <code>@Bean</code>，则使用 <code>@ReadOperation</code>、<code>@WritOperation</code> 或 <code>@DeleteOperation</code> 注解的所有方法都将通过 JMX 自动暴露，并且在 Web 应用程序中也将通过 HTTP 暴露。可以使用 Jersey、Spring MVC 或 Spring WebFlux 通过 HTTP 暴露端点。</p>
<p>你还可以使用 <code>@JmxEndpoint</code> 或 <code>@WebEndpoint</code> 编写特定技术的端点。这些端点仅限于各自的技术。例如，<code>@WebEndpoint</code> 仅通过 HTTP 暴露，而不是 JMX。</p>
<p>你可以使用 <code>@EndpointWebExtension</code> 和 <code>@EndpointJmxExtension</code> 编写特定技术的扩展。通过这些注解，你可以提供特定技术的操作来扩充现有端点。</p>
<p>最后，如果你需要访问特定 Web 框架的功能，则可以实现 Servlet 或 Spring <code>@Controller</code> 和 <code>@RestController</code> 端点，但代价是它们无法通过 JMX 或使用其他 Web 框架。</p>
<p><a id="production-ready-endpoints-custom-input"></a></p>
<h4 id="5371、接收输入">53.7.1、接收输入</h4>
<p>端点上的操作通过参数接收输入。通过 Web 暴露时，这些参数的值取自 URL 的查询参数和 JSON 请求体。通过 JMX 暴露时，参数将映射到 MBean 操作的参数。默认情况下参数是必须的。可以使用 <code>@org.springframework.lang.Nullable</code> 对它们进行注解，使它们成为可选项。</p>
<p>JSON 请求体中的每个根属性都可以映射到端点的参数。考虑以下 JSON 请求体：</p>
<pre class="language-"><code class="lang-json"><span class="token punctuation">{</span>
    <span class="token property">"name"</span><span class="token operator">:</span> <span class="token string">"test"</span><span class="token punctuation">,</span>
    <span class="token property">"counter"</span><span class="token operator">:</span> <span class="token number">42</span>
<span class="token punctuation">}</span>
</code></pre>
<p>这可用于调用带有 <code>String name</code> 和 <code>int counter</code> 参数的写操作。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>由于端点与技术无关，因此只能在方法签名中指定简单类型。特别是不支持使用定义一个 <code>name</code> 和 <code>counter</code> 属性的自定义类型声明单个参数。</p>
</blockquote>
<p><strong>注意</strong></p>
<blockquote>
<p>要允许将输入映射到操作方法的参数，应使用 <code>-parameters</code> 编译实现端点的 Java 代码，并且应使用 <code>-java-parameters</code> 编译实现端点的 Kotlin 代码。如果你使用的是 Spring Boot 的 Gradle 插件，或者是 Maven 和 spring-boot-starter-parent，则它们会自动执行此操作。</p>
</blockquote>
<p><a id="production-ready-endpoints-custom-input-conversion"></a></p>
<h5 id="输入类型转换">输入类型转换</h5>
<p>如有必要，传递给端点操作方法的参数将自动转换为所需类型。在调用操作方法之前，使用 <code>ApplicationConversionService</code> 实例将通过 JMX 或 HTTP 请求接收的输入转换为所需类型。</p>
<p><a id="production-ready-endpoints-custom-web"></a></p>
<h4 id="5372、自定义-web-端点">53.7.2、自定义 Web 端点</h4>
<p><code>@Endpoint</code>、<code>@WebEndpoint</code> 或 <code>@EndpointWebExtension</code> 上的操作将使用 Jersey、Spring MVC 或 Spring WebFlux 通过 HTTP 自动暴露。</p>
<p><a id="production-ready-endpoints-custom-web-predicate"></a></p>
<h5 id="web-端点请求谓词">Web 端点请求谓词</h5>
<p>为 Web 暴露的端点上的每个操作自动生成请求谓词。</p>
<p><a id="production-ready-endpoints-custom-web-predicate-path"></a></p>
<h5 id="路径">路径</h5>
<p>谓词的路径由端点的 ID 和 Web 暴露的端点的基础路径确定。默认基础路径是 <code>/actuator</code>。例如，有 ID 为 <code>sessions</code> 的端点将使用 <code>/actuator/sessions</code> 作为其在谓词中的路径。</p>
<p>通过使用 <code>@Selector</code> 注解操作方法的一个或多个参数，可以进一步自定义路径。这样的参数作为路径变量添加到路径谓词中。调用端点操作时，变量的值将传递给操作方法。</p>
<p><a id="production-ready-endpoints-custom-web-predicate-http-method"></a></p>
<h5 id="http-方法">HTTP 方法</h5>
<p>谓词的 HTTP 方法由操作类型决定，如下表所示：</p>
<table>
<thead>
<tr>
<th>操作</th>
<th>HTTP 方法</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>@ReadOperation</code></td>
<td><code>GET</code></td>
</tr>
<tr>
<td><code>@WriteOperation</code></td>
<td><code>POST</code></td>
</tr>
<tr>
<td><code>@DeleteOperation</code></td>
<td><code>DELETE</code></td>
</tr>
</tbody>
</table>
<p><a id="production-ready-endpoints-custom-web-predicate-consumes"></a></p>
<h5 id="consume">Consume</h5>
<p>对于使用请求体的 <code>@WriteOperation</code>（HTTP <code>POST</code>），谓词的 consume 子句是 <code>application/vnd.spring-boot.actuator.v2+json, application/json</code>。对于所有其他操作，consume 子句为空。</p>
<p><a id="production-ready-endpoints-custom-web-predicate-produces"></a></p>
<h5 id="produce">Produce</h5>
<p>谓词的 produce 子句可以由 <code>@DeleteOperation</code>、<code>@ReadOperation</code> 和 <code>@WriteOperation</code> 注解的 <code>produce</code> 属性确定。该属性是可选的。如果未使用，则自动确定 produce 子句。</p>
<p>如果操作方法返回 <code>void</code> 或 <code>Void</code>，则 produce 子句为空。如果操作方法返回 <code>org.springframework.core.io.Resource</code>，则 produce 子句为 <code>application/octet-stream</code>。对于所有其他操作，produce 子句是 <code>application/vnd.spring-boot.actuator.v2+json, application/json</code>。</p>
<p><a id="production-ready-endpoints-custom-web-response-status"></a></p>
<h5 id="web-端点响应状态">Web 端点响应状态</h5>
<p>端点操作的默认响应状态取决于操作类型（读取、写入或删除）以及操作返回的内容（如果有）。</p>
<p><code>@ReadOperation</code> 返回一个值，响应状态为 200（OK）。如果它未返回值，则响应状态将为 404（未找到）。</p>
<p>如果 <code>@WriteOperation</code> 或 <code>@DeleteOperation</code> 返回值，则响应状态将为 200（OK）。如果它没有返回值，则响应状态将为 204（无内容）。</p>
<p>如果在没有必需参数的情况下调用操作，或者使用无法转换为所需类型的参数，则不会调用操作方法，并且响应状态将为 400（错误请求）。</p>
<p><a id="production-ready-endpoints-custom-web-range-requests"></a></p>
<h5 id="web-端点范围请求">Web 端点范围请求</h5>
<p>可用 HTTP 范围请求请求部分 HTTP 资源。使用 Spring MVC 或 Spring Web Flux 时，返回 <code>org.springframework.core.io.Resource</code> 的操作会自动支持范围请求。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>使用 Jersey 时不支持范围请求。</p>
</blockquote>
<p><a id="production-ready-endpoints-custom-web-security"></a></p>
<h5 id="web-端点安全">Web 端点安全</h5>
<p>Web 端点或特定 Web 的端点扩展上的操作可以接收当前的 <code>java.security.Principal</code> 或 <code>org.springframework.boot.actuate.endpoint.SecurityContext</code> 作为方法参数。前者通常与 <code>@Nullable</code> 结合使用，为经过身份验证和未经身份验证的用户提供不同的行为。后者通常用于使用其 <code>isUserInRole(String)</code> 方法执行授权检查。</p>
<p><a id="production-ready-endpoints-custom-servlet"></a></p>
<h4 id="5373、servlet-端点">53.7.3、Servlet 端点</h4>
<p>通过实现一个带有 <code>@ServletEndpoint</code> 注解的类，<code>Servlet</code> 可以作为端点暴露，该类也实现了 <code>Supplier<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>EndpointServlet</span><span class="token punctuation">&gt;</span></span></code>。Servlet 端点提供了与 Servlet 容器更深层次的集成，但代价是可移植性。它们旨在用于将现有 Servlet 作为端点暴露。对于新端点，应尽可能首选 <code>@Endpoint</code> 和 <code>@WebEndpoint</code> 注解。</p>
<p><a id="production-ready-endpoints-custom-controller"></a></p>
<h4 id="5374、控制器端点">53.7.4、控制器端点</h4>
<p><code>@ControllerEndpoint</code> 和 <code>@RestControllerEndpoint</code> 可用于实现仅由 Spring MVC 或 Spring WebFlux 暴露的端点。使用 Spring MVC 和 Spring WebFlux 的标准注解（如 <code>@RequestMapping</code> 和 <code>@GetMapping</code>）映射方法，并将端点的 ID 用作路径的前缀。控制器端点提供了与 Spring 的 Web 框架更深层次的集成，但代价是可移植性。应尽可能首选 <code>@Endpoint</code> 和 <code>@WebEndpoint</code> 注解。</p>
<p><a id="production-ready-health"></a></p>
<h3 id="538、健康信息">53.8、健康信息</h3>
<p>你可以使用健康信息来检查正在运行的应用程序的状态。监控软件经常在生产系统出现故障时使用它提醒某人。<code>health</code> 端点暴露的信息取决于 <code>management.endpoint.health.show-details</code> 属性，该属性可以使用以下值之一进行配置：</p>
<table>
<thead>
<tr>
<th>名称</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>never</code></td>
<td>永远不会显示细节。</td>
</tr>
<tr>
<td><code>when-authorized</code></td>
<td>详细信息仅向授权用户显示。可以使用 <code>management.endpoint.health.roles</code> 配置授权角色。</td>
</tr>
<tr>
<td><code>always</code></td>
<td>向所有用户显示详细信息。</td>
</tr>
</tbody>
</table>
<p>默认值为 <code>never</code>。当用户处于一个或多个端点的角色时，将被视为已获得授权。如果端点没有配置角色（默认值），则认为所有经过身份验证的用户都已获得授权。可以使用 <code>management.endpoint.health.roles</code> 属性配置角色。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>如果你已保护应用程序并希望使用 <code>always</code>，则安全配置必须允许经过身份验证和未经身份验证的用户对健康端点的访问。</p>
</blockquote>
<p>健康信息是从 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/HealthIndicatorRegistry.java" target="_blank"><code>HealthIndicatorRegistry</code></a> 的内容中收集的（默认情况下，<code>ApplicationContext</code> 中定义的所有 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/HealthIndicator.java" target="_blank"><code>HealthIndicator</code></a> 实例）。Spring Boot 包含许多自动配置的 <code>HealthIndicators</code>，你也可以自己编写。默认情况下，最终系统状态由 <code>HealthAggregator</code> 根据状态的有序列表对每个 <code>HealthIndicator</code> 的状态进行排序。排序列表中的第一个状态作为整体健康状态。如果没有 <code>HealthIndicator</code> 返回一个 <code>HealthAggregator</code> 已知的状态，则使用 <code>UNKNOWN</code> 状态。</p>
<p><strong>提示</strong></p>
<blockquote>
<p><code>HealthIndicatorRegistry</code> 可用于在运行时注册和注销健康指示器。</p>
</blockquote>
<p><a id="_auto_configured_healthindicators"></a></p>
<h4 id="5381、自动配置的-healthindicator">53.8.1、自动配置的 HealthIndicator</h4>
<p>适当时，Spring Boot 会自动配置以下 <code>HealthIndicator</code>：</p>
<table>
<thead>
<tr>
<th>名称</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr>
<td><a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/cassandra/CassandraHealthIndicator.java" target="_blank"><code>CassandraHealthIndicator</code></a></td>
<td>检查 Cassandra 数据库是否已启动。</td>
</tr>
<tr>
<td><a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/couchbase/CouchbaseHealthIndicator.java" target="_blank"><code>CouchbaseHealthIndicator</code></a></td>
<td>检查 Couchbase 集群是否已启动。</td>
</tr>
<tr>
<td><a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/system/DiskSpaceHealthIndicator.java" target="_blank"><code>DiskSpaceHealthIndicator</code></a></td>
<td>检查是否磁盘空间不足。</td>
</tr>
<tr>
<td><a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/jdbc/DataSourceHealthIndicator.java" target="_blank"><code>DataSourceHealthIndicator</code></a></td>
<td>检查是否可以获得与 <code>DataSource</code> 的连接。</td>
</tr>
<tr>
<td><a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/elasticsearch/ElasticsearchHealthIndicator.java" target="_blank"><code>ElasticsearchHealthIndicator</code></a></td>
<td>检查 Elasticsearch 集群是否已启动。</td>
</tr>
<tr>
<td><a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/influx/InfluxDbHealthIndicator.java" target="_blank"><code>InfluxDbHealthIndicator</code></a></td>
<td>检查 InfluxDB 服务器是否已启动。</td>
</tr>
<tr>
<td><a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/jms/JmsHealthIndicator.java" target="_blank"><code>JmsHealthIndicator</code></a></td>
<td>检查 JMS broker 是否已启动。</td>
</tr>
<tr>
<td><a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/mail/MailHealthIndicator.java" target="_blank"><code>MailHealthIndicator</code></a></td>
<td>检查邮件服务器是否已启动。</td>
</tr>
<tr>
<td><a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/mongo/MongoHealthIndicator.java" target="_blank"><code>MongoHealthIndicator</code></a></td>
<td>检查 Mongo 数据库是否已启动。</td>
</tr>
<tr>
<td><a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/neo4j/Neo4jHealthIndicator.java" target="_blank"><code>Neo4jHealthIndicator</code></a></td>
<td>检查 Neo4j 服务器是否已启动。</td>
</tr>
<tr>
<td><a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/amqp/RabbitHealthIndicator.java" target="_blank"><code>RabbitHealthIndicator</code></a></td>
<td>检查 Rabbit 服务器是否已启动。</td>
</tr>
<tr>
<td><a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/redis/RedisHealthIndicator.java" target="_blank"><code>RedisHealthIndicator</code></a></td>
<td>检查 Redis 服务器是否已启动。</td>
</tr>
<tr>
<td><a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/solr/SolrHealthIndicator.java" target="_blank"><code>SolrHealthIndicator</code></a></td>
<td>检查 Solr 服务器是否已启动。</td>
</tr>
</tbody>
</table>
<p><strong>提示</strong></p>
<blockquote>
<p>你可以通过设置 <code>management.health.defaults.enabled</code> 属性来禁用它们。</p>
</blockquote>
<p><a id="_writing_custom_healthindicators"></a></p>
<h4 id="5382、编写自定义-healthindicator">53.8.2、编写自定义 HealthIndicator</h4>
<p>要提供自定义健康信息，可以注册实现 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/HealthIndicator.java" target="_blank"><code>HealthIndicator</code></a> 接口的 Spring bean。你需要提供 <code>health()</code> 方法的实现并返回一个 <code>Health</code> 响应。<code>Health</code> 响应应包括一个状态，并且可以选择包括要显示的其他详细信息。以下代码展示了一个 HealthIndicator 实现示例：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>boot<span class="token punctuation">.</span>actuate<span class="token punctuation">.</span>health</span><span class="token punctuation">.</span><span class="token class-name">Health</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>boot<span class="token punctuation">.</span>actuate<span class="token punctuation">.</span>health</span><span class="token punctuation">.</span><span class="token class-name">HealthIndicator</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>stereotype</span><span class="token punctuation">.</span><span class="token class-name">Component</span><span class="token punctuation">;</span>

<span class="token annotation punctuation">@Component</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyHealthIndicator</span> <span class="token keyword">implements</span> <span class="token class-name">HealthIndicator</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@Override</span>
    <span class="token keyword">public</span> <span class="token class-name">Health</span> <span class="token function">health</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">int</span> errorCode <span class="token operator">=</span> <span class="token function">check</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">// 执行某些特定的健康检查</span>
        <span class="token keyword">if</span> <span class="token punctuation">(</span>errorCode <span class="token operator">!=</span> <span class="token number">0</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token keyword">return</span> <span class="token class-name">Health</span><span class="token punctuation">.</span><span class="token function">down</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">withDetail</span><span class="token punctuation">(</span><span class="token string">"Error Code"</span><span class="token punctuation">,</span> errorCode<span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">build</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
        <span class="token keyword">return</span> <span class="token class-name">Health</span><span class="token punctuation">.</span><span class="token function">up</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">build</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p><strong>注意</strong></p>
<blockquote>
<p>给定 <code>HealthIndicator</code> 的标识符是没有 <code>HealthIndicator</code> 后缀的 bean 的名称（如果存在）。在前面的示例中，健康信息在名为 <code>my</code> 的条目中可用。</p>
</blockquote>
<p>除了 Spring Boot 的预定义 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/Status.java" target="_blank"><code>Status</code></a> 类型之外，<code>Health</code> 还可以返回一个表示新系统状态的自定义 <code>Status</code>。在这种情况下，还需要提供 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/HealthAggregator.java" target="_blank"><code>HealthAggregator</code></a> 接口的自定义实现，或者必须使用 <code>management.health.status.order</code> 配置属性配置默认实现。</p>
<p>例如，假设在你的一个 <code>HealthIndicator</code> 实现中使用了代码为 <code>FATAL</code> 的新 <code>Status</code>。需要配置严重性顺序，请将以下属性添加到应用程序属性：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.health.status.order</span><span class="token attr-value"><span class="token punctuation">=</span>FATAL, DOWN, OUT_OF_SERVICE, UNKNOWN, UP</span>
</code></pre>
<p>响应中的 HTTP 状态码反映了整体运行状况（例如，<code>UP</code> 映射到 200，而 <code>OUT_OF_SERVICE</code> 和 <code>DOWN</code> 映射到 503）。如果通过 HTTP 访问健康端点，则可能还需要注册自定义状态映射。例如，以下属性将 <code>FATAL</code> 映射到 503（服务不可用）：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.health.status.http-mapping.FATAL</span><span class="token attr-value"><span class="token punctuation">=</span>503</span>
</code></pre>
<p><strong>提示</strong></p>
<blockquote>
<p>如果需要控制更多，可以定义自己的 <code>HealthStatusHttpMapper</code> bean。</p>
</blockquote>
<p>下表展示了内置状态的默认状态映射：</p>
<table>
<thead>
<tr>
<th>状态</th>
<th>映射</th>
</tr>
</thead>
<tbody>
<tr>
<td>DOWN</td>
<td>SERVICE_UNAVAILABLE (503)</td>
</tr>
<tr>
<td>OUT_OF_SERVICE</td>
<td>SERVICE_UNAVAILABLE (503)</td>
</tr>
<tr>
<td>UP</td>
<td>默认没有映射，因此状态码为 200</td>
</tr>
<tr>
<td>UNKNOWN</td>
<td>默认没有映射，因此状态码为 200</td>
</tr>
</tbody>
</table>
<p><a id="reactive-health-indicators"></a></p>
<h4 id="5383、响应式健康指示器">53.8.3、响应式健康指示器</h4>
<p>对于响应式应用程序，例如使用 Spring WebFlux 的应用程序，<code>ReactiveHealthIndicator</code> 提供了一个非阻塞的接口来获取应用程序健康信息。与传统的 <code>HealthIndicator</code> 类似，健康信息从 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/ReactiveHealthIndicatorRegistry.java" target="_blank"><code>ReactiveHealthIndicatorRegistry</code></a> 的内容中收集（默认情况下，<code>ApplicationContext</code> 中定义的所有 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/HealthIndicator.java" target="_blank"><code>HealthIndicator</code></a> 和 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/ReactiveHealthIndicator.java" target="_blank"><code>ReactiveHealthIndicator</code></a> 实例）。不检查响应式 API 的常规 <code>HealthIndicator</code>在弹性调度程序上执行。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>在响应式应用程序中，<code>ReactiveHealthIndicatorRegistry</code> 可用于在运行时注册和取消注册健康指示器。</p>
</blockquote>
<p>要从响应式 API 提供自定义健康信息，可以注册实现 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/ReactiveHealthIndicator.java" target="_blank"><code>ReactiveHealthIndicator</code></a> 接口的 Spring bean。以下代码展示了 <code>ReactiveHealthIndicator</code> 实现的示例：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Component</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyReactiveHealthIndicator</span> <span class="token keyword">implements</span> <span class="token class-name">ReactiveHealthIndicator</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@Override</span>
    <span class="token keyword">public</span> <span class="token class-name">Mono</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">Health</span><span class="token punctuation">&gt;</span></span> <span class="token function">health</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> <span class="token function">doHealthCheck</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token comment">// 执行一些特定的健康检查并返回一个 Mono&lt;Health&gt;</span>
            <span class="token punctuation">.</span><span class="token function">onErrorResume</span><span class="token punctuation">(</span>ex <span class="token operator">-&gt;</span> <span class="token class-name">Mono</span><span class="token punctuation">.</span><span class="token function">just</span><span class="token punctuation">(</span><span class="token keyword">new</span> <span class="token class-name">Health</span><span class="token punctuation">.</span><span class="token class-name">Builder</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">down</span><span class="token punctuation">(</span>ex<span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">build</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p><strong>提示</strong></p>
<blockquote>
<p>要自动处理错误，请考虑从 <code>AbstractReactiveHealthIndicator</code> 进行扩展。</p>
</blockquote>
<p><a id="_auto_configured_reactivehealthindicators"></a></p>
<h4 id="5384、自动配置的-reactivehealthindicator">53.8.4、自动配置的 ReactiveHealthIndicator</h4>
<p>适当时，Spring Boot 会自动配置以下 <code>ReactiveHealthIndicator</code>：</p>
<table>
<thead>
<tr>
<th>名称</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr>
<td><a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/cassandra/CassandraReactiveHealthIndicator.java" target="_blank"><code>CassandraReactiveHealthIndicator</code></a></td>
<td>检查 Cassandra 数据库是否已启动。</td>
</tr>
<tr>
<td><a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/couchbase/CouchbaseReactiveHealthIndicator.java" target="_blank"><code>CouchbaseReactiveHealthIndicator</code></a></td>
<td>检查 Couchbase 集群是否已启动。</td>
</tr>
<tr>
<td><a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/mongo/MongoReactiveHealthIndicator.java" target="_blank"><code>MongoReactiveHealthIndicator</code></a></td>
<td>检查 Mongo 数据库是否已启动。</td>
</tr>
<tr>
<td><a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/redis/RedisReactiveHealthIndicator.java" target="_blank"><code>RedisReactiveHealthIndicator</code></a></td>
<td>检查 Redis 服务器是否已启动。</td>
</tr>
</tbody>
</table>
<p><strong>提示</strong></p>
<blockquote>
<p>必要时，响应式指示器取代常规指示器。此外，任何未明确处理的 <code>HealthIndicator</code> 都会自动包装。</p>
</blockquote>
<p><a id="production-ready-application-info"></a></p>
<h3 id="539、应用程序信息">53.9、应用程序信息</h3>
<p>应用程序信息暴露从 <code>ApplicationContext</code> 中定义的所有 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/info/InfoContributor.java" target="_blank"><code>InfoContributor</code></a> bean 收集的各种信息。Spring Boot 包含许多自动配置的 <code>InfoContributor</code> bean，你可以编写自己的 bean。</p>
<p><a id="production-ready-application-info"></a></p>
<h4 id="5391、自动配置的-infocontributor">53.9.1、自动配置的 InfoContributor</h4>
<p>适当时，Spring Boot 会自动配置以下 <code>InfoContributor</code> bean：</p>
<table>
<thead>
<tr>
<th>名称</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr>
<td><a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/info/EnvironmentInfoContributor.java" target="_blank"><code>EnvironmentInfoContributor</code></a></td>
<td>在 <code>info</code> key 下显示 <code>Environment</code> 中的所有 key。</td>
</tr>
<tr>
<td><a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/info/GitInfoContributor.java" target="_blank"><code>GitInfoContributor</code></a></td>
<td>如果 <code>git.properties</code> 可用则暴露 git 信息。</td>
</tr>
<tr>
<td><a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/info/BuildInfoContributor.java" target="_blank"><code>BuildInfoContributor</code></a></td>
<td>如果 <code>META-INF/build-info.properties</code> 可用则暴露构建信息。</td>
</tr>
</tbody>
</table>
<p><strong>提示</strong></p>
<blockquote>
<p>可以通过设置 <code>management.info.defaults.enabled</code> 属性来禁用它们。</p>
</blockquote>
<p><a id="production-ready-application-info-env"></a></p>
<h4 id="5392、自定义应用程序信息">53.9.2、自定义应用程序信息</h4>
<p>你可以通过设置 <code>info.*</code> 字符串属性来自定义 <code>info</code>端点暴露的数据。<code>info</code> key 下的所有 <code>Environment</code> 属性都会自动暴露。例如，你可以将以下设置添加到 <code>application.properties</code> 文件中：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">info.app.encoding</span><span class="token attr-value"><span class="token punctuation">=</span>UTF-8</span>
<span class="token constant">info.app.java.source</span><span class="token attr-value"><span class="token punctuation">=</span>1.8</span>
<span class="token constant">info.app.java.target</span><span class="token attr-value"><span class="token punctuation">=</span>1.8</span>
</code></pre>
<p><strong>提示</strong></p>
<blockquote>

你可以在[构建时扩展 info 属性](how-to.md#howto-automatic-expansion)，而不是对这些值进行硬编码。
假设你使用 Maven，你可以按如下方式重写前面的示例：

```ini
info.app.encoding=@project.build.sourceEncoding@
info.app.java.source=@java.version@
info.app.java.target=@java.version@
```

</blockquote>

<p><a id="production-ready-application-info-git"></a></p>
<h4 id="5393、git-提交信息">53.9.3、Git 提交信息</h4>
<p><code>info</code> 端点的另一个有用功能是它能够在构建项目时发布 git 源码仓库相关的状态的信息。如果 <code>GitProperties</code> bean 可用，则暴露 <code>git.branch</code>、<code>git.commit.id</code> 和 <code>git.commit.time</code> 属性。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>如果 <code>git.properties</code> 文件在 classpath 的根目录中可用，则会自动配置 <code>GitProperties</code> bean。有关更多详细信息，请参阅<a href="how-to.md#howto-git-info"><strong>生成 git 信息</strong></a>。</p>
</blockquote>
<p>如果要显示完整的 git 信息（即 <code>git.properties</code> 的完整内容），请使用 <code>management.info.git.mode</code> 属性，如下所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.info.git.mode</span><span class="token attr-value"><span class="token punctuation">=</span>full</span>
</code></pre>
<p><a id="production-ready-application-info-build"></a></p>
<h4 id="5394、构建信息">53.9.4、构建信息</h4>
<p>如果 <code>BuildProperties</code> bean 可用，则 <code>info</code> 端点还可以发布构建相关的信息。如果 classpath 中有 <code>META-INF/build-info.properties</code> 文件，则会发生这种情况。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>Maven 和 Gradle 插件都可以生成该文件。有关更多详细信息，请参阅<a href="how-to.md#howto-build-info"><strong>生成构建信息</strong></a>。</p>
</blockquote>
<p><a id="production-ready-application-info-build"></a></p>
<h4 id="5395、编写自定义-infocontributor">53.9.5、编写自定义 InfoContributor</h4>
<p>要提供自定义应用程序信息，可以注册实现 <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.3.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/info/InfoContributor.java" target="_blank"><code>InfoContributor</code></a> 接口的 Spring bean。</p>
<p>以下示例提供了具有单个值的 <code>example</code> 条目：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">import</span> <span class="token namespace">java<span class="token punctuation">.</span>util</span><span class="token punctuation">.</span><span class="token class-name">Collections</span><span class="token punctuation">;</span>

<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>boot<span class="token punctuation">.</span>actuate<span class="token punctuation">.</span>info</span><span class="token punctuation">.</span><span class="token class-name">Info</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>boot<span class="token punctuation">.</span>actuate<span class="token punctuation">.</span>info</span><span class="token punctuation">.</span><span class="token class-name">InfoContributor</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token namespace">org<span class="token punctuation">.</span>springframework<span class="token punctuation">.</span>stereotype</span><span class="token punctuation">.</span><span class="token class-name">Component</span><span class="token punctuation">;</span>

<span class="token annotation punctuation">@Component</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">ExampleInfoContributor</span> <span class="token keyword">implements</span> <span class="token class-name">InfoContributor</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@Override</span>
    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">contribute</span><span class="token punctuation">(</span><span class="token class-name">Info</span><span class="token punctuation">.</span><span class="token class-name">Builder</span> builder<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        builder<span class="token punctuation">.</span><span class="token function">withDetail</span><span class="token punctuation">(</span><span class="token string">"example"</span><span class="token punctuation">,</span>
                <span class="token class-name">Collections</span><span class="token punctuation">.</span><span class="token function">singletonMap</span><span class="token punctuation">(</span><span class="token string">"key"</span><span class="token punctuation">,</span> <span class="token string">"value"</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>如果访问 <code>info</code> 端点，你应该能看到包含以下附加条目的响应：</p>
<pre class="language-"><code class="lang-json"><span class="token punctuation">{</span>
    <span class="token property">"example"</span><span class="token operator">:</span> <span class="token punctuation">{</span>
        <span class="token property">"key"</span> <span class="token operator">:</span> <span class="token string">"value"</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<p><a id="production-ready-monitoring"></a></p>
<h2 id="54、通过-http-监控和管理">54、通过 HTTP 监控和管理</h2>
<p>如果你正在开发 Web 应用程序，Spring Boot Actuator 会自动配置所有已启用的端点以通过 HTTP 暴露。默认约定是使用前缀为 <code>/actuator</code> 的端点的 <code>id</code> 作为 URL 路径。例如，<code>health</code> 以 <code>/actuator/health</code> 暴露。提示：Spring MVC、Spring WebFlux 和 Jersey 本身支持 Actuator。</p>
<p><a id="production-ready-customizing-management-server-context-path"></a></p>
<h3 id="541、自定义-management-端点路径">54.1、自定义 Management 端点路径</h3>
<p>有时，自定义 management 端点的前缀很有用。例如，你的应用程序可能已将 <code>/actuator</code> 用于其他目的。你可以使用 <code>management.endpoints.web.base-path</code> 属性更改 management 端点的前缀，如下所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.endpoints.web.base-path</span><span class="token attr-value"><span class="token punctuation">=</span>/manage</span>
</code></pre>
<p>前面的 <code>application.properties</code> 示例将端点从 <code>/actuator/{id}</code> 更改为 <code>/manage/{id}</code>（例如，<code>/manage/info</code>）。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>除非已将 management 端口配置为<a href="production-ready-customizing-management-server-port">使用其他 HTTP 端口暴露端点</a>，否则 <code>management.endpoints.web.base-path</code> 与 <code>server.servlet.context-path</code> 相关联。如果配置了 <code>management.server.port</code>，则 <code>management.endpoints.web.base-path</code> 与 <code>management.server.servlet.context-path</code> 相关联。</p>
</blockquote>
<p>如果要将端点映射到其他路径，可以使用 <code>management.endpoints.web.path-mapping</code> 属性。</p>
<p>以下示例将 <code>/actuator/health</code> 重新映射到 <code>/healthcheck</code>：</p>
<p><strong>application.properties</strong></p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.endpoints.web.base-path</span><span class="token attr-value"><span class="token punctuation">=</span>/</span>
<span class="token constant">management.endpoints.web.path-mapping.health</span><span class="token attr-value"><span class="token punctuation">=</span>healthcheck</span>
</code></pre>
<p><a id="production-ready-customizing-management-server-port"></a></p>
<h3 id="542、自定义-management-服务器端口">54.2、自定义 Management 服务器端口</h3>
<p>使用默认 HTTP 端口暴露 management 端点是基于云部署的明智选择。但是，如果应用程序是在自己的数据中心内运行，你可能更喜欢使用其他 HTTP 端口暴露端点。</p>
<p>你可以设置 <code>management.server.port</code> 属性以更改 HTTP 端口，如下所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.server.port</span><span class="token attr-value"><span class="token punctuation">=</span>8081</span>
</code></pre>
<p><a id="production-ready-management-specific-ssl"></a></p>
<h3 id="543、配置-management-的-ssl">54.3、配置 Management 的 SSL</h3>
<p>当配置为使用自定义端口时，还可以使用各种 <code>management.server.ssl.*</code> 属性为 management 服务器配置自己的 SSL。例如，这样做可以在主应用程序使用 HTTPS 时可通过 HTTP 使用 management 服务器，如以下属性设置所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">server.port</span><span class="token attr-value"><span class="token punctuation">=</span>8443</span>
<span class="token constant">server.ssl.enabled</span><span class="token attr-value"><span class="token punctuation">=</span>true</span>
<span class="token constant">server.ssl.key-store</span><span class="token attr-value"><span class="token punctuation">=</span>classpath:store.jks</span>
<span class="token constant">server.ssl.key-password</span><span class="token attr-value"><span class="token punctuation">=</span>secret</span>
<span class="token constant">management.server.port</span><span class="token attr-value"><span class="token punctuation">=</span>8080</span>
<span class="token constant">management.server.ssl.enabled</span><span class="token attr-value"><span class="token punctuation">=</span>false</span>
</code></pre>
<p>或者，主服务器和 management 服务器都可以使用 SSL，但他们的 key store 不同，如下所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">server.port</span><span class="token attr-value"><span class="token punctuation">=</span>8443</span>
<span class="token constant">server.ssl.enabled</span><span class="token attr-value"><span class="token punctuation">=</span>true</span>
<span class="token constant">server.ssl.key-store</span><span class="token attr-value"><span class="token punctuation">=</span>classpath:main.jks</span>
<span class="token constant">server.ssl.key-password</span><span class="token attr-value"><span class="token punctuation">=</span>secret</span>
<span class="token constant">management.server.port</span><span class="token attr-value"><span class="token punctuation">=</span>8080</span>
<span class="token constant">management.server.ssl.enabled</span><span class="token attr-value"><span class="token punctuation">=</span>true</span>
<span class="token constant">management.server.ssl.key-store</span><span class="token attr-value"><span class="token punctuation">=</span>classpath:management.jks</span>
<span class="token constant">management.server.ssl.key-password</span><span class="token attr-value"><span class="token punctuation">=</span>secret</span>
</code></pre>
<p><a id="production-ready-customizing-management-server-address"></a></p>
<h3 id="544、配置-management-服务器地址">54.4、配置 Management 服务器地址</h3>
<p>你可以通过设置 <code>management.server.address</code> 属性来自定义 management 端点可用的地址。如果你只想在内部或操作的网络上监听或仅监听来自 <code>localhost</code> 的连接，那么这样做会非常有用。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>仅当端口与主服务器端口不同时，才能监听不同的地址。</p>
</blockquote>
<p>以下 <code>application.properties</code> 示例不允许远程连接 management：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.server.port</span><span class="token attr-value"><span class="token punctuation">=</span>8081</span>
<span class="token constant">management.server.address</span><span class="token attr-value"><span class="token punctuation">=</span>127.0.0.1</span>
</code></pre>
<p><a id="production-ready-disabling-http-endpoints"></a></p>
<h3 id="545、禁用-http-端点">54.5、禁用 HTTP 端点</h3>
<p>如果你不希望通过 HTTP 暴露端点，则可以将 management 端口设置为 <code>-1</code>，如下所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.server.port</span><span class="token attr-value"><span class="token punctuation">=</span>-1</span>
</code></pre>
<p>这可以使用 <code>management.endpoints.web.exposure.exclude</code> 属性来实现，如下所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.endpoints.web.exposure.exclude</span><span class="token attr-value"><span class="token punctuation">=</span>*</span>
</code></pre>
<p><a id="production-ready-jmx"></a></p>
<h2 id="55、通过-jmx-监控和管理">55、通过 JMX 监控和管理</h2>
<p>Java 管理扩展（Java Management Extensions，JMX）提供了一种监控和管理应用程序的标准机制。默认情况下，Spring Boot 将 management 端点暴露为 <code>org.springframework.boot</code> 域下的 JMX MBean。</p>
<p><a id="production-ready-custom-mbean-names"></a></p>
<h3 id="551、自定义-mbean-名称">55.1、自定义 MBean 名称</h3>
<p>MBean 的名称通常是从端点的 <code>id</code> 生成的。例如，<code>health</code> 端点公开为 <code>org.springframework.boot:type=Endpoint,name=Health</code>。</p>
<p>如果你的应用程序包含多个 Spring <code>ApplicationContext</code>，可能会发生名称冲突。要解决此问题，可以将 <code>spring.jmx.unique-names</code> 属性设置为 <code>true</code>，以保证 MBean 名称始终唯一。</p>
<p>你还可以自定义暴露端点的 JMX 域。以下设置展示了在 <code>application.properties</code> 中执行此操作的示例：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.jmx.unique-names</span><span class="token attr-value"><span class="token punctuation">=</span>true</span>
<span class="token constant">management.endpoints.jmx.domain</span><span class="token attr-value"><span class="token punctuation">=</span>com.example.myapp</span>
</code></pre>
<p><a id="production-ready-disable-jmx-endpoints"></a></p>
<h3 id="552、禁用-jmx-端点">55.2、禁用 JMX 端点</h3>
<p>如果你不想通过 JMX 暴露端点，可以将 <code>management.endpoints.jmx.exposure.exclude</code> 属性设置为 <code>*</code>，如下所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.endpoints.jmx.exposure.exclude</span><span class="token attr-value"><span class="token punctuation">=</span>*</span>
</code></pre>
<p><a id="production-ready-jolokia"></a></p>
<h3 id="553、通过-http-使用-jolokia-访问-jmx">55.3、通过 HTTP 使用 Jolokia 访问 JMX</h3>
<p>Jolokia 是一个 JMX-HTTP 桥，它提供了一种访问 JMX bean 的新方式。要使用 Jolokia，请引入依赖：<code>org.jolokia:jolokia-core</code>。例如，使用 Maven，你将添加以下依赖：</p>
<pre class="language-"><code class="lang-xml"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>dependency</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>groupId</span><span class="token punctuation">&gt;</span></span>org.jolokia<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>groupId</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>artifactId</span><span class="token punctuation">&gt;</span></span>jolokia-core<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>artifactId</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>dependency</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<p>之后可以通过将 <code>jolokia</code> 或 <code>*</code> 添加到 <code>management.endpoints.web.exposure.include</code> 属性来暴露 Jolokia 端点。最后，你可以在 management HTTP 服务器上使用 <code>/actuator/jolokia</code> 访问它。</p>
<p><a id="production-ready-customizing-jolokia"></a></p>
<h4 id="5531、自定义-jolokia">55.3.1、自定义 Jolokia</h4>
<p>Jolokia 有许多设置，你可以通过设置 servlet 参数来使用传统方式进行配置。使用 Spring Boot 时，你可以使用 <code>application.properties</code> 文件配置。请在参数前加上 <code>management.endpoint.jolokia.config</code>。如下所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.endpoint.jolokia.config.debug</span><span class="token attr-value"><span class="token punctuation">=</span>true</span>
</code></pre>
<p><a id="production-ready-disabling-jolokia"></a></p>
<h4 id="5532、禁用-jolokia">55.3.2、禁用 Jolokia</h4>
<p>如果你使用 Jolokia 但不希望 Spring Boot 配置它，请将 <code>management.endpoint.jolokia.enabled</code> 属性设置为 <code>false</code>，如下所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.endpoint.jolokia.enabled</span><span class="token attr-value"><span class="token punctuation">=</span>false</span>
</code></pre>
<p><a id="production-ready-loggers"></a></p>
<h2 id="56、日志记录器">56、日志记录器</h2>
<p>Spring Boot Actuator 有可在运行时查看和配置应用程序日志级别的功能。你可以查看全部或单个日志记录器的配置，该配置由显式配置的日志记录级别以及日志记录框架为其提供的有效日志记录级别组成。这些级别可以是以下之一：</p>
<ul>
<li><code>TRACE</code></li>
<li><code>DEBUG</code></li>
<li><code>INFO</code></li>
<li><code>WARN</code></li>
<li><code>ERROR</code></li>
<li><code>FATAL</code></li>
<li><code>OFF</code></li>
<li><code>null</code></li>
</ul>
<p><code>null</code> 表示没有显式配置。</p>
<p><a id="production-ready-logger-configuration"></a></p>
<h3 id="561、配置一个日志记录器">56.1、配置一个日志记录器</h3>
<p>要配置日志记录器，请将部分实体 <code>POST</code> 到资源的 URI，如下所示：</p>
<pre class="language-"><code class="lang-json"><span class="token punctuation">{</span>
    <span class="token property">"configuredLevel"</span><span class="token operator">:</span> <span class="token string">"DEBUG"</span>
<span class="token punctuation">}</span>
</code></pre>
<p><strong>提示</strong></p>
<blockquote>
<p>要<strong>重置</strong>日志记录器的特定级别（并使用默认配置代替），可以将 <code>null</code> 值作为 <code>configuredLevel</code> 传递。</p>
</blockquote>
<p><a id="production-ready-metrics"></a></p>
<h2 id="57、指标">57、指标</h2>
<p>Spring Boot Actuator 为 <a href="https://micrometer.io/" target="_blank">Micrometer</a> 提供了依赖管理和自动配置，Micrometer 是一个支持众多监控系统的应用程序指标门面，包括：</p>
<ul>
<li><a href="#production-ready-metrics-export-appoptics">AppOptics</a></li>
<li><a href="#production-ready-metrics-export-atlas">Atlas</a></li>
<li><a href="#production-ready-metrics-export-datadog">Datadog</a></li>
<li><a href="#production-ready-metrics-export-dynatrace">Dynatrace</a></li>
<li><a href="#production-ready-metrics-export-elastic">Elastic</a></li>
<li><a href="#production-ready-metrics-export-ganglia">Ganglia</a></li>
<li><a href="#production-ready-metrics-export-graphite">Graphite</a></li>
<li><a href="#production-ready-metrics-export-humio">Humio</a></li>
<li><a href="#production-ready-metrics-export-influx">Influx</a></li>
<li><a href="#production-ready-metrics-export-jmx">JMX</a></li>
<li><a href="#production-ready-metrics-export-kairos">KairosDB</a></li>
<li><a href="#production-ready-metrics-export-newrelic">New Relic</a></li>
<li><a href="#production-ready-metrics-export-prometheus">Prometheus</a></li>
<li><a href="#production-ready-metrics-export-signalfx">SignalFx</a></li>
<li><a href="#production-ready-metrics-export-simple">Simple (in-memory)</a></li>
<li><a href="#production-ready-metrics-export-statsd">StatsD</a></li>
<li><a href="#production-ready-metrics-export-wavefront">Wavefront</a></li>
</ul>
<p><strong>提示</strong></p>
<p>要了解有关 Micrometer 功能的更多信息，请参阅其<a href="https://micrometer.io/docs" target="_blank">参考文档</a>，特别是<a href="https://micrometer.io/docs/concepts" target="_blank">概念部分</a>。</p>
<p><a id="production-ready-metrics-getting-started"></a></p>
<h3 id="571、入门">57.1、入门</h3>
<p>Spring Boot 自动配置了一个组合的 <code>MeterRegistry</code>，并为 classpath 中每个受支持的实现向该组合注册一个注册表。在运行时，只需要 classpath 中有 <code>micrometer-registry-{system}</code> 依赖即可让 Spring Boot 配置该注册表。</p>
<p>大部分注册表都有共同点 例如，即使 Micrometer 注册实现位于 classpath 上，你也可以禁用特定的注册表。例如，要禁用 Datadog：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.metrics.export.datadog.enabled</span><span class="token attr-value"><span class="token punctuation">=</span>false</span>
</code></pre>
<p>Spring Boot 还会将所有自动配置的注册表添加到 <code>Metrics</code> 类的全局静态复合注册表中，除非你明确禁止：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.metrics.use-global-registry</span><span class="token attr-value"><span class="token punctuation">=</span>false</span>
</code></pre>
<p>在注册表中注册任何指标之前，你可以注册任意数量的 <code>MeterRegistryCustomizer</code> bean 以进一步配置注册表，例如通用标签：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Bean</span>
<span class="token class-name">MeterRegistryCustomizer</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">MeterRegistry</span><span class="token punctuation">&gt;</span></span> <span class="token function">metricsCommonTags</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">return</span> registry <span class="token operator">-&gt;</span> registry<span class="token punctuation">.</span><span class="token function">config</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">commonTags</span><span class="token punctuation">(</span><span class="token string">"region"</span><span class="token punctuation">,</span> <span class="token string">"us-east-1"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>
<p>你可以通过指定泛型类型，自定义注册表实现：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Bean</span>
<span class="token class-name">MeterRegistryCustomizer</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">GraphiteMeterRegistry</span><span class="token punctuation">&gt;</span></span> <span class="token function">graphiteMetricsNamingConvention</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">return</span> registry <span class="token operator">-&gt;</span> registry<span class="token punctuation">.</span><span class="token function">config</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">namingConvention</span><span class="token punctuation">(</span>MY_CUSTOM_CONVENTION<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>
<p>使用该设置，你可以在组件中注入 <code>MeterRegistry</code> 并注册指标：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Component</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">SampleBean</span> <span class="token punctuation">{</span>

    <span class="token keyword">private</span> <span class="token keyword">final</span> <span class="token class-name">Counter</span> counter<span class="token punctuation">;</span>

    <span class="token keyword">public</span> <span class="token class-name">SampleBean</span><span class="token punctuation">(</span><span class="token class-name">MeterRegistry</span> registry<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>counter <span class="token operator">=</span> registry<span class="token punctuation">.</span><span class="token function">counter</span><span class="token punctuation">(</span><span class="token string">"received.messages"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">handleMessage</span><span class="token punctuation">(</span><span class="token class-name">String</span> message<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">this</span><span class="token punctuation">.</span>counter<span class="token punctuation">.</span><span class="token function">increment</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token comment">// 处理消息实现</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<p>Spring Boot 还<a href="https://docs.spring.io/spring-boot/docs/2.1.4.RELEASE/reference/htmlsingle/#production-ready-metrics-meter" target="_blank">配置内置的测量工具</a>（即 <code>MeterBinder</code> 实现），你可以通过配置或专用注解标记来控制。</p>
<p><a id="production-ready-metrics-export"></a></p>
<h3 id="572、支持的监控系统">57.2、支持的监控系统</h3>
<p><a id="production-ready-metrics-export-appoptics"></a></p>
<h4 id="5721、appoptics">57.2.1、AppOptics</h4>
<p>默认情况下，AppOptics 注册表会定期将指标推送到 <a href="https://api.appoptics.com/v1/measurements" target="_blank">api.appoptics.com/v1/measurements</a>。要将指标导出到 SaaS <a href="https://micrometer.io/docs/registry/appoptics" target="_blank">AppOptics</a>，你必须提供 API 令牌：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.metrics.export.appoptics.api-token</span><span class="token attr-value"><span class="token punctuation">=</span>YOUR_TOKEN</span>
</code></pre>
<p><a id="production-ready-metrics-export-atlas"></a></p>
<h4 id="5722、atlas">57.2.2、Atlas</h4>
<p>默认情况下，度量标准将导出到本地的 <a href="https://micrometer.io/docs/registry/atlas" target="_blank">Atlas</a>。可以使用以下方式指定 <a href="https://github.com/Netflix/atlas" target="_blank">Atlas 服务器</a>的位置：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.metrics.export.atlas.uri</span><span class="token attr-value"><span class="token punctuation">=</span>https://atlas.example.com:7101/api/v1/publish</span>
</code></pre>
<p><a id="production-ready-metrics-export-datadog"></a></p>
<h4 id="5723、datadog">57.2.3、Datadog</h4>
<p>Datadog 注册表会定期将指标推送到 <a href="https://www.datadoghq.com/" target="_blank">datadoghq</a>。要将指标导出到 <a href="https://micrometer.io/docs/registry/datadog" target="_blank">Datadog</a>，你必须提供 API 密钥：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.metrics.export.datadog.api-key</span><span class="token attr-value"><span class="token punctuation">=</span>YOUR_KEY</span>
</code></pre>
<p>你还可以更改度量标准发送到 Datadog 的间隔时间：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.metrics.export.datadog.step</span><span class="token attr-value"><span class="token punctuation">=</span>30s</span>
</code></pre>
<p><a id="production-ready-metrics-export-dynatrace"></a></p>
<h4 id="5724、dynatrace">57.2.4、Dynatrace</h4>
<p>Dynatrace 注册表定期将指标推送到配置的 URI。要将指标导出到 <a href="https://micrometer.io/docs/registry/dynatrace" target="_blank">Dynatrace</a>，必须提供 API 令牌、设备 ID 和 URI：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.metrics.export.dynatrace.api-token</span><span class="token attr-value"><span class="token punctuation">=</span>YOUR_TOKEN</span>
<span class="token constant">management.metrics.export.dynatrace.device-id</span><span class="token attr-value"><span class="token punctuation">=</span>YOUR_DEVICE_ID</span>
<span class="token constant">management.metrics.export.dynatrace.uri</span><span class="token attr-value"><span class="token punctuation">=</span>YOUR_URI</span>
</code></pre>
<p>你还可以更改度量标准发送到 Dynatrace 的间隔时间：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.metrics.export.dynatrace.step</span><span class="token attr-value"><span class="token punctuation">=</span>30s</span>
</code></pre>
<p><a id="production-ready-metrics-export-elastic"></a></p>
<h4 id="5725、elastic">57.2.5、Elastic</h4>
<p>默认情况下，度量将导出到本地的 <a href="https://micrometer.io/docs/registry/elastic" target="_blank">Elastic</a>。可以使用以下属性提供 Elastic 服务器的位置：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.metrics.export.elastic.host</span><span class="token attr-value"><span class="token punctuation">=</span>https://elastic.example.com:8086</span>
</code></pre>
<p><a id="production-ready-metrics-export-ganglia"></a></p>
<h4 id="5726、ganglia">57.2.6、Ganglia</h4>
<p>默认情况下，度量将导出到本地的 <a href="https://micrometer.io/docs/registry/ganglia" target="_blank">Ganglia</a>。可以使用以下方式提供 <a href="http://ganglia.sourceforge.net/" target="_blank">Ganglia 服务器</a>主机和端口：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.metrics.export.ganglia.host</span><span class="token attr-value"><span class="token punctuation">=</span>ganglia.example.com</span>
<span class="token constant">management.metrics.export.ganglia.port</span><span class="token attr-value"><span class="token punctuation">=</span>9649</span>
</code></pre>
<p><a id="production-ready-metrics-export-graphite"></a></p>
<h4 id="5727、graphite">57.2.7、Graphite</h4>
<p>默认情况下，度量将导出到本地的 <a href="https://micrometer.io/docs/registry/graphite" target="_blank">Graphite</a>。可以使用以下方式提供 <a href="https://graphiteapp.org/" target="_blank">Graphite 服务器</a>主机和端口：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.metrics.export.graphite.host</span><span class="token attr-value"><span class="token punctuation">=</span>graphite.example.com</span>
<span class="token constant">management.metrics.export.graphite.port</span><span class="token attr-value"><span class="token punctuation">=</span>9004</span>
</code></pre>
<p>Micrometer 提供了一个默认的 <code>HierarchicalNameMapper</code>，它管理维度计数器 id 如何<a href="https://micrometer.io/docs/registry/graphite#_hierarchical_name_mapping" target="_blank">映射到平面分层名称</a>。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>要控制此行为，请定义 <code>GraphiteMeterRegistry</code> 并提供自己的 <code>HierarchicalNameMapper</code>。除非你自己定义，否则使用自动配置的 <code>GraphiteConfig</code> 和 <code>Clock</code> bean：</p>
</blockquote>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Bean</span>
<span class="token keyword">public</span> <span class="token class-name">GraphiteMeterRegistry</span> <span class="token function">graphiteMeterRegistry</span><span class="token punctuation">(</span><span class="token class-name">GraphiteConfig</span> config<span class="token punctuation">,</span> <span class="token class-name">Clock</span> clock<span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">return</span> <span class="token keyword">new</span> <span class="token class-name">GraphiteMeterRegistry</span><span class="token punctuation">(</span>config<span class="token punctuation">,</span> clock<span class="token punctuation">,</span> MY_HIERARCHICAL_MAPPER<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>
<p><a id="production-ready-metrics-export-humio"></a></p>
<h4 id="5728、humio">57.2.8、Humio</h4>
<p>默认情况下，Humio 注册表会定期将指标推送到 <a href="https://cloud.humio.com/" target="_blank">cloud.humio.com</a>。要将指标导出到 SaaS <a href="https://micrometer.io/docs/registry/humio" target="_blank">Humio</a>，你必须提供 API 令牌：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.metrics.export.humio.api-token</span><span class="token attr-value"><span class="token punctuation">=</span>YOUR_TOKEN</span>
</code></pre>
<p>你还应配置一个或多个标记，以标识要推送指标的数据源：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.metrics.export.humio.tags.alpha</span><span class="token attr-value"><span class="token punctuation">=</span>a</span>
<span class="token constant">management.metrics.export.humio.tags.bravo</span><span class="token attr-value"><span class="token punctuation">=</span>b</span>
</code></pre>
<p><a id="production-ready-metrics-export-influx"></a></p>
<h4 id="5729、influx">57.2.9、Influx</h4>
<p>默认情况下，度量将导出到本地的 <a href="https://micrometer.io/docs/registry/influx" target="_blank">Influx</a>。要指定 <a href="https://www.influxdata.com/" target="_blank">Influx 服务器</a>的位置，可以使用：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.metrics.export.influx.uri</span><span class="token attr-value"><span class="token punctuation">=</span>https://influx.example.com:8086</span>
</code></pre>
<p><a id="production-ready-metrics-export-jmx"></a></p>
<h4 id="57210、jmx">57.2.10、JMX</h4>
<p>Micrometer 提供了与 <a href="https://micrometer.io/docs/registry/jmx" target="_blank">JMX</a> 的分层映射，主要为了方便在本地查看指标且可移植。默认情况下，度量将导出到 <code>metrics</code> JMX 域。可以使用以下方式提供要使用的域：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.metrics.export.jmx.domain</span><span class="token attr-value"><span class="token punctuation">=</span>com.example.app.metrics</span>
</code></pre>
<p>Micrometer 提供了一个默认的 <code>HierarchicalNameMapper</code>，它管理维度计数器 id 如何<a href="https://micrometer.io/docs/registry/jmx#_hierarchical_name_mapping" target="_blank">映射到平面分层名称</a>。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>要控制此行为，请定义 <code>JmxMeterRegistry</code> 并提供自己的 <code>HierarchicalNameMapper</code>。除非你自己定义，否则使用自动配置的 <code>JmxConfig</code> 和 <code>Clock</code> bean：</p>
</blockquote>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Bean</span>
<span class="token keyword">public</span> <span class="token class-name">JmxMeterRegistry</span> <span class="token function">jmxMeterRegistry</span><span class="token punctuation">(</span><span class="token class-name">JmxConfig</span> config<span class="token punctuation">,</span> <span class="token class-name">Clock</span> clock<span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">return</span> <span class="token keyword">new</span> <span class="token class-name">JmxMeterRegistry</span><span class="token punctuation">(</span>config<span class="token punctuation">,</span> clock<span class="token punctuation">,</span> MY_HIERARCHICAL_MAPPER<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>
<p><a id="production-ready-metrics-export-kairos"></a></p>
<h4 id="57211、kairosdb">57.2.11、KairosDB</h4>
<p>默认情况下，度量将导出到本地的 <a href="https://micrometer.io/docs/registry/kairos" target="_blank">KairosDB</a>。可以使用以下方式提供 <a href="https://kairosdb.github.io/" target="_blank">KairosDB 服务器</a>的位置：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.metrics.export.kairos.uri</span><span class="token attr-value"><span class="token punctuation">=</span>https://kairosdb.example.com:8080/api/v1/datapoints</span>
</code></pre>
<p><a id="production-ready-metrics-export-newrelic"></a></p>
<h4 id="57212、new-relic">57.2.12、New Relic</h4>
<p>New Relic 注册表定期将指标推送到 <a href="https://micrometer.io/docs/registry/new-relic" target="_blank">New Relic</a>。要将指标导出到 <a href="https://newrelic.com/" target="_blank">New Relic</a>，你必须提供 API 密钥和帐户 ID：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.metrics.export.newrelic.api-key</span><span class="token attr-value"><span class="token punctuation">=</span>YOUR_KEY</span>
<span class="token constant">management.metrics.export.newrelic.account-id</span><span class="token attr-value"><span class="token punctuation">=</span>YOUR_ACCOUNT_ID</span>
</code></pre>
<p>你还可以更改将度量发送到 New Relic 的间隔时间：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.metrics.export.newrelic.step</span><span class="token attr-value"><span class="token punctuation">=</span>30s</span>
</code></pre>
<p><a id="production-ready-metrics-export-prometheus"></a></p>
<h4 id="57213、prometheus">57.2.13、Prometheus</h4>
<p><a href="https://micrometer.io/docs/registry/prometheus" target="_blank">Prometheus</a> 希望抓取或轮询各个应用实例以获取指标数据。Spring Boot 在 <code>/actuator/prometheus</code> 上提供 actuator 端点，以适当的格式呈现 <a href="https://prometheus.io/" target="_blank">Prometheus scrape </a>。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>默认情况下端点不可用，必须暴露，请参阅<a href="#production-ready-endpoints-exposing-endpoints">暴露端点</a>以获取更多详细信息。</p>
</blockquote>
<p>以下是要添加到 <code>prometheus.yml</code> 的示例 <code>scrape_config</code>：</p>
<pre class="language-"><code class="lang-yaml"><span class="token key atrule">scrape_configs</span><span class="token punctuation">:</span>
  <span class="token punctuation">-</span> <span class="token key atrule">job_name</span><span class="token punctuation">:</span> <span class="token string">'spring'</span>
    <span class="token key atrule">metrics_path</span><span class="token punctuation">:</span> <span class="token string">'/actuator/prometheus'</span>
    <span class="token key atrule">static_configs</span><span class="token punctuation">:</span>
      <span class="token punctuation">-</span> <span class="token key atrule">targets</span><span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token string">'HOST:PORT'</span><span class="token punctuation">]</span>
</code></pre>
<p><a id="production-ready-metrics-export-signalfx"></a></p>
<h4 id="57214、signalfx">57.2.14、SignalFx</h4>
<p>SignalFx 注册表定期将指标推送到 <a href="https://micrometer.io/docs/registry/signalfx" target="_blank">SignalFx</a>。要将指标导出到 <a href="https://signalfx.com/" target="_blank">SignalFx</a>，你必须提供访问令牌：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.metrics.export.signalfx.access-token</span><span class="token attr-value"><span class="token punctuation">=</span>YOUR_ACCESS_TOKEN</span>
</code></pre>
<p>你还可以更改将指标发送到 SignalFx 的间隔时间：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.metrics.export.signalfx.step</span><span class="token attr-value"><span class="token punctuation">=</span>30s</span>
</code></pre>
<p><a id="production-ready-metrics-export-simple"></a></p>
<h4 id="57215、simple">57.2.15、Simple</h4>
<p>Micrometer 附带一个简单的内存后端，如果没有配置其他注册表，它将自动用作后备。这使你可以查看<a href="#production-ready-metrics-endpoint">指标端点</a>中收集的指标信息。</p>
<p>只要你使用了任何其他可用的后端，内存后端就会自动禁用。你也可以显式禁用它：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.metrics.export.simple.enabled</span><span class="token attr-value"><span class="token punctuation">=</span>false</span>
</code></pre>
<p><a id="production-ready-metrics-export-statsd"></a></p>
<h4 id="57216、statsd">57.2.16、StatsD</h4>
<p>StatsD 注册表将 UDP 上的指标推送到 <a href="https://micrometer.io/docs/registry/statsd" target="_blank">StatsD</a> 代理。 默认情况下，度量将导出到本地的 StatsD 代理，可以使用以下方式提供 StatsD 代理主机和端口：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.metrics.export.statsd.host</span><span class="token attr-value"><span class="token punctuation">=</span>statsd.example.com</span>
<span class="token constant">management.metrics.export.statsd.port</span><span class="token attr-value"><span class="token punctuation">=</span>9125</span>
</code></pre>
<p>你还可以更改要使用的 StatsD 线路协议（默认为 Datadog）：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.metrics.export.statsd.flavor</span><span class="token attr-value"><span class="token punctuation">=</span>etsy</span>
</code></pre>
<p><a id="production-ready-metrics-export-wavefront"></a></p>
<h4 id="57217、wavefront">57.2.17、Wavefront</h4>
<p>Wavefront 注册表定期将指标推送到 <a href="https://micrometer.io/docs/registry/wavefront" target="_blank">Wavefront</a>。如果要将指标直接导出到 <a href="https://www.wavefront.com/" target="_blank">Wavefront</a>，则你必须提供 API 令牌：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.metrics.export.wavefront.api-token</span><span class="token attr-value"><span class="token punctuation">=</span>YOUR_API_TOKEN</span>
</code></pre>
<p>或者，你可以在环境中使用 Wavefront sidecar 或内部代理设置，将指标数据转发到 Wavefront API 主机：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.metrics.export.wavefront.uri</span><span class="token attr-value"><span class="token punctuation">=</span>proxy://localhost:2878</span>
</code></pre>
<p><strong>提示</strong></p>
<blockquote>
<p>如果将度量发布到 Wavefront 代理（如<a href="https://docs.wavefront.com/proxies_installing.html" target="_blank">文档</a>中所述），则主机必须采用 <code>proxy://HOST:PORT</code> 格式。</p>
</blockquote>
<p>你还可以更改将指标发送到 Wavefront 的间隔时间：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.metrics.export.wavefront.step</span><span class="token attr-value"><span class="token punctuation">=</span>30s</span>
</code></pre>
<p><a id="production-ready-metrics-meter"></a></p>
<h3 id="573、支持的指标">57.3、支持的指标</h3>
<p>Spring Boot 在适当的环境注册以下核心指标：</p>
<ul>
<li>JVM 指标，报告利用率：<ul>
<li>各种内存和缓冲池</li>
<li>与垃圾回收有关的统计</li>
<li>线程利用率</li>
<li>加载/卸载 class 的数量</li>
</ul>
</li>
<li>CPU 指标</li>
<li>文件描述符指标</li>
<li>Kafka 消费者指标</li>
<li>Log4j2 指标：记录每个级别记录到 Log4j2 的事件数</li>
<li>Logback 指标：记录每个级别记录到 Logback 的事件数</li>
<li>正常运行时间指标：报告正常运行时间和表示应用程序绝对启动时间的固定计量值</li>
<li>Tomcat 指标</li>
<li><a href="https://docs.spring.io/spring-integration/docs/current/reference/html/system-management-chapter.html#micrometer-integration" target="_blank">Spring Integration</a> 指标</li>
</ul>
<p><a id="production-ready-metrics-spring-mvc"></a></p>
<h4 id="5731、spring-mvc-指标">57.3.1、Spring MVC 指标</h4>
<p>自动配置启用 Spring MVC 处理的请求的指标记录。当 <code>management.metrics.web.server.auto-time-requests</code> 为 <code>true</code> 时，将对所有请求进行此检测。或者，当设置为 <code>false</code> 时，你可以通过将 <code>@Timed</code> 添加到请求处理方法来启用检测：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@RestController</span>
<span class="token annotation punctuation">@Timed</span> <span class="token comment">// &lt;1&gt;</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">MyController</span> <span class="token punctuation">{</span>

    <span class="token annotation punctuation">@GetMapping</span><span class="token punctuation">(</span><span class="token string">"/api/people"</span><span class="token punctuation">)</span>
    <span class="token annotation punctuation">@Timed</span><span class="token punctuation">(</span>extraTags <span class="token operator">=</span> <span class="token punctuation">{</span> <span class="token string">"region"</span><span class="token punctuation">,</span> <span class="token string">"us-east-1"</span> <span class="token punctuation">}</span><span class="token punctuation">)</span> <span class="token comment">// &lt;2&gt;</span>
    <span class="token annotation punctuation">@Timed</span><span class="token punctuation">(</span>value <span class="token operator">=</span> <span class="token string">"all.people"</span><span class="token punctuation">,</span> longTask <span class="token operator">=</span> <span class="token boolean">true</span><span class="token punctuation">)</span> <span class="token comment">// &lt;3&gt;</span>
    <span class="token keyword">public</span> <span class="token class-name">List</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">Person</span><span class="token punctuation">&gt;</span></span> <span class="token function">listPeople</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span> <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span> <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre>
<ol>
<li>一个控制器类，为控制器中的每个请求处理程序启用计时。</li>
<li>启用单个端点。如果你在类上使用了它，就不需要在方法上再次声明，但可以用它来进一步自定义该特定端点的计时器。</li>
<li>使用 <code>longTask = true</code> 的方法为该方法启用长任务计时器。长任务计时器需要单独的指标名称，并且可以使用短任务计时器进行堆叠。</li>
</ol>
<p>默认情况下，使用名称为 <code>http.server.requests</code> 生成度量指标。可以通过设置 <code>management.metrics.web.server.requests-metric-name</code> 属性来自定义名称。</p>
<p>默认情况下，Spring MVC 相关指标使用了以下标签标记：</p>
<table>
<thead>
<tr>
<th>标签</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>exception</code></td>
<td>处理请求时抛出的异常的简单类名。</td>
</tr>
<tr>
<td><code>method</code></td>
<td>请求的方法（例如，<code>GET</code> 或 <code>POST</code>）</td>
</tr>
<tr>
<td><code>outcome</code></td>
<td>根据响应状态码生成结果。1xx 是 <code>INFORMATIONAL</code>，2xx 是 <code>SUCCESS</code>，3xx 是 <code>REDIRECTION</code>，4xx 是 <code>CLIENT_ERROR</code>，5xx 是 <code>SERVER_ERROR</code></td>
</tr>
<tr>
<td><code>status</code></td>
<td>响应的 HTTP 状态码（例如，<code>200</code> 或 <code>500</code>）</td>
</tr>
<tr>
<td><code>uri</code></td>
<td>如果可能，在变量替换之前请求 URI 模板（例如，<code>/api/person/{id}</code>）</td>
</tr>
</tbody>
</table>
<p>要自定义标签，请提供一个实现了 <code>WebMvcTagsProvider</code> 的 <code>@Bean</code>。</p>
<p><a id="production-ready-metrics-web-flux"></a></p>
<h4 id="5732、spring-webflux-指标">57.3.2、Spring WebFlux 指标</h4>
<p>自动配置启用了 WebFlux 控制器和函数式处理程序处理的所有请求的指标记录功能。</p>
<p>默认情况下，使用名为 <code>http.server.requests</code> 生成度量指标。你可以通过设置 <code>management.metrics.web.server.requests-metric-name</code> 属性来自定义名称。</p>
<p>默认情况下，与 WebFlux 相关的指标使用以下标签标记：</p>
<table>
<thead>
<tr>
<th>标签</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>exception</code></td>
<td>处理请求时抛出的异常的简单类名。</td>
</tr>
<tr>
<td><code>method</code></td>
<td>请求方法（例如，<code>GET</code>或 <code>POST</code>）</td>
</tr>
<tr>
<td><code>outcome</code></td>
<td>根据响应状态码生成请求结果。1xx 是 <code>INFORMATIONAL</code>，2xx 是 <code>SUCCESS</code>，3xx 是 <code>REDIRECTION</code>，4xx 是 <code>CLIENT_ERROR</code>，5xx 是 <code>SERVER_ERROR</code></td>
</tr>
<tr>
<td><code>status</code></td>
<td>响应的 HTTP 状态码（例如，<code>200</code> 或 <code>500</code>）</td>
</tr>
<tr>
<td><code>uri</code></td>
<td>如果可能，在变量替换之前请求 URI 模板（例如，<code>/api/person/{id}</code>）</td>
</tr>
</tbody>
</table>
<p>要自定义标签，请提供一个实现了 <code>WebFluxTagsProvider</code> 的 <code>@Bean</code>。</p>
<p><a id="production-ready-metrics-jersey-server"></a></p>
<h4 id="5733、jersey-server-指标">57.3.3、Jersey Server 指标</h4>
<p>自动配置启用了由 Jersey JAX-RS 实现处理的请求的指标记录功能。当 <code>management.metrics.web.server.auto-time-requests</code> 为 <code>true</code> 时，将对所有请求进行该项检测。当设置为 <code>false</code> 时，你可以通过将 <code>@Timed</code> 添加到请求处理方法上来启用检测：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Component</span>
<span class="token annotation punctuation">@Path</span><span class="token punctuation">(</span><span class="token string">"/api/people"</span><span class="token punctuation">)</span>
<span class="token annotation punctuation">@Timed</span> <span class="token comment">// &lt;1&gt;</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">Endpoint</span> <span class="token punctuation">{</span>
    <span class="token annotation punctuation">@GET</span>
    <span class="token annotation punctuation">@Timed</span><span class="token punctuation">(</span>extraTags <span class="token operator">=</span> <span class="token punctuation">{</span> <span class="token string">"region"</span><span class="token punctuation">,</span> <span class="token string">"us-east-1"</span> <span class="token punctuation">}</span><span class="token punctuation">)</span> <span class="token comment">// &lt;2&gt;</span>
    <span class="token annotation punctuation">@Timed</span><span class="token punctuation">(</span>value <span class="token operator">=</span> <span class="token string">"all.people"</span><span class="token punctuation">,</span> longTask <span class="token operator">=</span> <span class="token boolean">true</span><span class="token punctuation">)</span> <span class="token comment">// &lt;3&gt;</span>
    <span class="token keyword">public</span> <span class="token class-name">List</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">Person</span><span class="token punctuation">&gt;</span></span> <span class="token function">listPeople</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span> <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span> <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<ol>
<li>在资源类上，为资源中的每个请求处理程序启用计时。</li>
<li>在方法上则启用单个端点。如果你在类上使用了它，则不需在方法上再次声明，但可以用它来进一步自定义该特定端点的计时器。</li>
<li>在有 <code>longTask = true</code> 的方法上，为该方法启用长任务计时器。长任务计时器需要单独的度量名称，并且可以使用短任务计时器进行堆叠。</li>
</ol>
<p>默认情况下，使用名为 <code>http.server.requests</code> 生成度量指标。可以通过设置 <code>management.metrics.web.server.requests-metric-name</code> 属性来自定义名称。</p>
<p>默认情况下，Jersey 服务器指标使用以下标签标记：</p>
<table>
<thead>
<tr>
<th>标签</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>exception</code></td>
<td>处理请求时抛出的异常的简单类名。</td>
</tr>
<tr>
<td><code>method</code></td>
<td>请求的方法（例如，<code>GET</code> 或 <code>POST</code>）</td>
</tr>
<tr>
<td><code>outcome</code></td>
<td>根据响应状态码生成的请求结果。1xx 是 <code>INFORMATIONAL</code>，2xx 是 <code>SUCCESS</code>，3xx 是 <code>REDIRECTION</code>，4xx 是 <code>CLIENT_ERROR</code>，5xx 是 <code>SERVER_ERROR</code></td>
</tr>
<tr>
<td><code>status</code></td>
<td>响应的 HTTP 状态码（例如，<code>200</code>或 <code>500</code>）</td>
</tr>
<tr>
<td><code>uri</code></td>
<td>如果可能，在变量替换之前请求 URI 模板（例如，<code>/api/person/{id}</code>）</td>
</tr>
</tbody>
</table>
<p>要自定义标签，请提供一个实现了 <code>JerseyTagsProvider</code> 的 <code>@Bean</code>。</p>
<p><a id="production-ready-metrics-http-clients"></a></p>
<h4 id="5734、http-client-指标">57.3.4、HTTP Client 指标</h4>
<p>Spring Boot Actuator 管理 RestTemplate 和 WebClient 的指标记录。为此，你必须注入一个自动配置的 builder 并使用它来创建实例：</p>
<ul>
<li><code>RestTemplateBuilder</code> 用于 <code>RestTemplate</code></li>
<li><code>WebClient.Builder</code> 用于 <code>WebClient</code></li>
</ul>
<p>也可以手动指定负责此指标记录的自定义程序，即 <code>MetricsRestTemplateCustomizer</code> 和 <code>MetricsWebClientCustomizer</code>。</p>
<p>默认情况下，使用名为 <code>http.client.requests</code> 生成度量指标。可以通过设置 <code>management.metrics.web.client.requests-metric-name</code> 属性来自定义名称。</p>
<p>默认情况下，已指标记录客户端生成的度量指标使用以下标签标记：</p>
<ul>
<li><code>method</code>，请求的方法（例如，<code>GET</code>或 <code>POST</code>）。</li>
<li><code>uri</code>，变量替换之前的请求 URI 模板（如果可能）（例如，<code>/api/person/{id}</code>）。</li>
<li><code>status</code>，响应的 HTTP 状态码（例如，<code>200</code> 或 <code>500</code>）。</li>
<li><code>clientName</code>，URI 的主机部分 。</li>
</ul>
<p>要根据你选择的客户端自定义标签，你可以提供一个实现了 <code>RestTemplateExchangeTagsProvider</code> 或 <code>WebClientExchangeTagsProvider</code> 的 <code>@Bean</code>。<code>RestTemplateExchangeTags</code> 和 <code>WebClientExchangeTags</code> 中有便捷的静态函数。</p>
<p><a id="production-ready-metrics-cache"></a></p>
<h4 id="5735、cache-指标">57.3.5、Cache 指标</h4>
<p>在启动时，自动配置启动所有可用 <code>Cache</code> 的指标记录功能，指标以 <code>cache</code> 为前缀。缓存指标记录针对一组基本指标进行了标准化。此外，还提供了缓存特定的指标。</p>
<p>支持以下缓存库：</p>
<ul>
<li>Caffeine</li>
<li>EhCache 2</li>
<li>Hazelcast</li>
<li>所有兼容 JCache（JSR-107）的实现</li>
</ul>
<p>度量指标由缓存的名称和从 bean 名称派生的 <code>CacheManager</code> 的名称标记。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>只有启动时可用的缓存才会绑定到注册表。对于在启动阶段之后即时或以编程方式创建的缓存，需要显式注册。可用 <code>CacheMetricsRegistrar</code> bean 简化该过程。</p>
</blockquote>
<p><a id="production-ready-metrics-jdbc"></a></p>
<h4 id="5736、数据源指标">57.3.6、数据源指标</h4>
<p>自动配置启用对所有可用 <code>DataSource</code> 对象进行指标记录功能，指标的名称为 <code>jdbc</code>。数据源指标记录会生成表示池中当前活动、大允许和最小允许连接的计量器（gauge）。这些计量器都有一个以 <code>jdbc</code> 为前缀的名称。</p>
<p>度量指标也由基于 bean 名称计算的 <code>DataSource</code> 的名称标记。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>默认情况下，Spring Boot 为所有支持的数据源提供了元数据。如果开箱即用不支持你喜欢的数据源，则可以添加其他 <code>DataSourcePoolMetadataProvider</code> bean。有关示例，请参阅 <code>DataSourcePoolMetadataProvidersConfiguration</code>。</p>
</blockquote>
<p>此外，Hikari 特定的指标用 <code>hikaricp</code> 前缀暴露。每个度量指标都由池名称标记（可以使用 <code>spring.datasource.name</code> 控制）。</p>
<p><a id="production-ready-metrics-hibernate"></a></p>
<h4 id="5737、hibernate-指标">57.3.7、Hibernate 指标</h4>
<p>自动配置启用所有可用 Hibernate <code>EntityManagerFactory</code> 实例的指标记录功能，这些实例使用名为 <code>hibernate</code> 的度量指标统计信息。</p>
<p>度量指标也由从 bean 名称派生的 <code>EntityManagerFactory</code> 的名称标记。</p>
<p>要启用信息统计，必须将标准 JPA 属性 <code>hibernate.generate_statistics</code> 设置为 <code>true</code>。你可以在自动配置的 <code>EntityManagerFactory</code> 上启用它，如下所示：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">spring.jpa.properties.hibernate.generate_statistics</span><span class="token attr-value"><span class="token punctuation">=</span>true</span>
</code></pre>
<p><a id="production-ready-metrics-rabbitmq"></a></p>
<h4 id="5738、rabbitmq-指标">57.3.8、RabbitMQ 指标</h4>
<p>自动配置将使用名为 <code>rabbitmq</code> 的度量指标启用对所有可用 RabbitMQ 连接工厂进行指标记录。</p>
<p><a id="production-ready-metrics-custom"></a></p>
<h3 id="574、注册自定义指标">57.4、注册自定义指标</h3>
<p>要注册自定义指标，请将 <code>MeterRegistry</code> 注入你的组件中，如下所示：</p>
<pre class="language-"><code class="lang-java"><span class="token keyword">class</span> <span class="token class-name">Dictionary</span> <span class="token punctuation">{</span>

    <span class="token keyword">private</span> <span class="token keyword">final</span> <span class="token class-name">List</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token class-name">String</span><span class="token punctuation">&gt;</span></span> words <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">CopyOnWriteArrayList</span><span class="token generics"><span class="token punctuation">&lt;</span><span class="token punctuation">&gt;</span></span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

    <span class="token class-name">Dictionary</span><span class="token punctuation">(</span><span class="token class-name">MeterRegistry</span> registry<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        registry<span class="token punctuation">.</span><span class="token function">gaugeCollectionSize</span><span class="token punctuation">(</span><span class="token string">"dictionary.size"</span><span class="token punctuation">,</span> <span class="token class-name">Tags</span><span class="token punctuation">.</span><span class="token function">empty</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token keyword">this</span><span class="token punctuation">.</span>words<span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token comment">// …</span>

<span class="token punctuation">}</span>
</code></pre>
<p>如果你发现跨组件或应用程序重复记录一套度量指标，则可以将此套件封装在 <code>MeterBinder</code> 实现中。默认情况下，所有 <code>MeterBinder</code> bean 的指标都将自动绑定到 Spring 管理的 <code>MeterRegistry</code>。</p>
<p><a id="production-ready-metrics-per-meter-properties"></a></p>
<h3 id="575、自定义单独指标">57.5、自定义单独指标</h3>
<p>如果需要将自定义特定的 <code>Meter</code> 实例，可以使用 <code>io.micrometer.core.instrument.config.MeterFilter</code> 接口。默认情况下，所有 <code>MeterFilter</code> bean 都将自动应用于 <code>MeterRegistry.Config</code>。</p>
<p>例如，如果要将 <code>mytag.region</code> 标记重命名为 <code>mytag.area</code> 以获取以 <code>com.example</code> 开头的所有 meter ID，则可以执行以下操作：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Bean</span>
<span class="token keyword">public</span> <span class="token class-name">MeterFilter</span> <span class="token function">renameRegionTagMeterFilter</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">return</span> <span class="token class-name">MeterFilter</span><span class="token punctuation">.</span><span class="token function">renameTag</span><span class="token punctuation">(</span><span class="token string">"com.example"</span><span class="token punctuation">,</span> <span class="token string">"mytag.region"</span><span class="token punctuation">,</span> <span class="token string">"mytag.area"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>
<p><a id="production-ready-metrics-common-tags"></a></p>
<h4 id="5751、自定义标签">57.5.1、自定义标签</h4>
<p>通用标签通常用于操作环境中的维度下钻，例如主机、实例、区域、堆栈等。通用标签应用于所有 meter，并且可以按照以下示例进行配置：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.metrics.tags.region</span><span class="token attr-value"><span class="token punctuation">=</span>us-east-1</span>
<span class="token constant">management.metrics.tags.stack</span><span class="token attr-value"><span class="token punctuation">=</span>prod</span>
</code></pre>
<p>上面的示例将 <code>region</code> 和 <code>stack</code> 标签添加到所有 meter 中，其值分别为 <code>us-east-1</code> 和 <code>prod</code>。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>如果你使用 Graphite，那么标签的顺序很重要。由于使用此方法无法保证通用标签的顺序，因此建议 Graphite 用户定义自定义 <code>MeterFilter</code>。</p>
</blockquote>
<p><a id="_per_meter_properties"></a></p>
<h4 id="5752、per-meter-属性">57.5.2、Per-meter 属性</h4>
<p>除了 <code>MeterFilter</code> bean 之外，还可以使用 properties 在 per-meter 基础上自定义。Per-meter 定义适用于以给定名称开头的所有 meter ID。例如，以下将禁用任何以 <code>example.remote</code> 开头的 ID 的 meter：</p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.metrics.enable.example.remote</span><span class="token attr-value"><span class="token punctuation">=</span>false</span>
</code></pre>
<p>以下属性允许 per-meter 自定义：</p>
<p><strong>表 57.1、Per-meter 自定义</strong></p>
<p>| 属性 | 描述 |
| <code>management.metrics.enable</code> | 是否拒绝 meter 发布任何指标。 |
| <code>management.metrics.distribution.percentiles-histogram</code> | 是否发布一个适用于计算可聚合（跨维度）的百分比近似柱状图。 |
| <code>management.metrics.distribution.minimum-expected-value</code>，<br> <code>management.metrics.distribution.maximum-expected-value</code>| 通过限制预期值的范围来发布较少的柱状图桶。 |
| <code>management.metrics.distribution.percentiles</code> | 发布在你自己的应用程序中计算的百分比数值 |
| <code>management.metrics.distribution.sla</code> | 发一个使用 SLA 定义的存储桶发布累积柱状图。 |</p>
<p>有关 <code>percentiles-histogram</code>、<code>percentiles</code> 和 <code>sla</code> 概念的更多详细信息，请参阅「<a href="https://micrometer.io/docs/concepts#_histograms_and_percentiles" target="_blank">柱状图与百分位数</a>」部分的文档。</p>
<p><a id="production-ready-metrics-endpoint"></a></p>
<h3 id="576、指标端点">57.6、指标端点</h3>
<p>Spring Boot 提供了一个 <code>metrics</code> 端点，可以在诊断中用于检查应用程序收集的度量指标。默认情况下端点不可用，必须手动暴露，请参阅<a href="#production-ready-endpoints-exposing-endpoints">暴露端点</a>以获取更多详细信息。</p>
<p>访问 <code>/actuator/metrics</code> 会显示可用的 meter 名称列表。你可以查看某一个 meter 的信息，方法是将其名称作为选择器，例如，<code>/actuator/metrics/jvm.memory.max</code>。</p>
<p><strong>提示</strong></p>
<blockquote>
<p>你在此处使用的名称应与代码中使用的名称相匹配，而不是在命名约定规范化后的名称 —— 为了发送到监控系统。换句话说，如果 <code>jvm.memory.max</code> 由于 Prometheus 命名约定而显示为 <code>jvm_memory_max</code>，则在审查度量指标端点中的 meter 时，应仍使用 <code>jvm.memory.max</code> 作为选择器。</p>
</blockquote>
<p>你还可以在 URL 的末尾添加任意数量的 <code>tag=KEY:VALUE</code> 查询参数，以便多维度向下钻取 meter，例如 <code>/actuator/metrics/jvm.memory.max?tag=area:nonheap</code>。</p>
<p><strong>提示</strong></p>
<p>报告的测量值是与 meter 名称和已应用的任何标签匹配的所有 meter 的统计数据的总和。因此，在上面的示例中，返回的 Value 统计信息是堆的 Code Cache，Compressed Class Space 和 Metaspace 区域的最大内存占用量的总和。如果你只想查看 Metaspace 的最大大小，可以添加一个额外的 <code>tag=id:Metaspace</code>，即 <code>/actuator/metrics/jvm.memory.max?tag=area:nonheap&amp;tag=id:Metaspace</code>。</p>
<p><a id="production-ready-auditing"></a></p>
<h2 id="58、审计">58、审计</h2>
<p>一旦 Spring Security 生效，Spring Boot Actuator 就拥有一个灵活的审计框架，它可以发布事件（默认情况下，<code>authentication success</code>、<code>failure</code> 和 <code>access denied</code> 例外）。此功能对事件报告和基于身份验证失败实现一个锁定策略非常有用。要自定义发布的安全事件，你可以提供自己的 <code>AbstractAuthenticationAuditListener</code> 和 <code>AbstractAuthorizationAuditListener</code> 实现。</p>
<p>你还可以将审计服务用于自己的业务事件。为此，请将现有的 <code>AuditEventRepository</code> 注入自己的组件并直接使用它或使用 Spring <code>ApplicationEventPublisher</code>（通过实现 <code>ApplicationEventPublisherAware</code>）发布 <code>AuditApplicationEvent</code>。</p>
<p><a id="production-ready-http-tracing"></a></p>
<h2 id="59、http-追踪">59、HTTP 追踪</h2>
<p>所有 HTTP 请求将自动启用追踪功能。你可以通过查看 <code>httptrace</code> 端点来获取最近相关的 100 个请求响应信息。</p>
<p><a id="production-ready-http-tracing-custom"></a></p>
<h3 id="591、自定义-http-追踪">59.1、自定义 HTTP 追踪</h3>
<p>要自定义每个追踪信息中包含的项，请使用 <code>management.trace.http.include</code> 属性配置。对于高级自定义，请考虑注册自己的 <code>HttpExchangeTracer</code> 实现。</p>
<p>默认情况下，使用一个 <code>InMemoryHttpTraceRepository</code> 存储最新的 100 个请求响应信息。如果需要扩展容量，可定义自己的 <code>InMemoryHttpTraceRepository</code> bean 实例。你还可以创建自己的 <code>HttpTraceRepository</code> 实现来替代默认配置。</p>
<p><a id="production-ready-process-monitoring"></a></p>
<h2 id="60、进程监控">60、进程监控</h2>
<p>在 <code>spring-boot</code> 模块中，你可以找到两个类来创建文件，他们通常用于进程监控：</p>
<ul>
<li><code>ApplicationPidFileWriter</code> 创建一个包含应用程序 PID 的文件（默认在应用程序目录中，文件名为 <code>application.pid</code>）。</li>
<li><code>WebServerPortFileWriter</code> 创建一个或多个文件，其包含正在运行的 Web 服务器的端口（默认在应用程序目录中，文件名为 <code>application.port</code>）。</li>
</ul>
<p>默认情况下，这些 writer 未激活，但你可以启用：</p>
<ul>
<li><a href="#production-ready-process-monitoring-configuration">扩展配置</a></li>
<li><a href="#production-ready-process-monitoring-programmatically">第 60.2 节、编程方式</a></li>
</ul>
<p><a id="production-ready-process-monitoring-configuration"></a></p>
<h3 id="601、扩展配置">60.1、扩展配置</h3>
<p>你可以在 <code>META-INF/spring.factories</code> 文件中激活生成和写入 PID 文件的监听器（Listener），如下所示：</p>
<pre class="language-"><code>org.springframework.context.ApplicationListener=\
org.springframework.boot.context.ApplicationPidFileWriter,\
org.springframework.boot.web.context.WebServerPortFileWriter
</code></pre><p><a id="production-ready-process-monitoring-configuration"></a></p>
<h3 id="602、编程方式">60.2、编程方式</h3>
<p>你还可以通过调用 <code>SpringApplication.addListeners(...)</code> 方法并传递相应的 <code>Writer</code> 对象来激活监听器。此方法还允许你在 <code>Writer</code> 构造方法中自定义文件名和路径。</p>
<p><a id="production-ready-cloudfoundry"></a></p>
<h2 id="61、cloud-foundry-支持">61、Cloud Foundry 支持</h2>
<p>当你部署到一个兼容 Cloud Foundry 的实例时，Spring Boot 的 Actuator 模块包含的其他支持将被激活。<code>/cloudfoundryapplication</code> 路径为所有 <code>@Endpoint</code> bean 提供了另外一个安全路由。</p>
<p>该扩展支持允许使用 Spring Boot Actuator 信息扩充 Cloud Foundry 管理 UI（例如可用于查看已部署应用的 Web 应用）。比如，应用程序状态页面可以包括完整的健康信息而不是常见的 running 或 stop 状态。</p>
<p><strong>注意</strong></p>
<blockquote>
<p>常规用户无法直接访问 <code>/cloudfoundryapplication</code> 路径。为了能访问端点，你必须在请求时传递一个有效的 UAA 令牌。</p>
</blockquote>
<p><a id="production-ready-cloudfoundry-disable"></a></p>
<h3 id="611、禁用-cloud-foundry-actuator-扩展支持">61.1、禁用 Cloud Foundry Actuator 扩展支持</h3>
<p>如果要完全禁用 <code>/cloudfoundryapplication</code> 端点，可以将以下设置添加到 <code>application.properties</code> 文件中：</p>
<p><strong>application.properties</strong></p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.cloudfoundry.enabled</span><span class="token attr-value"><span class="token punctuation">=</span>false</span>
</code></pre>
<p><a id="production-ready-cloudfoundry-ssl"></a></p>
<h3 id="612、cloud-foundry-自签名证书">61.2、Cloud Foundry 自签名证书</h3>
<p>默认情况下，<code>/cloudfoundryapplication</code> 端点的安全验证会对各种 Cloud Foundry 服务进行 SSL 调用。如果你的 Cloud Foundry UAA 或 Cloud Controller 服务使用自签名证书，则需要设置以下属性：</p>
<p><strong>application.properties</strong></p>
<pre class="language-"><code class="lang-ini"><span class="token constant">management.cloudfoundry.skip-ssl-validation</span><span class="token attr-value"><span class="token punctuation">=</span>true</span>
</code></pre>
<p><a id="_custom_context_path"></a></p>
<h3 id="613、自定义上下文路径">61.3、自定义上下文路径</h3>
<p>如果服务器的 context-path 已配置为 <code>/</code> 以外的其他内容，则 Cloud Foundry 端点将无法在应用程序的根目录中使用。例如，如果 <code>server.servlet.context-path=/app</code>，Cloud Foundry 端点将在 <code>/app/cloudfoundryapplication/*</code> 上可用。</p>
<p>如果你希望 Cloud Foundry 端点始终在 <code>/cloudfoundryapplication/*</code> 上可用，则无论服务器的 context-path 如何，你都需要在应用程序中明确配置它。配置因使用的 Web 服务器而有所不同。针对 Tomcat，可以添加以下配置：</p>
<pre class="language-"><code class="lang-java"><span class="token annotation punctuation">@Bean</span>
<span class="token keyword">public</span> <span class="token class-name">TomcatServletWebServerFactory</span> <span class="token function">servletWebServerFactory</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">return</span> <span class="token keyword">new</span> <span class="token class-name">TomcatServletWebServerFactory</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>

        <span class="token annotation punctuation">@Override</span>
        <span class="token keyword">protected</span> <span class="token keyword">void</span> <span class="token function">prepareContext</span><span class="token punctuation">(</span><span class="token class-name">Host</span> host<span class="token punctuation">,</span>
                <span class="token class-name">ServletContextInitializer</span><span class="token punctuation">[</span><span class="token punctuation">]</span> initializers<span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token keyword">super</span><span class="token punctuation">.</span><span class="token function">prepareContext</span><span class="token punctuation">(</span>host<span class="token punctuation">,</span> initializers<span class="token punctuation">)</span><span class="token punctuation">;</span>
            <span class="token class-name">StandardContext</span> child <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">StandardContext</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            child<span class="token punctuation">.</span><span class="token function">addLifecycleListener</span><span class="token punctuation">(</span><span class="token keyword">new</span> <span class="token class-name">Tomcat</span><span class="token punctuation">.</span><span class="token class-name">FixContextListener</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            child<span class="token punctuation">.</span><span class="token function">setPath</span><span class="token punctuation">(</span><span class="token string">"/cloudfoundryapplication"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            <span class="token class-name">ServletContainerInitializer</span> initializer <span class="token operator">=</span> <span class="token function">getServletContextInitializer</span><span class="token punctuation">(</span>
                    <span class="token function">getContextPath</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            child<span class="token punctuation">.</span><span class="token function">addServletContainerInitializer</span><span class="token punctuation">(</span>initializer<span class="token punctuation">,</span> <span class="token class-name">Collections</span><span class="token punctuation">.</span><span class="token function">emptySet</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            child<span class="token punctuation">.</span><span class="token function">setCrossContext</span><span class="token punctuation">(</span><span class="token boolean">true</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            host<span class="token punctuation">.</span><span class="token function">addChild</span><span class="token punctuation">(</span>child<span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>

    <span class="token punctuation">}</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token keyword">private</span> <span class="token class-name">ServletContainerInitializer</span> <span class="token function">getServletContextInitializer</span><span class="token punctuation">(</span><span class="token class-name">String</span> contextPath<span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">return</span> <span class="token punctuation">(</span>c<span class="token punctuation">,</span> context<span class="token punctuation">)</span> <span class="token operator">-&gt;</span> <span class="token punctuation">{</span>
        <span class="token class-name">Servlet</span> servlet <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">GenericServlet</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>

            <span class="token annotation punctuation">@Override</span>
            <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">service</span><span class="token punctuation">(</span><span class="token class-name">ServletRequest</span> req<span class="token punctuation">,</span> <span class="token class-name">ServletResponse</span> res<span class="token punctuation">)</span>
                    <span class="token keyword">throws</span> <span class="token class-name">ServletException</span><span class="token punctuation">,</span> <span class="token class-name">IOException</span> <span class="token punctuation">{</span>
                <span class="token class-name">ServletContext</span> context <span class="token operator">=</span> req<span class="token punctuation">.</span><span class="token function">getServletContext</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
                        <span class="token punctuation">.</span><span class="token function">getContext</span><span class="token punctuation">(</span>contextPath<span class="token punctuation">)</span><span class="token punctuation">;</span>
                context<span class="token punctuation">.</span><span class="token function">getRequestDispatcher</span><span class="token punctuation">(</span><span class="token string">"/cloudfoundryapplication"</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">forward</span><span class="token punctuation">(</span>req<span class="token punctuation">,</span>
                        res<span class="token punctuation">)</span><span class="token punctuation">;</span>
            <span class="token punctuation">}</span>

        <span class="token punctuation">}</span><span class="token punctuation">;</span>
        context<span class="token punctuation">.</span><span class="token function">addServlet</span><span class="token punctuation">(</span><span class="token string">"cloudfoundry"</span><span class="token punctuation">,</span> servlet<span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">addMapping</span><span class="token punctuation">(</span><span class="token string">"/*"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>
<p><a id="production-ready-whats-next"></a></p>
<h2 id="62、下一步">62、下一步</h2>
<p>如果你想了解本章中讨论的一些概念，你可以查看 actuator <a href="https://github.com/spring-projects/spring-boot/tree/v2.1.5.RELEASE/spring-boot-samples" target="_blank">示例应用程序</a>。或许你还想了解 <a href="https://graphite.wikidot.com/" target="_blank">Graphite</a> 等图形工具的相关知识。</p>
<p>此外，你可以继续阅读<a href="deployment.html">应用部署</a>相关内容，或继续阅读有关 Spring Boot <a href="build-tool-plugins.md">构建工具插件</a>的相关内容。</p>
<footer class="page-footer"><span class="copyright">felord.cn</span>&nbsp; &nbsp; <a href="http://beian.miit.gov.cn/" class="copyright-links" target="_blank" rel="nofollow">豫ICP备19038867号-1</a><span class="footer-modification">File Modify:
2019-10-16 21:49:43
</span></footer>
                                
                                </section>
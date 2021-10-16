<section class="normal markdown-section">
<div id="content">
<h1>12. 服务发现：Eureka Server</h1>
<div><ins class="adsbygoogle" style="display:block; text-align:center;" data-ad-layout="in-article" data-ad-format="fluid" data-ad-client="ca-pub-6108808167664152" data-ad-slot="6964403648"></ins>
<script>
(adsbygoogle = window.adsbygoogle || []).push({});
</script></div>
<div><h2 id="如何包含-eureka-server"><a href="#netflix-eureka-server-starter" id="netflix-eureka-server-starter"></a> 12.1 如何包含 Eureka Server</h2>
<p>要在项目中包含 Eureka Server，请使用带有 group <code>org.springframework.cloud</code>和 artifact id <code>spring-cloud-starter-netflix-eureka-server</code>的 starter。有关使用当前 Spring Cloud Release Train 设置 build 系统的详细信息，请参阅<a href="https://projects.spring.io/spring-cloud/" target="_blank" rel="noopener noreferrer">Spring Cloud 项目页面</a>。</p>
<h2 id="如何运行-eureka-服务器"><a href="#spring-cloud-running-eureka-server" id="spring-cloud-running-eureka-server"></a> 12.2 如何运行 Eureka 服务器</h2>
<p>Example eureka 服务器;</p>
<pre><code class="language-">@SpringBootApplication
@EnableEurekaServer
public class Application {

    public static void main(String[] args) {
        new SpringApplicationBuilder(Application.class).web(true).run(args);
    }

}
</code></pre>
<p>服务器有一个带有 UI 的主页，以及<code>/eureka/*</code>下常规 Eureka 功能的 HTTP API endpoints。</p>
<p>Eureka 背景阅读：见<a href="https://github.com/cfregly/fluxcapacitor/wiki/NetflixOSS-FAQ#eureka-service-discovery-load-balancer" target="_blank" rel="noopener noreferrer">磁通电容器</a>和<a href="https://groups.google.com/forum/?fromgroups#!topic/eureka_netflix/g3p2r7gHnN0" target="_blank" rel="noopener noreferrer">google group 讨论</a>。</p>
<blockquote><p>由于 Gradle 的依赖性解析规则和缺少 parent bom feature，仅仅依赖 spring-cloud-starter-netflix-eureka-server 会导致 application 启动失败。要解决这个问题，必须添加 Spring Boot Gradle 插件，并且必须像这样导入 Spring cloud starter parent bom：</p>
</blockquote>
<p><strong>build.gradle.</strong></p>
<pre><code class="language-">buildscript {
  dependencies {
    classpath("org.springframework.boot:spring-boot-gradle-plugin:1.5.10.RELEASE")
  }
}

apply plugin: "spring-boot"

dependencyManagement {
  imports {
    mavenBom "org.springframework.cloud:spring-cloud-dependencies:Edgware.SR2"
  }
}
</code></pre>
<h2 id="高可用性区域和区域"><a href="#spring-cloud-eureka-server-zones-and-regions" id="spring-cloud-eureka-server-zones-and-regions"></a> 12.3 高可用性，区域和区域</h2>
<p>Eureka 服务器没有后端 store，但是注册表中的服务实例都必须发送心跳以使其注册达到 date(因此可以在 memory 中完成)。 Clients 还有一个 in-memory 缓存的 eureka 注册(因此他们不必为服务的每个请求转到注册表)。</p>
<p>默认情况下，每个 Eureka 服务器也是 Eureka client，并且需要(至少一个)服务 URL 来定位对等体。如果你没有提供它，那么服务将会运行并运行，但它会给你的日志带来很多噪音，因为它们无法向对等方注册。</p>
<p>另请参阅 client 侧的<a href="multi_spring-cloud-ribbon.html">以下是 Ribbon 支持的详细信息</a>以了解 Zones 和 Regions。</p>
<h2 id="独立模式"><a href="#_standalone_mode" id="_standalone_mode"></a> 12.4 独立模式</h2>
<p>两个缓存(client 和服务器)和心跳的组合使得独立的 Eureka 服务器对故障具有相当的弹性，因为有一些监视器或 elastic 运行时使其保持活动状态(e.g. Cloud Foundry)。在独立模式下，您可能更愿意关闭 client 端行为，因此它不会继续尝试并且无法访问其对等方。 例：</p>
<p><strong>application.yml(独立 Eureka 服务器).</strong></p>
<pre><code class="language-">server:
  port: 8761

eureka:
  instance:
    hostname: localhost
  client:
    registerWithEureka: false
    fetchRegistry: false
    serviceUrl:
      defaultZone: http://${eureka.instance.hostname}:${server.port}/eureka/
</code></pre>
<p>请注意，<code>serviceUrl</code>指向与本地实例相同的 host。</p>
<h2 id="同侪意识"><a href="#_peer_awareness" id="_peer_awareness"></a> 12.5 同侪意识</h2>
<p>通过 running 多个实例并要求他们相互注册，Eureka 可以变得更有弹性和可用性。实际上，这是默认行为，因此您需要做的就是将有效的<code>serviceUrl</code>添加到对等体 e.g.</p>
<p><strong>application.yml(两个 Peer Aware Eureka 服务器).</strong></p>
<pre><code class="language-">---
spring:
  profiles: peer1
eureka:
  instance:
    hostname: peer1
  client:
    serviceUrl:
      defaultZone: http://peer2/eureka/

---
spring:
  profiles: peer2
eureka:
  instance:
    hostname: peer2
  client:
    serviceUrl:
      defaultZone: http://peer1/eureka/
</code></pre>
<p>在这个 example 中，我们有一个 YAML 文件，可用于在 2 个主机(peer1 和 peer2)上运行相同的服务器，通过在不同的 Spring profiles 中运行它。您可以使用此 configuration 通过操作<code>/etc/hosts</code>来解析 host 名称来测试单个 host 上的对等感知(在 production 中执行该操作时没有多少 value)。实际上，如果您在知道自己的主机名的计算机上运行，则不需要<code>eureka.instance.hostname</code>(默认情况下使用<code>java.net.InetAddress</code>查找)。</p>
<p>您可以将多个对等体添加到系统中，并且由于它们彼此直接相连，因此它们将在它们之间同步注册。</p>
<p><strong>application.yml(三个同行意识 Eureka 服务器).</strong></p>
<pre><code class="language-">eureka:
  client:
    serviceUrl:
      defaultZone: http://peer1/eureka/,http://peer2/eureka/,http://peer3/eureka/

---
spring:
  profiles: peer1
eureka:
  instance:
    hostname: peer1

---
spring:
  profiles: peer2
eureka:
  instance:
    hostname: peer2

---
spring:
  profiles: peer3
eureka:
  instance:
    hostname: peer3
</code></pre>
<h2 id="首选-ip-地址"><a href="#_prefer_ip_address" id="_prefer_ip_address"></a> 12.6 首选 IP 地址</h2>
<p>在某些情况下，Eureka 最好宣传服务的 IP 地址而不是主机名。将<code>eureka.instance.preferIpAddress</code>设置为<code>true</code>，当 application 向 eureka 注册时，它将使用其 IP 地址而不是其主机名。</p>
<blockquote><p>如果 Java 无法确定主机名，则会将 IP 地址发送到 Eureka。只有使用<code>eureka.instance.hostname</code>来设置主机名的明确方法。对于 example <code>eureka.instance.hostname=${HOST_NAME}</code>，您可以使用环境变量在 run time 设置主机名。</p>
</blockquote>
</div>
</div>
</section>
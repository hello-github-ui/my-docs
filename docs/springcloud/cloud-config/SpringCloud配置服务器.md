<section class="normal markdown-section">
<div id="content">
<h1>5. Spring Cloud 配置服务器</h1>
<div><ins class="adsbygoogle" style="display:block; text-align:center;" data-ad-layout="in-article" data-ad-format="fluid" data-ad-client="ca-pub-6108808167664152" data-ad-slot="6964403648"></ins>
<script>
(adsbygoogle = window.adsbygoogle || []).push({});
</script></div>
<div><p>服务器为外部配置(name-value 对或等效的 YAML 内容)提供 HTTP，resource-based API。使用<code>@EnableConfigServer</code> annotation 可以轻松地将服务器嵌入到 Spring Boot application 中。所以这个应用程序是配置服务器：</p>
<p><strong>ConfigServer.java.</strong></p>
<pre><code class="language-">@SpringBootApplication
@EnableConfigServer
public class ConfigServer {
  public static void main(String[] args) {
    SpringApplication.run(ConfigServer.class, args);
  }
}
</code></pre>
<p>像所有 Spring Boot 应用程序一样，它默认在 port 8080 上运行，但您可以通过各种方式将其切换到传统的 port 8888。最简单的，也是设置默认的 configuration repository，是通过<code>spring.config.name=configserver</code>启动它(Config Server jar 中有<code>configserver.yml</code>)。另一种是使用你自己的<code>application.properties</code>，e.g.</p>
<p><strong>application.properties.</strong></p>
<pre><code class="language-">server.port: 8888
spring.cloud.config.server.git.uri: file://${user.home}/config-repo
</code></pre>
<p>其中<code>${user.home}/config-repo</code>是包含 YAML 和 properties files 的 git repository。</p>
<blockquote><p>在 Windows 中，如果文件 URL 绝对带有驱动器前缀 e.g，则需要额外的“/”。 <code>file:///${user.home}/config-repo</code>。</p>
</blockquote><blockquote><p>这是 creating 上面 example 中 git repository 的配方：</p>
</blockquote>
<pre><code class="language-">$ cd $HOME
$ mkdir config-repo
$ cd config-repo
$ git init .
$ echo info.foo: bar &gt; application.properties
$ git add -A .
$ git commit -m "Add application.properties"
</code></pre>
<blockquote><p>使用 git repository 的本地文件系统仅用于测试。在 production 中使用服务器来托管 configuration repositories。</p>
</blockquote><blockquote><p>如果只保留文本 files，则 configuration repository 的初始克隆将快速有效。如果您开始 store 二进制 files，特别是大型文件，您可能会遇到服务器中 memory 错误的第一次 configuration and/or 请求延迟。</p>
</blockquote>
<h2 id="环境存储库"><a href="#_environment_repository" id="_environment_repository"></a> 5.1 环境存储库</h2>
<p>您想在哪里存储 Config Server 的 configuration 数据？管理此行为的策略是<code>EnvironmentRepository</code>，提供<code>Environment</code> objects。这个<code>Environment</code>是来自 Spring <code>Environment</code>的域的浅表副本(包括<code>propertySources</code>作为主 feature)。 <code>Environment</code>资源由三个变量参数化：</p>
<ul>
<li>
<p>在 client 端<code>{application}</code> maps 到“spring.application.name”;</p>
</li>
<li>
<p><code>{profile}</code> maps 到 client 上的“spring.profiles.active”(以逗号分隔的列表);和</p>
</li>
<li>
<p><code>{label}</code>这是一个服务器端 feature，标记了一个“版本化”的 config files 集。</p>
</li>
</ul>
<p>Repository implementations 通常表现得像 Spring Boot application loading configuration files 从“spring.config.name”等于<code>{application}</code>参数，“spring.profiles.active”等于<code>{profiles}</code>参数。 profiles 的优先规则也与常规 Boot application 相同：active profiles 优先于默认值，如果有多个 profiles，则最后一个获胜(如添加条目到<code>Map</code>)。</p>
<p>示例：client application 具有此引导程序 configuration：</p>
<p><strong>bootstrap.yml.</strong></p>
<pre><code class="language-">spring:
  application:
    name: foo
  profiles:
    active: dev,mysql
</code></pre>
<p>(与 Spring Boot application 一样，这些 properties 也可以设置为环境变量或命令 line arguments)。</p>
<p>如果 repository 是 file-based，则服务器将从<code>application.yml</code>(在所有 clients 之间共享)和<code>foo.yml</code>(以<code>foo.yml</code>优先)创建<code>Environment</code>。如果 YAML files 中包含指向 Spring profiles 的文档，那么它们的优先级更高(在列出的 profiles 的 order 中)，如果有 profile-specific YAML(或 properties)files，它们的优先级也高于默认值。较高的优先级转换为<code>Environment</code>中较早列出的<code>PropertySource</code>。 (这些规则适用于独立的 Spring Boot application.)</p>
<h3 id="git-后端"><a href="#_git_backend" id="_git_backend"></a> 5.1.1 Git 后端</h3>
<p><code>EnvironmentRepository</code>的默认_impleration 使用 Git 后端，这对于管理升级和物理环境以及审计更改非常方便。要更改 repository 的位置，可以在 Config Server 中设置“spring.cloud.config.server.git.uri”configuration property(e.g. 在<code>application.yml</code>中)。如果你使用<code>file:</code>前缀设置它，它应该从本地 repository 工作，这样你可以在没有服务器的情况下快速轻松地开始使用，但是在这种情况下，服务器直接在本地 repository 上运行而不克隆它(如果它是无关紧要的)因为 Config Server 永远不会对“remote”repository 进行更改，所以不会裸露。要向上扩展 Config Server 并使其具有高可用性，您需要让服务器的所有实例指向同一个 repository，因此只有共享文件系统才能工作。即使在这种情况下，最好将<code>ssh:</code>协议用于共享文件系统 repository，以便服务器可以克隆它并使用本地工作副本作为缓存。</p>
<p>此 repository implementation maps 将 HTTP 资源的<code>{label}</code>参数映射到 git 标签(commit id，branch name 或 tag)。如果 git 分支或标记 name 包含斜杠(“/”)，则应使用特殊的 string“(<em>)”来指定 HTTP URL 中的标签(以避免与其他 URL paths 的歧义)。对于 example，如果标签为<code>foo/bar</code>，则替换斜杠将导致标签看起来像<code>foo(_)bar</code>。包含特殊 string“(</em>)”也可以应用于<code>{application}</code>参数。如果您使用命令 line client(如 curl)，请小心 URL 中的括号(e.g. 使用引号''从 shell 中转义它们)。</p>
<h4 id="git-uri-中的占位符"><a href="#_placeholders_in_git_uri" id="_placeholders_in_git_uri"></a> Git URI 中的占位符</h4>
<p>Spring Cloud Config Server 支持 git repository URL，其中包含<code>{application}</code>和<code>{profile}</code>的占位符(如果需要，则为<code>{label}</code>，但请记住，标签仍然作为 git 标签应用)。所以你可以使用(for example)轻松支持“one repo per application”policy：</p>
<pre><code class="language-">spring:
  cloud:
    config:
      server:
        git:
          uri: https://github.com/myorg/{application}
</code></pre>
<p>或者使用类似 pattern 但使用<code>{profile}</code>的“一个 repo/_ofofile”policy。</p>
<p>此外，在<code>{application}</code>参数中使用特殊的 string“(_)”可以支持多个组织(对于 example)：</p>
<pre><code class="language-">spring:
  cloud:
    config:
      server:
        git:
          uri: https://github.com/{application}
</code></pre>
<p>其中<code>{application}</code>在请求 time 时以“organization(_)application”格式提供。</p>
<h4 id="pattern-匹配和多个-repositories"><a href="#_pattern_matching_and_multiple_repositories" id="_pattern_matching_and_multiple_repositories"></a> Pattern 匹配和多个 Repositories</h4>
<p>在 application 和 profile name 上使用 pattern 匹配也支持更复杂的需求。 pattern 格式是带有通配符的<code>{application}/{profile}</code>名称的 comma-separated 列表(其中可能需要引用以通配符开头的 pattern)。 例：</p>
<pre><code class="language-">spring:
  cloud:
    config:
      server:
        git:
          uri: https://github.com/spring-cloud-samples/config-repo
          repos:
            simple: https://github.com/simple/config-repo
            special:
              pattern: special*/dev*,*special*/dev*
              uri: https://github.com/special/config-repo
            local:
              pattern: local*
              uri: file:/home/configsvc/config-repo
</code></pre>
<p>如果<code>{application}/{profile}</code>不匹配任何模式，它将使用“spring.cloud.config.server.git.uri”下定义的默认 uri。在上面的例子中，对于“简单”repository，pattern 是<code>simple/*</code>(i.e.它只匹配所有 profiles 中名为“simple”的一个 application)。 “local”repository 匹配所有 profiles 中以“local”开头的所有 application 名称(<code>/*</code>后缀自动添加到任何没有 profile 匹配器的 pattern)。</p>
<blockquote><p>上面“简单”example 中使用的“one-liner”快捷方式只能在要设置的唯一 property 是 URI 时使用。如果您需要设置其他任何内容(凭据，pattern，etc.)，则需要使用完整表单。</p>
</blockquote>
<p>repo 中的<code>pattern</code> property 实际上是一个 array，因此您可以使用 YAML array(或 properties files 中的<code>[0]</code>，<code>[1]</code>等后缀)绑定到多个模式。如果您打算使用多个 profiles 运行应用程序，则可能需要执行此操作。 例：</p>
<pre><code class="language-">spring:
  cloud:
    config:
      server:
        git:
          uri: https://github.com/spring-cloud-samples/config-repo
          repos:
            development:
              pattern:
                - '*/development'
                - '*/staging'
              uri: https://github.com/development/config-repo
            staging:
              pattern:
                - '*/qa'
                - '*/production'
              uri: https://github.com/staging/config-repo
</code></pre>
<blockquote><p>Spring Cloud 会猜测包含 profile 但不以<code>*</code>结尾的 pattern 意味着您实际上想要_以_Ttern 开头的 profiles 列表(因此<code>*/staging</code>是<code>["*/staging", "*/staging,*"]</code>的快捷方式)。这是 common，你需要在本地的“development”profile 中运行应用程序，例如远程地运行“cloud”profile。</p>
</blockquote>
<p>每个 repository 也可以选择在 sub-directories 中 store config files，并且搜索这些目录的模式可以指定为<code>searchPaths</code>。对于顶部 level 的 example：</p>
<pre><code class="language-">spring:
  cloud:
    config:
      server:
        git:
          uri: https://github.com/spring-cloud-samples/config-repo
          searchPaths: foo,bar*
</code></pre>
<p>在此 example 中，服务器在 top level 和“foo /”sub-directory 以及 name 以_bar 开头的任何 sub-directory 中搜索 config files。</p>
<p>默认情况下，首次请求 configuration 时，服务器会克隆 remote repositories。可以将服务器配置为在启动时克隆 repositories。对于顶部 level 的 example：</p>
<pre><code class="language-">spring:
  cloud:
    config:
      server:
        git:
          uri: https://git/common/config-repo.git
          repos:
            team-a:
                pattern: team-a-*
                cloneOnStart: true
                uri: http://git/team-a/config-repo.git
            team-b:
                pattern: team-b-*
                cloneOnStart: false
                uri: http://git/team-b/config-repo.git
            team-c:
                pattern: team-c-*
                uri: http://git/team-a/config-repo.git
</code></pre>
<p>在此 example 中，服务器在接受任何请求之前在启动时克隆 team-a 的 config-repo。在请求 repository 的 configuration 之前，不会克隆所有其他 repositories。</p>
<blockquote><p>在 Config Server 启动时设置要克隆的 repository 可以帮助在 Config Server 启动时快速识别配置错误的 configuration 源(e.g. ，无效的 repository URI)。如果未启用 configuration 源，则配置服务器可能会使用配置错误或无效的 configuration 源成功启动，并且在 application 从该 configuration 源请求 configuration 之前不会检测到错误。</p>
</blockquote>
<h4 id="身份验证"><a href="#_authentication" id="_authentication"></a>身份验证</h4>
<p>要在 remote repository 上使用 HTTP 基本身份验证，请单独添加“username”和“password”properties(不在 URL 中)，e.g.</p>
<pre><code class="language-">spring:
  cloud:
    config:
      server:
        git:
          uri: https://github.com/spring-cloud-samples/config-repo
          username: trolley
          password: strongpassword
</code></pre>
<p>如果您不使用 HTTPS 和用户凭据，当您在默认目录(<code>~/.ssh</code>)中存储密钥并且 uri 指向 SSH 位置 e.g 时，SSH 也应该开箱即用。 “<a href="mailto:git@github.com" target="_blank" rel="noopener noreferrer">[电子邮件保护]</a> :configuration/cloud-configuration”。重要的是 Git 服务器的条目存在于<code>~/.ssh/known_hosts</code>文件中，并且它是<code>ssh-rsa</code>格式。不支持其他格式(如<code>ecdsa-sha2-nistp256</code>)。为避免出现意外，您应确保 Git 服务器的<code>known_hosts</code>文件中只有一个条目，并且它与您提供给配置服务器的 URL 匹配。如果您在 URL 中使用了主机名，则希望在<code>known_hosts</code>文件中使用主机名，而不是 IP。使用 JGit 访问 repository，因此您在其上找到的任何文档都应该适用。 HTTPS 代理设置可以在<code>~/.git/config</code>中设置，也可以通过 system properties(<code>-Dhttps.proxyHost</code>和<code>-Dhttps.proxyPort</code>)以与任何其他 JVM process 相同的方式设置。</p>
<blockquote><p>如果您不知道<code>~/.git</code>目录在哪里使用<code>git config --global</code>来操作设置(e.g .<code>git config --global http.sslVerify false</code>)。</p>
</blockquote>
<h4 id="使用-aws-codecommit-进行身份验证"><a href="#_authentication_with_aws_codecommit" id="_authentication_with_aws_codecommit"></a>使用 AWS CodeCommit 进行身份验证</h4>
<p>也可以进行<a href="https://docs.aws.amazon.com/codecommit/latest/userguide/welcome.html" target="_blank" rel="noopener noreferrer">AWS CodeCommit</a>认证。从命令 line 使用 Git 时，AWS CodeCommit 使用身份验证帮助程序。此助手不与 JGit library 一起使用，因此如果 Git URI 与 AWS CodeCommit pattern 匹配，则将创建 AWS CodeCommit 的 JGit CredentialProvider。 AWS CodeCommit URI 总是看起来像<a href="https://git-codecommit.${AWS_REGION}.amazonaws.com/${repopath}" target="_blank" rel="noopener noreferrer">https://git-codecommit。${AWS_REGION } .amazonaws.com/ ${repopath }</a>。</p>
<p>如果您提供带有 AWS CodeCommit URI 的用户名和密码，那么这些用户名和密码必须是<a href="https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSGettingStartedGuide/AWSCredentials.html" target="_blank" rel="noopener noreferrer">AWS accessKeyId 和 secretAccessKey</a>才能用于访问 repository。如果您未指定用户名和密码，则将使用<a href="https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/credentials.html" target="_blank" rel="noopener noreferrer">AWS 默认凭据提供商链</a>检索 accessKeyId 和 secretAccessKey。</p>
<p>如果 Git URI 与 CodeCommit URI pattern(上图)匹配，则必须在用户名和密码中或默认凭据提供程序链支持的某个位置提供有效的 AWS 凭据。 AWS EC2 实例可以使用<a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/iam-roles-for-amazon-ec2.html" target="_blank" rel="noopener noreferrer">IAM 对 EC2 实例的角色</a>。</p>
<p>注意：aws-java-sdk-core jar 是可选的依赖项。如果 aws-java-sdk-core jar 不在 classpath 上，则无论 git 服务器 URI 如何，都不会创建 AWS Code Commit 凭证提供程序。</p>
<h4 id="使用-properties-创建-ssh-configuration"><a href="#_git_ssh_configuration_using_properties" id="_git_ssh_configuration_using_properties"></a> 使用 properties 创建 SSH configuration</h4>
<p>默认情况下，当使用 SSH URI 连接到 Git repositories 时，Spring Cloud Config Server 使用的 JGit library 使用 SSH configuration files，例如<code>~/.ssh/known_hosts</code>和<code>/etc/ssh/ssh_config</code>。在诸如 Cloud Foundry 之类的云环境中，本地文件系统可能是短暂的或不容易访问的。对于这些情况，可以使用 Java properties 设置 SSH configuration。在 order 中激活基于 property 的 SSH configuration，property <code>spring.cloud.config.server.git.ignoreLocalSshSettings</code>必须设置为<code>true</code>。 例：</p>
<pre><code class="language-">spring:
    cloud:
      config:
        server:
          git:
            uri: git@gitserver.com:team/repo1.git
            ignoreLocalSshSettings: true
            hostKey: someHostKey
            hostKeyAlgorithm: ssh-rsa
            privateKey: |
                         -----BEGIN RSA PRIVATE KEY-----
                         MIIEpgIBAAKCAQEAx4UbaDzY5xjW6hc9jwN0mX33XpTDVW9WqHp5AKaRbtAC3DqX
                         IXFMPgw3K45jxRb93f8tv9vL3rD9CUG1Gv4FM+o7ds7FRES5RTjv2RT/JVNJCoqF
                         ol8+ngLqRZCyBtQN7zYByWMRirPGoDUqdPYrj2yq+ObBBNhg5N+hOwKjjpzdj2Ud
                         1l7R+wxIqmJo1IYyy16xS8WsjyQuyC0lL456qkd5BDZ0Ag8j2X9H9D5220Ln7s9i
                         oezTipXipS7p7Jekf3Ywx6abJwOmB0rX79dV4qiNcGgzATnG1PkXxqt76VhcGa0W
                         DDVHEEYGbSQ6hIGSh0I7BQun0aLRZojfE3gqHQIDAQABAoIBAQCZmGrk8BK6tXCd
                         fY6yTiKxFzwb38IQP0ojIUWNrq0+9Xt+NsypviLHkXfXXCKKU4zUHeIGVRq5MN9b
                         BO56/RrcQHHOoJdUWuOV2qMqJvPUtC0CpGkD+valhfD75MxoXU7s3FK7yjxy3rsG
                         EmfA6tHV8/4a5umo5TqSd2YTm5B19AhRqiuUVI1wTB41DjULUGiMYrnYrhzQlVvj
                         5MjnKTlYu3V8PoYDfv1GmxPPh6vlpafXEeEYN8VB97e5x3DGHjZ5UrurAmTLTdO8
                         +AahyoKsIY612TkkQthJlt7FJAwnCGMgY6podzzvzICLFmmTXYiZ/28I4BX/mOSe
                         pZVnfRixAoGBAO6Uiwt40/PKs53mCEWngslSCsh9oGAaLTf/XdvMns5VmuyyAyKG
                         ti8Ol5wqBMi4GIUzjbgUvSUt+IowIrG3f5tN85wpjQ1UGVcpTnl5Qo9xaS1PFScQ
                         xrtWZ9eNj2TsIAMp/svJsyGG3OibxfnuAIpSXNQiJPwRlW3irzpGgVx/AoGBANYW
                         dnhshUcEHMJi3aXwR12OTDnaLoanVGLwLnkqLSYUZA7ZegpKq90UAuBdcEfgdpyi
                         PhKpeaeIiAaNnFo8m9aoTKr+7I6/uMTlwrVnfrsVTZv3orxjwQV20YIBCVRKD1uX
                         VhE0ozPZxwwKSPAFocpyWpGHGreGF1AIYBE9UBtjAoGBAI8bfPgJpyFyMiGBjO6z
                         FwlJc/xlFqDusrcHL7abW5qq0L4v3R+FrJw3ZYufzLTVcKfdj6GelwJJO+8wBm+R
                         gTKYJItEhT48duLIfTDyIpHGVm9+I1MGhh5zKuCqIhxIYr9jHloBB7kRm0rPvYY4
                         VAykcNgyDvtAVODP+4m6JvhjAoGBALbtTqErKN47V0+JJpapLnF0KxGrqeGIjIRV
                         cYA6V4WYGr7NeIfesecfOC356PyhgPfpcVyEztwlvwTKb3RzIT1TZN8fH4YBr6Ee
                         KTbTjefRFhVUjQqnucAvfGi29f+9oE3Ei9f7wA+H35ocF6JvTYUsHNMIO/3gZ38N
                         CPjyCMa9AoGBAMhsITNe3QcbsXAbdUR00dDsIFVROzyFJ2m40i4KCRM35bC/BIBs
                         q0TY3we+ERB40U8Z2BvU61QuwaunJ2+uGadHo58VSVdggqAo0BSkH58innKKt96J
                         69pcVH/4rmLbXdcmNYGm6iu+MlPQk4BUZknHSmVHIFdJ0EPupVaQ8RHT
                         -----END RSA PRIVATE KEY-----
</code></pre>
<p><a href="" id="d0e1465"></a></p>
<p><strong>表格 1_.SSH Configuration properties</strong></p>
<table>
<thead>
<tr><th>Property Name</th><th>备注</th></tr>
</thead>
<tbody>
<tr><td>**** ignoreLocalSshSettings</td><td>如果 true，请使用基于 property 的 SSH 配置而不是基于文件。必须在 repository 定义中设置为<code>spring.cloud.config.server.git.ignoreLocalSshSettings</code>，<strong>而不是</strong>。</td></tr>
<tr><td>****专用密钥</td><td>有效的 SSH 私有 key。如果<code>ignoreLocalSshSettings</code>是 true 且 Git URI 是 SSH 格式，则必须设置</td></tr>
<tr><td>**** hostKey</td><td>有效的 SSH host key。如果还设置了<code>hostKeyAlgorithm</code>，则必须设置</td></tr>
<tr><td>**** hostKeyAlgorithm</td><td><code>ssh-dss, ssh-rsa, ecdsa-sha2-nistp256, ecdsa-sha2-nistp384 ,ecdsa-sha2-nistp521</code>之一。如果还设置了<code>hostKey</code>，则必须设置</td></tr>
<tr><td>****的 ProxyHost</td><td>ssh 代理连接的主机名。是可选的，仅在<code>ignoreLocalSshSettings</code>为 true 时使用</td></tr>
<tr><td><strong>代理端口</strong></td><td>Port 用于 ssh 代理连接。如果还设置了<code>proxyHost</code>，则必须设置</td></tr>
<tr><td>**** strictHostKeyChecking</td><td><code>true</code>或<code>false</code>。如果 false，则忽略 host key 的错误</td></tr>
<tr><td>**** knownHostsFile</td><td>自定义.knownhosts 文件的位置</td></tr>
<tr><td>**** preferredAuthentications</td><td>覆盖服务器身份验证方法 order。如果服务器在<code>publickey</code>方法之前具有 keyboard-interactive 身份验证，则应允许 evade 登录提示。</td></tr>
</tbody>
</table>
<h4 id="git-中的占位符搜索-paths"><a href="#git-中的占位符搜索-paths" id="git-中的占位符搜索-paths"></a>Git 中的占位符搜索 Paths</h4>
<p>Spring Cloud Config Server 还支持带有<code>{application}</code>和<code>{profile}</code>占位符的搜索路径(如果需要，还支持<code>{label}</code>)。 例：</p>
<pre><code class="language-">spring:
  cloud:
    config:
      server:
        git:
          uri: https://github.com/spring-cloud-samples/config-repo
          searchPaths: '{application}'
</code></pre>
<p>在 repository 中搜索与目录相同的 name 中的 files(以及 top level)。通配符在带占位符的搜索路径中也有效(搜索中包含任何匹配的目录)。</p>
<h4 id="强制拉入-git-repositories"><a href="#_force_pull_in_git_repositories" id="_force_pull_in_git_repositories"></a>强制拉入 Git Repositories</h4>
<p>如前所述 Spring Cloud Config Server 复制了 remote git repository，如果以某种方式使本地副本变脏(e.g. 文件夹内容由 OS process 更改)，则 Spring Cloud Config Server 无法从 remote repository 更新本地副本。</p>
<p>要解决这个问题，有一个<code>force-pull</code> property，如果本地副本是脏的，将使 Spring Cloud Config Server 强制从 remote repository 拉出。 例：</p>
<pre><code class="language-">spring:
  cloud:
    config:
      server:
        git:
          uri: https://github.com/spring-cloud-samples/config-repo
          force-pull: true
</code></pre>
<p>如果您有多个 repositories configuration，则可以为每个 repository 配置<code>force-pull</code> property。 例：</p>
<pre><code class="language-">spring:
  cloud:
    config:
      server:
        git:
          uri: https://git/common/config-repo.git
          force-pull: true
          repos:
            team-a:
                pattern: team-a-*
                uri: http://git/team-a/config-repo.git
                force-pull: true
            team-b:
                pattern: team-b-*
                uri: http://git/team-b/config-repo.git
                force-pull: true
            team-c:
                pattern: team-c-*
                uri: http://git/team-a/config-repo.git
</code></pre>
<blockquote><p><code>force-pull</code> property 的默认 value 是<code>false</code>。</p>
</blockquote>
<h4 id="删除-git-repositories-中未跟踪的分支"><a href="#_deleting_untracked_branches_in_git_repositories" id="_deleting_untracked_branches_in_git_repositories"></a>删除 Git Repositories 中未跟踪的分支</h4>
<p>由于 Spring Cloud Config Server 在 check-outing 分支到本地 repo(按标签 e.g 获取 properties)之后有 remote git repository 的克隆，它将永久保留此分支或直到下一个服务器重新启动(这将创建新的本地 repo)。因此，可能存在删除 remote 分支但仍然可以获取它的本地副本的情况。如果 Spring Cloud Config Server client 服务以<code>--spring.cloud.config.label=deletedRemoteBranch,master</code>开头，它将从<code>deletedRemoteBranch</code>本地分支获取 properties，但不从<code>master</code>获取。</p>
<p>在 order 中保持本地 repository 分支清理并且最多 remote - 可以设置<code>deleteUntrackedBranches</code> property。它会使 Spring Cloud Config Server <strong>强制</strong>从本地 repository 删除未跟踪的分支。 例：</p>
<pre><code class="language-">spring:
  cloud:
    config:
      server:
        git:
          uri: https://github.com/spring-cloud-samples/config-repo
          deleteUntrackedBranches: true
</code></pre>
<blockquote><p><code>deleteUntrackedBranches</code> property 的默认 value 是<code>false</code>。</p>
</blockquote>
<h3 id="version-控制后端文件系统使用"><a href="#_version_control_backend_filesystem_use" id="_version_control_backend_filesystem_use"></a> 5.1.2 Version 控制后端文件系统使用</h3>
<blockquote><p>使用基于 VCS 的后端(git，svn)files 被签出或克隆到本地文件系统。默认情况下，它们放在系统临时目录中，前缀为<code>config-repo-</code>。在 linux 上，对于 example，它可能是<code>/tmp/config-repo-&lt;randomid&gt;</code>。一些操作系统<a href="https://serverfault.com/questions/377348/when-does-tmp-get-cleared/377349#377349" target="_blank" rel="noopener noreferrer">经常清理</a>临时目录。这可能会导致意外行为，例如缺少 properties。要避免此问题，请通过将<code>spring.cloud.config.server.git.basedir</code>或<code>spring.cloud.config.server.svn.basedir</code>设置为不驻留在系统临时结构中的目录来更改 Config Server 使用的目录。</p>
</blockquote>
<h3 id="文件系统后端"><a href="#_file_system_backend" id="_file_system_backend"></a> 5.1.3 文件系统后端</h3>
<p>Config Server 中还有一个“native”profile，它不使用 Git，只是从本地 classpath 或文件系统加载 config files(任何想要指向“spring.cloud.config.server.native.searchLocations”的静态 URL)。要使用本机 profile，只需使用“spring.profiles.active=native”启动配置服务器。</p>
<blockquote><p>请记住使用<code>file:</code>前缀作为文件资源(没有前缀的默认值通常是 classpath)。就像任何 Spring Boot configuration 一样，您可以嵌入<code>${}</code> -style 环境占位符，但请记住 Windows 中的绝对_path 需要额外的“/”，e.g. <code>file:///${user.home}/config-repo</code></p>
</blockquote><blockquote><p><code>searchLocations</code>的默认 value 与本地 Spring Boot application(so <code>[classpath:/, classpath:/config, file:./, file:./config]</code>)相同。这不会将<code>application.properties</code>从服务器暴露给所有 clients，因为服务器中存在的任何 property 源在被发送到 client 之前都会被删除。</p>
</blockquote><blockquote><p>文件系统后端非常适合快速入门和测试。要在 production 中使用它，您需要确保文件系统是可靠的，并在 Config Server 的所有实例之间共享。</p>
</blockquote>
<p>搜索位置可以包含<code>{application}</code>，<code>{profile}</code>和<code>{label}</code>的占位符。通过这种方式，您可以隔离路径中的目录，并选择对您有意义的策略(e.g. sub-directory 每 application，或 sub-directory 每 profile)。</p>
<p>如果您不在搜索位置使用占位符，则此 repository 还会将 HTTP 资源的<code>{label}</code>参数附加到搜索路径上的后缀，因此从每个搜索位置加载 properties files <strong>和</strong>具有相同的子目录 name 作为标签(标记的 properties 在 Spring 环境中优先)。因此，没有占位符的默认行为与添加以<code>/{label}/</code>结尾的搜索位置相同。对于 example <code>file:/tmp/config</code>与<code>file:/tmp/config,file:/tmp/config/{label}</code>相同。可以通过设置<code>spring.cloud.config.server.native.addLabelLocations=false</code>来禁用此行为。</p>
<h3 id="vault-后端"><a href="#_vault_backend" id="_vault_backend"></a> 5.1.4 Vault 后端</h3>
<p>Spring Cloud Config Server 还支持<a href="https://www.vaultproject.io" target="_blank" rel="noopener noreferrer">Vault</a>作为后端。</p>
<hr>
<p>Vault 是一种安全访问机密的工具。 secret 是您想要严格控制访问的任何内容，例如 API 密钥，密码，证书等。 Vault 为任何 secret 提供统一的接口，同时提供严格的访问控制和记录详细的审计 log。</p>
<hr>
<p>有关 Vault 的更多信息，请参阅<a href="https://www.vaultproject.io/intro/index.html" target="_blank" rel="noopener noreferrer">Vault 快速入门指南</a>。</p>
<p>要使配置服务器能够使用 Vault 后端，您可以使用<code>vault</code> profile 运行配置服务器。对于配置服务器的<code>application.properties</code>中的 example，您可以添加<code>spring.profiles.active=vault</code>。</p>
<p>默认情况下，配置服务器将假定您的 Vault 服务器在<code>http://127.0.0.1:8200</code>处运行。它还会假设后端的 name 是<code>secret</code>而 key 是<code>application</code>。所有这些默认值都可以在配置服务器的<code>application.properties</code>中配置。下面是一个 table 可配置 Vault properties。所有 properties 都以<code>spring.cloud.config.server.vault</code>为前缀。</p>
<table>
<thead>
<tr><th>名称</th><th>默认值</th></tr>
</thead>
<tbody>
<tr><td>主办</td><td>127.0.0.1</td></tr>
<tr><td>港口</td><td>8200</td></tr>
<tr><td>方案</td><td>HTTP</td></tr>
<tr><td>后端</td><td>秘密</td></tr>
<tr><td>defaultKey</td><td>应用</td></tr>
<tr><td>profileSeparator</td><td>,</td></tr>
</tbody>
</table>
<p>所有可配置的 properties 都可以在<code>org.springframework.cloud.config.server.environment.VaultEnvironmentRepository</code>中找到。</p>
<p>使用配置服务器 running，您可以向服务器发出 HTTP 请求，以从 Vault 后端检索值。为此，您需要为 Vault 服务器提供令牌。</p>
<p>首先在你的 Vault 中放置一些数据。例如</p>
<pre><code class="language-">$ vault write secret/application foo=bar baz=bam
$ vault write secret/myapp foo=myappsbar
</code></pre>
<p>现在向配置服务器发出 HTTP 请求以检索值。</p>
<p><code>$ curl -X "GET" "http://localhost:8888/myapp/default" -H "X-Config-Token: yourtoken"</code></p>
<p>在提出上述请求后，您应该会看到与此类似的响应。</p>
<pre><code class="language-">{
   "name":"myapp",
   "profiles":[
      "default"
   ],
   "label":null,
   "version":null,
   "state":null,
   "propertySources":[
      {
         "name":"vault:myapp",
         "source":{
            "foo":"myappsbar"
         }
      },
      {
         "name":"vault:application",
         "source":{
            "baz":"bam",
            "foo":"bar"
         }
      }
   ]
}
</code></pre>
<h4 id="多个-properties-来源"><a href="#_multiple_properties_sources" id="_multiple_properties_sources"></a>多个 Properties 来源</h4>
<p>使用 Vault 时，您可以为 applications 提供多个 properties 源。对于 example，假设您已将数据写入 Vault 中的以下_path。</p>
<pre><code class="language-">secret/myApp,dev
secret/myApp
secret/application,dev
secret/application
</code></pre>
<p>写入<code>secret/application</code>的 Properties 可用于<a href="multi__spring_cloud_config_server.html#_vault_server">使用 Config Server 的所有 applications</a>。 name <code>myApp</code>的 application 将有和<code>secret/application</code>可用的任何 properties。当<code>myApp</code>启用<code>dev</code> profile 时，写入所有上述_path 的 properties 将可用，其中列表中第一个路径中的 properties 优先于其他路径。</p>
<h3 id="与所有-applications-共享-configuration"><a href="#_sharing_configuration_with_all_applications" id="_sharing_configuration_with_all_applications"></a> 5.1.5 与所有 Applications 共享 Configuration</h3>
<h4 id="基于文件的存储库"><a href="#_file_based_repositories" id="_file_based_repositories"></a>基于文件的存储库</h4>
<p>使用 file-based(i.e.git，svn 和 native)repositories，<code>application*</code>中文件名的资源在所有 client applications 之间共享(所以<code>application.properties</code>，<code>application.yml</code>，<code>application-*.properties</code> etc.)。您可以使用具有这些文件名的资源来配置 global 默认值并重写它们必要时通过 application-specific files。</p>
<p>#property_overrides [188] feature 也可以用于设置 global 默认值，并且使用占位符 applications 可以在本地覆盖它们。</p>
<blockquote><p>使用“native”profile(本地文件系统后端)，建议您使用不属于服务器自己的 configuration 的显式搜索位置。否则，将删除默认搜索位置中的<code>application*</code>资源，因为它们是服务器的一部分。</p>
</blockquote>
<h4 id="vault-服务器"><a href="#_vault_server" id="_vault_server"></a> Vault 服务器</h4>
<p>使用 Vault 作为后端时，可以通过在<code>secret/application</code>中放置 configuration 来与所有 applications 共享 configuration。例如，如果您运行此 Vault 命令</p>
<pre><code class="language-">$ vault write secret/application foo=bar baz=bam
</code></pre>
<p>使用配置服务器的所有 applications 将为它们提供 properties <code>foo</code>和<code>baz</code>。</p>
<h3 id="jdbc-后端"><a href="#_jdbc_backend" id="_jdbc_backend"></a> 5.1.6 JDBC 后端</h3>
<p>Spring Cloud Config Server 支持 JDBC(关系数据库)作为 configuration properties 的后端。您可以通过将<code>spring-jdbc</code>添加到 classpath，并使用“jdbc”profile 或添加类型的 bean 来启用此 feature。如果在 classpath 中包含正确的依赖项，Spring Boot 将配置数据源(有关详细信息，请参阅用户指南)。</p>
<p>数据库需要有一个名为“PROPERTIES”的 table，其列为“APPLICATION”，“ PROFILE”，“LABEL”(通常为<code>Environment</code>含义)，加上“KEY”和“VALUE”为<code>Properties</code>样式中的 key 和 value 对。所有字段都是 Java 中的 String 类型，因此您可以将它们设置为所需长度的<code>VARCHAR</code>。 Property 值的行为方式与它们来自 Spring Boot properties files 命名为<code>{application}-{profile}.properties</code>的方式相同，包括所有加密和解密，它们将作为 post-processing 步骤应用(i.e.不直接在 repository implementation 中)。</p>
<h3 id="复合环境存储库"><a href="#_composite_environment_repositories" id="_composite_environment_repositories"></a> 5.1.7 复合环境存储库</h3>
<p>在某些情况下，您可能希望从多个环境 repositories 中提取 configuration 数据。要执行此操作，您只需在配置服务器的 application properties 或 YAML 文件中启用多个 profiles。例如，如果要从 Git repository 以及 SVN repository 中提取 configuration 数据，则应为 configuration 服务器设置以下 properties。</p>
<pre><code class="language-">spring:
  profiles:
    active: git, svn
  cloud:
    config:
      server:
        svn:
          uri: file:///path/to/svn/repo
          order: 2
        git:
          uri: file:///path/to/git/repo
          order: 1
</code></pre>
<p>除了指定 URI 的每个 repo 之外，您还可以指定<code>order</code> property。 <code>order</code> property 允许您为所有 repositories 指定优先级 order。 <code>order</code> property 的数值值越低，它的优先级越高。 repository 的 priority order 将帮助解决包含相同 properties 值的 repositories 之间的任何潜在冲突。</p>
<blockquote><p>从环境 repositoy 中检索值时的任何类型的失败都将导致整个复合环境失败。</p>
</blockquote><blockquote><p>使用复合环境时，重要的是所有 repos 都包含相同的 label(s)。如果您的环境与上述环境类似，并且您使用标签<code>master</code>请求 configuration 数据，但 SVN repo 不包含名为<code>master</code>的分支，则整个请求将失败。</p>
</blockquote>
<h4 id="自定义复合环境存储库"><a href="#_custom_composite_environment_repositories" id="_custom_composite_environment_repositories"></a>自定义复合环境存储库</h4>
<p>除了使用 Spring Cloud 中的一个环境存储库之外，还可以将自己的<code>EnvironmentRepository</code> bean 作为复合环境的一部分包含在内。为此，bean 必须实现<code>EnvironmentRepository</code>接口。如果您想在复合环境中控制自定义<code>EnvironmentRepository</code>的优先级，您还应该实现<code>Ordered</code>接口并覆盖<code>getOrdered</code>方法。如果您没有实现<code>Ordered</code>接口，那么<code>EnvironmentRepository</code>将被赋予最低优先级。</p>
<h3 id="property-覆盖"><a href="#_property_overrides" id="_property_overrides"></a> 5.1.8 Property 覆盖</h3>
<p>Config Server 有一个“覆盖”feature，它允许 operator 为使用普通 Spring Boot 挂钩的 application 不会意外更改的所有 applications 提供 configuration properties。要声明覆盖，只需将 name-value 对的 map 添加到<code>spring.cloud.config.server.overrides</code>。例如</p>
<pre><code class="language-">spring:
  cloud:
    config:
      server:
        overrides:
          foo: bar
</code></pre>
<p>将导致所有 applications 是 config clients 读取<code>foo=bar</code>独立于他们自己的 configuration。 (当然应用程序可以以任何方式使用 Config Server 中的数据，因此覆盖是不可执行的，但如果它们是 Spring Cloud Config clients.)它们确实提供了有用的默认行为</p>
<blockquote><p>正常，带有“$ {}”的 Spring 环境占位符可以使用反斜杠(“”)进行转义(并在 client 上解析)以转义“$”或“{”，e.g. <code>\${app.foo:bar}</code>解析为“bar”，除非应用程序提供自己的“app.foo”。请注意，在 YAML 中，您不需要转义反斜杠本身，但在 properties files 中，当您在服务器上配置覆盖时。</p>
</blockquote>
<p>您可以将 client 中所有覆盖的优先级更改为更像默认值，允许 applications 在环境变量或 System properties 中提供自己的值，方法是在 remote repository 中设置 flag <code>spring.cloud.config.overrideNone=true</code>(默认为 false)。</p>
<h2 id="健康指标"><a href="#_health_indicator_2" id="_health_indicator_2"></a> 5.2 健康指标</h2>
<p>Config Server 附带一个运行状况指示器，用于检查配置的<code>EnvironmentRepository</code>是否正常工作。默认情况下，它会向<code>EnvironmentRepository</code>请求名为<code>app</code>的 application，<code>default</code> profile 以及<code>EnvironmentRepository</code> implementation 提供的默认标签。</p>
<p>您可以配置运行状况指示器以检查更多 applications 以及自定义 profiles 和自定义标签 e.g.</p>
<pre><code class="language-">spring:
  cloud:
    config:
      server:
        health:
          repositories:
            myservice:
              label: mylabel
            myservice-dev:
              name: myservice
              profiles: development
</code></pre>
<p>您可以通过设置<code>spring.cloud.config.server.health.enabled=false</code>来禁用健康指标。</p>
<h2 id="安全"><a href="#_security" id="_security"></a> 5.3 安全</h2>
<p>您可以以任何对您有意义的方式(从物理网络安全到 OAuth2 承载令牌)自由保护您的配置服务器，并且 Spring Security 和 Spring Boot 可以轻松完成任何操作。</p>
<p>要使用默认的 Spring Boot 配置的 HTTP Basic 安全性，只需在 classpath(e.g. 到<code>spring-boot-starter-security</code>)上包含 Spring Security。默认值是“user”的用户名和随机生成的密码，这在实践中不会非常有用，因此我们建议您配置密码(通过<code>security.user.password</code>)并对其进行加密(有关如何操作的说明，请参阅下文)那)。</p>
<h2 id="加密和解密"><a href="#_encryption_and_decryption_2" id="_encryption_and_decryption_2"></a> 5.4 加密和解密</h2>
<blockquote><p>**先决条件：**使用加密和解密 features 您需要在 JVM 中安装 full-strength JCE(默认情况下不存在)。您可以从 Oracle 下载“Java Cryptography Extension(JCE)Unlimited Strength Jurisdiction Policy Files”，并按照安装说明进行操作(基本上将 JRE lib/security 目录中的 2 policy files 替换为您下载的那些)。</p>
</blockquote>
<p>如果 remote property 源包含加密内容(以<code>{cipher}</code>开头的值)，则在通过 HTTP 发送给 clients 之前，它们将被解密。这种设置的主要优点是 property 值在“at rest”(e.g. 在 git repository 中)时不必是纯文本。如果无法解密 value，则会从 property 源中删除它，并使用相同的 key 添加其他 property，但前缀为“invalid”。和 value 表示“不适用”(通常为“&lt; <em>3</em> &gt;”)。这主要是为了防止密文被用作密码并意外泄露。</p>
<p>如果要为 config client applications 设置 remote config repository，它可能包含这样的<code>application.yml</code>，例如：</p>
<p><strong>application.yml.</strong></p>
<pre><code class="language-">spring:
  datasource:
    username: dbuser
    password: '{cipher}FKSAJDFGYOS8F7GLHAKERGFHLSAJ'
</code></pre>
<p>.properties 文件中的加密值不能用引号括起来，否则 value 将不会被解密：</p>
<p><strong>application.properties.</strong></p>
<pre><code class="language-">spring.datasource.username: dbuser
spring.datasource.password: {cipher}FKSAJDFGYOS8F7GLHAKERGFHLSAJ
</code></pre>
<p>您可以安全地将此纯文本推送到共享 git repository，并且 secret 密码受到保护。</p>
<p>服务器还公开<code>/encrypt</code>和<code>/decrypt</code> endpoints(假设这些将被保护并且仅由授权代理访问)。如果您正在编辑 remote 配置文件，则可以使用配置服务器通过 POST 到<code>/encrypt</code>端点 e.g 来加密值。</p>
<pre><code class="language-">$ curl localhost:8888/encrypt -d mysecret
682bc583f4641835fa2db009355293665d2647dade3375c0ee201de2a49f7bda
</code></pre>
<blockquote><p>如果您正在加密的 value 中包含需要进行 URL 编码的字符，则应使用<code>--data-urlencode</code>选项<code>curl</code>来确保它们已正确编码。</p>
</blockquote><blockquote><p>请确保不要在加密的 value 中包含任何 curl 命令统计信息。将 value 输出到文件可以帮助避免此问题。</p>
</blockquote>
<p>反向操作也可以通过<code>/decrypt</code>(如果服务器配置了对称 key 或完整的 key 对)：</p>
<pre><code class="language-">$ curl localhost:8888/decrypt -d 682bc583f4641835fa2db009355293665d2647dade3375c0ee201de2a49f7bda
mysecret
</code></pre>
<blockquote><p>如果你使用 curl 进行这样的测试，那么使用<code>--data-urlencode</code>(而不是<code>-d</code>)或设置一个显式的<code>Content-Type: text/plain</code>以确保当有特殊字符时，curl 会正确编码数据(''特别棘手)。</p>
</blockquote>
<p>获取加密的 value 并在将其放入 YAML 或 properties 文件之前添加<code>{cipher}</code>前缀，然后在提交并将其推送到 remote 之前，可能是不安全的 store。</p>
<p><code>/encrypt</code>和<code>/decrypt</code> endpoints 也接受<code>/*/{name}/{profiles}</code>形式的 paths，当 clients 调用主环境资源时，它可用于控制每个 application(name)和 profile 的加密。</p>
<blockquote><p>要以这种精细的方式控制加密，您还必须提供<code>@Bean</code>类型的<code>TextEncryptorLocator</code>，它为每个 name 和 profiles 创建一个不同的加密器。默认情况下提供的那个不执行此操作(因此所有加密使用相同的 key)。</p>
</blockquote>
<p><code>spring</code>命令 line client(安装了 Spring Cloud CLI extensions)也可用于加密和解密，e.g.</p>
<pre><code class="language-">$ spring encrypt mysecret --key foo
682bc583f4641835fa2db009355293665d2647dade3375c0ee201de2a49f7bda
$ spring decrypt --key foo 682bc583f4641835fa2db009355293665d2647dade3375c0ee201de2a49f7bda
mysecret
</code></pre>
<p>要在文件中使用 key(e.g. 用于加密的 RSA public key)，请在 key value 前加上“@”，并提供文件路径 e.g.</p>
<pre><code class="language-">$ spring encrypt mysecret --key @${HOME}/.ssh/id_rsa.pub
AQAjPgt3eFZQXwt8tsHAVv/QHiY5sI2dRcR+...
</code></pre>
<p>key 参数是必需的(尽管有<code>--</code>前缀)。</p>
<h2 id="key-management"><a href="#_key_management" id="_key_management"></a> 5.5 Key Management</h2>
<p>Config Server 可以使用对称(共享)key 或非对称 key(RSA key 对)。非对称选择在安全性方面更优越，但使用对称 key 通常更方便，因为它只是在<code>bootstrap.properties</code>中配置的单个 property value。</p>
<p>要配置对称 key，您只需将<code>encrypt.key</code>设置为 secret String(或使用环境变量<code>ENCRYPT_KEY</code>以使其不受纯文本 configuration files 的影响)。</p>
<blockquote><p>您无法使用<code>encrypt.key</code>配置非对称 key。</p>
</blockquote>
<p>要配置非对称 key，请使用密钥库(e.g. 由 JDK 附带的<code>keytool</code>实用程序创建)。密钥库 properties 是<code>encrypt.keyStore.*</code>，<code>*</code>等于</p>
<ul>
<li>
<p><code>location</code>(a <code>Resource</code>位置)，</p>
</li>
<li>
<p><code>password</code>(解锁密钥库)和</p>
</li>
<li>
<p><code>alias</code>(标识要使用 store 中的 key)。</p>
</li>
</ul>
<p>加密是使用 public key 完成的，解密时需要私有 key。因此，原则上，如果您只想进行加密(并且准备使用私有 key 在本地解密值)，则只能在服务器中配置 public key。在实践中，您可能不希望这样做，因为它在所有 clients 周围传播 key management process，而不是将其集中在服务器中。另一方面，如果您的配置服务器确实相对不安全且只有少数客户端需要加密的 properties，那么它是一个有用的选项。</p>
<h2 id="创建一个-key-store-进行测试"><a href="#_creating_a_key_store_for_testing" id="_creating_a_key_store_for_testing"></a> 5.6 创建一个 Key Store 进行测试</h2>
<p>要创建用于测试的密钥库，您可以执行以下操作：</p>
<pre><code class="language-">$ keytool -genkeypair -alias mytestkey -keyalg RSA \
  -dname "CN=Web Server,OU=Unit,O=Organization,L=City,S=State,C=US" \
  -keypass changeme -keystore server.jks -storepass letmein
</code></pre>
<p>将<code>server.jks</code>文件放在 classpath(例如)中，然后放在<code>bootstrap.yml</code>中用于 Config Server：</p>
<pre><code class="language-">encrypt:
  keyStore:
    location: classpath:/server.jks
    password: letmein
    alias: mytestkey
    secret: changeme
</code></pre>
<h2 id="使用多个键和-key-旋转"><a href="#_using_multiple_keys_and_key_rotation" id="_using_multiple_keys_and_key_rotation"></a> 5.7 使用多个键和 Key 旋转</h2>
<p>除了加密的 property 值中的<code>{cipher}</code>前缀之外，Config Server 还会在(Base64 编码的)密文开始之前查找<code>{name:value}</code>前缀(零或多个)。密钥传递给<code>TextEncryptorLocator</code>，它可以执行为密码定位<code>TextEncryptor</code>所需的任何逻辑。如果已配置密钥库(<code>encrypt.keystore.location</code>)，则默认定位器将在 store 中查找带有“key”前缀 i.e 提供的别名的密钥。使用这样的密文：</p>
<pre><code class="language-">foo:
  bar: `{cipher}{key:testkey}...`
</code></pre>
<p>定位器将查找名为“testkey”的 key。也可以通过前缀中的<code>{secret:…}</code> value 提供 secret，但如果不是，则默认使用密钥库密码(这是您在构建密钥库时未获得 secret 的密码)。如果你**提供 secret，建议你也使用自定义<code>SecretLocator</code>加密秘密。</p>
<p>如果密钥仅用于加密几个字节的 configuration 数据(i.e.它们没有在其他地方使用)，那么在加密方面几乎不需要密钥轮换，但如果存在安全漏洞，有时可能需要更改密钥例如。在这种情况下，所有 clients 都需要更改其源配置 files(e.g. 在 git 中)并在所有密码中使用新的<code>{key:…}</code>前缀，事先检查配置服务器密钥库中的 key 别名是否可用。</p>
<blockquote><p>如果要让 Config Server 处理所有加密和解密，也可以将<code>{name:value}</code>前缀添加到发布到<code>/encrypt</code>端点的明文中。</p>
</blockquote>
<h2 id="提供加密-properties"><a href="#_serving_encrypted_properties" id="_serving_encrypted_properties"></a> 5.8 提供加密 Properties</h2>
<p>有时您希望 clients 在本地解密 configuration，而不是在服务器中执行此操作。在你仍然可以有这种情况/encrypt 和/decrypt endpoints(如果你提供的<code>encrypt.*</code> configuration 找到一个 key)，但你需要在<code>bootstrap.[yml|properties]</code>将<code>spring.cloud.config.server.encrypt.enabled=false</code>明确关掉传出 properties 的解密。如果您不关心 endpoints，那么如果既未配置 key 也未配置启用 flag，则它应该有效。</p>
</div>
</div>
</section>
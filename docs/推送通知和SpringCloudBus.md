<section class="normal markdown-section">
<div id="content">
<h1>9. 推送通知和 Spring Cloud Bus</h1>
<div><ins class="adsbygoogle" style="display:block; text-align:center;" data-ad-layout="in-article" data-ad-format="fluid" data-ad-client="ca-pub-6108808167664152" data-ad-slot="6964403648"></ins>
<script>
(adsbygoogle = window.adsbygoogle || []).push({});
</script></div>
<div><p>许多 source code repository 提供程序(例如 Github，Gitlab 或 Bitbucket)将通过 webhook 通知您 repository 中的更改。您可以通过提供商的用户界面将 webhook 配置为您感兴趣的 URL 和一组 events。例如，<a href="https://developer.github.com/v3/activity/events/types/#pushevent" target="_blank" rel="noopener noreferrer">Github 上</a>将使用包含提交列表的 JSON 主体以及等于“推送”的标题“X-Github-Event”POST 到 webhook。如果在<code>spring-cloud-config-monitor</code> library 上添加依赖项并在配置服务器中激活 Spring Cloud Bus，则启用“/monitor”端点。</p>
<p>当 webhook 被激活时，Config Server 将发送<code>RefreshRemoteApplicationEvent</code>针对它认为可能已更改的 applications。可以策略化更改检测，但默认情况下，它只查找 files 中的如果要覆盖行为，策略是<code>PropertyPathNotificationExtractor</code>，它接受请求 headers 和 body 作为参数，并返回已更改的文件_path 的列表。</p>
<p>默认的 configuration 与 Github，Gitlab 或 Bitbucket 开箱即用。除了来自 Github，Gitlab 或 Bitbucket 的 JSON 通知之外，您还可以通过使用 form-encoded body 参数<code>path={name}</code> POST 到“/monitor”来触发更改通知。这将 broadcast 到 applications 匹配“{。59}”pattern(可以包含通配符)。</p>
<blockquote><p>只有在 Config Server 和 client application 中激活<code>spring-cloud-bus</code>时才会传输<code>RefreshRemoteApplicationEvent</code>。</p>
</blockquote><blockquote><p>默认的 configuration 还会检测本地 git repositories 中的文件系统更改(在这种情况下不使用 webhook，但只要编辑配置文件，刷新就会 broadcast)。</p>
</blockquote>
</div>
</div>
</section>
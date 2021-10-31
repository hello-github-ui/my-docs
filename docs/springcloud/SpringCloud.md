<section class="normal markdown-section">
<div id="content">
<h1>Spring Cloud Edgware.SR5 Reference</h1>
<div><ins class="adsbygoogle" style="display:block; text-align:center;" data-ad-layout="in-article" data-ad-format="fluid" data-ad-client="ca-pub-6108808167664152" data-ad-slot="6964403648"></ins>
<script>
(adsbygoogle = window.adsbygoogle || []).push({});
</script></div>
<div><div class="divider">
<span class="divider-inner-text">Table of Contents</span>
</div>
<ul class="toc">
<li> <a href="multi_pr01.html#"> </a> </li>
<li> <a href="multi__features.html#特征" title="1. 特征"> 1. 特征 </a> </li>
<li> <a href="multi__cloud_native_applications.html#i-cloud-native-applications" title="I. Cloud Native Applications"> I. Cloud Native Applications <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_context_application_context_services.html#spring-cloud-contextapplication-context-services" title="2. Spring Cloud Context：Application Context Services"> 2. Spring Cloud Context：Application Context Services <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_context_application_context_services.html#_the_bootstrap_application_context" title="2.1. Bootstrap Application Context"> 2.1. Bootstrap Application Context </a> </li>
<li> <a href="multi__spring_cloud_context_application_context_services.html#_application_context_hierarchies" title="2.2. Application Context 层次结构"> 2.2. Application Context 层次结构 </a> </li>
<li> <a href="multi__spring_cloud_context_application_context_services.html#customizing-bootstrap-properties" title="2.3. 更改 Bootstrap Properties 的位置"> 2.3. 更改 Bootstrap Properties 的位置 </a> </li>
<li> <a href="multi__spring_cloud_context_application_context_services.html#overriding-bootstrap-properties" title="2.4. 覆盖 Remote Properties 的值"> 2.4. 覆盖 Remote Properties 的值 </a> </li>
<li> <a href="multi__spring_cloud_context_application_context_services.html#_customizing_the_bootstrap_configuration" title="2.5. 自定义 Bootstrap Configuration"> 2.5. 自定义 Bootstrap Configuration </a> </li>
<li> <a href="multi__spring_cloud_context_application_context_services.html#customizing-bootstrap-property-sources" title="2.6. 自定义 Bootstrap Property Sources"> 2.6. 自定义 Bootstrap Property Sources </a> </li>
<li> <a href="multi__spring_cloud_context_application_context_services.html#_logging_configuration" title="2.7. Logging Configuration"> 2.7. Logging Configuration </a> </li>
<li> <a href="multi__spring_cloud_context_application_context_services.html#_environment_changes" title="2.8. 环境变化"> 2.8. 环境变化 </a> </li>
<li> <a href="multi__spring_cloud_context_application_context_services.html#_refresh_scope" title="2.9. 刷新范围"> 2.9. 刷新范围 </a> </li>
<li> <a href="multi__spring_cloud_context_application_context_services.html#_encryption_and_decryption" title="2.10. 加密和解密"> 2.10. 加密和解密 </a> </li>
<li> <a href="multi__spring_cloud_context_application_context_services.html#_endpoints" title="2.11. Endpoints"> 2.11. Endpoints </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_commons_common_abstractions.html#spring-cloud-commonscommon-abstractions" title="3. Spring Cloud Commons：Common Abstractions"> 3. Spring Cloud Commons：Common Abstractions <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_commons_common_abstractions.html#__enablediscoveryclient" title="3.1. @EnableDiscoveryClient"> 3.1. @EnableDiscoveryClient <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_commons_common_abstractions.html#_health_indicator" title="3.1.1. 健康指标"> 3.1.1. 健康指标 </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_commons_common_abstractions.html#_serviceregistry" title="3.2. ServiceRegistry"> 3.2. ServiceRegistry <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_commons_common_abstractions.html#_serviceregistry_auto_registration" title="3.2.1. ServiceRegistry Auto-Registration"> 3.2.1. ServiceRegistry Auto-Registration </a> </li>
<li> <a href="multi__spring_cloud_commons_common_abstractions.html#_service_registry_actuator_endpoint" title="3.2.2. Service Registry Actuator 端点"> 3.2.2. Service Registry Actuator 端点 </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_commons_common_abstractions.html#_spring_resttemplate_as_a_load_balancer_client" title="3.3. Spring RestTemplate 作为负载均衡器 Client"> 3.3. Spring RestTemplate 作为负载均衡器 Client <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_commons_common_abstractions.html#_retrying_failed_requests" title="3.3.1. 重试失败的请求"> 3.3.1. 重试失败的请求 </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_commons_common_abstractions.html#_multiple_resttemplate_objects" title="3.4. 多个 RestTemplate objects"> 3.4. 多个 RestTemplate objects </a> </li>
<li> <a href="multi__spring_cloud_commons_common_abstractions.html#ignore-network-interfaces" title="3.5. 忽略网络接口"> 3.5. 忽略网络接口 </a> </li>
<li> <a href="multi__spring_cloud_commons_common_abstractions.html#http-clients" title="3.6. HTTP Client Factories"> 3.6. HTTP Client Factories </a> </li>
</ul> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_config.html#ii-spring-cloud-配置" title="II. Spring Cloud 配置"> II. Spring Cloud 配置 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__quick_start.html#快速开始" title="4. 快速开始"> 4. 快速开始 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__quick_start.html#_client_side_usage" title="4.1. Client Side Usage"> 4.1. Client Side Usage </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_config_server.html#spring-cloud-配置服务器" title="5. Spring Cloud 配置服务器"> 5. Spring Cloud 配置服务器 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_config_server.html#_environment_repository" title="5.1. 环境存储库"> 5.1. 环境存储库 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_config_server.html#_git_backend" title="5.1.1. Git 后端"> 5.1.1. Git 后端 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_config_server.html#_placeholders_in_git_uri" title="占位符在 Git URI 中"> 占位符在 Git URI 中 </a> </li>
<li> <a href="multi__spring_cloud_config_server.html#_pattern_matching_and_multiple_repositories" title="Pattern 匹配和多个 Repositories"> Pattern 匹配和多个 Repositories </a> </li>
<li> <a href="multi__spring_cloud_config_server.html#_authentication" title="认证"> 认证 </a> </li>
<li> <a href="multi__spring_cloud_config_server.html#_authentication_with_aws_codecommit" title="使用 AWS CodeCommit 进行身份验证"> 使用 AWS CodeCommit 进行身份验证 </a> </li>
<li> <a href="multi__spring_cloud_config_server.html#_git_ssh_configuration_using_properties" title="使用 properties 创建 SSH configuration"> 使用 properties 创建 SSH configuration </a> </li>
<li> <a href="multi__spring_cloud_config_server.html#_placeholders_in_git_search_paths" title="Git 中的占位符搜索 Paths"> Git 中的占位符搜索 Paths </a> </li>
<li> <a href="multi__spring_cloud_config_server.html#_force_pull_in_git_repositories" title="强制拉入 Git Repositories"> 强制拉入 Git Repositories </a> </li>
<li> <a href="multi__spring_cloud_config_server.html#_deleting_untracked_branches_in_git_repositories" title="删除 Git Repositories 中未跟踪的分支"> 删除 Git Repositories 中未跟踪的分支 </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_config_server.html#_version_control_backend_filesystem_use" title="5.1.2. Version 控制后端文件系统使用"> 5.1.2. Version 控制后端文件系统使用 </a> </li>
<li> <a href="multi__spring_cloud_config_server.html#_file_system_backend" title="5.1.3. 文件系统后端"> 5.1.3. 文件系统后端 </a> </li>
<li> <a href="multi__spring_cloud_config_server.html#_vault_backend" title="5.1.4. Vault 后端"> 5.1.4. Vault 后端 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_config_server.html#_multiple_properties_sources" title="多个 Properties 源"> 多个 Properties 源 </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_config_server.html#_sharing_configuration_with_all_applications" title="5.1.5. 与所有 Applications 共享 Configuration"> 5.1.5. 与所有 Applications 共享 Configuration <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_config_server.html#_file_based_repositories" title="基于文件的 Repositories"> 基于文件的 Repositories </a> </li>
<li> <a href="multi__spring_cloud_config_server.html#_vault_server" title="Vault 服务器"> Vault 服务器 </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_config_server.html#_jdbc_backend" title="5.1.6. JDBC 后端"> 5.1.6. JDBC 后端 </a> </li>
<li> <a href="multi__spring_cloud_config_server.html#_composite_environment_repositories" title="5.1.7. 复合环境 Repositories"> 5.1.7. 复合环境 Repositories <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_config_server.html#_custom_composite_environment_repositories" title="自定义复合环境 Repositories"> 自定义复合环境 Repositories </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_config_server.html#_property_overrides" title="5.1.8. Property 覆盖"> 5.1.8. Property 覆盖 </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_config_server.html#_health_indicator_2" title="5.2. 健康指标"> 5.2. 健康指标 </a> </li>
<li> <a href="multi__spring_cloud_config_server.html#_security" title="5.3. 安全"> 5.3. 安全 </a> </li>
<li> <a href="multi__spring_cloud_config_server.html#_encryption_and_decryption_2" title="5.4. 加密和解密"> 5.4. 加密和解密 </a> </li>
<li> <a href="multi__spring_cloud_config_server.html#_key_management" title="5.5. Key Management"> 5.5. Key Management </a> </li>
<li> <a href="multi__spring_cloud_config_server.html#_creating_a_key_store_for_testing" title="5.6. 创建一个 Key Store 进行测试"> 5.6. 创建一个 Key Store 进行测试 </a> </li>
<li> <a href="multi__spring_cloud_config_server.html#_using_multiple_keys_and_key_rotation" title="5.7. 使用多个键和 Key 旋转"> 5.7. 使用多个键和 Key 旋转 </a> </li>
<li> <a href="multi__spring_cloud_config_server.html#_serving_encrypted_properties" title="5.8. 提供加密的 Properties"> 5.8. 提供加密的 Properties </a> </li>
</ul> </li>
<li> <a href="multi__serving_alternative_formats.html#提供替代格式" title="6. 提供替代格式"> 6. 提供替代格式 </a> </li>
<li> <a href="multi__serving_plain_text.html#提供纯文本" title="7. 提供纯文本"> 7. 提供纯文本 </a> </li>
<li> <a href="multi__embedding_the_config_server.html#嵌入配置服务器" title="8. 嵌入配置服务器"> 8. 嵌入配置服务器 </a> </li>
<li> <a href="multi__push_notifications_and_spring_cloud_bus.html#推送通知和-spring-cloud-bus" title="9. 推送通知和 Spring Cloud Bus"> 9. 推送通知和 Spring Cloud Bus </a> </li>
<li> <a href="multi__spring_cloud_config_client.html#spring-cloud-config-client" title="10. Spring Cloud Config Client"> 10. Spring Cloud Config Client <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_config_client.html#config-first-bootstrap" title="10.1. 配置第一个引导程序"> 10.1. 配置第一个引导程序 </a> </li>
<li> <a href="multi__spring_cloud_config_client.html#discovery-first-bootstrap" title="10.2. Discovery First Bootstrap"> 10.2. Discovery First Bootstrap </a> </li>
<li> <a href="multi__spring_cloud_config_client.html#config-client-fail-fast" title="10.3. 配置 Client 快速失败"> 10.3. 配置 Client 快速失败 </a> </li>
<li> <a href="multi__spring_cloud_config_client.html#config-client-retry" title="10.4. 配置 Client 重试"> 10.4. 配置 Client 重试 </a> </li>
<li> <a href="multi__spring_cloud_config_client.html#_locating_remote_configuration_resources" title="10.5. 找到 Remote Configuration Resources"> 10.5. 找到 Remote Configuration Resources </a> </li>
<li> <a href="multi__spring_cloud_config_client.html#_security_2" title="10.6. 安全"> 10.6. 安全 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_config_client.html#_health_indicator_3" title="10.6.1. 健康指标"> 10.6.1. 健康指标 </a> </li>
<li> <a href="multi__spring_cloud_config_client.html#custom-rest-template" title="10.6.2. 提供自定义 RestTemplate"> 10.6.2. 提供自定义 RestTemplate </a> </li>
<li> <a href="multi__spring_cloud_config_client.html#_vault" title="10.6.3. Vault"> 10.6.3. Vault </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_config_client.html#_vault_2" title="10.7. Vault"> 10.7. Vault <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_config_client.html#_nested_keys_in_vault" title="10.7.1. 嵌套密钥在 Vault 中"> 10.7.1. 嵌套密钥在 Vault 中 </a> </li>
</ul> </li>
</ul> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_netflix.html#iii-spring-cloud-netflix" title="III. Spring Cloud Netflix"> III. Spring Cloud Netflix <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__service_discovery_eureka_clients.html#服务发现eureka-clients" title="11. 服务发现：Eureka Clients"> 11. 服务发现：Eureka Clients <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__service_discovery_eureka_clients.html#netflix-eureka-client-starter" title="11.1. 如何包含 Eureka Client"> 11.1. 如何包含 Eureka Client </a> </li>
<li> <a href="multi__service_discovery_eureka_clients.html#_registering_with_eureka" title="11.2. 注册 Eureka"> 11.2. 注册 Eureka </a> </li>
<li> <a href="multi__service_discovery_eureka_clients.html#_authenticating_with_the_eureka_server" title="11.3. 使用 Eureka Server 进行身份验证"> 11.3. 使用 Eureka Server 进行身份验证 </a> </li>
<li> <a href="multi__service_discovery_eureka_clients.html#_status_page_and_health_indicator" title="11.4. 状态页面和健康指标"> 11.4. 状态页面和健康指标 </a> </li>
<li> <a href="multi__service_discovery_eureka_clients.html#_registering_a_secure_application" title="11.5. 注册安全 Application"> 11.5. 注册安全 Application </a> </li>
<li> <a href="multi__service_discovery_eureka_clients.html#_eureka_s_health_checks" title="11.6. Eureka 的健康检查"> 11.6. Eureka 的健康检查 </a> </li>
<li> <a href="multi__service_discovery_eureka_clients.html#_eureka_metadata_for_instances_and_clients" title="11.7. Eureka 实例和 Clients 的元数据"> 11.7. Eureka 实例和 Clients 的元数据 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__service_discovery_eureka_clients.html#_using_eureka_on_cloud_foundry" title="11.7.1. 在 Cloud Foundry 上使用 Eureka"> 11.7.1. 在 Cloud Foundry 上使用 Eureka </a> </li>
<li> <a href="multi__service_discovery_eureka_clients.html#_using_eureka_on_aws" title="11.7.2. 在 AWS 上使用 Eureka"> 11.7.2. 在 AWS 上使用 Eureka </a> </li>
<li> <a href="multi__service_discovery_eureka_clients.html#_changing_the_eureka_instance_id" title="11.7.3. 更改 Eureka 实例 ID"> 11.7.3. 更改 Eureka 实例 ID </a> </li>
</ul> </li>
<li> <a href="multi__service_discovery_eureka_clients.html#_using_the_eurekaclient" title="11.8. 使用 EurekaClient"> 11.8. 使用 EurekaClient <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__service_discovery_eureka_clients.html#_eurekaclient_without_jersey" title="11.8.1. 没有 Jersey 的 EurekaClient"> 11.8.1. 没有 Jersey 的 EurekaClient </a> </li>
</ul> </li>
<li> <a href="multi__service_discovery_eureka_clients.html#_alternatives_to_the_native_netflix_eurekaclient" title="11.9. 原生 Netflix EurekaClient 的替代品"> 11.9. 原生 Netflix EurekaClient 的替代品 </a> </li>
<li> <a href="multi__service_discovery_eureka_clients.html#_why_is_it_so_slow_to_register_a_service" title="11.10. 为什么注册服务这么慢？"> 11.10. 为什么注册服务这么慢？ </a> </li>
<li> <a href="multi__service_discovery_eureka_clients.html#_zones" title="11.11. Zones"> 11.11. Zones </a> </li>
</ul> </li>
<li> <a href="multi_spring-cloud-eureka-server.html#服务发现eureka-server" title="12. 服务发现：Eureka Server"> 12. 服务发现：Eureka Server <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_spring-cloud-eureka-server.html#netflix-eureka-server-starter" title="12.1. 如何包含 Eureka Server"> 12.1. 如何包含 Eureka Server </a> </li>
<li> <a href="multi_spring-cloud-eureka-server.html#spring-cloud-running-eureka-server" title="12.2. 如何运行 Eureka 服务器"> 12.2. 如何运行 Eureka 服务器 </a> </li>
<li> <a href="multi_spring-cloud-eureka-server.html#spring-cloud-eureka-server-zones-and-regions" title="12.3. 高可用性，区域和区域"> 12.3. 高可用性，区域和区域 </a> </li>
<li> <a href="multi_spring-cloud-eureka-server.html#_standalone_mode" title="12.4. 独立模式"> 12.4. 独立模式 </a> </li>
<li> <a href="multi_spring-cloud-eureka-server.html#_peer_awareness" title="12.5. 同伴意识"> 12.5. 同伴意识 </a> </li>
<li> <a href="multi_spring-cloud-eureka-server.html#_prefer_ip_address" title="12.6. 首选 IP 地址"> 12.6. 首选 IP 地址 </a> </li>
</ul> </li>
<li> <a href="multi__circuit_breaker_hystrix_clients.html#断路器hystrix-clients" title="13. 断路器：Hystrix Clients"> 13. 断路器：Hystrix Clients <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__circuit_breaker_hystrix_clients.html#netflix-hystrix-starter" title="13.1. 如何包含 Hystrix"> 13.1. 如何包含 Hystrix </a> </li>
<li> <a href="multi__circuit_breaker_hystrix_clients.html#_propagating_the_security_context_or_using_spring_scopes" title="13.2. 传播安全性 Context 或使用 Spring 范围"> 13.2. 传播安全性 Context 或使用 Spring 范围 </a> </li>
<li> <a href="multi__circuit_breaker_hystrix_clients.html#_health_indicator_4" title="13.3. 健康指标"> 13.3. 健康指标 </a> </li>
<li> <a href="multi__circuit_breaker_hystrix_clients.html#_hystrix_metrics_stream" title="13.4. Hystrix Metrics Stream"> 13.4. Hystrix Metrics Stream </a> </li>
</ul> </li>
<li> <a href="multi__circuit_breaker_hystrix_dashboard.html#断路器hystrix-仪表板" title="14. 断路器：Hystrix 仪表板"> 14. 断路器：Hystrix 仪表板 </a> </li>
<li> <a href="multi__hystrix_timeouts_and_ribbon_clients.html#hystrix-超时和-ribbon-clients" title="15. Hystrix 超时和 Ribbon Clients"> 15. Hystrix 超时和 Ribbon Clients <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__hystrix_timeouts_and_ribbon_clients.html#netflix-hystrix-dashboard-starter" title="15.1. 如何包含 Hystrix 仪表板"> 15.1. 如何包含 Hystrix 仪表板 </a> </li>
<li> <a href="multi__hystrix_timeouts_and_ribbon_clients.html#_turbine" title="15.2. 涡轮"> 15.2. 涡轮 </a> </li>
<li> <a href="multi__hystrix_timeouts_and_ribbon_clients.html#_turbine_stream" title="15.3. Turbine Stream"> 15.3. Turbine Stream </a> </li>
</ul> </li>
<li> <a href="multi_spring-cloud-ribbon.html#client-side-load-balancerribbon" title="16. Client Side Load Balancer：Ribbon"> 16. Client Side Load Balancer：Ribbon <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_spring-cloud-ribbon.html#netflix-ribbon-starter" title="16.1. 如何包含 Ribbon"> 16.1. 如何包含 Ribbon </a> </li>
<li> <a href="multi_spring-cloud-ribbon.html#_customizing_the_ribbon_client" title="16.2. 自定义 Ribbon Client"> 16.2. 自定义 Ribbon Client </a> </li>
<li> <a href="multi_spring-cloud-ribbon.html#_customizing_default_for_all_ribbon_clients" title="16.3. 自定义所有 Ribbon Clients 的默认值"> 16.3. 自定义所有 Ribbon Clients 的默认值 </a> </li>
<li> <a href="multi_spring-cloud-ribbon.html#_customizing_the_ribbon_client_using_properties" title="16.4. 使用 properties 自定义 Ribbon Client"> 16.4. 使用 properties 自定义 Ribbon Client </a> </li>
<li> <a href="multi_spring-cloud-ribbon.html#_using_ribbon_with_eureka" title="16.5. 使用 Ribbon 和 Eureka"> 16.5. 使用 Ribbon 和 Eureka </a> </li>
<li> <a href="multi_spring-cloud-ribbon.html#spring-cloud-ribbon-without-eureka" title="16.6. 示例：如何在没有 Eureka 的情况下使用 Ribbon"> 16.6. 示例：如何在没有 Eureka 的情况下使用 Ribbon </a> </li>
<li> <a href="multi_spring-cloud-ribbon.html#_example_disable_eureka_use_in_ribbon" title="16.7. 示例：在 Ribbon 中禁用 Eureka 使用"> 16.7. 示例：在 Ribbon 中禁用 Eureka 使用 </a> </li>
<li> <a href="multi_spring-cloud-ribbon.html#_using_the_ribbon_api_directly" title="16.8. 直接使用 Ribbon API"> 16.8. 直接使用 Ribbon API </a> </li>
<li> <a href="multi_spring-cloud-ribbon.html#ribbon-child-context-eager-load" title="16.9. 缓存 Ribbon Configuration"> 16.9. 缓存 Ribbon Configuration </a> </li>
<li> <a href="multi_spring-cloud-ribbon.html#how-to-configure-hystrix-thread-pools" title="16.10. 如何配置 Hystrix 线程池"> 16.10. 如何配置 Hystrix 线程池 </a> </li>
<li> <a href="multi_spring-cloud-ribbon.html#how-to-provdie-a-key-to-ribbon" title="16.11. 如何为 Ribbon 的 IRule 提供 Key"> 16.11. 如何为 Ribbon 的 IRule 提供 Key </a> </li>
</ul> </li>
<li> <a href="multi_spring-cloud-feign.html#声明性-rest-clientfeign" title="17. 声明性 REST Client：Feign"> 17. 声明性 REST Client：Feign <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_spring-cloud-feign.html#netflix-feign-starter" title="17.1. 如何包含 Feign"> 17.1. 如何包含 Feign </a> </li>
<li> <a href="multi_spring-cloud-feign.html#spring-cloud-feign-overriding-defaults" title="17.2. 覆盖 Feign 默认值"> 17.2. 覆盖 Feign 默认值 </a> </li>
<li> <a href="multi_spring-cloud-feign.html#_creating_feign_clients_manually" title="17.3. 手动创建 Feign Clients"> 17.3. 手动创建 Feign Clients </a> </li>
<li> <a href="multi_spring-cloud-feign.html#spring-cloud-feign-hystrix" title="17.4. Feign Hystrix 支持"> 17.4. Feign Hystrix 支持 </a> </li>
<li> <a href="multi_spring-cloud-feign.html#spring-cloud-feign-hystrix-fallback" title="17.5. Feign Hystrix Fallbacks"> 17.5. Feign Hystrix Fallbacks </a> </li>
<li> <a href="multi_spring-cloud-feign.html#_feign_and_literal_primary_literal" title="17.6. Feign 和@Primary"> 17.6. Feign 和@Primary </a> </li>
<li> <a href="multi_spring-cloud-feign.html#spring-cloud-feign-inheritance" title="17.7. Feign 继承支持"> 17.7. Feign 继承支持 </a> </li>
<li> <a href="multi_spring-cloud-feign.html#_feign_request_response_compression" title="17.8. Feign request/response 压缩"> 17.8. Feign request/response 压缩 </a> </li>
<li> <a href="multi_spring-cloud-feign.html#_feign_logging" title="17.9. Feign logging"> 17.9. Feign logging </a> </li>
</ul> </li>
<li> <a href="multi__external_configuration_archaius.html#外部-configurationarchaius" title="18. 外部 Configuration：Archaius"> 18. 外部 Configuration：Archaius </a> </li>
<li> <a href="multi__router_and_filter_zuul.html#router-和-filterzuul" title="19. Router 和 Filter：Zuul"> 19. Router 和 Filter：Zuul <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__router_and_filter_zuul.html#netflix-zuul-starter" title="19.1. 如何包括 Zuul"> 19.1. 如何包括 Zuul </a> </li>
<li> <a href="multi__router_and_filter_zuul.html#netflix-zuul-reverse-proxy" title="19.2. 嵌入式 Zuul 反向代理"> 19.2. 嵌入式 Zuul 反向代理 </a> </li>
<li> <a href="multi__router_and_filter_zuul.html#_zuul_http_client" title="19.3. Zuul Http Client"> 19.3. Zuul Http Client </a> </li>
<li> <a href="multi__router_and_filter_zuul.html#_cookies_and_sensitive_headers" title="19.4. Cookies and Sensitive Headers"> 19.4. Cookies and Sensitive Headers </a> </li>
<li> <a href="multi__router_and_filter_zuul.html#_ignored_headers" title="19.5. 忽略 Headers"> 19.5. 忽略 Headers </a> </li>
<li> <a href="multi__router_and_filter_zuul.html#_management_endpoints" title="19.6. Management Endpoints"> 19.6. Management Endpoints <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__router_and_filter_zuul.html#_routes_endpoint" title="19.6.1. Routes Endpoint"> 19.6.1. Routes Endpoint </a> </li>
<li> <a href="multi__router_and_filter_zuul.html#_filters_endpoint" title="19.6.2. 过滤端点"> 19.6.2. 过滤端点 </a> </li>
</ul> </li>
<li> <a href="multi__router_and_filter_zuul.html#_strangulation_patterns_and_local_forwards" title="19.7. 扼杀模式和地方前锋"> 19.7. 扼杀模式和地方前锋 </a> </li>
<li> <a href="multi__router_and_filter_zuul.html#_uploading_files_through_zuul" title="19.8. 通过 Zuul 上传 Files"> 19.8. 通过 Zuul 上传 Files </a> </li>
<li> <a href="multi__router_and_filter_zuul.html#_query_string_encoding" title="19.9. 查询 String 编码"> 19.9. 查询 String 编码 </a> </li>
<li> <a href="multi__router_and_filter_zuul.html#_plain_embedded_zuul" title="19.10. 普通嵌入式 Zuul"> 19.10. 普通嵌入式 Zuul </a> </li>
<li> <a href="multi__router_and_filter_zuul.html#_disable_zuul_filters" title="19.11. 禁用 Zuul 过滤器"> 19.11. 禁用 Zuul 过滤器 </a> </li>
<li> <a href="multi__router_and_filter_zuul.html#hystrix-fallbacks-for-routes" title="19.12. 为 Routes 提供 Hystrix 后备"> 19.12. 为 Routes 提供 Hystrix 后备 </a> </li>
<li> <a href="multi__router_and_filter_zuul.html#_zuul_timeouts" title="19.13. Zuul 超时"> 19.13. Zuul 超时 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__router_and_filter_zuul.html#_service_discovery_configuration" title="19.13.1. 服务发现配置"> 19.13.1. 服务发现配置 </a> </li>
<li> <a href="multi__router_and_filter_zuul.html#_url_configuration" title="19.13.2. URL Configuration"> 19.13.2. URL Configuration </a> </li>
</ul> </li>
<li> <a href="multi__router_and_filter_zuul.html#zuul-redirect-location-rewrite" title="19.14. 重写位置标题"> 19.14. 重写位置标题 </a> </li>
<li> <a href="multi__router_and_filter_zuul.html#zuul-developer-guide" title="19.15. Zuul 开发人员指南"> 19.15. Zuul 开发人员指南 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__router_and_filter_zuul.html#_the_zuul_servlet" title="19.15.1. Zuul Servlet"> 19.15.1. Zuul Servlet </a> </li>
<li> <a href="multi__router_and_filter_zuul.html#_zuul_requestcontext" title="19.15.2. Zuul RequestContext"> 19.15.2. Zuul RequestContext </a> </li>
<li> <a href="multi__router_and_filter_zuul.html#__literal_enablezuulproxy_literal_vs_literal_enablezuulserver_literal" title="19.15.3. @EnableZuulProxy 与@EnableZuulServer"> 19.15.3. @EnableZuulProxy 与@EnableZuulServer </a> </li>
<li> <a href="multi__router_and_filter_zuul.html#__literal_enablezuulserver_literal_filters" title="19.15.4. @EnableZuulServer 过滤器"> 19.15.4. @EnableZuulServer 过滤器 </a> </li>
<li> <a href="multi__router_and_filter_zuul.html#__literal_enablezuulproxy_literal_filters" title="19.15.5. @EnableZuulProxy 过滤器"> 19.15.5. @EnableZuulProxy 过滤器 </a> </li>
<li> <a href="multi__router_and_filter_zuul.html#_custom_zuul_filter_examples" title="19.15.6. 自定义 Zuul 过滤器示例"> 19.15.6. 自定义 Zuul 过滤器示例 </a> </li>
<li> <a href="multi__router_and_filter_zuul.html#_how_to_write_a_pre_filter" title="19.15.7. 如何编写预过滤器"> 19.15.7. 如何编写预过滤器 </a> </li>
<li> <a href="multi__router_and_filter_zuul.html#_how_to_write_a_route_filter" title="19.15.8. 如何编写 Route 过滤器"> 19.15.8. 如何编写 Route 过滤器 </a> </li>
<li> <a href="multi__router_and_filter_zuul.html#_how_to_write_a_post_filter" title="19.15.9. 如何编写后置过滤器"> 19.15.9. 如何编写后置过滤器 </a> </li>
<li> <a href="multi__router_and_filter_zuul.html#_how_zuul_errors_work" title="19.15.10. Zuul 错误如何工作"> 19.15.10. Zuul 错误如何工作 </a> </li>
<li> <a href="multi__router_and_filter_zuul.html#_zuul_eager_application_context_loading" title="19.15.11. Zuul Eager Application Context Loading"> 19.15.11. Zuul Eager Application Context Loading </a> </li>
</ul> </li>
</ul> </li>
<li> <a href="multi__polyglot_support_with_sidecar.html#sideg-的-polyglot-支持" title="20. Sideg 的 Polyglot 支持"> 20. Sideg 的 Polyglot 支持 </a> </li>
<li> <a href="multi_netflix-rxjava-springmvc.html#rxjava-与-spring-mvc" title="21. RxJava 与 Spring MVC"> 21. RxJava 与 Spring MVC </a> </li>
<li> <a href="multi_netflix-metrics.html#metricsspectatorservo-和-atlas" title="22. Metrics：Spectator，Servo 和 Atlas"> 22. Metrics：Spectator，Servo 和 Atlas <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_netflix-metrics.html#_dimensional_vs_hierarchical_metrics" title="22.1. 维度与分层 Metrics"> 22.1. 维度与分层 Metrics </a> </li>
<li> <a href="multi_netflix-metrics.html#_default_metrics_collection" title="22.2. 默认 Metrics 集合"> 22.2. 默认 Metrics 集合 </a> </li>
<li> <a href="multi_netflix-metrics.html#netflix-metrics-spectator" title="22.3. Metrics Collection：Spectator"> 22.3. Metrics Collection：Spectator <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_netflix-metrics.html#_spectator_counter" title="22.3.1. Spectator Counter"> 22.3.1. Spectator Counter </a> </li>
<li> <a href="multi_netflix-metrics.html#_spectator_timer" title="22.3.2. Spectator Timer"> 22.3.2. Spectator Timer </a> </li>
<li> <a href="multi_netflix-metrics.html#_spectator_gauge" title="22.3.3. Spectator Gauge"> 22.3.3. Spectator Gauge </a> </li>
<li> <a href="multi_netflix-metrics.html#_spectator_distribution_summaries" title="22.3.4. Spectator 分布摘要"> 22.3.4. Spectator 分布摘要 </a> </li>
</ul> </li>
<li> <a href="multi_netflix-metrics.html#netflix-metrics-servo" title="22.4. Metrics Collection：Servo"> 22.4. Metrics Collection：Servo <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_netflix-metrics.html#_creating_servo_monitors" title="22.4.1. Creating Servo Monitors"> 22.4.1. Creating Servo Monitors </a> </li>
</ul> </li>
<li> <a href="multi_netflix-metrics.html#netflix-metrics-atlas" title="22.5. Metrics 后端：Atlas"> 22.5. Metrics 后端：Atlas <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_netflix-metrics.html#_global_tags" title="22.5.1. Global 标签"> 22.5.1. Global 标签 </a> </li>
<li> <a href="multi_netflix-metrics.html#_using_atlas" title="22.5.2. 使用 Atlas"> 22.5.2. 使用 Atlas </a> </li>
</ul> </li>
<li> <a href="multi_netflix-metrics.html#retrying-failed-requests" title="22.6. 重试失败的请求"> 22.6. 重试失败的请求 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_netflix-metrics.html#_backoff_policies" title="22.6.1. BackOff Policies"> 22.6.1. BackOff Policies </a> </li>
<li> <a href="multi_netflix-metrics.html#_configuration" title="22.6.2. 组态"> 22.6.2. 组态 </a> </li>
<li> <a href="multi_netflix-metrics.html#_zuul" title="22.6.3. Zuul"> 22.6.3. Zuul </a> </li>
</ul> </li>
</ul> </li>
<li> <a href="multi__http_clients.html#http-clients" title="23. HTTP Clients"> 23. HTTP Clients </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_stream.html#iv-spring-cloud-stream" title="IV. Spring Cloud Stream"> IV. Spring Cloud Stream <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__introducing_spring_cloud_stream.html#介绍-spring-cloud-stream" title="24. 介绍 Spring Cloud Stream"> 24. 介绍 Spring Cloud Stream </a> </li>
<li> <a href="multi__main_concepts.html#主要概念" title="25. 主要概念"> 25. 主要概念 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__main_concepts.html#_application_model" title="25.1. Application Model"> 25.1. Application Model <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__main_concepts.html#_fat_jar" title="25.1.1. Fat JAR"> 25.1.1. Fat JAR </a> </li>
</ul> </li>
<li> <a href="multi__main_concepts.html#_the_binder_abstraction" title="25.2. Binder 抽象"> 25.2. Binder 抽象 </a> </li>
<li> <a href="multi__main_concepts.html#_persistent_publish_subscribe_support" title="25.3. 持久 Publish-Subscribe 支持"> 25.3. 持久 Publish-Subscribe 支持 </a> </li>
<li> <a href="multi__main_concepts.html#consumer-groups" title="25.4. Consumer Groups"> 25.4. Consumer Groups <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__main_concepts.html#durability" title="25.4.1. 耐久力"> 25.4.1. 耐久力 </a> </li>
</ul> </li>
<li> <a href="multi__main_concepts.html#partitioning" title="25.5. 分区支持"> 25.5. 分区支持 </a> </li>
</ul> </li>
<li> <a href="multi__programming_model.html#编程-model" title="26. 编程 Model"> 26. 编程 Model <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__programming_model.html#_declaring_and_binding_channels" title="26.1. 声明和 Binding Channels"> 26.1. 声明和 Binding Channels <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__programming_model.html#_triggering_binding_via_literal_enablebinding_literal" title="26.1.1. 通过@EnableBinding 触发 Binding"> 26.1.1. 通过@EnableBinding 触发 Binding </a> </li>
<li> <a href="multi__programming_model.html#__literal_input_literal_and_literal_output_literal" title="26.1.2. @Input 和@Output"> 26.1.2. @Input 和@Output <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__programming_model.html#_customizing_channel_names" title="自定义 Channel 名称"> 自定义 Channel 名称 </a> </li>
<li> <a href="multi__programming_model.html#__literal_source_literal_literal_sink_literal_and_literal_processor_literal" title="Source，Sink 和 Processor"> Source，Sink 和 Processor </a> </li>
</ul> </li>
<li> <a href="multi__programming_model.html#_accessing_bound_channels" title="26.1.3. 访问绑定的 Channels"> 26.1.3. 访问绑定的 Channels <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__programming_model.html#_injecting_the_bound_interfaces" title="注入绑定接口"> 注入绑定接口 </a> </li>
<li> <a href="multi__programming_model.html#_injecting_channels_directly" title="直接注入 Channels"> 直接注入 Channels </a> </li>
</ul> </li>
<li> <a href="multi__programming_model.html#_producing_and_consuming_messages" title="26.1.4. Producing 和 Consuming 消息"> 26.1.4. Producing 和 Consuming 消息 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__programming_model.html#_native_spring_integration_support" title="Native Spring Integration 支持"> Native Spring Integration 支持 </a> </li>
<li> <a href="multi__programming_model.html#_spring_integration_error_channel_support" title="Spring Integration Error Channel 支持"> Spring Integration Error Channel 支持 </a> </li>
<li> <a href="multi__programming_model.html#binder-error-channels" title="消息 Channel Binder 和 Error Channels"> 消息 Channel Binder 和 Error Channels </a> </li>
<li> <a href="multi__programming_model.html#_using_streamlistener_for_automatic_content_type_handling" title="使用 @StreamListener 进行自动 Content Type 处理"> 使用 @StreamListener 进行自动 Content Type 处理 </a> </li>
<li> <a href="multi__programming_model.html#_using_streamlistener_for_dispatching_messages_to_multiple_methods" title="使用 @StreamListener 将消息分派给多个方法"> 使用 @StreamListener 将消息分派给多个方法 </a> </li>
</ul> </li>
<li> <a href="multi__programming_model.html#_reactive_programming_support" title="26.1.5. Reactive Programming Support"> 26.1.5. Reactive Programming Support <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__programming_model.html#_reactor_based_handlers" title="Reactor-based 处理程序"> Reactor-based 处理程序 </a> </li>
<li> <a href="multi__programming_model.html#_rxjava_1_x_support" title="RxJava 1.x 支持"> RxJava 1.x 支持 </a> </li>
<li> <a href="multi__programming_model.html#_reactive_sources" title="Reactive Sources"> Reactive Sources </a> </li>
</ul> </li>
<li> <a href="multi__programming_model.html#_aggregation" title="26.1.6. 聚合"> 26.1.6. 聚合 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__programming_model.html#_configuring_aggregate_application" title="配置聚合应用程序"> 配置聚合应用程序 </a> </li>
<li> <a href="multi__programming_model.html#_configuring_binding_service_properties_for_non_self_contained_aggregate_application" title="为非自包含聚合 application 配置 binding service properties"> 为非自包含聚合 application 配置 binding service properties </a> </li>
</ul> </li>
</ul> </li>
</ul> </li>
<li> <a href="multi__binders.html#binders" title="27. Binders"> 27. Binders <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__binders.html#_producers_and_consumers" title="27.1. 生产者和消费者"> 27.1. 生产者和消费者 </a> </li>
<li> <a href="multi__binders.html#_binder_spi" title="27.2. Binder SPI"> 27.2. Binder SPI </a> </li>
<li> <a href="multi__binders.html#_binder_detection" title="27.3. Binder 检测"> 27.3. Binder 检测 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__binders.html#_classpath_detection" title="27.3.1. Classpath 检测"> 27.3.1. Classpath 检测 </a> </li>
</ul> </li>
<li> <a href="multi__binders.html#multiple-binders" title="27.4. Classpath 上有多个 Binder"> 27.4. Classpath 上有多个 Binder </a> </li>
<li> <a href="multi__binders.html#multiple-systems" title="27.5. 连接到多个系统"> 27.5. 连接到多个系统 </a> </li>
<li> <a href="multi__binders.html#_binder_configuration_properties" title="27.6. Binder configuration properties"> 27.6. Binder configuration properties </a> </li>
</ul> </li>
<li> <a href="multi__configuration_options.html#configuration-选项" title="28. Configuration 选项"> 28. Configuration 选项 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__configuration_options.html#_spring_cloud_stream_properties" title="28.1. Spring Cloud Stream Properties"> 28.1. Spring Cloud Stream Properties </a> </li>
<li> <a href="multi__configuration_options.html#binding-properties" title="28.2. Binding Properties"> 28.2. Binding Properties <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__configuration_options.html#_properties_for_use_of_spring_cloud_stream" title="28.2.1. Properties 使用 Spring Cloud Stream"> 28.2.1. Properties 使用 Spring Cloud Stream </a> </li>
<li> <a href="multi__configuration_options.html#_consumer_properties" title="28.2.2. Consumer properties"> 28.2.2. Consumer properties </a> </li>
<li> <a href="multi__configuration_options.html#_producer_properties" title="28.2.3. Producer Properties"> 28.2.3. Producer Properties </a> </li>
</ul> </li>
<li> <a href="multi__configuration_options.html#dynamicdestination" title="28.3. 使用动态绑定目标"> 28.3. 使用动态绑定目标 </a> </li>
</ul> </li>
<li> <a href="multi_contenttypemanagement.html#content-type-和-transformation" title="29. Content Type 和 Transformation"> 29. Content Type 和 Transformation <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_contenttypemanagement.html#mime-types" title="29.1. MIME 类型"> 29.1. MIME 类型 </a> </li>
<li> <a href="multi_contenttypemanagement.html#mime-types-and-java-types" title="29.2. MIME 类型和 Java 类型"> 29.2. MIME 类型和 Java 类型 </a> </li>
<li> <a href="multi_contenttypemanagement.html#_customizing_message_conversion" title="29.3. 自定义邮件转换"> 29.3. 自定义邮件转换 </a> </li>
<li> <a href="multi_contenttypemanagement.html#__literal_streamlistener_literal_and_message_conversion" title="29.4. @StreamListener 和消息转换"> 29.4. @StreamListener 和消息转换 </a> </li>
</ul> </li>
<li> <a href="multi_schema-evolution.html#schema-evolution-支持" title="30. Schema Evolution 支持"> 30. Schema Evolution 支持 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_schema-evolution.html#_schema_registry_client" title="30.1. Schema Registry Client"> 30.1. Schema Registry Client <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_schema-evolution.html#_schema_registry_client_properties" title="30.1.1. Schema Registry Client Properties"> 30.1.1. Schema Registry Client Properties </a> </li>
</ul> </li>
<li> <a href="multi_schema-evolution.html#_avro_schema_registry_client_message_converters" title="30.2. Avro Schema Registry Client 消息转换器"> 30.2. Avro Schema Registry Client 消息转换器 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_schema-evolution.html#_avro_schema_registry_message_converter_properties" title="30.2.1. Avro Schema 注册表消息转换器 Properties"> 30.2.1. Avro Schema 注册表消息转换器 Properties </a> </li>
</ul> </li>
<li> <a href="multi_schema-evolution.html#_apache_avro_message_converters" title="30.3. Apache Avro 消息转换器"> 30.3. Apache Avro 消息转换器 </a> </li>
<li> <a href="multi_schema-evolution.html#_converters_with_schema_support" title="30.4. 具有 Schema 支持的转换器"> 30.4. 具有 Schema 支持的转换器 </a> </li>
<li> <a href="multi_schema-evolution.html#_schema_registry_server" title="30.5. Schema Registry Server"> 30.5. Schema Registry Server <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_schema-evolution.html#_schema_registry_server_api" title="30.5.1. Schema Registry Server API"> 30.5.1. Schema Registry Server API <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_schema-evolution.html#spring-cloud-stream-overview-registering-new-schema" title="注册一个新的 Schema"> 注册一个新的 Schema </a> </li>
<li> <a href="multi_schema-evolution.html#spring-cloud-stream-overview-retrieve-schema-subject-format-version" title="按主题，格式和 Version 检索现有 Schema"> 按主题，格式和 Version 检索现有 Schema </a> </li>
<li> <a href="multi_schema-evolution.html#spring-cloud-stream-overview-retrieve-schema-subject-format" title="按主题和格式检索现有 Schema"> 按主题和格式检索现有 Schema </a> </li>
<li> <a href="multi_schema-evolution.html#spring-cloud-stream-overview-retrieve-schema-id" title="按 ID 检索现有 Schema"> 按 ID 检索现有 Schema </a> </li>
<li> <a href="multi_schema-evolution.html#spring-cloud-stream-overview-deleting-schema-subject-format-version" title="按主题，格式和 Version 删除 Schema"> 按主题，格式和 Version 删除 Schema </a> </li>
<li> <a href="multi_schema-evolution.html#spring-cloud-stream-overview-deleting-schema-id" title="按 ID 删除 Schema"> 按 ID 删除 Schema </a> </li>
<li> <a href="multi_schema-evolution.html#spring-cloud-stream-overview-deleting-schema-subject" title="按主题删除 Schema"> 按主题删除 Schema </a> </li>
</ul> </li>
<li> <a href="multi_schema-evolution.html#_using_confluent_s_schema_registry" title="30.5.2. 使用 Confluent 的 Schema Registry"> 30.5.2. 使用 Confluent 的 Schema Registry </a> </li>
</ul> </li>
<li> <a href="multi_schema-evolution.html#_schema_registration_and_resolution" title="30.6. Schema 注册和解决方案"> 30.6. Schema 注册和解决方案 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_schema-evolution.html#spring-cloud-stream-overview-schema-registration-process" title="30.6.1. Schema Registration Process(Serialization)"> 30.6.1. Schema Registration Process(Serialization) </a> </li>
<li> <a href="multi_schema-evolution.html#spring-cloud-stream-overview-schema-resolution-process" title="30.6.2. Schema Resolution Process(反序列化)"> 30.6.2. Schema Resolution Process(反序列化) </a> </li>
</ul> </li>
</ul> </li>
<li> <a href="multi__inter_application_communication.html#inter-application-沟通" title="31. Inter-Application 沟通"> 31. Inter-Application 沟通 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__inter_application_communication.html#_connecting_multiple_application_instances" title="31.1. 连接多个 Application 实例"> 31.1. 连接多个 Application 实例 </a> </li>
<li> <a href="multi__inter_application_communication.html#_instance_index_and_instance_count" title="31.2. 实例索引和实例计数"> 31.2. 实例索引和实例计数 </a> </li>
<li> <a href="multi__inter_application_communication.html#_partitioning" title="31.3. 分区"> 31.3. 分区 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__inter_application_communication.html#_configuring_output_bindings_for_partitioning" title="31.3.1. 配置输出绑定以进行分区"> 31.3.1. 配置输出绑定以进行分区 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__inter_application_communication.html#_spring_managed_custom_literal_partitionkeyextractorclass_literal_implementations" title="Spring-managed 自定义 PartitionKeyExtractorClass implementations"> Spring-managed 自定义 PartitionKeyExtractorClass implementations </a> </li>
<li> <a href="multi__inter_application_communication.html#_configuring_input_bindings_for_partitioning" title="配置输入绑定以进行分区"> 配置输入绑定以进行分区 </a> </li>
</ul> </li>
</ul> </li>
</ul> </li>
<li> <a href="multi__testing.html#测试" title="32. 测试"> 32. 测试 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__testing.html#_disabling_the_test_binder_autoconfiguration" title="32.1. 禁用测试 binder 自动配置"> 32.1. 禁用测试 binder 自动配置 </a> </li>
</ul> </li>
<li> <a href="multi__health_indicator_5.html#健康指标" title="33. 健康指标"> 33. 健康指标 </a> </li>
<li> <a href="multi__metrics_emitter.html#metrics-emitter" title="34. Metrics Emitter"> 34. Metrics Emitter </a> </li>
<li> <a href="multi__samples.html#samples" title="35. samples"> 35. samples </a> </li>
<li> <a href="multi__getting_started.html#入门" title="36. 入门"> 36. 入门 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__getting_started.html#_deploying_stream_applications_on_cloudfoundry" title="36.1. 在 CloudFoundry 上部署 Stream applications"> 36.1. 在 CloudFoundry 上部署 Stream applications </a> </li>
</ul> </li>
</ul> </li>
<li> <a href="multi__binder_implementations.html#v-binder-implementations" title="V. Binder Implementations"> V. Binder Implementations <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__apache_kafka_binder.html#apache-kafka-binder" title="37. Apache Kafka Binder"> 37. Apache Kafka Binder <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__apache_kafka_binder.html#_usage" title="37.1. 用法"> 37.1. 用法 </a> </li>
<li> <a href="multi__apache_kafka_binder.html#_apache_kafka_binder_overview" title="37.2. Apache Kafka Binder 概述"> 37.2. Apache Kafka Binder 概述 </a> </li>
<li> <a href="multi__apache_kafka_binder.html#_configuration_options_2" title="37.3. Configuration 选项"> 37.3. Configuration 选项 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__apache_kafka_binder.html#_kafka_binder_properties" title="37.3.1. Kafka Binder Properties"> 37.3.1. Kafka Binder Properties </a> </li>
<li> <a href="multi__apache_kafka_binder.html#_kafka_consumer_properties" title="37.3.2. Kafka Consumer Properties"> 37.3.2. Kafka Consumer Properties </a> </li>
<li> <a href="multi__apache_kafka_binder.html#_kafka_producer_properties" title="37.3.3. Kafka Producer Properties"> 37.3.3. Kafka Producer Properties </a> </li>
<li> <a href="multi__apache_kafka_binder.html#_usage_examples" title="37.3.4. 用法示例"> 37.3.4. 用法示例 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__apache_kafka_binder.html#_example_setting_literal_autocommitoffset_literal_false_and_relying_on_manual_acking" title="示例：设置 autoCommitOffset false 并依赖于手动执行."> 示例：设置 autoCommitOffset false 并依赖于手动执行. </a> </li>
<li> <a href="multi__apache_kafka_binder.html#_example_security_configuration" title="Example：security configuration"> Example：security configuration </a> </li>
<li> <a href="multi__apache_kafka_binder.html#_using_the_binder_with_apache_kafka_0_10" title="将 binder 与 Apache Kafka 0.10 一起使用"> 将 binder 与 Apache Kafka 0.10 一起使用 </a> </li>
<li> <a href="multi__apache_kafka_binder.html#exclude-admin-utils" title="从基于 binder 的 application 的 classpath 中排除 Kafka broker jar"> 从基于 binder 的 application 的 classpath 中排除 Kafka broker jar </a> </li>
</ul> </li>
</ul> </li>
<li> <a href="multi__apache_kafka_binder.html#_kafka_streams_binding_capabilities_of_spring_cloud_stream" title="37.4. Kafka Streams _Bring Spring Cloud Stream 的功能"> 37.4. Kafka Streams _Bring Spring Cloud Stream 的功能 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__apache_kafka_binder.html#_usage_example_of_high_level_streams_dsl" title="37.4.1. 用法示例高 level 流 DSL"> 37.4.1. 用法示例高 level 流 DSL </a> </li>
<li> <a href="multi__apache_kafka_binder.html#_support_for_interactive_queries" title="37.4.2. 支持交互式查询"> 37.4.2. 支持交互式查询 </a> </li>
<li> <a href="multi__apache_kafka_binder.html#_kafka_streams_properties" title="37.4.3. Kafka Streams properties"> 37.4.3. Kafka Streams properties </a> </li>
</ul> </li>
<li> <a href="multi__apache_kafka_binder.html#kafka-error-channels" title="37.5. 错误 Channels"> 37.5. 错误 Channels </a> </li>
<li> <a href="multi__apache_kafka_binder.html#kafka-metrics" title="37.6. Kafka Metrics"> 37.6. Kafka Metrics </a> </li>
<li> <a href="multi__apache_kafka_binder.html#kafka-dlq-processing" title="37.7. Dead-Letter Topic Processing"> 37.7. Dead-Letter Topic Processing </a> </li>
</ul> </li>
<li> <a href="multi__rabbitmq_binder.html#rabbitmq-binder" title="38. RabbitMQ Binder"> 38. RabbitMQ Binder <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__rabbitmq_binder.html#_usage_2" title="38.1. 用法"> 38.1. 用法 </a> </li>
<li> <a href="multi__rabbitmq_binder.html#_rabbitmq_binder_overview" title="38.2. RabbitMQ Binder 概述"> 38.2. RabbitMQ Binder 概述 </a> </li>
<li> <a href="multi__rabbitmq_binder.html#_configuration_options_3" title="38.3. Configuration 选项"> 38.3. Configuration 选项 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__rabbitmq_binder.html#rabbit-binder-properties" title="38.3.1. RabbitMQ Binder Properties"> 38.3.1. RabbitMQ Binder Properties </a> </li>
<li> <a href="multi__rabbitmq_binder.html#_rabbitmq_consumer_properties" title="38.3.2. RabbitMQ Consumer Properties"> 38.3.2. RabbitMQ Consumer Properties </a> </li>
<li> <a href="multi__rabbitmq_binder.html#_rabbit_producer_properties" title="38.3.3. Rabbit Producer Properties"> 38.3.3. Rabbit Producer Properties </a> </li>
</ul> </li>
<li> <a href="multi__rabbitmq_binder.html#_retry_with_the_rabbitmq_binder" title="38.4. 使用 RabbitMQ Binder 重试"> 38.4. 使用 RabbitMQ Binder 重试 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__rabbitmq_binder.html#_overview" title="38.4.1. 概观"> 38.4.1. 概观 </a> </li>
<li> <a href="multi__rabbitmq_binder.html#_putting_it_all_together" title="38.4.2. 全部放在一起"> 38.4.2. 全部放在一起 </a> </li>
</ul> </li>
<li> <a href="multi__rabbitmq_binder.html#rabbit-error-channels" title="38.5. 错误 Channels"> 38.5. 错误 Channels </a> </li>
<li> <a href="multi__rabbitmq_binder.html#rabbit-dlq-processing" title="38.6. Dead-Letter 队列处理"> 38.6. Dead-Letter 队列处理 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__rabbitmq_binder.html#_non_partitioned_destinations" title="38.6.1. Non-Partitioned 目的地"> 38.6.1. Non-Partitioned 目的地 </a> </li>
<li> <a href="multi__rabbitmq_binder.html#_partitioned_destinations" title="38.6.2. 分区目的地"> 38.6.2. 分区目的地 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__rabbitmq_binder.html#_republishtodlq_false" title="republishToDlq=false"> republishToDlq=false </a> </li>
<li> <a href="multi__rabbitmq_binder.html#_republishtodlq_true" title="republishToDlq=true"> republishToDlq=true </a> </li>
</ul> </li>
</ul> </li>
</ul> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_bus.html#vi-spring-cloud-bus" title="VI. Spring Cloud Bus"> VI. Spring Cloud Bus <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__quick_start_2.html#快速开始" title="39. 快速开始"> 39. 快速开始 </a> </li>
<li> <a href="multi__addressing_an_instance.html#解决实例问题" title="40. 解决实例问题"> 40. 解决实例问题 </a> </li>
<li> <a href="multi__addressing_all_instances_of_a_service.html#解决服务的所有实例" title="41. 解决服务的所有实例"> 41. 解决服务的所有实例 </a> </li>
<li> <a href="multi__application_context_id_must_be_unique.html#application-context-id-必须是唯一" title="42. Application Context ID 必须是唯一"> 42. Application Context ID 必须是唯一 </a> </li>
<li> <a href="multi__customizing_the_message_broker.html#自定义消息-broker" title="43. 自定义消息 Broker"> 43. 自定义消息 Broker </a> </li>
<li> <a href="multi__tracing_bus_events.html#跟踪-bus-events" title="44. 跟踪 Bus Events"> 44. 跟踪 Bus Events </a> </li>
<li> <a href="multi__broadcasting_your_own_events.html#broadcasting-your-own-events" title="45. Broadcasting Your Own Events"> 45. Broadcasting Your Own Events <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__broadcasting_your_own_events.html#_registering_events_in_custom_packages" title="45.1. 在自定义包中注册 events"> 45.1. 在自定义包中注册 events </a> </li>
</ul> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_sleuth.html#vii-spring-cloud-sleuth" title="VII. Spring Cloud Sleuth"> VII. Spring Cloud Sleuth <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__introduction.html#介绍" title="46. 介绍"> 46. 介绍 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__introduction.html#_terminology" title="46.1. 术语"> 46.1. 术语 </a> </li>
<li> <a href="multi__introduction.html#_purpose" title="46.2. 目的"> 46.2. 目的 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__introduction.html#_distributed_tracing_with_zipkin" title="46.2.1. 使用 Zipkin 进行分布式跟踪"> 46.2.1. 使用 Zipkin 进行分布式跟踪 </a> </li>
<li> <a href="multi__introduction.html#_visualizing_errors" title="46.2.2. 可视化错误"> 46.2.2. 可视化错误 </a> </li>
<li> <a href="multi__introduction.html#_live_examples" title="46.2.3. 实例"> 46.2.3. 实例 </a> </li>
<li> <a href="multi__introduction.html#_log_correlation" title="46.2.4. Log 关联"> 46.2.4. Log 关联 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__introduction.html#_json_logback_with_logstash" title="使用 Logstash 的 JSON Logback"> 使用 Logstash 的 JSON Logback </a> </li>
</ul> </li>
<li> <a href="multi__introduction.html#_propagating_span_context" title="46.2.5. 传播 Span Context"> 46.2.5. 传播 Span Context <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__introduction.html#_baggage_vs_span_tags" title="Baggage vs. Span Tags"> Baggage vs. Span Tags </a> </li>
</ul> </li>
</ul> </li>
<li> <a href="multi__introduction.html#_adding_to_the_project" title="46.3. 添加到项目中"> 46.3. 添加到项目中 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__introduction.html#_only_sleuth_log_correlation" title="46.3.1. 只有 Sleuth(log 相关)"> 46.3.1. 只有 Sleuth(log 相关) </a> </li>
<li> <a href="multi__introduction.html#_sleuth_with_zipkin_via_http" title="46.3.2. Sleuth 通过 HTTP 与 Zipkin"> 46.3.2. Sleuth 通过 HTTP 与 Zipkin </a> </li>
<li> <a href="multi__introduction.html#_sleuth_with_zipkin_via_rabbitmq_or_kafka" title="46.3.3. Sleuth 与 Zipkin 通过 RabbitMQ 或 Kafka"> 46.3.3. Sleuth 与 Zipkin 通过 RabbitMQ 或 Kafka </a> </li>
</ul> </li>
</ul> </li>
<li> <a href="multi__additional_resources.html#其他资源" title="47. 其他资源"> 47. 其他资源 </a> </li>
<li> <a href="multi__features_2.html#特征" title="48. 特征"> 48. 特征 </a> </li>
<li> <a href="multi__sampling.html#采样" title="49. 采样"> 49. 采样 </a> </li>
<li> <a href="multi__instrumentation.html#仪表" title="50. 仪表"> 50. 仪表 </a> </li>
<li> <a href="multi__span_lifecycle.html#span-生命周期" title="51. Span 生命周期"> 51. Span 生命周期 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__span_lifecycle.html#creating-and-closing-spans" title="51.1. 创建和关闭 spans"> 51.1. 创建和关闭 spans </a> </li>
<li> <a href="multi__span_lifecycle.html#continuing-spans" title="51.2. 继续 spans"> 51.2. 继续 spans </a> </li>
<li> <a href="multi__span_lifecycle.html#creating-spans-with-explicit-parent" title="51.3. 使用显式 parent 创建 spans"> 51.3. 使用显式 parent 创建 spans </a> </li>
</ul> </li>
<li> <a href="multi__naming_spans.html#命名-spans" title="52. 命名 spans"> 52. 命名 spans <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__naming_spans.html#__spanname_annotation" title="52.1. @SpanName annotation"> 52.1. @SpanName annotation </a> </li>
<li> <a href="multi__naming_spans.html#_tostring_method" title="52.2. toString()方法"> 52.2. toString()方法 </a> </li>
</ul> </li>
<li> <a href="multi__managing_spans_with_annotations.html#使用-annotations-管理-spans" title="53. 使用 annotations 管理 spans"> 53. 使用 annotations 管理 spans <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__managing_spans_with_annotations.html#_rationale" title="53.1. 合理"> 53.1. 合理 </a> </li>
<li> <a href="multi__managing_spans_with_annotations.html#_creating_new_spans" title="53.2. 创建新的 spans"> 53.2. 创建新的 spans </a> </li>
<li> <a href="multi__managing_spans_with_annotations.html#_continuing_spans" title="53.3. 继续 spans"> 53.3. 继续 spans </a> </li>
<li> <a href="multi__managing_spans_with_annotations.html#_more_advanced_tag_setting" title="53.4. 更高级的标签设置"> 53.4. 更高级的标签设置 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__managing_spans_with_annotations.html#_custom_extractor" title="53.4.1. 定制提取器"> 53.4.1. 定制提取器 </a> </li>
<li> <a href="multi__managing_spans_with_annotations.html#_resolving_expressions_for_value" title="53.4.2. 解析 value 的表达式"> 53.4.2. 解析 value 的表达式 </a> </li>
<li> <a href="multi__managing_spans_with_annotations.html#_using_tostring_method" title="53.4.3. 使用 toString 方法"> 53.4.3. 使用 toString 方法 </a> </li>
</ul> </li>
</ul> </li>
<li> <a href="multi__customizations.html#自定义" title="54. 自定义"> 54. 自定义 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__customizations.html#_spring_integration" title="54.1. Spring Integration"> 54.1. Spring Integration </a> </li>
<li> <a href="multi__customizations.html#_http" title="54.2. HTTP"> 54.2. HTTP </a> </li>
<li> <a href="multi__customizations.html#_example" title="54.3. 例"> 54.3. 例 </a> </li>
<li> <a href="multi__customizations.html#_tracefilter" title="54.4. TraceFilter"> 54.4. TraceFilter </a> </li>
<li> <a href="multi__customizations.html#_custom_sa_tag_in_zipkin" title="54.5. Zipkin 中的自定义 SA 标记"> 54.5. Zipkin 中的自定义 SA 标记 </a> </li>
<li> <a href="multi__customizations.html#_custom_service_name" title="54.6. 自定义服务 name"> 54.6. 自定义服务 name </a> </li>
<li> <a href="multi__customizations.html#_customization_of_reported_spans" title="54.7. 报告 spans 的自定义"> 54.7. 报告 spans 的自定义 </a> </li>
<li> <a href="multi__customizations.html#_host_locator" title="54.8. Host 定位器"> 54.8. Host 定位器 </a> </li>
</ul> </li>
<li> <a href="multi__sending_spans_to_zipkin.html#将-spans-发送到-zipkin" title="55. 将 spans 发送到 Zipkin"> 55. 将 spans 发送到 Zipkin </a> </li>
<li> <a href="multi__span_data_as_messages.html#span-数据作为消息" title="56. Span 数据作为消息"> 56. Span 数据作为消息 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__span_data_as_messages.html#_zipkin_consumer" title="56.1. Zipkin Consumer"> 56.1. Zipkin Consumer </a> </li>
<li> <a href="multi__span_data_as_messages.html#_custom_consumer" title="56.2. 自定义 Consumer"> 56.2. 自定义 Consumer </a> </li>
</ul> </li>
<li> <a href="multi__metrics.html#metrics" title="57. Metrics"> 57. Metrics </a> </li>
<li> <a href="multi__integrations.html#集成" title="58. 集成"> 58. 集成 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__integrations.html#_runnable_and_callable" title="58.1. 可运行和可调用"> 58.1. 可运行和可调用 </a> </li>
<li> <a href="multi__integrations.html#_hystrix" title="58.2. Hystrix"> 58.2. Hystrix <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__integrations.html#_custom_concurrency_strategy" title="58.2.1. 自定义并发策略"> 58.2.1. 自定义并发策略 </a> </li>
<li> <a href="multi__integrations.html#_manual_command_setting" title="58.2.2. 手动命令设置"> 58.2.2. 手动命令设置 </a> </li>
</ul> </li>
<li> <a href="multi__integrations.html#_rxjava" title="58.3. RxJava"> 58.3. RxJava </a> </li>
<li> <a href="multi__integrations.html#_http_integration" title="58.4. HTTP integration"> 58.4. HTTP integration <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__integrations.html#_http_filter" title="58.4.1. HTTP 过滤器"> 58.4.1. HTTP 过滤器 </a> </li>
<li> <a href="multi__integrations.html#_handlerinterceptor" title="58.4.2. 的 HandlerInterceptor"> 58.4.2. 的 HandlerInterceptor </a> </li>
<li> <a href="multi__integrations.html#_async_servlet_support" title="58.4.3. Async Servlet 支持"> 58.4.3. Async Servlet 支持 </a> </li>
</ul> </li>
<li> <a href="multi__integrations.html#_http_client_integration" title="58.5. HTTP client integration"> 58.5. HTTP client integration <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__integrations.html#_synchronous_rest_template" title="58.5.1. 同步 Rest Template"> 58.5.1. 同步 Rest Template </a> </li>
<li> <a href="multi__integrations.html#_asynchronous_rest_template" title="58.5.2. 异步 Rest Template"> 58.5.2. 异步 Rest Template <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__integrations.html#_multiple_asynchronous_rest_templates" title="多个异步 Rest 模板"> 多个异步 Rest 模板 </a> </li>
</ul> </li>
<li> <a href="multi__integrations.html#_traverson" title="58.5.3. Traverson"> 58.5.3. Traverson </a> </li>
</ul> </li>
<li> <a href="multi__integrations.html#_feign" title="58.6. 假装"> 58.6. 假装 </a> </li>
<li> <a href="multi__integrations.html#_asynchronous_communication" title="58.7. 异步通信"> 58.7. 异步通信 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__integrations.html#__async_annotated_methods" title="58.7.1. @Async 带注释的方法"> 58.7.1. @Async 带注释的方法 </a> </li>
<li> <a href="multi__integrations.html#__scheduled_annotated_methods" title="58.7.2. @Scheduled 带注释的方法"> 58.7.2. @Scheduled 带注释的方法 </a> </li>
<li> <a href="multi__integrations.html#_executor_executorservice_and_scheduledexecutorservice" title="58.7.3. Executor，ExecutorService 和 ScheduledExecutorService"> 58.7.3. Executor，ExecutorService 和 ScheduledExecutorService <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__integrations.html#_customization_of_executors" title="执行者的定制"> 执行者的定制 </a> </li>
</ul> </li>
</ul> </li>
<li> <a href="multi__integrations.html#_messaging" title="58.8. 消息"> 58.8. 消息 </a> </li>
<li> <a href="multi__integrations.html#_zuul_2" title="58.9. Zuul"> 58.9. Zuul </a> </li>
<li> <a href="multi__integrations.html#_spring_cloud_function" title="58.10. Spring Cloud Function"> 58.10. Spring Cloud Function </a> </li>
</ul> </li>
<li> <a href="multi__running_examples.html#运行的例子" title="59. 运行的例子"> 59. 运行的例子 </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_consul.html#viii-spring-cloud-consul" title="VIII. Spring Cloud Consul"> VIII. Spring Cloud Consul <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_spring-cloud-consul-install.html#安装-consul" title="60. 安装 Consul"> 60. 安装 Consul </a> </li>
<li> <a href="multi_spring-cloud-consul-agent.html#consul-agent" title="61. Consul Agent"> 61. Consul Agent </a> </li>
<li> <a href="multi_spring-cloud-consul-discovery.html#使用-consul-进行服务发现" title="62. 使用 Consul 进行服务发现"> 62. 使用 Consul 进行服务发现 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_spring-cloud-consul-discovery.html#_how_to_activate" title="62.1. 如何激活"> 62.1. 如何激活 </a> </li>
<li> <a href="multi_spring-cloud-consul-discovery.html#_registering_with_consul" title="62.2. 注册 Consul"> 62.2. 注册 Consul </a> </li>
<li> <a href="multi_spring-cloud-consul-discovery.html#_http_health_check" title="62.3. HTTP 健康检查"> 62.3. HTTP 健康检查 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_spring-cloud-consul-discovery.html#_metadata_and_consul_tags" title="62.3.1. 元数据和 Consul 标记"> 62.3.1. 元数据和 Consul 标记 </a> </li>
<li> <a href="multi_spring-cloud-consul-discovery.html#_making_the_consul_instance_id_unique" title="62.3.2. 使 Consul 实例 ID 唯一"> 62.3.2. 使 Consul 实例 ID 唯一 </a> </li>
</ul> </li>
<li> <a href="multi_spring-cloud-consul-discovery.html#_looking_up_services" title="62.4. 查找服务"> 62.4. 查找服务 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_spring-cloud-consul-discovery.html#_using_ribbon" title="62.4.1. 使用 Ribbon"> 62.4.1. 使用 Ribbon </a> </li>
<li> <a href="multi_spring-cloud-consul-discovery.html#_using_the_discoveryclient" title="62.4.2. 使用 DiscoveryClient"> 62.4.2. 使用 DiscoveryClient </a> </li>
</ul> </li>
</ul> </li>
<li> <a href="multi_spring-cloud-consul-config.html#使用-consul-分发-configuration" title="63. 使用 Consul 分发 Configuration"> 63. 使用 Consul 分发 Configuration <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_spring-cloud-consul-config.html#_how_to_activate_2" title="63.1. 如何激活"> 63.1. 如何激活 </a> </li>
<li> <a href="multi_spring-cloud-consul-config.html#_customizing" title="63.2. 定制"> 63.2. 定制 </a> </li>
<li> <a href="multi_spring-cloud-consul-config.html#spring-cloud-consul-config-watch" title="63.3. 配置 Watch"> 63.3. 配置 Watch </a> </li>
<li> <a href="multi_spring-cloud-consul-config.html#spring-cloud-consul-config-format" title="63.4. YAML 或 Properties with Config"> 63.4. YAML 或 Properties with Config </a> </li>
<li> <a href="multi_spring-cloud-consul-config.html#spring-cloud-consul-config-git2consul" title="63.5. git2consul with Config"> 63.5. git2consul with Config </a> </li>
<li> <a href="multi_spring-cloud-consul-config.html#spring-cloud-consul-failfast" title="63.6. 快速失败"> 63.6. 快速失败 </a> </li>
</ul> </li>
<li> <a href="multi_spring-cloud-consul-retry.html#consul-重试" title="64. Consul 重试"> 64. Consul 重试 </a> </li>
<li> <a href="multi_spring-cloud-consul-bus.html#spring-cloud-bus-with-consul" title="65. Spring Cloud Bus with Consul"> 65. Spring Cloud Bus with Consul <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_spring-cloud-consul-bus.html#_how_to_activate_3" title="65.1. 如何激活"> 65.1. 如何激活 </a> </li>
</ul> </li>
<li> <a href="multi_spring-cloud-consul-hystrix.html#断路器与-hystrix" title="66. 断路器与 Hystrix"> 66. 断路器与 Hystrix </a> </li>
<li> <a href="multi_spring-cloud-consul-turbine.html#使用-turbine-和-consul-进行-hystrix-metrics-聚合" title="67. 使用 Turbine 和 Consul 进行 Hystrix metrics 聚合"> 67. 使用 Turbine 和 Consul 进行 Hystrix metrics 聚合 </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_zookeeper.html#ix-spring-cloud-zookeeper" title="IX. Spring Cloud Zookeeper"> IX. Spring Cloud Zookeeper <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_spring-cloud-zookeeper-install.html#安装-zookeeper" title="68. 安装 Zookeeper"> 68. 安装 Zookeeper </a> </li>
<li> <a href="multi_spring-cloud-zookeeper-discovery.html#使用-zookeeper-进行服务发现" title="69. 使用 Zookeeper 进行服务发现"> 69. 使用 Zookeeper 进行服务发现 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_spring-cloud-zookeeper-discovery.html#_how_to_activate_4" title="69.1. 如何激活"> 69.1. 如何激活 </a> </li>
<li> <a href="multi_spring-cloud-zookeeper-discovery.html#_registering_with_zookeeper" title="69.2. 注册 Zookeeper"> 69.2. 注册 Zookeeper </a> </li>
<li> <a href="multi_spring-cloud-zookeeper-discovery.html#_using_the_discoveryclient_2" title="69.3. 使用 DiscoveryClient"> 69.3. 使用 DiscoveryClient </a> </li>
</ul> </li>
<li> <a href="multi_spring-cloud-zookeeper-netflix.html#将-spring-cloud-zookeeper-与-spring-cloud-netflix-组件一起使用" title="70. 将 Spring Cloud Zookeeper 与 Spring Cloud Netflix 组件一起使用"> 70. 将 Spring Cloud Zookeeper 与 Spring Cloud Netflix 组件一起使用 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_spring-cloud-zookeeper-netflix.html#_ribbon_with_zookeeper" title="70.1. Ribbon 与 Zookeeper"> 70.1. Ribbon 与 Zookeeper </a> </li>
</ul> </li>
<li> <a href="multi_spring-cloud-zookeeper-service-registry.html#spring-cloud-zookeeper-和-service-registry" title="71. Spring Cloud Zookeeper 和 Service Registry"> 71. Spring Cloud Zookeeper 和 Service Registry <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_spring-cloud-zookeeper-service-registry.html#_instance_status" title="71.1. 实例状态"> 71.1. 实例状态 </a> </li>
</ul> </li>
<li> <a href="multi_spring-cloud-zookeeper-dependencies.html#zookeeper-依赖关系" title="72. Zookeeper 依赖关系"> 72. Zookeeper 依赖关系 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_spring-cloud-zookeeper-dependencies.html#_using_the_zookeeper_dependencies" title="72.1. 使用 Zookeeper 依赖项"> 72.1. 使用 Zookeeper 依赖项 </a> </li>
<li> <a href="multi_spring-cloud-zookeeper-dependencies.html#_how_to_activate_zookeeper_dependencies" title="72.2. 如何激活 Zookeeper 依赖项"> 72.2. 如何激活 Zookeeper 依赖项 </a> </li>
<li> <a href="multi_spring-cloud-zookeeper-dependencies.html#_setting_up_zookeeper_dependencies" title="72.3. 设置 Zookeeper 依赖项"> 72.3. 设置 Zookeeper 依赖项 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_spring-cloud-zookeeper-dependencies.html#_aliases" title="72.3.1. 别名"> 72.3.1. 别名 </a> </li>
<li> <a href="multi_spring-cloud-zookeeper-dependencies.html#_path" title="72.3.2. 路径"> 72.3.2. 路径 </a> </li>
<li> <a href="multi_spring-cloud-zookeeper-dependencies.html#_load_balancer_type" title="72.3.3. 负载平衡器类型"> 72.3.3. 负载平衡器类型 </a> </li>
<li> <a href="multi_spring-cloud-zookeeper-dependencies.html#_content_type_template_and_version" title="72.3.4. Content-Type 模板和 version"> 72.3.4. Content-Type 模板和 version </a> </li>
<li> <a href="multi_spring-cloud-zookeeper-dependencies.html#_default_headers" title="72.3.5. 默认 headers"> 72.3.5. 默认 headers </a> </li>
<li> <a href="multi_spring-cloud-zookeeper-dependencies.html#_obligatory_dependencies" title="72.3.6. 强制依赖"> 72.3.6. 强制依赖 </a> </li>
<li> <a href="multi_spring-cloud-zookeeper-dependencies.html#_stubs" title="72.3.7. 存根"> 72.3.7. 存根 </a> </li>
</ul> </li>
<li> <a href="multi_spring-cloud-zookeeper-dependencies.html#_configuring_spring_cloud_zookeeper_dependencies" title="72.4. 配置 Spring Cloud Zookeeper 依赖项"> 72.4. 配置 Spring Cloud Zookeeper 依赖项 </a> </li>
</ul> </li>
<li> <a href="multi_spring-cloud-zookeeper-dependency-watcher.html#spring-cloud-zookeeper-依赖观察者" title="73. Spring Cloud Zookeeper 依赖观察者"> 73. Spring Cloud Zookeeper 依赖观察者 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_spring-cloud-zookeeper-dependency-watcher.html#_how_to_activate_5" title="73.1. 如何激活"> 73.1. 如何激活 </a> </li>
<li> <a href="multi_spring-cloud-zookeeper-dependency-watcher.html#_registering_a_listener" title="73.2. 注册 listener"> 73.2. 注册 listener </a> </li>
<li> <a href="multi_spring-cloud-zookeeper-dependency-watcher.html#_presence_checker" title="73.3. 存在检查器"> 73.3. 存在检查器 </a> </li>
</ul> </li>
<li> <a href="multi_spring-cloud-zookeeper-config.html#使用-zookeeper-分发-configuration" title="74. 使用 Zookeeper 分发 Configuration"> 74. 使用 Zookeeper 分发 Configuration <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_spring-cloud-zookeeper-config.html#_how_to_activate_6" title="74.1. 如何激活"> 74.1. 如何激活 </a> </li>
<li> <a href="multi_spring-cloud-zookeeper-config.html#_customizing_2" title="74.2. 定制"> 74.2. 定制 </a> </li>
<li> <a href="multi_spring-cloud-zookeeper-config.html#_acls" title="74.3. 访问控制列表"> 74.3. 访问控制列表 </a> </li>
</ul> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_security.html#x-spring-cloud-安全" title="X. Spring Cloud 安全"> X. Spring Cloud 安全 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__quickstart.html#快速开始" title="75. 快速开始"> 75. 快速开始 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__quickstart.html#_oauth2_single_sign_on" title="75.1. OAuth2 单点登录"> 75.1. OAuth2 单点登录 </a> </li>
<li> <a href="multi__quickstart.html#_oauth2_protected_resource" title="75.2. OAuth2 受保护资源"> 75.2. OAuth2 受保护资源 </a> </li>
</ul> </li>
<li> <a href="multi__more_detail.html#更多详情" title="76. 更多详情"> 76. 更多详情 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__more_detail.html#_single_sign_on" title="76.1. 单点登录"> 76.1. 单点登录 </a> </li>
<li> <a href="multi__more_detail.html#_token_relay" title="76.2. 令牌中继"> 76.2. 令牌中继 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__more_detail.html#_client_token_relay" title="76.2.1. Client Token Relay"> 76.2.1. Client Token Relay </a> </li>
<li> <a href="multi__more_detail.html#_client_token_relay_in_zuul_proxy" title="76.2.2. Zuul 代理中的 Client 令牌中继"> 76.2.2. Zuul 代理中的 Client 令牌中继 </a> </li>
<li> <a href="multi__more_detail.html#_resource_server_token_relay" title="76.2.3. 资源服务器令牌中继"> 76.2.3. 资源服务器令牌中继 </a> </li>
</ul> </li>
</ul> </li>
<li> <a href="multi__configuring_authentication_downstream_of_a_zuul_proxy.html#配置-zuul-代理下游的身份验证" title="77. 配置 Zuul 代理下游的身份验证"> 77. 配置 Zuul 代理下游的身份验证 </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_for_cloud_foundry.html#xi-spring-cloud-for-cloud-foundry" title="XI. Spring Cloud for Cloud Foundry"> XI. Spring Cloud for Cloud Foundry <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__discovery.html#发现" title="78. 发现"> 78. 发现 </a> </li>
<li> <a href="multi__single_sign_on_2.html#单点登录" title="79. 单点登录"> 79. 单点登录 </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_contract.html#xii-spring-cloud-contract" title="XII. Spring Cloud Contract"> XII. Spring Cloud Contract <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_contract_2.html#spring-cloud-contract" title="80. Spring Cloud Contract"> 80. Spring Cloud Contract </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_introduction.html#spring-cloud-contract-verifier-简介" title="81. Spring Cloud Contract Verifier 简介"> 81. Spring Cloud Contract Verifier 简介 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_contract_verifier_introduction.html#_why_a_contract_verifier" title="81.1. 为什么选择 Contract Verifier？"> 81.1. 为什么选择 Contract Verifier？ <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_contract_verifier_introduction.html#_testing_issues" title="81.1.1. 测试问题"> 81.1.1. 测试问题 </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_contract_verifier_introduction.html#_purposes" title="81.2. 目的"> 81.2. 目的 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_introduction.html#_how_it_works" title="81.3. 这个怎么运作"> 81.3. 这个怎么运作 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_contract_verifier_introduction.html#_defining_the_contract" title="81.3.1. 定义 contract"> 81.3.1. 定义 contract </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_introduction.html#_client_side" title="81.3.2. 客户端"> 81.3.2. 客户端 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_introduction.html#_server_side" title="81.3.3. 服务器端"> 81.3.3. 服务器端 </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_contract_verifier_introduction.html#_step_by_step_guide_to_consumer_driven_contracts_cdc" title="81.4. Step-by-step Consumer Driven Contracts(CDC)指南"> 81.4. Step-by-step Consumer Driven Contracts(CDC)指南 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_contract_verifier_introduction.html#_technical_note" title="81.4.1. 技术说明"> 81.4.1. 技术说明 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_introduction.html#_consumer_side_loan_issuance" title="81.4.2. 消费者方(贷款发行)"> 81.4.2. 消费者方(贷款发行) </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_introduction.html#_producer_side_fraud_detection_server" title="81.4.3. Producer 方面(欺诈检测服务器)"> 81.4.3. Producer 方面(欺诈检测服务器) </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_introduction.html#_consumer_side_loan_issuance_final_step" title="81.4.4. Consumer Side(Loan Issuance)决赛 Step"> 81.4.4. Consumer Side(Loan Issuance)决赛 Step </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_contract_verifier_introduction.html#_dependencies" title="81.5. 依赖"> 81.5. 依赖 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_introduction.html#_additional_links" title="81.6. 其他链接"> 81.6. 其他链接 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_contract_verifier_introduction.html#_spring_cloud_contract_video" title="81.6.1. Spring Cloud Contract video"> 81.6.1. Spring Cloud Contract video </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_introduction.html#_readings" title="81.6.2. 阅读"> 81.6.2. 阅读 </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_contract_verifier_introduction.html#_samples_2" title="81.7. samples"> 81.7. samples </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_contract_faq.html#spring-cloud-contract-faq" title="82. Spring Cloud Contract FAQ"> 82. Spring Cloud Contract FAQ <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_contract_faq.html#_why_use_spring_cloud_contract_verifier_and_not_x" title="82.1. 为什么要使用 Spring Cloud Contract Verifier 而不是 X？"> 82.1. 为什么要使用 Spring Cloud Contract Verifier 而不是 X？ </a> </li>
<li> <a href="multi__spring_cloud_contract_faq.html#_i_don_t_want_to_write_a_contract_in_groovy" title="82.2. 我不想在 Groovy 中写一个 contract！"> 82.2. 我不想在 Groovy 中写一个 contract！ </a> </li>
<li> <a href="multi__spring_cloud_contract_faq.html#_what_is_this_value_consumer_producer" title="82.3. 这是什么 value(consumer()，producer())？"> 82.3. 这是什么 value(consumer()，producer())？ </a> </li>
<li> <a href="multi__spring_cloud_contract_faq.html#_how_to_do_stubs_versioning" title="82.4. 如何进行 Stubs 版本控制？"> 82.4. 如何进行 Stubs 版本控制？ <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_contract_faq.html#_api_versioning" title="82.4.1. API 版本控制"> 82.4.1. API 版本控制 </a> </li>
<li> <a href="multi__spring_cloud_contract_faq.html#_jar_versioning" title="82.4.2. JAR 版本控制"> 82.4.2. JAR 版本控制 </a> </li>
<li> <a href="multi__spring_cloud_contract_faq.html#_dev_or_prod_stubs" title="82.4.3. Dev 或 prod stubs"> 82.4.3. Dev 或 prod stubs </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_contract_faq.html#_common_repo_with_contracts" title="82.5. Common repo with contracts"> 82.5. Common repo with contracts <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_contract_faq.html#_repo_structure" title="82.5.1. Repo 结构"> 82.5.1. Repo 结构 </a> </li>
<li> <a href="multi__spring_cloud_contract_faq.html#_workflow" title="82.5.2. 工作流程"> 82.5.2. 工作流程 </a> </li>
<li> <a href="multi__spring_cloud_contract_faq.html#_consumer" title="82.5.3. 消费者"> 82.5.3. 消费者 </a> </li>
<li> <a href="multi__spring_cloud_contract_faq.html#_producer" title="82.5.4. Producer"> 82.5.4. Producer </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_contract_faq.html#_can_i_have_multiple_base_classes_for_tests" title="82.6. 我可以为测试安装多个 base classes 吗？"> 82.6. 我可以为测试安装多个 base classes 吗？ </a> </li>
<li> <a href="multi__spring_cloud_contract_faq.html#_how_can_i_debug_the_request_response_being_sent_by_the_generated_tests_client" title="82.7. 如何调试生成的测试 client 发送的 request/response？"> 82.7. 如何调试生成的测试 client 发送的 request/response？ <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_contract_faq.html#_how_can_i_debug_the_mapping_request_response_being_sent_by_wiremock" title="82.7.1. 如何调试 WireMock 发送的 mapping/request/response？"> 82.7.1. 如何调试 WireMock 发送的 mapping/request/response？ </a> </li>
<li> <a href="multi__spring_cloud_contract_faq.html#_how_can_i_see_what_got_registered_in_the_http_server_stub" title="82.7.2. 如何查看在 HTTP 服务器存根中注册的内容？"> 82.7.2. 如何查看在 HTTP 服务器存根中注册的内容？ </a> </li>
<li> <a href="multi__spring_cloud_contract_faq.html#_can_i_reference_the_request_from_the_response" title="82.7.3. 我可以从响应中引用请求吗？"> 82.7.3. 我可以从响应中引用请求吗？ </a> </li>
<li> <a href="multi__spring_cloud_contract_faq.html#_can_i_reference_text_from_file" title="82.7.4. 我可以从文件中引用文本吗？"> 82.7.4. 我可以从文件中引用文本吗？ </a> </li>
</ul> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#spring-cloud-contract-verifier-setup" title="83. Spring Cloud Contract Verifier Setup"> 83. Spring Cloud Contract Verifier Setup <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#gradle-project" title="83.1. Gradle 项目"> 83.1. Gradle 项目 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#gradle-prerequisites" title="83.1.1. 先决条件"> 83.1.1. 先决条件 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#gradle-add-gradle-plugin" title="83.1.2. 添加带有依赖项的 Gradle 插件"> 83.1.2. 添加带有依赖项的 Gradle 插件 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#gradle-and-rest-assured" title="83.1.3. Gradle 和 Rest 保证 2.0"> 83.1.3. Gradle 和 Rest 保证 2.0 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#gradle-snapshot-versions" title="83.1.4. Gradle 的快照版本"> 83.1.4. Gradle 的快照版本 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#gradle-add-stubs" title="83.1.5. 添加存根"> 83.1.5. 添加存根 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#gradle-run-plugin" title="83.1.6. Run 插件"> 83.1.6. Run 插件 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#gradle-default-setup" title="83.1.7. 默认设置"> 83.1.7. 默认设置 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#gradle-configure-plugin" title="83.1.8. 配置插件"> 83.1.8. 配置插件 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#gradle-configuration-options" title="83.1.9. Configuration 选项"> 83.1.9. Configuration 选项 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#gradle-single-base-class" title="83.1.10. 所有测试的单 Base Class"> 83.1.10. 所有测试的单 Base Class </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#gradle-different-base-classes" title="83.1.11. Contracts 的不同 Base Classes"> 83.1.11. Contracts 的不同 Base Classes </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#gradle-invoking-generated-tests" title="83.1.12. 调用生成的测试"> 83.1.12. 调用生成的测试 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#gradle-consumer" title="83.1.13. Consumer 侧的 Spring Cloud Contract Verifier"> 83.1.13. Consumer 侧的 Spring Cloud Contract Verifier </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#maven-project" title="83.2. Maven 项目"> 83.2. Maven 项目 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#maven-add-plugin" title="83.2.1. 添加 maven 插件"> 83.2.1. 添加 maven 插件 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#maven-rest-assured" title="83.2.2. Maven 和 Rest 保证 2.0"> 83.2.2. Maven 和 Rest 保证 2.0 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#maven-snapshot-versions" title="83.2.3. Maven 的快照版本"> 83.2.3. Maven 的快照版本 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#maven-add-stubs" title="83.2.4. 添加存根"> 83.2.4. 添加存根 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#maven-run-plugin" title="83.2.5. Run 插件"> 83.2.5. Run 插件 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#maven-configure-plugin" title="83.2.6. 配置插件"> 83.2.6. 配置插件 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#maven-configuration-options" title="83.2.7. Configuration 选项"> 83.2.7. Configuration 选项 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#maven-single-base" title="83.2.8. 所有测试的单 Base Class"> 83.2.8. 所有测试的单 Base Class </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#maven-different-base" title="83.2.9. contracts 的 base classes 不同"> 83.2.9. contracts 的 base classes 不同 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#maven-invoking-generated-tests" title="83.2.10. 调用生成的测试"> 83.2.10. 调用生成的测试 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#maven-sts" title="83.2.11. Maven 插件和 STS"> 83.2.11. Maven 插件和 STS </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#_stubs_and_transitive_dependencies" title="83.3. 存根和传递依赖"> 83.3. 存根和传递依赖 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#_ci_server_setup" title="83.4. CI 服务器设置"> 83.4. CI 服务器设置 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#_scenarios" title="83.5. 方案"> 83.5. 方案 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#docker-project" title="83.6. Docker 项目"> 83.6. Docker 项目 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#_short_intro_to_maven_jars_and_binary_storage" title="83.6.1. Maven，JARs 和二进制存储的简短介绍"> 83.6.1. Maven，JARs 和二进制存储的简短介绍 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#_how_it_works_2" title="83.6.2. 这个怎么运作"> 83.6.2. 这个怎么运作 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#_environment_variables" title="环境变量"> 环境变量 </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#_example_of_usage" title="83.6.3. 使用示例"> 83.6.3. 使用示例 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_setup.html#docker-server-side" title="83.6.4. 服务器端(nodejs)"> 83.6.4. 服务器端(nodejs) </a> </li>
</ul> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_contract_verifier_messaging.html#spring-cloud-contract-verifier-messaging" title="84. Spring Cloud Contract Verifier Messaging"> 84. Spring Cloud Contract Verifier Messaging <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_contract_verifier_messaging.html#_integrations_2" title="84.1. 集成"> 84.1. 集成 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_messaging.html#_manual_integration_testing" title="84.2. 手动 Integration 测试"> 84.2. 手动 Integration 测试 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_messaging.html#_publisher_side_test_generation" title="84.3. Publisher-Side 测试生成"> 84.3. Publisher-Side 测试生成 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_contract_verifier_messaging.html#_scenario_1_no_input_message" title="84.3.1. 场景 1：没有输入消息"> 84.3.1. 场景 1：没有输入消息 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_messaging.html#_scenario_2_output_triggered_by_input" title="84.3.2. 场景 2：输入触发的输出"> 84.3.2. 场景 2：输入触发的输出 </a> </li>
<li> <a href="multi__spring_cloud_contract_verifier_messaging.html#_scenario_3_no_output_message" title="84.3.3. 场景 3：无输出消息"> 84.3.3. 场景 3：无输出消息 </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_contract_verifier_messaging.html#_consumer_stub_generation" title="84.4. Consumer Stub Generation"> 84.4. Consumer Stub Generation </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_contract_stub_runner.html#spring-cloud-contract-stub-runner" title="85. Spring Cloud Contract Stub Runner"> 85. Spring Cloud Contract Stub Runner <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_snapshot_versions" title="85.1. 快照版本"> 85.1. 快照版本 </a> </li>
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_publishing_stubs_as_jars" title="85.2. 将 Stubs 发布为 JAR"> 85.2. 将 Stubs 发布为 JAR </a> </li>
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_stub_runner_core" title="85.3. Stub Runner 核心"> 85.3. Stub Runner 核心 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_retrieving_stubs" title="85.3.1. 检索存根"> 85.3.1. 检索存根 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_stub_downloading" title="存根下载"> 存根下载 </a> </li>
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_classpath_scanning" title="Classpath 扫描"> Classpath 扫描 </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_running_stubs" title="85.3.2. 运行存根"> 85.3.2. 运行存根 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_running_using_main_app" title="使用主应用程序运行"> 使用主应用程序运行 </a> </li>
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_http_stubs" title="HTTP 存根"> HTTP 存根 </a> </li>
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_viewing_registered_mappings" title="查看已注册的映射"> 查看已注册的映射 </a> </li>
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_messaging_stubs" title="消息存根"> 消息存根 </a> </li>
</ul> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_stub_runner_junit_rule" title="85.4. Stub Runner JUnit 规则"> 85.4. Stub Runner JUnit 规则 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_maven_settings" title="85.4.1. Maven 设置"> 85.4.1. Maven 设置 </a> </li>
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_providing_fixed_ports" title="85.4.2. 提供固定端口"> 85.4.2. 提供固定端口 </a> </li>
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_fluent_api" title="85.4.3. Fluent API"> 85.4.3. Fluent API </a> </li>
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_stub_runner_with_spring" title="85.4.4. 与 Spring 的 Stub Runner"> 85.4.4. 与 Spring 的 Stub Runner </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_stub_runner_spring_cloud" title="85.5. Stub Runner Spring Cloud"> 85.5. Stub Runner Spring Cloud <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_stubbing_service_discovery" title="85.5.1. Stubbing Service Discovery"> 85.5.1. Stubbing Service Discovery <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_test_profiles_and_service_discovery" title="测试 profiles 和服务发现"> 测试 profiles 和服务发现 </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_additional_configuration" title="85.5.2. 额外的 Configuration"> 85.5.2. 额外的 Configuration </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_stub_runner_boot_application" title="85.6. Stub Runner Boot Application"> 85.6. Stub Runner Boot Application <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_how_to_use_it" title="85.6.1. 如何使用它？"> 85.6.1. 如何使用它？ <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_stub_runner_server" title="Stub Runner Server"> Stub Runner Server </a> </li>
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_stub_runner_server_fat_jar" title="Stub Runner Server Fat Jar"> Stub Runner Server Fat Jar </a> </li>
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_spring_cloud_cli" title="Spring Cloud CLI"> Spring Cloud CLI </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_endpoints_2" title="85.6.2. Endpoints"> 85.6.2. Endpoints <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_http_2" title="HTTP"> HTTP </a> </li>
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_messaging_2" title="消息"> 消息 </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_example_2" title="85.6.3. 例"> 85.6.3. 例 </a> </li>
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_stub_runner_boot_with_service_discovery" title="85.6.4. Stub Runner Boot with Service Discovery"> 85.6.4. Stub Runner Boot with Service Discovery </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_stubs_per_consumer" title="85.7. Stubs Per Consumer"> 85.7. Stubs Per Consumer </a> </li>
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_common" title="85.8. 共同"> 85.8. 共同 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_contract_stub_runner.html#common-properties-junit-spring" title="85.8.1. Common Properties for JUnit 和 Spring"> 85.8.1. Common Properties for JUnit 和 Spring </a> </li>
<li> <a href="multi__spring_cloud_contract_stub_runner.html#stub-runner-stub-ids" title="85.8.2. Stub Runner Stubs ID"> 85.8.2. Stub Runner Stubs ID </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_contract_stub_runner.html#stubrunner-docker" title="85.9. Stub Runner Docker"> 85.9. Stub Runner Docker <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_how_to_use_it_2" title="85.9.1. 如何使用它"> 85.9.1. 如何使用它 </a> </li>
<li> <a href="multi__spring_cloud_contract_stub_runner.html#_example_of_client_side_usage_in_a_non_jvm_project" title="85.9.2. 非 JVM 项目中 client 端用法的示例"> 85.9.2. 非 JVM 项目中 client 端用法的示例 </a> </li>
</ul> </li>
</ul> </li>
<li> <a href="multi__stub_runner_for_messaging.html#stub-runner-for-messaging" title="86. Stub Runner for Messaging"> 86. Stub Runner for Messaging <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__stub_runner_for_messaging.html#_stub_triggering" title="86.1. 存根触发"> 86.1. 存根触发 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__stub_runner_for_messaging.html#trigger-label" title="86.1.1. 按标签触发"> 86.1.1. 按标签触发 </a> </li>
<li> <a href="multi__stub_runner_for_messaging.html#trigger-group-artifact-ids" title="86.1.2. 由 Group 和 Artifact ID 触发"> 86.1.2. 由 Group 和 Artifact ID 触发 </a> </li>
<li> <a href="multi__stub_runner_for_messaging.html#trigger-artifact-ids" title="86.1.3. 由 Artifact ID 触发"> 86.1.3. 由 Artifact ID 触发 </a> </li>
<li> <a href="multi__stub_runner_for_messaging.html#trigger-all-messages" title="86.1.4. 触发所有消息"> 86.1.4. 触发所有消息 </a> </li>
</ul> </li>
<li> <a href="multi__stub_runner_for_messaging.html#_stub_runner_camel" title="86.2. Stub Runner Camel"> 86.2. Stub Runner Camel <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__stub_runner_for_messaging.html#_adding_the_runner_to_the_project" title="86.2.1. 将 Runner 添加到项目中"> 86.2.1. 将 Runner 添加到项目中 </a> </li>
<li> <a href="multi__stub_runner_for_messaging.html#_disabling_the_functionality" title="86.2.2. 禁用该功能"> 86.2.2. 禁用该功能 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__stub_runner_for_messaging.html#camel-scenario-1" title="场景 1(无输入消息)"> 场景 1(无输入消息) </a> </li>
<li> <a href="multi__stub_runner_for_messaging.html#camel-scenario-2" title="场景 2(输入触发输出)"> 场景 2(输入触发输出) </a> </li>
<li> <a href="multi__stub_runner_for_messaging.html#camel-scenario-3" title="场景 3(没有输出的输入)"> 场景 3(没有输出的输入) </a> </li>
</ul> </li>
</ul> </li>
<li> <a href="multi__stub_runner_for_messaging.html#_stub_runner_integration" title="86.3. Stub Runner Integration"> 86.3. Stub Runner Integration <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__stub_runner_for_messaging.html#_adding_the_runner_to_the_project_2" title="86.3.1. 将 Runner 添加到项目中"> 86.3.1. 将 Runner 添加到项目中 </a> </li>
<li> <a href="multi__stub_runner_for_messaging.html#_disabling_the_functionality_2" title="86.3.2. 禁用该功能"> 86.3.2. 禁用该功能 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__stub_runner_for_messaging.html#integration-scenario-1" title="场景 1(无输入消息)"> 场景 1(无输入消息) </a> </li>
<li> <a href="multi__stub_runner_for_messaging.html#integration-scenario-1" title="场景 2(输入触发输出)"> 场景 2(输入触发输出) </a> </li>
<li> <a href="multi__stub_runner_for_messaging.html#integration-scenario-3" title="场景 3(没有输出的输入)"> 场景 3(没有输出的输入) </a> </li>
</ul> </li>
</ul> </li>
<li> <a href="multi__stub_runner_for_messaging.html#_stub_runner_stream" title="86.4. Stub Runner Stream"> 86.4. Stub Runner Stream <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__stub_runner_for_messaging.html#_adding_the_runner_to_the_project_3" title="86.4.1. 将 Runner 添加到项目中"> 86.4.1. 将 Runner 添加到项目中 </a> </li>
<li> <a href="multi__stub_runner_for_messaging.html#_disabling_the_functionality_3" title="86.4.2. 禁用该功能"> 86.4.2. 禁用该功能 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__stub_runner_for_messaging.html#stream-scenario-1" title="场景 1(无输入消息)"> 场景 1(无输入消息) </a> </li>
<li> <a href="multi__stub_runner_for_messaging.html#stream-scenario-2" title="场景 2(输入触发输出)"> 场景 2(输入触发输出) </a> </li>
<li> <a href="multi__stub_runner_for_messaging.html#stream-scenario-3" title="场景 3(没有输出的输入)"> 场景 3(没有输出的输入) </a> </li>
</ul> </li>
</ul> </li>
<li> <a href="multi__stub_runner_for_messaging.html#_stub_runner_spring_amqp" title="86.5. Stub Runner Spring AMQP"> 86.5. Stub Runner Spring AMQP <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__stub_runner_for_messaging.html#_adding_the_runner_to_the_project_4" title="86.5.1. 将 Runner 添加到项目中"> 86.5.1. 将 Runner 添加到项目中 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__stub_runner_for_messaging.html#_triggering_the_message" title="触发消息"> 触发消息 </a> </li>
<li> <a href="multi__stub_runner_for_messaging.html#_spring_amqp_test_configuration" title="Spring AMQP Test Configuration"> Spring AMQP Test Configuration </a> </li>
</ul> </li>
</ul> </li>
</ul> </li>
<li> <a href="multi__contract_dsl.html#contract-dsl" title="87. Contract DSL"> 87. Contract DSL <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__contract_dsl.html#_limitations" title="87.1. 限制"> 87.1. 限制 </a> </li>
<li> <a href="multi__contract_dsl.html#_common_top_level_elements" title="87.2. Common Top-Level 元素"> 87.2. Common Top-Level 元素 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__contract_dsl.html#contract-dsl-description" title="87.2.1. 描述"> 87.2.1. 描述 </a> </li>
<li> <a href="multi__contract_dsl.html#contract-dsl-name" title="87.2.2. 名称"> 87.2.2. 名称 </a> </li>
<li> <a href="multi__contract_dsl.html#contract-dsl-ignoring-contracts" title="87.2.3. 忽略 Contracts"> 87.2.3. 忽略 Contracts </a> </li>
<li> <a href="multi__contract_dsl.html#contract-dsl-passing-values-from-files" title="87.2.4. 从 Files 传递值"> 87.2.4. 从 Files 传递值 </a> </li>
<li> <a href="multi__contract_dsl.html#contract-dsl-http-top-level-elements" title="87.2.5. HTTP Top-Level 元素"> 87.2.5. HTTP Top-Level 元素 </a> </li>
</ul> </li>
<li> <a href="multi__contract_dsl.html#_request" title="87.3. 请求"> 87.3. 请求 </a> </li>
<li> <a href="multi__contract_dsl.html#_response" title="87.4. 响应"> 87.4. 响应 </a> </li>
<li> <a href="multi__contract_dsl.html#_dynamic_properties" title="87.5. 动态 properties"> 87.5. 动态 properties <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__contract_dsl.html#_dynamic_properties_inside_the_body" title="87.5.1. 体内的动态 properties"> 87.5.1. 体内的动态 properties </a> </li>
<li> <a href="multi__contract_dsl.html#_regular_expressions" title="87.5.2. 常用表达"> 87.5.2. 常用表达 </a> </li>
<li> <a href="multi__contract_dsl.html#_passing_optional_parameters" title="87.5.3. 传递可选参数"> 87.5.3. 传递可选参数 </a> </li>
<li> <a href="multi__contract_dsl.html#_executing_custom_methods_on_the_server_side" title="87.5.4. 在服务器端执行自定义方法"> 87.5.4. 在服务器端执行自定义方法 </a> </li>
<li> <a href="multi__contract_dsl.html#_referencing_the_request_from_the_response" title="87.5.5. 引用响应中的请求"> 87.5.5. 引用响应中的请求 </a> </li>
<li> <a href="multi__contract_dsl.html#_registering_your_own_wiremock_extension" title="87.5.6. 注册您自己的 WireMock 扩展"> 87.5.6. 注册您自己的 WireMock 扩展 </a> </li>
<li> <a href="multi__contract_dsl.html#contract-matchers" title="87.5.7. 匹配器部分中的动态 Properties"> 87.5.7. 匹配器部分中的动态 Properties </a> </li>
</ul> </li>
<li> <a href="multi__contract_dsl.html#_jax_rs_support" title="87.6. JAX-RS 支持"> 87.6. JAX-RS 支持 </a> </li>
<li> <a href="multi__contract_dsl.html#_async_support" title="87.7. 异步支持"> 87.7. 异步支持 </a> </li>
<li> <a href="multi__contract_dsl.html#_working_with_context_paths" title="87.8. 使用 Context Paths"> 87.8. 使用 Context Paths </a> </li>
<li> <a href="multi__contract_dsl.html#_messaging_top_level_elements" title="87.9. 消息 Top-Level 元素"> 87.9. 消息 Top-Level 元素 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__contract_dsl.html#contract-dsl-output-triggered-method" title="87.9.1. 由方法触发的输出"> 87.9.1. 由方法触发的输出 </a> </li>
<li> <a href="multi__contract_dsl.html#contract-dsl-output-triggered-message" title="87.9.2. 输出由消息触发"> 87.9.2. 输出由消息触发 </a> </li>
<li> <a href="multi__contract_dsl.html#contract-dsl-consumer-producer" title="87.9.3. Consumer/Producer"> 87.9.3. Consumer/Producer </a> </li>
<li> <a href="multi__contract_dsl.html#contract-dsl-common" title="87.9.4. 共同"> 87.9.4. 共同 </a> </li>
</ul> </li>
<li> <a href="multi__contract_dsl.html#_multiple_contracts_in_one_file" title="87.10. 一个文件中有多个 Contracts"> 87.10. 一个文件中有多个 Contracts </a> </li>
</ul> </li>
<li> <a href="multi__customization.html#定制" title="88. 定制"> 88. 定制 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__customization.html#_extending_the_dsl" title="88.1. 扩展 DSL"> 88.1. 扩展 DSL <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__customization.html#_common_jar" title="88.1.1. Common JAR"> 88.1.1. Common JAR </a> </li>
<li> <a href="multi__customization.html#_adding_the_dependency_to_the_project" title="88.1.2. 将依赖项添加到项目中"> 88.1.2. 将依赖项添加到项目中 </a> </li>
<li> <a href="multi__customization.html#_test_the_dependency_in_the_project_s_dependencies" title="88.1.3. 测试项目依赖关系中的依赖关系"> 88.1.3. 测试项目依赖关系中的依赖关系 </a> </li>
<li> <a href="multi__customization.html#_test_a_dependency_in_the_plugin_s_dependencies" title="88.1.4. 测试插件依赖关系中的依赖关系"> 88.1.4. 测试插件依赖关系中的依赖关系 </a> </li>
<li> <a href="multi__customization.html#_referencing_classes_in_dsls" title="88.1.5. 在 DSL 中引用 classes"> 88.1.5. 在 DSL 中引用 classes </a> </li>
</ul> </li>
</ul> </li>
<li> <a href="multi__using_the_pluggable_architecture.html#使用-pluggable-architecture" title="89. 使用 Pluggable Architecture"> 89. 使用 Pluggable Architecture <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__using_the_pluggable_architecture.html#_custom_contract_converter" title="89.1. 自定义合同转换器"> 89.1. 自定义合同转换器 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__using_the_pluggable_architecture.html#_pact_converter" title="89.1.1. 契约转换器"> 89.1.1. 契约转换器 </a> </li>
<li> <a href="multi__using_the_pluggable_architecture.html#_pact_contract" title="89.1.2. 契约合同"> 89.1.2. 契约合同 </a> </li>
<li> <a href="multi__using_the_pluggable_architecture.html#_pact_for_producers" title="89.1.3. 生产者契约"> 89.1.3. 生产者契约 </a> </li>
<li> <a href="multi__using_the_pluggable_architecture.html#_pact_for_consumers" title="89.1.4. 消费者契约"> 89.1.4. 消费者契约 </a> </li>
</ul> </li>
<li> <a href="multi__using_the_pluggable_architecture.html#_using_the_custom_test_generator" title="89.2. 使用 Custom Test Generator"> 89.2. 使用 Custom Test Generator </a> </li>
<li> <a href="multi__using_the_pluggable_architecture.html#_using_the_custom_stub_generator" title="89.3. 使用 Custom Stub Generator"> 89.3. 使用 Custom Stub Generator </a> </li>
<li> <a href="multi__using_the_pluggable_architecture.html#_using_the_custom_stub_runner" title="89.4. 使用自定义存根运行器"> 89.4. 使用自定义存根运行器 </a> </li>
<li> <a href="multi__using_the_pluggable_architecture.html#_using_the_custom_stub_downloader" title="89.5. 使用 Custom Stub Downloader"> 89.5. 使用 Custom Stub Downloader </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_contract_wiremock.html#spring-cloud-contract-wiremock" title="90. Spring Cloud Contract WireMock"> 90. Spring Cloud Contract WireMock <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__spring_cloud_contract_wiremock.html#_registering_stubs_automatically" title="90.1. 自动注册存根"> 90.1. 自动注册存根 </a> </li>
<li> <a href="multi__spring_cloud_contract_wiremock.html#_using_files_to_specify_the_stub_bodies" title="90.2. 使用 Files 指定存根体"> 90.2. 使用 Files 指定存根体 </a> </li>
<li> <a href="multi__spring_cloud_contract_wiremock.html#_alternative_using_junit_rules" title="90.3. 替代方案：使用 JUnit 规则"> 90.3. 替代方案：使用 JUnit 规则 </a> </li>
<li> <a href="multi__spring_cloud_contract_wiremock.html#_relaxed_ssl_validation_for_rest_template" title="90.4. Rest Template 的轻松 SSL 验证"> 90.4. Rest Template 的轻松 SSL 验证 </a> </li>
<li> <a href="multi__spring_cloud_contract_wiremock.html#_wiremock_and_spring_mvc_mocks" title="90.5. WireMock 和 Spring MVC Mocks"> 90.5. WireMock 和 Spring MVC Mocks </a> </li>
<li> <a href="multi__spring_cloud_contract_wiremock.html#_customization_of_wiremock_configuration" title="90.6. 自定义 WireMock configuration"> 90.6. 自定义 WireMock configuration </a> </li>
<li> <a href="multi__spring_cloud_contract_wiremock.html#_generating_stubs_using_rest_docs" title="90.7. 使用 REST Docs 生成存根"> 90.7. 使用 REST Docs 生成存根 </a> </li>
<li> <a href="multi__spring_cloud_contract_wiremock.html#_generating_contracts_by_using_rest_docs" title="90.8. 使用 REST Docs 生成 Contracts"> 90.8. 使用 REST Docs 生成 Contracts </a> </li>
</ul> </li>
<li> <a href="multi__migrations.html#迁移" title="91. 迁移"> 91. 迁移 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__migrations.html#cloud-verifier-1.0-1.1" title="91.1. 1.0.x→1.1.x"> 91.1. 1.0.x→1.1.x <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__migrations.html#_new_structure_of_generated_stubs" title="91.1.1. 生成的存根的新结构"> 91.1.1. 生成的存根的新结构 </a> </li>
</ul> </li>
<li> <a href="multi__migrations.html#cloud-verifier-1.1-1.2" title="91.2. 1.1.x→1.2.x"> 91.2. 1.1.x→1.2.x <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__migrations.html#_custom_literal_httpserverstub_literal" title="91.2.1. 自定义 HttpServerStub"> 91.2.1. 自定义 HttpServerStub </a> </li>
<li> <a href="multi__migrations.html#_new_packages_for_generated_tests" title="91.2.2. 生成测试的新包"> 91.2.2. 生成测试的新包 </a> </li>
<li> <a href="multi__migrations.html#_new_methods_in_templateprocessor" title="91.2.3. TemplateProcessor 中的新方法"> 91.2.3. TemplateProcessor 中的新方法 </a> </li>
<li> <a href="multi__migrations.html#_restassured_3_0" title="91.2.4. RestAssured 3.0"> 91.2.4. RestAssured 3.0 </a> </li>
</ul> </li>
</ul> </li>
<li> <a href="multi__links.html#链接" title="92. 链接"> 92. 链接 </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_vault.html#xiii-spring-cloud-vault" title="XIII. Spring Cloud Vault"> XIII. Spring Cloud Vault <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__quick_start_3.html#快速开始" title="93. 快速开始"> 93. 快速开始 </a> </li>
<li> <a href="multi__client_side_usage_2.html#client-side-usage" title="94. Client Side Usage"> 94. Client Side Usage <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__client_side_usage_2.html#_authentication_2" title="94.1. 认证"> 94.1. 认证 </a> </li>
</ul> </li>
<li> <a href="multi_vault.config.authentication.html#验证方法" title="95. 验证方法"> 95. 验证方法 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_vault.config.authentication.html#vault.config.authentication.token" title="95.1. 令牌认证"> 95.1. 令牌认证 </a> </li>
<li> <a href="multi_vault.config.authentication.html#vault.config.authentication.appid" title="95.2. AppId 身份验证"> 95.2. AppId 身份验证 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_vault.config.authentication.html#_custom_userid" title="95.2.1. 自定义 UserId"> 95.2.1. 自定义 UserId </a> </li>
</ul> </li>
<li> <a href="multi_vault.config.authentication.html#_approle_authentication" title="95.3. AppRole 身份验证"> 95.3. AppRole 身份验证 </a> </li>
<li> <a href="multi_vault.config.authentication.html#vault.config.authentication.awsec2" title="95.4. AWS-EC2 认证"> 95.4. AWS-EC2 认证 </a> </li>
<li> <a href="multi_vault.config.authentication.html#vault.config.authentication.awsiam" title="95.5. AWS-IAM 认证"> 95.5. AWS-IAM 认证 </a> </li>
<li> <a href="multi_vault.config.authentication.html#vault.config.authentication.clientcert" title="95.6. TLS 证书身份验证"> 95.6. TLS 证书身份验证 </a> </li>
<li> <a href="multi_vault.config.authentication.html#vault.config.authentication.cubbyhole" title="95.7. Cubbyhole 认证"> 95.7. Cubbyhole 认证 </a> </li>
<li> <a href="multi_vault.config.authentication.html#vault.config.authentication.kubernetes" title="95.8. Kubernetes 认证"> 95.8. Kubernetes 认证 </a> </li>
</ul> </li>
<li> <a href="multi_vault.config.backends.html#secret-后端" title="96. Secret 后端"> 96. Secret 后端 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_vault.config.backends.html#vault.config.backends.generic" title="96.1. 通用后端"> 96.1. 通用后端 </a> </li>
<li> <a href="multi_vault.config.backends.html#vault.config.backends.consul" title="96.2. 领事"> 96.2. 领事 </a> </li>
<li> <a href="multi_vault.config.backends.html#vault.config.backends.rabbitmq" title="96.3. 的 RabbitMQ"> 96.3. 的 RabbitMQ </a> </li>
<li> <a href="multi_vault.config.backends.html#vault.config.backends.aws" title="96.4. AWS"> 96.4. AWS </a> </li>
</ul> </li>
<li> <a href="multi_vault.config.backends.database-backends.html#数据库后端" title="97. 数据库后端"> 97. 数据库后端 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi_vault.config.backends.database-backends.html#vault.config.backends.cassandra" title="97.1. Apache Cassandra"> 97.1. Apache Cassandra </a> </li>
<li> <a href="multi_vault.config.backends.database-backends.html#vault.config.backends.mongodb" title="97.2. MongoDB"> 97.2. MongoDB </a> </li>
<li> <a href="multi_vault.config.backends.database-backends.html#vault.config.backends.mysql" title="97.3. MySQL"> 97.3. MySQL </a> </li>
<li> <a href="multi_vault.config.backends.database-backends.html#vault.config.backends.postgresql" title="97.4. PostgreSQL"> 97.4. PostgreSQL </a> </li>
</ul> </li>
<li> <a href="multi_vault.config.backends.configurer.html#配置-propertysourcelocator-行为" title="98. 配置 PropertySourceLocator 行为"> 98. 配置 PropertySourceLocator 行为 </a> </li>
<li> <a href="multi__service_registry_configuration.html#service-registry-configuration" title="99. Service Registry Configuration"> 99. Service Registry Configuration </a> </li>
<li> <a href="multi_vault.config.fail-fast.html#vault-client-快速失败" title="100. Vault Client 快速失败"> 100. Vault Client 快速失败 </a> </li>
<li> <a href="multi_vault.config.ssl.html#vault-client-ssl-configuration" title="101. Vault Client SSL configuration"> 101. Vault Client SSL configuration </a> </li>
<li> <a href="multi_vault-lease-renewal.html#租赁生命周期管理续订和撤销" title="102. 租赁生命周期管理(续订和撤销)"> 102. 租赁生命周期管理(续订和撤销) </a> </li>
</ul> </li>
<li> <a href="multi__spring_cloud_function_2.html#xiv-spring-cloud-function" title="XIV. Spring Cloud Function"> XIV. Spring Cloud Function <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__introduction_2.html#介绍" title="103. 介绍"> 103. 介绍 </a> </li>
<li> <a href="multi__getting_started_2.html#入门" title="104. 入门"> 104. 入门 </a> </li>
<li> <a href="multi__building_and_running_a_function.html#building-和-running-一个-function" title="105. Building 和 Running 一个 Function"> 105. Building 和 Running 一个 Function </a> </li>
<li> <a href="multi__function_catalog_and_flexible_function_signatures.html#功能目录和灵活的功能签名" title="106. 功能目录和灵活的功能签名"> 106. 功能目录和灵活的功能签名 </a> </li>
<li> <a href="multi__standalone_web_applications.html#独立的-web-applications" title="107. 独立的 Web Applications"> 107. 独立的 Web Applications </a> </li>
<li> <a href="multi__standalone_streaming_applications.html#独立流媒体-applications" title="108. 独立流媒体 Applications"> 108. 独立流媒体 Applications </a> </li>
<li> <a href="multi__deploying_a_packaged_function.html#部署打包的-function" title="109. 部署打包的 Function"> 109. 部署打包的 Function </a> </li>
<li> <a href="multi__dynamic_compilation.html#动态编译" title="110. 动态编译"> 110. 动态编译 </a> </li>
<li> <a href="multi__serverless_platform_adapters.html#无服务器平台适配器" title="111. 无服务器平台适配器"> 111. 无服务器平台适配器 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__serverless_platform_adapters.html#_aws_lambda" title="111.1. AWS Lambda"> 111.1. AWS Lambda <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__serverless_platform_adapters.html#_introduction_3" title="111.1.1. 介绍"> 111.1.1. 介绍 </a> </li>
<li> <a href="multi__serverless_platform_adapters.html#_notes_on_jar_layout" title="111.1.2. 关于 JAR 布局的注释"> 111.1.2. 关于 JAR 布局的注释 </a> </li>
<li> <a href="multi__serverless_platform_adapters.html#_upload" title="111.1.3. 上传"> 111.1.3. 上传 </a> </li>
<li> <a href="multi__serverless_platform_adapters.html#_platfom_specific_features" title="111.1.4. Platfom Specific Features"> 111.1.4. Platfom Specific Features <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__serverless_platform_adapters.html#_http_and_api_gateway" title="HTTP 和 API 网关"> HTTP 和 API 网关 </a> </li>
</ul> </li>
</ul> </li>
<li> <a href="multi__serverless_platform_adapters.html#_azure_functions" title="111.2. Azure 功能"> 111.2. Azure 功能 <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__serverless_platform_adapters.html#_notes_on_jar_layout_2" title="111.2.1. 关于 JAR 布局的注释"> 111.2.1. 关于 JAR 布局的注释 </a> </li>
<li> <a href="multi__serverless_platform_adapters.html#_json_configuration" title="111.2.2. JSON Configuration"> 111.2.2. JSON Configuration </a> </li>
<li> <a href="multi__serverless_platform_adapters.html#_build" title="111.2.3. 建立"> 111.2.3. 建立 </a> </li>
<li> <a href="multi__serverless_platform_adapters.html#_running_the_sample" title="111.2.4. 运行 sample"> 111.2.4. 运行 sample </a> </li>
</ul> </li>
<li> <a href="multi__serverless_platform_adapters.html#_apache_openwhisk" title="111.3. Apache Openwhisk"> 111.3. Apache Openwhisk <i class="exc-trigger fa"></i></a>
<ul class="articles">
<li> <a href="multi__serverless_platform_adapters.html#_quick_start_4" title="111.3.1. 快速开始"> 111.3.1. 快速开始 </a> </li>
</ul> </li>
</ul> </li>
</ul> </li>
<li> <a href="multi__appendix_compendium_of_configuration_properties.html#xv-附录configuration-properties-的汇编" title="XV. 附录：Configuration Properties 的汇编"> XV. 附录：Configuration Properties 的汇编 </a> </li>
</ul></div>
</div>
</section>
# Spring Cloud Config : 配置管理中心
1. Config服务注册到本地的Eureka服务中。
2. 配置文件是放在Git仓库中的（例如Github或GitLab）。
3. 其他服务通过Eureka发现Config服务，Config服务再从Git仓库中根据服务名拉取配置文件
# Spring Cloud Eureka ：服务发现
## 说明：



#一、resources/bootstrap.yml文件中是EurekaServer常用的配置项。</br>
<pre>
#==============================================================================================================================================
#该文件中的配置项都是EurekaServer通用的配置，对于一些环境差异的配置项在application-'*'.yml中定义。在应用启动的时候添加--spring.profiles.active='*'参数。
#该文件中的配置可在application-*.yml文件重新定义进行覆盖，应用启动时后加载的配置会覆盖先加载的配置。
#对于eureka.client.service-url.defaultZone配置项中的环境变量，是用来配置EurekaServer高可用集群时指定其他EurekaServer Instance用的。
#===============================================================================================================================================
spring:
  application:
    name: eureka-server-discovery
server:
  port: 8080
security:
  basic:
    enabled: false
  user:
    name: user
    password: password
management:
  security:
    enabled: false
eureka:
  instance:
    prefer-ip-address: true
  client:
    #自己是注册中心，不向注册中心注册自己
    register-with-eureka: false
    #自己是注册中心，只负责维护服务实例，不需要去检索服务实例
    fetch-registry: false
    #该配置项定义在bootstrap中是为了同一套代码和配置文件可以用来部署EurekaServer高可用集群，指定向其他EurekaSever实例的Domain URL来相互注册自己，以实现其中的服务清单相互同步，达到高可用。
    #需要在Target Jar包启动时设置应用的环境变量EUREKASEVER{1~3}为其他EurekaServer示例的IP地址+端口号
    service-url:
      defaultZone: http://user:password@${EUREKASEVER1}/eureka,http://user:password@${EUREKASEVER2}/eureka,http://user:password@${EUREKASEVER3}/eureka
  server:
    #关闭自我保护机制
    enable-self-preservation: false
    #启用主动失效，并且每次主动失效检测间隔为3s
    eviction-interval-timer-in-ms: 3000
    #刷新readCacheMap的时间
    response-cache-update-interval-ms: 3000
</pre>

#二. 在resource/application-环境标识.yml中定义各个环境差异的配置，启动时只需指定相应的配置文件即可，启动命令如下：
<pre>
nohup java -jar eureka-0.0.1-SNAPSHOT.jar --EUREKASEVER1=ip1:port1 --EUREKASEVER2=ip2:port2 --EUREKASEVER3=ip3:port3 --spring.profiles.active=环境标识  >eurekaserver.log 2>&1 &
</pre>


Idea中指定Programma Argument为：--spring.profiles.active=环境标识

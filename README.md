# Spring Cloud Common Modules：<br>
* EurekaServer-----------------------Port:8080
* ZipkinServer-----------------------Port:9411
* ConfigSever------------------------Port:7001
* ZipkinClient-trace-1---------------Port:9101
* ZipkinClient-trace-2---------------Port:9102

# 项目简介
1. 项目中包含了Spring Cloud的标准组件：Eureka、Config、Zipkin等。
2. 顶级POM文件中定义了Spring Boot和Spring Cloud的版本依赖和插件依赖。
3. 模块内的POM文件中定义了各自服务的依赖。
4. 如需要各个模块的Jar包，只需使用Maven到相应模块的的根目录下Install就可以。
5. 各个模块的根目录也包含RADME.md

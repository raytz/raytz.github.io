#1. 微服务
###1.1 多微的服务才是微服务
业界没有统一的标准，曾听说过要微到一个函数是一个服务，这样管理起来简直就是个灾难。

一般方式是按照业务纬度进行划分，形成清晰、职责单一的服务即可。

###1.2 微服务的通讯方式
业务也没有划分统一的标准，常见的RPC方式有gRPC、apache thrift、dubbo、HTTP。这些方案主要是解决数据如何打包、传输与解包。


###1.3 服务治理
* 服务注册与发现
* 身份验证与授权
* 服务的伸缩控制
* 反向代理与负载均衡
* 路由控制
* 流量切换
* 日志管理
* 性能度量、监控与调优
* 分布式跟踪
* 过载保护
* 服务降级
* 服务部署与版本升级策略支持
* 错误处理

# 2. ServiceMesh
一般微服务之间的微服务治理逻辑的位置示意图：

![avatar](https://raw.githubusercontent.com/raytz/raytz.github.io/master/_data/cf5f69451ffa68b35cb3a61fc1c62d4a.png)

微服务治理逻辑被独立出来之后的位置示意图：

![avatar](https://raw.githubusercontent.com/raytz/raytz.github.io/master/_data/91d38eba53850b5d3d7bbce8d3f043e5.png)

由“Service Govern Logic”这一层组成的逻辑网络被定义为Service Mesh，每个微服务都包含一个Service Mesh的端点。

# 3. Istio
Istio项目是Service Mesh概念的最新实现，旨在所有主流集群管理平台上提供Service Mesh层，初期以实现Kubernetes上的服务治理层为目标。它由控制平面和数据平面组成（是不是感觉和SDN的设计理念相似啊）。控制平面由Go语言实现，包括pilot、mixer、auth三个组件；数据平面功能暂由Envoy在pod中以Sidecar的部署形式提供。下面是官方的架构图：

![avatar](https://raw.githubusercontent.com/raytz/raytz.github.io/master/_data/948ad297f5cccf1a6e887e998350d103.png)

# 参考资料
<a href="http://www.servicemesh.cn/?/article/33">使用 Istio治理微服务入门</a>


# Spring

## SpringCloud

### Eureka
工作流程

1. Eureka Server启动成功，等待服务端注册。在启动过程中如果配置了集群，集群之间定时通过Replicate同步注册表，每个Eureka Server都存在独立完整的服务注册表信息
2. Eureka Client启动时根据配置的Eureka Server地址去注册中心注册服务
3. Eureka Client会每30s向Eureka Server发送一次心跳请求（续约），证明客户端服务正常
4. 当Eureka Server在90s内没有收到Eureka Client的心跳，注册中心则认为该节点失效，会注销该实例
5. 单位时间内Eureka Server统计到有大量的Eureka Client没有上报心跳，则认为可能为网络异常，进入自我保护机制，不再剔除没有上报心跳的客户端
6. 当Eureka Client心跳请求恢复正常之后，Eureka Server自动退出自我保护模式
7. Eureka Client定时全量或者增量从注册中心获取服务注册表，并且将获取到的信息缓存到本地
8. 服务调用时，Eureka Client会先从本地缓存找寻调取的服务。如果获取不到，先从注册中心刷新注册表，再同步到本地缓存
9. Eureka Client获取到目标服务器信息，发起服务调用
10. Eureka Client程序关闭时向 Eureka Server发送取消请求，Eureka Server将实例从注册表中删除
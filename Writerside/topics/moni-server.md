# 数据监视服务

## Overview

`MoniServer`(`monitor server`)的功能是对`SCADA`数据库中的采集数据进行监视，主要功能包括告警、光字牌操作、监盘操作、极值统计、拓扑计算、设备监视等等。

`MoniServer`对性能的要求不如AcqServer高，除少数由界面发起的操作外，大多数功能基本以定时任务的方式注册至Server上，功能之间互不影响互不依赖。

`MoniServer`响应界面操作的时序图如下所示：

[//]: # (![]&#40;moni_server_seq.png&#41;)

```plantuml

@startuml


autonumber


actor "User" as User

participant "Browser" as Browser

participant "Moni Server" as Server #orange


activate User


User -> Browser: operate

activate Browser


Browser -> Server: send request

activate Server


Server -> Server: parse request


Server -> Server: do function


note right of Server: return result


Server --> Browser: return result

deactivate Server


Browser --> User: show result


@enduml



```

## 主备机制

`MoniServer`
程序的负载并不高，可以由主机执行所有任务，备机处于热备状态，其中涉及主备切换的任务是遥信变位告警：为了保证所有的遥信变位能够确实发送告警，备机需要监视主机对变位的处理情况，保存未发送告警的变位信息，在备机切换为主机时及时将这些变位信息发送告警。
当然严格来说还需要保证设备告警、越限告警等等的主备切换，为了不使程序过于复杂，在没有明确需求时暂不处理。

## 程序缓存

### 变化数据缓存

COSDataQueue/SOEDataQueue，与`AcqServer`一样，也使用固定大小的`spsc_queue`(单生产单消费无锁队列)
来放置缓存。变化数据缓存由平台网络事件回调线程生产，由`MoniServer`主线程的相关任务进行消费。

### 变位告警缓存

COSAlmQueue/SOEAlmQueue，告警信息缓存队列。

- 对于主机来说，由变位处理任务进行生产，
-
对于备机来说，订阅接收遥信变位告警，用于与变化数据缓存比较，防止在主备切换时丢失告警数据。缓存由平台网络事件回调线程生产，由`MoniServer`
主线程的变位处理任务进行消费。

### 服务请求缓存

RequestQueue，存放外部程序发送的监视服务请求缓存。缓存由平台网络事件回调线程生产，由`MoniServer`主线程的相关任务进行消费。

### 服务回复缓存

ResponseQueue，存放需要给外部程序发送的服务回复缓存。缓存由`MoniServer`主线程的相关任务进行生产、消费。

## 事件回调

`MoniServer`需要处理的事件包括：

- 装库事件(scada)；
- 配置文件变化事件；
- SCADA变化数据事件；
- SCADA遥信告警事件；
- 监视服务请求事件；

## 主要任务说明

### 变位处理任务

本任务对接收到的遥信变位事件进行处理，包括变位告警、SOE告警、双位置处理、计时告警、计次告警，生成告警数据缓存。
对于备机来说，本任务负责将超出缓存时间范围的数据进行消费。

### 越限监视任务

本任务对模拟量的越限情况进行监视。类似的任务还包括数据不变监视任务、数据跳变监视任务。

### 发送告警任务

本任务负责将告警数据缓存发送至`AlmServer`。
对于备机来说，本任务负责将超出缓存时间范围的数据进行消费。

### 服务调用路由任务

本任务负责将外部程序发送来的服务调用请求进行路由处理(分发给相应的子任务)，并将子任务的执行情况返回给外部程序。

### 拓扑计算任务

### 合理性校验任务

### 一次设备监视任务

### 二次设备监视任务

### 监盘任务

### 光字牌任务



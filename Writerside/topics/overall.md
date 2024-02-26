# 总体说明

## SCADA功能说明

`SCADA(Supervisory Control and Data Acquisition)`系统的基础功能可分为数据采集服务(`ACQ_SERVER`)、数据监视服务(`MONI_SERVER`)、控制操作服务(`CTRL_SERVER`)、专用计算服务(`CALC_SERVER`)、应用告警服务(`ALM_SERVER`)、数据查询服务(`DATA_SERVER`)六大部分。

各个服务的分工原则如下：

### 数据采集服务
数据处理服务的功能是将`FE`子系统的采集数据(生数据)获取至`SCADA`数据库中，并处理为熟数据以供后续程序使用。处理的范围包括模拟量、状态量、累计量和`SOE`。详见[**数据采集服务**](acq-server.md)页面。

### 数据监视服务
数据监视服务功能范围较广，主要功能为定期运行或触发式运行的监视功能，例如：
- 监盘操作；
- 一次设备监视；
- 二次设备监视；
- 拓扑着色；
- 光字牌监视；
有一些监视功能是由界面程序通过网络总线发来请求触发，例如监盘操作中的挂牌、置数等等。详见[**数据监视服务**](moni-server.md)页面。

### 控制操作服务
控制操作服务是为`SCADA`程序提供设备远程操作的功能，包括：
- 一次设备控制操作；
- 二次设备控制操作；
- 辅助设备控制操作；
- 联动控制操作；

### 专用计算服务
专用计算服务有别于通用计算服务，是带有应用业务逻辑的计算服务，功能包括光字牌计算、总加计算、事故总计算、新能源各类指标计算等。

### 应用告警服务
处理`SCADA`各程序发送的告警事件存入数据库，并根据配置提供音响、推画面、语音、短信等功能。

## 架构设计
`SCADA`与其他`CBB`的依赖调用关系如下图所示：

![servers.png](servers.png)
- 与平台`CBB`的交互通过`dll`调用方式来实现；
- 与`SCADA`数据库之间的交互通过数据总线来完成；
- 与`FE CBB`之间的交互通过数据总线、消息总线方式来完成；

除开`SCADA`数据库(`scadamdl/alarmmdl/calmdl`)以及平台运行必需的数据库，其余交互均通过网络方式实现，架构上不允许有数据库本地部署依赖。
`SCADA`中采集->监视->告警的架构设计图如下：

![acq-moni-alm.png](acq-moni-alm.png)

`SCADA`公共动态库的架构设计图如下：
> 公共动态库指所有SCADA程序(后台、界面)可以调用的公用功能动态库。

![scada_lib.png](scada_lib.png)


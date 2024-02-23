# 总体说明

## SCADA功能说明

`SCADA(Supervisory Control and Data Acquisition)`系统的基础功能可分为数据采集服务(`ACQ_SERVER`)、数据监视服务(`MONI_SERVER`)、控制操作服务(`CTRL_SERVER`)、专用计算服务(`CALC_SERVER`)、应用告警服务(`ALM_SERVER`)、数据查询服务(`DATA_SERVER`)六大部分。

各个部分的分工原则如下：

### 数据采集服务
数据处理服务的功能是将FE子系统的采集数据(生数据)获取至SCADA数据库中，并处理为熟数据以供后续程序使用。处理的范围包括模拟量、状态量、累计量和`SOE`。详见[数据采集服务](acq-server.md)页面。

### 数据监视服务
数据监视服务功能范围较广，主要分为

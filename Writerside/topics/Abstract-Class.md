# 基类模型

## Overview

提供公共的基类模型，基类的划分及其属性设计应符合电力系统特点。
基类模型不实际建模，仅提供公用属性。

## IdentifiedObject

对象类，电力系统监控相关的模型类应从此类继承。

<tabs>
    <tab title="维护分区">

| **属性**  | **中文名** |                   **类型**                   |         **说明**         |
|:-------:|:-------:|:------------------------------------------:|:----------------------:|
| `name`  |   名称    | [String128](Base-Attribute-Type.md#string) |     对象名称一般需要保证唯一性      |
| `alias` |   别名    | [String128](Base-Attribute-Type.md#string) | 在名称不能随意修改的情况下使用，可以用于展示 |
| `desc`  |   描述    | [String64](Base-Attribute-Type.md#string)  |          对象描述          |
| `mRID`  | 外部系统ID  | [String128](Base-Attribute-Type.md#string) |     对象为外部系统导入时可能用到     |

</tab>
<tab title="同步分区">
无
</tab>
<tab title="索引分区">
无
</tab>

</tabs>

## PowerSystemResource

电力系统资源类，继承自[`IdentifiedObject`](#identifiedobject)。需要参与管理、统计的模型类应从此类继承。


<tabs>
    <tab title="维护分区">

| **属性** | **中文名** |                **类型**                 |  **说明**   |
|:------:|:-------:|:-------------------------------------:|:---------:|
| `aor`  |  责任区号   | [ULong](Base-Attribute-Type.md#ulong) | 参见责任区设计说明 |

</tab>
<tab title="同步分区">
无
</tab>
<tab title="索引分区">
无
</tab>

</tabs>

## Equipment

设备类，继承自[`PowerSystemResource`](#powersystemresource)。

<tabs>
    <tab title="维护分区">

|   **属性**    | **中文名** |               **类型**                | **说明** |
|:-----------:|:-------:|:-----------------------------------:|:------:|
| `aggregate` | 是否为等值设备 | [Bool](Base-Attribute-Type.md#bool) |   备用   |

</tab>
<tab title="同步分区">

|     **属性**      | **中文名** |                        **类型**                         |  **说明**   |
|:---------------:|:-------:|:-----------------------------------------------------:|:---------:|
|  `moniStatus`   | 设备监盘状态  | [**MoniStatus**](Self-defined-Bit-Type.md#monistatus) |           |
| `serviceStatus` |  投运状态   |    [**ServiceStatus**](Enum-Type.md#servicestatus)    | 记录设备的投运状态 |
| `inServiceTime` |  投运时间   |         [STime](Base-Attribute-Type.md#stime)         |           |
|  `retireTime`   |  退役时间   |         [STime](Base-Attribute-Type.md#stime)         |           |

</tab>
<tab title="索引分区">
无
</tab>

</tabs>

## EquipmentContainer

设备容器类，继承自[`PowerSystemResource`](#powersystemresource)。

<tabs>
    <tab title="维护分区">

|   **属性**    |  **中文名**  |               **类型**                | **说明** |
|:-----------:|:---------:|:-----------------------------------:|:------:|
| `aggregate` | 是否为等值设备容器 | [Bool](Base-Attribute-Type.md#bool) |   备用   |

</tab>
<tab title="同步分区">

|     **属性**      | **中文名** |                           **类型**                            |   **说明**    |
|:---------------:|:-------:|:-----------------------------------------------------------:|:-----------:|
|  `moniStatus`   | 设备监盘状态  |    [**MoniStatus**](Self-defined-Bit-Type.md#monistatus)    |             |
| `serviceStatus` |  投运状态   |       [**ServiceStatus**](Enum-Type.md#servicestatus)       | 记录设备容器的投运状态 |
| `runningStatus` |  运行状态   | [**RunningStatus**](Self-defined-Bit-Type.md#runningstatus) |             |
| `inServiceTime` |  投运时间   |            [STime](Base-Attribute-Type.md#stime)            |             |
|  `retireTime`   |  退役时间   |            [STime](Base-Attribute-Type.md#stime)            |             |
|   `genPower`    |   总发电   |       [**Power**](Self-defined-Struct-Type.md#power)        |             |
|   `loadPower`   |   总用电   |       [**Power**](Self-defined-Struct-Type.md#power)        |             |
|   `tranLoss`    |  变压器损耗  |       [**Power**](Self-defined-Struct-Type.md#power)        |             |
|   `lineLoss`    |  线路损耗   |       [**Power**](Self-defined-Struct-Type.md#power)        |             |
|    `facLoss`    |   厂用电   |       [**Power**](Self-defined-Struct-Type.md#power)        |             |
|     `loss`      |   总损耗   |       [**Power**](Self-defined-Struct-Type.md#power)        |             |

</tab>
<tab title="索引分区">
无
</tab>

</tabs>

## PrimaryEquipment

一次设备类，继承自[`Equipment`](#equipment)。

> 目前一次设备最多为双端设备，故模型上只建立了首末两组拓扑相关的域
>
> 后续可按需扩展

<tabs>
    <tab title="维护分区">
无
</tab>
<tab title="同步分区">

|       **属性**       | **中文名**  |                           **类型**                            |       **说明**       |
|:------------------:|:--------:|:-----------------------------------------------------------:|:------------------:|
|      `status`      |  设备运行状态  | [**RunningStatus**](Self-defined-Bit-Type.md#runningstatus) |                    |
|    `lastStatus`    | 设备上次运行状态 | [**RunningStatus**](Self-defined-Bit-Type.md#runningstatus) | 用于与当前运行状态比较，判断状态变化 |
| `statusUpdateTime` | 运行状态刷新时间 |             [Time](Base-Attribute-Type.md#time)             |                    |
|     `topColor`     | 设备首端拓扑状态 |      [**TopColor**](Self-defined-Bit-Type.md#topcolor)      |                    |
|    `ztopColor`     | 设备末端拓扑状态 |      [**TopColor**](Self-defined-Bit-Type.md#topcolor)      |                    |
|      `itnode`      | 设备首端拓扑点号 |             [Long](Base-Attribute-Type.md#long)             |                    |
|      `ztnode`      | 设备末端拓扑点号 |             [Long](Base-Attribute-Type.md#long)             |                    |

</tab>
<tab title="索引分区">
无
</tab>

</tabs>

## Switch

开合设备类，继承自[`PrimaryEquipment`](#primaryequipment)。

<tabs>
    <tab title="维护分区">

|    **属性**    | **中文名** |               **类型**                | **说明** |
|:------------:|:-------:|:-----------------------------------:|:------:|
| `normalOpen` |  是否常开   | [Bool](Base-Attribute-Type.md#bool) |        |

</tab>
<tab title="同步分区">

|    **属性**     | **中文名** |                      **类型**                       | **说明** |
|:-------------:|:-------:|:-------------------------------------------------:|:------:|
|     `pos`     |  位置状态   | [**Position**](Self-defined-Bit-Type.md#position) |        |
|  `openCount`  |  开断次数   |       [ULong](Base-Attribute-Type.md#ulong)       |        |
| `actionCount` | 保护动作次数  |       [ULong](Base-Attribute-Type.md#ulong)       |        |
|  `openTime`   | 最近开断时间  |        [Time](Base-Attribute-Type.md#time)        |        |
| `actionTime`  | 最近动作时间  |        [Time](Base-Attribute-Type.md#time)        |        |

</tab>
<tab title="索引分区">
无
</tab>

</tabs>
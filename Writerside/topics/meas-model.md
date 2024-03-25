# 量测模型

## Overview

包括采集装置、四遥等。
> SCADA的量测模型与FE的量测模型基本是一一对应的，包括IED、模拟量、状态量、累计量、遥控、遥调。
>
> 量测可以与设备、设备容器进行关联。

## IED

量测采集装置，继承自[`Equipment`](Abstract-Class.md#equipment)。

<tabs>
    <tab title="维护分区">

|     **属性**     | **中文名**  |                   **类型**                   |          **说明**          |
|:--------------:|:--------:|:------------------------------------------:|:------------------------:|
|     `type`     |  IED类型   |    [**IEDType**](Enum-Type.md#iedtype)     |          IED分类           |
|  `isVirtual`   | 是否为虚拟IED |    [Bool](Base-Attribute-Type.md#bool)     | 虚拟IED非实采，用来存放SCADA自建的量测点 |
| `manufacturer` |   制造厂商   | [String128](Base-Attribute-Type.md#string) |      从comdb数据库同步而来       |
| `productModel` |   产品型号   | [String128](Base-Attribute-Type.md#string) | 从comdb数据库同步而来，与制造厂商配合使用  |

</tab>
<tab title="同步分区">

|        **属性**         |  **中文名**   |               **类型**                | **说明** |
|:---------------------:|:----------:|:-----------------------------------:|:------:|
|     `commStatus`      |    通讯状态    | [Bool](Base-Attribute-Type.md#bool) |        |
| `lastDisconnectTime`  |  上次通讯中断时间  | [Time](Base-Attribute-Type.md#time) |        |
|     `commAStatus`     |   A网通讯状态   | [Bool](Base-Attribute-Type.md#bool) |        |
| `lastADisconnectTime` | 上次A网通讯中断时间 | [Time](Base-Attribute-Type.md#time) |        |
|     `commBStatus`     |   B网通讯状态   | [Bool](Base-Attribute-Type.md#bool) |        |
| `lastBDisconnectTime` | 上次B网通讯中断时间 | [Time](Base-Attribute-Type.md#time) |        |

</tab>
<tab title="索引分区">

|        **属性**         |                     **中文名**                     |                               **类型**                                |    **说明**     |
|:---------------------:|:-----------------------------------------------:|:-------------------------------------------------------------------:|:-------------:|
| `MemberOfSubstation`  |  所属的[**Substation**](Core-Model.md#substation)  |  [**SymbSeqArraySlave**](Base-Attribute-Type.md#symbseqarrayslave)  |               |
|      `RefFeIED`       |                    关联的前置IED                     |           [**CrossRef**](Base-Attribute-Type.md#crossref)           |               |
|   `ContainsAnalog`    |      包含的[**Analog**](meas-model.md#analog)      | [**SymbSeqArrayMaster**](Base-Attribute-Type.md#symbseqarraymaster) |               |
|   `ContainsStatus`    |      包含的[**Status**](meas-model.md#status)      | [**SymbSeqArrayMaster**](Base-Attribute-Type.md#symbseqarraymaster) |               |
| `ContainsAccumulator` | 包含的[**Accumulator**](meas-model.md#accumulator) | [**SymbSeqArrayMaster**](Base-Attribute-Type.md#symbseqarraymaster) |               |
|    `RefCommStatus`    |                     IED通讯状态                     |           [**CrossRef**](Base-Attribute-Type.md#crossref)           |               |
| `RefPrimaryEquipment` |                     关联的一次设备                     |          [**SingleRef**](Base-Attribute-Type.md#singleref)          | 可关联到所有种类的一次设备 |

</tab>

</tabs>

## Analog

模拟量，继承自[`PowerSystemResource`](Abstract-Class.md#powersystemresource)。

<tabs>
    <tab title="维护分区">

|        **属性**        |   **中文名**    |                  **类型**                   |       **说明**        |
|:--------------------:|:------------:|:-----------------------------------------:|:-------------------:|
|        `type`        |    模拟量类型     | [**AnalogType**](Enum-Type.md#analogtype) |                     |
|      `zeroZone`      |     零漂死区     |  [Double](Base-Attribute-Type.md#double)  |                     |
|      `deadZone`      |     变化死区     |  [Double](Base-Attribute-Type.md#double)  |                     |
|      `avaTime`       |   有效时限(秒)    |   [ULong](Base-Attribute-Type.md#ulong)   |                     |
|         `k`          |     转换系数     |  [Double](Base-Attribute-Type.md#double)  |                     |
|         `b`          |     偏移系数     |  [Double](Base-Attribute-Type.md#double)  |                     |
|        `abs`         |    是否取绝对值    |    [Bool](Base-Attribute-Type.md#bool)    |                     |
|   `reasonableMoni`   |   启用合理性监视    |    [Bool](Base-Attribute-Type.md#bool)    |                     |
| `reasonableMinValue` |    合理范围下值    |  [Double](Base-Attribute-Type.md#double)  |                     |
| `reasonableMaxValue` |    合理范围上值    |  [Double](Base-Attribute-Type.md#double)  |                     |
|      `jumpMoni`      |    启用跳变监视    |    [Bool](Base-Attribute-Type.md#bool)    |                     |
|    `jumpSetValue`    |    跳变监视限值    |  [Double](Base-Attribute-Type.md#double)  |                     |
|     `isJumpPct`      | 跳变监视是否为百分比限值 |    [Bool](Base-Attribute-Type.md#bool)    |                     |
|    `constantMoni`    |    启用不变监视    |    [Bool](Base-Attribute-Type.md#bool)    |                     |
|  `constantSetValue`  |  不变监视限值(秒)   |  [Double](Base-Attribute-Type.md#double)  |                     |
|     `limitMoni`      |    启用限值监视    |    [Bool](Base-Attribute-Type.md#bool)    |                     |
|     `overDelay`      |  越限延迟参数(秒)   |  [UShort](Base-Attribute-Type.md#ushort)  | 越限/恢复需保持一段时间，以免频繁变动 |
|   `limitDeadZone`    |    越限判断死区    |  [Double](Base-Attribute-Type.md#double)  |                     |
|  `highLimitLevel1`   |     上限值      |  [Double](Base-Attribute-Type.md#double)  |                     |
|   `lowLimitLevel1`   |     下限值      |  [Double](Base-Attribute-Type.md#double)  |                     |
|  `highLimitLevel2`   |     上上限值     |  [Double](Base-Attribute-Type.md#double)  |                     |
|   `lowLimitLevel2`   |     下下限值     |  [Double](Base-Attribute-Type.md#double)  |                     |
|  `highLimitLevel3`   |    上上上限值     |  [Double](Base-Attribute-Type.md#double)  |                     |
|   `lowLimitLevel3`   |    下下下限值     |  [Double](Base-Attribute-Type.md#double)  |                     |
|  `ctrlUniqueCheck`   |  参与唯一性闭锁校验   |    [Bool](Base-Attribute-Type.md#bool)    |                     |
|  `ctrlResultCheck`   |   进行控制结果校验   |    [Bool](Base-Attribute-Type.md#bool)    |                     |

</tab>
<tab title="同步分区">

|         **属性**          |  **中文名**  |                           **类型**                            | **说明** |
|:-----------------------:|:---------:|:-----------------------------------------------------------:|:------:|
|        `feValue`        |   前置采集值   |           [Double](Base-Attribute-Type.md#double)           |        |
|       `feQuality`       |  前置采集质量码  | [**FeMeasQuality**](Self-defined-Bit-Type.md#femeasquality) |        |
|      `feTimeStamp`      |  前置采集时标   |             [Time](Base-Attribute-Type.md#time)             | 精确到毫秒  |
|         `value`         |  SCADA值   |           [Double](Base-Attribute-Type.md#double)           |        |
|        `quality`        | SCADA质量位  |   [**MeasQuality**](Self-defined-Bit-Type.md#measquality)   |        |
|       `timeStamp`       |  SCADA时标  |             [Time](Base-Attribute-Type.md#time)             | 精确到毫秒  |
|      `controlling`      |    控制中    |             [Bool](Base-Attribute-Type.md#bool)             |        |
|      `moniStatus`       |   监盘状态    |           [Double](Base-Attribute-Type.md#double)           |        |
|     `overBeginTime`     | 最近越限开始时间  |             [Time](Base-Attribute-Type.md#time)             |        |
|     `overDuration`      |  越限持续时间   |            [RTime](Base-Attribute-Type.md#rtime)            |        |
|     `todayMinValue`     |   本日极小值   |           [Double](Base-Attribute-Type.md#double)           |        |
|   `todayMinValueTime`   | 本日极小值发生时间 |             [Time](Base-Attribute-Type.md#time)             |        |
|     `todayMaxValue`     |   本日极大值   |           [Double](Base-Attribute-Type.md#double)           |        |
|   `todayMaxValueTime`   | 本日极大值发生时间 |             [Time](Base-Attribute-Type.md#time)             |        |
|   `yesterdayMinValue`   |   昨日极小值   |           [Double](Base-Attribute-Type.md#double)           |        |
| `yesterdayMinValueTime` | 昨日极小值发生时间 |             [Time](Base-Attribute-Type.md#time)             |        |
|   `yesterdayMaxValue`   |   昨日极大值   |           [Double](Base-Attribute-Type.md#double)           |        |
| `yesterdayMaxValueTime` | 昨日极大值发生时间 |             [Time](Base-Attribute-Type.md#time)             |        |

</tab>
<tab title="索引分区">

|         **属性**          |                            **中文名**                            |                               **类型**                                |  **说明**  |
|:-----------------------:|:-------------------------------------------------------------:|:-------------------------------------------------------------------:|:--------:|
|      `MemberOfIED`      |                所属的[**IED**](meas-model.md#ied)                |  [**SymbSeqArraySlave**](Base-Attribute-Type.md#symbseqarrayslave)  |          |
|   `MemberOfEquipment`   |                          所属的设备/设备容器                           | [**ASymbSeqDlistSlave**](Base-Attribute-Type.md#asymbseqdlistslave) |          |
|    `RefStaticLimit`     |        关联的[**StaticLimit**](moni-model.md#staticlimit)        |          [**SingleRef**](Base-Attribute-Type.md#crossref)           |          |
|   `RefDynLimitGroup`    |      关联的[**DynLimitGroup**](moni-model.md#dynlimitgroup)      |          [**SingleRef**](Base-Attribute-Type.md#crossref)           |          |
|      `RefFeAnalog`      |                           关联的前置模拟量                            |           [**CrossRef**](Base-Attribute-Type.md#crossref)           |          |
|  `RefMultiSrcSelector`  | 关联的[**FeMultiSrcSelector**](meas-model.md#femultisrcselector) |          [**SingleRef**](Base-Attribute-Type.md#singleref)          |          |
|     `RefRegulating`     |         关联的[**Regulating**](meas-model.md#regulating)         |          [**SingleRef**](Base-Attribute-Type.md#singleref)          |   关联遥调   |
| `RefRegulatingSelector` | 关联的[**FeMultiSrcSelector**](meas-model.md#femultisrcselector) |          [**SingleRef**](Base-Attribute-Type.md#singleref)          |  关联遥调多源  |
|      `RefControl`       |            关联的[**Control**](meas-model.md#control)            |          [**SingleRef**](Base-Attribute-Type.md#singleref)          |   关联遥控   |
|  `RefControlSelector`   | 关联的[**FeMultiSrcSelector**](meas-model.md#femultisrcselector) |          [**SingleRef**](Base-Attribute-Type.md#singleref)          |  关联遥控多源  |
|    `RefControlOpen`     |            关联的[**Control**](meas-model.md#control)            |          [**SingleRef**](Base-Attribute-Type.md#singleref)          |  关联遥控分   |
|    `RefControlClose`    |            关联的[**Control**](meas-model.md#control)            |          [**SingleRef**](Base-Attribute-Type.md#singleref)          |  关联遥控合   |
|        `RefBay`         |                关联的[**Bay**](Core-Model.md#bay)                |          [**SingleRef**](Base-Attribute-Type.md#singleref)          | 方便查找上级对象 |
|    `RefVoltageLevel`    |       关联的[**VoltageLevel**](Core-Model.md#voltagelevel)       |          [**SingleRef**](Base-Attribute-Type.md#singleref)          | 方便查找上级对象 |
|     `RefSubstation`     |         关联的[**Substation**](Core-Model.md#substation)         |          [**SingleRef**](Base-Attribute-Type.md#singleref)          | 方便查找上级对象 |
|     `RefAuxSystem`      |       关联的[**AuxSystem**](auxi-model.md#auxiliarysystem)       |          [**SingleRef**](Base-Attribute-Type.md#singleref)          | 方便查找上级对象 |
|      `RefAlarmCfg`      |           关联的[**AlarmCfg**](meas-model.md#alarmcfg)           |          [**SingleRef**](Base-Attribute-Type.md#singleref)          |  关联告警配置  |

</tab>

</tabs>

## Status

状态量，继承自[`PowerSystemResource`](Abstract-Class.md#powersystemresource)。

<tabs>
    <tab title="维护分区">

|        **属性**        |  **中文名**   |                  **类型**                   | **说明** |
|:--------------------:|:----------:|:-----------------------------------------:|:------:|
|        `type`        |   状态量类型    | [**StatusType**](Enum-Type.md#statustype) |        |
|      `reverse`       |    是否取反    |    [Bool](Base-Attribute-Type.md#bool)    |        |
|      `avaTime`       |  有效时限(秒)   |   [ULong](Base-Attribute-Type.md#ulong)   |        |
|   `reasonableMoni`   |  启用合理性监视   |    [Bool](Base-Attribute-Type.md#bool)    |        |
| `reasonableMinValue` |   合理范围下值   |    [Long](Base-Attribute-Type.md#long)    |        |
| `reasonableMaxValue` |   合理范围上值   |    [Long](Base-Attribute-Type.md#long)    |        |
|    `ctrlPriority`    |  控制方式优先级   | [CtrlPriority](Enum-Type.md#ctrlpriority) |        |
|  `ctrlOpenReverse`   |   控分是否取反   |    [Bool](Base-Attribute-Type.md#bool)    |        |
|  `ctrlCloseReverse`  |   控合是否取反   |    [Bool](Base-Attribute-Type.md#bool)    |        |
| `noCtrlUniqueCheck`  | 不参与唯一性闭锁校验 |    [Bool](Base-Attribute-Type.md#bool)    |        |
|  `ctrlResultCheck`   |  进行控制结果校验  |    [Bool](Base-Attribute-Type.md#bool)    |        |

</tab>
<tab title="同步分区">

|    **属性**     | **中文名**  |                           **类型**                            | **说明** |
|:-------------:|:--------:|:-----------------------------------------------------------:|:------:|
|   `feValue`   |  前置采集值   |             [Long](Base-Attribute-Type.md#long)             |        |
|  `feQuality`  | 前置采集质量码  | [**FeMeasQuality**](Self-defined-Bit-Type.md#femeasquality) |        |
| `feTimeStamp` |  前置采集时标  |             [Time](Base-Attribute-Type.md#time)             | 精确到毫秒  |
|    `value`    |  SCADA值  |             [Long](Base-Attribute-Type.md#long)             |        |
|   `quality`   | SCADA质量位 |   [**MeasQuality**](Self-defined-Bit-Type.md#measquality)   |        |
|  `timeStamp`  | SCADA时标  |             [Time](Base-Attribute-Type.md#time)             | 精确到毫秒  |
| `moniStatus`  |   监盘状态   |           [Double](Base-Attribute-Type.md#double)           |        |

</tab>
<tab title="索引分区">

|        **属性**         |                            **中文名**                            |                               **类型**                                |  **说明**  |
|:---------------------:|:-------------------------------------------------------------:|:-------------------------------------------------------------------:|:--------:|
|     `MemberOfIED`     |                所属的[**IED**](meas-model.md#ied)                |  [**SymbSeqArraySlave**](Base-Attribute-Type.md#symbseqarrayslave)  |          |
|  `MemberOfEquipment`  |                          所属的设备/设备容器                           | [**ASymbSeqDlistSlave**](Base-Attribute-Type.md#asymbseqdlistslave) |          |
|     `RefFeStatus`     |                           关联的前置模拟量                            |           [**CrossRef**](Base-Attribute-Type.md#crossref)           |          |
| `RefMultiSrcSelector` | 关联的[**FeMultiSrcSelector**](meas-model.md#femultisrcselector) |          [**SingleRef**](Base-Attribute-Type.md#singleref)          |          |
|     `RefControl`      |            关联的[**Control**](meas-model.md#control)            |          [**SingleRef**](Base-Attribute-Type.md#singleref)          |   关联遥控   |
| `RefControlSelector`  | 关联的[**FeMultiSrcSelector**](meas-model.md#femultisrcselector) |          [**SingleRef**](Base-Attribute-Type.md#singleref)          |  关联遥控多源  |
|   `RefControlOpen`    |            关联的[**Control**](meas-model.md#control)            |          [**SingleRef**](Base-Attribute-Type.md#singleref)          |  关联遥控分   |
|   `RefControlClose`   |            关联的[**Control**](meas-model.md#control)            |          [**SingleRef**](Base-Attribute-Type.md#singleref)          |  关联遥控合   |
|    `RefControlJTQ`    |            关联的[**Control**](meas-model.md#control)            |          [**SingleRef**](Base-Attribute-Type.md#singleref)          | 关联遥控检同期  |
|    `RefControlJWY`    |            关联的[**Control**](meas-model.md#control)            |          [**SingleRef**](Base-Attribute-Type.md#singleref)          | 关联遥控检无压  |
|       `RefBay`        |                关联的[**Bay**](Core-Model.md#bay)                |          [**SingleRef**](Base-Attribute-Type.md#singleref)          | 方便查找上级对象 |
|   `RefVoltageLevel`   |       关联的[**VoltageLevel**](Core-Model.md#voltagelevel)       |          [**SingleRef**](Base-Attribute-Type.md#singleref)          | 方便查找上级对象 |
|    `RefSubstation`    |         关联的[**Substation**](Core-Model.md#substation)         |          [**SingleRef**](Base-Attribute-Type.md#singleref)          | 方便查找上级对象 |
|    `RefAuxSystem`     |       关联的[**AuxSystem**](auxi-model.md#auxiliarysystem)       |          [**SingleRef**](Base-Attribute-Type.md#singleref)          | 方便查找上级对象 |
|     `RefAlarmCfg`     |           关联的[**AlarmCfg**](meas-model.md#alarmcfg)           |          [**SingleRef**](Base-Attribute-Type.md#singleref)          |  关联告警配置  |

</tab>

</tabs>

## Accumulator

累计量，继承自[`PowerSystemResource`](Abstract-Class.md#powersystemresource)。

<tabs>
    <tab title="维护分区">

|  **属性**   | **中文名** |               **类型**                | **说明** |
|:---------:|:-------:|:-----------------------------------:|:------:|
|  `type`   |  累计量类型  |                                     |        |
| `reverse` |  是否取反   | [Bool](Base-Attribute-Type.md#bool) |        |
|   `abs`   | 是否取绝对值  | [Bool](Base-Attribute-Type.md#bool) |        |

</tab>
<tab title="同步分区">

|      **属性**       | **中文名**  |                           **类型**                            | **说明** |
|:-----------------:|:--------:|:-----------------------------------------------------------:|:------:|
|     `feValue`     |  前置采集值   |           [Double](Base-Attribute-Type.md#double)           |        |
|    `feQuality`    | 前置采集质量码  | [**FeMeasQuality**](Self-defined-Bit-Type.md#femeasquality) |        |
|   `feTimeStamp`   |  前置采集时标  |             [Time](Base-Attribute-Type.md#time)             | 精确到毫秒  |
|      `value`      |  SCADA值  |           [Double](Base-Attribute-Type.md#double)           |        |
|     `quality`     | SCADA质量位 |   [**MeasQuality**](Self-defined-Bit-Type.md#measquality)   |        |
|    `timeStamp`    | SCADA时标  |             [Time](Base-Attribute-Type.md#time)             | 精确到毫秒  |
|   `moniStatus`    |   监盘状态   |           [Double](Base-Attribute-Type.md#double)           |        |
| `todayBeginValue` | 本日累计初始值  |           [Double](Base-Attribute-Type.md#double)           |        |
|   `todayValue`    |  本日累计值   |           [Double](Base-Attribute-Type.md#double)           |        |
| `monthBeginValue` | 本月累计初始值  |           [Double](Base-Attribute-Type.md#double)           |        |
|   `monthValue`    |  本月累计值   |           [Double](Base-Attribute-Type.md#double)           |        |
| `yearBeginValue`  | 本年累计初始值  |           [Double](Base-Attribute-Type.md#double)           |        |
|    `yearValue`    |  本年累计值   |           [Double](Base-Attribute-Type.md#double)           |        |

</tab>
<tab title="索引分区">

|        **属性**        |                         **中文名**                         |                               **类型**                                |  **说明**  |
|:--------------------:|:-------------------------------------------------------:|:-------------------------------------------------------------------:|:--------:|
|    `MemberOfIED`     |             所属的[**IED**](meas-model.md#ied)             |  [**SymbSeqArraySlave**](Base-Attribute-Type.md#symbseqarrayslave)  |          |
| `MemberOfEquipment`  |                       所属的设备/设备容器                        | [**ASymbSeqDlistSlave**](Base-Attribute-Type.md#asymbseqdlistslave) |          |
|  `RefFeAccmulator`   |                        关联的前置累计量                         |           [**CrossRef**](Base-Attribute-Type.md#crossref)           |          |
|       `RefBay`       |             关联的[**Bay**](Core-Model.md#bay)             |          [**SingleRef**](Base-Attribute-Type.md#singleref)          | 方便查找上级对象 |
|  `RefVoltageLevel`   |    关联的[**VoltageLevel**](Core-Model.md#voltagelevel)    |          [**SingleRef**](Base-Attribute-Type.md#singleref)          | 方便查找上级对象 |
|   `RefSubstation`    |      关联的[**Substation**](Core-Model.md#substation)      |          [**SingleRef**](Base-Attribute-Type.md#singleref)          | 方便查找上级对象 |
| `RefAuxiliarySystem` | 关联的[**AuxiliarySystem**](auxi-model.md#auxiliarysystem) |          [**SingleRef**](Base-Attribute-Type.md#singleref)          | 方便查找上级对象 |

</tab>

</tabs>

## Control

遥控，继承自[`PowerSystemResource`](Abstract-Class.md#powersystemresource)。

<tabs>
    <tab title="维护分区">

|     **属性**     | **中文名**  |                       **类型**                        | **说明** |
|:--------------:|:--------:|:---------------------------------------------------:|:------:|
|  `guardMode`   |   监护模式   |       [**GuardMode**](Enum-Type.md#guardmode)       |        |
|  `checkMode`   |   校验模式   | [**CheckMode**](Self-defined-Bit-Type.md#checkmode) |        |
| `isDirectCtrl` |   是否直控   |         [Bool](Base-Attribute-Type.md#bool)         |        |
| `checkResult`  | 是否检查控制结果 |         [Bool](Base-Attribute-Type.md#bool)         |        |

</tab>
<tab title="同步分区">

|     **属性**      | **中文名** |               **类型**                | **说明** |
|:---------------:|:-------:|:-----------------------------------:|:------:|
| `isControlling` |   控制中   | [Bool](Base-Attribute-Type.md#bool) |        |

</tab>
<tab title="索引分区">

|        **属性**         |                            **中文名**                            |                              **类型**                               | **说明** |
|:---------------------:|:-------------------------------------------------------------:|:-----------------------------------------------------------------:|:------:|
|     `MemberOfIED`     |                所属的[**IED**](meas-model.md#ied)                | [**SymbSeqArraySlave**](Base-Attribute-Type.md#symbseqarrayslave) |        |
|       `RefFeYK`       |                            关联的前置遥控                            |          [**CrossRef**](Base-Attribute-Type.md#crossref)          |        |
| `RefMultiSrcSelector` | 关联的[**FeMultiSrcSelector**](meas-model.md#femultisrcselector) |         [**SingleRef**](Base-Attribute-Type.md#singleref)         |        |

</tab>

</tabs>

## Regulating

遥调，继承自[`PowerSystemResource`](Abstract-Class.md#powersystemresource)。

<tabs>
    <tab title="维护分区">

|     **属性**     | **中文名**  |                       **类型**                        | **说明** |
|:--------------:|:--------:|:---------------------------------------------------:|:------:|
|  `guardMode`   |   监护模式   |       [**GuardMode**](Enum-Type.md#guardmode)       |        |
|  `checkMode`   |   校验模式   | [**CheckMode**](Self-defined-Bit-Type.md#checkmode) |        |
| `isDirectCtrl` |   是否直控   |         [Bool](Base-Attribute-Type.md#bool)         |        |
|  `checkZone`   | 是否检查控制死区 |         [Bool](Base-Attribute-Type.md#bool)         |        |
|   `deadZone`   |   控制死区   |       [Double](Base-Attribute-Type.md#double)       |        |

</tab>
<tab title="同步分区">

|     **属性**      | **中文名** |               **类型**                | **说明** |
|:---------------:|:-------:|:-----------------------------------:|:------:|
| `isControlling` |   控制中   | [Bool](Base-Attribute-Type.md#bool) |        |

</tab>
<tab title="索引分区">

|        **属性**         |                            **中文名**                            |                              **类型**                               | **说明** |
|:---------------------:|:-------------------------------------------------------------:|:-----------------------------------------------------------------:|:------:|
|     `MemberOfIED`     |                所属的[**IED**](meas-model.md#ied)                | [**SymbSeqArraySlave**](Base-Attribute-Type.md#symbseqarrayslave) |        |
|       `RefFeYT`       |                            关联的前置遥调                            |          [**CrossRef**](Base-Attribute-Type.md#crossref)          |        |
| `RefMultiSrcSelector` | 关联的[**FeMultiSrcSelector**](meas-model.md#femultisrcselector) |         [**SingleRef**](Base-Attribute-Type.md#singleref)         |        |

</tab>

</tabs>

## FeMultiSrc

采集多源表。

> 用于表示采集多源关系。

<tabs>
    <tab title="维护分区">

| **属性** | **中文名** |                    **类型**                     | **说明** |
|:------:|:-------:|:---------------------------------------------:|:------:|
| `type` |  多源类型   | [**MultiSrcType**](Enum-Type.md#multisrctype) |        |

</tab>
<tab title="同步分区">

|     **属性**      | **中文名** |               **类型**                | **说明** |
|:---------------:|:-------:|:-----------------------------------:|:------:|
|   `selected`    |   被选中   | [Bool](Base-Attribute-Type.md#bool) |        |
| `forceSelected` |  强制选中   | [Bool](Base-Attribute-Type.md#bool) |        |

</tab>
<tab title="索引分区">

|            **属性**            |                            **中文名**                            |                              **类型**                               | **说明** |
|:----------------------------:|:-------------------------------------------------------------:|:-----------------------------------------------------------------:|:------:|
| `MemberOfFeMultiSrcSelector` | 所属的[**FeMultiSrcSelector**](meas-model.md#femultisrcselector) | [**SymbSeqArraySlave**](Base-Attribute-Type.md#symbseqarrayslave) |        |
|         `RefFeMeas`          |                            关联的前置测点                            |          [**CrossRef**](Base-Attribute-Type.md#crossref)          |        |

</tab>

</tabs>

## FeMultiSrcSelector

采集多源选择器。

> 用于表示采集多源选择结果。

<tabs>
    <tab title="维护分区">

|    **属性**    | **中文名** |                     **类型**                      | **说明** |
|:------------:|:-------:|:-----------------------------------------------:|:------:|
| `selectMode` | 多源选择模式  | [**SrcSelectMode**](Enum-Type.md#srcselectmode) |        |

</tab>
<tab title="同步分区">

|       **属性**        |  **中文名**  |                 **类型**                  |     **说明**      |
|:-------------------:|:---------:|:---------------------------------------:|:---------------:|
|  `selectedSource`   | 被选中的源对象id | [TDBOID](Base-Attribute-Type.md#tdboid) | 有可能是遥信、遥测、遥控、遥调 |
| `selectedTimeStamp` | 选择结果更新时标  |   [Time](Base-Attribute-Type.md#time)   |                 |

</tab>
<tab title="索引分区">

|        **属性**        |                    **中文名**                    |                               **类型**                                | **说明** |
|:--------------------:|:---------------------------------------------:|:-------------------------------------------------------------------:|:------:|
| `ContainsFeMultiSrc` | 包含的[**FeMultiSrc**](meas-model.md#femultisrc) | [**SymbSeqArrayMaster**](Base-Attribute-Type.md#symbseqarraymaster) |        |

</tab>

</tabs>

## AlarmCfg

告警配置表。

> 用于配置状态量、模拟量告警方式，除了变化告警、越限告警配置，还包括关联的遥控、遥调告警方式配置。

<tabs>
    <tab title="维护分区">

|     **属性**      | **中文名** |                           **类型**                            |         **说明**          |
|:---------------:|:-------:|:-----------------------------------------------------------:|:-----------------------:|
|     `name`      |   名称    |          [String64](Base-Attribute-Type.md#string)          |     使用英文，代码内部使用，不翻译     |
|     `desc`      |   描述    |          [String64](Base-Attribute-Type.md#string)          |     使用中文，需要进行国际化处理      |
| `ctrlOpenDesc`  |  控分描述   |          [String64](Base-Attribute-Type.md#string)          | 告警中的控分描述，使用中文，需要进行国际化处理 |
| `ctrlCloseDesc` |  控合描述   |          [String64](Base-Attribute-Type.md#string)          | 告警中的控合描述，使用中文，需要进行国际化处理 |
|  `contentCfg`   |  内容配置   | [**AlmContentCfg**](Self-defined-Bit-Type.md#almcontentcfg) |         告警内容配置          |

</tab>
<tab title="同步分区">

无。

</tab>
<tab title="索引分区">

|      **属性**       |   **中文名**   |                     **类型**                      | **说明** |
|:-----------------:|:-----------:|:-----------------------------------------------:|:------:|
| `RefCloseAlmItem` |   状态量合告警项   | [**CrossRef**](Base-Attribute-Type.md#crossref) |        |
| `RefOpenAlmItem`  |   状态量分告警项   | [**CrossRef**](Base-Attribute-Type.md#crossref) |        |
|  `RefH1AlmItem`   |  模拟量越上限告警项  | [**CrossRef**](Base-Attribute-Type.md#crossref) |        |
|  `RefH2AlmItem`   | 模拟量越上上限告警项  | [**CrossRef**](Base-Attribute-Type.md#crossref) |        |
|  `RefH3AlmItem`   | 模拟量越上上上限告警项 | [**CrossRef**](Base-Attribute-Type.md#crossref) |        |
|  `RefL1AlmItem`   |  模拟量越下限告警项  | [**CrossRef**](Base-Attribute-Type.md#crossref) |        |
|  `RefL2AlmItem`   | 模拟量越下下限告警项  | [**CrossRef**](Base-Attribute-Type.md#crossref) |        |
|  `RefL3AlmItem`   | 模拟量越下下下限告警项 | [**CrossRef**](Base-Attribute-Type.md#crossref) |        |

</tab>

</tabs>
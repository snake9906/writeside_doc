# 量测模型

## Overview

包括采集装置、三遥和限值相关的表。
> SCADA的量测模型与FE的量测模型基本是一一对应的，包括IED、模拟量、状态量、累计量。
>
> 量测可以与设备、设备容器进行关联。

## IED

量测采集装置，继承自[`Equipment`](Abstract-Class.md#equipment)。

<tabs>
    <tab title="维护分区">

|   **属性**    | **中文名**  |               **类型**                |          **说明**          |
|:-----------:|:--------:|:-----------------------------------:|:------------------------:|
| `isVirtual` | 是否为虚拟IED | [Bool](Base-Attribute-Type.md#bool) | 虚拟IED非实采，用来存放SCADA自建的量测点 |

</tab>
<tab title="同步分区">
无
</tab>
<tab title="索引分区">

|        **属性**         |                     **中文名**                     |                               **类型**                                | **说明** |
|:---------------------:|:-----------------------------------------------:|:-------------------------------------------------------------------:|:------:|
| `MemberOfSubstation`  |  所属的[**Substation**](Core-Model.md#substation)  |  [**SymbSeqArraySlave**](Base-Attribute-Type.md#symbseqarrayslave)  |        |
|      `RefFeIED`       |                    关联的前置IED                     |           [**CrossRef**](Base-Attribute-Type.md#crossref)           |        |
|   `ContainsAnalog`    |      包含的[**Analog**](meas-model.md#analog)      | [**SymbSeqArrayMaster**](Base-Attribute-Type.md#symbseqarraymaster) |        |
|   `ContainsStatus`    |      包含的[**Status**](meas-model.md#status)      | [**SymbSeqArrayMaster**](Base-Attribute-Type.md#symbseqarraymaster) |        |
| `ContainsAccumulator` | 包含的[**Accumulator**](meas-model.md#accumulator) | [**SymbSeqArrayMaster**](Base-Attribute-Type.md#symbseqarraymaster) |        |

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

</tab>
<tab title="同步分区">

|         **属性**          |  **中文名**  |                         **类型**                          | **说明** |
|:-----------------------:|:---------:|:-------------------------------------------------------:|:------:|
|        `feValue`        |   前置采集值   |         [Double](Base-Attribute-Type.md#double)         |        |
|       `feQuality`       |  前置采集质量码  | [FeMeasQuality](Self-defined-Bit-Type.md#femeasquality) |        |
|      `feTimeStamp`      |  前置采集时标   |           [Time](Base-Attribute-Type.md#time)           | 精确到毫秒  |
|         `value`         |  SCADA值   |         [Double](Base-Attribute-Type.md#double)         |        |
|        `quality`        | SCADA质量位  |   [MeasQuality](Self-defined-Bit-Type.md#measquality)   |        |
|       `timeStamp`       |  SCADA时标  |           [Time](Base-Attribute-Type.md#time)           | 精确到毫秒  |
|      `moniStatus`       |   监盘状态    |         [Double](Base-Attribute-Type.md#double)         |        |
|     `overBeginTime`     | 最近越限开始时间  |           [Time](Base-Attribute-Type.md#time)           |        |
|     `overDuration`      |  越限持续时间   |          [RTime](Base-Attribute-Type.md#rtime)          |        |
|     `todayMinValue`     |   本日极小值   |         [Double](Base-Attribute-Type.md#double)         |        |
|   `todayMinValueTime`   | 本日极小值发生时间 |           [Time](Base-Attribute-Type.md#time)           |        |
|     `todayMaxValue`     |   本日极大值   |         [Double](Base-Attribute-Type.md#double)         |        |
|   `todayMaxValueTime`   | 本日极大值发生时间 |           [Time](Base-Attribute-Type.md#time)           |        |
|   `yesterdayMinValue`   |   昨日极小值   |         [Double](Base-Attribute-Type.md#double)         |        |
| `yesterdayMinValueTime` | 昨日极小值发生时间 |           [Time](Base-Attribute-Type.md#time)           |        |
|   `yesterdayMaxValue`   |   昨日极大值   |         [Double](Base-Attribute-Type.md#double)         |        |
| `yesterdayMaxValueTime` | 昨日极大值发生时间 |           [Time](Base-Attribute-Type.md#time)           |        |

</tab>
<tab title="索引分区">

|       **属性**        |                       **中文名**                       |                               **类型**                                |  **说明**  |
|:-------------------:|:---------------------------------------------------:|:-------------------------------------------------------------------:|:--------:|
|    `MemberOfIED`    |           所属的[**IED**](meas-model.md#ied)           |  [**SymbSeqArraySlave**](Base-Attribute-Type.md#symbseqarrayslave)  |          |
| `MemberOfEquipment` |                     所属的设备/设备容器                      | [**ASymbSeqDlistSlave**](Base-Attribute-Type.md#asymbseqdlistslave) |          |
|  `RefStaticLimit`   |   关联的[**StaticLimit**](meas-model.md#staticlimit)   |          [**SingleRef**](Base-Attribute-Type.md#crossref)           |          |
| `RefDynLimitGroup`  | 关联的[**DynLimitGroup**](meas-model.md#dynlimitgroup) |          [**SingleRef**](Base-Attribute-Type.md#crossref)           |          |
|    `RefFeAnalog`    |                      关联的前置模拟量                       |           [**CrossRef**](Base-Attribute-Type.md#crossref)           |          |
|      `RefBay`       |           关联的[**Bay**](Core-Model.md#bay)           |          [**SingleRef**](Base-Attribute-Type.md#singleref)          | 方便查找上级对象 |
|  `RefVoltageLevel`  |  关联的[**VoltageLevel**](Core-Model.md#voltagelevel)  |          [**SingleRef**](Base-Attribute-Type.md#singleref)          | 方便查找上级对象 |
|   `RefSubstation`   |    关联的[**Substation**](Core-Model.md#substation)    |          [**SingleRef**](Base-Attribute-Type.md#singleref)          | 方便查找上级对象 |
|   `RefAuxSystem`    |                                                     |          [**SingleRef**](Base-Attribute-Type.md#singleref)          | 方便查找上级对象 |

</tab>

</tabs>

## Status

状态量，继承自[`PowerSystemResource`](Abstract-Class.md#powersystemresource)。

<tabs>
    <tab title="维护分区">

|        **属性**        | **中文名** |                  **类型**                   | **说明** |
|:--------------------:|:-------:|:-----------------------------------------:|:------:|
|        `type`        |  状态量类型  | [**StatusType**](Enum-Type.md#statustype) |        |
|      `reverse`       |  是否取反   |    [Bool](Base-Attribute-Type.md#bool)    |        |
|      `avaTime`       | 有效时限(秒) |   [ULong](Base-Attribute-Type.md#ulong)   |        |
|   `reasonableMoni`   | 启用合理性监视 |    [Bool](Base-Attribute-Type.md#bool)    |        |
| `reasonableMinValue` | 合理范围下值  |    [Long](Base-Attribute-Type.md#long)    |        |
| `reasonableMaxValue` | 合理范围上值  |    [Long](Base-Attribute-Type.md#long)    |        |

</tab>
<tab title="同步分区">

|    **属性**     | **中文名**  |                         **类型**                          | **说明** |
|:-------------:|:--------:|:-------------------------------------------------------:|:------:|
|   `feValue`   |  前置采集值   |           [Long](Base-Attribute-Type.md#long)           |        |
|  `feQuality`  | 前置采集质量码  | [FeMeasQuality](Self-defined-Bit-Type.md#femeasquality) |        |
| `feTimeStamp` |  前置采集时标  |           [Time](Base-Attribute-Type.md#time)           | 精确到毫秒  |
|    `value`    |  SCADA值  |           [Long](Base-Attribute-Type.md#long)           |        |
|   `quality`   | SCADA质量位 |   [MeasQuality](Self-defined-Bit-Type.md#measquality)   |        |
|  `timeStamp`  | SCADA时标  |           [Time](Base-Attribute-Type.md#time)           | 精确到毫秒  |
| `moniStatus`  |   监盘状态   |         [Double](Base-Attribute-Type.md#double)         |        |

</tab>
<tab title="索引分区">

|       **属性**        |                      **中文名**                      |                               **类型**                                |  **说明**  |
|:-------------------:|:-------------------------------------------------:|:-------------------------------------------------------------------:|:--------:|
|    `MemberOfIED`    |          所属的[**IED**](meas-model.md#ied)          |  [**SymbSeqArraySlave**](Base-Attribute-Type.md#symbseqarrayslave)  |          |
| `MemberOfEquipment` |                    所属的设备/设备容器                     | [**ASymbSeqDlistSlave**](Base-Attribute-Type.md#asymbseqdlistslave) |          |
|    `RefFeStatus`    |                     关联的前置模拟量                      |           [**CrossRef**](Base-Attribute-Type.md#crossref)           |          |
|      `RefBay`       |          关联的[**Bay**](Core-Model.md#bay)          |          [**SingleRef**](Base-Attribute-Type.md#singleref)          | 方便查找上级对象 |
|  `RefVoltageLevel`  | 关联的[**VoltageLevel**](Core-Model.md#voltagelevel) |          [**SingleRef**](Base-Attribute-Type.md#singleref)          | 方便查找上级对象 |
|   `RefSubstation`   |   关联的[**Substation**](Core-Model.md#substation)   |          [**SingleRef**](Base-Attribute-Type.md#singleref)          | 方便查找上级对象 |
|   `RefAuxSystem`    |                                                   |          [**SingleRef**](Base-Attribute-Type.md#singleref)          | 方便查找上级对象 |

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

|      **属性**       | **中文名**  |                         **类型**                          | **说明** |
|:-----------------:|:--------:|:-------------------------------------------------------:|:------:|
|     `feValue`     |  前置采集值   |         [Double](Base-Attribute-Type.md#double)         |        |
|    `feQuality`    | 前置采集质量码  | [FeMeasQuality](Self-defined-Bit-Type.md#femeasquality) |        |
|   `feTimeStamp`   |  前置采集时标  |           [Time](Base-Attribute-Type.md#time)           | 精确到毫秒  |
|      `value`      |  SCADA值  |         [Double](Base-Attribute-Type.md#double)         |        |
|     `quality`     | SCADA质量位 |   [MeasQuality](Self-defined-Bit-Type.md#measquality)   |        |
|    `timeStamp`    | SCADA时标  |           [Time](Base-Attribute-Type.md#time)           | 精确到毫秒  |
|   `moniStatus`    |   监盘状态   |         [Double](Base-Attribute-Type.md#double)         |        |
| `todayBeginValue` | 本日累计初始值  |         [Double](Base-Attribute-Type.md#double)         |        |
|   `todayValue`    |  本日累计值   |         [Double](Base-Attribute-Type.md#double)         |        |
| `monthBeginValue` | 本月累计初始值  |         [Double](Base-Attribute-Type.md#double)         |        |
|   `monthValue`    |  本月累计值   |         [Double](Base-Attribute-Type.md#double)         |        |
| `yearBeginValue`  | 本年累计初始值  |         [Double](Base-Attribute-Type.md#double)         |        |
|    `yearValue`    |  本年累计值   |         [Double](Base-Attribute-Type.md#double)         |        |

</tab>
<tab title="索引分区">

|       **属性**        |                      **中文名**                      |                               **类型**                                |  **说明**  |
|:-------------------:|:-------------------------------------------------:|:-------------------------------------------------------------------:|:--------:|
|    `MemberOfIED`    |          所属的[**IED**](meas-model.md#ied)          |  [**SymbSeqArraySlave**](Base-Attribute-Type.md#symbseqarrayslave)  |          |
| `MemberOfEquipment` |                    所属的设备/设备容器                     | [**ASymbSeqDlistSlave**](Base-Attribute-Type.md#asymbseqdlistslave) |          |
|  `RefFeAccmulator`  |                     关联的前置累计量                      |           [**CrossRef**](Base-Attribute-Type.md#crossref)           |          |
|      `RefBay`       |          关联的[**Bay**](Core-Model.md#bay)          |          [**SingleRef**](Base-Attribute-Type.md#singleref)          | 方便查找上级对象 |
|  `RefVoltageLevel`  | 关联的[**VoltageLevel**](Core-Model.md#voltagelevel) |          [**SingleRef**](Base-Attribute-Type.md#singleref)          | 方便查找上级对象 |
|   `RefSubstation`   |   关联的[**Substation**](Core-Model.md#substation)   |          [**SingleRef**](Base-Attribute-Type.md#singleref)          | 方便查找上级对象 |
|   `RefAuxSystem`    |                                                   |          [**SingleRef**](Base-Attribute-Type.md#singleref)          | 方便查找上级对象 |

</tab>

</tabs>

## 限值建模说明

为了兼容各种情况下对遥测量的限值设置，引入了静态限值、动态限值设置：

![限值模型](limit_model.png){border-effect="line"}

> 动态限值采用公式定义的方式来描述动态限值组生效的条件，每个限值组上记录可令该限值组生效的条件值。当前生效的限制组记录在动态限值对象上。
>
> `Analog`上自身限值的优先级最高，其次是静态限值，动态限值优先级最低。
>
{style="note"}

## StaticLimit

模拟量静态限值类。

> 静态限值类的属性与模拟量的限值属性基本一致，在需要批量设置模拟量限值的场景下使用。

<tabs>
    <tab title="维护分区">

|      **属性**       |  **中文名**  |                   **类型**                   | **说明** |
|:-----------------:|:---------:|:------------------------------------------:|:------:|
|      `name`       |    名称     | [String64](Base-Attribute-Type.md#string)  |        |
|      `desc`       |    描述     | [String128](Base-Attribute-Type.md#string) |        |
|     `enabled`     |   是否启用    |    [Bool](Base-Attribute-Type.md#bool)     |        |
|    `overDelay`    | 越限延迟参数(秒) |  [UShort](Base-Attribute-Type.md#ushort)   |        |
|  `limitDeadZone`  |  越限判断死区   |  [Double](Base-Attribute-Type.md#double)   |        |
| `highLimitLevel1` |    上限值    |  [Double](Base-Attribute-Type.md#double)   |        |
| `lowLimitLevel1`  |    下限值    |  [Double](Base-Attribute-Type.md#double)   |        |
| `highLimitLevel2` |   上上限值    |  [Double](Base-Attribute-Type.md#double)   |        |
| `lowLimitLevel2`  |   下下限值    |  [Double](Base-Attribute-Type.md#double)   |        |
| `highLimitLevel3` |   上上上限值   |  [Double](Base-Attribute-Type.md#double)   |        |
| `lowLimitLevel3`  |   下下下限值   |  [Double](Base-Attribute-Type.md#double)   |        |

</tab>
<tab title="同步分区">
无
</tab>
<tab title="索引分区">
无
</tab>

</tabs>

## DynLimitGroup

模拟量动态限值组。

> 动态限值组需要定义一个限值条件公式，根据公式的计算值决定使用哪一组动态限值。

<tabs>
    <tab title="维护分区">

|     **属性**      |  **中文名**  |                   **类型**                   | **说明** |
|:---------------:|:---------:|:------------------------------------------:|:------:|
|     `name`      |    名称     | [String64](Base-Attribute-Type.md#string)  |        |
|     `desc`      |    描述     | [String128](Base-Attribute-Type.md#string) |        |
|    `enabled`    |   是否启用    |    [Bool](Base-Attribute-Type.md#bool)     |        |
|   `condition`   |   限值条件    | [String128](Base-Attribute-Type.md#string) |        |
|   `overDelay`   | 越限延迟参数(秒) |  [UShort](Base-Attribute-Type.md#ushort)   |        |
| `limitDeadZone` |  越限判断死区   |  [Double](Base-Attribute-Type.md#double)   |        |

</tab>
<tab title="同步分区">

|      **属性**      | **中文名** |               **类型**                | **说明** |
|:----------------:|:-------:|:-----------------------------------:|:------:|
| `conditionValue` | 限值条件计算值 | [Long](Base-Attribute-Type.md#long) |        |

</tab>
<tab title="索引分区">

|             **属性**              |                               **中文名**                               |                               **类型**                                | **说明** |
|:-------------------------------:|:-------------------------------------------------------------------:|:-------------------------------------------------------------------:|:------:|
|       `ContainsDynLimit`        |              包含的[**DynLimit**](meas-model.md#dynlimit)              | [**SymbSeqArrayMaster**](Base-Attribute-Type.md#symbseqarraymaster) |        |
| `ContainsDynLimitConditionItem` | 包含的[**DynLimitConditionItem**](meas-model.md#dynlimitconditionitem) | [**SymbSeqArrayMaster**](Base-Attribute-Type.md#symbseqarraymaster) |        |
|          `RefDynLimit`          |             当前生效的[**DynLimit**](meas-model.md#dynlimit)             |          [**SingleRef**](Base-Attribute-Type.md#singleref)          |        |

</tab>

</tabs>

## DynLimit

模拟量动态限值。

> 从属于动态限值组，同组的动态限值在同一时间点只有一个对象生效。

<tabs>
    <tab title="维护分区">

|      **属性**       |  **中文名**   |                   **类型**                   |               **说明**                |
|:-----------------:|:----------:|:------------------------------------------:|:-----------------------------------:|
|      `name`       |     名称     | [String64](Base-Attribute-Type.md#string)  |                                     |
|      `desc`       |     描述     | [String128](Base-Attribute-Type.md#string) |                                     |
|   `enableValue`   | 生效对应的限值条件值 |    [Long](Base-Attribute-Type.md#long)     | 与`DynLimitGroup`的conditionValue进行比较 |
| `highLimitLevel1` |    上限值     |  [Double](Base-Attribute-Type.md#double)   |                                     |
| `lowLimitLevel1`  |    下限值     |  [Double](Base-Attribute-Type.md#double)   |                                     |
| `highLimitLevel2` |    上上限值    |  [Double](Base-Attribute-Type.md#double)   |                                     |
| `lowLimitLevel2`  |    下下限值    |  [Double](Base-Attribute-Type.md#double)   |                                     |
| `highLimitLevel3` |   上上上限值    |  [Double](Base-Attribute-Type.md#double)   |                                     |
| `lowLimitLevel3`  |   下下下限值    |  [Double](Base-Attribute-Type.md#double)   |                                     |

</tab>
<tab title="同步分区">
无

</tab>
<tab title="索引分区">

|         **属性**          |                       **中文名**                       |                              **类型**                               | **说明** |
|:-----------------------:|:---------------------------------------------------:|:-----------------------------------------------------------------:|:------:|
| `MemberOfDynLimitGroup` | 所属的[**DynLimitGroup**](meas-model.md#dynlimitgroup) | [**SymbSeqArraySlave**](Base-Attribute-Type.md#symbseqarrayslave) |        |

</tab>

</tabs>

## DynLimitConditionItem

模拟量动态限值条件因子。

> 名称与动态限值组限值条件字符串中的内容对应

<tabs>
    <tab title="维护分区">

| **属性** | **中文名** |                  **类型**                   | **说明** |
|:------:|:-------:|:-----------------------------------------:|:------:|
| `name` |   名称    | [String64](Base-Attribute-Type.md#string) |        |

</tab>
<tab title="同步分区">

|   **属性**    | **中文名** |                 **类型**                  | **说明** |
|:-----------:|:-------:|:---------------------------------------:|:------:|
|   `value`   |  因子的值   | [Double](Base-Attribute-Type.md#double) |        |
| `timeStamp` | 因子更新时间  |   [Time](Base-Attribute-Type.md#time)   |        |

</tab>
<tab title="索引分区">

|         **属性**          |                       **中文名**                       |                              **类型**                               |                                   **说明**                                   |
|:-----------------------:|:---------------------------------------------------:|:-----------------------------------------------------------------:|:--------------------------------------------------------------------------:|
| `MemberOfDynLimitGroup` | 所属的[**DynLimitGroup**](meas-model.md#dynlimitgroup) | [**SymbSeqArraySlave**](Base-Attribute-Type.md#symbseqarrayslave) |                                                                            |
|        `RefMeas`        |                        关联的测点                        |         [**SingleRef**](Base-Attribute-Type.md#singleref)         | 可以关联至[**Analog**](meas-model.md#analog)或[**Status**](meas-model.md#status) |

</tab>

</tabs>

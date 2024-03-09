# 一次设备模型

> 一次模型与电压等级、间隔的关联性最强，所以与间隔建立共生关系；
> 变压器比较特殊，与间隔建立非共生关系，与厂站建立共生关系；

## NormalPriEquipment

普通一次设备，继承自[`PrimaryEquipment`](Abstract-Class.md#primaryequipment)。

> 凡是不需要进行详细建模的一次设备，都可以归于此类。以`type`进行区分。

<tabs>
    <tab title="维护分区">

| **属性** | **中文名** |                        **类型**                         | **说明** |
|:------:|:-------:|:-----------------------------------------------------:|:------:|
| `type` | 一次设备类型  | [**PriEquipmentType**](Enum-Type.md#priequipmenttype) |  设备分类  |

</tab>
<tab title="同步分区">
无
</tab>
<tab title="索引分区">

|        **属性**         |                     **中文名**                     |                                **类型**                                 | **说明** |
|:---------------------:|:-----------------------------------------------:|:---------------------------------------------------------------------:|:------:|
|     `MemberOfBay`     |         所属的[**Bay**](Core-Model.md#bay)         |   [**SymbSeqArraySlave**](Base-Attribute-Type.md#symbseqarrayslave)   |        |
|  `ContainsTerminal`   |    包含的[**Terminal**](Core-Model.md#terminal)    | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|   `ContainsAnalog`    |      包含的[**Analog**](meas-model.md#analog)      | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|   `ContainsStatus`    |      包含的[**Status**](meas-model.md#status)      | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
| `ContainsAccumulator` | 包含的[**Accumulator**](meas-model.md#accumulator) | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |

</tab>

</tabs>

## PowerTransformer

变压器类，继承自[`PrimaryEquipment`](Abstract-Class.md#primaryequipment)。

> 为了使一次设备与间隔之间的关联关系统一为共生关系，将变压器绕组与变压器的关系设置为非共生。

<tabs>
    <tab title="维护分区">

| **属性** | **中文名** |               **类型**                |  **说明**  |
|:------:|:-------:|:-----------------------------------:|:--------:|
| `bool` | 是否为两卷变  | [Bool](Base-Attribute-Type.md#bool) | 两卷变or三卷变 |

</tab>
<tab title="同步分区">
无
</tab>
<tab title="索引分区">

|            **属性**             |                      **中文名**                       |                                **类型**                                 | **说明** |
|:-----------------------------:|:--------------------------------------------------:|:---------------------------------------------------------------------:|:------:|
| `ContainsPowerTransformerEnd` | 包含的[**PowerTransformerEnd**](#powertransformerend) | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|     `MemberOfSubstation`      |   所属的[**Substation**](Core-Model.md#substation)    |   [**SymbSeqArraySlave**](Base-Attribute-Type.md#symbseqarrayslave)   |        |
|         `MemberOfBay`         |          所属的[**Bay**](Core-Model.md#bay)           |  [**ASymbSeqDlistSlave**](Base-Attribute-Type.md#asymbseqdlistslave)  |        |
|       `ContainsAnalog`        |       包含的[**Analog**](meas-model.md#analog)        | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|       `ContainsStatus`        |       包含的[**Status**](meas-model.md#status)        | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|     `ContainsAccumulator`     |  包含的[**Accumulator**](meas-model.md#accumulator)   | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |

</tab>

</tabs>

## PowerTransformerEnd

变压器绕组类，继承自[`PrimaryEquipment`](Abstract-Class.md#primaryequipment)。

> 为了使一次设备与间隔之间的关联关系统一为共生关系，将变压器绕组与变压器的关系设置为非共生。

<tabs>
    <tab title="维护分区">

| **属性** | **中文名** |                               **类型**                                | **说明** |
|:------:|:-------:|:-------------------------------------------------------------------:|:------:|
| `type` |  绕组类型   | [**PowerTransformerEndType**](Enum-Type.md#powertransformerendtype) | 高/中/低  |

</tab>
<tab title="同步分区">
无
</tab>
<tab title="索引分区">

|           **属性**           |                     **中文名**                     |                                **类型**                                 | **说明** |
|:--------------------------:|:-----------------------------------------------:|:---------------------------------------------------------------------:|:------:|
| `MemberOfPowerTransformer` |  所属的[**PowerTransformer**](#powertransformer)   |  [**ASymbSeqDlistSlave**](Base-Attribute-Type.md#asymbseqdlistslave)  |        |
|       `MemberOfBay`        |         所属的[**Bay**](Core-Model.md#bay)         |   [**SymbSeqArraySlave**](Base-Attribute-Type.md#symbseqarrayslave)   |        |
|     `ContainsTerminal`     |    包含的[**Terminal**](Core-Model.md#terminal)    | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|      `ContainsAnalog`      |      包含的[**Analog**](meas-model.md#analog)      | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|      `ContainsStatus`      |      包含的[**Status**](meas-model.md#status)      | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|   `ContainsAccumulator`    | 包含的[**Accumulator**](meas-model.md#accumulator) | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |

</tab>

</tabs>

## ACLine

交流线路类，继承自[`PowerSystemResource`](Abstract-Class.md#powersystemresource)。

> 交流线路是交流线路端的容器，在SCADA模型里并不算是一次设备。交流线路会有两端，分别对应两个交流线路端对象。

<tabs>
    <tab title="维护分区">
无

</tab>
<tab title="同步分区">

|  **属性**   | **中文名** |                     **类型**                     | **说明** |
|:---------:|:-------:|:----------------------------------------------:|:------:|
| `mpower`  |  首端潮流   | [**Power**](Self-defined-Struct-Type.md#power) |        |
| `zmpower` |  末端潮流   | [**Power**](Self-defined-Struct-Type.md#power) |        |
| `empower` |  两端潮流差  | [**Power**](Self-defined-Struct-Type.md#power) |        |

</tab>
<tab title="索引分区">

> 交流线路的索引分区由验证程序自动关联，不允许手动更改;
>
{style="warning"}

> 必需的关联关系当然只有线路首末端引用关系，其他的关联其实已经间接可知，但为了查看方便还是加上了一些常用关联；
>
{style="note"}

|      **属性**      |                     **中文名**                     |                      **类型**                       | **说明** |
|:----------------:|:-----------------------------------------------:|:-------------------------------------------------:|:------:|
| `RefBaseVoltage` | 关联的[**BaseVoltage**](Core-Model.md#basevoltage) | [**SingleRef**](Base-Attribute-Type.md#singleref) |  方便查看  |
|  `RefACLineEnd`  |        关联的首端[**ACLineEnd**](#aclineend)         | [**SingleRef**](Base-Attribute-Type.md#singleref) |        |
| `RefSubstation`  | 关联的首端[**Substation**](Core-Model.md#substation) | [**SingleRef**](Base-Attribute-Type.md#singleref) |  方便查看  |
| `RefZACLineEnd`  |        关联的末端[**ACLineEnd**](#aclineend)         | [**SingleRef**](Base-Attribute-Type.md#singleref) |        |
| `RefZSubstation` | 关联的末端[**Substation**](Core-Model.md#substation) | [**SingleRef**](Base-Attribute-Type.md#singleref) |  方便查看  |

</tab>

</tabs> 

## MulBchACLine

多分支交流线路类，继承自[`PowerSystemResource`](Abstract-Class.md#powersystemresource)。

> 多分支交流线路也是是交流线路端的容器，但有可能有多个线路端(至少有3个)；
> 三分支属于T型接线方式，四分支属于π型接线方式；
> 模型上允许更多的分支数量；

<tabs>
    <tab title="维护分区">
无

</tab>
<tab title="同步分区">

|  **属性**   | **中文名**  |                     **类型**                     | **说明** |
|:---------:|:--------:|:----------------------------------------------:|:------:|
|  `bool`   | 是否进行潮流分配 |      [Bool](Base-Attribute-Type.md#bool)       |        |
| `empower` |   潮流差    | [**Power**](Self-defined-Struct-Type.md#power) |        |

</tab>
<tab title="索引分区">

> 交流线路端与多分支交流线路的关联需要人工指定;
>
{style="note"}

|       **属性**        |            **中文名**             |                                **类型**                                 | **说明** |
|:-------------------:|:------------------------------:|:---------------------------------------------------------------------:|:------:|
| `ContainsACLineEnd` | 包含的[**ACLineEnd**](#aclineend) | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |

</tab>

</tabs> 

## ACLineEnd

交流线路端类，继承自[`PrimaryEquipment`](Abstract-Class.md#primaryequipment)。

> 代表变电站内的线路对象；
> 通过名称一致性来进行交流线路端的匹配，即名称一致的两个线路端对象被认为是线路的首末端；

<tabs>
    <tab title="维护分区">
无

</tab>
<tab title="同步分区">

|  **属性**   | **中文名** |                     **类型**                     | **说明** |
|:---------:|:-------:|:----------------------------------------------:|:------:|
| `mpower`  |  首端潮流   | [**Power**](Self-defined-Struct-Type.md#power) |        |
| `zmpower` |  末端潮流   | [**Power**](Self-defined-Struct-Type.md#power) |        |
| `empower` |  两端潮流差  | [**Power**](Self-defined-Struct-Type.md#power) |        |

</tab>
<tab title="索引分区">

> 除了与多分支交流线路的关联外，交流线路端的索引分区由验证程序自动关联，不允许手动更改;
> 当多分支交流线路的关联设置后，其余的关联属性会清空。即一个线路端要么从属于交流线路，要么从属于多分支交流线路，不允许同时关联；
> {style="warning"}

|         **属性**         |                     **中文名**                     |                                **类型**                                 | **说明** |
|:----------------------:|:-----------------------------------------------:|:---------------------------------------------------------------------:|:------:|
|      `RefACLine`       |            关联的[**ACLine**](#acline)             |           [**SingleRef**](Base-Attribute-Type.md#singleref)           |        |
|     `RefACLineEnd`     |        关联的对端[**ACLineEnd**](#aclineend)         |           [**SingleRef**](Base-Attribute-Type.md#singleref)           |        |
| `MemberOfMulBchACLine` |      所属的[**MulBchACLine**](#mulbchacline)       |  [**ASymbSeqDlistSlave**](Base-Attribute-Type.md#asymbseqdlistslave)  |        |
|     `MemberOfBay`      |         所属的[**Bay**](Core-Model.md#bay)         |   [**SymbSeqArraySlave**](Base-Attribute-Type.md#symbseqarrayslave)   |        |
|   `ContainsTerminal`   |    包含的[**Terminal**](Core-Model.md#terminal)    | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|    `ContainsAnalog`    |      包含的[**Analog**](meas-model.md#analog)      | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|    `ContainsStatus`    |      包含的[**Status**](meas-model.md#status)      | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
| `ContainsAccumulator`  | 包含的[**Accumulator**](meas-model.md#accumulator) | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |

</tab>

</tabs> 

## BusbarSection

母线类，继承自[`PrimaryEquipment`](Abstract-Class.md#primaryequipment)。

> 母线通过维护`type`和`sectionType`来描述其具体类型信息；
>
> 在判断间隔运行状态时需要用到母线类型；
>
> 类型信息需要人工维护；

<tabs>
    <tab title="维护分区">

|    **属性**     | **中文名** |                  **类型**                   | **说明** |
|:-------------:|:-------:|:-----------------------------------------:|:------:|
|    `type`     |  母线类型   |    [**BusType**](Enum-Type.md#bustype)    |        |
| `sectionType` |  分段类型   | [**BusSecType**](Enum-Type.md#bussectype) |        |

</tab>
<tab title="同步分区">
无

</tab>
<tab title="索引分区">

|        **属性**         |                     **中文名**                     |                                **类型**                                 | **说明** |
|:---------------------:|:-----------------------------------------------:|:---------------------------------------------------------------------:|:------:|
|     `MemberOfBay`     |         所属的[**Bay**](Core-Model.md#bay)         |   [**SymbSeqArraySlave**](Base-Attribute-Type.md#symbseqarrayslave)   |        |
|  `ContainsTerminal`   |    包含的[**Terminal**](Core-Model.md#terminal)    | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|   `ContainsAnalog`    |      包含的[**Analog**](meas-model.md#analog)      | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|   `ContainsStatus`    |      包含的[**Status**](meas-model.md#status)      | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
| `ContainsAccumulator` | 包含的[**Accumulator**](meas-model.md#accumulator) | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |

</tab>

</tabs> 

## Disconnector

隔离刀闸类，继承自[`Switch`](Abstract-Class.md#switch)。

> 注意：接地刀闸作为一种分类，归到了隔离刀闸中
>
{style="warning"}

<tabs>
    <tab title="维护分区">

| **属性** | **中文名** |                        **类型**                         | **说明** |
|:------:|:-------:|:-----------------------------------------------------:|:------:|
| `type` | 隔离刀闸类型  | [**DisconnectorType**](Enum-Type.md#disconnectortype) |        |

</tab>
<tab title="同步分区">
无

</tab>
<tab title="索引分区">

|          **属性**           |                     **中文名**                     |                                **类型**                                 |        **说明**         |
|:-------------------------:|:-----------------------------------------------:|:---------------------------------------------------------------------:|:---------------------:|
|       `MemberOfBay`       |         所属的[**Bay**](Core-Model.md#bay)         |   [**SymbSeqArraySlave**](Base-Attribute-Type.md#symbseqarrayslave)   |                       |
| `MemberOfCompositeSwitch` |   所属的[**CompositeSwitch**](#compositeswitch)    |  [**ASymbSeqDlistSlave**](Base-Attribute-Type.md#asymbseqdlistslave)  | 所属的组合刀闸，联动用。例如手车、三态刀闸 |
|    `ContainsTerminal`     |    包含的[**Terminal**](Core-Model.md#terminal)    | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |                       |
|     `ContainsAnalog`      |      包含的[**Analog**](meas-model.md#analog)      | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |                       |
|     `ContainsStatus`      |      包含的[**Status**](meas-model.md#status)      | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |                       |
|   `ContainsAccumulator`   | 包含的[**Accumulator**](meas-model.md#accumulator) | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |

</tab>

</tabs> 

## CompositeSwitch

组合刀闸类，继承自[`PowerSystemResource`](Abstract-Class.md#powersystemresource)。

> 主要应用于小车刀闸。小车比较特殊，一般在模型上会处理成两把刀闸，需要把这两把刀闸的关联关系通过组合刀闸类保存下来，以便处理这两把刀闸的位置信号同步。
> 还有一种可能的应用场景就是三态刀闸，合/分/接地，也可以处理为两把刀闸，与小车的区别是这两把刀闸的位置信号是相反的。
>
{style="warning"}

<tabs>
    <tab title="维护分区">

| **属性** | **中文名** |                           **类型**                            | **说明** |
|:------:|:-------:|:-----------------------------------------------------------:|:------:|
| `type` | 组合刀闸类型  | [**CompositeSwitchType**](Enum-Type.md#compositeswitchtype) |        |

</tab>
<tab title="同步分区">
无

</tab>
<tab title="索引分区">

|         **属性**         |               **中文名**                |                                **类型**                                 |        **说明**         |
|:----------------------:|:------------------------------------:|:---------------------------------------------------------------------:|:---------------------:|
| `ContainsDisconnector` | 包含的[**Disconnector**](#disconnector) | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) | 所属的组合刀闸，联动用。例如手车、三态刀闸 |

</tab>

</tabs> 

## Breaker

开关类，继承自[`Switch`](Abstract-Class.md#switch)。

<tabs>
    <tab title="维护分区">

| **属性** | **中文名** |                   **类型**                    | **说明** |
|:------:|:-------:|:-------------------------------------------:|:------:|
| `type` |  开关类型   | [**BreakerType**](Enum-Type.md#breakertype) |        |

</tab>
<tab title="同步分区">
无

</tab>
<tab title="索引分区">

|        **属性**         |                     **中文名**                     |                                **类型**                                 | **说明** |
|:---------------------:|:-----------------------------------------------:|:---------------------------------------------------------------------:|:------:|
|     `MemberOfBay`     |         所属的[**Bay**](Core-Model.md#bay)         |   [**SymbSeqArraySlave**](Base-Attribute-Type.md#symbseqarrayslave)   |        |
|  `ContainsTerminal`   |    包含的[**Terminal**](Core-Model.md#terminal)    | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|   `ContainsAnalog`    |      包含的[**Analog**](meas-model.md#analog)      | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|   `ContainsStatus`    |      包含的[**Status**](meas-model.md#status)      | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
| `ContainsAccumulator` | 包含的[**Accumulator**](meas-model.md#accumulator) | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |

</tab>

</tabs>

## ShuntCompensator

并联容抗器类，继承自[`PrimaryEquipment`](Abstract-Class.md#primaryequipment)。


<tabs>
    <tab title="维护分区">

|   **属性**    | **中文名** |                 **类型**                  | **说明** |
|:-----------:|:-------:|:---------------------------------------:|:------:|
| `isReactor` | 是否为电抗器  |   [Bool](Base-Attribute-Type.md#bool)   | 默认为电容器 |
|  `ratedU`   |  额定电压   | [Double](Base-Attribute-Type.md#double) |        |
|  `ratedQ`   |  额定无功   | [Double](Base-Attribute-Type.md#double) |        |

</tab>
<tab title="同步分区">
无

</tab>
<tab title="索引分区">

|        **属性**         |                     **中文名**                     |                                **类型**                                 | **说明** |
|:---------------------:|:-----------------------------------------------:|:---------------------------------------------------------------------:|:------:|
|     `MemberOfBay`     |         所属的[**Bay**](Core-Model.md#bay)         |   [**SymbSeqArraySlave**](Base-Attribute-Type.md#symbseqarrayslave)   |        |
|  `ContainsTerminal`   |    包含的[**Terminal**](Core-Model.md#terminal)    | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|   `ContainsAnalog`    |      包含的[**Analog**](meas-model.md#analog)      | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|   `ContainsStatus`    |      包含的[**Status**](meas-model.md#status)      | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
| `ContainsAccumulator` | 包含的[**Accumulator**](meas-model.md#accumulator) | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |
|   `ContainsAnalog`    |      包含的[**Analog**](meas-model.md#analog)      | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|   `ContainsStatus`    |      包含的[**Status**](meas-model.md#status)      | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
| `ContainsAccumulator` | 包含的[**Accumulator**](meas-model.md#accumulator) | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |

</tab>

</tabs>

## SeriesCompensator

串联容抗器类，继承自[`PrimaryEquipment`](Abstract-Class.md#primaryequipment)。


<tabs>
    <tab title="维护分区">

| **属性** | **中文名** |                 **类型**                  | **说明** |
|:------:|:-------:|:---------------------------------------:|:------:|
|  `r`   |  正序电阻   | [Double](Base-Attribute-Type.md#double) |        |
|  `x`   |  正序电抗   | [Double](Base-Attribute-Type.md#double) |        |
| `xmin` | 电抗可调节下限 | [Double](Base-Attribute-Type.md#double) |        |
| `xmax` | 电抗可调节上限 | [Double](Base-Attribute-Type.md#double) |        |

</tab>
<tab title="同步分区">
无

</tab>
<tab title="索引分区">

|        **属性**         |                     **中文名**                     |                                **类型**                                 | **说明** |
|:---------------------:|:-----------------------------------------------:|:---------------------------------------------------------------------:|:------:|
|     `MemberOfBay`     |         所属的[**Bay**](Core-Model.md#bay)         |   [**SymbSeqArraySlave**](Base-Attribute-Type.md#symbseqarrayslave)   |        |
|  `ContainsTerminal`   |    包含的[**Terminal**](Core-Model.md#terminal)    | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|   `ContainsAnalog`    |      包含的[**Analog**](meas-model.md#analog)      | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|   `ContainsStatus`    |      包含的[**Status**](meas-model.md#status)      | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
| `ContainsAccumulator` | 包含的[**Accumulator**](meas-model.md#accumulator) | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |

</tab>

</tabs>

## StaticVarGenerator

SVG类，继承自[`PrimaryEquipment`](Abstract-Class.md#primaryequipment)。


<tabs>
    <tab title="维护分区">

| **属性** | **中文名** | **类型** | **说明** |
|:------:|:-------:|:------:|:------:|

</tab>
<tab title="同步分区">
无

</tab>
<tab title="索引分区">

|        **属性**         |                     **中文名**                     |                                **类型**                                 | **说明** |
|:---------------------:|:-----------------------------------------------:|:---------------------------------------------------------------------:|:------:|
|     `MemberOfBay`     |         所属的[**Bay**](Core-Model.md#bay)         |   [**SymbSeqArraySlave**](Base-Attribute-Type.md#symbseqarrayslave)   |        |
|  `ContainsTerminal`   |    包含的[**Terminal**](Core-Model.md#terminal)    | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|   `ContainsAnalog`    |      包含的[**Analog**](meas-model.md#analog)      | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|   `ContainsStatus`    |      包含的[**Status**](meas-model.md#status)      | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
| `ContainsAccumulator` | 包含的[**Accumulator**](meas-model.md#accumulator) | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |

</tab>

</tabs>

## StaticVarCompensator

SVC类，继承自[`PrimaryEquipment`](Abstract-Class.md#primaryequipment)。


<tabs>
    <tab title="维护分区">

| **属性** | **中文名** | **类型** | **说明** |
|:------:|:-------:|:------:|:------:|

</tab>
<tab title="同步分区">
无

</tab>
<tab title="索引分区">

|        **属性**         |                     **中文名**                     |                                **类型**                                 | **说明** |
|:---------------------:|:-----------------------------------------------:|:---------------------------------------------------------------------:|:------:|
|     `MemberOfBay`     |         所属的[**Bay**](Core-Model.md#bay)         |   [**SymbSeqArraySlave**](Base-Attribute-Type.md#symbseqarrayslave)   |        |
|  `ContainsTerminal`   |    包含的[**Terminal**](Core-Model.md#terminal)    | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|   `ContainsAnalog`    |      包含的[**Analog**](meas-model.md#analog)      | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|   `ContainsStatus`    |      包含的[**Status**](meas-model.md#status)      | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
| `ContainsAccumulator` | 包含的[**Accumulator**](meas-model.md#accumulator) | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |

</tab>

</tabs>

## EnergyConsumer

负荷类，继承自[`PrimaryEquipment`](Abstract-Class.md#primaryequipment)。

<tabs>
    <tab title="维护分区">

| **属性** | **中文名** |                **类型**                 | **说明** |
|:------:|:-------:|:-------------------------------------:|:------:|
| `type` |  负荷类型   | [**LoadType**](Enum-Type.md#loadtype) |        |

</tab>
<tab title="同步分区">
无

</tab>
<tab title="索引分区">

|        **属性**         |                     **中文名**                     |                                **类型**                                 | **说明** |
|:---------------------:|:-----------------------------------------------:|:---------------------------------------------------------------------:|:------:|
|     `MemberOfBay`     |         所属的[**Bay**](Core-Model.md#bay)         |   [**SymbSeqArraySlave**](Base-Attribute-Type.md#symbseqarrayslave)   |        |
|  `ContainsTerminal`   |    包含的[**Terminal**](Core-Model.md#terminal)    | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|   `ContainsAnalog`    |      包含的[**Analog**](meas-model.md#analog)      | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|   `ContainsStatus`    |      包含的[**Status**](meas-model.md#status)      | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
| `ContainsAccumulator` | 包含的[**Accumulator**](meas-model.md#accumulator) | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |

</tab>

</tabs>
# 核心模型

## Overview
核心模型基本参照IEC61970的分类方式。

## BaseVoltage

基准电压类，继承自[`IdentifiedObject`](Abstract-Class.md#identifiedobject)。

> **基准电压建模原则**
>
> 整个监控系统的基准电压建模在scada数据库中，不能随意增删。
>
{style="warning"}

<tabs>
    <tab title="维护分区">

|     **属性**     |  **中文名**  |                  **类型**                   |  **说明**   |
|:--------------:|:---------:|:-----------------------------------------:|:---------:|
|    `color`     |   颜色设定    | [String16](Base-Attribute-Type.md#string) |   界面显示用   |
| `ratedVoltage` |   额定电压    |  [Double](Base-Attribute-Type.md#double)  |  单位默认为kV  |
|     `isDC`     | 是否为直流电压等级 |    [Bool](Base-Attribute-Type.md#bool)    |           |
|  `enableMoni`  |  启用不平衡监视  |    [Bool](Base-Attribute-Type.md#bool)    |           |
| `normVoltage`  |   基准电压    |  [Double](Base-Attribute-Type.md#double)  |  单位默认为kV  |
|    `normR`     |   基准阻抗    |  [Double](Base-Attribute-Type.md#double)  |           |
|    `normP`     |  基准有功功率   |  [Double](Base-Attribute-Type.md#double)  |  单位默认为MW  |
|    `normQ`     |  基准无功功率   |  [Double](Base-Attribute-Type.md#double)  | 单位默认为MVar |
|     `unbP`     |  有功不平衡定值  |  [Double](Base-Attribute-Type.md#double)  |  单位默认为MW  |
|     `unbQ`     |  无功不平衡定值  |  [Double](Base-Attribute-Type.md#double)  | 单位默认为MVar |
|    `unbPQI`    | PQI不平衡定值  |  [Double](Base-Attribute-Type.md#double)  |           |

</tab>
<tab title="同步分区">
无
</tab>
<tab title="索引分区">
无
</tab>

</tabs>

## Substation

厂站类，继承自[`EquipmentContainer`](Abstract-Class.md#equipmentcontainer)。

<tabs>
    <tab title="维护分区">

|    **属性**    | **中文名** |                   **类型**                   |     **说明**      |
|:------------:|:-------:|:------------------------------------------:|:---------------:|
|    `type`    |  厂站类型   |      [FacType](Enum-Type.md#factype)       |   二级枚举，默认为变电站   |
| `longtitude` |   经度    |   [Float](Base-Attribute-Type.md#float)    |                 |
|  `latitude`  |   纬度    |   [Float](Base-Attribute-Type.md#float)    |                 |
|  `altitude`  |   海拔    |   [Float](Base-Attribute-Type.md#float)    |                 |
|  `picName`   |  厂站图名称  | [String128](Base-Attribute-Type.md#string) | 存放图形全路径，用于告警推画面 |

</tab>
<tab title="同步分区">
无
</tab>
<tab title="索引分区">

- 厂站与电压等级、IED、控制对象、二次设备为共生父子关联
- 厂站与状态量、模拟量、累计量为非共生父子关联

|            **属性**            |                              **中文名**                               |                              **类型**                               | **说明** |
|:----------------------------:|:------------------------------------------------------------------:|:-----------------------------------------------------------------:|:------:|
|    `ContainsVoltageLevel`    |                  包含的[VoltageLevel](#voltagelevel)                  |  [SymbSeqArrayMaster](Base-Attribute-Type.md#symbseqarraymaster)  |        |
|  `ContainsPowerTransformer`  | 包含的[PowerTransformer](primary-equipment-model.md#powertransformer) |  [SymbSeqArrayMaster](Base-Attribute-Type.md#symbseqarraymaster)  |        |
|        `ContainsIED`         |                    包含的[IED](meas-model.md#ied)                     |  [SymbSeqArrayMaster](Base-Attribute-Type.md#symbseqarraymaster)  |        |
|       `ContainsStatus`       |                               包含的状态量                               | [ASymbSeqDlistMaster](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|       `ContainsAnalog`       |                               包含的模拟量                               | [ASymbSeqDlistMaster](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|     `ContainsAccmulator`     |                               包含的累计量                               | [ASymbSeqDlistMaster](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|      `ContainsControl`       |                              包含的控制对象                               |  [SymbSeqArrayMaster](Base-Attribute-Type.md#symbseqarraymaster)  |        |
| `ContainsSecondaryEquipment` |                              包含的二次设备                               |  [SymbSeqArrayMaster](Base-Attribute-Type.md#symbseqarraymaster)  |        |
|    `RefCtrlCheckSetting`     |                             关联的控制防误设定                              |           [SingleRef](Base-Attribute-Type.md#singleref)           |        |

</tab>

</tabs>

## VoltageLevel

电压等级类，继承自[`EquipmentContainer`](Abstract-Class.md#equipmentcontainer)。

<tabs>
    <tab title="维护分区">
无

</tab>
<tab title="同步分区">
无
</tab>
<tab title="索引分区">

|           **属性**           |                 **中文名**                  |                             **类型**                              |     **说明**     |
|:--------------------------:|:----------------------------------------:|:---------------------------------------------------------------:|:--------------:|
|    `MemberOfSubstation`    |       从属于[Substation](#substation)       |  [SymbSeqArraySlave](Base-Attribute-Type.md#symbseqarrayslave)  |                |
|      `RefBaseVoltage`      |      关联的[BaseVoltage](#basevoltage)      |          [SingleRef](Base-Attribute-Type.md#singleref)          |       必填       |
|       `ContainsBay`        |              包含的[Bay](#bay)              | [SymbSeqArrayMaster](Base-Attribute-Type.md#symbseqarraymaster) |                |
| `ContainsConnectivityNode` | 包含的[ConnectivityNode](#connectivitynode) | [SymbSeqArrayMaster](Base-Attribute-Type.md#symbseqarraymaster) | 用于体现设备与设备的连接关系 |

</tab>

</tabs>

## Bay

间隔类，继承自[`EquipmentContainer`](Abstract-Class.md#equipmentcontainer)。

设计原则
: 所有的设备(一、二次设备)都应根据其所属的电压等级，从属于某个间隔下；
: 站控层设备可建立虚拟电压等级、虚拟间隔来存放；
: 变压器根据其最高电压等级来存放；
: 在验证数据库时，自动维护间隔主设备与间隔开关，方便后续应用使用；
: 间隔运行状态由scada服务程序定时刷新(在建立了拓扑模型的情况下)；

<tabs>
    <tab title="维护分区">

|  **属性**   | **中文名** |                   **类型**                   | **说明**  |
|:---------:|:-------:|:------------------------------------------:|:-------:|
| `picName` |  间隔图名称  | [String128](Base-Attribute-Type.md#string) | 用于告警推画面 |
|  `type`   |  间隔类型   |                                            |  需求待定   |

</tab>
<tab title="同步分区">

|  **属性**  | **中文名** |               **类型**                |    **说明**    |
|:--------:|:-------:|:-----------------------------------:|:------------:|
| `status` | 间隔运行状态  | [BayStatus](Enum-Type.md#baystatus) | 由程序自动判断，用于顺控 |

</tab>
<tab title="索引分区">

|            **属性**            |                              **中文名**                               |                              **类型**                               |    **说明**    |
|:----------------------------:|:------------------------------------------------------------------:|:-----------------------------------------------------------------:|:------------:|
|         `RefBreaker`         |                                间隔开关                                |           [SingleRef](Base-Attribute-Type.md#singleref)           | 由验库程序判断并自动关联 |
|    `RefPrimaryEquipment`     |                             间隔主设备(多表)                              |           [SingleRef](Base-Attribute-Type.md#singleref)           | 由验库程序判断并自动关联 |
|    `MemberOfVoltageLevel`    |                  从属于[VoltageLevel](#voltagelevel)                  |   [SymbSeqArraySlave](Base-Attribute-Type.md#symbseqarrayslave)   |              |
|  `ContainsPrimaryEquipment`  |                            包含的一次设备(多表)                             |  [SymbSeqArrayMaster](Base-Attribute-Type.md#symbseqarraymaster)  |              |
|  `ContainsPowerTransformer`  | 包含的[PowerTransformer](primary-equipment-model.md#powertransformer) | [ASymbSeqDlistMaster](Base-Attribute-Type.md#asymbseqdlistmaster) |              |
| `ContainsSecondaryEquipment` |                              包含的二次设备                               |                                                                   |              |
|       `ContainsStatus`       |                               包含的状态量                               |                                                                   |              |
|       `ContainsAnalog`       |                               包含的模拟量                               |                                                                   |              |
|     `ContainsAccmulator`     |                               包含的累计量                               |                                                                   |              |

</tab>

</tabs>

## ConnectivityNode

连接节点类，继承自[`IdentifiedObject`](Abstract-Class.md#identifiedobject)。

> 拓扑节点与连接节点是动态的一对多的关系，且时常需要更新，不适合直接通过实时库的关联关系来体现。
> 采用下标链表的方式记录关系，使用起来稍微麻烦一些，但可以避免频繁增删关联关系。
> `tnode`域记录连接节点所属拓扑节点的下标，拓扑节点在验库初始化时插满，后续只更新属性，不进行增删操作。
> 拓扑点上记录第一个连接节点的下标，然后与连接节点上的`next`域配合形成链表以用于遍历。

<tabs>
    <tab title="维护分区">
无
</tab>
<tab title="同步分区">

|   **属性**   |  **中文名**  |                    **类型**                     | **说明** |
|:----------:|:---------:|:---------------------------------------------:|:------:|
| `topColor` |   拓扑状态    | [TopColor](Self-defined-Bit-Type.md#topcolor) |        |
|  `tnode`   |  所属拓扑点下标  |      [Long](Base-Attribute-Type.md#long)      | 为负数时无效 |
|   `next`   | 下一个连接节点下标 |      [Long](Base-Attribute-Type.md#long)      | 为负数时无效 |

</tab>
<tab title="索引分区">

|         **属性**         |             **中文名**              |                              **类型**                               | **说明** |
|:----------------------:|:--------------------------------:|:-----------------------------------------------------------------:|:------:|
| `MemberOfVoltageLevel` | 从属于[VoltageLevel](#voltagelevel) |   [SymbSeqArraySlave](Base-Attribute-Type.md#symbseqarrayslave)   |        |
|   `ContainsTerminal`   |     包含的[Terminal](#terminal)     | [ASymbSeqDlistMaster](Base-Attribute-Type.md#asymbseqdlistmaster) |        |

</tab>

</tabs>

## Terminal

端点类，继承自[`IdentifiedObject`](Abstract-Class.md#identifiedobject)。

> 与图形中图元的端点需要一一对应。
> `picName`记录图元的端点名称。

<tabs>
    <tab title="维护分区">

|  **属性**   |    **中文名**    |                  **类型**                   |  **说明**   |
|:---------:|:-------------:|:-----------------------------------------:|:---------:|
| `picName` | 对应图元在画面中的端点名称 | [String16](Base-Attribute-Type.md#string) | 由画图填库程序填写 |

</tab>
<tab title="同步分区">
无
</tab>
<tab title="索引分区">

|           **属性**           |                 **中文名**                  |                             **类型**                              | **说明** |
|:--------------------------:|:----------------------------------------:|:---------------------------------------------------------------:|:------:|
| `MemberOfConnectivityNode` | 从属于[ConnectivityNode](#connectivitynode) | [ASymbSeqDlistSlave](Base-Attribute-Type.md#asymbseqdlistslave) |        |
| `MemberOfPrimaryEquipment` |               从属于一次设备(多表)                |  [SymbSeqDlistSlave](Base-Attribute-Type.md#symbseqdlistslave)  |        |

</tab>

</tabs>
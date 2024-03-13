# 储能模型

## ESUnit

储能机组类，继承自[`Equipment`](Abstract-Class.md#equipment)。

<tabs>
    <tab title="维护分区">

|     **属性**      | **中文名** |                 **类型**                  | **说明** |
|:---------------:|:-------:|:---------------------------------------:|:------:|
| `ratedCapacity` |  额定容量   | [Double](Base-Attribute-Type.md#double) |        |
|  `ratedPower`   |  额定功率   | [Double](Base-Attribute-Type.md#double) |        |
|     `type`      |  机组类型   |   [Long](Base-Attribute-Type.md#long)   |   备用   |

</tab>
<tab title="同步分区">
无

</tab>
<tab title="索引分区">

|        **属性**         |                     **中文名**                     |                                **类型**                                 | **说明** |
|:---------------------:|:-----------------------------------------------:|:---------------------------------------------------------------------:|:------:|
| `MemberOfSubstation`  |  所属的[**Substation**](Core-Model.md#substation)  |     [SymbSeqArraySlave](Base-Attribute-Type.md#symbseqarrayslave)     |        |
|   `MemberOfRegion`    |      所属的[**Region**](auxi-model.md#region)      | [**ASymbSeqDlistSlave**](Base-Attribute-Type.md#asymbseqdlistmaster)  |        |
|      `RefJKIed`       |      关联的机控IED[**IED**](meas-model.md#ied)       |           [**SingleRef**](Base-Attribute-Type.md#singleref)           |        |
|   `ContainsAnalog`    |      包含的[**Analog**](meas-model.md#analog)      | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|   `ContainsStatus`    |      包含的[**Status**](meas-model.md#status)      | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
| `ContainsAccumulator` | 包含的[**Accumulator**](meas-model.md#accumulator) | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|     `ContainsPcs`     |       包含的[**ESPcs**](ess-model.md#espcs)        | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |

</tab>
</tabs>

## ESPcs

储能PCS类，继承自[`PrimaryEquipment`](Abstract-Class.md#primaryequipment)。

<tabs>
    <tab title="维护分区">

| **属性** | **中文名** |               **类型**                | **说明** |
|:------:|:-------:|:-----------------------------------:|:------:|
|  `no`  |   序号    | [Long](Base-Attribute-Type.md#long) | 机控内部序号 |

</tab>
<tab title="同步分区">
无

</tab>
<tab title="索引分区">

|        **属性**         |                     **中文名**                     |                                **类型**                                 | **说明** |
|:---------------------:|:-----------------------------------------------:|:---------------------------------------------------------------------:|:------:|
|   `MemberOfESUnit`    |      所属的[**ESUnit**](ess-model.md#esunit)       |  [**ASymbSeqDlistSlave**](Base-Attribute-Type.md#asymbseqdlistslave)  |        |
|   `ContainsAnalog`    |      包含的[**Analog**](meas-model.md#analog)      | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|   `ContainsStatus`    |      包含的[**Status**](meas-model.md#status)      | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
| `ContainsAccumulator` | 包含的[**Accumulator**](meas-model.md#accumulator) | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|    `ContainsBCMU`     |        包含的[**BCMU**](ess-model.md#bcmu)         |  [**SymbSeqArrayMaster**](Base-Attribute-Type.md#symbseqarraymaster)  |        |

</tab>

</tabs>

## BCMU

电池簇类，继承自[`Equipment`](Abstract-Class.md#equipment)。

<tabs>
    <tab title="维护分区">

| **属性** | **中文名** |               **类型**                | **说明**  |
|:------:|:-------:|:-----------------------------------:|:-------:|
|  `no`  |   序号    | [Long](Base-Attribute-Type.md#long) | pcs内部序号 |

</tab>
<tab title="同步分区">
无

</tab>
<tab title="索引分区">

|        **属性**         |                     **中文名**                     |                                **类型**                                 | **说明** |
|:---------------------:|:-----------------------------------------------:|:---------------------------------------------------------------------:|:------:|
|   `ContainsAnalog`    |      包含的[**Analog**](meas-model.md#analog)      | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|   `ContainsStatus`    |      包含的[**Status**](meas-model.md#status)      | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
| `ContainsAccumulator` | 包含的[**Accumulator**](meas-model.md#accumulator) | [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster) |        |
|    `MemberOfESPcs`    |       所属的[**ESPcs**](ess-model.md#espcs)        |   [**SymbSeqArraySlave**](Base-Attribute-Type.md#symbseqarrayslave)   |        |

</tab>

</tabs>
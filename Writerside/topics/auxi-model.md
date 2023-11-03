# 辅控模型

## Region

站内区域表，继承自[`PowerSystemResource`](Abstract-Class.md#powersystemresource)。

> 站内区域在辅控系统中使用较多，但实际上所有设备都可以与区域发生关联；
>
> 区域使用坐标来描述位置信息，不同的楼层属于不同的区域；
>
> 区域可以自嵌套以记录区域之间的从属关系；
>
> 如果站内区域为矩形，使用对角两个坐标点来描述；
>
> 其他情况需使用多个坐标点来描述区域的边界；
> {style="note"}

<tabs>
    <tab title="维护分区">

|  **属性**  | **中文名** |                  **类型**                   | **说明** |
|:--------:|:-------:|:-----------------------------------------:|:------:|
|  `type`  | 一次设备类型  | [**RegionType**](Enum-Type.md#regiontype) |  区域分类  |
| `length` |   长度    |   [Float](Base-Attribute-Type.md#float)   |        |
| `width`  |   宽度    |   [Float](Base-Attribute-Type.md#float)   |        |
| `height` |   高度    |   [Float](Base-Attribute-Type.md#float)   |        |
| `isRect` |  是否为矩形  |   [Bool](Base-Attribute-Type.md#float)    |        |

</tab>
<tab title="同步分区">
无
</tab>
<tab title="索引分区">

|            **属性**            |                                  **中文名**                                   |                                   **类型**                                    | **说明** |
|:----------------------------:|:--------------------------------------------------------------------------:|:---------------------------------------------------------------------------:|:------:|
|       `MemberOfRegion`       |                   所属的[**Region**](auxi-model.md#region)                    |  [**ASymbInlineDlistSlave**](Base-Attribute-Type.md#asymbinlinedlistslave)  |        |
|       `ContainsRegion`       |                   包含的[**Region**](auxi-model.md#region)                    | [**ASymbInlineDlistMaster**](Base-Attribute-Type.md#asymbinlinedlistmaster) |        |
|  `ContainsRegionCoordinate`  |         包含的[**RegionCoordinate**](auxi-model.md#regioncoordinate)          |     [**SymbSeqArrayMaster**](Base-Attribute-Type.md#symbseqarraymaster)     |        |
|  `ContainsPrimaryEquipment`  |                                  包含的一次设备                                   |    [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster)    |        |
| `ContainsSecondaryEquipment` | 包含的[**AuxiliaryEquipment**](primary-equipment-model.md#secondaryequipment) |    [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster)    |        |
| `ContainsAuxiliaryEquipment` |       包含的[**AuxiliaryEquipment**](auxi-model.md#auxiliaryequipment)        |    [**ASymbSeqDlistMaster**](Base-Attribute-Type.md#asymbseqdlistmaster)    |        |

</tab>

</tabs>

## RegionCoordinate

站内区域坐标表。

<tabs>
    <tab title="维护分区">

| **属性** | **中文名** |                  **类型**                   | **说明** |
|:------:|:-------:|:-----------------------------------------:|:------:|
| `name` |  坐标名称   | [String32](Base-Attribute-Type.md#string) |        |
|  `x`   |   横坐标   |   [Float](Base-Attribute-Type.md#float)   |        |
|  `y`   |   纵坐标   |   [Float](Base-Attribute-Type.md#float)   |        |

</tab>
<tab title="同步分区">
无
</tab>
<tab title="索引分区">

|      **属性**      |                **中文名**                |                                 **类型**                                  | **说明** |
|:----------------:|:-------------------------------------:|:-----------------------------------------------------------------------:|:------:|
| `MemberOfRegion` | 所属的[**Region**](auxi-model.md#region) |  [ASymbInlineDlistSlave](Base-Attribute-Type.md#asymbinlinedlistslave)  |        |
| `ContainsRegion` | 包含的[**Region**](auxi-model.md#region) | [ASymbInlineDlistMaster](Base-Attribute-Type.md#asymbinlinedlistmaster) |        |

</tab>

</tabs>

## AuxiliarySystem

辅控系统表，继承自[`IdentifiedObject`](Abstract-Class.md#identifiedobject)。

> 各地对辅控系统的分类方式不统一，故采用自定义的方式来对辅控系统进行分类
>
> {style="note"}

<tabs>
    <tab title="维护分区">
无
</tab>
<tab title="同步分区">
无
</tab>
<tab title="索引分区">

|            **属性**            |                            **中文名**                            |                               **类型**                                | **说明** |
|:----------------------------:|:-------------------------------------------------------------:|:-------------------------------------------------------------------:|:------:|
|     `MemberOfSubstation`     |         所属的[**Substation**](Core-Model.md#substation)         |    [SymbSeqArraySlave](Base-Attribute-Type.md#symbseqarrayslave)    |        |
| `ContainsAuxiliaryEquipment` | 包含的[**AuxiliaryEquipment**](auxi-model.md#auxiliaryequipment) |   [SymbSeqArrayMaster](Base-Attribute-Type.md#symbseqarraymaster)   |        |
|  `ContainsRegionCoordinate`  |   包含的[**RegionCoordinate**](auxi-model.md#regioncoordinate)   | [**SymbSeqArrayMaster**](Base-Attribute-Type.md#symbseqarraymaster) |        |

</tab>

</tabs>

## AuxiliaryEquipment

辅控设备表，继承自[`Equipment`](Abstract-Class.md#equipment)。

<tabs>
    <tab title="维护分区">

| **属性** | **中文名** |                            **类型**                             | **说明** |
|:------:|:-------:|:-------------------------------------------------------------:|:------:|
| `type` | 辅控设备类型  | [AuxiliaryEquipmentType](Enum-Type.md#auxiliaryequipmenttype) |        |

</tab>
<tab title="同步分区">
无
</tab>
<tab title="索引分区">

|            **属性**            |                            **中文名**                            |                               **类型**                                |    **说明**     |
|:----------------------------:|:-------------------------------------------------------------:|:-------------------------------------------------------------------:|:-------------:|
|   `MemberOfAuxilarySystem`   |    所属的[**AuxilarySystem**](auxi-model.md#auxiliarysystem)     |    [SymbSeqArraySlave](Base-Attribute-Type.md#symbseqarrayslave)    |               |
| `ContainsAuxiliaryEquipment` | 包含的[**AuxiliaryEquipment**](auxi-model.md#auxiliaryequipment) |   [SymbSeqArrayMaster](Base-Attribute-Type.md#symbseqarraymaster)   |               |
|  `ContainsRegionCoordinate`  |   包含的[**RegionCoordinate**](auxi-model.md#regioncoordinate)   | [**SymbSeqArrayMaster**](Base-Attribute-Type.md#symbseqarraymaster) |               |
|    `RefPrimaryEquipment`     |                            关联的一次设备                            |          [**SingleRef**](Base-Attribute-Type.md#singleref)          | 可关联到所有种类的一次设备 |

</tab>

</tabs>

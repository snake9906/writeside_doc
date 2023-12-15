# 监视模型

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
|       `ContainsDynLimit`        |              包含的[**DynLimit**](moni-model.md#dynlimit)              | [**SymbSeqArrayMaster**](Base-Attribute-Type.md#symbseqarraymaster) |        |
| `ContainsDynLimitConditionItem` | 包含的[**DynLimitConditionItem**](moni-model.md#dynlimitconditionitem) | [**SymbSeqArrayMaster**](Base-Attribute-Type.md#symbseqarraymaster) |        |
|          `RefDynLimit`          |             当前生效的[**DynLimit**](moni-model.md#dynlimit)             |          [**SingleRef**](Base-Attribute-Type.md#singleref)          |        |

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
| `MemberOfDynLimitGroup` | 所属的[**DynLimitGroup**](moni-model.md#dynlimitgroup) | [**SymbSeqArraySlave**](Base-Attribute-Type.md#symbseqarrayslave) |        |

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
| `MemberOfDynLimitGroup` | 所属的[**DynLimitGroup**](moni-model.md#dynlimitgroup) | [**SymbSeqArraySlave**](Base-Attribute-Type.md#symbseqarrayslave) |                                                                            |
|        `RefMeas`        |                        关联的测点                        |         [**SingleRef**](Base-Attribute-Type.md#singleref)         | 可以关联至[**Analog**](meas-model.md#analog)或[**Status**](meas-model.md#status) |

</tab>

</tabs>

## 标识牌建模说明

对于标识牌模型来说，有两个方面需要灵活设置，一个是允许挂牌的对象，一个是挂牌的影响：

- 可挂牌对象通过定义设备来进行配置；
- 挂牌影响通过配置对设备、测点的“监盘状态”域的修改来进行配置；

![标识牌模型](tag_model.png){border-effect="line"}

## EquipmentDefine

设备定义表。通过指定表id和过滤条件的方式来进行特定设备类型的定义。

> `condition`需符合平台条件检索String的语法规则
>
{style="warning"}

<tabs>
    <tab title="维护分区">

|   **属性**    | **中文名**  |                   **类型**                   |             **说明**              |
|:-----------:|:--------:|:------------------------------------------:|:-------------------------------:|
|   `name`    |    名称    | [String64](Base-Attribute-Type.md#string)  |                                 |
|   `desc`    |    描述    | [String128](Base-Attribute-Type.md#string) |                                 |
|  `tableID`  | 对应的设备表id |   [ULong](Base-Attribute-Type.md#ulong)    |          用于指定一张特定的设备表           |
| `condition` |   过滤条件   | [String128](Base-Attribute-Type.md#string) | 可以设置过滤条件对设备进行筛选，例如对设备`type`进行判断 |

</tab>
<tab title="同步分区">
无

</tab>
<tab title="索引分区">

|       **属性**       |                   **中文名**                   |                      **类型**                       | **说明** |
|:------------------:|:-------------------------------------------:|:-------------------------------------------------:|:------:|
| `ContainTagDefine` | 所属的[**TagDefine**](moni-model.md#tagdefine) | [**M2NMaster**](Base-Attribute-Type.md#m2nmaster) | m:n关联  |

</tab>

</tabs>

## TagActionDefine

牌置数定义表。配置对挂牌对象的域置数操作(摘牌时进行挂牌的反向置数操作)。

> 设备上有可能同时挂有多个牌，在摘牌进行反向置数时需注意对剩余牌的影响。
>
{style="warning"}

<tabs>
    <tab title="维护分区">

|   **属性**    | **中文名** |                   **类型**                   |   **说明**   |
|:-----------:|:-------:|:------------------------------------------:|:----------:|
|   `name`    |   名称    | [String64](Base-Attribute-Type.md#string)  |            |
|   `desc`    |   描述    | [String128](Base-Attribute-Type.md#string) |            |
| `fieldName` | 置数影响的域名 | [String32](Base-Attribute-Type.md#string)  | 用于指定需要置数的域 |
| `setValue`  |  置数的值   |    [Bool](Base-Attribute-Type.md#bool)     |   只能置0/1   |

</tab>
<tab title="同步分区">
无

</tab>
<tab title="索引分区">

|       **属性**       |                   **中文名**                   |                      **类型**                       | **说明** |
|:------------------:|:-------------------------------------------:|:-------------------------------------------------:|:------:|
| `ContainTagDefine` | 所属的[**TagDefine**](moni-model.md#tagdefine) | [**M2NMaster**](Base-Attribute-Type.md#m2nmaster) | m:n关联  |

</tab>

</tabs>

## TagDefine

牌定义表。通过其关联的`EquipmentDefine`和`TagActionDefine`来自定义牌的行为特性。

<tabs>
    <tab title="维护分区">

| **属性** | **中文名** |                   **类型**                   | **说明** |
|:------:|:-------:|:------------------------------------------:|:------:|
| `name` |   名称    | [String64](Base-Attribute-Type.md#string)  |        |
| `desc` |   描述    | [String128](Base-Attribute-Type.md#string) |        |

</tab>
<tab title="同步分区">
无

</tab>
<tab title="索引分区">

|          **属性**          |                         **中文名**                         |                     **类型**                      | **说明** |
|:------------------------:|:-------------------------------------------------------:|:-----------------------------------------------:|:------:|
| `ContainEquipmentDefine` | 所属的[**EquipmentDefine**](moni-model.md#equipmentdefine) | [**M2NSlave**](Base-Attribute-Type.md#m2nslave) | m:n关联  |
| `ContainTagActionDefine` | 所属的[**TagActionDefine**](moni-model.md#tagactiondefine) | [**M2NSlave**](Base-Attribute-Type.md#m2nslave) | m:n关联  |

</tab>

</tabs>

## Tag

标识牌表。

> 会在系统运行时进行增删操作，不允许与本表对象建立关联关系
>
{style="warning"}

> SCADA数据库做为标志牌的信息源，需要提供mmi所需的相关属性以实现图形展示的功能
>
{style="tip"}

<tabs>
    <tab title="维护分区">
无

</tab>
<tab title="同步分区">

|    **属性**    |    **中文名**    |                   **类型**                   |       **说明**       |
|:------------:|:-------------:|:------------------------------------------:|:------------------:|
|    `name`    |      名称       | [String64](Base-Attribute-Type.md#string)  |                    |
|  `comment`   |      备注       | [String256](Base-Attribute-Type.md#string) |                    |
| `oprObjOID`  |    挂牌对象OID    |  [TDBOID](Base-Attribute-Type.md#tdboid)   | 不一定是设备，也有可能是间隔、光字牌 |
| `oprObjName` |    挂牌对象名称     | [String128](Base-Attribute-Type.md#string) |                    |
|  `facName`   |     厂站名称      | [String128](Base-Attribute-Type.md#string) |                    |
|  `bayName`   |     间隔名称      | [String128](Base-Attribute-Type.md#string) |                    |
|   `oprMan`   |      操作人      | [String128](Base-Attribute-Type.md#string) |                    |
|  `oprTime`   |     挂牌时间      |    [Time](Base-Attribute-Type.md#time)     |                    |
|     `x`      |     牌x轴坐标     |   [Float](Base-Attribute-Type.md#float)    |       mmi使用        |
|     `y`      |     牌y轴坐标     |   [Float](Base-Attribute-Type.md#float)    |       mmi使用        |
|   `length`   |      牌长度      |   [Float](Base-Attribute-Type.md#float)    |       mmi使用        |
|   `height`   |      牌高度      |   [Float](Base-Attribute-Type.md#float)    |       mmi使用        |
| `oprObjType` | 挂牌对象在mmi中的类型名 | [String16](Base-Attribute-Type.md#string)  |       mmi使用        |

</tab>
<tab title="索引分区">

|     **属性**     |                   **中文名**                   |                      **类型**                       | **说明** |
|:--------------:|:-------------------------------------------:|:-------------------------------------------------:|:------:|
| `RefTagDefine` | 所属的[**TagDefine**](moni-model.md#tagdefine) | [**SingleRef**](Base-Attribute-Type.md#singleref) |        |

</tab>

</tabs>


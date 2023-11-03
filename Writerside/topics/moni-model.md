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
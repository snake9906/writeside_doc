# Core Model

核心模型参照IEC61970的分类方式：

## BaseVoltage

基准电压类，继承自[`IdentifiedObject`](Abstract-Class.md#identifiedobject)。

> **Highlight important information**
>
> You can change the element to *tip* or *warning* by renaming the style attribute below.
>
{style="tip"}

<tabs>
    <tab title="维护分区">

|     **属性**     |  **中文名**  |                 **类型**                  |  **说明**   |
|:--------------:|:---------:|:---------------------------------------:|:---------:|
| `ratedVoltage` |   额定电压    | [Double](Base-Attribute-Type.md#double) |  单位默认为kV  |
|     `isDC`     | 是否为直流电压等级 |   [Bool](Base-Attribute-Type.md#bool)   |           |
|  `enableMoni`  |  启用不平衡监视  |   [Bool](Base-Attribute-Type.md#bool)   |           |
| `normVoltage`  |   基准电压    | [Double](Base-Attribute-Type.md#double) |  单位默认为kV  |
|    `normR`     |   基准阻抗    | [Double](Base-Attribute-Type.md#double) |           |
|    `normP`     |  基准有功功率   | [Double](Base-Attribute-Type.md#double) |  单位默认为MW  |
|    `normQ`     |  基准无功功率   | [Double](Base-Attribute-Type.md#double) | 单位默认为MVar |
|     `unbP`     |  有功不平衡定值  | [Double](Base-Attribute-Type.md#double) |  单位默认为MW  |
|     `unbQ`     |  无功不平衡定值  | [Double](Base-Attribute-Type.md#double) | 单位默认为MVar |
|    `unbPQI`    | PQI不平衡定值  | [Double](Base-Attribute-Type.md#double) |           |

</tab>
<tab title="同步分区">
无
</tab>
<tab title="索引分区">
无
</tab>

</tabs>

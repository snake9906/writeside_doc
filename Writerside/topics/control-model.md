# 控制模型

## Control

控制对象类，继承自[`PowerSystemResource`](Abstract-Class.md#powersystemresource)。

> 控制对象将前置的遥控、遥调与状态量、模拟量关联起来。

<tabs>
    <tab title="维护分区">

|     **属性**     | **中文名**  |                   **类型**                   |      **说明**      |
|:--------------:|:--------:|:------------------------------------------:|:----------------:|
|     `type`     |   控制类型   |   [**CtrlType**](Enum-Type.md#ctrltype)    |                  |
|  `guardMode`   |   监护模式   |  [**GuardMode**](Enum-Type.md#guardmode)   |                  |
|  `ctrlObjOID`  |  控制对象id  |  [TDBOID](Base-Attribute-Type.md#tdboid)   | 根据关联的被控制测点自动查找填写 |
| `ctrlObjName`  |  控制对象名称  | [String128](Base-Attribute-Type.md#string) |                  |
| `ctrlObjCode`  | 控制对象调度编号 | [String16](Base-Attribute-Type.md#string)  |                  |
| `isDirectCtrl` |   是否直控   |    [Bool](Base-Attribute-Type.md#bool)     |                  |
|   `wfCheck`    |  启用五防闭锁  |    [Bool](Base-Attribute-Type.md#bool)     |                  |
|   `sigCheck`   |  启用信号闭锁  |    [Bool](Base-Attribute-Type.md#bool)     |                  |
|  `logicCheck`  | 启用逻辑规则闭锁 |    [Bool](Base-Attribute-Type.md#bool)     |                  |
|   `topCheck`   |  启用拓扑闭锁  |    [Bool](Base-Attribute-Type.md#bool)     |                  |

</tab>
<tab title="同步分区">

| **属性**  | **中文名** |                 **类型**                  | **说明** |
|:-------:|:-------:|:---------------------------------------:|:------:|
| `stage` |  控制阶段   | [**CtrlStage**](Enum-Type.md#ctrlstage) |        |

</tab>
<tab title="索引分区">

|            **属性**            |                    **中文名**                    |                              **类型**                               |   **说明**   |
|:----------------------------:|:---------------------------------------------:|:-----------------------------------------------------------------:|:----------:|
|     `MemberOfSubstation`     | 所属的[**Substation**](Core-Model.md#substation) | [**SymbSeqArraySlave**](Base-Attribute-Type.md#symbseqarrayslave) |            |
|          `RefMeas`           |                     关联的测点                     |         [**SingleRef**](Base-Attribute-Type.md#singleref)         | 可关联状态量、模拟量 |
|        `RefFeYKClose`        |                  关联的前置遥控点(合)                  |          [**CrossRef**](Base-Attribute-Type.md#crossref)          |            |
|        `RefFeYKOpen`         |                  关联的前置遥控点(分)                  |          [**CrossRef**](Base-Attribute-Type.md#crossref)          |            |
|          `RefFeYT`           |                   关联的前置遥调点                    |          [**CrossRef**](Base-Attribute-Type.md#crossref)          |            |
|         `RefFeYKTQ`          |                 关联的前置遥控点(检同期)                 |          [**CrossRef**](Base-Attribute-Type.md#crossref)          |            |
|         `RefFeYKWY`          |                 关联的前置遥控点(检无压)                 |          [**CrossRef**](Base-Attribute-Type.md#crossref)          |            |
| `RefYKCloseMultiSrcSelector` |               关联的前置遥控点(合)多源选择器                |         [**SingleRef**](Base-Attribute-Type.md#singleref)         |            |
| `RefYKOpenMultiSrcSelector`  |               关联的前置遥控点(分)多源选择器                |         [**SingleRef**](Base-Attribute-Type.md#singleref)         |            |
|   `RefYTMultiSrcSelector`    |                 关联的前置遥调多源选择器                  |         [**SingleRef**](Base-Attribute-Type.md#singleref)         |            |

</tab>

</tabs>



防误模型待补充 。。。
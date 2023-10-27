# 自定义枚举

SCADA定义的枚举类型如下：

#### ServiceStatus

设备投运状态

| 一级枚举             | 备注  |
|------------------|-----|
| `NOT_IN_SERVICE` | 未投运 |
| `IN_SERVICE`     | 已投运 |
| `RETIRED`        | 退役  |

#### FacType

厂站类型

| 一级枚举    | 二级枚举      | 备注        |
|---------|-----------|-----------|
| `STN`   | `STN`     | 常规电站/变电站  |
| `STN`   | `JK`      | 常规电站/集控站  |
| `GREEN` | `WIND`    | 新能源站/风电场  |
| `GREEN` | `SOLAR`   | 新能源站/光伏电站 |
| `GREEN` | `ESS`     | 新能源站/储能电站 |
| `GREEN` | `MG`      | 新能源站/多源电站 |
| `PLANT` | `COAL`    | 发电厂/火电厂   |
| `PLANT` | `HYD`     | 发电厂/水电站   |
| `PLANT` | `NUCLEAR` | 发电厂/核电站   |
| `SP`    | `VIRTUAL` | 特殊/虚厂站    |
| `SP`    | `GPS`     | 特殊/天文钟    |

#### BayType

间隔类型

| 一级枚举       | 备注     |
|------------|--------|
| `VIRTUAL`  | 虚拟间隔   |
| `ACLINE`   | 线路间隔   |
| `TRANS`    | 变压器间隔  |
| `XF`       | 变压器卷间隔 |
| `LOAD`     | 负荷间隔   |
| `BUS`      | 母线间隔   |
| `BUS_CONN` | 母联间隔   |
| `BYPASS`   | 旁路间隔   |
| `BRK`      | 开关间隔   |

#### BayStatus

间隔运行状态

| 一级枚举     | 二级枚举               | 备注       |
|----------|--------------------|----------|
| `RUN`    | `RUN`              | 运行/运行    |
| `RUN`    | `RING`             | 运行/合环    |
| `RUN`    | `CHARGING`         | 运行/充电    |
| `RUN`    | `RUN_ONE`          | 运行/接正母运行 |
| `RUN`    | `RUN_TWO`          | 运行/接副母运行 |
| `RUN`    | `RUN_ONE_CHARGING` | 运行/接正母充电 |
| `RUN`    | `RUN_TWO_CHARING`  | 运行/接副母充电 |
| `HOT`    | `HOT`              | 热备/热备    |
| `HOT`    | `HOT_ONE`          | 热备/接正母热备 |
| `HOT`    | `HOT_TWO`          | 热备/接副母热备 |
| `COLD`   | `COLD`             | 冷备/冷备    |
| `COLD`   | `COLD_ONE`         | 冷备/接正母冷备 |
| `COLD`   | `COLD_TWO`         | 冷备/接副母冷备 |
| `REPAIR` | `REPAIR`           | 检修/检修    |

#### PriEquipmentType

普通一次设备分类

| 一级枚举       | 备注    |
|------------|-------|
| `GROUND`   | 大地    |
| `PT`       | 电压互感器 |
| `CT`       | 电流互感器 |
| `ARRESTER` | 避雷器   |
| `ARC`      | 消弧线圈  |

#### PowerTransformerEndType

变压器绕组类型

| 一级枚举   | 备注    |
|--------|-------|
| `HIGH` | 高压侧绕组 |
| `MID`  | 中压侧绕组 |
| `LOW`  | 低压侧绕组 |

#### BusType

母线类型

| 一级枚举        | 备注 |
|-------------|----|
| `PRIMARY`   | 主母 |
| `SECONDARY` | 副母 |
| `BACKUP`    | 旁母 |

#### BusSecType

母线分段类型

| 一级枚举         | 备注  |
|--------------|-----|
| `NO_SECTION` | 不分段 |
| `SECTION_I`  | I段  |
| `SECTION_II` | II段 |

#### DisconnectorType

隔离刀闸类型

| 一级枚举     | 备注   |
|----------|------|
| `COMM`   | 普通刀闸 |
| `CART`   | 小车   |
| `BYPASS` | 旁路刀闸 |
| `GROUND` | 接地刀闸 |

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

#### BreakerType

开关类型

| 一级枚举       | 备注         |
|------------|------------|
| `COMM`     | 普通开关       |
| `BUS_CONN` | 母联开关       |
| `BYPASS`   | 旁路开关       |
| `MID`      | 中开关(3/2接线) |
| `SIDE`     | 边开关(3/2接线) |

#### LoadType

负荷类型

| 一级枚举    | 备注   |
|---------|------|
| `NORM`  | 普通负荷 |
| `GTRAN` | 接地变  |
| `FTRAN` | 站用变  |

#### IEDType

二次设备类型

| 一级枚举      | 二级枚举          | 备注            |
|-----------|---------------|---------------|
| `PROT`    | `NORM`        | 保护装置/普通保护     |
| `PROT`    | `LINE`        | 保护装置/线路保护     |
| `PROT`    | `BUS`         | 保护装置/母线保护     |
| `PROT`    | `SC`          | 保护装置/高抗保护     |
| `PROT`    | `TRAN`        | 保护装置/主变保护     |
| `PROT`    | `BUS_CONN`    | 保护装置/母联保护     |
| `PROT`    | `LINE_MC`     | 保护装置/线路保测一体   |
| `PROT`    | `BUS_CONN_MC` | 保护装置/分段保测一体   |
| `PROT`    | `ZYB`         | 保护装置/站用变保护    |
| `PROT`    | `CP`          | 保护装置/电容器保护    |
| `PROT`    | `SP`          | 保护装置/电抗器保护    |
| `MC`      | `NORM`        | 测控装置/普通测控     |
| `MC`      | `FUNC`        | 测控装置/多功能测控    |
| `MC`      | `XB`          | 测控装置/箱变测控     |
| `GATEWAY` | `NORM`        | 网关机/普通网关机     |
| `GATEWAY` | `REALTIME`    | 网关机/实时网关机     |
| `GATEWAY` | `SERVICE`     | 网关机/服务网关机     |
| `MONITOR` | `NORM`        | 监控主机/普通主机     |
| `MONITOR` | `MONITOR`     | 监控主机/监控主机     |
| `MONITOR` | `APPLICATON`  | 监控主机/综合应用主机   |
| `SECU`    | `NORM`        | 安自装置/普通设备     |
| `SECU`    | `FAULT`       | 安自装置/故障解列装置   |
| `SECU`    | `DPDY`        | 安自装置/低频低压减载装置 |
| `SECU`    | `FAULT`       | 储能装置/机组控制器    |
| `SECU`    | `DPDY`        | 储能装置/协调控制器    |
| `OTHER`   | `NORM`        | 其他/普通设备       |
| `OTHER`   | `ROUTER`      | 其他/路由器        |
| `OTHER`   | `WAVE`        | 其他/故障录波       |
| `OTHER`   | `JZJL`        | 其他/集中计量装置     |
| `OTHER`   | `JSJL`        | 其他/结算记录装置     |
| `OTHER`   | `ACDC`        | 其他/交直流电压      |

#### AnalogType

模拟量类型

| 一级枚举        | 二级枚举                   | 备注             |
|-------------|------------------------|----------------|
| `PRIMARY`   | `NORM`                 | 一次设备/普通遥测      |
| `PRIMARY`   | `P`                    | 一次设备/有功        |
| `PRIMARY`   | `Q`                    | 一次设备/无功        |
| `PRIMARY`   | `IA`                   | 一次设备/A相电流      |
| `PRIMARY`   | `IB`                   | 一次设备/B相电流      |
| `PRIMARY`   | `IC`                   | 一次设备/C相电流      |
| `PRIMARY`   | `I0`                   | 一次设备/零序电流      |
| `PRIMARY`   | `UA`                   | 一次设备/A相电压      |
| `PRIMARY`   | `UB`                   | 一次设备/B相电压      |
| `PRIMARY`   | `UC`                   | 一次设备/C相电压      |
| `PRIMARY`   | `UAB`                  | 一次设备/AB相电压     |
| `PRIMARY`   | `UBC`                  | 一次设备/BC相电压     |
| `PRIMARY`   | `UCA`                  | 一次设备/CA相电压     |
| `PRIMARY`   | `U0`                   | 一次设备/零序电压      |
| `PRIMARY`   | `ANG`                  | 一次设备/电压相角      |
| `PRIMARY`   | `TAP`                  | 一次设备/变压器档位     |
| `PRIMARY`   | `COS`                  | 一次设备/功率因数      |
| `PRIMARY`   | `F`                    | 一次设备/电网频率      |
| `PRIMARY`   | `TEMP`                 | 一次设备/油温        |
| `SECONDARY` | `NORM`                 | 二次设备/普通遥测      |
| `SECONDARY` | `CPU_LOAD`             | 二次设备/CPU负载率    |
| `SECONDARY` | `MEM_USAGE`            | 二次设备/内存使用率     |
| `SECONDARY` | `DISK_USAGE`           | 二次设备/磁盘使用率     |
| `SECONDARY` | `TEMP`                 | 二次设备/装置内部温度    |
| `SECONDARY` | `LIGHT_POWER`          | 二次设备/光功率       |
| `SECONDARY` | `U`                    | 二次设备/工作电压      |
| `ENV`       | `NORM`                 | 辅控动环/普通遥测      |
| `ENV`       | `SF6`                  | 辅控动环/SF6浓度     |
| `ENV`       | `O2`                   | 辅控动环/氧气浓度      |
| `ENV`       | `H2O`                  | 辅控动环/水位        |
| `ENV`       | `COND_TEMP`            | 辅控动环/空调温度      |
| `ENV`       | `COND_MODE`            | 辅控动环/空调模式      |
| `ENV`       | `COND_WD`              | 辅控动环/空调风速      |
| `ENV`       | `U0`                   | 辅控动环/零序电压      |
| `MONI`      | `NORM`                 | 辅控在线监测/普通遥测    |
| `MONI`      | `C2H2`                 | 辅控在线监测/乙炔      |
| `MONI`      | `C2H4`                 | 辅控在线监测/乙烯      |
| `MONI`      | `C2H6`                 | 辅控在线监测/甲烷      |
| `MONI`      | `CO`                   | 辅控在线监测/一氧化碳    |
| `MONI`      | `H2`                   | 辅控在线监测/氢气      |
| `MONI`      | `N2`                   | 辅控在线监测/氮气      |
| `MONI`      | `O2`                   | 辅控在线监测/氧气      |
| `MONI`      | `H2O`                  | 辅控在线监测/水分      |
| `MONI`      | `HYD`                  | 辅控在线监测/总烃      |
| `MONI`      | `PDMIN`                | 辅控在线监测/局部最小放电量 |
| `MONI`      | `PDMAX`                | 辅控在线监测/局部最大放电量 |
| `MONI`      | `PDCOUNT`              | 辅控在线监测/放电次数    |
| `MONI`      | `LOSS`                 | 辅控在线监测/介质损耗因数  |
| `MONI`      | `CAPA`                 | 辅控在线监测/电容量     |
| `MONI`      | `CORE`                 | 辅控在线监测/铁芯接地电流  |
| `MONI`      | `CLAMP`                | 辅控在线监测/夹件接地电流  |
| `MONI`      | `PRESSURE`             | 辅控在线监测/压力      |
| `MONI`      | `TEMP`                 | 辅控在线监测/温度      |
| `SECU`      | `NORM`                 | 辅控安防/普通遥测      |
| `SECU`      | `LOCK`                 | 辅控安防/锁控遥测      |
| `FIRE`      | `NORM`                 | 辅控消防/普通遥测      |
| `ESS`       | `CHARGE_PMAX`          | 储能系统/可供最大充电功率  |
| `ESS`       | `DISCHARGE_PMAX`       | 储能系统/可供最大放电功率  |
| `ESS`       | `SOC`                  | 储能系统/SOC       |
| `ESS`       | `SOC`                  | 储能系统/SOH       |
| `ESS`       | `AVA_CHARGE`           | 储能系统/可充电电量     |
| `ESS`       | `AVA_DISCHARGE`        | 储能系统/可放电电量     |
| `ESS`       | `DAY_CHARGE`           | 储能系统/日充电电量     |
| `ESS`       | `DAY_DISCHARGE`        | 储能系统/日放电电量     |
| `ESS`       | `TOTAL_CHARGE`         | 储能系统/累计充电电量    |
| `ESS`       | `TOTAL_CHARGE_LOW`     | 储能系统/累计充电电量低位  |
| `ESS`       | `TOTAL_CHARGE_HIGH`    | 储能系统/累计充电电量高位  |
| `ESS`       | `TOTAL_DISCHARGE`      | 储能系统/累计放电电量    |
| `ESS`       | `TOTAL_DISCHARGE_LOW`  | 储能系统/累计放电电量低位  |
| `ESS`       | `TOTAL_DISCHARGE_HIGH` | 储能系统/累计放电电量高位  |
| `ESS`       | `TOTAL_CHARGE_TIME`    | 储能系统/累计充电时间    |
| `ESS`       | `TOTAL_DISCHARGE_TIME` | 储能系统/累计放电时间    |
| `ESS`       | `P_COMMAND`            | 储能系统/有功指令值     |
| `ESS`       | `Q_COMMAND`            | 储能系统/无功指令值     |
| `ESS`       | `CONV_EFF`             | 储能系统/交直流转换效率   |
| `ESS`       | `BCMU_UMAX`            | 储能系统/交直流转换效率   |

#### StatusType

状态量类型

| 一级枚举        | 二级枚举                | 备注           |
|-------------|---------------------|--------------|
| `PRIMARY`   | `NORM`              | 一次设备/普通遥信    |
| `PRIMARY`   | `OPEN_CLOSE`        | 一次设备/双位置     |
| `PRIMARY`   | `CLOSE`             | 一次设备/合位      |
| `PRIMARY`   | `OPEN`              | 一次设备/分位      |
| `PRIMARY`   | `CLOSE_A`           | 一次设备/A相合位    |
| `PRIMARY`   | `CLOSE_B`           | 一次设备/B相合位    |
| `PRIMARY`   | `CLOSE_C`           | 一次设备/C相合位    |
| `PRIMARY`   | `OPEN_A`            | 一次设备/A相分位    |
| `PRIMARY`   | `OPEN_B`            | 一次设备/B相分位    |
| `PRIMARY`   | `OPEN_C`            | 一次设备/C相分位    |
| `SECONDARY` | `NORM`              | 二次设备/普通遥信    |
| `SECONDARY` | `COMM`              | 二次设备/通讯状态    |
| `SECONDARY` | `WARN`              | 二次设备/异常告警    |
| `SECONDARY` | `CHECK`             | 二次设备/装置自检    |
| `SECONDARY` | `TS_SIG`            | 二次设备/对时信号状态  |
| `SECONDARY` | `TS_SVR`            | 二次设备/对时服务状态  |
| `SECONDARY` | `TS_JUMP`           | 二次设备/时间跳变    |
| `SECONDARY` | `DUTY`              | 二次设备/主备机状态   |
| `SECONDARY` | `FAULT_ACT`         | 二次设备/保护动作    |
| `SECONDARY` | `YB`                | 二次设备/压板      |
| `AUXI`      | `NORM`              | 辅控/普通遥信      |
| `AUXI`      | `RUN`               | 辅控/运行状态      |
| `AUXI`      | `ALARM`             | 辅控/告警状态      |
| `AUXI`      | `COMM`              | 辅控/通讯状态      |
| `AUXI`      | `FAULT`             | 辅控/故障状态      |
| `AUXI`      | `SYNC`              | 辅控/对时状态      |
| `AUXI`      | `DEFEND`            | 辅控/布防状态      |
| `AUXI`      | `DOOR`              | 辅控/门状态       |
| `AUXI`      | `PUMP`              | 辅控/水泵运行工况    |
| `AUXI`      | `COND_MODE`         | 辅控/空调运行模式    |
| `AUXI`      | `COND_WD`           | 辅控/空调风速      |
| `AUXI`      | `FIRE`              | 辅控/火警信号      |
| `AUXI`      | `INVADE`            | 辅控/入侵信号      |
| `AUXI`      | `PRESSURE`          | 辅控/压力异常      |
| `AUXI`      | `LK_DEV`            | 辅控/锁控设备配置更新  |
| `AUXI`      | `LK_ZONE`           | 辅控/锁控区域配置更新  |
| `AUXI`      | `LK_MON`            | 辅控/锁控监测信息更新  |
| `AUXI`      | `LK_ALM`            | 辅控/锁控报警信息更新  |
| `AUXI`      | `LK_TIP`            | 辅控/锁控提示信息更新  |
| `AUXI`      | `MONI_FILE`         | 辅控/在线监测文件更新  |
| `ESS`       | `NORM`              | 储能系统/普通遥信    |
| `ESS`       | `WARN`              | 储能系统/异常告警    |
| `ESS`       | `FAULT_ACT`         | 储能系统/保护动作    |
| `ESS`       | `DEV_STOP`          | 储能系统/停机状态    |
| `ESS`       | `DEV_WAIT`          | 储能系统/待机状态    |
| `ESS`       | `DEV_RUN`           | 储能系统/运行状态    |
| `ESS`       | `DEV_LOCAL`         | 储能系统/就地状态    |
| `ESS`       | `DEV_REMOTE_TYPE`   | 储能系统/远方类型    |
| `ESS`       | `DEV_DISCHARGE`     | 储能系统/放电状态    |
| `ESS`       | `DEV_CHARGE`        | 储能系统/充电状态    |
| `ESS`       | `DEV_ALARM`         | 储能系统/告警总     |
| `ESS`       | `DEV_FAULT`         | 储能系统/故障总     |
| `ESS`       | `DEV_SELF_ALARM`    | 储能系统/自诊断告警   |
| `ESS`       | `DEV_SELF_ALARM_L1` | 储能系统/自诊断轻微故障 |
| `ESS`       | `DEV_SELF_ALARM_L2` | 储能系统/自诊断一般故障 |
| `ESS`       | `DEV_SELF_ALARM_L3` | 储能系统/自诊断严重故障 |

#### RegionType

站内区域类型

| 一级枚举            | 备注    |
|-----------------|-------|
| `COMM`          | 普通区域  |
| `BUILDING`      | 建筑    |
| `FLOOR`         | 楼层    |
| `ROOM`          | 房间    |
| `SWITCH_AREA`   | 开关场所  |
| `BAY_AREA`      | 间隔场所  |
| `ROAD`          | 道路    |
| `DITCH`         | 电缆沟   |
| `DOOR`          | 门     |
| `WALL`          | 围墙    |
| `PRE_CABINET`   | 预制舱   |
| `CABINET`       | 屏柜    |
| `ESS_CONTAINER` | 储能集装箱 |

#### AuxiliaryEquipmentType

辅控设备类型

| 一级枚举   | 二级枚举         | 备注                   |
|--------|--------------|----------------------|
| `MONI` | `NORM`       | 在线监测/普通设备            |
| `MONI` | `YSP`        | 在线监测/油中溶解气体在线监测单元    |
| `MONI` | `JF`         | 在线监测/局放在线监测传感器       |
| `MONI` | `BYQTG`      | 在线监测/变压器套管在线监测传感器    |
| `MONI` | `TXJJ`       | 在线监测/铁芯夹件接地电流在线监测传感器 |
| `MONI` | `BLQ`        | 在线监测/避雷器在线监测传感器      |
| `MONI` | `RXSB`       | 在线监测/容性设备在线监测传感器     |
| `MONI` | `BRK_SF6`    | 在线监测/断路器SF6气体监测传感器   |
| `MONI` | `BRK_JX`     | 在线监测/断路器机械特性监测传感器    |
| `SECU` | `NORM`       | 安防/普通设备              |
| `SECU` | `DZWL`       | 安防/电子围栏              |
| `SECU` | `HWDS`       | 安防/红外对射              |
| `SECU` | `HWSJ`       | 安防/红外双鉴              |
| `SECU` | `DZWL_ZD`    | 安防/电子围栏终端            |
| `SECU` | `SECU_ZD`    | 安防/安防监控终端            |
| `SECU` | `DOOR_ZD`    | 安防/门禁监控终端            |
| `SECU` | `ELEC_KEY`   | 安防/电子钥匙              |
| `SECU` | `LOCK_ZD`    | 安防/锁控监控终端            |
| `ENV`  | `NORM`       | 动环/普通设备              |
| `ENV`  | `WEATHER`    | 动环/微气象传感器            |
| `ENV`  | `TEMP_HUM`   | 动环/温湿度传感器            |
| `ENV`  | `TEMP`       | 动环/温度传感器             |
| `ENV`  | `HUM`        | 动环/湿度传感器             |
| `ENV`  | `O2`         | 动环/氧气传感器             |
| `ENV`  | `H2O_LEAK`   | 动环/漏水传感器             |
| `ENV`  | `H2O_LEVEL`  | 动环/水位传感器             |
| `ENV`  | `SF6`        | 动环/SF6传感器            |
| `ENV`  | `POSTURE`    | 动环/姿势传感器             |
| `ENV`  | `PUMP`       | 动环/水泵                |
| `ENV`  | `WIND`       | 动环/风机                |
| `ENV`  | `COND`       | 动环/空调                |
| `ENV`  | `DEHUM`      | 动环/除湿机               |
| `ENV`  | `LIGHT_CTRL` | 动环/照明控制器             |
| `ENV`  | `ENV_ZD`     | 动环/动环监测终端            |
| `FIRE` | `YLF`        | 消防/雨淋阀               |
| `FIRE` | `PYZD`       | 消防/排油注氮              |
| `FIRE` | `XSW`        | 消防/细水雾灭火设备           |
| `FIRE` | `FIRE_ALARM` | 消防/火灾自动报警系统          |
| `FIRE` | `YG`         | 消防/烟感探测器             |
| `FIRE` | `WG`         | 消防/温感探测器             |

#### GuardMode

控制监护模式

| 一级枚举           | 备注   |
|----------------|------|
| `NO_LOGIN`     | 无登录  |
| `NO_GUARD`     | 无监护  |
| `LOCAL_GUARD`  | 本机监护 |
| `REMOTE_GUARD` | 异机监护 |

#### MultiSrcType

多源类型

| 一级枚举 | 备注 |
|------|----|
| `YX` | 遥信 |
| `YC` | 遥测 |
| `YM` | 遥脉 |
| `YK` | 遥控 |
| `YT` | 遥调 |

#### SrcSelectMode

多源选择模式

| 一级枚举           | 备注   |
|----------------|------|
| `ONLINE_FIRST` | 在线优先 |
| `DUTY_FIRST`   | 值班优先 |
| `MANUAL`       | 人工选择 |

#### CompositeSwitchType

组合刀闸类型

| 一级枚举   | 备注   |
|--------|------|
| `CART` | 手车   |
| `TRI`  | 三态刀闸 |
# 自定义Bit位

SCADA扩展的位域如下：

#### CheckMode

控制校核模式

| 名称          | 别名   |
|-------------|------|
| NO_CHECK    | 不校核  |
| WF_CHECK    | 五防校核 |
| SIG_CHECK   | 信号校核 |
| LOGIC_CHECK | 逻辑校核 |
| TOP_CHECK   | 拓扑校核 |

#### MoniStatus

监盘状态

| 名称            | 别名   |
|---------------|------|
| NORMAL        | 正常   |
| TAG           | 挂牌   |
| SUPPRESS      | 抑制告警 |
| BLOCK         | 封锁   |
| NO_CTRL       | 禁止控制 |
| NO_CTRL_CLOSE | 禁止控合 |
| NO_CTRL_OPEN  | 禁止控分 |
| ENSURING      | 保电中  |
| REPAIRING     | 检修中  |    
| TRANSMISSION  | 传动中  |
| TESTING       | 测试中  |
| DEFECT        | 有缺陷  |

#### RunningStatus

设备运行状态

| 名称          | 别名      |
|-------------|---------|
| QUIT        | 停电      |
| CHARGING    | 充电      |
| RUN         | 运行      |
| ABNORMAL    | 异常      |
| ACCIDENT    | 故障      |
| HEAVY_LOAD  | 重载      |
| OVER_LOAD   | 过载      |
| CONTROLLING | 控制中     |
| GROUNDED    | 接地      |
| BYPASS      | 旁路代     |
| OPPO        | 对端代     |    
| UNP         | 有功不平衡   |
| UNQ         | 无功不平衡   |
| UNV         | 线电压不平衡  |
| UNPV        | 相电压不平衡  |    
| UNBV        | 并列电压不平衡 |
| UNPQI       | PQI不匹配  |
| UNSA        | 遥信遥测不匹配 |
| TPINCON     | 三相位置不一致 |

#### Position

设备开合状态

| 名称           | 别名     |
|--------------|--------|
| OPEN         | 分位     |
| CLOSE        | 合位     |
| INVALID      | 是否无效   |
| LAST_OPEN    | 上次分位   |
| LAST_CLOSE   | 上次合位   |
| LAST_INVALID | 上次是否无效 |

#### FeMeasQuality

前置测点质量位

| 名称               | 别名    |
|------------------|-------|
| GOOD             | 良好    |
| INVALID          | 无效    |
| QUESTIONABLE     | 可疑    |
| OVER_FLOW        | 溢出    |
| OUT_OF_RANGE     | 超过量程  |
| BAD_REFERENCE    | 基准值错误 |
| OSCILLATORY      | 抖动    |
| FAILURE          | 故障    |
| OLD_DATA         | 老数据   |    
| INCONSISTENT     | 不一致   |
| INACCURATE       | 精度不足  |
| SOURCE           | 是否替代  |
| TEST             | 测试    |    
| OPERATOR_BLOCKED | 闭锁刷新  |

#### TopColor

拓扑信息

| 名称             | 别名     |
|----------------|--------|
| TRACED         | 已搜索    |
| LAST_ENERGIZED | 上次是否带电 |
| ENERGIZED      | 是否带电   |
| GROUNDED       | 接地     |
| TAG_GROUNDED   | 挂牌接地   |
| IS_DC          | 直流拓扑点  |
| MAIN_ISLAND    | 主岛     |
| ISLAND2        | 岛2     |
| ISLAND3        | 岛3     |
| ISLAND4        | 岛4     |    
| OTHER_ISLAND   | 其他岛    |

#### MeasQuality

测点质量位

| 名称          | 别名    | 说明             |
|-------------|-------|----------------|
| UN_INIT     | 未初始化  | 前置未上送过数据       |
| ACQ_ERR     | 采集中断  | 前置通讯中断         |
| SUSPICIOUS  | 可疑数据  |                |
| OLD_DATA    | 数据不刷新 | 在定义的周期内未收到前置数据 |
| BYPASS      | 旁路代   |                |
| OPPO        | 对端代   |                |    
| CONTROLLING | 控制中   |                |
| UNREASON    | 越合理限值 |                |
| CONSTANT    | 数据不变  |                |
| OVER_LIMIT  | 越监视限值 |                |
| OVER_L1     | 越下限   |                |
| OVER_L2     | 越下下限  |                |
| OVER_L3     | 越下下下限 |                |
| OVER_H1     | 越上限   |                |
| OVER_H2     | 越上上限  |                |
| OVER_H3     | 越上上上限 |                |

#### AlmContentCfg

告警内容组成方式

| 名称        | 别名    | 说明            |
|-----------|-------|---------------|
| AREA      | 地区    | 是否拼接地区名称，下面类似 |
| SUB       | 厂站    |               |
| VOL       | 电压等级  |               |
| BAY       | 间隔    |               |
| IED       | IED   |               |
| EQUIP     | 一次设备  |               |    
| AUX_SYS   | 辅控系统  |               |
| AUX_AREA  | 辅控区域  |               |
| AUX_EQUIP | 辅控设备  |               |
| ESS_UNIT  | 储能单元  |               |
| ESS_PCS   | 储能逆变器 |               |
| ESS_BCMU  | 储能电池簇 |               |
| MEAS_TYPE | 测点类型  |               |

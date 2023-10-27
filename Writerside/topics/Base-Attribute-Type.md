# 平台自带类型


数据库原生支持的属性类型如下：

### 基本数据类型
#### Bool
布尔类型

#### Byte
1字节带符号整数

#### Octet
1字节无符号整数

#### Short
2字节带符号整数

#### UShort
2字节无符号整数

#### Long
4字节带符号整数

#### ULong
4字节无符号整数

#### LongLong
8字节带符号整数

#### ULongLong
8字节无符号整数

#### String
字符串(utf-8编码)

#### Time
精确到毫秒的时间戳

#### RTime
两个Time时间戳的差，单位毫秒

#### STime
精确到秒的时间戳

#### RSTime
两个STime时间戳的差，单位秒

#### Date
日期

#### Float
单精度浮点数

#### Double
双精度浮点数

#### TDBOID
对象ID

### 关联关系类型
#### SingleRef
单向引用

#### CrossRef
跨库单向引用

#### InterRefMaster
双向引用父端

#### InterRefSlave
双向引用子端

#### SymbSeqArrayMaster
共生数组父端

#### SymbSeqArraySlave
共生数组子端

#### SymbSeqDlistMaster
共生连续链表父端

#### SymbSeqDlistSlave
共生连续链表子端

#### ASymbSeqDlistMaster
非共生连续链表父端

#### ASymbSeqDlistSlave
非共生连续链表子端

#### SymbDisDlistMaster
共生离散链表父端

#### SymbDisDlistSlave
共生离散链表子端

#### ASymbInlineDlistMaster
非共生内联链表父端

#### ASymbInlineDistSlave
非共生内联链表子端

#### SymbCycSlave
共生循环嵌套
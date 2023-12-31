# 数据库字段类型


[//]: # (<format style="subscript" color="Red">Hello, world!</format>)

## 原生支持的字段类型

> 数据库原生支持的字段类型分为**基本数据类型**、**关联关系类型**。
>
> 基本数据类型包括数值型、字符串型、日期时间型等；
>
> 关联关系类型表征了对象与对象之间的引用关系，分类比较复杂；
> 
{style="note"}

### 基本数据类型
#### Bool
布尔类型

#### Byte
1字节带符号整数，对应`int8_t`。

#### Octet
1字节无符号整数，对应`uint8_t`。

#### Short
2字节带符号整数，对应`int16_t`。

#### UShort
2字节无符号整数，对应`uint16_t`。

#### Long
4字节带符号整数，对应`int32_t`。

#### ULong
4字节无符号整数，对应`uint32_t`。

#### LongLong
8字节带符号整数，对应`int64_t`。

#### ULongLong
8字节无符号整数，对应`uint64_t`。

#### String
字符串类型，需明确指定长度，默认采用UTF-8编码存储。

#### Time
精确到毫秒的时间戳

#### RTime
两个Time时间戳的差，单位毫秒

#### STime
精确到秒的时间戳

#### RSTime
两个STime时间戳的差，单位秒

#### Date
日期，实际是忽略时分秒的时间戳

#### Float
单精度浮点数，对应`float`。

#### Double
双精度浮点数，对应`double`。

#### TDBOID
对象ID，可转换为[ULongLong](#ulonglong)。

### 关联关系类型

关联关系中引入了“共生/非共生”的概念，解释如下：

共生关系不是平等关系，会有一方为父端，一方为子端，在父端对象被删除时，与之关联的子端对象必须删除，反之，子端对象不允许脱离父端对象而存在。
以厂站-电压等级为例，厂站与电压等级之间即为共生关系，其中厂站为父端，电压等级为子端。

共生关系会产生如下约束：
> 在新建子端对象时，必须指定其父端对象；
> 
> 删除父端对象时，其下辖的子端对象会自动删除；
> 
> {style="note"}

非共生关系不存在上述约束，可以先建立对象，再进行关联关系的设置；删除对象时也不会自动删除非共生关系的子对象。

#### SingleRef
单向引用

1对1关联，其关联关系只记录在引用者上，被引用者上不记录

#### CrossRef
跨库单向引用

与SingleRef的区别是允许引用者、被引用者不属于同一个数据库

#### InterRefMaster
双向引用父端

1对1关联，其关联关系在引用者与被引用者上都会记录

#### InterRefSlave
双向引用子端

1对1关联，其关联关系在引用者与被引用者上都会记录

#### SymbSeqArrayMaster
共生数组父端

1对N共生关联

#### SymbSeqArraySlave
共生数组子端

1对N共生关联，子端对象以数组形式连续存放

#### SymbSeqDlistMaster
共生连续链表父端

1对N共生关联

#### SymbSeqDlistSlave
共生连续链表子端

1对N共生关联，子端对象以链表形式非连续存放

#### ASymbSeqDlistMaster
非共生连续链表父端

1对N非共生关联

#### ASymbSeqDlistSlave
非共生连续链表子端

1对N非共生关联，子端对象以链表形式非连续存放

#### SymbDisDlistMaster
共生离散链表父端

#### SymbDisDlistSlave
共生离散链表子端

#### ASymbInlineDlistMaster
非共生内联链表父端

用于单表自嵌套关联

#### ASymbInlineDlistSlave
非共生内联链表子端

用于单表自嵌套关联

#### SymbCycMaster
共生循环子表父端

#### SymbCycSlave
共生循环子表

用于循环子表

#### M2NMaster
多对多关联父端

用于描述m:n关联

#### M2NSlave
多对多关联子端

用于描述m:n关联

## 支持自定义扩展的字段类型

### 自定义位串

数据库提供长度为8/16/32位的自定义位串，如下图所示：

![自定义位串截图](selfbit.png){border-effect="line"}


### 自定义结构体

数据库提供自定义结构体的手段，结构体的字段必须是基本数据类型，如下图所示：

![自定义结构截图](selfstruct.png){border-effect="line"}

---
title: MySQL 字段选择建议
date: 2017-03-02 17:42:52
tags:
- MySQL
- 数据库
---
## 前言
数据库设计一个比较重要的部分就是数据库字段的选择，MySQL 提供了 Numberic（数字）, Date and Time（日期和时间）, String（字符串），同时也提供了相关扩展，用户也可以自定义字段类型。如何选择一个合适的字段类型是很重要的，字段选择的不合适，不仅会浪费数据库存储空间，也会影响到后期数据库的拓展和优化。记录少的时候这些影响你可能觉察不到，当只要记录达到一定数量级，那些隐藏在代深处的弊端就会显现出来，到时候追悔莫及。

同样都是 MySQL，可以用来构建 facebook、淘宝这样熟十亿级大项目，同时，也有可能一个几万 pv 的小站跑起来都很吃力。虽然影响因素很多，但不可否认的是，数据库结构设计和字段设计也是其中一个比较重要的原因。下面，就常见的使用场景，来说明下如何选择数据库字段。

## 几种字段类型
关于
## Numberic
|Type|    Storage | Minimum Value|   Maximum Value |
 |   | (Bytes) |(Signed/Unsigned) |  (Signed/Unsigned)|
 | :---: | :---: | :---: | :---: |

|TINYINT |1|   -128 |   127|
|      | |0  |255|
|SMALLINT |   2 |  -32768 | 32767|
 |       || 0  | 65535|
|MEDIUMINT   3   -8388608    8388607
 |       || 0   |16777215|
|INT |4 |  -2147483648 |2147483647|
|    |  |0  | 4294967295|
|BIGINT|  8  | -9223372036854775808|    9223372036854775807|
  |    |  |0   |18446744073709551615|

上表列出了常见整数类型占用的字节大小和所能表示的最大/最小值




### 
## 选择合适的字段类型
1. 订单使用纯数字，类型单独是一个字段
2. IP 地址
3. 时间
4. 金钱，一般，double，要求精确 bigint
5. 文章
6. 
## 总结
看了上面那些字段类型的特点以及存储需求，总结这么几点字段选择原则：
1. 常见字段的选择和
2. 贪婪原则，选择最能满足当前需求的字段
3. 根据实际项目需求，是追求精度还是追求速度？
3. 慎重使用 enum


## 参考
1. [data-types](http://dev.mysql.com/doc/refman/5.5/en/data-types.html)
2. [storage-requirements](http://dev.mysql.com/doc/refman/5.5/en/storage-requirements.html)
    - 贪婪原则, 但也要考虑拓展性
    - 慎重使用 enum [Why enum is evil](http://komlenic.com/244/8-reasons-why-mysqls-enum-data-type-is-evil/)
    需要使用到 enum 的时候选择Tinyint或Char
        * 举例子 zfix_banner 表的 type

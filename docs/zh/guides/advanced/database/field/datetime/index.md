# 概述

### 日期时间字段类型
日期与时间字段可以分为几种类型，具体如下：

- 带时区的日期时间：统一将日期时间转为 UTC 时间，并在必要时调整为对应时区；
- 不带时区的日期时间：存储日期和时间，但不包括时区；
- 日期（不带时间）：仅存储日期部分，忽略时间；
- 时间（不带日期）：只存储时间，日期部分不包含；
- Unix 时间戳：以 Unix 时间戳表示，通常为从1970年1月1日开始的秒数。
示例：各类日期字段类型的不同表现形式：

|字段类型|示例值|描述|
|-------|-----|---|
|日期时间（带时区）	|2025-02-26T11:30:00.000Z|转换为 UTC 时间，存储的日期时间包含时区信息。|
|日期时间（不带时区）|2025-02-26 11:45:14|不带时区信息，仅记录日期和时间。|
|日期（无时间）|2025-08-24|存储日期，不包括时间。|
|时间（无日期）|11:45:14|存储时间，但不记录日期信息。|
|Unix 时间戳|1814437800|记录自 1970 年 1 月 1 日以来的秒数（UTC 时间）。|

### 各数据源对照
灵矶、MySQL和PostgreSQL的对照表格:
|字段类型|灵矶|MySQL|PostgreSQL|
|-------|-------|------|----------|
|日期时间（含时区）|Datetime with timezone|TIMESTAMP DATETIME|TIMESTAMP WITH TIME ZONE|
|日期时间（不含时区）|Datetime without timezone|DATETIME|TIMESTAMP WITHOUT TIME ZONE|
|日期（不含时间）|Date|DATE|DATE|
|时间|Time|TIME|TIME WITHOUT TIME ZONE|
|Unix 时间戳|Unix timestamp|INTEGER BIGINT|INTEGER BIGINT|
|时间（含时区）|-	|-|	TIME WITH TIME ZONE|

**注意：**
**MySQL**的**TIMESTAMP**类型支持的时间范围是从 UTC 时间*1970-01-01 00:00:01*到*2038-01-19 03:14:07*。若超出此时间范围，建议使用**DATETIME**类型或**BIGINT**类型来存储 Unix 时间戳。

### 日期时间存储的处理流程

##### 含时区

包括包括日期时间（不含时区）和 Unix 时间戳
<!--TODO: 添加图片-->

**注意：**
- 为了支持更广泛的数据范围，**灵矶**将日期时间（含时区）字段在 MySQL 中存储为 DATETIME。存储的日期值是基于服务端 TZ 环境变量转换后的值。如果该环境变量发生变化，存储的日期时间值也会相应变化。 
- UTC 时间和本地时间之间有时区差，展示原始 UTC 值可能会导致用户误解。

##### 不含时区
<!--TODO: 添加图片-->

#### UTC
**协调世界时UTC**是全球时间标准，用于统一世界各地的时间。它基于原子钟的高精度计时，并与地球自转的时间同步。

由于 UTC 时间和本地时间之间的时区差异，直接展示 UTC 原始时间可能会引起用户的误解，例如：
|时区|日期时间|
|---|-------|
|UTC|2025-02-26T03:30:00.000Z|
|东八区 (UTC+8)|2025-02-26 11:30:00|
|东五区 (UTC+5)|2025-02-26 08:30:00|
|西五区 (UTC-5)|2025-02-26 01:30:00|
|英国时间 (UTC+0)|2025-02-26 03:30:00|
|中部时间 (UTC-6)|2025-02-25 21:30:00|

该表格展示的都是同一时间。
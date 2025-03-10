# 设置数据范围

## 介绍

关系字段的数据范围设置类似于卡片的数据范围设置，为关系数据设定默认的筛选条件。

## 使用说明

![20240422153711](/field/field-settings/data-scope-1.png)

### 静态值

示例：仅在售商品可以选择关联。

![20240422155953](/field/field-settings/data-scope-2.png)

### 变量值

示例：仅商品生产日期早于上个月的商品可以选择关联。

![20240422163640](/field/field-settings/data-scope-3.png)

更多关于变量内容参考 [变量](../../variable.md)

### 关系字段联动

关系字段之间通过设置数据范围实现联动。

示例：订单表中有多对多关系字段「商品」和多对一关系字段「客户」， 商品表有多对多关系字段 「客户」，在订单表单卡片中，商品的可选数据为当前表单中所选客户关联的商品。

![20240422163640](/field/field-settings/data-scope-4.png)

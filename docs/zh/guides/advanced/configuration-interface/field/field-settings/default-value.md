# 默认值

## 介绍

默认值是字段在新建状态下的初始值。可以在数据表配置字段时为其设定默认值，也可以在新增表单卡片中为字段指定默认值，可以设置为常量或变量。
## 哪些地方可以配置默认值

### 数据表字段

![20240411095933](/field/field-settings/default-value-1.png)

### 新增表单的字段

新增表单的大部分字段都支持设置默认值。

![20240411100030](/field/field-settings/default-value-2.png)

### 子表单的添加

无论是新增或编辑表单里的子表单字段添加的子数据都有默认值。

子表单的 Add new

![20240411100341](/field/field-settings/default-value-3.png)

子表格 Add new

![20240411100424](/field/field-settings/default-value-4.png)

![20240411100634](/field/field-settings/default-value-5.png)

编辑已有的数据，数据为空时也不会被默认值填充，新添加的数据才会用默认值填充，未保存。

![20240411100729](/field/field-settings/default-value-6.png)


### 关系数据的默认值

只有「**多对一**」和「**多对多**」类型的关系，并使用的选择器组件（Select、RecordPicker）时才有默认值。

![20240411101025](/field/field-settings/default-value-7.png)

## 默认值变量

### 有哪些变量

- 日期变量；
- 当前用户；
- 当前记录，已存在的数据才有当前记录的概念；
- 当前表单，理想情况只列出表单里的字段；
- 当前对象，子表单里的概念（子表单里的每一行数据对象）；
- 表单选中记录，目前仅限于 「Table 卡片 + Add Record 表单」组合；

更多关于变量内容参考 [变量](../../variable.md)

### 字段默认值变量

分为非关系字段和关系字段两类。

#### 关系字段默认值变量

- 变量对象必须是 collection 记录；
- 必须是继承链路上的表，可以是当前表，也可以是父子表；
- 「表单选中记录」变量仅限于「多对多」和「一对多/多对一」关系字段里可用；
- **多层级时，需要拍平并去重处理**

```typescript
// 表格选中记录：
[{id:1},{id:2},{id:3},{id:4}]

// 表格选中记录/对一：
[{对一: {id:2}}, {对一: {id:3}}, {对一: {id:3}}] 
// 拍平并去重
[{id: 2}, {id: 3}]

// 表格选中记录/对多：
[{对多: [{id: 1}, {id:2}]}, {对多: {[id:3}, {id:4}]}]
// 拍平  
[{id:1},{id:2},{id:3},{id:4}]
```

#### 非关系默认值变量

- 类型一致或兼容，如字符串兼容数字，和所有有提供 toString 方法的对象；
- JSON 字段比较特殊，什么数据都可以存；

### 字段层级（可选字段）

![20240411101157](/field/field-settings/default-value-8.png)
- 非关系默认值变量

  - 多层级选择字段时，仅限于对一的关系，不支持对多的关系；
  - JSON 字段比较特殊，可以不限制；
- 关系默认值变量

  - hasOne，只支持对一关系；
  - hasMany，对一（内部转换）和对多都可以；
  - belongsToMany，对一（内部转换）和对多都可以；
  - belongsTo，一般为对一，当父级关系为 hasMany 时，也支持对多（因为 hasMany/belongsTo 实质就是多对多关系）；

## 特殊情况说明

### 「多对多」等价于「一对多/多对一」组合

模型
<!-- TODO: tachybase已删除插件 -->

多对多设置默认值变量时，如果变量有多条记录，那选中的数据就有多条，如下图所示：
当表格卡片数据表与关系字段数据表相同时使用。
![20240411103021](/field/field-settings/default-value-10.png)


### 为什么一对一和一对多没有默认值？

例如 A.B 关系，b1 被 a1 关联了，就不能被 a2 关联了，如果 b1 关联 a2，那就会解除与 a1 的关联，这种情况下数据并不是共享的，而默认值是共享的机制（都可以关联），所以一对一和一对多不能设置默认值。

### 为什么多对一和多对多的子表单或子表格也不能有默认值？

因为子表单和子表格的侧重点是直接对关系数据进行编辑（包括新增、移除），而关系默认值是共享机制，都可以关联，但不能修改关系数据。所以这种场景下不适合提供默认值。

另外，子表单或子表格是有子字段的，子表单或子表格的默认值设置的是行默认值还是列默认值会分不清楚。

综合考虑，无论什么关系子表单或子表格都不能直接设置默认值比较合适。

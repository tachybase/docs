# 表达式表

::: info &#9432; 提示
该功能由插件 module-data-source 提供。
:::

#### 创建“表达式表”模板表

在工作流中使用动态表达式运算节点之前，需要先在数据表管理工具中创建一个“表达式”模板表，以存储不同的表达式。

![](/datasource/datasource-14.png)

#### 录入表达式表

接着，需要创建一个表格卡片，并向该模板表添加几条公式数据。“表达式”模板表的每一行数据都可视为针对特定表数据模型的计算规则。每条公式数据可以使用不同数据表的数据模型中的字段值作为变量，编写相应的表达式来定义计算规则。此外，不同的计算引擎也可以用于执行这些规则。

![](/datasource/datasource-15.png)

::: info &#9432; 提示
在创建公式后，需要将业务数据与公式关联。由于直接将每条业务数据与公式数据行关联较为繁琐，通常会借助类似分类的元数据表，将其与公式表建立多对一（或一对一）关联，并进一步让业务数据与分类元数据建立多对一关联。这样，在创建业务数据时，只需指定对应的分类元数据，后续使用时便可通过这条关联路径找到相应的公式数据进行计算与应用。

:::

#### 在流程中加载相关数据
以数据表事件为例，可以创建一个工作流，在订单创建时触发，并预加载订单关联的商品数据以及商品相关的表达式数据。具体如下：
![](/datasource/datasource-16.png)

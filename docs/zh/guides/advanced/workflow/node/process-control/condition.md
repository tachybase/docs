# 条件判断

类型于编程语言中的 `if` 语句，根据配置条件判断的结果，决定后续流程的走向。

## 创建节点

条件判断有两种模式，分别是“‘是’则继续”和“‘是’和‘否’分别继续”，在创建节点时需要选择其中一种模式，之后在节点的配置中不能修改。

<!-- ![条件判断_模式选择] -->
<!-- TODO: 插入图片 -->

“‘是’则继续”的模式下，当条件判断的结果为“是”时，流程将继续执行后续节点，否则流程将终止，并以失败的状态提前退出。

<!-- ![“是”则继续模式] -->
<!-- TODO: 插入图片 -->

这种模式适合于不满足条件的情况下，流程不再继续的场景，例如绑定了“操作前事件”的表单提交按钮配提交订单，但在订单对应商品库存不足的情况下，不继续生成订单，而是失败退出。

“‘是’和‘否’分别继续”的模式下，条件节点后续会产生两条分支流程，分别对应条件判断的结果为“是”和“否”时的流程，两条分支流程可以分别配置后续节点，在任意分支执行完毕后，再自动汇合到条件节点所在的上级分支，继续执行之后的节点。

<!-- ![“是”和“否”分别继续模式] -->
<!-- TODO: 插入图片 -->

这种模式适合于满足条件和不满足条件的情况下，流程需要分别执行不同的操作的场景，例如查询某条数据是否存在，不存在的时候新增，存在的时候更新。

## 节点配置

### 运算引擎

目前支持三种引擎：

- **基础**：通过简单的双目计算和“与”、“或”分组，得到逻辑结果。
- **Math.js**：计算 [Math.js](https://mathjs.org/) 引擎支持的表达式得到逻辑结果。
- **Formula.js**：计算 [Formula.js](https://formulajs.info/) 引擎支持的表达式得到逻辑结果。

三种计算中均可以使用流程上下文的变量，用作计算的操作数。

## 示例

### “‘是’则继续”模式

<!-- TODO -->

### “‘是’和‘否’分别继续”模式

<!-- TODO -->
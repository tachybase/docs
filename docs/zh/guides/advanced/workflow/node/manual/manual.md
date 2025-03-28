# 人工节点

## 创建节点

在工作流配置界面中，点击流程中的加号（“+”）按钮，添加“人工处理”节点：

![创建人工节点]
<!-- TODO: 插入图片 -->

## 配置节点

### 负责人

人工节点需要指定一个用户，作为待办任务的执行者。待办任务的列表可以在页面添加卡片时添加，每个节点的任务弹窗内容需要在节点中进行界面配置。

选定一个用户，或者通过变量选择上下文中的用户数据的主键或外键。

![人工节点_配置_负责人_选择变量]
<!-- TODO: 插入图片 -->

:::info{title=提示}
目前人工节点的负责人选项暂不支持针对多人处理，会在未来的版本中支持。
:::

### 配置用户界面

待办事项的界面配置是人工节点的核心内容，可以通过点击“配置用户界面”按钮弹窗打开独立配置，和普通页面一样，可以所见即所得地配置：

![人工节点_节点配置_界面配置]
<!-- TODO: 插入图片 -->

#### 标签页

标签页可以用于区分不同的内容，例如一个标签页用于通过的表单提交，另一个标签页用于拒绝的表单提交，或者用于展示相关数据的详情等，可自由配置。

#### 卡片

支持的卡片类型主要有两大类，数据卡片和表单卡片，另外的 Markdown 主要用于提示信息等静态内容。

##### 数据卡片

数据卡片可选择触发器数据或任意的节点处理结果，用于提供给待办负责人相关的上下文信息。例如工作流是表单事件触发的，即可以创建一个触发数据的详情卡片，与普通页面的详情配置一致，可任选触发数据内有的字段进行数据展示：

![人工节点_节点配置_界面配置_数据卡片_触发器]
<!-- TODO: 插入图片 -->

节点数据卡片类似，可以选择上游节点中的数据结果作为详情展示。例如上游一个计算节点的结果，作为负责人待办的上下文参考信息：

![人工节点_节点配置_界面配置_数据卡片_节点数据]
<!-- TODO: 插入图片 -->

:::info{title=提示}
由于配置界面时工作流都处于未执行的状态，所以数据卡片中都是没有具体数据显示的，只有当工作流被触发执行后，在待办弹窗界面中才可看到具体流程的相关数据。
:::

##### 表单卡片

待办界面中至少需要配置一个表单卡片，作为工作流是否继续执行的最终决策处理，不配置表单会导致流程中断后无法继续。表单卡片有三种类型，分别是：

- 自定义表单
- 新增数据表单
- 更新数据表单

![人工节点_节点配置_界面配置_表单类型]
<!-- TODO: 插入图片 -->

新增数据表单和更新数据表单需要选择基于的数据表，待办用户提交后会使用表单内的值新增或更新特定数据表的数据。自定义表单则可以自由定义一个数据表无关的临时表单，待办用户提交后的字段值可以在后续节点中使用。

表单的提交按钮可以配置三种类型，分别是：

- 提交后继续流程
- 提交后终止流程
- 仅暂存表单值

![人工节点_节点配置_界面配置_表单按钮]
<!-- TODO: 插入图片 -->

三个按钮代表流程处理中三种节点状态，提交后该节点的状态修改为“完成”、“拒绝”或继续处于“等待”的状态，一个表单至少要配置前两者之一，以决定整个流程的后续处理流向。

在“继续流程”按钮上可以配置对表单字段的赋值：

![人工节点_节点配置_界面配置_表单按钮_设置表单值]
<!-- TODO: 插入图片 -->

![人工节点_节点配置_界面配置_表单按钮_设置表单值弹窗]
<!-- TODO: 插入图片 -->

打开弹窗后可以对表单任意字段进行赋值，表单提交后将会以该值作为字段的终值。通常在对一些数据进行审核时比较有用，可以在表单中使用多个不同的“继续流程”按钮，每个按钮对类似状态的字段设置不同的枚举值，以达到继续后续流程执行且使用不同数据值的效果。

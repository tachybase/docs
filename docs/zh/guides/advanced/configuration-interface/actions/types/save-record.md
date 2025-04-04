# 保存记录

<!-- TODO: 实际版本有问题 -->
## 介绍

保存数据操作允许通过字段赋值指定字段保存的值，优先级高于表单填写的值，还可以结合工作流，实现数据自动化流程。

![20240413214755](/actions/save-record-1.png)

![20240413214926](/actions/save-record-2.png)

## 操作配置项

### 字段赋值

如果配置了字段赋值，那么同一字段将以字段赋值配置的值为准，优先级高于表单中填写的值。

![20240423213245](/actions/save-record-3.png)

更多内容参考 [字段赋值](/guides/advanced/configuration-interface/actions/action-settings/assign-value)

- [编辑按钮](/guides/advanced/configuration-interface/actions/action-settings/edit-button)
- [二次确认](/guides/advanced/configuration-interface/actions/action-settings/double-check)
- [提交成功后](/guides/advanced/configuration-interface/actions/action-settings/affter-successful)
- [绑定工作流](/guides/advanced/configuration-interface/actions/action-settings/bind-workflow)
- 跳过必填校验
- 执行后刷新
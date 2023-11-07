# 代码扩展

对于本地部署 Dify 的开发者，如果想实现扩展能力，无需重新写一个 API 服务，可以使用代码扩展，即在 Dify 功能的基础上，以代码形式扩展或增强程序的能力（即插件能力），而不破坏 Dify 原有代码逻辑。它遵循一定的接口或规范，以实现与主程序的兼容和可插拔性。 目前，Dify 开放了两种代码扩展，分别为：

* 新增一种新的外部数据工具类型 [external\_data\_tool.md](external\_data\_tool.md "mention")
* 扩展敏感内容审查策略 [moderation.md](moderation.md "mention")

可在上述功能的基础上，遵循代码层 interface 的规范，来实现横向扩展的目的。

### schema.json 规范定义

Code-based Extension 前端样式通过 `schema.json` 定义，以下是定义规范。

* label：自定义类型名称，支持系统语言切换
* form\_schema：表单内容列表
  * type：组件类型
    * select：下拉选项
    * text-input：文本
    * paragraph：段落
  * label：组件名称，支持系统语言切换
  * variable：变量名称
  * required：是否必填
  * default：默认值
  * placeholder：组件提示内容
  * options：组件「select」专有属性，定义下拉内容
    * label：下拉名称，支持系统语言切换
    * value：下拉选项值
  * max\_length：组件「text-input」专有属性，最大长度

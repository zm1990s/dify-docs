# Code-based 扩展

对于本地部署 Dify 的开发者，如果想实现扩展能力，无需重新写一个 API 服务，可以使用 Code-based Extension 即在 Dify 功能的基础上，以代码形式扩展或增强程序的能力（即插件能力），而不破坏 Dify 原有代码逻辑。它遵循一定的接口或规范，以实现与主程序的兼容和可插拔性。 目前，Dify 开放了两种 Code-based Extension，分别为：

* 新增一种新的外部数据工具类型[external\_data\_tool.md](api\_based\_extension/external\_data\_tool.md "mention")
* 扩展敏感内容审查策略[moderation.md](api\_based\_extension/moderation.md "mention")

可在上述功能的基础上，遵循代码层 interface 的规范，来实现横向扩展的目的。

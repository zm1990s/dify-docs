# 应用管理

### 编辑应用信息

创建应用后，如果你想要修改应用名称或描述，可以点击应用左上角的 「编辑信息」 ，重新修改应用的图标、名称或描述。

<figure><img src="../../.gitbook/assets/image (260).png" alt="zh-Hans-edit-app-info"><figcaption><p>编辑应用信息</p></figcaption></figure>

### 复制应用

应用均支持复制操作，点击应用左上角的 「复制」。

### 导出应用

在 Dify 内创建的应用均支持以 DSL 格式进行导出，你可以自由地将配置文件导入至任意 Dify 团队。你可以通过以下两种方式导出 DSL 文件。

- 在 “工作室” 页点击应用菜单按钮中 “导出 DSL”
- 进入应用的编排页后，点击左上角 “导出 DSL”

![](../../../img/export-dsl.png)

DSL 文件不包含以下敏感信息：

- 第三方工具的授权信息，例如 API Key。
- 如果环境变量中包含 `Secret`，导出文件时将进行提示是否允许导出敏感信息。

![](../../../img/export-dsl-secret.png)

{% hint style="info" %}
Dify DSL 格式文件是 Dify.AI 定义的 AI 应用工程文件标准，文件格式为 YML。该标准涵盖应用的基本描述、模型参数、编排配置等信息。
{% endhint %}

### 删除应用

如果你想要清理应用，可以点击应用左上角的 「删除」 。

{% hint style="info" %}
⚠️ 应用的删除操作无法撤销，所有用户将无法访问你的应用，应用内的所有 Prompt、编排配置和日志均会被删除。
{% endhint %}

# 创建应用

你可以通过 3 种方式在 Dify 的工作室内创建应用：

* 基于应用模板创建（新手推荐）
* 创建一个空白应用
* 通过 DSL 文件（本地/在线）创建应用

### 从模板创建应用

初次使用 Dify 时，你可能对于应用创建比较陌生。为了帮助新手用户快速了解在 Dify 上能够构建哪些类型的应用，Dify 团队内的提示词工程师已经创建好了多场景、高质量的应用模板。

你可以从导航选择 「工作室 」，在应用列表内选择 「从模版创建」。

<figure><img src="https://assets-docs.dify.ai/img/zh_CN/application-orchestrate/4b1add0e1ee1cba45a91d88b4e09ab2a.webp" alt=""><figcaption><p>从模板创建应用</p></figcaption></figure>

任意选择某个模板，并将其添加至工作区。

<figure><img src="https://assets-docs.dify.ai/img/zh_CN/application-orchestrate/3f296bf2238c147a477155850022d83d.webp" alt=""><figcaption><p>Dify 应用模板</p></figcaption></figure>

### 创建一个新应用

如果你需要在 Dify 上创建一个空白应用，你可以从导航选择 「工作室」 ，在应用列表内选择 「从空白创建 」。

<figure><img src="https://assets-docs.dify.ai/img/zh_CN/application-orchestrate/7c27e660631bdfc0795465d8f03e7871.webp" alt=""><figcaption></figcaption></figure>

初次创建应用时，你可能需要先理解 Dify 上 4 种不同应用类型的[基本概念](./#application\_type)，分别是聊天助手、文本生成应用、Agent 和工作流。

创建应用时，你需要给应用起一个名字、选择合适的图标，或者上传喜爱的图片用作图标、使用简介清晰的文字来描述此应用的用途，以方便后续应用在团队内的使用。

<figure><img src="https://assets-docs.dify.ai/img/zh_CN/application-orchestrate/b8e1c1a499ea87d78e2f06e88a1ef14d.webp" alt=""><figcaption><p>创建一个空白应用</p></figcaption></figure>

### 通过 DSL 文件创建应用

{% hint style="info" %}
Dify DSL 是由 Dify.AI 所定义的 AI 应用工程文件标准，文件格式为 YML。该标准涵盖应用在 Dify 内的基本描述、模型参数、编排配置等信息。
{% endhint %}

#### 本地导入

如果你从社区或其它人那里获得了一个应用模版（DSL 文件），可以从工作室选择 「 导入DSL 文件 」。DSL 文件导入后将直接加载原应用的所有配置信息。

<figure><img src="https://assets-docs.dify.ai/img/zh_CN/application-orchestrate/f582fa78c9c3ef9be0575cdbc7c036b7.webp" alt=""><figcaption><p>导入 DSL 文件创建应用</p></figcaption></figure>

#### URL 导入

你也可以通过 URL 导入 DSL 文件，参考的链接格式：

```URL
https://example.com/your_dsl.yml
```

<figure><img src="https://assets-docs.dify.ai/img/zh_CN/application-orchestrate/a5ab84ec20faf225db2fc403569d1deb.webp" alt=""><figcaption><p>通过 URL 导入 DSL 文件</p></figcaption></figure>

> 导入 DSL 文件时将校对文件版本号。如果 DSL 版本号差异较大，有可能会出现兼容性问题。详细说明请参考 [应用管理：导入](https://docs.dify.ai/zh-hans/guides/management/app-management#dao-ru-ying-yong)。

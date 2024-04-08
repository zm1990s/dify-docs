# 知识检索

知识库检索节点用于从 Dify 知识库中查询与用户问题相关的文本内容，可作为后续 LLM 的上下文进行回答。

<figure><img src="https://langgenius.feishu.cn/space/api/box/stream/download/asynccode/?code=NmJmZTY0NDUzOGZkYTFmOTQ5YTcwZWRiMzhiODY5MDNfeVhsVTZPTkhaZzZjR3ZZcWt6bldoQ1g2Y0ljc1N0eUdfVG9rZW46QmFFOWJzMXJEb2tWWjl4YUZBUWM5dU5nbnhkXzE3MTI1ODY0OTI6MTcxMjU5MDA5Ml9WNA" alt=""><figcaption></figcaption></figure>

配置知识库检索节点主要包含三个部分：

1. 选择查询变量
2. 选择查询的知识库
3. 配置检索策略

**选择查询变量**

在知识库检索场景中，用于知识库检索的查询变量一般为用户输入的问题，在对话型应用的「开始」节点中，系统预设了「sys.query」作为用户输入变量，你可以使用该变量用于查询知识库内与用户问题最相近的文本分段结果。

**选择查询知识库**

在知识库检索节点中你可以添加一个 Dify 内已有的知识库，如何在 Dify 内创建知识库请参考[知识库帮助文档](https://docs.dify.ai/v/zh-hans/guides/knowledge-base)。

**配置检索策略**

可以在节点内修改单个知识库的索引策略和检索模式。关于该设置的具体原理请参考[知识库帮助文档](https://docs.dify.ai/v/zh-hans/learn-more/extended-reading/retrieval-augment/hybrid-search)。

<figure><img src="https://langgenius.feishu.cn/space/api/box/stream/download/asynccode/?code=ODQ4OWM3MmU4OWE0MzJkMzA4ZDNjMGI5ZGJiOTUzODJfajhqRzlKeGFqTnk1SzhxSjFhcE10TlpPTThPU05CR0JfVG9rZW46UVhWNGJ0R3JGb2x6MTJ4YWVEY2M3YmE2blFkXzE3MTI1ODY1MDk6MTcxMjU5MDEwOV9WNA" alt=""><figcaption></figcaption></figure>

Dify 针对多知识库的不同检索场景提供了两种召回策略：「N选1召回」和「多路召回」，在 N 选 1 模式下，知识库查询通过工具函数调用（Function Calling）来实现，需要选择系统推理模型。在多路召回模式下，需要配置 Rerank 模型用于结果重排。关于两种召回策略的具体原理请参考帮助文档中的[召回模式说明](https://docs.dify.ai/v/zh-hans/learn-more/extended-reading/retrieval-augment/retrieval)。

<figure><img src="https://langgenius.feishu.cn/space/api/box/stream/download/asynccode/?code=N2FiZTg5NDFkZWY5MDE3MDRjYmMxNDkwNTZkNmIwMjlfZ21jMEFIRFM2bjBBa0hVZW0zUm4zWTdRQ1lvY2RIT3pfVG9rZW46T1JjNmJuZzJLb2RzQVF4NWdWRGNxVVkzbkZoXzE3MTI1ODY1MzA6MTcxMjU5MDEzMF9WNA" alt=""><figcaption></figcaption></figure>

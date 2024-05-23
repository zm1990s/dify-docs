# 应用关联知识库

### 如何编排一个 AI 知识库应用

已创建的知识库可以作为外部知识提供给大模型用于精确回复用户问题。你可以在 Dify 的[所有应用类型](../application-design/#application\_type)关联知识库。

以聊天助手为例，使用流程如下：

1. 打开应用编排页
2. 在上下文设置中点击 「 添加 」
3. 从已创建的知识库中选择单个或者多个知识库
4. 配置知识库召回策略并保存
5. 在 「 添加功能 」 内打开 「引用和归属 」 功能
6. 在 「 调试与预览 」 内输入与知识库相关的用户问题进行调试
7. 调试完成之后保存并发布为一个 AI 知识库问答类应用

<figure><img src="../../.gitbook/assets/image (187).png" alt=""><figcaption><p>在应用内关联知识库</p></figcaption></figure>

### 召回设置

在应用编排的知识库召回设置中提供了两种召回策略：

**N 选 1 召回**，根据用户意图和知识库描述，由 Agent 自主判断选择最匹配的单个知识库来查询相关文本，适合知识库描述区分度大且知识库数量偏少的应用。

**多路召回（推荐）**，根据用户意图同时匹配所有知识库，从多路知识库查询相关文本片段，经过重排序步骤，从多路查询结果中选择匹配用户问题的最佳结果，需配置 Rerank 模型 API。

<figure><img src="../../.gitbook/assets/image (189).png" alt=""><figcaption></figcaption></figure>

### 选择适合的召回模式

**N 选 1 召回模式**

N 选 1 召回由  Function Call/ReAct 进行驱动，每一个关联的知识库作为函数，LLM 会自主选择与用户问题最匹配的 1 个知识库来进行查询，推理的依据为用户问题与知识库描述的语义匹配性。

因此 N 选 1 模式的召回效果主要受三个因素影响：

* 系统推理模型的能力
* 知识库的描述是否清晰，知识库描述决定了 LLM 能够推理出正确的 Function
* 知识库的个数，函数过多时将会影响 LLM 的推理精确性

当应用内关联过多知识库时， N 选 1 模式的召回率会随之下降。

用户上传知识库时，系统推理模型将自动为知识库生成一个摘要描述。为了在该模式下获得最佳的召回效果，你可以在“知识库->设置->知识库描述”中查看到系统默认创建的摘要描述，并检查该内容是否可以清晰的概括知识库的内容。

以下是 N 选 1 召回模式的技术流程图：

<figure><img src="../../.gitbook/assets/image (190).png" alt=""><figcaption></figcaption></figure>

#### 多路召回模式（推荐） <a href="#duo-lu-zhao-hui-mo-shi" id="duo-lu-zhao-hui-mo-shi"></a>

在多路召回模式下，检索器会在所有与应用关联的知识库中去检索与用户问题相关的文本内容，并将多路召回的相关文档结果合并，并通过后置的重排序（Rerank）步骤对检索召回的文档进行语义重排。

以下是多路召回模式的技术流程图：

<figure><img src="https://docs.dify.ai/~gitbook/image?url=https%3A%2F%2F1288284732-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FCdDIVDY6AtAz028MFT4d%252Fuploads%252Fgit-blob-9bb237ea9a2b4cc09637e951e696d5b52eb31033%252Fimage.png%3Falt%3Dmedia&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=0790e257848b5e6c45ce226109aa1c2f5d54bae1c04d1e14dec9fa6a46bdee17" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
多路召回模式下需要配置 Rerank 模型
{% endhint %}

多路召回模式不依赖于模型的推理能力或知识库描述，该模式在多知识库检索时能够获得质量更高的召回效果，因此更推荐将召回模式设置为多路召回。

### 重排序（Rerank）

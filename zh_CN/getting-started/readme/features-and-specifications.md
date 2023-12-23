---
description: >-
  如果你对 LLM 应用技术栈已有前置知识，希望快速了解 Dify 相对于当前技术共识的支持程度和产品特性，这份文档是为你准备的。便于你将 Dify
  与其它产品做对比，并推荐给您的团队和友人。
---

# 特性与技术规格

{% hint style="info" %}
我们的团队对产品特性和技术规格采取透明化政策，确保您可以在充了解 Dify 产品信息时进行选型。这也有利于社区对我们的产品进行贡献。
{% endhint %}

### 项目基础信息

<table data-header-hidden><thead><tr><th width="165"></th><th></th></tr></thead><tbody><tr><td>项目设立</td><td>2023 年 3 月</td></tr><tr><td>开源协议</td><td>基于 Apache License 2.0 的有限商业化授权</td></tr><tr><td>官方研发团队</td><td>超过 10 名全职员工</td></tr><tr><td>社区贡献者</td><td>超过 60 人</td></tr><tr><td>后端技术</td><td>Python/Flask/PostgreSQL</td></tr><tr><td>前端技术</td><td>Next.js</td></tr><tr><td>代码行数</td><td>超过 12 万行</td></tr><tr><td>发版周期</td><td>平均每周一次</td></tr></tbody></table>

### 技术特性

<table data-header-hidden><thead><tr><th width="255"></th><th></th></tr></thead><tbody><tr><td>LLM SDK</td><td>Dify Runtime 及少量 LangChain 代码</td></tr><tr><td>API 规格</td><td>RESTful，已覆盖大部分功能</td></tr><tr><td>商业模型支持</td><td><p>8 家，包括 OpenAI 与 Authropic</p><p>新的主流模型通常在 48 小时内完成接入</p></td></tr><tr><td>MaaS 供应商支持</td><td>2 家，Hugging Face 与 Replicate</td></tr><tr><td>本地模型推理 Runtime 支持</td><td>Xoribits（推荐），OpenLLM</td></tr><tr><td>多模态技术</td><td><p>ASR 模型</p><p>GPT-4V 规格的富文本模型</p></td></tr><tr><td>预制应用类型</td><td>文本生成型 与 对话型</td></tr><tr><td>Prompt 即服务编排</td><td><p>广受好评的可视化的 Prompt 编排界面，在同一个界面中修改 Prompt 并预览效果<br></p><p><strong>编排模式</strong></p><ul><li>简易编排</li><li>高级编排</li><li>Flow 编排（即将支持）</li></ul><p><strong>Prompt 变量类型</strong></p><ul><li>字符串</li><li>单选枚举</li><li>外部 API</li></ul></td></tr><tr><td>RAG 特性</td><td><p>首创的可视化的知识库管理界面<br><br><strong>索引方式</strong></p><ul><li>关键词</li><li>文本向量</li></ul><p><strong>检索方式</strong></p><ul><li>关键词</li><li>文本相似度匹配</li><li>混合检索</li></ul></td></tr><tr><td>ETL 技术</td><td><p>支持对上传文件和 Notion 知识库中的内容进行清洗</p><p>内置了 <a href="https://unstructured.io">Unstructured</a> 服务（可选）</p></td></tr><tr><td>向量数据库支持</td><td>Qdrant（推荐），Weaviate，Zilliz</td></tr><tr><td>Agent 技术</td><td><p>ReAct，Function Calling<br></p><p><strong>工具支持</strong></p><ul><li>可调用 OpenAI Plugin 标准的工具</li><li>可直接调用 OpenAPI 标准的 API</li></ul></td></tr><tr><td>模型调用缓存技术</td><td>基于经人类标注的 Q&#x26;A 对的相似度命中</td></tr><tr><td>调用日志</td><td>支持，可进行标注和导出，可用于缓存</td></tr><tr><td>部署方式</td><td>Docker</td></tr><tr><td>内容审查机制</td><td>OpenAI 或外部 API</td></tr><tr><td>团队协同</td><td>工作空间与多成员管理支持</td></tr></tbody></table>

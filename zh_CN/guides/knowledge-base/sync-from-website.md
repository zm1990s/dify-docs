# 从网页导入数据

Dify 知识库目前支持通过第三方工具 [Jina Reader](https://jina.ai/reader), [Firecrawl ](https://www.firecrawl.dev/) 来抓取网页并解析为 Markdown 导入至知识库。

{% hint style="info" %}
Jina Reader 和 Firecrawl 均是开源的网页解析工具，能将网页将其转换为干净并且方便 LLM 识别的 Markdown 格式文本，同时提供了易于使用的 API 服务。
{% endhint %}

### 配置 Firecrawl

首先需要在 DataSource 页面内配置 Firecrawl 的凭据。

<figure><img src="../../.gitbook/assets/dataset-creation-step1(firecrawl).png" alt=""><figcaption></figcaption></figure>

登录 [Firecrawl 官网](https://www.firecrawl.dev/) 完成注册，获取 API Key 后填入并保存。

<figure><img src="../../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

在知识库创建页选择 **Sync from website**，**填入需要抓取的网页 URL**。

<figure><img src="../../.gitbook/assets/dataset-creation-step3(firecrawl).png" alt=""><figcaption><p>网页抓取配置</p></figcaption></figure>

设置中的配置项包括：是否抓取子页面、抓取页面数量上限、页面抓取深度、排除页面、仅抓取页面、提取内容。完成配置后点击 **Run**，预览已解析的页面。

<figure><img src="../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption><p>执行抓取</p></figcaption></figure>

导入网页解析的文本后存储至知识库的文档中，查看导入结果。点击 **Add URL** 可以继续导入新的网页。

<figure><img src="../../.gitbook/assets/image (5) (1) (1).png" alt=""><figcaption><p>导入网页解析文本至知识库内</p></figcaption></figure>

### 配置 Jina Reader

首先需要在 DataSource 页面内配置相应工具的凭据。

<figure><img src="../../.gitbook/assets/dataset-creation-step1(jina).png" alt=""><figcaption></figcaption></figure>

[进入 Jina Reader 官网](https://jina.ai/reader) 即可获取拥有 1M 免费词元额度的 API Key。之后填入保存。

<figure><img src="../../.gitbook/assets/dataset-creation-step2(jina).png" alt=""><figcaption></figcaption></figure>

在知识库创建页选择 **Sync from website**，**填入需要抓取的网页 URL**。

<figure><img src="../../.gitbook/assets/dataset-creation-step3(jina).png" alt=""><figcaption><p>网页抓取配置</p></figcaption></figure>

设置中的配置项包括：是否抓取子页面、抓取页面数量上限、是否使用 sitemap 抓取。完成配置后点击 **Run**，预览已解析的页面。

<figure><img src="../../.gitbook/assets/dataset-creation-step4(jina).png" alt=""><figcaption><p>执行抓取</p></figcaption></figure>

导入网页解析的文本后存储至知识库的文档中，查看导入结果。点击 **Add URL** 可以继续导入新的网页。

<figure><img src="../../.gitbook/assets/dataset-creation-step5(jina).png" alt=""><figcaption><p>导入网页解析文本至知识库内</p></figcaption></figure>
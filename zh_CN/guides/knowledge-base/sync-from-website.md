# 从网页导入数据

Dify 知识库支持通过第三方工具如 [Jina Reader](https://jina.ai/reader), [Firecrawl ](https://www.firecrawl.dev/)抓取公开网页中的内容，解析为 Markdown 内容并导入至知识库。

{% hint style="info" %}
Jina Reader 和 Firecrawl 均是开源的网页解析工具，能将网页将其转换为干净并且方便 LLM 识别的 Markdown 格式文本，同时提供了易于使用的 API 服务。
{% endhint %}

下文将分别介绍 Firecrawl 和 Jina Reader 的使用方法。

### Firecrawl

#### 配置 Firecrawl 凭据

点击右上角头像，然后前往 **DataSource** 页面，点击 Firecrawl 右侧的 Configure 按钮。

<figure><img src="https://assets-docs.dify.ai/img/zh_CN/knowledge-base/2d54fe0ec49bef1db5f3959c61a89acd.webp" alt=""><figcaption><p>配置 Firecrawl</p></figcaption></figure>

登录 [Firecrawl 官网](https://www.firecrawl.dev/) 完成注册，获取 API Key 后填入并保存。

<figure><img src="https://assets-docs.dify.ai/img/zh_CN/knowledge-base/7c8deb9b0a3798a55828f9e638633019.webp" alt=""><figcaption></figcaption></figure>

#### 使用 Firecrawl 抓取网页内容

在知识库创建页选择 **Sync from website**，provider 选中 Firecrawl，填入需要抓取的目标 URL。

<figure><img src="https://assets-docs.dify.ai/img/zh_CN/knowledge-base/6ca80b791ba20ef4551a428283a44c9f.webp" alt=""><figcaption><p>网页抓取配置</p></figcaption></figure>

设置中的配置项包括：是否抓取子页面、抓取页面数量上限、页面抓取深度、排除页面、仅抓取页面、提取内容。完成配置后点击 **Run**，预览将要被抓取的目标页面链接。

<figure><img src="https://assets-docs.dify.ai/img/zh_CN/knowledge-base/e9410bb923af79f9de0d2acfee212598.webp" alt=""><figcaption><p>执行抓取</p></figcaption></figure>

导入网页解析的文本后存储至知识库的文档中，查看导入结果。点击 **Add URL** 可以继续导入新的网页。

<figure><img src="https://assets-docs.dify.ai/img/zh_CN/knowledge-base/301090201162d1eba3554ae36b39a355.webp" alt=""><figcaption><p>导入网页解析文本至知识库内</p></figcaption></figure>

抓取完成后，网页中的内容将会被收录至知识库内。

***

### Jina Reader

#### 配置 Jina Reader 凭据

点击右上角头像，然后前往 **DataSource** 页面，点击 Jina Reader 右侧的 Configure 按钮。

<figure><img src="https://assets-docs.dify.ai/img/zh_CN/knowledge-base/727d87ecc38607d7b472271c111739c7.webp" alt=""><figcaption><p>配置 Jina Reader</p></figcaption></figure>

登录[ Jina Reader 官网](https://jina.ai/reader) 完成注册，获取 API Key 后填入并保存。

<figure><img src="https://assets-docs.dify.ai/img/zh_CN/knowledge-base/5e2da7fb31eae4015e54a9fd29983539.webp" alt=""><figcaption><p>填写 Jina 配置</p></figcaption></figure>

#### 使用 Jina Reader 抓取网页内容

在知识库创建页选择 **Sync from website**，provider 选中 Jina Reader，填写需要抓取的目标 URL。

<figure><img src="https://assets-docs.dify.ai/img/zh_CN/knowledge-base/f186a78e2117024d9f91ea44aad350f1.webp" alt=""><figcaption><p>网页抓取配置</p></figcaption></figure>

设置中的配置项包括：是否抓取子页面、抓取页面数量上限、是否使用 sitemap 抓取。完成配置后点击 **Run** 按钮，预览将要被抓取的页面链接。

<figure><img src="https://assets-docs.dify.ai/img/zh_CN/knowledge-base/3fb63bee8f943396f02a3c359b65cd26.webp" alt=""><figcaption><p>执行抓取</p></figcaption></figure>

导入网页解析的文本后存储至知识库的文档中，查看导入结果。如需继续添加网页，轻点右侧 **Add URL** 按钮继续导入新的网页。

<figure><img src="https://assets-docs.dify.ai/img/zh_CN/knowledge-base/713ef5e1ce4b131c98893721d62d4174.webp" alt=""><figcaption><p>导入网页解析文本至知识库内</p></figcaption></figure>

抓取完成后，网页中的内容将会被收录至知识库内。

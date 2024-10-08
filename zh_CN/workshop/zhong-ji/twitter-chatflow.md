---
cover: ../../.gitbook/assets/%E7%94%BB%E6%9D%BF_1.png
coverY: 0
---

# ChatFlow 实战：使用 Agent 生成 Twitter 账号的报告

> 作者： Steven Lynn。 Dify Technical Writer。

## 简介

在 Dify 中，你可以使用一些爬虫工具，比如 Jina ，它可以将网页转换为 LLM 可以读取的 markdown 格式。

最近，[wordware.ai](https://www.wordware.ai/) 爆火让我们了解到我们可以使用爬虫来抓取社交媒体内容以供大语言模型分析，从而创造出更有趣的应用。

然而，X（以前叫 Twitter）自2023年2月2日起停止提供免费 API 访问，并且升级了其反爬虫措施。像 Jina 这样的工具无法直接访问 X 的内容。

> Starting February 9, we will no longer support free access to the Twitter API, both v2 and v1.1. A paid basic tier will be available instead 🧵
>
> — Developers (@XDevelopers) [February 2, 2023](https://twitter.com/XDevelopers/status/1621026986784337922?ref\_src=twsrc%5Etfw)

好在 Dify有 HTTP 工具，我们可以通过发送 HTTP 请求来调用外部爬虫工具。下面让我们开始吧！

## **前提条件**

### 注册Crawlbase

Crawlbase 是一个为企业和开发者设计的全方位数据爬取和抓取平台。

此外，Crawlbase Scraper 可以从 X、Facebook 和 Instagram 等社交平台抓取数据。

点击注册：[crawlbase.com](https://crawlbase.com)

### 本地部署Dify

Dify 是一个开源的LLM应用开发平台。你可以选择云服务或使用 docker compose 在本地部署。

本次实验中，如果你不想本地部署也没关系，可以使用 Cloud 版本。

本地部署的详细流程请参考 [Dify - 文档](https://docs.dify.ai/)。以下是简要教程：

#### 克隆Dify

```bash
git clone https://github.com/langgenius/dify.git
```

#### **启动Dify**

```bash
cd dify/docker
cp .env.example .env
docker compose up -d
```

### 配置模型供应商

在账户设置中配置模型供应商：

<figure><img src="../../.gitbook/assets/build-ai-image-generation-app-3.png" alt=""><figcaption></figcaption></figure>

## 创建 ChatFlow

现在，让我们开始创建 ChatFlow。

点击`创建空白应用 - 工作流编排`：

<figure><img src="../../.gitbook/assets/截屏2024-10-08 10.48.27.png" alt=""><figcaption></figcaption></figure>

初始化的 ChatFlow 如下：

<figure><img src="../../.gitbook/assets/截屏2024-10-08 10.54.41.png" alt=""><figcaption></figcaption></figure>

## 添加节点

### 开始节点

在开始节点中，我们可以在聊天开始时添加一些系统变量。在本文中，我们需要一个 Twitter 用户的 ID 作为字符串变量。让我们将其命名为`id`。

点击开始节点并添加一个新变量：

<figure><img src="../../.gitbook/assets/截屏2024-10-08 11.02.42.png" alt=""><figcaption></figcaption></figure>

### 代码节点

根据[Crawlbase文档](https://crawlbase.com/docs/crawling-api/scrapers/#twitter-profile)所述，变量`url`（将在下一个节点中使用）为 `https%3A%2F%2Ftwitter.com%2F` + `user id`，例如 Elon Musk 应当是`https%3A%2F%2Ftwitter.com%2Felonmusk`。

为了将用户ID转换为完整URL，我们可以使用以下Python代码将前缀`https%3A%2F%2Ftwitter.com%2F`与用户 ID 整合：

```python
def main(id: str) -> dict:
    return {
        "url": "https%3A%2F%2Ftwitter.com%2F"+id,
    }
```

添加一个代码节点并选择 Python ，然后设置输入和输出变量名：

<figure><img src="../../.gitbook/assets/截屏2024-10-08 11.04.40.png" alt=""><figcaption></figcaption></figure>

### HTTP 请求节点

根据 [Crawlbase文档](https://crawlbase.com/docs/crawling-api/scrapers/#twitter-profile)，如果以 HTTP 请求格式抓取 Twitter 用户的个人资料，我们需要按以下格式填写 HTTP 请求节点：

<figure><img src="../../.gitbook/assets/截屏2024-10-08 11.07.54.png" alt=""><figcaption></figcaption></figure>

出于安全考虑，最好不要直接将 API Key 作为明文输入。

好在 Dify 的最新版本中，我们可以在`环境变量`中设置令牌值。点击 `env` - `添加变量`来设置 API Key，这样就不会以明文出现在节点中。

<figure><img src="../../.gitbook/assets/截屏2024-10-08 11.14.08.png" alt=""><figcaption></figcaption></figure>

在 [https://crawlbase.com/dashboard/account/docs](https://crawlbase.com/dashboard/account/docs) 获取 Crawlbase API Key。

输入`/`可以插入为变量。

<figure><img src="../../.gitbook/assets/截屏2024-10-08 11.18.49.png" alt=""><figcaption></figcaption></figure>

点击此节点的开始按钮，输入Elon Musk 的 URL 进行测试：

<figure><img src="../../.gitbook/assets/截屏2024-10-08 11.32.38.png" alt=""><figcaption></figcaption></figure>

### LLM节点

现在，我们可以使用 LLM 来分析 Crawlbase 抓取的结果并执行我们的命令。

变量 `context` 的值为 HTTP 请求节点的 `body`。

以下是一个提示词示例。

<figure><img src="../../.gitbook/assets/截屏2024-10-08 11.34.11.png" alt=""><figcaption></figcaption></figure>

## 测试运行

点击 `预览`开始测试运行，并在`id`中输入 Twitter 用户 ID：

例如，我想分析 Elon Musk 的推文，并以他的语气写一条关于全球变暖的推文。

<figure><img src="../../.gitbook/assets/%E6%88%AA%E5%B1%8F2024-09-02_23.47.20.png" alt=""><figcaption></figcaption></figure>

点击右上角的`发布`，并将其添加到你的网站中。

## 写在最后

### 其他 X(Twitter) 爬虫

在本文中，我介绍了 Crawlbase ，应该是目前最便宜的 Twitter 爬虫服务，但有时它可能无法正确抓取用户推文的内容。

前面提到的 [wordware.ai](http://wordware.ai) 使用的 Twitter 爬虫服务是 **Tweet Scraper V2**，但它的托管平台 **apify** 的订阅费用是每月49美元。

## 链接

* [X@dify\_ai](https://x.com/dify\_ai)
* Dify的GitHub仓库：[https://github.com/langgenius/dify](https://github.com/langgenius/dify)

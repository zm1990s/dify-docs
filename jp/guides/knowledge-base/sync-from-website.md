# Webサイトからデータをインポート

Dify のナレッジベースでは、Firecrawl を利用してウェブページをスクレイピングし、解析したデータをMarkdownの形式でナレッジベースに取り込むことができます。

{% hint style="info" %}
[Firecrawl ](https://www.firecrawl.dev/)は、オープンソースのウェブページ解析ツールです。ウェブページをクリーンで大規模言語モデル（LLM）が扱いやすいMarkdown形式のテキストに変換します。また、使いやすいAPIサービスも提供しています。
{% endhint %}

### 設定方法

まず、DataSourceページでFirecrawlの認証情報を設定する必要があります。

<figure><img src="https://assets-docs.dify.ai/img/jp/knowledge-base/afd9eda23e25c1d3d339fe32832c0237.webp" alt=""><figcaption></figcaption></figure>

[Firecrawl 公式サイト](https://www.firecrawl.dev/) にログインして登録を完了し、APIキーを取得してから入力し、保存します。

<figure><img src="https://assets-docs.dify.ai/img/jp/knowledge-base/1fecd0b7a53b6c3df7eee3761b5380ae.webp" alt=""><figcaption></figcaption></figure>

ナレッジベース作成のページで**Sync from website**を選択し、**スクレイピングの対象どしてのウェブページのURLを入力します**。

<figure><img src="https://assets-docs.dify.ai/img/jp/knowledge-base/8679908c3d3a981d769700f0cd6bad9d.webp" alt=""><figcaption><p>网页抓取配置</p></figcaption></figure>

設定項目には、サブページのスクレイピング、スクレイピングするページの上限、ページのスクレイピング深度、ページの除外、指定ページのみのスクレイピング、コンテンツの抽出などが含まれます。設定が完了したら **Run** をクリックし、解析結果のページをプレビューします。

<figure><img src="https://assets-docs.dify.ai/img/jp/knowledge-base/d4c619de65d201e59f2bf26738515dfd.webp" alt=""><figcaption><p>执行抓取</p></figcaption></figure>

解析されたテキストをナレッジベースのドキュメントにインポートし、結果を確認します。**Add URL** をクリックすると、新しいウェブページをさらにインポートできます。

<figure><img src="https://assets-docs.dify.ai/img/jp/knowledge-base/c47cce032317a3736f137f98737e3abd.webp" alt=""><figcaption><p>解析されたウェブページのテキストをナレッジベースにインポート</p></figcaption></figure>

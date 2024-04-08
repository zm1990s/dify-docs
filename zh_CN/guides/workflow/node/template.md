# 模板转换

模板功能允许你借助 Jinja2 这一强大的 Python 模板语言，灵活地格式化并合并来自前面步骤的变量，创建出单一的文本输出。这非常适合于将多个数据源的信息汇总成一个特定格式，满足后续步骤的需求。例如，以下简单示例说明了如何利用之前步骤的输出来拼接一篇文章：&#x20;

<figure><img src="../../../.gitbook/assets/image (158).png" alt="" width="375"><figcaption></figcaption></figure>

对于更复杂的应用场景，你可以参考 Jinja 的[官方文档](https://jinja.palletsprojects.com/en/3.1.x/templates/)，创建更为复杂的模板来执行各种任务。这里有一个模板示例，它把从知识检索节点获取的信息及其相关的元数据，整理成一个结构化的 Markdown 格式：

{% code fullWidth="false" %}
```Plain
{% raw %}
{% for item in chunks %}
### Chunk {{ loop.index }}. 
### Similarity: {{ item.metadata.score | default('N/A') }}

#### {{ item.title }}

##### Content
{{ item.content | replace('\n', '\n\n') }}

---
{% endfor %}
{% endraw %}
```
{% endcode %}

<figure><img src="../../../.gitbook/assets/image (159).png" alt=""><figcaption></figcaption></figure>

模版节点可以在聊天流程（Chatflow）中应用，用于在触发大型语言模型（LLM）进行回应前，向用户展示中间结果。

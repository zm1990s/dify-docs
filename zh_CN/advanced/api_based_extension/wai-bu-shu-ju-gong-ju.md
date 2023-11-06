# 外部数据工具

## 功能介绍

此前，为了应对大多数语言模型使用过时训练数据,且对文本长度有限制,无法利用用户最新的私有上下文进行对话等问题，Dify 通过数据集功能实现了简易的数据集管理和集成，参见 👉 [datasets](../datasets/ "mention")。开发者可以直接上传各类格式的长文本、结构化数据来构建数据集，同时支持从外部数据源同步数据至数据集，比如 [sync-from-notion.md](../datasets/sync-from-notion.md "mention")。Dify 会自动将数据集内容集成到 AI 应用中,使其基于用户的私有、最新上下文进行对话。这种数据集管理集成方式,解决了语言模型使用限制的同时,也降低了开发者获取高质量对话上下文的门槛。

然而企业在开发 AI 应用如企业知识库 ChatBot 的时候，会面临以下 4 个方面的难题：

1. 数据安全

很多企业拥有自己的知识库或私有数据集，通常以数据库方式存储，其中可能包含隐私或敏感信息,不能直接上传到第三方平台。

2. 自定义能力

虽然此前 Dify 提供了统一管理数据集的平台以便于维护，但是企业可能根据自己的业务需要寻求更加定制化的需求。

3. 实时调用

上传离线数据，无法做到实时同步企业日益更新的知识库，频繁的手动上传无法跟上大批量内容更迭的脚步，在维护方面需要更宽泛的灵活性。

4. 保护核心竞争力

业务能力往往是企业的核心竞争力，无论是独特的产品或服务，还是创新的商业模式，都是企业珍贵的资产，企业往往不想直接暴露给第三方。



所以，我们开发了外部数据工具（External\_Data\_Tool），借助该功能，你可以通过企业自己的 API 来扩展 Dify 的查询模块能力，而无需将数据集上传到 Dify，同时解决了以上的 4 个难题。

## 具体实现

当终端用户向对话系统提出请求时，平台后端会触发外部数据工具（即调用自己的 API），它会查询用户问题相关的外部信息，如员工资料、实时记录等，并返回与当前请求相关的部分。平台后端会将返回的结果组装成文本作为上下文注入到 Prompt 中，以输出更加个性化和符合用户需求的回复内容。这样的设计避免了语言模型只依赖单次请求中的有限信息进行推理,让其可以基于更丰富的用户背景积累进行对话,从而产生更智能、贴近人的交互体验。

### 扩展点

`app.external_data_tool.query` 应用外部数据工具查询扩展点。

该扩展点将终端用户传入的应用变量内容和对话输入内容（对话型应用固定参数）作为参数，传给 API。

开发者需要实现对应工具的查询逻辑，并返回字符串类型的查询结果。

#### Request Body <a href="#user-content-request-body" id="user-content-request-body"></a>

```
{
    "point": "app.external_data_tool.query", // 扩展点类型，此处固定为 app.external_data_tool.query
    "params": {
        "app_id": string,  // 应用 ID
        "tool_variable": string,  // 外部数据工具变量名称，表示对应变量工具调用来源
        "inputs": {  // 终端用户传入变量值，key 为变量名，value 为变量值
            "var_1": "value_1",
            "var_2": "value_2",
            ...
        },
        "query": string | null  // 终端用户当前对话输入内容，对话型应用固定参数。
    }
}
```

* Example
  * ```
    {
        "point": "app.external_data_tool.query",
        "params": {
            "app_id": "61248ab4-1125-45be-ae32-0ce91334d021",
            "tool_variable": "weather_retrieve",
            "inputs": {
                "location": "London"
            },
            "query": "How's the weather today?"
        }
    }
    ```

#### API 返回 <a href="#usercontentapi-fan-hui" id="usercontentapi-fan-hui"></a>

```
{
    "result": string
}
```

* Example
  * ```
    {
        "result": "City: London\nTemperature: 10°C\nRealFeel®: 8°C\nAir Quality: Poor\nWind Direction: ENE\nWind Speed: 8 km/h\nWind Gusts: 14 km/h\nPrecipitation: Light rain"
    }
    ```

\

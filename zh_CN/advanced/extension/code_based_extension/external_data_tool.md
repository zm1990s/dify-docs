# 外部数据工具

外部数据工具用于在终端用户提交数据后，利用外部工具获取额外数据组装至提示词中作为 LLM 额外上下文信息。Dify 默认提供了外部 API 调用的工具，具体参见 [api\_based\_extension](../api\_based\_extension/ "mention")。

而对于本地部署 Dify 的开发者，为了满足更加定制化的需求，或者不希望额外开发一个 API Server，可以直接在 Dify 服务的基础上，以插件的形式插入定制的外部数据工具实现逻辑。扩展自定义工具后，将会在工具类型的下拉列表中增加您的自定义工具选项，团队成员即可使用自定义的工具来获取外部数据。

## 如何开发扩展

开发新的外部数据工具需要准备下面几个文件：

*   `{your_tool_name}.py` 工具扩展实现代码

    * &#x20; `your_tool_name` 为您定义的工具唯一标识，唯一标识不可与其他工具重复，建议以 `custom_` 为开头，目录结构示例如下：



    ```Python
    .
    └── external_data_tool
        └── custom_db_search
            ├── custom_db_search.py
            └── schema.json
    ```

    PS. Python 文件名称必须与文件夹名称保持一致。
*   `schema.json` 前端表单结构规范



    <figure><img src="../../../.gitbook/assets/红框.png" alt=""><figcaption><p>Front-end Form Structure</p></figcaption></figure>

    红框上的为固定表单项，红框中的表单项可在 schema.json 中的 form\_schema 自定义，规范见：[.](./ "mention")

### 实现代码

```python
from typing import Optional

from core.external_data_tool.base import ExternalDataTool


class YourToolNameTool(ExternalDataTool):
    name: str = "{your_tool_name}"

    @classmethod
    def validate_config(cls, tenant_id: str, config: dict) -> None:
        """
        Validate the incoming form config data.

        :param tenant_id: the id of workspace
        :param config: the form config data
        :return:
        """
        
        # implement your own validate logic here

    def query(self, inputs: dict, query: Optional[str] = None) -> str:
        """
        Query the external data tool.

        :param inputs: user inputs
        :param query: the query of chat app
        :return: the tool query result
        """
        # TODO implement your own query logic here
        
        return ''
```

代码需要放置在 `api/core/external_data_tool`中，目录结构如下：

```python
.
└── api
    └── core
        └── external_data_tool
            ├── base.py
            ├── external_data_tool_factory.py
            ├── api
            │   ├── api.py
            │   └── schema.json
            ├── {your_tool_name}
            │   ├── {your_tool_name}.py
            │   └── schema.json
```

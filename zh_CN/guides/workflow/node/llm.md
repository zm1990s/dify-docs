---
description: LLM
---

# LLM

调用大语言模型回答问题或者对自然语言进行处理。你可以在 LLM 节点中选择合适的模型，编写提示词，设置提示词中引用的上下文，配置记忆开关、设置记忆窗口的大小等。

<figure><img src="https://langgenius.feishu.cn/space/api/box/stream/download/asynccode/?code=MDUxNGRkNDdkZjYwNmZkNGY1ZTNiYTAwOGFkMjEzOGVfZFhqR29ibjZKZVExeHVqa0poYk5wTHhOOVpMSjVNUnVfVG9rZW46Wlo4YWJTUjlUb29YU014b200bGNZUzZkbmlmXzE3MTI1ODE3NzI6MTcxMjU4NTM3Ml9WNA" alt=""><figcaption></figcaption></figure>

配置 LLM 节点主要包括两个部分：

1. 选择模型
2. 编写系统提示词

#### **配置模型**

在选择适合任务的模型之前，你需要在「系统设置—模型供应商」内完成模型配置。具体配置方式可以参考[模型配置说明](https://docs.dify.ai/v/zh-hans/guides/model-configuration)。选择好模型后可以对模型参数进行配置。

<figure><img src="https://langgenius.feishu.cn/space/api/box/stream/download/asynccode/?code=Y2QzOGJlZjA2ODY2YTBhMjNhOGY1OTI0ZGFmYTlkZDVfbmViRmtDck5DdFBoZGQ2aHE1R3JrNVJjWEJsc0hJdGZfVG9rZW46VWpUemJFZkN3b1lyWnV4MkExY2N3YzRlblRjXzE3MTI1ODE3NzI6MTcxMjU4NTM3Ml9WNA" alt=""><figcaption></figcaption></figure>

#### **编写提示词**

在 LLM 节点内，你可以自定义模型输入的提示词。如果选择对话型模型，你可以自定义系统提示词/用户消息/助手消息三部分的内容。

以知识库问答情景为例，在「上下文」中关联知识库检索节点的「结果」变量后，在提示词中插入「上下文」特殊变量即可将从知识库从检索到的文本内容作为模型输入的上下文背景信息。

<figure><img src="https://langgenius.feishu.cn/space/api/box/stream/download/asynccode/?code=NmU5NDQ2YzE3ODVkNTMyOGEwZjJlNjY4NzU5OThkYmFfR3F4TU02THJLTldBM2g5REFuWkQxS2w3ZjBzVW5Da21fVG9rZW46Uk5HOWJDb1NJb0dtRlZ4dnBuS2NKNk53blRnXzE3MTI1ODE3NzI6MTcxMjU4NTM3Ml9WNA" alt=""><figcaption></figcaption></figure>

在提示词编辑器中，你可以通过输入“/”或者“{”呼出变量插入菜单，将特殊变量块或者前置流程节点中的变量插入到提示词中作为上下文内容。

<figure><img src="../../../.gitbook/assets/image (151).png" alt="" width="375"><figcaption></figcaption></figure>

如果选择补全型模型，系统预置了提示词模板用于实现对话型应用，你可以自定义提示词的内容，在提示词合适的位置内输入“/”或者“{”插入特殊变量块：「会话历史」「上下文」来实现更丰富的会话功能。

<figure><img src="https://langgenius.feishu.cn/space/api/box/stream/download/asynccode/?code=MDUxMGFhZjAyOTExZjkxYjgwM2Y2MTUwZDRlZDQ4OTRfSUlJbFFkR0JIOXFodVRGZENsUjRLYVdSVXl2QW9yZUFfVG9rZW46UEUxSmJXdDZRb1pHU2N4cmFMRmNWR1BNbnFiXzE3MTI1ODE3NzI6MTcxMjU4NTM3Ml9WNA" alt=""><figcaption></figcaption></figure>

#### **记忆开关设置**

在对话型应用（Chatflow）中，LLM 节点会默认开启系统记忆设置，在多轮对话场景中，系统会将历史对话消息存储并在对话中传入模型。

在工作流应用（Workflow）中默认关闭系统记忆，且未提供记忆设置的选项。

#### **记忆窗口设置**

若关闭记忆窗口设置，系统将根据模型上下文窗口动态传入历史对话消息。开启记忆窗口设置后，你可以根据需求配置窗口传入历史对话消息的条数。

#### **对话角色名设置**

由于模型在训练阶段的差异，不同模型对于角色名的指令遵循程度不同，如 Human/Assistant，Human/AI，人类/助手等等。为适配多模型的提示响应效果，系统提供了对话角色名的设置，修改对话角色名将会修改会话历史的角色前缀。

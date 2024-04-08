# 关键概念

### 节点

节点是工作流中的关键构成，通过连接不同功能的节点，执行工作流的一系列操作。节点按类型分为：

* 基础节点：开始、结束、直接回复、LLM、知识检索、应用（即将上线）
* 问题转换：问题分类、问题重写（即将上线）、子问题拆分（即将上线）
* 逻辑处理：条件分支、合并（即将上线）、循环（即将上线）
* 转换：代码执行、模版转换、变量赋值、函数提取（即将上线）
* 其他：HTTP 请求
* 工具：内置工具、自定义工具

### 变量

变量用于串联工作流中前后节点的输入与输出，实现流程中的复杂处理逻辑。

* 工作流需要定义启动执行或者对话的输入变量。
* 节点需要定义启动执行的输入变量，如问题分类器的输入变量一般为用户输入的问题。
* 节点内引用变量时只可以引用该节点前置流程节点的变量。
* 为了避免引用变量名重复，节点名称不可同名。
* 节点的输出变量为系统固定变量，不可编辑修改。

### Chatflow 和 Workflow 的区别

1. 应用场景的区别

* Chatflow：面向对话类情景，属于 Chatbot 应用类型的高阶编排模式
* Workflow：面向自动化和批处理情景

2. 可用节点的区别

| **节点**              | **Chatflow**                        | **Workflow**                         |
| ------------------- | ----------------------------------- | ------------------------------------ |
| Start               | 系统内置变量：用户输入和文件上传                    | 系统内置变量：文件上传                          |
| End                 | 无 End 节点                            | 使用 End 节点在执行结束时输出，可输出结构化文本，不可在流程中间输出 |
| Answer              | 使用 Answer 节点进行流式输出或者固定文本回复，可在流程中间输出 | 无 Answer 节点                          |
| LLM                 | 默认开启 Memory 用于存储和传递多轮对话的历史消息        | 无 Memory 配置                          |
| Question Classifier | 默认开启 Memory 用于存储和传递多轮对话的历史消息        | 无 Memory 配置                          |

3. 应用入口的划分

Chatflow 入口：

<figure><img src="https://langgenius.feishu.cn/space/api/box/stream/download/asynccode/?code=ODM3ZGU4MDk2YWVhMzU5YjI5MzhjODJkM2NjMmVjMDdfYVBlbEtpQk95ZUFkOGVqY0NWR1ZFZXI2Q2ZiQzA5Y1pfVG9rZW46Uks4bmJ6T3Npb1JtU3J4TlJSZmNFdE1Xbm5mXzE3MTI1ODU0ODk6MTcxMjU4OTA4OV9WNA" alt=""><figcaption></figcaption></figure>

Workflow 入口：

<figure><img src="https://langgenius.feishu.cn/space/api/box/stream/download/asynccode/?code=M2ZlNTgyNTRmNzI2MDI3Njg4OTMzNjZjODkzNTc5MDhfWDUyRGFVSlR4RUFHc1l3Rk1DZmRnUXRRcldQd0xzMXVfVG9rZW46SEhlWGJyM0s0b1FkNTd4OTFSa2NJNU5jbjVwXzE3MTI1ODU1MTI6MTcxMjU4OTExMl9WNA" alt=""><figcaption></figcaption></figure>

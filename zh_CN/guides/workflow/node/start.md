# 开始

定义一个 workflow 流程启动的初始参数。你可以在开始节点中自定义启动工作流的输入变量。每一个工作流都需要一个开始节点。

<figure><img src="../../../.gitbook/assets/output (1) (2).png" alt=""><figcaption></figcaption></figure>

在「开始」节点内定义输入变量支持四种类型：文本、段落、下拉选项和数字。

<figure><img src="../../../.gitbook/assets/output (2) (1).png" alt=""><figcaption></figcaption></figure>

配置完成后，在工作流执行时会要求输入开始节点中定义的变量值。

<figure><img src="../../../.gitbook/assets/output (3) (1).png" alt=""><figcaption></figcaption></figure>

提示：在 Chatflow 中，开始节点会提供系统内置变量：sys.query 和 sys.files，sys.query 用于对话型应用中的用户问题输入，sys.files 用于对话中上传文件，如上传一张图片用于理解含义，需要配合图像理解模型或者图片输入的工具来使用。

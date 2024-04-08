# 开始

定义一个 workflow 流程启动的初始参数。你可以在开始节点中自定义启动工作流的输入变量。每一个工作流都需要一个开始节点。

<figure><img src="https://langgenius.feishu.cn/space/api/box/stream/download/asynccode/?code=ODBkZjc5ZjQxNGQzMmZiNGNkNzRiNmM1Y2FmNDAxMTFfVDBwSkxEOVpVSXF2MmN3MkZVZUVDWW5VeE0yek9QWkxfVG9rZW46WmIzSGJyNVdIb2xodUt4Tm5pVGNQRmdybkVBXzE3MTI1ODU1Mjk6MTcxMjU4OTEyOV9WNA" alt=""><figcaption></figcaption></figure>

在「开始」节点内定义输入变量支持四种类型：文本、段落、下拉选项和数字。

<figure><img src="https://langgenius.feishu.cn/space/api/box/stream/download/asynccode/?code=YzE1NWY3YzA1OTM0YWY5OTk5OWIyZTdmMmIyNWE4MDNfUldUMHhDcXhvOWF5T3hoWGVmR3gwVXJkYVdjNHlVQWxfVG9rZW46VGVUNGIwU3dlb0lSWmt4TVBNbGNnSUwxbkpiXzE3MTI1ODU1NDE6MTcxMjU4OTE0MV9WNA" alt=""><figcaption></figcaption></figure>

配置完成后，在工作流执行时会要求输入开始节点中定义的变量值。

<figure><img src="https://langgenius.feishu.cn/space/api/box/stream/download/asynccode/?code=MjAzNjYwY2FjMjIyNjU0NTlkODE4ZTQwZDk1NDcxODVfNk5Nc1hNb0Z3VzZrbmp1aUpqVThneFlEcm5JdHBjMktfVG9rZW46SDhMUmJhQUN5b2ZvT0l4Zk44NmNqNmpwbnhoXzE3MTI1ODU1NTk6MTcxMjU4OTE1OV9WNA" alt=""><figcaption></figcaption></figure>

提示：在 Chatflow 中，开始节点会提供系统内置变量：sys.query 和 sys.files，sys.query 用于对话型应用中的用户问题输入，sys.files 用于对话中上传文件，如上传一张图片用于理解含义，需要配合图像理解模型或者图片输入的工具来使用。

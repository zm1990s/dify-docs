# 结束

定义一个 workflow 流程结束的最终输出内容。每一个工作流在完整执行后都需要至少一个「结果」节点，用于输出完整执行的最终结果。

「结果」节点为流程终止节点，后面无法再添加其他节点，工作流应用中只有运行到「结果」节点才会输出执行结果。若流程中出现条件分叉，则需要定义多个「结束」节点。

**单路执行示例：**

<figure><img src="https://langgenius.feishu.cn/space/api/box/stream/download/asynccode/?code=ODc1MDQ3OWMzOWI3NjkzNTVkZjc3ZTJiNDNkMmYzOTZfQ0phYk5QWG5yOTZiUFVJUXBtOTZMazFtbVdhVE0xQ0ZfVG9rZW46QVVqcmJmWElHb1pVdUJ4cnBET2NjRHFpbmhjXzE3MTI1ODU1ODY6MTcxMjU4OTE4Nl9WNA" alt=""><figcaption></figcaption></figure>

**多路执行示例：**

<figure><img src="https://langgenius.feishu.cn/space/api/box/stream/download/asynccode/?code=MTc2MTYzOTIxNWVmNWJjNzU3YmViNmUzODY2NGM2M2NfOVR4a0k0Y3ZQYUJJempuMTl4Rm5oQnl0YVRLWWlQVTFfVG9rZW46UkRPdGI2Yngwb01wdGJ4WlBrWWM4dW15bmdpXzE3MTI1ODU2MDE6MTcxMjU4OTIwMV9WNA" alt=""><figcaption></figcaption></figure>

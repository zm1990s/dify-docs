# Code

The Code node provides the ultimate level of flexibility, allowing developers to inject custom scripts in Python or Javascript into their workflows and manipulate variables in ways pre-defined nodes cannot. The configuration fields lets you define the expected input/output variables and write the code to execute:

<figure><img src="https://langgenius.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDVmYjg5MjUwYzA3ZjhkODAxOWQxZWI3OGRiZjE1ZDZfTTljRjd1YmlkTFlWRjRqZ0g4QzhsQVhkWFJPcnVPOVlfVG9rZW46T1c1VGJZR1JLb1pjNDJ4ZTV2NmMxN25WbmxoXzE3MTI1OTczNDc6MTcxMjYwMDk0N19WNA" alt="" width="375"><figcaption></figcaption></figure>

The execution environment is sandboxed for both Python and Javascript, meaning that certain functionalities that require extensive system resources or pose security risks are not available. This includes, but is not limited to, direct file system access, network calls, and operating system-level commands.

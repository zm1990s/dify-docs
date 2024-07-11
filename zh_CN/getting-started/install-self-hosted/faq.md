# 常见问题

### 1. 长时间未收到密码重置邮件应如何处理？

你需要在 `.env` 文件内配置 `Mail` 参数项，详细说明请参考 [《环境变量说明：邮件相关配置》](https://docs.dify.ai/v/zh-hans/getting-started/install-self-hosted/environments#you-jian-xiang-guan-pei-zhi)。

修改配置后，运行以下命令重启服务。

```bash
docker compose down
docker compose up -d
```

如果依然没能收到邮件，请检查邮件服务是否正常，以及邮件是否进入了垃圾邮件列表。

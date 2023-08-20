# 接入 OpenLLM 部署的本地模型

> 🚧 WIP

使用 [OpenLLM](https://github.com/bentoml/OpenLLM), 您可以针对任何开源大型语言模型进行推理,部署到云端或本地,并构建强大的 AI 应用程序。
Dify 支持以本地部署的方式接入 OpenLLM 部署的大型语言模型的推理能力。

## 部署 OpenLLM 模型

每个 OpenLLM Server 可以部署一个模型，您可以通过以下方式部署：

1. 首先通过 PyPI 安装 OpenLLM：

    ```bash
    $ pip install openllm
    ```

2. 本地部署并启动 OpenLLM 模型：

    ```bash
    $ openllm start opt --model_id facebook/opt-125m -p 3333
    2023-08-20T23:49:59+0800 [INFO] [cli] Prometheus metrics for HTTP BentoServer from "_service:svc" can be accessed at http://localhost:3333/metrics.
    2023-08-20T23:50:00+0800 [INFO] [cli] Starting production HTTP BentoServer from "_service:svc" listening on http://0.0.0.0:3333 (Press CTRL+C to quit)
    ```
   
    OpenLLM 启动后，为本机的 `3333` 端口提供 API 接入服务，端点为：`http://127.0.0.1:3333`，由于默认的 3000 端口与 Dify 的 WEB 服务冲突，这边修改为 3333 端口。
    如需修改 host 或 port，可查看 OpenLLM 启动的帮助信息：`openllm start opt --model_id facebook/opt-125m -h`。

    > 注意：此处使用 facebook/opt-125m 模型仅作为示例，效果可能不佳，请根据实际情况选择合适的模型，更多模型请参考：[支持的模型列表](https://github.com/bentoml/OpenLLM#-supported-models)。

3. 模型部署完毕，在 Dify 中使用接入模型

   在 `设置 > 模型供应商 > OpenLLM` 中填入：

   - 模型名称：`facebook/opt-125m`
   - 服务器 URL：`http://127.0.0.1:3333`

   "保存" 后即可在应用中使用该模型。

本说明仅作为快速接入的示例，如需使用 OpenLLM 更多特性和信息，请参考：[OpenLLM](https://github.com/bentoml/OpenLLM)
# Connecting to OpenLLM Local Deployed Models

With [OpenLLM](https://github.com/bentoml/OpenLLM), you can run inference with any open-source large-language models, deploy to the cloud or on-premises, and build powerful AI apps.
And Dify supports connecting to OpenLLM deployed large language model's inference capabilities locally.

## Deploy OpenLLM Model

Each OpenLLM Server can deploy one model, and you can deploy it in the following way:

1. First, install OpenLLM through PyPI:

    ```bash
    $ pip install openllm
    ```

2. Locally deploy and start the OpenLLM model:

    ```bash
    $ openllm start opt --model_id facebook/opt-125m -p 3333
    2023-08-20T23:49:59+0800 [INFO] [cli] Prometheus metrics for HTTP BentoServer from "_service:svc" can be accessed at http://localhost:3333/metrics.
    2023-08-20T23:50:00+0800 [INFO] [cli] Starting production HTTP BentoServer from "_service:svc" listening on http://0.0.0.0:3333 (Press CTRL+C to quit)
    ```
   
    After OpenLLM starts, it provides API access service for the local port `3333`, the endpoint being: `http://127.0.0.1:3333`. Since the default 3000 port conflicts with Dify's WEB service, the port is changed to 3333 here.
    If you need to modify the host or port, you can view the help information for starting OpenLLM: `openllm start opt --model_id facebook/opt-125m -h`.

    > Note: Using the `facebook/opt-125m` model here is only for demonstration, and the effect may not be good. Please choose the appropriate model according to the actual situation. For more models, please refer to: [Supported Model List](https://github.com/bentoml/OpenLLM#-supported-models).

3. After the model is deployed, use the connected model in Dify.

   Fill in under `Settings > Model Providers > OpenLLM`:

   - Model Name: `facebook/opt-125m`
   - Server URL: `http://127.0.0.1:3333`

   Click "Save" and the model can be used in the application.

This instruction is only for quick connection as an example. For more features and information on using OpenLLM, please refer to: [OpenLLM](https://github.com/bentoml/OpenLLM)
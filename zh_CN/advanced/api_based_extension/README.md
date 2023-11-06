# API-based 扩展

开发者可通过 API 扩展模块能力，当前支持以下模块扩展：

* `moderation` 敏感内容审计&#x20;
* `external_data_tool` 外部数据工具&#x20;

在扩展模块能力之前，您需要准备一个 API 和用于鉴权的 API Key（也可由 Dify 自动生成，可选）。

除了需要开发对应的模块能力，还需要遵照以下规范，以便 Dify 正确调用 API。

<figure><img src="../../.gitbook/assets/api_based_01.png" alt=""><figcaption><p>基于 API 扩展</p></figcaption></figure>

### [API 规范](https://github.com/langgenius/dify-docs/diffs/2?branch=main\&name=main\&qualified\_name=refs%2Fheads%2Fmain\&sha1=fb07d2bea301bd6388c393d5f3d8a80386c4dfdb\&sha2=a72d056812efe42f153d649085811e5b49ee131e\&short\_path=e2d7adb\&unchanged=expanded\&w=false#api-%E8%A7%84%E8%8C%83) <a href="#usercontentapi-gui-fan" id="usercontentapi-gui-fan"></a>

Dify 将会以以下规范调用您的接口：

```
POST {Your-API-Endpoint}
```

#### [Header](https://github.com/langgenius/dify-docs/diffs/2?branch=main\&name=main\&qualified\_name=refs%2Fheads%2Fmain\&sha1=fb07d2bea301bd6388c393d5f3d8a80386c4dfdb\&sha2=a72d056812efe42f153d649085811e5b49ee131e\&short\_path=e2d7adb\&unchanged=expanded\&w=false#header) <a href="#user-content-header" id="user-content-header"></a>

| Header          | Value             | Desc                                                                  |
| --------------- | ----------------- | --------------------------------------------------------------------- |
| `Content-Type`  | application/json  | 请求内容为 JSON 格式。                                                        |
| `Authorization` | Bearer {api\_key} | API Key 以 Token 令牌的方式传输，您需要解析该 `api_key` 并确认是否和提供的 API Key 一致，保证接口安全。 |

#### [Request Body](https://github.com/langgenius/dify-docs/diffs/2?branch=main\&name=main\&qualified\_name=refs%2Fheads%2Fmain\&sha1=fb07d2bea301bd6388c393d5f3d8a80386c4dfdb\&sha2=a72d056812efe42f153d649085811e5b49ee131e\&short\_path=e2d7adb\&unchanged=expanded\&w=false#request-body) <a href="#user-content-request-body" id="user-content-request-body"></a>

```
{
    "point":  string, //  扩展点，不同模块可能包含多个扩展点
    "params": {
        ...  // 各模块扩展点传入参数
    }
}
```

#### [API 返回](https://github.com/langgenius/dify-docs/diffs/2?branch=main\&name=main\&qualified\_name=refs%2Fheads%2Fmain\&sha1=fb07d2bea301bd6388c393d5f3d8a80386c4dfdb\&sha2=a72d056812efe42f153d649085811e5b49ee131e\&short\_path=e2d7adb\&unchanged=expanded\&w=false#api-%E8%BF%94%E5%9B%9E) <a href="#usercontentapi-fan-hui" id="usercontentapi-fan-hui"></a>

```
{
    ...  // API 返回的内容，不同扩展点返回见不同模块的规范设计
}
```

### [校验](https://github.com/langgenius/dify-docs/diffs/2?branch=main\&name=main\&qualified\_name=refs%2Fheads%2Fmain\&sha1=fb07d2bea301bd6388c393d5f3d8a80386c4dfdb\&sha2=a72d056812efe42f153d649085811e5b49ee131e\&short\_path=e2d7adb\&unchanged=expanded\&w=false#%E6%A0%A1%E9%AA%8C) <a href="#usercontent-xiao-yan" id="usercontent-xiao-yan"></a>

在 Dify 配置 API-based Extension 时，Dify 将会发送一个请求至 API Endpoint，以检验 API 的可用性。

当 API Endpoint 接收到 `point=ping` 时，接口应返回 `result=pong`，具体如下：

#### [Header](https://github.com/langgenius/dify-docs/diffs/2?branch=main\&name=main\&qualified\_name=refs%2Fheads%2Fmain\&sha1=fb07d2bea301bd6388c393d5f3d8a80386c4dfdb\&sha2=a72d056812efe42f153d649085811e5b49ee131e\&short\_path=e2d7adb\&unchanged=expanded\&w=false#header-1) <a href="#user-content-header-1" id="user-content-header-1"></a>

```
Content-Type: application/json
Authorization: Bearer {api_key}
```

#### [Request Body](https://github.com/langgenius/dify-docs/diffs/2?branch=main\&name=main\&qualified\_name=refs%2Fheads%2Fmain\&sha1=fb07d2bea301bd6388c393d5f3d8a80386c4dfdb\&sha2=a72d056812efe42f153d649085811e5b49ee131e\&short\_path=e2d7adb\&unchanged=expanded\&w=false#request-body-1) <a href="#user-content-request-body-1" id="user-content-request-body-1"></a>

```
{
    "point": "ping"
}
```

#### [API 期望返回](https://github.com/langgenius/dify-docs/diffs/2?branch=main\&name=main\&qualified\_name=refs%2Fheads%2Fmain\&sha1=fb07d2bea301bd6388c393d5f3d8a80386c4dfdb\&sha2=a72d056812efe42f153d649085811e5b49ee131e\&short\_path=e2d7adb\&unchanged=expanded\&w=false#api-%E6%9C%9F%E6%9C%9B%E8%BF%94%E5%9B%9E) <a href="#usercontentapi-qi-wang-fan-hui" id="usercontentapi-qi-wang-fan-hui"></a>

```
{
    "result": "pong"
}
```

### [范例](https://github.com/langgenius/dify-docs/diffs/2?branch=main\&name=main\&qualified\_name=refs%2Fheads%2Fmain\&sha1=fb07d2bea301bd6388c393d5f3d8a80386c4dfdb\&sha2=a72d056812efe42f153d649085811e5b49ee131e\&short\_path=e2d7adb\&unchanged=expanded\&w=false#%E8%8C%83%E4%BE%8B) <a href="#usercontent-fan-li" id="usercontent-fan-li"></a>

此处以外部数据工具为例，场景为根据地区获取外部天气信息作为上下文。

#### [API 范例](https://github.com/langgenius/dify-docs/diffs/2?branch=main\&name=main\&qualified\_name=refs%2Fheads%2Fmain\&sha1=fb07d2bea301bd6388c393d5f3d8a80386c4dfdb\&sha2=a72d056812efe42f153d649085811e5b49ee131e\&short\_path=e2d7adb\&unchanged=expanded\&w=false#api-%E8%8C%83%E4%BE%8B) <a href="#usercontentapi-fan-li" id="usercontentapi-fan-li"></a>

```
POST https://fake-domain.com/api/dify/receive
```

[**Header**](https://github.com/langgenius/dify-docs/diffs/2?branch=main\&name=main\&qualified\_name=refs%2Fheads%2Fmain\&sha1=fb07d2bea301bd6388c393d5f3d8a80386c4dfdb\&sha2=a72d056812efe42f153d649085811e5b49ee131e\&short\_path=e2d7adb\&unchanged=expanded\&w=false#header-2)

```
Content-Type: application/json
Authorization: Bearer 123456
```

[**Request Body**](https://github.com/langgenius/dify-docs/diffs/2?branch=main\&name=main\&qualified\_name=refs%2Fheads%2Fmain\&sha1=fb07d2bea301bd6388c393d5f3d8a80386c4dfdb\&sha2=a72d056812efe42f153d649085811e5b49ee131e\&short\_path=e2d7adb\&unchanged=expanded\&w=false#request-body-2)

```
{
    "point": "app.external_data_tool.query",
    "params": {
        "app_id": "61248ab4-1125-45be-ae32-0ce91334d021",
        "tool_variable": "weather_retrieve",
        "inputs": {
            "location": "London"
        },
        "query": "How's the weather today?"
    }
}
```

[**API 返回**](https://github.com/langgenius/dify-docs/diffs/2?branch=main\&name=main\&qualified\_name=refs%2Fheads%2Fmain\&sha1=fb07d2bea301bd6388c393d5f3d8a80386c4dfdb\&sha2=a72d056812efe42f153d649085811e5b49ee131e\&short\_path=e2d7adb\&unchanged=expanded\&w=false#api-%E8%BF%94%E5%9B%9E-1)

```
{
    "result": "City: London\nTemperature: 10°C\nRealFeel®: 8°C\nAir Quality: Poor\nWind Direction: ENE\nWind Speed: 8 km/h\nWind Gusts: 14 km/h\nPrecipitation: Light rain"
}
```

#### [代码范例](https://github.com/langgenius/dify-docs/diffs/2?branch=main\&name=main\&qualified\_name=refs%2Fheads%2Fmain\&sha1=fb07d2bea301bd6388c393d5f3d8a80386c4dfdb\&sha2=a72d056812efe42f153d649085811e5b49ee131e\&short\_path=e2d7adb\&unchanged=expanded\&w=false#%E4%BB%A3%E7%A0%81%E8%8C%83%E4%BE%8B) <a href="#usercontent-dai-ma-fan-li" id="usercontent-dai-ma-fan-li"></a>

代码基于 Python FastAPI 框架。

1.  安装依赖

    ```
    pip install fastapi[all] uvicorn
    ```
2.  按照接口规范编写代码

    ```
    from fastapi import FastAPI, Body, HTTPException, Header
    from pydantic import BaseModel

    app = FastAPI()


    class InputData(BaseModel):
        point: str
        params: dict


    @app.post("/api/dify/receive")
    async def dify_receive(data: InputData = Body(...), authorization: str = Header(None)):
        """
        Receive API query data from Dify.
        """
        expected_api_key = "123456"  # TODO Your API key of this API
        auth_scheme, _, api_key = authorization.partition(' ')

        if auth_scheme.lower() != "bearer" or api_key != expected_api_key:
            raise HTTPException(status_code=401, detail="Unauthorized")

        point = data.point

        # for debug
        print(f"point: {point}")

        if point == "ping":
            return {
                "result": "pong"
            }
        if point == "app.external_data_tool.query":
            return handle_app_external_data_tool_query(params=data.params)
        # elif point == "{point name}":
            # TODO other point implementation here

        raise HTTPException(status_code=400, detail="Not implemented")


    def handle_app_external_data_tool_query(params: dict):
        app_id = params.get("app_id")
        tool_variable = params.get("tool_variable")
        inputs = params.get("inputs")
        query = params.get("query")

        # for debug
        print(f"app_id: {app_id}")
        print(f"tool_variable: {tool_variable}")
        print(f"inputs: {inputs}")
        print(f"query: {query}")

        # TODO your external data tool query implementation here, 
        #  return must be a dict with key "result", and the value is the query result
        if inputs.get("location") == "London":
            return {
                "result": "City: London\nTemperature: 10°C\nRealFeel®: 8°C\nAir Quality: Poor\nWind Direction: ENE\nWind "
                          "Speed: 8 km/h\nWind Gusts: 14 km/h\nPrecipitation: Light rain"
            }
        else:
            return {"result": "Unknown city"}
    ```
3.  启动 API 服务，默认端口为 8000，API 完整地址为：`http://127.0.0.1:8000/api/dify/receive`，配置的 API Key 为 `123456`。

    ```
    uvicorn main:app --reload
    ```
4. 在 Dify 配置该 API。

[![](https://github.com/langgenius/dify-docs/raw/main/zh\_CN/.gitbook/assets/api\_based\_01.png)](../../.gitbook/assets/api\_based\_01.png)

5. 在 App 中选择该 API 扩展。

[![](https://github.com/langgenius/dify-docs/raw/main/zh\_CN/.gitbook/assets/api\_based\_02.png)](../../.gitbook/assets/api\_based\_02.png)

App 调试时，Dify 将请求配置的 API，并发送以下内容（范例）：

```
{
    "point": "app.external_data_tool.query",
    "params": {
        "app_id": "61248ab4-1125-45be-ae32-0ce91334d021",
        "tool_variable": "weather_retrieve",
        "inputs": {
            "location": "London"
        },
        "query": "How's the weather today?"
    }
}
```

API 返回为：

```
{
    "result": "City: London\nTemperature: 10°C\nRealFeel®: 8°C\nAir Quality: Poor\nWind Direction: ENE\nWind Speed: 8 km/h\nWind Gusts: 14 km/h\nPrecipitation: Light rain"
}
```

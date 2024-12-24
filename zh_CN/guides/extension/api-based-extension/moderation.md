# 敏感内容审查

该模块用于审查应用中终端用户输入的内容和 LLM 输出的内容，分为两个扩展点类型。

### 扩展点 <a href="#usercontent-kuo-zhan-dian" id="usercontent-kuo-zhan-dian"></a>

* `app.moderation.input` 终端用户输入的内容审查扩展点
  * 用于审查终端用户传入的变量内容以及对话型应用中对话的输入内容。
* `app.moderation.output`LLM 输出的内容审查扩展点
  * 用于审查 LLM 输出的内容，
  * 当 LLM 输出为流式时，输出的内容将分 100 字为一个分段进行请求 API，尽可能避免输出内容较长时，审查不及时的问题。

### app.moderation.input 扩展点 <a href="#usercontentappmoderationinput-kuo-zhan-dian" id="usercontentappmoderationinput-kuo-zhan-dian"></a>

当在 Chatflow、Agent、聊天助手等应用下开启**内容审查>审查输入内容**时，Dify 会给相应的 API 扩展发送下列 HTTP POST 请求：

#### Request Body <a href="#user-content-request-body" id="user-content-request-body"></a>

```
{
    "point": "app.moderation.input", // 扩展点类型，此处固定为 app.moderation.input
    "params": {
        "app_id": string,  // 应用 ID
        "inputs": {  // 终端用户传入变量值，key 为变量名，value 为变量值
            "var_1": "value_1",
            "var_2": "value_2",
            ...
        },
        "query": string | null  // 终端用户当前对话输入内容，对话型应用固定参数。
    }
}
```

* Example
  * ```
    {
        "point": "app.moderation.input",
        "params": {
            "app_id": "61248ab4-1125-45be-ae32-0ce91334d021",
            "inputs": {
                "var_1": "I will kill you.",
                "var_2": "I will fuck you."
            },
            "query": "Happy everydays."
        }
    }
    ```

#### API 返回规范 <a href="#usercontentapi-fan-hui" id="usercontentapi-fan-hui"></a>

```
{
    "flagged": bool,  // 是否违反校验规则
    "action": string, // 动作，direct_output 直接输出预设回答; overridden 覆写传入变量值
    "preset_response": string,  // 预设回答（仅当 action=direct_output 返回）
    "inputs": {  // 终端用户传入变量值，key 为变量名，value 为变量值（仅当 action=overridden 返回）
        "var_1": "value_1",
        "var_2": "value_2",
        ...
    },
    "query": string | null  // 覆写的终端用户当前对话输入内容，对话型应用固定参数。（仅当 action=overridden 返回）
}
```

* Example
  * `action=direct_output`
    * ```
      {
          "flagged": true,
          "action": "direct_output",
          "preset_response": "Your content violates our usage policy."
      }
      ```
  * `action=overridden`
    * ```
      {
          "flagged": true,
          "action": "overridden",
          "inputs": {
              "var_1": "I will *** you.",
              "var_2": "I will *** you."
          },
          "query": "Happy everydays."
      }
      ```

### app.moderation.output 扩展点 <a href="#usercontentappmoderationoutput-kuo-zhan-dian" id="usercontentappmoderationoutput-kuo-zhan-dian"></a>

当在 Chatflow、Agent、聊天助手等应用下开启**内容审查>审查输出内容**时，Dify 会给相应的 API 扩展发送下列 HTTP POST 请求：

#### Request Body <a href="#user-content-request-body-1" id="user-content-request-body-1"></a>

```
{
    "point": "app.moderation.output", // 扩展点类型，此处固定为 app.moderation.output
    "params": {
        "app_id": string,  // 应用 ID
        "text": string  // LLM 回答内容。当 LLM 输出为流式时，此处为 100 字为一个分段的内容。
    }
}
```

* Example
  * ```
    {
        "point": "app.moderation.output",
        "params": {
            "app_id": "61248ab4-1125-45be-ae32-0ce91334d021",
            "text": "I will kill you."
        }
    }
    ```

#### API 返回规范 <a href="#usercontentapi-fan-hui-1" id="usercontentapi-fan-hui-1"></a>

```
{
    "flagged": bool,  // 是否违反校验规则
    "action": string, // 动作，direct_output 直接输出预设回答; overridden 覆写传入变量值
    "preset_response": string,  // 预设回答（仅当 action=direct_output 返回）
    "text": string  // 覆写的 LLM 回答内容。（仅当 action=overridden 返回）
}
```

* Example
  * `action=direct_output`
    * ```
      {
          "flagged": true,
          "action": "direct_output",
          "preset_response": "Your content violates our usage policy."
      }
      ```
  * `action=overridden`
    * ```
      {
          "flagged": true,
          "action": "overridden",
          "text": "I will *** you."
      }
      ```
## 代码示例
下面展示一段可部署在 Cloudflare 的 `src/index.ts` 代码。（Cloudflare 完整的使用方法参见[此文档](https://docs.dify.ai/zh-hans/guides/extension/api-based-extension/cloudflare-workers)）

代码工作原理是进行关键词匹配，实现对 Input （用户输入的内容）以及输出（大模型返回的内容）进行过滤。用户可以按照需求自行修改匹配逻辑。
```
import { Hono } from "hono";
import { bearerAuth } from "hono/bearer-auth";
import { z } from "zod";
import { zValidator } from "@hono/zod-validator";
import { generateSchema } from '@anatine/zod-openapi';

type Bindings = {
  TOKEN: string;
};

const app = new Hono<{ Bindings: Bindings }>();

// API 格式校验 ⬇️
const schema = z.object({
  point: z.union([
    z.literal("ping"),
    z.literal("app.external_data_tool.query"),
    z.literal("app.moderation.input"),
    z.literal("app.moderation.output"),
  ]), // Restricts 'point' to two specific values
  params: z
    .object({
      app_id: z.string().optional(),
      tool_variable: z.string().optional(),
      inputs: z.record(z.any()).optional(),
      query: z.any(),
      text: z.any()
    })
    .optional(),
});


// Generate OpenAPI schema
app.get("/", (c) => {
  return c.json(generateSchema(schema));
});

app.post(
  "/",
  (c, next) => {
    const auth = bearerAuth({ token: c.env.TOKEN });
    return auth(c, next);
  },
  zValidator("json", schema),
  async (c) => {
    const { point, params } = c.req.valid("json");
    if (point === "ping") {
      return c.json({
        result: "pong",
      });
    }
    // ⬇️ impliment your logic here ⬇️
    // point === "app.external_data_tool.query"
    else if (point === "app.moderation.input"){
    // 输入检查 ⬇️
    const inputkeywords = ["输入过滤测试1", "输入过滤测试2", "输入过滤测试3"];

    if (inputkeywords.some(keyword => params.query.includes(keyword))) 
      {
      return c.json({
        "flagged": true,
        "action": "direct_output",
        "preset_response": "输入存在违法内容，请换个问题再试！"
      });
    } else {
      return c.json({
        "flagged": false,
        "action": "direct_output",
        "preset_response": "输入无异常"
      });
    }
    // 输入检查完毕 
    }
    
    else {
      // 输出检查 ⬇️
      const outputkeywords = ["输出过滤测试1", "输出过滤测试2", "输出过滤测试3"]; 

  if (outputkeywords.some(keyword => params.text.includes(keyword))) 
    {
      return c.json({
        "flagged": true,
        "action": "direct_output",
        "preset_response": "输出存在敏感内容，已被系统过滤，请换个问题再问！"
      });
    }
  
  else {
    return c.json({
      "flagged": false,
      "action": "direct_output",
      "preset_response": "输出无异常"
    });
  };
    }
    // 输出检查完毕 
  }
);

export default app;

```

# 增加新供应商

供应商支持三种模型配置方式：

*   `predefined-model`预定义模型

    表示用户只需要配置统一的供应商凭据即可使用供应商下的预定义模型。
*   `customizable-model`自定义模型

    用户需要新增每个模型的凭据配置，如 Xinference，它同时支持 LLM 和 Text Embedding，但是每个模型都有唯一的 **model\_uid**，如果想要将两者同时接入，就需要为每个模型配置一个 **model\_uid**。
*   `fetch-from-remote`从远程获取

    与 `predefined-model`配置方式一致，只需要配置统一的供应商凭据即可，模型通过凭据信息从供应商获取。

    如OpenAI，我们可以基于 gpt-turbo-3.5 来 Fine Tune 多个模型，而他们都位于同一个 **api\_key** 下，当配置为`fetch-from-remote`时，开发者只需要配置统一的 **api\_key** 即可让 Dify Runtime 获取到开发者所有的微调模型并接入 Dify。

这三种配置方式**支持共存**，即存在供应商支持`predefined-model` + `customizable-model` 或 `predefined-model` + `fetch-from-remote`等，也就是配置了供应商统一凭据可以使用预定义模型和从远程获取的模型，若新增了模型，则可以在此基础上额外使用自定义的模型。

### 开始

#### 介绍

**名词解释**

* `module`: 一个`module`即为一个Python Package，或者通俗一点，称为一个文件夹，里面包含了一个`__init__.py`文件，以及其他的`.py`文件。

**步骤**

新增一个供应商主要分为几步，这里简单列出，帮助大家有一个大概的认识，具体的步骤会在下面详细介绍。

* 创建供应商 yaml 文件，根据 [Provider Schema](#user-content-fn-1)[^1] 编写。
* 创建供应商代码，实现一个`class`。
* 根据模型类型，在供应商`module`下创建对应的模型类型 `module`，如`llm`或`text_embedding`。
* 根据模型类型，在对应的模型`module`下创建同名的代码文件，如`llm.py`，并实现一个`class`。
* 如果有预定义模型，根据模型名称创建同名的yaml文件在模型`module`下，如`claude-2.1.yaml`，根据 [AI Model Entity](#user-content-fn-2)[^2] 编写。
* 编写测试代码，确保功能可用。

#### 开始吧

增加一个新的供应商需要先确定供应商的英文标识，如 `anthropic`，使用该标识在 `model_providers` 创建以此为名称的 `module`。

在此 `module` 下，我们需要先准备供应商的 YAML 配置。

**准备供应商 YAML**

此处以 `Anthropic` 为例，预设了供应商基础信息、支持的模型类型、配置方式、凭据规则。

```YAML
provider: anthropic  # 供应商标识
label:  # 供应商展示名称，可设置 en_US 英文、zh_Hans 中文两种语言，zh_Hans 不设置将默认使用 en_US。
  en_US: Anthropic
icon_small:  # 供应商小图标，存储在对应供应商实现目录下的 _assets 目录，中英文策略同 label
  en_US: icon_s_en.png
icon_large:  # 供应商大图标，存储在对应供应商实现目录下的 _assets 目录，中英文策略同 label
  en_US: icon_l_en.png
supported_model_types:  # 支持的模型类型，Anthropic 仅支持 LLM
- llm
configurate_methods:  # 支持的配置方式，Anthropic 仅支持预定义模型
- predefined-model
provider_credential_schema:  # 供应商凭据规则，由于 Anthropic 仅支持预定义模型，则需要定义统一供应商凭据规则
  credential_form_schemas:  # 凭据表单项列表
  - variable: anthropic_api_key  # 凭据参数变量名
    label:  # 展示名称
      en_US: API Key
    type: secret-input  # 表单类型，此处 secret-input 代表加密信息输入框，编辑时只展示屏蔽后的信息。
    required: true  # 是否必填
    placeholder:  # PlaceHolder 信息
      zh_Hans: 在此输入您的 API Key
      en_US: Enter your API Key
  - variable: anthropic_api_url
    label:
      en_US: API URL
    type: text-input  # 表单类型，此处 text-input 代表文本输入框
    required: false
    placeholder:
      zh_Hans: 在此输入您的 API URL
      en_US: Enter your API URL
```

如果接入的供应商提供自定义模型，比如`OpenAI`提供微调模型，那么我们就需要添加`model_credential_schema`，以`OpenAI`为例：

```yaml
model_credential_schema:
  model: # 微调模型名称
    label:
      en_US: Model Name
      zh_Hans: 模型名称
    placeholder:
      en_US: Enter your model name
      zh_Hans: 输入模型名称
  credential_form_schemas:
  - variable: openai_api_key
    label:
      en_US: API Key
    type: secret-input
    required: true
    placeholder:
      zh_Hans: 在此输入您的 API Key
      en_US: Enter your API Key
  - variable: openai_organization
    label:
        zh_Hans: 组织 ID
        en_US: Organization
    type: text-input
    required: false
    placeholder:
      zh_Hans: 在此输入您的组织 ID
      en_US: Enter your Organization ID
  - variable: openai_api_base
    label:
      zh_Hans: API Base
      en_US: API Base
    type: text-input
    required: false
    placeholder:
      zh_Hans: 在此输入您的 API Base
      en_US: Enter your API Base
```

也可以参考`model_providers`目录下其他供应商目录下的[ YAML ](#user-content-fn-3)[^3]配置信息。

**实现供应商代码**

我们需要在`model_providers`下创建一个同名的python文件，如`anthropic.py`，并实现一个`class`，继承`__base.provider.Provider`基类，如`AnthropicProvider`。

**自定义模型供应商**

当供应商为Xinference等自定义模型供应商时，可跳过该步骤，仅创建一个空的`XinferenceProvider`类即可，并实现一个空的`validate_provider_credentials`方法，该方法并不会被实际使用，仅用作避免抽象类无法实例化。

```python
class XinferenceProvider(Provider):
    def validate_provider_credentials(self, credentials: dict) -> None:
        pass
```

**预定义模型供应商**

供应商需要继承 `__base.model_provider.ModelProvider` 基类，实现 `validate_provider_credentials` 供应商统一凭据校验方法即可，可参考 [AnthropicProvider](https://github.com/langgenius/dify-runtime/blob/main/lib/model\_providers/anthropic/anthropic.py)。

```python
def validate_provider_credentials(self, credentials: dict) -> None:
    """
    Validate provider credentials
    You can choose any validate_credentials method of model type or implement validate method by yourself,
    such as: get model list api

    if validate failed, raise exception

    :param credentials: provider credentials, credentials form defined in `provider_credential_schema`.
    """
```

当然也可以先预留 `validate_provider_credentials` 实现，在模型凭据校验方法实现后直接复用。

**增加模型**

**增加预定义模型 👈🏻**

对于预定义模型，我们可以通过简单定义一个 yaml，并通过实现调用代码来接入。

**增加自定义模型 👈🏻**

对于自定义模型，我们只需要实现调用代码即可接入，但是它需要处理的参数可能会更加复杂。

***

#### 测试

为了保证接入供应商/模型的可用性，编写后的每个方法均需要在 `tests` 目录中编写对应的集成测试代码。

依旧以 `Anthropic` 为例。

在编写测试代码前，需要先在 `.env.example` 新增测试供应商所需要的凭据环境变量，如：`ANTHROPIC_API_KEY`。

在执行前需要将 `.env.example` 复制为 `.env` 再执行。

**编写测试代码**

在 `tests` 目录下创建供应商同名的 `module`: `anthropic`，继续在此模块中创建 `test_provider.py` 以及对应模型类型的 test py 文件，如下所示：

```shell
.
├── __init__.py
├── anthropic
│   ├── __init__.py
│   ├── test_llm.py       # LLM 测试
│   └── test_provider.py  # 供应商测试
```

针对上面实现的代码的各种情况进行测试代码编写，并测试通过后提交代码。

[^1]: ## 配置规则

    * 供应商规则基于 Provider 实体。
    * 模型规则基于 AIModelEntity 实体。

    以下所有实体均基于 `Pydantic BaseModel`，可在 `entities` 模块中找到对应实体。

    #### Provider

    * `provider` (string) 供应商标识，如：`openai`
    * `label` (object) 供应商展示名称，i18n，可设置 `en_US` 英文、`zh_Hans` 中文两种语言
      * `zh_Hans` (string) \[optional] 中文标签名，`zh_Hans` 不设置将默认使用 `en_US`。
      * `en_US` (string) 英文标签名
    * `description` (object) \[optional] 供应商描述，i18n
      * `zh_Hans` (string) \[optional] 中文描述
      * `en_US` (string) 英文描述
    * `icon_small` (string) \[optional] 供应商小 ICON，存储在对应供应商实现目录下的 `_assets` 目录，中英文策略同 `label`
      * `zh_Hans` (string) \[optional] 中文 ICON
      * `en_US` (string) 英文 ICON
    * `icon_large` (string) \[optional] 供应商大 ICON，存储在对应供应商实现目录下的 \_assets 目录，中英文策略同 label
      * `zh_Hans` (string) \[optional] 中文 ICON
      * `en_US` (string) 英文 ICON
    * `background` (string) \[optional] 背景颜色色值，例：#FFFFFF，为空则展示前端默认色值。
    * `help` (object) \[optional] 帮助信息
      * `title` (object) 帮助标题，i18n
        * `zh_Hans` (string) \[optional] 中文标题
        * `en_US` (string) 英文标题
      * `url` (object) 帮助链接，i18n
        * `zh_Hans` (string) \[optional] 中文链接
        * `en_US` (string) 英文链接
    * `supported_model_types` (array\[ModelType]) 支持的模型类型
    * `configurate_methods` (array\[ConfigurateMethod]) 配置方式
    * `provider_credential_schema` (ProviderCredentialSchema) 供应商凭据规格
    * `model_credential_schema` (ModelCredentialSchema) 模型凭据规格

    #### AIModelEntity

    * `model` (string) 模型标识，如：`gpt-3.5-turbo`
    * `label` (object) \[optional] 模型展示名称，i18n，可设置 `en_US` 英文、`zh_Hans` 中文两种语言
      * `zh_Hans` (string) \[optional] 中文标签名
      * `en_US` (string) 英文标签名
    * `model_type` (ModelType) 模型类型
    * `features` (array\[ModelFeature]) \[optional] 支持功能列表
    * `model_properties` (object) 模型属性
      * `mode` (LLMMode) 模式 (模型类型 `llm` 可用)
      * `context_size` (int) 上下文大小 (模型类型 `llm` `text-embedding` 可用)
      * `max_chunks` (int) 最大分块数量 (模型类型 `text-embedding moderation` 可用)
      * `file_upload_limit` (int) 文件最大上传限制，单位：MB。（模型类型 `speech2text` 可用）
      * `supported_file_extensions` (string) 支持文件扩展格式，如：mp3,mp4（模型类型 `speech2text` 可用）
      * `default_voice` (string) 缺省音色，可选：alloy,echo,fable,onyx,nova,shimmer（模型类型 `tts` 可用）
      * `word_limit` (int) 单次转换字数限制，默认按段落分段（模型类型 `tts` 可用）
      * `audio_type` (string) 支持音频文件扩展格式，如：mp3,wav（模型类型 `tts` 可用）
      * `max_workers` (int) 支持文字音频转换并发任务数（模型类型 `tts` 可用）
      * `max_characters_per_chunk` (int) 每块最大字符数 (模型类型 `moderation` 可用)
    * `parameter_rules` (array\[ParameterRule]) \[optional] 模型调用参数规则
    * `pricing` (PriceConfig) \[optional] 价格信息
    * `deprecated` (bool) 是否废弃。若废弃，模型列表将不再展示，但已经配置的可以继续使用，默认 False。

    #### ModelType

    * `llm` 文本生成模型
    * `text-embedding` 文本 Embedding 模型
    * `rerank` Rerank 模型
    * `speech2text` 语音转文字
    * `tts` 文字转语音
    * `moderation` 审查

    #### ConfigurateMethod

    *   `predefined-model` 预定义模型

        表示用户只需要配置统一的供应商凭据即可使用供应商下的预定义模型。
    *   `customizable-model` 自定义模型

        用户需要新增每个模型的凭据配置。
    *   `fetch-from-remote` 从远程获取

        与 `predefined-model` 配置方式一致，只需要配置统一的供应商凭据即可，模型通过凭据信息从供应商获取。

    #### ModelFeature

    * `agent-thought` Agent 推理，一般超过 70B 有思维链能力。
    * `vision` 视觉，即：图像理解。

    #### FetchFrom

    * `predefined-model` 预定义模型
    * `fetch-from-remote` 远程模型

    #### LLMMode

    * `completion` 文本补全
    * `chat` 对话

    #### ParameterRule

    * `name` (string) 调用模型实际参数名
    *   `use_template` (string) \[optional] 使用模板

        默认预置了 5 种变量内容配置模板：

        * `temperature`
        * `top_p`
        * `frequency_penalty`
        * `presence_penalty`
        * `max_tokens`

        可在 use\_template 中直接设置模板变量名，将会使用 entities.defaults.PARAMETER\_RULE\_TEMPLATE 中的默认配置 不用设置除 `name` 和 `use_template` 之外的所有参数，若设置了额外的配置参数，将覆盖默认配置。 可参考 `openai/llm/gpt-3.5-turbo.yaml`。
    * `label` (object) \[optional] 标签，i18n
      * `zh_Hans`(string) \[optional] 中文标签名
      * `en_US` (string) 英文标签名
    * `type`(string) \[optional] 参数类型
      * `int` 整数
      * `float` 浮点数
      * `string` 字符串
      * `boolean` 布尔型
    * `help` (string) \[optional] 帮助信息
      * `zh_Hans` (string) \[optional] 中文帮助信息
      * `en_US` (string) 英文帮助信息
    * `required` (bool) 是否必填，默认 False。
    * `default`(int/float/string/bool) \[optional] 默认值
    * `min`(int/float) \[optional] 最小值，仅数字类型适用
    * `max`(int/float) \[optional] 最大值，仅数字类型适用
    * `precision`(int) \[optional] 精度，保留小数位数，仅数字类型适用
    * `options` (array\[string]) \[optional] 下拉选项值，仅当 `type` 为 `string` 时适用，若不设置或为 null 则不限制选项值

    #### PriceConfig

    * `input` (float) 输入单价，即 Prompt 单价
    * `output` (float) 输出单价，即返回内容单价
    * `unit` (float) 价格单位，如：每 100K 的单价为 `0.000001`
    * `currency` (string) 货币单位

    #### ProviderCredentialSchema

    * `credential_form_schemas` (array\[CredentialFormSchema]) 凭据表单规范

    #### ModelCredentialSchema

    * `model` (object) 模型标识，变量名默认 `model`
      * `label` (object) 模型表单项展示名称
        * `en_US` (string) 英文
        * `zh_Hans`(string) \[optional] 中文
      * `placeholder` (object) 模型提示内容
        * `en_US`(string) 英文
        * `zh_Hans`(string) \[optional] 中文
    * `credential_form_schemas` (array\[CredentialFormSchema]) 凭据表单规范

    #### CredentialFormSchema

    * `variable` (string) 表单项变量名
    * `label` (object) 表单项标签名
      * `en_US`(string) 英文
      * `zh_Hans` (string) \[optional] 中文
    * `type` (FormType) 表单项类型
    * `required` (bool) 是否必填
    * `default`(string) 默认值
    * `options` (array\[FormOption]) 表单项为 `select` 或 `radio` 专有属性，定义下拉内容
    * `placeholder`(object) 表单项为 `text-input` 专有属性，表单项 PlaceHolder
      * `en_US`(string) 英文
      * `zh_Hans` (string) \[optional] 中文
    * `max_length` (int) 表单项为`text-input`专有属性，定义输入最大长度，0 为不限制。
    * `show_on` (array\[FormShowOnObject]) 当其他表单项值符合条件时显示，为空则始终显示。

    #### FormType

    * `text-input` 文本输入组件
    * `secret-input` 密码输入组件
    * `select` 单选下拉
    * `radio` Radio 组件
    * `switch` 开关组件，仅支持 `true` 和 `false`

    #### FormOption

    * `label` (object) 标签
      * `en_US`(string) 英文
      * `zh_Hans`(string) \[optional] 中文
    * `value` (string) 下拉选项值
    * `show_on` (array\[FormShowOnObject]) 当其他表单项值符合条件时显示，为空则始终显示。

    #### FormShowOnObject

    * `variable` (string) 其他表单项变量名
    * `value` (string) 其他表单项变量值

[^2]: ## 配置规则

    * 供应商规则基于 Provider 实体。
    * 模型规则基于 AIModelEntity 实体。

    以下所有实体均基于 `Pydantic BaseModel`，可在 `entities` 模块中找到对应实体。

    #### Provider

    * `provider` (string) 供应商标识，如：`openai`
    * `label` (object) 供应商展示名称，i18n，可设置 `en_US` 英文、`zh_Hans` 中文两种语言
      * `zh_Hans` (string) \[optional] 中文标签名，`zh_Hans` 不设置将默认使用 `en_US`。
      * `en_US` (string) 英文标签名
    * `description` (object) \[optional] 供应商描述，i18n
      * `zh_Hans` (string) \[optional] 中文描述
      * `en_US` (string) 英文描述
    * `icon_small` (string) \[optional] 供应商小 ICON，存储在对应供应商实现目录下的 `_assets` 目录，中英文策略同 `label`
      * `zh_Hans` (string) \[optional] 中文 ICON
      * `en_US` (string) 英文 ICON
    * `icon_large` (string) \[optional] 供应商大 ICON，存储在对应供应商实现目录下的 \_assets 目录，中英文策略同 label
      * `zh_Hans` (string) \[optional] 中文 ICON
      * `en_US` (string) 英文 ICON
    * `background` (string) \[optional] 背景颜色色值，例：#FFFFFF，为空则展示前端默认色值。
    * `help` (object) \[optional] 帮助信息
      * `title` (object) 帮助标题，i18n
        * `zh_Hans` (string) \[optional] 中文标题
        * `en_US` (string) 英文标题
      * `url` (object) 帮助链接，i18n
        * `zh_Hans` (string) \[optional] 中文链接
        * `en_US` (string) 英文链接
    * `supported_model_types` (array\[ModelType]) 支持的模型类型
    * `configurate_methods` (array\[ConfigurateMethod]) 配置方式
    * `provider_credential_schema` (ProviderCredentialSchema) 供应商凭据规格
    * `model_credential_schema` (ModelCredentialSchema) 模型凭据规格

    #### AIModelEntity

    * `model` (string) 模型标识，如：`gpt-3.5-turbo`
    * `label` (object) \[optional] 模型展示名称，i18n，可设置 `en_US` 英文、`zh_Hans` 中文两种语言
      * `zh_Hans` (string) \[optional] 中文标签名
      * `en_US` (string) 英文标签名
    * `model_type` (ModelType) 模型类型
    * `features` (array\[ModelFeature]) \[optional] 支持功能列表
    * `model_properties` (object) 模型属性
      * `mode` (LLMMode) 模式 (模型类型 `llm` 可用)
      * `context_size` (int) 上下文大小 (模型类型 `llm` `text-embedding` 可用)
      * `max_chunks` (int) 最大分块数量 (模型类型 `text-embedding moderation` 可用)
      * `file_upload_limit` (int) 文件最大上传限制，单位：MB。（模型类型 `speech2text` 可用）
      * `supported_file_extensions` (string) 支持文件扩展格式，如：mp3,mp4（模型类型 `speech2text` 可用）
      * `default_voice` (string) 缺省音色，可选：alloy,echo,fable,onyx,nova,shimmer（模型类型 `tts` 可用）
      * `word_limit` (int) 单次转换字数限制，默认按段落分段（模型类型 `tts` 可用）
      * `audio_type` (string) 支持音频文件扩展格式，如：mp3,wav（模型类型 `tts` 可用）
      * `max_workers` (int) 支持文字音频转换并发任务数（模型类型 `tts` 可用）
      * `max_characters_per_chunk` (int) 每块最大字符数 (模型类型 `moderation` 可用)
    * `parameter_rules` (array\[ParameterRule]) \[optional] 模型调用参数规则
    * `pricing` (PriceConfig) \[optional] 价格信息
    * `deprecated` (bool) 是否废弃。若废弃，模型列表将不再展示，但已经配置的可以继续使用，默认 False。

    #### ModelType

    * `llm` 文本生成模型
    * `text-embedding` 文本 Embedding 模型
    * `rerank` Rerank 模型
    * `speech2text` 语音转文字
    * `tts` 文字转语音
    * `moderation` 审查

    #### ConfigurateMethod

    *   `predefined-model` 预定义模型

        表示用户只需要配置统一的供应商凭据即可使用供应商下的预定义模型。
    *   `customizable-model` 自定义模型

        用户需要新增每个模型的凭据配置。
    *   `fetch-from-remote` 从远程获取

        与 `predefined-model` 配置方式一致，只需要配置统一的供应商凭据即可，模型通过凭据信息从供应商获取。

    #### ModelFeature

    * `agent-thought` Agent 推理，一般超过 70B 有思维链能力。
    * `vision` 视觉，即：图像理解。

    #### FetchFrom

    * `predefined-model` 预定义模型
    * `fetch-from-remote` 远程模型

    #### LLMMode

    * `completion` 文本补全
    * `chat` 对话

    #### ParameterRule

    * `name` (string) 调用模型实际参数名
    *   `use_template` (string) \[optional] 使用模板

        默认预置了 5 种变量内容配置模板：

        * `temperature`
        * `top_p`
        * `frequency_penalty`
        * `presence_penalty`
        * `max_tokens`

        可在 use\_template 中直接设置模板变量名，将会使用 entities.defaults.PARAMETER\_RULE\_TEMPLATE 中的默认配置 不用设置除 `name` 和 `use_template` 之外的所有参数，若设置了额外的配置参数，将覆盖默认配置。 可参考 `openai/llm/gpt-3.5-turbo.yaml`。
    * `label` (object) \[optional] 标签，i18n
      * `zh_Hans`(string) \[optional] 中文标签名
      * `en_US` (string) 英文标签名
    * `type`(string) \[optional] 参数类型
      * `int` 整数
      * `float` 浮点数
      * `string` 字符串
      * `boolean` 布尔型
    * `help` (string) \[optional] 帮助信息
      * `zh_Hans` (string) \[optional] 中文帮助信息
      * `en_US` (string) 英文帮助信息
    * `required` (bool) 是否必填，默认 False。
    * `default`(int/float/string/bool) \[optional] 默认值
    * `min`(int/float) \[optional] 最小值，仅数字类型适用
    * `max`(int/float) \[optional] 最大值，仅数字类型适用
    * `precision`(int) \[optional] 精度，保留小数位数，仅数字类型适用
    * `options` (array\[string]) \[optional] 下拉选项值，仅当 `type` 为 `string` 时适用，若不设置或为 null 则不限制选项值

    #### PriceConfig

    * `input` (float) 输入单价，即 Prompt 单价
    * `output` (float) 输出单价，即返回内容单价
    * `unit` (float) 价格单位，如：每 100K 的单价为 `0.000001`
    * `currency` (string) 货币单位

    #### ProviderCredentialSchema

    * `credential_form_schemas` (array\[CredentialFormSchema]) 凭据表单规范

    #### ModelCredentialSchema

    * `model` (object) 模型标识，变量名默认 `model`
      * `label` (object) 模型表单项展示名称
        * `en_US` (string) 英文
        * `zh_Hans`(string) \[optional] 中文
      * `placeholder` (object) 模型提示内容
        * `en_US`(string) 英文
        * `zh_Hans`(string) \[optional] 中文
    * `credential_form_schemas` (array\[CredentialFormSchema]) 凭据表单规范

    #### CredentialFormSchema

    * `variable` (string) 表单项变量名
    * `label` (object) 表单项标签名
      * `en_US`(string) 英文
      * `zh_Hans` (string) \[optional] 中文
    * `type` (FormType) 表单项类型
    * `required` (bool) 是否必填
    * `default`(string) 默认值
    * `options` (array\[FormOption]) 表单项为 `select` 或 `radio` 专有属性，定义下拉内容
    * `placeholder`(object) 表单项为 `text-input` 专有属性，表单项 PlaceHolder
      * `en_US`(string) 英文
      * `zh_Hans` (string) \[optional] 中文
    * `max_length` (int) 表单项为`text-input`专有属性，定义输入最大长度，0 为不限制。
    * `show_on` (array\[FormShowOnObject]) 当其他表单项值符合条件时显示，为空则始终显示。

    #### FormType

    * `text-input` 文本输入组件
    * `secret-input` 密码输入组件
    * `select` 单选下拉
    * `radio` Radio 组件
    * `switch` 开关组件，仅支持 `true` 和 `false`

    #### FormOption

    * `label` (object) 标签
      * `en_US`(string) 英文
      * `zh_Hans`(string) \[optional] 中文
    * `value` (string) 下拉选项值
    * `show_on` (array\[FormShowOnObject]) 当其他表单项值符合条件时显示，为空则始终显示。

    #### FormShowOnObject

    * `variable` (string) 其他表单项变量名
    * `value` (string) 其他表单项变量值

[^3]: Provider

    * `provider` (string) 供应商标识，如：`openai`
    * `label` (object) 供应商展示名称，i18n，可设置 `en_US` 英文、`zh_Hans` 中文两种语言
      * `zh_Hans` (string) \[optional] 中文标签名，`zh_Hans` 不设置将默认使用 `en_US`。
      * `en_US` (string) 英文标签名
    * `description` (object) \[optional] 供应商描述，i18n
      * `zh_Hans` (string) \[optional] 中文描述
      * `en_US` (string) 英文描述
    * `icon_small` (string) \[optional] 供应商小 ICON，存储在对应供应商实现目录下的 `_assets` 目录，中英文策略同 `label`
      * `zh_Hans` (string) \[optional] 中文 ICON
      * `en_US` (string) 英文 ICON
    * `icon_large` (string) \[optional] 供应商大 ICON，存储在对应供应商实现目录下的 \_assets 目录，中英文策略同 label
      * `zh_Hans` (string) \[optional] 中文 ICON
      * `en_US` (string) 英文 ICON
    * `background` (string) \[optional] 背景颜色色值，例：#FFFFFF，为空则展示前端默认色值。
    * `help` (object) \[optional] 帮助信息
      * `title` (object) 帮助标题，i18n
        * `zh_Hans` (string) \[optional] 中文标题
        * `en_US` (string) 英文标题
      * `url` (object) 帮助链接，i18n
        * `zh_Hans` (string) \[optional] 中文链接
        * `en_US` (string) 英文链接
    * `supported_model_types` (array\[ModelType]) 支持的模型类型
    * `configurate_methods` (array\[ConfigurateMethod]) 配置方式
    * `provider_credential_schema` (ProviderCredentialSchema) 供应商凭据规格
    * `model_credential_schema` (ModelCredentialSchema) 模型凭据规格

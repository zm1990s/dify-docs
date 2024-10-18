# LLM

### Definition

Invoke large language models to answer questions or process natural language.

<figure><img src="../../../.gitbook/assets/llm-node-1.png" alt=""><figcaption><p>LLM Node</p></figcaption></figure>

***

### Scenarios

LLM is the core node of Chatflow/Workflow, utilizing the conversational/generative/classification/processing capabilities of large language models to handle a wide range of tasks based on given prompts and can be used in different stages of workflows.

* **Intent Recognition**: In customer service scenarios, identifying and classifying user inquiries to guide downstream processes.
* **Text Generation**: In content creation scenarios, generating relevant text based on themes and keywords.
* **Content Classification**: In email batch processing scenarios, automatically categorizing emails, such as inquiries/complaints/spam.
* **Text Conversion**: In translation scenarios, translating user-provided text into a specified language.
* **Code Generation**: In programming assistance scenarios, generating specific business code or writing test cases based on user requirements.
* **RAG**: In knowledge base Q\&A scenarios, reorganizing retrieved relevant knowledge to respond to user questions.
* **Image Understanding**: Using multimodal models with vision capabilities to understand and answer questions about the information within images.

By selecting the appropriate model and writing prompts, you can build powerful and reliable solutions within Chatflow/Workflow.

***

### How to Configure

<figure><img src="../../../.gitbook/assets/llm-node-2.png" alt=""><figcaption><p>LLM Node Configuration - Model Selection</p></figcaption></figure>

**Configuration Steps:**

1. **Select a Model**: Dify supports major global models, including OpenAI's GPT series, Anthropic's Claude series, and Google's Gemini series. Choosing a model depends on its inference capability, cost, response speed, context window, etc. You need to select a suitable model based on the scenario requirements and task type.
2. **Configure Model Parameters**: Model parameters control the generation results, such as temperature, TopP, maximum tokens, response format, etc. To facilitate selection, the system provides three preset parameter sets: Creative, Balanced, and Precise.
3. **Write Prompts**: The LLM node offers an easy-to-use prompt composition page. Selecting a chat model or completion model will display different prompt composition structures.
4. **Advanced Settings**: You can enable memory, set memory windows, and use the Jinja-2 template language for more complex prompts.

{% hint style="info" %}
If you are using Dify for the first time, you need to complete the [model configuration](../../model-configuration/) in **System Settings—Model Providers** before selecting a model in the LLM node.
{% endhint %}

#### **Writing Prompts**

In the LLM node, you can customize the model input prompts. If you select a chat model, you can customize the SYSTEM/User/ASSISTANT sections.

**Prompt Generator**

If you're struggling to come up with effective system prompts (SYSTEM), you can use the Prompt Generator to quickly create prompts suitable for your specific business scenarios, leveraging AI capabilities.

<figure><img src="../../../.gitbook/assets/en-prompt-generator.png" alt="" width="352"><figcaption></figcaption></figure>

In the prompt editor, you can call out the **variable insertion menu** by typing **"/"** or **"{"** to insert **special variable blocks** or **upstream node variables** into the prompt as context content.

<figure><img src="../../../.gitbook/assets/llm-node-3.png" alt="" width="366"><figcaption><p>Calling Out the Variable Insertion Menu</p></figcaption></figure>

***

### Explanation of Special Variables

**Context Variables**

Context variables are a special type of variable defined within the LLM node, used to insert externally retrieved text content into the prompt.

<figure><img src="../../../.gitbook/assets/llm-node-4.png" alt=""><figcaption><p>Context Variables</p></figcaption></figure>

In common knowledge base Q\&A applications, the downstream node of knowledge retrieval is typically the LLM node. The **output variable** `result` of knowledge retrieval needs to be configured in the **context variable** within the LLM node for association and assignment. After association, inserting the **context variable** at the appropriate position in the prompt can incorporate the externally retrieved knowledge into the prompt.

This variable can be used not only as external knowledge introduced into the prompt context for LLM responses but also supports the application's [**citation and attribution**](../../knowledge-base/retrieval\_test\_and\_citation.md#id-2-yin-yong-yu-gui-shu) feature due to its data structure containing segment reference information.

{% hint style="info" %}
If the context variable is associated with a common variable from an upstream node, such as a string type variable from the start node, the context variable can still be used as external knowledge, but the **citation and attribution** feature will be disabled.
{% endhint %}

**Conversation History**

To achieve conversational memory in text completion models (e.g., gpt-3.5-turbo-Instruct), Dify designed the conversation history variable in the original [Prompt Expert Mode (discontinued)](../../../learn-more/extended-reading/prompt-engineering/prompt-engineering-1/). This variable is carried over to the LLM node in Chatflow, used to insert chat history between the AI and the user into the prompt, helping the LLM understand the context of the conversation.

{% hint style="info" %}
The conversation history variable is not widely used and can only be inserted when selecting text completion models in Chatflow.
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (204).png" alt=""><figcaption><p>Inserting Conversation History Variable</p></figcaption></figure>

**Model Parameters**

The parameters of the model affect the output of the model. Different models have different parameters. The following figure shows the parameter list for `gpt-4`.

<figure><img src="../../../.gitbook/assets/截屏2024-10-18 11.35.17.png" alt="" width="363"><figcaption></figcaption></figure>

The main parameter terms are explained as follows:

**Temperature**: Usually a value between 0-1, it controls randomness. The closer the temperature is to 0, the more certain and repetitive the results; the closer it is to 1, the more random the results.

**Top P**: Controls the diversity of the results. The model selects from candidate words based on probability, ensuring that the cumulative probability does not exceed the preset threshold P.

**Presence Penalty**: Used to reduce the repetitive generation of the same entity or information by imposing penalties on content that has already been generated, making the model inclined to generate new or different content. As the parameter value increases, greater penalties are applied in subsequent generations to content that has already been generated, lowering the likelihood of repeating content.

**Frequency Penalty**: Imposes penalties on words or phrases that appear too frequently by reducing their probability of generation. With an increase in parameter value, greater penalties are imposed on frequently occurring words or phrases. Higher parameter values reduce the frequency of these words, thereby increasing the lexical diversity of the text.

If you do not understand what these parameters are, you can choose to load presets and select from the three presets: Creative, Balanced, and Precise.

<figure><img src="../../../.gitbook/assets/截屏2024-10-18 11.37.43.png" alt="" width="364"><figcaption></figcaption></figure>

***

### Advanced Features

**Memory**: When enabled, each input to the intent classifier will include chat history from the conversation to help the LLM understand the context and improve question comprehension in interactive dialogues.

**Memory Window**: When the memory window is closed, the system dynamically filters the amount of chat history passed based on the model's context window; when open, users can precisely control the amount of chat history passed (in terms of numbers).

**Conversation Role Name Settings**: Due to differences in model training stages, different models adhere to role name instructions differently, such as Human/Assistant, Human/AI, Human/Assistant, etc. To adapt to the prompt response effects of multiple models, the system provides conversation role name settings. Modifying the role name will change the role prefix in the conversation history.

**Jinja-2 Templates**: The LLM prompt editor supports Jinja-2 template language, allowing you to leverage this powerful Python template language for lightweight data transformation and logical processing. Refer to the [official documentation](https://jinja.palletsprojects.com/en/3.1.x/templates/).

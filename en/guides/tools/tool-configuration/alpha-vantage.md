# AlphaVantage Stock Analysis

> Tool author [@zhuhao](https://github.com/hwzhuhao).

AlphaVantage is an online platform that provides financial market data and APIs, making it convenient for individual investors and developers to access stock quotes, technical indicators, and stock analysis.

## 1. Apply for AlphaVantage API Key

Please apply for an API Key at [AlphaVantage](https://www.alphavantage.co/support/#api-key).

## 2. Fill in the configuration in Dify

In the Dify navigation page, click on `Tools > AlphaVantage > Go to authorize` to fill in the API Key.

## 3. Using the tool

- **Chatflow / Workflow applications**

Both Chatflow and Workflow applications support adding `AlphaVantage` tool nodes. After adding, you need to use [variables](https://docs.dify.ai/guides/workflow/variables) to reference the user's input query in the "Input Variables → Stock Code" section within the node. Finally, use variables to reference the output content of the `AlphaVantage` node in the "End" node.

- **Agent applications**

Add the `AlphaVantage` tool in the Agent application, then send stock descriptions in the chat box to invoke the tool and obtain accurate financial data.
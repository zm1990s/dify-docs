# Deploy Dify to Zeabur

[Zeabur](https://zeabur.com) is a cloud platform that allows you to deploy Dify with one click. This guide will walk you through the process of deploying Dify to Zeabur.

## Prerequisites

Before you begin, you'll need the following:

- A Zeabur account. If you don't have one, you can sign up for free at [Zeabur](https://zeabur.com/).
- Upgrade your Zeabur account to Developer Plan($5 per month). You can upgrade your account from the [Zeabur Pricing](https://zeabur.com/pricing) page.

## Deploy Dify to Zeabur

There is a one-click deploy template for Dify on Zeabur. To get started, just press the button below:

[![Deploy to Zeabur](https://zeabur.com/button.svg)](https://zeabur.com/1D4DOW)

After clicking the button, you'll be navigated to the template page on Zeabur where you can see the details and instructions for deployment.

<figure><img src="../../.gitbook/assets/zeabur-template-overview.jpeg" alt="Zeabur Template Overview"><figcaption></figcaption></figure>

Press on the Deploy button, you need to input a generated domain so that the domain can be binded to your Dify instance and inject to other services as environment variable. And then select your favourite region, press the deploy button, your Dify instance will be deployed in a few minutes.

<figure><img src="../../.gitbook/assets/zeabur-region-select.png" alt="Select Region"><figcaption></figcaption></figure>

After the deployment is done, you can see a project page in Zeabur dashboard like the following picture, and the domain you inputed in the deploying process will be binded to the NGINX service automatically, you can access your Dify instance through that domain. 

<figure><img src="../../.gitbook/assets/zeabur-project.png" alt="Zeabur Project Overview"><figcaption></figcaption></figure>

You can also change the domain in the Networking tab in NGINX service page. You can refer to the [Zeabur Documentation](https://zeabur.com/docs/deploy/domain-binding) for more information.
# Create Application

You can create applications in Dify's studio in three ways:

* Create based on an application template (recommended for beginners)
* Create a blank application
* Import via a DSL file

### Creating an Application from a Template

When using Dify for the first time, you might be unfamiliar with creating applications. To help new users quickly understand what types of applications can be built on Dify, the prompt engineers from the Dify team have already created high-quality application templates for multiple scenarios.

You can select "Studio" from the navigation menu, then choose "Create from Template" in the application list.

<figure><img src="../../.gitbook/assets/guides/application_orchestrate/creating-an-application/image (168).png" alt=""><figcaption><p>Create an application from a template</p></figcaption></figure>

Select any template and click **Use this template.**

<figure><img src="../../.gitbook/assets/guides/application_orchestrate/creating-an-application/image (169).png" alt=""><figcaption><p>Dify application templates</p></figcaption></figure>

### Creating a New Application

If you need to create a blank application on Dify, you can select "Studio" from the navigation and then choose "Create from Blank" in the application list.

<figure><img src="../../.gitbook/assets/guides/application_orchestrate/creating-an-application/image (167).png" alt=""><figcaption></figcaption></figure>

When creating an application for the first time, you might need to first understand the [basic concepts](./#application\_type) of the four different types of applications on Dify: Chatbot, Text Generator, Agent and Workflow.

When creating an application, you need to give it a name, choose an appropriate icon, and use clear and concise text to describe the purpose of this application, to facilitate its subsequent use within the team.

<figure><img src="../../.gitbook/assets/guides/application_orchestrate/creating-an-application/image (170).png" alt=""><figcaption><p>Create a blank application</p></figcaption></figure>

### Creating from a DSL File

If you have obtained a template (DSL file) from the community or others, you can choose "Import DSL File" from the studio. After importing, all configuration information of the original application will be loaded directly.

<figure><img src="../../.gitbook/assets/guides/application_orchestrate/creating-an-application/image (172).png" alt=""><figcaption><p>Create an application by importing a DSL file</p></figcaption></figure>

{% hint style="info" %}
Dify DSL is an AI application engineering file standard defined by Dify.AI in v0.6 and later. The file format is YML. This standard covers the basic description of the application, model parameters, orchestration configuration, and other information.
{% endhint %}

### Editing Application Information

After creating an application, if you want to modify the application name or description, you can click "Edit info" in the upper left corner of the application to revise the application's icon, name, or description.

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption><p>Edit App Info</p></figcaption></figure>

### Duplicating Application

All applications support copying. Click "Duplicate" in the upper left corner of the application.

### Exporting Application

Applications created in Dify can be exported in DSL format. You can freely import the configuration file into any Dify workspace.

{% hint style="info" %}
Dify DSL is an AI application engineering file standard defined by Dify.AI in v0.6 and later. The file format is YML. This standard covers the basic description of the application, model parameters, orchestration configuration, and other information.
{% endhint %}

### Deleting Application

If you want to remove an application, you can click "Delete" in the upper left corner of the application.

{% hint style="info" %}
⚠️ The deletion of an application cannot be undone. All users will be unable to access your application, and all prompts, orchestration configurations, and logs within the application will be deleted.
{% endhint %}

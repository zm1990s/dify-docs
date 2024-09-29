# Manage App

### Editing Application Information

After creating an application, if you want to modify the application name or description, you can click "Edit info" in the upper left corner of the application to revise the application's icon, name, or description.

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption><p>Edit App Info</p></figcaption></figure>

### Duplicating Application

All applications support copying. Click "Duplicate" in the upper left corner of the application.

### Switch to Workflow Orchestrate

TODO 🚧

### Exporting Application

Applications created in Dify support export in DSL format files, allowing you to import the configuration files into other Dify teams freely. You can export DSL files using either of the following two methods:

- Click "Export DSL" in the application menu button on the "Studio" page
- After entering the application's orchestration page, click "Export DSL" in the upper left corner

![](../../../img/export-dsl.png)

The DSL file does not include the following sensitive information:

- Authorization information for third-party tools, such as API Keys.
- If environment variables contain `Secret`, a prompt will appear during export asking whether to allow the export of sensitive information.

![](../../../img/export-dsl-secret.png)

{% hint style="info" %}
Dify DSL is an AI application engineering file standard defined by Dify.AI in v0.6 and later. The file format is YML. This standard covers the basic description of the application, model parameters, orchestration configuration, and other information.
{% endhint %}

### Deleting Application

If you want to remove an application, you can click "Delete" in the upper left corner of the application.

{% hint style="info" %}
⚠️ The deletion of an application cannot be undone. All users will be unable to access your application, and all prompts, orchestration configurations, and logs within the application will be deleted.
{% endhint %}

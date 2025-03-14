# Finetune models

# **[Preview]** Introducing Remote Development with AI Toolkit for VS Code

In addition to local development, the AI Toolkit for VS Code now supports remote development. This feature enables users to provision for Azure Container Apps to run model fine-tuning and inference endpoint in the cloud.

## Prerequisites
1. To run the model fine-tuning and inference in your remote Azure Container Apps Environment, make sure your subscription has enough GPU capacity. Submit a [support ticket](https://azure.microsoft.com/support/create-ticket/) to request the required capacity for your application. [Get More Info about GPU capacity](https://learn.microsoft.com/en-us/azure/container-apps/workload-profiles-overview)
2. Make sure you have a [HuggingFace account](https://huggingface.co/) and [generate an access token](https://huggingface.co/docs/hub/security-tokens) if you are using private dataset on HuggingFace or your base model needs access control.
3. Accept the LICENSE on HuggingFace if you are fine-tuning Mistral or Llama. 
4. Enable Remote Fine-tuning and Inference feature flag in the AI Toolkit for VS Code
   1. Open the VS Code Settings by selecting *File -> Preferences -> Settings*.
   2. Navigate to *Extensions* and select *AI Toolkit*.
   3. Select the *"Enable Remote Fine-tuning And Inference"* option.
   4. Reload VS Code for the changes to take effect.
   ![AI Toolkit Settings](Images/remote/settings.png)

## Setting Up a Remote Development Project
1. Execute the command palette `AI Toolkit: Focus on Resource View`.
![Command: Focus on Resource View](Images/remote/command-focus-resource-view.png)
2. Navigate to *Model Fine-tuning* to access the model catalog. Assign a name to your project and select its location on your machine. Then, hit the *"Configure Project"* button.
![Panel: Select Model](Images/remote/panel-select-model.png)
3. Project Configuration
    1. Avoid enabling the *"Fine-tune locally"* option.
    2. The Olive configuration settings will appear with pre-set default values. Please adjust and fill in these configurations as required.
    3. Move on to *Generate Project*. This stage leverages WSL and involves setting up a new Conda environment, preparing for future updates that include Dev Containers.
![Panel: Configure the Model](Images/remote/panel-config-model.png)
4. Click on *"Relaunch Window In Workspace"* to open your remote development project.
![Panel: Generate Project](Images/remote/panel-generate-project.png)

> **Note:** The project currently works either locally or remotely within the AI Toolkit for VS Code. If you choose *"Fine-tune locally"* during project creation, it will operate exclusively in WSL without remote development capabilities. On the other hand, if you forego enabling *"Fine-tune locally"*, the project will be restricted to the remote Azure Container App environment.

## What's Next
Refer to [Fine-Tuning models remotely](#fine-tuning-models-remotely) for instructions on how to fine-tune a model in Azure Container Apps.
To learn how to create an inference API endpoint in Azure Container Apps, see I[Inferencing with the fine-tuned model](#inferencing-with-the-fine-tuned-model).

# Fine-Tuning models remotely
Model fine-tuning in machine learning involves subtly adjusting an existing model, originally trained on a larger dataset, to perform a similar but new task using a smaller dataset. If you don't have local computing resources like a GPU, you can do this fine tuning remotely with AI Toolkit and Azure Container App.

## Provision Azure Resources
To get started, you need to provision the Azure Resource for remote fine-tuning. Do this by running the `AI Toolkit: Provision Azure Container Apps job for fine-tuning` from the command palette. During this process, you will be prompted to select your Azure Subscription and resource group.

![Provision Fine-Tuning](Images/remote/command-provision-finetune.png)

Monitor the progress of the provision through the link displayed in the output channel.
![Provision Progress](Images/remote/log-finetining-progress.png)

## Run
To start the remote fine-tuning job, execute the `AI Toolkit: Run fine-tuning` command.
![Run Fine-tuning](Images/remote/command-run-finetuning.png)

Upon running this command, the extension will do the following operations:
1. Synchronize your workspace with Azure Files.
1. Trigger the Azure Container Appjob using the commands specified in `./infra/fintuning.config.json`.

During this process, QLoRA will be used for fine-tuning, and will create LoRA adapters for the model to use during inference.

The results of the fine-tuning will be stored in the Azure Files.
To explore the output files in the Azure File share, you can navigate to the Azure portal using the link provided in the output panel. Alternatively, you can directly access the Azure portal and locate the storage account named `STORAGE_ACCOUNT_NAME` as defined in `./infra/fintuning.config.json` and the file share named `FILE_SHARE_NAME` as defined in `./infra/fintuning.config.json`.  

![file-share](Images/remote/log-finetuning-files.png)

### View Logs
Once the fine-tuning job has been started, you can access the system and console logs by visiting the Azure portal. 
Alternatively, you can view the console logs directly in the VSCode output panel.
> **Note:** The job might take a few minutes to initiate. If there is already a running job, the current one may be queued to start later.

![log-button](Images/remote/notification-finetune.png)

#### View and Query Logs on Azure

After fine-tuning job was triggered, you can view logs on Azure by clicking the "*Open Logs in Azure Portal*" button from the VSCode notification.

Or, if you've already opened the Azure Portal, find job history from the "*Execution history*" panel to the Azure Container Apps job.

![Job Execution History](Images/remote/finetune-job-history.png)

There are two types of logs, "*Console*" and "*System*".
- Console logs are messages from your app, including `stderr` and `stdout` messages. This is what you might have already seen in the streaming logs section.
- System logs are messages from the Container Apps service, including the status of service-level events.

To view and query your logs, click the "*Console*" button and navigate to the Log Analytics page where you can view all logs and write your queries.

![Job Log Analytics](Images/remote/finetune-job-log-query.png)


> For more information about Azure Container Apps Logs, see [Application Logging in Azure Container Apps](https://learn.microsoft.com/azure/container-apps/logging).


#### View streaming logs in VSCode
After initiating the fine-tuning job, you can also view logs on Azure by clicking on the "*Show Streaming Logs in VS Code*" button in the VSCode notification.
Or you can execute the command `AI Toolkit: Show the running fine-tuning job streaming logs`.
![Streaming Log Command](Images/remote/command-show-streaming-log.png)

The streaming log of the running fine-tuning job will be displayed in the output panel.

![Streaming Log Output](Images/remote/log-finetuning-res.png)

> **Note:** 
> 1. The job might be queued due to insufficient resources. If the log is not displayed, wait for a while and then execute the command to re-connect to the streaming log.
> 2. The streaming log may timeout and disconnect. However, it can be reconnected by execute the command again.

## Fine-tuning Components Included in the Template
 
| Folder | Contents |
| ------ |--------- |
| `infra` | Contains all necessary configurations for remote operations. |
| `infra/provision/finetuning.parameters.json` | Holds parameters for the bicep templates, used for provisioning Azure resources for fine-tuning. |
| `infra/provision/finetuning.bicep` | Contains templates for provisioning Azure resources for fine-tuning. |
| `infra/finetuning.config.json` |The configuration file, generated by the `AI Toolkit: Provision Azure Container Apps job for fine-tuning` command. It is used as input for other remote command palettes. |

## Advanced usage
### Configuring Secrets for fine-tuning in Azure Container Apps
Azure Container App Secrets provide a secure way to store and manage sensitive data within Azure Container Apps, like HuggingFace tokens and Weights & Biases API keys. Using AI toolkit's command palette, you can input the secrets into the provisioned Azure container app job(as stored in `./finetuning.config.json`). These secrets are then set as **environment variables** in all containers.

#### Steps:
1. In the Command Palette, type and select `AI Toolkit: Add Azure Container Apps Job secret for fine-tuning`
![Add secret](Images/remote/command-add-secret.png)

1. Input Secret Name and Value: You'll be prompted to input the name and value of the secret.
   ![Input secret name](Images/remote/input-secret-name.png)
   ![Input secret](Images/remote/input-secret.png)
   For example, if you're using private HuggingFace dataset or models that need Hugging Face access control, set your HuggingFace token as an environment variable [`HF_TOKEN`](https://huggingface.co/docs/huggingface_hub/package_reference/environment_variables#hftoken) to avoid the need for manual login on the Hugging Face Hub.

After you've set up the secret, you can now use it in your Azure Container App. The secret will be set in the environment variables of your container app.

### Configuring Azure Resource Provision
This guide will help you configure the `AI Toolkit: Provision Azure Container Apps job for fine-tuning` command.

You can find configuration parameters in `./infra/provision/finetuning.parameters.json` file. Here are the details:
| Parameter | Description |
| --------- |------------ |
| `defaultCommands` | This is the default command to start a fine-tuning job. It can be overwritten in `./infra/finetuning.config.json`. |
| `maximumInstanceCount` | This parameter sets the maximum capacity of GPU instances. |
| `timeout` | This sets the timeout for the Azure Container Appfine-tuning job in seconds. The default value is 10800, which equals to 3 hours. If the Azure Container Appjob reaches this timeout, the fine-tuning process halts. However, checkpoints are saved by default, allowing the fine-tuning process to resume from the last checkpoint instead of starting over if it is run again. |
| `location` | This is the location where Azure resources are provisioned. The default value is the same as the chosen resource group's location. |
| `storageAccountName`, `fileShareName` `acaEnvironmentName`, `acaEnvironmentStorageName`, `acaJobName`,  `acaLogAnalyticsName` | These parameters are used to name the Azure resources for provision. You can input a new, unused resource name to create your own custom-named resources, or you can input the name of an already existing Azure resource if you'd prefer to use that. For details, refer to the section [Using existing Azure Resources](#using-existing-azure-resources). |

#### Using existing Azure Resources
If you have existing Azure resources that need to be configured for fine-tuning, you can specify their names in the `./infra/provision/finetuning.parameters.json` file and then run the `AI Toolkit: Provision Azure Container Apps job for fine-tuning` from the command palette. This will update the resources you've specified and create any that are missing.

For example, if you have an existing Azure container environment, your `./infra/finetuning.parameters.json` should look like this:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      ...
      "acaEnvironmentName": {
        "value": "<your-aca-env-name>"
      },
      "acaEnvironmentStorageName": {
        "value": null
      },
      ...
    }
  }
```

### Manual Provision
If you prefer to manually set up the Azure resources, you can use the provided bicep files in the `./infra/provision` folders. If you've already set up and configured all the Azure resources without using the AI Toolkit command palette, you can simply enter the resource names in the `finetune.config.json` file.

For example:

```json
{
  "SUBSCRIPTION_ID": "<your-subscription-id>",
  "RESOURCE_GROUP_NAME": "<your-resource-group-name>",
  "STORAGE_ACCOUNT_NAME": "<your-storage-account-name>",
  "FILE_SHARE_NAME": "<your-file-share-name>",
  "ACA_JOB_NAME": "<your-aca-job-name>",
  "COMMANDS": [
    "cd /mount",
    "pip install huggingface-hub==0.22.2",
    "huggingface-cli download <your-model-name> --local-dir ./model-cache/<your-model-name> --local-dir-use-symlinks False",
    "pip install -r ./setup/requirements.txt",
    "python3 ./finetuning/invoke_olive.py && find models/ -print | grep adapter/adapter"
  ]
}
```


# Inferencing with the fine-tuned model
After the adapters are trained in the remote environment, use a simple Gradio application to interact with the model.

![Fine-tune complete](Images/remote/log-finetuning-res.png)

## Provision Azure Resources
Similar to the fine-tuning process, you need to set up the Azure Resources for remote inference by executing the `AI Toolkit: Provision Azure Container Apps for inference` from the command palette. During this setup, you will be asked to select your Azure Subscription and resource group.  
![Provision Inference Resource](Images/remote/command-provision-inference.png)
   
By default, the subscription and the resource group for inference should match those used for fine-tuning. The inference will use the same Azure Container App Environment and access the model and model adapter stored in Azure Files, which were generated during the fine-tuning step. 

## Deployment for Inference  
If you wish to revise the inference code or reload the inference model, please execute the `AI Toolkit: Deploy for inference` command. This will synchronize your latest code with ACA and restart the replica.  

![Deploy for inference](./Images/remote/command-deploy.png)

After the successful completion of the deployment, the model is now ready for evaluation using this endpoint.
You can access the inference API by clicking on the "*Go to Inference Endpoint*" button displayed in the VSCode notification. Alternatively, the web API endpoint can be found under `ACA_APP_ENDPOINT` in `./infra/inference.config.json` and in the output panel.

![App Endpoint](Images/remote/notification-deploy.png)

> **Note:** The inference endpoint may require a few minutes to become fully operational.

## Inference Components Included in the Template
 
| Folder | Contents |
| ------ |--------- |
| `infra` | Contains all necessary configurations for remote operations. |
| `infra/provision/inference.parameters.json` | Holds parameters for the bicep templates, used for provisioning Azure resources for inference. |
| `infra/provision/inference.bicep` | Contains templates for provisioning Azure resources for inference. |
| `infra/inference.config.json` |The configuration file, generated by the `AI Toolkit: Provision Azure Container Apps for inference` command. It is used as input for other remote command palettes. |

## Advanced usage
### Configuring Azure Resource Provision
This guide will help you configure the `AI Toolkit: Provision Azure Container Apps for inference` command.

You can find configuration parameters in `./infra/provision/inference.parameters.json` file. Here are the details:
| Parameter | Description |
| --------- |------------ |
| `defaultCommands` | This is the commands to initiate a web API. |
| `maximumInstanceCount` | This parameter sets the maximum capacity of GPU instances. |
| `location` | This is the location where Azure resources are provisioned. The default value is the same as the chosen resource group's location. |
| `storageAccountName`, `fileShareName` `acaEnvironmentName`, `acaEnvironmentStorageName`, `acaAppName`,  `acaLogAnalyticsName` | These parameters are used to name the Azure resources for provision. By default, they will be same to the fine-tuning resource name. You can input a new, unused resource name to create your own custom-named resources, or you can input the name of an already existing Azure resource if you'd prefer to use that. For details, refer to the section [Using existing Azure Resources](#using-existing-azure-resources). |

#### Using Existing Azure Resources
By default, the inference provision use the same Azure Container App Environment, Storage Account, Azure File Share, and Azure Log Analytics that were used for fine-tuning. A separate Azure Container App is created solely for the inference API. 

If you have customized the Azure resources during the fine-tuning step or want to use your own existing Azure resources for inference, specify their names in the `./infra/inference.parameters.json` file. Then, run the `AI Toolkit: Provision Azure Container Apps for inference` command from the command palette. This updates any specified resources and creates any that are missing.

For example, if you have an existing Azure container environment, your `./infra/finetuning.parameters.json` should look like this:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      ...
      "acaEnvironmentName": {
        "value": "<your-aca-env-name>"
      },
      "acaEnvironmentStorageName": {
        "value": null
      },
      ...
    }
  }
```

### Manual Provision  
If you prefer to manually configure the Azure resources, you can use the provided bicep files in the `./infra/provision` folders. If you have already set up and configured all the Azure resources without using the AI Toolkit command palette, you can simply enter the resource names in the `inference.config.json` file.

For example:

```json
{
  "SUBSCRIPTION_ID": "<your-subscription-id>",
  "RESOURCE_GROUP_NAME": "<your-resource-group-name>",
  "STORAGE_ACCOUNT_NAME": "<your-storage-account-name>",
  "FILE_SHARE_NAME": "<your-file-share-name>",
  "ACA_APP_NAME": "<your-aca-name>",
  "ACA_APP_ENDPOINT": "<your-aca-endpoint>"
}
```


# Explore an Azure Machine Learning Workspace

A workspace is a context for the experiments, data, compute targets, and other assets associated with a machine learning workload.

## Workspaces for Machine Learning Assets
A workspace defines the boundary for a set of related machine learning assets. You can use workspaces to group machine learning assets based on projects, deployment environments (for example, test and production), teams, or some other organizing principle. The assets in a workspace include:

* Compute targets for development, training, and deployment.
* Data for experimentation and model training.
* Notebooks containing shared code and documentation.
* Experiments, including run history with logged metrics and outputs.
* Pipelines that define orchestrated multi-step processes.
* Models that you have trained.

## Workspaces as Azure Resources
Workspaces are Azure resources, and as such they are defined within a resource group in an Azure subscription, along with other related Azure resources that are required to support the workspace

![](https://docs.microsoft.com/en-us/learn/wwl-data-ai/intro-to-azure-machine-learning-service/media/01-02-workspace.png)

The Azure resources created alongside a workspace include:

* A storage account - used to store files used by the workspace as well as data for experiments and model training.
* An Application Insights instance, used to monitor predictive services in the workspace.
* An Azure Key Vault instance, used to manage secrets such as authentication keys and credentials used by the workspace.
* A container registry, created as-needed to manage containers for deployed models.

### Connect to your Workspace and explore Azure ML stduio

You can manage some workspace assets in the Azure portal, but for data scientists, this tool contains lots of irrelevant information and links that relate to managing general Azure resources. Azure Machine Learning studio provides a dedicated web portal for working with your workspace.

1. In the Azure portal blade for your Azure Machine Learning workspace, click the link to launch studio; or alternatively, in a new browser tab, open https://ml.azure.com. If prompted, sign in using your Microsoft account and select your Azure subscription and workspace.

2. View the Azure Machine Learning studio interface for your workspace - you can manage all of the assets in your workspace from here.

3. In Azure Machine Learning studio, toggle the ☰ icon at the top left to show and hide the various pages in the interface. You can use these pages to manage the resources in your workspace. 


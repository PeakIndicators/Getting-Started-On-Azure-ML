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

### Create a compute instance

One of the benefits of Azure Machine Learning is the ability to create cloud-based compute (*Compute Instances*) in a workspace to provide a development environment that is managed with all of the other assets in the workspace. These compute instances enable you to run experiments and training scripts at scale.

![](https://docs.microsoft.com/en-us/learn/wwl-data-ai/intro-to-azure-machine-learning-service/media/01-05-notebook-vm.jpg)

1. In Azure Machine Learning studio, view the Compute page. This is where you’ll manage compute resources for your data science activities. There are four kinds of compute resource you can create:

* **Compute instances:** Development workstations that data scientists can use to work with data and models.
* **Compute clusters:**  Scalable clusters of virtual machines for on-demand processing of experiment code.
* **Inference clusters:** Deployment targets for predictive services that use your trained models.
* **Attached compute:** Links to other Azure compute resources, such as Virtual Machines or Azure Databricks clusters.

For most scenarios a compute instance is enough for developing and testing code.  As a development environment, a compute instance cannot, however, be shared with other users in your workspace—each individual will have to create their own compute instance. 

2. On the **Compute instances** tab, add a new compute instance with the following settings. You’ll use this as a workstation to run code in notebooks.

* **Region:** *The same region as your workspace*
* **Virtual machine type:** Select *CPU* for general use unless you know your code will use GPU (example for training deep learning models
* **Virtual machine size:** *Standard_DS11_v2*
* **Compute name:** *enter a unique name*
* **Enable SSH access:** Unselected (you can use this to enable direct access to the virtual machine using an SSH client)
* **Show advanced settings:** Note the following settings, but do not select them unless you think you requore them:
    * **Enable virtual network:** Unselected (you would typically use this in an enterprise environment to enhance network security)
    * **Assign to another user:** Unselected (you can use this to assign a compute instance to a data scientist)
  
3. Wait for the compute instance to start and its status to change to **Running**.
  


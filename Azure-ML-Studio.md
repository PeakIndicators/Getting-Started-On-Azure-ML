# How to access Azure Machine Learning Studio

Azure Machine Learning Studio is an Azure resources, and as such they are defined within a resource group in an Azure subscription, along with other related Azure resources that are required to support the workspace

![mlresources](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/azure-machine-learning-resources.png)

The Azure resources created alongside studio include:

* A storage account - used to store files used by the workspace as well as data for experiments and model training.
* An Application Insights instance, used to monitor predictive services in the workspace.
* An Azure Key Vault instance, used to manage secrets such as authentication keys and credentials used by the workspace.
* A container registry, created as-needed to manage containers for deployed models.

## Connect and explore Azure Machine Learning Studio

You can manage some studio assets in the Azure portal, but for data scientists, this tool contains lots of irrelevant information and links that relate to managing general Azure resources. Azure Machine Learning studio provides a dedicated web portal for working with your studio.

** Option 1 - Accessing Azure Machine Learning Studio through Azure Portal **

1. Access Azure Portal using the following: https://portal.azure.com/#home

2. You will be prompted with a user and password. Fill with the correct information

3. On the top search option write Subscriptions and press enter

4. Select the subscription you need to work on and the go to Resource Groups

5. Open the resource group your studio is attached to.

6. Select the Azure Machine Learning Studio you want to work.

7. Click on - Open Studio -

8. You will be redirected to the Azure Machine Learning studio interface - this is where you can all the studio assets.

9. In Azure Machine Learning studio, toggle the ☰ icon at the top left to show and hide the various pages in the interface. You can use these pages to manage the resources in your studio.
 

** Option 2 - Accessing Azure Machine Learning Studio diretly from Azure ML Studio web link **

1. In a browser tab, open https://ml.azure.com. If prompted, sign in using your Microsoft account and select your Azure subscription and workspace.

2. View the Azure Machine Learning studio interface for your workspace - you can manage all of the assets in your workspace from here.

3. In Azure Machine Learning studio, toggle the ☰ icon at the top left to show and hide the various pages in the interface. You can use these pages to manage the resources in your workspace.

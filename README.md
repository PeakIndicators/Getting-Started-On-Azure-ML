<p align="center">
  <img src="Images/azure%20ML%20logo.png">
</p>

# Getting Started On Azure Machine Learning Studio

Before getting into detail on how to work with Azure Machine Learning Studio (azure ML Studio), let's introduce what is the tool for. 

## What is machine learning?
Machine learning is a data science technique that allows computers to use existing data to forecast future behaviors, outcomes, and trends. By using machine learning, computers learn without being explicitly programmed. Forecasts or predictions from machine learning can make apps and devices smarter. 

## How can we perform machine learning tasks in Azure?
Among others, Azure has a resource called: Azure Machine Learning Studio, which is the web portal for data scientist developers in Azure Machine Learning. The studio combines no-code and code-first experiences for an inclusive data science platform.

With this in mind, the main purpose of this repository, is to establish a guide on how to get started with Azure Machine Learning Studio.

The ultimate goal is to provide a guide on:

* How to author machine learning projects in the studio.
* How to manage assets and resources in the studio.

We recommend the use of the most up-to-date browser that's compatible with your operating system. The following browsers are supported:

* Microsoft Edge (The new Microsoft Edge, latest version. Not Microsoft Edge legacy)
* Safari (latest version, Mac only)
* Chrome (latest version)
* Firefox (latest version)

We will also re-use some of Microsoft documentation (see: https://docs.microsoft.com/en-us/azure/machine-learning/) on the subject but we will try to present it in a structured way. This repo contains snippets of code and notebooks that you will be able to run in your own time. All the code used in this repo is shown in Python unless specifiied otheriwse. 


Content: 

* Introduction to Azure Machine Learning (AzureML):

  * [What is Azure ML Studio](Documents/what-is-azure-ml-studio.md)
  * [How to access Azure ML Studio](Documents/Azure-ML-Studio.md)
  * [Create a Datastore using the web portal](Documents/Work-With-Data-in-Azure-ML.md)
  * [Unregister a Datastore using the web portal](Documents/Unregister-a-datastore.md)
  * [Create Datasets using the web portal](Documents/Work-With-Data-in-Azure-ML-Datasets.md)
  * [Unregister Datasets using the web portal](Documents/Unregister-a-dataset.md)
  * [How to work with Azure Machine Learning Studio Designer](Documents/studio-designer.md)
  * [How to work with Azure Machine Learning Studio Automated ML](Documents/Automated-ML.md)
  
* Introduction to training a machine learning model with AzureML SDK:
  * [Create an Experiment](Documents/Azure-ML-Experiments.md)
  

* Work with Data in AzureML
  * [Work with Datastores and Datasets using code](Documents/Work-with-Data-in-Azure-ML-code.md)

* Lab Exercises and and documentation on working with Compute in AzureML
  * [Create Compute Instances](Documents/Create-Compute-Instance.md)
  * [Stop a Compute Instance](Documents/Stop-Compute-Instance.md)
  * [Creating and Running a Python or R Notebook](Documents/Creating-and-Running-a-Python-Notebook.md)
  * [Cloning and Running a Notebook](Documents/Clone-and-Run-a-Notebook.md)
  * [JupyterLab notebook templates](labs)
  * [Data for your notebook templates](labs/data)
  
 * Build AI solutions with AzureML:
   * [Create a Pipeline](Documents/Orchestrate-ML-With-Pipelines.md)
   * [Deploy a model as a real-time inferencing service](Documents/Deploy-Real-Time-Service.md)
   * [Create a batch webservice](Documents/Deploy-Batch-Inference-Pipeline.md)
   * [Tune hyperparameters with Azure ML](Documents/Tune_hyperparameters_with_Azure_ML.md)
   * [Automate machine learning model selection with Azure Machine Learning](Documents/Automate-ML-model-selection.md)
   * [Explain machine learning models with Azure Machine Learning](Documents/Explain-machine-learning-models-with-AzureML.md)
   * [Detect and mitigate unfairness in models with Azure Machine Learning](Documents/Detect-mitigate-unfairness-in-models.md
   * [Monitor models with Azure Machine Learning](Documents/Monitor_Models_AzureML.md)
   * [Monitor data drift on datasets using the Web Portal](Documents/Dataset-Monitors.md)
   * [Monitor data drift on datasets with Python](Documents/Monitor-Data-Drift.md)
   * [Integrate with Azure Key Vault secrets](Documents/Integrate-with-Azure-Key-Vault-secrets.MD)
   * [How to productionize your Azure ML model](Documents/How-to-productionize-your-Azure-ML-model.md)
   
    
* How to work with desktop tools and connect to Azure ML:
  * Install Python and create a a virtual environment to manage your work:
    * [Installing Anaconda on Windows](Documents/Anaconda_Windows.md)
    * [Installing Anaconda on macOS](Documents/Anaconda_macos.md)
    * [Installing Anaconda on Linux](Documents/Anaconda_linux.md)
    * [Getting Started with Anaconda](Documents/Starting_with_conda.md)
  * Install Visual Studio Code and practise using it to build and debug your Pyton code:
    * [Getting Started with Python in Visual Studio Code](Documents/Installing_VS_Code.md)
    * [Data Science in Visual Studio Code](Documents/DS_Visual_Studio_Code.md)
  * Connect your Visual Studio Code with AzureML:
    * [Azure Machine Learning in Visual Studio Code](Documents/VS_Code_Azure_ML_Git.md)
    * [Train and deploy an image classification TensorFlow model using the Azure Machine Learning Visual Studio Code Extension](Documents/Train_Deploy_Model_AzureML_VSCode_Extension_GitHub.md)

* Integrate your work with Git
  * [Create a project in Azure DevOps and establish a Git repo for source code](Documents/Create_project_Azure_DevOps.md)
  * [Integrating AzureML notebooks with Git](Documents/Integrating_AzureML_notebooks_with%20Git.md)
  * [Working with Git locally](Documents/Working_with_Git_locally.md)

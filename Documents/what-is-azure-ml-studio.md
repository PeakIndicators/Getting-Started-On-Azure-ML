# What is Azure Machine Learning Studio?

Azure Machine Learning Studio is the top-level resource for Azure Machine Learning, providing a centralized place to work with all the artifacts created by the users while working with Azure Machine Learning. 
Studio keeps a history of all training runs, including logs, metrics, output and a snapshot of the scripts. 
The user can then utilise this information to determine which training run produces the best model.

Once the user has a model he likes, it can be registered within the studio and can then can be used alongside with scoring scripts to deploy to Azure Container Instances, Azure Kubernetes Service or to a field-programmable gate array (FPGA) as a REST-based HTTP endpoint. The model can also be deployed to an Azure IoT Edge device as a module.

As a sum-up we can say that Azure Machine Learning Studio is a context for the experiments, data, compute targets, and other assets associated with a machine learning workload.

## Taxonomy
A taxonomy of studio is illustrated in the following diagram (provided by Microsoft):

<p align="center">
  <img src="Images/azure-machine-learning-taxonomy.png">
</p>

The diagram shows the following components of Azure Machine Learning Studio:

* It can contain Azure Machine Learning compute instances, cloud resources configured with the Python environment necessary to run Azure Machine Learning.
* User roles enable you to share your workspace with other users, teams, or projects.
* Compute targets are used to run your experiments.
* When you create the workspace, associated resources are also created for you.
* Experiments are training runs you use to build your models.
* Pipelines are reusable workflows for training and retraining your model.
* Datasets aid in management of the data you use for model training and pipeline creation.
* Once you have a model you want to deploy, you create a registered model.
* Use the registered model and a scoring script to create a deployment endpoint.


## Azure Machine Learning Studio for Machine Learning Assets
Azure Machine Learning Studio defines the boundary for a set of related machine learning assets. You can use it to group machine learning assets based on projects, deployment environments (for example, test and production), teams, or some other organizing principle. The assets in a workspace include:

* Compute targets for development, training, and deployment.
* Data for experimentation and model training.
* Notebooks containing shared code and documentation.
* Experiments, including run history with logged metrics and outputs.
* Pipelines that define orchestrated multi-step processes.
* Models that you have trained.


## What tasks can we do within Azure Machine Learning Studio?

Once again if we check Microsoft documentation we can define those task as:

* Run an experiment to train a model - writes experiment run results to the workspace.
* Use automated ML to train a model - writes training results to the workspace.
* Register a model in the workspace.
* Deploy a model - uses the registered model to create a deployment.
* Create and run reusable workflows.
* View machine learning artifacts such as experiments, pipelines, models, deployments.
* Track and monitor models.

## How can the user interact with the tools provided by Azure Machine Learning Studio?

* On the web accessing Azure Portal and then selecting the resource Azure Machine Learning studio
* In any Python environment with the Azure Machine Learning SDK for Python.
* In any R environment with the Azure Machine Learning SDK for R (preview).
* On the command line using the Azure Machine Learning CLI extension
* Azure Machine Learning VS Code Extension

In our guidelines we will start by focusing on the web access and then we will give an overview on the other options.

Web Access: [How to access Azure ML Studio](Documents/Azure-ML-Studio.md)

#### Note
Azure Machine Learning Studio has suffered a branding rename, previouly it was called Azure Machine Learning Workspace and it has been renamed to Azure Machine Learning Studio. Therefore, some Microsoft documentation hasn't been updated yet and it might still refer to Azure Machine Learning Workspace but as we said it's the same resource as Azure Machine Learning Studio.




*Source: https://docs.microsoft.com/en-us/azure/machine-learning/concept-workspace*

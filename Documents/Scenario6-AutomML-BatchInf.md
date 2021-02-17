# Scenario 6 - Model was build using studio Automated ML and it needs to be deployed as a batch inference in another environment (stored in a specific shedule in a data lake file or database table)

In this scenario, this tutorial will demonstrate how to deploy the best model defined within the Azure Studio Automated ML run as a batch inference. But with the caveat that the deployment will be done in a different environment than the one where the Automated ML run took place.

The life cycle defined in this tutorial to suppport this solution is based on the following flow:

![](../Images/devops_autmoml2.png)

## Development Stage

**Automated ML: Train, Retrieve and Donwload the Best Model** 

This step is meant to the done in the "dev" environment, it consists of:

* Running an automated machine learning experiment - This means creating an Automated ML run, more details can be seen [here](../Documents/Automated-ML.md#New-AutomatedML-Run).
* View experiment details - This means exploring the Automated ML models that were tested, more details can be seen [here](../Documents/Automated-ML.md#Explore-AutomatedML-Models).
* Download Best Model details - Once the Best Model is chosen, the next step is to download its information so it can be applied in a different environments, more details on how to download the Best Model details can be seen [here](../Documents/Automated-ML.md#Download-Best-Model).

**Notebook: Deploy Model** 

For the deployment, the following steps should be developed:

* Register the Model - This step will upload and register the model, following the steps shown below:
![](../Images/devops2d.gif)
This will mean using the downloaded files retrieved on the _Download Best Model details_ stage.
* Scoring script - This step consists of getting the scoring script retrieved on the _Download Best Model details_ stage into the new environment. 
* [Create a pipeline with a ParallelRunStep](../Documents/Deploy-Batch-Inference-Pipeline.md#Batch-Pipeline-parallelstep) - This task consists of creating a pipeline particular step called _ParallelRunStep_ that is specifically defined for performing parallel batch inferencing.
* [Run the pipeline and retrieve the step output](../Documents/Deploy-Batch-Inference-Pipeline.md#Batch-Pipeline-publish) - In the example provided in this tutorial, this is where the output of the model is stored in a file (but other options are available such as: saving the model output in a database table, publishing it as a REST service that then can be invoked by Power BI,...).
* [Publishing and Scheduling a batch inference pipeline](../Documents/Deploy-Batch-Inference-Pipeline.md#Batch-Pipeline-publish) - The model will be published as a batch inferencing pipeline. For this particular example, everytime it is invoked it will be storing a file in the defined storage area. Once again, in the example, the scheduling is being done within the Azure ML pipeline code but the option defined in [Note](#Note) can also be considered.

## Archiving and Version Controlling

The contents of the .zip file retrieved from the _Download of the Best Model details_ should be stored in the GIT repository for future reference and versioning control. 
Once all the notebooks code is properly tested, it also should be archived in the GIT repository. In this tutorial, we are considering Azure DevOps Repos as the GIT Repository but others can be used. More details on how to do this step can be found in [Integrating Azure ML notebooks with Git](../Documents/Integrating_AzureML_notebooks_with%20Git.md).

## Migrating and Deploying to a different environment

**Step 1:** Upload and register the model to the new environment. Following the steps shown below:

![](../Images/devops2d.gif)

This will mean using the downloaded files retrieved on the _Download Best Model details_ stage and that were stored in GIT repository (task: _Archiving and Version Controlling_).

**Step 2:** Deploy the model in this new environment as a batch inference by following the steps below:

* The migration of the code to a new environment is a very simple task, it consists of cloning the repository from the previous task (_Archiving and Version Controlling_) into the new environment. More details on how to do this can be seen in [Clone and Run a Notebook](../Documents/Clone-and-Run-a-Notebook.md). 
* Once the code has been added to the new environment, it should be executed. This will create and register the model and will also scheduled the pipeline with the recurrence defined (Minute, Hour, Day, Week or Month). This will mean the code associated with that pipeline will be executed with the defined recurrence and the predictions will be retrieved with that defined frequency. If the end result, instead of saving the model outputs into a storage area, is to publish a REST service, then the process is the same except the scheduling of the pipeline, as for this case it's not needed.

<a name = 'Note'> **Note: This example considers the pipeline will be scheduled within Azure ML Studio, another option can be to schedule and execute the pipeline using Azure Data Factory, more details can be seen [here](https://docs.microsoft.com/en-us/azure/data-factory/transform-data-machine-learning-service).**

## Useful links: 
https://vladiliescu.net/deploying-models-with-azure-ml-pipelines/

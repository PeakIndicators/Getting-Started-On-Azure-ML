# Pipelines

In Azure Machine learning, you run workloads as experiments that leverage data assets and compute resources. In an enterprise data science process, you'll generally want to separate the overall process into individual tasks, and orchestrate these tasks as pipelines of connected steps. Pipelines are key to implementing an effective Machine Learning Operationalization (ML Ops) solution in Azure. In this documents we will explore how to define and run them. 

**Note:** The term *pipeline* is used extensively in machine learning, often with different meanings. For example, in Scikit-Learn, you can define pipelines that combine data preprocessing transformations with a training algorithm; and in Azure DevOps, you can define a build or release pipeline to perform the build and configuration tasks required to deliver software. The focus here is on Azure Machine Learning pipelines, which encapsulate steps that can be run as an experiment. However, bear in mind that it's perfectly feasible to have an Azure DevOps pipeline with a task that initiates an Azure Machine Learning pipeline, which in turn includes a step that trains a model based on a Scikit-Learn pipeline!

## Learning Objectives:

* Create an Azure Machine Learning pipeline.
* Publish an Azure Machine Learning pipeline.
* Schedule an Azure Machine Learning pipeline.

## Introduction to pipelines

In Azure Machine Learning, a *pipeline* is a workflow of machine learning tasks in which each task is implemented as a *step*.

Steps can be arranged sequentially or in parallel, enabling you to build sophisticated flow logic to orchestrate machine learning operations. Each step can be run on a specific compute target, making it possible to combine different types of processing as required to achieve an overall goal.

A pipeline can be executed as a process by running the pipeline as an experiment. Each step in the pipeline runs on its allocated compute target as part of the overall experiment run.

You can publish a pipeline as a REST endpoint, enabling client applications to initiate a pipeline run. You can also define a schedule for a pipeline, and have it run automatically at periodic intervals.

## Pipeline Steps

An Azure Machine Learning pipeline consists of one or more *steps* that perform tasks. There are many kinds of steps supported by Azure Machine Learning pipelines, each with its own specialized purpose and configuration options.

Common kinds of step in an Azure Machine Learning pipeline include:

* **PythonScriptStep**: Runs a specified Python script.
* **DataTransferStep**: Uses Azure Data Factory to copy data between data stores.
* **DatabricksStep**: Runs a notebook, script, or compiled JAR on a databricks cluster.
* **AdlaStep**: Runs a U-SQL job in Azure Data Lake Analytics.
* **ParallelRunStep** - Runs a Python script as a distributed task on multiple compute nodes.

**Note:** For a full list of supported step types, see [azure.pipeline.steps package documentation](https://aka.ms/AA70rrh).

To create a pipeline, you must first define each step and then create a pipeline that includes the steps. The specific configuration of each step depends on the step type. For example the following code defines two **PythonScriptStep** steps to prepare data, and then train a model.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/5.PNG)

After defining the steps, you can assign them to a pipeline, and run it as an experiment:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/6.PNG)

## Pass data between pipeline steps

Often, a pipeline line includes at least one step that depends on the output of a preceding step. For example, you might use a step that runs a python script to preprocess some data, which must then be used in a subsequent step to train a model.

### The PipelineData object

The **PipelineData** object is a special kind of **DataReference** that:

* References a location in a datastore.
* Creates a data dependency between pipeline steps.

You can view a **PipelineData** object as an intermediary store for data that must be passed from a step to a subsequent step.

![](https://docs.microsoft.com/en-us/learn/wwl-data-ai/create-pipelines-in-aml/media/06-01-pipelinedata.jpg)

### PipelineData step inputs and outputs

To use a **PipelineData** object to pass data between steps, you must:

1. Define a named **PipelineData** object that references a location in a datastore.
2. Pass the **PipelineData** object as a script argument in steps that run scripts (and include code in those scripts to read or write data)
3. Specify the **PipelineData** object as an input or output for the steps as appropriate.

For example, the following code defines a **PipelineData** object that for the preprocessed data that must be passed between the steps.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/7.PNG)

In the scripts themselves, you can obtain a reference to the **PipelineData** object from the script argument, and use it like a local folder.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/8.PNG)




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

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/Pipeline-Steps.PNG)

### PipelineData step inputs and outputs

To use a **PipelineData** object to pass data between steps, you must:

1. Define a named **PipelineData** object that references a location in a datastore.
2. Pass the **PipelineData** object as a script argument in steps that run scripts (and include code in those scripts to read or write data)
3. Specify the **PipelineData** object as an input or output for the steps as appropriate.

For example, the following code defines a **PipelineData** object that for the preprocessed data that must be passed between the steps.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/7.PNG)

In the scripts themselves, you can obtain a reference to the **PipelineData** object from the script argument, and use it like a local folder.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/8.PNG)


## Reuse pipeline steps

Pipelines with multiple long-running steps can take a significant time to complete. Azure Machine Learning includes some caching and reuse features to reduce this time.

### Managing step output reuse
By default, the step output from a previous pipeline run is reused without rerunning the step provided the script, source directory, and other parameters for the step have not changed. Step reuse can reduce the time it takes to run a pipeline, but it can lead to stale results when changes to downstream data sources have not been accounted for.

To control reuse for an individual step, you can set the **allow_reuse** parameter in the step configuration, like this:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/9.PNG)

### Forcing all steps to run
When you have multiple steps, you can force all of them to run regardless of individual reuse configuration by setting the **regenerate_outputs** parameter when submitting the pipeline experiment:

`pipeline_run = experiment.submit(train_pipeline, regenerate_outputs=True)`

## Publish pipelines

After you have created a pipeline, you can publish it to create a REST endpoint through which the pipeline can be run on demand.

### Publishing a pipeline
To publish a pipeline, you can call its publish method, as shown here:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/10.PNG)

Alternatively, you can call the **publish** method on a successful run of the pipeline:


![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/11.PNG)

After the pipeline has been published, you can view it in Azure Machine Learning studio. You can also determine the URI of its endpoint like this:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/12.PNG)

### Using a published pipeline
To initiate a published endpoint, you make an HTTP request to its REST endpoint, passing an authorization header with a token for a service principal with permission to run the pipeline, and a JSON payload specifying the experiment name. The pipeline is run asynchronously, so the response from a successful REST call includes the run ID. You can use this to track the run in Azure Machine Learning studio.

For example, the following Python code makes a REST request to run a pipeline and displays the returned run ID.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/13.PNG)

## Use pipeline parameters

You can increase the flexibility of a pipeline by defining parameters.

### Defining parameters for a pipeline
To define parameters for a pipeline, create a **PipelineParameter** object for each parameter, and specify each parameter in at least one step.

For example, you could use the following code to include a parameter for a regularization rate in the script used by an estimator:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/14.PNG)

**Note: You must define parameters for a pipeline before publishing it.**

### Running a pipeline with a parameter

After you publish a parameterized pipeline, you can pass parameter values in the JSON payload for the REST interface:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/15.PNG)

## Schedule pipelines

After you have published a pipeline, you can initiate it on demand through its REST endpoint, or you can have the pipeline run automatically based on a periodic schedule or in response to data updates.

### Scheduling a pipeline for periodic intervals
To schedule a pipeline to run at periodic intervals, you must define a **ScheduleRecurrence** that determines the run frequency, and use it to create a **Schedule**.

For example, the following code schedules a daily run of a published pipeline.


![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/16.PNG)

### Triggering a pipeline run on data changes
To schedule a pipeline to run whenever data changes, you must create a **Schedule** that monitors a specified path on a datastore, like this:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/17.PNG)

## Create a Pipeline

You can use the Azure Machine Learning SDK to perform all of the tasks required to create and operate a machine learning solution in Azure. Rather than perform these tasks individually, you can use pipelines to orchestrate the steps required to prepare data, run training scripts, register models, and other tasks.

In this tutorial we provide some jupyter notebook templates (more detail in: _[Jupyter Lab notebook templates](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/tree/main/labs)_). This example is based on the one provided in order to create a pipeline.

### Before you start

In this tutorial we provide some jupyter notebook templates that you can run (more detail in: [Jupyter Lab notebook templates](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/tree/main/labs)).

If you have not already done so, create a [compute instance](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Azure-ML-Studio.md) and ensure you have [cloned the notebooks](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Clone-and-Run-a-Notebook.md) required for this exercise.

## Open Jupyter

1. In Azure Machine Learning studio, view the **Compute** page for your workspace; and on the Compute Instances tab, start your compute instance if it is not already running.
2. When the compute instance is running, click the **Jupyter** link to open the Jupyter home page in a new browser tab. Be sure to open Jupyter and not JupyterLab.


## Example on how to run experiments in a notebook
Experiments in Azure Machine Learning need to be initiated from some sort of *control layer*; often a script or program. In this exercise, you’ll use a notebook to control experiments.

1. In the Jupyter home page, browse to the Users/labs folder where you cloned the notebook repository, and open the **Run-Experiments.ipynb** notebook.

2. Then read the notes in the notebook, running each code cell in turn.

3. When you have finished running the code in the notebook, on the **File** menu, click **Close and Halt** to close it and shut down its Python kernel. Then close all Jupyter browser tabs.

### Clean-up
If you’re finished working with Azure Machine Learning for now refer to [this page](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Stop-Compute-Instance.md) to stop your compute instance. 

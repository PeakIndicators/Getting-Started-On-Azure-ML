# Deploy batch inference pipelines with Azure Machine Learning 

## Introduction

In many production scenarios, long-running tasks that operate on large volumes of data are performed as *batch* operations. In machine learning, *batch inferencing* is used to apply a predictive model to multiple cases asynchronously - usually writing the results to a file or database.
![](https://docs.microsoft.com/en-us/learn/wwl-data-ai/deploy-batch-inference-pipelines-with-azure-machine-learning/media/07-02-batch.png)

In Azure Machine Learning, you can implement batch inferencing solutions by creating a pipeline that includes a step to read the input data, load a registered model, predict labels, and write the results as its output.

## Learning objectives

* Publish batch inference pipeline for a trained model.
* Use a batch inference pipeline to generate predictions.

## Creating a batch inference pipeline
To create a batch inferencing pipeline, perform the following tasks:

### 1. Register a model
To use a trained model in a batch inferencing pipeline, you must register it in your Azure Machine Learning workspace.

To register a model from a local file, you can use the **register** method of the **Model** object as shown in the following example code:

1[](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/33.PNG)

Alternatively, if you have a reference to the **Run** used to train the model, you can use its **register_model** method as shown in the following example code:

1[](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/34.PNG)

## 2. Create a scoring script
Batch inferencing service requires a scoring script to load the model and use it to predict new values. It must include two functions:

* **init()**: Called when the pipeline is initialized.
* **run(mini_batch):** Called for each batch of data to be processed.

Typically, you use the **init** function to load the model from the model registry, and use the **run** function to generate predictions from each batch of data and return the results. The following example script shows this pattern:

1[](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/35.PNG)

## 3. Create a pipeline with a ParallelRunStep

Azure Machine Learning provides a type of pipeline step specifically for performing parallel batch inferencing. Using the ParallelRunStep class, you can read batches of files from a File dataset and write the processing output to a PipelineData reference. Additionally, you can set the output_action setting for the step to "append_row", which will ensure that all instances of the step being run in parallel will collate their results to a single output file named parallel_run_step.txt. The following code snippet shows an example of creating a pipeline with a ParallelRunStep:

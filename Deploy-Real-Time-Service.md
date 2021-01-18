# Deploy real-time machine learning services with Azure Machine Learning

## Introduction

In machine learning, *inferencing* refers to the use of a trained model to predict labels for new data on which the model has not been trained. Often, the model is deployed as part of a service that enables applications to request immediate, or *real-time*, predictions for individual or small numbers of data observations.

![](https://docs.microsoft.com/en-us/learn/wwl-data-ai/register-and-deploy-model-with-amls/media/07-01-real-time.jpg)

In Azure Machine learning, you can create real-time inferencing solutions by deploying a model as a service, hosted in a containerized platform such as Azure Kubernetes Services (AKS).

## Learning objectives
In this module, you will learn how to:

* Deploy a model as a real-time inferencing service.
* Consume a real-time inferencing service.
* Troubleshoot service deployment

## Deploying a model as a real-time service

You can deploy a model as a real-time web service to several kinds of compute target, including local compute, an Azure Machine Learning compute instance, an Azure Container Instance (ACI), an Azure Kubernetes Service (AKS) cluster, an Azure Function, or an Internet of Things (IoT) module. Azure Machine Learning uses containers as a deployment mechanism, packaging the model and the code to use it as an image that can be deployed to a container in your chosen compute target.

**Note:** Deployment to a local service, a compute instance, or an ACI is a good choice for testing and development. For production, you should deploy to a target that meets the specific performance, scalability, and security needs of your application architecture.

To deploy a model as a real-time inferencing service, you must perform the following tasks:

## 1. Register a trained model

After successfully training a model, you must register it in your Azure Machine Learning workspace. Your real-time service will then be able to load the model when required.

To register a model from a local file, you can use the **register** method of the **Model** object as shown here:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/18.PNG)

Alternatively, if you have a reference to the **Run** used to train the model, you can use its **register_model** method as shown here:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/19.PNG)

## 2. Define an inference configuration
The model will be deployed as a service that consist of:

* A script to load the model and return predictions for submitted data.
* An environment in which the script will be run.

You must therefore define the script and environment for the service.

### Creating an entry script

Create the *entry script* (sometimes referred to as the *scoring script*) for the service as a Python (.py) file. It must include two functions:

* **init():** Called when the service is initialized.
* **run(raw_data):** Called when new data is submitted to the service.

Typically, you use the **init** function to load the model from the model registry, and use the **run** function to generate predictions from the input data. The following example script shows this pattern:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/20.PNG)

### Creating an environment
Your service requires a Python environment in which to run the entry script, which you can configure using Conda configuration file. An easy way to create this file is to use a **CondaDependencies** class to create a default environment (which includes the **azureml-defaults** package and commonly-used packages like **numpy** and **pandas**), add any other required packages, and then serialize the environment to a string and save it:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/21.PNG)

### Combining the script and environment in an InferenceConfig
After creating the entry script and environment configuration file, you can combine them in an **InferenceConfig** for the service like this:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/22.PNG)

## 3. Define a deployment configuration
Now that you have the entry script and environment, you need to configure the compute to which the service will be deployed. If you are deploying to an AKS cluster, you must create the cluster and a compute target for it before deploying:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/23.PNG)

With the compute target created, you can now define the deployment configuration, which sets the target-specific compute specification for the containerized deployment:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/24.PNG)

The code to configure an ACI deployment is similar, except that you do not need to explicitly create an ACI compute target, and you must use the **deploy_configuration** class from the **azureml.core.webservice.AciWebservice** namespace. Similarly, you can use the azureml.core.webservice.LocalWebservice namespace to configure a local Docker-based service.

**Note:** To deploy a model to an Azure Function, you do not need to create a deployment configuration. Instead, you need to package the model based on the type of function trigger you want to use. This functionality is in preview at the time of writing. For more details, see [Deploy a machine learning model to Azure Functions](https://aka.ms/AA70rrn) in the Azure Machine Learning documentation.

## 4. Deploy the model

After all of the configuration is prepared, you can deploy the model. The easiest way to do this is to call the **deploy** method of the **Model** class, like this:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/25.PNG)

For ACI or local services, you can omit the **deployment_target parameter** (or set it to **None**).

**More Information**: For more information about deploying models with Azure Machine Learning, see [Deploy models with Azure Machine Learning](https://aka.ms/AA70zfv) in the documentation.

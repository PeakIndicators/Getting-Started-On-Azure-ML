# Connect to data with the Azure Machine Learning studio - Datastore Creation (Code Free)

## Introduction to data connection in Azure Machine Learning Studio

In Azure Machine Learning Studio you can:
* Access your data without using code. 

* Connect to your data in storage services on Azure with [Azure Machine Learning datastores](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-access-data), and then package that data for tasks in your ML workflows with [Azure Machine Learning datasets](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-create-register-datasets).

The following table defines and summarizes the benefits of datastores and datasets.

| **Object** | **Description** | **Benefits** |
| ---------- | -------------- | ---------------- |
|Datastores | Securely connect to your storage service on Azure, by storing your connection information, like your subscription ID and token authorization in your [Key Vault](https://azure.microsoft.com/services/key-vault/) associated with the workspace | Because your information is securely stored, you: <ul><li>Don't put authentication credentials or original data sources at risk.</li><li>No longer need to hard code them in your scripts.</li></ul>|
|Datasets | By creating a dataset, you create a reference to the data source location, along with a copy of its metadata. With datasets you can: <ul><li> Access data during model training.</li><li>Share data and collaborate with other users.</li><li>Leverage open-source libraries, like pandas, for data exploration</li></ul> | Because datasets are lazily evaluated, and the data remains in its existing location, you: <ul><li>Keep a single copy of data in your storage.</li><li> Incur no extra storage cost.</li><li> Don't risk unintentionally changing your original data sources.</li><li>Improve ML workflow performance speeds.</li></ul>|

In this section we will explain how to create a Datastore.

## Introduction to datastores

In Azure Machine Learning, *datastores* are abstractions for cloud data sources. They encapsulate the information required to connect to data sources. You can access datastores directly in code by using the Azure Machine Learning SDK, and use it to upload or download data.

### Types of Datastore
Azure Machine Learning supports the creation of datastores for multiple kinds of Azure data source, including:

* Azure Storage (blob and file containers)
* Azure Data Lake stores
* Azure SQL Database
* Azure Databricks file system (DBFS)

### Built-in Datastores
Every studio has two built-in datastores (an Azure Storage blob container, and an Azure Storage file container) that are automatically registered as datastores to the workspace and are used as system storage by Azure Machine Learning.  They're named `workspaceblobstore` and `workspacefilestore`, respectively. If blob storage is sufficient for your needs, the `workspaceblobstore` is set as the default datastore, and already configured for use.

In most machine learning projects, you will likely need to work with data sources of your own - either because you need to store larger volumes of data than the built-in datastores support or because you need to integrate your machine learning solution with data from existing applications.

  
 ## Create datastores

 To create a new datastore in a few steps with the Azure Machine Learning studio:
 
1. Sign in to [Azure Machine Learning studio](https://ml.azure.com/).
2. Select **Datastores** on the left pane under **Manage**.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/datastore1.PNG)

3. Select + **New datastore**.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/datastore2.PNG)

4. Complete the form to create and register a new datastore. See the [storage access and permissions section](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-connect-data-ui#access-validation) if you need support on how to find the authentication credentials you need to populate this form.

  **Note:** Datastore name should only consist of lowercase letters, digits and underscore.

  The following example demonstrates what the form looks like when you create an **Azure blob datastore**:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/new-datastore-form.png)



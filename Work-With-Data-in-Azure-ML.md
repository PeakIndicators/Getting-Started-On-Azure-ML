# Work with Data in Azure Machine Learning 

This will cover how to: 

* Create and use datastores
* Create and use datasets

## Introduction to datastores

In Azure Machine Learning, *datastores* are abstractions for cloud data sources. They encapsulate the information required to connect to data sources. You can access datastores directly in code by using the Azure Machine Learning SDK, and use it to upload or download data.

What is Azure Machine Learning SDK?

Azure Machine Learning provides software development kits (SDKs) for Python and R, which you can use to create, manage, and use assets in an Azure Machine Learning workspace..
This will be covered in more depth later on. 


### Types of Datastore

Azure Machine Learning supports the creation of datastores for multiple kinds of Azure data source, including:

* Azure Storage (blob and file containers)
* Azure Data Lake stores
* Azure SQL Database
* Azure Databricks file system (DBFS)
**Note:** For a full list of supported datastores, see the Azure Machine Learning documentation.

### Built-in Datastores
Every workspace has two built-in datastores (an Azure Storage blob container, and an Azure Storage file container) that are used as system storage by Azure Machine Learning. 

In most machine learning projects, you will likely need to work with data sources of your own - either because you need to store larger volumes of data than the built-in datastores support, or because you need to integrate your machine learning solution with data from existing applications

### Use datastores

To add a datastore to your workspace, you can register it using the graphical interface in Azure Machine Learning studio, or you can use the Azure Machine Learning SDK. For example, the following code registers an Azure Storage blob container as a datastore named blob_data.

![]()

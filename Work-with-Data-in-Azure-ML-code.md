# Work with Data in Azure Machine Learning 

## Introduction

Data is a fundamental element in any machine learning workload, so in this docuemnt, you will learn how to create and manage datastores and datasets in an Azure Machine Learning workspace, and how to use them in model training experiments.

## Learning objectives:

* Create and use datastores
* Create and use datasets

## Introduction to datastores

In Azure Machine Learning, *datastores* are abstractions for cloud data sources. They encapsulate the information required to connect to data sources. You can access datastores directly in code by using the Azure Machine Learning SDK, and use it to upload or download data.

## Types of Datastore

Azure Machine Learning supports the creation of datastores for multiple kinds of Azure data source, including:

* Azure Storage (blob and file containers)
* Azure Data Lake stores
* Azure SQL Database
* Azure Databricks file system (DBFS)

**Note:** For a full list of supported datastores, see the [Azure Machine Learning documentation](https://aka.ms/AA70zfl).

## Built-in Datastores

Every workspace has two built-in datastores (an Azure Storage blob container, and an Azure Storage file container) that are used as system storage by Azure Machine Learning. There's also a third datastore that gets added to your workspace if you make use of the open datasets provided as samples (for example, by creating a designer pipeline based on a sample dataset)

In most machine learning projects, you will likely need to work with data sources of your own - either because you need to store larger volumes of data than the built-in datastores support, or because you need to integrate your machine learning solution with data from existing applications.

## Use datastores

To add a datastore to your workspace, you can register it using the graphical interface in Azure Machine Learning studio as shown on [this page](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Work-With-Data-in-Azure-ML.md), or you can use the Azure Machine Learning SDK. For example, the following code registers an Azure Storage blob container as a datastore named **blob_data**.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/41.PNG)

### Managing datastores

You can view and manage datastores in Azure Machine Learning Studio, as shown on [this page](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Work-With-Data-in-Azure-ML.md), or you can use the Azure Machine Learning SDK. For example, the following code lists the names of each datastore in the workspace.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/42.PNG)

You can get a reference to any datastore by using the Datastore.get() method as shown here:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/43.PNG)

The workspace always includes a *default* datastore (initially, this is the built-in **workspaceblobstore** datastore), which you can retrieve by using the **get_default_datastore()** method of a **Workspace** object, like this:

`default_store = ws.get_default_datastore()`

### Considerations for datastores

When planning for datastores, consider the following guidelines:

* When using Azure blob storage, *premium* level storage may provide improved I/O performance for large datasets. However, this option will increase cost and may limit replication options for data redundancy.
* When working with data files, although CSV format is very common, Parquet format generally results in better performance.
* You can access any datastore by name, but you may want to consider changing the default datastore (which is initially the built-in **workspaceblobstore** datastore).

To change the default datastore, use the **set_default_datastore()** method:

`ws.set_default_datastore('blob_data')`


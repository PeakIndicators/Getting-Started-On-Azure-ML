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

## Introduction to datasets

*Datasets* are versioned packaged data objects that can be easily consumed in experiments and pipelines. Datasets are the recommended way to work with data, and are the primary mechanism for advanced Azure Machine Learning capabilities like data labeling and data drift monitoring.

## Types of dataset
Datasets are typically based on files in a datastore, though they can also be based on URLs and other sources. You can create the following types of dataset:

* **Tabular:** The data is read from the dataset as a table. You should use this type of dataset when your data is consistently structured and you want to work with it in common tabular data structures, such as Pandas dataframes.
* **File:** The dataset presents a list of file paths that can be read as though from the file system. Use this type of dataset when your data is unstructured, or when you need to process the data at the file level (for example, to train a convolutional neural network from a set of image files).

## Creating and registering datasets
You can use the visual interface in Azure Machine Learning studio as shown on [this page](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Work-With-Data-in-Azure-ML.md), or the Azure Machine Learning SDK to create datasets from individual files or multiple file paths. The paths can include wildcards (for example, */files/*.csv*) making it possible to encapsulate data from a large number of files in a single dataset.

After you've created a dataset, you can *register* it in the workspace to make it available for use in experiments and data processing pipelines later.

## Creating and registering tabular datasets
To create a tabular dataset using the SDK, use the **from_delimited_files** method of the **Dataset.Tabular class**, like this:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/44.PNG)

The dataset in this example includes data from two file paths within the default datastore:

* The **current_data.csv** file in the **data/files** folder.
* All .csv files in the **data/files/archive/** folder.

After creating the dataset, the code registers it in the workspace with the name **csv_table**.

## Creating and registering file datasets
To create a file dataset using the SDK, use the **from_files** method of the **Dataset.File** class, like this:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/45.PNG)

The dataset in this example includes all .jpg files in the **data/files/images** path within the default datastore:

After creating the dataset, the code registers it in the workspace with the name **img_files**.

## Retrieving a registered dataset
After registering a dataset, you can retrieve it by using any of the following techniques:

* The **datasets** dictionary attribute of a **Workspace** object.
* The **get_by_name** or **get_by_id** method of the **Dataset** class.

Both of these techniques are shown in the following code:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/46.PNG)

## Dataset versioning
Datasets can be *versioned*, enabling you to track historical versions of datasets that were used in experiments, and reproduce those experiments with data in the same state.

You can create a new version of a dataset by registering it with the same name as a previously registered dataset and specifying the **create_new_version** property:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/47.PNG)

In this example, the .png files in the **images** folder have been added to the definition of the **img_paths** dataset example used in the previous topic.

## Retrieving a specific dataset version

You can retrieve a specific version of a dataset by specifying the **version** parameter in the **get_by_name** method of the **Dataset** class.

`img_ds = Dataset.get_by_name(workspace=ws, name='img_files', version=2)`

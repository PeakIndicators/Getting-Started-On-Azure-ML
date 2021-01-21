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

## Use datasets

Datasets are the primary way to pass data to experiments that train models.

## Work with tabular datasets
You can read data directly from a tabular dataset by converting it into a Pandas or Spark dataframe:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/48.PNG)

## Pass a tabular dataset to an experiment script
When you need to access a dataset in an experiment script, you must pass the dataset to the script. There are two ways you can do this.

### Use a script argument for a tabular dataset
You can pass a tabular dataset as a script argument. When you take this approach, the argument received by the script is the unique ID for the dataset in your workspace. In the script, you can then get the workspace from the run context and use it to retrieve the dataset by it's ID.

*ScriptRunConfig:*

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/49.PNG)

*Script:*

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/50.PNG)

## Use a named input for a tabular dataset
Alternatively, you can pass a tabular dataset as a *named input*. In this approach, you use the **as_named_input** method of the dataset to specify a name for the dataset. Then in the script, you can retrieve the dataset by name from the run context's **input_datasets** collection without needing to retrieve it from the workspace. Note that if you use this approach, you still need to include a script argument for the dataset, even though you don’t actually use it to retrieve the dataset.

*ScriptRunConfig:*

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/51.PNG)

*Script:*

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/52.PNG)

## Work with file datasets
When working with a file dataset, you can use the **to_path()** method to return a list of the file paths encapsulated by the dataset:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/53.PNG)

### Pass a file dataset to an experiment script
Just as with a Tabular dataset, there are two ways you can pass a file dataset to a script. However, there are some key differences in the way that the dataset is passed.

### Use a script argument for a file dataset
You can pass a file dataset as a script argument. Unlike with a tabular dataset, you must specify a mode for the file dataset argument, which can be **as_download** or **as_mount**. This provides an access point that the script can use to read the files in the dataset. In most cases, you should use **as_download**, which copies the files to a temporary location on the compute where the script is being run. However, if you are working with a large amount of data for which there may not be enough storage space on the experiment compute, use **as_mount** to stream the files directly from their source.

*ScriptRunConfig:*

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/54.PNG)

*Script:*

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/55.PNG)

### Use a named input for a file dataset
You can also pass a file dataset as a *named input*. In this approach, you use the **as_named_input** method of the dataset to specify a name before specifying the access mode. Then in the script, you can retrieve the dataset by name from the run context's **input_datasets** collection and read the files from there. As with tabular datasets, if you use a named input, you still need to include a script argument for the dataset, even though you don’t actually use it to retrieve the dataset.

*ScriptRunConfig:*

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/56.PNG)

*Script:*

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/57.PNG)

## Exercise - Work with data

Although it’s fairly common to work with data on their local file system, in an enterprise environment it can be more effective to store the data in a central location where multiple data scientists and machine learning engineers can access it.

In this exercise, you’ll explore *datastores* and *datasets*, which are the primary objects used to abstract data access in Azure Machine Learning.

### Before you start

In this tutorial we provide some jupyter notebook templates (more detail in: [Jupyter Lab notebook templates](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/tree/main/labs)).

If you have not already done so, create a [compute instance](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Azure-ML-Studio.md) and ensure you have [cloned the notebooks](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Clone-and-Run-a-Notebook.md) required for this exercise.

## Open Jupyter

1. In Azure Machine Learning studio, view the **Compute** page for your workspace; and on the Compute Instances tab, start your compute instance if it is not already running.
2. When the compute instance is running, click the **Jupyter** link to open the Jupyter home page in a new browser tab. Be sure to open Jupyter and not JupyterLab.


## Example on how to run experiments in a notebook
Experiments in Azure Machine Learning need to be initiated from some sort of *control layer*; often a script or program. In this exercise, you’ll use a notebook to control experiments.

1. In the Jupyter home page, browse to the Users/labs folder where you cloned the notebook repository, and open the **Work-with-Data.ipynb** notebook.

2. Then read the notes in the notebook, running each code cell in turn.

3. When you have finished running the code in the notebook, on the **File** menu, click **Close and Halt** to close it and shut down its Python kernel. Then close all Jupyter browser tabs.

### Clean-up
If you’re finished working with Azure Machine Learning for now refer to [this page](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Stop-Compute-Instance.md) to stop your compute instance.  


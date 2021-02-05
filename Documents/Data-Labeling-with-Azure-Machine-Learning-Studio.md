# Data Labeling with Azure Machine Learning Studio

If you want to train a machine learning model to classify images, you need hundreds or even thousands of images that are correctly labeled. Azure Machine Learning helps you manage the progress of your private team of domain experts as they label ((also referred to as tagging) your data.

In this tutorial we will explain you how to:

* Create a multi-class image labeling project.
* Label your data. Either you or your labelers can perform this task.
* Complete the project by reviewing and exporting the data.

## Start a labeling project

1 - Sign in to [Azure Machine Learning studio](https://ml.azure.com/).

2 - Select your subscription and the workspace you created.

3 - Create a datastore (follow the steps described in [Create Datastores](../Documents/Work-With-Data-in-Azure-ML.md#Create-Datastores)).

And fill with the following settings:

|Field	|Description|
|-------|-----------|
|Datastore name	|Give the datastore a name. Here we use data_labeling_tutorial.|
|Datastore type	|Select the type of storage. Here we use Azure Blob Storage, the preferred storage for images.|
|Account selection method|	Select Enter manually.|
|URL|	https://azureopendatastorage.blob.core.windows.net/openimagescontainer|
|Authentication type| Select SAS token.|
|Account key|	?sv=2019-02-02&ss=bfqt&srt=sco&sp=rl&se=2025-03-25T04:51:17Z&st=2020-03-24T20:51:17Z&spr=https&sig=7D7SdkQidGT6pURQ9R4SUzWGxZ%2BHlNPCstoSRRVg8OY%3D|

**Note:** This example is taken from a [Microsoft Tutorial](https://docs.microsoft.com/en-gb/azure/machine-learning/tutorial-labeling#start-a-labeling-project), it uses images of cats and dogs. Since each image is either a cat or a dog, this will be a multi-class labeling project.

![](../Images/DataLabeling1.PNG)

## Create a labeling project
Now that you have access to the data you want to have labeled, create your labeling project.

1 - Select **Data Labeling** on the left pane under Manage.

![](../Images/DataLabeling2.PNG)

2 - At the top of the page, select Projects and then select + Add project.

*Source: https://docs.microsoft.com/en-gb/azure/machine-learning/tutorial-labeling*

# How to work with Azure Machine Learning Studio Designer

This section will explain how to use the Azure Machine Learning Studio Designer to train and deploy a machine learning model. The designer is a drag-and-drop tool that lets the user creates machine learning models without a single line of code.

In part one of the tutorial, we will describe how to:

* Create a new pipeline.
* Import data.
* Prepare data.
* Train a machine learning model.
* Evaluate a machine learning model.
* Deploy the model

### Before you start

If you have not already done so, please:

* Create a Compute Cluster, this Automated ML feature won't work with a compute instance, it requires a compute cluster. More details can be seen in: [compute instance](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Azure-ML-Studio.md).
* Create a Datastore and a Dataset with the data you want to use. For more information see: [Create a Datastore using the web portal](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Work-With-Data-in-Azure-ML.md) and [Create Datasets using the web portal](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Work-With-Data-in-Azure-ML-Datasets.md).

**Note**
If you do not see the graphical elements mentioned in the steps below, such as buttons, you may not have the right level of permissions to studio. Please contact your Azure subscription administrator to verify that you have been granted the correct level of access.


### Create a pipeline
1. Sign in to [Azure Machine Learning studio](https://ml.azure.com/).

2. Select **Designer** on the left pane under **Author** section and select **Easy-to-use prebuilt modules**.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/designer1.png)

3. At the top of the canvas, select the default pipeline name Pipeline-Created-on. Rename it to the name you want to give to your pipeline. The name doesn't need to be unique.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/designer2.PNG)

### Set the default Compute Target
A pipeline runs on a compute target, which is a compute resource that's attached to your studio.The compute target can be reused in future runs.

You can set a Default compute target for the entire pipeline, which will tell every module to use the same compute target by default. However, you can specify compute targets on a per-module basis.

1. Next to the pipeline name, select the **Gear icon**![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/gear-icon.png)  at the top of the canvas to open the Settings pane.

2. In the Settings pane to the right of the canvas, select Select compute target.

3. If you already have an available compute target, you can select it to run this pipeline.

 Note

The designer can only run training experiments on Azure Machine Learning Compute but other compute targets won't be shown.

Enter a name for the compute resource.

Select Save.

 Note

It takes approximately five minutes to create a compute resource. After the resource is created, you can reuse it and skip this wait time for future runs.

The compute resource autoscales to zero nodes when it's idle to save cost. When you use it again after a delay, you might experience approximately five minutes of wait time while it scales back up.

https://docs.microsoft.com/en-us/azure/machine-learning/tutorial-designer-automobile-price-train-score

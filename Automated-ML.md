# How to work with Azure Machine Learning Studio Automated Machine Learning (ML)

Azure Machine Learning Studio Automated ML allows the user to create a model without writing a single line of code.

Automated ML provides the automation of intensive tasks, it rapidly iterates over many combinations of algorithms and hyperparameters to help find the best model based on a success metric of your choosing.

In this tutorial, we will guide you on how to do the following tasks:

* Run an automated machine learning experiment.
* View experiment details.
* Deploy the model.


### Before you start

If you have not already done so, please:

* Create a Compute Cluster, this Automated ML feature won't work with a compute instance, it requires a compute cluster. More details can be seen in: [compute instance](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Azure-ML-Studio.md).
* Create a Datastore and a Dataset with the data you want to use. For more information see: [Create a Datastore using the web portal](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Work-With-Data-in-Azure-ML.md) and [Create Datasets using the web portal](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Work-With-Data-in-Azure-ML-Datasets.md).

The example below shows how to create a simple classification model using automated machine learning in the Azure Machine Learning studio. This classification model predicts if a client will subscribe to a fixed term deposit with a financial institution.
Another example, using time-series forecasting model can be seen here: https://docs.microsoft.com/en-us/azure/machine-learning/tutorial-automated-ml-forecast

Anyway, independent on the type of model, the steps are aimilar.

### Create a new Automated ML run

1. Sign in to [Azure Machine Learning studio](https://ml.azure.com/).

2. Select **Automated ML** on the left pane under **Author** section.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/automatedml1.png)

3. Select **+New automated ML** run.

4. A new window will appear where you need to select the dataset you want to work with and then press **Next**.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/automatedml2.PNG)

5. After loading and configuring the data, the next step is to set up the experiment on the  **Configure Run** section. This setup includes experiment design tasks such as, selecting the size of your compute environment and specifying what column you want to predict. Populate the Configure Run form as follows:

* Enter this **experiment name** taking into account the rule: experiment name must be 1-256 characters, start with a letter or a number and can only contain letters, numbers, underscores and dashes.

* Select the target column, which is what you want to predict. 

* Select the compute cluster created for this feature.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/automatedml3.PNG)

Click **Next**.

6. On the **Task type and settings** form, complete the setup for your automated ML experiment by specifying the machine learning task type and configuration settings. 
Select the **machine learning task type** and then select *View additional configuration settings* and populate the fields as follows. 

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/automatedml4.PNG)

These settings are to better control the training job. Otherwise, defaults are applied based on experiment selection and data.

| **Additional configurations** | **Description** |
| ---------- | -------------- |
| Primary metric|	Evaluation metric that the machine learning algorithm will be measured by.	|
| Explain best model|	Automatically shows explainability on the best model created by automated ML.|
|Blocked algorithms|	Algorithms you want to exclude from the training job	|
|Exit criterion|	If a criteria is met, the training job is stopped.|
|Validation|	Choose a cross-validation type and number of tests.|
|Concurrency|	The maximum number of parallel iterations executed per iteration|

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/automatedml5.PNG)

Once all the setting are properly filled, select **Save**.

7. Select **View featurization settings**. 

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/automatedml6.PNG)

Configure accordingly.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/automatedml7.PNG)

Select **Save**.

8. Select **Finish** to run the experiment. 

9. The Run Detail screen opens with the Run status at the top as the experiment preparation begins. This status updates as the experiment progresses. Notifications also appear in the top right corner of the studio, to inform you of the status of your experiment.

_Preparation takes 10-15 minutes to prepare the experiment run. Once running, it takes 2-3 minutes more for each iteration._

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/automatedml8.PNG)


# Monitor data drift with Azure Machine Learning 

## Introduction
You typically train a machine learning model using a historical dataset that is representative of the new data that your model will receive for inferencing. However, over time there may be trends that change the profile of the data, making your model less accurate.

For example, suppose a model is trained to predict the expected gas mileage of an automobile based on the number of cylinders, engine size, weight, and other features. Over time, as car manufacturing and engine technologies advance, the typical fuel-efficiency of vehicles might improve dramatically; making the predictions made by the model trained on older data less accurate.

![](../Images/Monitor10.PNG)

This change in data profiles between training and inferencing is known as data drift, and it can be a significant issue for predictive models used in production. It is therefore important to be able to monitor data drift over time, and retrain models as required to maintain predictive accuracy.

## Learning Objectives

* Create a data drift monitor. 
* Schedule data drift monitoring. 
* View data drift monitoring results.

## Creating a data drift monitor

Azure Machine Learning supports data drift monitoring through the use of *datasets*. You can capture new feature data in a dataset and compare it to the dataset with which the model was trained.

### Monitor data drift by comparing datasets
It's common for organizations to continue to collect new data after a model has been trained. For example, a health clinic might use diagnostic measurements from previous patients to train a model that predicts diabetes likelihood, but continue to collect the same diagnostic measurements from all new patients. The clinic's data scientists could then periodically compare the growing collection of new data to the original training data, and identify any changing data trends that might affect model accuracy.

To monitor data drift using registered datasets, you need to register two datasets:

* A *baseline* dataset - usually the original training data.
* A *target* dataset that will be compared to the baseline based on time intervals. This dataset requires a column for each feature you want to compare, and a timestamp column so the rate of data drift can be measured.

**Note:** 
You can configure a deployed service to collect new data submitted to the model for inferencing, which is saved in Azure blob storage and can be used as a target dataset for data drift monitoring. See [Collect data from models in production](https://aka.ms/AA70zg8) in the Azure Machine Learning documentation for more information. This has been explored prior to the creation of this document to see if it could be added as an additional document and practical example. The *azureml-monitoring* module required to enable data collection, however, at the time of writing (03/02/21), this module is still in [preview](https://pypi.org/project/azureml-monitoring/). 

After creating these datasets, you can define a *dataset* monitor to detect data drift and trigger alerts if the rate of drift exceeds a specified threshold. You can create dataset monitors using the visual interface in Azure Machine Learning studio, or by using the **DataDriftDetector** class in the Azure Machine Learning SDK as shown in the following example code:

     from azureml.datadrift import DataDriftDetector

     monitor = DataDriftDetector.create_from_datasets(workspace=ws,
                                               name='dataset-drift-detector',
                                               baseline_data_set=train_ds,
                                               target_data_set=new_data_ds,
                                               compute_target='aml-cluster',
                                               frequency='Week',
                                               feature_list=['age','height', 'bmi'],
                                               latency=24)

After creating the dataset monitor, you can *backfill* to immediately compare the baseline dataset to existing data in the target dataset, as shown in the following example, which backfills the monitor based on weekly changes in data for the previous six weeks:

     import datetime as dt

     backfill = monitor.backfill( dt.datetime.now() - dt.timedelta(weeks=6), dt.datetime.now())
     
## Scheduling alerts

When you define a data monitor, you specify a schedule on which it should run. Additionally, you can specify a threshold for the rate of data drift and an operator email address for notifications if this threshold is exceeded.

### Configure data drift monitor schedules

Data drift monitoring works by running a comparison at scheduled **frequency**, and calculating data drift metrics for the features in the dataset that you want to monitor. You can define a schedule to run every **Day**, **Week**, or **Month**.

For dataset monitors, you can specify a **latency**, indicating the number of hours to allow for new data to be collected and added to the target dataset. For deployed model data drift monitors, you can specify a **schedule_start** time value to indicate when the data drift run should start (if omitted, the run will start at the current time).

### Configure alerts
Data drift is measured using a calculated *magnitude* of change in the statistical distribution of feature values over time. You can expect some natural random variation between the baseline and target datasets, but you should monitor for large changes that might indicate significant data drift.

You can define a **threshold** for data drift magnitude above which you want to be notified, and configure alert notifications by email. The following code shows an example of scheduling a data drift monitor to run every week, and send an alert if the drift magnitude is greater than 0.3:

    alert_email = AlertConfiguration('data_scientists@contoso.com')
    monitor = DataDriftDetector.create_from_datasets(ws, 'dataset-drift-detector', 
                                                    baseline_data_set, target_data_set,
                                                    compute_target=cpu_cluster,
                                                    frequency='Week', latency=2,
                                                    drift_threshold=.3,
                                                     alert_configuration=alert_email)
                                                                                                          
## 

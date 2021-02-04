# Automate machine learning model selection with Azure Machine Learning

*Automated Machine Learning* enables you to try multiple algorithms and preprocessing transformations with your data. This, combined with scalable cloud-based compute makes it possible to find the best performing model for your data without the huge amount of time-consuming manual trial and error that would otherwise be required.

![](../Images/AutoML1.PNG)

Azure Machine Learning includes support for automated machine learning through a visual interface in Azure Machine Learning studio for *Enterprise* edition workspaces only. You can use the Azure Machine Learning SDK to run automated machine learning experiments in either *Basic* or *Enterprise* edition workspaces.

## Learning Objectives

* Use Azure Machine Learning's automated machine learning capabilities to determine the best performing algorithm for your data.
* Use automated machine learning to preprocess data for training.
* Run an automated machine learning experiment.

## Automated machine learning tasks and algorithms

You can use automated machine learning in Azure Machine Learning to train models for the following types of machine learning task:

* Classification
* Regression
* Time Series Forecasting

## Task-specific algorithms
Azure Machine Learning includes support for numerous commonly used algorithms for these tasks, including:

### Classification algorithms
* Logistic Regression
* Light Gradient Boosting Machine (GBM)
* Decision Tree
* Random Forest
* Naive Bayes
* Linear Support Vector Machine (SVM)
* XGBoost
* Deep Neural Network (DNN) Classifier
* Others...

### Regression algorithms
* Linear Regression
* Light Gradient Boosting Machine (GBM)
* Decision Tree
* Random Forest
* Elastic Net
* LARS Lasso
* XGBoost
* Others...

### Forecasting algorithms
* Linear Regression
* Light Gradient Boosting Machine (GBM)
* Decision Tree
* Random Forest
* Elastic Net
* LARS Lasso
* XGBoost
* Others...

More Information: For a full list of supported algorithms, see [How to define a machine learning task](https://aka.ms/AA70rrr).

### Restrict algorithm selection
By default, automated machine learning will randomly select from the full range of algorithms for the specified task. You can choose to block individual algorithms from being selected; which can be useful if you know that your data is not suited to a particular type of algorithm, or you have to comply with a policy that restricts the type of machine learning algorithms you can use in your organization.

## Preprocessing and featurization

As well as trying a selection of algorithms, automated machine learning can apply preprocessing transformations to your data; improving the performance of the model.

### Scaling and normalization
Automated machine learning applies scaling and normalization to numeric data automatically, helping prevent any large-scale features from dominating training. During an automated machine learning experiment, multiple scaling or normalization techniques will be applied.

### Optional featurization
You can choose to have automated machine learning apply preprocessing transformations, such as:

* Missing value imputation to eliminate nulls in the training dataset.

* Categorical encoding to convert categorical features to numeric indicators.

* Dropping high-cardinality features, such as record IDs.

* Feature engineering (for example, deriving individual date parts from DateTime features)

* Others...

More Information: For more information about the preprocessing support in automated machine learning, see [What is automated machine learning](https://aka.ms/AA70rrt).

## Running automated machine learning experiments

To run an automated machine learning experiment, you can either use the user interface in Azure Machine Learning studio, or submit an experiment using the SDK.

### Configure an automated machine learning experiment
The user interface provides an intuitive way to select options for your automated machine learning experiment. When using the SDK, you have greater flexibility, and you can set experiment options using the **AutoMLConfig** class, as shown in the following example.

      from azureml.train.automl import AutoMLConfig

      automl_run_config = RunConfiguration(framework='python')
      automl_config = AutoMLConfig(name='Automated ML Experiment',
                                  task='classification',
                                  primary_metric = 'AUC_weighted',
                                  compute_target=aml_compute,
                                  training_data = train_dataset,
                                  validation_data = test_dataset,
                                  label_column_name='Label',
                                  featurization='auto',
                                  iterations=12,
                                  max_concurrent_iterations=4)

### Specify data for training
Automated machine learning is designed to enable you to simply bring your data, and have Azure Machine Learning figure out how best to train a model from it.

When using the Automated Machine Learning user interface in Azure Machine Learning studio, you can create or select an Azure Machine Learning [dataset](https://aka.ms/AA6zxeb) to be used as the input for your automated machine learning experiment.

When using the SDK to run an automated machine learning experiment, you can submit the data in the following ways:

* Specify a dataset or dataframe of training data that includes features and the label to be predicted.
* Optionally, specify a second validation data dataset or dataframe that will be used to validate the trained model. if this is not provided, Azure Machine Learning will apply cross-validation using the training data.

Alternatively:

* Specify a dataset, dataframe, or numpy array of X values containing the training features, with a corresponding y array of label values.
* Optionally, specify X_valid and y_valid datasets, dataframes, or numpy arrays of X_valid values to be used for validation.

### Specify the primary metric
One of the most important settings you must specify is the **primary_metric**. This is the target performance metric for which the optimal model will be determined. Azure Machine Learning supports a set of named metrics for each type of task. To retrieve the list of metrics available for a particular task type, you can use the **get_primary_metrics** function as shown here:

    from azureml.train.automl.utilities import get_primary_metrics

      get_primary_metrics('classification')
      
**More Information:** You can find a full list of primary metrics and their definitions in [Understand automated machine learning results](https://aka.ms/AA70rrw).  

### Submit an automated machine learning experiment
You can submit an automated machine learning experiment like any other SDK-based experiment.

      from azureml.core.experiment import Experiment

      automl_experiment = Experiment(ws, 'automl_experiment')
      automl_run = automl_experiment.submit(automl_config)
      
 You can monitor automated machine learning experiment runs in Azure Machine Learning studio, or in the Jupyter Notebooks **RunDetails** widget.   
 
### Retrieve the best run and its model
You can easily identify the best run in Azure Machine Learning studio, and download or deploy the model it generated. To accomplish this programmatically with the SDK, you can use code like the following example: 

      best_run, fitted_model = automl_run.get_output()
      best_run_metrics = best_run.get_metrics()
      for metric_name in best_run_metrics:
          metric = best_run_metrics[metric_name]
          print(metric_name, metric)
          
### Explore preprocessing steps
Automated machine learning uses scikit-learn pipelines to encapsulate preprocessing steps with the model. You can view the steps in the fitted model you obtained from the best run using the code above like this:    

      for step_ in fitted_model.named_steps:
          print(step_)
          
## Exercise  - Using automated machine learning

Determining the right algorithm and preprocessing transformations for model training can involve a lot of guesswork and experimentation.

In this exercise, you’ll use automated machine learning to determine the optimal algorithm and preprocessing steps for a model by performing multiple training runs in parallel.

### Before you start

If you have not already done so, create a [compute instance](../Documents/Create-Compute-Instance.md) and ensure you have [Cloned the notebooks](../Documents/Clone-and-Run-a-Notebook.md) required for this exercise.

### Additional Information to note as you're working through your notebook

After creating a compute cluster to deploy your model you can view it selecting the **compute** page in [Azure Machine Learning studio](https://ml.azure.com/?tid=168c1fe3-a841-49b5-b692-7b3132c0a997&wsid=/subscriptions/52cbf6c7-01f2-4df2-bae9-c80cee4db7eb/resourcegroups/churn-prediction-azure-tutorial/workspaces/churn-machine-learning-ws) and clicking on **Compute clusters** at the top of the page. 

### Open Jupyter

1. In Azure Machine Learning studio, view the **Compute** page for your workspace and on the **Compute Instances** tab, start your compute instance if it is not already running.
2. When the compute instance is running, click the **Jupyter** link to open the Jupyter home page in a new browser tab. Be sure to open Jupyter and not JupyterLab.

### Use the SDK to run an automated machine learning experiment
In this exercise, the code to run an automated machine learning experiment is provided in a notebook.

1. In the Jupyter home page, browse to the Users/<user_name>/labs folder where you cloned the notebook repository, and open the **Use-Automated-Machine-Learning.ipynb** notebook.
2. Then read the notes in the notebook, running each code cell in turn.
3. When you have finished running the code in the notebook, on the **File** menu, click **Close and Halt** to close it and shut down its Python kernel. Then close all Jupyter browser tabs.

### Clean-up
If you’re finished working with Azure Machine Learning for now refer to [this page](../Documents/Stop-Compute-Instance.md) to stop your compute instance.           
          

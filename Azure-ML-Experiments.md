# Azure Machine Learning experiments

Like any scientific discipline, data science involves running experiments; typically to explore data or to build and evaluate predictive models. In Azure Machine Learning, an experiment is a named process, usually the running of a script or a pipeline, that can generate metrics and outputs and be tracked in the Azure Machine Learning workspace.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/Azure-ML-Experiments.PNG)

An experiment can be run multiple times, with different data, code, or settings; and Azure Machine Learning tracks each run, enabling you to view run history and compare results for each run.

## The Experiment Run Context
When you submit an experiment, you use its run context to initialize and end the experiment run that is tracked in Azure Machine Learning, as shown in the following code sample:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/1.PNG)

## Logging Metrics and Creating Outputs
Experiments are most useful when they produce metrics and outputs that can be tracked across runs.

### Logging Metrics
Every experiment generates log files that include the messages that would be written to the terminal during interactive execution. This enables you to use simple print statements to write messages to the log. However, if you want to record named metrics for comparison across runs, you can do so by using the Run object; which provides a range of logging functions specifically for this purpose. These include:

* **log:** Record a single named value.
* **log_list:** Record a named list of values.
* **log_row:** Record a row with multiple columns.
* **log_table:** Record a dictionary as a table.
* **log_image:** Record an image file or a plot.

**More Information:** For more information about logging metrics during experiment runs, see [Monitor Azure ML experiment runs and metrics](https://aka.ms/AA70zf6) in the Azure Machine Learning documentation.

As an example, the following code records the number of observations (records) in a CSV file:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/2.PNG)

### Retrieving and Viewing Logged Metrics
You can view the metrics logged by an experiment run in Azure Machine Learning studio or by using the **RunDetails** widget in a notebook, as shown here:

`from azureml.widgets import RunDetails`

`RunDetails(run).show()`

You can also retrieve the metrics using the **Run** object's **get_metrics** method, which returns a JSON representation of the metrics, as shown here:

`import json`

`# Get logged metrics`


`metrics = run.get_metrics()`

`print(json.dumps(metrics, indent=2))`

The previous code might produce output similar to this:

`{`

  `"observations": 15000`
  
`}` 

## Experiment Output Files
In addition to logging metrics, an experiment can generate output files. Often these are trained machine learning models, but you can save any sort of file and make it available as an output of your experiment run. The output files of an experiment are saved in its **outputs** folder.

The technique you use to add files to the outputs of an experiment depend on how you're running the experiment. The examples shown so far control the experiment lifecycle inline in your code, and when taking this approach you can upload local files to the run's **outputs** folder by using the **Run** object's **upload_file** method in your experiment code as shown here:

`run.upload_file(name='outputs/sample.csv', path_or_stream='./sample.csv')`

When running an experiment in a remote compute context (which we'll discuss later in this course), any files written to the **outputs** folder in the compute context are automatically uploaded to the run's **outputs** folder when the run completes.

Whichever approach you use to run your experiment, you can retrieve a list of output files from the **Run** object like this:

`import json`

`files = run.get_file_names()`

`print(json.dumps(files, indent=2))`

The previous code would produce output similar to this:

`[`

  `"outputs/sample.csv"`
  
`]`

## Running a Script as an Experiment
You can run an experiment inline using the `start_logging` method of the **Experiment** object, but it's more common to encapsulate the experiment logic in a script and run the script as an experiment. The script can be run in any valid compute context, making this a more flexible solution for running experiments as scale.

An experiment script is just a Python code file that contains the code you want to run in the experiment. To access the experiment run context (which is needed to log metrics) the script must import the `azureml.core.Run` class and call its `get_context` method. The script can then use the run context to log metrics, upload files, and complete the experiment, as shown in the following example:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/3.PNG)

To run a script as an experiment, you must define a *script configuration* that defines the script to be run and the Python environment in which to run it. This is implemented by using a **ScriptRunConfig** object.

For example, the following code could be used to run an experiment based on a script in the **experiment_files** folder (which must also contain any files used by the script, such as the *data.csv* file in previous script code example):

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/4.PNG)

**!Note:** 
An implicitly created RunConfiguration object defines the Python environment for the experiment, including the packages available to the script. If your script depends on packages that are not included in the default environment, you must associate the ScriptRunConfig with an Environment object that makes use of a CondaDependencies object to specify the Python packages required. Runtime environments are discussed in more detail later in this course.

## Run Experiments

In this tutorial we provide some jupyter notebook templates (more detail in: _[Jupyter Lab notebook templates](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/tree/main/labs)_). This examples is based on the one provided in order to run experiments.

### Before you start

If you have not already done so, create a [compute instance](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Azure-ML-Studio.md) and ensure you have [Cloning and Running a Notebook] (https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Clone-and-Run-a-Notebook.md) required for this exercise.

## Open Jupyter

1. In Azure Machine Learning studio, view the **Compute** page for your workspace; and on the Compute Instances tab, start your compute instance if it is not already running.
2. When the compute instance is running, click the **Jupyter** link to open the Jupyter home page in a new browser tab. Be sure to open Jupyter and not JupyterLab.


## Example on how to run experiments in a notebook
Experiments in Azure Machine Learning need to be initiated from some sort of *control layer*; often a script or program. In this exercise, you’ll use a notebook to control experiments.

1. In the Jupyter home page, browse to the Users/labs folder where you cloned the notebook repository, and open the **Run-Experiments.ipynb** notebook.

2. Then read the notes in the notebook, running each code cell in turn.

3. When you have finished running the code in the notebook, on the **File** menu, click **Close and Halt** to close it and shut down its Python kernel. Then close all Jupyter browser tabs.

### Clean-up
If you’re finished working with Azure Machine Learning for now refer to [this page](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Stop-Compute-Instance.md) to stop your compute instance.  

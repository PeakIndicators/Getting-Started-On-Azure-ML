# Monitor models with Azure Machine Learning

After a machine learning model has been deployed into production, it's important to understand how it is being used by capturing and viewing telemetry.

## Introduction

Application Insights is an application performance management service in Microsoft Azure that enables the capture, storage and analysis of telemetry data from applications. Refer to the complete [Azure Application Insights](https://docs.microsoft.com/en-gb/azure/azure-monitor/app/app-insights-overview) documentation for details.

![](../Images/78.PNG)

You can use Application Insights to monitor telemetry from many kinds of application, including applications that are not running in Azure. All that's required is a low-overhead instrumentation package to capture and send the telemetry data to Application Insights. The necessary package is already included in Azure Machine Learning Web services, so you can use it to capture and review telemetry from models published with Azure Machine Learning.

## Learning objectives

* Enable Application Insights monitoring for an Azure Machine Learning web service.
* Capture and view model telemetry.

## Enable Application Insights

## Using Python Notebooks

To log telemetry in application insights from an Azure machine learning service, you must have an Application Insights resource associated with your Azure Machine Learning workspace and you must configure your service to use it for telemetry logging.

### Associate Application Insights with a workspace

When you create an Azure Machine Learning Studio workspace, you can select an Azure Application Insights resource to associate with it. If you do not select an existing Application Insights resource, a new one is created in the same resource group as your Studio.

You can determine the Application Insights resource associated with your Studio by viewing the **Overview** page of the workspace blade in the Azure portal or by using the **get_details()** method of a **Workspace** object as shown in the following code example:

```
from azureml.core import Workspace

ws = Workspace.from_config()

ws.get_details()['applicationInsights']
```

### Enable Application Insights for a service

When deploying a new real-time service, you can enable Application Insights in the deployment configuration for the service, as shown in this example:

![](../Images/79.PNG)

If you want to enable Application Insights for a service that is already deployed, you can modify the deployment configuration for Azure Kubernetes Service (AKS) based services in the Azure portal. Alternatively, you can update any web service by using the Azure Machine Learning SDK, like this:
```
service = ws.webservices['my-svc']
service.update(enable_app_insights=True)
```
## Capture and view telemetry

Application Insights automatically captures any information written to the standard output and error logs and provides a query capability to view data in these logs.

### Write log data
To capture telemetry data for Application insights, you can write any values to the standard output log in the scoring script for your service by using a `print` statement, as shown in the following example:

```
import pickle
import json
import numpy 
from sklearn.externals import joblib
from sklearn.linear_model import Ridge
from azureml.core.model import Model
import time

def init():
    global model
    #Print statement for appinsights custom traces:
    print ("model initialized" + time.strftime("%H:%M:%S"))

    # note here "sklearn_regression_model.pkl" is the name of the model registered under the workspace
    # this call should return the path to the model.pkl file on the local disk.
    model_path = Model.get_model_path(model_name = 'sklearn_regression_model.pkl')

    # deserialize the model file back into a sklearn model
    model = joblib.load(model_path)


# note you can pass in multiple rows for scoring
def run(raw_data):
    try:
        data = json.loads(raw_data)['data']
        data = numpy.array(data)
        result = model.predict(data)
        # Log the input and output data to appinsights:
        info = {
            "input": raw_data,
            "output": result.tolist()
            }
        print(json.dumps(info))
        # you can return any datatype as long as it is JSON-serializable
        return result.tolist()
    except Exception as e:
        error = str(e)
       print (error + time.strftime("%H:%M:%S"))
        return error
```

Azure Machine Learning creates a custom dimension in the Application Insights data model for the output you write.

### Configure logging with Azure Machine Learning studio
You can also enable Azure Application Insights from Azure Machine Learning studio. When you're ready to deploy your model as a web service, use the following steps to enable Application Insights:

1 - Sign in to [Azure ML Studio](https://ml.azure.com).

2 - Go to **Models** and select the model you want to deploy.

3 - Select **+Deploy**.

4 - Fill the Deploy model form.

5 - Expand the **Advanced** menu.

![](../Images/deploy-form.png)

6 - Select **Enable Application Insights diagnostics and data collection**.

![](../Images/enable-app-insights.png)

### View logged data and query logs in Application Insights
To analyze captured log data, you can use the Log Analytics query interface for Application Insights in the Azure portal. This interface supports a SQL-like query syntax that you can use to extract fields from logged data, including custom dimensions created by your Azure Machine Learning service. This SQL-like query syntax uses **Kusto query language**, more details can be seen [here](https://docs.microsoft.com/en-us/services-hub/health/log_analytics_query_language).

To view logged data:

* In the [Azure portal](https://portal.azure.com/#home), open your machine learning workspace. 

* On the **Overview** page, click the link for the associated **Application Insights resource**.

![](../Images/85.PNG)

* In the Application Insights blade, click **Logs**.

![](../Images/86.PNG)

**Note**: If this is the first time you've opened log analytics, you may need to click **Get Started** to open the query editor. If a tip explaining how to write a query is displayed, close it.

![](../Images/87.PNG)

* Paste the following query into the query editor and click **Run**

`traces`

`|where  message == "STDOUT"`

`and customDimensions.["Service Name"] == "diabetes-service-app-insights"`

`|project timestamp, customDimensions.Content`

![](../Images/89.PNG)

* View the results. At first there may be none, because an ACI web service can take as long as five minutes to send the telemetry to Application Insights. 
Wait a few minutes and re-run the query until you see the logged data and predictions simialarly to what is shown below

![](../Images/90.PNG)

As an example of querying logs using Python on Jupyterlab, the query below returns the `timestamp` and `customDimensions.Content` fields from log traces that have a message field value of STDOUT (indicating the data is in the standard output log) and a customDimensions.["Service Name"] field value of *my-svc*:

![](../Images/80.PNG)

This query returns the logged data as a table:

|timestamp|customDimensions_content|
|-------|-------|
|01/02/2020...	|Data:[[1, 2, 2.5, 3.1], [0, 1, 1,7, 2.1]] - Predictions:[0 1]|
|01/02/2020...	|Data:[[3, 2, 1.7, 2.0]] - Predictions:[0]|

## Exercise - Monitor a model

### Before you start

In this tutorial we provide some jupyter notebook templates that you can run (more detail in: [Jupyter Lab notebook templates](../labs)).

If you have not already done so, create a [compute instance](../Documents/Create-Compute-Instance.md) and ensure you have [cloned the notebooks](../Documents/Clone-and-Run-a-Notebook.md) required for this exercise.

### Open Jupyter

1. In Azure Machine Learning studio, view the **Compute** page for your workspace and on the Compute Instances tab, start your compute instance if it is not already running.
2. When the compute instance is running, click the **Jupyter** link to open the Jupyter home page in a new browser tab. Be sure to open Jupyter and not JupyterLab.

### Use Application Insights to monitor a real-time service
In this exercise, the code to configure application insights for a deployed predictive service is provided in a notebook.

1. In the Jupyter home page, browse to the Users/<user_name>/labs folder where you cloned the notebook repository and open the **Monitor_a_Model.ipynb** notebook.

2. Then read the notes in the notebook, running each code cell in turn.

3. When you have finished running the code in the notebook, on the **File** menu, click **Close and Halt** to close it and shut down its Python kernel. Then close all Jupyter browser tabs.

### Clean-up
If you’re finished working with Azure Machine Learning for now refer to [this page](../Documents/Stop-Compute-Instance.md) to stop your compute instance. 

_Source: https://docs.microsoft.com/en-us/azure/machine-learning/monitor-azure-machine-learning and https://docs.microsoft.com/en-us/azure/machine-learning/how-to-enable-app-insights_

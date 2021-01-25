# Connect to data with the Azure Machine Learning studio - Dataset Creation using the web portal

## Introduction to data connection in Azure Machine Learning Studio

In Azure Machine Learning Studio you can:
* Access your data without using code. 

* Connect to your data in storage services on Azure with [Azure Machine Learning datastores](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-access-data), and then package that data for tasks in your ML workflows with [Azure Machine Learning datasets](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-create-register-datasets).

The following table defines and summarizes the benefits of datastores and datasets.

| **Object** | **Description** | **Benefits** |
| ---------- | -------------- | ---------------- |
|Datastores | Securely connect to your storage service on Azure, by storing your connection information, like your subscription ID and token authorization in your [Key Vault](https://azure.microsoft.com/services/key-vault/) associated with the workspace | Because your information is securely stored, you: <ul><li>Don't put authentication credentials or original data sources at risk.</li><li>No longer need to hard code them in your scripts.</li></ul>|
|Datasets | By creating a dataset, you create a reference to the data source location, along with a copy of its metadata. With datasets you can: <ul><li> Access data during model training.</li><li>Share data and collaborate with other users.</li><li>Leverage open-source libraries, like pandas, for data exploration</li></ul> | Because datasets are lazily evaluated, and the data remains in its existing location, you: <ul><li>Keep a single copy of data in your storage.</li><li> Incur no extra storage cost.</li><li> Don't risk unintentionally changing your original data sources.</li><li>Improve ML workflow performance speeds.</li></ul>|

In this section we will explain how to create a Dataset.


## Create datasets

After you create a datastore, create a dataset to interact with your data. Datasets package your data into a lazily evaluated consumable object for machine learning tasks, like training. [Learn more about datasets](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-create-register-datasets).

There are two types of datasets, FileDataset and TabularDataset. 
[FileDatasets](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-create-register-datasets#filedataset) create references to single or multiple files or public URLs. Whereas, [TabularDatasets](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-create-register-datasets#tabulardataset) represent your data in a tabular format.

The following steps and animation show how to create a dataset in Azure Machine Learning studio.

1. Sign in to the [Azure Machine Learning studio](https://ml.azure.com/).

2. Select **Datasets** in the **Assets** section of the left pane.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/dataset1.PNG)

3. Select **Create Dataset** to choose the source of your dataset. This source can be local files, a datastore, public URLs, or [Azure Open Datasets](https://docs.microsoft.com/en-us/azure/open-datasets/how-to-create-azure-machine-learning-dataset-from-open-dataset).

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/dataset2.PNG)

4. Assign a **Name** to your dataset (rule: Dataset name cannot have trailing whitespace), select **Tabular** or **File** for Dataset type and provide a description of it. 

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/dataset3.PNG)

5. Select **Next** to open the **Datastore and file selection** form. On this form you select where to keep your dataset after creation, as well as select what data files to use for your dataset. 

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/dataset4.PNG)

     * If you leave unchecked the option **Skip Data Validation** then studio will not validate the data path or try to access the data for preview and schema.

     * For Tabular datasets, you can specify a 'timeseries' trait to enable time related operations on your dataset. Learn how to [add the timeseries trait to your dataset](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-monitor-datasets#studio-dataset).

6. Select **Next** to populate the **Settings and preview** and **Schema** forms; they are intelligently populated based on file type and you can further configure your dataset prior to creation on these forms.

**Settings and preview**
![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/dataset5.PNG)

**Schema**
![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/dataset6.PNG)

7. Select **Next** to review the **Confirm details** form. Check your selections and create an optional data profile for your dataset. Learn more about [data profiling](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-connect-data-ui#profile).

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/dataset7.PNG)

8. Select **Create** to complete your dataset creation.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/dataset8.PNG)

## Data profile and preview
After you create your dataset, verify you can view the profile and preview in the studio with the following steps.

1. Select **Datasets** in the **Assets** section of the left pane.

2. Select the name of the dataset you want to view.

3. Select the **Explore** tab.

4. Select the **Preview** or **Profile** tab.

![](https://docs.microsoft.com/en-us/azure/machine-learning/media/how-to-connect-data-ui/dataset-preview-profile.gif)

You can get a vast variety of summary statistics across your data set to verify whether your data set is ML-ready. For non-numeric columns, they include only basic statistics like min, max, and error count. For numeric columns, you can also review their statistical moments and estimated quantiles.

Specifically, Azure Machine Learning dataset's data profile includes:

**Note:** Blank entries appear for features with irrelevant types.

| Statistic |	Description |
| --------- | ----------- |
| Feature |	Name of the column that is being summarized. |
| Profile |	In-line visualization based on the type inferred. For example, strings, booleans, and dates will have value counts, while decimals (numerics) have approximated histograms. This allows you to gain a quick understanding of the distribution of the data. |
| Type distribution	| In-line value count of types within a column. Nulls are their own type, so this visualization is useful for detecting odd or missing values. |
| Type |	Inferred type of the column. Possible values include: strings, booleans, dates, and decimals. |
| Min |	Minimum value of the column. Blank entries appear for features whose type does not have an inherent ordering (like, booleans). |
| Max |	Maximum value of the column. |
| Count	| Total number of missing and non-missing entries in the column. |
| Not missing count |	Number of entries in the column that are not missing. Empty strings and errors are treated as values, so they will not contribute to the "not missing count."| 
| Quantiles	| Approximated values at each quantile to provide a sense of the distribution of the data.| 
| Mean |	Arithmetic mean or average of the column. |
| Standard deviation | Measure of the amount of dispersion or variation of this column's data. |
| Variance |Measure of how far spread out this column's data is from its average value. |
| Skewness |	Measure of how different this column's data is from a normal distribution. |
| Kurtosis |	Measure of how heavily tailed this column's data is compared to a normal distribution. |


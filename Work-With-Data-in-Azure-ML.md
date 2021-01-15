# Connect to data with the Azure Machine Learning studio

This document will detail how:
* You can access your data without using code. 

* Connect to your data in storage services on Azure with [Azure Machine Learning datastores](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-access-data), and then package that data for tasks in your ML workflows with [Azure Machine Learning datasets](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-create-register-datasets).

The following table defines and summarizes the benefits of datastores and datasets.

| **Object** | **Description** | **Benefits** |
| ---------- | -------------- | ---------------- |
|Datastores | Securely connect to your storage service on Azure, by storing your connection information, like your subscription ID and token authorization in your [Key Vault](https://azure.microsoft.com/services/key-vault/) associated with the workspace | Because your information is securely stored, you: <ul><li>Don't put authentication credentials or original data sources at risk.</li><li>No longer need to hard code them in your scripts.</li></ul>|
|Datasets | By creating a dataset, you create a reference to the data source location, along with a copy of its metadata. With datasets you can: <ul><li> Access data during model training.</li><li>Share data and collaborate with other users.</li><li>Leverage open-source libraries, like pandas, for data exploration</li></ul> | Because datasets are lazily evaluated, and the data remains in its existing location, you: <ul><li>Keep a single copy of data in your storage.</li><li> Incur no extra storage cost.</li><li> Don't risk unintentionally changing your original data sources.</li><li>Improve ML workflow performance speeds.</li></ul>|


## Introduction to datastores

In Azure Machine Learning, *datastores* are abstractions for cloud data sources. They encapsulate the information required to connect to data sources. You can access datastores directly in code by using the Azure Machine Learning SDK, and use it to upload or download data.

### Types of Datastore
Azure Machine Learning supports the creation of datastores for multiple kinds of Azure data source, including:

* Azure Storage (blob and file containers)
* Azure Data Lake stores
* Azure SQL Database
* Azure Databricks file system (DBFS)

### Built-in Datastores
Every workspace has two built-in datastores (an Azure Storage blob container, and an Azure Storage file container) that are automatically registered as datastores to the workspace and are used as system storage by Azure Machine Learning.  They're named `workspaceblobstore` and `workspacefilestore`, respectively. If blob storage is sufficient for your needs, the `workspaceblobstore` is set as the default datastore, and already configured for use.

In most machine learning projects, you will likely need to work with data sources of your own - either because you need to store larger volumes of data than the built-in datastores support, or because you need to integrate your machine learning solution with data from existing applications

  
 ## Create datastores

 To create a new datastore in a few steps with the Azure Machine Learning studio:
 
1. Sign in to Azure Machine Learning studio.
2. Select **Datastores** on the left pane under **Manage**.
3. Select + **New datastore**.
4. Complete the form to create and register a new datastore. See the [storage access and permissions section](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-connect-data-ui#access-validation) if you need support on how to find the authentication credentials you need to populate this form.

The following example demonstrates what the form looks like when you create an **Azure blob datastore**:

![](https://docs.microsoft.com/en-us/azure/machine-learning/media/how-to-connect-data-ui/new-datastore-form.png)

## Create datasets

After you create a datastore, create a dataset to interact with your data. Datasets package your data into a lazily evaluated consumable object for machine learning tasks, like training. [Learn more about datasets](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-create-register-datasets).

There are two types of datasets, FileDataset and TabularDataset. [FileDatasets](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-create-register-datasets#filedataset) create references to single or multiple files or public URLs. Whereas, [TabularDatasets](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-create-register-datasets#tabulardataset) represent your data in a tabular format.

The following steps and animation show how to create a dataset in [Azure Machine Learning studio](https://ml.azure.com/).

**Note**—Datasets created through Azure Machine Learning studio are automatically registered to the workspace.

![](https://docs.microsoft.com/en-us/azure/machine-learning/media/how-to-connect-data-ui/create-dataset-ui.gif)

To create a dataset in the studio:

1. Sign in to the [Azure Machine Learning studio](https://ml.azure.com/).

2. Select **Datasets** in the **Assets** section of the left pane.

3. Select **Create Dataset** to choose the source of your dataset. This source can be local files, a datastore, public URLs, or [Azure Open Datasets](https://docs.microsoft.com/en-us/azure/open-datasets/how-to-create-azure-machine-learning-dataset-from-open-dataset).

4. Select **Tabular** or **File** for Dataset type.

5. Select **Next** to open the **Datastore and file selection** form. On this form you select where to keep your dataset after creation, as well as select what data files to use for your dataset. 

  * Enable skip validation if your data is in a virtual network. Learn more about [virtual network isolation and privacy](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-enable-studio-virtual-network).

  * For Tabular datasets, you can specify a 'timeseries' trait to enable time related operations on your dataset. Learn how to [add the timeseries trait to your dataset](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-monitor-datasets#studio-dataset).

6. Select **Next** to populate the **Settings and preview** and **Schema** forms; they are intelligently populated based on file type and you can further configure your dataset prior to creation on these forms.

7. Select **Next** to review the **Confirm details** form. Check your selections and create an optional data profile for your dataset. Learn more about [data profiling](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-connect-data-ui#profile).

8. Select **Create** to complete your dataset creation.

## Data profile and preview
After you create your dataset, verify you can view the profile and preview in the studio with the following steps.

1. Sign in to the Azure Machine Learning studio

2. Select **Datasets** in the **Assets** section of the left pane.

3. Select the name of the dataset you want to view.

4. Select the **Explore** tab.

5. Select the **Preview** or **Profile** tab.

![](https://docs.microsoft.com/en-us/azure/machine-learning/media/how-to-connect-data-ui/dataset-preview-profile.gif)

You can get a vast variety of summary statistics across your data set to verify whether your data set is ML-ready. For non-numeric columns, they include only basic statistics like min, max, and error count. For numeric columns, you can also review their statistical moments and estimated quantiles.

Specifically, Azure Machine Learning dataset's data profile includes:

**note**—Blank entries appear for features with irrelevant types.

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

## Storage access and permissions
To ensure you securely connect to your Azure storage service, Azure Machine Learning requires that you have permission to access the corresponding data storage. This access depends on the authentication credentials used to register the datastore.

## Virtual network
If your data storage account is in a **virtual network**, additional configuration steps are required to ensure Azure Machine Learning has access to your data. See [Network isolation & privacy](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-enable-studio-virtual-network) to ensure the appropriate configuration steps are applied when you create and register your datastore.

## Access validation
**As part of the initial datastore creation and registration process**, Azure Machine Learning automatically validates that the underlying storage service exists and the user provided principal (username, service principal, or SAS token) has access to the specified storage.

**After datastore creation**, this validation is only performed for methods that require access to the underlying storage container, **not** each time datastore objects are retrieved. For example, validation happens if you want to download files from your datastore; but if you just want to change your default datastore, then validation does not happen.

To authenticate your access to the underlying storage service, you can provide either your account key, shared access signatures (SAS) tokens, or service principal according to the datastore type you want to create. The [storage type matrix](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-access-data#matrix) lists the supported authentication types that correspond to each datastore type.

You can find account key, SAS token, and service principal information on your [Azure portal](https://portal.azure.com/).

* If you plan to use an account key or SAS token for authentication, select **Storage Accounts** on the left pane, and choose the storage account that you want to register.
  The **Overview** page provides information such as the account name, container, and file share name.

    1. For account keys, go to **Access keys** on the **Settings pane**.

    2. For SAS tokens, go to **Shared access signatures** on the **Settings pane**.

* If you plan to use a [service principal](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal) for authentication, go to your **App registrations** and select which app you want to use.
  * Its corresponding **Overview** page will contain required information like tenant ID and client ID.

**Important**:
*If you need to change your access keys for an Azure Storage account (account key or SAS token), be sure to sync the new credentials with your workspace and the datastores connected to it. [Learn how to sync your updated credentials](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-change-storage-access-key).

## Permission 
For Azure blob container and Azure Data Lake Gen 2 storage, make sure your authentication credentials have **Storage Blob Data Reader** access. Learn more about [Storage Blob Data Reader](https://docs.microsoft.com/en-us/azure/role-based-access-control/built-in-roles#storage-blob-data-reader). An account SAS token defaults to no permissions.

* For data **read access**, your authentication credentials must have a minimum of list and read permissions for containers and objects.

* For data **write access**, write and add permissions also are required.

## Train with datasets
Use your datasets in your machine learning experiments for training ML models. [Learn more about how to train with datasets](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-train-with-datasets).

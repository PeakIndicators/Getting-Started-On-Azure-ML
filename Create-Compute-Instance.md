# Create a compute instance

One of the benefits of Azure Machine Learning is the ability to create cloud-based compute (*Compute Instances*) in a workspace to provide a development environment that is managed with all of the other assets in the workspace. These compute instances enable you to run experiments and training scripts at scale.

![](https://docs.microsoft.com/en-us/learn/wwl-data-ai/intro-to-azure-machine-learning-service/media/01-05-notebook-vm.jpg)

1. In Azure Machine Learning studio, view the Compute page. This is where you’ll manage compute resources for your data science activities. There are four kinds of compute resource you can create:

* **Compute instances:** Development workstations that data scientists can use to work with data and models.
* **Compute clusters:**  Scalable clusters of virtual machines for on-demand processing of experiment code.
* **Inference clusters:** Deployment targets for predictive services that use your trained models.
* **Attached compute:** Links to other Azure compute resources, such as Virtual Machines or Azure Databricks clusters.

For most scenarios a compute instance is enough for developing and testing code.  As a development environment, a compute instance cannot, however, be shared with other users in your workspace—each individual will have to create their own compute instance. 

2. On the **Compute instances** tab, add a new compute instance with the following settings. You’ll use this as a workstation to run code in notebooks.

* **Region:** *The same region as your workspace*
* **Virtual machine type:** Select *CPU* for general use unless you know your code will use GPU (example for training deep learning models
* **Virtual machine size:** *Standard_DS2_v2* if you want to run AutoML runs and pipeline runs select *Standard_DS3_v2*. Select a compute with higher RAM if you are training on large datasets or want to do real-time inferencing, etc.  

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/NewCompute1.PNG)

* **Compute name:** *enter a unique name*
* **Enable SSH access:** Unselected (you can use this to enable direct access to the virtual machine using an SSH client)
* **Show advanced settings:** Note the following settings, but do not select them unless you think you requore them:
    * **Enable virtual network:** Unselected (you would typically use this in an enterprise environment to enhance network security)
    * **Assign to another user:** Unselected (you can use this to assign a compute instance to a data scientist)
    
![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/NewCompute2.PNG)

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/NewCompute3.PNG)
  
3. Wait for the compute instance to start and its status to change to **Running**.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/NewCompute4.PNG)

## Stop Compute Instance

**When you are done with using your compute instance for now shut down your compute instance to avoid incurring unnecessary charges in your Azure subscription.**

To stop your compute instance:

* In Azure Machine Learning studio, on the **Compute** page, select your compute instance.

* Click **Stop** to stop your compute instance. When it has shut down, its status will change to **Stopped**.

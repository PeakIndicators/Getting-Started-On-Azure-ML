# Running a Jupyter notebook and installing Azure Machine Learning SDK

A lot of data science and machine learning experimentation is performed by running code in notebooks. Your compute instance includes fully featured Python notebook environments (Jupyter and JuypyterLab) that you can use for extensive work; but for basic notebook editing, you can use the built-in Notebooks page in Azure Machine learning studio.

1. In Azure Machine Learning studio, view the **Notebooks** page.
2. Open a **Terminal**, and ensure its **Compute** is set to your compute instance.

3. Enter the following commands to clone a Git repository containing notebooks, data, and other files to your workspace:

` cd Users`

 `git clone https://github.com/felicity-borg/Getting-Started-On-Azure-ML/tree/main/labs`
 
 4. When the command has completed, in the **My files** pane, click ↻ to refresh the view and verify that a new **Users/mslearn-dp100** folder has been created. This folder contains multiple **.ipynb** notebook files.
 
 5. In the terminal pane, enter the following command to upgrade the Azure Machine Learning SDK and notebook widgets python packages to the latest version (these packages are used in most of the notebooks):
 
 ` pip install --upgrade azureml-sdk azureml-widgets`
 
 You may see some warnings as the package dependencies are installed. You can ignore these.
 
 6. Close the terminal pane, terminating the session.
 
 7. In the **Users/mslearn-dp100 folder**, open the **Get Started with Notebooks** notebook. Then read the notes and follow the instructions it contains to learn how to connect to your Azure ML workspace, view resources and run cells. 
 
 **Tip:** To run a code cell, select the cell you want to run and then use the ▷ button to run it.
 
 ## Stop your compute instance
 
 When you are done with using your compute instance shut down your compute instance to avoid incurring unnecessary charges in your Azure subscription.
 
 1. In Azure Machine Learning studio, on the **Compute** page, select your compute instance.
 
2. Click **Stop** to stop your compute instance. When it has shut down, its status will change to **Stopped**.


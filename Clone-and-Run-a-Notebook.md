# Clone and run a notebook

A lot of data science and machine learning experimentation is performed by running code in notebooks. Your compute instance includes fully featured Python notebook environments (Jupyter and JuypyterLab) that you can use for extensive work; but for basic notebook editing, you can use the built-in Notebooks page in Azure Machine learning studio.

1. In Azure Machine Learning studio, view the **Notebooks** page.
2. Open a **Terminal**, and ensure its **Compute** is set to your compute instance.

3. Enter the following commands to clone a Git repository containing notebooks, data, and other files to your workspace:

` cd Users`

 `git clone https://github.com/MicrosoftLearning/mslearn-dp100`
 
 4. When the command has completed, in the My files pane, click ↻ to refresh the view and verify that a new Users/mslearn-dp100 folder has been created. This folder contains multiple .ipynb notebook files.


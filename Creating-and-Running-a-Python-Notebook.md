# Creating and Running a Python or R Notebook

There are 3 possible ways of creating and running python notebooks in Azure Machine Learning studio:

1. Running those directly in the portal
2. Using the Jupyter option provided on the compute instance
3. Using the JupyterLab option provided on the compute instance

The next sections will explain how to use eaxh of the options described above.

### Before you start

If you have not already done so, create a [compute instance](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Azure-ML-Studio.md)

## Notebooks directly in your Azure Machine Learning studio
In your Azure Machine Learning studio, create a new Jupyter notebook and start working. The newly created notebook is stored in the default studio storage. This notebook can be shared with anyone with access to the studio.

To create a new notebook:

1. Sign in to [Azure Machine Learning studio](https://ml.azure.com/).

2. On the left side, select Notebooks.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/create-new-notebook1.PNG)

3. Select the icon **Create new file** which is under the Files section.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/create-new-notebook2.PNG)

4. Name the file. For Jupyter notebook Files, select Notebook as the file type (you can also create text files. Select Text as the file type and add the extension to the name (for example, myfile.py or myfile.txt)). Select a file directory and finally select Create.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/create-new-notebook3.PNG)

5. Once the file is created it will appear under your user name.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/create-new-notebook4.PNG)

6. Double click on the file name to open it

You can also upload folders and files, including notebooks, with the tools at the top of the Notebooks page. Notebooks and most text file types display in the preview section. No preview is available for most other file types.










## Clone samples
Your workspace contains a Samples folder with notebooks designed to help you explore the SDK and serve as examples for your own machine learning projects. You can clone these notebooks into your own folder on your workspace storage container.

## Use files from Git and version my files
You can access all Git operations by using a terminal window. All Git files and folders will be stored in your workspace file system.


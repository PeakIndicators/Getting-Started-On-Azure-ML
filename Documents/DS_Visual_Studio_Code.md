# Data Science in Visual Studio Code

## Set up a data science environment

Visual Studio Code and the Python extension provides a great editor for data science scenarios. With native support for Jupyter notebooks combined with Anaconda, it's easy to get started. In this section, you will create a workspace for the tutorial, create an Anaconda environment with the data science modules needed for the tutorial and create a Jupyter notebook that you'll use to create a machine learning model.

1. Begin by creating an Anaconda environment for the data science tutorial. Refer to [Getting started with Conda](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Documents/Starting_with_conda.md) for details on how to install conda. Open an Anaconda command prompt and run `conda create -n myenv python=3.9 pandas jupyter seaborn scikit-learn keras tensorflow` to create an environment named **myenv**. For additional information about creating and managing Anaconda environments, navigate to this [page](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Documents/Starting_with_conda.md).

2. Next, create a folder in a convenient location to serve as your VS Code workspace for the tutorial, name it `hello_ds`.

3. Open the project folder in VS Code by running VS Code and using the **File > Open Folder command**.

4. Once VS Code launches, open the Command Palette **(View > Command Palette** or `Ctrl+Shift+P`). Then select the **Python: Select Interpreter command**:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/VS25.PNG)

5. The **Python: Select Interpreter** command presents the list of available interpreters that VS Code was able to locate automatically (your list will vary from the one shown below), including virtual environments. If you don't see the desired interpreter, select *Enter interpreter path...* .
Select the Python Interpreter you want to use for your project. This should be the virtual environment your created with conda, which should include the text 'myenv': conda.

**Note:** When using an Anaconda distribution, the correct interpreter should have the suffix `('envname':conda)`, for example `Python 3.7.3 64-bit ('envname':conda)`.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/VS5.PNG) 

Select the Python Interpreter you want to use for your project. This should be the virtual environment your created with conda. 

You can also use the **Select Python Environment** option on the Status Bar if available (it may already show a selected interpreter, too):

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/VS6.PNG) 
&nbsp;

6. With the environment and VS Code setup, the final step is to create the Jupyter notebook that will be used for the tutorial. Open the Command Palette (`Ctrl+Shift+P`) and select **Jupyter: Create New Blank Jupyter Notebook**.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/VS26.PNG) 


**Note:** Alternatively, from the VS Code File Explorer, you can use the New File icon to create a Notebook file named `hello.ipynb`.

7. Use the Save icon on the main notebook toolbar to save the notebook with the filename `hello`.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/VS27.PNG) 

8. After your file is created, you should see the open [Jupyter notebook](https://jupyter.org/) in the native notebook editor. For additional information about native Jupyter notebook support, see [this page](https://code.visualstudio.com/docs/python/jupyter-support).

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/VS28.PNG) 

## Prepare the data

This tutorial uses the [Titanic dataset](https://hbiostat.org/data/repo/titanic3.csv) available on [OpenML.org](https://www.openml.org/d/40945), which is obtained from [Vanderbilt University's Department of Biostatistics](https://biostat.app.vumc.org/wiki/Main/DataSets). The Titanic data provides information about the survival of passengers on the Titanic, as well as characteristics about the passengers such as age and ticket class. Using this data, the tutorial will establish a model for predicting whether a given passenger would have survived the sinking of the Titanic. This section shows how to load and manipulate data in your Jupyter notebook.

1. To begin, download the Titanic data from [OpenML.org](https://www.openml.org/d/40945) as a csv file named `data.csv` and save it to the `hello_ds` folder that you created in the previous section.

2. In VS Code, open the `hello_ds` folder and the Jupyter notebook (`hello.ipynb`) by going to **File > Open Folder**.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/VS29.PNG)

3. Within your Jupyter notebook begin by importing the [pandas](https://pandas.pydata.org/) and [numpy](https://numpy.org/) libraries (these have already been installed when you created the conda virtual environment above). These are two common libraries used for manipulating data and loading the Titanic data into a pandas [DataFrame](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html). To do so, copy the below code into the first cell of the notebook. For additional guidance about working with Jupyter notebooks in VS Code, see the [Working with Jupyter Notebooks](https://code.visualstudio.com/docs/python/jupyter-support) documentation. If you need more information on importing and installing packages refer to Import and Install packages in [here](Getting Started with Python in VS Code).

`import pandas as pd`
`import numpy as np`
`data = pd.read_csv('data.csv)`

4. Now, run the cell using the Run cell icon or the `Shift+Enter` shortcut.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/VS30.PNG)

5. After the cell finishes running, you can view the data that was loaded using the variable explorer and data viewer. First click on the chart icon in the notebook's upper toolbar, then the data viewer icon to the right of the `data` variable. For additional information about the data set, refer to [this document](http://biostat.mc.vanderbilt.edu/wiki/pub/Main/DataSets/titanic3info.txt) about how it was build.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main//Images/31.PNG)

You can then use the data viewer to view, sort and filter data rows. After reviewing the data, it can then be helpful to graph some aspects of it to help visualize the relationships between the different variables.

6. Before the data can be graphed though, you need to make sure that there aren't any issues with it. If you look at the Titanic .csv file, one thing you'll notice is that a question mark ("?") was used to designate cells where data wasn't available.

While Pandas can read this value into a DataFrame, the result for a column like Age is that its data type will be set to Object instead of a Numeric data type, which is problematic for graphing.

This problem can be rectified by replacing the question mark with a missing value that pandas is able to understand. Add the following code to the next cell in your notebook to replace the question marks in the **age** and **fare** columns with the [numpy NaN](https://docs.scipy.org/doc/numpy/reference/constants.html?highlight=nan#numpy.nan) value. Notice that we also need to update the column's data type after replacing the values.

**Tip**: To add a new cell you can use the insert cell icon that's in the bottom left corner of an existing cell. Alternatively, you can also use the `Esc` to enter command mode followed by the `B` key.

`data.replace('?', np.nan, inplace= True)`
`data = data.astype({"age": np.float64, "fare": np.float64})`

**Note**: If you ever need to see the data type that has been used for a column, you can use the [DataFrame dtypes](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.dtypes.html#pandas.DataFrame.dtypes) attribute.

7. Now that the data is in good shape, you can use [seaborn](https://seaborn.pydata.org/) and [matplotlib](https://matplotlib.org/) to view how certain columns of the dataset relate to survivability. Add the following code to the next cell in your notebook and run it to see the generated plots.

`import seaborn as sns`
`import matplotlib.pyplot as plt`

`fig, axs = plt.subplots(ncols=5, figsize=(30,5))`
`sns.violinplot(x="survived", y="age", hue="sex", data=data, ax=axs[0])`
`sns.pointplot(x="sibsp", y="survived", hue="sex", data=data, ax=axs[1])`
`sns.pointplot(x="parch", y="survived", hue="sex", data=data, ax=axs[2])`
`sns.pointplot(x="pclass", y="survived", hue="sex", data=data, ax=axs[3])`
`sns.violinplot(x="survived", y="fare", hue="sex", data=data, ax=axs[4])`

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/32.PNG) 

**Note**: To better view details on the graphs, you can open them in plot viewer by hovering over the upper left corner of the graph and clicking the button that appears.

8. These graphs are helpful in seeing some of the relationships between survival and the input variables of the data, but it's also possible to use **pandas** to calculate correlations. To do so, all the variables used need to be numeric for the correlation calculation and currently gender is stored as a string. To convert those string values to integers, add and run the following code.

`data.replace({'male': 1, 'female': 0}, inplace=True)`

9. Now, you can analyze the correlation between all the input variables to identify the features that would be the best inputs to a machine learning model. The closer a value is to 1, the higher the correlation between the value and the result. Use the following code to correlate the relationship between all variables and survival.

`data.corr().abs()[["survived"]]`

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/33.PNG)

10. Looking at the correlation results, you'll notice that some variables like gender have a fairly high correlation to survival, while others like relatives (sibsp = siblings or spouse, parch = parents or children) seem to have little correlation.

Let's hypothesize that **sibsp** and **parch** are related in how they affect survivability and group them into a new column called "relatives" to see whether the combination of them has a higher correlation to survivability. To do this, you will check if for a given passenger, the number of **sibsp** and **parch** is greater than 0 and, if so, you can then say that they had a relative on board.

Use the following code to create a new variable and column in the dataset called **relatives** and check the correlation again.


`data['relatives'] = data.apply (lambda row: int((row['sibsp'] + row['parch']) > 0), axis=1)`
`data.corr().abs()[["survived"]]`

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/34.PNG)

11. You'll notice that in fact when looked at from the standpoint of whether a person had relatives, versus how many relatives, there is a higher correlation with survival. With this information in hand, you can now drop from the dataset the low value **sibsp** and **parch** columns, as well as any rows that had **NaN** values, to end up with a dataset that can be used for training a model.

`data = data[['sex', 'pclass','age','relatives','fare','survived']].dropna()`

**Note**: Although **age** had a low direct correlation, it was kept because it seems reasonable that it might still have correlation in conjunction with other inputs.

## Train and evaluate a model
With the dataset ready, you can now begin creating a model. For this section you'll use the [scikit-learn library](https://scikit-learn.org/stable/) to do pre-processing of the dataset, train a classification model to determine survivability on the Titanic and then use that model with test data to determine its accuracy.

1. A common first step to training a model is to divide up the dataset into training and validation data. This allows you to use a portion of the data to train the model and a portion of the data to test the model. If you used all your data to train the model, you wouldn't have a way to estimate how well it would actually perform against data the model has not yet seen. A benefit of the **scikit-learn** library is that it provides a method specifically for splitting a dataset into **training** and **test** data.

Add and run a cell with the following code to the notebook to split up the data.

`from sklearn.model_selection import train_test_split`
`x_train, x_test, y_train, y_test = train_test_split(data[['sex','pclass','age','relatives','fare']], data.survived, test_size=0.2, random_state=0)`

2. Next, you'll normalize the inputs such that all features are treated equally. For example, within the dataset the values for age range from ~0-100, while gender is only a 1 or 0. By normalizing all the variables, you can ensure that the ranges of values are all the same. Use the following code in a new code cell to scale the input values

`from sklearn.preprocessing import StandardScaler`
`sc = StandardScaler()`
`X_train = sc.fit_transform(x_train)`
`X_test = sc.transform(x_test)`

3. There are a number of different machine learning algorithms that you could choose from to model the data and **scikit-learn** provides support for a number of them, as well as a chart to help select the one that's right for your scenario. For now, use the [Naïve Bayes algorithm](https://scikit-learn.org/stable/modules/naive_bayes.html), a common algorithm for classification problems. Add a cell with the following code to create and train the algorithm.

`from sklearn.naive_bayes import GaussianNB`
`model = GaussianNB()`
`model.fit(X_train, y_train)`

4. With a trained model, you can now try it against the **test** data set that was held back from training. Add and run the following code to predict the outcome of the test data and calculate the accuracy of the model.

`from sklearn import metrics`
`predict_test = model.predict(X_test)`
`print(metrics.accuracy_score(y_test, predict_test))`

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/35.PNG) 

Looking at the result of the test data, you'll see that the trained algorithm had a ~75% success rate at estimating survival.

## (Optional) Use a neural network to increase accuracy

A neural network is a model that uses weights and activation functions, modeling aspects of human neurons, to determine an outcome based on provided inputs. Unlike the machine learning algorithm you looked at previously, neural networks are a form of deep learning wherein you don't need to know an ideal algorithm for your problem set ahead of time. It can be used for many different scenarios and classification is one of them. For this section, you'll use the [Keras](https://keras.io/) library with [TensorFlow](https://www.tensorflow.org/) to construct the neural network, and explore how it handles the Titanic dataset.

1. The first step is to import the required libraries and to create the model. In this case, you'll use a [Sequential](https://keras.io/getting-started/sequential-model-guide/) neural network, which is a layered neural network wherein there are multiple layers that feed into each other in sequence.

`from keras.models import Sequential`
`from keras.layers import Dense`

`model = Sequential()`

2. After defining the model, the next step is to add the layers of the neural network. For now, let's keep things simple and just use three layers. Add the following code to create the layers of the neural network.

`model.add(Dense(5, kernel_initializer = 'uniform', activation = 'relu', input_dim = 5))`
`model.add(Dense(5, kernel_initializer = 'uniform', activation = 'relu'))`
`model.add(Dense(1, kernel_initializer = 'uniform', activation = 'sigmoid'))`

* The first layer will be set to have a dimension of 5, since you have 5 inputs: sex, pclass, age, relatives, and fare.
* The last layer must output 1, since you want a 1-dimensional output indicating whether a passenger would survive.
* The middle layer was kept at 5 for simplicity, although that value could have been different.
&nbsp;
The **rectified linear unit (relu)** activation function is used as a good general activation function for the first two layers, while the sigmoid activation function is required for the final layer as the output you want (of whether a passenger survives or not) needs to be scaled in the range of 0-1 (the probability of a passenger surviving).

You can also look at the summary of the model you built with this line of code:

`model.summary()`

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/6.PNG)

3. Once the model is created, it needs to be compiled. As part of this, you need to define what type of optimizer will be used, how loss will be calculated, and what metric should be optimized for. Add the following code to build and train the model. You'll notice that after training the accuracy is ~80%.

**Note**: This step may take anywhere from a few seconds to a few minutes to run depending on your machine.

`model.compile(optimizer="adam", loss='binary_crossentropy', metrics=['accuracy'])`
`model.fit(X_train, y_train, batch_size=32, epochs=50)`

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/37.PNG)

4. With the model built and trained its now time to see how it performs against the test data.

`y_pred = model.predict_classes(X_test)`
`print(metrics.accuracy_score(y_test, y_pred))`

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/38.PNG)

Similar to the training, you'll notice that you were able to get close to 80% accuracy in predicting survival of passengers. This result was better than the 75% accuracy from the Naive Bayes Classifier tried previously.


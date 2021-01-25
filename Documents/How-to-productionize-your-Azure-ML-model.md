# How to productionize your Azure ML model

Creating a model is just one part of a Machine Learning pipeline, arguably the easier part. 
To take the model to production and obtain benefits of it is a completely different game. 
"Productionizing a model" needs to be able to package the models, deploy the models, track and monitor these models in various deployment targets, collects metrics, use these metrics to determine the efficacy of these models and then enable retraining of the models on the basis of these insights and/or new data. To add to it, all this needs a mechanism that can be automated with the right knobs and dials to allow data science teams to be able to keep a tab and not allow the pipeline to go rogue, which could result in considerable business losses, as these data science models are often linked directly to customer actions.

This problem is very similar to what application development teams face with respect to managing apps and releasing new versions of it at regular intervals with improved features and capabilities. The app dev teams address these with DevOps, which is the industry standard for managing operations for an app dev cycle. To be able to replicate the same to machine learning cycles is not the easiest task.

For the development pahse, its life-cycle can be defined as:

<p align="center">
  <img src="https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/devops1.PNG">
</p>

##### _Source: https://subscription.packtpub.com/book/big_data_and_business_intelligence/9781838550356/1/ch01lvl1sec13/ml-development-life-cycle_

Things are fairly simple (process wise) until we get to the final stage **Integrate and Deploy** and it's continous integration with **Validating and Testing the Algorithm**. 

This is where the Azure Machine Learning studio glows the most. It presents the most complete and intuitive model lifecycle management experience alongside integrating with Azure DevOps and GitHub.

## Life-cycle management with Azure Machine Learning and Azure DevOps

1. The first task is to be able to version control these models. Now, the code generated, like the Python notebooks or scripts can be easily versioned controlled in GitHub/DevOps repositories and this is the recommended approach, but in addition to the notebooks and scripts you also need a way to version control the models, which are different entities than the python files. This is important as data scientists may create multiple versions of the model, and very easily lose track of these in search of better accuracy or performance. Azure Machine Learning provides a central model registry, which forms the foundation of the lifecycle management process. This repository enables version control of models, it stores model metrics, it allows for one-click deployment, and even tracks all deployments of the models so that you can restrict usage, in case the model becomes stale or its efficacy is no longer acceptable. Having this model registry is key as it also helps trigger other activities in the lifecycle when new changes appear or metrics cross a threshold.

2. The next step in the ML lifecycle management, after a data scientist has created and validated a model or an ML pipeline, is that it needs to be packaged, so that it can execute where it needs to be deployed.

Once these tasks are done, then a tight collaboration between the DevOps development team and the Data Scientists using Azure ML needs to kick-off.

**Azure DevOps** is the environment to manage app lifecycles and now it also enables data science teams and devOps teams to collaborate seamlessly and trigger new version of the code whenever certain conditions are met for the MLOps cycle, as they are the ones often leveraging the new versions of the ML models, infusing them into apps or updating inference call URLs, when desired.

This may sound simple and the most logical way of doing it, but nobody has been able to bring MLOps to life with such close-knit integration into the whole process. Azure Machine Learning does an amazing job of it enabling data science teams to become immensely productive.

The following flow represents a MLOps flow within Azure Machine Learning.

<p align="center">
  <img src="https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/devops2.PNG">
</p>

### Explaining MLOps flow within Azure Machine Learning and Azure DevOps

#### Train, Validate and Deploy the Model

The idea behing this model can be explained.

Once the data scientist is happy with the prediction developed in Azure Machine Learning, an Azure DevOps pipeline/release can be created to automate the process of training, registering and deploying the model and this is where the collaboration between DevOps Development Team and Data Science Team begins.

With this in mind, the following should be created in the Azure DevOps resource:

1. A Data Science project - _Team Responsible: DevOps Development Team_

2. Within the Data Science project, a new GIT repository should be created. - _Team Responsible: DevOps Development Team_

3. The following information should be added to the repository (note: the repository can be created outside Azure DevOps and can then be cloned into its). - _Team Responsible to odd the code: Data Science Team_ and  _Team Responsible to clone the repository, if needed: DevOps Development Team_

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/devops3.png)

**Note**: As you can check, this implies the creation of separate python files for training, scoring, testing and also configuration files. But it really depends on which step the user needs to start the deployment. More details are given below

4.  Once all the necessary code is added to the repository the following pipeline should be created with the following steps: - _Team Responsible: DevOps Development Team_
**Note:**
In this example the following steps are defined: Training, Register and Downloading the model. This is just an example and the user might want to train and register the model in an Azure ML notebook and in Azure DevOps he only wants do dowload the model in order to be able to deploy it, if that is the case then the pipeline should only start from task Download the Model onwards.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/devops4.png)

And variables can also be added to make the pipeline more clean:
![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/devops5.png)

The next step is to run the pipeline. The screenshot below shows an example of a successful running:
![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/devops6.png)

5. After each execution in order to verify the model, we can access Azure Machine Learning and verify that the model was trained and register: - _Team Responsible: Data Science Team_
![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/devops7.png)



<u>Releases: Peak DS Int ChurnPrediction</u>

The release has the following structure:
![mlops6](images/mlops_deployment.png)

The deployment tasks were defined as:
![mlops7](images/mlops_dep_pipeline.png)

The idea behind the creation of a Pipeline and Release Pipeline is that on the pipeline itself the user will be able to train the model as much as he needs and once the results are the expected then it can be released/deployed using the Release pipeline.


#### Monitor the Model
Once your model is deployed, you want to be able to collect metrics on the model. You want to ascertain that the model is drifting from its objective and that the inference is useful for the business. This means you capture a lot of metrics and analyze them. Azure Machine Learning enables this tracking of metrics for the model is a very efficient manner. The central model registry becomes the one place where all this hosted.

As you collect more metrics and additional data becomes available for training, there may be a need to be able to retrain the model in the hope of improving its accuracy and/or performance. Also, since this is a continuous process of integrations and deployment (CI/CD), there’s a need for this process to be automated. This process of retraining and effective CI/CD of ML models is the biggest strength of Azure Machine Learning.

#### Retrain the Model


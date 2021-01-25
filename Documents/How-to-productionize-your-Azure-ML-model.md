# How to productionize your Azure ML model

Creating a model is just one part of a Machine Learning pipeline, arguably the easier part. 
To take the model to production and obtain benefits of it is a completely different game. 
"Productionizing a model" needs to be able to package the models, deploy the models, track and monitor these models in various deployment targets, collects metrics, use these metrics to determine the efficacy of these models and then enable retraining of the models on the basis of these insights and/or new data. To add to it, all this needs a mechanism that can be automated with the right knobs and dials to allow data science teams to be able to keep a tab and not allow the pipeline to go rogue, which could result in considerable business losses, as these data science models are often linked directly to customer actions.

This problem is very similar to what application development teams face with respect to managing apps and releasing new versions of it at regular intervals with improved features and capabilities. The app dev teams address these with DevOps, which is the industry standard for managing operations for an app dev cycle. To be able to replicate the same to machine learning cycles is not the easiest task.

For the development pahse, its life-cycle can be defined as:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/devops1.PNG)

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



### MLOps flow within Azure Machine Learning




Once your model is deployed, you want to be able to collect metrics on the model. You want to ascertain that the model is drifting from its objective and that the inference is useful for the business. This means you capture a lot of metrics and analyze them. Azure Machine Learning enables this tracking of metrics for the model is a very efficient manner. The central model registry becomes the one place where all this hosted.

As you collect more metrics and additional data becomes available for training, there may be a need to be able to retrain the model in the hope of improving its accuracy and/or performance. Also, since this is a continuous process of integrations and deployment (CI/CD), there’s a need for this process to be automated. This process of retraining and effective CI/CD of ML models is the biggest strength of Azure Machine Learning.
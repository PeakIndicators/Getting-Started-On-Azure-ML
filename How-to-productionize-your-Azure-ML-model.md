# How to productionize your Azure ML model

Creating a model is just one part of a Machine Learning pipeline, arguably the easier part. 
To take the model to production and obtain benefits of it is a completely different game. 
"Productionizing a model" needs to be able to package the models, deploy the models, track and monitor these models in various deployment targets, collects metrics, use these metrics to determine the efficacy of these models and then enable retraining of the models on the basis of these insights and/or new data. To add to it, all this needs a mechanism that can be automated with the right knobs and dials to allow data science teams to be able to keep a tab and not allow the pipeline to go rogue, which could result in considerable business losses, as these data science models are often linked directly to customer actions.

This problem is very similar to what application development teams face with respect to managing apps and releasing new versions of it at regular intervals with improved features and capabilities. The app dev teams address these with DevOps, which is the industry standard for managing operations for an app dev cycle. To be able to replicate the same to machine learning cycles is not the easiest task.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/devops1.PNG)

<font size="+6">Source: https://subscription.packtpub.com/book/big_data_and_business_intelligence/9781838550356/1/ch01lvl1sec13/ml-development-life-cycle</font>

This is where the Azure Machine Learning studio glows the most. It presents the most complete and intuitive model lifecycle management experience alongside integrating with Azure DevOps and GitHub.

The first task in the ML lifecycle management, after a data scientist has created and validated a model or an ML pipeline, is that it needs to be packaged, so that it can execute where it needs to be deployed. 

The next step is to be able to version control these models. Now, the code generated, like the Python notebooks or scripts can be easily versioned controlled in GitHub, and this is the recommended approach, but in addition to the notebooks and scripts you also need a way to version control the models, which are different entities than the python files. This is important as data scientists may create multiple versions of the model, and very easily lose track of these in search of better accuracy or performance. Azure Machine Learning provides a central model registry, which forms the foundation of the lifecycle management process. This repository enables version control of models, it stores model metrics, it allows for one-click deployment, and even tracks all deployments of the models so that you can restrict usage, in case the model becomes stale or its efficacy is no longer acceptable. Having this model registry is key as it also helps trigger other activities in the lifecycle when new changes appear, or metrics cross a threshold.

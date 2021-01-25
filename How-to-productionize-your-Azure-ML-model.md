# How to productionize your Azure ML model

Creating a model is just one part of an ML pipeline, arguably the easier part. To take this model to production and reap benefits of the data science model is a completely different ball game. One has to be able to package the models, deploy the models, track and monitor these models in various deployment targets, collects metrics, use these metrics to determine the efficacy of these models and then enable retraining of the models on the basis of these insights and/or new data. To add to it, all this needs a mechanism that can be automated with the right knobs and dials to allow data science teams to be able to keep a tab and not allow the pipeline to go rogue, which could result in considerable business losses, as these data science models are often linked directly to customer actions.

This problem is very similar to what application development teams face with respect to managing apps and releasing new versions of it at regular intervals with improved features and capabilities. The app dev teams address these with DevOps, which is the industry standard for managing operations for an app dev cycle. To be able to replicate the same to machine learning cycles is not the easiest task.
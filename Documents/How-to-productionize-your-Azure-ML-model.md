# How to deploy your model to a new environment

Creating a model it's just one part of a Machine Learning pipeline, arguably the easiest part. 
To take the model to production and obtain benefits of it, it's a completely different game. 
"Productionizing a model" needs to be able to package, deploy, track and monitor the model in various deployment targets. It needs to collect metrics, use those metrics to determine the value of the model and then enable retraining of it on the basis of these insights and/or new data. In addition to it, all this needs a mechanism that can be automated with the right knobs and dials to allow data science teams to be able to keep a tab and not allow the pipeline to go rogue, which could result in considerable business losses, as these data science models are often linked directly to customer actions.

This problem is very similar to what application development teams face with respect to managing apps and releasing new versions of it at regular intervals with improved features and capabilities. The app dev teams address these with DevOps, which is the industry standard for managing operations for an app dev cycle. To be able to replicate the same to machine learning cycles it's not an easy task.

For the development phase, Machine Learning life-cycle can be defined as:

<p align="center">
  <img src="../Images/devops1.PNG">
</p>

##### _Source: https://subscription.packtpub.com/book/big_data_and_business_intelligence/9781838550356/1/ch01lvl1sec13/ml-development-life-cycle_

Things are fairly simple (process wise) until we get to the final stage **Integrate and Deploy** and its continous integration with **Validating and Testing the Algorithm**. 

This is where Azure Machine Learning studio shines the most. It presents the most complete and intuitive model lifecycle management experience alongside integrating with Azure DevOps and also with GitHub.

Now the big question is what is the best way to run a machine learning model in production. There are 2 options: 
 * Using real-time inference
 * Using batch inference 

In a real-time inference the model is up and running continuously on a server, usually exposed as a WebService, generating real time predictions whenever it's invoked. In contrast, in batch inference the idea is to only run the model from time to time, generating all possible predictions in a batch, removing the need to have your model up all the time.

**The decision on which deployment solution to follow depends on how the use case results should be delivered.*

[Machine Learning Crash]Course(https://developers.google.com/machine-learning/crash-course/static-vs-dynamic-inference/video-lecture) provided by Google has some interesting information regarding advantages and disadvantages, we quote a couple below:

Here are the pros and cons of real time inference:

> Pro: Can make a prediction on any new item as it comes in — great for long tail.

> Con: Compute intensive, latency sensitive—may limit model complexity.

> Con: Monitoring needs are more intensive.

Here are the pros and cons of batch inference:

> Pro: Don’t need to worry much about cost of inference.

> Pro: Can likely use batch quota or some giant MapReduce.

> Pro: Can do post-verification of predictions before pushing.

> Con: Can only predict things we know about — bad for long tail.

> Con: Update latency is likely measured in hours or days.


If we search on the internet a lot of the Azure ML guidance focuses on real time inference (Azure MLOps is one example). This is good when the need is to deliver real time predictions, but not so good when it comes to control costs or return predictions with the lowest latency possible. After all, running a model on a server all the time can be quite expensive, while running it every now and then is definitely cheaper. Batched predictions can be cached and returned almost instantly, too.

In order to balance things out, in this tutorial we are going to focus on different ways of deploying the results of a data science use case based on different scenarios:
Click on each scenario to understand how it works:

* [Scenario 1](../Documents/Scenario1-Designer-RealTimeInf.md) - Model was build using studio designer and it needs to be deployed as a real-time inference in another environment.

* [Scenario 2](../Documents/Scenario2-Designer-BatchInf.md) - Model was build using studio designer and it needs to be deployed as a batch inference.

* [Scenario 3](../Documents/Scenario3-Notebook-RealTimeInf.md) - Model was build using studio notebooks and now it needs to be deployed as a real time inference.

* [Scenario 4](../Documents/Scenario4-Notebook-BatchInf.md) - Model was build using studio notebooks and now its results needs to be deployed as a batch inference (stored in a specific shedule in a data lake file or database table).

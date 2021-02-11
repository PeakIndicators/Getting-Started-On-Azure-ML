# Scenario 1 - Model was build using studio designer and it needs to be deployed as a real-time inference in another environment

In this scenario we are considering that the model training, scoring and evaluation is being done through studio designer and we just need to deploy it as a real time webservice in another environment (the idea is the developer is working in a development enviromnent with production data, once he gets the best model, that will be deployed to a production resource as a real-time webservice).

* Register the model (optional, see below).
* Prepare an inference configuration (unless using no-code deployment).
* Prepare an entry script (unless using no-code deployment).
* Choose a compute target.
* Deploy the model to the compute target.
* Test the resulting web service.

**Work in Progress** 

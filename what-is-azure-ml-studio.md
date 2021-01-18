# What is Azure ML Studio?

Azure Machine Learning Studio is the top-level resource for Azure Machine Learning, providing a centralized place to work with all the artifacts created by the users while working with Azure Machine Learning. 
Studio keeps a history of all training runs, including logs, metrics, output and a snapshot of the scripts. 
The user can then utilise this information to determine which training run produces the best model.

Once the user has a model he likes, it can be registered within the studio and can then can be used alongside with scoring scripts to deploy to Azure Container Instances, Azure Kubernetes Service or to a field-programmable gate array (FPGA) as a REST-based HTTP endpoint. The model can also be deployed to an Azure IoT Edge device as a module.

## Taxonomy
A taxonomy of studio is illustrated in the following diagram (provided by Microsoft):

<p align="center">
  <img src="https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/azure-machine-learning-taxonomy.png">
</p>


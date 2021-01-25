# Integrate with Azure Key Vault secrets

Authentication information such as user names, passwords and connection strings shouldn't be displayed in our code, they should be treated as secrets. For example, if you connect to an external database in order to query training data, you would need to pass your username and password to the remote run context. Coding such values into training scripts in cleartext is insecure as it would expose the credentials.

Instead, your Azure Machine Learning studio has an associated resource called a [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/general/overview). Use this Key Vault to pass secrets to remote runs securely through a set of APIs in the Azure Machine Learning Python SDK.

The standard flow for using secrets is:

1. Log in to Azure and connect to your Subscription.
2. In the Azure Key Vault resource, set the secret and its permissions.
3. Connect to Azure ML Studio and submit a remote run.
4. Within the remote run, get the secret from Key Vault and use it.

In order to access and manage secrets, in Azure ML an environment needs to be created.

## Packages needed
The following packages are needed in order to connect to Azure Key Vault:

```
azure-keyvault-secrets==4.1.0
azure-keyvault==1.1.0
azure.identity==1.3.1
azure-keyvault-keys==4.1.0
azure-common==1.1.25
```
These will be configured in the environment created in the next section.

## Creating an environment

In order to get the secrets information, a remote run needs to be created. This means an environment needs to be set up.

1. The first step is to get the workspace where the environment is going to be created:
```
from azureml.core import Workspace

ws = Workspace.from_config()
```

2. Create an environment:
```
# Create a Python Environment for the Experiment
envtest = Environment(name="your-env-name")
```

3. Configure the environment and add the necessary packages:
```
from azureml.core.conda_dependencies import CondaDependencies

envtest.docker.enabled = True
envtest.docker.base_dockerfile = 'FROM mcr.microsoft.com/azureml/base:latest\nRUN apt-get update && apt-get -y install freetds-dev freetds-bin vim gcc' + \
'\nRUN apt-get install -y curl\nRUN apt-get install -y apt-transport-https\nRUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -' + \
'\nRUN curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | tee /etc/apt/sources.list.d/msprod.list\nRUN apt-get update' + \
'\nENV ACCEPT_EULA=y DEBIAN_FRONTEND=noninteractive\nRUN apt-get install mssql-tools unixodbc-dev -y'
envtest.docker.base_image = None

# Create a set of package dependencies
env_packages = CondaDependencies.create(conda_packages=['pandas', 'pyodbc', 'requests', 'sqlalchemy', 'urllib3'],
                                         pip_packages = ['azureml-sdk', 'pymssql==2.1.1','azure-keyvault-secrets==4.1.0','azure.identity==1.3.1','azure-keyvault-keys==4.1.0','azure-common==1.1.25','azure-keyvault==1.1.0'])

# Add ,''the dependencies to the enviroment 
envtest.python.conda_dependencies = env_packages
```

4. Set the variable in the environment. This is a one-only task, it should always be performed once and as soon as the environment is ready this information should be removed from any script.
```
envtest.environment_variables = {"AZURE_CLIENT_ID": "<client_id>","AZURE_CLIENT_SECRET" : "<client_secret>","AZURE_TENANT_ID": <tenant_id>","KEY_VAULT_URL": "https://<subscription>.vault.azure.net/","AZURE_SECRET_1":"<secret1_name>","AZURE_SECRET_1_VERSION":"<secret1_version>","AZURE_SECRET_2":"<secret2_name>","AZURE_SECRET_VERSION_INSERT":"<secret2_version>"}
```
Most organizations have very restrict security policies and therefore the access to Azure Key Vault is very limited. In these cases what happens is a specific team will create the secrets in the Key Vault and give to the ML developers the information needed to invoke those secrets.
For the code above, the team who created the secrets also needs to:

* Create a [Service Principal](https://docs.microsoft.com/en-us/powershell/azure/create-azure-service-principal-azureps?view=azps-5.4.0) that will allow the connection between the Azure Key Vault and Azure Machine Learning Studio and provide the _<client_id>,<client_secret> and <tenant_id>_ to the ML Developers.
* Configure the Azure Key Vault secrets access to that Service Principal
* Provide informationo on the secrets name and version to the ML Developers

5. Register the environment in the workspace
```
envtest.register(workspace = ws)
```

6. A final test can be done to check if the environment was properly set.
```
from azureml.core import Environment

env = Environment.get(workspace=ws, name="you")
print(env)
```
This will allow the user the check the following information:
![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/key-vault1.PNG)

```
envs = Environment.list(workspace=ws)

for env in envs:
    if env.startswith("your-env-name"):
        print("Name",env)
        print("packages", envs[env].python.conda_dependencies.serialize_to_string())
```
This will allow the user the check the following information:
![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/key-vault2.PNG)


## Get secrets
Once the environment is created 


## Set secrets
Most organizations have very restrict security policies and therefore the access to Azure Key Vault is very limited. In these cases what happens is a specific team will create the secrets in the Key Vault and give to the ML developers the information needed to invoke those secrets. Meaning only the Get Secrets section is needed.

Anyway we will show an example on how to set secrets directly in Azure Machine Learning Studio

In the Azure Machine Learning, the Keyvault class contains methods for setting secrets. In your local Python session, first obtain a reference to your workspace Key Vault, and then use the set_secret() method to set a secret by name and value. The set_secret method updates the secret value if the name already exists.

```
from azureml.core import Workspace
from azureml.core import Keyvault
import os


ws = Workspace.from_config()
my_secret = os.environ.get("MY_SECRET")
keyvault = ws.get_default_keyvault()
keyvault.set_secret(name="mysecret", value = my_secret)
```

Do not put the secret value in your Python code as it is insecure to store it in file as cleartext. Instead, obtain the secret value from an environment variable, for example Azure DevOps build secret, or from interactive user input.

You can list secret names using the **list_secrets()** method and there is also a batch version, **set_secrets()** that allows you to set multiple secrets at a time.

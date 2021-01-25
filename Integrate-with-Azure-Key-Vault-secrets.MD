# Integrate with Azure Key Vault secrets

Authentication information such as user names, passwords and connection strings shouldn't be displayed in our code, they should be treated as secrets. For example, if you connect to an external database in order to query training data, you would need to pass your username and password to the remote run context. Coding such values into training scripts in cleartext is insecure as it would expose the credentials.

Instead, your Azure Machine Learning studio has an associated resource called a [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/general/overview). Use this Key Vault to pass secrets to remote runs securely through a set of APIs in the Azure Machine Learning Python SDK.

The standard flow for using secrets is:

1. Log in to Azure and connect to your Subscription.
2. In the Azure Key Vault resource, set the secret and its permissions.
3. Connect to Azure ML Studio and submit a remote run.
4. Within the remote run, get the secret from Key Vault and use it.

In order to access and manage secrets, in Azure ML an environment needs to be created.

## Installing packages
The following packages need to be installed:

```
pip install azure-keyvault-secrets==4.1.0
pip install azure-keyvault==1.1.0
pip install azure.identity==1.3.1
pip install azure-keyvault-keys==4.1.0
pip install azure-common==1.1.25
```

## Creating an environment


Most organizations have very restrict security policies and therefore the access to Azure Key Vault is very limited. In these cases what happens is a specific team will create the secrets in the Key Vault and give to the ML developers the information needed to invoke those secrets.

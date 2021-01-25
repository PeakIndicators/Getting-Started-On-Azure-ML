# Integrate with Azure Key Vault secrets

Authentication information such as user names, passwords and connection strings shouldn't be displayed in our code, they should be treated as secrets. For example, if you connect to an external database in order to query training data, you would need to pass your username and password to the remote run context. Coding such values into training scripts in cleartext is insecure as it would expose the credentials.

Instead, your Azure Machine Learning studio has an associated resource called a [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/general/overview). Use this Key Vault to pass secrets to remote runs securely through a set of APIs in the Azure Machine Learning Python SDK.

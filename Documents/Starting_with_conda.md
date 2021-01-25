# Getting started with conda

Conda is a powerful package manager and environment manager that you use with command line commands at the Anaconda Prompt for Windows, or in a terminal window for macOS or Linux.

## <b name = '#Before-you-start-2'></b>Before you start


Ensure that you have already installed Anaconda. click on the relevant link before if you still need to intall it. 
* [Windows](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Documents/Anaconda_Windows.md)
* [MacOS](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Documents/Anaconda_macos.md)
* [Linux](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Documents/Anaconda_linux.md)

## Starting conda

**Windows**

* from the start menu, search for and open "Anaconda Prompt". 

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/A10.PNG) Anaconda Prompt from the Windows Start menu

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/A2.PNG) Anaconda Promp when opened

On Windows, all commands below are typed into the Anaconda Prompt window.

**MacOS**

* Open Launchpad, then click the terminal icon.

On macOS, all commands below are typed into the terminal window.

**Linux**

* Open a terminal window.

On Linux, all commands below are typed into the terminal window.

## Managing conda

Verify that conda is installed and running on your system by typing:

`conda --version`

Conda displays the number of the version that you have installed. You do not need to navigate to the Anaconda directory. You should expect an output like the below:

`conda 4.7.12`

**Note**—If you get an error message, make sure you closed and re-opened the terminal window after installing, or do it now. Then verify that you are logged into the same user account that you used to install Anaconda or Miniconda.

2. Update conda to the current version. Type the following:

`conda update conda`

Conda compares versions and then displays what is available to install.

If a newer version of conda is available, type `y` to update:

`Proceed ([y]/n)? y`

**Tip**—We recommend that you always keep conda updated to the latest version.

## Managing Environments

Conda allows you to create separate environments containing files, packages, and their dependencies that will not interact with other environments. 

With conda, you can also export, list, remove, and update environments that have different versions of Python and/or packages installed in them. Switching or moving between environments is called activating the environment. You can also share an environment file.

When you begin using conda, you already have a default environment named base. You don't want to put programs into your base environment, though. Create separate environments to keep your programs isolated from each other.

### Creating an environment with commands

**Tip**—By default, environments are installed into the `envs` directory in your conda directory. See [Specifying a location for an environment](#Specifying-location-for-environment-1)

Use the terminal or an Anaconda Prompt for the following steps:

1. To create an environment: 

`conda create --name myenv`

**note**—Replace myenv with the environment name.

2. When conda asks you to proceed, type `y`:

`Procees ([y]/n)`

This creates the myenv environment in `/envs/`. No packages will be installed in this environment.

3. To create an environment with a specific version of Python:

`conda create -n myenv python = 3.6`

4. To create an environment with a specific package:

`conda create - n myenv scipy`

OR: 

`conda create -n myenv python`
` conda install -n myenv scipy`

5. To create an environment with a specific version of a package:

`conda create -n myenv scipy=0.15.0`

OR: 

`conda create -n myenv python`
`conda install -n myenv scipy=0.15.0`

6. To create an environment with a specific version of Python and multiple packages:

`conda create -n myenv python=3.6 scipy=0.15.0 astroid babel`

**Tip**—Install all the programs that you want in this environment at the same time. Installing 1 program at a time can lead to dependency conflicts.

To automatically install pip or another program every time a new environment is created, add the default programs to the [create_default_packages](https://docs.conda.io/projects/conda/en/latest/user-guide/configuration/use-condarc.html#config-add-default-pkgs) section of your `.condarc` configuration file. The default packages are installed every time you create a new environment. If you do not want the default packages installed in a particular environment, use the `--no-default-packages` flag:

`conda create --no-default-packages -n myenv python`

**Tip**—You can add much more to the `conda create` command. For details, run `conda create --help`.

### <a name='Specifying-location-for-environment-1'></a>Specifying a location for an environment

You can control where a conda environment lives by providing a path to a target directory when creating the environment. For example, the following command will create a new environment in a subdirectory of the current working directory called envs:

`conda create --prefix ./envs jupyterlab=0.35 matplotlib=3.1 numpy=1.16`

You then activate an environment created with a prefix using the same command used to activate environments created by name:

`conda activate ./envs`

Specifying a path to a subdirectory of your project directory when creating an environment has the following benefits:

* It makes it easy to tell if your project uses an isolated environment by including the environment as a subdirectory.

* It makes your project more self-contained as everything, including the required software, is contained in a single project directory.

An additional benefit of creating your project’s environment inside a subdirectory is that you can then use the same name for all your environments. If you keep all of your environments in your `envs` folder, you’ll have to give each environment a different name.

There are a few things to be aware of when placing conda environments outside of the default `envs` folder.

1. Conda can no longer find your environment with the `--name`flag. You’ll generally need to pass the `--prefix` flag along with the environment’s full path to find the environment.

2. Specifying an install path when creating your conda environments makes it so that your command prompt is now prefixed with the active environment’s absolute path rather than the environment’s name
&nbsp;
After activating an environment using its prefix, your prompt will look similar to the following:
`(/absolute/path/to/envs) $`
&nbsp;
This can result in long prefixes:
`(/Users/USER_NAME/research/data-science/PROJECT_NAME/envs) $`
&nbsp;
To remove this long prefix in your shell prompt, modify the env_prompt setting in your .condarc file:
`$ conda config --set env_prompt '({name})'`
&nbsp;
This will edit your `.condarc` file if you already have one or create a `.condarc` file if you do not.
&nbsp;
Now your command prompt will display the active environment’s generic name, which is the name of the environment's root folder:
`$ cd project-directory`
`$ conda activate ./env`
`(env) project-directory $`

### Updating an environment

You may need to update your environment for a variety of reasons. For example, it may be the case that:

* one of your core dependencies just released a new version (dependency version number update).

* you need an additional package for data analysis (add a new dependency).

* you have found a better package and no longer need the older package (add new dependency and remove old dependency).

If any of these occur, all you need to do is update the contents of your environment.yml file accordingly and then run the following command:

`$ conda env update --prefix ./env --file environment.yml  --prune`

**Note**— The `--prune` option causes conda to remove any dependencies that are no longer required for the environment. 

In this last section we will cover activating and deactiving your environment. We have tried to cover the main commands you will need to know to get started with conda but here is a lot more you can do including [cloning your environemnt](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#cloning-an-environment) and [exporting your environment](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#exporting-the-environment-yml-file). For more information on managing conda see [here](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#).

### Activating an environment

Activating environments is essential to making the software in the environments work well. Activation entails two primary functions: adding entries to PATH for the environment and running any activation scripts that the environment may contain. These activation scripts are how packages can set arbitrary environment variables that may be necessary for their operation. You can also [use the config API to set environment variables](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#set-env-vars).

To activate an environment: `conda activate myenv`

**Note**—Replace `myenv` with the environment name or directory path. 

### Deactivating an environment
To deactivate an environment, type: `conda deactivate`

Conda removes the path name for the currently active environment from your system command.






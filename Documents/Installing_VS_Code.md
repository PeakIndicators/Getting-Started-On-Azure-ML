# Getting Started with Python in Visual Studio Code

## Install Visual Studio (VS) Code and the Python Extension

1. If you have not already done so, install [VS Code](https://code.visualstudio.com/).

2. Next, install the [Python extension for VS Code](https://marketplace.visualstudio.com/items?itemName=ms-python.python) from the Visual Studio Marketplace. For additional details on installing extensions, see [Extension Marketplace](https://code.visualstudio.com/docs/editor/extension-gallery). The Python extension is named **Python** and it's published by Microsoft.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/VS1.PNG)

### Install a Python interpreter
Along with the Python extension, you need to install a Python interpreter. Which interpreter you use is dependent on your specific needs, as this documentation is primarily written for using Python to build Data Science solutions the document [Getting started with Conda](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Documents/Starting_with_conda.md) details how to install and create your virtual environment with conda. Conda was selected for the purpose of this document as it provides not just a Python interpreter, but many useful libraries and tools for data science.

## Verify the Python installation

To verify that you've installed Python successfully on your machine, run one of the following commands (depending on your operating system):

* Linux/macOS: open a Terminal Window and type the following command:

`python3 --version`

* Windows: open a command prompt and run the following command:

`py -3 --version`

If the installation was successful, the output window should show the version of Python that you installed.

**Note** You can use the `py -0` command in the VS Code integrated terminal to view the versions of python installed on your machine. The default interpreter is identified by an asterisk (*).

## Start VS Code in a project (workspace) folder

1. Open the conda command prompt.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/VS10.PNG) 


2. Create an empty folder called "hello".
&nbsp;
3. Navigate into it.
&nbsp;
4. Open VS Code (`code`) in that folder (`.`) by entering the following commands:

`mkdir hello`
`cd hello`
`code .`

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/VS2.PNG) 

By starting VS Code in a folder, that folder becomes your "workspace". VS Code stores settings that are specific to that workspace in `.vscode/settings.json,` which are separate from user settings that are stored globally.

Alternatively, you can run VS Code through the operating system UI, then use **File > Open Folder** to open the project folder.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/VS3.PNG) Open File through the operating system UI

### Select a Python interpreter

Python is an interpreted language and in order to run Python code and get Python IntelliSense, you must tell VS Code which interpreter to use. In our case this should be the Conda environment we have created earlier. As you get more comfortable using Python and conda you may have more than one virtual environment. Select the one you want to use for your particular project. 

From within VS Code, select a Python 3 interpreter by opening the **Command Palette (Ctrl+Shift+P)**, start typing the **Python: Select Interpreter** command to search, then select the command. 

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/VS4.PNG) 

Open the Command Palette and select Python: Select Interpreter

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/VS5.PNG) 

Select the Python Interpreter you want to use for your project. This should be the virtual environment your created with conda. 

You can also use the **Select Python Environment** option on the Status Bar if available (it may already show a selected interpreter, too):

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/VS6.PNG) 


The command presents a list of available interpreters that VS Code can find automatically, including virtual environments. If you don't see the desired interpreter, select *Enter interpreter path...* .

**Note:** When using an Anaconda distribution, the correct interpreter should have the suffix `('envname':conda)`, for example `Python 3.7.3 64-bit ('envname':conda)`.

**Note:** If you select an interpreter without a workspace folder open, VS Code sets `python.pythonPath` in your user settings instead, which sets the default interpreter for VS Code in general. The user setting makes sure you always have a default interpreter for Python projects. The workspace settings lets you override the user settings.

### Create a Python Hello World source code file
From the File Explorer toolbar, select the **New File** button on the `hello` folder:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/VS7.PNG)

Name the file `hello.py` and it automatically opens in the editor:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/VS8.PNG)

By using the `.py` file extension, you tell VS Code to interpret this file as a Python program, so that it evaluates the contents with the Python extension and the selected interpreter.

**Note:** The File Explorer toolbar also allows you to create folders within your workspace to better organize your code. You can use the **New folder** button to quickly create a folder.

Now that you have a code file in your Workspace, enter the following source code in `hello.py`:

`msg = "Hello world"`
`print (msg)`

When you start typing `print`, notice how [IntelliSense](https://code.visualstudio.com/docs/editor/intellisense) presents auto-completion options.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/VS9.PNG)

IntelliSense and auto-completions work for standard Python modules as well as other packages you've installed into the environment of the selected Python interpreter. It also provides completions for methods available on object types. For example, because the `msg` variable contains a string, IntelliSense provides string methods when you type `msg.`:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/VS11.PNG)

Feel free to experiment with IntelliSense some more, but then revert your changes so you have only the `msg` variable and the `print` call and save the file **(Ctrl+S)**.

### Run Hello World
It's simple to run `hello.py` with Python. Just click the **Run Python File in Terminal** play button in the top-right side of the editor.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/VS15.PNG)

The button opens a terminal panel in which your python interpreter is automatically activated, then runs `python 3 hello.py` (macOS/Linux) or `python hello.py` (Windows):

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/VS16.PNG)

There are three other ways you can run Python code within VS Code:

* Right-click anywhere in the editor window and **select Run Python File in Terminal** (which saves the file automatically):

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/VS17.PNG)

* Select one or more lines, then press Shift+Enter or right-click and select **Run Selection/Line in Python Terminal**. This command is convenient for testing just a part of a file.

* From the Command Palette (Ctrl+Shift+P), select the **Python: Start REPL** command to open a REPL terminal for the currently selected Python interpreter. In the REPL, you can then enter and run lines of code one at a time.


### Configure and run the debugger

Let's now try debugging our simple Hello World program.

First, set a breakpoint on line 2 of `hello.py` by placing the cursor on the print call and pressing F9. Alternatively, just click in the editor's left gutter, next to the line numbers. When you set a breakpoint, a red circle appears in the gutter.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/VS18.PNG)

Next, to initialize the debugger, press `F5`. Since this is your first time debugging this file, a configuration menu will open from the Command Palette allowing you to select the type of debug configuration you would like for the opened file.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/VS19.PNG)

**Note**: VS Code uses JSON files for all of its various configurations; `launch.json` is the standard name for a file containing debugging configurations.

These different configurations are fully explained in Debugging configurations; for now, just select **Python File**, which is the configuration that runs the current file shown in the editor using the currently selected Python interpreter.

The debugger will stop at the first line of the file breakpoint. The current line is indicated with a yellow arrow in the left margin. If you examine the **Local** variables window at this point, you will see now the defined msg variable appears in the **Local** pane.

!![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/VS20.PNG)

A debug toolbar appears along the top with the following commands from left to right: continue (`F5)`, step over (`F10`), step into (`F11`), step out (`Shift+F11`), restart (`Ctrl+Shift+F5`), and stop (`Shift+F5`).

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/VS21.PNG)

The Status Bar also changes color (orange in many themes) to indicate that you're in debug mode. The Python Debug Console also appears automatically in the lower right panel to show the commands being run, along with the program output.

To continue running the program, select the continue command on the debug toolbar (`F5`). The debugger runs the program to the end.

**Tip** Debugging information can also be seen by hovering over code, such as variables. In the case of msg, hovering over the variable will display the string `Hello world` in a box above the variable.

You can also work with variables in the **Debug Console** (If you don't see it, select **Debug Console** in the lower right area of VS Code or select it from the ... menu). Then try entering the following lines, one by one, at the > prompt at the bottom of the console:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/VS22.PNG)

Select the blue **Continue** button on the toolbar again (or press F5) to run the program to completion. "Hello World" appears in the **Python Debug Console** if you switch back to it and VS Code exits debugging mode once the program is complete.

If you restart the debugger, the debugger again stops on the first breakpoint.

To stop running a program before it completes, use the red square stop button on the debug toolbar (`Shift+F5`) or use the **Run > Stop debugging** menu command.

For full details, see [Debugging configurations](https://code.visualstudio.com/docs/python/debugging), which includes notes on how to use a specific Python interpreter for debugging.

**Tip: Use Logpoints instead of print statements**: Developers often litter source code with print statements to quickly inspect variables without necessarily stepping through each line of code in a debugger. In VS Code, you can instead use **Logpoints**. A Logpoint is like a breakpoint except that it logs a message to the console and doesn't stop the program. For more information, see [Logpoints](https://code.visualstudio.com/docs/editor/debugging#_logpoints) in the main VS Code debugging article.

### Install and use packages

Let's now run an example that's a little more interesting. In Python, packages are how you obtain a number of useful code libraries, typically from PyPI. For this example, you use the `matplotlib` and `numpy` packages to create a graphical plot as it's commonly done with data science. (Note that `matplotlib` cannot show graphs when running in the Windows Subsystem for Linux as it lacks the necessary UI support).

Return to the **Explorer** view (the top-most icon on the left side, which shows files), create a new file called `standardplot.py` and paste in the following source code:

`import matplotlib.pyplot as plt`
`import numpy as np`

`x = np.linspace(0, 20, 100)`  `# Create a list of evenly-spaced numbers over the range`
`plt.plot(x, np.sin(x)) `      `# Plot the sine of each x point`
`plt.show()`                   `# Display the plot`

**Tip:** If you enter the above code by hand, you may find that auto-completions change the names after the as keywords when you press `Enter` at the end of a line. To avoid this, type a space, then Enter.

Next, try running the file in the debugger using the "Python: Current file" configuration as described in the last section.

Unless you're using an Anaconda distribution or have previously installed the `matplotlib` package, you should see the message, `"ModuleNotFoundError: No module named 'matplotlib'"`. Such a message indicates that the required package isn't available in your system.

To install the `matplotlib` package (which also installs `numpy` as a dependency), stop the debugger and use the Command Palette to run `Terminal: Create New Integrated Terminal (Ctrl+Shift+P`). This command opens a command prompt for your selected interpreter.

A best practice among Python developers is to avoid installing packages into a global interpreter environment. You instead use a project-specific `virtual environment` that contains a copy of a global interpreter. Once you activate that environment, any packages you then install are isolated from other environments. Such isolation reduces many complications that can arise from conflicting package versions. As mentioned earlier in this document [Getting started with Conda](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Documents/Starting_with_conda.md) explains how to install and create your virtual environment with conda. If you haven't done this yet and would like to create a `virtual environment` with the required packages using `python` instead of Conda, enter the following commands as appropriate for your operating system:

1. Create and activate the virtual environment

**Note:** When you create a new virtual environment, you should be prompted by VS Code to set it as the default for your workspace folder. If selected, the environment will automatically be activated when you open a new terminal.

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/VS23.PNG)

**For Windows**

`py -3 -m venv .venv`
`.venv\scripts\activate`

If the activate command generates the message "Activate.ps1 is not digitally signed. You cannot run this script on the current system.", then you need to temporarily change the PowerShell execution policy to allow scripts to run (see [About Execution Policies](https://go.microsoft.com/fwlink/?LinkID=135170) in the PowerShell documentation):

`Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process`

**For macOS/Linux**

`python3 -m venv .venv`
`source .venv/bin/activate`

2. Select your new environment by using the **Python: Select Interpreter** command from the **Command Palette**.

3. Install the packages.

`# Don't use with Anaconda distributions because they include matplotlib already.`

`# macOS`
`python3 -m pip install matplotlib`

`# Windows (may require elevation)`
`python -m pip install matplotlib`

`# Linux (Debian)`
`apt-get install python3-tk`
`python3 -m pip install matplotlib`

4. Re-run the program (with or without the debugger) and after a few moments a plot window appears with the output:

![](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Images/VS24.PNG)

5. Once you are finished, type `deactivate` ( type`conda deactivate` if you are using conda as your interpreter) in the terminal window to deactivate the virtual environment.

### Futher Information

You can configure VS Code to use any Python environment you have installed, including other virtual and conda environments. You can also use a separate environment for debugging. For full details, see [Environments](https://code.visualstudio.com/docs/python/environments).

To learn more about the Python language, follow any of the [programming tutorials](https://wiki.python.org/moin/BeginnersGuide/Programmers) listed on python.org within the context of VS Code.

There is then much more to explore with Python in Visual Studio Code:

* [Editing code](https://code.visualstudio.com/docs/python/editing) - Learn about autocomplete, IntelliSense, formatting, and refactoring for Python.
* [Linting](https://code.visualstudio.com/docs/python/linting) - Enable, configure and apply a variety of Python linters.
* [Debugging](https://code.visualstudio.com/docs/python/debugging) - Learn to debug Python both locally and remotely.
* [Testing](https://code.visualstudio.com/docs/python/testing) - Configure test environments and discover, run, and debug tests.
* [Settings reference](https://code.visualstudio.com/docs/python/settings-reference) - Explore the full range of Python-related settings in VS Code.

The next tutorial [Data Science in Visual Studio Code](https://github.com/felicity-borg/Getting-Started-On-Azure-ML/blob/main/Documents/DS_Visual_Studio_Code.md) is a tutorial demonstrating how you can use Visual Studio Code and common data science libraries to explore a basic data science scenario on a Jupyter notebook. 

# How do virtual envrionments work?

## Copies structure and files.

The `venv` module recreates the file and folder structure of a standard Python installation on the machine/OS.

Python copies or symlinks into that folder structure the Python executable with which `venv` is called.

## Adapts the Prefix-Finding Process

Python interpreter in the virtual envrionment can understand where all relevant files are located.

Instead of looking for the `os` module to determine the location of the standard library, it first looks for a `pyvenv.cfg` file.

If the interpreter finds one and it contains a _home_ key, then it will use that key to set the value for 2 variables `sys.base.prefix` and `sys.prefix`.

Otherwise, it determines that it's not running in within a virtual envrionment, and both `sys.base.prefix` and `sys.prefix` will point to the same path.

## Links back to the standard library

`venv` copies the minimally neccesary files, hence virtual envrionments in Python are lightweight with quick operations.

Python executable in the virtual environment has access to the modules of the standard-library from the original installation.

This is done by pointing to the file path of the base Python executable in the _home_ setting from a `pyvenv.cfg` file.

```txt
home = C:\Users\Name\AppData\Local\Programs\Python\Python312
include-system-site-packages = false
...
```

Listing contents of home directory finds the base Python executable used to create the virtual envrionment.

Python is set up to find these modules by adding the relevant path to `sys.path`. It automatically imports (during initialisation) the _site module_ that sets the defaults for this argument.

## Modifies the PYTHONPATH

To ensure that the desired scripts use the Python interpreter within the virtual envrionment, `venv` modifies _PYTHONPATH_ env variable that can be accessed using `sys.path`.

Inspecting that env variable without an active virtual envrionment will output the default paths for the Python installation.

```txt
>>> import sys
>>> sys.path
['',
 'C:\\Users\\Name\\AppData\\Local\\Programs\\Python\\Python312\\python312.zip',
 'C:\\Users\\Name\\AppData\\Local\\Programs\\Python\\Python312\\DLLs',
 'C:\\Users\\Name\\AppData\\Local\\Programs\\Python\\Python312\\lib',
 'C:\\Users\\Name\\AppData\\Local\\Programs\\Python\\Python312',
 'C:\\Users\\Name\\AppData\\Roaming\\Python\\Python312\\site-packages',
 'C:\\Users\\Name\\AppData\\Local\\Programs\\Python\\Python312\\lib\\site-packages']
```

However, if a virtual envrionment is activated, the command will output the site-packages directory of the virtual envrionment.

```txt
>>> import sys
>>> sys.path
['',
 'C:\\Users\\Name\\AppData\\Local\\Programs\\Python\\Python312\\python312.zip',
 'C:\\Users\\Name\\AppData\\Local\\Programs\\Python\\Python312\\DLLs',
 'C:\\Users\\Name\\AppData\\Local\\Programs\\Python\\Python312\\lib',
 'C:\\Users\\Name\\AppData\\Local\\Programs\\Python\\Python312',
 'C:\\Users\\Name\\path\\to\\venv',
 'C:\\Users\\Name\\path\\to\\venv\\lib\\site-packages']
```

This means that Python will load any external packages installed within the virtual envrionment.

## Changes PATH Variable on Activation

Activation script used depends on the OS and the shell in use i.e., shipped with different activation functions within virtual environment's folder structure.

```txt
venv\
│
├── Include\
│
├── Lib\
│
├── Scripts\
-------------------------
│   ├── Activate.ps1
│   ├── activate
│   ├── activate.bat
-------------------------
│   ├── deactivate.bat
│   ├── pip.exe
│   ├── pip3.12.exe
│   ├── pip3.exe
│   ├── python.exe
│   └── pythonw.exe
│
└── pyvenv.cfg
```

Two very important steps/actions happen in the activation script:

- **Path:** Sets the _VIRTUAL_ENV_ variable to the root folder path of the virtual environment and prepends the relative location of its Python executable to the PATH.

- **Command prompt:** Changes the command prompt to the name that passed when creating the virtual environment. It takes that name and puts it into parentheses.

These two changes put the convenience of virtual environments into effect within your shell:

- **Path:** Because the path to all the executables in the virtual environment now lives at the front of the PATH, the shell will invoke internal versions of pip or Python when typing `pip` or `python`.

- **Command prompt:** Because the script changed the command prompt, it can be easily recognised whether the virtual environment is active or not.

Inspecting before and after activation of a virtual envrionment to understand the difference in the set of PATH variables.

```txt
(venv) PS> $Env:Path
C:\Users\Name\path\to\venv\Scripts;C:\Windows\system32;
C:\Windows;C:\Windows\System32\Wbem;
C:\Users\Name\AppData\Local\Programs\Python\Python312\Scripts\;
C:\Users\Name\AppData\Local\Programs\Python\Python312\;
c:\users\name\.local\bin;
c:\users\name\appdata\roaming\python\python312\scripts
```

When you _deactivate_ your virtual environment, shell reverses these changes and returns PATH and the command prompt back to how they were before.

## Runs from Anywhere with Absolute Paths

It's not required to activate a `venv` to work with it, but it's recommended to do so.

If only provided with the name of an executable to the shell, it will look at the location recorded in _PATH_ for an executable file carrying that name.

The activation script changes your PATH variable so that the binaries folder of your virtual environment is the first place your shell looks for executables. This change allows you to type only `pip` or `python` to run the program located inside the virtual environment.

Using an inactive virtual environment instead requires passing the absolute path of the Python executable inside the `venv`.

## Resources

- TL;DR for busy readers: [How virtual environments work](https://snarky.ca/how-virtual-environments-work/)

- Longer article: [Python Virtual Environments: A Primer](https://realpython.com/python-virtual-environments-a-primer)

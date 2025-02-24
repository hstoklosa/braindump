# VENV with Jupyter in VSCode

## Problem

When you create a virtual environment (venv) and install Jupyter in it, you can't see the kernel in VSCode or Jupyter Notebook.

## Solution

_"...an extra step needed - you need to explicitly install a Jupyter kernel that points to your new Python virtual environment. You can't simply activate Jupyter-lab or Notebook from the virtual environment._

### Steps

1.  Create a virtual environment

    ```bash
    python3 -m venv virtual_env_name
    ```

2.  Activate the virtual environment

    ```bash
    source virtual_env_name/bin/activate
    ```

3.  Install ipykernel using pip

    ```bash
    pip install ipykernel
    ```

4.  Install a new kernel

    ```bash
    ipython kernel install --user --name=virtual_env_name
    ```

5.  Restart VSCode (in my case)

6.  Select newly created kernel within the Jupyter Notebook extension just like you would select the global kernel.

## References

- [Jupyter notebooks in Visual Studio Code does not use the active virtual environment](https://stackoverflow.com/a/58134257)

- [Using jupyter notebooks with a virtual environment
  ](https://anbasile.github.io/posts/2017-06-25-jupyter-venv/)

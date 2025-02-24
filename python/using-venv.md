# Using Virtual Environment in Python

## Navigating virtual environments

tl;dr version of the official documentation when it comes to using `venv` to navigate virtual environment.

```bash
# Create a new virtual environment
python3 -m venv /path/to/new/virtual/environment

# Start the virtual environment
source <venv>/bin/activate

# Exit the virtual environment
deactivate
```

## Usage

```bash
usage: venv [-h] [--system-site-packages] [--symlinks | --copies] [--clear]
            [--upgrade] [--without-pip] [--prompt PROMPT] [--upgrade-deps]
            [--without-scm-ignore-files]
            ENV_DIR [ENV_DIR ...]

Creates virtual Python environments in one or more target directories.

positional arguments:
  ENV_DIR               A directory to create the environment in.

options:
  -h, --help            show this help message and exit
  --system-site-packages
                        Give the virtual environment access to the system
                        site-packages dir.
  --symlinks            Try to use symlinks rather than copies, when
                        symlinks are not the default for the platform.
  --copies              Try to use copies rather than symlinks, even when
                        symlinks are the default for the platform.
  --clear               Delete the contents of the environment directory
                        if it already exists, before environment creation.
  --upgrade             Upgrade the environment directory to use this
                        version of Python, assuming Python has been
                        upgraded in-place.
  --without-pip         Skips installing or upgrading pip in the virtual
                        environment (pip is bootstrapped by default)
  --prompt PROMPT       Provides an alternative prompt prefix for this
                        environment.
  --upgrade-deps        Upgrade core dependencies (pip) to the latest
                        version in PyPI
  --without-scm-ignore-files
                        Skips adding SCM ignore files to the environment
                        directory (Git is supported by default).

Once an environment has been created, you may wish to activate it, e.g. by
sourcing an activate script in its bin directory.
```

## References

- [venv — Creation of virtual environments](https://docs.python.org/3/library/venv.html)

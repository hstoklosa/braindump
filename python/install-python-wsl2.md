# Install Python on WSL2

## Install WSL2 & Ubuntu 22

```bash
# from cmd.exe as administrator
wsl --install

# check which version of WSL ie 1 or 2
# and what linux distribution(s) are installed
wsl -l -v


# list of available distributions
wsl --list --online

# install 22.04. I had to do this as had an older version running in WSL
wsl --install -d Ubuntu-22.04
```

Then install the terminal:

> Set the default terminal to Ubuntu 22.04.2 LTS.

```bash
sudo apt get update
sudo apt get upgrade
```

## Install Python, Pip, and Virtual Environment

```bash
# 3.8.10 (on Ubuntu 20) and 3.10.6 on Ubuntu 22
python3 -V

# 20.0.2 - this is old
sudo apt install python3-pip -y

# update pip to 23.0.1
pip install --upgrade pip
```

Then install the virtual environment:

```bash
sudo apt install python3-venv
```

### References

- [Install python on wsl2 and ubuntu 22](https://davemateer.com/2023/03/31/install-python-on-WSL2-and-Ubuntu-22)

# How to Install Multiple Versions of Python on Ubuntu and Create Virtual Environments Using Your Preferred Version of Python

## Why should you use `pyenv` and Virtual Python Environments?
As a programmer or as a hobbyist you may want to work on several python projects simultaneously. And most of the projects require different Python versions and some project may require a specific version of a package e.g. specific version of numpy or django. In such cases you'll need to install multiple versions of python and will have to install several versions of a specific package and that is when virtual environment is required to maintain several python ecosystems based on various projects in isolation. `pyenv` makes it easier to maintain various versions of python on ubuntu and unix based systems as those systems by default contains a python version which they uses for various system operations and we don't wanna mess up with that python version.

## How to install `pyenv` on your ubuntu?
To install `pyenv` on Debian or Ubuntu based Linux distributions, you'll have to install several libraries and packages necessary for building Python from scratch. Enter the following command into your terminal to install all the necessary packages.<br>

```
sudo apt install -y make build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev \
libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev python-openssl \
git
```

To install `pyenv` you can clone it directly from [github](https://github.com/pyenv/pyenv) repository.
```
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
```

After that you need to enter the following commands to add `pyenv` to your `$PATH`. To see the effect you'll have to open a new terminal.
```
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init --path)"' >> ~/.bashrc
```

**If you use `zsh`, use `.zshrc` instead of `.bashrc`.**

## Using `pyenv`
If you followed the previous steps successfully, you should be able to use `pyenv` from your terminal. Type the following command on your terminal to check whether `pyenv` successfully installed or not. It should print the pyenv version.

```
pyenv --version
```

It you get the `pyenv` version, congratulations!. Next step is to install Python of your desired version. First check which Python versions are available to you. For that use the following command.

```
pyenv install -l
```

This command will display the various CPython versions(displays just the versions) along with other Python distributions such as Miniconda and Anaconda. In this tutorial we'll install a CPython version. Let's say you want to install CPython version 3.9.7. For that execute the following command on you terminal.

```
pyenv install 3.9.7
```

It'll take some time to build and install the desired Python version. However after completion of installation, type the following command to see the available python versions on your system.

```
pyenv versions
```

You'll find all the Python versions currently installed on your system and the current global version is indicated by an `*` on the left. To change the default global version of Python on your system type the following command.

```
pyenv global [PYTHON_VERSION]
```

Or if you want to use a specific version of python for a specific folder i.e. project, navigate to that directory and execute the command below.

```
pyenv local [PYTHON_VERSION]
```

Or if you want to set a specific Python version for your current terminal session use.

```
pyenv shell [PYTHON_VERSION]
```
This will set the Python version only as long as your session is active. So after you close your terminal, everything will be back to default.

## Creating Virtual Environment and Installing Package on that Environment
Python installation includes some basic packages and modules. Your Python version should include `pip` module by default. So, set the specific Python version as global Python version. After that open a new terminal and you can close the previous session.

After that install `pipenv` using `pip` command. It will install some dependencies along with `pipenv`. Creating and maintaining virtual environment using `pipenv` is much easier.

```
pip install pipenv
```

You can check the installed packages on your current Python version using `pip list` command.

To create virtual environment navigate to your preferred directory and create a folder. Suppose you want to start a django project, type the following command to install django under a virtual environment.

```
pipenv install django
```

It'll create an environment at first and then install the latest django version for that environment. It should successfully install django on a virtual environment. You can activate the environment by navigating to that folder and then executing the following command.

```
pipenv shell
```

After activating the environment, you can run django command. e.g. you can try the following command - 

```
django-admin
```

For installation of more packages, run the following command keeping the environment activated.

```
pipenv install [PACKAGE_NAME]
```

Exit the environment by just typing `exit`.

## Deleting Virtual Environment

You can delete a specific virtual environment from `~/.local/share/virtualenvs/` folder. Or you can delete all the virtual environments using -

```
rm -rf ~/.local/share/virtualenvs
```

## Removing a Specific Version of Python

You can uninstall a specific python version using `pyenv` using - 

```
pyenv uninstall [PYTHON_VERSION]
```

**Before deleting the active Python version, set the Python version to system default.**

##  Updating packages
If you want a list of outdated packages, run this to see all the packages needing an upgrade.

```
pipenv update --outdated
```

You can choose to blindly update all packages.

```
pipenv update
```

Or you can update a specific package one at a time.

```
pipenv update pandas
```

## Installing from Requirements.txt file
If you have a legacy requirements.txt file, `pipenv` can be used for that.

```
pipenv install -r requirements.txt
```

If you want a generate a requirements.txt file, you can run the following command after activating the environment from you project directory.

```
pip freeze > requirements.txt
```

## Using Virtual Environment with VSCode
Open the directory using VS Code. After that open the workspace using `Ctrl + Shift + p` and type `settings.json`. Select `Preferences: Open Workspace Settings (JSON)` and hit `Enter` on your keyboard. It should open an empty JSON file. Now inside the file type the following command.

```
{
  "python.terminal.activateEnvironment": true
}
```
Then go to option `run` and select `run without debugging`. It should automatically activate the environment everytime you run from that directory.

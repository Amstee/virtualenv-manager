# virtualenv-manager : A simple python virtual environment manager (cross-platform)

## 1. Usage

    Installer parser [-h] [--conf CONF] [--path PATH] [--name NAME]
                        [--env ENV] [--req REQ]
                        command
    
    positional arguments:
    command      The command you want to execute. 
                 Default commands : init [create a configuration file] |
                                    install [create a basic virtual environment]
    
    optional arguments:
      -h, --help   show this help message and exit
      --conf CONF  Specify the configuration file (.json)
      --path PATH  Path where the virtual env will be created
      --name NAME  Your configuration name
      --env ENV    Your environment directory name
      --req REQ    Your requirements file

## 2. Configuration

    The configuration file let you define your own configuration
    you can see the syntax by creating a default configuration file with the init command
    -> python install.py init
    
    You must have the key, content "Configuration" in your installation file
    You can define rules that you can call at the execution of the program as a command
    For example : {
                    ...
                    "test": {
                        "env_bin": [test.py],
                        "env_pip": [install --upgrade pip],
                        "link": ["test2"],
                        "normal": ["mv venv v"],
                        "private": ["test"]
                    },
                    ...
                  }
    
    Explanations :
        The key "env_bin" define commands that will be executed with 
        the python bin located in your virtual environment. (for this rule : execute the test.py file)
        
        The key "env_pip" define commands that will be executed with
        the pip bin located in your virtual environment. (for this rule : pip install --upgrade pip)
        
        The key "normal" define commands that will be executed without a special context
        (for this rule : mv venv v)
        
        The key "link" define commands that you want to be called after the execution of the current one
        (for this rule, it will call the rule test2)
        
        The key "private" reference hardcoded commands, you can add your own commands in the class
        Installer who inheritates from AInstaller.
        
        By default, AInstaller defines two specific commands : create and requirements
           - create : create your virtual environment
           - requirements : install the requirements specified in a requirements file in your virtual environment

## 3. TODO
    1. Handle names of config
    2. Handle colors on windows
    3. Clean the code
    4. Compatibility for python 2.7

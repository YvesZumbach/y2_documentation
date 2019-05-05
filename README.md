# y2 Documentation

The documentation for the y2 cluster is hosted in this repository.
If you want to read the documentation, have a look at [https://yveszumbachcmu.github.io/y2_documentation/](https://yveszumbachcmu.github.io/y2_documentation/).

## Setup

- `pip3 install -r requirements.txt` to install the website's required packages

## Virtual Environments

It is highly recommended to work using virtual environments in Python.

- Install virtualenvwrapper: `pip install virtualenvwrapper`.
- Create a new virtual environment for the y2 documentation: `mkvirtualenv y2_doc`.
- Activate the y2 documentation virtual environment: `workon y2_doc`
- Deactivate the virtual environment: `deactivate`

## Package Management

Please only issue those commands inside a virtual environment.

- `pip3 install -r requirements.txt` to install all required dependencies
- `pip3 install <package_name>` to install a new package (you should probably add the newly install package to the project's list of dependencies)
- `pip3 freeze --local -r requirements.txt > requirements.txt` to update the list of requirements (without deleting any entry already present in the `requirements.txt` file)

## Generating the Documentation

Type `make html` at the root of the project to generate the documentation for the y2 cluster.

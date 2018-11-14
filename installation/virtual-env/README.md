# Overview
[That section](http://github.com/machine-learning-helpers/induction-python/tree/master/installation/virtual-env)
explains how to install and configure Python virtual environments.
It is part of [the Python induction for Machine Learning (ML) project](http://github.com/machine-learning-helpers/induction-python),
but may be referenced by many other projects.

An alternative way to install Python virtual environments, and software pieces
such as Jupyter Lab, is to use a
[Docker image for Python Jupyter Lab notebooks](http://github.com/machine-learning-helpers/docker-python-jupyter).

## See also
* [Pipenv: Python Development Workflow for Humans](http://pypi.org/project/pipenv)
* [Basic Usage of Pipenv](http://pipenv.readthedocs.io/en/latest/basics/)
* [Pipenv and Virtual Environments](http://docs.python-guide.org/dev/virtualenvs/)
* [Installing Python ``virtualenv`` on CentOS 7](https://blog.teststation.org/centos/python/2016/05/11/installing-python-virtualenv-centos-7)

# Installation

## ``pipenv``

### Linux

#### Debian / Ubuntu
```bash
$ apt-get install python3-pip python3-all
$ pip3 install --user -U pipenv
```

#### CentOS
```bash
$ yum -y install pipenv
```

#### Fedora
```bash
$ dnf -y install pipenv
```

### MacOS
```bash
$ brew install pipenv
```

### Install specific versions in a given project
* Go to a project directory and install the required libraries.
  It will create a ``Pipfile`` file, if not already exising.
```bash
$ mkdir ~/dev/geo && cd ~/dev/geo
$ git clone https://github.com/opentraveldata/quality-assurance.git opentraveldata-qa
$ cd opentraveldata-qa
$ ./mkLocalDir.sh 
$ pipenv --python /usr/bin/python3 install
```

### Launch Python scripts with ``pipenv``
* Check that the Python environment is ready
```bash
$ pipenv check
Checking PEP 508 requirements…
Passed!
Checking installed package safety…
All good!
```

* Just prefix the commands with ``pipenv run``:
```bash
$ pipenv run checkers/check-por-cmp-optd-unlc.py > results/optd-qa-por-optd-vs-unlc.json
```

## ``virtualenv``

### On CentOS
* If needed, enable the [EPEL](https://fedoraproject.org/wiki/EPEL) repository:
```bash
$ sudo yum -y install epel-release
```

* Install ``python34`` and ``python-pip`` packages
  (but not ``virtualenv``):
```bash
$ sudo yum -y install python34 python34-devel python34-pip
```

* If needed, uninstall the CentOS-packaged ``virtualenv``:
```bash
$ sudo yum remove python-virtualenv
```

* Update ``pip`` and install ``virtualenv`` with ``pip``:
```bash
$ sudo pip3 install -U pip
$ sudo pip3 install virtualenv
```

* Create and activate a new Python 3 virtual environment:
```bash
$ mkdir -p ~/dev && cd ~/dev
$ PYTHON_VERSION=$(python3 --version 2>&1 | cut -d' ' -f2,2 | cut -d'.' -f1,2)
$ virtualenv -p python3 venv${PYTHON_VERSION}
$ ln -s venv${PYTHON_VERSION} venv3
```

* Optionally, install [Java 8](http://openjdk.java.net/projects/jdk8u),
  needed for instance by [Spark](https://spark.apache.org):
```bash
$ sudo yum -y install java-1.8.0-openjdk-devel java-1.8.0-openjdk-javadoc
```

### Fedora
* Install ``python3`` and ``python3-pip`` packages
  (but not ``virtualenv``):
```bash
$ sudo dnf -y install python3 python3-devel python3-pip
```

* If needed, uninstall the Fedora-packaged ``virtualenv``:
```bash
$ sudo dnf remove python3-virtualenv
```

* Update ``pip`` and install ``virtualenv`` with ``pip``:
```bash
$ sudo pip install -U pip
$ sudo pip install virtualenv
```

* Create and activate a new Python 3 virtual environment:
```bash
$ mkdir -p ~/dev && cd ~/dev
$ PYTHON_VERSION=$(python3 --version 2>&1 | cut -d' ' -f2,2 | cut -d'.' -f1,2)
$ python3 -m venv venv${PYTHON_VERSION}
$ ln -s venv${PYTHON_VERSION} venv3
```

* Optionally, install [Java 8](http://openjdk.java.net/projects/jdk8u),
  needed for instance by [Spark](https://spark.apache.org):
```bash
$ sudo dnf -y install java-1.8.0-openjdk-devel java-1.8.0-openjdk-javadoc
```

### MacOS
* With your favorite MacOS package manager, for instance
  [Homebrew](https://brew.sh), install Python 3:
```bash
$ brew install python3
```

* Install the Python 3 virtual environment:
```bash
$ mkdir -p ~/dev && cd ~/dev
$ PYTHON_VERSION=$(python3 --version 2>&1 | cut -d' ' -f2,2 | cut -d'.' -f1,2)
$ python3 -m venv venv${PYTHON_VERSION}
$ ln -s venv${PYTHON_VERSION} venv3
```

* Add a Shell script function for graphical packages
  (eg, [Matplotlib](https://matplotlib.org)) in ``~/.bashrc``:
```bash
$ cat >> ~/.bashrc << _EOF

# Python - support for Matplotlib in virtual environment
# http://matplotlib.org/faq/osx_framework.html#osxframework-faq
function frameworkpython {
        PYVER=$(python --version | cut -d' ' -f2 | cut -d'.' -f1)
        PYTHON_EXEC=/usr/local/bin/python$PYVER
        if [[ ! -z "${VIRTUAL_ENV}" ]]
        then
                PYTHONHOME=${VIRTUAL_ENV} ${PYTHON_EXEC} "$@"
        else
                ${PYTHON_EXEC} "$@"
        fi
}

_EOF
```

* Any Matplotlib-based Python script can then be launched with:
```bash
$ frameworkpython myPyscript.py
```

### General - A few useful packages
An arbitrary selection of useful packages.

* Activate the Python virtual environment:
```bash
$ source ~/dev/venv3/bin/activate
(venv3.7) $ python --version
Python 3.7.0
```

* Upgrade ``pip`` if needed:
```bash
(venv3.7) $ pip install -U pip
```

#### Machine Learning (ML)
* [NumPy](http://www.numpy.org), [SciKit-Learn](http://scikit-learn.org/stable),
  [Pandas](http://pandas.pydata.org), [Jupyter Lab](https://jupyterlab.readthedocs.io/en/stable),
  [Dask](http://dask.org):
```bash
(venv3.7) $ pip install -U numpy scikit-learn pandas jupyterlab dask
```

* [Matplotlib](https://matplotlib.org), [Seaborn](https://seaborn.pydata.org):
```bash
(venv3.7) * pip install -U matplotlib seaborn
```

* [Featuretools](http://www.featuretools.com)(not available on CentOS 7):
```bash
(venv3.7) $ pip install -U featuretools
```

* [Altair for visualization](https://altair-viz.github.io):
```bash
(venv3.7) $ pip install -U altair vega_datasets gpdvega
```

* [PySpark](https://spark.apache.org/docs/2.3.0/api/python/pyspark.html):
```bash
(venv3.7) $ pip install -U pyspark
```

# Typical session

## ``pipenv``
* Prefix any Python command/script with ``pipenv run``:
```bash
$ pipenv run python --version
Python 3.7.0
```

## ``virtualenv``
* Activate the Python virtual environment:
```bash
$ source ~/dev/venv3/bin/activate
```

* Use Python:
```bash
(venv3.7) $ python --version
Python 3.7.0
```

* When done with the need for Python, deactivate the virtual environment:
```bash
(venv3.7) $ deactivate
```

# PySpark
* PySpark, run from the Python virtual environment, needs a standalone
  Java Virtual Machine (JVM) to run Spark. So, be sure to install Java 8,
  as explained in the above installation section.

* Launch a Spark Shell:
```bash
(venv3.7) $ spark-shell
[...]
Spark context Web UI available at http://localhost:4040
Spark context available as 'sc' (master = local[*], app id = local-12345).
Spark session available as 'spark'.
Welcome to
      ____              __
     / __/__  ___ _____/ /__
    _\ \/ _ \/ _ `/ __/  '_/
   /___/ .__/\_,_/_/ /_/\_\   version 2.3.2
      /_/
         
Using Scala version 2.11.8 (OpenJDK 64-Bit Server VM, Java 1.8.0_181)
Type in expressions to have them evaluated.
Type :help for more information.

scala> spark.version
res0: String = 2.3.2

scala> :quit
$ 
```


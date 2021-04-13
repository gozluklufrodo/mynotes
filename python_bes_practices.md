**Fork on github:** To copy someone elses project and make your changes to that project. You can also start with someone else's project by forking it, then add their licence. 

## Python implementations:

Cpython:  reference implementation, written in C. This is the standard python implementation

PyPy: Faster implementation compared to the cpython

Jython: Python implementation to work with java

IronPython: Python implementation to work with .net 

PythonNet: Python implementation to work with .net

## Pipenv and Virtual Environments

### **Pipenv**:

Dependency manager for python projects. 

Manages dependencies on a per-project basis. 

```
 pipenv install requests
```

--> this command will install requests library and create a Pipfile file where all the dependencies will be added.

```
pipenv run python main.py 
```

--> this way we run the main script. We add pipenv before, to ensure installed pipenv packages are available to the python script. İf we do not add pipenv before, libraries installed by pipenv for this project will not be accessible to the python script.

### **Virtualenv**

```
pip install virtualenv
virtualenv testing
```

--> installs virtualenv and creates a virtualenv named testing in the given directory.

```
to activate: source testing/bin/activate
```

### VirtualEnvWrapper

```
pip install virtualenvwrapper
export WORKON_HOME=~/ENVS
source ./local/bin/virtualenvwrapper.sh
```

first command installs virtualenvwrapper.

second command exports its main directory where all the created virtual environments will be installed.

third command activates the virtual environment wrapper

```
mkvirtualenv venv --> creates a virtual environment named venv in ENVS folder
workon venv --> activates the venv virtual environment
```

# Python BASICS

- Is a dynamically typed laguage. Object's suitability for a context is determined on runtime.

- Also strongly type language, there is no implicit conversion. Meaning you can not add string and int it will give **TYPE ERROR**

- <u>**<mark>DO NOT USE MUTABLE OBJECTS SUCH AS LISTS AS DEFAULT ARGUMENTS TO A METHOD</mark>**</u>

- Is an interpreted language. --> But compiled to bytecode before it is executed

- PEP8 --> python coding standards

- PEP20 --> zen of python. just type **import this** 

- ```
  import math
  help(math) --> returns any documentation for math module
  ```

- ```
  float("inf")
  float("nan")    --> converts these to floats
  float("-inf")
  ```

- - [x] Whenever you see nested if statement, fix it using elif.

##### Strings and Collections

**String: str**  --> immutable sequences of unicode codepoints. 

**Multiline Strings**: String below will be written as multiline. Each row is a line. 

```
"""
Mene deniz verin,
O tenha qalıb,
O meni axtarır,
Meni gözleyir
"""
```

**Raw strings:** r before the string.  

```
path = 'C:\Users\frodo\documents\bagginss' --> this will give errors
path = r'C:\Users\frodo\documents\bagginss' --> this will run clean
```

**Lists:** 

```
list_ = ["farid",
         "haziyev",
         "frodo"]  --> we can do this
```

# 

#### Modules, Scripts and Programs

**Module**: Any .py code is a module. Mainly modules are convenient to import with api.

**Script**: any simple python code, that is more compatible to run from terminal rather than using it in an api.

**Program**: Composed of many modules.

##### Modules:

- ```
  from word import (fetch_words, print_words) --> we can import several 
                              functions from the word module like this
  ```

- **CODE OF ZEN**: Sparse is better than Dense. You should put two blank lines between the functions.

- **Docstring**: (documentation of the module)
  
  - In the first line use it as an information about what the module do in general, and how to run it
  
  - ```
    """
    What this module does in general, what is its purpose?
    Usage: python3 module_frodo.py "frodo baggıns"
    """
    ```
  
  - In each function add docstring, explaining the purpose of the function, what it does, input arguments and what it will return
  
  - ```
    """
    This function will make the life a better place for us.
    Args:
        url: the url you want to connect
        age: your age
    Returns:
        A list of movies that u could watch
    """
    ```

  





## Classes in Python

**String representation of instances**: 

1.   **\_\_str\_\_**  --> result when we call **print(object)** .  

2. **\_\_repr\_\_** --> Printable representation of the class. 
   
   These two are mainly similar and have the purpose of showing the printable representation of the class
   
    

**_\_slots\_\_**  :    When the instances are created a lot like more than 1000 instances will be created and this class keeps some data that will not be changed, it is better to keep them  in tupple instead of dictionary. Using __slots__ wil do this for us and decrease the memory usage. **So use this whenever the instances are created a lot**.

```
class Date:
  __slots__ = ['year', 'month', 'day']
  def __init__(self, year, month, day):
      self.year = year
      self.month = month
      self.day = day
```

##### **Encapsulating names**:

1) Any name that starts with a single leading **underscore (_) should always be assumed to be internal implementation.** 

2) Any name starting with two leading **underscores (__) is called private implementation**. What private implementations give is that mainly they are also internal operations and should be approached carefully. Also, their difference from single underscore is that these implementations are not available in inheritance. Meaning, private methods and properties of the parent **class are not inherited by the child class.**

##### Class Method and Static Method

**Class Method**: These methods are used like alternative constructors.

**Static Method**: To attach to the class, the utility functions somehow related to the class.

**\_\_init\_\_** : is not a constructor  

# PYCHARM

1. **ctrl+alt+s** --> goes to settings. In settings you can add documentation types **such as plain, google or numpy**.

2. 
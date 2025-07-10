# 🐍 Learn Python

*Python is a interpreted, object-oriented, high-level programming language with dynamic semantics, known for its readability and ease of use.*

---

## What is Python?
Python is a high-level, general-purpose programming language known for its simplicity and readability. It's widely used in fields ranging from web development and data analysis, to scientific computing, automation, and HPC workflows.

### Python Basics
**Variables**

Variables in Python are dynamic, meaning you don't have to declare their data type.
```python
name = "Chloe"
age = 30
pi = 3.14159
```

**Data Types**

Despite not needing to declare the data type of a variable, Python still associates every value with a data type. These data types determine how Python treats and processes data.

|**Type**|**Description**        |**Example**        |
|:------:|:---------------------:|:-----------------:|
| `int`  |Integer numbers        | `42`              |
|`float` |Decimal numbers        | `3.14`            |
|`str`   |String of characters   | `"hello"`         |
|`bool`  |Boolean logic          | `True`            |
| `list` |Ordered, changeable    | `[1. 2, 3,]`      |
|`tuple` |Ordered, unchangeable  | `(1, 2)`          |
| `dict` |Key-value pairs        |`{"name": "Chloe"}`|
| `set`  |Unordered unique values| `{1, 2, cat, dog}`|

**Functions**

Functions let you reuse blocks of code and structure logic clearly.
```python
def greet(name):
    return f"Hello, {name}!"
```

#### Working with Libraries
Python libraries are a collection of pre-written, reusbale code modules that extend Python's functionality and allow programmers to perform various tasks without having to write code from scratch.
- **The Python Standard Library** is a collection of modules and packages that are included with the Python installation.
- **The Python Package Index (PyPI)** is an additional active collection of hundreds of thousands of components, from individual programs and modules to packages and entire application development frameworks. PyPI acts as a central hub where developers can share and find Python packages and libraries. PyPI integrates with the `pip` package manager, making it simple to install packages directly from the index.

Use `import` to bring in built-in or external libraries to your code base:
```python
import math
print(math.sqrt(16))
```

Some common libraries include:
- `numpy` - numerical computing
- `scipy` - scientific tools
- `matplotlib` - plotting
- `pandas` - dataframes

## Resources
- [Offical Docs](https://docs.python.org/3/): Python's offical documentation site.
- [Python for Beginners](https://www.python.org/about/gettingstarted/): A helpful resource for installing and learning Python.
- [Python for Non-Programmers](https://wiki.python.org/moin/BeginnersGuide/NonProgrammers): A list of resources for those new to programming and Python.
- [Beginners Guide to Python](https://wiki.python.org/moin/BeginnersGuide/Programmers): A list of resources for those with some programming experience.
- [Google's Python Class](https://developers.google.com/edu/python): A free Python tutorial with videos and code exercises.
- [Learn Python](https://www.learnpython.org/): An interactive in-the-browser tutorial for learning Python.
- [PyPI](https://pypi.org/): A repository of software for the Python programming language.
- [The Python Standard Library](https://docs.python.org/3/library/index.html): Deep dive into Python's standard library.

---
tags: language
---


a high-level, general-purpose programming language

### What makes python so popular?

- **READABILITY**: because it is a high-level language, the syntax is supposed to be easily readable and understandable.
	- this makes interpreting python really easy
	- many languages are compiled, meaning the source code you create needs to be translated into machine code, *the language of your computer's processor* before it can run.

- **COMMUNITY**: python has a large, active community of python developers that help contribute a vast ecosystem of [[libraries]], [[framework]](s), and other resources from developers
	- open directory and "pip install" your library
	- python comes with some *built-in* modules (os, random)
	- you can import functions or classes from modules

 - **VERSATILITY**: python development ranges from web applications, data analysis, and even automation. This means there are a lot of industries you can specialize in.


---
### importing libraries and modules
you need to install the library to your local environment, then import modules (and functions)
```python
from math import sqrt
from datetime import datetime
# notice how "sqrt" is a function from the math module
```
---
### python logic
- #variable a named object which stores data or any information
- #operators: symbols with special meaning that perform computation
- #functions: collection of code (code snippet) that performs a specific task

```python
name = float(input("What is your age?: "))
print(name + 20)

# "float" function allows for concantenation:
# 40

pet = "cat"
print(f"John has a {pet}")

# swaps out variable:
# "John has a cat"
```
---

---
title: Python
---
Python is a general-purpose [object-oriented](/object_oriented_programming.md?fileId=24803) interpreted duck-typed programming language. It is known for being easy to use at the expense of being slower than statically compiled languages. Since it is interpreted, it is also often used as a scripting language.

Python was created by Dutch computer scientist Guido Van Rossum and was released in 1991. He named it after the British comedy group "Monty Python".

The Python read-eval-print-loop (REPL) can be started by running `python` with no arguments.

## Concepts

### File Organization

Each independent Python file (with the filename extension `.py`) is known as a *module.* Modules can reference other modules in order to split application into discrete files for organization.  
Modules can be contained in *packages.* Packages are folders containing modules with a special Python file designating that folder as a package - `init.py`.

### Objects

Objects in Python have three pieces of data associated with them by default:

- an identifier (ID), which is immutable,
- a type,
- and a value.

An object is created when a class's *initializer* method is run. This a Python magic method called `__init__`.

All objects are mutable by default.

### Data Types

#### Numeric Types

All numeric data types are immutable.

##### `int`

`int`s have no fixed size, so as long as the number to be represented can fit into memory, Python will allocate however many bytes required to fit that number (as long as enough memory exists). Underscores can be placed in any place in a number to make it more readable (eg. `1_000`).

##### `bool`

`bool`s are a subclass of `int`, where `True` is like `1` and `False` is like `0`. Every object can be cast to a `bool` and will evaluate to either `True` or `False`.

##### `float`

`float`s are implemented according to the IEEE 754 double-precision binary floating point standard. Single-precision is not available in Python. `float` numbers suffer from the same approximation issues that floating point numbers implemented in any language will have - this type is not recommended for usage where the degree of precision required has no room for error (such as financial applications).

##### `complex`

`complex`s can represent numbers with a real part and an imaginary part (known as `j`).

##### `fractions.Fraction`

`fractions.Fraction`s represents the ratio between two numbers without a loss of precision. Addition, multiplication, and exponentiation operations can be performed on them. They are always stored as the simplest ratio possible - common factors are automatically removed.

##### `decimal.Decimal`

`decimal.Decimal`s store decimal numbers at an arbitrary level of precision at the expense  of computation performance. In order to avoid capturing the approximation issues that comes with `float` numbers, they must be initialized using a `str` instead (ex. `'0.3'`).

#### Immutable Sequences

##### `str`

`str`s are sequences of Unicode code points. There is no representation of a single character in Python - instead a `str` of length one is used.

##### `bytes`

`bytes` are sequences of data that are typically encoded. A `bytes` literal can be represented by placing a `b` in front of a string literal. Bytes in the ASCII range are represented using their corresponding ASCII character. A byte that cannot be mapped to an ASCII character is represented using the `\x` prefix followed by two hexadecimal numbers.

### Execution Model

In code, programmers can assign *names* to objects. An operation that assigns an object to a name is called a *name-binding operation.* An example of a name-binding operation would be the following assignment:

```
message = "Hello World!"
```

The name `message` would be assigned the value `"Hello World!"`. 

Each name is held in a *namespace*, which maps names to objects. Creating new namespaces allows a programmer to assign names to objects that may already exist in other namespaces without interference. Namespaces are directly accessible in *scopes.* There are four different scopes in a Python program:

1. the local scope,
2. the enclosing scope,
3. the global scope,
4. and the built-in scope.

Python will search for an object assigned to a name in each of above scopes' namespaces in the above order. Enclosing and local scopes are created by indenting a line when creating a function or object.

### Virtual Environments

A virtual environment is an isolated Python environment used to isolate Python version dependencies from one another. Python ships with a virtual environment creator called `venv`. To create a virtual environment, one can run:

```
python -m venv venv # creates a venv folder called venv
```

### Magic Methods

A magic method is a special method used by the Python interpreter to modify its behavior. Magic methods are preceded and succeeded by double underscores.

## Evolution

Changes to the Python language, interpreter, or standard library are proposed through "Python Enhancement Proposals", which can be approved and incorporated into future versions.

## References

*Learn Python Programming*, Third Edition. Fabrizio Romano, Heinrich Kruger

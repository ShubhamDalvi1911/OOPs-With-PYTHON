# OOPs With Python

A hands-on collection of Python Object-Oriented Programming (OOP) notes, examples, and practice problems. This repository follows a gradual learning path from classes and objects to encapsulation, inheritance, polymorphism, abstraction, and class relationships.

The material is written as Jupyter notebooks so that each concept can be studied, changed, and executed interactively.

## Contents

| Notebook | Focus |
| --- | --- |
| [OOPs.ipynb](OOPs.ipynb) | Classes, constructors, an ATM example, and operator overloading with fractions |
| [OOPs_Part2.ipynb](OOPs_Part2.ipynb) | Attributes, methods, reference variables, mutability, encapsulation, and static variables |
| [OOPs_Part3.ipynb](OOPs_Part3.ipynb) | Aggregation, inheritance, method overriding, `super()`, polymorphism, and abstraction |
| [OOPs_Assignment1.ipynb](OOPs_Assignment1.ipynb) | Point and line classes with coordinate geometry operations |

## Learning Path

1. Start with `OOPs.ipynb` to learn how classes are declared, how constructors initialize objects, and how instance methods use `self`.
2. Continue with `OOPs_Part2.ipynb` to understand object references, mutable objects, private attributes, getter/setter methods, and class-level data.
3. Work through `OOPs_Part3.ipynb` for relationships between classes, inheritance hierarchies, method resolution order, polymorphism, and abstract classes.
4. Use `OOPs_Assignment1.ipynb` as practice by implementing and testing a small geometry model.

## Topics Covered

### Classes, Objects, and Constructors

The notebooks introduce classes as blueprints and objects as their instances. The `__init__` method is used to initialize instance attributes when an object is created.

```python
class Person:
	def __init__(self, name, country):
		self.name = name
		self.country = country

	def greet(self):
		greeting = "Namaste" if self.country == "india" else "Hello"
		print(greeting, self.name)


person = Person("Shubham", "india")
person.greet()
```

The first notebook also uses an `Atm` class to demonstrate a stateful, menu-driven object with a PIN, balance, and operations for creating a PIN, changing a PIN, checking a balance, and withdrawing money. The ATM example requires interactive input.

### Instance Attributes and Reference Variables

`OOPs_Part2.ipynb` demonstrates that variables hold references to objects. Assigning a second variable to an existing object does not copy it:

```python
first = Person("Shubham", "male")
second = first

second.name = "Sakshi"
print(first.name)  # Sakshi
```

Both variables refer to the same object, so a change through either reference is visible through the other. The notebook also passes objects to functions and demonstrates that a function can mutate an object in place.

### Encapsulation

The ATM examples use a double underscore attribute, `__balance`, to restrict direct access to internal state. Public methods such as `get_balance`, `set_balance`, `check_balance`, and `withdraw` provide controlled access.

```python
class Account:
	def __init__(self, balance=0):
		self.__balance = balance

	def get_balance(self):
		return self.__balance

	def set_balance(self, amount):
		if isinstance(amount, int):
			self.__balance = amount
```

This is Python name mangling rather than absolute privacy. It is a convention and mechanism for protecting implementation details from accidental direct access.

### Static or Class-Level Variables

The second notebook compares instance attributes with class-level attributes. The `Atm` class uses a shared counter to assign customer IDs and a `@staticmethod` to read that counter without requiring an instance.

```python
class CustomerId:
	counter = 1

	def __init__(self):
		self.customer_id = CustomerId.counter
		CustomerId.counter += 1

	@staticmethod
	def current_count():
		return CustomerId.counter
```

Class-level values are shared by instances, while instance attributes belong to one object.

### Aggregation: Has-A Relationship

`OOPs_Part3.ipynb` models a `Customer` that has an `Address`. The customer receives an `Address` object and delegates address-specific work to it. This keeps each class focused on its own responsibility.

```python
address = Address("Pune", 411018, "Maharashtra")
customer = Customer("Shubham", "Male", address)
customer.print_address()
```

### Inheritance

The inheritance examples build specialized classes from general ones:

- `Student` inherits from `User`.
- `SmartPhone` inherits from `Phone`.
- `SmartPhone` can inherit from both `Phone` and `Product`.
- Multilevel, hierarchical, multiple, and hybrid inheritance are introduced.

Inherited constructors, non-private attributes, and non-private methods are demonstrated. The notebooks also show that a child class cannot directly access a parent class's private attributes.

### Method Overriding and `super()`

A child class can replace a parent method with its own implementation. The `SmartPhone.buy` example overrides `Phone.buy`. The `super()` function is then used to call the parent implementation or constructor:

```python
class SmartPhone(Phone):
	def __init__(self, price, brand, camera, operating_system):
		super().__init__(price, brand, camera)
		self.operating_system = operating_system

	def buy(self):
		print("Buying a smartphone")
		super().buy()
```

The multiple-inheritance examples also introduce Method Resolution Order (MRO), which determines which implementation Python finds first.

### Polymorphism

The notebooks cover three forms of polymorphic behavior:

- **Method overriding:** a child class supplies a specialized implementation.
- **Method overloading:** Python does not support traditional signature-based overloading; the example uses a default argument instead.
- **Operator overloading:** the same operator can behave differently for strings, numbers, lists, and user-defined classes.

The `Fraction` class in `OOPs.ipynb` implements `__str__`, `__add__`, `__sub__`, `__mul__`, and `__truediv__`, allowing fraction objects to be displayed and combined with familiar operators.

### Abstraction

`OOPs_Part3.ipynb` uses the `abc` module to define a required interface:

```python
from abc import ABC, abstractmethod


class BankApp(ABC):
	def database(self):
		print("connected to database")

	@abstractmethod
	def security(self):
		pass


class MobileApp(BankApp):
	def security(self):
		print("mobile security")
```

`BankApp` defines the contract, while `MobileApp` provides the concrete security behavior. A subclass must implement the abstract method before it can be instantiated.

### Coordinate Geometry Assignment

`OOPs_Assignment1.ipynb` applies OOP to two-dimensional geometry:

- `Point(x, y)` creates and displays coordinates.
- `Point.euclidean_distance(other)` finds the distance between two points.
- `Point.distance_from_origin()` finds the distance from `(0, 0)`.
- `Line(A, B, C)` represents the equation `$Ax + By + C = 0$`.
- `Line.point_on_line(point)` checks whether a point satisfies the line equation.
- `Line.shortest_distance(point)` calculates the perpendicular distance from a point to a line.

The assignment is a useful checkpoint because it combines constructors, instance methods, object collaboration, and mathematical formulas in one small model.

## Running the Notebooks

### Requirements

- Python 3
- Jupyter Notebook or JupyterLab
- A Python kernel available to Jupyter

The examples use Python's standard library and do not require third-party packages.

### Local Setup

From the repository directory:

```bash
python -m pip install notebook
jupyter notebook
```

Open a notebook, select a Python kernel, and run the cells from top to bottom. The ATM cells prompt for input, so execute them interactively. Some cells intentionally explore invalid access or incorrect behavior, such as accessing a missing attribute or a private member; those cells are included as learning demonstrations.

### Google Colab

Each notebook contains an **Open in Colab** badge. The notebooks can also be opened directly from the GitHub repository:

- [Open `OOPs.ipynb` in Colab](https://colab.research.google.com/github/ShubhamDalvi1911/OOPs-With-PYTHON/blob/main/OOPs.ipynb)
- [Open `OOPs_Part2.ipynb` in Colab](https://colab.research.google.com/github/ShubhamDalvi1911/OOPs-With-PYTHON/blob/main/OOPs_Part2.ipynb)
- [Open `OOPs_Part3.ipynb` in Colab](https://colab.research.google.com/github/ShubhamDalvi1911/OOPs-With-PYTHON/blob/main/OOPs_Part3.ipynb)
- [Open `OOPs_Assignment1.ipynb` in Colab](https://colab.research.google.com/github/ShubhamDalvi1911/OOPs-With-PYTHON/blob/main/OOPs_Assignment1.ipynb)

## Repository Structure

```text
OOPs-With-PYTHON/
├── OOPs.ipynb
├── OOPs_Part2.ipynb
├── OOPs_Part3.ipynb
├── OOPs_Assignment1.ipynb
└── README.md
```

## Learning Goals

After completing the notebooks, you should be able to:

- Define classes and instantiate objects.
- Initialize and manage object state with constructors and instance methods.
- Explain object references, mutation, and shared class-level state.
- Encapsulate data with controlled access methods.
- Model has-a relationships through object composition.
- Reuse and specialize behavior with inheritance.
- Override methods and use `super()` correctly.
- Explain Python's approach to method and operator overloading.
- Define abstract interfaces with `ABC` and `abstractmethod`.
- Design a small object-oriented solution to a practical problem.

## Author

Shubham Nanasaheb Dalvi

MSc( Computer Science)



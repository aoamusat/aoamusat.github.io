---
layout: post
title: Crafting Code That Stands the Test of Time - The SOLID Principles
categories: [Programming, Software Engineering]
tags: [Python, OOP, Software Engineering]
---

## What is SOLID?

In the realm of object-oriented programming, a set of five guiding principles reigns supreme: SOLID. These principles pave the way toward building code that not only functions flawlessly but also gracefully adapts to change and stands the test of time.

These principles define methodologies that promote the creation of software with a focus on maintainability and scalability as the project expands. Embracing these methodologies can further help in steering clear of code smells, facilitating code refactoring, and aligning with Agile or Adaptive software development approaches.

SOLID stands for:
- S - Single-responsibility principle
- O - Open-close principle
- L - Liskov substitution principle
- I - Interface segregation principle
- D - Dependency inversion principle

In this blog post, we'll explore each of the SOLID principles and demonstrate how they can be implemented in Python.

## 1. Single Responsibility 

The Single Responsibility Principle states that a class should have only one reason to change. In other words, a class should have only one responsibility or job. See the code sample below:

```python
class Report:
    def __init__(self, data: dict):
        self.data = data

    def generate_report(self):
        # Generate the report logic here

    def save_to_file(self, filename: str):
        # Save the report to a file logic here
```

In this example, the Report class has a single responsibility: generating and saving reports. If the logic for generating reports changes, it won't affect the saving logic.

## 2. Open/Closed Principle (OCP)

The Open/Closed Principle states that a class should be open for extension but closed for modification. This means that you should be able to add new functionality without altering existing code. See the code sample below:

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14 * self.radius * self.radius
```

Here, the Shape class is closed for modification, but new shapes (e.g., Rectangle and Circle) can be added without modifying Shape.

## 3. Liskov Substitution Principle (LSP)

The Liskov Substitution Principle states that objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program. See the code sample below:

```python
class Bird:
    def fly(self):
        pass

class Sparrow(Bird):
    def fly(self):
        print("Sparrow can fly")

class Penguin(Bird):
    def fly(self):
        raise NotImplementedError("Penguin can't fly")
```
In this example, both Sparrow and Penguin are subclasses of Bird, and they can be used interchangeably without breaking the code.

## 4. Interface Segregation Principle (ISP)
   
The Interface Segregation Principle states that a class should not be forced to implement interfaces it does not use. In other words, a class should only be required to implement methods that are relevant to its behavior. See the code sample below:

```python
from abc import ABC, abstractmethod

class Worker(ABC):
    @abstractmethod
    def work(self):
        pass

    @abstractmethod
    def eat(self):
        pass

class Engineer(Worker):
    def work(self):
        print("Engineering work")

    def eat(self):
        print("Eating lunch")

class Waiter(Worker):
    def work(self):
        print("Serving customers")

    def eat(self):
        print("Eating snacks")
```
Here, Worker interface is divided into smaller interfaces (work and eat), and classes implement only the methods that are relevant to their role.

## 5. Dependency Inversion Principle (DIP)

Dependency inversion principle states:
Entities must depend on abstractions, not on concretions. It states that the high-level module must not depend on the low-level module, but they should depend on abstractions. Additionally, abstractions should not depend on details; details should depend on abstractions.

```python
from abc import ABC, abstractmethod

class Switchable(ABC):
    @abstractmethod
    def turn_on(self):
        pass

    @abstractmethod
    def turn_off(self):
        pass

class LightBulb(Switchable):
    def turn_on(self):
        print("LightBulb is ON")

    def turn_off(self):
        print("LightBulb is OFF")

class Fan(Switchable):
    def turn_on(self):
        print("Fan is ON")

    def turn_off(self):
        print("Fan is OFF")

class ElectricPowerSwitch:
    def __init__(self, device: Switchable):
        self.device = device
        self._is_on = False

    def press(self):
        if self._is_on:
            self.device.turn_off()
            self._is_on = False
        else:
            self.device.turn_on()
            self._is_on = True
```
Here, ElectricPowerSwitch depends on the abstraction (Switchable), and the high-level module (ElectricPowerSwitch) is not directly dependent on low-level modules (LightBulb and Fan).

## Conclusion
By adhering to the SOLID principles, developers can create more maintainable, scalable, and flexible software. These principles promote clean code, reduce code smells, and make it easier to adapt to changing requirements. Understanding and applying SOLID principles in Python or any other programming language can lead to more robust and maintainable software architecture.

In this tutorial, you've gained knowledge on:

- Grasping the significance and objectives of each SOLID principle.
- Recognizing class designs that contravene certain SOLID principles in Python.
- Leveraging the SOLID principles for refining Python code and enhancing its Object-Oriented Design (OOD).

Armed with this understanding, you now possess a robust groundwork of widely accepted best practices to employ when crafting your class structures and their associations in Python. By adhering to these principles, you can craft code that is not only more maintainable, extensible, and scalable but also conducive to effective testing.


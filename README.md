# OOP_materials
## 1. Understand the Object-Oriented approach
- **class:** A blueprint for creating objects, defining properties and methods.
- **object:** An instance of a class, representing a specific entity.
- **properties:** Attributes of a class/object that hold data.
- **method:** A function in a class that defines actions for objects. 
- **encapsulation:** Bundling data and methods in a class while restricting access.
- **inheritance:** A mechanism for a subclass to inherit properties/methods from a superclass.
- **superclass:** The parent class from which properties/methods are inherited.
- **subclass:** A class that inherits from a superclass, potentially adding or overriding features.

```python
class Vehicle:  # superclass
    def __init__(self, brand, model):  # Constructor
        self.brand = brand  # Property
        self.model = model  # Property

    def display_info(self):  # Method
        return f"{self.brand} {self.model}"

class Car(Vehicle):  # Subclass
    def honk(self):
        return "Beep beep!"

my_car = Car("Toyota", "Corolla")  # Object
print(my_car.display_info())  # Output: Toyota Corolla
print(my_car.honk())  # Output: Beep beep!
```

## 2. Employ class and object properties
- **Instance Variables**
  - Definition: Variables that are specific to an instance (object) of a class.
  - Scope: Each object has its own copy of instance variables.

- **Class Variables**
  - Definition: Variables that are shared among all instances of a class.
  - Scope: There is only one copy of class variables, regardless of how many instances exist.

- **`__dict__ `Property**
  - Definition: `__dict__` is an attribute of Python objects that stores the object's attributes in a dictionary format.

```python
class Example:
    class_variable = "I am a class variable"  # Class variable

    def __init__(self, value):
        self.instance_variable = value  # Instance variable

obj = Example("I am an instance variable")
print(obj.__dict__)  # Output: {'instance_variable': 'I am an instance variable'}
print(Example.class_variable)  # Output: I am a class variable
print(obj.instance_variable) #  Output: I am an instance variable

obj2 =  Example("I am another instance variable")
print(obj2.__dict__)  # Output: {'instance_variable': 'I am another instance variable
print(Example.class_variable)  # Output: I am a class variable
print(obj.instance_variable) #  Output: I am  another instance variable

print(Example.__dict__)   # Output: {'class_variable': 'I am a class variable'}
```

## 3. Equip a class with methods
#### - Construct (`__init__`) and initialize objects
It is a special method for initializing new objects with specific attributes, and it is called automatically when creating a new object.

#### - self Parameter
The `self` keyword is used to represent the class instance in method definitions. It allows you to access instance variables and methods from within the class.

```python
class Dog:
    def __init__(self, name, age): # Construct
        self.name = name  # Instance variable
        self.age = age    # Instance variable

    def bark(self):
        return f"{self.name} says Woof!"

    def get_age(self):
        return self.age

# Creating an instance of Dog
my_dog = Dog("Buddy", 5)

# Accessing attributes and methods using self
print(my_dog.bark())        # Output: Buddy says Woof!
print(my_dog.age)     # Output: 5
```

## 4. Discover the class structure
- **hasattr()  method**
    - Purpose: The hasattr(object, name) function checks if the specified object has an attribute with the given name.
    - Parameters:
        - object: The object or class you want to check.
        - name: A string representing the name of the attribute.
    - Return Value
        - Returns True if the attribute exists, and False otherwise.
#### - `__name__` attribute
This attribute returns the name of the class or function.
#### - ` __module__` attribute
This attribute returns the name of the module in which the class or function was defined.
#### - `__bases__` attribute
This attribute returns a tuple containing the base(super) classes of a class or typically be **_(<class 'object'>,)_** if it doesn't inherit from any other class.
#### - `__str__` method
Method that returns a string representation of an object

```python
class Car:
    wheels = 4  # Class variable

    def __init__(self, make, model):
        self.make = make  # Instance variable
        self.model = model  # Instance variable

    def drive(self):
        return f"{self.make} {self.model} is driving."
    
    def __str__(self):
        return f"{self.make} {self.model}"

# Creating an instance of Car
my_car = Car("Toyota", "Corolla")

print(my_car)  # Output: Toyota Corolla using  __str__()

# Checking attributes on the instance
print(hasattr(my_car, 'make'))      # Output: True
print(hasattr(my_car, 'wheels'))    # Output: False (instance does not have this attribute)
print(hasattr(my_car, 'drive'))     # Output: True

# Checking attributes on the class
print(hasattr(Car, 'wheels'))         # Output: True
print(hasattr(Car, 'drive'))          # Output: True
print(hasattr(Car, 'color'))          # Output: False (no such attribute)

print(Car.__name__)      # Output: 'Car'
print(Car.__module__)    # Output: '__main__' (or the name of the module)
print(Car.__bases__)     # Output: (<class 'object'>,)
```

## 5. Build a class hierarchy using inheritance

#### - Single Inheritance
A class inherits from only one parent class.
#### - Multiple Inheritance
A class can inherit from more than one parent class.
#### - isinstance() method
Determine whether an object is an instance of a specified class or a subclass.
  - Parameters:
    - object: The object to check.
    - classinfo: A class, type, or a tuple of classes and types.
  - Return Value
    - Returns True if the object is an instance of the specified class or any of its subclasses, otherwise, it returns False.

#### - Method Overriding 
Occurs when a subclass defines a method with the same name, signature, and parameters as a method in its superclass.

#### - operators: not is, is
Determine if two objects are identical (i.e., they are the same instance).
```python
class Animal:
    def speak(self):
        return "Animal speaks"

class Dog(Animal):  # Single inheritance
    def speak(self):  # Overriding
        return "Dog barks"

class Cat(Animal):  # Single inheritance
    def speak(self):  # Overriding
        return "Cat meows"

def animal_sound(animal):  # Polymorphism
    print(animal.speak())
#The function takes an instance of Animal (or its subclasses) and calls its speak() method. The same function can operate on different types of objects.


# Creating an instance
dog = Dog()
cat = Cat()
animal_sound(dog)  # Output: Dog barks
animal_sound(cat)  # Output: Cat meows
another_dog = dog
print(isinstance(dog, Animal))  # Output: True


# Using `is` and `is not` directly
if dog is cat:
    print("dog and cat are the same instance.")
else:
    print("dog and cat are different instances.") # This will execute

if dog is another_dog:
    print("dog and another_dog are the same instance.")  # This will execute
else:
    print("dog and another_dog are different instances.")
```

## 6. Method Resolution Order (MRO):  
Determine the order in which classes are searched for methods and attributes

```python 
class a :
    def  __init__(self):
        self.x = 10
    def  __str__(self):
        return str(self.x)
    def disply(self):
        print("a")
    def call(self):
        self.disply() 

class b(a):
    def __init__(self):
      self.x = 20
    def  __str__(self):
        return str(self.x)
    def disply(self):
        print("b")
    def do(self):
        self.call() 

class c (a):
    def __init__(self):
      self.x = 30
    def  __str__(self):
        return str(self.x)
    def disply(self):
        print("c")
    def do(self):
        self.call()

a().call()# A 
b().call() # B 
c().call() # C
b().do() # B
c().do() # C 
```





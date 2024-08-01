
Calling child from parent class

In most object-oriented programming languages, a parent class cannot directly call a method defined in a child class because it does not have knowledge of the child class's methods. However, you can achieve this through several techniques:

Method Overriding:
Define a method in the parent class and override it in the child class. When the parent class calls this method, the child class's implementation is invoked if the object is an instance of the child class.

Abstract Methods (or Interfaces):
Define an abstract method in the parent class, which must be implemented by any child class. This ensures the parent class can call the method, knowing that the child class will provide the implementation.

Callbacks or Hooks:
Define a callback mechanism in the parent class that the child class can set. This allows the parent class to call methods indirectly defined in the child class.

Method Overriding
```
class Parent:
    def call_child_method(self):
        self.method_to_override()

    def method_to_override(self):
        print("Parent's method")

class Child(Parent):
    def method_to_override(self):
        print("Child's method")

parent = Parent()
parent.call_child_method()  # Outputs: Parent's method

child = Child()
child.call_child_method()  # Outputs: Child's method
```

Abstract method
```
from abc import ABC, abstractmethod

class Parent(ABC):
    def call_child_method(self):
        self.method_to_implement()

    @abstractmethod
    def method_to_implement(self):
        pass

class Child(Parent):
    def method_to_implement(self):
        print("Child's implementation")

child = Child()
child.call_child_method()  # Outputs: Child's implementation
```

Callback or hooks
```
class Parent:
    def __init__(self):
        self.callback = None

    def set_callback(self, callback):
        self.callback = callback

    def call_child_method(self):
        if self.callback:
            self.callback()

class Child(Parent):
    def __init__(self):
        super().__init__()
        self.set_callback(self.child_method)

    def child_method(self):
        print("Child's method")

child = Child()
child.call_child_method()  # Outputs: Child's method
```

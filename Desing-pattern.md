## event-driven architecture
## Publisher-Subscriber (Pub-Sub) architecture

The Publisher-Subscriber (Pub-Sub) architecture is a messaging pattern where publishers send messages without needing to know who the subscribers are. Likewise, subscribers receive messages without needing to know who the publishers are. This pattern is widely used in systems where decoupling components is essential, allowing them to communicate without directly depending on each other.

Key Concepts:
Publisher: The component that generates and sends messages (or events).
Subscriber: The component that listens for and processes messages from publishers.
Message (Event): The data or information sent from the publisher to the subscriber.
Topic (or Channel): A named entity to which messages are sent. Subscribers listen to specific topics to receive messages.

```
// Define types for Topic and Callback
type Topic = string;
type Callback = (data: any) => void;

class PubSub {
    private topics: Map<Topic, Callback[]>;

    constructor() {
        this.topics = new Map();
    }

    // Subscribe to a topic with a callback function
    subscribe(topic: Topic, callback: Callback) {
        if (!this.topics.has(topic)) {
            this.topics.set(topic, []);
        }
        this.topics.get(topic)!.push(callback);
    }

    // Publish an event to a specific topic
    publish(topic: Topic, data: any) {
        const subscribers = this.topics.get(topic);
        if (subscribers) {
            subscribers.forEach(callback => callback(data));
        }
    }

    // Unsubscribe from a topic
    unsubscribe(topic: Topic, callback: Callback) {
        const subscribers = this.topics.get(topic);
        if (subscribers) {
            this.topics.set(topic, subscribers.filter(sub => sub !== callback));
        }
    }
}

// Usage example

const pubSub = new PubSub();

// Define a subscriber callback function
const subscriberCallback = (data: any) => {
    console.log(`Subscriber received data: ${data}`);
};

// Subscribe to a topic
pubSub.subscribe('news', subscriberCallback);

// Publish an event to the 'news' topic
pubSub.publish('news', 'Breaking News: Pub-Sub Pattern Explained!');

// Output: Subscriber received data: Breaking News: Pub-Sub Pattern Explained!

// Unsubscribe from the 'news' topic
pubSub.unsubscribe('news', subscriberCallback);
```



## Dependency injection
tight vs loose coupling
https://jefedcreator.medium.com/loose-coupling-via-dependency-injection-in-node-js-express-server-applications-a-performance-2c09a2d409ce






## Calling child from parent class

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

**1.**      **OOP principles**

Modifiers
- public: accesible from all classes
- private: only withing decalred class
- default: only in same package
- protected: only in same package and subclasses
- Final: Atributes and methods cannot be overwritten/modified
- Static: Can be accessed without creating an instance of a class
- Abstract: Methods from abstract classes(Do not contain implementation), cannot create instances from it
- Transient: Attributes and methods are skiped when serializing
- Syncronized: methods can be accesed one thread at a time
- Volatile: The value of an attribute is not cached in thread, reads from main memory



**Encapsulation** (achieved with modifiers private,public etc)
The meaning of **Encapsulation**, is to make sure that "sensitive" data is hidden from users.
For: Better control of attributes and methods, Flexible, Security

- Getters/Setters

**Inheritance**
subclass (child)
superclass (parent)

**Polymorphism** (method overloading(methods with same name but diff number of parameters))
It occurs when we have many classes that are related to each other by inheritance.
To increase reusability of code


**Abstraction** (achieved with abstract classes, interfaces)
Ιs the process of hiding certain details and showing only essential information to the user.  
Abstraction can be achieved with either **abstract classes** or **interfaces** 

We **cannot** create instances of Abstract classes

**Interface**
Iterface classses do not contain Implementation, act as "blueprint".
Upon implementing it you must override all it's methods
Interface attribures are public, static, final
Interface methods are public, abstract

A class can implement multiple interfactes
A class **cannot** inherit multiple classes

**Enum**
Special class that contains group of constants 

```
// Java
enum Level {
  LOW,
  MEDIUM,
  HIGH
}
Level Var = Level.MEDIUM;
```

----------------------------------------------------------
Abstract VS Interface:
- **Interfaces** define methods without implementation (in Java 8+, they can have default methods with implementations). They allow a class to inherit multiple behaviors from different interfaces.
- **Abstract classes** can have both abstract methods (without implementation) and concrete methods (with implementation), and they are meant to be extended by subclasses. A class can inherit only one abstract class.




**3.**      **Collections Framework**

**ArrayList**
- Resizable array

**LinkedList**
The `LinkedList` stores its items in "containers." The list has a link to the first container and each container has a link to the next container in the list. To add an element to the list, the element is placed into a new container and that container is linked to one of the other containers in the list.

**Hash Map** (Dictionary)
- Key/Value pairs
- Not duplicate Keys

**HashSet**
- Set with no duplicate values

**Iterator**
object that can be used to loop through collections

- **List**:
    - Ordered collection that allows duplicates.
    - Implementations: `ArrayList`, `LinkedList`, `Vector`.
    - Key points:
        - `ArrayList`: Backed by a dynamic array, allows random access.
        - `LinkedList`: Doubly linked list, better for frequent insertions/removals.
- **Set**:
    
    - Unordered collection that doesn’t allow duplicates.
    - Implementations: `HashSet`, `LinkedHashSet`, `TreeSet`.
    - Key points:
        - `HashSet`: Backed by a hash table, offers fast access (O(1)).
        - `TreeSet`: Maintains sorted order, backed by a red-black tree (O(log n) operations).
- **Queue**:
    
    - Used for holding elements before processing, usually in FIFO order.
    - Implementations: `PriorityQueue`, `LinkedList`.
    - Key points:
        - `PriorityQueue`: Orders elements based on natural ordering or a custom comparator.
- **Map**:
    
    - Key-value pairs, where each key is unique.
    - Implementations: `HashMap`, `LinkedHashMap`, `TreeMap`, `Hashtable`.
    - Key points:
        - `HashMap`: Unordered map, allows null keys and values, O(1) access time.
        - `TreeMap`: Sorted map, O(log n) access time.

**Comparable VS Comperator**
- Comparable: need implementation
- Comparator

Fail-fast behavior
iterator throuws error when collection is modified when it s iterating over

Thread-safe collections?
- Using synchronized collectinos
- Concurrent collections



**5.**      **Java I/O and file handling**

**6.**      **Mutlithreading**

Create a thread by extending Thread Class

**Thread Lifecycle**: A thread in Java goes through different states:

- **New**: The thread is created but not yet started.
- **Runnable**: The thread is ready to run and may be running.
- **Blocked**: The thread is waiting for a resource or a lock.
- **Waiting/Timed Waiting**: The thread is waiting indefinitely or for a specific time for another thread to perform a task.
- **Terminated**: The thread has finished executing.

SYNC
synchronized void: Ensures that only one thread at a time can access it
Threads can have different priorities (1-10)
with wait(),notify(),notifyAll() you can achieve inter-thread communication

start() starts new thread witch runs the run() method

calling run() will run on the same thread

wait(): causes the current thread to wait until another thread calls notify() on the same object
notify() wakes a single thread thath is waiting on that object's monitor

**Common problems**

- Race Condition
when 2+ threads try yo access and modify shared data
Use *synchronized* keyword

- Deadlock
When 2+ threads are waiting for each other for resources
use trylock()

- Starvation
When a thread is perpetually denied access to resources because of lower priority

- Livelock
Similar to deadlock, threads keep changin their states but without making progress



**7.**      **Lambda expressions, Streams, Optional Classes**


```
(parameters) -> expression  
or  
(parameters) -> { block of code }

```
A lambda expression provides a concise way to implement the method of a functional interface, allowing you to pass behavior as an argument without needing to create a separate class.



**Streams API**
process collections of data 

you can:
filter() : filter elements base on a filter
map(); transform each element
sorted(): sort the elements

**Optional Class** 
The `Optional` class helps to avoid `NullPointerException` by returning an empty `Optional` instead of `null` when a value is not present. This makes it easier to handle cases where a value might be missing

Used to avoid NullPointerExceptions
Instead of returning null -> returns Optional 


**8.**      **Functional Interfaces**

A **functional interface** in Java is an interface that contains exactly one abstract method, but it can have multiple default or static methods. Functional interfaces are commonly used in lambda expressions and method references.

**9. Databases**
ACID properties
**A**tomicity
**C**onsistency
**I**solation
**D**urability
to ensure all actions leave the database in a valid state in case of unepected errors


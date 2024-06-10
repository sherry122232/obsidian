## (important) Usage of Collections in coding: 
### List, Set, Map 
- minimum ArrayList, LinkedList, HashMap (hashCode equals)
## Sorting
a List/Array in a given attribute. Like sorting a list of students by age or name.
```
List<Student> students = new ArrayList<>();
// Add students to the list...

// Sort by age using lambda expression
Collections.sort(students, (s1, s2) -> Integer.compare(s1.getAge(), s2.getAge()));

// Sort by age in descending order
Collections.sort(students, Comparator.comparing(Student::getAge).reversed());

// Sort in descending lexicographic order
Collections.sort(strings, (s1, s2) -> s2.compareTo(s1));

```

```
Student[] students = new Student[size];
// Initialize students array...

// Sort by age using lambda expression
Arrays.sort(students, (s1, s2) -> Integer.compare(s1.getAge(), s2.getAge())); // asc

// Sort by age in descending order using lambda expression
Arrays.sort(students, (s1, s2) -> Integer.compare(s2.getAge(), s1.getAge()));


```

如果比较年龄和age
#array
```
// Sort by age first, then by name using lambda expression
Arrays.sort(students, Comparator.comparing(Student::getAge)
                                .thenComparing(Student::getName));


方法二：
// Sort by age first, then by name using lambda expression
Arrays.sort(students, (s1, s2) -> {
    // Compare by age
    int ageComparison = Integer.compare(s1.getAge(), s2.getAge());
    
    // If ages are equal, compare by name
    if (ageComparison == 0) {
        return s1.getName().compareTo(s2.getName());
    } else {
        return ageComparison; // Return the result of age comparison
    }
});

```
#list
```
List<Student> students = new ArrayList<>();
// Add students to the list...

// Sort by age first, then by name using lambda expression
Collections.sort(students, (s1, s2) -> {
    // Compare by age
    int ageComparison = Integer.compare(s1.getAge(), s2.getAge());
    
    // If ages are equal, compare by name
    if (ageComparison == 0) {
        return s1.getName().compareTo(s2.getName());
    } else {
        return ageComparison; // Return the result of age comparison
    }
});

```

## (important) Basic java coding
#### String, 
**String**: In Java, `String` is a built-in class that represents a sequence of characters. Strings in Java are immutable, meaning once a ==`String` object is created, its value cannot be changed==. You can perform various operations on strings such as concatenation, substring, length calculation, etc.
#### sub-class,
**Sub-class**: In object-oriented programming, a subclass (or derived class) is a class that inherits properties and behaviors from another class called a superclass (or base class). A subclass can extend the functionality of its superclass by adding new methods or overriding existing ones.
```
class Animal {
    void eat() {
        System.out.println("Animal is eating");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Dog is barking");
    }
}

```
#### constructor,
**Constructor**: A constructor in Java is a special type of method that is automatically called when an instance (object) of a class is created. It is used to initialize the object's state. Constructors have the same name as the class and can be overloaded (i.e., a class can have multiple constructors with different parameters).
```
class Person {
    String name;

    // Constructor
    public Person(String n) {
        name = n;
    }
}

```
#### getter/setter, etc.
**Getter/Setter**: Getters and setters are methods used to read and modify the values of private fields (variables) in a class, respectively. They are often used to implement encapsulation, which is a fundamental principle of object-oriented programming aimed at hiding the internal state of objects and restricting direct access to it.
```
class Car {
    private String model;

    // Getter
    public String getModel() {
        return model;
    }

    // Setter
    public void setModel(String m) {
        model = m;
    }
}

```
## (important) Basic algorithm:
Leetcode easy level

## Advanced concepts in java: 
### Object-Oriented Programming (OOP):

Object-Oriented Programming is a programming paradigm based on the concept of "objects", which can contain data in the form of fields (attributes) and code in the form of procedures (methods). OOP principles include:

- **Encapsulation**: Bundling data and methods that operate on the data into a single unit (class), and restricting access to some of the object's components.
- **Inheritance**: Mechanism by which a class can inherit properties and behavior from another class, facilitating code reuse and establishing hierarchical relationships between classes.
- **Polymorphism**: Ability to present the same interface for different data types, allowing objects to be treated as instances of their parent class or their subclass.

### SOLID Principles:

SOLID is an acronym that represents a set of five design principles for writing maintainable and scalable object-oriented software:

- **Single Responsibility Principle (SRP)**: A class should have only one reason to change, meaning it should have only one responsibility.
- **Open/Closed Principle (OCP)**: Software entities (classes, modules, functions, etc.) should be open for extension but closed for modification.
- **Liskov Substitution Principle (LSP)**: Subtypes must be substitutable for their base types without altering the correctness of the program.
- **Interface Segregation Principle (ISP)**: Clients should not be forced to depend on interfaces they do not use.
- **Dependency Inversion Principle (DIP)**: High-level modules should not depend on low-level modules; both should depend on abstractions. Abstractions should not depend on details; details should depend on abstractions.

### Model-View-Controller (MVC):

MVC is a software architectural pattern commonly used for developing user interfaces. It separates an application into three interconnected components:

- **Model**: Represents the data and business logic of the application.
- **View**: Represents the presentation layer, responsible for displaying the data to the user.
- **Controller**: Acts as an intermediary between the Model and View, handling user input and updating the Model accordingly.

### Design Patterns:

Design patterns are reusable solutions to commonly occurring problems in software design. They provide a template for solving particular design problems in a way that is proven to be effective and efficient. Some common design patterns include:

- **Creational Patterns**: Singleton, Factory, Builder, Prototype.
- **Structural Patterns**: Adapter, Decorator, Proxy, Composite.
- **Behavioral Patterns**: Observer, Strategy, Command, Iterator.

### Multithreading:

Multithreading allows concurrent execution of multiple threads within a single process. In Java, multithreading is achieved using the `Thread` class or the `Runnable` interface. Java provides built-in support for multithreading through features like synchronization, locks, and concurrent data structures. Multithreading is crucial for improving the performance and responsiveness of Java applications, especially in scenarios where tasks can be executed concurrently.

These advanced concepts form the foundation of robust, scalable, and maintainable Java applications. Understanding and applying these concepts appropriately can significantly enhance the quality and efficiency of software development in Java. If you have any further questions or need clarification on any specific topic, feel free to ask!
## Basic network
Hypertext Transfer Protocol (HTTP) and Transmission Control Protocol (TCP)

### HTTP (Hypertext Transfer Protocol):

HTTP is an application layer protocol commonly used for transferring hypertext documents on the World Wide Web. It is the foundation of data communication for the World Wide Web, and it defines how messages are formatted and transmitted between web servers and web browsers.

- **Client-Server Model**: HTTP follows a client-server model where a client (typically a web browser) sends requests to a server (typically a web server), and the server responds with the requested resources (such as HTML pages, images, etc.).
- **Stateless Protocol**: HTTP is stateless, meaning each request from a client to a server is independent and does not retain information about previous requests.
- **Request-Response Protocol**: HTTP operates on a request-response model, where clients send HTTP requests to servers and servers respond with HTTP responses, typically containing the requested resources along with status codes and headers.
### HTTP/1.0:

HTTP/1.0 was the first version of the Hypertext Transfer Protocol. It was standardized in 1996 by the Internet Engineering Task Force (IETF). Some key features of HTTP/1.0 include:

- **Stateless Protocol**: Each request/response cycle is independent, and the server does not maintain any state between requests.
- **Connection Persistence**: By default, each request/response pair is sent over a separate TCP connection. However, HTTP/1.0 introduced the `Connection: keep-alive` header to allow persistent connections, reducing latency and overhead.
- **Limited Header Fields**: HTTP/1.0 had a limited set of header fields compared to later versions.

### HTTP/1.1:

HTTP/1.1, standardized in 1999, is a significant improvement over HTTP/1.0. It introduced several enhancements and optimizations, including:

- **Persistent Connections by Default**: HTTP/1.1 introduced persistent connections by default, eliminating the need for the `Connection: keep-alive` header.
- **Pipelining**: HTTP/1.1 allows multiple requests to be sent over a single TCP connection without waiting for responses, improving performance.
- **Host Header**: HTTP/1.1 introduced the `Host` header, allowing multiple domains to be hosted on the same IP address.

### HTTP/2:

HTTP/2 is a major revision of the HTTP protocol, standardized in 2015. It was designed to address the limitations and performance bottlenecks of HTTP/1.x. Some key features of HTTP/2 include:

- **Binary Protocol**: HTTP/2 uses a binary framing layer instead of plain text, reducing overhead and improving efficiency.
- **Multiplexing**: Multiple requests and responses can be sent and received in parallel over a single TCP connection, eliminating the need for pipelining.
- **Header Compression**: HTTP/2 uses HPACK compression to compress header fields, reducing bandwidth usage.
- **Server Push**: Servers can push resources to clients proactively, improving page load times.
- **Stream Prioritization**: HTTP/2 allows prioritization of streams, enabling more efficient resource allocation.

### TCP (Transmission Control Protocol):

TCP is a connection-oriented protocol that operates at the transport layer of the OSI model. It provides reliable, ordered, and error-checked delivery of data between applications running on devices connected to a network. TCP ensures that data packets are delivered intact and in order by establishing a connection between the sender and receiver before data transfer.

- **Connection Establishment**: Before data transfer begins, TCP establishes a connection between the client and server using a three-way handshake mechanism (SYN, SYN-ACK, ACK).
- **Reliability**: TCP ensures reliable delivery of data by using acknowledgments, retransmissions, and sequence numbers to detect and recover from packet loss, duplication, and errors.
- **Flow Control**: TCP uses flow control mechanisms to regulate the rate of data transmission between sender and receiver, preventing data overflow and congestion.
- **Connection Termination**: After data transfer is complete, TCP terminates the connection between the client and server using a four-way handshake mechanism (FIN, ACK, FIN, ACK).
## Basic DB: SQL, joins, index..

        CLUSTERED ：聚集索引。非聚集索引：NONCLUSTERED。

        clustered是物理上实现数据排序，并且同一个表里只能有一个clustered索引，而nonclustered是逻辑上的排序。

        微软的SQL Server 支持两种类型的索引:clustered 索引和nonclustered索引。

        Clustered索引在数据表中按照物理顺序存储数据。因为在表中只有一个物理顺序，所以在每个表中只能有一个clustered索引。在查找某个范围内的数据时，Clustered索引是一种非常有效的索引，因为这些数据在存储的时候已经按照物理顺序排好序了。

　　Nonclustered索引不会影响到下面的物理存储，但是它是由数据行指针构成的。如果已经存在一个clustered索引，在nonclustered中的索引指针将包含clustered索引的位置参考。这些索引比数据更紧促，而且对这些索引的扫描速度比对实际的数据表扫描要快得多。  
        PRIMARY KEY 约束默认为 CLUSTERED；UNIQUE 约束默认为 NONCLUSTERED。
## Anything showing on their resumes.
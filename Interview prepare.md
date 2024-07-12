
# Antra
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


# Amazon

### oop knowledge
1. **访问修饰符**:
    
    - `private`: 仅在类内部可访问
    - `protected`: 在类内部和子类中可访问
    - `public`: 任何地方都可访问
    - `default` (无关键字): 在同一个包内可访问
2. **继承 (Inheritance)**:
    
    - 子类可以继承父类的属性和方法
    - 使用 `extends` 关键字来实现继承
    - 子类可以重写(override)父类的方法
    - `super` 关键字用于访问父类的属性和方法
3. **抽象类 (Abstract Class)**:
    
    - 使用 `abstract` 关键字定义
    - 可以包含抽象方法,也可以包含普通方法
    - 抽象类不能被实例化,只能被继承
    - 子类必须实现抽象类中的所有抽象方法,除非子类也是抽象类
4. **接口 (Interface)**:
    
    - 使用 `interface` 关键字定义
    - 接口中的方法默认是 `public abstract` 的
    - 接口中的变量默认是 `public static final` 的
    - 类可以实现多个接口
    - 接口可以继承其他接口
5. **多态 (Polymorphism)**:
    - 父类引用可以指向子类对象
    - 方法的重写(Override)体现多态
    - 方法的重载(Overload)也是一种多态
6. **封装 (Encapsulation)**:
    - 将数据和方法包装在类中
    - 通过访问修饰符控制成员的可见性
    - 提供 Getter 和 Setter 方法来访问私有成员
7. **SOLID 原则**:
    
    - **S**ingle Responsibility Principle (单一职责原则)
    - **O**pen/Closed Principle (开闭原则)
    - **L**iskov Substitution Principle (里氏替换原则)
    - **I**nterface Segregation Principle (接口隔离原则)
    - **D**ependency Inversion Principle (依赖倒置原则)

1. **protected**:
    
    - This variable is declared with the `protected` access modifier, which means it can be accessed by the `PizzaDecor` class and its subclasses, but not directly by other classes.
    - The `protected` access is used instead of `private` because the subclasses need to be able to access this variable to implement their own logic.
2. **final**:
    - The `final` keyword means this variable is immutable - once it is initialized, it cannot be modified.
    - This ensures that the `pizza` instance is set once and cannot be accidentally changed, preserving the encapsulation of `PizzaDecor`.

## OOD

### 例子

#### tiny url
**How long a tiny url would be ? Will it ever expire ?**
**what would be the maximum size of custom url ?**
#Traffic
![[Pasted image 20240707161743.png]]
![[Pasted image 20240707161926.png]]
那我们可以用多台机器，通过sharding的方式，就是把某个URL取一个hash值再％N，这样就把这个请求分配到某台具体机器上，然后再这台机器上进行读取或者存储。另外我们要注意一种分配不均的情况，你可以想象也许机器1就是非常热门，它的负载比其他的机器高很多，但总体负载又不高，如果我们简单的扩容，一方面浪费了机器，涉及到迁移成本，并且也不见得解决真正1号机负载高的问题。最好的做法是把1号机的旁边再放置一台同样规模和数据的机器，这个叫热等待(Hot standby), 通过流量的导流，实现负载均衡。对于可靠性，你想象某台机器当机，它如何做恢复呢？首先你要保证数据是有备份的，也许再另一个数据库中，然后当那台机器重启后，可以先载入上次备份的地方，也叫快照(snapshot)，然后再把日志中应该重新做的操作继续做一遍，这样就保证了数据的一致性。

dynamo DB - key value based nosql database


Assuming _200:1 read/write_ ratio
#### parking lot
##### enum:
```java  
public enum VehicleSize{  
TWOWHEELER, FOURWHEELER;  
}
// size = VehicleSize.Motorcycle;

```
##### entity:
Parkinglot implements Parking
slot
vehicle
ticket
```java
public class FourWheelerWeekDayChargeStrategy implements ParkingChargeStrategy {  
  
@Override  
public int getCharge(int parkHours) {  
if (parkHours < 1) {  
return 20;  
}  
return parkHours * 20;  
}  
}
```

##### interface: 
收费的
```java
public interface ParkingChargeStrategy {  
int getCharge(int parkHours);  
}
```
parking 
```java
public interface Parking {  
  
public Ticket park(Vehicle vehicle) throws ParkingFullException;  
  
public int unPark(Ticket ticket, ParkingChargeStrategy parkingCostStrategy) throws InvalidVehicleNumberException;  
  
}
```

#### decoration pattern - coffee shop/pizza

#### elevator system
- 不需要考虑超重的情况
- 该电梯系统目前只有 1 台电梯，该楼共有 `n` 层，电梯初始在第 1 层
- 每台电梯有三种状态：上升，下降，空闲
- 当电梯往一个方向移动时，在电梯内无法按反向的楼层

enum:
state: up idle down
direction: up and down

class:
elevator
request:
	internal request
	external request

#### 形状工厂
```java
interface Shape {
9    void draw();
10}
11
12class Rectangle implements Shape {
13    // Write your code here
14    @Override
15    public void draw() {
16        System.out.println(" ---- ");
17        System.out.println("|    |");
18        System.out.println(" ---- ");
19   }
20}
```

#### 21点
https://www.jiuzhang.com/problem/black-jack-oo-design/

Class:
Hand：
	List<>card;
Card:
	
player:
Dealer:
	Hand
	bets
	blackjack game
BlackJack
	dealer
	player

```java
	public void placeBets(int amount) throws Exception {
113		if (totalBets < amount) {
114			throw new Exception("No enough money.");
115		}
116		bets = amount;
117		totalBets -= bets;
118	}
```
#### GFS
```java
 Definition of BaseGFSClient
3  class BaseGFSClient {
4      private Map<String, String> chunk_list;
5      public BaseGFSClient() {}
6      public String readChunk(String filename, int chunkIndex) {
7          // Read a chunk from GFS
8      }
9      public void writeChunk(String filename, int chunkIndex,
10      String content) {
11          // Write a chunk to GFS
12      }
13 }
14 
15public class GFSClient extends BaseGFSClient {
16
17    public int chunkSize;
18    public Map<String, Integer> chunkNum;
19
20    public GFSClient(int chunkSize) {
21        // initialize your data structure here
22        this.chunkSize = chunkSize;
23        this.chunkNum = new HashMap<String, Integer>();
24    }
25    
26    // @param filename a file name
27    // @return conetent of the file given from GFS
28    public String read(String filename) {
29        // Write your code here
30        if (!chunkNum.containsKey(filename))
31            return null;
32
33        StringBuffer content = new StringBuffer();
34
35        for (int i = 0; i < chunkNum.get(filename); ++i) {
36            String sub_content = readChunk(filename, i);
37            if (sub_content != null)
38                content.append(sub_content);
39        }
40        return content.toString();
41    }
42
43    // @param filename a file name
44    // @param content a string
45    // @return void
46    public void write(String filename, String content) {
47        // Write your code here
48        int length = content.length();
49
50        int num = (length - 1) / chunkSize + 1;
51        chunkNum.put(filename, num);
52
53        for (int i = 0; i < num; ++i) {
54            int start = i * chunkSize;
55            int end = i == num -1 ? length : (i + 1) * chunkSize; 
56            String sub_content = content.substring(start, end);
57            writeChunk(filename, i, sub_content);
58        }
59    }
60}
```
#### Amazon locks
![[Pasted image 20240706230724.png]]
```java
List<Locker> lockers = locks.values().stream()  
        .filter(l -> !l.status)  
        .sorted((a, b) -> a.size - b.size)  
        .collect(Collectors.toList());
    
public class hasBeenUsedException extends Exception{  
    public hasBeenUsedException(String message){  
        super(message);  
    }  
}

public void pickup(int code) throws hasBeenUsedException{  
    Locker locker = locks.get(code);  
    if (!locker.status) throw new hasBeenUsedException("Ohno, it is empty!");  
    else locker.status = false;  
}

public static void main(String[] args) throws AmazonLocker.hasBeenUsedException {
}
```

### knowledge

![[Pasted image 20240629234938.png]]

![[Pasted image 20240625162603.png]]


## LP
![[Pasted image 20240625160832.png]]

## BQ
Situation Task Action Result

- 对页面的内容进行分片/分屏加载
- 仅加载需要的资源，通过异步或是懒加载的方式加载剩余资源
- 使用骨架屏进行预渲染
- 使用差异化服务，比如读写分离，对于不同场景按需加载所需要的模块
- 使用服务端直出渲染，减少页面二次请求和渲染的耗时
#### why amazon
1. As a tech industry leader, Amazon offers its employees extensive opportunities for professional development and career advancement. Many see working at Amazon as a way to gain valuable experience that can propel their future career growth.
    
2. Company Prestige: Amazon enjoys a strong reputation in the tech industry, and having Amazon on one's resume can be a significant asset. For many job seekers, the chance to work at Amazon is an excellent way to build their professional credentials.
3. 
#### （1）**你曾收到过来自同事或领导的负面反馈吗？你是如何改进的？**

**模范回答：**

**S/T:** 我刚进X公司实习的时候，被分配做一个XXX项目，需要在2个月内完成，时间也比较紧迫。但是我一开始特别想证明自己，想把这个事情独立完成，结果自己也很累，任务做的也磕磕绊绊。于是收到了mentor的反馈，说我应该早些寻求帮助。

**A:** 我意识到了这个问题，于是我开始合理地评估自己面临的困难，并且及时和manager去交流进度。

**R：**我学会了自我评估与及时沟通，最终这个项目成功deadline前上线，而且实现的也很好，Manager也对这个项目给予了肯定。


#### （2）**如果你的小组同事经常表现不好，甚至影响到你工作，您是如何处理的？ search module**

**模范回答：**

他做UI search module
**S/T:** 我和XX一起做了XXX项目，发现他总是做不好，不仅速度慢，还经常有Bug，耽误了进度。

**A:** 于是，我先尝试和他沟通，了解到他的困难和问题，如果可以，协助他解决问题；如果实在无法沟通/无法解决，预估任务能否顺利完成，和manager及时沟通，并且获得了manager的理解和支持。

**R:** 最终任务顺利完成，我也在这个过程中加强了和队友、领导协调和沟通的能力。

> 点评：这道题关联了LP14条的**Ownership（主人翁精神）**。注意不要有埋怨队友的情绪，因为团队是需要合作的。找到队友犯错的原因，**帮助解决问题，完成工作任务**才是重点。

#### （3）**你是否遇到无法完成任务的时候？为什么无法完成？** rxjs

**模范回答：**

**S/T：**在F公司实习时，我有一个XX Project的任务，需要用到rxjs并且结合angular，这些都是我没接触过的知识。但当时我预估可以在2个月内完成。

**A：**我开始自学xx和yy，也按照自己的理解开始去做。但是在做到一半时候发现我的理解有偏差，于是我赶紧与自己的mentor去沟通和请教。

**R：**最后虽然晚了一周完成任务，但是项目的质量非常好。因为及时沟通，所以Mentor和老板也给予了理解。

> 点评：这道题关联LP14条的**Deliver Result（达成业绩）**。回答问题时注意说明无法按时完成任务的原因，并且做了哪些**行动上的补救，以及阐述最后的结果和影响**。

#### （4）conflict - pagination: 
1. S: 在做项目分页的时候，我们对分页的两种版本有了一些分歧。一种是通过hashmap来记录页码，和对应的data，支持。另一种是更简洁，但是没有跳转到某页的功能，并且还没有实现代码。我支持在第一种上进行代码的修改。我的mentor支持直接写 采用第二种。
2. A:  我们对第二种方案的实现与第一种方案的改进进行了评估，并且比较了两种版本在实际应用中的体验。发现第一种方案不够健壮，维护成本高。最终我听从了manager的建议。
3. R: 我也认识到clean code的重要性，磨练了跟人沟通的能力。

**Situation:** There was a disagreement between myself and my manager/peer regarding the pagination solution for our application. I preferred the first solution that was already implemented, but had more complex logic. The second solution was more straightforward, but lacked a key navigation feature.

**Task:** I felt it was important to prioritize user experience, and the first solution already had working functionality. My manager/peer was leaning towards the simpler second solution.

**Action:** I analyzed the potential issues with the second solution and compared the user experience differences between the two options. I presented my findings to my manager/peer, highlighting the trade-offs between development complexity and user experience.

**Result:** After our discussion and analysis, we ultimately decided to go with the second, simpler pagination solution. While it lacked the navigation feature I had preferred, we determined it provided an overall better user experience. Looking back, I believe I handled the situation appropriately by thoroughly evaluating the alternatives and having a constructive dialogue to reach the best decision for the business.


处理压力：

#### （5）limited time 安排优先级SWIFTUI：
1. S 我们在做3Dibner app的时候，会有很多个feature和模块，比如借书还书，会议室预约。。。但我们希望2个月之内上线该项目
2. A：我们最初就进行了一次会议，确定milestone，按照feature的重要性对feature进行排序，确定其优先级。安排更多的时间给重要的feature。
3. R：我们完成了第一版测试，再ddl之前上线。其它fun的feature会在后续接着上线。

#### 12）Impact
#### 13) innovation:


#### (7) 最自豪的项目：swiftUI
#### (6）挑战：RXJS
1. S： 使用一个新的技术：RXJS 去实现project module的异步、同步操作。
3. A：我学习了以前的代码，例如登录的代码。阅读document和googling，printout来学习代码执行的顺序。
4. R：了解了逻辑。成功代码ddl之前上线。

#### 8)1.  Tell me about a time when you didn’t have enough data to make the right decision. 
S: 大学本科的时候做新冠病毒进化检测。因为新的病毒与旧的病毒存在巨大差异，我们的旧模型表现不佳。我们面临选择：是在旧的数据建立的model进行更改，还是直接根据新的数据进行新的model building。但是我们并没有那么多的新病毒数据，因为病毒还在演变。
A:  我们尽可能收集新的数据，做了research，结合医生和研究组的建议，分析他们的演化trend，制定plan，小规模测试。
R: 根据新的数据进行model building. 取得成功。

#### 9）Dive deep - offline persistance
1.Tell me about a time when you were trying to understand a complex problem on your team and you had to dig into the details to figure it out. Who did you talk with or where did you have to look to find the most valuable information? How did you use that information to help solve the problem?

我们在做project的页面的时候，该页面有两个表，第一个是favorite projects，第二个是所有的表。但是我们发现了一个十分wierd的问题，有时favorite的projects会在所有的表中出现两次。最初我仔细检查了代码的逻辑，因为其中有很多异步操作。我在mentor的指导下，优化了代码的结构和逻辑，写得更简洁清晰。但并没有解决该问题。后面我printout每一个异步操作，检查执行顺序，并查看firebase的log，和emulator的log，最终发现是firebase 的offline enablePersistence带来的问题。

**Situation:** My team was working on a project that had a complex issue where favorite projects were sometimes appearing twice in the list of all projects.

**Task:** I needed to thoroughly investigate this issue to understand the root cause and find an effective solution.

**Action:** I started by carefully reviewing the code logic, as there were many asynchronous operations involved. Under the guidance of my mentor, I optimized the code structure and logic to make it more streamlined and clear. However, this did not resolve the problem.

Next, I decided to take a deeper dive into the details. I added print statements to track the execution order of each asynchronous operation. I also examined the Firebase logs and the emulator logs to see if there were any clues there.

Through this more in-depth investigation, I ultimately discovered that the issue was caused by the use of Firebase's `enablePersistence()` feature, which was leading to the duplicate project entries.

**Result:** By thoroughly digging into the details, examining the code, and analyzing the various logs, I was able to identify the root cause of the complex issue - the Firebase offline persistence feature was introducing the unexpected behavior of duplicate project entries.

Armed with this understanding, I was then able to work with the team to implement a solution that addressed the underlying problem. This experience highlighted the importance of not just relying on surface-level information, but truly immersing myself in the intricacies of a complex challenge in order to devise an effective resolution.

Going forward, I will be sure to apply a similar level of diligence and detail-oriented investigation when faced with complex problems on my team.

#### 10) tight ddl
swiftUI
1. situation: 3 months ddl , a lot of features, and new teammates comming in
2. Action: had a meeting at the beginning, assign tasks, make sure milestones and prioritize the tasks with higher importance. maximize the efficiency.
3. We finished all big features, only left one small feature into next iteration and we successfully finishing testing and pushed the app to Appstore, gained over 100+ new user and received over 4.7 out of 5 rating.

# Bytedance
## resume

1. why firebase: 
	1. document-based, cloud firestore, high scalable, - It has advanced features and tools for web hosting. It can be classed as an efficient database, since it syncs with real-time changes. 
2. why nosql: 
	1. flexible data model, fast query, horizontally scaling
3. why rxjs:
	1. involves asynchronous operations, observables streamline the administration of asynchronous processes, such as HTTP requests and user input.

### kafka
kalfa
	1. ==Apache Kafka is a distributed data store optimized for **ingesting and processing streaming data in real-time**.==
	2. In scenarios where immediate and reliable data processing is key, **Apache Kafka** shines as a distributed streaming platform that excels in fault tolerance and event-driven architectures.
	3. ![[Pasted image 20240618111745.png]]
	4. https://blog.devgenius.io/creating-a-news-notification-system-with-kafka-and-spring-boot-01b41837e807
	5. ![[Pasted image 20240618112231.png]]
	6. ### Server sent event

[](https://github.com/mkapiczy/server-sent-events#server-sent-event

Service is using Server Sent Event for one-way communication with client.
![[Pasted image 20240621191536.png]]

kalfa 为什么吞吐量这么高
kafka的producer往broker上发消息是怎么实现的
消息发到哪个partition是怎么决定的
producer发送消息有几个流程
kafka动态扩容之后怎么样让producer知道
## frontend
比如event loop, promise async 判断输出.(网上很多类似题) 
React hooks, useEffect, useLayoutEffect什么区别……
如果需要一个customized hook, 去判断user的view port，怎么写

面了promise：
一个function传入一个数组，数组里是已经定义好的receive or reject，return一个数组，数组是receive后返回的值。

HTTP vs HTTP2, angular VS react, 怎么SEO， 什么是CSRF， 给你一堆async promise timeout await， print出来的顺序，怎么migrate project， safe deployment 怎么做， 怎么优化

算法是蠡扣物留，关于int interval overlap的题





题目是：实现一个tiktok 的投票活动系统，重点在于前端和可复用。不过我从high level讲起，后面大概讲了下API 和数据结构

给了一个数独的网站，参照这个实现一版。

2048游戏

学习前端系统设计的资源不多，Youtube上的JSer和FrontendSystemDesign是很多人都看过的，
https://www.1point3acres.com/bbs/thread-907864-1-1.html


#### eg instagram
![[Pasted image 20240622141115.png]]
![[Pasted image 20240622141315.png]]
![[Pasted image 20240622141332.png]]
![[Pasted image 20240622141353.png]]

#### 前端到底用nginx来做啥
Nginx 是开源、高性能、高可靠的 Web 和反向代理服务器，而且支持热部署，几乎可以做到 7 * 24 小时不间断运行
1. web相关-单页面history配置
2. web相关-跨域问题解决（反向代理或者设置跨域头部）
3. web相关-动静分离 + 缓存
4. 负载均衡
5. 简易的灰度部署
6. 优雅降级-ssr方案的容灾处理
![[Pasted image 20240622142918.png]]

### react相关

#### function component vs class component
1. **语法**
    
    - **Functional Component**: 使用函数定义组件,函数返回 JSX 作为组件的输出。
    - **Class-based Component**: 使用 ES6 类定义组件,需要继承 `React.Component` 并实现 `render()` 方法返回 JSX。
2. **状态管理**
    
    - **Functional Component**: 通常使用 React 的 `useState` hook 来管理组件内部状态。
    - **Class-based Component**: 使用类组件的 `state` 对象来管理组件内部状态。
3. **生命周期钩子**
    
    - **Functional Component**: 使用 React 的生命周期 hook 如 `useEffect`、`useLayoutEffect`、`useMemo`、`useCallback` 等来管理组件的生命周期。
    - **Class-based Component**: 使用类组件的生命周期钩子方法,如 `componentDidMount`、`componentDidUpdate`、`componentWillUnmount` 等。
4.  1. **Hook 特性**
    
    - **Functional Component**: 可以使用 React 提供的各种 Hook 特性,如 `useState`、`useEffect`、`useContext` 等,更加灵活和强大。
    - **Class-based Component**: 无法直接使用 Hook 特性,需要使用其他替代方案,如 HOC 或 Render Props。
### 八股文

CSS: color 和 background-color的区别：color是text，
box-sizing是什么: 就是包含border margin的width,height
HTML：getElementByID 等等方法；
#### js相关
`filter()` 用于过滤数组,`reduce()` 用于数组的累计计算

```
const numbers = [1, 2, 3, 4, 5];
const sum = numbers.reduce((acc, cur) => acc + cur, 0);
console.log(sum); // 15


const numbers = [1, 2, 3, 4, 5];
const evenNumbers = numbers.filter(num => num % 2 === 0);
console.log(evenNumbers); // [2, 4]
```

#### **CSS 居中**

CSS 居中主要有以下几种实现方式:

- 行内元素/文本居中:使用 `text-align: center;`
- 块级元素居中:
    - 水平居中: `margin: 0 auto;`
    - 垂直居中: 利用 `position: absolute;` 和 `transform: translateY(-50%);`
    - 水平垂直居中: 利用 `position: absolute;` 和 `transform: translate(-50%, -50%);`
- Flex 布局居中:
    - 水平居中: `justify-content: center;`
    - 垂直居中: `align-items: center;`
    - 水平垂直居中: `justify-content: center; align-items: center;`

#### 前端缓存
![[Pasted image 20240622160153.png]]

#### 常用的页面优化实现方案包括:

1. 资源优化:压缩、合并、CDN部署、缓存管理等。
2. 渲染优化:减少DOM操作、合理使用硬件加速、优化关键渲染路径等。
3. 网络优化:HTTP/2、服务端渲染、PWA技术等。
4. 代码优化:Tree Shaking、Code Splitting、懒加载等。
5. 监控优化:定期检查性能指标,持续优化。

#### 对于首页加载优化,可以采取以下方式:

1. 压缩和合并CSS/JS文件,减少HTTP请求数。
2. 使用CDN加速静态资源的加载。
3. 开启Gzip压缩,减小资源体积。
4. 采用懒加载技术,延迟加载非关键资源。
5. 合理利用浏览器缓存,降低重复请求。
6. 优化关键渲染路径,尽早展现页面关键内容。

#### 提高页面渲染速度的常见方式包括:

1. 减少DOM节点数量和DOM深度,优化DOM结构。
2. 合理使用硬件加速,提升GPU渲染能力。
3. 使用骨架屏或shimmer loading效果,改善用户体验。
4. 采用service worker技术实现离线缓存和快速响应。
5. 优化图片格式和尺寸,降低图片资源的加载开销。
6. 使用Web Worker分担主线程的计算任务。

#### 单点登录 与 扫码登录
1. **单点登录的原理**:
    - 用户在第一次登录时,应用程序会颁发一个认证令牌(token)给客户端。
    - 之后客户端在访问其他应用时,会携带这个令牌进行认证。
    - 认证中心负责验证令牌的有效性,并返回登录状态。
2. **扫码登录的原理**:
    - 手机端和网页端通过二维码建立连接。
    - 手机端生成唯一的登录凭证,网页端通过轮询获取该凭证的状态。
    - 当手机端确认登录时,网页端会获取到登录成功的状态,完成登录流程。

#### web安全
1. **对称加密**:
    
    - 对称加密是一种加密方式,也称为共享密钥加密。
    - 在对称加密中,发送方和接收方使用相同的密钥进行加密和解密。
    - 这种加密方式相对简单,计算速度快,但需要双方事先协商好密钥,存在密钥管理的问题。
    - 常见的对称加密算法有 AES、DES、Blowfish 等。
2. **XSS (Cross-Site Scripting)**:
    
    - XSS 是一种Web应用程序安全漏洞,攻击者通过注入恶意的脚本代码到网页中,从而控制用户的浏览器并窃取用户数据。
    - 主要有两种类型:
        - 反射型 XSS: 恶意脚本代码包含在 URL 中,被服务器端返回并执行。
        - 存储型 XSS: 恶意脚本代码被存储在服务器端,每次访问页面时都会执行。
    - 预防 XSS 的关键是对用户输入进行充分的验证和过滤。
3. **CSRF (Cross-Site Request Forgery)**:
    
    - CSRF 是一种利用受害者已登录的Web应用程序的一种攻击方式。
    - 攻击者构造一个包含恶意请求的URL或表单,诱使用户点击或提交,从而在用户的授权下执行了非法操作。
    - 预防 CSRF 的关键是使用随机令牌(CSRF token)等机制来验证用户的真实意图。
### 单元测试
Jasmine和Karma是两款广泛应用于前端JavaScript单元测试的工具:

1. **Jasmine**:
    
    - Jasmine是一个行为驱动开发(BDD)风格的JavaScript测试框架。
    - 它提供了一套易于阅读和编写的语法,用于描述应用程序的行为。
    - Jasmine的主要特点包括:
        - 支持异步测试
        - 提供丰富的断言库
        - 可以编写嵌套的测试套件
        - 支持spies(模拟依赖)和matchers(自定义断言)
    - Jasmine可以独立运行,也可以与其他测试运行器集成使用。
2. **Karma**:
    
    - Karma是一个JavaScript测试运行器,用于在浏览器环境中执行单元测试。
    - 它的主要功能包括:
        - 管理和运行测试
        - 自动刷新页面并重新执行测试
        - 支持多种浏览器和移动设备
        - 与各种测试框架(如Jasmine、Mocha等)集成
    - Karma的优势在于:
        - 提供灵活的配置,可以针对不同的项目需求进行定制
        - 支持并发测试,加快测试执行速度
        - 提供测试覆盖率报告

通常情况下,Jasmine用于编写测试用例,Karma则负责运行这些测试用例并生成报告。两者结合使用可以构建一个完整的前端单元测试解决方案,帮助开发者编写高质量的JavaScript代码。

design pattern
1. **MVC (Model-View-Controller)**:
    
    - 模型(Model)负责管理应用程序的数据和逻辑。
    - 视图(View)负责展示数据和处理用户交互。
    - 控制器(Controller)负责协调模型和视图,处理用户输入,更新模型。
    - 控制器直接与视图和模型交互,耦合度较高。
2. **MVP (Model-View-Presenter)**:
    
    - 与MVC类似,但将控制器拆分为Presenter。
    - 模型(Model)和视图(View)的职责与MVC一致。
    - Presenter负责协调模型和视图,处理用户交互。
    - Presenter与视图和模型的耦合度较低,可测试性更强。
3. **MVVM (Model-View-ViewModel)**:
    
    - 模型(Model)和视图(View)的职责与MVC一致。
    - 引入ViewModel作为模型和视图之间的中间层。
    - ViewModel负责将模型数据转换为视图所需的格式。
    - 视图与模型完全解耦,通过数据绑定实现协作。
    - 视图和ViewModel之间的交互更加灵活和可测试。

对比来看:

- MVC中控制器和视图/模型耦合较高,MVVM通过ViewModel实现了视图和模型的完全解耦。
- MVP在MVC基础上引入Presenter,降低了控制器与视图/模型的耦合度。
- MVVM进一步将视图和模型解耦,引入ViewModel作为中间层,实现了更加松耦合的架构。

### 前端code
Image Carousel, Tab Component, Accordion, Dropdown, Star Rating, Tri-state Checkbox。

**async/await就是可以把复杂难懂的异步代码变成类同步语法的语法糖**。

#### promise
```
const onMyBirthday = (isKayoSick) => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (!isKayoSick) {
        resolve(2);
      } else {
        reject(new Error("I am sad"));
      }
    }, 2000);
  });
};
```
#### async/await
```
const handleGuess = async () => {
  try {
    const result = await enterNumber(); // 代替then方法，我们只需将await放在promise前，就可以直接获得结果

    alert(\`Dice: ${result.randomNumber}: you got ${result.points} points\`);

    const isContinuing = await continueGame();

    if (isContinuing) {
      handleGuess();
    } else {
      alert("Game ends");
    }
  } catch (error) { // catch 方法可以由try, catch函数来替代
    alert(error);
  }
};
```

#### fetch
```
const fetchCountry = async (alpha3Code) => {
  try {
    const res = await fetch(
      \`https://restcountries.eu/rest/v2/alpha/${alpha3Code}\`
    );
    const data = await res.json();
    return data;
  } catch (error) {
    console.log(error);
  }
};

const fetchCountryAndNeigbors = async () => {
  const china = await fetchCountry("cn");
  const neighbors = await Promise.all(
    china.borders.map((border) => fetchCountry(border))
  );
  console.log(neighbors);
};

fetchCountryAndNeigbors();
```


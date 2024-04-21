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
OOP, 
SOLID, 
MVC,
design patterns, 
multithreading.
## Basic network
HTTP, 
TCP
## Basic DB: SQL, joins, index..
## Anything showing on their resumes.
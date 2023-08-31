---
title: "Object Oriented_Programming_in_Go"
date: 2023-08-30T14:36:58-04:00
draft: false
---

V. Object-Oriented Programming in Go
# V. Object-Oriented Programming in Go
## A. Structs and methods

### 1. Defining and using structs

a. Syntax for defining structs

In Go, a struct is a composite data type that allows you to group together zero or more values with different data types. You can define a struct using the `type` keyword followed by the struct name and a list of field names and their corresponding data types.

```go
type Person struct {
    Name  string
    Age   int
    Email string
}
```

b. Initializing and assigning values to struct fields

To initialize a struct, you can use the struct literal syntax by assigning values to the struct fields.

```go
person := Person{
    Name:  "John Doe",
    Age:   30,
    Email: "johndoe@example.com",
}
```

c. Accessing and modifying struct fields

You can access struct fields using the dot notation (`structName.fieldName`). To modify a struct field, you can simply assign a new value to it.

```go
fmt.Println(person.Name)  // Output: John Doe

person.Age = 31
fmt.Println(person.Age)   // Output: 31
```

d. Creating and using struct methods

Go allows you to define methods on types, including structs. A method is a function associated with a specific type, and it can access and modify the fields of the struct it is associated with.

```go
func (p Person) PrintDetails() {
    fmt.Printf("Name: %s\nAge: %d\nEmail: %s\n", p.Name, p.Age, p.Email)
}

person.PrintDetails()
```

### 2. Associating methods with structs

a. Syntax for defining methods

To define a method for a struct, you need to specify the receiver type before the method name. The receiver type is the struct on which the method is associated.

```go
func (p Person) PrintDetails() {
    // Method definition
}
```

b. Implementing methods for structs

Inside the method definition, you can access the struct fields using the receiver variable (`p` in this case). You can also modify the struct fields within the method.

```go
func (p Person) PrintDetails() {
    fmt.Printf("Name: %s\nAge: %d\nEmail: %s\n", p.Name, p.Age, p.Email)
}

person.PrintDetails()  // Output: Name: John Doe, Age: 31, Email: johndoe@example.com
```

c. Invoking struct methods

To invoke a struct method, you can use the dot notation (`structInstance.methodName()`).

```go
person.PrintDetails()
```

By associating methods with structs, you can encapsulate related behavior and operations together, making your code more organized and reusable.
# B. Interfaces and Polymorphism

## 1. Defining and Implementing Interfaces

### a. Syntax for Interface Declaration

In Go, an interface is a collection of method signatures. It defines a set of behaviors that a struct must implement to be considered as implementing the interface. The syntax for interface declaration is as follows:

```go
type InterfaceName interface {
    Method1() returnType
    Method2(param1 type, param2 type) returnType
    // ...
}
```

Here, `InterfaceName` is the name of the interface, and `Method1()`, `Method2(param1 type, param2 type)`, etc., are the method signatures that the implementing struct must satisfy. The return type of each method is optional.

For example, let's define an interface named `Shape` with a single method `Area()` that returns a float64:

```go
type Shape interface {
    Area() float64
}
```

### b. Implementing an Interface with a Struct

To implement an interface in Go, a struct needs to define all the methods declared in the interface. This way, the struct implicitly satisfies the interface. Here's an example:

```go
type Rectangle struct {
    length float64
    width  float64
}

func (r Rectangle) Area() float64 {
    return r.length * r.width
}
```

In this example, the `Rectangle` struct implements the `Shape` interface by providing an implementation for the `Area()` method. Now, any variable of type `Shape` can hold a `Rectangle` value.

### c. Implementing Multiple Interfaces

Go allows a struct to implement multiple interfaces simultaneously. To do so, the struct must define all the methods specified by each interface it aims to implement. Here's an example:

```go
type Shape interface {
    Area() float64
}

type Perimeter interface {
    Perimeter() float64
}

type Rectangle struct {
    length float64
    width  float64
}

func (r Rectangle) Area() float64 {
    return r.length * r.width
}

func (r Rectangle) Perimeter() float64 {
    return 2 * (r.length + r.width)
}
```

In this example, the `Rectangle` struct implements both the `Shape` and `Perimeter` interfaces by providing implementations for all the required methods.

## 2. Achieving Polymorphism through Interfaces

### a. Understanding Polymorphism in Go

Polymorphism is the ability of an object to take on many forms. In Go, interfaces enable polymorphism by allowing different types to be treated as the same type when they satisfy a given interface.

### b. Assigning Interface Types to Variables

Since interfaces define a set of behaviors, we can assign any value that implements an interface to a variable of that interface type. This allows us to work with different types using a common interface.

```go
var s Shape
s = Rectangle{length: 5, width: 3}
```

In this example, we assign a `Rectangle` value to a variable `s` of type `Shape`. Even though `Rectangle` is a concrete type and `Shape` is an interface, the assignment is valid because `Rectangle` implements the `Area()` method defined by the `Shape` interface.

### c. Invoking Methods on Interface Types

Once a value is assigned to an interface variable, we can invoke methods declared in the interface on that variable. Go will automatically call the appropriate method implementation based on the underlying type.

```go
s := Rectangle{length: 5, width: 3}
area := s.Area()
```

In this example, we create a `Rectangle` value and assign it to the `s` variable of type `Shape`. We then invoke the `Area()` method on `s`, which will call the `Area()` method implemented by the `Rectangle` struct.

### d. Implementing Polymorphism with Type Assertions

Type assertions allow us to access the underlying concrete type from an interface variable. This enables us to perform type-specific operations on the value.

```go
var s Shape
s = Rectangle{length: 5, width: 3}

rect, ok := s.(Rectangle)
if ok {
    // Access methods specific to Rectangle
    perimeter := rect.Perimeter()
}
```

In this example, we assign a `Rectangle` value to the `s` variable of type `Shape`. We then use a type assertion to access the underlying `Rectangle` type. If the assertion is successful (i.e., `ok` is `true`), we can access methods specific to `Rectangle`, such as `Perimeter()`.

By utilizing interfaces and type assertions, Go allows us to achieve polymorphism and work with different types in a flexible and extensible manner.
# C. Inheritance and Composition

## 1. Understanding inheritance in Go

Inheritance is a fundamental concept in object-oriented programming (OOP) that allows a class to inherit properties and behaviors from another class. However, Go does not support traditional inheritance like some other programming languages such as Java or C++. Instead, it emphasizes composition over inheritance.

Composition is a design technique where a struct can include other structs, effectively combining their properties and methods. This approach promotes code reuse and provides flexibility in defining complex types.

Let's consider an example to understand how composition works in Go:

```go
type Shape struct {
    color string
}

func (s *Shape) setColor(color string) {
    s.color = color
}

type Circle struct {
    Shape
    radius float64
}

func main() {
    c := Circle{Shape: Shape{color: "red"}, radius: 5.0}
    fmt.Println("Circle color:", c.color)
    c.setColor("blue")
    fmt.Println("New circle color:", c.color)
}
```

In the above code, we have a `Shape` struct with a `color` field and a method `setColor()`. The `Circle` struct embeds the `Shape` struct, effectively inheriting its fields and methods.

By creating a new `Circle` instance, we can access the `color` field and call the `setColor()` method from the embedded `Shape` struct. This demonstrates how composition allows us to reuse existing functionality.

## 2. Implementing composition in Go

In Go, composition is achieved through struct embedding. Let's explore the different aspects of implementing composition:

### a. Embedding structs in Go

Struct embedding allows us to include one or more structs within another struct. The fields and methods of the embedded struct become part of the outer struct, enabling composition.

Consider the following example:

```go
type Vehicle struct {
    weight int
}

type Car struct {
    Vehicle
    model string
}

func main() {
    c := Car{Vehicle: Vehicle{weight: 2000}, model: "Sedan"}
    fmt.Println("Car weight:", c.weight)
}
```

In this example, the `Car` struct embeds the `Vehicle` struct. As a result, the `weight` field from the `Vehicle` struct becomes accessible from the `Car` struct.

### b. Accessing embedded struct fields and methods

When a struct is embedded, its fields and methods can be accessed directly from the outer struct. This behavior is similar to inheritance, but with a different syntax.

For instance, let's modify our previous example to include a method in the embedded struct:

```go
type Vehicle struct {
    weight int
}

func (v *Vehicle) startEngine() {
    fmt.Println("Engine started")
}

type Car struct {
    Vehicle
    model string
}

func main() {
    c := Car{Vehicle: Vehicle{weight: 2000}, model: "Sedan"}
    c.startEngine()
}
```

In this updated code, the `Vehicle` struct now has a `startEngine()` method. By embedding the `Vehicle` struct within the `Car` struct, we can directly access and call this method on a `Car` instance.

### c. Overriding embedded struct methods

Go also allows us to override methods of embedded structs in the outer struct. This flexibility allows customization and specialization while reusing existing functionality.

Here's an example that demonstrates method overriding:

```go
type Vehicle struct {
    weight int
}

func (v *Vehicle) startEngine() {
    fmt.Println("Engine started")
}

type Car struct {
    Vehicle
    model string
}

func (c *Car) startEngine() {
    fmt.Println("Car engine started")
}

func main() {
    c := Car{Vehicle: Vehicle{weight: 2000}, model: "Sedan"}
    c.startEngine()
}
```

In this case, the `Car` struct overrides the `startEngine()` method defined in the embedded `Vehicle` struct. As a result, when we call `c.startEngine()`, it prints "Car engine started" instead of the default "Engine started" message.

This ability to override methods provides flexibility in customizing behavior while still leveraging the power of composition.

In conclusion, Go's approach to composition offers a powerful alternative to traditional inheritance. By using embedded structs, we can achieve reusable and flexible code structures, allowing us to design robust object-oriented programs.

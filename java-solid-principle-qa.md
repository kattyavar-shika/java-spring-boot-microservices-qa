# Java Solid principle Questions & Answer

## Disclaimer

- [Disclaimer](disclaimer-qa.md)

## What is the SOLID Principle in Object-Oriented Programming (OOP)?

<details>
<summary>Answer</summary>

- SOLID is a set of five design principles that help developers write more understandable, flexible, and maintainable
  code. The principles are:
    - S: Single Responsibility Principle (SRP)
    - O: Open/Closed Principle (OCP)
    - L: Liskov Substitution Principle (LSP)
    - I: Interface Segregation Principle (ISP)
    - D: Dependency Inversion Principle (DIP)

Each of these principles aims to reduce coupling and increase cohesion in a codebase.

</details>

## What is the Single Responsibility Principle (SRP)?

<details>
<summary>Answer</summary>

- The Single Responsibility Principle (SRP) states that a class should have only one reason to change, meaning that it
  should only have one job or responsibility.

```java
// Violates SRP - a class with multiple responsibilities
class User {
  private String name;
  private String email;

  public void saveToDatabase() {
    // Code to save user to the database
  }

  public void sendEmail() {
    // Code to send email
  }
}

```

- In the above code, the User class has two responsibilities: saving the user to the database and sending emails. To
  adhere to SRP, we can split these responsibilities into separate classes:

```java
class User {
  private String name;
  private String email;
  // User related properties and methods
}

class UserDatabase {
  public void saveToDatabase(User user) {
    // Code to save user to the database
  }
}

class EmailService {
  public void sendEmail(User user) {
    // Code to send email
  }
}

```

</details>

## What is the Open/Closed Principle (OCP)?

<details>
<summary>Answer</summary>

- The Open/Closed Principle (OCP) states that a class should be open for extension but closed for modification.
- This means that you should be able to extend the behavior of a class without changing its existing code.

Issue Example:

```java
// Violates OCP
class Rectangle {
  private int width;
  private int height;

  public int calculateArea() {
    return width * height;
  }
}

class AreaCalculator {
  public int calculateArea(Object shape) {
    if (shape instanceof Rectangle) {
      return ((Rectangle) shape).calculateArea();
    }
    // Adding new shapes requires modifying this method
    return 0;
  }
}

```

- In this code, the AreaCalculator class must be modified whenever a new shape is introduced.

- To adhere to OCP, we can introduce an interface for shapes:

```java
interface Shape {
  int calculateArea();
}

class Rectangle implements Shape {
  private int width;
  private int height;

  @Override
  public int calculateArea() {
    return width * height;
  }
}

class Circle implements Shape {
  private int radius;

  @Override
  public int calculateArea() {
    return (int) (Math.PI * radius * radius);
  }
}

class AreaCalculator {
  public int calculateArea(Shape shape) {
    return shape.calculateArea();
  }
}

```

- Now, new shapes can be added by simply implementing the Shape interface, without changing the AreaCalculator class.

</details>

## What is the Liskov Substitution Principle (LSP)?

<details>
<summary>Answer</summary>

- The Liskov Substitution Principle (LSP) states that objects of a superclass should be replaceable with objects of its
  subclasses without affecting the correctness of the program.
- In other words, subclasses should behave in a way that they can be substituted wherever the parent class is expected.

Issue Example :

```java
class Bird {
  public void fly() {
    // Flying logic
  }
}

class Sparrow extends Bird {
  @Override
  public void fly() {
    // Sparrow specific flying logic
  }
}

class Ostrich extends Bird {
  @Override
  public void fly() {
    // Ostrich cannot fly, so this violates LSP
  }
}

```

- In this example, Ostrich is a subclass of Bird, but it cannot fly.
- Replacing Bird with Ostrich breaks the Liskov Substitution Principle because the fly method is expected to work for
  all subclasses of Bird.

- To fix this, we can redesign the inheritance hierarchy:

```java
interface Flyable {
  void fly();
}

class Sparrow implements Flyable {
  @Override
  public void fly() {
    // Sparrow specific flying logic
  }
}

class Ostrich {
  public void run() {
    // Ostrich-specific running logic
  }
}

```

- Now, we separate the Flyable behavior and avoid forcing Ostrich to inherit from Bird.

</details>

## What is the Interface Segregation Principle (ISP)?

<details>
<summary>Answer</summary>

- The Interface Segregation Principle (ISP) states that no client should be forced to depend on methods it does not use.
  In other words, classes should not be forced to implement interfaces they don't need.

Issue:

```java
// Violates ISP
interface Worker {
  void work();

  void eat();
}

class Employee implements Worker {
  @Override
  public void work() {
    // Employee work logic
  }

  @Override
  public void eat() {
    // Employee eat logic
  }
}

class Robot implements Worker {
  @Override
  public void work() {
    // Robot work logic
  }

  @Override
  public void eat() {
    // Robot does not eat, violating ISP
  }
}

```

- To follow ISP, we can create separate interfaces for distinct functionalities:

```java
interface Workable {
  void work();
}

interface Eatable {
  void eat();
}

class Employee implements Workable, Eatable {
  @Override
  public void work() {
    // Employee work logic
  }

  @Override
  public void eat() {
    // Employee eat logic
  }
}

class Robot implements Workable {
  @Override
  public void work() {
    // Robot work logic
  }
}

```

- Now, Robot does not have to implement the eat method, adhering to ISP.

</details>

## What is the Dependency Inversion Principle (DIP)?

<details>
<summary>Answer</summary>

- The Dependency Inversion Principle (DIP) states that high-level modules should not depend on low-level modules, but
  both should depend on abstractions.
- Additionally, abstractions should not depend on details. Details should depend on abstractions.

Issue:

```java
// Violates DIP
class LightBulb {
  public void turnOn() {
    System.out.println("Light turned on");
  }

  public void turnOff() {
    System.out.println("Light turned off");
  }
}

class Switch {
  private LightBulb bulb;

  public Switch(LightBulb bulb) {
    this.bulb = bulb;
  }

  public void operate() {
    // Direct dependency on LightBulb
    bulb.turnOn();
  }
}

```

To adhere to DIP, we can introduce an abstraction:

```java
interface Switchable {
  void turnOn();

  void turnOff();
}

class LightBulb implements Switchable {
  @Override
  public void turnOn() {
    System.out.println("Light turned on");
  }

  @Override
  public void turnOff() {
    System.out.println("Light turned off");
  }
}

class Switch {
  private Switchable device;

  public Switch(Switchable device) {
    this.device = device;
  }

  public void operate() {
    device.turnOn();
  }
}

```

- Now, Switch depends on the Switchable interface (an abstraction), not on a concrete LightBulb class. This allows
  Switch to work with any Switchable device, adhering to DIP.

</details>
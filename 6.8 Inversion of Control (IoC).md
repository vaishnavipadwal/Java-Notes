# **Inversion of Control (IoC)**  

Inversion of Control means **giving the control of creating and managing objects** to the framework (like Spring), instead of the developer writing the code manually to create objects. In simple words, **the control of object creation and dependency management is inverted** from the programmer to the container (like Spring container).

Normally, in a basic Java program, if you need an object, you use `new` keyword like:

```java
Car car = new Car();
```

Here, you are controlling the creation of the `Car` object yourself.

But in **IoC**, you don't create the object manually. Instead, you define the object and its dependencies in a configuration file (XML) or using annotations, and the **Spring container automatically creates** and manages those objects for you.

---

**Real-World Example**  
Imagine you are building a house.  
Without IoC: you yourself are buying bricks, cement, wiring, pipes and constructing everything.  
With IoC: you hire a contractor (Spring container) and just tell him **what you want**. He takes care of **how to build** and **how to connect** everything.

---

**How Spring Implements IoC**

- Spring has a **container** (like `ApplicationContext`).
- It **reads the configuration** (XML or Annotations like `@Component`, `@Bean`, `@Autowired`).
- It **creates** all required objects (beans).
- It **manages** the life cycle and **injects** dependencies automatically.

---

**Simple Programmatic Example**

Model class:

```java
@Component
public class Car {
    public void drive() {
        System.out.println("Car is running...");
    }
}
```

Controller class:

```java
@Component
public class CarService {

    @Autowired
    private Car car;

    public void start() {
        car.drive();
    }
}
```

Main application:

```java
AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
CarService carService = context.getBean(CarService.class);
carService.start();
```

Here, you **did not manually create `Car` object**.  
Spring **injected `Car` automatically** into `CarService` using **IoC**.

---

**Key Points of IoC**

- Objects are created, managed, and destroyed by Spring Container.
- Dependencies are injected automatically.
- It improves code modularity, flexibility, and testability.

---


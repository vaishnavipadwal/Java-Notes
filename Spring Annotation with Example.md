# **Spring Annotation with Example**

### **Important Spring annotations are:**
- `@Component`
- `@Controller`
- `@Service`
- `@Repository`
- `@Autowired`
- `@Configuration`
- `@Bean`

Each of them plays a specific role in building a Spring application.

**Simple Example**

Suppose you are creating a simple application that uses a service class to display a message.

**1. Create a Service Class**

```java
import org.springframework.stereotype.Service;

@Service
public class MyService {
    public String getMessage() {
        return "Hello from MyService!";
    }
}
```
Here, `@Service` tells Spring that this class is a service component and should be managed as a bean.

**2. Create a Controller Class**

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;

@Controller
public class MyController {

    @Autowired
    private MyService myService;

    public void displayMessage() {
        System.out.println(myService.getMessage());
    }
}
```
Here, `@Controller` marks this class as a controller component. `@Autowired` automatically injects the `MyService` bean into `MyController`.

**3. Configuration Class**

```java
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;

@Configuration
@ComponentScan(basePackages = "com.example")
public class AppConfig {
}
```
Here, `@Configuration` marks this class as a configuration class, and `@ComponentScan` tells Spring to scan the package `com.example` for components like `@Service`, `@Controller`, etc.

**4. Main Application**

```java
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class MainApp {
    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
        MyController controller = context.getBean(MyController.class);
        controller.displayMessage();
    }
}
```
When you run this, it will output:

```
Hello from MyService!
```


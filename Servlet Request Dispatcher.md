 # **Using RequestDispatcher in Servlets to forward a request from one servlet to another — while passing data using request attributes**

---

## 1. **First Servlet – `FirstServlet.java`**

This servlet sets a message in the request and forwards the request to another servlet.

```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.WebServlet;

@WebServlet("/FirstServlet")
public class FirstServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {

        // Set content type
        response.setContentType("text/html");

        // Set an attribute in the request
        request.setAttribute("message", "Hello from FirstServlet!");

        // Forward the request to SecondServlet
        RequestDispatcher dispatcher = request.getRequestDispatcher("SecondServlet");
        dispatcher.forward(request, response);
    }
}
```

---

## 2. **Second Servlet – `SecondServlet.java`**

This servlet receives the forwarded request and accesses the attribute.

```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.WebServlet;

@WebServlet("/SecondServlet")
public class SecondServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {

        // Set content type
        response.setContentType("text/html");

        // Get the attribute from the request
        String msg = (String) request.getAttribute("message");

        // Display the message
        PrintWriter out = response.getWriter();
        out.println("<h2>Second Servlet</h2>");
        out.println("<p>Message received: " + msg + "</p>");
    }
}
```

---

## 3. **How to Run**

Just hit this URL in the browser:
```
http://localhost:8080/YourAppName/FirstServlet
```

---

## Output

```
Second Servlet
Message received: Hello from FirstServlet!
```

---

### What are we trying to do?

We're creating **two servlets**:

1. `FirstServlet`: sets some data (a message).
2. `SecondServlet`: receives that data and shows it.

We use **RequestDispatcher** to *forward* the request from the first servlet to the second. When we forward, we also send some data using the **request object**.

---

### FirstServlet.java – What happens here?

```java
request.setAttribute("message", "Hello from FirstServlet!");
```
This line puts data into the request. Think of `request` as a temporary container that travels from one servlet to another. You're putting `"Hello from FirstServlet!"` inside it and naming it `"message"`.

```java
RequestDispatcher dispatcher = request.getRequestDispatcher("SecondServlet");
dispatcher.forward(request, response);
```
These two lines mean:
- "I want to forward this request to another servlet named `SecondServlet`."
- And then you actually *send* the request using `forward()`.

So, no response is shown here in the browser yet. It’s being sent over to the second servlet.

---

### SecondServlet.java – What happens here?

```java
String msg = (String) request.getAttribute("message");
```
This is where `SecondServlet` *pulls out* the data from the request. It says: “Hey, I see there’s an attribute named `message`—let’s read it.”

```java
out.println("<p>Message received: " + msg + "</p>");
```
Now we display the message we got. So if `FirstServlet` sent `"Hello from FirstServlet!"`, that’s what gets printed here.

---

### Flow Summary (Like a delivery):

1. You open the browser and go to `FirstServlet`.
2. It prepares a parcel (sets data inside `request`) and forwards it to `SecondServlet`.
3. `SecondServlet` receives the parcel and opens it (gets the attribute from the request).
4. Then it prints the message on the screen.

---

### Why use this in real life?

Let’s say:
- You have a login form.
- One servlet checks the credentials.
- If login is valid, it forwards the request to a **dashboard servlet** and passes the **username** or **login status**.
That’s a real-world use of `RequestDispatcher`.

# **How to handle sessions in Servlet using cookies**


### **1. What is a Session?**

A **session** allows the server to store user-specific information (like login data) between multiple requests from the same client.

---

### **2. What is a Cookie?**

A **cookie** is a small piece of data that the server sends to the client. The client stores it and sends it back with future requests to the server. Cookies are commonly used to manage **sessions**.

---

### **3. Steps to Handle Session Using Cookies in Servlets**

1. **Create a cookie on user login or form submission.**
2. **Add the cookie to the response.**
3. **In the next request, read the cookie from the request.**
4. **Use the cookie value to identify the user session.**

---

### **4. Program Example**

#### **First Servlet: Create and Set Cookie**
```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class SetCookieServlet extends HttpServlet {
    public void doPost(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
        String username = request.getParameter("username");

        Cookie userCookie = new Cookie("username", username);
        userCookie.setMaxAge(60 * 60); // 1 hour
        response.addCookie(userCookie);

        response.setContentType("text/html");
        PrintWriter out = response.getWriter();
        out.println("<h2>Welcome, " + username + "! Cookie is set.</h2>");
    }
}
```

#### **HTML Form to trigger it**
```html
<form action="setcookie" method="post">
  Enter Name: <input type="text" name="username" />
  <input type="submit" value="Submit" />
</form>
```

#### **web.xml Mapping**
```xml
<servlet>
  <servlet-name>SetCookieServlet</servlet-name>
  <servlet-class>SetCookieServlet</servlet-class>
</servlet>

<servlet-mapping>
  <servlet-name>SetCookieServlet</servlet-name>
  <url-pattern>/setcookie</url-pattern>
</servlet-mapping>
```

---

#### **Second Servlet: Read Cookie to Identify Session**
```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class ReadCookieServlet extends HttpServlet {
    public void doGet(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
        Cookie[] cookies = request.getCookies();
        String username = "Guest";

        if (cookies != null) {
            for (Cookie c : cookies) {
                if (c.getName().equals("username")) {
                    username = c.getValue();
                }
            }
        }

        response.setContentType("text/html");
        PrintWriter out = response.getWriter();
        out.println("<h2>Hello again, " + username + "!</h2>");
    }
}
```

#### **web.xml Mapping**
```xml
<servlet>
  <servlet-name>ReadCookieServlet</servlet-name>
  <servlet-class>ReadCookieServlet</servlet-class>
</servlet>

<servlet-mapping>
  <servlet-name>ReadCookieServlet</servlet-name>
  <url-pattern>/readcookie</url-pattern>
</servlet-mapping>
```

---

### **How It Works**
- User submits the form → `SetCookieServlet` stores the name in a cookie.
- Later, user accesses `/readcookie` → `ReadCookieServlet` reads the cookie and welcomes the user by name.


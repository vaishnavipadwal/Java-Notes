# **Servlet to accept student information from an HTML form and display it on the browser.**

###  1. **HTML Form – student.html**

```html
<!DOCTYPE html>
<html>
<head>
    <title>Student Info Form</title>
</head>
<body>
    <h2>Enter Student Details</h2>
    <form action="StudentServlet" method="post">
        Name: <input type="text" name="name"><br><br>
        Roll No: <input type="text" name="roll"><br><br>
        Course: <input type="text" name="course"><br><br>
        Marks: <input type="text" name="marks"><br><br>
        <input type="submit" value="Submit">
    </form>
</body>
</html>
```

---

### 2. **Servlet – StudentServlet.java**

```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.WebServlet;

@WebServlet("/StudentServlet")
public class StudentServlet extends HttpServlet {

    protected void doPost(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
        response.setContentType("text/html");
        PrintWriter out = response.getWriter();

        // Retrieve form data
        String name = request.getParameter("name");
        String roll = request.getParameter("roll");
        String course = request.getParameter("course");
        String marks = request.getParameter("marks");

        // Display student information
        out.println("<h2>Student Information</h2>");
        out.println("<p>Name: " + name + "</p>");
        out.println("<p>Roll No: " + roll + "</p>");
        out.println("<p>Course: " + course + "</p>");
        out.println("<p>Marks: " + marks + "</p>");
    }
}
```

---

### Output
If the user enters:

```
Name: Aarti  
Roll No: 23  
Course: MCA  
Marks: 85
```
Then the output will be:
```
Student Information  
Name: Aarti  
Roll No: 23  
Course: MCA  
Marks: 85
```

---

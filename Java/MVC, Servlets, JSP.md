1. **Servlets**
- Java programs that run on a server and handle client requets 
- Backbone of Java web apps (Dynamic content creation, Http requests)
**Purpose**
To process requests from web browsers, communicate with databases, generate responses

**How it works**
A client sends an HTTP request to a web server
Server forwards the request
Servlet processes the request, interacts with any backend resources, send back HTTP response

**Example**: A login form sends a username/password to the server, and a servlet verifies it.

2. **JSP**
Allows embedding java code directly to html pages. It's used to create dynamic web pages.

Simplifies the process of creating dynamic content
When a JSP page is requested, server converts it to servlet
Java code on JSP page is excecuted on the server, generated HTML is returned

**Example**: A JSP page might dynamically display the username after a user logs in.

3. **MVC**
Design pattern used to seperate logic of application into three components:

**Model**: Represents Data/Bussness logic - Interacts with database (Dao Implementations)
**View**: Presentation Layer, (HTML, jsp pages)
**Controller**: Processes user input, interacts with the model to retrieve/update data

**How MVC works in a Java Web app**
Controller (servlet) receives a user request
Controller interacts with model to process data
Model provides the processed data back to Controller
Controller forwards data to View

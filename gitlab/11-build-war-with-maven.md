# Build war-file with maven 

## Part 1: pom.xml  (Project Object Model)

```
# put this file:
pom.xml
# in top folder
```

```
<project xmlns="http://maven.apache.org/POM/4.0.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>io.happycoding</groupId>
  <artifactId>hello-world-maven</artifactId>
  <version>1</version>
  <packaging>war</packaging>

  <properties>
    <!-- Java 11 -->
    <maven.compiler.source>11</maven.compiler.source>
    <maven.compiler.target>11</maven.compiler.target>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>

  <dependencies>
    <!-- Jakarta Servlets API -->
    <dependency>
      <groupId>jakarta.servlet</groupId>
      <artifactId>jakarta.servlet-api</artifactId>
      <version>5.0.0</version>
      <scope>provided</scope>
    </dependency>
  </dependencies>

  <build>
    <plugins>
      <!-- Enable building as a .war file with `mvn package` -->
      <plugin>
        <artifactId>maven-war-plugin</artifactId>
        <version>3.3.1</version>
      </plugin>
    </plugins>

    <!-- The output .war file's name, which will be the name of the webapp. -->
    <finalName>${project.artifactId}</finalName>
  </build>

```

## Part 2:  /src/main/webapp/index.html 

```
<!DOCTYPE html>
<html>
  <head>
    <title>Server Hello World: Maven</title>
  </head>
  <body>
    <h1>Happy Coding</h1>
    <p>Hello world!</p>
  </body>
</html>
```

## Part 3: /src/main/java/io/happycoding/servlets/HelloWorldServlets.java

```
package io.happycoding.servlets;

import java.io.IOException;

import jakarta.servlet.annotation.WebServlet;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

@WebServlet("/hello")
public class HelloWorldServlet extends HttpServlet {

  @Override
  public void doGet(HttpServletRequest request, HttpServletResponse response)
      throws IOException {
    response.setContentType("text/html;");
    response.getWriter().println("<h1>Hello world!</h1>");
  }
}
```

## Part 4: .gitlab-ci.yml 

```



```

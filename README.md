# 🚀 Maven + Docker Demo Project

This project demonstrates how to build and run a simple Java application using Maven and Docker. It is ideal for beginners learning about containerizing Java applications, building with Maven, and running the app locally or in a CI/CD pipeline (e.g., Jenkins).

---

## 🛠️ Local Setup: Maven + Docker

Follow these steps to set up and run the project on your local machine.

### ✅ Prerequisites

Make sure you have the following tools installed on your system:

- **Bash** (for running terminal commands)
- **Java 8+ (JDK)**
    ```bash
    java -version
    ```
- **Maven**
    ```bash
    mvn -version
    ```
- **Docker**
    ```bash
    docker --version
    ```

---

### 🏗️ Step 1 : Project Structure

Your project directory should look like this:

```
dock-Jen/
├── Dockerfile
├── Jenkinsfile      # (optional for CI/CD)
├── pom.xml
├── README.md
└── src/
    └── main/
        └── java/
            └── com/demo/DemoApp.java
```

#### 📄 DemoApp.java Example

A minimal Java application demonstrating standard output.

```java
package com.demo;

public class DemoApp {
    public static void main(String[] args) {
        System.out.println("Hello from Docker + Maven Demo App!");
    }
}
```

---

### 📝 pom.xml – Full, Corrected Version

This is the Maven Project Object Model configuration for your project. It specifies dependencies, Java version, and build plugins.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.demo</groupId>
    <artifactId>maven-docker-demo</artifactId>
    <version>1.0-SNAPSHOT</version>
    <properties>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>
    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13.2</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>log4j</groupId>
            <artifactId>log4j</artifactId>
            <version>1.2.17</version>
        </dependency>
    </dependencies>
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.1</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-jar-plugin</artifactId>
                <version>3.2.2</version>
                <configuration>
                    <archive>
                        <manifest>
                            <mainClass>com.demo.DemoApp</mainClass>
                        </manifest>
                    </archive>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

---

### 🐳 Step 2 : Dockerfile

The Dockerfile defines the environment to run your Java application inside a container.

```dockerfile
FROM openjdk:11-jre-slim
WORKDIR /app
COPY target/maven-docker-demo-1.0-SNAPSHOT.jar app.jar
ENTRYPOINT ["java", "-jar", "app.jar"]
```

---

### ⚙️ Step 3 : Build and Run Locally

#### 1. Build the JAR with Maven

```bash
cd /path/to/dock-Jen
mvn clean package
```

Check that the JAR file is created:

```bash
ls target/
# You should see: maven-docker-demo-1.0-SNAPSHOT.jar
```

#### 2. Build Docker Image

```bash
docker build -t demo-app-image .
```

#### 3. Run Docker Container

```bash
docker run --rm demo-app-image
```

#### 📦 Output

You should see:

```
Hello from Docker + Maven Demo App!
```

---

## 🔄 CI/CD with Jenkins

This project supports automated pipelines with Jenkins and Docker.

- **Build**: Compile and package your code.
- **Test**: Run unit tests.
- **Dockerize**: Build the Docker image.
- **Deploy**: Push or deploy the built image.

### 📝 Requirements

- Java 17+
- Maven 3.8+
- Docker & Docker Compose
- Jenkins (with Docker plugins)

---

## 🧑‍💻 Author

**✨ Rajat Jaiswal**

- Passionate about Cloud ☁️, DevOps ⚙️, and Backend 🐳

---

## 📝 Common Use Cases

- **Learning DevOps**: Use this project to practice containerizing Java apps.
- **Team Onboarding**: Demonstrate simple Java CI/CD with Maven and Docker.
- **Template**: Serve as a base for more complex Java microservices.

---

## 📦 Summary Table

| File/Folder      | Purpose                                     |
|------------------|---------------------------------------------|
| `Dockerfile`     | Builds a Docker image for the Java app      |
| `Jenkinsfile`    | (Optional) Jenkins CI/CD pipeline           |
| `pom.xml`        | Maven project configuration                 |
| `src/main/java`  | Java source code                            |
| `DemoApp.java`   | Main Java application entry point           |

---

## 📊 Build & Run: Flowchart

```mermaid
flowchart TD
    A[Developer writes code] --> B[Run mvn package]
    B --> C[Generates JAR file]
    C --> D[Build Docker image]
    D --> E[Run Docker container]
    E --> F[App prints: "Hello from Docker + Maven Demo App!"]
```
---

## ❓ FAQ

- **Q: Can I use Java 11 or higher?**
  - A: Yes, but ensure the Docker image and Maven config match your Java version.
- **Q: How do I add dependencies?**
  - A: Add them to `pom.xml` under `<dependencies>`.
- **Q: Can I run this in the cloud?**
  - A: Yes! Any Docker-compatible environment will work.

---

Happy coding! 🚀

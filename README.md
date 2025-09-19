A. Local Setup: Maven + Docker
Prerequisites
Install Java 8+ (JDK).

 java -version
Install Maven.

 mvn -version
Install Docker.

 docker --version
 
Step 1: Project Structure
Ensure your project looks like this:
 
dock-Jen/
 ├── Dockerfile
 ├── Jenkinsfile (optional for later)
 ├── pom.xml
 ├── README.md
 └── src/
 	└── main/
     	└── java/
         	└── com/demo/DemoApp.java









DemoApp.java example:
 
package com.demo;
public class DemoApp {
 	public static void main(String[] args) {
     	System.out.println("Hello from Docker + Maven Demo App!");
 	}
 }
pom.xml – full, corrected version:
 
<!-- The pom.xml we finalized with Java 8 + Main-Class + dependencies -->
 <project xmlns="http://maven.apache.org/POM/4.0.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                          	http://maven.apache.org/xsd/maven-4.0.0.xsd">
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
 
Step 2: Dockerfile
 
FROM openjdk:11-jre-slim
 WORKDIR /app
 COPY target/maven-docker-demo-1.0-SNAPSHOT.jar app.jar
 ENTRYPOINT ["java", "-jar", "app.jar"]
 
Step 3: Build and Run Locally
Build the JAR with Maven
 
cd /path/to/dock-Jen
 mvn clean package
Check the JAR:
 
ls target/
 # You should see maven-docker-demo-1.0-SNAPSHOT.jar
Build Docker image
 
docker build -t demo-app-image .
Run Docker container
 
docker run --rm demo-app-image
Output should be:
 
Hello from Docker + Maven Demo App!
Local setup complete.


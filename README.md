🪜 Step 1: Create a Maven Project in IntelliJ
Open IntelliJ IDEA.

Go to File → New → Project.

Choose Maven (from the left panel).

Uncheck Create from archetype.

Click Next.

Fill the following:

GroupId: com.monisha

ArtifactId: oracleconnect

Version: leave default

Name: oracleconnect

Click Next → Finish.

🪜 Step 2: Set up the Maven pom.xml
Open your pom.xml and replace everything with this:

xml
Copy
Edit
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
         http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.monisha</groupId>
    <artifactId>oracleconnect</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>jar</packaging>
    <name>oracleconnect</name>

    <properties>
        <java.version>17</java.version>
        <spring.boot.version>3.2.4</spring.boot.version>
    </properties>

    <dependencies>
        <!-- Spring Boot Starter Web -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
            <version>${spring.boot.version}</version>
        </dependency>

        <!-- Spring Data JPA -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
            <version>${spring.boot.version}</version>
        </dependency>

        <!-- Oracle JDBC Driver -->
        <dependency>
            <groupId>com.oracle.database.jdbc</groupId>
            <artifactId>ojdbc8</artifactId>
            <version>19.3.0.0</version>
        </dependency>

        <!-- Spring Boot Starter -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter</artifactId>
            <version>${spring.boot.version}</version>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <!-- Spring Boot Plugin -->
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <version>${spring.boot.version}</version>
            </plugin>
        </plugins>
    </build>
</project>
➡ Then click the Maven reload button in the right pane of IntelliJ.

🪜 Step 3: Project Structure Setup
Inside src/main/java, create this package structure:

markdown
Copy
Edit
com.monisha.oracleconnect
 ├── OracleconnectApplication.java
 ├── model
 │    └── User.java
 ├── repository
 │    └── UserRepository.java
 └── controller
      └── UserController.java
🪜 Step 4: Add Code Files
OracleconnectApplication.java
java
Copy
Edit
package com.monisha.oracleconnect;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class OracleconnectApplication {
    public static void main(String[] args) {
        SpringApplication.run(OracleconnectApplication.class, args);
    }
}
model/User.java
java
Copy
Edit
package com.monisha.oracleconnect.model;

import jakarta.persistence.*;

@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;
    private String email;

    // Getters and setters
    public Long getId() { return id; }
    public void setId(Long id) { this.id = id; }

    public String getName() { return name; }
    public void setName(String name) { this.name = name; }

    public String getEmail() { return email; }
    public void setEmail(String email) { this.email = email; }
}
repository/UserRepository.java
java
Copy
Edit
package com.monisha.oracleconnect.repository;

import com.monisha.oracleconnect.model.User;
import org.springframework.data.jpa.repository.JpaRepository;

public interface UserRepository extends JpaRepository<User, Long> {
}
controller/UserController.java
java
Copy
Edit
package com.monisha.oracleconnect.controller;

import com.monisha.oracleconnect.model.User;
import com.monisha.oracleconnect.repository.UserRepository;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/users")
public class UserController {

    private final UserRepository repo;

    public UserController(UserRepository repo) {
        this.repo = repo;
    }

    @PostMapping
    public User createUser(@RequestBody User user) {
        return repo.save(user);
    }

    @GetMapping
    public List<User> getUsers() {
        return repo.findAll();
    }
}
🪜 Step 5: application.properties
Create this file:
src/main/resources/application.properties

properties
Copy
Edit
# Oracle DB
spring.datasource.url=jdbc:oracle:thin:@localhost:1521/XEPDB1
spring.datasource.username=your_username
spring.datasource.password=your_password
spring.datasource.driver-class-name=oracle.jdbc.OracleDriver

# Hibernate
spring.jpa.database-platform=org.hibernate.dialect.Oracle12cDialect
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
🔁 Replace your Oracle DB credentials above.

🟢 Final Step: Run Your App
Right-click on OracleconnectApplication.java → Run.

Test endpoints:

GET http://localhost:8080/users

POST http://localhost:8080/users with JSON:

json
Copy
Edit
{
  "name": "Monisha",
  "email": "monisha@example.com"
}
Let me know if you want me to give you this full setup as a ZIP file, or if you get stuck on any part! 💪✨













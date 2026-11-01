# spring-jakartaee
How Spring Boot Uses Jakarta EE

Instead of implementing the entire specification (the former "Java EE Full Profile"), Spring Boot uses individual Jakarta EE specifications under the hood:


Jakarta Servlet (Jakarta Servlets 6.0): This is the foundation of Spring MVC. The Tomcat server built into Spring Boot 3+ implements the Jakarta Servlet API.


Jakarta Persistence (JPA 3.1): Used by Spring Data JPA (with Hibernate 6+ by default).


Jakarta Validation (Bean Validation 3.0): Used by Spring validation annotations (e.g., @NotNull, @Size).


Jakarta JSON Binding / Processing: Used for JSON manipulation.


Jakarta Transactions (JTA): Used for declarative transaction management (@Transactional).


Package Change: javax.* to jakarta.*
If you are migrating a project from Spring Boot 2.x to Spring Boot 3.x, the main practical difference is the change in how you import classes in your code:

// ❌ Padrão antigo (Spring Boot 2.x / Java EE / javax)
import javax.persistence.Entity;
import javax.persistence.Id;
import javax.servlet.http.HttpServletRequest;

// ✅ Padrão atual (Spring Boot 3.x / Jakarta EE)
import jakarta.persistence.Entity;
import jakarta.persistence.Id;
import jakarta.servlet.http.HttpServletRequest;


#How do I update the Maven/Gradle dependencies to ensure compatibility with Jakarta EE in Spring Boot 3?

Old Addiction (Spring Boot 2 / javax),Nova Dependência (Spring Boot 3 / jakarta)
javax.persistence:javax.persistence-api,jakarta.persistence:jakarta.persistence-api
javax.validation:validation-api,jakarta.validation:jakarta.validation-api
javax.servlet:javax.servlet-api,jakarta.servlet:jakarta.servlet-api
javax.annotation:javax.annotation-api,jakarta.annotation:jakarta.annotation-api
javax.transaction:javax.transaction-api,jakarta.transaction:jakarta.transaction-api
Sources

Note: If you use the official Spring Boot 3 starters (e.g., spring-boot-starter-data-jpa, spring-boot-starter-web), Spring Boot already manages these versions automatically via its BOM (Bill of Materials).


2. Updating Maven (pom.xml)
A. Update the Spring Boot and Java versions
Make sure the Java property is set to version 17 (or higher) and the Spring Boot parent is set to version 3.x:

<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>3.2.x</version> <!-- ou versão mais recente do Spring Boot 3 -->
    <relativePath/>
</parent>

<properties>
    <java.version>17</java.version>
</properties>

B. Removing Old Explicit Dependencies
Remove any legacy javax dependencies that are manually declared in your pom.xml. If you need to explicitly declare a Jakarta specification, use the new groupId

<!-- Exemplo correto para Jakarta Persistence (Hibernate / JPA) -->
<dependency>
    <groupId>jakarta.persistence</groupId>
    <artifactId>jakarta.persistence-api</artifactId>
</dependency>

<!-- Exemplo correto para Jakarta Validation -->
<dependency>
    <groupId>jakarta.validation</groupId>
    <artifactId>jakarta.validation-api</artifactId>
</dependency>

3. Updating Gradle (build.gradle)
A. Update the plugin and Java versions
In your build.gradle file, define the Spring Boot 3 plugin and configure compatibility with JVM 17:

plugins {
    id 'org.springframework.boot' version '3.2.x'
    id 'io.spring.dependency-management' version '1.1.4'
    id 'java'
}

java {
    sourceCompatibility = JavaVersion.VERSION_17
    targetCompatibility = JavaVersion.VERSION_17
}

plugins {
    id 'org.springframework.boot' version '3.2.x'
    id 'io.spring.dependency-management' version '1.1.4'
    id 'java'
}

java {
    sourceCompatibility = JavaVersion.VERSION_17
    targetCompatibility = JavaVersion.VERSION_17
}

B. Updating Dependencies
Replace the old javax dependencies with the corresponding jakarta dependencies:

dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-web'
    implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
    
    // Se precisar declarar a especificação do Jakarta Bean Validation explicitamente:
    implementation 'jakarta.validation:jakarta.validation-api'
}


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

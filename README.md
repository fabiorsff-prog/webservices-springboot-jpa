# 🛒 Web Services with Spring Boot & JPA / Hibernate

A complete RESTful Web API built with **Java** and **Spring Boot**, following layered architecture best practices, object-relational mapping (ORM) with **JPA/Hibernate**, and standardized error handling.

This project simulates a complete Order Management and E-commerce domain, featuring users, orders, order items, products, categories, and payment processing.

Project from the online course Java COMPLETO Programação Orientada a Objetos + Projetos by Nelio Alves.

---

## 🏛️ Domain Model & Architecture

The application is structured into clearly defined architectural layers to ensure low coupling, maintainability, and scalability:

[ HTTP Client / Postman ]
│  (JSON / REST)
▼

    Resource Layer  (REST Controllers)  ──► Endpoints & HTTP Responses
    │
    ▼

    Service Layer   (Business Logic)    ──► Business Rules & Exception Handling
    │
    ▼

    Repository Layer (Data Access)      ──► Spring Data JPA Interfaces
    │
    ▼
    [ Database: H2 (Test) / PostgreSQL ]

### 🧩 Domain Entities & Associations
* **User & Order:** One-to-Many (`@OneToMany` / `@ManyToOne`)
* **Order & OrderItem & Product:** Many-to-Many with composite primary key using an intermediate entity (`@Embeddable` / `@EmbeddedId` in `OrderItemPK`)
* **Product & Category:** Many-to-Many relationship (`@ManyToMany` with `@JoinTable`)
* **Order & Payment:** One-to-One relationship sharing the same ID (`@OneToOne` with `@MapsId`)

---

## 🚀 Technologies & Tools

* **Java 25+**
* **Spring Boot 3 / 4**
* **Spring Data JPA / Hibernate (ORM)**
* **H2 Database** (In-memory database for testing and automatic seeding)
* **PostgreSQL** (Production database driver support)
* **Maven** (Dependency management & build tool)
* **Postman** (API testing)

---

## ✨ Key Features

* **Complete CRUD Operations:** Create, Read, Update, and Delete operations for domain entities.
* **Database Seeding:** Automatic test database population on startup using Spring's `CommandLineRunner` (`@Profile("test")`).
* **Global Exception Handling:** Custom HTTP exception interception using `@ControllerAdvice` (`ResourceExceptionHandler`) returning clean and standardized JSON errors:
  * `404 Not Found` for nonexistent resources (`ResourceNotFoundException`).
  * `400 Bad Request` for database referential integrity violations (`DatabaseException`).
* **RESTful HTTP Standards:** Proper usage of HTTP verbs (`GET`, `POST`, `PUT`, `DELETE`) and status codes (`200 OK`, `201 Created`, `204 No Content`).
* **Performance Optimization:** Use of JPA `getReferenceById()` to avoid unnecessary database queries during entity updates.

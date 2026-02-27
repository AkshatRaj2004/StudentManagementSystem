# 📘 Student Management System (CRUD Application)

This project is a simple **Student Management System** built using **Spring Boot MVC**, **Spring Data JPA**, and **MySQL**.  

It allows users to perform basic CRUD operations:

- ➕ Add Student  
- 📄 View All Students  
- ✏ Update Student  
- ❌ Delete Student  

The application follows a proper layered architecture:  
**Controller → Service → Repository → Database**

---

## 🛠 Technologies Used

### Backend
- Java 17
- Spring Boot
- Spring MVC
- Spring Data JPA (Hibernate)

### Frontend
- Thymeleaf Template Engine
- HTML
- CSS
- Bootstrap

### Database
- MySQL

### Build Tool
- Maven

---

## 🏗 Project Structure

```
src/main/java/learn/spring/studentmanagement/
│
├── Controller      → Handles HTTP requests
├── Service         → Business logic
├── repository      → Database operations using JPA
├── Entity          → Student model class
└── StudentManagementSystemApplication.java
```

```
src/main/resources/
└── application.properties   → Database configuration
```

---

## ⚙ How to Run the Project

### 1️⃣ Create Database in MySQL

```sql
CREATE DATABASE studentdb;
```

### 2️⃣ Configure Database Connection

Update `application.properties`:

```
spring.datasource.url=jdbc:mysql://localhost:3306/studentdb
spring.datasource.username=root
spring.datasource.password=yourpassword
spring.jpa.hibernate.ddl-auto=update
```

### 3️⃣ Run the Application

Using Maven:

```
./mvnw spring-boot:run
```

Or run directly from your IDE (IntelliJ / VS Code).

Application will start at:

```
http://localhost:8080
```

---

## 🎯 Learning Outcomes

- Implementation of CRUD operations
- Understanding Spring Boot MVC architecture
- Using Hibernate JPA for database interaction
- Connecting Spring Boot with MySQL
- Handling form data using Thymeleaf

---

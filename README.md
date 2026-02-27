# 🎓 Student Management System (AWS + Docker Deployment)

## 📌 Project Description

This is a simple Student Management System CRUD Application built using:

- Backend: Java + Spring Boot  
- Frontend: ReactJS  
- Database: MySQL  
- Containerization: Docker  
- Cloud: AWS (EC2, RDS, S3)

The application allows users to:

- Add new students  
- View all students  
- Update student details  
- Delete students  

---

## 🏗️ Tech Stack

### Backend
- Java 17
- Spring Boot
- Spring Data JPA
- Maven

### Frontend
- ReactJS
- Axios
- Bootstrap

### Database
- MySQL (AWS RDS)

### DevOps & Cloud
- Docker
- AWS EC2
- AWS RDS
- AWS S3

---

## 📂 Project Structure

```
student-management-system/
│
├── backend/
│   ├── .mvn/
│   ├── src/
│   │   └── main/
│   │       ├── java/com/example/student/
│   │       │   ├── controller/
│   │       │   ├── service/
│   │       │   ├── repository/
│   │       │   └── model/
│   │       └── resources/
│   │           └── application.properties
│   │
│   ├── pom.xml
│   ├── mvnw
│   ├── mvnw.cmd
│   └── Dockerfile
│
├── frontend/
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   │   ├── AddStudent.js
│   │   │   ├── ListStudent.js
│   │   │   └── UpdateStudent.js
│   │   ├── services/
│   │   │   └── StudentService.js
│   │   ├── App.js
│   │   └── index.js
│   │
│   ├── package.json
│   └── Dockerfile
│
├── docker-compose.yml
└── README.md
```

---

## ☁️ AWS Architecture

User → S3 (React Frontend)  
        ↓  
EC2 (Docker Container - Spring Boot Backend)  
        ↓  
RDS (MySQL Database)

### AWS Services Used

1. EC2  
   - Hosts backend Docker container  
   - Runs Spring Boot application  

2. RDS (MySQL)  
   - Managed MySQL database  
   - Stores student records  

3. S3  
   - Hosts React frontend as static website  

---

## 🐳 Docker Setup

### Backend Dockerfile

```dockerfile
FROM openjdk:17
COPY target/student-management.jar app.jar
ENTRYPOINT ["java","-jar","/app.jar"]
```

### Frontend Dockerfile

```dockerfile
FROM node:18 as build
WORKDIR /app
COPY . .
RUN npm install
RUN npm run build

FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
```

---

## ⚙️ application.properties

```
spring.datasource.url=jdbc:mysql://<RDS-ENDPOINT>:3306/studentdb
spring.datasource.username=admin
spring.datasource.password=yourpassword

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
```

---

## ▶️ How to Run Locally

### Backend

```
mvn clean install
mvn spring-boot:run
```

### Frontend

```
npm install
npm start
```

---

## 🚀 Deployment Steps

### Step 1: Create RDS MySQL
- Create database in AWS RDS
- Allow EC2 security group access
- Update RDS endpoint in application.properties

### Step 2: Deploy Backend to EC2
- Launch Ubuntu EC2 instance
- Install Docker
- Build jar file
- Build Docker image

```
docker build -t student-backend .
docker run -p 8080:8080 student-backend
```

### Step 3: Deploy Frontend to S3
- Run:

```
npm run build
```

- Upload build/ folder to S3 bucket
- Enable Static Website Hosting
- Make bucket public

---

## 📌 Features

- Full CRUD Operations
- REST API based backend
- Docker containerized
- AWS Cloud Deployment
- Simple MVC architecture

---

## 🎯 Future Enhancements

- Add JWT Authentication
- Add CI/CD Pipeline (Jenkins)
- Add Load Balancer
- Use Docker Compose for full stack

---

# Thank You

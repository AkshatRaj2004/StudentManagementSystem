🎓 Student Management System (AWS + Docker Deployment)
📌 Project Description

This is a simple Student Management System CRUD Application built using:

Backend: Java + Spring Boot

Frontend: ReactJS

Database: MySQL

Containerization: Docker

Cloud Services Used: AWS EC2, AWS RDS, AWS S3

Using this application, users can:

✅ Add new students

✅ View all students

✅ Update student details

✅ Delete students

🏗️ Tech Stack
Backend

Java 17

Spring Boot

Spring Data JPA

Maven

Frontend

ReactJS

Axios

Bootstrap

Database

MySQL (AWS RDS)

DevOps & Cloud

Docker

AWS EC2

AWS RDS

AWS S3

📂 Project Structure
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
│   │           ├── application.properties
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
│   │   ├── App.js
│   │   ├── index.js
│   │   └── services/StudentService.js
│   │
│   ├── package.json
│   └── Dockerfile
│
├── docker-compose.yml
└── README.md
🚀 Architecture Overview
User → S3 (Frontend - React)
        ↓
      EC2 (Docker Container - Spring Boot Backend)
        ↓
      RDS (MySQL Database)
🔹 AWS Services Used
1️⃣ EC2

Used to deploy backend Docker container

Runs Spring Boot application

2️⃣ RDS (MySQL)

Managed MySQL database

Stores student data securely

3️⃣ S3

Hosts React frontend as static website

Publicly accessible

🐳 Docker Setup
Backend Dockerfile
FROM openjdk:17
COPY target/student-management.jar app.jar
ENTRYPOINT ["java","-jar","/app.jar"]
Frontend Dockerfile
FROM node:18 as build
WORKDIR /app
COPY . .
RUN npm install
RUN npm run build

FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
⚙️ Configuration
application.properties
spring.datasource.url=jdbc:mysql://<RDS-ENDPOINT>:3306/studentdb
spring.datasource.username=admin
spring.datasource.password=yourpassword

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
🧪 How to Run Locally
Backend
mvn clean install
mvn spring-boot:run
Frontend
npm install
npm start
☁️ Deployment Steps (AWS)
Step 1: Deploy Database (RDS)

Create MySQL RDS instance

Allow EC2 security group access

Update RDS endpoint in application.properties

Step 2: Deploy Backend on EC2

Launch EC2 instance (Ubuntu)

Install Docker

Build jar file

Build Docker image

docker build -t student-backend .
docker run -p 8080:8080 student-backend
Step 3: Deploy Frontend on S3

Run:

npm run build

Upload build/ folder to S3 bucket

Enable static website hosting

Make bucket public

📸 Features

REST API based backend

Fully containerized using Docker

Cloud deployment on AWS

Clean MVC architecture

Simple and easy for viva explanation

🎯 Future Improvements

Add Authentication (JWT)

Use CI/CD (Jenkins)

Add Load Balancer

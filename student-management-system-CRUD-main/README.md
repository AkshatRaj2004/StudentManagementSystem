#  Student Management System – Full Stack Cloud Deployment

A production-ready Full Stack Student Management System built with:

- ⚛️ React (Frontend)
- ☕ Spring Boot (Backend)
- 🛢 MySQL (Database)
- 🐳 Docker (Containerization)
- ☁️ AWS Cloud Deployment (S3, CloudFront, Route53, API Gateway, ECS/EKS, RDS)

This project demonstrates end-to-end full stack development and cloud-native deployment architecture.

---

## 🏗 Architecture Overview

Frontend:
React App → S3 → CloudFront → Route53

Backend:
Spring Boot (Dockerized) → ECR → ECS (Fargate) / EKS

Database:
Amazon RDS (MySQL)

API Management:
API Gateway → Load Balancer → ECS Service

---

## 🛠 Technology Stack

### Frontend
- React
- TypeScript
- TailwindCSS
- Vite

### Backend
- Java
- Spring Boot
- JPA / Hibernate

### Database
- MySQL (Local Development)
- Amazon RDS MySQL (Production)

### DevOps & Cloud
- Docker
- AWS S3
- AWS CloudFront
- AWS Route53
- AWS API Gateway
- AWS ECS / EKS
- AWS RDS
- AWS ECR
- Terraform (Optional)
- GitHub Actions (Optional CI/CD)

---

# 📂 Project Structure

```
student-management-system/
│
├── frontend/
│   ├── Dockerfile
│   └── src/
│
├── backend/
│   ├── Dockerfile
│   ├── src/
│   └── application.properties
│
├── docker-compose.yml
├── k8s/
│   ├── deployment.yaml
│   ├── service.yaml
│
└── README.md
```

---

# 🐳 Docker Setup (Local Development)

## Backend Dockerfile

```dockerfile
FROM openjdk:17-jdk-slim
WORKDIR /app
COPY target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java","-jar","app.jar"]
```

## Frontend Dockerfile

```dockerfile
FROM node:18-alpine as build
WORKDIR /app
COPY . .
RUN npm install
RUN npm run build

FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

---

# 🐳 Docker Compose (Local Full Stack)

```yaml
version: '3.8'

services:
  mysql:
    image: mysql:8
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: studentdb
    ports:
      - "3306:3306"

  backend:
    build: ./backend
    ports:
      - "8080:8080"
    depends_on:
      - mysql

  frontend:
    build: ./frontend
    ports:
      - "3000:80"
    depends_on:
      - backend
```

---

# ☁️ AWS Deployment Architecture

## 🔹 Frontend Deployment

1. Build React App
```
npm run build
```

2. Upload `/dist` folder to:
- AWS S3 (Static Website Hosting)

3. Create:
- CloudFront Distribution
- Route53 domain mapping

---

## 🔹 Backend Deployment (ECS Fargate)

1. Build Docker Image
```
docker build -t student-backend .
```

2. Push to AWS ECR

3. Create:
- ECS Cluster
- Task Definition
- ECS Service
- Application Load Balancer

---

## 🔹 Database (Amazon RDS)

- Engine: MySQL
- Multi-AZ (Optional)
- Public access: Disabled
- Security Group: Allow ECS access only

Update `application.properties`:

```
spring.datasource.url=jdbc:mysql://<RDS-ENDPOINT>:3306/studentdb
spring.datasource.username=admin
spring.datasource.password=yourpassword
```

---

## 🔹 API Gateway Setup

- Create HTTP API
- Connect to Application Load Balancer
- Enable CORS
- Deploy stage

---

# ☸ Kubernetes Deployment (Optional – EKS)

## deployment.yaml

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: student-backend
spec:
  replicas: 2
  selector:
    matchLabels:
      app: student-backend
  template:
    metadata:
      labels:
        app: student-backend
    spec:
      containers:
        - name: backend
          image: <ECR_IMAGE_URI>
          ports:
            - containerPort: 8080
```

## service.yaml

```yaml
apiVersion: v1
kind: Service
metadata:
  name: student-backend-service
spec:
  type: LoadBalancer
  selector:
    app: student-backend
  ports:
    - port: 80
      targetPort: 8080
```

---

# 🔐 Environment Variables

Use environment variables instead of hardcoding credentials.

Example:

```
SPRING_DATASOURCE_URL
SPRING_DATASOURCE_USERNAME
SPRING_DATASOURCE_PASSWORD
```

---

# 🚀 CI/CD (Optional)

- GitHub Actions
- Build Docker image
- Push to ECR
- Trigger ECS deployment

---

# 📈 Future Improvements

- JWT Authentication
- Role-based Access Control
- Monitoring (CloudWatch)
- Logging
- Auto Scaling
- Blue-Green Deployment
- Terraform Infrastructure as Code

---

# 🎯 Learning Outcomes

- Full Stack Development
- REST API Design
- Dockerization
- Cloud Architecture
- Container Orchestration
- Production Deployment on AWS

---

# 👨‍💻 Author

Akshat Raj  
B.Tech CSE (AIML)  
Cloud & DevOps Enthusiast  

---

# 📜 License

This project is licensed under the MIT License.

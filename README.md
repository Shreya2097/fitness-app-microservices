# 🏋️ Fitness App – Microservices

A full-stack **Fitness Tracking Application** built using **Spring Boot Microservices, React, Spring Cloud, RabbitMQ, MongoDB, PostgreSQL, Keycloak, and Google Gemini AI**.

The application allows users to manage fitness activities and receive AI-powered analysis and recommendations based on their activities.

---

## 📌 Project Overview

The Fitness App is designed using a **microservices architecture**, where different business responsibilities are separated into independent services.

The application consists of dedicated services for:

* 👤 User Management
* 🏃 Activity Tracking
* 🤖 AI-based Fitness Recommendations
* 🌐 API Gateway
* 🔎 Service Discovery
* ⚙️ Centralized Configuration
* 🔐 Authentication & Authorization

The application also uses **RabbitMQ** for asynchronous communication between the Activity Service and AI Service.

---

## 🎯 Purpose of the Project

The purpose of this project is to develop a scalable and modular fitness application while implementing real-world backend concepts such as:

* Microservices Architecture
* REST APIs
* Service Discovery
* API Gateway
* Centralized Configuration
* OAuth2 / JWT Authentication
* Asynchronous Messaging
* Database Integration
* AI Integration

---

## ❗ Problem Statement

Traditional monolithic applications can become difficult to maintain as the number of features increases because different functionalities are tightly coupled.

This project addresses this challenge by separating major application functionalities into independent microservices. Each service is responsible for a specific business capability and can be developed, maintained, and scaled independently.

---

## 🎯 Objectives

* Develop a fitness tracking application using microservices.
* Implement user registration and profile management.
* Allow users to record and retrieve fitness activities.
* Generate AI-based fitness recommendations.
* Implement secure authentication using Keycloak and OAuth2/JWT.
* Implement service discovery using Eureka.
* Implement centralized configuration using Spring Cloud Config.
* Implement asynchronous communication using RabbitMQ.
* Provide a React-based user interface.
* Use appropriate databases for different service requirements.

---

## ✨ Features & Functionality

### 👤 User Management

* User registration
* User profile retrieval
* User validation
* Email uniqueness validation
* User roles such as `USER` and `ADMIN`

### 🏃 Activity Management

Users can record fitness activities such as:

* Running
* Walking
* Cycling
* Swimming
* Weight Training
* Yoga
* HIIT
* Cardio
* Stretching
* Other activities

Activity information includes:

* Activity type
* Duration
* Calories burned
* Start time
* Additional metrics

Users can also retrieve their previous activities.

### 🤖 AI Fitness Recommendations

After an activity is recorded:

1. The activity is stored in the Activity Service.
2. The Activity Service publishes the activity through RabbitMQ.
3. The AI Service consumes the activity.
4. The AI Service sends the activity information to Google Gemini.
5. Gemini generates fitness analysis and recommendations.
6. The recommendation is stored in MongoDB.
7. The user can retrieve the generated recommendation.

AI recommendations may include:

* Overall activity analysis
* Pace analysis
* Heart-rate analysis
* Calorie analysis
* Improvement suggestions
* Workout suggestions
* Safety guidance

### 🔐 Authentication & Authorization

The application uses **Keycloak** and **OAuth2/JWT** for authentication.

The API Gateway validates authenticated requests before forwarding them to the appropriate microservice.

### 🌐 API Gateway

Spring Cloud Gateway provides a single entry point for backend APIs.

Example routes:

```text
/api/users/**            → User Service
/api/activities/**       → Activity Service
/api/recommendations/**  → AI Service
```

### 🔎 Service Discovery

**Netflix Eureka** is used for service discovery.

Microservices register themselves with Eureka, allowing services to communicate using service names instead of hard-coded service locations.

### ⚙️ Centralized Configuration

**Spring Cloud Config Server** is used to manage configuration centrally for the different microservices.

### 📨 Asynchronous Communication

**RabbitMQ** is used to communicate between the Activity Service and AI Service.

```text
Activity Service
       │
       ▼
   RabbitMQ
       │
       ▼
   AI Service
       │
       ▼
  Gemini API
       │
       ▼
 Recommendation
```

---

## 🏗️ System Architecture

```text
                         ┌─────────────────────┐
                         │       User          │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │   React Frontend   │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │    API Gateway      │
                         │      :8080          │
                         └──────────┬──────────┘
                                    │
              ┌─────────────────────┼─────────────────────┐
              │                     │                     │
              ▼                     ▼                     ▼
     ┌────────────────┐    ┌────────────────┐    ┌────────────────┐
     │  User Service  │    │Activity Service│    │   AI Service   │
     │     :8081      │    │     :8082      │    │     :8083      │
     └───────┬────────┘    └───────┬────────┘    └───────┬────────┘
             │                     │                     │
             ▼                     ▼                     ▼
       PostgreSQL              MongoDB              MongoDB
                                   │
                                   ▼
                              RabbitMQ
                                   │
                                   ▼
                              Gemini API
```

Supporting infrastructure:

```text
                ┌───────────────────┐
                │   Eureka Server   │
                │      :8761        │
                └───────────────────┘

                ┌───────────────────┐
                │   Config Server   │
                │      :8888        │
                └───────────────────┘

                ┌───────────────────┐
                │     Keycloak      │
                │      :8181        │
                └───────────────────┘
```

---

## 🧩 Microservices

| Service              | Responsibility                   | Port |
| -------------------- | -------------------------------- | ---: |
| **User Service**     | User registration and management | 8081 |
| **Activity Service** | Fitness activity management      | 8082 |
| **AI Service**       | AI analysis and recommendations  | 8083 |
| **API Gateway**      | API routing and security         | 8080 |
| **Eureka Server**    | Service discovery                | 8761 |
| **Config Server**    | Centralized configuration        | 8888 |

---

## 🛠️ Technology Stack

### Backend

* Java
* Spring Boot
* Spring Cloud
* Spring Web
* Spring Data JPA
* Spring Data MongoDB
* Spring Security
* Spring Cloud Gateway
* Spring Cloud Config
* Netflix Eureka
* Lombok

### Frontend

* React
* Vite
* React Router
* Redux Toolkit
* Axios
* Material UI

### Databases

* PostgreSQL
* MongoDB

### Messaging

* RabbitMQ

### Authentication

* Keycloak
* OAuth2
* JWT

### AI

* Google Gemini API

### Development Tools

* Git
* GitHub
* Maven
* IntelliJ IDEA / Eclipse / VS Code
* Postman

---

## 🔄 Application Workflow

### User Authentication

```text
User
 │
 ▼
React Frontend
 │
 ▼
Keycloak
 │
 ▼
JWT Token
 │
 ▼
API Gateway
 │
 ▼
Microservices
```

### Activity Tracking

```text
User
 │
 ▼
React Frontend
 │
 ▼
API Gateway
 │
 ▼
Activity Service
 │
 ├── Validate User
 │
 ├── Store Activity
 │
 └── Publish Message
          │
          ▼
       RabbitMQ
          │
          ▼
      AI Service
          │
          ▼
     Gemini API
          │
          ▼
   AI Recommendation
          │
          ▼
       MongoDB
```

---

## 📂 Project Structure

```text
fitness-microservice/
│
├── userservice/
│
├── activityService/
│
├── aiservice/
│
├── gateway/
│
├── eureka/
│
├── configserver/
│
├── fitness-app-frontend/
│
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites

Make sure the following are installed:

* Java 17+
* Maven
* Node.js
* npm
* PostgreSQL
* MongoDB
* RabbitMQ
* Keycloak

---

### 1. Clone the Repository

```bash
git clone https://github.com/Shreya2097/fitness-app-microservices.git
```

```bash
cd fitness-app-microservices
```

---

### 2. Start Infrastructure

Start:

* PostgreSQL
* MongoDB
* RabbitMQ
* Keycloak

Make sure the required environment variables and database credentials are configured.

---

### 3. Start Eureka Server

Navigate to the Eureka project:

```bash
cd eureka
```

Run:

```bash
mvn spring-boot:run
```

Eureka Dashboard:

```text
http://localhost:8761
```

---

### 4. Start Config Server

```bash
cd configserver
mvn spring-boot:run
```

Config Server:

```text
http://localhost:8888
```

---

### 5. Start Microservices

Start the following services:

```text
User Service
Activity Service
AI Service
API Gateway
```

Each service can be started using:

```bash
mvn spring-boot:run
```

---

### 6. Start Frontend

Navigate to:

```bash
cd fitness-app-frontend
```

Install dependencies:

```bash
npm install
```

Start the application:

```bash
npm run dev
```

The frontend will normally be available at:

```text
http://localhost:5173
```

---

## 🔗 API Endpoints

### User Service

| Method | Endpoint                       | Description      |
| ------ | ------------------------------ | ---------------- |
| `POST` | `/api/users/register`          | Register a user  |
| `GET`  | `/api/users/{userId}`          | Get user profile |
| `GET`  | `/api/users/{userId}/validate` | Validate user    |

### Activity Service

| Method | Endpoint                       | Description         |
| ------ | ------------------------------ | ------------------- |
| `POST` | `/api/activities`              | Create activity     |
| `GET`  | `/api/activities`              | Get user activities |
| `GET`  | `/api/activities/{activityId}` | Get activity        |

### AI Service

| Method | Endpoint                                     | Description                 |
| ------ | -------------------------------------------- | --------------------------- |
| `GET`  | `/api/recommendations/user/{userId}`         | Get user recommendations    |
| `GET`  | `/api/recommendations/activity/{activityId}` | Get activity recommendation |

---

## 🔒 Security

The application uses:

* Keycloak for identity management
* OAuth2 / OpenID Connect
* JWT access tokens
* Spring Security OAuth2 Resource Server
* API Gateway security

The API Gateway validates the JWT before forwarding authenticated requests to backend services.

---

## 📊 Database Design

### PostgreSQL

Used by the **User Service** for user information.

```text
users
 ├── id
 ├── email
 ├── password
 ├── firstName
 ├── lastName
 ├── role
 ├── createdAt
 └── updatedAt
```

### MongoDB

Used by:

**Activity Service**

```text
activities
 ├── id
 ├── userId
 ├── type
 ├── duration
 ├── caloriesBurned
 ├── startTime
 ├── additionalMetrics
 ├── createdAt
 └── updatedAt
```

**AI Service**

```text
recommendations
 ├── id
 ├── activityId
 ├── userId
 ├── activityType
 ├── recommendation
 ├── improvements
 ├── suggestions
 ├── safety
 └── createdAt
```

---

## 📈 Project Scope

### Current Scope

* User management
* Authentication
* Fitness activity tracking
* Activity history
* AI-based recommendations
* Microservices architecture
* Service discovery
* Centralized configuration
* API Gateway
* Asynchronous messaging

### Future Scope

* Fitness progress dashboard
* Workout planning
* Fitness goals
* Nutrition tracking
* Notifications
* Admin dashboard
* Advanced analytics
* Mobile application
* CI/CD pipeline
* Cloud deployment

---

## ⚠️ Limitations

* The current project is primarily configured for local development.
* AI recommendations depend on the availability of the Gemini API.
* More comprehensive automated tests can be added.
* Production-grade monitoring and distributed tracing can be added.
* Additional validation and centralized exception handling can improve robustness.
* Production deployment would require secure secret management.

---

## 🔮 Future Enhancements

* Dockerize all services.
* Add Docker Compose for local infrastructure.
* Implement CI/CD using GitHub Actions.
* Add Spring Boot Actuator.
* Add centralized logging.
* Implement distributed tracing.
* Add circuit breakers and resilience patterns.
* Improve AI prompt handling.
* Add fitness progress visualization.
* Add personalized workout plans.
* Add nutrition management.

---

## 👩‍💻 Development Workflow

```text
Requirement Analysis
        ↓
Microservice Design
        ↓
Backend Development
        ↓
Database Integration
        ↓
Service Discovery
        ↓
API Gateway
        ↓
Authentication
        ↓
RabbitMQ Integration
        ↓
AI Integration
        ↓
React Frontend
        ↓
Integration Testing
        ↓
Deployment
```

---

## 📚 Key Concepts Demonstrated

This project demonstrates practical knowledge of:

* Microservices Architecture
* Spring Boot
* Spring Cloud
* REST API Development
* API Gateway
* Service Discovery
* Centralized Configuration
* OAuth2
* JWT
* Keycloak
* PostgreSQL
* MongoDB
* RabbitMQ
* Asynchronous Communication
* React
* AI API Integration
* Distributed Application Design

---

## 🚧 Future Improvements

The project is continuously evolving. Future improvements will focus on:

* Better security
* Improved testing
* Production-ready configuration
* Monitoring and observability
* Performance optimization
* Cloud deployment
* Additional fitness features

---

## 👩‍💻 Author

**Shreya Deshpande**

GitHub:
https://github.com/Shreya2097


# 🍿 Film Info Service Backend

<div align="center">

![PopcornAPI Logo](https://img.icons8.com/color/96/000000/popcorn.png)

**A modern, secure, and scalable Spring Boot backend for movie management**

[![Java](https://img.shields.io/badge/Java-17-orange?style=for-the-badge&logo=java)](https://openjdk.java.net/)
[![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.x-green?style=for-the-badge&logo=spring-boot)](https://spring.io/projects/spring-boot)
[![MySQL](https://img.shields.io/badge/MySQL-8.0-blue?style=for-the-badge&logo=mysql)](https://www.mysql.com/)
[![JWT](https://img.shields.io/badge/JWT-Authentication-red?style=for-the-badge&logo=json-web-tokens)](https://jwt.io/)

[![Build Status](https://img.shields.io/badge/build-passing-brightgreen?style=flat-square)]()
[![License](https://img.shields.io/badge/license-MIT-blue?style=flat-square)](LICENSE)
[![Stars](https://img.shields.io/github/stars/username/PopcornAPI?style=flat-square)]()
[![Forks](https://img.shields.io/github/forks/username/PopcornAPI?style=flat-square)]()

[🚀 Quick Start](#-quick-start) • [📖 Documentation](#-api-documentation) • [🛠️ Installation](#️-installation) • [🤝 Contributing](#-contributing)

</div>

---

## 📋 Table of Contents

- [✨ Features](#-features)
- [🛠️ Tech Stack](#️-tech-stack)
- [🏗️ System Architecture](#️-system-architecture)
- [🚀 Quick Start](#-quick-start)
- [⚙️ Installation](#️-installation)
- [📖 API Documentation](#-api-documentation)
- [🔧 Configuration](#-configuration)
- [📊 Database Schema](#-database-schema)
- [🔐 Authentication](#-authentication)
- [🧪 Testing](#-testing)
- [📈 Performance](#-performance)
- [🐳 Docker Support](#-docker-support)
- [🤝 Contributing](#-contributing)
- [📄 License](#-license)

---

## ✨ Features

<div align="center">

| Feature | Description | Status |
|---------|-------------|--------|
| 🎬 **Movie CRUD** | Complete movie management system | ✅ |
| 📁 **File Upload** | Poster upload & retrieval | ✅ |
| 🔐 **JWT Security** | Secure authentication & authorization | ✅ |
| 📄 **Pagination** | Efficient data pagination | ✅ |
| 🔄 **Sorting** | Multi-field sorting support | ✅ |
| 🏗️ **Clean Architecture** | Three-layered design pattern | ✅ |
| 🛡️ **Role-based Access** | User & Admin role management | ✅ |
| 📊 **Database Integration** | MySQL with JPA/Hibernate | ✅ |

</div>

### 🎯 Core Capabilities

- **🎥 Movie Management**: Full CRUD operations with validation
- **📁 File Handling**: Secure poster upload and retrieval system
- **🔍 Advanced Querying**: Pagination, sorting, and filtering
- **🔐 Security**: JWT-based authentication with role-based access control
- **📊 Data Persistence**: MySQL integration with optimized queries
- **🏗️ Scalable Architecture**: Clean separation of concerns

---

## 🛠️ Tech Stack

<div align="center">

### Backend
![Java](https://img.shields.io/badge/Java-17-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=for-the-badge&logo=spring&logoColor=white)
![Spring Security](https://img.shields.io/badge/Spring_Security-6DB33F?style=for-the-badge&logo=Spring-Security&logoColor=white)
![Spring Data JPA](https://img.shields.io/badge/Spring_Data_JPA-6DB33F?style=for-the-badge&logo=spring&logoColor=white)

### Database & Storage
![MySQL](https://img.shields.io/badge/MySQL-005C84?style=for-the-badge&logo=mysql&logoColor=white)
![Hibernate](https://img.shields.io/badge/Hibernate-59666C?style=for-the-badge&logo=Hibernate&logoColor=white)

### Security & Authentication
![JWT](https://img.shields.io/badge/JWT-black?style=for-the-badge&logo=JSON%20web%20tokens)
![BCrypt](https://img.shields.io/badge/BCrypt-003A70?style=for-the-badge)

### Build Tools
![Maven](https://img.shields.io/badge/Apache%20Maven-C71A36?style=for-the-badge&logo=Apache%20Maven&logoColor=white)

</div>

---

## 🏗️ System Architecture

### High-Level Architecture Diagram

```mermaid
graph TB
    subgraph "Client Layer"
        WebClient[Web Browser]
        MobileClient[Mobile App]
        APIClient[API Consumer]
    end
    
    subgraph "Application Layer"
        subgraph "Spring Boot Application"
            Controller[Controller Layer<br/>REST Endpoints]
            Security[Spring Security<br/>JWT Authentication]
            Service[Service Layer<br/>Business Logic]
            Repository[Repository Layer<br/>Data Access]
        end
        
        FileService[File Service<br/>Poster Management]
        JWTUtil[JWT Utility<br/>Token Management]
    end
    
    subgraph "Data Layer"
        MySQL[(MySQL Database<br/>Port: 3306)]
        FileStorage[File Storage<br/>./uploads]
    end
    
    WebClient -->|HTTP/REST| Controller
    MobileClient -->|HTTP/REST| Controller
    APIClient -->|HTTP/REST| Controller
    
    Controller -->|Validate Token| Security
    Security -->|Check Auth| JWTUtil
    Controller -->|Business Logic| Service
    Service -->|CRUD Operations| Repository
    Repository -.->|SQL Queries| MySQL
    
    Controller -->|Upload/Retrieve| FileService
    FileService -.->|Store/Read| FileStorage
    
    style Controller fill:#4CAF50,color:#fff
    style Security fill:#FF9800,color:#fff
    style Service fill:#2196F3,color:#fff
    style Repository fill:#9C27B0,color:#fff
    style FileService fill:#00BCD4,color:#fff
    style JWTUtil fill:#FF5722,color:#fff
    style MySQL fill:#f0f0f0
    style FileStorage fill:#f0f0f0
```

### Three-Layered Architecture Pattern

```mermaid
graph LR
    subgraph "Presentation Layer"
        MC[Movie Controller]
        AC[Auth Controller]
        FC[File Controller]
    end
    
    subgraph "Business Layer"
        MS[Movie Service]
        AS[Auth Service]
        FS[File Service]
    end
    
    subgraph "Data Layer"
        MR[Movie Repository]
        UR[User Repository]
    end
    
    MC --> MS
    AC --> AS
    FC --> FS
    
    MS --> MR
    AS --> UR
    
    MR -.-> DB[(MySQL)]
    UR -.-> DB
    
    style MC fill:#4CAF50,color:#fff
    style AC fill:#4CAF50,color:#fff
    style FC fill:#4CAF50,color:#fff
    style MS fill:#2196F3,color:#fff
    style AS fill:#2196F3,color:#fff
    style FS fill:#2196F3,color:#fff
    style MR fill:#9C27B0,color:#fff
    style UR fill:#9C27B0,color:#fff
```

### Component Interaction Diagram

```mermaid
graph TB
    subgraph "Security Components"
        JWTFilter[JWT Filter]
        AuthProvider[Auth Provider]
        SecurityConfig[Security Config]
    end
    
    subgraph "Core Components"
        MovieCtrl[Movie Controller]
        AuthCtrl[Auth Controller]
        MovieSvc[Movie Service]
        AuthSvc[Auth Service]
    end
    
    subgraph "Data Components"
        MovieRepo[Movie Repository]
        UserRepo[User Repository]
        JPA[JPA/Hibernate]
    end
    
    JWTFilter -->|Validate| AuthProvider
    SecurityConfig -->|Configure| JWTFilter
    
    MovieCtrl -->|Protected Routes| JWTFilter
    AuthCtrl -->|Login/Register| AuthSvc
    MovieCtrl -->|Business Logic| MovieSvc
    
    AuthSvc -->|User Operations| UserRepo
    MovieSvc -->|Movie Operations| MovieRepo
    
    MovieRepo -->|ORM| JPA
    UserRepo -->|ORM| JPA
    JPA -.->|JDBC| MySQL[(MySQL)]
    
    style JWTFilter fill:#FF9800,color:#fff
    style MovieCtrl fill:#4CAF50,color:#fff
    style AuthCtrl fill:#4CAF50,color:#fff
    style MovieSvc fill:#2196F3,color:#fff
    style AuthSvc fill:#2196F3,color:#fff
    style MovieRepo fill:#9C27B0,color:#fff
    style UserRepo fill:#9C27B0,color:#fff
```

---

## 🔄 Request Flow Diagrams

### Movie Creation Flow (with File Upload)

```mermaid
sequenceDiagram
    autonumber
    participant Client
    participant Controller as Movie Controller
    participant Security as JWT Filter
    participant Service as Movie Service
    participant FileService as File Service
    participant Repository as Movie Repository
    participant DB as MySQL Database
    participant Storage as File Storage
    
    Client->>Controller: POST /api/v1/movie/add-movie<br/>(multipart/form-data + JWT)
    activate Controller
    
    Controller->>Security: Validate JWT Token
    activate Security
    Security->>Security: Extract User Info
    Security-->>Controller: User Authenticated
    deactivate Security
    
    Controller->>FileService: Save Poster File
    activate FileService
    FileService->>Storage: Write File to Disk
    Storage-->>FileService: File Path
    FileService-->>Controller: Poster Filename
    deactivate FileService
    
    Controller->>Service: createMovie(movieDto)
    activate Service
    Service->>Service: Validate Movie Data
    Service->>Repository: save(movie)
    activate Repository
    Repository->>DB: INSERT INTO movies
    DB-->>Repository: Movie Entity
    Repository-->>Service: Saved Movie
    deactivate Repository
    Service-->>Controller: MovieDto
    deactivate Service
    
    Controller-->>Client: 201 Created (MovieDto)
    deactivate Controller
```

### Authentication & Authorization Flow

```mermaid
sequenceDiagram
    autonumber
    participant Client
    participant AuthCtrl as Auth Controller
    participant AuthSvc as Auth Service
    participant UserRepo as User Repository
    participant DB as MySQL
    participant JWTUtil as JWT Utility
    participant BCrypt
    
    rect rgb(240, 248, 255)
        Note over Client,BCrypt: Registration Flow
        Client->>AuthCtrl: POST /auth/register
        activate AuthCtrl
        AuthCtrl->>AuthSvc: register(userDto)
        activate AuthSvc
        AuthSvc->>BCrypt: encodePassword()
        BCrypt-->>AuthSvc: Hashed Password
        AuthSvc->>UserRepo: save(user)
        activate UserRepo
        UserRepo->>DB: INSERT INTO users
        DB-->>UserRepo: User Entity
        UserRepo-->>AuthSvc: Saved User
        deactivate UserRepo
        AuthSvc-->>AuthCtrl: Success Response
        AuthCtrl-->>Client: 201 Created
        deactivate AuthSvc
        deactivate AuthCtrl
    end
    
    rect rgb(255, 250, 240)
        Note over Client,JWTUtil: Login Flow
        Client->>AuthCtrl: POST /auth/login
        activate AuthCtrl
        AuthCtrl->>AuthSvc: login(credentials)
        activate AuthSvc
        AuthSvc->>UserRepo: findByUsername()
        activate UserRepo
        UserRepo->>DB: SELECT FROM users
        DB-->>UserRepo: User Data
        UserRepo-->>AuthSvc: User Entity
        deactivate UserRepo
        AuthSvc->>BCrypt: matches(password)
        BCrypt-->>AuthSvc: Validation Result
        AuthSvc->>JWTUtil: generateToken(user)
        activate JWTUtil
        JWTUtil->>JWTUtil: Create JWT Claims
        JWTUtil->>JWTUtil: Sign Token
        JWTUtil-->>AuthSvc: JWT Token
        deactivate JWTUtil
        AuthSvc-->>AuthCtrl: AuthResponse + Token
        AuthCtrl-->>Client: 200 OK (JWT Token)
        deactivate AuthSvc
        deactivate AuthCtrl
    end
```

### Get All Movies with Pagination Flow

```mermaid
sequenceDiagram
    autonumber
    participant Client
    participant Controller as Movie Controller
    participant Security as JWT Filter
    participant Service as Movie Service
    participant Repository as Movie Repository
    participant DB as MySQL
    
    Client->>Controller: GET /api/v1/movie/allMoviesPage<br/>?pageNumber=0&pageSize=10<br/>(JWT Token)
    activate Controller
    
    Controller->>Security: Validate JWT Token
    activate Security
    Security-->>Controller: Valid
    deactivate Security
    
    Controller->>Service: getAllMoviesPage(pageNumber, pageSize)
    activate Service
    Service->>Service: Create Pageable Object
    Service->>Repository: findAll(pageable)
    activate Repository
    Repository->>DB: SELECT * FROM movies<br/>LIMIT 10 OFFSET 0
    DB-->>Repository: Page<Movie>
    Repository-->>Service: Movie Page
    deactivate Repository
    Service->>Service: Convert to DTOs
    Service-->>Controller: MoviePageResponse
    deactivate Service
    
    Controller-->>Client: 200 OK (Paginated Response)
    deactivate Controller
```

### File Retrieval Flow

```mermaid
sequenceDiagram
    autonumber
    participant Client
    participant FileCtrl as File Controller
    participant FileSvc as File Service
    participant Storage as File Storage
    
    Client->>FileCtrl: GET /file/{filename}
    activate FileCtrl
    
    FileCtrl->>FileSvc: getFile(filename)
    activate FileSvc
    FileSvc->>Storage: Read File
    activate Storage
    Storage-->>FileSvc: File Bytes
    deactivate Storage
    FileSvc->>FileSvc: Determine Content Type
    FileSvc-->>FileCtrl: Resource + ContentType
    deactivate FileSvc
    
    FileCtrl-->>Client: 200 OK (Image File)
    deactivate FileCtrl
```

---

## 📊 Database Schema

### Entity Relationship Diagram

```mermaid
erDiagram
    USERS ||--o{ MOVIES : manages
    USERS {
        bigint id PK
        varchar name
        varchar username UK
        varchar email UK
        varchar password
        varchar role
        timestamp created_at
        timestamp updated_at
    }
    
    MOVIES {
        bigint id PK
        varchar title
        varchar director
        varchar studio
        varchar movie_cast
        integer release_year
        varchar poster
        bigint created_by FK
        timestamp created_at
        timestamp updated_at
    }
```

### Detailed Schema Diagram

```mermaid
graph TB
    subgraph "Users Table"
        U1[id: BIGINT PK AUTO_INCREMENT]
        U2[name: VARCHAR 100]
        U3[username: VARCHAR 50 UNIQUE]
        U4[email: VARCHAR 100 UNIQUE]
        U5[password: VARCHAR 255]
        U6[role: VARCHAR 20]
        U7[created_at: TIMESTAMP]
        U8[updated_at: TIMESTAMP]
    end
    
    subgraph "Movies Table"
        M1[id: BIGINT PK AUTO_INCREMENT]
        M2[title: VARCHAR 255 NOT NULL]
        M3[director: VARCHAR 100 NOT NULL]
        M4[studio: VARCHAR 100]
        M5[movie_cast: TEXT]
        M6[release_year: INT]
        M7[poster: VARCHAR 255]
        M8[created_by: BIGINT FK]
        M9[created_at: TIMESTAMP]
        M10[updated_at: TIMESTAMP]
    end
    
    U1 -.->|Foreign Key| M8
    
    style U1 fill:#9C27B0,color:#fff
    style M1 fill:#2196F3,color:#fff
    style M8 fill:#FF9800,color:#fff
```

### Data Flow in Repository Layer

```mermaid
graph LR
    subgraph "Application Layer"
        Service[Service Layer]
    end
    
    subgraph "Data Access Layer"
        Repo[JPA Repository]
        EntityMgr[Entity Manager]
    end
    
    subgraph "ORM Layer"
        Hibernate[Hibernate ORM]
        Cache[Second Level Cache]
    end
    
    subgraph "Database"
        MySQL[(MySQL Database)]
    end
    
    Service -->|CRUD Operations| Repo
    Repo -->|JPA API| EntityMgr
    EntityMgr -->|Persistence Context| Hibernate
    Hibernate -->|Check Cache| Cache
    Cache -.->|Cache Miss| MySQL
    Hibernate -->|JDBC| MySQL
    
    style Service fill:#2196F3,color:#fff
    style Repo fill:#9C27B0,color:#fff
    style Hibernate fill:#00BCD4,color:#fff
    style Cache fill:#FFC107
```

---

## 🔐 Authentication Architecture

### JWT Security Architecture

```mermaid
graph TB
    subgraph "Security Layer"
        Filter[JWT Authentication Filter]
        Provider[Authentication Provider]
        UserDetails[UserDetails Service]
    end
    
    subgraph "JWT Components"
        JWTUtil[JWT Utility]
        TokenStore[Token Store]
    end
    
    subgraph "Security Config"
        WebSecurity[Web Security Config]
        CORS[CORS Configuration]
        CSRF[CSRF Protection]
    end
    
    Request[HTTP Request] -->|1. Intercept| Filter
    Filter -->|2. Extract Token| JWTUtil
    JWTUtil -->|3. Validate| TokenStore
    Filter -->|4. Load User| UserDetails
    UserDetails -->|5. Authenticate| Provider
    Provider -->|6. Set Security Context| Filter
    Filter -->|7. Continue| Controller[Protected Controller]
    
    WebSecurity -->|Configure| Filter
    WebSecurity -->|Enable| CORS
    WebSecurity -->|Disable| CSRF
    
    style Filter fill:#FF9800,color:#fff
    style JWTUtil fill:#FF5722,color:#fff
    style Provider fill:#9C27B0,color:#fff
    style Controller fill:#4CAF50,color:#fff
```

### Token Generation & Validation Flow

```mermaid
graph TB
    subgraph "Token Generation"
        A[User Credentials] -->|Login| B[Authenticate]
        B -->|Success| C[Create Claims]
        C -->|Add User Info| D[Set Expiration]
        D -->|Sign with Secret| E[JWT Token]
    end
    
    subgraph "Token Validation"
        F[Incoming Request] -->|Extract Token| G[Parse JWT]
        G -->|Verify Signature| H{Valid?}
        H -->|Yes| I[Check Expiration]
        H -->|No| J[Reject Request]
        I -->|Not Expired| K[Extract User]
        I -->|Expired| J
        K -->|Load from DB| L[Authenticate User]
    end
    
    E -.->|Store in Client| F
    
    style E fill:#4CAF50,color:#fff
    style K fill:#2196F3,color:#fff
    style J fill:#f44336,color:#fff
```

### Role-Based Access Control

```mermaid
graph TB
    subgraph "User Roles"
        Admin[ADMIN Role]
        User[USER Role]
        Guest[GUEST Role]
    end
    
    subgraph "Endpoints"
        subgraph "Public"
            Login[POST /auth/login]
            Register[POST /auth/register]
        end
        
        subgraph "User Protected"
            GetMovies[GET /movie/all]
            GetMovie[GET /movie/:id]
            GetPoster[GET /file/:filename]
        end
        
        subgraph "Admin Protected"
            AddMovie[POST /movie/add-movie]
            UpdateMovie[PUT /movie/update/:id]
            DeleteMovie[DELETE /movie/delete/:id]
        end
    end
    
    Admin -->|Full Access| AddMovie
    Admin -->|Full Access| UpdateMovie
    Admin -->|Full Access| DeleteMovie
    Admin -->|Access| GetMovies
    
    User -->|Read Access| GetMovies
    User -->|Read Access| GetMovie
    User -->|Access| GetPoster
    
    Guest -->|No Auth| Login
    Guest -->|No Auth| Register
    
    style Admin fill:#9C27B0,color:#fff
    style User fill:#2196F3,color:#fff
    style Guest fill:#607D8B,color:#fff
    style AddMovie fill:#f44336,color:#fff
    style UpdateMovie fill:#FF9800,color:#fff
    style DeleteMovie fill:#f44336,color:#fff
```

---

## 📁 Project Structure

```mermaid
graph TB
    Root[PopcornAPI Root]
    
    Root --> SrcMain[src/main]
    Root --> SrcTest[src/test]
    Root --> POM[pom.xml]
    Root --> README[README.md]
    
    SrcMain --> Java[java/com/popcornapi]
    SrcMain --> Resources[resources]
    
    Java --> Controller[controller/]
    Java --> Service[service/]
    Java --> Repository[repository/]
    Java --> Entity[entity/]
    Java --> Config[config/]
    Java --> DTO[dto/]
    Java --> Exception[exception/]
    Java --> Security[security/]
    
    Controller --> MovieCtrl[MovieController.java]
    Controller --> AuthCtrl[AuthController.java]
    Controller --> FileCtrl[FileController.java]
    
    Service --> MovieSvc[MovieService.java]
    Service --> AuthSvc[AuthService.java]
    Service --> FileSvc[FileService.java]
    
    Repository --> MovieRepo[MovieRepository.java]
    Repository --> UserRepo[UserRepository.java]
    
    Entity --> Movie[Movie.java]
    Entity --> User[User.java]
    
    Config --> SecConfig[SecurityConfig.java]
    Config --> JWTConfig[JwtConfig.java]
    Config --> WebConfig[WebConfig.java]
    
    Resources --> AppProps[application.properties]
    Resources --> DataSQL[data.sql]
    
    style Root fill:#FFC107
    style Controller fill:#4CAF50,color:#fff
    style Service fill:#2196F3,color:#fff
    style Repository fill:#9C27B0,color:#fff
    style Config fill:#FF9800,color:#fff
```

---

## 🚀 Quick Start

### Prerequisites

- ☕ **Java 17** or higher
- 🐬 **MySQL 8.0** or higher
- 🔧 **Maven 3.6** or higher

### Installation Workflow

```mermaid
graph LR
    A[Clone Repository] --> B[Setup Database]
    B --> C[Configure Properties]
    C --> D[Build Project]
    D --> E[Run Application]
    E --> F[Verify API]
    
    style A fill:#4CAF50,color:#fff
    style E fill:#2196F3,color:#fff
    style F fill:#FF9800,color:#fff
```

### 1️⃣ Clone & Navigate

```bash
git clone https://github.com/Prahlad-7/PopcornAPI.git
cd PopcornAPI
```

### 2️⃣ Database Setup

Create a MySQL database:

```sql
CREATE DATABASE popcorn_db;
CREATE USER 'popcorn_user'@'localhost' IDENTIFIED BY 'your_password';
GRANT ALL PRIVILEGES ON popcorn_db.* TO 'popcorn_user'@'localhost';
FLUSH PRIVILEGES;
```

### 3️⃣ Configure Application

Update `src/main/resources/application.properties`:

```properties
# Database Configuration
spring.datasource.url=jdbc:mysql://localhost:3306/popcorn_db
spring.datasource.username=popcorn_user
spring.datasource.password=your_password

# JPA Configuration
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL8Dialect

# JWT Configuration
jwt.secret=your-secret-key-must-be-at-least-256-bits
jwt.expiration=86400000

# File Upload Configuration
spring.servlet.multipart.max-file-size=10MB
spring.servlet.multipart.max-request-size=10MB
file.upload-dir=./uploads
```

### 4️⃣ Build & Run

```bash
# Clean and build
./mvnw clean install

# Run the application
./mvnw spring-boot:run
```

### 5️⃣ Access the API

- **Base URL**: `http://localhost:8080`
- **Health Check**: `GET /actuator/health`
- **API Documentation**: `http://localhost:8080/swagger-ui.html`

---

## 📖 API Documentation

### API Endpoint Map

```mermaid
graph TB
    API[PopcornAPI Base URL<br/>http://localhost:8080]
    
    API --> Auth[/api/v1/auth]
    API --> Movie[/api/v1/movie]
    API --> File[/file]
    
    Auth --> Register[POST /register]
    Auth --> Login[POST /login]
    
    Movie --> AddMovie[POST /add-movie 🔒]
    Movie --> GetAll[GET /all 🔒]
    Movie --> GetById[GET /:id 🔒]
    Movie --> Update[PUT /update/:id 🔒]
    Movie --> Delete[DELETE /delete/:id 🔒]
    Movie --> Paginated[GET /allMoviesPage 🔒]
    Movie --> Sorted[GET /allMoviesPageSort 🔒]
    
    File --> GetPoster[GET /:filename]
    
    style API fill:#FFC107
    style Auth fill:#9C27B0,color:#fff
    style Movie fill:#4CAF50,color:#fff
    style File fill:#2196F3,color:#fff
    style Register fill:#00BCD4,color:#fff
    style Login fill:#00BCD4,color:#fff
```

### 🎬 Movie Endpoints

<details>
<summary>Click to expand Movie API details</summary>

#### Create Movie
```http
POST /api/v1/movie/add-movie
Content-Type: multipart/form-data
Authorization: Bearer {token}

{
    "title": "The Matrix",
    "director": "The Wachowskis",
    "studio": "Warner Bros",
    "movieCast": "Keanu Reeves, Laurence Fishburne",
    "releaseYear": 1999,
    "poster": file
}
```

**Response:**
```json
{
    "id": 1,
    "title": "The Matrix",
    "director": "The Wachowskis",
    "studio": "Warner Bros",
    "movieCast": "Keanu Reeves, Laurence Fishburne",
    "releaseYear": 1999,
    "poster": "matrix-poster.jpg",
    "posterUrl": "http://localhost:8080/file/matrix-poster.jpg"
}
```

#### Get All Movies
```http
GET /api/v1/movie/all
Authorization: Bearer {token}
```

#### Get Movie by ID
```http
GET /api/v1/movie/{id}
Authorization: Bearer {token}
```

#### Update Movie
```http
PUT /api/v1/movie/update/{id}
Content-Type: multipart/form-data
Authorization: Bearer {token}

{
    "title": "The Matrix Reloaded",
    "director": "The Wachowskis",
    "studio": "Warner Bros",
    "movieCast": "Keanu Reeves, Laurence Fishburne",
    "releaseYear": 2003,
    "poster": file
}
```

#### Delete Movie
```http
DELETE /api/v1/movie/delete/{id}
Authorization: Bearer {token}
```

#### Paginated Movies
```http
GET /api/v1/movie/allMoviesPage?pageNumber=0&pageSize=10
Authorization: Bearer {token}
```

**Response:**
```json
{
    "content": [...],
    "pageNumber": 0,
    "pageSize": 10,
    "totalElements": 50,
    "totalPages": 5,
    "last": false
}
```

#### Sorted Movies
```http
GET /api/v1/movie/allMoviesPageSort?sortBy=title&pageNumber=0&pageSize=10
Authorization: Bearer {token}
```

</details>

### 🔐 Authentication Endpoints

<details>
<summary>Click to expand Auth API details</summary>

#### Register User
```http
POST /api/v1/auth/register
Content-Type: application/json

{
    "name": "John Doe",
    "username": "johndoe",
    "email": "john@example.com",
    "password": "securePassword123"
}
```

**Response:**
```json
{
    "message": "User registered successfully",
    "userId": 1,
    "username": "johndoe"
}
```

#### Login User
```http
POST /api/v1/auth/login
Content-Type: application/json

{
    "username": "johndoe",
    "password": "securePassword123"
}
```

**Response:**
```json
{
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "type": "Bearer",
    "username": "johndoe",
    "email": "john@example.com",
    "role": "USER",
    "expiresIn": 86400000
}
```

</details>

### 📁 File Endpoints

<details>
<summary>Click to expand File API details</summary>

#### Get Poster
```http
GET /file/{filename}
```

**Response:** Image file (JPEG, PNG, etc.)



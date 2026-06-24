🏢 Enterprise Order System

A production-style Spring Boot Order Management System demonstrating enterprise backend development concepts such as layered architecture, transactional processing, idempotency, inventory validation, payment processing, and database persistence.
-------------------------------------------------------------
🚀 Features
User Management
Order Management
Inventory Management
Payment Processing
Idempotent Order Creation
Transaction Management
REST APIs
MySQL Database Integration
Spring Data JPA
Exception Handling
Swagger/OpenAPI Documentation
Enterprise Layered Architecture
------------------------------------------------------
🏗️ Architecture
Client
   │
   ▼
REST Controllers
   │
   ▼
Service Layer
   │
   ▼
Repository Layer
   │
   ▼
MySQL Database
------------------------------------------------------
Project Structure
src/main/java
│
├── controller
│   ├── UserController
│   ├── OrderController
│   ├── InventoryController
│   └── PaymentController
│
├── service
│   ├── UserService
│   ├── OrderService
│   ├── InventoryService
│   └── PaymentService
│
├── repository
│   ├── UserRepository
│   ├── OrderRepository
│   ├── InventoryRepository
│   └── PaymentRepository
│
├── entity
│   ├── User
│   ├── Order
│   ├── Inventory
│   └── Payment
│
└── dto
Future Enhancements
JWT Authentication
Role Based Authorization
Kafka Event Streaming
Email Notifications
Redis Caching
--------------------------------------------------
Modules
Enterprise Order System
│
├── Users
├── Orders
├── Inventory
└── Payments
-----------------------------------------------
🛠️ Tech Stack
Technology	Version
Java	17+
Spring Boot	3.x
Spring Data JPA	Latest
MySQL	8.x
Maven	3.9+
Lombok	Latest
Swagger/OpenAPI	Latest
---------------------------------------------
Database Schema
Users Table
CREATE TABLE users (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(255),
    email VARCHAR(255)
);
Sample Data
id	username	email
4	nikhil	nikhil@enterprise.com
5	sai	sai@enterprise.com
6	yashwanth	yashwanth@enterprise.com
7	keerthi	keerthi@enterprise.com
-------------------------------------------------------------
Inventory Table
CREATE TABLE inventory (
    product_id BIGINT PRIMARY KEY,
    product_name VARCHAR(255),
    stock INT
);
Sample Data
product_id	product_name	stock
104	Enterprise Desktop	80
105	Mobile	100
106	Notebook	50
107	Speakers	150
----------------------------------------------------------------
Orders Table
CREATE TABLE orders (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    created_at TIMESTAMP,
    idempotency_key VARCHAR(255),
    product_id BIGINT,
    quantity INT,
    status VARCHAR(50),
    status_reason VARCHAR(500),
    total DECIMAL(10,2),
    user_id BIGINT
);
Sample Data
id	status	total
1	CONFIRMED	500.00
2	CONFIRMED	1000.00
3	FAILED	1500.00
-----------------------------------------------------------
Payments Table
CREATE TABLE payments (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    amount DECIMAL(10,2),
    created_at TIMESTAMP,
    order_id BIGINT,
    status VARCHAR(50)
);
Sample Data
id	amount	status
1	500.00	COMPLETED
2	1000.00	COMPLETED
-----------------------------------------------------------
API Endpoints
User APIs
Get All Users
GET /users

Response

[
  {
    "id": 4,
    "username": "nikhil",
    "email": "nikhil@enterprise.com"
  }
]
Create User
POST /users

Request

{
  "username": "john",
  "email": "john@example.com"
}
---------------------------------------------
Inventory APIs
Get Inventory
GET /inventory/{productId}

Example

GET /inventory/104
Order APIs
Create Order
POST /orders

Headers

Content-Type: application/json
X-Idempotency-Key: ORDER-001

Request

{
  "userId": 4,
  "productId": 104,
  "quantity": 2,
  "total": 500.00
}

Success Response

{
  "id": 1,
  "status": "CONFIRMED",
  "statusReason": "Order completed successfully"
}
Get Order By Id
GET /orders/{id}

Example

GET /orders/1
Payment APIs
Get Payment By Order Id
GET /payments/order/{orderId}

Example

GET /payments/order/1
Order Processing Flow
Create Order Request
          │
          ▼
Validate User
          │
          ▼
Check Inventory
          │
          ▼
Reserve Stock
          │
          ▼
Create Payment
          │
          ▼
Confirm Order
          │
          ▼
Return Response
Idempotency Support

Duplicate order submissions are prevented using:

X-Idempotency-Key

Example

X-Idempotency-Key: ORDER-001

If the same key is submitted multiple times, the system returns the previously processed order instead of creating duplicates.
----------------------------------------------------------------------

Swagger Documentation

After starting the application:

http://localhost:8080/swagger-ui/index.html

OpenAPI Docs:

http://localhost:8080/v3/api-docs
Running the Application
Clone Repository
git clone https://github.com/your-username/enterprise-order-system.git
Configure MySQL
spring.datasource.url=jdbc:mysql://localhost:3306/enterprise_order_system
spring.datasource.username=root
spring.datasource.password=root
Build Project
mvn clean install
Run Application
mvn spring-boot:run

Application starts on:

http://localhost:8080

# 🛍️ E-Commerce Backend API

A comprehensive backend system for e-commerce applications built with the MERN stack, featuring secure authentication, product management, cart functionality, and order processing.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Tech Stack](#tech-stack)
- [System Design](#system-design)
- [API Documentation](#api-documentation)
- [Database Schema](#database-schema)
- [Security Features](#security-features)
- [Getting Started](#getting-started)

---

## 🔍 Overview

This project implements a scalable e-commerce backend using microservices architecture. Each service handles specific business logic, ensuring modularity, maintainability, and ease of testing [web:1][web:3].

### Design Approach

- **HLD (High-Level Design)**: Overall system architecture and component interactions
- **LLD (Low-Level Design)**: Detailed implementation of individual services and data models

---

## 🛠️ Tech Stack

| Technology | Purpose |
|------------|---------|
| **Node.js** | Runtime environment for server-side JavaScript |
| **Express.js** | Web framework for routing and middleware [web:2] |
| **MongoDB** | NoSQL database for flexible data storage |
| **Mongoose** | ODM for MongoDB with schema validation [web:4] |
| **JWT** | Stateless authentication and authorization [web:7] |
| **bcrypt** | Password hashing and encryption [web:4] |
| **dotenv** | Environment variable management |
| **nodemon** | Development server with auto-restart |

---

## 🏗️ System Design

### Core Components

┌─────────────────┐
│ Express Server │
│ - Routing │
│ - Middleware │
│ - Security │
└────────┬────────┘
│
├──► Authentication Layer (JWT + bcrypt)
├──► Rate Limiting
├──► Data Validation (Mongoose)
└──► MongoDB Database

text

### Microservices Architecture

The application is divided into the following microservices:

1. **User Authentication Service**
2. **Product Management Service**
3. **Cart Service**
4. **Order Processing Service**

---

## 📡 API Documentation

### 🔐 User Authentication

| Endpoint | Method | Description | Auth Required |
|----------|--------|-------------|---------------|
| `/signup` | POST | Register new user | ❌ |
| `/login` | POST | User login (returns JWT) | ❌ |
| `/logout` | POST | User logout | ✅ |
| `/updatePassword` | PUT | Update user password | ✅ |
| `/profile/:id` | GET | Get user profile | ✅ |

### 📦 Products

| Endpoint | Method | Description | Auth Required | Role |
|----------|--------|-------------|---------------|------|
| `/createproduct` | POST | Create new product | ✅ | Admin |
| `/product` | GET | Fetch all products | ❌ | - |
| `/product/:id` | GET | Fetch single product | ❌ | - |
| `/updateProduct/:id` | PUT | Update product | ✅ | Admin |
| `/deleteProduct/:id` | DELETE | Delete product | ✅ | Admin |
| `/searchProduct` | GET | Search products | ❌ | - |

### 🛒 Cart Service

| Endpoint | Method | Description | Auth Required |
|----------|--------|-------------|---------------|
| `/cart/add` | POST | Add item to cart | ✅ |
| `/cart` | GET | Fetch user cart | ✅ |
| `/cart/remove/:id` | DELETE | Remove item from cart | ✅ |

### 📋 Orders

| Endpoint | Method | Description | Auth Required |
|----------|--------|-------------|---------------|
| `/order/place` | POST | Place new order | ✅ |
| `/order/cancel/:id` | PUT | Cancel order | ✅ |
| `/order/track/:id` | GET | Track order status | ✅ |

---

## 🗄️ Database Schema

### User Schema

{
_id: ObjectId,
name: String,
age: Number,
email: String (unique, required),
address: String,
contact: Number,
role: String (enum: ["user", "admin"]),
password: String (hashed with bcrypt),
createdAt: Date
}

text

### Product Schema

{
_id: ObjectId,
name: String (required),
description: String,
costPrice: Number,
salePrice: Number,
category: String,
stock: Number,
image: [String], // CDN links from frontend
createdAt: Date (default: Date.now)
}

text

### Cart Schema

{
_id: ObjectId,
userId: ObjectId (ref: 'User'),
products: [{
productId: ObjectId (ref: 'Product'),
price: Number,
quantity: Number
}],
totalAmount: Number
}

text

### Order Schema

{
_id: ObjectId,
userId: ObjectId (ref: 'User'),
items: [{
productId: ObjectId (ref: 'Product'),
quantity: Number,
price: Number
}],
totalAmount: Number,
shippingAddress: String,
status: String (enum: ["pending", "processing", "shipped", "delivered", "cancelled"]),
createdAt: Date
}

text

---

## 🔒 Security Features

### Mandatory Security Implementations

1. **JWT Authentication**
   - Token-based stateless authentication [web:7]
   - Secure token generation and verification
   - Token expiration handling

2. **Password Encryption**
   - bcrypt hashing with salt rounds [web:4]
   - Secure password storage
   - No plain-text password storage

3. **Rate Limiting**
   - Prevent brute-force attacks
   - API request throttling
   - DDoS protection

### Additional Security Measures

- **CORS Configuration**: Cross-origin resource sharing controls
- **Input Validation**: Mongoose schema validation
- **Environment Variables**: Sensitive data protection with dotenv
- **Role-Based Access Control (RBAC)**: Admin vs. user permissions

---

## 📝 Development Notes

- Follow RESTful API conventions
- Use async/await for asynchronous operations
- Implement proper error handling middleware
- Write comprehensive API documentation
- Test endpoints using Postman or Thunder Client

---

## 📄 License

This project is licensed under the MIT License.

---

## 👨‍💻 Author

Built with 💙 by Vishoo

---

**Happy Coding! 🚀**

# E-Commerce API

A full-featured e-commerce REST API built with Node.js and Express, featuring user authentication, product management, shopping cart functionality, and administrative tools.

## Project Description

This is a comprehensive e-commerce backend application that provides a complete API for managing an online store. The system supports user registration and authentication, product browsing with advanced filtering and pagination, shopping cart management, and administrative features for product and user management. The application includes JWT-based authentication, role-based access control, email notifications, and API documentation through Swagger.

## Technology Stack

### Core Technologies
- **Runtime**: Node.js
- **Framework**: Express.js
- **Database**: MongoDB with Mongoose ODM
- **Authentication**: JSON Web Tokens (JWT), Passport.js
- **Template Engine**: Handlebars (Express-Handlebars)

### Key Dependencies
- **bcrypt**: Password hashing and encryption
- **jsonwebtoken**: JWT token generation and verification
- **passport**: Authentication middleware with multiple strategies (Local, GitHub, JWT)
- **mongoose-paginate-v2**: Advanced pagination for MongoDB queries
- **winston**: Logging system
- **nodemailer**: Email notifications
- **swagger-jsdoc & swagger-ui-express**: API documentation
- **socket.io**: Real-time communication capabilities
- **express-session**: Session management
- **connect-mongo**: MongoDB session store
- **cookie-parser**: Cookie handling
- **multer**: File upload handling

## Architecture and Design Patterns

### MVC Pattern (Model-View-Controller)
The application follows the MVC architectural pattern:
- **Models** (`src/models/`): Define data schemas using Mongoose (User, Product, Cart)
- **Controllers** (`src/controllers/`): Handle business logic and request processing
- **Views** (`src/views/`): Handlebars templates for rendering HTML
- **Routes** (`src/routes/`): Define API endpoints and route handlers

### Repository Pattern
Mongoose models abstract data access, providing a clean separation between the data layer and business logic.

### Middleware Pattern
Authentication, logging, and error handling are implemented as Express middleware, promoting code reusability and separation of concerns.

### Authentication Strategy
- JWT-based stateless authentication
- Cookie-based token storage
- Role-based access control (Admin/User roles)
- Multiple authentication strategies via Passport.js

## API Overview

### Main API Endpoints

#### Authentication
- `POST /login` - User login with email and password
- `POST /register` - New user registration
- `GET /logout` - User logout

#### Products
- `GET /products` - Get products with pagination and filtering
  - Query parameters: `limit`, `page`, `filter`, `ord`
- Admin-only product management endpoints

#### Shopping Cart
- `POST /cart` - Add products to cart
- `GET /cart` - View cart contents
- `DELETE /cart/:productId` - Remove product from cart

#### Admin
- User management endpoints
- Product CRUD operations
- Restricted to users with admin role

### API Documentation
The API includes interactive Swagger documentation available at `/apidocs` when the server is running.

## Installation Guide

### Prerequisites
- Node.js (v14 or higher recommended)
- MongoDB instance (local or cloud-based like MongoDB Atlas)
- npm or yarn package manager

### Step-by-Step Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd ecommerce
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables**
   
   Create a `.env` file in the root directory with the following variables:
   ```env
   MONGO_URI=mongodb://localhost:27017/ecommerce
   PRIVATE_KEY=your_jwt_secret_key
   ```

   Replace the values with your actual MongoDB connection string and a secure secret key for JWT.

4. **Start the application**
   ```bash
   npm start
   ```

   The server will start on port 8000 by default.

5. **Access the application**
   - Main application: `http://localhost:8000`
   - API documentation: `http://localhost:8000/apidocs`

## Usage

### Default Admin Access
The application includes a default admin account:
- Email: `admin@admin.com`
- Password: `1234`

### User Registration
New users can register through the `/register` endpoint and will be assigned the "User" role by default.

### Authentication Flow
1. Users log in via `/login` endpoint
2. Upon successful authentication, a JWT token is generated and stored in an HTTP-only cookie
3. The token is valid for 12 hours
4. Protected routes verify the token on each request
5. Users are redirected based on their role (admin to `/admin/users`, regular users to `/products`)

## Project Structure

```
ecommerce/
├── src/
│   ├── controllers/     # Business logic handlers
│   ├── models/          # Mongoose data models
│   ├── routes/          # API route definitions
│   ├── views/           # Handlebars templates
│   ├── utils/           # Utility functions (JWT, logger, mailer)
│   ├── docs/            # Swagger API documentation
│   └── index.js         # Application entry point
├── package.json         # Project dependencies
└── README.md           # Project documentation
```

## Features

- User authentication and authorization
- Role-based access control (Admin/User)
- Product catalog with pagination and filtering
- Shopping cart functionality
- Stock management
- Email notifications
- Logging system with Winston
- API documentation with Swagger
- Session management with MongoDB store
- Secure password hashing with bcrypt
- JWT token-based authentication

## Security Considerations

- Passwords are hashed using bcrypt before storage
- JWT tokens are stored in HTTP-only cookies
- Role-based access control for sensitive operations
- Environment variables for sensitive configuration
- Input validation on API endpoints

# AirBnB Clone Project

## 🚀 Objective
The backend for the Airbnb Clone project is designed to provide a robust and scalable foundation for managing user interactions, property listings, bookings, and payments. This backend will support various functionalities required to mimic the core features of Airbnb, ensuring a smooth experience for users and hosts.
## 🏆 Project Goals
1. **User Management:** Implement a secure system for user registration, authentication, and profile management.
2. **Property Management:** Develop features for property listing, creation, updates, and retrieval.
3. **Booking System:** Create a booking mechanism for users to reserve properties and manage booking details.
4. **Payment Processing:** Integrate a payment system to handle transactions between users and hosts, and record payment details.
5. **Review System:** Allow users to leave reviews and ratings for properties.
6. **Data Optimization:** Ensure efficient data retrieval and storage through database optimizations.
## 👥 Team Roles
- **Backend Developer**: Implements the core of the app, API endpoints, database schema, and business logic.
- **Database Administrator**: Manage database design, indexing, and optimizations.
- **DevOps Enginner**: Handle deployment, monitoring, and scaling of backend services.
- **QA Engineer**: Ensures the backend functionalities are thoroughly tested and meets quality standards.
## ⚙️ Technology Stack
- **Django**: A high-level Python framework used for building RESTful APIs.
- **Django REST Framework**: Provides tools for creating and managing RESTful APIs.
- **PostgreSQL**: A powerful relational database used for data storage.
- **GraphQL**: Allows for flexible and efficient querying of data.
- **Celery**: For handling asynchronous tasks such as sending notifications or processing payments.
- **Redis**: Used for caching and session management.
- **Docker**: Containerization tool for consistent development and deployment environments.
- **CI/CD Pipelines**: Automated pipelines for testing and deploying code changes.
## 🧱 Database Design
### Users
- **user_id**: Primary Key, UUID, Indexed
- **first_name**: VARCHAR, NOT NULL
- **last_name**: VARCHAR, NOT NULL
- **email**: VARCHAR, UNIQUE, NOT NULL, Indexed
- **password_hash**: VARCHAR, NOT NULL
- **phone_number**: VARCHAR, NULL
- **role**: ENUM (`guest`, `host`, `admin`), NOT NULL
- **created_at**: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP
### Properties
- **property_id**: Primary Key, UUID, Indexed
- **host_id**: Foreign Key, references `Users[user_id]`
- **name**: VARCHAR, NOT NULL
- **description**: TEXT, NOT NULL
- **location**: VARCHAR, NOT NULL
- **pricepernight**: DECIMAL, NOT NULL
- **created_at**: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP
- **updated_at**: TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP
### Bookings
- **booking_id**: Primary Key, UUID, Indexed
- **property_id**: Foreign Key, references `Properties[property_id]` Indexed
- **user_id**: Foreign Key, references `Users[user_id]`
- **start_date**: DATE, NOT NULL
- **end_date**: DATE, NOT NULL
- **total_price**: DECIMAL, NOT NULL
- **status**: ENUM (`pending`, `confirmed`, `canceled`), NOT NULL
- **created_at**: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP
### Payments
- **payment_id**: Primary Key, UUID, Indexed
- **booking_id**: Foreign Key, references `Bookings[booking_id]`
- **amount**: DECIMAL, NOT NULL
- **payment_date**: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP
- **payment_method**: ENUM (`credit_card`, `paypal`, `stripe`), NOT NULL
### Reviews
- **review_id**: Primary Key, UUID, Indexed
- **property_id**: Foreign Key, references `Properties[property_id]` Indexed
- **user_id**: Foreign Key, references `Users[user_id]`
- **rating**: INTEGER, CHECK: `rating >= 1 AND rating <= 5`, NOT NULL
- **comment**: TEXT, NOT NULL
- **created_at**: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP
### Messages
- **message_id**: Primary Key, UUID, Indexed
- **sender_id**: Foreign Key, references `Users[user_id]`
- **recipient_id**: Foreign Key, references `Users[user_id]`
- **message_body**: TEXT, NOT NULL
- **sent_at**: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP

## 🛠️ Feature Breakdown
### 1. User Management
- **Endpoints**: `/users/`, `/users/{user_id}/`
- **Features**: Register new users, authenticate, and manage user profiles.
### 2. Property Management
- **Endpoints**: `/properties/`, `/properties/{property_id}/`
- **Features**: Create, update, retrieve, and delete property listings.
### 3. Booking System
- **Endpoints**: `/bookings/`, `/bookings/{booking_id}/`
- **Features**: Make, update, and manage bookings, including check-in and check-out details.
### 4. Payment Processing
- **Endpoints**: `/payments/`
- **Features**: Handle payments transactions related to bookings.
### 5. Review System
- **Endpoints**: `/reviews/`, `/reviews/{review_id}/`
- **Features**: Post and manage reviews for properties.
### 6. Database Optimizations
- **Indexing**: Implement indexes for fast retrieval of frequently accessed data.
- **Caching**: Use caching strategies to reduce database load and improve performance.
### 7. API Documentation
- **OpenAPI Standard**: The backend APIs are documented using the OpenAPI standard to ensure clarity and ease of integration.
- **Django REST Framework**: Provides a comprehensive RESTful API for handling CRUD operations on user and property data.
- **GraphQL**: Offers a flexible and efficient query mechanism for interacting with the backend.
## 🔒 API Security
- **Authentication**: Validating every request to protect user data.
- **Authorization**: Securing payments.
- **Rate limiting**: Restricting the number request that can be made in a certain time frame to reduce load and protect from malicious attacks.
## 🔁 CI/CD Pipeline
(Continuous Integration / Continuous Delivery)
Automating the continuous development, testing, and deployment of code changes, integrating features, and applying bug fixes.
### Tools
- **Docker**: Provide app containerization, combining app and it's dependencies in a single system.
- **GitHub Actions**: Automate deployment process.

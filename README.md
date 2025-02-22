# YumZoom API

The YumZoom API is a Spring Boot-based backend service that facilitates food ordering, user management, and order tracking. This API also handles user authentication and authorization.

## Features

### User Management:
- User authentication and registration.
- Role-based access control (e.g., CUSTOMER, ADMIN, DELIVERY_PERSON roles).

### Restaurant & Menu Management:
- Add, update, retrieve, and manage restaurant details.
- Manage menu items including name, price, description, and availability.

### Order & Cart Management:
- Add items to the cart and update quantities.
- Place and track orders in real-time.
- Manage order status updates via WebSockets.

### Secure Endpoints:
- Endpoints are secured using JSON Web Tokens (JWT) for authentication.

## Prerequisites

Ensure you have the following installed:

- Java 21
- Maven for dependency management.
- Docker for containerization and streamlined deployment.
- Vannila for UI.

## Getting Started

### 1. Clone the Repository
```sh
git clone https://github.com/YumZoom/yumzoom-api.git
cd yumzoom-api
```

### 2. Configure the Application
Update the `src/main/resources/application.yml` file with your database configuration:
```yaml
spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/yumzoom_db
    username: your_database_user
    password: your_database_password
  jpa:
    hibernate:
      ddl-auto: update
  client:
  end-point: your_front_end_url

stripe:
  secretKey: your_stripe_secretKey
  primaryKey: your_primary_key
  webhookSecret: your_secret_webhook
```

### 3. Run the Backend Service
Using Maven:
```sh
mvn clean install
mvn spring-boot:run
```
The backend will be available at `http://localhost:8080`.


### 4. Run the Frontend (Optional)
If you are using the `yumzoom-ui` (Vannila js):
```sh
cd yumzoom-ui
open with live server
```
Access the frontend at `(http://127.0.0.1:5501/)`.

## API Documentation

API endpoints are documented using Swagger. Once the application is running, you can access the API documentation at:

`http://localhost:8080/swagger-ui/index.html`

## Project Structure
```plaintext
yumzoom-api/
├── src/
│   ├── main/
│   │   ├── java/com/yumzoom/
│   │   │   ├── address/     
│   │   │   ├── agent/        
│   │   │   ├── agentOrders/  
│   │   │   ├── cart/         
│   │   │   ├── cartItem/     
│   │   │   ├── configration/ 
│   │   │   ├── customer/     
│   │   │   ├── menu/         
│   │   │   ├── order/        
│   │   │   ├── orderItem/    
│   │   │   ├── payment/     
│   │   │   ├── restaurant/  
│   │   │   ├── restaurantOrder/ 
│   │   │   ├── security/        
│   │   │   ├── user/       
│   │   │   ├── util/       
│   │   │   ├── websocket/  
│   │   │   ├── YumZoomAppliction/  
│   │   └── resources/
│   │       ├── application.yml  # Application properties
│   │       ├── banner.txt       # Custom banner
├── pom.xml               # Maven configuration
└── Dockerfile            # Dockerfile for backend
```

## Key Endpoints

### Authentication
| Method | Endpoint       | Description |
|--------|----------------|-------------|
| POST   | `/signup`  | Log in a user and get a JWT. |
| POST   | `/signin`  | Register a new user. |

### Restaurants
| Method | Endpoint         | Description |
|--------|------------------|-------------|
| GET    | `/get/eatinghouse`        | Get a list of restaurants. |
| POST   | `/signin`                 | Add a new restaurant. based on user selection |
| GET    | `/restaurant/information` | Get restaurant details. using token |

### Menu Items
| Method | Endpoint            | Description |
|--------|---------------------|-------------|
| GET    | `/restaurant/getAllFood`            | Get a list of food items. |
| POST   | `/restaurant/addFoodItem`           | Add a new food item. |
| DELETE | `/restaurant/removeFoodItem`        | Delete a food item. |

### Cart
| Method | Endpoint         | Description |
|--------|------------------|-------------|
| GET    | `/customer/getCartList`          | Get cart details. |
| POST   | `/customer/addtocart`            | Add item to cart. |
| POST   | `/customer/updatecart/{itemId}`  | Update cart based on quantity; if value reaches 0, remove item, otherwise, update quantity. |

### Orders
| Method | Endpoint          | Description |
|--------|-------------------|-------------|
| POST   | `/customer/placeOrder`         | Place an order. |
| GET    | `/customer/orderlist`          | Get order details. |
| WebSocket | `/order/update `            | Order updates are handled via WebSocket responses.

## Common Errors

### 1. Service Not Initialized in the Default Constructor
Ensure all services are properly annotated with `@RequiredArgsConstructor` or autowired.

### 2. Database Connection Errors
Check your `application.yml` for the correct database URL, username, and password.

## Contact
For queries or support, contact the YumZoom team at `guna.asin06@gmail.com`. 🎉


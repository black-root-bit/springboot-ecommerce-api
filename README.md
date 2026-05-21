# 🛒 springboot-ecommerce-api

> **Production-grade e-commerce REST API built with Spring Boot, PostgreSQL, Redis and Docker.**
> Clean architecture · Scalable · Fully documented · CI/CD ready

[![Java](https://img.shields.io/badge/Java-17-ED8B00?style=flat-square&logo=openjdk)](https://openjdk.org/)
[![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.2-6DB33F?style=flat-square&logo=springboot)](https://spring.io/projects/spring-boot)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-316192?style=flat-square&logo=postgresql)](https://postgresql.org)
[![Docker](https://img.shields.io/badge/Docker-Ready-2496ED?style=flat-square&logo=docker)](https://docker.com)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)
[![Swagger](https://img.shields.io/badge/Swagger-Documented-85EA2D?style=flat-square&logo=swagger)](http://localhost:8080/swagger-ui.html)

---

## 🚀 Features

- ✅ **Product catalog** — categories, search, filters, pagination
- ✅ **Cart & Checkout** — session-based cart with Redis
- ✅ **Order management** — order lifecycle, status tracking
- ✅ **JWT Authentication** — secure login, refresh tokens
- ✅ **Role-based access** — ADMIN / CUSTOMER / SELLER roles
- ✅ **Payment integration** — Stripe webhook handling
- ✅ **Image upload** — AWS S3 integration
- ✅ **Email notifications** — order confirmations via SMTP
- ✅ **Rate limiting** — IP-based throttling
- ✅ **Swagger UI** — fully documented API at `/swagger-ui.html`
- ✅ **Docker Compose** — one command startup
- ✅ **GitHub Actions CI** — automated test & build pipeline

---

## 🗂️ Project Structure

```
springboot-ecommerce-api/
├── src/
│   ├── main/
│   │   ├── java/com/blackrootbit/ecommerce/
│   │   │   ├── EcommerceApplication.java
│   │   │   ├── config/
│   │   │   │   ├── SecurityConfig.java
│   │   │   │   ├── SwaggerConfig.java
│   │   │   │   ├── RedisConfig.java
│   │   │   │   └── CorsConfig.java
│   │   │   ├── controller/
│   │   │   │   ├── AuthController.java
│   │   │   │   ├── ProductController.java
│   │   │   │   ├── CartController.java
│   │   │   │   ├── OrderController.java
│   │   │   │   ├── UserController.java
│   │   │   │   └── PaymentController.java
│   │   │   ├── service/
│   │   │   │   ├── AuthService.java
│   │   │   │   ├── ProductService.java
│   │   │   │   ├── CartService.java
│   │   │   │   ├── OrderService.java
│   │   │   │   ├── PaymentService.java
│   │   │   │   └── EmailService.java
│   │   │   ├── repository/
│   │   │   │   ├── UserRepository.java
│   │   │   │   ├── ProductRepository.java
│   │   │   │   ├── OrderRepository.java
│   │   │   │   └── CategoryRepository.java
│   │   │   ├── model/
│   │   │   │   ├── User.java
│   │   │   │   ├── Product.java
│   │   │   │   ├── Order.java
│   │   │   │   ├── OrderItem.java
│   │   │   │   ├── Cart.java
│   │   │   │   └── Category.java
│   │   │   ├── dto/
│   │   │   │   ├── request/
│   │   │   │   └── response/
│   │   │   ├── security/
│   │   │   │   ├── JwtTokenProvider.java
│   │   │   │   ├── JwtAuthFilter.java
│   │   │   │   └── UserDetailsServiceImpl.java
│   │   │   ├── exception/
│   │   │   │   ├── GlobalExceptionHandler.java
│   │   │   │   ├── ResourceNotFoundException.java
│   │   │   │   └── BusinessException.java
│   │   │   └── util/
│   │   │       ├── PageUtil.java
│   │   │       └── SlugUtil.java
│   │   └── resources/
│   │       ├── application.yml
│   │       ├── application-dev.yml
│   │       ├── application-prod.yml
│   │       └── db/migration/
│   │           ├── V1__create_users.sql
│   │           ├── V2__create_products.sql
│   │           └── V3__create_orders.sql
│   └── test/
│       └── java/com/blackrootbit/ecommerce/
│           ├── controller/
│           └── service/
├── docker/
│   ├── Dockerfile
│   └── docker-compose.yml
├── .github/
│   └── workflows/
│       └── ci.yml
├── postman/
│   └── ecommerce-api.postman_collection.json
├── pom.xml
└── README.md
```

---

## 🔌 API Endpoints

### Auth
| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/v1/auth/register` | Register new user |
| `POST` | `/api/v1/auth/login` | Login & get JWT |
| `POST` | `/api/v1/auth/refresh` | Refresh access token |
| `POST` | `/api/v1/auth/logout` | Invalidate token |

### Products
| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/v1/products` | List products (paginated) |
| `GET` | `/api/v1/products/{id}` | Get product by ID |
| `GET` | `/api/v1/products/search?q=` | Search products |
| `POST` | `/api/v1/products` | Create product `[ADMIN]` |
| `PUT` | `/api/v1/products/{id}` | Update product `[ADMIN]` |
| `DELETE` | `/api/v1/products/{id}` | Delete product `[ADMIN]` |

### Orders
| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/v1/orders` | Place order |
| `GET` | `/api/v1/orders/{id}` | Get order details |
| `GET` | `/api/v1/orders/my-orders` | Get user's orders |
| `PUT` | `/api/v1/orders/{id}/status` | Update status `[ADMIN]` |
| `POST` | `/api/v1/orders/{id}/cancel` | Cancel order |

### Cart
| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/v1/cart` | Get current cart |
| `POST` | `/api/v1/cart/items` | Add item to cart |
| `PUT` | `/api/v1/cart/items/{id}` | Update quantity |
| `DELETE` | `/api/v1/cart/items/{id}` | Remove item |
| `DELETE` | `/api/v1/cart/clear` | Clear cart |

---

## 🗄️ Database Schema

```sql
-- Users
CREATE TABLE users (
    id          BIGSERIAL PRIMARY KEY,
    email       VARCHAR(255) UNIQUE NOT NULL,
    password    VARCHAR(255) NOT NULL,
    full_name   VARCHAR(255),
    role        VARCHAR(50) DEFAULT 'CUSTOMER',
    is_active   BOOLEAN DEFAULT TRUE,
    created_at  TIMESTAMP DEFAULT NOW(),
    updated_at  TIMESTAMP DEFAULT NOW()
);

-- Products
CREATE TABLE products (
    id           BIGSERIAL PRIMARY KEY,
    name         VARCHAR(255) NOT NULL,
    slug         VARCHAR(255) UNIQUE NOT NULL,
    description  TEXT,
    price        DECIMAL(10,2) NOT NULL,
    stock        INTEGER DEFAULT 0,
    category_id  BIGINT REFERENCES categories(id),
    image_url    VARCHAR(500),
    is_active    BOOLEAN DEFAULT TRUE,
    created_at   TIMESTAMP DEFAULT NOW()
);

-- Orders
CREATE TABLE orders (
    id              BIGSERIAL PRIMARY KEY,
    user_id         BIGINT REFERENCES users(id),
    total_amount    DECIMAL(10,2) NOT NULL,
    status          VARCHAR(50) DEFAULT 'PENDING',
    payment_status  VARCHAR(50) DEFAULT 'UNPAID',
    shipping_address TEXT,
    created_at      TIMESTAMP DEFAULT NOW()
);

-- Order Items
CREATE TABLE order_items (
    id          BIGSERIAL PRIMARY KEY,
    order_id    BIGINT REFERENCES orders(id),
    product_id  BIGINT REFERENCES products(id),
    quantity    INTEGER NOT NULL,
    unit_price  DECIMAL(10,2) NOT NULL
);
```

---

## 🐳 Docker Setup

```bash
# Clone the repository
git clone https://github.com/black-root-bit/springboot-ecommerce-api.git
cd springboot-ecommerce-api

# Start all services (API + PostgreSQL + Redis)
docker compose up -d

# API will be available at:
# http://localhost:8080
# http://localhost:8080/swagger-ui.html
```

**docker-compose.yml**
```yaml
version: '3.8'
services:
  app:
    build: .
    ports:
      - "8080:8080"
    environment:
      - SPRING_DATASOURCE_URL=jdbc:postgresql://db:5432/ecommerce
      - SPRING_DATASOURCE_USERNAME=postgres
      - SPRING_DATASOURCE_PASSWORD=secret
      - SPRING_REDIS_HOST=redis
      - JWT_SECRET=${JWT_SECRET}
    depends_on:
      - db
      - redis

  db:
    image: postgres:15-alpine
    environment:
      POSTGRES_DB: ecommerce
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: secret
    volumes:
      - pgdata:/var/lib/postgresql/data
    ports:
      - "5432:5432"

  redis:
    image: redis:7-alpine
    ports:
      - "6379:6379"

volumes:
  pgdata:
```

---

## ⚙️ CI/CD — GitHub Actions

```yaml
# .github/workflows/ci.yml
name: CI Pipeline

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  build-and-test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Set up JDK 17
        uses: actions/setup-java@v4
        with:
          java-version: '17'
          distribution: 'temurin'
      - name: Build with Maven
        run: mvn clean package -DskipTests
      - name: Run tests
        run: mvn test
      - name: Build Docker image
        run: docker build -t springboot-ecommerce-api .
```

---

## 🔐 JWT Authentication Flow

```
Client                     API Server                    Database
  │                            │                              │
  ├─── POST /auth/login ──────►│                              │
  │    {email, password}       ├─── Validate credentials ───►│
  │                            │◄── User record ─────────────┤
  │◄── {accessToken,           │                              │
  │     refreshToken} ─────────┤                              │
  │                            │                              │
  ├─── GET /products ─────────►│                              │
  │    Authorization: Bearer   ├─── Validate JWT ────────────┤
  │    <accessToken>           │◄── Valid / Expired ──────────┤
  │◄── 200 Products ───────────┤                              │
```

---

## 🏷️ GitHub Topics

`java` `spring-boot` `rest-api` `ecommerce` `postgresql` `redis` `docker` `jwt` `microservices` `maven` `swagger` `aws`

---

## 📄 License

MIT © [black-root-bit](https://github.com/black-root-bit)

# Monex

Proyecto de título Monex con arquitectura de microservicios backend en Spring Boot y frontend en React + Vite.

## Estado del proyecto

El repositorio contiene los siguientes módulos:

- `Monex/users-service`: autenticación, usuarios, recuperación de contraseña y configuración de tarjeta de crédito.
- `Monex/categories-service`: CRUD de categorías con seguridad basada en JWT.
- `Monex/expenses-service`: CRUD de gastos con filtros, cuotas y estimación mensual.
- `Monex/frontend`: aplicación web en React + Vite.

## Tecnologías principales

- Java 21
- Spring Boot 4.0.5 (`users-service`, `categories-service`)
- Spring Boot 3.4.4 (`expenses-service`)
- Spring Web MVC / Spring Web
- Spring Data JPA
- PostgreSQL
- Bean Validation
- JWT (`jjwt` 0.12.3)
- Swagger/OpenAPI (`springdoc-openapi`)
- Lombok
- Maven
- React 19
- Vite 7

## Estructura del repositorio

```text
Monex/
  docker-compose.yml
  users-service/
  categories-service/
  expenses-service/
  frontend/
```

---

## URLs de producción

- `users-service`: https://users-service-y9rl.onrender.com
- `categories-service`: https://categories-service-75op.onrender.com
- `expenses-service`: https://expenses-service-x5hz.onrender.com
- `frontend`: https://monex-frontend-pi.vercel.app/

> Local solo si Render/Vercel no están disponibles.

---

## users-service

### Descripción

Microservicio de autenticación y gestión de usuarios con:

- registro y login
- login con Google
- recuperación de contraseña por correo
- perfiles de usuario
- cambio de contraseña
- configuración de tarjeta de crédito

### Configuración

- Producción en Render: `https://users-service-y9rl.onrender.com`
- Swagger: `https://users-service-y9rl.onrender.com/swagger-ui/index.html#/`
- Local (fallback solo si Render no está disponible): `http://localhost:8081`

### Endpoints clave

Base URL de producción: `https://users-service-y9rl.onrender.com`

Autenticación:

- `POST /api/auth/register`
- `POST /api/auth/login`
- `POST /api/auth/google`
- `GET /api/auth/me`
- `POST /api/auth/recuperar/enviar-codigo`
- `POST /api/auth/recuperar/verificar-codigo`
- `POST /api/auth/recuperar/cambiar-contrasena`

Usuarios:

- `GET /api/users/{id}`
- `GET /api/users/me`
- `PUT /api/users/{id}`
- `DELETE /api/users/{id}`
- `POST /api/users/cambiar-password`

Tarjeta de crédito:

- `GET /api/tarjeta/configuracion`
- `POST /api/tarjeta/configuracion`

---

## categories-service

### Descripción

Microservicio de categorías con control de acceso por JWT y gestión de recursos por usuario.

### Configuración

- Producción en Render: `https://categories-service-75op.onrender.com`
- Base de datos: `categorias`
- Swagger: `https://categories-service-75op.onrender.com/swagger-ui/index.html#/`
- Local (fallback solo si Render no está disponible): `http://localhost:8082`

### Endpoints clave

Base URL de producción: `https://categories-service-75op.onrender.com`

- `GET /api/categorias`
- `GET /api/categorias/paginadas`
- `GET /api/categorias/{id}`
- `POST /api/categorias`
- `PUT /api/categorias/{id}`
- `DELETE /api/categorias/{id}`

---

## expenses-service

### Descripción

Microservicio de gastos con filtros, cuotas, paginación y estimación mensual.

### Configuración

- Producción en Render: `https://expenses-service-x5hz.onrender.com`
- Base de datos: `gastos`
- Swagger: `https://expenses-service-x5hz.onrender.com/swagger-ui/index.html#/`
- Local (fallback solo si Render no está disponible): `http://localhost:8083`

### Endpoints clave

Base URL de producción: `https://expenses-service-x5hz.onrender.com`

- `GET /api/expenses`
- `GET /api/expenses/paginadas`
- `GET /api/expenses/{id}`
- `POST /api/expenses`
- `PUT /api/expenses/{id}`
- `DELETE /api/expenses/{id}`
- `GET /api/expenses/payment-method/{paymentMethod}`
- `GET /api/expenses/category/{categoryId}`
- `GET /api/expenses/date-range?startDate=YYYY-MM-DD&endDate=YYYY-MM-DD`
- `GET /api/expenses/monthly-estimate`

### Métodos de pago válidos

- `EFECTIVO`
- `DEBITO`
- `CREDITO`

---

## frontend

### Descripción

Aplicación web construida con React y Vite.

### Producción

- Frontend desplegado en Vercel: `https://monex-frontend-pi.vercel.app/`
- Local (fallback solo si Vercel no está disponible): `http://localhost:5173`

### Comandos

```bash
cd Monex/frontend
npm install
npm run dev
```

---

## Docker Compose

El archivo `Monex/docker-compose.yml` levanta los siguientes servicios:

- `postgres-users` → puerto `5433`
- `users-service` → puerto `8081`
- `postgres-categories` → puerto `5434`
- `categories-service` → puerto `8082`
- `postgres-expenses` → puerto `5435`
- `expenses-service` → puerto `8083`

---

## Prerrequisitos

- Java 21
- Maven 3.9+
- Node.js 18+ / npm 10+
- PostgreSQL 12+

---

## Ejecución local

### Opción 1: Con Docker Compose

```bash
cd Monex
docker compose up --build
```

### Opción 2: Sin Docker

#### Backend usuarios

```powershell
cd Monex/users-service
.\mvnw.cmd spring-boot:run
```

#### Backend categorías

```powershell
cd Monex/categories-service
.\mvnw.cmd spring-boot:run
```

#### Backend gastos

```powershell
cd Monex/expenses-service
.\mvnw.cmd spring-boot:run
```

#### Frontend

```bash
cd Monex/frontend
npm install
npm run dev
```

---

## Variables de entorno importantes

### users-service

- `PORT` (default `8081`)
- `SPRING_DATASOURCE_URL`
- `SPRING_DATASOURCE_USERNAME`
- `SPRING_DATASOURCE_PASSWORD`
- `JWT_SECRET`
- `JWT_EXPIRATION` (default `86400000`)
- `GOOGLE_CLIENT_ID`
- `RESEND_API_KEY`
- `RESEND_FROM_EMAIL`

### categories-service

- `PORT` (default `8082`)
- `SPRING_DATASOURCE_URL` (default `jdbc:postgresql://localhost:5432/categorias`)
- `SPRING_DATASOURCE_USERNAME` (default `postgres`)
- `SPRING_DATASOURCE_PASSWORD` (default `1234`)
- `JWT_SECRET` (default `clave-super-secreta-para-testeo-1234567890`)

### expenses-service

- `PORT` (default `8083`)
- `SPRING_DATASOURCE_URL`
- `SPRING_DATASOURCE_USERNAME`
- `SPRING_DATASOURCE_PASSWORD`
- `JWT_SECRET`
- `JWT_EXPIRATION` (default `86400000`)

---

## Flujo recomendado

1. Registrar usuario en `users-service`.
2. Iniciar sesión y obtener JWT.
3. Usar `Authorization: Bearer <token>` para consultar categorías y gastos.
4. Crear categorías en `categories-service`.
5. Crear y consultar gastos en `expenses-service`.
6. Consultar estimación mensual con `GET /api/expenses/monthly-estimate`.

---

## Notas

- El JWT secret debe ser el mismo en todos los servicios para validar correctamente los tokens.
- `categories-service` y `expenses-service` requieren token JWT en `Authorization: Bearer <token>`.
- Cada backend expone documentación OpenAPI en `/swagger-ui.html`.
- `users-service` soporta recuperación de contraseña y login con Google.

- **Estimación mensual**: El endpoint `/api/expenses/monthly-estimate` calcula el total de cuotas activas para el mes actual en pagos con crédito.

## Flujo de uso recomendado

### 1. Registro e inicio de sesión
```
POST /api/auth/register → Registrar nuevo usuario
POST /api/auth/login → Obtener JWT
```

### 2. Configurar tarjeta de crédito (Solo en caso de tener tarjeta de credito)
```
POST /api/tarjeta/configuracion → Guardar configuración de tarjeta
GET /api/tarjeta/configuracion → Ver configuración guardada
```

### 3. Gestionar gastos
```
POST /api/expenses → Crear gasto
GET /api/expenses → Listar todos los gastos
GET /api/expenses?paymentMethod=CREDITO&startDate=2026-05-01&endDate=2026-05-31 → Filtrar gastos
GET /api/expenses/monthly-estimate → Ver estimación de pago mensual
```

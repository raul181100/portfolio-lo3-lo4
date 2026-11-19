---
type: reference
updated: 2026-11-13
source: SpringBoot/HouseMate — controller/
---
# HouseMate API — Endpoints

> [!info] Server
> | | Address | Where |
> | --- | --- | --- |
> | 🌐 API Spring Boot (curl / Postman) | `http://localhost:8080` | My Mac (local) |
> | 📱 Android emulator → API | `http://10.0.2.2:8080/` | My Mac (local) |
> | 🗄️ PostgreSQL (used by Spring, not an endpoint) | `192.168.158.10:5432` | Fontys Netlab (VPN on) |
>
> Run once in the terminal, then copy any curl:
> ```bash
> export API=http://localhost:8080
> ```

> [!warning] Later: API on a server
> Spring Boot runs locally for now. It will be deployed on a server later — then only `API` (and the Android `BASE_URL`) change; the curls stay the same.

## Overview

| | Endpoint | What it does | OK | Errors | Android |
| --- | --- | --- | --- | --- | --- |
| 🔵 | `POST /users` | Register | `201` | `400` `409` | ✅ `UserApi` |
| 🔵 | `POST /users/login` | Log in | `200` | `400` `401` | ✅ `UserApi` |
| 🟢 | `GET /users/{userId}/house` | Get my house | `200` | `404` | ✅ `HouseApi` |
| 🔵 | `POST /users/{userId}/house` | Create house | `201` | `400` `404` `409` | ✅ `HouseApi` |
| 🔵 | `POST /users/{userId}/house/join` | Join by code | `201` | `400` `404` `409` | ✅ `HouseApi` |
| 🟢 | `GET /users/{userId}/expenses` | Get expenses | `200` | `404` | ✅ `ExpenseApi` |
| 🔵 | `POST /users/{userId}/expenses` | Add expense | `201` | `400` `404` | ❌ not used yet |

> [!note]- Error format
> `401`, `404` and `409` return the message as **plain text**. Validation errors (`400`) return Spring's default JSON.
> Body format: JSON · header `Content-Type: application/json`

## 👤 Users — `UserController`

> [!post]- POST /users — Register
> Creates a user. The password is stored as a BCrypt hash; the email is saved trimmed and in lowercase.
>
> **Request**
> ```json
> { "username": "raul", "email": "raul@example.com", "password": "secret123" }
> ```
> | Field | Rules |
> | --- | --- |
> | `username` | required · 3–50 chars |
> | `email` | required · valid email · max 255 |
> | `password` | required · 8–72 chars |
>
> **Response `201`**
> ```json
> { "id": 1, "username": "raul", "email": "raul@example.com" }
> ```
>
> **Errors:** `400` invalid data · `409` "A user with the email … already exists"
>
> ```bash
> curl -X POST $API/users \
>   -H "Content-Type: application/json" \
>   -d '{"username":"raul","email":"raul@example.com","password":"secret123"}'
> ```

> [!post]- POST /users/login — Log in
> Checks email + password. It doesn't say which one was wrong (security).
>
> **Request**
> ```json
> { "email": "raul@example.com", "password": "secret123" }
> ```
> | Field | Rules |
> | --- | --- |
> | `email` | required · valid email · max 255 |
> | `password` | required · max 72 |
>
> **Response `200`**
> ```json
> { "id": 1, "username": "raul", "email": "raul@example.com" }
> ```
>
> **Errors:** `400` invalid data · `401` "Incorrect email or password"
>
> ```bash
> curl -X POST $API/users/login \
>   -H "Content-Type: application/json" \
>   -d '{"email":"raul@example.com","password":"secret123"}'
> ```

## 🏠 House — `HouseController`

> [!get]- GET /users/{userId}/house — Get my house
> Returns the house the user belongs to (as creator or as member).
>
> **Response `200`**
> ```json
> {
>   "id": 1,
>   "userId": 1,
>   "address": "Rachelsmolen 1",
>   "postalCode": "5612 MA",
>   "housingCode": "H-001",
>   "joinCode": "K7M3QX"
> }
> ```
> `userId` is the **creator** of the house.
>
> **Errors:** `404` the user has no house (empty body)
>
> ```bash
> curl $API/users/1/house
> ```

> [!post]- POST /users/{userId}/house — Create house
> Creates the house and makes the user its first member. A random 6-character `joinCode` is generated (no 0/O/1/I/L to avoid confusion).
>
> **Request**
> ```json
> { "address": "Rachelsmolen 1", "postalCode": "5612 MA", "housingCode": "H-001" }
> ```
> | Field | Rules |
> | --- | --- |
> | `address` | required · max 255 |
> | `postalCode` | required · max 20 |
> | `housingCode` | required · max 50 |
>
> **Response `201`:** same JSON as `GET /users/{userId}/house`
>
> **Errors:** `400` invalid data · `404` "No user exists with id …" · `409` "User … already has a house assigned"
>
> ```bash
> curl -X POST $API/users/1/house \
>   -H "Content-Type: application/json" \
>   -d '{"address":"Rachelsmolen 1","postalCode":"5612 MA","housingCode":"H-001"}'
> ```

> [!post]- POST /users/{userId}/house/join — Join by code
> Adds the user as a member of the house with that code. The code is not case-sensitive.
>
> **Request**
> ```json
> { "joinCode": "K7M3QX" }
> ```
> | Field | Rules |
> | --- | --- |
> | `joinCode` | required · max 6 |
>
> **Response `201`:** the JSON of the joined house
>
> **Errors:** `400` invalid data · `404` "No user exists with id …" or "The joinCode is not correct" · `409` "User … already has a house assigned"
>
> ```bash
> curl -X POST $API/users/2/house/join \
>   -H "Content-Type: application/json" \
>   -d '{"joinCode":"K7M3QX"}'
> ```

## 💶 Expenses — `ExpenseController`

> [!get]- GET /users/{userId}/expenses — Get expenses
> Returns all expenses of the user's house and what each member pays (amount ÷ members, rounded to 2 decimals).
>
> **Response `200`**
> ```json
> {
>   "houseId": 1,
>   "memberCount": 4,
>   "totalAmount": 120.00,
>   "expenses": [
>     { "id": 1, "name": "Electricity", "amount": 80.00, "sharePerPerson": 20.00 },
>     { "id": 2, "name": "Internet", "amount": 40.00, "sharePerPerson": 10.00 }
>   ]
> }
> ```
>
> **Errors:** `404` "User … does not belong to any house"
>
> ```bash
> curl $API/users/1/expenses
> ```

> [!post]- POST /users/{userId}/expenses — Add expense
> Adds an expense to the user's house. The amount is rounded to 2 decimals.
>
> **Request**
> ```json
> { "name": "Electricity", "amount": 80.00 }
> ```
> | Field | Rules |
> | --- | --- |
> | `name` | required · max 100 |
> | `amount` | required · min 0.01 · max 10 digits + 2 decimals |
>
> **Response `201`**
> ```json
> { "id": 1, "name": "Electricity", "amount": 80.00, "sharePerPerson": 20.00 }
> ```
>
> **Errors:** `400` invalid data · `404` "User … does not belong to any house"
>
> ⚠️ Not called from the Android app yet (`ExpenseApi` only has the GET) → task "Add expenses" in [[Sprint 3]].
>
> ```bash
> curl -X POST $API/users/1/expenses \
>   -H "Content-Type: application/json" \
>   -d '{"name":"Electricity","amount":80.00}'
> ```

> [!todo]- Planned in [[Sprint 3]]
> - Role (tenant / landlord) in `POST /users` and in the login response → [[Role type]]
> - Only landlords can `POST /users/{userId}/house`
> - IoT endpoints → [[IoT devices]]

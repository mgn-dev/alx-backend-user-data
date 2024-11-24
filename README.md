# ALX Backend User Data

Security-focused backend tasks covering personal data protection, HTTP Basic Authentication, session-based authentication, and a Flask user authentication service with SQLAlchemy.

## Overview

This project includes four tasks that address how backend systems handle sensitive user information and authenticate requests. Learners implement log redaction for PII fields, password hashing with bcrypt, Flask API protection with Basic and session auth, and a complete user authentication service with registration, login, session management, and route guards.

Each module extends a shared API skeleton (`models/`, `api/v1/`) with progressively stronger authentication mechanisms.

## Skills covered


- Redact personally identifiable information (PII) in log messages using regex formatters
- Hash and verify passwords with bcrypt
- Build HTTP Basic Authentication with Base64 credential extraction
- Manage user sessions via cookies and server-side session stores
- Build a Flask authentication service with SQLAlchemy ORM
- Register users, validate logins, create/destroy sessions, and protect routes with decorators

## Tech Stack

| Category | Technologies |
|----------|-------------|
| Language | Python 3 |
| Framework | Flask |
| ORM | SQLAlchemy |
| Security | bcrypt, HTTP Basic Auth, session cookies |
| Database | SQLite (via SQLAlchemy) |
| Logging | Python `logging` with custom formatters |

## Project Structure

| Module | Directory | Focus |
|--------|-----------|-------|
| 0x00 | `0x00-personal_data` | PII redaction, secure password hashing |
| 0x01 | `0x01-Basic_authentication` | Basic Auth API, Base64 header parsing |
| 0x02 | `0x02-Session_authentication` | Cookie sessions, session DB storage |
| 0x03 | `0x03-user_authentication_service` | Full auth service: register, login, sessions |

## Key Implementations

- **Personal data (`0x00`)** — `filter_datum()` regex redaction, `RedactingFormatter` logging class, and `hash_password()` using bcrypt for one-way password storage
- **Basic authentication (`0x01`)** — Flask API with `User` model, CRUD user endpoints, and `BasicAuth` class extending `Auth` with Base64 authorization header extraction, credential decoding, and `user_id`-by-credentials lookup
- **Session authentication (`0x02`)** — `SessionAuth` and `SessionDBAuth` classes storing session IDs in cookies, `UserSession` model for database-backed sessions, and protected route decorators on `/api/v1/users` endpoints
- **Authentication service (`0x03`)** — Standalone Flask app with `Auth` class (register, valid_login, create_session, validate_session, destroy_session), SQLAlchemy `User` model, and route handlers for sign-up, sign-in, and logout

### API Routes (Basic Auth module)

| Method | Route | Description |
|--------|-------|-------------|
| GET | `/api/v1/status` | API health status |
| GET | `/api/v1/stats` | API statistics |
| GET | `/api/v1/users` | List all users |
| GET | `/api/v1/users/:id` | Retrieve user by ID |
| POST | `/api/v1/users` | Create user (email, password, optional names) |
| PUT | `/api/v1/users/:id` | Update user names |
| DELETE | `/api/v1/users/:id` | Delete user by ID |

## Getting Started

### Prerequisites

- Python 3.8+
- `pip install -r 0x01-Basic_authentication/requirements.txt`
- `pip install -r 0x02-Session_authentication/requirements.txt`

Typical dependencies: Flask, bcrypt, SQLAlchemy, mysql-connector-python (where applicable).

### Setup

```bash
git clone <repository-url>
cd alx-backend-user-data
pip3 install flask bcrypt sqlalchemy
```

### Running Tasks

Personal data module:

```bash
python3 0x00-personal_data/main.py
```

Basic Auth API:

```bash
cd 0x01-Basic_authentication
pip3 install -r requirements.txt
API_HOST=0.0.0.0 API_PORT=5000 python3 -m api.v1.app
```

Session authentication checkers:

```bash
python3 0x02-Session_authentication/main_0.py
python3 0x02-Session_authentication/main_4.py
```

User authentication service:

```bash
cd 0x03-user_authentication_service
python3 app.py
# Test with provided main scripts:
python3 0-main.py
python3 10-main.py
```

## Curriculum Context

This project is a capstone of the ALX backend specialization, applying SQLAlchemy ORM skills from `alx-higher_level_programming` and storage patterns from `alx-backend-storage`. Authentication concepts introduced here—password hashing, session cookies, route guards—are directly reused in the AirBnB clone API (`AirBnB_clone_v3`/`v4`) where user identity and protected endpoints are core requirements. Completing all four modules prepares learners to implement secure, production-style auth in Flask and to understand OWASP-aligned handling of personal data in logs and databases.

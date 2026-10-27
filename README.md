# Pet Vaccination Management API

A production-ready RESTful API for managing veterinary vaccination, built with Python and Django REST Framework. This project implements a strict **Service Layer architecture**, role-based JWT authentication, and is validated by a comprehensive suite of **93 automated tests**.

## Technical Architecture

*   **Service Layer Pattern:** Completely decoupled business logic from the HTTP view layer (`services.py`). This guarantees testability and prevents "fat controllers", a standard requirement for scalable enterprise applications.
*   **Segregated Serialization:** Implemented distinct Read and Write serializers. This ensures strict input validation while allowing complex, nested data representations on GET requests without circular dependencies.
*   **Role-Based Access Control (RBAC):** Built custom permission classes governing a 3-tier hierarchy (Admin, Veterinarian, Regular User). Enforces object-level permissions (e.g., Veterinarians can only modify their own vaccination records).
*   **Extensive Test Coverage:** Engineered **93 automated tests** utilizing Django's `TestCase`. Covers model constraints, API integration, business logic, and strict role authorization edge cases.

## Overview

Internal tool for veterinary clinics to manage pet owners, pets, vaccines, and vaccination records with role-based access control.

**Key Features:**
- Owner, Pet, Vaccine, and Vaccination Record management
- JWT authentication with 3-tier role system (Regular/Vet/Admin)
- Automatic next-dose calculation based on vaccine intervals
- Granular permissions with ownership validation
- Tests covering models, APIs, and permissions

## Tech Stack

*   **Language & Framework:** Python 3.12, Django 6.0.2, Django REST Framework 3.16.1
*   **Security:** JWT Authentication (`djangorestframework-simplejwt`)
*   **Database:** SQLite (Configured for seamless local testing/migration)
*   **Infrastructure:** Docker


## Running the Infrastructure Locally

The application is fully containerized for zero-setup execution.

### Build and Execute
Run the following command to spin up the API and expose it on port 8000:
```bash
docker build -t pet-vaccination-management-api .
docker run --name pet-vaccination -p 8000:8000 pet-vaccination-management-api 
```

*(Note: The database is automatically migrated and populated with a default admin user upon startup via Django migrations).*

### Access the API

* **Health Check:** `http://127.0.0.1:8000/api/health/`

## Running the Test Suite

To execute the 93 automated unit and integration tests, run:

```bash
docker exec -it pet-vaccination python manage.py test
```
## Authentication Flow Example

```bash
# 1. Obtain JWT Access Token
POST /api/accounts/login/
{
  "username": "admin",
  "password": "admin123"
}

# 2. Access Protected Routes
GET /api/owners/
Authorization: Bearer <your_access_token>

```
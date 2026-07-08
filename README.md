# College ERP

CIET's Django-based ERP for academics, faculty, students, parents, notifications, and internal administration.

## Overview

This repository is a Django 5.2 project with a MongoDB-backed database layer and app-level modules for:

- `apps.accounts` for authentication, RBAC, OTP services, and bulk import utilities
- `apps.academics` for academic data and result workflows
- `apps.faculty` for mentor and faculty workflows
- `apps.students` for profiles, certifications, and student-facing features
- `apps.parents` for parent access
- `apps.notifications` and `apps.messaging` for communication flows
- `apps.audit` for audit logging
- `apps.core` for shared middleware, base models, and site-level views

## Tech Stack

- Backend: Django, Django REST Framework, django-htmx, django-extensions
- Database: MongoDB via `django-mongodb-backend`
- Background jobs: Celery, Redis, django-celery-beat, django-celery-results
- API docs: drf-spectacular
- Quality tools: pytest, pytest-django, black, flake8, isort

## Quick Start

1. Create and activate a virtual environment.
2. Install dependencies:
   ```bash
   pip install -r requirements/development.txt
   ```
3. Create a `.env` file in the project root and set at least:
   ```env
   SECRET_KEY=your-secret-key
   MONGODB_NAME=erp_portal
   MONGODB_URI=mongodb://127.0.0.1:27017/erp_portal
   ```
4. Apply database migrations:
   ```bash
   python manage.py migrate
   ```
5. Create default role groups and permissions:
   ```bash
   python manage.py setup_roles
   ```
6. Run the development server:
   ```bash
   python manage.py runserver
   ```

## Migration Commands

Use these when you change models or need to inspect migration state:

```bash
python manage.py makemigrations
python manage.py makemigrations accounts
python manage.py migrate
python manage.py showmigrations
```

## Database Setup Notes

The project is configured to use MongoDB as the default database engine in `config/settings/base.py`. If you are setting up a new environment, make sure the MongoDB URI in `.env` points to the correct server before running migrations.

## Useful Commands

- `python manage.py setup_roles` creates the default Django groups and permissions.
- `python manage.py createsuperuser` creates an admin user.
- `python -m pytest` runs the test suite.

## Data Utilities

- `scripts/migrate_sqlite_to_mongodb.py` migrates legacy SQLite data into MongoDB.
- `scripts/repair_mongodb_types.py` repairs MongoDB document types for Django compatibility.
- `scripts/seed_departments.py` seeds department data.
- `scripts/clear_mongodb_data.py` clears MongoDB data for local resets.

## Project Layout

- `apps/` contains the Django apps
- `config/` contains settings, ASGI, WSGI, and URLs
- `templates/` contains Django templates
- `static/` contains CSS, JS, images, and shared assets
- `scripts/` contains data maintenance utilities

## Testing

```bash
python -m pytest
```

## Notes

- Student roll numbers are admin-controlled and should not be edited by students.
- OTP verification for email and phone is available from the student portal settings flow.

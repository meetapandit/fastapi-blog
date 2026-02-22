# fastapi-blog

A full-stack blog application built with FastAPI, SQLAlchemy, and Jinja2 templates. Supports user registration, JWT authentication, and post management via both a browser UI and a REST API.

## Features

- User registration and login with JWT bearer token auth
- Create, read, update, and delete blog posts
- User profile with optional profile picture
- Jinja2-rendered HTML pages alongside a JSON REST API
- Async SQLite database via SQLAlchemy + aiosqlite
- Password hashing with Argon2

## Project Structure

```
fastapi-blog/
├── main.py          # App entry point, HTML routes, exception handlers
├── auth.py          # JWT creation, password hashing, current user dependency
├── config.py        # Settings loaded from .env
├── database.py      # Async SQLAlchemy engine and session
├── models.py        # User and Post ORM models
├── schemas.py       # Pydantic request/response schemas
├── routers/
│   ├── users.py     # /api/users — register, login, profile CRUD
│   └── posts.py     # /api/posts — post CRUD
├── templates/       # Jinja2 HTML templates
├── static/          # CSS, JS, default profile picture
└── media/           # Uploaded profile pictures
```

## Setup

**Requirements:** Python 3.10+, [uv](https://github.com/astral-sh/uv)

1. Clone the repo and install dependencies:

```bash
uv sync
```

2. Create a `.env` file in the project root:

```env
SECRET_KEY=your-secret-key-here
```

Generate a secure key with:

```bash
python -c "import secrets; print(secrets.token_hex(32))"
```

## Running

```bash
uv run fastapi dev main.py
```

The app will be available at <http://localhost:8000>.

Interactive API docs: <http://localhost:8000/docs>

## API Endpoints

| Method | Path | Description |
|--------|------|-------------|
| POST | `/api/users` | Register a new user |
| POST | `/api/users/token` | Login and get a JWT |
| GET | `/api/users/me` | Get current user |
| GET | `/api/users/{id}` | Get user by ID |
| PATCH | `/api/users/{id}` | Update user |
| DELETE | `/api/users/{id}` | Delete user |
| GET | `/api/posts` | List all posts |
| POST | `/api/posts` | Create a post |
| GET | `/api/posts/{id}` | Get post by ID |
| PATCH | `/api/posts/{id}` | Update post |
| DELETE | `/api/posts/{id}` | Delete post |

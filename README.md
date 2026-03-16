# rest-api-2- 16-3
postman and sqlite



# 🛒 Items API

> A blazing-fast **REST API** built with **FastAPI** — full CRUD for items with auto-increment IDs, Pydantic validation, and interactive Swagger docs.

![FastAPI](https://img.shields.io/badge/FastAPI-0.111.0-009688?style=flat-square&logo=fastapi&logoColor=white)
![Uvicorn](https://img.shields.io/badge/Uvicorn-0.30.1-4051b5?style=flat-square&logo=gunicorn&logoColor=white)
![Pydantic](https://img.shields.io/badge/Pydantic-2.7.4-e92063?style=flat-square&logo=python&logoColor=white)
![Python](https://img.shields.io/badge/Python-3.10+-3776ab?style=flat-square&logo=python&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Endpoints](#-endpoints)
- [Data Model](#-data-model)
- [Getting Started](#-getting-started)
- [Usage Examples](#-usage-examples)
- [Project Structure](#-project-structure)

---

## 🌐 Overview

**Items API** exposes a simple in-memory items store over HTTP. Each item has an `id`, `name`, `price`, and optional `description`. The API supports all standard REST operations and ships with a 3D animated landing page and full Swagger/OpenAPI docs.

| 🔗 Route | Description |
|---|---|
| `http://127.0.0.1:8002/` | 🎨 Animated landing page |
| `http://127.0.0.1:8002/docs` | 📖 Swagger UI |
| `http://127.0.0.1:8002/items` | 📦 Items resource |

---

## 📡 Endpoints

| Method | Endpoint | Description | Status |
|---|---|---|---|
| `GET` | `/items` | List all items | `200 OK` |
| `GET` | `/items/{id}` | Fetch a single item by ID | `200 OK` / `404` |
| `POST` | `/items` | Create a new item | `201 Created` |
| `PUT` | `/items/{id}` | Full replace — creates if not found | `200 OK` |
| `PATCH` | `/items/{id}` | Partial update (only provided fields) | `200 OK` / `404` |
| `DELETE` | `/items/{id}` | Delete an item by ID | `200 OK` / `404` |

---

## 📦 Data Model

### Item

```json
{
  "id": 1,
  "name": "Laptop",
  "price": 1200.0,
  "description": "Gaming laptop"
}
```

| Field | Type | Required | Notes |
|---|---|---|---|
| `id` | `int` | auto | Auto-incremented by the server |
| `name` | `str` | ✅ | Item display name |
| `price` | `float` | ✅ | Item price |
| `description` | `str` | ❌ | Optional description |

### ItemUpdate (PATCH only)

All fields are optional — only provided fields are updated:

```json
{
  "price": 999.0
}
```

---

## 🚀 Getting Started

### 1. Install dependencies

```bash
pip install -r requirements.txt
```

### 2. Start the server

```bash
uvicorn 01_servers:app --port 8002 --reload
```

> 💡 If the page doesn't reload after a change, try switching to a different port (e.g. `--port 8003`).

### 3. Open in browser

```
http://127.0.0.1:8002/        ← Landing page
http://127.0.0.1:8002/docs    ← Swagger UI
http://127.0.0.1:8002/items   ← Raw JSON
```

---

## 🧪 Usage Examples

### Get all items
```bash
curl http://127.0.0.1:8002/items
```

### Get item by ID
```bash
curl http://127.0.0.1:8002/items/1
```

### Create a new item
```bash
curl -X POST http://127.0.0.1:8002/items \
  -H "Content-Type: application/json" \
  -d '{"name": "Headphones", "price": 250, "description": "Noise cancelling"}'
```

### Full update (PUT — creates if not found)
```bash
curl -X PUT http://127.0.0.1:8002/items/1 \
  -H "Content-Type: application/json" \
  -d '{"name": "Laptop Pro", "price": 1500, "description": "Updated model"}'
```

### Partial update (PATCH — only updates what you send)
```bash
curl -X PATCH http://127.0.0.1:8002/items/1 \
  -H "Content-Type: application/json" \
  -d '{"price": 999}'
```

### Delete an item
```bash
curl -X DELETE http://127.0.0.1:8002/items/1
```

---

## 🗂 Project Structure

```
.
├── 01_servers.py       # FastAPI app — all routes and models
├── requirements.txt    # Pinned dependencies
└── README.md           # You are here
```

---

## 📦 Requirements

```
fastapi==0.111.0
uvicorn==0.30.1
pydantic==2.7.4
```

---

## 🔧 PUT vs PATCH — Key Difference

| | `PUT` | `PATCH` |
|---|---|---|
| **All fields required?** | ✅ Yes — full replace | ❌ No — partial update |
| **Item not found?** | Creates a new one | Returns `404` |
| **Use when** | Replacing the whole item | Updating one or two fields |

---

*Built with ❤️ using [FastAPI](https://fastapi.tiangolo.com/) · [16.03.2026]*

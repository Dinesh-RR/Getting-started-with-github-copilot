# Copilot Instructions for Mergington High School Activities API

## Project Overview
- **Purpose:** Simple FastAPI backend and static frontend for managing extracurricular activity signups at Mergington High School.
- **Main Components:**
  - `src/app.py`: FastAPI app with endpoints for listing activities and signing up students.
  - `src/static/`: Static frontend (HTML, JS, CSS) for interacting with the API.

## Architecture & Data Flow
- **API Endpoints:**
  - `GET /activities`: Returns all activities and their details (see in-memory `activities` dict in `app.py`).
  - `POST /activities/{activity_name}/signup?email=...`: Adds a student to an activity by email.
- **Frontend:**
  - `index.html` loads activities via JS (`fetch /activities`) and allows signups via form (POSTs to `/activities/{activity_name}/signup`).
  - `app.js` handles all API calls and DOM updates.
- **Static Files:** Served at `/static/` (see FastAPI `app.mount`). Root `/` redirects to `/static/index.html`.

## Developer Workflows
- **Install dependencies:**
  ```bash
  pip install fastapi uvicorn
  ```
- **Run the app:**
  ```bash
  python src/app.py
  # or
  uvicorn src.app:app --reload
  ```
- **View API docs:**
  - Swagger: [http://localhost:8000/docs](http://localhost:8000/docs)
  - ReDoc: [http://localhost:8000/redoc](http://localhost:8000/redoc)
- **Frontend:**
  - Open [http://localhost:8000/static/index.html](http://localhost:8000/static/index.html)

## Project-Specific Patterns & Conventions
- **Data Model:**
  - Activities are stored in-memory as a dict keyed by activity name. Each activity has `description`, `schedule`, `max_participants`, and `participants` (list of emails).
  - No persistent storage; all data resets on restart.
- **Signups:**
  - No authentication; any email can be used.
  - No duplicate signup or max participant checks (can be added if needed).
- **Frontend-Backend Integration:**
  - All API calls are relative (no CORS issues in local dev).
  - JS dynamically populates activity list and signup dropdown from `/activities`.

## Key Files
- `src/app.py`: FastAPI app, API logic, static file serving
- `src/static/index.html`: Main UI
- `src/static/app.js`: Frontend logic (fetch, signup)
- `src/static/styles.css`: Styling
- `src/README.md`: API and usage documentation

## Example: Adding a New Activity
- Add to the `activities` dict in `app.py`.
- No migration or DB update needed.

---
For more, see `src/README.md`.

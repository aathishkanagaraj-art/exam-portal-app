# Cloud-Based Online Examination Portal

A minimal but complete Django project implementing a role-based online examination portal with MCQ/subjective questions, timed exams, randomized questions, instant scoring for MCQs, and basic browser-activity monitoring.

## Features
- Roles: **Admin**, **Faculty**, **Student**
- Create question bank: MCQ and Subjective
- Create exams with time-window, duration, randomized question order
- Students take exams with a visible countdown timer
- Instant scoring for MCQs; manual grading support for subjective answers
- Results dashboard for students and analytics for faculty
- Basic integrity: tab-switch detection + attempt log
- Dockerfile included; SQLite by default (simple), Postgres-ready via env

## Quickstart (Local)

### 1) Python environment
```bash
cd backend
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

### 2) Configure env (optional)
Create a `.env` (optional). Defaults use SQLite.
```
SECRET_KEY=dev-secret-change-me
DEBUG=1
ALLOWED_HOSTS=*
TIME_ZONE=Asia/Kolkata
DATABASE_URL=sqlite:///db.sqlite3
```

### 3) Initialize DB and superuser
```bash
python manage.py migrate
python manage.py createsuperuser --username admin --email admin@example.com
python manage.py seed_demo   # creates demo users, questions, and a sample exam
```

### 4) Run
```bash
python manage.py runserver
```
Open http://127.0.0.1:8000/

- Admin: /admin/
- Faculty login: demo_faculty / Pass@123
- Student login: student01 / Pass@123

## Docker (SQLite)
```bash
docker build -t cloud-exam-portal:dev -f infra/Dockerfile .
docker run -p 8000:8000 cloud-exam-portal:dev
```

## Deploy tips
- Use Postgres in production: set `DATABASE_URL=postgres://...`
- Set `DEBUG=0` and configure `ALLOWED_HOSTS`
- Add TLS and a reverse proxy (e.g., Nginx, Caddy)

## Project layout
```
backend/
  ceportal/        # project settings
  exam/            # app with models/views
  templates/       # HTML templates (Bootstrap)
  static/          # JS/CSS (timer + integrity)
infra/
  Dockerfile
  docker-compose.postgres.yml (optional, simple example)
```

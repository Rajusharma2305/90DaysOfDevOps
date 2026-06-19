Today's goal is to build a production-like multi-container application using Docker Compose.

Project Structure
docker-compose-advanced/
│
├── docker-compose.yml
│
└── app/
    ├── Dockerfile
    ├── requirements.txt
    └── app.py
Task 1: Build a 3-Service Stack
1. Create Flask App
app.py
from flask import Flask
import psycopg2
import os

app = Flask(__name__)

@app.route("/")
def home():
    return "Hello from Flask + PostgreSQL + Redis"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
requirements.txt
flask
psycopg2-binary
Dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt

COPY . .

EXPOSE 5000

CMD ["python","app.py"]
Task 2: Docker Compose with Database and Cache
docker-compose.yml
services:

  web:
    build: ./app

    ports:
      - "5000:5000"

    depends_on:
      db:
        condition: service_healthy

    networks:
      - app-network

    labels:
      - "project=day32"
      - "service=web"

  db:
    image: postgres:16

    environment:
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: admin123
      POSTGRES_DB: mydb

    volumes:
      - postgres-data:/var/lib/postgresql/data

    restart: always

    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U admin"]
      interval: 10s
      timeout: 5s
      retries: 5

    networks:
      - app-network

    labels:
      - "project=day32"
      - "service=db"

  redis:
    image: redis:7

    networks:
      - app-network

    labels:
      - "project=day32"
      - "service=cache"

networks:
  app-network:

volumes:
  postgres-data:
Task 3: Test Healthchecks & Dependencies

Start everything:

docker compose up

Check containers:

docker ps

Check health status:

docker inspect postgres_container

Look for:

"Health": {
  "Status": "healthy"
}
What happens?
PostgreSQL starts
Healthcheck runs
Database becomes healthy
Flask app starts

Without healthcheck:

depends_on:
  - db

The app may start before PostgreSQL is ready.

Task 4: Restart Policies
Restart Always
restart: always

Kill database:

docker kill <container_id>

Docker automatically recreates it.

Restart On Failure
restart: on-failure

Container restarts only when it crashes with an error.

If you stop manually:

docker stop <container_id>

It stays stopped.

Notes
restart: always

Use for:

Databases
Production applications
Critical services
restart: on-failure

Use for:

Batch jobs
Worker containers
Debugging environments
Task 5: Build Using Dockerfile

Compose builds image automatically.

web:
  build: ./app

Start:

docker compose up --build
Make a Code Change

Change:

return "Hello from Flask + PostgreSQL + Redis"

to

return "Docker Compose Day 32"

Rebuild:

docker compose up --build

One command:

✔ Rebuild image

✔ Recreate container

✔ Start application

Task 6: Named Networks

Instead of Docker's default network:

networks:
  app-network:

Services communicate using names:

db
redis
web

Example:

host="db"

Docker DNS automatically resolves service names.

Task 7: Named Volumes

Store database data permanently.

volumes:
  - postgres-data:/var/lib/postgresql/data

Check volume:

docker volume ls

Even if container is removed:

docker compose down

Database data remains.

Task 8: Labels
labels:
  - "project=day32"
  - "service=db"

Useful for:

Monitoring
Logging
Container organization

View labels:

docker inspect <container_id>
Task 9: Scaling (Bonus)

Scale web app:

docker compose up --scale web=3

Check:

docker ps

You should see:

web-1
web-2
web-3
What Breaks?

If compose file contains:

ports:
  - "5000:5000"

Only one container can use host port 5000.

Second and third containers fail.

Error:

Bind for 0.0.0.0:5000 failed
Why?

Host machine has only one port:

localhost:5000

Three containers cannot share it.

Production Solution

Use:

Nginx
HAProxy
Load Balancer

Architecture:

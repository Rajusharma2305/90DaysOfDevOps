Task 1: Install & Verify Docker Compose
Check if Docker Compose is installed
docker compose version
Expected Output
Docker Compose version v2.x.x
Verify Docker is running
docker ps
Task 2: Your First Compose File
Create Project Folder
mkdir compose-basics
cd compose-basics
Create docker-compose.yml
services:
  nginx:
    image: nginx:latest
    ports:
      - "8080:80"
Start Container
docker compose up
Run in Background
docker compose up -d
Verify

Open browser:

http://<EC2-PUBLIC-IP>:8080

You should see:

Welcome to nginx!
View Running Containers
docker ps
Stop Everything
docker compose down
Task 3: WordPress + MySQL Multi-Container Setup
Create New Folder
mkdir wordpress-compose
cd wordpress-compose
Create docker-compose.yml
services:

  db:
    image: mysql:8.0
    container_name: mysql-db

    environment:
      MYSQL_ROOT_PASSWORD: rootpass
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wpuser
      MYSQL_PASSWORD: wppass

    volumes:
      - mysql_data:/var/lib/mysql

  wordpress:
    image: wordpress:latest
    container_name: wordpress-app

    ports:
      - "8080:80"

    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wpuser
      WORDPRESS_DB_PASSWORD: wppass
      WORDPRESS_DB_NAME: wordpress

    depends_on:
      - db

volumes:
  mysql_data:
Start Both Containers
docker compose up -d
Check Running Services
docker compose ps
Access WordPress

Browser:

http://<EC2-PUBLIC-IP>:8080

Complete the WordPress installation wizard.

Verify Data Persistence

Stop Containers:

docker compose down

Start Again:

docker compose up -d

Open WordPress again.

✅ Website and database data should still exist because MySQL data is stored inside:

volumes:
  - mysql_data:/var/lib/mysql
Task 4: Important Docker Compose Commands
Start Services
docker compose up
Start in Detached Mode
docker compose up -d
View Running Services
docker compose ps
View All Logs
docker compose logs
View Logs of One Service
docker compose logs wordpress

or

docker compose logs db
Follow Logs Live
docker compose logs -f
Stop Services Only
docker compose stop
Start Stopped Services
docker compose start
Remove Containers & Networks
docker compose down
Remove Containers, Networks & Volumes
docker compose down -v
Rebuild Images
docker compose up --build
Rebuild in Detached Mode
docker compose up -d --build
Task 5: Environment Variables
Create .env File
MYSQL_ROOT_PASSWORD=rootpass
MYSQL_DATABASE=wordpress
MYSQL_USER=wpuser
MYSQL_PASSWORD=wppass
Update docker-compose.yml
services:

  db:
    image: mysql:8.0

    environment:
      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
      MYSQL_DATABASE: ${MYSQL_DATABASE}
      MYSQL_USER: ${MYSQL_USER}
      MYSQL_PASSWORD: ${MYSQL_PASSWORD}

    volumes:
      - mysql_data:/var/lib/mysql

  wordpress:
    image: wordpress:latest

    ports:
      - "8080:80"

    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: ${MYSQL_USER}
      WORDPRESS_DB_PASSWORD: ${MYSQL_PASSWORD}
      WORDPRESS_DB_NAME: ${MYSQL_DATABASE}

    depends_on:
      - db

volumes:
  mysql_data:
Verify Environment Variables

Check the generated configuration:

docker compose config

You should see actual values substituted from the .env file.

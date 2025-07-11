🐳 WordPress + MySQL: 2-Tier Dockerized Application
This is a 2-tier application deployed using Docker and Docker Compose.
It consists of:

Frontend: WordPress (a PHP-based CMS)

Backend: MySQL (a relational database)


Project Overview :- 
| Tier          | Technology     | Role                     |
| ------------- | -------------- | ------------------------ |
| Tier 1        | WordPress      | Frontend Web Application |
| Tier 2        | MySQL          | Backend Database Server  |
| Orchestration | Docker Compose | Container management     |



🔧 Prerequisites
Make sure the following are installed on your system:

✅ Docker → docker --version

✅ Docker Compose → docker compose version

✅ Git (optional for cloning)

step1: 
sudo apt update -y
sudo apt install docker.io docker-compose -y

step2:
sudo systemctl start docker
sudo systemctl enable docker

step3: 
vim docker-compose.yml

version: '3'

services:
  db:
    image: mysql:5.7
    container_name: wp-mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: rootpass
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wpuser
      MYSQL_PASSWORD: wppass
    volumes:
      - db_data:/var/lib/mysql
    networks:
      - wp-network

  wordpress:
    image: wordpress:latest
    container_name: wp-site
    restart: always
    ports:
      - "8080:80"
    environment:
      WORDPRESS_DB_HOST: wp-mysql:3306
      WORDPRESS_DB_NAME: wordpress
      WORDPRESS_DB_USER: wpuser
      WORDPRESS_DB_PASSWORD: wppass
    networks:
      - wp-network

volumes:
  db_data:

networks:
  wp-network:


step4: start the application 
       docker-compose up -d


step5: Access the applicaton 
on browser:   <ip-address>:8080
  
Stop the container : - docker-compose down

Remove Container volume & network :- docker-compose down --volumes




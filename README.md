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


Step 1: 
<img width="972" height="223" alt="Screenshot 2025-07-11 230729" src="https://github.com/user-attachments/assets/9b9bcfb4-3c5f-4aa0-9c65-ca7f00e449a1" />

Step 2:
<img width="1729" height="518" alt="Screenshot 2025-07-11 231042" src="https://github.com/user-attachments/assets/a2989051-9b19-476a-b599-9b47dbc8bb7e" />

Step 3:
<img width="763" height="85" alt="Screenshot 2025-07-11 231157" src="https://github.com/user-attachments/assets/02923dc0-cb02-47b1-a9f9-907569873b81" />

Step 4:
<img width="941" height="69" alt="Screenshot 2025-07-11 231326" src="https://github.com/user-attachments/assets/917e1561-4f5c-457a-8021-d5f52fdcde9d" />

Step 5:
<img width="630" height="40" alt="Screenshot 2025-07-11 231502" src="https://github.com/user-attachments/assets/da5eba0e-c94d-48a3-81de-96422ef2c847" />

<img width="776" height="969" alt="Screenshot 2025-07-11 231418" src="https://github.com/user-attachments/assets/2f00af85-980d-4699-af0e-eaa710ee08c6" />

Step 6:
<img width="1893" height="1002" alt="Screenshot 2025-07-11 231727" src="https://github.com/user-attachments/assets/cfb2c14b-6236-4c8a-b876-075f351ad431" />

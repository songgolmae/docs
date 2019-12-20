version: '2'

services:
  db:
    image: mariadb:10.4.10    
    container_name: mariadb
    environment:
      MYSQL_ROOT_PASSWORD: root!
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress!
    ports:
      - "3306:3306"          
    volumes:
      - mysql_data:/var/lib/mysql     
  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    container_name: wordpress
    volumes: 
      - app_data:/var/www/html
    ports:
      - "8000:80"
    restart: always
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_NAME: wordpress      
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress!
    depends_on:
      - db
volumes:
  mysql_data:
    driver: local
  app_data: 
    driver: local
    

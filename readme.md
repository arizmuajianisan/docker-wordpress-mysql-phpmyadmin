# Docker Compose Setup for WordPress and MySQL

This repository contains a Docker Compose setup for running a WordPress site along with a MySQL database and phpMyAdmin for database management.

## Table of Content

1. Setup
2. Operation Wordpress
   - Backup
   - Restore

## Setup

1. **Clone the Repository** :rocket:

2. **Set Up the Environment File**:
   You need to create a `.env` file from the example provided. To do this, rename the `.env.EXAMPLE` file to `.env`:
   ```bash
   mv .env.EXAMPLE .env
   ```

3. **Configure the .env File**:
   Open the `.env` file and update the following variables with your own values:
   - `MYSQL_DB_NAME`: Your desired database name.
   - `MYSQL_USER`: Your MySQL username.
   - `MYSQL_ROOT_PASSWORD`: Your MySQL root password.
   - `MYSQL_PASSWORD`: Your MySQL user password.
   - `PORT_WORDPRESS`: The port for accessing WordPress.
   - `PORT_MYSQL`: The port for accessing MySQL.
   - `PORT_PHPMYADMIN`: The port for accessing phpMyAdmin.
   - `NAME_WORDPRESS`: The name for your WordPress container.
   - `NAME_DB`: The name for your MySQL container.
   - `NAME_PHPMYADMIN`: The name for your phpMyAdmin container.

4. **Create the Docker Network** (if it doesn't already exist):
   It is recommended to create a Docker network for your services. You can create the network using the following command:
   ```bash
   docker network create your-network-name --subnet 10.0.1.0/24
   ```

   After creating the network, you need to specify it in your `docker-compose.yml` file to ensure that all services can communicate with each other. Add the following at the end of your `docker-compose.yml` file:
   ```yaml
   networks:
     default:
       name: your-network-name
       external: true
       driver: bridge
   ```
   This configuration tells Docker Compose to use the existing network you created, allowing your WordPress, MySQL, and phpMyAdmin services to interact seamlessly.

5. **Run the Docker Compose**:
   After configuring the `.env` file and creating the network, you can start the services using Docker Compose:
   ```bash
   docker-compose up -d
   ```

6. **Access the Services**:
   - WordPress: [http://localhost:8080](http://localhost:8080)
   - phpMyAdmin: [http://localhost:8082](http://localhost:8082)

## Stopping the Services

To stop the services, run:
```bash
docker-compose down
```

## Move the Project from Dev to Production

**WARNING**
Make sure you already run the Wordpress on the production server and completed the instalation.

We will use the plugin UpdraftPlus: WP Backup & Migration Plugin.
This plugin need to installed on both Development WP and Production WP.

Step to perform:
   On the Wordpress Development:
     1. Do the full backup:
        - Database
        - Plugins
        - Themes
        - Uploads
        - Others
     2. Download all the backup file
     3. Copy to your Production Server

   On the Wordpress Production:
      1. Go to UdraftPlus setting area
      2. Upload the backup files
      3. Restore with it
   After the process is completed, you will need to login using the credentials from Development WP.



This README provides a basic overview of how to set up and run the Docker Compose file for WordPress and MySQL.
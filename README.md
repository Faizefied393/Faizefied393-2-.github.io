# Faizefied393-2-.github.io
Docker Compose Project 2 WordPress Installation Documentation
This is the guide that I followed throughout this project [guide](https://www.hostinger.com/tutorials/run-docker-wordpress)

## Install the Compose of docker with docker

1. In order the install the packages run the following commands:
```Bash
sudo apt update
sudo apt install ca-certificates curl gnupg lsb-release
```
2. Adding the GPG key for Docker
```Bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg 
```
3. The command you use to set up the repository 
```Bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
4. You will add the following Docker packages yourself in the Docker group by installing them
```Bash
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
sudo usermod -aG docker faizt
```
5. Test Docker compose by installing it first causing a success message to appear
```Bash
sudo apt install docker-compose-plugin
sudo docker run hello-world
```
---

## Setting up word press install

1. Make a new directory for **Wordpress** and get navigating into this

```Bash
mkdir wordpress
cd wordpress
```
2. Creating a file in order to insert the contents below which is **docker-compose.yml**

```Bash
vim docker-compose.yml
i #get into insert modde
version: "3" 
# Defining th compose version tht is usable
services:
  # To define which docker images to run you use services. In this case it will be a wordpress image with MySQL server
  db:
    image: mysql:5.7
    # The image in the MySQL 5.7 server indicates a container image of a database which is from Docker hub and it used in the installation. 
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: MyR00tMySQLPa$$5w0rD
      MYSQL_DATABASE: MyWordPressDatabaseName
      MYSQL_USER: MyWordPressUser
      MYSQL_PASSWORD: Pa$$5w0rD
      # The four past lines define the main variables that are needed in order for the MySQL container to be able to work correctly: including database, database username, as well as database username password. Also make sure to include the MySQL root password. 
  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    restart: always
    # Use the restart mode to restart the line controls which means that is the container stops working for any given reason this restarts the immediate process. 
    ports:
      - "8000:80"
      # When it comes to defining the previous line when it comes to the port that the wordpress container will use due to a successful installation, this is what the full path will look like: http://localhost:8000
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: MyWordPressUser
      WORDPRESS_DB_PASSWORD: Pa$$5w0rD
      WORDPRESS_DB_NAME: MyWordPressDatabaseName
# When it comes to MySQL image variables, the four lines that are last will define the main variables which is needed for wordpress in order to work for the Wordpress containers properly, as well as using  the MySQL container. 
    volumes:
      ["./:/var/www/html"]
volumes:
  mysql: {}
```
3. In order to start the containers run the following command.

```Bash
sudo docker compose up -d
```
4. Go to the browser and navigate to the site **http://localhost:8000/**. This will greet you with the page **WordPress** to set up. Now you are filling in all of the information and logging in to access the **WordPress** dashboard. 
---

## The Dashboards Screenshot

![Imgur](https://imgur.com/DzASDMa.png)

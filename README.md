# Laravel-Docker
Laravel in Dcoker Compose
Use php 8.2 or higher

`
Clone repositories
`
`
git clone 
`

`
cd to folder
`

# Setup

Copy File Env  
`
cp .env-example .env
`

`
cp src/.env-example .env
`

Setup env  
`
vim .env
`

`
vim src/.env
`

# Run Docker  
`
docker-compose up -d --build
`


# Run Docker next time
`
docker-compose up -d
`

# Run in command
`
docker exec -it php sh // php คือ container name
`

`
chown laravel:laravel /var/www/html
`


# Dependencies Install
`
cd src
`

`
docker-compose run composer install
`

`
docker-compose run npm install
`

# Setup Laravel
Generate Key  
`
docker-compose run artisan key:generate
`

# Phpmyadmin 
`
http://localhost:81
`

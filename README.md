## TODO SIMPLE PROJECT WITH LARAVEL VITE AND VUE JS
### How to install
For this project, Laravel 9 is being used, which calls for PHP 8, Vue 3, and Tailwind CSS.<br />
Let’s get started with the following command:
- Install package module
````command
npm install
````
- Install laravel vendor with Composer
````command
composer install
````
- Make .env
````command
cp .env.example .env
````
- Generate key for .env
````command
php artisan key:generate
````
- Run migration for database
````command
php artisan migrate --seed
````

### Run Project
- Run Vue
````command
npm run dev
````
- Run Laravel
````command
php artisan serve
````
- Check project on:
````php
http://localhost:8000
````
- Project running:
![image](https://user-images.githubusercontent.com/65013338/208233681-ca18f355-7384-411c-b6ee-1c8f69516b7d.png)


### Note
- Default Password user :
````php
password
````

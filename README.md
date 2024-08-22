#pull 
docker run php:8.2-fpm-buster php -m


# git clone form laravel 
# git batch 
$ git cd src
$ git clone https://github.com/laravel/laravel.git

# install Composer
docker-compose exec app composer install

# gen laravel APP_KEY
docker-compose exec app php artisan key:generate


# confie .env
DB_CONNECTION=db
DB_HOST=db
DB_PORT=3306
DB_DATABASE=laravel_env11_db
DB_USERNAME=admin
DB_PASSWORD=1234

# check nodejs version
docker-compose exec app node -v

# check composer 
docker-compose exec app php composer -v

# check artisan 
docker-compose exec app php artisan -v

# check config laravel 
docker-compose exec app php artisan config:clear


# up docker with  
docker-compose up -d


# สร้าง testmail 
docker-compose exec app php artisan make:mail TestMail



# database migrate 
docker-compose exec app php artisan migrate


# ทำการติดตั้ง vendor  depency predis/predis ในโปรเจ็กต์ Laravel  (src/vendor)
docker-compose exec  app composer require predis/predis

# congig emv redid
CACHE_DRIVER = redis

REDIS_CLIENT=redis
REDIS_HOST=redis
REDIS_PASSWORD=null
REDIS_PORT=6379



#การใช้งาน Redid 
# Example reis chas
# use reis chas
    use Illuminate\Support\Facades\Redis;
    Route::get('/store', function () {
        Redis::set('Bangkok','Krung Thep Maha Nakhon');
    });
    Route::get('/retrive', function () {
        return  Redis::get('Bangkok');
    });



# Step 18: สร้าง Laravel Mail
---
docker-compose exec app php artisan make:mail TestMail

    #  19: เพิ่ม route
    
    // Test Mailhog
    # use cls mail 
    use Illuminate\Support\Facades\Mail;
    use App\Mail\TestMail;
    Route::get('/send-email', function() {
        Mail::to('samit@itgeniussite.dev')->send(new TestMail);
    });

#   # viewfolde,blade file view/email , test.blade.php

        http://localhost:8025
        public function content(): Content
            {
                return new Content(
                    view: 'email.test',
                );
            }



# check bride network ต้องมี Name : bridge  เพื่อให้ docker ออก internet  ภายนอกได้
docker network ls

 # การ intall vendor
 docker-compose exec app composer install

composer require laravel/sanctum

 # การสร้าง Rest API ใน Laravel  
 Step 1: ลบฐานข้อมูลเดิมทั้งหมดออกก่อน
 - docker-compose exec app php artisan migrate:rollback

 Step 2: สร้าง migration resource conrtroller and model
 - docker-compose exec app php artisan make:model --migration --controller Product --api



---
public function up()
    {
        Schema::create('users', function (Blueprint $table) {
            $table->id();
            $table->string('fullname');
            $table->string('username');
            $table->string('email')->unique();
            $table->timestamp('email_verified_at')->nullable();
            $table->string('password');
            $table->string('tel');
            $table->string('avatar')->nullable();
            $table->tinyInteger('role')->default(1);
            $table->rememberToken();
            $table->timestamps();
        });
    }

Step 4: กำหนดโครงสร้าง migrations "create_products_table.php"
---
public function up()
    {
        Schema::create('products', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->string('slug');
            $table->string('description')->nullable();
            $table->decimal('price',9, 2); // 2,859,893.50
            $table->string('image')->nullable();
            $table->unsignedBigInteger('user_id')->comment('Created By User');
            $table->foreign('user_id')->references('id')->on('users');
            $table->timestamps();
        });
    }

Step 5: ทำการ migrate ฐานข้อมูล

 docker-compose exec app php artisan migrate

# install sanctum
# https://laravel-news.com/laravel-11-directory-structure#:%7E:text=The%20Kernel.,php%20file
- docker-compose exec  app composer require laravel/sanctum 
- docker-compose exec  app php artisan vendor:publish --provider="Laravel\Sanctum\SanctumServiceProvider"
- docker-compose exec  app php artisan install:api
- docker-compose exec  app php artisan migrate



docker-compose exec app rm -rf node_modules
docker-compose exec app npm install
docker-compose exec app npm run build



##
 use Laravel\Sanctum\HasApiTokens;

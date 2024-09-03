# Laravel Core Root | Laravel Only Without Third Party
Laravel Core Root
Prasyarat:
1. Dwonload zip [PHP](https://www.php.net/downloads.php) versi NTS, kemudian ekstrak dan rename folder nya menjadi php. Kemudian masukkan ke dalam path dan cek menggunakan cmd.
   ![364014395-e73dd75f-fd4a-4ab7-a92b-241e25706e03](https://github.com/user-attachments/assets/8641ad2e-8793-4083-9705-3b01bb127192)  

   ```sh
   php -v
   ```
   ![image](https://github.com/user-attachments/assets/6c1dcc3c-99a8-4c72-a2b4-d82b9b13755b)  
3. Copy php.ini-development menjadi php.ini kemudian buka ekstensi openssl
   ```conf
   extension_dir = "ext"
   extension=openssl
   extension=zip
   extension=fileinfo
   extension=pgsql
   extension=pdo_pgsql
   ```
4. Install [Composer](https://getcomposer.org/download/)
   ![image](https://github.com/user-attachments/assets/5c59f00b-74ff-4706-8f0a-ae6a6f421d3c)  
   ![image](https://github.com/user-attachments/assets/549a53ec-8f01-4833-a65f-bdf5cfa288ad)  

5. Pindahkan file composer.phar ke direktori php kemudian buat file composer.bat yang berisi:
   ```bat
   @echo off
   php "%~dp0composer.phar" %*
   ```
6. Selesai

## Memulai Project

1. Siapkan direktori kerja kemudian masuk ke CMD pada direktori kerja yang baru dibuat, ketikkan perintah:
   ```sh
   composer create-project --prefer-dist laravel/laravel laracroot
   ```
2. Buat database di supabase kemudian masukkan ke .env
   ![image](https://github.com/user-attachments/assets/7642a606-60a2-40ff-a27d-6883918fd5ed)
   
   ```env
   DB_CONNECTION=pgsql
   DB_HOST=your-supabase-host.supabase.co
   DB_PORT=5432
   DB_DATABASE=your-database-name
   DB_USERNAME=your-database-username
   DB_PASSWORD=your-database-password
   ```
## Buat Migration dan Model
   - Buat migration dan model untuk resource yang ingin Anda kelola melalui API, misalnya `Post`.
   - Jalankan perintah:
     ```bash
     php artisan make:model Post -m
     ```
   - Buka file migration di `database/migrations/` dan tambahkan kolom yang diperlukan, contoh:
     ```php
     public function up()
     {
         Schema::create('posts', function (Blueprint $table) {
             $table->id();
             $table->string('title');
             $table->text('content');
             $table->timestamps();
         });
     }
     ```
   - Jalankan migration untuk membuat tabel di database:
     ```bash
     php artisan migrate
     ```


## Catatan tambahan
1. [Membuat model dan migrasi](01.%20Model%20dan%20Migrasi/)
2. [Factory dan Seeder](02.%20Factory%20dan%20Seeder/)
3. Membangun Fungsi CRUD
4. API

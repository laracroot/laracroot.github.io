# Laravel Core Root | Laravel Only Without Third Party
Laravel Core Root
Prasyarat:
1. Dwonload zip [PHP](https://www.php.net/downloads.php) versi NTS, kemudian ekstrak dan rename folder nya menjadi php. Kemudian masukkan ke dalam path dan cek menggunakan cmd.
   ![image](https://github.com/user-attachments/assets/e73dd75f-fd4a-4ab7-a92b-241e25706e03)
   ```sh
   php -v
   ```
   ![image](https://github.com/user-attachments/assets/6c1dcc3c-99a8-4c72-a2b4-d82b9b13755b)  
2. Copy php.ini-development menjadi php.ini kemudian buka ekstensi openssl
   ```conf
   extension_dir = "ext"
   extension=openssl
   extension=zip
   extension=fileinfo
   ```
3. Install [Composer](https://getcomposer.org/download/)
   ![image](https://github.com/user-attachments/assets/5c59f00b-74ff-4706-8f0a-ae6a6f421d3c)  
   ![image](https://github.com/user-attachments/assets/549a53ec-8f01-4833-a65f-bdf5cfa288ad)  

4. Pindahkan file composer.phar ke direktori php kemudian buat file composer.bat yang berisi:
   ```bat
   @echo off
   php "%~dp0composer.phar" %*
   ```
5. Selesai

## Memulai Project
1. Siapkan direktori kerja kemudian masuk ke CMD pada direktori kerja yang baru dibuat, ketikkan perintah:
   ```sh
   composer create-project --prefer-dist laravel/laravel laracroot
   ```



3. 

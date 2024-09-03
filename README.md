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
   - Buat migration dan model untuk resource yang ingin Anda kelola melalui API, misalnya `Category`. Dengan field: id, name, is_publish (boolean), created_at, dan updated_at
   - Jalankan perintah dengan opsi membuat file migration(-m) saat model dibuat:
     ```bash
     php artisan make:model Category -m
     ```
     maka akan menghasilkan file Model: app/Models/Category.php
     ```php
     <?php

      namespace App\Models;
      
      use Illuminate\Database\Eloquent\Factories\HasFactory;
      use Illuminate\Database\Eloquent\Model;
      
      class Category extends Model
      {
          use HasFactory;
          protected $fillable = ['name', 'is_publish'];//opsional bisa di tambahkan baris ini
      }
     ```
     $fillable: Properti ini menentukan kolom mana yang bisa diisi secara massal. Anda bisa menambah atau mengurangi kolom yang diizinkan sesuai kebutuhan.
   - Buka file migration di `database/migrations/` dan tambahkan kolom yang diperlukan, contoh:
     ```php
     <?php
      use Illuminate\Database\Migrations\Migration;
      use Illuminate\Database\Schema\Blueprint;
      use Illuminate\Support\Facades\Schema;
      
      return new class extends Migration
      {
          /**
           * Run the migrations.
           */
          public function up(): void
          {
              Schema::create('categories', function (Blueprint $table) {
                  $table->id();
                  $table->string('name'); // Kolom name
                  $table->boolean('is_publish')->default(true); // Kolom is_publish dengan nilai default true
                  $table->timestamps();//created_at dan updated_at
              });
          }
      
          /**
           * Reverse the migrations.
           */
          public function down(): void
          {
              Schema::dropIfExists('categories');
          }
      };
     ```
   - Jalankan migration untuk membuat tabel di database:
     ```bash
     php artisan migrate
     ```
   Dengan langkah-langkah ini, Anda telah berhasil membuat model Category dan migration yang sesuai. Model ini siap digunakan untuk berinteraksi dengan tabel categories di database.  
   ![image](https://github.com/user-attachments/assets/7b11dfca-522a-4d00-821f-2c4aebcd8ab2)


## Mengisi database dengan data dummy
Berikut adalah langkah-langkah untuk membuat factory dan seeder untuk model `Category` serta memasukkan 100 data menggunakan Faker:

### 1. **Membuat Factory untuk `Category`**

Pertama, kita perlu membuat factory untuk model `Category`. Anda dapat membuat factory menggunakan perintah berikut:

```bash
php artisan make:factory CategoryFactory --model=Category
```

Ini akan membuat file `CategoryFactory` di direktori `database/factories/`.

### 2. **Mengedit Factory**

Buka file `CategoryFactory.php` di `database/factories/` dan edit seperti berikut:

```php
<?php

namespace Database\Factories;

use App\Models\Category;
use Illuminate\Database\Eloquent\Factories\Factory;

/**
 * @extends \Illuminate\Database\Eloquent\Factories\Factory<\App\Models\Category>
 */
class CategoryFactory extends Factory
{
    /**
     * Define the model's default state.
     *
     * @return array<string, mixed>
     */
    protected $model = Category::class;//opsional tambahan baris ini lihat di model jika disana ada maka tambahkan ini

    public function definition(): array
    {
        return [
            'name' => $this->faker->word, // Menghasilkan nama kategori acak
            'is_publish' => $this->faker->boolean, // Menghasilkan nilai true/false secara acak
            'created_at' => now(),
            'updated_at' => now(),
        ];
    }
}
```

### 3. **Membuat Seeder untuk `Category`**

Sekarang, kita akan membuat seeder untuk mengisi tabel `categories` dengan data dari factory. Jalankan perintah berikut untuk membuat seeder:

```bash
php artisan make:seeder CategorySeeder
```

Ini akan membuat file `CategorySeeder.php` di direktori `database/seeders/`.

### 4. **Mengedit Seeder**

Buka file `CategorySeeder.php` di `database/seeders/` dan edit seperti berikut:

```php
<?php

namespace Database\Seeders;

use Illuminate\Database\Seeder;
use App\Models\Category;

class CategorySeeder extends Seeder
{
    /**
     * Run the database seeds.
     */
    public function run(): void
    {
        // Menggunakan factory untuk membuat 100 data kategori
        Category::factory()->count(100)->create();
    }
}
```

### 5. **Menjalankan Seeder**

Untuk menjalankan seeder dan mengisi tabel `categories` dengan 100 data contoh, Anda bisa menjalankan perintah berikut:

```bash
php artisan db:seed --class=CategorySeeder
```

Opsional, jika Anda ingin menjalankan semua seeder sekaligus, Anda bisa mengedit file `DatabaseSeeder.php` untuk memanggil `CategorySeeder`:

```php
public function run()
{
    $this->call(CategorySeeder::class);
}
```

Kemudian jalankan:

```bash
php artisan db:seed
```

### 6. **Menggunakan Database Seeder**

Menjalankan seeder ini akan mengisi tabel `categories` dengan 100 data acak yang dihasilkan oleh Faker, sesuai dengan definisi dalam factory.
![image](https://github.com/user-attachments/assets/f9a8c753-8267-478e-8320-98229d632f34)


## Controller dan Route

Pada bagian ini kita akan membuat controller dan menambahkannya ke route 

### 1. **Buat Controller**
   - Buat controller untuk mengelola API:
     ```bash
     php artisan make:controller CategoryController --resource
     ```
   - Ini akan membuat `CategoryController` dengan metode CRUD (Create, Read, Update, Delete) dasar.

### 2. **Atur Route API**
   - Edit file `bootstrap/app.php` agar mendeklarasikan api.php:
     ```php
     <?php

      use Illuminate\Foundation\Application;
      use Illuminate\Foundation\Configuration\Exceptions;
      use Illuminate\Foundation\Configuration\Middleware;
      
      return Application::configure(basePath: dirname(__DIR__))
          ->withRouting(
              web: __DIR__.'/../routes/web.php',
              api: __DIR__.'/../routes/api.php',//tambahan untuk api
              commands: __DIR__.'/../routes/console.php',
              health: '/up',
              apiPrefix: '/api',//prefix untuk api
          )
          ->withMiddleware(function (Middleware $middleware) {
              //
          })
          ->withExceptions(function (Exceptions $exceptions) {
              //
          })->create();

     ```
   - Buka file `routes/api.php` dan tambahkan route untuk resource `Category`:
     ```php
     <?php

      use Illuminate\Support\Facades\Route;
      use App\Http\Controllers\CategoryController;
      
      Route::apiResource('categories', CategoryController::class);

     ```
   - Route ini secara otomatis akan membuat route untuk GET, POST, PUT, dan DELETE.
   - Untuk mengecek route : `php artisan route:list`

### 3. **Implementasi Metode di Controller**
   - Buka `CategoryController.php` dan implementasikan logika CRUD. Contoh implementasi untuk metode `store` (POST), `index` (GET), dan `update` (PUT):
   - ```php
     use App\Models\Category; // Pastikan Anda mengimpor model Category di sini
     ```

     **GET: Mengambil Data**
     ```php
     public function index()
     {
         return Category::all();
     }
     ```

     **POST: Menambahkan Data**
     ```php
     public function store(Request $request)
     {
         $post = Category::create($request->all());
         return response()->json($post, 201);
     }
     ```

     **PUT: Mengupdate Data**
     ```php
     public function update(Request $request, $id)
     {
         $post = Category::findOrFail($id);
         $post->update($request->all());
         return response()->json($post, 200);
     }
     ```

### 4. **Test API dengan Postman atau Curl**
   - Gunakan Postman atau Curl untuk mengetes API Anda. Misalnya, untuk membuat data baru:
     - Method: `POST`
     - URL: `http://localhost:8000/api/posts`
     - Body: `{"title": "Judul Baru", "content": "Konten baru"}`

### 5. **Jalankan Server**
   - Jalankan server Laravel menggunakan perintah:
     ```bash
     php artisan serve
     ```
   - API akan tersedia di `http://localhost:8000`.

### 6. **Optional: Menambah Middleware untuk Otentikasi**
   - Jika Anda ingin menambahkan otentikasi, Laravel memiliki paket `sanctum` yang sederhana untuk membuat API dengan token otentikasi.



## Catatan tambahan
1. [Membuat model dan migrasi](01.%20Model%20dan%20Migrasi/)
2. [Factory dan Seeder](02.%20Factory%20dan%20Seeder/)
3. Membangun Fungsi CRUD
4. API

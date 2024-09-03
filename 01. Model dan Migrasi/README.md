## Model dan Migration Task
Berikut adalah langkah-langkah untuk membuat model bernama `Category` beserta migration-nya dengan field `id`, `name`, `is_publish` (boolean), `created_at`, dan `updated_at` di Laravel:

### 1. **Membuat Model dan Migration**
Anda dapat membuat model `Category` beserta migration-nya dengan menjalankan perintah Artisan berikut di terminal:

```bash
php artisan make:model Category -m
```

- `-m` adalah opsi yang otomatis akan membuat file migration saat model dibuat.

### 2. **Mengedit Migration**

Setelah menjalankan perintah di atas, Laravel akan membuat dua file:

1. **Model:** `app/Models/Category.php`
2. **Migration:** File migration baru di dalam folder `database/migrations/`.

Buka file migration yang baru saja dibuat. File ini akan terlihat seperti berikut:

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

### 3. **Menjalankan Migration**

Setelah Anda mengedit migration sesuai kebutuhan, jalankan migration tersebut untuk membuat tabel `categories` di database Anda:

```bash
php artisan migrate
```

Perintah ini akan membuat tabel `categories` dengan kolom `id`, `name`, `is_publish`, `created_at`, dan `updated_at`.

### 4. **Model Category**

Secara default, model `Category` akan terlihat seperti berikut:

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Category extends Model
{
    use HasFactory;
    protected $fillable = ['name', 'is_publish'];
}
```

- **`$fillable`**: Properti ini menentukan kolom mana yang bisa diisi secara massal. Anda bisa menambah atau mengurangi kolom yang diizinkan sesuai kebutuhan.

Dengan langkah-langkah ini, Anda telah berhasil membuat model `Category` dan migration yang sesuai. Model ini siap digunakan untuk berinteraksi dengan tabel `categories` di database.
## Mengisi database
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
    protected $model = Category::class;

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

Jika Anda ingin menjalankan semua seeder sekaligus, Anda bisa mengedit file `DatabaseSeeder.php` untuk memanggil `CategorySeeder`:

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
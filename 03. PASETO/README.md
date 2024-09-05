## Generate Key

Anda dapat menjalankan kode tersebut di salah satu tempat berikut di Laravel:

### 1. **Menjalankannya di Tinker:**
Laravel memiliki tool interaktif yang disebut **Tinker** untuk menjalankan PHP di dalam konteks aplikasi Laravel. Anda bisa menggunakan Tinker untuk menjalankan kode secara langsung di command line.

Berikut langkah-langkah untuk menjalankan kode di Tinker:

1. Buka terminal di direktori proyek Laravel Anda.
2. Jalankan perintah berikut untuk membuka Tinker:

   ```bash
   php artisan tinker
   ```

3. Setelah berada di dalam Tinker, tempelkan kode berikut:

   ```php
   use ParagonIE\Paseto\Keys\AsymmetricSecretKey;
   use ParagonIE\Paseto\Protocol\Version4;

   $secretKey = AsymmetricSecretKey::generate(new Version4());
   $publicKey = $secretKey->getPublicKey();

   echo "Private Key: " . base64_encode($secretKey->encode()) . PHP_EOL;
   echo "Public Key: " . base64_encode($publicKey->encode()) . PHP_EOL;
   ```

4. Tinker akan menampilkan private key dan public key dalam format base64. Anda bisa menyalin hasilnya untuk disimpan di file `.env`.

### 2. **Menjalankan Kode dalam Command Line Script Terpisah:**
Jika Anda tidak ingin menggunakan Tinker, Anda bisa membuat script PHP terpisah dan menjalankannya melalui command line.

1. Buat file PHP baru, misalnya `generate_paseto_keys.php`, di dalam root proyek Laravel Anda:

   ```php
   <?php

   require 'vendor/autoload.php';

   use ParagonIE\Paseto\Keys\AsymmetricSecretKey;
   use ParagonIE\Paseto\Protocol\Version4;

   // Membuat kunci privat
   $secretKey = AsymmetricSecretKey::generate(new Version4());
   $publicKey = $secretKey->getPublicKey();

   // Tampilkan kunci privat dan publik
   echo "Private Key: " . base64_encode($secretKey->encode()) . PHP_EOL;
   echo "Public Key: " . base64_encode($publicKey->encode()) . PHP_EOL;
   ```

2. Jalankan file tersebut melalui terminal:

   ```bash
   php generate_paseto_keys.php
   ```

3. Setelah dijalankan, Anda akan melihat private key dan public key ditampilkan di terminal. Salin dan simpan di file `.env` Anda.

### 3. **Menggunakan Controller atau Route Sementara:**
Jika Anda lebih suka menjalankan kode dalam aplikasi Laravel melalui route, Anda dapat menambahkan sementara route di `web.php` dan menampilkan kunci melalui browser.

1. Tambahkan route sementara di `routes/web.php`:

   ```php
   use ParagonIE\Paseto\Keys\AsymmetricSecretKey;
   use ParagonIE\Paseto\Protocol\Version4;

   Route::get('/generate-paseto-keys', function () {
       $secretKey = AsymmetricSecretKey::generate(new Version4());
       $publicKey = $secretKey->getPublicKey();

       return response()->json([
           'private_key' => base64_encode($secretKey->encode()),
           'public_key' => base64_encode($publicKey->encode()),
       ]);
   });
   ```

2. Buka browser dan akses URL berikut:

   ```
   http://localhost:8000/generate-paseto-keys
   ```

3. Anda akan melihat output berupa private key dan public key dalam format JSON. Salin nilai-nilai tersebut ke file `.env`.

### Kesimpulan

Anda dapat menjalankan kode ini di Laravel melalui Tinker, file PHP terpisah, atau bahkan menggunakan route sementara untuk mendapatkan private key dan public key. Setelah kunci dihasilkan, pastikan Anda menyimpannya di file `.env` dengan aman.
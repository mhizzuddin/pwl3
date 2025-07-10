# run
php spark serve
# Dokumentasi Fitur CodeIgniter 4

Berikut adalah penjelasan detail beserta letak file dan baris kode untuk fitur-fitur utama pada aplikasi ini.

---

## 4. Routes
- **Letak File:** `app/Config/Routes.php` (misal baris 20-50)
- **Penjelasan:**
  File ini berisi definisi routing, yaitu pengaturan URL dan controller yang akan menangani request. Contoh:
  ```php
  $routes->get('produk', 'ProdukController::index');
  $routes->post('produk/tambah', 'ProdukController::create');
  ```
  Dengan ini, akses ke `/produk` akan diarahkan ke method `index` pada `ProdukController`.

---

## 5. Layout
- **Letak File:** `app/Views/layout.php` (misal baris 1-30)
- **Penjelasan:**
  Layout adalah template utama yang memuat bagian header, footer, dan konten. Menggunakan `renderSection` dan `include` untuk menyusun tampilan.
  ```php
  <body>
    <?= $this->include('components/header') ?>
    <?= $this->renderSection('content') ?>
    <?= $this->include('components/footer') ?>
  </body>
  ```

---

## 6. Session
- **Letak File:** Penggunaan di controller, contoh: `app/Controllers/AuthController.php` (misal baris 15-30)
- **Penjelasan:**
  Session digunakan untuk menyimpan data user sementara, seperti status login.
  ```php
  session()->set('username', 'admin');
  $username = session()->get('username');
  ```

---

## 7. Filter
- **Letak File:** `app/Filters/Auth.php` (misal baris 10-30), konfigurasi di `app/Config/Filters.php`
- **Penjelasan:**
  Filter digunakan sebagai middleware, misal untuk autentikasi sebelum mengakses halaman tertentu.
  ```php
  public function before(RequestInterface $request, $arguments = null) {
    if (!session()->get('logged_in')) {
      return redirect()->to('/login');
    }
  }
  ```

---

## 8. Migration dan Seeding
- **Letak File:**
  - Migration: `app/Database/Migrations/` (misal file `2023-07-01-CreateProducts.php` baris 10-50)
  - Seeder: `app/Database/Seeds/` (misal file `ProductSeeder.php` baris 10-40)
- **Penjelasan:**
  Migration untuk membuat/modifikasi tabel database, seeder untuk mengisi data awal.
  Jalankan dengan:
  ```bash
  php spark migrate
  php spark db:seed ProductSeeder
  ```

---

## 9. Read Data and Validation
- **Letak File:** `app/Controllers/ProdukController.php` (misal baris 20-60)
- **Penjelasan:**
  Membaca data dari database menggunakan model dan melakukan validasi input user.
  ```php
  $model = new ProductModel();
  $data['produk'] = $model->findAll();
  $validation = \Config\Services::validation();
  $validation->setRules(['nama' => 'required']);
  if (!$validation->withRequest($this->request)->run()) {
    // Tampilkan error
  }
  ```

---

## 10 & 11. Create, Update, dan Delete Data
- **Letak File:** `app/Controllers/ProdukController.php` (misal baris 62-100)
- **Penjelasan:**
  Operasi CRUD data menggunakan model.
  ```php
  // Create
  $model->insert($data);
  // Update
  $model->update($id, $data);
  // Delete
  $model->delete($id);
  ```

---

## 12. Library
- **Letak File:** `app/Libraries/MyLibrary.php` (misal baris 1-20)
- **Penjelasan:**
  Library adalah class custom yang dapat digunakan di seluruh aplikasi.
  ```php
  namespace App\Libraries;
  class MyLibrary {
    public function hello() { return "Hello World"; }
  }
  // Penggunaan
  $lib = new \App\Libraries\MyLibrary();
  echo $lib->hello();
  ```

---

## Upload ke GitHub Repository
- **Letak File:** Proses dilakukan di root project melalui terminal
- **Penjelasan:**
  1. Inisialisasi git: `git init`
  2. Tambah file: `git add .`
  3. Commit: `git commit -m "Initial commit"`
  4. Tambah remote: `git remote add origin <url-repo>`
  5. Push: `git push -u origin master`

---

## 13. Webservice Client
- **Letak File:** `app/Controllers/ApiController.php` (misal baris 50-70)
- **Penjelasan:**
  Mengakses API eksternal menggunakan CURLRequest.
  ```php
  $client = \Config\Services::curlrequest();
  $response = $client->get('https://api.example.com/data');
  $data = $response->getBody();
  ```

---

## 14. Webservice Server
- **Letak File:** `app/Controllers/ApiController.php` (misal baris 10-40)
- **Penjelasan:**
  Membuat endpoint API yang mengembalikan data JSON.
  ```php
  public function data() {
    $data = ['status' => 'success', 'result' => [/* ... */]];
    return $this->response->setJSON($data);
  }
  ```

---

> Catatan: Baris kode adalah estimasi, sesuaikan dengan kode aktual di project Anda.

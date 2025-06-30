#Praktikum one,too,three
# Lab11Web - Praktikum Pemrograman Web

## Informasi Praktikum
- **Nama**: [Dede Syifa Sifriani]
- **NIM**: [312310372]
- **Kelas**: [TI.23.C2]

## Latihan 1: HTML dan CSS Dasar

### Langkah 1: Membuat File HTML
Saya membuat file `index.html` dengan struktur HTML dasar.

### Langkah 2: Menambahkan CSS
Saya membuat file `style.css` untuk styling halaman.

#### Praktikum 1: PHP Framework (CodeIgniter 4)

## Tujuan Praktikum
1. Mahasiswa mampu memahami konsep dasar Framework
2. Mahasiswa mampu memahami konsep dasar MVC
3. Mahasiswa mampu membuat program sederhana menggunakan Framework CodeIgniter 4

## Persiapan

### Tools yang Dibutuhkan
1. Text editor (VSCode)
2. XAMPP Web Server
3. Browser

### Langkah Persiapan
1. Buat folder baru dengan nama `lab11_php_ci` pada docroot webserver (htdocs)
2. Pastikan ekstensi PHP sudah aktif

## Langkah 1: Konfigurasi PHP Extensions

### Ekstensi yang Perlu Diaktifkan:
- `php-json` - untuk bekerja dengan JSON
- `php-mysqlnd` - native driver untuk MySQL
- `php-xml` - untuk bekerja dengan XML
- `php-intl` - untuk aplikasi multibahasa
- `libcurl` - (opsional) untuk Curl

### Cara Mengaktifkan:
1. Buka XAMPP Control Panel
2. Pada bagian Apache, klik **Config** → **PHP.ini**
3. Cari bagian `extension`, hilangkan tanda `;` (titik koma) pada ekstensi yang akan diaktifkan:
   ```ini
   extension=json
   extension=mysqlnd
   extension=xml
   extension=intl
   extension=curl
   ```
4. Simpan file dan restart Apache web server

## Langkah 2: Instalasi CodeIgniter 4

### Download dan Setup:
1. Unduh CodeIgniter dari https://codeigniter.com/download
2. Extract file zip ke direktori `htdocs/lab11_ci`
3. Ubah nama direktori `framework-4.x.xx` menjadi `ci4`
4. Test instalasi dengan membuka browser: `http://localhost/lab11_ci/ci4/public/`

### Struktur Direktori Penting:
```
ci4/
├── app/           # Kode aplikasi yang dikembangkan
├── public/        # File yang bisa diakses publik (index.php, css, js, dll)
├── vendor/        # Library yang dibutuhkan aplikasi
├── writable/      # File yang ditulis aplikasi (upload, logs, session)
└── .env           # Variabel environment
```

## Langkah 3: Menjalankan CLI (Command Line Interface)

### Setup CLI:
1. Buka terminal/command prompt
2. Arahkan ke direktori project: `xampp/htdocs/lab11_ci/ci4/`
3. Jalankan perintah: `php spark`

### Perintah CLI Berguna:
```bash
php spark                    # Menampilkan daftar perintah
php spark routes            # Menampilkan semua route
php spark serve             # Menjalankan development server
```

## Langkah 4: Mengaktifkan Mode Debugging

### Cara Mengaktifkan:
1. Ubah nama file `env` menjadi `.env`
2. Buka file `.env`
3. Ubah nilai variable:
   ```
   CI_ENVIRONMENT = development
   ```
4. Simpan file

### Test Error Handling:
- Coba buat error dengan menghilangkan titik koma di `app/Controllers/Home.php`
- Refresh browser untuk melihat error detail

## Langkah 5: Memahami Konsep MVC

### Model-View-Controller:
- **Model**: Pemodelan data (database, API, dll)
- **View**: Tampilan user interface (HTML, CSS)
- **Controller**: Logic proses yang menghubungkan Model dan View

### Alur Request:
```
Request → Router → Controller → Model/View → Response
```

## Langkah 6: Routing dan Controller

### Membuat Route Baru:
1. Buka file `app/Config/Routes.php`
2. Tambahkan route baru:
   ```php
   $routes->get('/about', 'Page::about');
   $routes->get('/contact', 'Page::contact');
   $routes->get('/faqs', 'Page::faqs');
   ```

### Cek Route:
```bash
php spark routes
```

## Langkah 7: Membuat Controller

### Buat Controller Page:
1. Buat file `app/Controllers/Page.php`
2. Isi dengan kode:
   ```php
   <?php
   namespace App\Controllers;
   
   class Page extends BaseController
   {
       public function about()
       {
           echo "Ini halaman About";
       }
   
       public function contact()
       {
           echo "Ini halaman Contact";
       }
   
       public function faqs()
       {
           echo "Ini halaman FAQ";
       }
   }
   ```

### Test Controller:
- Akses: `http://localhost:8080/about`
- Akses: `http://localhost:8080/contact`
- Akses: `http://localhost:8080/faqs`

## Langkah 8: Auto Routing

### Menggunakan Auto Route:
1. Pastikan auto route aktif di `Routes.php`:
   ```php
   $routes->setAutoRoute(true);
   ```

2. Tambah method baru di Controller Page:
   ```php
   public function tos()
   {
       echo "Ini halaman Terms of Services";
   }
   ```

3. Akses dengan: `http://localhost:8080/page/tos`

## Langkah 9: Membuat View

### Buat File View:
1. Buat file `app/Views/about.php`
2. Isi dengan kode:
   ```php
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <title><?= $title; ?></title>
   </head>
   <body>
       <h1><?= $title; ?></h1>
       <hr>
       <p><?= $content; ?></p>
   </body>
   </html>
   ```

### Update Controller:
```php
public function about()
{
    return view('about', [
        'title' => 'Halaman About',
        'content' => 'Ini adalah halaman about yang menjelaskan tentang isi halaman ini.'
    ]);
}
```

## Langkah 10: Membuat Layout dengan CSS

### Setup CSS:
1. Copy file CSS dari praktikum sebelumnya ke `public/style.css`
2. Buat folder `app/Views/template/`

### Buat Header Template:
File: `app/Views/template/header.php`
```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title><?= $title; ?></title>
    <link rel="stylesheet" href="<?= base_url('/style.css');?>">
</head>
<body>
    <div id="container">
        <header>
            <h1>Layout Sederhana</h1>
        </header>
        <nav>
            <a href="<?= base_url('/');?>" class="active">Home</a>
            <a href="<?= base_url('/artikel');?>">Artikel</a>
            <a href="<?= base_url('/about');?>">About</a>
            <a href="<?= base_url('/contact');?>">Kontak</a>
        </nav>
        <section id="wrapper">
            <section id="main">
```

### Buat Footer Template:
File: `app/Views/template/footer.php`
```php
            </section>
            <aside id="sidebar">
                <div class="widget-box">
                    <h3 class="title">Widget Header</h3>
                    <ul>
                        <li><a href="#">Widget Link</a></li>
                        <li><a href="#">Widget Link</a></li>
                    </ul>
                </div>
                <div class="widget-box">
                    <h3 class="title">Widget Text</h3>
                    <p>Vestibulum lorem elit, iaculis in nisl volutpat, malesuada tincidunt arcu. Proin in leo fringilla, vestibulum mi porta, faucibus felis.</p>
                </div>
            </aside>
        </section>
        <footer>
            <p>&copy; 2021 - Universitas Pelita Bangsa</p>
        </footer>
    </div>
</body>
</html>
```

### Update View About:
File: `app/Views/about.php`
```php
<?= $this->include('template/header'); ?>

<h1><?= $title; ?></h1>
<hr>
<p><?= $content; ?></p>

<?= $this->include('template/footer'); ?>
```

## Tugas

### Lengkapi Menu Lainnya:
1. Buat view untuk `contact.php` dan `faqs.php`
2. Update method di Controller Page untuk menggunakan view
3. Pastikan semua link navigasi berfungsi dengan layout yang sama

### Contoh untuk Contact:
```php
// Di Controller Page
public function contact()
{
    return view('contact', [
        'title' => 'Halaman Kontak',
        'content' => 'Ini adalah halaman kontak untuk menghubungi kami.'
    ]);
}
```

```php
// File app/Views/contact.php
<?= $this->include('template/header'); ?>

<h1><?= $title; ?></h1>
<hr>
<p><?= $content; ?></p>

<?= $this->include('template/footer'); ?>
```

## Tips Debugging

### Error Umum:
1. **404 Not Found**: Controller atau method tidak ditemukan
2. **500 Internal Server Error**: Syntax error dalam kode
3. **CSS tidak load**: Periksa path di `base_url()`

### Perintah Berguna:
```bash
php spark routes          # Cek semua route
php spark serve          # Run development server
php spark cache:clear    # Clear cache
```

## Laporan Praktikum

1. Buat repository baru dengan nama **Lab7Web**
2. Kerjakan semua latihan sesuai urutan
3. Screenshot setiap perubahan
4. Buat file README.md dengan penjelasan setiap langkah
5. Commit hasil ke repository
6. Kirim URL repository ke e-learning

---



### Hasil:
[Screenshot hasil ada disetiap latihan]

## Latihan 2: []
[# Praktikum 2: Framework Lanjutan (CRUD) - CodeIgniter 4

**Mata Kuliah:** Pemrograman Web 2  
**Dosen:** Agung Nugroho (agung@pelitabangsa.ac.id)  
**Universitas:** Pelita Bangsa, Bekasi

## 📋 Tujuan Praktikum

1. Memahami konsep dasar Model dalam CodeIgniter 4
2. Memahami konsep dasar CRUD (Create, Read, Update, Delete)
3. Membuat program sederhana menggunakan Framework CodeIgniter 4

## 🛠️ Persiapan

### Tools yang Dibutuhkan:
- Text Editor (VSCode)
- XAMPP (MySQL Server)
- Web Browser
- CodeIgniter 4

### Struktur Folder:
```
lab7_php_ci/
├── app/
│   ├── Controllers/
│   ├── Models/
│   ├── Views/
│   └── Config/
├── public/
└── .env
```

## 📊 Database Setup

### 1. Membuat Database
```sql
CREATE DATABASE lab_ci4;
```

### 2. Membuat Tabel Artikel
```sql
CREATE TABLE artikel (
    id INT(11) auto_increment,
    judul VARCHAR(200) NOT NULL,
    isi TEXT,
    gambar VARCHAR(200),
    status TINYINT(1) DEFAULT 0,
    slug VARCHAR(200),
    PRIMARY KEY(id)
);
```

### 3. Sample Data
```sql
INSERT INTO artikel (judul, isi, slug) VALUES
('Artikel pertama', 'Lorem Ipsum adalah contoh teks atau dummy dalam industri percetakan dan penataan huruf atau typesetting. Lorem Ipsum telah menjadi standar contoh teks sejak tahun 1500an, saat seorang tukang cetak yang tidak dikenal mengambil sebuah kumpulan teks dan mengacaknya untuk menjadi sebuah buku contoh huruf.', 'artikel-pertama'),
('Artikel kedua', 'Tidak seperti anggapan banyak orang, Lorem Ipsum bukanlah teks-teks yang diacak. Ia berakar dari sebuah naskah sastra latin klasik dari era 45 sebelum masehi, hingga bisa dipastikan usianya telah mencapai lebih dari 2000 tahun.', 'artikel-kedua');
```

## ⚙️ Konfigurasi

### Database Configuration (.env)
```env
database.default.hostname = localhost
database.default.database = lab_ci4
database.default.username = root
database.default.password = 
database.default.DBDriver = MySQLi
```

## 🏗️ Implementasi CRUD

### 1. Model (ArtikelModel.php)
```php
<?php
namespace App\Models;
use CodeIgniter\Model;

class ArtikelModel extends Model
{
    protected $table = 'artikel';
    protected $primaryKey = 'id';
    protected $useAutoIncrement = true;
    protected $allowedFields = ['judul', 'isi', 'status', 'slug', 'gambar'];
}
```

### 2. Controller (Artikel.php)
Controller berisi method-method untuk:
- `index()` - Menampilkan daftar artikel
- `view($slug)` - Menampilkan detail artikel
- `admin_index()` - Menampilkan halaman admin
- `add()` - Menambah artikel baru
- `edit($id)` - Mengubah artikel
- `delete($id)` - Menghapus artikel

### 3. Views
- `artikel/index.php` - Tampilan daftar artikel untuk user
- `artikel/detail.php` - Tampilan detail artikel
- `artikel/admin_index.php` - Tampilan admin panel
- `artikel/form_add.php` - Form tambah artikel
- `artikel/form_edit.php` - Form edit artikel

### 4. Routing (Routes.php)
```php
// Public routes
$routes->get('/artikel', 'Artikel::index');
$routes->get('/artikel/(:any)', 'Artikel::view/$1');

// Admin routes
$routes->group('admin', function($routes) {
    $routes->get('artikel', 'Artikel::admin_index');
    $routes->add('artikel/add', 'Artikel::add');
    $routes->add('artikel/edit/(:any)', 'Artikel::edit/$1');
    $routes->get('artikel/delete/(:any)', 'Artikel::delete/$1');
});
```

## 📸 Screenshots

### 1. Tampilan Awal (Belum Ada Data)
![Tampilan Web Kosong](screenshot/tampilan-kosong.png)
*Tampilan web ketika belum ada data artikel*

### 2. Daftar Artikel
![Daftar Artikel](screenshot/daftar-artikel.png)
*Tampilan daftar artikel setelah data ditambahkan*

### 3. Detail Artikel
![Detail Artikel](screenshot/detail-artikel.png)
*Tampilan detail artikel ketika judul diklik*

### 4. Admin Panel
![Admin Panel](screenshot/admin-panel.png)
*Tampilan halaman admin untuk mengelola artikel*

### 5. Form Tambah Artikel
![Form Tambah](screenshot/form-tambah.png)
*Form untuk menambah artikel baru*

### 6. Form Edit Artikel
![Form Edit](screenshot/form-edit.png)
*Form untuk mengubah artikel yang sudah ada*

## 🚀 Cara Menjalankan

1. **Clone Repository**
   ```bash
   git clone [URL_REPOSITORY]
   cd Lab7Web
   ```

2. **Setup Database**
   - Jalankan XAMPP
   - Buat database `lab_ci4`
   - Import struktur tabel dan sample data

3. **Konfigurasi Environment**
   - Copy `.env.example` ke `.env`
   - Sesuaikan konfigurasi database

4. **Jalankan Aplikasi**
   ```bash
   php spark serve
   ```

5. **Akses Aplikasi**
   - User: `http://localhost:8080/artikel`
   - Admin: `http://localhost:8080/admin/artikel`

## 🔧 Fitur CRUD

### Create (Tambah)
- Form tambah artikel dengan validasi
- Auto-generate slug dari judul
- Redirect ke halaman admin setelah berhasil

### Read (Baca)
- Tampilan daftar artikel dengan preview
- Detail artikel dengan slug-based URL
- Paginasi untuk data banyak

### Update (Ubah)
- Form edit dengan data yang sudah ada
- Validasi input
- Update data ke database

### Delete (Hapus)
- Konfirmasi sebelum menghapus
- Soft delete atau hard delete
- Redirect setelah berhasil hapus

## 📝 Validasi

- **Judul:** Required field
- **Isi:** Opsional
- **Slug:** Auto-generate dari judul
- **Status:** Default 0

## 🔍 Struktur MVC

```
Model (ArtikelModel)
├── Database interaction
├── Data validation rules
└── Business logic

View (Templates)
├── artikel/index.php
├── artikel/detail.php
├── artikel/admin_index.php
├── artikel/form_add.php
└── artikel/form_edit.php

Controller (Artikel)
├── index() - List articles
├── view() - Show detail
├── admin_index() - Admin panel
├── add() - Create article
├── edit() - Update article
└── delete() - Remove article
```

## 🎯 Hasil yang Dicapai

✅ Berhasil membuat aplikasi CRUD sederhana  
✅ Implementasi Model-View-Controller  
✅ Database integration dengan MySQL  
✅ Form validation  
✅ Routing configuration  
✅ User-friendly interface  
✅ Admin panel untuk manajemen konten  



## Latihan 3: [Judul Latihan 3]
[Akan diisi setelah mengerjakan latihan 3]

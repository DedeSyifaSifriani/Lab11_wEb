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

## Checklist Praktikum

- [ ] Konfigurasi PHP extensions
- [ ] Install CodeIgniter 4
- [ ] Setup CLI dan debugging mode
- [ ] Buat route baru
- [ ] Buat Controller Page
- [ ] Test auto routing
- [ ] Buat view dengan template
- [ ] Implementasi layout CSS
- [ ] Lengkapi semua menu navigasi
- [ ] Dokumentasi dan screenshot
- [ ] Upload ke repository

### Hasil:
[Screenshot hasil ada disetiap latihan]

## Latihan 2: []
[Akan diisi setelah mengerjakan latihan 2]

## Latihan 3: [Judul Latihan 3]
[Akan diisi setelah mengerjakan latihan 3]

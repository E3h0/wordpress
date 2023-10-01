<h1 align="center"><img src="https://s.w.org/style/images/about/WordPress-logotype-alternative-white.png"></h1>

[Sekilas Tentang](#sekilas-tentang) | [Instalasi](#instalasi) | [Konfigurasi](#konfigurasi) | [Otomatisasi](#otomatisasi) | [Cara Pemakaian](#cara-pemakaian) | [Pembahasan](#pembahasan) | [Referensi](#referensi)
:---:|:---:|:---:|:---:|:---:|:---:|:---:



# Sekilas Tentang

WordPress adalah proyek *Content Management System* (*CMS*) bersifat *Open Source* yang di desain sedemikian rupa untuk semua orang. Orang-orang dengan pengalaman teknologi terbatas dapat menggunakan WordPress secara “*out of the box*”, dan orang-orang yang lebih paham teknologi dapat menyesuaikan WordPress dengan cara yang luar biasa. WordPress berbasiskan PHP, MySQL dan JavaScript, serta menggunakan Node untuk dependensi JavaScript-nya. 


# Instalasi 

Dalam menginstall akan lebih baik jika memahami dasar tentang cara menggunakan *command* di komputer/Laptop. Hal tersebut akan memudahkan untuk mengatur lingkungan pengembangan lokal, memulai dan menghentikannya bila diperlukan, dan menjalankan rangkaian *test*.

### Kebutuhan Sistem :
- [Node.js](https://nodejs.org/en) V16.x (*JavaScript runtime environment*)
- Npm V8.x
- [PHP](https://www.php.net/) V7.4+ 
- [MySQL](https://www.mysql.com/) V5.7+ atau [MariaDB](https://mariadb.org/) V10.4+
- [Apache](https://httpd.apache.org/) atau [Nginx](https://nginx.org/) terbaru
- [Docker](https://www.docker.com/products/docker-desktop/) (*virtualization local Dev Env*)

### Proses Instalasi :
1. Pastikan Docker dalam keadaan sudah berjalan
2. Clone repository dengan
   
    ```
    git clone https://github.com/WordPress/wordpress-develop.git
    ```
3. Masuk ke folder repository
   
   ```
   cd wordpress-develop
   ```
4. Selanjutnya, jalankan *command* berikut dan tunggu hingga semua prosesnya benar-benar sudah selesai
   ```
   npm install
   npm run build:dev
   npm run env:start
   npm run env:install
   ```
5. Jika langkah demi langkah sudah dilakukan dengan benar, pada tahap ini WordPress *CMS* sudah dapat diakses di [localhost:8889](http://localhost:8889)


# Konfigurasi

Salah satu file terpenting dalam instalasi WordPress adalah file `wp-config.php`. File ini terletak di root direktori file WordPress dan berisi detail konfigurasi dasar situs web, seperti informasi koneksi database.

### table_prefix
Adalah nilai yang ditempatkan di bagian depan tabel basis data. Ubah nilainya jika ingin menggunakan nama selain `wp_` untuk awalan databas. Biasanya diubah jika menginstal beberapa blog WordPress dalam database yang sama, seperti yang dilakukan dengan fitur multisite.
```
table_prefix = 'example123_'; // Only numbers, letters, and underscores please!
```

### WP_SITEURL
Digunakan untuk menentukan alamat (*URL*) WordPress. Nilai yang dimasukkan adalah alamat tempat file-file inti WordPress berada. Alamat harus menyertakan bagian `http://`. Jangan gunakan tanda `/` di bagian akhir. Menambahkan nilai pada `WP_SITEURL` dapat mengurangi jumlah pemanggilan database saat memuat situs. 

Jika WordPress diinstal ke dalam direktori bernama `wordpress` untuk domain `example.com`, maka nilai `WP_SITEURL`
```
define( 'WP_SITEURL', 'https://example.com/wordpress' );
```
Mengatur `WP_SITEURL` secara dinamis berdasarkan `$_SERVER['HTTP_HOST']`
```
define( 'WP_SITEURL', 'https://' . $_SERVER['HTTP_HOST'] . '/path/to/wordpress' );
```
Mengatur `WP_SITEURL` secara dinamis berdasarkan `$_SERVER['NAMA_SERVER']`
```
define( 'WP_SITEURL', 'http://' . $_SERVER['SERVER_NAME'] . '/path/to/wordpress' );
```


Plugin untuk fungsi tambahan
- login dengan Google/Facebook
- editor Markdown
- dll


##  Maintenance (opsional)

Setting tambahan untuk maintenance secara periodik, misalnya:
- buat backup database tiap pekan
- hapus direktori sampah tiap hari
- dll


## Otomatisasi (opsional)

Skrip shell untuk otomatisasi instalasi, konfigurasi, dan maintenance.


## Cara Pemakaian

- Tampilan aplikasi web
- Fungsi-fungsi utama
- Isi dengan data real/dummy (jangan kosongan) dan sertakan beberapa screenshot


## Pembahasan

- Pendapat anda tentang aplikasi web ini
    - kelebihan
    - kekurangan
- Bandingkan dengan aplikasi web lain yang sejenis


## Referensi

Cantumkan tiap sumber informasi yang anda pakai.

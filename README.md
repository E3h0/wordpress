<h1 align="center"><img src="https://s.w.org/style/images/about/WordPress-logotype-alternative-white.png"></h1>

- [Sekilas Tentang](#sekilas-tentang)
- [Instalasi](#instalasi)
- [Konfigurasi](#konfigurasi)
- [Maintenance](#maintenance)
- [Otomatisasi](#otomatisasi)
- [Cara Pemakaian](#cara-pemakaian)
- [Pembahasan](#pembahasan)
- [Referensi](#referensi)




# Sekilas Tentang 
[`kembali ke atas ↑`](#)

WordPress adalah proyek *Content Management System* (*CMS*) bersifat *Open Source* yang di desain sedemikian rupa untuk semua orang. WordPress dimulai/dibangun pada tahun 2003 ketika Mike Little dan Matt Mullenweg menciptakan sebuah fork dari [b2/cafelog](https://cafelog.com/). Hal tersebut didasari oleh adanya kebutuhan akan sistem penerbitan personal yang elegan dan dirancang dengan baik pada saat itu. WordPress dibangun menggunakan PHP dan MySQL, dan dilisensikan di bawah GPLv2. Pada saat ini WordPress juga merupakan platform pilihan untuk lebih dari 43% dari semua situs di seluruh web. Orang-orang dengan pengalaman teknologi terbatas dapat menggunakan WordPress secara “*out of the box*”, dan orang-orang yang lebih paham teknologi dapat menyesuaikan WordPress dengan cara yang luar biasa. WordPress berbasiskan PHP, MySQL dan JavaScript, serta menggunakan Node untuk dependensi JavaScript-nya. 


# Instalasi 
[`kembali ke atas ↑`](#)

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
[`kembali ke atas ↑`](#)

Salah satu file terpenting dalam instalasi WordPress adalah file `wp-config.php`. File ini terletak di root direktori file WordPress dan berisi detail konfigurasi dasar situs web, seperti informasi koneksi database.

### table_prefix
Adalah nilai yang ditempatkan di bagian depan tabel basis data. Ubah nilainya jika ingin menggunakan nama selain `wp_` untuk awalan database. Biasanya diubah jika menginstal beberapa blog WordPress dalam database yang sama, seperti yang dilakukan dengan fitur multisite.
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

### Blog Address (URL) / WP_HOME
Digunakan untuk mengatur *URL* home. Home adalah alamat yang nantinya akan diketikkan oleh orang-orang di browser mereka untuk mencapai blog WordPress. Alamat ini harus menyertakan bagian `http://` dan tidak boleh ada garis miring `/` di bagian akhir. Menambahkan ini dapat mengurangi jumlah pemanggilan database saat memuat situs.
```
define( 'WP_HOME', 'http://example.com/wordpress' );
```
Jika enempatkan index.php di direktori web-root, maka dapat menggunakan konfigurasi berikut
```
define( 'WP_HOME', 'http://example.com' );
```
Mengatur `WP_HOME` secara dinamis berdasarkan `$_SERVER['HTTP_HOST']`
```
define( 'WP_HOME', 'http://' . $_SERVER['HTTP_HOST'] . '/path/to/wordpress' );
```

### Database Username
Mengatur username yang akan digunakan pada database
```
define( 'DB_USER', 'root' );
```

### Database Password
Mengatur password yang akan digunakan pada database
```
define( 'DB_PASSWORD', 'password' );
```

### Database hostname
Mengatur nama host pada database
```
define( 'DB_HOST', 'mysql' );
```

#  Maintenance
[`kembali ke atas ↑`](#)

### Quick Backup
Mencadangkan semua tabel di database WordPress tanpa kompresi, dengan menggunakan metode sederhana.
1. Login ke PhpMyadmin di server
2. Dari jendela sebelah kiri, pilih database WordPress. Dalam contoh ini, nama database adalah "wp"
3. Jendela sebelah kanan akan menampilkan semua tabel di dalam database WordPress. Klik tab `Eksport` pada tab atas.

![Backup](https://wordpress.org/documentation/files/2018/11/phpmyadmin_dbtop.jpg)

4.  Pastikan opsi `Quick` dipilih, klik `Go` dan file backup pun akan mulai diunduh. Simpan file ke komputer. Tergantung pada ukuran basis data, proses ini mungkin memerlukan waktu beberapa saat.

### Restoring Hasil Backup
1. Login ke PhpMyadmin di server
2. Klik `Database` dan pilih database yang akan digunakan untuk mengimpor data 
3. Kemudian akan ditampilkan daftar tabel yang sudah ada di dalam database tersebut
4. Di bagian atas layar akan ada deretan tab. Klik tab `Import`.

![dblist](https://github.com/E3h0/wordpress/blob/f701a1722d88948a76c3b7d8150a31f373da4ed8/Screenshot/Screenshot%202023-10-02%20075551.png)  

5. Pada layar berikutnya klik `Choose File` untuk mencari file backup yang akan di impor
6. Di bagian format pastikan `SQL` dipilih
7. Klik toombol `Import`

![importing](https://github.com/E3h0/wordpress/blob/f701a1722d88948a76c3b7d8150a31f373da4ed8/Screenshot/Screenshot%202023-10-02%20075743.png)

# Otomatisasi 
[`kembali ke atas ↑`](#)

Dalam menginstall Wordpress, sebenarnya ada cara lain yang lebih mudah yakni dengan menggunakan *service* yang sudah disediakan oleh *web hosting* terkait. Proses instalasi nya jauh lebih mudah karena dapat dilakukan *by click* dan tidak perlu memasukkan baris-baris command seperti cara sebelumnya. Berikut ini adalah langkah-langkah untuk install wordpress menggunakan layanan *auto installer* dari [Softaculus](https://www.softaculous.com/apps/blogs/WordPress)
1. Kunjungi website [Softaculus](https://www.softaculous.com/apps/blogs/WordPress) dan cari `Wordpress`
2. Pilih opsi Quickly Install with Softaculous Cloud

![install](https://github.com/E3h0/wordpress/blob/51f3bdefad866486c1a050f6242e01f20aae7c18/Screenshot/Screenshot%202023-10-02%20083743.png)

3. Isi semua Informasi yang diminta seperti domain, autentikasi dan pastikan semuanya sudah lengkap dan benar
4. Tunggu proses instalasi hingga selesai.
   
# Cara Pemakaian
[`kembali ke atas ↑`](#)

Wordpress merupakan *CMS* yang *user friendly* untuk semua orang. Cara pemakaian nya pun terbilang cukup sederhana dan mudah dilakukan. Berikut adalah langkah-langkahnya
1. Login ke dashboard dari Wordpress dengan mengunjungi  [localhost:8889/wp-admin](http://localhost:8889/wp-admin)
2. Masukkan `Username` & `password`. Secara default usernamenya adalah `admin` & passwordnya adalah `password`.
 
![login](https://github.com/E3h0/wordpress/blob/75ca041c815c05cd1098b4f84c94c543fd314ec4/Screenshot/Screenshot%202023-10-02%20084940.png)

3. Klik Login dan selanjutnya akan diarahkan pada halaman dashboard dari wordpress
   
![dboard](https://github.com/E3h0/wordpress/blob/481722fd2b45004ea0fa9d2a0bc295165daed439/Screenshot/Screenshot%202023-10-02%20085706.png)

4. Dashboard tersebut menampilkan berbagai menu dan beberapa informasi penting terkait situs seperti status *health* dari situs dan juga *quick draft*
5. Di jendela kiri terdapat berbagai macam menu yang dapat diakses untuk keperluan tertentu. Menu `Posts` berfungsi untuk mengelola post seperti membuat post baru, mengedit, melakukan kategorisasi dan juga menambahkan tag
   
![Posts](https://github.com/E3h0/wordpress/blob/4dc92e09f2b1b719629b589df96b1510213af90c/Screenshot/Screenshot%202023-10-02%20090444.png)

6. Menu `Media` berfungsi untuk mengelola media pada situs, seperti menambahkan/menghapus media dan melakukan pengelompokan media.

![Media](https://github.com/E3h0/wordpress/blob/0c4f71ff6f6e318f650e7a84cebcea658e0295f4/Screenshot/Screenshot%202023-10-02%20090856.png)

7. Menu `Pages` berfungsi untuk mengelola halaman, seperti menambahkan halaman baru, membuat template dan mengedit halaman.

![halaman](https://github.com/E3h0/wordpress/assets/101927398/0f61baf2-df6c-4204-b5db-b1acef833781)

8. Menu `Comments` berfungsi untuk mengelola dan melihat komentar yang ada ataupun masuk ke situs.

![komentar](https://github.com/E3h0/wordpress/blob/7ed91718a3d871d6a8e10d0ae853f12c5ca65edf/Screenshot/Screenshot%202023-10-02%20091725.png)

9. Menu `Appearance` berfungsi untuk mengelola dan melakukan edit pada tema yang digunakan pada situs.

![tema](https://github.com/E3h0/wordpress/blob/5fd2139f75886714dc2f7aee0ec68f587266cc1b/Screenshot/Screenshot%202023-10-02%20092124.png)

10. Menu `Plugins` berfungsi untuk mengelola plugin seperti menambahkan plugin baru dan mengupdate plugin yang sudah ada.

![plugin](https://github.com/E3h0/wordpress/blob/39bf94b24091924733969f0cd953371e3738a267/Screenshot/Screenshot%202023-10-02%20092440.png)

11. Menu `Users` berfungsi untuk mengelola user/pengguna pada situs seperti menambahkan user baru dan menghapus user.

![user](https://github.com/E3h0/wordpress/blob/d66ba8acbf51e382486bdd3cfa998aa069a0c0d1/Screenshot/Screenshot%202023-10-02%20092902.png)

12. Menu `Tools` digunakan untuk mengelola utilitas terkait situs seperti melakukan impor/ekspor post & comment dari sumber lain, melakukan pengecekan status kesehatan situs, ekspor data pribadi, melakukan edit tema dan plugin.

![tools](https://github.com/E3h0/wordpress/blob/7d45029dd1d81681a6b50e7a002420531eefea70/Screenshot/Screenshot%202023-10-02%20093327.png)

13. Menu `Settings` digunakan untuk melakukan pengaturan pada *CMS* Wordpress seperti mengatur alamat situs, alamat wordpress, format penanggalan, privasi dan permalink

![settings](https://github.com/E3h0/wordpress/blob/033aef591c90ad7a7e3f937106d963b4f1abf16b/Screenshot/Screenshot%202023-10-02%20093721.png)

Berikut ini contoh ketika melakukan edit pada halaman

![halaman](https://github.com/E3h0/wordpress/blob/c1c3c0b11542056baad4137065647bcca745c05a/Screenshot/Screenshot%202023-10-02%20094247.png)

Berikut ini contoh ketika melakukan edit pada tema halaman 

![tema](https://github.com/E3h0/wordpress/blob/0aa23d861a964b79ad23217369120d6af9e28cc7/Screenshot/Screenshot%202023-10-02%20094908.png)

# Pembahasan
[`kembali ke atas ↑`](#)




Proyek open source WordPress telah berkembang secara progresif dari waktu ke waktu-didukung oleh para pengembang, desainer, ilmuwan, blogger, dan banyak lagi. WordPress memberikan kesempatan bagi siapa saja untuk membuat dan berbagi, mulai dari kebutuhan pribadi yang sederhana hingga kebutuhan/ide besar yang mengubah dunia.




## Referensi

Cantumkan tiap sumber informasi yang anda pakai.

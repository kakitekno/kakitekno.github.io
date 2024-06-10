---
layout: post
title: Cara Mudah Memasang Wordpress Bagi Pemula
author: Amir Zulkarnain
excerpt_image: /assets/images/blog/wordpress-install/wordpress_banner.jpg
categories: tutorial
tags: [wordpress, tutorial]
---

![banner](/assets/images/blog/wordpress-install/wordpress_banner.jpg)

Anda ingin mempunyai website sendiri menggunakan Wordpress? Tapi tak faham macam mana cara mudah untuk install Wordpress. Dalam tutorial ini, saya akan guide anda untuk install Wordpress dengan cara yang mudah difahami. Tutorial ini menggunakan Ubuntu Server 22.04 (Jammy Jellyfish). Anda juga boleh menggunakan versi Ubuntu atau Debian yang lain dan sewaktu dengannya.

# Langkah-langkah untuk install Wordpress di Ubuntu 22.04

[1. Update Dan Upgrade Sistem](#update-dan-upgrade-ubuntu)<br>
[2. Memasang Apache](#memasang-apache)<br>
[3. Memasang PHP & Component](#memasang-php-dan-component)<br>
[4. Memasang MySQL Server serta mysql_secure_installation](#memasang-mysql-server)<br>
[5. Bina DB untuk Wordpress](#mencipta-pangkalan-data-wordpress)<br>
[6. Memuat Turun Wordpress](#memuat-turun-wordpress)<br>
[7. Konfigurasi Fail Wordpress](#konfigurasi-fail-wordpress)<br>
[8. Memasang Wordpress](#memasang-wordpress)<br>

## Update dan Upgrade Ubuntu

Pertama sekali, update dahulu Ubuntu server yang akan digunakan untuk install Wordpress. Ini bagi memastikan package yang akan digunakan adalah yang terkini.

```shell
sudo apt update && sudo apt upgrade -y
```

## Memasang Apache

Apache adalah elemen penting dalam Wordpress kerana ia menjadi [HTTP server](https://httpd.apache.org/) yang akan menghidupkan Wordpress. Kita juga perlu mengaktifkan Apache menggunakan command [enable](https://documentation.suse.com/smart/systems-management/html/reference-systemctl-enable-disable-services/index.html) supaya Apache akan start on boot.

```
sudo apt install apache2 -y
sudo systemctl enable apache2
sudo systemctl start apache2
```

## Memasang PHP dan Component

PHP adalah enjin yang akan menggerakkan fungsi fungsi dalaman didalam Wordpress. Jadi penting untuk kita install PHP dengan versi paling baru dan semua perkakasan PHP.

```
sudo apt install php -y
```

Component PHP

```
sudo apt install libapache2-mod-php php-mysql php-curl php-gd php-mbstring php-xml php-xmlrpc php-soap php-intl php-zip -y
```

Apa fungsi semua ni?

<ul>
  <li><b>libapache2-mod-php: </b>Integrasi PHP dan Apache.</li> 
  <li><b>php-mysql: </b>Integrasi PHP dan MySQL</li>
  <li><b>php-curl: </b>Digunakan supaya PHP dapat menggunakan curl.</li>
  <li><b>php-gd: </b>Graphic Library untuk PHP.</li>
  <li><b>php-mbstring: </b>Mengendalikan bahasa atau huruf yang bukan latin.</li>
  <li><b>php-xml: </b>XML support untuk PHP</li>
  <li><b>php-xmlrpc: </b>Support XML untuk (Remote Procedure Call)</li>
  <li><b>php-soap: </b>Support PHP untuk (Simple Object Access Protocol)</li>
  <li><b>php-intl: </b>Membantu features internationalization</li>
  <li><b>php-zip: </b>Mengedit ZIP</li>
</ul> 

## Memasang MySQL Server

MySQL adalah pengurus pangkalan data di mana semua data data akan diletakkan di dalam database MySQL. Wordpress memerlukan satu database untuk berfungsi.

```
sudo apt install mysql-server -y
```

Setelah memasang MySQL, kita perlu melakukan pemasangat selamat MySQL suupaya ia dapat digunakan dengan baik dan selamat.

```
sudo mysql_secure_installation
```

Terdapat beberapa soalan yang perlu dijawab, ikuti langkah di bawah.

<b>1. Kita boleh menukar password atau mengekalkan password asal. Tekan apa apa butang untuk kekalkan password asal.</b>

<img src="/assets/images/blog/wordpress-install/mysql1.png" alt="reset mysql password" width="80%" height="80%">

<b>2. Tekan "y" untuk membuang anonymous user.</b>

<img src="/assets/images/blog/wordpress-install/mysql2.png" alt="anonymous user" width="80%" height="80%">

<b>3. Tekan "y" untuk menutup akses login root dari rangkaian luar selain localhost. Ini bagi mencegah cubaan akses yang tidak dikehendaki dari luar.</b>

<img src="/assets/images/blog/wordpress-install/mysql3.png" alt="root access" width="80%" height="80%">

<b>4. Tekan "y" untuk membuang database test. Database ini hanyalah untuk menguji samada MySQL berjaya dipasang atau tidak.</b>

<img src="/assets/images/blog/wordpress-install/mysql4.png" alt="database test" width="80%" height="80%">

<b>5. Tekan "y" untuk memuat semula dan mengemaskini privilege tables dalam MySQL.</b>

<img src="/assets/images/blog/wordpress-install/mysql5.png" alt="privilege table" width="80%" height="80%">

## Mencipta pangkalan data Wordpress

Setelah melakukan installation MySQL, kita boleh login ke MySQL untuk membuat pangkalan data (database) bagi Wordpress, pengguna (user) Wordpress dan konfigurasi kebenaran kepada database.
```
sudo mysql -u root -p
```

Pertama sekali kita akan membuat sebuah database baharu bernama "wordpress".
```
CREATE DATABASE wordpress;
```

Ciptakan satu pengguna baharu bernama "wp_user" yang akan digunakan bagi mengawal pangkalan data. Ubah 'password' kepada kata laluan yang selamat.
```
CREATE USER 'wp_user'@'localhost' IDENTIFIED BY 'password';
```

Kita akan memberikan kebenaran pengguna "wp_user" kepada database wordpress yang telah dicipta sebentar tadi. 
```
GRANT ALL PRIVILEGES ON wordpress.* TO 'wp_user'@'localhost';
```

"Flush Privileges" digunakan untuk mengemas kini privileges tables dalam MySQL.
```
FLUSH PRIVILEGES;
```

Setelah selesai, kita boleh keluar dari MySQL.
```
EXIT;
```

## Memuat turun Wordpress

Setelah kita menyediakan database bagi Wordpress, seterusnya kita akan memuat turun Wordpress bagi dipasang di dalam server.

Kita akan melakukan pemasangan Wordpress di /var/www/html iaitu direktori penggunaan Apache.
```
cd /var/www/html
```

Muat turun pakej Wordpress yang terbaru.
```
sudo wget http://wordpress.org/latest.tar.gz
```

Ekstrak semua fail di dalam latest.tar.gz dan fail-fail tersebut akan diletakkan di dalam direktori bernama wordpress.
```
sudo tar -xzvf latest.tar.gz
```

Kita boleh membuat fail ekstrak setelah selesai mengekstrak semua kandungan di dalamnya.
```
sudo rm latest.tar.gz
```

## Konfigurasi Fail Wordpress

Cipta direktori muat naik.
```
sudo mkdir /var/www/html/wordpress/wp-content/uploads
```

Mengubah pemilik direktori wordpress.
```
sudo chown -R www-data:www-data /var/www/html/wordpress/
```

Mengubah kebenaran direktori wordpress.
```
sudo chmod -R 755 /var/www/html/wordpress/
```

## Memasang Wordpress

Setelah selesai konfigurasi fail Wordpress, kita boleh memulakan pemasangan Wordpress. Buka pelayan web (Browser) dan akses halaman Wordpress menggunakan IP address server.
```
http://127.0.0.1/wordpress
```

**Pilih bahasa pemasangan.**

<img src="/assets/images/blog/wordpress-install/language_installation.png" alt="memilih bahasa">

**Tekan Let's Go di halaman mula bagi memulakan pemasangan Wordpress.**

<img src="/assets/images/blog/wordpress-install/halaman_mula.png" alt="halaman mula" width="80%" height="80%">

**Isi maklumat berkaitan database yang telah dikonfigurasi di dalam MySQL.**
1. Nama Database: wordpress
2. Nama Pengguna: wp_user
3. Password: kata laluan yang telah ditetapkan
4. Database Host: localhost
5. Table Prefix: wp_

<img src="/assets/images/blog/wordpress-install/database_details.png" alt="database detail" width="80%" height="80%">

**Gambar di bawah menunjukkan database berjaya dikesan oleh Wordpress, maka kita boleh memulakan installation. Jika database tidak berjaya dikesan, periksa semula konfigurasi yang dimasukkan di halaman sebelum dan di dalam MySQL. Pastikan konfigurasi yang digunakan adalah sama.**

<img src="/assets/images/blog/wordpress-install/database_success.png" alt="db success" width="80%" height="80%">

**Isikan maklumat berkenaan website mengikut keinginan anda. Setelah maklumat dimasukkan, Wordpress sudah siap dipasang.**

<img src="/assets/images/blog/wordpress-install/installation.png" alt="db success" width="80%" height="80%">

## Mengakses Wordpress

Setelah Wordpress berjaya dipasang, anda kini boleh mengakses Wordpress dengan log masuk di URL berikut.

```
http://127.0.0.1/wordpress/wp-admin/
```
<img src="/assets/images/blog/wordpress-install/login.png" alt="db success">

Tahniah, Anda berjaya memasang Wordpress di dalam server Ubuntu anda sendiri. :)
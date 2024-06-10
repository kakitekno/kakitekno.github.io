---
layout: post
title: Belajar Menggunakan Burp Suite
author: Amir Zulkarnain
excerpt_image: /assets/images/blog/cara-guna-burpsuite/banner.jpg
categories: tutorial
tags: [pentest, tutorial]
---

![banner](/assets/images/blog/cara-guna-burpsuite/banner.jpg)

Burp Suite adalah alatan yang tidak asing lagi dalam kalangan Penetration Tester. Burp Suite adalah sebuah alatan komprehensif yang biasa digunakan untuk menguji keselamatan aplikasi web (Web Application). Ianya sering kali diguna pakai untuk mencari dan mengeksploit kelemahan yang ada di dalam web application. 

Dalam tutorial ini, saya akan menunjukkan cara-cara untuk menggunakan Burp Suite. Kita boleh memuat turun Burp Suite Community di Windows menggunakan link ini [https://portswigger.net/burp/communitydownload](https://portswigger.net/burp/communitydownload). Anda juga boleh menggunakan Burp Suite yang sedia dipasang di dalam [Kali Linux](https://www.kali.org/docs/introduction/what-is-kali-linux/).

# Memasang Foxy Proxy Di Dalam Browser

Burp Suite boleh digunakan dengan 2 kaedah iaitu menggunakan browser yang telah disediakan di dalam Burp Suite, atau menggunakan browser sendiri. Saya akan menunjukkan cara untuk menggunakan browser sendiri. Pertama, kita akan memuat turun extension browser bernama Foxy Proxy Standard.

![google_foxy_proxy](/assets/images/blog/cara-guna-burpsuite/google_foxy_proxy.png)

Tutorial ini menggunakan Mozilla Firefox, jadi anda boleh memuat turun Foxy Proxy mengikut browser anda.

![add_to_firefox](/assets/images/blog/cara-guna-burpsuite/add_to_firefox.png)

Bagi memudahkan akses ke Foxy Proxy, tambahkan Foxy Proxy ke toolbar, jadi Foxy Proxy akan sentiasa berada di atas toolbar.

![pin_to_toolbar](/assets/images/blog/cara-guna-burpsuite/pin_to_toolbar.png)

Tekan icon Foxy Proxy di toolbar, dan akan ada beberapa menu yang akan muncul, pilih "Options" untuk kita memulakan konfigurasi Foxy Proxy.

![foxy_options](/assets/images/blog/cara-guna-burpsuite/foxy_options.png)

Layar baru akan dibuka dan menunjukkan tetapan Foxy Proxy. Di bahagian pilihan atas, klik "Proxies". Kita akan mengisi beberapa konfigurasi seperti di bawah:

**Title: Burp Suite**<br>
**Hostname: 127.0.0.1**<br>
**Port: 8080**

![foxy_configuration](/assets/images/blog/cara-guna-burpsuite/foxy_configuration.png)
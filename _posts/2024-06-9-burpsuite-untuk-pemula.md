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

Setelah siap konfigurasi, Foxy Proxy sudah siap digunakan bersama Burp Suite, Jadi kita boleh hidupkan Burp Suite. Kita akan mulakan pintasan (intercept) di bahagian "Proxy" di mana intercept akan berada dalam keadaan "off".

![intercept_off](/assets/images/blog/cara-guna-burpsuite/proxy_off.png)

Untuk contoh pertama, kita akan intercept http request untuk melihat inti pati yang terkandung di dalam http GET request. Hidupkan Burp Suite proxy di Foxy Proxy dengan memilih setting yang telah kita konfigurasi sebentar tadi.

![select_proxy](/assets/images/blog/cara-guna-burpsuite/select_proxy.png)

Di Burp Suite hidupkan intercept dengan menekan "intercept off", butang ini akan berubah kepada "intercept on"

![intercept_on](/assets/images/blog/cara-guna-burpsuite/intercept_on.png)

Seterusnya, layari atau lakukan request terhadap website yang ingin kita intercept. Contoh di bawah, saya melayari website "www.example.com". Apabila kita melakukan request seperti melayari atau memuat semula (refresh) website, Burp Suite akan intercept request dari kita ke web server. Hasilnya, http request yang cuba dihantar akan ditahan di Burp Suite.

![intercept_request](/assets/images/blog/cara-guna-burpsuite/intercept_req.png)

Pada masa ini kita boleh mengedit http request yang cuba dihantar ke web server. Pelbagai perkara yang boleh dilakukan di http header yang sering kali digunakan dalam penetration testing untuk menguji tindak balas website terhadap request yang dihantar.

Jika kita ingin menghantar semula request yang telah di intercept kepada web server, kita hanya perlu menekan butang forward di bahagian atas request box. Terdapat 3 butang utama yang sering digunakan.

**Forward: Menyalurkan kembali request ke web server**<br>
**Drop: Membatalkan penghantaran request ke web server, jadi web server tidak akan menirima data yang dihantar.**<br>
**Action: Beberapa perkara yang boleh dilakukan kepada request untuk tindakan selanjutnya.**

![forward_request](/assets/images/blog/cara-guna-burpsuite/forward_req.png)

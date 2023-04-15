---
layout: post
title:  "Konfigurasikan DNS"
categories: [ clash ]
image: assets/images/1.jpg
---
## pengaturan dengan cara yang benar

> Konfigurasi DNS yang salah dapat menyebabkan akses jaringan lambat

### Apa yang dilakukan Clash untuk mengoptimalkan DNS?

- **Kueri bersamaan:** Saat nama domain meminta DNS, kueri bersamaan dibuat untuk semua server upstream di `nameserver` dan `fallback`.
- **Otomatis pilih hasil DNS yang benar:** Berdasarkan pengaturan di `fallback-filter`, clash akan otomatis memilih hasil DNS yang benar. Secara umum, clash menggunakan hasil di nameserver untuk ip CN dan hasil di fallback untuk ip asing.
- **Kueri DNS Proksi:** Untuk penyedia layanan jaringan raksasa, server mereka dapat tersebar di seluruh dunia, jadi saat kita menggunakan server proksi, penting untuk memastikan bahwa kita menggunakan lingkungan jaringan server proksi untuk melakukan kueri DNS. Jika Anda mendapatkan alamat IP setelah permintaan DNS di jaringan lokal Anda dan kemudian mengakses IP melalui jaringan proxy, kecepatan akses dapat dikurangi secara signifikan atau bahkan tidak tersedia. Clash memastikan bahwa semua permintaan yang menggunakan kebijakan proxy harus dikueri oleh **server jarak jauh**.
- **Cache DNS sederhana:** Clash memiliki cache DNS sederhana, clash tidak menanyakan permintaan DNS kedua saat yang pertama belum kedaluwarsa.
- **DNS optimis:** Ketika cache DNS lokal kedaluwarsa, clash terus terhubung menggunakan IP dari hasil cache lokal, sementara kueri DNS baru dibuat untuk memperbarui cache. Jika koneksi IP asli gagal, Clash coba lagi dengan hasil yang baru.

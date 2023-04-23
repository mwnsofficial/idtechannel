---
layout: post
title:  "Konfigurasikan DNS"
categories: [ clash ]
image: assets/images/4.jpg
---
## pengaturan dengan cara yang benar

> Konfigurasi DNS yang salah dapat menyebabkan akses jaringan lambat

### Apa yang dilakukan Clash untuk mengoptimalkan DNS?

- **Kueri bersamaan:** Saat nama domain meminta DNS, kueri bersamaan dibuat untuk semua server upstream di `nameserver` dan `fallback`.
- **Otomatis pilih hasil DNS yang benar:** Berdasarkan pengaturan di `fallback-filter`, clash akan otomatis memilih hasil DNS yang benar. Secara umum, clash menggunakan hasil di nameserver untuk ip CN dan hasil di fallback untuk ip asing.
- **Kueri DNS Proksi:** Untuk penyedia layanan jaringan raksasa, server mereka dapat tersebar di seluruh dunia, jadi saat kita menggunakan server proksi, penting untuk memastikan bahwa kita menggunakan lingkungan jaringan server proksi untuk melakukan kueri DNS. Jika Anda mendapatkan alamat IP setelah permintaan DNS di jaringan lokal Anda dan kemudian mengakses IP melalui jaringan proxy, kecepatan akses dapat dikurangi secara signifikan atau bahkan tidak tersedia. Clash memastikan bahwa semua permintaan yang menggunakan kebijakan proxy harus dikueri oleh **server jarak jauh**.
- **Cache DNS sederhana:** Clash memiliki cache DNS sederhana, clash tidak menanyakan permintaan DNS kedua saat yang pertama belum kedaluwarsa.
- **DNS optimis:** Ketika cache DNS lokal kedaluwarsa, clash terus terhubung menggunakan IP dari hasil cache lokal, sementara kueri DNS baru dibuat untuk memperbarui cache. Jika koneksi IP asli gagal, Clash coba lagi dengan hasil yang baru.

### Apa yang harus dilakukan pengguna dalam pengaturan DNS?

Mulailah dengan contoh berikut:

```
dns:
  enable: true
  ipv6: false
  listen: 0.0.0.0:53
  enhanced-mode: fake-ip
  nameserver:

  fallback:
```
Di nameserver Anda harus dengan poin-poin berikut:
- **Kecepatan dan stabilitas:** Server DNS membutuhkan stabilitas dan kecepatan, jadi gunakan server DNS yang secara geografis dekat dengannya jika memungkinkan.
- **Dukungan edns-client-subnet:** Untuk situs web raksasa (seperti microsoft.com), server CDN biasanya tersedia di seluruh dunia dan server DNS yang didukung ECS dapat mengembalikan alamat IP server yang paling sesuai berdasarkan akses ke alamat IP sumber.
- **Tidak lebih dari 4 Penyedia DNS di `nameserver`:** terlalu banyak penyedia DNS akan menyebabkan akses jaringan **latensi tinggi**.

Untuk pengguna yang tinggal di Cina daratan, `nameserver` harus memilih penyedia DNS yang memiliki BGP di Cina daratan. Berikut ini adalah merekomendasikan:

- AliDNS: UDP(`223.5.5.5 223.6.6.6`), DoH(`https://223.5.5.5/dns-query` `https://223.6.6.6/dns-query` `https://dns.alidns.com/dns-query` )

- Tencent DNS: UDP (`119.29.29.29` `119.28.28.28`)

- 114 DNS: UDP (`114.114.114.114` `114.114.115.115` )

- DNS rubyfish: DoT (`tls://rubyfish.cn:853` `tls://dns.rubyfish.cn:853`) DoH
  (`https://rubyfish.cn` `https://dns.rubyfish.cn`)

Dalam fallback Anda harus dengan poin-poin berikut:

- **Bersih dan bebas polusi:** Selalu kembalikan hasil DNS yang bersih dan andal

- **Tidak lebih dari 4 Penyedia DNS dalam fallback:** terlalu banyak penyedia DNS akan menyebabkan akses jaringan **latensi tinggi**.

Untuk pengguna yang tinggal di Cina daratan, **fallback** harus memilih penyedia DNS dengan hasil DNS yang bersih dan andal atau penyedia DNS luar negeri

> **Kapan saya harus menggunakan DoH atau DoT?**
> - Penyedia internet memiliki pembajakan DNS
> - Penyedia internet menjatuhkan terlalu banyak paket UDP
> - Orang yang sangat menghargai privasi

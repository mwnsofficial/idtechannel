---
layout: post
title: "Mengatur konfigurasi statik wan openwrt"
categories: [ openwrt ]
image: assets/images/6.jpg
youtubeid: 
---
Banyak yang sering mengalami kegagalan koneksi baik di jalur koneksi lan maupun di jalur koneksi wireless.

Itu di sebabkan oleh pengaturan pada wan openwrt itu sendiri karenakan waktu peminjaman wan ip sudah habis sehingga sering terjadi loss koneksi bahkan tidak bisa mengakses router openwrt.

Disini ID Tech Channel akan memberikan tutorial untuk anda agar mudah dan tidak akan lagi terjadi gangguan koneksi itu kembali pada router openwrt anda lagi.

`Pertama`, anda masuk ke router openwrt terlebih dahulu

`Kedua`, masuk lah pada menu network dan kemudian interfaces
 
`Ketiga`, carilah interface wan yang mengganggu koneksi anda kemudian tekan tombol edit

`Keempat`, pada bagian protokol ubah lah dhcp menjadi static address

`Kelima`, isikan address ip dengan ip modem anda namun angka ujung harus angka 100 atau lebih

`Keenam`, lalu tekan di bawahnya ipv4 netmask dan pilih subnet 255.255.255.0

`Ketujuh`, di gateway isikan saja dengan alamat ip modem kalian

`Kedelapan`, kemudian masuk ke bagian advanced settings isikan saja dns modem anda di custom dns

`Kesembilan`, tekan save kemudian save dan apply

`Kesepuluh`, tunggulah waktu mundur berjalan untuk proses namun masih terus berjalan waktu mundurnya cobalah cabut dan pasang lan kembali hingga berhasil

Semoga membantu anda yang sering gangguan koneksi lan dan wireless anda di openwrt

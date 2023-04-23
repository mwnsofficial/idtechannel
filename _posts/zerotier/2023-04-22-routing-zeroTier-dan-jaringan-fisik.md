---
layout: post
title:  "Routing ZeroTier dan Jaringan Fisik"
author: Muhammad Yusuf
categories: [ clash ]
image: assets/images/9.jpg
youtubeid: 
---
Ini tampaknya merupakan pola paling sederhana untuk mendapatkan akses jarak jauh ke LAN Anda. Itu tidak memerlukan akses ke router LAN atau memiliki beberapa perangkap menjembatani. Ini membutuhkan PC atau VM Linux, sesuatu yang menjalankan iptables, di LAN Anda. Sebuah raspberrypi bekerja. Ini adalah pengaturan NAT/Masquerade .

Kemungkinan Kerugian:

- Tidak ada siaran/multicast di seluruh jaringan (tetapi OS seluler tidak mengizinkan ini).

- Tidak dapat memulai koneksi dari LAN ke klien ZeroTier eksternal.

### Ringkasan

- Instal ZeroTier

- Tambahkan rute terkelola ke jaringan ZeroTier (di [my.zerotier.com](http://my.zerotier.com/) )

- Aktifkan Penerusan IP

- Konfigurasikan iptables

### Informasi yang dibutuhkan

Misalnya:

| info | contoh | singkatan nama di bawah ini |
| - | - | - |
| ID Jaringan ZeroTier | d5e04297a19bbd70 | $NETWORK_ID |
| Nama Antarmuka ZeroTier | zt7nnig26 | $ZT_IFACE |
| Nama Antarmuka Fisik | eth0 | $PHY_IFACE |
| subnet ZeroTier | 172.27.0.0/16 |  |
| Subnet fisik | 192.168.100.0/24 | $PHY_SUB |
| Alamat IP ZeroTier dari "Router" | 172.27.0.1 | $ZT_ADDR |

### Instal ZeroTier

[https://www.zerotier.com/download/](https://www.zerotier.com/download/)

```
sudo zerotier-cli join $NETWORK_ID
sudo zerotier-cli listnetworks 
```

Izinkan di

[my.zerotier.com/network/$NETWORK_ID](http://my.zerotier.com/network/$NETWORK_ID)

Keluaran listnetworks memiliki nama Antarmuka ZeroTier di bawah <"dev">


### Konfigurasikan rute terkelola ZeroTier

Di [my.zerotier.com/network/$NETWORK_ID](http://my.zerotier.com/network/$NETWORK_ID) -> Pengaturan -> Rute Terkelola

Ini menambahkan rute lain ke setiap perangkat yang bergabung ke jaringan ZeroTier.

| Tujuan | (Melalui) |
|- | - |
| $PHY_SUB | $ZT_ADDR |

Misalnya:

| Tujuan | (Melalui) |
| - | - |
| 192.168.100.0/23 | 172.27.0.1 |

Konfigurasikan rute tujuan sedikit lebih besar dari subnet fisik sebenarnya, di sini /23 daripada /24 (angka yang lebih kecil adalah subnet yang **lebih besar** dalam notasi ini) Ini membuat perangkat yang berada di jaringan fisik dan ZeroTier lebih memilih koneksi fisik.

### Aktifkan penerusan IP

Ini dapat bervariasi tergantung pada distribusi linux. Khas:

Edit **/etc/sysctl.conf** untuk menghapus komentar **net.ipv4.ip_forward**. Ini memungkinkan penerusan saat boot.

Untuk mengaktifkannya sekarang

```
sudo sysctl -w net.ipv4.ip_forward=1
```

### Konfigurasikan iptables

Tetapkan beberapa variabel shell (personalisasi ini)

```
PHY_IFACE=eth0; ZT_IFACE=zt7nnig26
```

Tambahkan aturan ke iptables
```
sudo iptables -t nat -A POSTROUTING -o $PHY_IFACE -j MASQUERADE
sudo iptables -A FORWARD -i $PHY_IFACE -o $ZT_IFACE -m state --state RELATED,ESTABLISHED -j ACCEPT
sudo iptables -A FORWARD -i $ZT_IFACE -o $PHY_IFACE -j ACCEPT
```

Simpan aturan iptables untuk boot selanjutnya
```
sudo apt install iptables-persistent
sudo bash -c iptables-save > /etc/iptables/rules.v4
```

### Tes!

- Matikan wifi di ponsel Anda

- Bergabunglah dengan jaringan zerotier, beri otorisasi

- Cobalah untuk mengakses sesuatu di LAN fisik

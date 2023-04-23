---
layout: post
title: "Clash Tun Mode 2"
author: Muhammad Yusuf
categories: [ clash ]
image: assets/images/7.jpg
---
Perkenalkan mode Clash TUN 2

Clash TUN mode 2 adalah mode TUN berdasarkan Netstack yang dikembangkan oleh C4H. Anda dapat mengunduh dari [https://github.com/comzyh/clash/releases](https://github.com/comzyh/clash/releases)

Ini memberikan pengalaman TUN kinerja tinggi. Ini akan lebih membantu saat menggunakan latensi pemerasan batas perdagangan frekuensi tinggi.
Dalam mode TUN 2, setiap permintaan DNS yang dilewati TUN akan dibajak secara otomatis untuk berbenturan.

> ℹ TUN mode 2 has been margin into TUN mode 1

> ⚠️ TUN mode 2 cannot worked in macOS due to some reasons: macOS don't allow use custom TUN name.
> Error information: 
> ERRO[0000] Start Tun interface error: Can't open tun: Interface name must be utun[0-9]*

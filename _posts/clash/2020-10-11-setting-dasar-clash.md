---
layout: post
title:  "Setting dasar clash"
author: Muhammad Yusuf
categories: [ clash ]
image: assets/images/2.jpg
---
Bagian umum mendefinisikan port, allow-lan, mode, log-level, external-controller, external-ui, otentikasi, dan fitur eksperimental.

## Port

Port adalah bagian di dalam komputer atau di dalam router switch. Komputer berkomunikasi sesuai dengan protokol lapisan transmisi INTERNET protokol TCP/IP, dan protokol yang berbeda sesuai dengan port yang berbeda

> ℹ Redir Port hanya berfungsi di macOS dan Linux.

```
# Port of HTTP(S) proxy server on the local end
port: 7890

# Port of SOCKS5 proxy server on the local end
socks-port: 7891

# Transparent proxy server port for Linux and macOS (Redirect TCP and TProxy UDP)
redir-port: 7892

# Transparent proxy server port for Linux (TProxy TCP and TProxy UDP)
tproxy-port: 7893

# HTTP(S) and SOCKS5 server on the same port
mixed-port: 7890
```

## Izinkan LAN

Izinkan perangkat lain di LAN untuk mengakses Internet melalui Clash.

```
allow-lan: false  # allow other devices access

bind-address: "*" # access by lan with a/some specific IP addresses
                  # "*": bind all IP addresses
                  # 192.168.122.11: bind a single IPv4 address
                  # "[aaaa::a8aa:ff:fe09:57d8]": bind a single IPv6 address

authentication:   # authentication of local SOCKS5/HTTP(S) server
  - "user1:pass1"
  - "user2:pass2"
```

## Mode

```
mode: rule # rule / global / direct / script (default is rule)
```

## Log Level

Level Log Clash Core. Debug akan menampilkan semua permintaan DNS dan log pembaruan penyedia, Debug tidak akan menyebabkan masalah kinerja apa pun.

```
log-level: info # silent / error / warning / info / debug 
```

## External Controller

Pengontrol Eksternal dapat mengontrol bentrokan dari luar dengan RESTful API untuk bentrokan

```
external-controller: 127.0.0.1:9090 

secret: "" # Secret for RESTful API (Optional)
```


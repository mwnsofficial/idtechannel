---
title: Group Olshop
layout: page
permalink: "/group-olshop/"
---

Sebelum anda memasukkan script ini.

Pastikan anda sudah menambahkan proxy provider di bawah ini pada config anda:

[Account](/account/)

Jangan lupa juga proxy group nya di bawah ini di salin dan tempelkan dalam config kalian:

```
- name: OLSHOP
  type: select
  disable-udp: false
  proxies:
  - NAMA-GROUP-ANDA
  - DIRECT
  url: http://www.gstatic.com/generate_204
  interval: '99'
```
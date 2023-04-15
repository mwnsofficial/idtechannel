---
layout: post
title: "Permintaan konfigurasi ke router dengan mudah"
categories: [ clash ]
image: assets/images/1.jpg
---
## Apa itu rule?

Bergantung pada aturan yang disesuaikan, pengguna memiliki cara mudah untuk mengalihkan setiap permintaan ke kebijakan yang berbeda.

> **Aturan memiliki Prioritas**
> Aturan cocok dengan urutan dari atas ke bawah, aturan di bagian atas daftar memiliki prioritas lebih tinggi daripada yang terakhir.
> **Apa itu kebijakan?**
> Kebijakan mencakup proxy dan grup proxy. Setiap aturan pasti memiliki kebijakan.

## Rule Syntax

Setiap aturan dalam clash memiliki 3 bagian (pertandingan adalah kasus khusus):
Contoh Aturan:

```
rules:
  - DOMAIN-SUFFIX,google.com,auto
  - DOMAIN-KEYWORD,google,auto
  - DOMAIN,ad.com,REJECT
  - SRC-IP-CIDR,192.168.1.201/32,DIRECT
  - IP-CIDR,127.0.0.0/8,DIRECT
  - IP-CIDR6,2620:0:2d0:200::7/32,auto
  - GEOIP,CN,DIRECT
  - DST-PORT,80,DIRECT
  - SRC-PORT,7777,DIRECT
  - MATCH,auto
```
| Type | Matcher | Policies |
| --- | --- | --- |
| DOMAIN-SUFFIX | google.com | auto |
| DOMAIN-KEYWORD | google | auto |
| DOMAIN | ad.com | REJECT |
| SRC-IP-CIDR | 192.168.1.201/32 | DIRECT |
| IP-CIDR | 127.0.0.1/8 | DIRECT |
| IP-CIDR6 | 2620:0:2d0:200::7/32 | auto |
| GEOIP | CN | DIRECT |
| DST-PORT | 80 | DIRECT |
| SRC-PORT | 7777 | DIRECT |
| MATCH | tida ada | auto |

> ℹ Rules harus diakhiri dengan aturan MATCH.
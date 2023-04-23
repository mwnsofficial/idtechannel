---
layout: post
title: "Permintaan konfigurasi ke router dengan mudah"
categories: [ clash ]
image: assets/images/5.jpg
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

<table>
<thead>
<tr>
<th>Type</th>
<th>Matcher</th>
<th>Policies</th>
</tr>
</thead>
<tbody>
<tr>
<td>DOMAIN-SUFFIX</td>
<td>google.com</td>
<td>auto</td>
</tr>
<tr>
<td>DOMAIN-KEYWORD</td>
<td>google</td>
<td>auto</td>
</tr>
<tr>
<td>DOMAIN</td>
<td>ad.com</td>
<td>REJECT</td>
</tr>
<tr>
<td>SRC-IP-CIDR</td>
<td>192.168.1.201/32</td>
<td>DIRECT</td>
</tr>
<tr>
<td>IP-CIDR</td>
<td>127.0.0.1/8</td>
<td>DIRECT</td>
</tr>
<tr>
<td>IP-CIDR6</td>
<td>2620:0:2d0:200::7/32</td>
<td>auto</td>
</tr>
<tr>
<td>GEOIP</td>
<td>CN</td>
<td>DIRECT</td>
</tr>
<tr>
<td>DST-PORT</td>
<td>80</td>
<td>DIRECT</td>
</tr>
<tr>
<td>SRC-PORT</td>
<td>7777</td>
<td>DIRECT</td>
</tr>
<tr>
<td>MATCH</td>
<td>tida ada</td>
<td>auto</td>
</tr>
</tbody>
</table>

> ℹ Rules harus diakhiri dengan aturan MATCH.

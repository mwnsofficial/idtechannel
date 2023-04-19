---
title: Account
layout: page
permalink: "/account/"
---

Sebelum anda memasukkan akun ini.

Pastikan anda sudah menambahkan script di bawah ini pada config anda:

```
proxy-providers:
  SIMCARD:
    type: file
    path: ./proxy_provider/simcard.yaml
    health-check:
      enable: true
      url: http://www.gstatic.com/generate_204
      interval: 99
```

Jangan lupa juga proxy-group nya di bawah ini di salin dan tempelkan dalam proxy group di config kalian:

```
- name: BERI-NAMA-GROUP
  type: select
  disable-udp: false
  use:
  - SIMCARD
  url: http://www.gstatic.com/generate_204
  interval: '99'
```

Buat file baru di folder `proxy_provider` dengan nama `simcard.yaml`

Ini untuk trojan gfw

```
proxies:
- name: beri-nama-akun
  type: trojan
  server: id1-idtechannel.id
  port: 443
  password: 00f2ebc0-d807-11ed-b8f4-1239d0255272
  udp: true
  sni: bugmu.com
  skip-cert-verify: true
```

Ini untuk trojan ws

```
proxies:
- name: beri-nama-akun
  type: trojan
  server: bugmu.com
  port: 443
  password: 00f2ebc0-d807-11ed-b8f4-1239d0255272
  udp: true
  sni: id1-idtechannel.id
  skip-cert-verify: true
  network: ws
  ws-opts:
    path: /path-akunmu
    headers:
      Host: id1-idtechannel.id
```
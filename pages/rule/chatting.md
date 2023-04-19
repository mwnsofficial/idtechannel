---
title: Rule Chatting
layout: page
permalink: "/chatting/"
---

Sebelum anda memasukkan rule ini.

Pastikan anda sudah menambahkan script di bawah ini pada config anda:

```
rule-providers:
  Chatting:
    type: file
    behavior: domain
    path: ./rule-chatting.yaml
```

Jangan lupa juga rules nya di bawah ini di salin dan tempelkan dalam config kalian:

```
- RULE-SET,Chatting,NAMA-PROXY-GRUP-ANDA
```

Buat file baru di folder `rule_provider` dengan nama `rule-chatting.yaml`

```
payload:

  # > RULE BY Id Tech Channel
  - "+.whatsapp.com"
  - "+.whatsapp.net"
  - "+.line.me"
```
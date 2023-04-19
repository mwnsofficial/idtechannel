---
title: Rule Bank
layout: page
permalink: "/bank/"
---

Sebelum anda memasukkan rule ini.

Pastikan anda sudah menambahkan script di bawah ini pada config anda:

```
rule-providers:
  Bank:
    type: file
    behavior: domain
    path: ./rule-bank.yaml
```

Jangan lupa juga rules nya di bawah ini di salin dan tempelkan dalam config kalian:

```
- RULE-SET,Bank,NAMA-PROXY-GRUP-ANDA
```

Buat file baru di folder `rule_provider` dengan nama `rule-bank.yaml`

```
payload:

  # > RULE BY Id Tech Channel
  - "+.bri.co.id"
  - "+.bni.co.id"
  - "+.klikbca.com"
  - "+.mandiri.co.id"
  - "+.bankbsi.co.id"
  - "+.cimbniaga.co.id"
  - "+.bankjateng.co.id"
  - "+.bankkalsel.co.id"
  - "+.bankaceh.co.id"
  - "+.banksumut.co.id"
  - "+.banknagari.co.id"
  - "+.banklampung.co.id"
  - "+.bankbandung.co.id"
  - "+.bankkalteng.co.id"
  - "+.bankkaltim.co.id"
  - "+.bankkalbar.co.id"
  - "+.bankkaltara.co.id"
  - "+.banksulsel.co.id"
  - "+.banksulteng.co.id"
  - "+.banksultra.co.id"
  - "+.banksulbar.co.id"
  - "+.banksultim.co.id"
  - "+.bankpapua.co.id"
```
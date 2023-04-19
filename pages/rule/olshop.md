---
title: Rule Olshop
layout: page
permalink: "/olshop/"
---

Sebelum anda memasukkan rule ini.

Pastikan anda sudah menambahkan script di bawah ini pada config anda:

```
rule-providers:
  Olshop:
    type: file
    behavior: domain
    path: ./rule-olshop.yaml
```

Jangan lupa juga rules nya di bawah ini di salin dan tempelkan dalam config kalian:

```
- RULE-SET,Olshop,NAMA-PROXY-GRUP-ANDA
```

Buat file baru di folder `rule_provider` dengan nama `rule-olshop.yaml`

```
payload:

  # > RULE BY Id Tech Channel
  - "+.shopee.co.id"
  - "+.shopeemobile.com"
  - "+.shopee.sg"
  - "+.lazada.co.id"
  - "+.bukalapak.com"
  - "+.blibli.com"
  - "+.tokopedia.com"
  - "+.amazon.com"
  - "+.alibaba.com"
  - "+.ebay.com"
  - "+.shopify.com"
```
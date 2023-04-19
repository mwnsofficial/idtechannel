---
title: Rule Sosmed
layout: page
permalink: "/sosmed/"
---

Sebelum anda memasukkan rule ini.

Pastikan anda sudah menambahkan script di bawah ini pada config anda:

```
rule-providers:
  Sosmed:
    type: file
    behavior: domain
    path: ./rule-sosmed.yaml
```

Jangan lupa juga rules nya di bawah ini di salin dan tempelkan dalam config kalian:

```
- RULE-SET,Sosmed,NAMA-PROXY-GRUP-ANDA
```

Buat file baru di folder `rule_provider` dengan nama `rule-sosmed.yaml`

```
payload:

  # > RULE BY ID Tech Channel
  - "+.fb.com"
  - "+.facebook.com"
  - "+.fbcdn.net"
  - "+.messenger.com"
  - "+.instagram.com"
  - "+.cdninstagram"
  - "+.twitter.com"
  - "+.twitpic.com"
  - "+.tiktok.com"
  - "+.tiktokv.com"
  - "+.tiktokcdn.com"
  - "+.path.com"
  - "+.discord.com"
  - "+.discus.com"
  - "+.line.me"
  - "+.pinterest.com"
  - "+.snapchat.com"
  - "+.kuaishou.com"
  - "+.weibo.com"
  - "+.qq.com"
  - "+.douyin.com"
  - "+.wechat.com"
```
---
title: Rule Stream
layout: page
permalink: "/stream/"
---

Sebelum anda memasukkan rule ini.

Pastikan anda sudah menambahkan script di bawah ini pada config anda:

```
rule-providers:
  Stream:
    type: file
    behavior: domain
    path: ./rule-stream.yaml
```

Jangan lupa juga rules nya di bawah ini di salin dan tempelkan dalam config kalian:

```
- RULE-SET,Stream,NAMA-PROXY-GRUP-ANDA
```

Buat file baru di folder `rule_provider` dengan nama `rule-stream.yaml`

```
payload:

  # > RULE BY Id Tech Channel
  - "+.youtube.com"
  - "+.youtubekids.com"
  - "+.youtubeedication.com"
  - "+.googlevideo.com"
  - "+.ggpht.com"
  - "+.gvt1.com"
  - "+.gvt2.com"
  - "+.ytimg.com"
  - "+.netflix.com"
  - "+.movi.com"
  - "+.hbo.com"
  - "+.m3u"
  - "+.wetv.vip"
  - "+.iflix.com"
  - "+.amazon.com"
  - "+.vidio.com"
  - "+.restream.io"
  - "+.rctiplus.com"
  - "+.transtv.co.id"
  - "+.netmedia.co.id"
  - "+.hotstar.com"
  - "+.visionplus.id"
  - "+.kompas.tv"
  - "+.tvonenews.com"
  - "+.inews.id"
  - "+.cnnindonesia.com"
  - "+.streamlabs.com"
  - "+.twitch.tv"
  - "+.nimo.tv"
  - "+.obsproject.com"
```
---
layout: post
title:  "Setting Clash Profil"
author: Muhammad Yusuf
categories: [ clash ]
image: assets/images/8.jpg
---
Opsi profil membantu inti bentrokan memperluas operasi yang terkait dengan operasi berikut

> ✅ Dukungan dari v1.4.0

> ⚠️ Beberapa opsi mungkin hanya tersedia di Premium Core.

```
profile:
  # store the `select` results in $HOME/.cache
  # when two different configurations have groups with the same name, the selected values are shared
  # set false if you don't want this behavior
  store-selected: false
  # open tracing exporter API
  tracing: true
  # persistence fakeip
  store-fake-ip: true
```

## store-selected

Clash akan menyimpan hasil pemilihan di $HOME/.cache. Saat restart terjadi, Clash akan menerapkan hasil ini secara otomatis. Ini adalah peningkatan keandalan yang efektif.

```
store-selected: true
```

> ℹ ketika dua konfigurasi berbeda memiliki grup dengan nama yang sama, nilai yang dipilih akan dibagikan

## tracing

Tracing is a dashboard which provide a large number of charts, help you debugging what happened in clash and why it's happened.

```
tracing: true
```

> ℹ Hanya tersedia di Inti Premium.

## store-fake-ip

Persistent Fake IP records

```
store-fake-ip: true
```

> Dukungan dari v1.8.0 atau Premium 2021.11.08

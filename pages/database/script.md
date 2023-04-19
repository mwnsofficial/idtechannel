---
title: Script
layout: page
permalink: "/script/"
---

Sebelum anda memasukkan script ini.

Pastikan anda sudah menambahkan semua di bawah ini pada config anda:

[Rule Game](/game/)

[Rule Sosmed](/sosmed/)

[Rule Stream](/stream/)

[Rule Olshop](/olshop/)

[Rule Bank](/bank/)

[Rule Chatting](/chatting/)

Jangan lupa juga script nya di bawah ini di salin dan tempelkan dalam config kalian:

```
script:
  code: |
    def main(ctx, metadata):
        ruleset_action = {"Game": "GAME",
            "Sosmed": "SOSMED",
            "Stream": "STREAM",
            "Olshop": "OLSHOP",
            "Bank": "BANK",
            "Chatting": "CHATTING",
          }

        port = int(metadata["dst_port"])

        if metadata["network"] == "UDP":
            if port == "21,22,23,53,80,443,8443":
                ctx.log('[Script] matched QUIC traffic use NAMA-GROUP-ANDA')
                return "NAMA-GROUP-ANDA"

        if metadata["dst_ip"] == "":
            metadata["dst_ip"] = ctx.resolve_ip(metadata["host"])

        port_list = [21, 22, 23, 53, 80, 81, 123, 443, 853, 5353, 8000, 8008, 8080, 8081, 8090, 8443, 8888, 9993]
        if port not in port_list:
            ctx.log('[Script] not common port use GAME')
            return "GAME"

        if metadata["dst_ip"] == "":
            return "DIRECT"

        for ruleset in ruleset_action:
            if ctx.rule_providers[ruleset].match(metadata):
                return ruleset_action[ruleset]

        code = ctx.geoip(metadata["dst_ip"])
        if code == "ID":
            ctx.log('[Script] Geoip ID')
            return "NAMA-GROUP-ANDA"

        ctx.log('[Script] NAMA-GROUP-ANDA')
        return "NAMA-GROUP-ANDA"
```
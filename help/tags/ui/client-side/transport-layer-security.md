---
title: TLS-informatie (Transport Layer Security)
description: Informatie over de TLS-versies en -ciphers
exl-id: 04948cd8-6cf0-4159-a9d3-3130b97af106
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# TLS-informatie (Transport Layer Security)

TLS (Transport Layer Security) is een cryptografisch protocol dat end-to-end beveiliging biedt voor gegevens die via internet tussen toepassingen worden verzonden. Voor meer gedetailleerde informatie over TLS, lees de [ basisbeginselen van TLS ](https://www.internetsociety.org/deploy360/tls/basics/) documentatie.

Tags in Adobe Experience Platform zijn een systeem voor tagbeheer dat is ontworpen om scripts op uw website dynamisch te laden. TLS beveiligt de communicatie tussen de Adobe-host `assets.adobedtm.com` en uw website wanneer deze scripts worden geladen.

Er zijn meerdere TLS-versies beschikbaar en deze ondersteunen een aantal verschillende ciphers. Niet alle versies en ciphers zijn het zelfde aangezien sommige als minder of veiliger dan andere worden beschouwd.

## Ondersteunde TLS-versies en -CIFERS

De Adobe-hostoptie biedt momenteel ondersteuning voor de volgende TLS-versies en -ciphers:

```
PORT    STATE SERVICE
443/tcp open  https
| ssl-enum-ciphers:
|   TLSv1.2:
|     ciphers:
|       TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384 (secp256r1) - A
|       TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256 (secp256r1) - A
|       TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 (secp256r1) - A
|     compressors:
|       NULL
|     cipher preference: server
|   TLSv1.3:
|     ciphers:
|       TLS_AKE_WITH_AES_128_GCM_SHA256 (secp256r1) - A
|       TLS_AKE_WITH_AES_256_GCM_SHA384 (secp256r1) - A
|       TLS_AKE_WITH_CHACHA20_POLY1305_SHA256 (secp256r1) - A
|     cipher preference: client
|_  least strength: A
```

### Zelfhosting

Als u [ zelf-gastheer ](../publishing/hosts/self-hosting-libraries.md) uw bibliotheek bent, dan zullen de gesteunde versies TLS door uw eigen het ontvangen dienst worden bepaald.

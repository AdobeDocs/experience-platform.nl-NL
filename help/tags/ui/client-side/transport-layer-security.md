---
title: TLS-informatie (Transport Layer Security)
description: Informatie over de TLS-versies en -ciphers
source-git-commit: 35ee2aca2b92cb8abe1fc69ad6cbc66b0e241e89
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# TLS-informatie (Transport Layer Security)

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Zie voor een geconsolideerde referentie van de terminologische wijzigingen de [termijnupdates](../../term-updates.md) document.

TLS (Transport Layer Security) is een cryptografisch protocol dat end-to-end beveiliging biedt voor gegevens die via internet tussen toepassingen worden verzonden. Lees voor meer informatie over TLS de [Basisbegrippen voor TLS](https://www.internetsociety.org/deploy360/tls/basics/) documentatie.

Tags in Adobe Experience Platform zijn een systeem voor tagbeheer dat is ontworpen om scripts op uw website dynamisch te laden. TLS beveiligt de communicatie tussen de Adobe host `assets.adobedtm.com` en uw website wanneer deze scripts zijn geladen.

Er zijn meerdere TLS-versies beschikbaar en deze ondersteunen een aantal verschillende ciphers. Niet alle versies en ciphers zijn het zelfde aangezien sommige als minder of veiliger dan andere worden beschouwd.

## Ondersteunde TLS-versies en -CIFERS

De host-optie Adobe biedt momenteel ondersteuning voor de volgende TLS-versies en -ciphers:

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

Als u [zelfhosting](../publishing/hosts/self-hosting-libraries.md) de ondersteunde TLS-versies worden bepaald door uw eigen hostingservice.

## Op 1 mei 2024 te verwijderen TLS-cifers

```
PORT    STATE SERVICE
443/tcp open  https
| ssl-enum-ciphers:
|   TLSv1.2:
|     ciphers:
|       TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384 (secp256r1) - A
|       TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA (secp256r1) - A
|       TLS_RSA_WITH_AES_256_GCM_SHA384 (rsa 2048) - A
|       TLS_RSA_WITH_AES_128_GCM_SHA256 (rsa 2048) - A
|       TLS_RSA_WITH_AES_256_CBC_SHA256 (rsa 2048) - A
|       TLS_RSA_WITH_AES_128_CBC_SHA256 (rsa 2048) - A
|       TLS_RSA_WITH_AES_256_CBC_SHA (rsa 2048) - A
|       TLS_RSA_WITH_AES_128_CBC_SHA (rsa 2048) - A
|     compressors:
|       NULL
|     cipher preference: server
|   TLSv1.3:
|     ciphers:
|       TLS_AKE_WITH_AES_128_CCM_8_SHA256 (secp256r1) - A
|       TLS_AKE_WITH_AES_128_CCM_SHA256 (secp256r1) - A
|     cipher preference: client
|_  least strength: A
```

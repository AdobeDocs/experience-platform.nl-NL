---
description: Gebruik de ondersteunde verificatieconfiguraties in Adobe Experience Platform Destination SDK om gebruikers te verifiëren en gegevens te activeren op het eindpunt van uw bestemming.
title: Verificatieconfiguratie
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: 485c1359f8ef5fef0c5aa324cd08de00b0b4bb2f
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# Verificatieconfiguratie {#credentials}

## Ondersteunde verificatietypen {#supported-authentication-types}

Adobe Experience Platform Destination SDK ondersteunt verschillende verificatietypen:

* Waardere verificatie
* OAuth 2 met vergunningscode
* OAUth 2 met wachtwoordsubsidie
* OAuth 2 met clientaanmeldingsgegevens verlenen

Voor de diverse gesteunde stromen OAuth 2, evenals voor douane OAuth 2 steun, lees de documentatie van SDK van de Bestemming op [OAuth 2 authentificatie](./oauth2-authentication.md).

U kunt de authentificatieinformatie voor uw bestemming via de `customerAuthenticationConfigurations` parameters van het `/destinations` eindpunt vormen. Raadpleeg de sectie [Configuraties voor klantverificatie](./destination-configuration.md#customer-authentication-configurations) in het artikel voor doelconfiguratie.

## Wanneer wordt het API-eindpunt `/credentials` gebruikt {#when-to-use}

>[!IMPORTANT]
>
>In de meeste gevallen hoeft u *niet* het API-eindpunt `/credentials` te gebruiken. In plaats daarvan, kunt u de authentificatieinformatie voor uw bestemming via de `customerAuthenticationConfigurations` parameters van het `/destinations` eindpunt vormen.

Gebruik het `activation/authoring/credentials` API eindpunt en selecteer `PLATFORM_AUTHENTICATION` in [bestemmingsconfiguratie](./destination-configuration.md#destination-delivery) als er een globaal authentificatiesysteem tussen Adobe en uw bestemming is en de [!DNL Platform] klant te hoeven om geen authentificatiegeloofsbrieven te verstrekken om met uw bestemming te verbinden. In dit geval moet u een aanmeldingsobject maken met het API-eindpunt `/credentials`. Lees [Referentials API eindpuntverrichtingen](./credentials-configuration-api.md) voor een volledige lijst van verrichtingen u op het `/credentials` eindpunt kunt uitvoeren.

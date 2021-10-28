---
description: Gebruik de ondersteunde verificatieconfiguraties in Adobe Experience Platform Destination SDK om gebruikers te verifiëren en gegevens te activeren op het eindpunt van uw bestemming.
title: Verificatieconfiguratie
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: e6d922800c17312df8529061c56d8a2deac46662
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Verificatieconfiguratie {#credentials}

## Ondersteunde verificatietypen {#supported-authentication-types}

Adobe Experience Platform Destination SDK ondersteunt verschillende verificatietypen:

* Waardere verificatie
* OAuth 2 met vergunningscode
* OAUth 2 met wachtwoordsubsidie
* OAuth 2 met clientaanmeldingsgegevens verlenen

U kunt de authentificatieinformatie voor uw bestemming via vormen `customerAuthenticationConfigurations` parameters van de `/destinations` eindpunt. Zie de [sectie met configuraties voor klantverificatie](./destination-configuration.md#customer-authentication-configurations) in het artikel van de bestemmingsconfiguratie en de secties hieronder voor details rond de configuraties voor elk authentificatietype.

## Waardere verificatie {#bearer}

Aan opstellingstradientypeauthentificatie voor uw bestemmingen, moet u enkel vormen `customerAuthenticationConfigurations` in de `/destinations` eindpunt zoals hieronder getoond:

```json
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ]
```

## OAuth 2-verificatie {#oauth2}

Voor informatie hoe te opstelling de diverse gesteunde stromen OAuth 2, evenals voor douane OAuth 2 steun, lees de documentatie van SDK van de Bestemming over [OAuth 2-verificatie](./oauth2-authentication.md).


## Wanneer gebruikt u de `/credentials` API-eindpunt {#when-to-use}

>[!IMPORTANT]
>
>In de meeste gevallen *niet* de `/credentials` API-eindpunt. In plaats daarvan, kunt u de authentificatieinformatie voor uw bestemming via vormen `customerAuthenticationConfigurations` parameters van de `/destinations` eindpunt.

De `/credentials` API eindpunt wordt verstrekt aan bestemmingsontwikkelaars voor de gevallen wanneer er een globaal authentificatiesysteem tussen Adobe en uw bestemming is en [!DNL Platform] klanten te hoeven om geen authentificatiegeloofsbrieven te verstrekken om met uw bestemming te verbinden.

In dit geval moet u een object credentials maken met de opdracht `/credentials` API-eindpunt. U moet ook `PLATFORM_AUTHENTICATION` in de [doelconfiguratie](./destination-configuration.md#destination-delivery). Lezen [API-eindpuntbewerkingen voor referenties](./credentials-configuration-api.md) voor een volledige lijst van verrichtingen die u op kunt uitvoeren `/credentials` eindpunt.

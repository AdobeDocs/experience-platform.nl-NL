---
description: Gebruik de gesteunde authentificatieconfiguraties in Adobe Experience Platform Destination SDK om gebruikers voor authentiek te verklaren en gegevens te activeren aan uw bestemmingspunt.
title: Verificatieconfiguratie
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: 92bca3600d854540fd2badd925e453fba41601a7
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 0%

---

# Verificatieconfiguratie {#credentials}

## Ondersteunde verificatietypen {#supported-authentication-types}

De authentificatieconfiguratie die u selecteert bepaalt hoe het Experience Platform aan uw bestemming, in het Platform UI voor authentiek verklaart.

Adobe Experience Platform Destination SDK ondersteunt verschillende verificatietypen:

* Waardere verificatie
* (bèta) Amazon S3-verificatie
* (Beta) Azure-verbindingstekenreeks
* (Beta) Azure service principal
* (Beta) SFTP met SSH-sleutel
* (Beta) SFTP met wachtwoord
* OAuth 2 met vergunningscode
* OAUth 2 met wachtwoordsubsidie
* OAuth 2 met clientaanmeldingsgegevens verlenen

U kunt de authentificatieinformatie voor uw bestemming via vormen `customerAuthenticationConfigurations` parameters van de `/destinations` eindpunt.

Verwijs naar de volgende secties voor de details van de authentificatieconfiguratie voor elk type van bestemming:

* [Verificatieconfiguraties voor streamingdoelen](destination-configuration.md#customer-authentication-configurations)
* [Verificatieconfiguraties voor bestandsgebaseerde doelen](file-based-destination-configuration.md#customer-authentication-configurations)

## Waardere verificatie {#bearer}

De authentificatie van de drager wordt gesteund voor het stromen bestemmingen in Experience Platform.

Aan opstellingstradientypeauthentificatie voor uw bestemming, vorm `customerAuthenticationConfigurations` in de `/destinations` eindpunt zoals hieronder getoond:

```json
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ]
```

## (bèta) [!DNL Amazon S3] verificatie {#s3}

[!DNL Amazon S3] de authentificatie wordt gesteund voor op dossier-gebaseerde bestemmingen in Experience Platform.

>[!IMPORTANT]
>
>Bestandsgebaseerde doelondersteuning in Adobe Experience Platform Destination SDK staat momenteel in bètaversie. De documentatie en functionaliteit kunnen worden gewijzigd.

Als u Amazon S3-verificatie voor uw bestemming wilt instellen, configureert u de `customerAuthenticationConfigurations` in de `/destinations` eindpunt zoals hieronder getoond:

```json
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ]
```

## (bèta) [!DNL Azure Blob Storage] {#blob}

[!DNL Azure Blob Storage] de authentificatie wordt gesteund voor op dossier-gebaseerde bestemmingen in Experience Platform.

>[!IMPORTANT]
>
>Bestandsgebaseerde doelondersteuning in Adobe Experience Platform Destination SDK staat momenteel in bètaversie. De documentatie en functionaliteit kunnen worden gewijzigd.

Aan opstelling [!DNL Azure Blob] de authentificatie voor uw bestemming, vormt `customerAuthenticationConfigurations` in de `/destinations` eindpunt zoals hieronder getoond:

```json
   "customerAuthenticationConfigurations":[
     {
        "authType":"AZURE_CONNECTION_STRING"
     }
  ]
```

## (bèta) [!DNL Azure Data Lake Storage] {#adls}

[!DNL Azure Data Lake Storage] de authentificatie wordt gesteund voor op dossier-gebaseerde bestemmingen in Experience Platform.

>[!IMPORTANT]
>
>Bestandsgebaseerde doelondersteuning in Adobe Experience Platform Destination SDK staat momenteel in bètaversie. De documentatie en functionaliteit kunnen worden gewijzigd.

Aan opstelling [!DNL Azure Data Lake Storage] (ADLS) authentificatie voor uw bestemming, vorm `customerAuthenticationConfigurations` in de `/destinations` eindpunt zoals hieronder getoond:

```json
   "customerAuthenticationConfigurations":[
     {
        "authType":"AZURE_SERVICE_PRINCIPAL"
     }
  ]
```

## (bèta) [!DNL SFTP] verificatie met [!DNL SSH] key {#sftp-ssh}

[!DNL SFTP] verificatie met [!DNL SSH] key wordt ondersteund voor op bestanden gebaseerde doelen in Experience Platform.

>[!IMPORTANT]
>
>Bestandsgebaseerde doelondersteuning in Adobe Experience Platform Destination SDK staat momenteel in bètaversie. De documentatie en functionaliteit kunnen worden gewijzigd.

Om de authentificatie van SFTP met de sleutel van SSH voor uw bestemming te plaatsen, vorm `customerAuthenticationConfigurations` in de `/destinations` eindpunt zoals hieronder getoond:

```json
   "customerAuthenticationConfigurations":[
      {
         "authType":"SFTP_WITH_SSH_KEY"
      }
   ]
```

## (bèta) [!DNL SFTP] verificatie met wachtwoord {#sftp-password}

[!DNL SFTP] verificatie met wachtwoord wordt ondersteund voor op bestanden gebaseerde doelen in Experience Platform.

>[!IMPORTANT]
>
>Bestandsgebaseerde doelondersteuning in Adobe Experience Platform Destination SDK staat momenteel in bètaversie. De documentatie en functionaliteit kunnen worden gewijzigd.

Als u SFTP-verificatie wilt instellen met een wachtwoord voor uw doel, configureert u de `customerAuthenticationConfigurations` in de `/destinations` eindpunt zoals hieronder getoond:

```json
   "customerAuthenticationConfigurations":[
      {
         "authType":"SFTP_WITH_PASSWORD"
      }
   ]
```

## [!DNL OAuth 2] verificatie {#oauth2}

[!DNL OAuth 2] De authentificatie wordt gesteund voor het stromen bestemmingen in Experience Platform.

Voor informatie hoe te opstelling de diverse gesteunde stromen OAuth 2, evenals voor de steun van douane OAuth 2, lees de documentatie van de Destination SDK over [OAuth 2-verificatie](./oauth2-authentication.md).


## Wanneer gebruikt u de `/credentials` API-eindpunt {#when-to-use}

>[!IMPORTANT]
>
>In de meeste gevallen *niet* de `/credentials` API-eindpunt. In plaats daarvan, kunt u de authentificatieinformatie voor uw bestemming via vormen `customerAuthenticationConfigurations` parameters van de `/destinations` eindpunt.

De `/credentials` API eindpunt wordt verstrekt aan bestemmingsontwikkelaars voor de gevallen wanneer er een globaal authentificatiesysteem tussen Adobe en uw bestemming is en [!DNL Platform] klanten te hoeven om geen authentificatiegeloofsbrieven te verstrekken om met uw bestemming te verbinden.

In dit geval moet u een object credentials maken met de opdracht `/credentials` API-eindpunt. U moet ook `PLATFORM_AUTHENTICATION` in de [doelconfiguratie](./destination-configuration.md#destination-delivery). Lezen [API-eindpuntbewerkingen voor referenties](./credentials-configuration-api.md) voor een volledige lijst van verrichtingen die u op kunt uitvoeren `/credentials` eindpunt.

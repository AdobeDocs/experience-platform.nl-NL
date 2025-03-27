---
title: Google BigQuery Source Connector - Overzicht
description: Leer hoe u Google BigQuery via API's of de gebruikersinterface met Adobe Experience Platform kunt verbinden.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 1900a8c6a3f3119c8b9049b12f5660cc9fd181a2
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---

# [!DNL Google BigQuery] bron

>[!IMPORTANT]
>
>De [!DNL Google BigQuery] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-Time Customer Data Platform Ultimate hebben aangeschaft.

Lees dit document voor de vereiste stappen die u moet uitvoeren om uw [!DNL Google BigQuery] -account met Adobe Experience Platform te kunnen verbinden op Azure of Amazon Web Services (AWS).

## Vereisten {#prerequisites}

Lees de volgende secties voor de vereiste configuratie die u moet voltooien voordat u uw [!DNL Google BigQuery] -account kunt verbinden met Experience Platform.

### IP adres lijst van gewenste personen

U moet gebied-specifieke IP adressen aan uw lijst van gewenste personen toevoegen alvorens uw bronnen aan Experience Platform op of Azure of Amazon Web Services (AWS) aan te sluiten. Voor meer informatie, lees de gids op [ voegend op lijst van gewenste personen IP adressen om met Experience Platform op Azure en AWS ](../../ip-address-allow-list.md) voor meer informatie te verbinden.

### Verifiëren voor Experience Platform in Azure {#azure}

U moet de volgende gegevens opgeven om uw [!DNL Google BigQuery] -account aan te sluiten op Experience Platform on Azure.

>[!BEGINTABS]

>[!TAB  Basisauthentificatie ]

Om het gebruiken van een combinatie OAuth 2.0 en basisauthentificatie voor authentiek te verklaren, verstrek de aangewezen waarden voor de volgende geloofsbrieven.

| Credentials | Beschrijving |
| --- | --- |
| `project` | Het project is de organisatie op basisniveau voor uw [!DNL Google Cloud] -bronnen, inclusief [!DNL Google BigQuery] . |
| `clientID` | De client-id is de helft van uw [!DNL Google BigQuery] OAuth 2.0-referenties. |
| `clientSecret` | Het clientgeheim is de andere helft van uw [!DNL Google BigQuery] OAuth 2.0-referenties. |
| `refreshToken` | Met het token Vernieuwen kunt u nieuwe toegangstokens voor uw API verkrijgen. Toegangstokens hebben beperkte levensduur en kunnen verlopen tijdens de uitvoering van uw project. U kunt gebruiken verfrist teken om verdere toegangstokens voor uw project voor authentiek te verklaren en te verzoeken wanneer nodig. |
| `largeResultsDataSetId` | (Optioneel) De vooraf gemaakte [!DNL Google BigQuery] dataset-id die vereist is om ondersteuning voor grote resultaatsets mogelijk te maken. |

Voor gedetailleerde instructies op hoe te om OAuth 2.0 geloofsbrieven voor [!DNL Google] APIs te produceren, zie de volgende [[!DNL Google]  OAuth 2.0 authentificatiegids ](https://developers.google.com/identity/protocols/oauth2).

>[!TAB  de authentificatie van de Dienst ]

Om het gebruiken van de dienstauthentificatie voor authentiek te verklaren, verstrek de aangewezen waarden voor de volgende geloofsbrieven.

**Nota**: Uw de dienstrekening moet voldoende toestemmingen, zoals: **[!DNL BigQuery Job User]**, **[!DNL BigQuery Data Viewer]**, **[!DNL BigQuery Read Session User]**, en **[!DNL BigQuery Data Owner]** hebben om met de dienstauthentificatie met succes voor authentiek te verklaren.

| Credentials | Beschrijving |
| --- | --- |
| `projectId` | De id van de [!DNL Google BigQuery] waarnaar u wilt zoeken. |
| `keyFileContent` | Het sleuteldossier dat wordt gebruikt om de de dienstrekening voor authentiek te verklaren. U kunt deze waarde van het [[!DNL Google Cloud service accounts]  dashboard ](https://console.cloud.google.com) terugwinnen. De inhoud van het sleutelbestand heeft de JSON-indeling. U moet dit coderen in [!DNL Base64] wanneer u autoriseert aan Experience Platform. |
| `largeResultsDataSetId` | (Optioneel) De vooraf gemaakte [!DNL Google BigQuery] dataset-id die vereist is om ondersteuning voor grote resultaatsets mogelijk te maken. |

Voor meer informatie bij het gebruiken van de dienstrekeningen in [!DNL Google BigQuery], lees de gids op [ gebruikend de dienstrekeningen in  [!DNL Google BigQuery] ](https://cloud.google.com/bigquery/docs/use-service-accounts).

>[!ENDTABS]

### Verifiëren voor Experience Platform op AWS {#aws}

U moet de volgende gegevens opgeven om uw [!DNL Google BigQuery] -account te verbinden met Experience Platform op AWS.

| Credentials | Beschrijving |
| --- | --- |
| `projectId` | De id van de [!DNL Google BigQuery] waarnaar u wilt zoeken. |
| `keyFileContent` | Het sleuteldossier dat wordt gebruikt om de de dienstrekening voor authentiek te verklaren. U kunt deze waarde van het [[!DNL Google Cloud service accounts]  dashboard ](https://console.cloud.google.com) terugwinnen. De inhoud van het sleutelbestand heeft de JSON-indeling. U moet dit coderen in [!DNL Base64] wanneer u autoriseert aan Experience Platform. |
| `datasetId` | De [!DNL Google BigQuery] dataset-id. Deze id vertegenwoordigt de locatie van de gegevenstabellen. |

## Verbinden [!DNL Google BigQuery] met Experience Platform

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen [!DNL Google BigQuery] en Experience Platform via API&#39;s of de gebruikersinterface:

### API&#39;s gebruiken

- [Een Google BigQuery-basisverbinding maken met de Flow Service API](../../tutorials/api/create/databases/bigquery.md)
- [Gegevenstabellen verkennen met de Flow Service API](../../tutorials/api/explore/tabular.md)
- [Een gegevensstroom maken voor een databasebron met behulp van de Flow Service API](../../tutorials/api/collect/database-nosql.md)

### UI gebruiken

- [Een Google BigQuery-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/databases/bigquery.md)
- [Een gegevensstroom maken voor een databasebronverbinding in de gebruikersinterface](../../tutorials/ui/dataflow/databases.md)

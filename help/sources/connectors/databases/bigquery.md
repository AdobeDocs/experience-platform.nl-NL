---
title: Google BigQuery Source Connector - Overzicht
description: Leer hoe u Google BigQuery via API's of de gebruikersinterface met Adobe Experience Platform kunt verbinden.
badgeUltimate: label="Ultieme" type="Positive"
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 1fa79b31b5a257ebb3cbd60246b757d8a4a63d7c
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# [!DNL Google BigQuery] bron

>[!IMPORTANT]
>
>De [!DNL Google BigQuery] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-time Customer Data Platform Ultimate hebben aangeschaft.

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de platformservices. U kunt gegevens uit diverse bronnen invoeren, zoals toepassingen voor Adobe, opslag in de cloud, databases en vele andere.

Lees dit document voor de vereiste stappen die u moet uitvoeren om uw [!DNL Google BigQuery] -account met Experience Platform te kunnen verbinden.

## Vereisten {#prerequisites}

In de volgende sectie vindt u meer informatie over de vereiste configuratie voordat u een [!DNL Google BigQuery] bronverbinding kunt maken.

### IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de ](../../ip-address-allow-list.md) pagina van de lijst van gewenste personen van het 0} IP adres {voor meer informatie.[

### Uw [!DNL Google BigQuery] gebruikersgegevens genereren {#credentials}

Als u [!DNL Google BigQuery] wilt verbinden met Experience Platform, moet u waarden voor de volgende referenties genereren:

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

## Verbinden [!DNL Google BigQuery] met platform

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen [!DNL Google BigQuery] en Platform via API&#39;s of de gebruikersinterface:

### API&#39;s gebruiken

- [Een Google BigQuery-basisverbinding maken met de Flow Service API](../../tutorials/api/create/databases/bigquery.md)
- [Gegevenstabellen verkennen met de Flow Service API](../../tutorials/api/explore/tabular.md)
- [Een gegevensstroom maken voor een databasebron met behulp van de Flow Service API](../../tutorials/api/collect/database-nosql.md)

### UI gebruiken

- [Een Google BigQuery-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/databases/bigquery.md)
- [Een gegevensstroom maken voor een databasebronverbinding in de gebruikersinterface](../../tutorials/ui/dataflow/databases.md)

---
keywords: Experience Platform;home;populaire onderwerpen;BigQuery;bigquery;Google BigQuery;google bigquery
solution: Experience Platform
title: Google BigQuery Source Connector - Overzicht
topic-legacy: overview
description: Leer hoe u Google BigQuery via API's of de gebruikersinterface met Adobe Experience Platform kunt verbinden.
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: fa861e9740e05b4fcc4e8039bb288301d42b8357
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# (bèta) [!DNL Google BigQuery] connector

>[!NOTE]
>
>De [!DNL Google BigQuery] is in bèta. Zie de [Overzicht van bronnen](../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de services van het Platform. U kunt gegevens van diverse bronnen, zoals Adobe-toepassingen, cloudopslag, databases en vele andere, invoeren.

[!DNL Experience Platform] verleent steun voor het opnemen van gegevens van een derdegegevensbestand. Het Platform kan met verschillende types van gegevensbestanden zoals relationeel, NoSQL, of gegevenspakhuizen verbinden. Ondersteuning voor databaseproviders omvat [!DNL Google BigQuery].

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de [IP adres lijst van gewenste personen](../../ip-address-allow-list.md) voor meer informatie.

## Vereisten

In het volgende gedeelte vindt u meer informatie over de vereiste configuratie voordat u een [!DNL Google BigQuery] bronverbinding.

### Uw [!DNL Google BigQuery] geloofsbrieven

Verbinding maken [!DNL Google BigQuery] aan Platform, moet u waarden voor de volgende geloofsbrieven produceren:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `project` | Het project is de organisatie op basisniveau voor uw [!DNL Google Cloud] middelen, waaronder [!DNL Google BigQuery]. |
| `clientID` | De client-id is de helft van uw [!DNL Google BigQuery] OAuth 2.0 geloofsbrieven. |
| `clientSecret` | Het clientgeheim is de andere helft van uw [!DNL Google BigQuery] OAuth 2.0 geloofsbrieven. |
| `refreshToken` | Met het token Vernieuwen kunt u nieuwe toegangstokens voor uw API verkrijgen. Toegangstokens hebben beperkte levensduur en kunnen verlopen tijdens de uitvoering van uw project. U kunt gebruiken verfrist teken om verdere toegangstokens voor uw project voor authentiek te verklaren en te verzoeken wanneer nodig. |

Voor gedetailleerde instructies over hoe te om geloofsbrieven te produceren OAuth 2.0 voor [!DNL Google] API&#39;s, zie het volgende [[!DNL Google] OAuth 2.0-verificatiegids](https://developers.google.com/identity/protocols/oauth2).

## Verbinden [!DNL Google BigQuery] naar Platform

In de onderstaande documentatie vindt u informatie over het maken van een verbinding [!DNL Google BigQuery] Platforms met behulp van API&#39;s of de gebruikersinterface:

### API&#39;s gebruiken

- [Een Google BigQuery-basisverbinding maken met de Flow Service API](../../tutorials/api/create/databases/bigquery.md)
- [Gegevenstabellen verkennen met de Flow Service API](../../tutorials/api/explore/tabular.md)
- [Een gegevensstroom maken voor een databasebron met behulp van de Flow Service API](../../tutorials/api/collect/database-nosql.md)

### De gebruikersinterface gebruiken

- [Een Google BigQuery-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/databases/bigquery.md)
- [Een gegevensstroom maken voor een databasebronverbinding in de gebruikersinterface](../../tutorials/ui/dataflow/databases.md)

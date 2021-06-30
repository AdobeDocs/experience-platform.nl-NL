---
keywords: Experience Platform;home;populaire onderwerpen;BigQuery;bigquery;Google BigQuery;google bigquery
solution: Experience Platform
title: Overzicht van Google BigQuery Source Connector
topic-legacy: overview
description: Leer hoe u Google BigQuery via API's of de gebruikersinterface met Adobe Experience Platform kunt verbinden.
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 5821f9304a37c1a03d17f0113d09548799662a2e
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# (Bèta) [!DNL Google BigQuery]-connector

>[!NOTE]
>
>De [!DNL Google BigQuery] is in bèta. Zie [Bronoverzicht](../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de services van het Platform. U kunt gegevens van diverse bronnen, zoals Adobe-toepassingen, cloudopslag, databases en vele andere, invoeren.

[!DNL Experience Platform] verleent steun voor het opnemen van gegevens van een derdegegevensbestand. Het Platform kan met verschillende types van gegevensbestanden zoals relationeel, NoSQL, of gegevenspakhuizen verbinden. Tot de ondersteuning voor databaseproviders behoren [!DNL Google BigQuery].

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie [IP adres lijst van gewenste personen](../../ip-address-allow-list.md) pagina voor meer informatie.

## Vereisten

In de volgende sectie vindt u meer informatie over de vereiste configuratie voordat u een [!DNL Google BigQuery]-bronverbinding kunt maken.

### Uw [!DNL Google BigQuery]-referenties genereren

Als u [!DNL Google BigQuery] wilt verbinden met Platform, moet u waarden voor de volgende referenties genereren:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `project` | Het project is de organisatie op basisniveau voor uw [!DNL Google Cloud] bronnen, inclusief [!DNL Google BigQuery]. |
| `clientID` | De client-id is de helft van uw [!DNL Google BigQuery] OAuth 2.0-referenties. |
| `clientSecret` | Het clientgeheim is de andere helft van uw [!DNL Google BigQuery] OAuth 2.0-referenties. |
| `refreshToken` | Met het token Vernieuwen kunt u nieuwe toegangstokens voor uw API verkrijgen. Toegangstokens hebben beperkte levensduur en kunnen verlopen tijdens de uitvoering van uw project. U kunt gebruiken verfrist teken om verdere toegangstokens voor uw project voor authentiek te verklaren en te verzoeken wanneer nodig. |

Voor gedetailleerde instructies op hoe te om geloofsbrieven OAuth 2.0 voor [!DNL Google] APIs te produceren, zie volgende [[!DNL Google] OAuth 2.0 authentificatiegids](https://developers.google.com/identity/protocols/oauth2).

## [!DNL Google BigQuery] verbinden met Platform

De onderstaande documentatie biedt informatie over hoe u [!DNL Google BigQuery] kunt verbinden met een Platform via API&#39;s of de gebruikersinterface:

### API&#39;s gebruiken

- [Een Google BigQuery-basisverbinding maken met de Flow Service API](../../tutorials/api/create/databases/bigquery.md)
- [Onderzoek de gegevensstructuur en de inhoud van een gegevensbestandbron gebruikend de Dienst API van de Stroom](../../tutorials/api/explore/database-nosql.md)
- [Een gegevensstroom maken voor een databasebron met behulp van de Flow Service API](../../tutorials/api/collect/database-nosql.md)

### De gebruikersinterface gebruiken

- [Een Google BigQuery-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/databases/bigquery.md)
- [Een gegevensstroom maken voor een databasebronverbinding in de gebruikersinterface](../../tutorials/ui/dataflow/databases.md)

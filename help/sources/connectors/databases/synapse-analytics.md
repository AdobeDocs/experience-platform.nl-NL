---
keywords: Experience Platform;home;populaire onderwerpen;Azure synapse Analytics;azure synapse Analytics;Synapse;synapse
solution: Experience Platform
title: Overzicht van azure synapse Analytics Source Connector
topic: ' - overzicht'
description: Leer hoe u Azure synapse Analytics met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
translation-type: tm+mt
source-git-commit: 0fb97fcf5d3f8230ff86906aeef245e4a7f44f30
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---


# (Bèta) [!DNL Azure Synapse Analytics]-connector

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen en biedt u de mogelijkheid om inkomende gegevens te structureren, labelen en verbeteren met behulp van [!DNL Platform]-services. U kunt gegevens van diverse bronnen, zoals Adobe-toepassingen, cloudopslag, databases en vele andere, invoeren.

[!DNL Experience Platform] verleent steun voor het opnemen van gegevens van een derdegegevensbestand. [!DNL Platform] kan met verschillende types van gegevensbestanden zoals relationeel, NoSQL, of gegevenspakhuizen verbinden. Tot de ondersteuning voor databaseproviders behoren [!DNL Azure Synapse Analytics].

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie [IP adres lijst van gewenste personen](../../ip-address-allow-list.md) pagina voor meer informatie.

>[!IMPORTANT]
>
>De [!DNL Azure Synapse Analytics] bronschakelaar steunt momenteel zelfde-gebiedconnectiviteit aan Platform niet. Dit betekent dat als uw Azure-instantie hetzelfde netwerkgebied gebruikt als Platform, een verbinding met bronnen van Platforms niet tot stand kan worden gebracht. Momenteel wordt alleen connectiviteit tussen regio&#39;s ondersteund. Neem contact op met uw Adobe-accountmanager voor meer informatie.

In de onderstaande documentatie vindt u informatie over hoe u [!DNL Azure Synapse Analytics] kunt verbinden met [!DNL Platform] via API&#39;s of de gebruikersinterface:

## Verbind [!DNL Azure Synapse Analytics] met [!DNL Platform] gebruikend APIs

- [Een Azure synapse Analytics-bronverbinding maken met de Flow Service API](../../tutorials/api/create/databases/synapse-analytics.md)
- [Een databasesysteem verkennen met de Flow Service API](../../tutorials/api/explore/database-nosql.md)
- [Gegevens verzamelen van een database met behulp van de Flow Service API](../../tutorials/api/collect/database-nosql.md)

## [!DNL Azure Synapse Analytics] verbinden met [!DNL Platform] gebruikend UI

- [Een Azure synapse Analytics-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/databases/synapse-analytics.md)
- [Een gegevensstroom configureren voor een databaseverbinding in de gebruikersinterface](../../tutorials/ui/dataflow/databases.md)
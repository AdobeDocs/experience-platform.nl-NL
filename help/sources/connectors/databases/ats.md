---
keywords: Experience Platform;thuis;populaire onderwerpen;Azure Table Storage;azure table storage;ATS;ats
solution: Experience Platform
title: Azure Table Storage Source Connector - Overzicht
topic-legacy: overview
description: Leer hoe u Azure Table Storage kunt verbinden met Adobe Experience Platform via API's of de gebruikersinterface.
exl-id: 096e01b1-7e95-4e30-87de-d0976f8b438a
source-git-commit: 7af79b9e0d6ed29b796ac7c98b4df1dda09f3513
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# [!DNL Azure Table Storage] connector

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de services van het Platform. U kunt gegevens van diverse bronnen, zoals Adobe-toepassingen, cloudopslag, databases en vele andere, invoeren.

Experience Platform verleent steun voor het opnemen van gegevens van een derdegegevensbestand. Het Platform kan met verschillende types van gegevensbestanden zoals relationeel, NoSQL, of gegevenspakhuizen verbinden. Tot de ondersteuning voor databaseproviders behoren [!DNL Azure Table Storage].

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie [IP adres lijst van gewenste personen](../../ip-address-allow-list.md) pagina voor meer informatie.

>[!IMPORTANT]
>
>De [!DNL Azure Table Storage] bronschakelaar steunt momenteel zelfde-gebiedconnectiviteit aan Platform niet. Dit betekent dat als uw Azure-instantie hetzelfde netwerkgebied gebruikt als Platform, een verbinding met bronnen van Platforms niet tot stand kan worden gebracht. Momenteel wordt alleen connectiviteit tussen regio&#39;s ondersteund. Neem contact op met uw Adobe-accountmanager voor meer informatie.

De onderstaande documentatie biedt informatie over hoe u [!DNL Azure Table Storage] kunt verbinden met een Platform via API&#39;s of de gebruikersinterface:

## [!DNL Azure Table Storage] verbinden met Platform met behulp van API&#39;s

- [Een Azure Table Storage-basisverbinding maken met de Flow Service API](../../tutorials/api/create/databases/ats.md)
- [Onderzoek de gegevensstructuur en de inhoud van een gegevensbestandbron gebruikend de Dienst API van de Stroom](../../tutorials/api/explore/database-nosql.md)
- [Een gegevensstroom maken voor een databasebron met behulp van de Flow Service API](../../tutorials/api/collect/database-nosql.md)

## [!DNL Azure Table Storage] verbinden met Platform gebruikend UI

- [Een Azure Table Storage-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/databases/ats.md)
- [Een gegevensstroom maken voor een databasebronverbinding in de gebruikersinterface](../../tutorials/ui/dataflow/databases.md)

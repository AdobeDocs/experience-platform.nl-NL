---
keywords: Experience Platform;thuis;populaire onderwerpen;Azure Table Storage;azure table storage;ATS;ats
solution: Experience Platform
title: Azure Table Storage Source Connector - Overzicht
topic: ' - overzicht'
description: Leer hoe u Azure Table Storage kunt verbinden met Adobe Experience Platform via API's of de gebruikersinterface.
translation-type: tm+mt
source-git-commit: 0fb97fcf5d3f8230ff86906aeef245e4a7f44f30
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---


# (Bèta) [!DNL Azure Table Storage]-connector

>[!NOTE]
>
>De [!DNL Azure Table Storage] schakelaar is in bèta. Zie [Bronoverzicht](../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen en biedt u de mogelijkheid om inkomende gegevens te structureren, labelen en verbeteren met behulp van [!DNL Platform]-services. U kunt gegevens van diverse bronnen, zoals Adobe-toepassingen, cloudopslag, databases en vele andere, invoeren.

[!DNL Experience Platform] verleent steun voor het opnemen van gegevens van een derdegegevensbestand. [!DNL Platform] kan met verschillende types van gegevensbestanden zoals relationeel, NoSQL, of gegevenspakhuizen verbinden. Tot de ondersteuning voor databaseproviders behoren [!DNL Azure Table Storage].

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie [IP adres lijst van gewenste personen](../../ip-address-allow-list.md) pagina voor meer informatie.

>[!IMPORTANT]
>
>De [!DNL Azure Table Storage] bronschakelaar steunt momenteel zelfde-gebiedconnectiviteit aan Platform niet. Dit betekent dat als uw Azure-instantie hetzelfde netwerkgebied gebruikt als Platform, een verbinding met bronnen van Platforms niet tot stand kan worden gebracht. Momenteel wordt alleen connectiviteit tussen regio&#39;s ondersteund. Neem contact op met uw Adobe-accountmanager voor meer informatie.

In de onderstaande documentatie vindt u informatie over hoe u [!DNL Azure Table Storage] kunt verbinden met [!DNL Platform] via API&#39;s of de gebruikersinterface:

## Verbind [!DNL Azure Table Storage] met [!DNL Platform] gebruikend APIs

- [Een Azure Table Storage-bronverbinding maken met de Flow Service API](../../tutorials/api/create/databases/ats.md)
- [Een databasesysteem verkennen met de Flow Service API](../../tutorials/api/explore/database-nosql.md)
- [Gegevens verzamelen van een database met behulp van de Flow Service API](../../tutorials/api/collect/database-nosql.md)

## [!DNL Azure Table Storage] verbinden met [!DNL Platform] gebruikend UI

- [Een Azure Table Storage-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/databases/ats.md)
- [Een gegevensstroom configureren voor een databaseverbinding in de gebruikersinterface](../../tutorials/ui/dataflow/databases.md)
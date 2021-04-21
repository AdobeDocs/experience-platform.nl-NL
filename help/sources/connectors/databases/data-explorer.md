---
keywords: Experience Platform;thuis;populaire onderwerpen;Azure Data Explorer;azure Data Explorer
solution: Experience Platform
title: Azure Data Explorer Source Connector - Overzicht
topic-legacy: overview
description: Leer hoe u Azure Data Explorer met Adobe Experience Platform verbindt via API's of de gebruikersinterface.
exl-id: 869bd8bb-51e6-4e0c-a3ec-ff083dda5789
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# (Bèta) [!DNL Azure Data Explorer]-connector

>[!NOTE]
>
>De [!DNL Azure Data Explorer] schakelaar is in bèta. Zie [Bronoverzicht](../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Adobe Experience Platform biedt native connectiviteit voor databaseproviders zoals [!DNL Microsoft], MySQL en [!DNL Azure]. U kunt uw gegevens van deze systemen naar [!DNL Platform] brengen.

Verschillende soorten derdegegevensbestanden worden gesteund, met inbegrip van relationele, NoSQL, of gegevenspakhuizen. Ondersteuning voor databaseproviders omvat [!DNL Azure Data Explorer].

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie [IP adres lijst van gewenste personen](../../ip-address-allow-list.md) pagina voor meer informatie.

>[!IMPORTANT]
>
>De [!DNL Azure Data Explorer] bronschakelaar steunt momenteel zelfde-gebiedconnectiviteit aan Platform niet. Dit betekent dat als uw Azure-instantie hetzelfde netwerkgebied gebruikt als Platform, een verbinding met bronnen van Platforms niet tot stand kan worden gebracht. Momenteel wordt alleen connectiviteit tussen regio&#39;s ondersteund. Neem contact op met uw Adobe-accountmanager voor meer informatie.

In de onderstaande documentatie vindt u informatie over hoe u [!DNL Azure Data Explorer] kunt verbinden met [!DNL Platform] via API&#39;s of de gebruikersinterface:

## Verbind [!DNL Azure Data Explorer] met [!DNL Platform] gebruikend APIs

- [Een Azure Data Explorer-bronverbinding maken met de Flow Service API](../../tutorials/api/create/databases/data-explorer.md)
- [Een databasesysteem verkennen met de Flow Service API](../../tutorials/api/explore/database-nosql.md)
- [Gegevens verzamelen van een database met behulp van de Flow Service API](../../tutorials/api/collect/database-nosql.md)

## [!DNL Azure Data Explorer] verbinden met [!DNL Platform] gebruikend UI

- [Een Azure Data Explorer-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/databases/data-explorer.md)
- [Een gegevensstroom configureren voor een databaseverbinding in de gebruikersinterface](../../tutorials/ui/dataflow/databases.md)

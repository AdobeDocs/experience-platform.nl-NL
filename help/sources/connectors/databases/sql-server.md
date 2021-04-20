---
keywords: Experience Platform;home;populaire onderwerpen;Microsoft SQL;microsoft sql;SQL;sql
solution: Experience Platform
title: Overzicht van SQL Server Source Connector
topic: overview
description: Leer hoe u Microsoft SQL Server met Adobe Experience Platform kunt verbinden met behulp van API's of de gebruikersinterface.
translation-type: tm+mt
source-git-commit: 0fb97fcf5d3f8230ff86906aeef245e4a7f44f30
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# (Bèta) [!DNL Microsoft] SQL Server-connector

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen en biedt u de mogelijkheid om inkomende gegevens te structureren, labelen en verbeteren met behulp van [!DNL Platform]-services. U kunt gegevens van diverse bronnen, zoals Adobe-toepassingen, cloudopslag, databases en vele andere, invoeren.

[!DNL Experience Platform] verleent steun voor het opnemen van gegevens van een derdegegevensbestand. [!DNL Platform] kan met verschillende types van gegevensbestanden zoals relationeel, NoSQL, of gegevenspakhuizen verbinden. De steun voor gegevensbestandleveranciers omvat [!DNL Microsoft] SQL Server.

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie [IP adres lijst van gewenste personen](../../ip-address-allow-list.md) pagina voor meer informatie.

>[!IMPORTANT]
>
>De [!DNL Microsoft] SQL de bronschakelaar van de Server steunt momenteel zelfde-gebiedconnectiviteit aan Platform niet. Dit betekent dat als uw Azure-instantie hetzelfde netwerkgebied gebruikt als Platform, een verbinding met bronnen van Platforms niet tot stand kan worden gebracht. Momenteel wordt alleen connectiviteit tussen regio&#39;s ondersteund. Neem contact op met uw Adobe-accountmanager voor meer informatie.

De documentatie hieronder verstrekt informatie over hoe te om [!DNL Microsoft] SQL Server aan [!DNL Platform] te verbinden gebruikend APIs of de gebruikersinterface:

## Verbind [!DNL Microsoft] SQL Server met [!DNL Platform] gebruikend APIs

- [Een Microsoft SQL Server-bronverbinding maken met de Flow Service API](../../tutorials/api/create/databases/sql-server.md)
- [Een databasesysteem verkennen met de Flow Service API](../../tutorials/api/explore/database-nosql.md)
- [Gegevens verzamelen van een database met behulp van de Flow Service API](../../tutorials/api/collect/database-nosql.md)

## Verbind [!DNL Microsoft] SQL Server met [!DNL Platform] gebruikend UI

- [Een Microsoft SQL Server-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/databases/sql-server.md)
- [Een gegevensstroom configureren voor een databaseverbinding in de gebruikersinterface](../../tutorials/ui/dataflow/databases.md)
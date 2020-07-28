---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: MySQL-connector
topic: overview
translation-type: tm+mt
source-git-commit: 3b5e76afea5689dbd59f64f6192e6ef2a6acb7d3
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# (Beta) MySQL-connector

>[!NOTE]
>De MySQL-connector is in bèta. Zie het [Bronoverzicht](../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Met Adobe Experience Platform kunnen gegevens uit externe bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van [!DNL Platform] services. U kunt gegevens van diverse bronnen, zoals Adobe-toepassingen, cloudopslag, databases en vele andere, invoeren.

[!DNL Experience Platform] verleent steun voor het opnemen van gegevens van een derdegegevensbestand. [!DNL Platform] kan verbinding maken met verschillende typen databases, zoals relationeel, NoSQL of data warehouse. Tot de ondersteuning voor databaseproviders behoort MySQL.

## IP adres lijst van gewenste personen

De volgende IP adressen moeten aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen.

### Oost-Amerikaanse regio

- `20.41.2.0/23`
- `20.41.4.0/26`
- `20.44.17.80/28`
- `20.49.102.16/29`
- `40.70.148.160/28`
- `52.167.107.224/28`

### West-Europa

- `13.69.67.192/28`
- `13.69.107.112/28`
- `13.69.112.128/28`
- `40.74.24.192/26`
- `40.74.26.0/23`
- `40.113.176.232/29`
- `52.236.187.112/28`

### Australië - oost

- `13.70.74.144/28`
- `20.37.193.0/25`
- `20.37.193.128/26`
- `20.37.198.224/29`
- `40.79.163.80/28`
- `40.79.171.160/28`

In de onderstaande documentatie vindt u informatie over hoe u MySQL kunt verbinden met het [!DNL Platform] gebruik van API&#39;s of de gebruikersinterface:

## MySQL verbinden met API&#39;s [!DNL Platform]

- [Een MySQL-connector maken met de Flow Service API](../../tutorials/api/create/databases/mysql.md)
- [Een databasesysteem verkennen met de Flow Service API](../../tutorials/api/explore/database-nosql.md)
- [Gegevens verzamelen van een database met behulp van de Flow Service API](../../tutorials/api/collect/database-nosql.md)

## Verbinding maken met MySQL om de gebruikersinterface te [!DNL Platform] gebruiken

- [Creeer een MySQL bronschakelaar in UI](../../tutorials/ui/create/databases/mysql.md)
- [Vorm een dataflow voor een gegevensbestandschakelaar in UI](../../tutorials/ui/dataflow/databases.md)
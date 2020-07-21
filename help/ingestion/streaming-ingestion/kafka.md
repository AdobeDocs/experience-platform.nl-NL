---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Kafka-connector
topic: overview
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---


# [!DNL Kafka] connector voor Adobe Experience Platform

De stroomschakelaar voor Adobe Experience Platform is gebaseerd op [!DNL Apache Kafka Connect]. Deze bibliotheek kan worden gebruikt om JSON-gebeurtenissen van [!DNL Kafka] onderwerpen in uw datacenter rechtstreeks naar [!DNL Experience Platform] in real-time te streamen.

De stroomschakelaar is een gootsteen (unidirectionele) schakelaar, leverend gegevens van [!DNL Kafka] onderwerpen aan een geregistreerd eindpunt op [!DNL Experience Platform]. Als u deze connector wilt gebruiken, moet u de bibliotheek downloaden, deze toevoegen aan uw bestaande [!DNL Kafka] implementatie en het [!DNL Kafka] onderwerp of de onderwerpen configureren naar de HTTP-URL voor streaming van Adobe. Aanvullende code is **niet** vereist. De schakelaar steunt de volgende eigenschappen:

- Geverifieerde verzameling van gegevens
- Berichten in batches om netwerkaanroepen te verminderen en de doorvoer te verhogen

Lees voor meer informatie over de [!DNL Kafka] connector, inclusief instructies over het instellen van de connector, de [gids](https://github.com/adobe/experience-platform-streaming-connect)Aan de slag. Lees de handleiding voor [ontwikkelaars voor een gedetailleerdere workflow](https://github.com/adobe/experience-platform-streaming-connect/blob/master/DEVELOPER_GUIDE.md).
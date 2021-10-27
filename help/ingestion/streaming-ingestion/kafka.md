---
keywords: Experience Platform;thuis;populaire onderwerpen;kafka;kafka-connector;Kafka;
solution: Experience Platform
title: Kafka Connector
topic-legacy: overview
description: De streamaansluiting voor Adobe Experience Platform is gebaseerd op Apache Kafka Connect. Deze bibliotheek kan worden gebruikt om JSON-gebeurtenissen van Kafka-onderwerpen in uw datacenter rechtstreeks naar Experience Platform in real-time te streamen.
exl-id: 062963e5-c727-4c2c-97db-8a9a5a7d903c
source-git-commit: 5a3aa74ca7319235c10902422abc0e897ad823b8
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# [!DNL Kafka] connector voor Adobe Experience Platform (afgekeurd)

>[!IMPORTANT]
>
>De Kafka-connector is afgekeurd. Raadpleeg de zelfstudie voor informatie over het maken van een streamingverbinding en het verzenden van gegevens naar Adobe Experience Platform. [een HTTP API-streamingverbinding maken](../../sources/connectors/streaming/http.md)

De streamconnector voor Adobe Experience Platform is gebaseerd op [!DNL Apache Kafka Connect]. Deze bibliotheek kan worden gebruikt om JSON-gebeurtenissen te streamen vanaf [!DNL Kafka] onderwerpen in uw datacenter rechtstreeks [!DNL Experience Platform] in real time.

De streamconnector is een sink-aansluiting (one-way) die gegevens levert van [!DNL Kafka] onderwerpen aan een geregistreerd eindpunt op [!DNL Experience Platform]. Als u deze connector wilt gebruiken, moet u de bibliotheek downloaden en toevoegen aan uw bestaande [!DNL Kafka] implementatie, en configureer de [!DNL Kafka] naar de HTTP-URL voor streaming Adobe. Aanvullende code is **niet** vereist. De schakelaar steunt de volgende eigenschappen:

- Geverifieerde verzameling van gegevens
- Het in batch plaatsen van berichten om netwerkvraag te verminderen en productie te verhogen

Voor meer informatie over de [!DNL Kafka] -aansluiting, inclusief instructies voor het instellen van de aansluiting, lees de [gids Aan de slag](https://github.com/adobe/experience-platform-streaming-connect). Voor een gedetailleerdere workflow leest u de [ontwikkelaarsgids](https://www.adobe.com/go/kafka-connector-developer-guide).

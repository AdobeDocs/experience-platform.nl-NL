---
keywords: Experience Platform;home;popular topics;kafka;kafka connector;Kafka;
solution: Experience Platform
title: Kafka-connector
topic: overview
description: De streamaansluiting voor Adobe Experience Platform is gebaseerd op Apache Kafka Connect. Deze bibliotheek kan worden gebruikt om JSON-gebeurtenissen van Kafka-onderwerpen in uw datacenter rechtstreeks naar Experience Platform in real-time te streamen.
translation-type: tm+mt
source-git-commit: 7fc7f0e525d994904dc71b1eb7136f11c05d5672
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---


# [!DNL Kafka] connector voor Adobe Experience Platform

De streamconnector voor Adobe Experience Platform is gebaseerd op [!DNL Apache Kafka Connect]. Deze bibliotheek kan worden gebruikt om JSON-gebeurtenissen van [!DNL Kafka] onderwerpen in uw datacenter rechtstreeks naar [!DNL Experience Platform] in real-time te streamen.

De stroomschakelaar is een gootsteen (unidirectionele) schakelaar, leverend gegevens van [!DNL Kafka] onderwerpen aan een geregistreerd eindpunt op [!DNL Experience Platform]. Om deze schakelaar te gebruiken, moet u de bibliotheek downloaden, het toevoegen aan uw bestaande [!DNL Kafka] plaatsing, en [!DNL Kafka] onderwerp(en) vormen aan de Adobe die HTTP URL stromen. Aanvullende code is **niet** vereist. De schakelaar steunt de volgende eigenschappen:

- Geverifieerde verzameling van gegevens
- Het in batch plaatsen van berichten om netwerkvraag te verminderen en productie te verhogen

Lees voor meer informatie over de [!DNL Kafka] connector, inclusief instructies over het instellen van de connector, de [gids](https://github.com/adobe/experience-platform-streaming-connect)Aan de slag. Lees de handleiding voor [ontwikkelaars voor een gedetailleerdere workflow](https://www.adobe.com/go/kafka-connector-developer-guide).
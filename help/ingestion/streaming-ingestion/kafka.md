---
keywords: Experience Platform;thuis;populaire onderwerpen;kafka;kafka-connector;Kafka;
solution: Experience Platform
title: Kafka Connector
description: De streamaansluiting voor Adobe Experience Platform is gebaseerd op Apache Kafka Connect. Deze bibliotheek kan worden gebruikt om JSON-gebeurtenissen van Kafka-onderwerpen in uw datacenter rechtstreeks naar Experience Platform in real-time te streamen.
exl-id: 062963e5-c727-4c2c-97db-8a9a5a7d903c
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---

# [!DNL Kafka] -connector voor Adobe Experience Platform

De streamconnector voor Adobe Experience Platform is gebaseerd op [!DNL Apache Kafka Connect] . Deze bibliotheek kan worden gebruikt om JSON-gebeurtenissen vanuit [!DNL Kafka] -onderwerpen in uw datacenter rechtstreeks te streamen naar [!DNL Experience Platform] in real-time.

De streamconnector is een &#39;sink&#39;-connector (one-way) die gegevens van [!DNL Kafka] -onderwerpen levert aan een geregistreerd eindpunt op [!DNL Experience Platform] . Als u deze connector wilt gebruiken, moet u de bibliotheek downloaden, deze toevoegen aan uw bestaande [!DNL Kafka] -implementatie en de [!DNL Kafka] -onderwerpen configureren naar de HTTP-URL voor streaming van de Adobe. De extra code wordt **niet** vereist. De schakelaar steunt de volgende eigenschappen:

- Geverifieerde verzameling van gegevens
- Berichten in batches om netwerkaanroepen te verminderen en de doorvoer te verhogen

Voor meer informatie over de [!DNL Kafka] schakelaar, met inbegrip van instructies op hoe te opstelling de schakelaar, gelieve te lezen [ begonnen gids ](https://github.com/adobe/experience-platform-streaming-connect) wordt begonnen. Voor een meer gedetailleerd werkschema, te lezen gelieve de [ ontwikkelaarsgids ](https://www.adobe.com/go/kafka-connector-developer-guide).

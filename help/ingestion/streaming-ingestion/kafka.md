---
keywords: Experience Platform;thuis;populaire onderwerpen;kafka;kafka-connector;Kafka;
solution: Experience Platform
title: Kafka Connector
topic: overview
description: De streamaansluiting voor Adobe Experience Platform is gebaseerd op Apache Kafka Connect. Deze bibliotheek kan worden gebruikt om JSON-gebeurtenissen van Kafka-onderwerpen in uw datacenter rechtstreeks naar Experience Platform in real-time te streamen.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# [!DNL Kafka] connector voor Adobe Experience Platform

De stroomconnector voor Adobe Experience Platform is gebaseerd op [!DNL Apache Kafka Connect]. Deze bibliotheek kan worden gebruikt om JSON-gebeurtenissen vanuit [!DNL Kafka]-onderwerpen in uw datacenter rechtstreeks te streamen naar [!DNL Experience Platform] in real-time.

De stroomschakelaar is een gootsteen (eenrichtings) schakelaar, leverend gegevens van [!DNL Kafka] onderwerpen aan een geregistreerd eindpunt op [!DNL Experience Platform]. Als u deze connector wilt gebruiken, moet u de bibliotheek downloaden, deze toevoegen aan uw bestaande [!DNL Kafka]-implementatie en het [!DNL Kafka]-onderwerp(en) configureren naar de HTTP-URL voor streaming van de Adobe. Aanvullende code is **niet** vereist. De schakelaar steunt de volgende eigenschappen:

- Geverifieerde verzameling van gegevens
- Het in batch plaatsen van berichten om netwerkvraag te verminderen en productie te verhogen

Voor meer informatie over de [!DNL Kafka] schakelaar, met inbegrip van instructies over hoe te opstelling de schakelaar, te lezen [begonnen gids](https://github.com/adobe/experience-platform-streaming-connect). Lees de [handleiding voor ontwikkelaars](https://www.adobe.com/go/kafka-connector-developer-guide) voor een gedetailleerdere workflow.
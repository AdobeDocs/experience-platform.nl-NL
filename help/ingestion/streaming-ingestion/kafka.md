---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Kafka-connector
topic: overview
translation-type: tm+mt
source-git-commit: f80b2e1d787d1f8d9fe8ac306422aa7744a69cd3

---


# Kafka-connector voor Adobe Experience Platform

De streamaansluiting voor het Adobe Experience Platform is gebaseerd op Apache Kafka Connect. Deze bibliotheek kan worden gebruikt om JSON-gebeurtenissen van Kafka-onderwerpen in uw datacenter rechtstreeks te streamen naar Experience Platform in real-time.

De stroomschakelaar is een gootsteen (unidirectionele) schakelaar, leverend gegevens van onderwerpen Kafka aan een geregistreerd eindpunt op het Platform van de Ervaring. Als u deze connector wilt gebruiken, moet u de bibliotheek downloaden, deze toevoegen aan uw bestaande Kafka-implementatie en het Kafka-onderwerp of de Kafka-onderwerpen configureren naar de HTTP-URL voor streaming van Adobe. Aanvullende code is **niet** vereist. De schakelaar steunt de volgende eigenschappen:

- Geverifieerde verzameling van gegevens
- Berichten in batches om netwerkaanroepen te verminderen en de doorvoer te verhogen

Lees voor meer informatie over de Kafka-connector, inclusief instructies over het instellen van de connector, de gids [Aan de slag](https://github.com/adobe/experience-platform-streaming-connect). Lees de handleiding voor [ontwikkelaars voor een gedetailleerdere workflow](https://github.com/adobe/experience-platform-streaming-connect/blob/master/DEVELOPER_GUIDE.md).
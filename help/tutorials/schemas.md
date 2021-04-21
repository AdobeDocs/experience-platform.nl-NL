---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: XDM-schema's en -beschrijvingen
topic-legacy: tutorial
type: Tutorial
description: Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter Adobe Experience Platform. Het Model van Gegevens van de ervaring (XDM), die door Adobe wordt gedreven, is een inspanning om de gegevens van de klantenervaring te standaardiseren en schema's voor het beheer van de klantenervaring te bepalen. De schema's zijn de standaardmanier om gegevens in Experience Platform te beschrijven, toestaand alle gegevens die aan schema's in overeenstemming zijn herbruikbaar zonder conflicten over een organisatie en zelfs om tussen veelvoudige organisaties te kunnen delen.
exl-id: 1cdc45d7-57ca-4a2d-99a4-9a8cd885a511
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# Werken met [!DNL Experience Data Model] (XDM) schema&#39;s en relatiebeschrijvers

Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter Adobe Experience Platform. [!DNL Experience Data Model] (XDM), gedreven door Adobe, is een inspanning om de gegevens van de klantenervaring te standaardiseren en schema&#39;s voor het beheer van de klantenervaring te bepalen. Schema&#39;s zijn de standaardmanier om gegevens te beschrijven in [!DNL Experience Platform], zodat alle gegevens die aan schema&#39;s voldoen opnieuw kunnen worden gebruikt zonder conflicten in een organisatie en zelfs tussen meerdere organisaties kunnen worden gedeeld. Om meer over schema&#39;s te leren XDM, begin door [XDM systeemoverzicht](../xdm/home.md) te lezen.

## Een schema maken met behulp van het schemaregister

Het schemaregister biedt een gebruikersinterface en RESTful-API waarmee u alle bronnen in de Adobe Experience Platform-schemabibliotheek kunt weergeven en beheren. De bibliotheek van het Schema bevat middelen die aan u door Adobe, [!DNL Experience Platform] partners, en verkopers worden ter beschikking gesteld de waarvan toepassingen u gebruikt, evenals middelen die u bepaalt en aan de Registratie van het Schema opslaat. Leer hoe te om schema&#39;s voor uw organisatie tot stand te brengen, volg de leerprogramma&#39;s voor [creërend een schema gebruikend de Registratie API](../xdm/tutorials/create-schema-api.md) of [creërend een schema gebruikend het gebruikersinterface van de Redacteur van het Schema](../xdm/tutorials/create-schema-ui.md).

## Een relatie tussen twee schema&#39;s definiëren

De mogelijkheid om de relaties tussen uw klanten en hun interactie met uw merk op verschillende kanalen te begrijpen is een belangrijk onderdeel van Adobe Experience Platform. Door deze relaties te definiëren binnen de structuur van uw [!DNL Experience Data Model] (XDM)-schema&#39;s kunt u complexe inzichten in uw klantgegevens opdoen. Deze relatiebeschrijvers kunnen worden bepaald gebruikend de Registratie API van het Schema en de Redacteur UI van het Schema. Voor meer informatie, zie de leerprogramma&#39;s voor het bepalen van verhoudingen tussen twee schema&#39;s [gebruikend API](../xdm/tutorials/relationship-api.md) of [gebruikend UI](../xdm/tutorials/relationship-ui.md).

## Een ad-hocschema maken

In specifieke omstandigheden, kan het noodzakelijk zijn om een [!DNL Experience Data Model] (XDM) schema met gebieden tot stand te brengen die namespaced voor gebruik slechts door één enkele dataset zijn. Dit wordt bedoeld als &quot;ad-hoc&quot;schema. Ad-hocschema&#39;s worden gebruikt in verschillende [gegevensinvoer](../ingestion/home.md)-workflows voor [!DNL Experience Platform], waaronder het opnemen van CSV-bestanden en het maken van bepaalde soorten [bronverbindingen](../sources/home.md). Het creëren van een ad hoc schema wordt gedaan gebruikend de Registratie API van het Schema en is bedoeld om samen met andere [!DNL Experience Platform] leerprogramma&#39;s worden gebruikt die het creëren van een ad hoc schema als deel van hun werkschema vereisen. Als u een ad-hocschema wilt gaan maken, raadpleegt u de zelfstudie voor het maken van een ad-hocschema met de API](../xdm/tutorials/ad-hoc.md).[

## Volgende stappen

Zodra u schema&#39;s voor uw organisatie hebt bepaald, kunt u beginnen datasets te creëren waarin de gegevens kunnen worden opgenomen. Raadpleeg de volgende documentatie om aan de slag te gaan:

* [Overzicht van gegevenssets](../catalog/datasets/overview.md)
* [Overzicht van gegevensinname](../ingestion/home.md)

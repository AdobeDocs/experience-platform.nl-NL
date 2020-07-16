---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: XDM-schema's en -beschrijvingen
topic: tutorial
translation-type: tm+mt
source-git-commit: 5c5f6c4868e195aef76bacc0a1e5df3857647bde
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---


# Werken met [!DNL Experience Data Model] (XDM) schema&#39;s en relatiebeschrijvers

Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter het Adobe Experience Platform. [!DNL Experience Data Model] (XDM), aangestuurd door Adobe, is een inspanning om de gegevens van de klantenervaring te standaardiseren en schema&#39;s voor het beheer van de klantenervaring te bepalen. Schema&#39;s zijn de standaardmanier om gegevens in te beschrijven [!DNL Experience Platform], zodat alle gegevens die aan schema&#39;s voldoen, opnieuw kunnen worden gebruikt zonder conflicten in een organisatie en zelfs tussen meerdere organisaties kunnen worden gedeeld. Voor meer informatie over XDM-schema&#39;s begint u met het lezen van het [XDM System-overzicht](../xdm/home.md).

## Een schema maken met behulp van het schemaregister

De Registratie van het Schema verstrekt een gebruikersinterface en RESTful API waarvan u alle middelen in de Bibliotheek van het Schema van het Adobe Experience Platform kunt bekijken en beheren. De Schemabibliotheek bevat middelen die aan u door Adobe, [!DNL Experience Platform] partners, en verkopers ter beschikking worden gesteld waarvan toepassingen u gebruikt, evenals middelen die u bepaalt en aan de Registratie van het Schema opslaat. Leren hoe te om schema&#39;s voor uw organisatie tot stand te brengen, volg de leerprogramma&#39;s voor het [creëren van een schema gebruikend de Registratie API](../xdm/tutorials/create-schema-api.md) van het Schema of [creërend een schema gebruikend het gebruikersinterface](../xdm/tutorials/create-schema-ui.md)van de Redacteur van het Schema.

## Een relatie tussen twee schema&#39;s definiëren

De mogelijkheid om de relaties tussen uw klanten en hun interactie met uw merk op verschillende kanalen te begrijpen is een belangrijk onderdeel van het Adobe Experience Platform. Het bepalen van deze verhoudingen binnen de structuur van uw [!DNL Experience Data Model] (XDM) schema&#39;s staat u toe om complexe inzichten in uw klantengegevens te bereiken. Deze relatiebeschrijvers kunnen worden bepaald gebruikend de Registratie API van het Schema en de Redacteur UI van het Schema. Voor meer informatie, zie de leerprogramma&#39;s voor het bepalen van verhoudingen tussen twee schema&#39;s [gebruikend API](../xdm/tutorials/relationship-api.md) of [gebruikend UI](../xdm/tutorials/relationship-ui.md).

## Een ad-hocschema maken

In specifieke omstandigheden, kan het noodzakelijk zijn om een [!DNL Experience Data Model] (XDM) schema met gebieden tot stand te brengen die namespaced voor gebruik slechts door één enkele dataset zijn. Dit wordt bedoeld als &quot;ad-hoc&quot;schema. Ad-hocschema&#39;s worden gebruikt in diverse [gegevensinsluitingsworkflows](../ingestion/home.md) voor [!DNL Experience Platform], waaronder het innemen van CSV-bestanden en het maken van bepaalde soorten [bronverbindingen](../sources/home.md). Het maken van een ad-hocschema wordt uitgevoerd met behulp van de API voor het schemaregister en is bedoeld voor gebruik in combinatie met andere [!DNL Experience Platform] zelfstudies waarvoor een ad-hocschema moet worden gemaakt als onderdeel van de workflow. Als u een ad-hocschema wilt gaan maken, raadpleegt u de zelfstudie voor het [maken van een ad-hocschema met de API](../xdm/tutorials/ad-hoc.md).

## Volgende stappen

Zodra u schema&#39;s voor uw organisatie hebt bepaald, kunt u beginnen datasets te creëren waarin de gegevens kunnen worden opgenomen. Raadpleeg de volgende documentatie om aan de slag te gaan:

* [Overzicht van gegevenssets](../catalog/datasets/overview.md)
* [Overzicht van gegevensinname](../ingestion/home.md)
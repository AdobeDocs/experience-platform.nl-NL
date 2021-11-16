---
keywords: Experience Platform;thuis;populaire onderwerpen;bronnen;connectors;bronconnectors;bronnen sdk;sdk;SDK
solution: Experience Platform
title: 'Bronnen: Overzicht SDK (bèta)'
topic-legacy: overview
description: Adobe Experience Platform Sources SDK is een set configuratie-API's waarmee u een REST API-gebaseerde bron kunt integreren met behulp van de Flow Service API om uw gegevens naar het Experience Platform te brengen.
hide: true
hidefromtoc: true
source-git-commit: bfe6be73ed05b494a4a3eb1153e53ee8b9864ecf
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# Overzicht SDK van bronnen (bètaversie)

>[!IMPORTANT]
>
>Bronnen-SDK bevindt zich momenteel in bètaversie en uw organisatie heeft mogelijk nog geen toegang tot deze SDK. De functionaliteit die in deze documentatie wordt beschreven, kan worden gewijzigd.

Adobe Experience Platform Sources SDK is een set configuratie-API&#39;s waarmee u een REST API-bron kunt integreren met behulp van de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) om uw gegevens naar het Experience Platform te brengen.

Met Bronnen SDK kunt u:

* Een nieuwe bron voor de catalogus met Platforms configureren, compleet met functies voor maken, lezen, bijwerken en verwijderen met de opdracht [!DNL Flow Service] API.
* Definieer specificaties voor uw bron, inclusief informatie over ondersteunde verificatietypen en hoe brongegevens worden opgehaald.
* Maak gebruikersgerichte documentatie voor uw nieuwe bron.

De documentatie van SDK van Bronnen verstrekt instructies voor u om Adobe Experience Platform Sources SDK te gebruiken om een REST API-based bronintegratie met Platform te vormen, te testen en vrij te geven, en uw bron te hebben deel van de steeds groeiende broncatalogus worden.

![catalogus](./assets/catalog.png)

## Bronnen begrijpen

Het Platform kan gegevens uit externe bronnen opnemen terwijl het toestaan van u om die gegevens te structureren, te etiketteren en te verbeteren gebruikend de diensten van het Platform. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Voor meer informatie over bronnen, en om een lijst van verschillende bronnen te zien momenteel gesteund op Platform, zie [overzicht van bronnen](../home.md).

## Een bron maken

Via Sources SDK kunt u uw eigen REST API-bron integreren en uw gegevens naar het Platform brengen met [!DNL Flow Service]. De bronnen SDK staat u toe om een nieuwe bron met Platform te integreren, door nieuwe verbindingsspecificatie te creëren en voor te leggen door [!DNL Flow Service] API.

Zie de handleiding op [een nieuwe verbindingsspecificatie maken](./api/overview.md) voor informatie over hoe te om een nieuwe bron aan Platform te integreren.

## Uw bron documenteren

Als uw bron is gemaakt, raadpleegt u de [documentatiehandleiding](./documentation/overview.md) voor instructies over hoe u de bron kunt documenteren via de [!DNL GitHub] webinterface of via uw eigen teksteditor.

## Proces op hoog niveau

Het stapsgewijze proces voor het configureren van uw bron in Experience Platform wordt hieronder beschreven:

* Lees de [Bronnen: SDK API-handleiding](./api/overview.md);
   * Lees de [gids Aan de slag](./api/getting-started.md);
   * Volg de zelfstudie op [een nieuwe verbindingsspecificatie maken](./api/create.md);
   * Volg de zelfstudie op [bijwerken van uw verbindingsspecificatie](./api/update-connection-specs.md);
   * Volg de zelfstudie op [het toevoegen van uw nieuwe identiteitskaart van de verbindingsspecificatie aan een stroomspecificatie](./api/update-flow-specs.md)
   * [Nieuwe bron verzenden](./api/submit.md).
* Voor een beter inzicht in de structuur en eigenschappen van een verbindingsspecificatie raadpleegt u de handleiding op [configuratieopties voor Bronnen SDK](./config/config.md);
   * Zie de handleiding op [configureren van verificatiespecificaties](./config/authspec.md);
   * Zie de handleiding op [configureren van uw bronspecificaties](./config/sourcespec.md);
   * Zie de handleiding op [configureren, specificaties](./config/explorespec.md);
* Als u wilt beginnen met het documenteren van de bron, raadpleegt u de [overzicht van het creëren van documentatie voor Bronnen SDK](./documentation/overview.md)
   * U kunt dit [source documentation template](./documentation/template.md) de structuur van uw documentatie te bepalen;
   * Zie de handleiding op [het gebruiken van de het Webinterface van GitHub](./documentation/github.md) voor stappen op hoe te om documentatie tot stand te brengen die GitHub gebruikt;
   * Zie de handleiding op [een teksteditor gebruiken](./documentation/text-editor.md) voor stappen voor het maken van documentatie met behulp van uw lokale computer.


---
keywords: Experience Platform;thuis;populaire onderwerpen;bronnen;connectors;bronconnectors;bronnen sdk;sdk;SDK
solution: Experience Platform
title: Zelfbedieningsbronnen (Batch SDK) - Overzicht
topic-legacy: overview
description: Adobe Experience Platform Self-Serve Sources (Batch SDK) is een set configuratie-API's waarmee u een REST API-bron kunt integreren met behulp van de Flow Service API om uw gegevens naar het Experience Platform te brengen.
exl-id: 5d5449ad-a1ba-402b-a281-0b2d8b704f32
source-git-commit: 4d7799b01c34f4b9e4a33c130583eadcfdc3af69
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# Overzicht van Self-Serve Sources (Batch SDK)

Adobe Experience Platform Self-Serve Sources (Batch SDK) is een framework waarmee u een REST API-gebaseerde bron kunt integreren in de catalogus met bronnen in het Experience Platform met behulp van de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Self-Serve Sources (Batch SDK) beschikt over een set configuratie-API&#39;s om uw eigen bron te maken en uw batchgegevens naar het Experience Platform te brengen.

Met Self-Serve Bronnen (Batch SDK) kunt u:

* Vorm en integreer een nieuwe bron aan de catalogus van het Experience Platform gebruikend [!DNL Flow Service] API.
* Definieer specificaties voor uw bron, inclusief informatie over ondersteunde verificatietypen en hoe brongegevens worden opgehaald.
* Maak gebruikersgerichte documentatie voor uw nieuwe bron.

De Self-Serve documentatie van Bronnen verstrekt instructies om, een REST API-Gebaseerde bronintegratie met Experience Platform te vormen te testen en vrij te geven, en uw bron te hebben deel van de alsmaar groeiende broncatalogus worden.

![catalogus](./assets/catalog.png)

## Bronnen begrijpen

Het Experience Platform kan gegevens uit externe bronnen opnemen terwijl het toestaan van u om die gegevens te structureren, te etiketteren en te verbeteren gebruikend de diensten van het Experience Platform. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Voor meer informatie over bronnen, en om een lijst van verschillende bronnen te zien momenteel gesteund op Experience Platform, zie [overzicht van bronnen](../home.md).

## Een bron maken

Via Self-Serve Sources kunt u uw eigen REST API-bron integreren en uw gegevens naar het Experience Platform brengen met [!DNL Flow Service]. U kunt een bron aan de catalogus van bronnen van het Experience Platform integreren door, nieuwe verbindingsspecificatie te creëren te vormen en voor te leggen door [!DNL Flow Service] API.

Zie de handleiding op [een nieuwe verbindingsspecificatie maken](./api/api-overview.md) voor informatie over hoe te om een nieuwe bron aan Experience Platform te integreren.

## Uw bron documenteren

Als uw bron is gemaakt, raadpleegt u de [documentatiehandleiding](./documentation/doc-overview.md) voor instructies over hoe u de bron kunt documenteren via de [!DNL GitHub] webinterface of via uw eigen teksteditor.

## Proces op hoog niveau

Het stapsgewijze proces voor het configureren van uw bron in Experience Platform wordt hieronder beschreven:

* Lees de [Zelfbedieningsbronnen (Batch SDK) API-handleiding](./api/api-overview.md).
   * Lees de [gids Aan de slag](./api/getting-started.md).
   * Volg de zelfstudie op [een nieuwe verbindingsspecificatie maken](./api/create.md).
   * Volg de zelfstudie op [bijwerken van uw verbindingsspecificatie](./api/update-connection-specs.md).
   * Volg de zelfstudie op [het toevoegen van uw nieuwe identiteitskaart van de verbindingsspecificatie aan een stroomspecificatie](./api/update-flow-specs.md)
   * [Nieuwe bron verzenden](./api/submit.md).
* Lees de handleiding voor een beter inzicht in de structuur en eigenschappen van een verbindingsspecificatie [configuratieopties voor Self-Serve Bronnen (Batch SDK)](./config/config.md).
   * Lees de handleiding op [configureren van verificatiespecificaties](./config/authspec.md) om een beter inzicht in de verschillende authentificatietypen te verkrijgen die u voor uw bron kunt gebruiken.
   * Lees de handleiding op [configureren van uw bronspecificaties](./config/sourcespec.md) voor informatie over de verschillende paginatietypen, het plannen formaten, en douaneschema&#39;s die voor uw bron kunnen worden gevormd.
   * Lees de handleiding op [configureren, specificaties](./config/explorespec.md) voor informatie over hoe u de parameters definieert die nodig zijn voor het verkennen en inspecteren van objecten in uw bron.
* Als u de bron wilt documenteren, leest u de [overzicht bij het creëren van documentatie voor Zelfbediening Bronnen](./documentation/doc-overview.md)
   * U kunt dit [bron-API documentatiesjabloon](./documentation/template.md) om uw API-documentatie te structureren.
   * U kunt dit [de documentatiesjabloon van bron UI](./documentation/ui-template.md) om uw UI-documentatie te structureren.
   * Zie de handleiding op [het gebruiken van de het Webinterface van GitHub](./documentation/github.md) voor stappen op hoe te om documentatie tot stand te brengen gebruikend GitHub.
   * Zie de handleiding op [een teksteditor gebruiken](./documentation/text-editor.md) voor stappen voor het maken van documentatie met behulp van uw lokale computer.

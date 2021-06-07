---
solution: Experience Platform
title: Gegevensmodel financiële dienstverlening ERD
topic-legacy: overview
description: Bekijk een entiteitsrelatiediagram (ERD) dat een gestandaardiseerd gegevensmodel beschrijft voor de bank-, financiële diensten- en verzekeringssector. Dit gegevensmodel is compatibel met Experience Data Model (XDM) voor gebruik in Adobe Experience Platform.
exl-id: 2e8f6b2a-10e7-4394-b45f-c03db0f25400
source-git-commit: 88c17992a391b24a76c3e387d3033df4c75a6aa6
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# [!UICONTROL Financial services] bedrijfsgegevensmodel ERD

Het volgende entiteitsrelatiediagram (ERD) vertegenwoordigt een gestandaardiseerd gegevensmodel voor de banksector, de financiële sector en de verzekeringssector (BFSI). De ERD wordt opzettelijk op een gedenormaliseerde wijze gepresenteerd en er wordt rekening mee gehouden hoe gegevens in Adobe Experience Platform worden opgeslagen.

Gebruik de volgende legenda om dit ERD te interpreteren:

* Elke entiteit die in wordt getoond is gebaseerd op een onderliggende [Klasse van het Gegevensmodel van de Ervaring (XDM)](../composition.md#class).
* Voor een bepaalde entiteit vertegenwoordigt elke rij die in **bold** wordt gemarkeerd, een veldgroep of een gegevenstype, met de relevante velden die hieronder in onbolle tekst worden weergegeven.
* De belangrijkste velden voor een bepaalde entiteit worden rood gemarkeerd.
* Alle eigenschappen die zouden kunnen worden gebruikt om individuele klanten te identificeren zijn duidelijk als &quot;identiteit&quot;, met één van deze eigenschappen duidelijk als &quot;primaire identiteit&quot;.
* Entiteitsrelaties zijn gemarkeerd als niet-afhankelijk, omdat op cookies gebaseerde gebeurtenissen vaak niet kunnen bepalen wie de transactie heeft uitgevoerd.

![](../../images/industries/financial.png)

>[!NOTE]
>
>De Experience Event-entiteit bevat het veld &quot;_ID&quot;, dat het unieke id-kenmerk (`_id`) vertegenwoordigt dat door de XDM ExperienceEvent-klasse wordt verschaft. Zie het referentiedocument op [XDM ExperienceEvent](../../classes/experienceevent.md) voor meer details over wat voor deze waarde wordt verwacht.
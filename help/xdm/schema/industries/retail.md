---
solution: Experience Platform
title: Gegevensmodel voor de detailhandel
topic-legacy: overview
description: Bekijk een diagram van de entiteitverhouding (ERD) dat een gestandaardiseerd gegevensmodel voor de kleinhandelsindustrie beschrijft, compatibel met het Model van de Gegevens van de Ervaring (XDM) voor gebruik in Adobe Experience Platform.
exl-id: 40cbb243-668b-4280-815f-1f94a06b6b87
source-git-commit: 629f47b934c59fe875a54cb13962033122097538
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# [!UICONTROL Retail] bedrijfsgegevensmodel ERD

Het volgende entiteitsrelatiediagram (ERD) vertegenwoordigt een gestandaardiseerd gegevensmodel voor de detailhandel. De ERD wordt opzettelijk op een gedenormaliseerde wijze gepresenteerd en er wordt rekening mee gehouden hoe gegevens in Adobe Experience Platform worden opgeslagen.

Gebruik de volgende legenda om dit ERD te interpreteren:

* Elke entiteit die in wordt getoond is gebaseerd op een onderliggende [Klasse van het Gegevensmodel van de Ervaring (XDM)](../composition.md#class).
* Voor een bepaalde entiteit vertegenwoordigt elke rij die in **bold** wordt gemarkeerd, een veldgroep of een gegevenstype, met de relevante velden die hieronder in onbolle tekst worden weergegeven.
* De belangrijkste velden voor een bepaalde entiteit worden rood gemarkeerd.
* Alle eigenschappen die zouden kunnen worden gebruikt om individuele klanten te identificeren zijn duidelijk als &quot;identiteit&quot;, met één van deze eigenschappen duidelijk als &quot;primaire identiteit&quot;.
* Entiteitsrelaties zijn gemarkeerd als niet-afhankelijk, omdat op cookies gebaseerde gebeurtenissen vaak niet kunnen bepalen wie de transactie heeft uitgevoerd.

![](../../images/industries/retail.png)

>[!NOTE]
>
>De Experience Event-entiteit bevat het veld &quot;_ID&quot;, dat het unieke id-kenmerk (`_id`) vertegenwoordigt dat door de XDM ExperienceEvent-klasse wordt verschaft. Zie het referentiedocument op [XDM ExperienceEvent](../../classes/experienceevent.md) voor meer details over wat voor deze waarde wordt verwacht.
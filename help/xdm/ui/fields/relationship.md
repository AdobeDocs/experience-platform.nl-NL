---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;gegevensmodel;ui;werkruimte;relatie;field;
solution: Experience Platform
title: Relatievelden definiëren in de gebruikersinterface
description: Leer hoe u een relatieveld in de gebruikersinterface van het Experience Platform definieert.
exl-id: 8a6be545-0edb-4b9c-b164-e44a7a5f54f5
source-git-commit: 7021725e011a1e1d95195c6c7318ecb5afe05ac6
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# Relatievatievelden definiëren in de UI

In het Model van Gegevens van de Ervaring (XDM), is het schema van de a [&#x200B; unie &#x200B;](../../schema/composition.md#union) een verenigde mening van alle schema&#39;s die tot de zelfde klasse behoren die ook voor [&#x200B; in real time het Profiel van de Klant &#x200B;](../../../profile/home.md) zijn toegelaten. Het samenvoegingsschema wordt gebruikt door Profiel om een volledige vertegenwoordiging van een klant van ongelijke ervaringsgegevens te construeren.

In sommige gevallen kunt u gegevens invoeren die niet noodzakelijkerwijs deel uitmaken van een profiel, maar die niettemin gerelateerd zijn aan het profiel. Een voorbeeld van dit soort gegevens zou een &quot;favoriet hotel&quot;gebied voor een klant zijn. Aangezien de kenmerken van het favoriete hotel van een persoon geen kenmerken van de persoon zelf zijn, kan een hotel het best worden weergegeven door een afzonderlijk schema op basis van een aangepaste klasse in plaats van [!DNL XDM Individual Profile] .

Aangezien de verenigingsschema&#39;s slechts op schema&#39;s worden gebaseerd die de zelfde klasse delen, eenvoudig zal het toelaten van het schema &quot;Hotels&quot;voor gebruik in Profiel zijn gebieden verenigingsschema voor [!DNL XDM Individual Profile] niet omvatten. In plaats daarvan moet u een relatie definiëren tussen &quot;Hotels&quot; en een ander schema dat tot de unie behoort. Dit impliceert het bepalen van het gebied van de a **verhouding** in een bronschema dat verwijzingen de primaire identiteit van een verwijzingsschema.

Voor gedetailleerde stappen bij het bepalen van een verband tussen twee schema&#39;s in Adobe Experience Platform UI, zie het [&#x200B; verhaal van verhouding UI &#x200B;](../../tutorials/relationship-ui.md).

---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;gegevensmodel;ui;werkruimte;relatie;field;
solution: Experience Platform
title: Relatievelden definiëren in de gebruikersinterface
description: Leer hoe u een relatieveld in de gebruikersinterface van het Experience Platform definieert.
topic: user guide
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---


# Relatievatievelden definiëren in de gebruikersinterface

In het Model van Gegevens van de Ervaring (XDM), is een [verenigingsschema](../../schema/composition.md#union) een verenigde mening van alle schema&#39;s die tot de zelfde klasse behoren die ook voor [Real-time Profiel van de Klant ](../../../profile/home.md) zijn toegelaten. Het samenvoegingsschema wordt gebruikt door Profiel om een volledige vertegenwoordiging van een klant van ongelijke ervaringsgegevens te construeren.

In sommige gevallen kunt u gegevens invoeren die niet noodzakelijkerwijs deel uitmaken van een profiel, maar die niettemin gerelateerd zijn aan het profiel. Een voorbeeld van dit soort gegevens zou een &quot;favoriet hotel&quot;gebied voor een klant zijn. Aangezien de kenmerken van het favoriete hotel van een persoon geen kenmerken van de persoon zelf zijn, kan een hotel het best worden weergegeven door een afzonderlijk schema op basis van een aangepaste klasse in plaats van [!DNL XDM Individual Profile].

Aangezien de verenigingsschema&#39;s slechts op schema&#39;s worden gebaseerd die de zelfde klasse delen, eenvoudig zal het toelaten van het &quot;Hotels&quot;schema voor gebruik in Profiel zijn gebieden verenigingsschema voor [!DNL XDM Individual Profile] niet omvatten. In plaats daarvan moet u een relatie definiëren tussen &quot;Hotels&quot; en een ander schema dat tot de unie behoort. Dit impliceert het bepalen van **relatieveld** in een bronschema dat verwijzingen de primaire identiteit van een bestemmingsschema.

Voor gedetailleerde stappen bij het bepalen van een verband tussen twee schema&#39;s in Adobe Experience Platform UI, zie [relatiezelfstudie UI](../../tutorials/relationship-ui.md).
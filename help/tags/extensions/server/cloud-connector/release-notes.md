---
title: Opmerkingen bij de release Adobe Experience Platform Cloud Connector Extension
description: De meest recente release bevat informatie over de extensie Cloud Connector in Adobe Experience Platform.
exl-id: 5ee85d9f-71f4-46ee-9064-4ceee1cf90e7
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# Opmerkingen bij de release Adobe Experience Platform Cloud Connector

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Gelieve te verwijzen naar het volgende [ document ](../../../term-updates.md) voor een geconsolideerde verwijzing van de terminologieveranderingen.

## woensdag 17 januari 2023

v1.0.1

* Probleem verhelpen waarbij een geldige JSON die in het tekstgebied Body Raw is geplakt, als een tekenreeks is opgeslagen in plaats van als een JSON.
* Instellen van Body op verzoek van GET of HEAD niet toestaan.
* Los een insect waar het bewaren van een reactie groter dan 5kb de regeluitvoering zou doen ontbreken.

---
title: Overzicht van Marketo Munchkin-extensie
description: Meer informatie over de Marketo Munchkin-tagextensie in Adobe Experience Platform.
exl-id: 8efc5203-91fc-4e89-be8f-74bf1aeeee5f
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Marketo Munchkin-extensie - overzicht

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Gebruik deze extensie om de extensie [!DNL Marketo Munchkin] JavaScript-code bijhouden met uw eigenschap. [!DNL Marketo Munchkin] JavaScript maakt het mogelijk bezoeken van eindgebruikerspagina&#39;s bij te houden en naar uw Marketo-bestemmingspagina&#39;s en externe webpagina&#39;s te navigeren.

## Marketo Munchkin-extensie installeren

Indien [!DNL Marketo Munchkin] extensie nog niet is geïnstalleerd, opent u de eigenschap en selecteert u **[!UICONTROL Extensions > Catalog]**, boven de [!DNL Marketo Munchkin] en selecteert u **[!UICONTROL Install]**.

Deze extensie heeft geen benodigde configuratie.

## Handelingstypen voor Marketo Munchkin-extensie

In deze sectie worden de actietypen beschreven die beschikbaar zijn in de [!DNL Marketo Munchkin] extensie.

### Initialiseren

![](../../../images/munchkin-Init.png)

**Munchkin-id: (vereist)** Munchkin-account-id gevonden onder Beheer > Integratie > Munchkin-menu.

**Configuraties:** Alle configureerbare parameters worden gedocumenteerd [hier](https://developers.marketo.com/javascript-api/lead-tracking/configuration/)

### Webpagina bezoeken

![](../../../images/munchkin-visit-page.png)

**URL: (vereist)** Het pad naar het URL-bestand waarmee een paginabezoek wordt opgenomen.

**param:** Een queryreeks met de gewenste parameters die moeten worden opgenomen.

**naam:** De aangepaste naam van het element van de webpagina.

### Klikken op koppeling

![](../../../images/munchkin-click-link.png)

**href: (vereist)** Het pad naar het URL-bestand waarmee een geselecteerde koppeling wordt opgenomen.

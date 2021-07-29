---
title: Overzicht van Marketo Munchkin-extensie
description: Meer informatie over de Marketo Munchkin-tagextensie in Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Marketo Munchkin-extensie - overzicht

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Gebruik deze extensie om de JavaScript-code [!DNL Marketo Munchkin] voor bijhouden in uw eigenschap te integreren. [!DNL Marketo Munchkin] JavaScript maakt het mogelijk bezoeken van eindgebruikerspagina&#39;s bij te houden en naar uw Marketo-bestemmingspagina&#39;s en externe webpagina&#39;s te navigeren.

## Marketo Munchkin-extensie installeren

Als de extensie [!DNL Marketo Munchkin] nog niet is geïnstalleerd, opent u de eigenschap en selecteert u **[!UICONTROL Extensions > Catalog]**, plaatst u de aanwijzer boven de extensie [!DNL Marketo Munchkin] en selecteert u **[!UICONTROL Install]**.

Deze extensie heeft geen benodigde configuratie.

## Handelingstypen voor Marketo Munchkin-extensie

In deze sectie worden de actietypen beschreven die beschikbaar zijn in de extensie [!DNL Marketo Munchkin].

### Initialiseren

![](../../../images/munchkin-Init.png)

**Munchkin-id: (vereist)** Munchkin-account-id gevonden onder Beheer > Integratie > Munchkin-menu.

**Configuraties:** alle configureerbare parameters worden  [hier beschreven](https://developers.marketo.com/javascript-api/lead-tracking/configuration/)

### Webpagina bezoeken

![](../../../images/munchkin-visit-page.png)

**URL: (vereist)** Het URL-bestandspad dat wordt gebruikt om een paginabezoek vast te leggen.

**params:** een queryreeks met de gewenste parameters die moeten worden opgenomen.

**name:** De aangepaste naam van het element van de webpagina.

### Klikken op koppeling

![](../../../images/munchkin-click-link.png)

**href: (vereist)** Het pad naar het URL-bestand waarmee een geselecteerde koppeling wordt opgenomen.

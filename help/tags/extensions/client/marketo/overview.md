---
title: Overzicht van Marketo Munchkin-extensie
description: Meer informatie over de Marketo Munchkin-tagextensie in Adobe Experience Platform.
exl-id: 8efc5203-91fc-4e89-be8f-74bf1aeeee5f
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# Marketo Munchkin-extensie - overzicht

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Gelieve te verwijzen naar het volgende [&#x200B; document &#x200B;](../../../term-updates.md) voor een geconsolideerde verwijzing van de terminologieveranderingen.

Gebruik deze extensie om de [!DNL Marketo Munchkin] JavaScript-trackingcode te integreren met uw eigenschap. [!DNL Marketo Munchkin] Met JavaScript kunt u bezoeken aan eindgebruikerspagina&#39;s bijhouden en naar Marketo-openingspagina&#39;s en externe webpagina&#39;s navigeren.

## Marketo Munchkin-extensie installeren

Als de extensie [!DNL Marketo Munchkin] nog niet is geïnstalleerd, opent u de eigenschap en selecteert u **[!UICONTROL Extensions > Catalog]** , plaatst u de aanwijzer op de extensie [!DNL Marketo Munchkin] en selecteert u **[!UICONTROL Install]** .

Deze extensie heeft geen benodigde configuratie.

## Handelingstypen voor Marketo Munchkin-extensie

In deze sectie worden de actietypen beschreven die beschikbaar zijn in de extensie [!DNL Marketo Munchkin] .

### Initialiseren

![](../../../images/munchkin-Init.png)

**Munchkin identiteitskaart: (vereist)** identiteitskaart van de Rekening Munchkin die onder Admin > Integratie > menu Munchkin wordt gevonden.

**Configuraties:** Alle configureerbare parameters zijn hier gedocumenteerd [&#128279;](https://developers.marketo.com/javascript-api/lead-tracking/configuration/)

### Webpagina bezoeken

![](../../../images/munchkin-visit-page.png)

**url: (vereist)** De URL dossierweg wordt gebruikt om een paginabezoek te registreren dat.

**params:** een vraagkoord van de gewenste te registreren parameters.

**naam:** de douanenaam van de Web-pagina activa.

### Klikken op koppeling

![](../../../images/munchkin-click-link.png)

**href: (vereist)** Het URL dossierweg wordt gebruikt om een verbinding te registreren uitgezocht.

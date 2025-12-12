---
title: Marketo Munchkin Extension Overzicht
description: Meer informatie over de Marketo Munchkin-tagextensie in Adobe Experience Platform.
exl-id: 8efc5203-91fc-4e89-be8f-74bf1aeeee5f
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# Marketo Munchkin-extensie - overzicht

Gebruik deze extensie om de [!DNL Marketo Munchkin] JavaScript-trackingcode te integreren met uw eigenschap. [!DNL Marketo Munchkin] Met JavaScript kunt u bezoeken aan eindgebruikerspagina&#39;s bijhouden en naar Marketo-openingspagina&#39;s en externe webpagina&#39;s navigeren.

## Marketo Munchkin-extensie installeren

Als de extensie [!DNL Marketo Munchkin] nog niet is geïnstalleerd, opent u de eigenschap en selecteert u **[!UICONTROL Extensions > Catalog]** , plaatst u de aanwijzer op de extensie [!DNL Marketo Munchkin] en selecteert u **[!UICONTROL Install]** .

Deze extensie heeft geen benodigde configuratie.

## Marketo Munchkin-extensietypen

In deze sectie worden de actietypen beschreven die beschikbaar zijn in de extensie [!DNL Marketo Munchkin] .

### Initialiseren

![](../../../images/munchkin-Init.png)

**identiteitskaart van Munchkin: (vereist)** identiteitskaart van de Rekening van Munchkin die onder Admin > Integratie > het menu van Munchkin wordt gevonden.

**Configuraties:** Alle configureerbare parameters zijn hier gedocumenteerd [&#x200B; &#x200B;](https://developers.marketo.com/javascript-api/lead-tracking/configuration/)

### Webpagina bezoeken

![](../../../images/munchkin-visit-page.png)

**url: (vereist)** De URL dossierweg wordt gebruikt om een paginabezoek te registreren dat.

**params:** een vraagkoord van de gewenste te registreren parameters.

**naam:** de douanenaam van de Web-pagina activa.

### Klikken op koppeling

![](../../../images/munchkin-click-link.png)

**href: (vereist)** Het URL dossierweg wordt gebruikt om een verbinding te registreren uitgezocht.

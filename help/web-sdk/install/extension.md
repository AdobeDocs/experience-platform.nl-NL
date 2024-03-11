---
title: De SDK van het web installeren met de tagextensie
description: Verwijs naar de bibliotheek van SDK van het Web gebruikend de Inzameling van Gegevens van Adobe Experience Cloud.
exl-id: ba8348c9-f642-4230-9f7f-4496d4154d83
source-git-commit: 58cd6300307881c3de7c52e07c401bf2ed908517
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---

# De SDK van het web installeren met de tagextensie

De Adobe biedt een specifieke markeringsuitbreiding aan om het Web SDK uit te voeren en te vormen. Deze implementatiemethode is de belangrijkste methode die door de Adobe wordt aanbevolen voor het implementeren en onderhouden van code voor gegevensverzameling.

Wanneer u voldoet aan de [voorwaarden](overview.md), kunt u de de markeringsuitbreiding van SDK van het Web opstellen door de volgende stappen te gebruiken:

## De extensie in een tag installeren

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap voor de tag of maak een eigenschap voor de tag.
1. Navigeren naar **[!UICONTROL Extensions]** en selecteert u vervolgens de **[!UICONTROL Catalog]** tab.
1. Zoek en installeer de **[!UICONTROL Adobe Experience Platform Web SDK]** extensie.
1. Selecteer de juiste sandbox en datastream voor elke omgeving en klik vervolgens op **[!UICONTROL Save]**.

Zie de documentatie over hoe u [configureren van de Web SDK-tagextensie](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) voor meer informatie .

## De code van de tag publiceren voor ontwikkeling

De Web SDK-extensie is nu geïnstalleerd voor deze tag. U kunt nu de tagcode publiceren voor gebruik in een ontwikkelomgeving.

1. Navigeren naar **[!UICONTROL Publishing flow]** selecteert u vervolgens **[!UICONTROL Add Library]**.
1. Geef deze bibliotheek een gewenste naam, zoals &quot;Add Web SDK library&quot;. Stel de [!UICONTROL Environment] vervolgkeuzelijst naar &quot;Ontwikkeling&quot;.
1. Selecteren **[!UICONTROL Add All Changed Resources]** en klik vervolgens op **[!UICONTROL Save & Build to Development]**.

## De lader-code op uw site installeren

Nu de tagcode is gepubliceerd, kunt u de code van de tagloader aan uw website toevoegen.

1. Navigeren naar **[!UICONTROL Environments]** Klik vervolgens op het pictogram Box naast &quot;Development&quot; om een modaal venster te openen met installatie-instructies voor deze omgeving.
1. De ingesloten code kopiëren en in de `<head>` -tag van uw website.

## Implementatie invullen en publiceren naar productie

Zie de [Overzicht van de Web SDK-extensie](../../tags/extensions/client/web-sdk/overview.md) voor meer informatie over de uitbreiding zelf , en [Overzicht van codes](../../tags/home.md) voor meer informatie over het navigeren door de taginterface.

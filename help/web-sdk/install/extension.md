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

Zodra u aan de [&#x200B; eerste vereisten &#x200B;](overview.md) voldoet, kunt u de de markeringsuitbreiding van SDK van het Web opstellen door de volgende stappen te gebruiken:

## De extensie in een tag installeren

1. Login aan [&#x200B; experience.adobe.com &#x200B;](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap voor de tag of maak een eigenschap voor de tag.
1. Navigeer naar **[!UICONTROL Extensions]** en selecteer vervolgens de tab **[!UICONTROL Catalog]** .
1. Zoek en installeer de extensie **[!UICONTROL Adobe Experience Platform Web SDK]** .
1. Selecteer de juiste sandbox en datastream voor elke omgeving en klik op **[!UICONTROL Save]** .

Zie de documentatie op hoe te [&#x200B; de de markeringsuitbreiding van SDK van het Web &#x200B;](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) voor meer informatie vormen.

## De labelcode naar ontwikkeling Publish

De Web SDK-extensie is nu geïnstalleerd voor deze tag. U kunt nu de tagcode publiceren voor gebruik in een ontwikkelomgeving.

1. Navigeer naar **[!UICONTROL Publishing flow]** en selecteer vervolgens **[!UICONTROL Add Library]** .
1. Geef deze bibliotheek een gewenste naam, zoals &quot;Add Web SDK library&quot;. Stel het vervolgkeuzemenu [!UICONTROL Environment] in op &quot;Ontwikkeling&quot;.
1. Selecteer **[!UICONTROL Add All Changed Resources]** en klik op **[!UICONTROL Save & Build to Development]** .

## De lader-code op uw site installeren

Nu de tagcode is gepubliceerd, kunt u de code van de tagloader aan uw website toevoegen.

1. Navigeer naar **[!UICONTROL Environments]** en klik vervolgens op het pictogram Box naast &quot;Development&quot; om een modaal venster te openen met installatie-instructies voor deze omgeving.
1. Kopieer de insluitcode en plak deze in de tag `<head>` van uw website.

## Implementatie invullen en publiceren naar productie

Zie het [&#x200B; de uitbreidingsoverzicht van SDK van het Web &#x200B;](../../tags/extensions/client/web-sdk/overview.md) voor meer informatie rond de uitbreiding zelf, en [&#x200B; overzicht van Markeringen &#x200B;](../../tags/home.md) voor meer informatie rond het navigeren van de markeringsinterface.

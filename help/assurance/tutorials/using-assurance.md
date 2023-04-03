---
title: Adobe Experience Platform Assurance gebruiken
description: In deze handleiding wordt uitgelegd hoe u Adobe Experience Platform Assurance kunt gebruiken nadat deze is geïnstalleerd en geïmplementeerd.
source-git-commit: 24f452bdb923179eefe53fdb28d3a92d43e533cd
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---


# Adobe Experience Platform Assurance gebruiken

In deze zelfstudie wordt uitgelegd hoe u Adobe Experience Platform Assurance kunt gebruiken. Voor instructies over het installeren en implementeren van de extensie Adobe Experience Platform Assurance raadpleegt u de zelfstudie over [de uitvoering van de verlenging van de betrouwbaarheidsverklaring](./implement-assurance.md).

## Sessies maken

Nadat u zich hebt aangemeld bij de [Assurance UI](https://experience.adobe.com/assurance), kunt u **[!UICONTROL Create Session]** om een sessie te beginnen maken.

![De knop voor het maken van sessies is gemarkeerd en geeft aan waar u een sessie kunt maken.](./images/using-assurance/create-session.png)

De **[!UICONTROL Create New Session]** wordt weergegeven. Controleer de gegeven instructies en ga door met **[!UICONTROL Start]**.

![Het dialoogvenster Nieuwe sessie maken wordt weergegeven met instructies over het gebruik van Verzekering.](./images/using-assurance/create-new-session.png)

U kunt nu een naam invoeren om de sessie te identificeren en vervolgens een **[!UICONTROL Base URL]** (deep linking URL for your app). Selecteer **[!UICONTROL Next]**.

>[!INFO]
>
>De basis-URL is de basisdefinitie die wordt gebruikt om uw app via een URL te starten. Er wordt een sessie-URL gegenereerd waarmee u de betrouwbaarheidssessie kunt starten. Een voorbeeldwaarde zou als kunnen kijken: `myapp://default` In de **[!UICONTROL Base URL]** veld, typt u de diepgaande-koppelingsdefinitie van de basis van uw app.

![De volledige workflow voor het maken van een nieuwe sessie wordt weergegeven.](./images/using-assurance/create-session.gif)

## Verbinding maken met een sessie

Nadat u een zitting hebt gecreeerd zorg ervoor dat u ziet **[!UICONTROL Create New Session]** toont u nu een verbinding, een QR code, en een SPELD.

![Er wordt een dialoogvenster weergegeven met de opties voor het maken van een verbinding met uw betrouwbaarheidssessie.](./images/using-assurance/create-new-session-pin.png)

Als dit dialoogvenster wordt weergegeven, kunt u de QR-code scannen met de camera-app van uw apparaat en de koppeling openen of kopiëren en openen in uw app. Wanneer uw app wordt gestart, wordt het scherm PIN-invoer weergegeven. Typ de pincode uit de vorige stap en druk op **[!UICONTROL Connect]**.

U kunt controleren of uw app is verbonden met Assurance wanneer het Adobe Experience Platform-pictogram (rode Adobe &quot;A&quot;) wordt weergegeven op uw app.

![De volledige workflow voor het verbinden van uw toepassing met een betrouwbaarheidssessie wordt weergegeven.](./images/using-assurance/connect-session.gif)

## Een sessie exporteren

Als u een betrouwbaarheidssessie wilt exporteren, selecteert u op de pagina met de sessiedetails van uw app de optie **[!UICONTROL Export to JSON]** in een sessie:

![Een sessie exporteren](./images/using-assurance/export-session.png)

De exportoptie respecteert de resultaten van het zoekfilter en exporteert alleen gebeurtenissen die in de gebeurtenisweergave worden weergegeven. Als u bijvoorbeeld hebt gezocht naar &#39;track&#39;-gebeurtenissen en vervolgens **[!UICONTROL Export to JSON]** worden alleen de resultaten van de gebeurtenis track geëxporteerd.

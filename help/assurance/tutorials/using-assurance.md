---
title: Adobe Experience Platform Assurance gebruiken
description: In deze handleiding wordt uitgelegd hoe u Adobe Experience Platform Assurance kunt gebruiken nadat deze is geïnstalleerd en geïmplementeerd.
exl-id: 872c83d1-82e8-40d8-9b66-3e51a91a955f
source-git-commit: f8576e7f7e1da7351f7860cba27d5d09d0161132
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 0%

---

# Adobe Experience Platform Assurance gebruiken

In deze zelfstudie wordt uitgelegd hoe u Adobe Experience Platform Assurance kunt gebruiken. Voor instructies op hoe te om de uitbreiding van Adobe Experience Platform Assurance te installeren en uit te voeren, te lezen gelieve het leerprogramma over [ het uitvoeren van de uitbreiding van Assurance ](./implement-assurance.md).

## Sessies maken

Na het registreren in [ Assurance UI ](https://experience.adobe.com/assurance), kunt u selecteren **[!UICONTROL Create Session]** beginnen creërend een zitting.

![ creeer zittingsknoop wordt benadrukt, tonend u waar u een zitting kunt tot stand brengen.](./images/using-assurance/create-session.png)

Het dialoogvenster **[!UICONTROL Create New Session]** wordt weergegeven met twee opties voor het maken van een sessie:

### Diepe verbinding maken

Selecteer deze optie om een unieke zitting-URL, QR code, en SPELD te produceren. Scan de QR-code of open de sessiekoppeling handmatig in uw app en voer vervolgens de pincode in om de verbinding tot stand te brengen.

Selecteer **[!UICONTROL Deep link connect]** en ga door te selecteren **[!UICONTROL Start]**.

![ de Create Nieuwe dialoog van de Zitting die Deep verbindt geselecteerde optie toont.](./images/using-assurance/create-new-session-deep-link.png)

U kunt nu een naam invoeren om de sessie te identificeren en vervolgens een **[!UICONTROL Base URL]** (deep linking-URL voor uw app) opgeven. Selecteer **[!UICONTROL Next]** nadat u deze gegevens hebt opgegeven.

>[!INFO]
>
>De basis-URL is de basisdefinitie die wordt gebruikt om uw app via een URL te starten. Er wordt een sessie-URL gegenereerd waarmee u de Assurance-sessie kunt starten. Een voorbeeldwaarde kan er als volgt uitzien: `myapp://default` Typ in het veld **[!UICONTROL Base URL]** de diepgaande-koppelingsdefinitie van de basis van uw app.

![ de zittingsnaam en de Invoergebieden van de Basis URL worden getoond.](./images/using-assurance/create-session-form-deep-link.png)

### Snelle verbinding

Trigger een verbinding van uw app, en uw apparaat zal in een lijst van beschikbare apparaten verschijnen. Selecteer **[!UICONTROL Quick connect]** om de Assurance-sessie te maken.

#### Vereisten

Controleer voordat u Quick Connect gebruikt of uw toepassing de vereiste SDK-versies en -implementatie heeft:

**Android SDK Vereisten:**

- Mobile Core v3.1.0 of hoger
- Adobe Journey Optimizer v3.1.0 of hoger
- Adobe Experience Platform Assurance v3.0.4 of hoger

**iOS SDK Vereisten:**

- Mobile Core v5.2.0 of hoger
- Adobe Journey Optimizer v5.1.1 of hoger
- Adobe Experience Platform Assurance v5.0.0 of hoger

**Implementatie:**

Uw app moet de [`startSession` API ](https://developer.adobe.com/client-sdks/home/base/assurance/api-reference/#startsession-quick-connect) implementeren om de Assurance-verbinding te activeren. Deze API-aanroep wordt meestal opgenomen in een handelingenset of geactiveerd in uw app.

#### Snel een verbindingssessie maken

![ de Create Nieuwe dialoog van de Zitting die Snelle geselecteerde optie toont verbindt.](./images/using-assurance/create-new-session-quick-connect.png)

Selecteer **[!UICONTROL Quick connect]** en selecteer **[!UICONTROL Start]** om door te gaan, wordt de interface van de apparaatkiezer weergegeven:

1. **Trigger de verbinding van Assurance** - in uw mobiele toepassing of implementatie, teweeg de actie die de verbinding van Assurance gebruikend `startSession` API in werking stelt. Hierdoor wordt uw apparaat herkenbaar.

2. **selecteer en verbind uw apparaat** - Zodra uw apparaat in de lijst van beschikbare apparaten verschijnt, selecteer het en klik **[!UICONTROL Connect]**.

![ de Snelle Connect interface van de apparatenplukker die beschikbare apparaten toont.](./images/using-assurance/quick-connect-device-picker.png)

## Verbinding maken met een sessie

Welke stappen moeten worden uitgevoerd, is afhankelijk van het sessietype dat u gebruikt:

### Verbindingssessies diepte koppelen

Voor sessies gemaakt met **[!UICONTROL Deep Link Connect]** :

1. Navigeer naar de pagina met uw sessiedetails (voor bestaande sessies) of ga verder vanaf het maken van de sessie om de koppeling, QR-code en pincode weer te geven
2. Gebruik de camera-app van uw apparaat om de QR-code te scannen of kopieer de koppeling en open deze in uw app
3. Wanneer uw app wordt gestart, wordt het scherm PIN-invoer bedekt. Voer de pincode in en druk op **[!UICONTROL Connect]**

![ een dialoog die de opties toont om met uw zitting van Assurance te verbinden wordt getoond.](./images/using-assurance/deep-link-connection.png)

### Sessies voor Snel verbinden

Voor sessies die zijn gemaakt met **[!UICONTROL Quick Connect]** (identificeerbaar door een sessie-URL die begint met `adobeassurance://` ), gebeurt de verbinding automatisch via de interface van de apparaatkiezer:

1. Navigeer naar de pagina met uw sessiedetails (voor bestaande sessies) of ga door met het maken van een sessie
2. In de sectie **[!UICONTROL Connect Device]** ziet u de interface van de apparaatkiezer
3. De handelingenset in uw app activeren om het apparaat te kunnen detecteren
4. Selecteer het apparaat in de lijst en klik op **[!UICONTROL Connect]**

![ de interface die van de apparatenplukker beschikbare apparaten toont om te verbinden.](./images/using-assurance/quick-connect-device-picker.png)

### Verbinding controleren

U kunt controleren of uw app is verbonden met Assurance wanneer het Adobe Experience Platform-pictogram (de rode Adobe &quot;A&quot;) wordt weergegeven op uw app.

## Een sessie exporteren

Als u een Assurance-sessie wilt exporteren, selecteert u **[!UICONTROL Export to JSON]** in een sessie op de detailpagina van uw app:

![ Exporterend een zitting ](./images/using-assurance/export-session.png)

De exportoptie respecteert de resultaten van het zoekfilter en exporteert alleen gebeurtenissen die in de gebeurtenisweergave worden weergegeven. Als u bijvoorbeeld hebt gezocht naar gebeurtenissen &#39;track&#39; en vervolgens **[!UICONTROL Export to JSON]** selecteert, worden alleen de resultaten van de gebeurtenis &#39;track&#39; geëxporteerd.
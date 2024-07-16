---
title: Adobe Experience Platform Assurance gebruiken
description: In deze handleiding wordt uitgelegd hoe u Adobe Experience Platform Assurance kunt gebruiken nadat deze is geïnstalleerd en geïmplementeerd.
exl-id: 872c83d1-82e8-40d8-9b66-3e51a91a955f
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---

# Adobe Experience Platform Assurance gebruiken

In deze zelfstudie wordt uitgelegd hoe u Adobe Experience Platform Assurance kunt gebruiken. Voor instructies op om de uitbreiding van de Verzekering van Adobe Experience Platform te installeren en uit te voeren, te lezen gelieve het leerprogramma op [ uitvoerend de uitbreiding van de Verzekering ](./implement-assurance.md).

## Sessies maken

Na het registreren in [ Verzekering UI ](https://experience.adobe.com/assurance), kunt u selecteren **[!UICONTROL Create Session]** beginnen creërend een zitting.

![ creeer zittingsknoop wordt benadrukt, tonend u waar u een zitting kunt tot stand brengen.](./images/using-assurance/create-session.png)

Het dialoogvenster **[!UICONTROL Create New Session]** wordt weergegeven. Controleer de gegeven instructies en selecteer **[!UICONTROL Start]** .

![ de Create Nieuwe dialoog van de Zitting wordt getoond, tonend instructies op hoe te om Verzekering te gebruiken.](./images/using-assurance/create-new-session.png)

U kunt nu een naam invoeren om de sessie te identificeren en vervolgens een **[!UICONTROL Base URL]** (deep linking-URL voor uw app) opgeven. Selecteer **[!UICONTROL Next]** nadat u deze gegevens hebt opgegeven.

>[!INFO]
>
>De basis-URL is de basisdefinitie die wordt gebruikt om uw app via een URL te starten. Er wordt een sessie-URL gegenereerd waarmee u de betrouwbaarheidssessie kunt starten. Een voorbeeldwaarde kan er als volgt uitzien: `myapp://default` Typ in het veld **[!UICONTROL Base URL]** de diepgaande-koppelingsdefinitie van de basis van uw app.

![ het volledige werkschema van het creëren van een nieuwe zitting wordt getoond.](./images/using-assurance/create-session.gif)

## Verbinding maken met een sessie

Nadat u een sessie hebt gemaakt, controleert u of u in het dialoogvenster **[!UICONTROL Create New Session]** nu een koppeling, een QR-code en een pincode ziet.

![ dialoog die A de opties toont om met uw zitting van de Verzekering te verbinden wordt getoond.](./images/using-assurance/create-new-session-pin.png)

Als dit dialoogvenster wordt weergegeven, kunt u de QR-code scannen met de camera-app van uw apparaat en de koppeling openen of kopiëren en openen in uw app. Wanneer uw app wordt gestart, wordt het scherm PIN-invoer weergegeven. Typ de pincode uit de vorige stap en druk op **[!UICONTROL Connect]** .

U kunt controleren of uw app is verbonden met Verzekering wanneer het Adobe Experience Platform-pictogram (rode Adobe &quot;A&quot;) wordt weergegeven op uw app.

![ het volledige werkschema om uw toepassing aan een zitting van de Verzekering te verbinden wordt getoond.](./images/using-assurance/connect-session.gif)

## Een sessie exporteren

Als u een betrouwbaarheidssessie wilt exporteren, selecteert u **[!UICONTROL Export to JSON]** in een sessie op de detailpagina van uw app:

![ Exporterend een zitting ](./images/using-assurance/export-session.png)

De exportoptie respecteert de resultaten van het zoekfilter en exporteert alleen gebeurtenissen die in de gebeurtenisweergave worden weergegeven. Als u bijvoorbeeld hebt gezocht naar gebeurtenissen &#39;track&#39; en vervolgens **[!UICONTROL Export to JSON]** selecteert, worden alleen de resultaten van de gebeurtenis &#39;track&#39; geëxporteerd.

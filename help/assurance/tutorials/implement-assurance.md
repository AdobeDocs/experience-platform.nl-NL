---
title: Adobe Experience Platform Assurance-extensie implementeren
description: In deze handleiding wordt uitgelegd hoe u de Adobe Experience Platform Assurance-extensie implementeert en installeert.
exl-id: b7bd1bb1-1606-4d00-97e0-c329c86d8ca4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---

# De Adobe Experience Platform Assurance-extensie implementeren

In deze zelfstudie wordt uitgelegd hoe u de Experience Platform Assurance-extensie installeert en implementeert in de Mobile SDK. Voor instructies bij het toevoegen van de uitbreiding van Assurance aan uw toepassing, gelieve te lezen het [ de uitbreidingsoverzicht van Adobe Experience Platform Assurance ](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

## Aan de slag

Als u de Assurance-extensie wilt installeren en implementeren, hebt u toegang nodig tot de volgende services:

- De [ UI van de Inzameling van Gegevens van Adobe Experience Platform ](https://experience.adobe.com/#/data-collection/)
- [ Adobe Experience Platform Assurance ](https://experience.adobe.com/assurance)

## Een mobiele eigenschap maken

>[!NOTE]
>
>Als u al een eigenschap voor mobiele apparaten hebt, kunt u verdergaan met de volgende stap.

Selecteer **[!UICONTROL Tags]** in de gebruikersinterface voor gegevensverzameling. Er wordt een lijst met mobiele en wegeigenschappen weergegeven, met informatie over de eigenschappen die bij uw organisatie horen. Selecteer **[!UICONTROL New property]** om een nieuwe eigenschap te maken.

![ de Nieuwe bezitsknoop wordt benadrukt, tonend wat u selecteert om een nieuw bezit ](./images/implement-assurance/create-new-property.png) tot stand te brengen

De pagina **[!UICONTROL Create Property]** wordt weergegeven. Voer de naam voor de nieuwe eigenschap in en selecteer **[!UICONTROL Mobile]** als uw platform. Nadat u de details hebt ingevoegd, selecteert u **[!UICONTROL Save]** om de eigenschap mobile te maken.

>[!NOTE]
>
>Het plaatsen van het mobiele bezit **[!UICONTROL Privacy]** beïnvloedt **niet** de gegevensinzameling van Assurance.

![ Create wordt de pagina van het Bezit getoond. U kunt informatie over uw mobiel bezit hier opnemen.](./images/implement-assurance/create-property.png)

## De Assurance-extensie installeren

Selecteer de eigenschap mobile waarin u de Assurance-extensie wilt installeren.

![ de pagina van de Eigenschappen van de Markering wordt getoond, met het geselecteerde mobiele bezit benadrukt.](./images/implement-assurance/select-mobile-property.png)

De **mobiele bezitsdetails** pagina verschijnt. Selecteer **[!UICONTROL Extensions]** om een lijst weer te geven met extensies die momenteel zijn gekoppeld aan uw mobiele eigenschap.

![ De mobiele pagina van bezitsdetails wordt getoond. Informatie over recente activiteiten wordt weergegeven. Het tabblad Extensies is gemarkeerd.](./images/implement-assurance/tag-properties.png)

Selecteer **[!UICONTROL Catalog]** om een lijst weer te geven met extensies die u kunt toevoegen aan de eigenschap mobile. Zoek met het filter de extensie **[!UICONTROL AEP Assurance]** en selecteer **[!UICONTROL Install]** .

![ de catalogus van uitbreidingen wordt getoond. De extensie Assurance wordt gefilterd voor en weergegeven, met de knop Installeren gemarkeerd.](./images/implement-assurance/assurance-extension.png)

## Volgende stappen

Nu u de Assurance-extensie in uw mobiele eigenschap hebt geïnstalleerd, kunt u Assurance in uw toepassingen gaan gebruiken. Leer hoe te om de uitbreiding van Assurance aan uw toepassing toe te voegen, te lezen gelieve het [ de uitbreidingsoverzicht van Adobe Experience Platform Assurance ](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app). Leren hoe te om Assurance te gebruiken, te lezen gelieve [ gebruikend de gids van Assurance ](./using-assurance.md).

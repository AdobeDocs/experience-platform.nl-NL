---
title: Adobe Experience Platform Assurance-extensie implementeren
description: In deze handleiding wordt uitgelegd hoe u de extensie Adobe Experience Platform Assurance implementeert en installeert.
exl-id: b7bd1bb1-1606-4d00-97e0-c329c86d8ca4
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 2%

---

# De extensie Adobe Experience Platform Assurance implementeren

In deze zelfstudie wordt uitgelegd hoe u de extensie Platform Assurance in de Mobile SDK installeert en implementeert. Voor instructies over het toevoegen van de uitbreiding van de Verzekering aan uw toepassing, gelieve te lezen [Overzicht van Adobe Experience Platform Assurance-extensie](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

## Aan de slag

Als u de extensie Verzekering wilt installeren en implementeren, hebt u toegang nodig tot de volgende services:

- De [UI voor gegevensverzameling van Adobe Experience Platform](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

## Een mobiele eigenschap maken

>[!NOTE]
>
>Als u al een eigenschap voor mobiele apparaten hebt, kunt u verdergaan met de volgende stap.

Selecteer in de gebruikersinterface voor gegevensverzameling de optie **[!UICONTROL Tags]**. Er wordt een lijst met mobiele en wegeigenschappen weergegeven, met informatie over de eigenschappen die bij uw organisatie horen. Selecteren **[!UICONTROL New property]** om een nieuwe eigenschap te maken.

![De knop Nieuwe eigenschap wordt gemarkeerd en geeft aan wat u selecteert om een nieuwe eigenschap te maken](./images/implement-assurance/create-new-property.png)

De **[!UICONTROL Create Property]** wordt weergegeven. Voer de naam voor de nieuwe eigenschap in en selecteer **[!UICONTROL Mobile]** als uw platform. Nadat u de details hebt ingevoegd, selecteert u **[!UICONTROL Save]** om de eigenschap mobile te maken.

>[!NOTE]
>
>De eigenschap mobile **[!UICONTROL Privacy]** instellen is **niet** de gegevensverzameling van Assurance beïnvloeden.

![De pagina Eigenschap maken wordt weergegeven. U kunt hier informatie over uw mobiele eigenschap invoegen.](./images/implement-assurance/create-property.png)

## De extensie Verzekering installeren

Selecteer de mobiele eigenschap waarin u de extensie Verzekering wilt installeren.

![De pagina Eigenschappen van tag wordt weergegeven en de geselecteerde eigenschap mobile wordt gemarkeerd.](./images/implement-assurance/select-mobile-property.png)

De **details van mobiele eigenschappen** wordt weergegeven. Selecteren **[!UICONTROL Extensions]** om een lijst weer te geven met extensies die momenteel zijn gekoppeld aan uw mobiele eigenschap.

![De pagina met details over mobiele eigenschappen wordt weergegeven. Informatie over recente activiteiten wordt weergegeven. Het tabblad Extensies is gemarkeerd.](./images/implement-assurance/tag-properties.png)

Selecteren **[!UICONTROL Catalog]** voor een lijst met extensies die u kunt toevoegen aan de eigenschap mobile. Zoek met het filter de **[!UICONTROL AEP Assurance]** en selecteert u **[!UICONTROL Install]**.

![De extensiecatalogus wordt weergegeven. De extensie Verzekering wordt gefilterd voor en weergegeven, met de knop Installeren gemarkeerd.](./images/implement-assurance/assurance-extension.png)

## Volgende stappen

Nu u de uitbreiding van de Verzekering in uw mobiel bezit hebt geïnstalleerd, kunt u beginnen betrouwbaarheidsverklaring binnen uw toepassingen te gebruiken. Als u wilt weten hoe u de extensie Verzekering toevoegt aan uw toepassing, leest u de [Overzicht van Adobe Experience Platform Assurance-extensie](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app). Lees voor meer informatie over het gebruik van Verzekering de [gebruiken van de gids van de Verzekering](./using-assurance.md).

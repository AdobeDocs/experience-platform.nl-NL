---
title: Adobe Experience Platform Assurance-extensie implementeren
description: In deze handleiding wordt uitgelegd hoe u de extensie Adobe Experience Platform Assurance implementeert en installeert.
exl-id: b7bd1bb1-1606-4d00-97e0-c329c86d8ca4
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 0%

---

# De extensie Adobe Experience Platform Assurance implementeren

In deze zelfstudie wordt uitgelegd hoe u de extensie Platform Assurance installeert en implementeert in de Mobile SDK. Voor instructies bij het toevoegen van de uitbreiding van de Verzekering aan uw toepassing, gelieve te lezen het [ de uitbreidingsoverzicht van de Verzekering van Adobe Experience Platform ](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

## Aan de slag

Als u de extensie Verzekering wilt installeren en implementeren, hebt u toegang nodig tot de volgende services:

- De [ UI van de Inzameling van Gegevens van Adobe Experience Platform ](https://experience.adobe.com/#/data-collection/)
- [ de Verzekering van Adobe Experience Platform ](https://experience.adobe.com/assurance)

## Een mobiele eigenschap maken

>[!NOTE]
>
>Als u al een eigenschap voor mobiele apparaten hebt, kunt u verdergaan met de volgende stap.

Selecteer **[!UICONTROL Tags]** in de gebruikersinterface voor gegevensverzameling. Er wordt een lijst met mobiele en wegeigenschappen weergegeven, met informatie over de eigenschappen die bij uw organisatie horen. Selecteer **[!UICONTROL New property]** om een nieuwe eigenschap te maken.

![ de Nieuwe bezitsknoop wordt benadrukt, tonend wat u selecteert om een nieuw bezit ](./images/implement-assurance/create-new-property.png) tot stand te brengen

De pagina **[!UICONTROL Create Property]** wordt weergegeven. Voer de naam voor de nieuwe eigenschap in en selecteer **[!UICONTROL Mobile]** als uw platform. Nadat u de details hebt ingevoegd, selecteert u **[!UICONTROL Save]** om de eigenschap mobile te maken.

>[!NOTE]
>
>Het plaatsen van het mobiele bezit **[!UICONTROL Privacy]** **** beïnvloedt de gegevensinzameling van de Verzekering niet.

![ Create wordt de pagina van het Bezit getoond. U kunt informatie over uw mobiel bezit hier opnemen.](./images/implement-assurance/create-property.png)

## De extensie Verzekering installeren

Selecteer de mobiele eigenschap waarin u de extensie Verzekering wilt installeren.

![ de pagina van de Eigenschappen van de Markering wordt getoond, met het geselecteerde mobiele bezit benadrukt.](./images/implement-assurance/select-mobile-property.png)

De **mobiele bezitsdetails** pagina verschijnt. Selecteer **[!UICONTROL Extensions]** om een lijst weer te geven met extensies die momenteel zijn gekoppeld aan uw mobiele eigenschap.

![ De mobiele pagina van bezitsdetails wordt getoond. Informatie over recente activiteiten wordt weergegeven. Het tabblad Extensies is gemarkeerd.](./images/implement-assurance/tag-properties.png)

Selecteer **[!UICONTROL Catalog]** om een lijst weer te geven met extensies die u kunt toevoegen aan de eigenschap mobile. Zoek met het filter de extensie **[!UICONTROL AEP Assurance]** en selecteer **[!UICONTROL Install]** .

![ de catalogus van uitbreidingen wordt getoond. De uitbreiding van de Verzekering wordt gefiltreerd voor en getoond, met de benadrukte installatieknoop.](./images/implement-assurance/assurance-extension.png)

## Volgende stappen

Nu u de uitbreiding van de Verzekering in uw mobiel bezit hebt geïnstalleerd, kunt u beginnen betrouwbaarheidsverklaring binnen uw toepassingen te gebruiken. Leren hoe te om de uitbreiding van de Verzekering aan uw toepassing toe te voegen, te lezen gelieve het [ de uitbreidingsoverzicht van de Verzekering van Adobe Experience Platform ](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app). Leren hoe te om Verzekering te gebruiken, te lezen gelieve [ gebruikend de gids van de Verzekering ](./using-assurance.md).

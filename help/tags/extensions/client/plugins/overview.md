---
title: Algemeen overzicht van extensie Analytics
description: Meer informatie over de extensie Common Analytics in Adobe Experience Platform.
exl-id: 9eeb4589-df90-4356-b927-b2c29c32370b
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# Overzicht van Common Analytics Plugins-extensie

Gebruik deze naslaggids voor informatie over het configureren van de extensie Algemene analytische plug-ins en de opties die beschikbaar zijn wanneer u deze extensie gebruikt om de extensie [!DNL Adobe Analytics] te verhogen.

## De extensie Common Analytics Plugins configureren

Deze sectie bevat een verwijzing naar de beschikbare opties wanneer u de extensie Algemene plug-ins voor analyse configureert.

>[!IMPORTANT]
>
>De extensie Common Analytics Plugins vergroot de extensie [!DNL Adobe Analytics] . De eigenschap werkt alleen als de extensie [!DNL Adobe Analytics] op de eigenschap is geïnstalleerd. Daarnaast moet u de tracker algemeen toegankelijk maken in de extensie [!DNL Adobe Analytics] .

Geen extra configuratie wordt vereist op het uitbreidingsniveau.

## Plug-ins toevoegen aan de extensie [!DNL Adobe Analytics]

Als u de plug-ins in deze extensie wilt gebruiken, moet u eerst de plug-ins die u wilt gebruiken, op hun eigen regel initialiseren.

1. Maak een nieuwe regel.
1. Voeg de gebeurtenis Core - Library Loaded (Pagina boven) toe.
1. Gebruik een van de onderstaande initialisatiemethoden.

## Algemene actietypen voor de extensie Analytics Plugins

In deze sectie worden de actietypen beschreven die beschikbaar zijn in de extensie Common Analytics Plugins.

De extensie Common Analytics Plugins biedt de volgende handelingen:

* [Initialiseren](#initialize)
* [Insteekmodule initialiseren](#initialize-plugin)

### Initialiseren

>[!IMPORTANT]
>
>Hoewel deze handeling eenvoudiger te implementeren is, wordt u door Adobe Consulting niet aangeraden deze handeling te gebruiken, omdat hierdoor het gewicht van de plug-in toeneemt.

In deze handeling kunt u elke plug-in selecteren die u in de implementatie wilt opnemen en de wijzigingen opslaan. Selecteer zo veel of weinig als u tijdens de implementatie wilt gebruiken.

### Insteekmodule initialiseren

Met deze acties initialiseert u de specifieke plug-in die u afzonderlijk wilt gebruiken. Als u alle insteekmodules die u wilt gebruiken in uw eigenschap wilt initialiseren, voegt u gewoon de corresponderende actie aan uw regel toe en slaat u de regel op. Terwijl er iets meer inspanning betrokken bij het vormen van de uitbreiding deze manier is, verstrekt het grotere codeefficiency. Daarom beveelt Adobe deze aanpak aan.

## Algemene gegevenselementen van plug-ins voor Analytics

De volgende gegevenselementen zijn beschikbaar in de Common Analytics Plugins-extensie, waarmee tagmogelijkheden worden gebruikt voor het instellen en configureren van de corresponderende plug-ins in Analytics:

* `getGeoCoordinates`
* `getNewRepeat`
* `getPageName`
* `getResponsiveLayout`
* `getTimeParting`
* `getTimeSinceLastVisit`
* `getVisitDuration`
* `getVisitNum`

>[!NOTE]
>
>Voor meer informatie over de bovengenoemde stoppen, gelieve de [&#x200B; documentatie van Analytics &#x200B;](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/impl-plugins.html) te raadplegen.

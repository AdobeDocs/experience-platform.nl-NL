---
title: Algemeen overzicht van extensie Analytics
description: Meer informatie over de extensie Common Analytics in Adobe Experience Platform.
exl-id: 9eeb4589-df90-4356-b927-b2c29c32370b
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---

# Overzicht van Common Analytics Plugins-extensie

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Gebruik deze verwijzing voor informatie over het vormen van de Gemeenschappelijke uitbreiding van de Insteekmodules van Analytics, en de opties beschikbaar wanneer het gebruiken van deze uitbreiding om [!DNL Adobe Analytics] Extensie.

## De extensie Common Analytics Plugins configureren

Deze sectie bevat een verwijzing naar de beschikbare opties wanneer u de extensie Algemene plug-ins voor analyse configureert.

>[!IMPORTANT]
>
>De uitbreiding Common Analytics Plugins breidt de [!DNL Adobe Analytics] extensie. U moet beschikken over de [!DNL Adobe Analytics] de extensie die op uw eigenschap is geïnstalleerd, werkt niet. Daarnaast moet u de tracker wereldwijd toegankelijk maken in de [!DNL Adobe Analytics] extensie.

Geen extra configuratie wordt vereist op het uitbreidingsniveau.

## Plug-ins toevoegen aan de [!DNL Adobe Analytics] extension

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

In deze handeling kunt u elke plug-in selecteren die u in de implementatie wilt opnemen en de wijzigingen opslaan. Selecteer zo veel of weinig als u tijdens de implementatie wilt gebruiken. In het dialoogvenster Analytics vindt u koppelingen naar documentatie over het gebruik van elke plug-in en een korte beschrijving. [Overzicht van plug-ins](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/impl-plugins.html).

### Insteekmodule initialiseren

Met deze acties initialiseert u de specifieke plug-in die u afzonderlijk wilt gebruiken. Als u alle insteekmodules die u wilt gebruiken in uw eigenschap wilt initialiseren, voegt u gewoon de corresponderende actie aan uw regel toe en slaat u de regel op. Terwijl er iets meer inspanning betrokken bij het vormen van de uitbreiding deze manier is, verstrekt het grotere codeefficiency. Adobe beveelt daarom deze aanpak aan.

## Algemene gegevenselementen van plug-ins voor Analytics

In deze sectie worden de gegevenselementen beschreven die beschikbaar zijn in de extensie Common Analytics Plugins.

### getGeoCoordinates

Hiermee kunnen gebruikers de native interface voor gegevensverzameling in Adobe Experience Platform gebruiken om de plug-in getGeoCoordinates in te stellen en te configureren.

### getNewRepeat

Hiermee kunnen gebruikers de native gegevensverzamelingsinterface gebruiken om de getNewRepeat-plug-in in te stellen en te configureren.

### getPageName

Hiermee kunnen gebruikers de native gegevensverzamelingsinterface gebruiken om de getPageName-insteekmodule in te stellen en te configureren.

### getResponsiveLayout

Hiermee kunnen gebruikers de native gegevensverzamelingsinterface gebruiken om de getResponsiveLayout-insteekmodule in te stellen en te configureren.

### getTimeParting

Hiermee kunnen gebruikers de native interface voor gegevensverzameling gebruiken om de getTimeParting-plug-in in te stellen en te configureren.

### getTimeSinceLastVisit

Hiermee kunnen gebruikers de native gegevensverzamelingsinterface gebruiken om de getTimeSinceLastVisit-insteekmodule in te stellen en te configureren.

### getVisitDuration

Hiermee kunnen gebruikers de native interface voor gegevensverzameling gebruiken om de getVisitDuration-insteekmodule in te stellen en te configureren.

### getVisitNum

Hiermee kunnen gebruikers de native interface voor gegevensverzameling gebruiken om de getVisitNum-plug-in in te stellen en te configureren.

---
title: Overzicht Adobe Audience Manager-extensie
description: Meer informatie over de Adobe Audience Manager-tagextensie in Adobe Experience Platform.
exl-id: d345e145-fdb9-4ca3-88c2-9c2a247ea59a
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# Overzicht Adobe Audience Manager-extensie

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Met de de markeringsuitbreiding van de Audience Manager, kunt u de code integreren van de DIL die door Audience Manager met uw eigenschappen in Adobe Experience Platform wordt gebruikt.

Gebruik deze verwijzing voor informatie over de beschikbare opties wanneer het gebruiken van deze uitbreiding om een regel te bouwen.

>[!NOTE]
>
>Deze extensie is niet bedoeld voor het doorsturen van gebeurtenissen van Adobe Analytics-gegevens. Gebruik voor het doorsturen van gebeurtenissen de [Adobe Analytics-extensie](../analytics/overview.md).

## De Adobe Audience Manager-extensie configureren

Als de extensie Adobe Audience Manager nog niet is geïnstalleerd, opent u de eigenschap en selecteert u **[!UICONTROL Extensions > Catalog]**, plaatst u de aanwijzer boven de Adobe Audience Manager-extensie en selecteert u **[!UICONTROL Install]**.

Als u de extensie wilt configureren, opent u de [!UICONTROL Extensions] , plaatst u de cursor boven de extensie en selecteert u vervolgens **[!UICONTROL Configure]**.

### DIL-instellingen

Configureer uw DIL-instellingen. De volgende configuratieopties zijn beschikbaar:

![](../../../images/ext-aam-config.png)

#### DIL-versie

Toont de Data Integration Library (DIL) versie.

Deze instelling kan niet worden gewijzigd.

#### Specifieke paden uitsluiten

Als de URL overeenkomt met een van de uitgesloten paden, wordt de extensie niet geladen.

Selecteren **[!UICONTROL Add Path]** om een uitgesloten URL op te geven.

Schakel Regex in als de URL een reguliere expressie is.

#### DIL Site Catalyst-module gebruiken

De [SiteCatalyst, module](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_sc_init.html) werkt met DIL om elementen van de tag Analytics naar de Audience Manager te verzenden.

Gebruik de Code-editor om het bestand siteCatalyst.init te configureren.

U kunt ook een notitie maken met informatie over deze configuratie.

#### DIL Google Analytics-module gebruiken

De optie [Google Analytics, module](https://experiencecloud.adobe.com/resources/help/en_US/aam/dil-google-universal-analytics.html).

#### DIL.Initialisatie-eigenschappen maken

Initialisatie-eigenschappen toevoegen die worden gebruikt door [DIL.create](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_create.html) en de naamruimte-subeigenschap voor de [Object bezoekorService](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_visitor_service.html). In de codeopmerkingen in de Code-editor zijn twee voorbeelden van voorbeeldgebruik opgenomen.

Selecteren **[!UICONTROL Choose an Item]** om extra eigenschappen toe te voegen.

Houd de muisaanwijzer boven de pictogrammen &#39;i&#39; om te zien wat elke eigenschap doet. Meer informatie over de eigenschappen vindt u in het dialoogvenster [Audience Manager DIL](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_create.html).

Selecteren **[!UICONTROL Save]** wanneer u klaar bent met het configureren van de extensie.

## Handelingstypen voor Adobe Audience Manager-extensies

Dit onderwerp beschrijft de actietypes beschikbaar in de uitbreiding van de Audience Manager.

De extensie Adobe Audience Manager biedt de volgende acties in het gedeelte Dan van een regel:

### Aangepaste code uitvoeren

Voer de aangepaste code uit die in de code-editor is geconfigureerd.

Ga de gewenste code in de Redacteur van de Code in, dan ga een naam voor de code in. Deze code zal beschikbaar in het Dan gedeelte van de regelbouwer worden.

![](../../../images/ext-aam-then.png)

U kunt ook een notitie toevoegen met informatie over de configuratie.

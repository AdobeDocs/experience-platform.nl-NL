---
title: Overzicht Adobe Audience Manager-extensie
description: Meer informatie over de Adobe Audience Manager-tagextensie in Adobe Experience Platform.
exl-id: d345e145-fdb9-4ca3-88c2-9c2a247ea59a
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 3%

---

# Overzicht Adobe Audience Manager-extensie

Met de Audience Manager-tagextensie kunt u de DIL-code die door Audience Manager wordt gebruikt, integreren met uw eigenschappen in Adobe Experience Platform.

Gebruik deze verwijzing voor informatie over de beschikbare opties wanneer het gebruiken van deze uitbreiding om een regel te bouwen.

>[!NOTE]
>
>Deze extensie is niet bedoeld voor het doorsturen van gebeurtenissen van Adobe Analytics-gegevens. Voor gebeurtenis door:sturen, gebruik de [&#x200B; uitbreiding van Adobe Analytics &#x200B;](../analytics/overview.md).

## De Adobe Audience Manager-extensie configureren

Als de Adobe Audience Manager-extensie nog niet is geïnstalleerd, opent u de eigenschap en selecteert u **[!UICONTROL Extensions > Catalog]** , plaatst u de aanwijzer op de Adobe Audience Manager-extensie en selecteert u **[!UICONTROL Install]** .

Als u de extensie wilt configureren, opent u het tabblad [!UICONTROL Extensions] , plaatst u de muisaanwijzer op de extensie en selecteert u **[!UICONTROL Configure]** .

### DIL-instellingen

Configureer uw DIL-instellingen. De volgende configuratieopties zijn beschikbaar:

![](../../../images/ext-aam-config.png)

#### DIL-versie

Geeft de Data Integration Library-versie (DIL) weer.

Deze instelling kan niet worden gewijzigd.

#### Specifieke paden uitsluiten

Als de URL overeenkomt met een van de uitgesloten paden, wordt de extensie niet geladen.

Selecteer **[!UICONTROL Add Path]** om een uitgesloten URL op te geven.

Laat Regex toe als URL een regelmatige uitdrukking is.

#### DIL Site Catalyst-module gebruiken

De [&#x200B; module SiteCatalyst &#x200B;](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_sc_init.html) werkt met DIL om de markeringselementen van Analytics naar Audience Manager te verzenden.

Gebruik de Code-editor om het bestand siteCatalyst.init te configureren.

U kunt ook een notitie maken met informatie over deze configuratie.

#### DIL Google Analytics-module gebruiken

Laat de [&#x200B; module van Google Analytics &#x200B;](https://experiencecloud.adobe.com/resources/help/en_US/aam/dil-google-universal-analytics.html) toe.

#### DIL.create Initialization Properties

Voeg initialisatieeigenschappen toe die door [&#x200B; worden gebruikt DIL.create &#x200B;](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_create.html) en namespace subproperty voor het [&#x200B; bezoekorService voorwerp &#x200B;](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_visitor_service.html). In de codeopmerkingen in de Code-editor zijn twee voorbeelden van voorbeeldgebruik opgenomen.

Selecteer **[!UICONTROL Choose an Item]** om extra eigenschappen toe te voegen.

Houd de muisaanwijzer boven de pictogrammen &#39;i&#39; om te zien wat elke eigenschap doet. U kunt meer informatie voor de eigenschappen in de [&#x200B; documentatie van Audience Manager DIL &#x200B;](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_create.html) vinden.

Selecteer **[!UICONTROL Save]** wanneer u de extensie hebt geconfigureerd.

## Handelingstypen voor Adobe Audience Manager-extensies

Dit onderwerp beschrijft de actietypes beschikbaar in de uitbreiding van Audience Manager.

De extensie Adobe Audience Manager biedt de volgende acties in het gedeelte Dan van een regel:

### Aangepaste code uitvoeren

Voer de aangepaste code uit die in de code-editor is geconfigureerd.

Ga de gewenste code in de Redacteur van de Code in, dan ga een naam voor de code in. Deze code zal beschikbaar in het Dan gedeelte van de regelbouwer worden.

![](../../../images/ext-aam-then.png)

U kunt ook een notitie toevoegen met informatie over de configuratie.

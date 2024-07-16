---
title: Overzicht van Meta-pixelextensie
description: Meer informatie over de extensie Meta Pixel in Adobe Experience Platform.
exl-id: c5127bbc-6fe7-438f-99f1-6efdbe7d092e
source-git-commit: 24001da61306a00d295bf9441c55041e20f488c0
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 0%

---

# [!DNL Meta Pixel] overzicht van extensies

[[!DNL Meta Pixel] ](https://developers.facebook.com/docs/meta-pixel/) is een op JavaScript gebaseerd analysehulpmiddel dat u toestaat om bezoekersactiviteit op uw website te volgen. De acties van de bezoeker die u (genoemd omzettingen) volgt worden verzonden naar [[!DNL Ads Manager] ](https://www.facebook.com/business/tools/ads-manager) waar zij kunnen worden gebruikt om de doeltreffendheid van uw advertenties, campagnes, omzettingskanalen, en meer te meten.

Met de tagextensie [!DNL Meta Pixel] kunt u [!DNL Pixel] -functies gebruiken in uw tagbibliotheken aan de clientzijde. Dit document behandelt hoe te om de uitbreiding te installeren en zijn mogelijkheden in a [ regel ](../../../ui/managing-resources/rules.md) te gebruiken.

## Vereisten

Als u de extensie wilt gebruiken, moet u een geldige [!DNL Meta] -account hebben met toegang tot [!DNL Ads Manager] . Specifiek, moet u [ een nieuw  [!DNL Meta Pixel] ](https://www.facebook.com/business/help/952192354843755) creëren en zijn kopiëren [!DNL Pixel ID] zodat kan de uitbreiding aan uw rekening worden gevormd. Als u al een bestaande [!DNL Meta Pixel] hebt, kunt u in plaats daarvan de id gebruiken.

Het wordt ten zeerste aangeraden [!DNL Meta Pixel] in combinatie met [!DNL Meta Conversions API] te gebruiken om dezelfde gebeurtenissen te delen en te verzenden vanaf respectievelijk de client en de server, aangezien dit ertoe kan bijdragen dat gebeurtenissen worden hersteld die niet door [!DNL Meta Pixel] zijn opgehaald. Zie de gids op de [[!DNL Meta Conversions API]  uitbreiding voor gebeurtenis door:sturen ](../../client/meta/overview.md) voor stappen op hoe te om het in uw server-zijimplementaties te integreren. Merk op dat uw organisatie toegang tot [ gebeurtenis moet hebben door:sturen ](../../../ui/event-forwarding/overview.md) om de server-zijuitbreiding te gebruiken.

## De extensie installeren

Als u de extensie [!DNL Meta Pixel] wilt installeren, navigeert u naar de gebruikersinterface van de gegevensverzameling of het Experience Platform en selecteert u **[!UICONTROL Tags]** in de linkernavigatie. Selecteer van hieruit een eigenschap waaraan u de extensie wilt toevoegen of maak een nieuwe eigenschap.

Wanneer u de gewenste eigenschap hebt geselecteerd of gemaakt, selecteert u **[!UICONTROL Extensions]** in de linkernavigatie en selecteert u vervolgens de tab **[!UICONTROL Catalog]** . Zoek de [!UICONTROL Meta Pixel] -kaart en selecteer vervolgens **[!UICONTROL Install]** .

![ de [!UICONTROL Install] knoop die voor de [!UICONTROL Meta Pixel] uitbreiding in de Inzameling UI van Gegevens wordt geselecteerd.](../../../images/extensions/client/meta/install.png)

In de configuratieweergave die wordt weergegeven, moet u de [!DNL Pixel] id opgeven die u eerder hebt gekopieerd om de extensie te koppelen aan uw account. U kunt de id rechtstreeks in de invoer plakken, maar u kunt ook een bestaand gegevenselement selecteren.

>[!TIP]
>
>Als u een gegevenselement gebruikt, kunt u de [!DNL Pixel] -id dynamisch wijzigen, afhankelijk van andere factoren, zoals de ontwikkelomgeving. Zie de appendix sectie op [ gebruikend verschillende  [!DNL Pixel]  IDs voor verschillende milieu&#39;s ](#id-data-element) voor meer informatie.

U kunt ook een gebeurtenis-id opgeven die u aan de extensie wilt koppelen. Hiermee worden identieke gebeurtenissen tussen [!DNL Meta Pixel] en [!DNL Meta Conversions API] gedupliceerd. Voor details, zie de sectie over [ gebeurtenis deduplicatie ](../../server/meta/overview.md#event-deduplication) in overzicht voor de [!DNL Conversions API] uitbreiding.

Selecteer **[!UICONTROL Save]** wanneer u klaar bent

![ identiteitskaart [!DNL Pixel] als gegevenselement in de mening van de uitbreidingsconfiguratie wordt verstrekt die.](../../../images/extensions/client/meta/configure.png)

De extensie is geïnstalleerd en u kunt nu de verschillende handelingen in de labelregels uitvoeren.

## Een labelregel configureren {#rule}

[!DNL Meta Pixel] keurt een reeks vooraf bepaalde [ standaardgebeurtenissen ](https://www.facebook.com/business/help/402791146561655), elk met hun eigen contexten en toegelaten eigenschappen goed. De handelingen van de regel die door de extensie [!DNL Pixel] worden aangeboden, correleren zich met deze gebeurtenistypen, zodat u de gebeurtenis die naar [!DNL Meta] wordt verzonden gemakkelijk kunt categoriseren en configureren op basis van het type.

Voor demonstratiedoeleinden toont deze sectie hoe u een regel bouwt die een gebeurtenis van de paginamening naar [!DNL Meta] verzendt.

Begin het creëren van een nieuwe markeringsregel en vorm zijn voorwaarden zoals gewenst. Wanneer u de handelingen voor de regel selecteert, selecteert u **[!UICONTROL Meta Pixel]** voor de extensie en selecteert u **[!UICONTROL Send Page View]** voor het actietype.

![ het [!UICONTROL Send Page View] actietype dat voor een regel in de Inzameling UI van Gegevens wordt geselecteerd.](../../../images/extensions/client/meta/select-action.png)

Er is geen verdere configuratie vereist voor de [!UICONTROL Send Page View] -actie. Selecteer **[!UICONTROL Keep Changes]** om de handeling aan de regelconfiguratie toe te voegen. Selecteer **[!UICONTROL Save to Library]** als u tevreden bent met de regel.

Tot slot publiceer een nieuwe markering [ bouwt ](../../../ui/publishing/builds.md) om de veranderingen in de bibliotheek toe te laten.

## Bevestig dat [!DNL Meta] gegevens ontvangt

Nadat uw bijgewerkte build is geïmplementeerd op uw website, kunt u bevestigen of gegevens naar behoren worden verzonden door conversiegebeurtenissen te genereren in uw browser en te controleren of deze gebeurtenissen worden weergegeven in [[!DNL Meta Events Manager] ](https://www.facebook.com/business/help/898185560232180) .

## Volgende stappen

In deze handleiding wordt beschreven hoe u gegevens naar [!DNL Meta] kunt verzenden met de tagextensie [!DNL Meta Pixel] . Als u op het verzenden van server-zijgebeurtenissen aan [!DNL Meta] ook van plan bent, kunt u nu te werk gaan om de [[!DNL Conversions API]  gebeurtenis te installeren en te vormen door:sturen uitbreiding ](../../server/meta/overview.md).

Voor meer informatie over markeringen in Experience Platform, verwijs naar het [ overzicht van markeringen ](../../../home.md).

## Bijlage: verschillende [!DNL Pixel] id&#39;s gebruiken voor verschillende omgevingen {#id-data-element}

Als u uw implementatie wilt testen in ontwikkelings- of staging-omgevingen terwijl de [!DNL Meta Pixel] -productieanalyse intact blijft, kunt u een gegevenselement gebruiken om dynamisch een geschikte [!DNL Pixel] -id te kiezen, afhankelijk van de gebruikte omgeving.

U kunt dit bereiken door een [!UICONTROL Custom Code] gegevenselement (dat door [[!UICONTROL Core] wordt verstrekt uitbreiding ](../core/overview.md)) in combinatie met [`turbine` vrije variabele ](../../../extension-dev/turbine.md) te gebruiken. Gebruik in de JavaScript-code van het gegevenselement het `turbine` -object om het huidige framewerkomgeving te zoeken en retourneer vervolgens een geschikte [!DNL Pixel] -id op basis van het resultaat.

In het volgende voorbeeld wordt een nepproductie-id `exampleProductionKey` geretourneerd wanneer deze in de productieomgeving wordt gebruikt en een andere id `exampleTestKey` wanneer een andere omgeving wordt gebruikt. Vervang bij het implementeren van deze code elke waarde door de werkelijke productie- en test- [!DNL Pixel] id&#39;s.

```js
return (turbine.environment.stage === "production" ? 'exampleProductionKey' : 'exampleTestKey');
```

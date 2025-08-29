---
title: Adobe Advertising Cloud ExperienceEvent Full Extension Schema Field Group
description: Meer informatie over de veldgroep Adobe Advertising Cloud ExperienceEvent Full Extension Schema.
badgeBeta: label="Beta" type="Informative"
source-git-commit: adfd0220b8bc53c44abc76a711b148a7e03edb7a
workflow-type: tm+mt
source-wordcount: '1563'
ht-degree: 0%

---

# [!UICONTROL Adobe Advertising Cloud ExperienceEvent Full Extension] schemaveldgroep

>[!AVAILABILITY]
>
>De veldgroep [!UICONTROL Adobe Advertising Cloud ExperienceEvent Full Extension] bevindt zich momenteel in bèta. De documentatie en de functionaliteit kunnen worden gewijzigd.

[!UICONTROL Adobe Advertising Cloud ExperienceEvent Full Extension] is een standaardgroep van het schemagebied voor de [[!DNL XDM ExperienceEvent]  klasse ](../../classes/experienceevent.md), die gemeenschappelijke metriek vangt die door Adobe Advertising (vroeger genoemd &quot;[!DNL Advertising Cloud]&quot;) wordt verzameld.

In dit document worden de structuur en het gebruik van hoofdletters en kleine letters beschreven voor de veldgroep met [!DNL Advertising Cloud] extensies.

>[!NOTE]
>
>U kunt ook omhoog deze gebiedsgroep [ in Experience Platform UI ](../../ui/explore.md) kijken of het volledige schema in de [ openbare bewaarplaats XDM ](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json) bekijken.

## Groepsstructuur van veld

De veldgroep biedt één `_experience` -object aan een schema, dat zelf één `adcloud` -object bevat.

![ Top-level gebieden voor de [!DNL Advertising Cloud] gebiedsgroep ](../../images/field-groups/advertising-full-extension/full-schema.png " Top-level gebieden voor de  [!DNL Advertising Cloud]  gebiedsgroep ")

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `adDeliveryDetails` | Object | Details van advertentie. Zie de [ onderafdeling hieronder op het `adDeliveryDetails` voorwerp ](#adDeliveryDetails) voor meer informatie over de inhoud van dit voorwerp. |
| `advertisement` | Object | Details van digitale advertentie. Zie de [ onderafdeling hieronder op het advertentievoorwerp ](#advertisement) voor meer informatie over de inhoud van dit voorwerp. |
| `campaign` | Object | Informatie over de campagnehiërarchie. Zie de [ onderafdeling hieronder op het campagnevoorwerp ](#campaign-campaign) voor meer informatie over de inhoud van dit voorwerp. |
| `conversionDetails` | Object | Conversiedetails voor een advertentie. Zie de [ onderafdeling hieronder ](#conversionDetails) voor meer informatie over de inhoud van dit voorwerp. |
| `eventType` | String | Het Adobe Advertising-gebeurtenistype. |
| `fees` | Object | Details Advertising-kosten. Zie de [ onderafdeling hieronder op het takenvoorwerp ](#fees) voor meer informatie over de inhoud van dit voorwerp. |
| `inventory` | Object | Voorraadgegevens. Zie de [ onderafdeling hieronder ](#inventory) voor meer informatie over de inhoud van dit voorwerp. |
| `productDetails` | Object | Product en details. Zie de [ onderafdeling hieronder op het productDetails voorwerp ](#productDetails) voor meer informatie over de inhoud van dit voorwerp. |
| `stitchId` | String | ID van de Adobe Advertising en servers om doorklikomzettingen bij te houden op browsers die derdekoekjes blokkeren. |

## `adDeliveryDetails` {#adDeliveryDetails}

Het adDeliveryDetails-object biedt informatie over waar en hoe de advertentie is geleverd, waaronder plaatsingswebsites en locatie-id&#39;s.

![ diagram dat van het Schema het `adDeliveryDetails` voorwerp en zijn gebieden toont.](../../images/field-groups/advertising-full-extension/adDeliveryDetails.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `placementWebsite` | String | De website waar de advertentie is weergegeven. |
| `siteLinkText` | String | De daadwerkelijke die plaatskoppeling in de reclame wordt geselecteerd. |
| `interestLocationID` | String | De locatie die wordt afgeleid van de zoekopdracht. Bijvoorbeeld, keert een vraag voor &quot;Hotel in Goa&quot;identiteitskaart voor Goa, ongeacht de daadwerkelijke het doorbladeren plaats van de gebruiker terug. |
| `physicalLocationID` | String | De bladerlocatie van de gebruiker, weergegeven door een referentie-id van het advertentienetwerk. Deze id is geen leesbare locatienaam (zoals een stad of land), maar een code die door het advertentienetwerk is toegewezen om een geografisch doel te identificeren. |

## `advertisement` {#advertisement}

In het advertentieobject worden details over de digitale advertentie beschreven, zoals id&#39;s, type, creatief, doelbewust en bijbehorende trefwoorden.

![ diagram dat van het Schema het `advertisement` voorwerp en zijn gebieden toont.](../../images/field-groups/advertising-full-extension/advertisement.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `adId` | String | De id voor de advertentie die aan deze gebeurtenis is gekoppeld. Deze id is niet gerelateerd aan de standaard voor de advertentie-id-industrie. |
| `runtime` | String | De runtime van de advertentie-eenheid, anders dan de runtime van de browser of het besturingssysteem. Mogelijke waarden zijn: `unknown` en `HTML5` . |
| `adClass` | String | De advertentieklasse van de stuurgebeurtenis: `display`, `video` of `social` . |
| `adUnitType` | String | De id voor de code die de advertentie in een browser of apparaat rendert. Mogelijke waarden zijn:<ul><li>`linearVideo`: Lineaire video</li><li>`interactiveVideo`: Interactieve video</li><li>`banner`: banner,</li><li>`richMediaBanner`: Rich media banner,</li><li>`newsFeedVideo`: News feed video,</li><li>`newsFeedDisplay`: nieuwsleefweergave,</li><li>`HTML5`: HTML5,</li><li>`inPageVideo`: In page video,</li><li>`inPageDisplay`: In paginaweergave,</li><li>`facebook`: Facebook,</li><li>`twitter`: Twitter,</li><li>`linearTv`: lineaire tv,</li><li>`vod`: Video on Demand</li></ul> |
| `promotedAssetId` | String | De id voor het element dat wordt bevorderd in de advertentie die aan deze gebeurtenis is gekoppeld. |
| `creativeID` | String | De id voor de creatieve advertentie (zoals een banner, video of sociale advertentie) die aan deze gebeurtenis is gekoppeld. |
| `keywordID` | String | De id voor het trefwoord dat de gebruiker heeft ingevoerd in een zoekquery die deze gebeurtenis heeft geactiveerd. |
| `keyword` | String | Het trefwoord waarop de klant heeft geboden. |
| `isDynamicSearchAd` | Boolean | Geeft aan of de gebeurtenis afkomstig is van een dynamische zoekadvertentie. |
| `audienceID` | String | De id voor het publiekssegment waarop de advertentie is gericht. |
| `adGroupID` | String | De id voor de advertentiegroep die is gekoppeld aan de advertentie die deze gebeurtenis heeft geactiveerd. |
| `campaignID` | String | De id voor de campagne die is gekoppeld aan de advertentie die deze gebeurtenis heeft geactiveerd. |
| `networkType` | String | Het netwerktype waar de gebeurtenis heeft plaatsgevonden. Mogelijke waarden zijn: <ul><li>`search`: De advertentie is weergegeven op het Zoeknetwerk.</li><li>`content`: De advertentie is weergegeven op het Inhoudsnetwerk.</li></ul> |
| `matchType` | String | Het trefwoordmatrixtype. Mogelijke waarden zijn: <ul><li>`exact`: Exacte overeenkomst met het trefwoord</li><li>`broad`: brede overeenkomst met het trefwoord</li><li>`phrase`: Phrase-overeenkomst van het trefwoord</li></ul> |

## `campaign` {#campaign}

Het campagneobject definieert de hiërarchie van de advertentiecampagne, inclusief account-, adverteerder-, plaatsing- en pakketid&#39;s, samen met valutadetails.

![ diagram dat van het Schema het `campaign` voorwerp en zijn gebieden toont.](../../images/field-groups/advertising-full-extension/campaign.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `accountId` | String | De id van de account. |
| `dspId` | String | De id voor de Demand Side Platform (DSP) waarin de campagne is gedefinieerd. Meestal is dit de id voor Adobe Advertising Cloud DSP. |
| `campaignId` | String | De id voor de campagne. |
| `placementId` | String | De id voor de plaatsing. |
| `packageId` | String | De id voor het Advertising DSP-pakket. |
| `advertiserId` | String | De id van de adverteerder. |
| `experimentId` | String | De id voor het experiment. |
| `sampleGroupId` | String | De id voor de voorbeeldgroep. |
| `currency` | String | De ISO 4217 factureringsvalutacode voor de rekening. Gebruikt het regelmatige uitdrukkingspatroon ^[ A-Z ] \ {3 \} $ (drie hoofdletters). Bijvoorbeeld: USD, EUR. |

## `conversionDetails` {#conversionDetails}

Het object conversionDetails legt trackinggegevens vast voor conversies van advertenties, waaronder trackingcodes, identiteiten en conversie-eigenschappen.

![ diagram dat van het schema het `conversionDetails` voorwerp en zijn gebieden toont.](../../images/field-groups/advertising-full-extension/conversionDetails.png " conversionDetails gebied ")

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `trackingCode` | String | De conversietrackingcode voor de gebeurtenis. Voor een lijst van mogelijke formaten, zie {de Formaten van identiteitskaart 0} AMO [.](https://experienceleague.adobe.com/nl/docs/advertising/integrations/customer-journey-analytics/ids#amo-id-formats) |
| `trackingIdentities` | String | De EF-id of identiteitsgegevens voor het bijhouden van een gebeurtenis. Voor een lijst van mogelijke formaten, zie [ EF identiteitskaart Formaten ](https://experienceleague.adobe.com/nl/docs/advertising/integrations/customer-journey-analytics/ids#ef-id-formats). |
| `conversionProperties` | Object | Een kaart met omzettingseigenschappen, die als serie van zeer belangrijk-waardepaarkoorden (zoals `subscriptions=253` wordt vertegenwoordigd). |

## `fees` {#fees}

Het object fee legt media, gegevens en andere advertentiekosten vast, uitgesplitst naar Advertising DSP, account en adverteerder.

![ diagram dat van het Schema het `fees` voorwerp en zijn gebieden toont.](../../images/field-groups/advertising-full-extension/fees.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `DSPMediaFees` | Getal | De mediadrachten die Advertising DSP in rekening brengt. |
| `DSPDataFees` | Getal | De gegevenskosten die Advertising DSP in rekening brengt. |
| `DSPOtherFees` | Getal | Overige door Advertising DSP in rekening te brengen kosten. |
| `accountMediaFees` | Getal | De mediadrachten voor het account maar kunnen niet door Advertising DSP worden gefactureerd. |
| `accountDataFees` | Getal | De gegevenskosten voor de account, maar kunnen niet door Advertising DSP worden opgevraagd. |
| `accountOtherFees` | Getal | Andere kosten voor de rekening, maar niet in rekening gebracht door Advertising DSP. |
| `advertiserMediaFees` | Getal | De kosten die de adverteerder voor mediabestanden van het account aan de adverteerder in rekening brengt. |
| `advertiserDataFees` | Getal | Andere kosten die de adverteerder van de account in rekening brengt. |
| `advertiserOtherFees` | Getal | Andere kosten die de adverteerder van de account in rekening brengt. |
| `billableMediaNetSpend` | Getal | De factureerbare netto-uitgaven voor mediaclame. |
| `totalMediaNetSpend` | Getal | De totale nettouitgaven voor mediaclame. |
| `billableDataNetSpend` | Getal | De factureerbare netto-uitgaven voor gegevensreclame. |
| `billableOtherNetSpend` | Getal | Het factureerbare nettobedrag voor andere soorten reclame. |
| `totalBillableNetSpend` | Getal | De totale factureringsbare nettouitgaven. |
| `totalNonBillableNetSpend` | Getal | De totale niet-factureerbare nettouitgaven. |
| `totalNetSpend` | Getal | De totale netto-uitgaven. |

## `inventory` {#inventory}

Het inventarisvoorwerp registreert details over de kans van de advertentie, met inbegrip van zittingsgegevens, partnercodes, plaats IDs, kostenvaluta, en segmenteringsregels.

![ diagram dat van het Schema het `inventory` voorwerp en zijn gebieden toont.](../../images/field-groups/advertising-full-extension/inventory.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `sessionId` | String | De sessie-id die aan een ervaringsgebeurtenis is gekoppeld, wordt gebruikt om onafhankelijke gebeurtenissen die in dezelfde sessie hebben plaatsgevonden, te koppelen. |
| `feedID` | String | Een samengestelde id van de uitgever, de uitwisseling en andere functies. |
| `sspPartnerCode` | String | De partner (uitwisseling) via welke Adobe Advertising Cloud de mogelijkheid tot inventarisatie krijgt. |
| `siteID` | String | De id van de website waar de advertentie werd weergegeven. |
| `costCurrency` | String | De ISO 4217-valutacode die wordt gebruikt om een partner voor een advertentiemogelijkheid te betalen. De waarde moet het regelmatige uitdrukkingspatroon ^[ a-z ] \ {3 \} $ (drie hoofdletters) volgen. Bijvoorbeeld: USD, EUR. |
| `inventorySourceId` | String | De id van de inventarisatiebron voor Adobe Advertising Cloud waarop deze mogelijkheid is geboden. |
| `segment` | Object | Details verbonden aan de regels van de gebruikerssegmentatie. De eigenschappen hiervan zijn:<ul><li>`attributablePartnerId` (String): De id voor de segmentprovider die eigenaar is van de assignSegmentId.</li><li>`attributableSegmentId` (String): Het segment dat door de gebruiker als doel is opgegeven in de doelregel van de plaatsing. Dit wordt gebruikt om de kosten en de betalende partners te volgen.</li><li>`segments` (String): Het snijpunt van de gebruikerssegmenten a\) waartoe de gebruiker behoorde, en b\) waarop de advertentie was gericht. Dit is niet de volledige lijst van segmenten waartoe de gebruiker op het tijdstip van de veiling behoorde.</li></ul> |
| `optimizationTag` | String | De tag voor optimalisatie. |
| `attributableDeviceGraphId` | String | De id voor de apparaatgrafiek die aan een conversiegebeurtenis wordt toegewezen. |

## `productDetails` {#productDetails}

Het `productDetails` -object bevat informatie over producten die in winkeladvertenties voor [!DNL Adobe Advertising Search, Social, & Commerce] worden weergegeven, zoals product-id&#39;s, land, taal, partitie, titel en type advertentie.

![ diagram dat van het Schema het `productDetails` voorwerp en zijn gebieden toont.](../../images/field-groups/advertising-full-extension/productDetails.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `productID` | String | De id voor het product die is vermeld in de advertentie die aan deze gebeurtenis is gekoppeld. |
| `country` | String | Het land van verkoop voor het product in de advertentie die bij het evenement hoort. |
| `language` | String | De taal van uw productinformatie, zoals die in de gegevens van het Merchant Center van de cliënt wordt vermeld. |
| `partitionID` | String | De id voor de productgroep die bij deze gebeurtenis aan de advertentie is gekoppeld. |
| `title` | String | De producttitel die in de advertentie wordt weergegeven. |
| `adType` | String | Het advertentietype voor het product dat wordt gebruikt in [!DNL Google] Winkelcampagnes. Mogelijke waarden zijn:<ul><li>`pla_with_pog`: Wanneer de gebeurtenis van een aankoop via een advertentie is gekomen</li><li>`pla`: Toen de gebeurtenis van een advertentie kwam.</li><li>`pla_multichannel`: Wanneer de gebeurtenis van een winkeladvertentie opties bevatte voor zowel &quot;online&quot; als &quot;lokale&quot; winkelkanalen.</li><li>`pla_with_promotion`: Wanneer de gebeurtenis van een winkeladvertentie een commerciële promotie vertoonde.</li></ul> |

## Volgende stappen

In dit document wordt de structuur en het gebruik van hoofdletters en kleine letters beschreven voor de veldgroep met extensies van [!DNL Advertising Cloud] . Voor meer details op de gebiedsgroep zelf, verwijs naar de [ openbare bewaarplaats XDM ](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/adcloud/experienceevent-all.schema.json).

Als u deze gebiedsgroep gebruikt om [!DNL Advertising] gegevens te verzamelen gebruikend het Web SDK van Adobe Experience Platform, zie de gids op [ vormend een datastream ](../../../datastreams/overview.md) om te leren hoe te om gegevens aan XDM op de server in kaart te brengen.

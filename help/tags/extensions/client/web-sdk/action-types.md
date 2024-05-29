---
title: Handelingstypen in de Adobe Experience Platform Web SDK Extension
description: Leer meer over de verschillende actietypen die door de de marktextensie van SDK van het Web van Adobe Experience Platform worden verstrekt.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: 377be6d97e6da9b4aaacfa23a188131bd38e66f4
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---


# Typen handelingen

Nadat u vormt [Adobe Experience Platform Web SDK-tagextensie](web-sdk-extension-configuration.md), moet u uw actietypes vormen.

Op deze pagina worden de actietypen beschreven die door de [Adobe Experience Platform Web SDK-tagextensie](web-sdk-extension-configuration.md).

## Gebeurtenis Send {#send-event}

Hiermee wordt een gebeurtenis naar de Adobe verzonden [!DNL Experience Platform] zodat Adobe Experience Platform de gegevens die u verzendt kan verzamelen en op die gegevens kan reageren. Selecteer een instantie (als u meerdere exemplaren hebt). Alle gegevens die u wilt verzenden, kunnen worden verzonden in het dialoogvenster **[!UICONTROL XDM Data]** veld. Gebruik een JSON-object dat voldoet aan de structuur van uw XDM-schema. Dit object kan op uw pagina worden gemaakt of via een **[!UICONTROL Custom Code]** **[!UICONTROL Data Element]**.

Er zijn een paar andere gebieden in het Send actietype van de Gebeurtenis die ook afhankelijk van uw implementatie nuttig zouden kunnen zijn. Deze velden zijn allemaal optioneel.

- **Type:** In dit veld kunt u een gebeurtenistype opgeven dat in uw XDM-schema wordt opgenomen. Zie [`type`](/help/web-sdk/commands/sendevent/type.md) in de `sendEvent` voor meer informatie.
- **Gegevens:** Gegevens die niet overeenkomen met een XDM-schema kunnen met dit veld worden verzonden. Dit veld is handig als u probeert een Adobe Target-profiel bij te werken of Recommendations-kenmerken van het doel te verzenden. Zie [`data`](/help/web-sdk/commands/sendevent/data.md) in de `sendEvent` voor meer informatie.<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
- **Gegevensset-id:** Als u gegevens naar een dataset buiten moet verzenden u in uw gegevensstroom specificeerde, kunt u die dataset identiteitskaart hier specificeren.
- **Document wordt verwijderd:** Als u ervoor wilt zorgen dat de gebeurtenissen de server bereiken zelfs als de gebruiker vanaf de pagina navigeert, controleert u de **[!UICONTROL Document will unload]** selectievakje. Hierdoor kunnen gebeurtenissen de server bereiken, maar reacties worden genegeerd.
- **Render visuele verpersoonlijkingsbesluiten:** Als u gepersonaliseerde inhoud op uw pagina wilt teruggeven, controleer **[!UICONTROL Render visual personalization decisions]** selectievakje. Indien nodig kunt u ook het beslissingsbereik en/of de oppervlakken opgeven. Zie de [verpersoonlijkingsdocumentatie](/help/web-sdk/personalization/rendering-personalization-content.md#automatically-rendering-content) voor meer informatie over het renderen van gepersonaliseerde inhoud.

## Goedkeuring instellen {#set-consent}

Nadat u toestemming van uw gebruiker hebt ontvangen, moet deze toestemming aan het Web SDK van Adobe Experience Platform worden meegedeeld door het &quot;Vastgestelde type van de Actie van de Toestemming te gebruiken&quot;. Momenteel worden twee typen standaarden ondersteund: &quot;Adobe&quot; en &quot;IAB TCF.&quot; Zie [Voorkeuren voor goedkeuring door klant ondersteunen](/help/web-sdk/consent/supporting-consent.md). Bij gebruik van Adobe versie 2.0 wordt alleen een waarde voor een gegevenselement ondersteund. U moet een gegevenselement maken dat wordt omgezet in het toestemmingsobject.

In deze handeling krijgt u ook een optioneel veld met een identiteitskaarten, zodat identiteiten kunnen worden gesynchroniseerd zodra de toestemming is ontvangen. Het synchroniseren is nuttig wanneer de toestemming als &quot;In behandeling&quot;of &quot;uit&quot;wordt gevormd omdat de toestemmingsvraag waarschijnlijk de eerste vraag aan brand is.

## Variabele bijwerken {#update-variable}

Gebruik deze handeling om een XDM-object als resultaat van een gebeurtenis te wijzigen. Deze handeling is bedoeld om een object op te bouwen waarnaar later kan worden verwezen vanuit een **[!UICONTROL Send event]** handeling, om het XDM-gebeurtenisobject op te nemen.

Als u dit actietype wilt gebruiken, moet u een [variabel](data-element-types.md#variable) gegevenselement. Nadat u een variabel gegevenselement hebt gekozen dat u wilt wijzigen, wordt een editor weergegeven die lijkt op de editor voor de [XDM-object](data-element-types.md#xdm-object) gegevenselement.

![](assets/update-variable.png)

Het XDM-schema dat voor de editor wordt gebruikt, is het schema dat op het [!UICONTROL variable] gegevenselement. U kunt een of meer eigenschappen van het object instellen door op een van de eigenschappen in de boomstructuur links te klikken en vervolgens de waarde aan de rechterkant te wijzigen. In de onderstaande schermafbeelding wordt de eigenschap productionBy bijvoorbeeld ingesteld op het gegevenselement &quot;Geproduceerd door gegevenselement&quot;.

![](assets/update-variable-set-property.png)

Er zijn sommige verschillen tussen de redacteur in de update veranderlijke actie tegenover de redacteur in het XDM objecten gegevenselement. Eerst heeft de actie van de updatevariabele een punt op wortelniveau genoemd &quot;xdm.&quot; Als u op dit item klikt, kunt u een gegevenselement opgeven dat moet worden gebruikt om het gehele object in te stellen. Ten tweede bevat de actie voor de updatevariabele selectievakjes om de gegevens van het xdm-object te wissen. Klik op een van de eigenschappen aan de linkerkant en schakel het selectievakje aan de rechterkant in om de waarde te wissen. Hierdoor wordt de huidige waarde gewist voordat waarden op de variabele worden ingesteld.

## Media-gebeurtenis verzenden {#send-media-event}

Hiermee verzendt u een mediagebeurtenis naar Adobe Experience Platform en/of Adobe Analytics. Deze handeling is handig wanneer u mediafouten op uw website bijhoudt. Selecteer een instantie (als u meerdere exemplaren hebt). De handeling vereist een `playerId` die een unieke id vertegenwoordigt voor een bijgehouden mediasessie. Het vereist ook een **[!UICONTROL Quality of Experience]** en `playhead` data element when starting a media session.

![Platform UI-afbeelding die het scherm voor het verzenden van media-gebeurtenissen weergeeft.](assets/send-media-event.png)

De **[!UICONTROL Send media event]** Het handelingstype ondersteunt de volgende eigenschappen:

- **[!UICONTROL Instance]**: De Web SDK-instantie die wordt gebruikt.
- **[!UICONTROL Media Event Type]**: Het type media-gebeurtenis dat wordt bijgehouden.
- **[!UICONTROL Player ID]**: De unieke id van de mediasessie.
- **[!UICONTROL Playhead]**: De huidige positie van het afspelen van media, in seconden.
- **[!UICONTROL Media session details]**: Bij het verzenden van een media start-gebeurtenis moeten de vereiste mediasessiedetails worden opgegeven.
- **[!UICONTROL Chapter details]**: In deze sectie kunt u de hoofdstukdetails opgeven wanneer u een hoofdstukstartmedia-gebeurtenis verzendt.
- **[!UICONTROL Advertising details]**: Wanneer u een `AdBreakStart` moet u de vereiste advertentiegegevens opgeven.
- **[!UICONTROL Advertising pod details]**: Details over de advertentiepod bij het verzenden van een `AdStart` gebeurtenis.
- **[!UICONTROL Error details]**: Details over de afspeelfout die wordt bijgehouden.
- **[!UICONTROL State Update Details]**: De toestand van de speler die wordt bijgewerkt.
- **[!UICONTROL Custom Metadata]**: De aangepaste metagegevens over de mediagebeurtenis die wordt bijgehouden.
- **[!UICONTROL Quality of Experience]**: De mediakwaliteit van ervaringsgegevens die worden bijgehouden.

## Media Analytics-beheer ophalen {#get-media-analytics-tracker}

Deze handeling wordt gebruikt om de verouderde Media Analytics API op te halen. Wanneer de handeling wordt geconfigureerd en een objectnaam wordt opgegeven, wordt de verouderde Media Analytics-API geëxporteerd naar dat vensterobject. Als er niets is opgegeven, wordt deze geëxporteerd naar `window.Media` zoals in de huidige Media JS-bibliotheek.

![Platform UI-afbeelding die het actietype Get Media Analytics Tracker weergeeft.](assets/get-media-analytics-tracker.png)

## Volgende stappen {#next-steps}

Na het lezen van dit artikel, zou u een beter inzicht in moeten hebben hoe te om uw acties te vormen. Lees vervolgens hoe u [configureren, gegevenselementen](data-element-types.md).

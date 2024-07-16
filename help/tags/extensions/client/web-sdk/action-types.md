---
title: Handelingstypen in de Adobe Experience Platform Web SDK Extension
description: Leer meer over de verschillende actietypen die door de de marktextensie van SDK van het Web van Adobe Experience Platform worden verstrekt.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: fb9f7757d77b221c733bbed5124fa576a6b02ed2
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 0%

---


# Typen handelingen

Nadat u de [ de markeringsuitbreiding van SDK van het Web van Adobe Experience Platform ](web-sdk-extension-configuration.md) vormt, moet u uw actietypen vormen.

Deze pagina beschrijft de actietypes die door de [ de markeringsuitbreiding van SDK van het Web van Adobe Experience Platform ](web-sdk-extension-configuration.md) worden gesteund.


## Antwoord toepassen {#apply-response}

Gebruik het actietype **[!UICONTROL Apply response]** wanneer u verschillende acties wilt uitvoeren die op een reactie van de Edge Network worden gebaseerd. Dit actietype wordt typisch gebruikt in hybride plaatsingen waar de server een aanvankelijke vraag aan de Edge Network maakt, dan neemt dit actietype de reactie van die vraag en initialiseert het Web SDK in browser.

Met dit actietype kan de laadtijd van de client worden verkort bij gebruik van hybride personalisatie.

![ Beeld van het gebruikersinterface van het Experience Platform die het Apply reactietactietype tonen.](assets/apply-response.png)

Dit handelingstype ondersteunt de volgende configuratieopties:

* **[!UICONTROL Instance]**: Selecteer de Web SDK-instantie die u gebruikt.
* **[!UICONTROL Response headers]**: Selecteer het gegevenselement dat een object retourneert dat de headertoetsen en waarden bevat die door de serveraanroep van de Edge Network worden geretourneerd.
* **[!UICONTROL Response body]**: selecteer het gegevenselement dat het object retourneert dat de JSON-payload bevat die door de reactie van de Edge Network wordt opgegeven.
* **[!UICONTROL Render visual personalization decisions]**: Schakel deze optie in om automatisch de personalisatie-inhoud te renderen die door de Edge Network wordt geleverd en om flikkering te voorkomen de inhoud vooraf te verbergen.

## Gebeurtenis Send {#send-event}

Verstuurt een gebeurtenis naar Adobe [!DNL Experience Platform] zodat Adobe Experience Platform de gegevens die u verzendt kan verzamelen en op die informatie kan reageren. Selecteer een instantie (als u meerdere exemplaren hebt). Alle gegevens die u wilt verzenden, kunnen in het veld **[!UICONTROL XDM Data]** worden verzonden. Gebruik een JSON-object dat voldoet aan de structuur van uw XDM-schema. Dit object kan op de pagina worden gemaakt of via een **[!UICONTROL Custom Code]** **[!UICONTROL Data Element]** .

Er zijn een paar andere gebieden in het Send actietype van de Gebeurtenis die ook afhankelijk van uw implementatie nuttig zouden kunnen zijn. Deze velden zijn allemaal optioneel.

* **Type:** Dit gebied staat u toe specificeert een gebeurtenistype dat in uw schema XDM zal worden geregistreerd. Zie [`type`](/help/web-sdk/commands/sendevent/type.md) in het `sendEvent` bevel voor meer informatie.
* **Gegevens:** Gegevens die geen schema XDM aanpassen kunnen worden verzonden gebruikend dit gebied. Dit veld is handig als u probeert een Adobe Target-profiel bij te werken of Recommendations-kenmerken van het doel te verzenden. Zie [`data`](/help/web-sdk/commands/sendevent/data.md) in het `sendEvent` bevel voor meer informatie.<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
* **identiteitskaart van de Dataset:** Als u gegevens naar een dataset buiten moet verzenden u in uw gegevensstroom specificeerde, kunt u die datasetidentiteitskaart hier specificeren.
* **het Document zal ontladen:** als u zou willen ervoor zorgen dat de gebeurtenissen de server bereiken zelfs als de gebruiker vanaf de pagina navigeert, controleer **[!UICONTROL Document will unload]** checkbox. Hierdoor kunnen gebeurtenissen de server bereiken, maar reacties worden genegeerd.
* **geeft visuele verpersoonlijkingsbesluiten terug:** Als u gepersonaliseerde inhoud op uw pagina wilt teruggeven, controleer **[!UICONTROL Render visual personalization decisions]** checkbox. Indien nodig kunt u ook het beslissingsbereik en/of de oppervlakken opgeven. Zie de [ verpersoonlijkingsdocumentatie ](/help/web-sdk/personalization/rendering-personalization-content.md#automatically-rendering-content) voor meer informatie bij het teruggeven van gepersonaliseerde inhoud.

## Goedkeuring instellen {#set-consent}

Nadat u toestemming van uw gebruiker hebt ontvangen, moet deze toestemming aan het Web SDK van Adobe Experience Platform worden meegedeeld door het &quot;Vastgestelde type van de Actie van de Toestemming te gebruiken&quot;. Momenteel worden twee typen standaarden ondersteund: &quot;Adobe&quot; en &quot;IAB TCF.&quot; Zie [ Ondersteunende Voorkeur van de Klanteninstemming ](../../../../web-sdk/commands/setconsent.md). Bij gebruik van Adobe versie 2.0 wordt alleen een waarde voor een gegevenselement ondersteund. U moet een gegevenselement maken dat wordt omgezet in het toestemmingsobject.

In deze handeling krijgt u ook een optioneel veld met een identiteitskaarten, zodat identiteiten kunnen worden gesynchroniseerd zodra de toestemming is ontvangen. Het synchroniseren is nuttig wanneer de toestemming als &quot;In behandeling&quot;of &quot;uit&quot;wordt gevormd omdat de toestemmingsvraag waarschijnlijk de eerste vraag aan brand is.

## Variabele bijwerken {#update-variable}

Gebruik deze handeling om een XDM-object als resultaat van een gebeurtenis te wijzigen. Deze handeling is bedoeld om een object op te bouwen waarnaar later kan worden verwezen vanuit een **[!UICONTROL Send event]** -actie, om het XDM-gebeurtenisobject op te nemen.

Om dit actietype te gebruiken moet u a [ veranderlijk ](data-element-types.md#variable) gegevenselement van a. hebben bepaald. Zodra u een veranderlijk gegevenselement kiest om te wijzigen, verschijnt een redacteur, gelijkend op de redacteur voor het [ XDM voorwerp ](data-element-types.md#xdm-object) gegevenselement.

![](assets/update-variable.png)

Het XDM-schema dat voor de editor wordt gebruikt, is het schema dat voor het gegevenselement [!UICONTROL variable] is geselecteerd. U kunt een of meer eigenschappen van het object instellen door op een van de eigenschappen in de boomstructuur links te klikken en vervolgens de waarde aan de rechterkant te wijzigen. In de onderstaande schermafbeelding wordt de eigenschap productionBy bijvoorbeeld ingesteld op het gegevenselement &quot;Geproduceerd door gegevenselement&quot;.

![](assets/update-variable-set-property.png)

Er zijn sommige verschillen tussen de redacteur in de update veranderlijke actie tegenover de redacteur in het XDM objecten gegevenselement. Eerst heeft de actie van de updatevariabele een punt op wortelniveau genoemd &quot;xdm.&quot; Als u op dit item klikt, kunt u een gegevenselement opgeven dat moet worden gebruikt om het gehele object in te stellen. Ten tweede bevat de actie voor de updatevariabele selectievakjes om de gegevens van het xdm-object te wissen. Klik op een van de eigenschappen aan de linkerkant en schakel het selectievakje aan de rechterkant in om de waarde te wissen. Hierdoor wordt de huidige waarde gewist voordat waarden op de variabele worden ingesteld.

## Media-gebeurtenis verzenden {#send-media-event}

Hiermee verzendt u een mediagebeurtenis naar Adobe Experience Platform en/of Adobe Analytics. Deze handeling is handig wanneer u mediafouten op uw website bijhoudt. Selecteer een instantie (als u meerdere exemplaren hebt). De handeling vereist een `playerId` die een unieke id vertegenwoordigt voor een bijgehouden mediasessie. Bij het starten van een mediasessie is ook een **[!UICONTROL Quality of Experience]** - en `playhead` -gegevenselement nodig.

![ beeld UI van het Platform dat het send scherm van de media gebeurtenis toont.](assets/send-media-event.png)

Het handelingstype **[!UICONTROL Send media event]** ondersteunt de volgende eigenschappen:

* **[!UICONTROL Instance]**: De Web SDK-instantie die wordt gebruikt.
* **[!UICONTROL Media Event Type]**: Het type media-gebeurtenis dat wordt bijgehouden.
* **[!UICONTROL Player ID]**: De unieke id van de mediasessie.
* **[!UICONTROL Playhead]**: De huidige positie van het afspelen van media, in seconden.
* **[!UICONTROL Media session details]**: Bij het verzenden van een media start-gebeurtenis moeten de vereiste mediasessiedetails worden opgegeven.
* **[!UICONTROL Chapter details]**: In deze sectie kunt u de hoofdstukdetails opgeven wanneer u een hoofdstukstartmedia-gebeurtenis verzendt.
* **[!UICONTROL Advertising details]**: wanneer u een `AdBreakStart` -gebeurtenis verzendt, moet u de vereiste advertentiedetails opgeven.
* **[!UICONTROL Advertising pod details]**: details over de advertentiepod wanneer u een `AdStart` -gebeurtenis verzendt.
* **[!UICONTROL Error details]**: details over de afspeelfout die wordt bijgehouden.
* **[!UICONTROL State Update Details]**: De spelerstatus die wordt bijgewerkt.
* **[!UICONTROL Custom Metadata]**: De aangepaste metagegevens over de mediagebeurtenis die wordt bijgehouden.
* **[!UICONTROL Quality of Experience]**: De mediakwaliteit van ervaringsgegevens die worden bijgehouden.

## Media Analytics-beheer ophalen {#get-media-analytics-tracker}

Deze handeling wordt gebruikt om de verouderde Media Analytics API op te halen. Wanneer de handeling wordt geconfigureerd en een objectnaam wordt opgegeven, wordt de verouderde Media Analytics-API geëxporteerd naar dat vensterobject. Als er niets is opgegeven, wordt deze geëxporteerd naar `window.Media` zoals in de huidige Media JS-bibliotheek.

![ beeld van Platform UI die het Get de actietype van de Traceur van de Analyse van Media toont.](assets/get-media-analytics-tracker.png)

## Omleiden met identiteit {#redirect-with-identity}

Gebruik dit actietype om identiteiten van de huidige pagina aan andere domeinen te delen. Deze handeling is bedoeld voor gebruik met een **[!UICONTROL click]** -gebeurtenistype en een vergelijkingsvoorwaarde voor waarden. Zie [ identiteit toevoegen aan URL gebruikend de uitbreiding van SDK van het Web ](../../../../web-sdk/commands/appendidentitytourl.md#extension) voor meer informatie over hoe te om dit actietype te gebruiken.

## Volgende stappen {#next-steps}

Na het lezen van dit artikel, zou u een beter inzicht in moeten hebben hoe te om uw acties te vormen. Daarna, lees over hoe te [ uw types van gegevenselement ](data-element-types.md) vormen.

---
title: Handelingstypen in de Adobe Experience Platform Web SDK Extension
description: Leer meer over de verschillende actietypen die door de de marktextensie van SDK van het Web van Adobe Experience Platform worden verstrekt.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: 760484bb7f95df97701f81f78783f0214aecaf5b
workflow-type: tm+mt
source-wordcount: '1969'
ht-degree: 0%

---


# Typen handelingen

Nadat u de [ de markeringsuitbreiding van SDK van het Web van Adobe Experience Platform ](web-sdk-extension-configuration.md) vormt, moet u uw actietypen vormen.

Deze pagina beschrijft de actietypes die door de [ de markeringsuitbreiding van SDK van het Web van Adobe Experience Platform ](web-sdk-extension-configuration.md) worden gesteund.

## Proposities toepassen {#apply-propositions}

Met het actietype **[!UICONTROL Apply propositions]** kunt u profielen weergeven in toepassingen van één pagina zonder dat de metriek toeneemt.

Dit handelingstype is handig wanneer u werkt met toepassingen van één pagina waarin delen van de pagina opnieuw worden weergegeven, waardoor eventuele al op de pagina toegepaste aanpassingen mogelijk worden overschreven.

U kunt dit actietype voor diverse gebruiksgevallen gebruiken, zoals:

1. **geeft mbox HTML aanbiedingen** terug. Proposities die expliciet via een bereik of oppervlak van een **[!UICONTROL Send event]** -actie worden aangevraagd, worden niet automatisch gerenderd. U kunt het actietype **[!UICONTROL Apply propositions]** gebruiken om Web SDK te vertellen waar te om hen terug te geven door de propositiemeta-gegevens te specificeren.
2. **geef de aanbiedingen voor een mening op een enig-paginatoepassing** terug. Als bij het renderen van een weergavewijzigingsgebeurtenis de analysegegevens nog niet beschikbaar zijn, kunt u de handeling **[!UICONTROL Apply propositions]** gebruiken om de weergavevoorstellingen boven aan de pagina weer te geven. Zie [ bovenkant en bodem van paginagebeurtenissen (Tweede paginamening - Optie 2) ](../../../../web-sdk/use-cases/top-bottom-page-events.md) voor meer details. Als u dit wilt gebruiken, voert u een **[!UICONTROL View name]** in het formulier in.
3. **teruggeven voorstellingen**. Wanneer uw site gebruikmaakt van een framework zoals Reageren om inhoud opnieuw te renderen, moet u mogelijk de personalisatie opnieuw toepassen. In dergelijke gevallen kunt u hiervoor het actietype **[!UICONTROL Apply propositions]** gebruiken.

Dit actietype zal geen vertoningsgebeurtenis voor teruggegeven voorstellingen verzenden. Het zal spoor van teruggegeven voorstellingen houden zodat deze in verdere **[!UICONTROL Send event]** vraag kunnen worden omvat.


![ de Markeringen UI van het Platform die het Apply actietype van Voorstellen tonen.](assets/apply-propositions.png)

Dit handelingstype ondersteunt de volgende velden:

* **[!UICONTROL Propositions]**: Een array van propositieobjecten die u opnieuw wilt renderen.
* **[!UICONTROL View name]**: De naam van de weergave die moet worden weergegeven.
* **[!UICONTROL Proposition metadata]**: Een object dat bepaalt hoe HTML-aanbiedingen kunnen worden toegepast. U kunt deze informatie opgeven via het formulier of via een gegevenselement. Het bevat de volgende eigenschappen:
   * **[!UICONTROL Scope]**
   * **[!UICONTROL Selector]**
   * **[!UICONTROL Action type]**

## Antwoord toepassen {#apply-response}

Gebruik het actietype **[!UICONTROL Apply response]** wanneer u verschillende acties wilt uitvoeren die op een reactie van de Edge Network worden gebaseerd. Dit actietype wordt typisch gebruikt in hybride plaatsingen waar de server een aanvankelijke vraag aan de Edge Network maakt, dan neemt dit actietype de reactie van die vraag en initialiseert het Web SDK in browser.

Met dit actietype kan de laadtijd van de client worden verkort bij gebruik van hybride personalisatie.

![ Beeld van het gebruikersinterface van het Experience Platform die het Apply reactietactietype tonen.](assets/apply-response.png)

Dit handelingstype ondersteunt de volgende configuratieopties:

* **[!UICONTROL Instance]**: Selecteer de Web SDK-instantie die u gebruikt.
* **[!UICONTROL Response headers]**: Selecteer het gegevenselement dat een object retourneert dat de headertoetsen en waarden bevat die door de serveraanroep van de Edge Network worden geretourneerd.
* **[!UICONTROL Response body]**: selecteer het gegevenselement dat het object retourneert dat de JSON-payload bevat die door de reactie van de Edge Network wordt opgegeven.
* **[!UICONTROL Render visual personalization decisions]**: Schakel deze optie in om automatisch de personalisatie-inhoud te renderen die door de Edge Network wordt geleverd en om flikkering te voorkomen de inhoud vooraf te verbergen.

## Regels evalueren {#evaluate-rulesets}

Dit actietype activeert manueel liniaalevaluatie. Regels worden door Adobe Journey Optimizer geretourneerd ter ondersteuning van functies zoals in-browser berichten.

![ Beeld van het gebruikersinterface die van het Experience Platform het Evaluate type van de liniaalreactie toont.](assets/evaluate-rulesets.png)

Dit handelingstype ondersteunt de volgende opties:

* **[!UICONTROL Render visual personalization decisions]**: Schakel deze optie in om visuele aanpassingsbeslissingen te renderen voor de liniaalitems die overeenkomen.
* **[!UICONTROL Decision context]**: dit is een sleutel-waardekaart die wordt gebruikt wanneer het evalueren van de Adobe Journey Optimizer-regels voor het op-apparaat beslissen. U kunt de besluitvormingscontext manueel of door een gegevenselement verstrekken.

## Media Analytics-beheer ophalen {#get-media-analytics-tracker}

Deze handeling wordt gebruikt om de verouderde Media Analytics API op te halen. Wanneer de handeling wordt geconfigureerd en een objectnaam wordt opgegeven, wordt de verouderde Media Analytics-API geëxporteerd naar dat vensterobject. Als er niets is opgegeven, wordt deze geëxporteerd naar `window.Media` zoals in de huidige Media JS-bibliotheek.

![ beeld van Platform UI die het Get de actietype van de Traceur van de Analyse van Media toont.](assets/get-media-analytics-tracker.png)

## Omleiden met identiteit {#redirect-with-identity}

Gebruik dit actietype om identiteiten van de huidige pagina aan andere domeinen te delen. Deze handeling is bedoeld voor gebruik met een **[!UICONTROL click]** -gebeurtenistype en een vergelijkingsvoorwaarde voor waarden. Zie [ identiteit toevoegen aan URL gebruikend de uitbreiding van SDK van het Web ](../../../../web-sdk/commands/appendidentitytourl.md#extension) voor meer informatie over hoe te om dit actietype te gebruiken.

## Gebeurtenis Send {#send-event}

Verzendt een gebeurtenis naar het Experience Platform, zodat Platform de gegevens kan verzamelen die u verzendt en op die informatie kan handelen. Alle gegevens die u wilt verzenden, kunnen in het veld **[!UICONTROL XDM Data]** worden verzonden. Gebruik een [!DNL JSON] -object dat voldoet aan de structuur van uw [!DNL XDM] -schema. Dit object kan op de pagina worden gemaakt of via een **[!UICONTROL Custom Code]** **[!UICONTROL Data Element]** .

Het handelingstype **[!UICONTROL Send Event]** ondersteunt de onderstaande velden en instellingen. Deze velden zijn allemaal optioneel.

### Instantie-instellingen {#instance}

Gebruik de kiezer van **[!UICONTROL Instance]** om de Web SDK-instantie te kiezen die u wilt configureren. Als u slechts één instantie hebt, wordt deze vooraf geselecteerd.

![ beeld van de Markeringen UI van het Platform die de instantiemontages voor het Send actietype van de Gebeurtenis tonen.](assets/instance-settings.png)

* **[!UICONTROL Instance]**: Selecteer de instantie van SDK van het Web die u wilt vormen. Als u slechts één instantie hebt, wordt deze vooraf geselecteerd.
* **[!UICONTROL Use guided events]**: Schakel deze optie in om bepaalde velden automatisch in te vullen of te verbergen om een bepaald geval van gebruik in te schakelen. Als u deze optie inschakelt, worden de volgende instellingen weergegeven.
   * **[!UICONTROL Request personalization]**: Deze gebeurtenis moet boven aan de pagina worden aangeroepen. Wanneer deze gebeurtenis is geselecteerd, worden de volgende velden ingesteld:
      * **[!UICONTROL Type]**: **[!UICONTROL Decisioning Proposition Fetch]**
      * **[!UICONTROL Automatically send a display event]**: **[!UICONTROL false]**
      * Schakel de optie **[!UICONTROL Render visual personalization decisions]** in als u de personalisatie in dit geval automatisch wilt renderen.
   * **[!UICONTROL Collect analytics]**: deze gebeurtenis moet onder aan de pagina worden aangeroepen. Wanneer deze gebeurtenis is geselecteerd, worden de volgende velden ingesteld:
      * **[!UICONTROL Include rendered propositions]**: **[!UICONTROL true]**
      * De **[!UICONTROL Personalization]** -instellingen zijn verborgen

  >[!NOTE]
  >
  >De geleide gebeurtenissen zijn verwant met [ bovenkant en bodem van paginagebeurtenissen ](../../../../web-sdk/use-cases/top-bottom-page-events.md).


### Gegevens {#data}

![ beeld van de Markeringen UI van het Platform die de het elementenmontages van Gegevens voor het Send actietype van de Gebeurtenis tonen.](assets/data.png)

* **[!UICONTROL Type]**: In dit veld kunt u een gebeurtenistype opgeven dat wordt opgenomen in uw XDM-schema. Zie [`type`](/help/web-sdk/commands/sendevent/type.md) in het `sendEvent` bevel voor meer informatie.
* **[!UICONTROL XDM]**:
* **[!UICONTROL Data]**: Gebruik dit veld om gegevens te verzenden die niet overeenkomen met een XDM-schema. Dit veld is handig als u probeert een Adobe Target-profiel bij te werken of Recommendations-kenmerken van het doel te verzenden. Zie [`data`](/help/web-sdk/commands/sendevent/data.md) in het `sendEvent` bevel voor meer informatie.
* **[!UICONTROL Include rendered propositions]**: Schakel deze optie in om alle voorstellingen op te nemen die zijn gerenderd, maar er is geen weergavegebeurtenis verzonden. Gebruik dit in combinatie met **[!UICONTROL Automatically send a display event]** uitgeschakeld. Met deze instelling wordt het XDM-veld `_experience.decisioning` bijgewerkt met informatie over de gerenderde profielen.
* **[!UICONTROL Document will unload]**: Schakel deze optie in om ervoor te zorgen dat de gebeurtenissen de server bereiken, zelfs als de gebruiker bij de pagina vandaan navigeert. Hierdoor kunnen gebeurtenissen de server bereiken, maar reacties worden genegeerd.
* **[!UICONTROL Merge ID]**: **Dit gebied wordt afgekeurd**. Hiermee wordt het XDM-veld `eventMergeId` gevuld.

### Personalisatie {#personalization}

![ beeld van de Markeringen UI van het Platform die de montages van Personalization voor het Send actietype van de Gebeurtenis tonen.](assets/personalization-settings.png)

* **[!UICONTROL Scopes]**: selecteer het bereik (Adobe Target [!DNL mboxes] ) dat u expliciet wilt aanvragen voor personalisatie. U kunt het bereik handmatig invoeren of een gegevenselement opgeven.
* **[!UICONTROL Surfaces]**: stel de weboppervlakken in die beschikbaar zijn op de pagina voor personalisatie. Zie de [ documentatie van Adobe Journey Optimizer ](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) voor meer details.
* **geeft visuele verpersoonlijkingsbesluiten terug:** Als u gepersonaliseerde inhoud op uw pagina wilt teruggeven, controleer **[!UICONTROL Render visual personalization decisions]** checkbox. Indien nodig kunt u ook het beslissingsbereik en/of de oppervlakken opgeven. Zie de [ verpersoonlijkingsdocumentatie ](/help/web-sdk/personalization/rendering-personalization-content.md#automatically-rendering-content) voor meer informatie bij het teruggeven van gepersonaliseerde inhoud.
* **[!UICONTROL Request default personalization]**: gebruik deze sectie om te bepalen of het bereik (globale mbox) voor de hele pagina en het standaardoppervlak (weboppervlak op basis van de huidige URL) worden aangevraagd. Deze wordt standaard automatisch aangevraagd tijdens de eerste `sendEvent` oproep van het laden van de pagina. U kunt uit de volgende opties kiezen:
   * **[!UICONTROL Automatic]**: dit is het standaardgedrag. Vraag slechts standaardverpersoonlijking aan wanneer het nog niet gevraagd is. Dit komt overeen met `requestDefaultPersonalization` niet ingesteld in de opdracht Web SDK.
   * **[!UICONTROL Enabled]**: vraag expliciet om het paginabereik en het standaardoppervlak. Hiermee werkt u de SPA weergavecache bij. Dit komt overeen met `requestDefaultPersonalization` ingesteld op `true` .
   * **[!UICONTROL Disabled]**: Hiermee onderdrukt u expliciet de aanvraag voor het paginabereik en het standaardoppervlak. Dit komt overeen met `requestDefaultPersonalization` ingesteld op `false` .
* **[!UICONTROL Decision context]**: dit is een sleutel-waardekaart die wordt gebruikt wanneer het evalueren van de Adobe Journey Optimizer-regels voor het op-apparaat beslissen. U kunt de besluitvormingscontext manueel of door een gegevenselement verstrekken.

### DataStream-configuratieoverschrijvingen {#datastream-overrides}

Met overschrijvingen van gegevensstroom kunt u aanvullende configuraties voor uw gegevensstreams definiëren. Deze configuraties worden via de SDK van het web doorgegeven aan de Edge Network.

Dit helpt u verschillend gegevensstroomgedrag dan de standaarddegenen teweegbrengen, zonder het creëren van een nieuwe gegevensstroom of het wijzigen van uw bestaande montages. Zie de documentatie op [ vormend datastream treedt ](web-sdk-extension-configuration.md#datastream-overrides) voor meer details met voeten.

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

## Volgende stappen {#next-steps}

Na het lezen van dit artikel, zou u een beter inzicht in moeten hebben hoe te om uw acties te vormen. Daarna, lees over hoe te [ uw types van gegevenselement ](data-element-types.md) vormen.

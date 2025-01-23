---
title: Opmerkingen bij de release Adobe Experience Platform Web SDK
description: Adobe Experience Platform Web SDK-tagextensie
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: 08b07aa874b9ca9b5ea76850d6c0320bddddc85e
workflow-type: tm+mt
source-wordcount: '2400'
ht-degree: 5%

---

# Opmerkingen bij de release Adobe Experience Platform Web SDK

In dit document worden de releaseopmerkingen voor de Adobe Experience Platform Web SDK-tagextensie besproken. Voor de recentste versienota&#39;s op SDK zelf, zie de [ de versienota&#39;s van SDK van het Web van het Platform ](/help/web-sdk/release-notes.md).

## Versie 2.28.0 - woensdag 23 januari 2024

**Bevestigingen en verbeteringen**

- Correctie van een probleem waarbij ID Sync Container-overschrijvingen niet konden worden ingesteld zonder Audience Manager in te schakelen.
- Probleem verholpen waarbij Data Stream config overschrijvingen uitgeschakeld werden tijdens de upgrade naar de meest recente versie.
- Probleem verholpen waarbij gebruikers de instellingen voor automatisch klikken op doelverzameling niet konden opslaan.

**Nieuwe Eigenschappen**

- Er is een nieuwe functie toegevoegd om te schakelen tussen technische namen en weergavenamen in het XDM-object.
- Bevat [ versie 2.25.0 ](../../../../web-sdk/release-notes.md#2-25-0) van het Web SDK van Adobe Experience Platform.

## Versie 2.27.0 - vrijdag 31 oktober 2024

**Nieuwe functies**

- [ DataStream treedt ](../web-sdk/web-sdk-extension-configuration.md#datastream-overrides) nu montages met voeten om de oplossingen van het Experience Cloud en de diensten van Adobe Experience Platform onbruikbaar te maken.
- U kunt [ datastream overschrijvingen ](../web-sdk/web-sdk-extension-configuration.md) voor media zittingen nu tot stand brengen.

Bevat versie 2.24.0 van Adobe Experience Platform Web SDK.

## Versie 2.26.1 - 19 september 2024

**Bevestigingen en verbeteringen**

- Probleem verholpen waarbij cookies niet correct werden geschreven wanneer de Web SDK lokaal werd uitgevoerd.

Bevat versie 2.23.0 van Adobe Experience Platform Web SDK.

## Versie 2.26.0 - 22 augustus 2024

**Nieuwe functies**

- Toegevoegde controlehaakgebeurtenis `triggered` .
- [ Geleide gebeurtenissen ](action-types.md#instance), [ verzoek standaardverpersoonlijking ](action-types.md#personalization), [ Abonneren heersersset punten ](event-types.md#subscribe-ruleset-items), en [ evalueert heersers ](action-types.md#evaluate-rulesets) zijn nu algemeen beschikbaar.

**Bevestigingen en verbeteringen**

- Probleem verholpen waarbij gedupliceerde variabele-gegevenselementen elkaar konden overschrijven.
- Wanneer het gebruiken van de [ standaardverpersoonlijking van het Verzoek ](action-types.md#personalization) geleide gebeurtenis, worden de visuele verpersoonlijkingsbesluiten nu automatisch toegelaten.

Bevat versie 2.2.2.0 van Adobe Experience Platform Web SDK.

## Versie 2.25.0 - vrijdag 18 juli 2024

**Nieuwe functies**

- Extra ondersteuning voor automatisch bijhouden van personalisatie in Adobe Journey Optimizer.
- Introduceerde nieuwe montages om verbeterde klikinzameling te beheren.

Bevat versie 2.21.1 van Adobe Experience Platform Web SDK.

## Versie 2.24.0 - donderdag 5 juni 2024

**Bevestigingen en verbeteringen**

- Oplossing voor een fout die optrad bij het wijzigen van de extensieconfiguratie toen config-overschrijvingen werden gedefinieerd.
- Lege waarden voor mediagroep mogen worden ingesteld met pingsintervallen.
- Oplossing voor een fout die optrad bij het wijzigen van een actie voor een updatevariabele.
- Herstellen van container voor id-synchronisatie toestaan in config-overschrijvingen.

Bevat versie 2.20.0 van Adobe Experience Platform Web SDK.

## Versie 2.23.1 - woensdag 28 mei 2024

**Nieuwe functies**

- Toegevoegde ondersteuning voor de component [`Streaming Media Collection`](web-sdk-extension-configuration.md#streaming-media) in de extensieconfiguratie.
- De handeling [`Send Media Event`](action-types.md#send-media-event) is toegevoegd voor de functie [!DNL Streaming Media Collection] .
- Het gegevenselement [`Media: Quality of Experience`](data-element-types.md#quality-experience) is toegevoegd voor de functie [!DNL Streaming Media Collection] .

Bevat versie 2.20.0 van Adobe Experience Platform Web SDK.

**Bevestigingen en verbeteringen**

- Vaste een fout die voorkwam wanneer het zoeken naar gegevenselementen in de [ veranderlijke ](action-types.md#update-variable) actie van de Update.
- [!UICONTROL Media] -gebeurtenistypen zijn verwijderd uit de gebeurtenistypen die worden voorgesteld voor gebruik in de `sendEvent` -handeling.

## Versie 2.22.0 - zaterdag 3 mei 2024

**Nieuwe functies**

- Breid veranderlijk gegevenselement uit om gegevensvoorwerpen te steunen.
- De actie voor het bijwerken van variabelen ondersteunt nu het wijzigen van doorloopgegevens van Adobe Analytics, Adobe Audience Manager en Adobe Target.

Bevat versie 2.19.2 van Adobe Experience Platform Web SDK.

## Versie 2.21.4 - donderdag 10 januari 2024

**Bevestigingen en verbeteringen**

- Oplossing van een probleem waarbij het opslaan van configuratieoverschrijvingen zonder alle drie omgevingen die waren ingesteld, de interface van de extensie zou vastlopen.
- Probleem verholpen waarbij het selectievakje voor het wissen van bestaande waarden niet werd ingevuld bij het bewerken van een actie voor een updatevariabele.

Bevat versie 2.19.2 van Adobe Experience Platform Web SDK.

## Versie 2.21.3 - zaterdag 10 november 2023

Bevat versie 2.19.1 van Adobe Experience Platform Web SDK.

**Bevestigingen en verbeteringen**

- Probleem verholpen waarbij de array proposities die beschikbaar was in `Send event complete` -gebeurtenissen altijd leeg was.

## Versie 2.21.2 - donderdag 1 november 2023

**Nieuwe functies**

- Optie `Request default personalization` toegevoegd om gebeurtenisactie te verzenden.
- Toegevoegde ondersteuning voor boven- en onderaan-pagina-gebeurtenissen in de verzendgebeurtenis.
- Toegevoegde handeling `Apply propositions` .
- Toegevoegde `Evaluate rulesets` actie en `Subscribe ruleset items` gebeurtenis voor in-app berichten.
- Toegevoegd `Decision context` om een gebeurtenisactie te verzenden.

**Bevestigingen en verbeteringen**

- Bevat versie 2.19.0 van Adobe Experience Platform Web SDK.

## Versie 2.20.3 - 8 augustus 2023

**Bevestigingen en verbeteringen**

- Gegevenselementen konden niet worden opgeslagen in het veld ID synchronisatiecontainer ID overschrijven. Dit probleem is nu opgelost.

## Versie 2.20.1 - 3 augustus 2023

**Bevestigingen en verbeteringen**

- Verbeterde validatie van opgeslagen gegevensstroomoverschrijvingsinstellingen.

## Versie 2.20.0 - dinsdag 31 juli 2023

**Nieuwe functies**

- Toegevoegde steun voor [ per-bevel treedt van datastream identiteitskaart ](../../../../datastreams/overrides.md) met voeten.

**Bevestigingen en verbeteringen**

- `edgeConfigId` vervangen door `datastreamId` in de SDK-configuratie.
- De veelvoudige verbeteringen van de gebruikerservaring voor de configuratie van de gegevensstroom treden gebruikersinterface met voeten.

## Versie 2.19.0 - donderdag 21 juni 2023

- De acties **[!UICONTROL Variable]** data element en **[!UICONTROL Update Variable]** zijn nu over het algemeen beschikbaar.

## Versie 2.18.0 - vrijdag 18 mei 2023

- Bevat versie 2.17.0 van Adobe Experience Platform Web SDK.

## Versie 2.17.0 - 25 april 2023

**Nieuwe functies**

- Bevat versie 2.16.0 van Adobe Experience Platform Web SDK.
- Toegevoegde steun voor [ datastream configuratie treedt met voeten ](/help/datastreams/overrides.md).
- Voeg een bericht over de vervangen toe aan de optie `datasetId` in de opdracht `sendEvent` .

**Bevestigingen en verbeteringen**

- Probleem verholpen waarbij schuiven in Safari de gegevensstroomkiezer zou sluiten.

## Versie 2.16.1 - 14 april 2023

- Probleem verholpen met XDM-object en variabele gegevenselementen waarbij u geen schema kon selecteren vanuit een niet-standaardsandbox.

## Versie 2.16.0 - 30 maart 2023

**Nieuwe functies**

- (Beta) Toegevoegde handeling **[!UICONTROL Update variable]** en gegevenselement **[!UICONTROL Variable]** .
- Toegevoegde configuratie voor de callback-functie [`onBeforeLinkClickSend`](/help/web-sdk/commands/configure/onbeforelinkclicksend.md) .

**Bevestigingen en verbeteringen**

- Probleem verholpen waarbij klikken op elementen binnen een ankertag niet werkte wanneer de handeling **[!UICONTROL Redirect with identity]** werd gebruikt.
- Probleem verholpen waarbij gegevenselementen van XDM-objectgegevens niet werkten als er slechts één schema aanwezig was.
- Bevat versie 2.15.0 van Adobe Experience Platform Web SDK.

## Versie 2.15.1 - vrijdag 26 januari 2023

- Probleem verholpen waarbij gebruikers zonder toegang tot gegevensstromen de extensieconfiguratie niet konden bewerken.
- Extra ondersteuning voor oppervlakken in de handeling `sendEvent` .

Bevat versie 2.14.0 van Adobe Experience Platform Web SDK.

## Versie 2.14.1 - vrijdag 13 oktober 2022

- Probleem verholpen waarbij de Web SDK de id van de Experience Cloud-id-service niet naleeft.

Bevat versie 2.13.1 van de Adobe Experience Platform Web SDK Library.

## Versie 2.14.0 - 28 september 2022

- Nieuwe configuratie `targetMigrationEnabled` toegevoegd waarmee de volledige migratie van pagina&#39;s mogelijk is.
- Er is een reactieactie toegevoegd en toegepast om hybride server-client implementaties in te schakelen.
- Optie voor hoge entropy user-agent client hints toegevoegd.

Bevat versie 2.13.0 van de Adobe Experience Platform Web SDK Library.

## Versie 2.13.0 - donderdag 29 juni 2022

- Oplossing voor de sorteervolgorde van numerieke eigenschappen in het gegevenselement XDM Object, zoals Vars.

Bevat versie 2.12.0 van de Adobe Experience Platform Web SDK Library.

## Versie 2.12.0 - dinsdag 13 juni 2022

- Het gegevenselement `identityMap` is bijgewerkt en vult de naamruimteopties op basis van de sandboxen die zijn gedefinieerd door de extensie-instellingen.
- Actie **[!UICONTROL Redirect with identity]** toegevoegd om delen van domeinidentiteit toe te staan.
- Toegevoegde documentatie verwijst naar de handeling `sendEvent` .
- Bijgewerkte gebruikersinterfacebibliotheek React Spectrum.
- Verbeteringen in de gebruikersinterface.

Bevat versie 2.11.0 van de Adobe Experience Platform Web SDK Library.

## Versie 2.11.2 - woensdag 3 mei 2022

Bevat versie 2.10.1 van de Adobe Experience Platform Web SDK Library.

## Versie 2.11.1 - 22 april 2022

- Opdrachtfout voor configureren van versie 2.11.0 is opgelost.

Bevat versie 2.10.0 van de Adobe Experience Platform Web SDK Library.

## Versie 2.11.0 - 22 april 2022

- Verbeterde prestaties van de gebruikersinterface voor tags.
- Sandboxkiezers toevoegen aan de extensieconfiguratie van gegevensstreams.

Bevat versie 2.10.0 van de Adobe Experience Platform Web SDK Library.

## Versie 2.10.0 - 10 maart 2022

- Werk het preHide fragment bij dat beschikbaar is om op de configuratiepagina te kopiëren om met de bijgewerkte redacteur van Adobe Target VEC te werken.

Bevat versie 2.9.0 van de Adobe Experience Platform Web SDK-bibliotheek.

## Versie 2.9.0 - donderdag 19 januari 2022

Bevat versie 2.8.0 van de Adobe Experience Platform Web SDK-bibliotheek.

## Versie 2.8.0 - woensdag 26 oktober 2021

Bevat versie 2.7.0 van de Adobe Experience Platform Web SDK-bibliotheek.

- Aanvullende informatie van de Edge Network is beschikbaar in de gebeurtenis Send Event Complete, inclusief `inferences` en `destinations` . Het formaat van deze eigenschappen kan veranderen aangezien deze eigenschappen momenteel als deel van een Beta uitrollen.

## Versie 2.7.3 - 7 september 2021

Bevat versie 2.6.4 van de Adobe Experience Platform Web SDK-bibliotheek.

- Er is niet langer een waarschuwing voor de afbreking van `container.buildInfo.environment.`

## Versie 2.7.0 - 16 augustus 2021

Bevat versie 2.6.3 van de Adobe Experience Platform Web SDK-bibliotheek.

- Wanneer u het gegevenstype Identity Map gebruikt, worden id&#39;s waarvan de id&#39;s worden omgezet in waarden die niet-gevulde tekenreeksen zijn, nu automatisch verwijderd uit de identiteitskaart.
- Oplossing voor een fout die zou optreden wanneer werd geprobeerd een gegevenselement op te slaan met het gegevenstype XDM Object en er was geen schema geselecteerd.
- Verbeterde typografie van de gebruikersinterface.

## Versie 2.6.2 - 4 augustus 2021

Bevat versie 2.6.2 van de Adobe Experience Platform Web SDK-bibliotheek.

## Versie 2.6.1 - juli 2021

Bevat versie 2.6.1 van de Adobe Experience Platform Web SDK-bibliotheek.

## Versie 2.6.0 - woensdag 27 juli 2021

Bevat versie 2.6.0 van de Adobe Experience Platform Web SDK-bibliotheek.

- De etiketten, de beschrijvingen, en de foutenmeldingen die de term &quot;randconfiguratie&quot;gebruiken zijn veranderd om de term &quot;datastream&quot;te gebruiken om zich aan de recentste terminologie van Adobe Experience Platform te richten.
- In de mening van de uitbreidingsconfiguratie, werd de steun toegevoegd voor de behandeling van grote aantallen gegevensstromen en gegevensstroommilieu&#39;s.
- In de het gegevenselementenmening van Objecten XDM, werd de steun toegevoegd voor de behandeling van grote aantallen schema&#39;s.
- Er is een gebeurtenistype Send Event Complete toegevoegd, dat kan worden gebruikt om een regel uit te voeren nadat een gebeurtenis naar de server is verzonden en een reactie is ontvangen. Meer documentatie is binnenkort beschikbaar.
- Het gebeurtenistype Besluiten ontvangen is vervangen. Gebruik in plaats hiervan het gebeurtenistype Send Event Complete.
- De gebruikersinterface en foutafhandeling zijn over het algemeen verbeterd.

## Versie 2.5.0 - woensdag 1 juni 2021

Bevat versie 2.5.0 van de Adobe Experience Platform Web SDK-bibliotheek.

- Een veld `data` toegevoegd aan de handeling Gebeurtenis verzenden. De komende documentatie zal beschrijven hoe dit in bepaalde scenario&#39;s kan worden gebruikt.
- In de gegevenselementweergave van het XDM-object is een probleem opgelost waarbij een fout is gegenereerd als de gebruiker toegang had tot Adobe Experience Platform-sandboxen, maar niet tot de sandbox die als standaard voor de organisatie is geconfigureerd.
- In de weergave van het gegevenselement XDM Object is een probleem opgelost waarbij een vereist schemaveld als ongeldig wordt beschouwd, zelfs als het bovenliggende object geen waarden bevat.

## Versie 2.4.0 - 9 maart 2021

Bevat versie 2.4.0 van de Adobe Experience Platform Web SDK-bibliotheek.

- Toegevoegd [ &quot;Document het ontladen&quot;](/help/web-sdk/commands/sendevent/documentunloading.md) checkbox om de actie UI van de Gebeurtenis te verzenden.
- Toegevoegde steun voor een `out` optie wanneer [ vormend standaardtoestemming ](/help/web-sdk/commands/configure/defaultconsent.md) die alle gebeurtenissen laat vallen tot de toestemming wordt ontvangen (de bestaande `pending` optie maakt gebeurtenissen een rij en verzendt hen zodra de toestemming wordt ontvangen).
- Knopinfo is toegevoegd aan het veld Standaardtoestemming.
- Toegevoegde ondersteuning voor de standaard Goedkeuring 2.0 van Adobe bij gebruik van de opdracht [`setConsent`](/help/web-sdk/commands/setconsent.md) .
- Er wordt nu een betere fout weergegeven in de gebruikersinterface van het XDM Object-gegevenselement als het toegangstoken van de gebruiker ongeldig is of niet correct is ingericht.
- Probleem verholpen waarbij een kruisoorsprongfout (die geen invloed heeft op de werking van de extensie) is verholpen die tijdens het weergeven van een XDM Object-gegevenselement in de browserontwikkelingsconsole werd weergegeven.

## Versie 2.3.0 - donderdag 4 november 2020

Bevat versie 2.3.0 van de Adobe Experience Platform Web SDK-bibliotheek.

- Toegevoegde steun voor het gebruiken van een gegevenselement wanneer het vormen van standaardtoestemming.
- Toegevoegde mogelijkheid om te zoeken naar XDM-schema&#39;s met het gegevenstype XDM Object.
- Het toegevoegde klonen van XDM gegevens binnen het Send actietype van de Gebeurtenis om ervoor te zorgen dat om het even welke verdere veranderingen in het XDM gegevensvoorwerp niet in het verzoek zullen worden weerspiegeld.

## Versie 2.2.0 - vrijdag 1 oktober 2020

- Wanneer klanten probeerden om een voorwerp XDM van zandbakschema&#39;s tot stand te brengen, kwamen zij in authentificatiekwesties in werking. De API die Platform roept is zich nu bewust van milieu&#39;s zodat worden de gebruikers slechts voorgesteld van die schema&#39;s die zij toegang hebben om uit te geven.
- Wanneer u het gegevenselement `identityMap` gebruikt, worden de naamruimten nu vooraf ingevuld in een vervolgkeuzelijst, zodat u deze niet handmatig hoeft in te vullen.
- De interface voor het gegevenselement `xdmObject` is vernieuwd. In de nieuwe UI, kunt u zien welke gebieden zijn bevolkt zonder het moeten elk punt in het voorwerp ingaan.

## Versie 2.1.1 - 26 augustus 2020

- Hiermee wordt een probleem verholpen waarbij Adobe Experience Platform-sandboxen in de weergave XDM-object onjuist worden weergegeven. Als bij het gebruik van deze versie van de extensie een verwachte sandbox niet in de lijst wordt weergegeven, moet de gebruiker bij de Adobe Experience Platform-beheerder controleren of de toegangsrechten correct zijn ingesteld.

## Versie 2.1.0 - 5 augustus 2020

- Doorlopende wijziging: verwijder de handeling `syncIdentity` en geef in plaats daarvan ondersteuning voor het doorgeven van deze id&#39;s in de handeling `sendEvent` . Schakel bestaande regels met deze handeling uit voordat u de extensie upgradet.
- Update aan Alloy v. 2.1.0 ([ de Nota&#39;s van de Versie ](/help/web-sdk/release-notes.md))
- Ondersteuning voor IAB 2.0 Consent Standard in de handeling `setConsent` .
- Ondersteuning voor het overschrijven van de gegevensset-id in de handeling `sendEvent` .
- Voeg een nieuw gegevenselement van het type `IdentityMap` toe dat kan worden gebruikt om de `identityMap` -vermelding te vullen in het XDM Object Data Element dat nu is ingeschakeld, en in de `setConsent` -actie.
- Ondersteuning voor het doorgeven van een identiteitsoverzicht in de handeling `setConsent` .
- Ondersteuning voor het kiezen van een platformsandbox in het XDM Object Data Element.

## Versie 1.0.0 - woensdag 26 mei 2020

- Steun die het milieu van de Dienst van de Configuratie selecteert.

## Versie 0.1.2 - dinsdag 4 mei 2020

- Naam gewijzigd in `configId` in `edgeConfigId` .
- Naam gewijzigd `viewStart` in `renderDecisions` , standaard ingesteld op false. Indien ingesteld op true, worden Personalization-aanbiedingen opgehaald en automatisch weergegeven.
- Wijzigingen met betrekking tot `Get Decisions`:
   - De opdracht `getDecisions` is verwijderd.
   - Een optie `scopes` toegevoegd aan de opdracht `sendEvent` . Besluiten worden geretourneerd in de promise van `sendEvent` .
   - Er is een ingebouwd `__view__` bereik toegevoegd dat zal resulteren in het retourneren van aanbiedingen voor het weergeven van pagina&#39;s in het algemeen. (VEC-aanbiedingen in Target bijvoorbeeld.)
Deze beslissingen worden alleen van de opdracht `sendEvent` geretourneerd als `renderDecisions` is ingesteld op false.
   - Er is een `Decisions Received` -gebeurtenis toegevoegd die wordt geactiveerd wanneer beslissingen beschikbaar komen.
- Meerdere Personalization-berichten zijn gecombineerd onder één serveraanroep.
- Probleem opgelost in de samenvoegings-id voor gebeurtenissen waarbij het element telkens opnieuw werd ingesteld toen naar het gegevenselement werd verwezen.
- De naam van de handeling `setCustomerIds` is gewijzigd in `syncIdentity` .
- Een opdracht `getIdentity` toegevoegd. Dit kan alleen voorlopig worden verbruikt via aangepaste code.
- Als u foutopsporing inschakelt met `_satellite` , wordt foutopsporing nu ingeschakeld in de Adobe Experience Platform Web SDK.
- Toegevoegde ondersteuning voor getypte waarden in het XDM-object: Booleaanse waarden, getallen en decimalen.

## Versie 0.0.10 - 16 maart 2020

- Combineer de concepten Inschakelen en Uitschakelen onder `Consent` en voeg een nieuwe opdracht `setConsent` toe.
- Er is een nieuw gegevenselement van het type `XDM Object` toegevoegd waarmee toewijzingen van JavaScript/JSON naar XDM zijn toegestaan.

## Versie 0.0.7 - 18 februari 2020

- Verwijderd idSyncContainerId, datasetId, schemaId, urlDestinationEnabled en cookieDesturesEnabled opties
- Toegevoegde ondersteuning voor afbreekstreepjes in waarde van optie edgeDomain
- Verzoek die tijdens de migratie van identiteitskaart wordt gemaakt wordt verzonden naar demdex eindpunt om dwars-domeinidentificatie te verbeteren wanneer de demdex koekje niet wordt geplaatst
- Aanvraag die tijdens de migratie van id&#39;s is gemaakt, verwacht altijd een reactie om ervoor te zorgen dat het identiteitscookie wordt ingesteld
- Wanneer het uitvoeren van een ongeldig bevel, zal een lijst van geldige bevelnamen in de console worden geregistreerd
- Selectievakje toegevoegd om cookie-ondersteuning van derden in- en uit te schakelen voor de tagextensie. Hiermee worden oproepen naar demdex.net uitgeschakeld

## Versie 0.0.5 - zaterdag 20 december 2019

- Activiteitenbeheer toevoegen aan tagextensie
- EventType en EventMergeId beschikbaar maken voor de opdracht event
- OnBeforeEventSend config toevoegen aan tagextensie
- EdgeBasePath-config toevoegen aan tagextensie

## Versie 0.0.3 - dinsdag 25 november 2019

- De nieuwe gebieden van de Fusie ID en van het Type op de Send actie van de Gebeurtenis. De kaart van identiteitskaart van de fusie aan `xdm.eventMergeID` in het XDM- schema en het Type wijst aan `xdm.eventType` in het XDM- schema toe.

## Versie 0.0.2 - dinsdag 18 november 2019

- Eerste release

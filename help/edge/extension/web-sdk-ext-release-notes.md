---
title: Opmerkingen bij de release Adobe Experience Platform Web SDK
description: Adobe Experience Platform Web SDK-tagextensie
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 0%

---

# Opmerkingen bij de release Adobe Experience Platform Web SDK

In dit document worden de releaseopmerkingen voor de tagextensie Adobe Experience Platform Web SDK besproken. Voor de recentste versienota&#39;s op SDK zelf, zie [de versienota&#39;s van SDK van het Web van het Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html).

## Versie 2.6.0 - 27 juli 2021

* De etiketten, de beschrijvingen, en de foutenmeldingen die de term &quot;randconfiguratie&quot;gebruiken zijn veranderd om de term &quot;datastream&quot;te gebruiken om zich aan de recentste terminologie van Adobe Experience Platform te richten.
* In de mening van de uitbreidingsconfiguratie, werd de steun toegevoegd voor de behandeling van grote aantallen gegevensstromen en gegevensstroommilieu&#39;s.
* In de het gegevenselementenmening van Objecten XDM, werd de steun toegevoegd voor de behandeling van grote aantallen schema&#39;s.
* Er is een gebeurtenistype Send Event Complete toegevoegd, dat kan worden gebruikt om een regel uit te voeren nadat een gebeurtenis naar de server is verzonden en een reactie is ontvangen. Meer documentatie is binnenkort beschikbaar.
* Het gebeurtenistype Besluiten ontvangen is afgekeurd. Gebruik in plaats hiervan het gebeurtenistype Send Event Complete.
* De gebruikersinterface en foutafhandeling zijn over het algemeen verbeterd.

## Versie 2.5.0 - 1 juni 2021

Bevat versie 2.5.0 van de bibliotheek van SDK van het Web van Adobe Experience Platform.

* Een veld `data` toegevoegd aan de handeling Gebeurtenis verzenden. De komende documentatie zal beschrijven hoe dit in bepaalde scenario&#39;s kan worden gebruikt.
* In de gegevenselementweergave van het XDM-object is een probleem opgelost waarbij een fout is gegenereerd als de gebruiker toegang had tot Adobe Experience Platform-sandboxen maar niet tot de sandbox die als standaard voor de organisatie is geconfigureerd.
* In de weergave van het gegevenselement XDM Object is een probleem opgelost waarbij een vereist schemaveld als ongeldig wordt beschouwd, zelfs als het bovenliggende object geen waarden bevat.

## Versie 2.4.0 - 9 maart 2021

Bevat versie 2.4.0 van de bibliotheek van SDK van het Web van Adobe Experience Platform.

* [&quot;document unloading&quot;](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) checkbox toegevoegd om de actie UI van de Gebeurtenis te verzenden.
* Toegevoegde steun voor een `out` optie wanneer [vormend standaardtoestemming](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent) die alle gebeurtenissen laat vallen tot de toestemming wordt ontvangen (de bestaande `pending` optie vormt gebeurtenissen en verzendt hen zodra de toestemming wordt ontvangen).
* Knopinfo is toegevoegd aan het veld Standaardtoestemming.
* Toegevoegde steun [Adobe verzonden 2.0 norm](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* Er wordt nu een betere fout weergegeven in de gebruikersinterface van het XDM Object-gegevenselement als het toegangstoken van de gebruiker ongeldig is of niet correct is ingericht.
* Probleem verholpen waarbij een kruisoorsprongfout (die geen invloed heeft op de werking van de extensie) is verholpen die tijdens het weergeven van een XDM Object-gegevenselement in de browserontwikkelingsconsole werd weergegeven.

## Versie 2.3.0 - 4 november 2020

Bevat versie 2.3.0 van de bibliotheek van SDK van het Web van Adobe Experience Platform.

* Toegevoegde steun voor het gebruiken van een gegevenselement wanneer het vormen van standaardtoestemming.
* Toegevoegde mogelijkheid om te zoeken naar XDM-schema&#39;s met het gegevenstype XDM Object.
* Het toegevoegde klonen van XDM gegevens binnen het Send actietype van de Gebeurtenis om ervoor te zorgen dat om het even welke verdere veranderingen in het XDM gegevensvoorwerp niet in het verzoek zullen worden weerspiegeld.

## Versie 2.2.0 - 1 oktober 2020

* Wanneer klanten probeerden om een voorwerp XDM van zandbakschema&#39;s tot stand te brengen, kwamen zij in authentificatiekwesties in werking. API die Platform roept is zich nu bewust van milieu&#39;s zodat worden de gebruikers slechts voorgesteld van die schema&#39;s die zij toegang hebben om uit te geven.
* Wanneer u het gegevenselement `identityMap` gebruikt, worden de naamruimten nu vooraf ingevuld in een vervolgkeuzelijst, zodat u deze niet handmatig hoeft in te vullen.
* De interface voor het gegevenselement `xdmObject` is vernieuwd. In de nieuwe UI, kunt u zien welke gebieden zijn bevolkt zonder het moeten elk punt in het voorwerp ingaan.

## Versie 2.1.1 - 26 augustus 2020

* Hiermee wordt een probleem verholpen waarbij Adobe Experience Platform-sandboxen in de weergave XDM-object onjuist worden weergegeven. Als bij het gebruik van deze versie van de extensie een verwachte sandbox niet in de lijst wordt weergegeven, moet de gebruiker bij de Adobe Experience Platform-beheerder controleren of de toegangsrechten correct zijn ingesteld.

## Versie 2.1.0 - 5 augustus 2020

* Wijziging van regeleinde: Verwijder de `syncIdentity` actie en steun die IDs in de `sendEvent` actie in plaats daarvan overgaan. Schakel bestaande regels met deze handeling uit voordat u de extensie upgradet.
* Bijwerken naar versie 2.1.0 ([Opmerkingen bij de release](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html))
* Ondersteuning voor IAB 2.0 Consent Standard in de handeling `setConsent`.
* Ondersteuning voor het overschrijven van de gegevensset-id in de handeling `sendEvent`.
* Voeg een nieuw gegevenselement van type `IdentityMap` toe dat kan worden gebruikt om de `identityMap` ingang in het Element van de Gegevens van Objecten te bevolken XDM dat nu wordt toegelaten, en in `setConsent` actie.
* Ondersteuning voor het doorgeven van een identiteitsoverzicht in de handeling `setConsent`.
* Ondersteuning voor het kiezen van een Platform-sandbox in het XDM Object Data Element.

## Versie 1.0.0 - 26 mei 2020

* Steun die het milieu van de Dienst van de Configuratie selecteert.

## Versie 0.1.2 - 4 mei 2020

* Naam gewijzigd in `configId` in `edgeConfigId`.
* Naam gewijzigd in `viewStart` in `renderDecisions`, standaard ingesteld op false. Indien ingesteld op true, worden aanbiedingen voor personalisatie opgehaald en automatisch weergegeven.
* Wijzigingen met betrekking tot `Get Decisions`:
   * De opdracht `getDecisions` is verwijderd.
   * Optie `scopes` toegevoegd aan de opdracht `sendEvent`. Besluiten worden geretourneerd in de opgeloste belofte `sendEvent`.
   * Er is een ingebouwd `__view__` bereik toegevoegd dat zal resulteren in het retourneren van aanbiedingen voor de pagina/weergave in het algemeen. (VEC-aanbiedingen in Target bijvoorbeeld.)
Die besluiten keren van `sendEvent` bevel terug slechts als `renderDecisions` aan vals wordt geplaatst.
   * Er is een gebeurtenis `Decisions Received` toegevoegd die wordt geactiveerd wanneer beslissingen beschikbaar komen.
* Gecombineerde veelvoudige berichten van de Personalisatie onder één enkele servervraag.
* Probleem opgelost in de samenvoegings-id voor gebeurtenissen waarbij het element telkens opnieuw werd ingesteld toen naar het gegevenselement werd verwezen.
* De naam van de handeling `setCustomerIds` is gewijzigd in `syncIdentity`.
* Een opdracht `getIdentity` toegevoegd. Dit kan alleen voorlopig worden verbruikt via aangepaste code.
* Als u foutopsporing inschakelt met `_satellite`, wordt foutopsporing nu ingeschakeld in de SDK van het Adobe Experience Platform-web.
* Toegevoegde ondersteuning voor getypte waarden in het XDM-object: Booleaanse cijfers, getallen en decimalen.

## Versie 0.0.10 - 16 maart 2020

* Gecombineerd de concepten Opt-In &amp; Opt-Out onder `Consent`, en voegde een nieuw `setConsent` bevel toe.
* Er is een nieuw gegevenselement van het type `XDM Object` toegevoegd dat toewijzing van JavaScript/JSON aan XDM toestaat.

## Versie 0.0.7 - 18 februari 2020

* Verwijderd idSyncContainerId, datasetId, schemaId, urlDestinationEnabled en cookieDesturesEnabled opties
* Toegevoegde ondersteuning voor afbreekstreepjes in de waarde van de optie edgeDomain
* Verzoek die tijdens de migratie van identiteitskaart wordt gemaakt wordt verzonden naar demdex eindpunt om dwars-domeinidentificatie te verbeteren wanneer de demdex koekje niet wordt geplaatst
* Aanvraag die tijdens de migratie van id&#39;s is gemaakt, verwacht altijd een reactie om ervoor te zorgen dat het identiteitscookie wordt ingesteld
* Wanneer het uitvoeren van een ongeldig bevel, zal een lijst van geldige bevelnamen in de console worden geregistreerd
* Selectievakje toegevoegd om cookie-ondersteuning van derden in- en uit te schakelen voor de tagextensie. Dit maakt vraag aan demdex.net onbruikbaar

## Versie 0.0.5 - 20 december 2019

* Activiteitenbeheer toevoegen vormt een tag-extensie
* EventType en EventMergeId beschikbaar maken voor de opdracht event
* OnBeforeEventSend config toevoegen aan tagextensie
* EdgeBasePath-config toevoegen aan tagextensie

## Versie 0.0.3 - 25 november 2019

* De nieuwe gebieden van de Fusie ID en van het Type op de Send actie van de Gebeurtenis. Identiteitskaart van de fusie brengt aan `xdm.eventMergeID` in het XDM schema en het Type brengt aan `xdm.eventType` in het XDM schema in kaart.

## Versie 0.0.2 - 18 november 2019

* Eerste release

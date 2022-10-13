---
title: Opmerkingen bij de release Adobe Experience Platform Web SDK
description: Adobe Experience Platform Web SDK-tagextensie
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: f406ad74da00a7f4bf7ef1b52bee59cd91435d8f
workflow-type: tm+mt
source-wordcount: '1493'
ht-degree: 0%

---


# Opmerkingen bij de release Adobe Experience Platform Web SDK

In dit document worden de releaseopmerkingen voor de tagextensie Adobe Experience Platform Web SDK besproken. Voor de meest recente releaseopmerkingen over de SDK zelf raadpleegt u de [Opmerkingen bij de release van Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html).

## Versie 2.14.1 - 13 oktober 2022

* Probleem verholpen waarbij de web SDK de id van de Experience Cloud ID-service niet respecteert.

Bevat versie 2.13.1 van de Adobe Experience Platform Web SDK Library.

## Versie 2.14.0 - 28 september 2022

* Nieuw toegevoegd `targetMigrationEnabled` configuratie die de volledige migratie van pagina naar pagina mogelijk maakt.
* Er is een reactieactie toegevoegd en toegepast om hybride server-client implementaties in te schakelen.
* Optie voor hoge entropy user-agent client hints toegevoegd.

Bevat versie 2.13.0 van de Adobe Experience Platform Web SDK Library.

## Versie 2.13.0 - 29 juni 2022

* Oplossing voor de sorteervolgorde van numerieke eigenschappen in het gegevenselement XDM Object, zoals Vars.

Bevat versie 2.12.0 van de SDK-bibliotheek van Adobe Experience Platform Web.

## Versie 2.12.0 - 13 juni 2022

* De `identityMap` data element to populate the namespace options based on the sandboxes defined by the extension settings.
* Toegevoegd **[!UICONTROL Redirect with identity]** actie voor het delen van domeinidentiteit.
* Documentatiekoppelingen toegevoegd aan de `sendEvent` handeling.
* Bijgewerkte gebruikersinterfacebibliotheek React Spectrum.
* Verbeteringen in de gebruikersinterface.

Bevat versie 2.11.0 van de Adobe Experience Platform Web SDK Library.

## Versie 2.11.2 - 3 mei 2022

Bevat versie 2.10.1 van de Adobe Experience Platform Web SDK Library.

## Versie 2.11.1 - 22 april 2022

* Opdrachtfout voor configureren van versie 2.11.0 is opgelost.

Bevat versie 2.10.0 van de Adobe Experience Platform Web SDK Library.

## Versie 2.11.0 - 22 april 2022

* Verbeterde prestaties van de gebruikersinterface voor tags.
* Sandboxkiezers toevoegen aan de extensieconfiguratie van gegevensstreams.

Bevat versie 2.10.0 van de Adobe Experience Platform Web SDK Library.

## Versie 2.10.0 - 10 maart 2022

* Werk het preHide fragment bij dat beschikbaar is om op de configuratiepagina te kopiëren om met de bijgewerkte redacteur van Adobe Target VEC te werken.

Bevat versie 2.9.0 van de bibliotheek van SDK van het Web van Adobe Experience Platform.

## Versie 2.9.0 - 19 januari 2022

Bevat versie 2.8.0 van de bibliotheek van SDK van het Web van Adobe Experience Platform.

## Versie 2.8.0 - 26 oktober 2021

Bevat versie 2.7.0 van de bibliotheek van SDK van het Web van Adobe Experience Platform.

* Aanvullende informatie van Experience Edge is beschikbaar in de gebeurtenis Send Event Complete, waaronder `inferences` en `destinations`. Het formaat van deze eigenschappen kan veranderen aangezien deze eigenschappen momenteel als deel van een Bèta rollen. Zie voor meer informatie [Gebeurtenissen bijhouden.](../fundamentals/tracking-events.md)

## Versie 2.7.3 - 7 september 2021

Bevat versie 2.6.4 van de SDK-bibliotheek van Adobe Experience Platform Web.

* Er is niet langer een afgekeurde waarschuwing voor `container.buildInfo.environment.`

## Versie 2.7.0 - 16 augustus 2021

Bevat versie 2.6.3 van de bibliotheek van SDK van het Web van Adobe Experience Platform.

* Wanneer u het gegevenstype Identity Map gebruikt, worden id&#39;s waarvan de id&#39;s worden omgezet in waarden die niet-gevulde tekenreeksen zijn, nu automatisch verwijderd uit de identiteitskaart.
* Oplossing voor een fout die zou optreden wanneer werd geprobeerd een gegevenselement op te slaan met het gegevenstype XDM Object en er was geen schema geselecteerd.
* Verbeterde typografie van de gebruikersinterface.

## Versie 2.6.2 - 4 augustus 2021

Bevat versie 2.6.2 van de bibliotheek van SDK van het Web van Adobe Experience Platform.

## Versie 2.6.1 - juli 2021

Bevat versie 2.6.1 van de bibliotheek van SDK van het Web van Adobe Experience Platform.

## Versie 2.6.0 - 27 juli 2021

Bevat versie 2.6.0 van de bibliotheek van SDK van het Web van Adobe Experience Platform.

* De etiketten, de beschrijvingen, en de foutenmeldingen die de term &quot;randconfiguratie&quot;gebruiken zijn veranderd om de term &quot;datastream&quot;te gebruiken om zich aan de recentste terminologie van Adobe Experience Platform te richten.
* In de mening van de uitbreidingsconfiguratie, werd de steun toegevoegd voor de behandeling van grote aantallen gegevensstromen en gegevensstroommilieu&#39;s.
* In de het gegevenselementenmening van Objecten XDM, werd de steun toegevoegd voor de behandeling van grote aantallen schema&#39;s.
* Er is een gebeurtenistype Send Event Complete toegevoegd, dat kan worden gebruikt om een regel uit te voeren nadat een gebeurtenis naar de server is verzonden en een reactie is ontvangen. Meer documentatie is binnenkort beschikbaar.
* Het gebeurtenistype Besluiten ontvangen is afgekeurd. Gebruik in plaats hiervan het gebeurtenistype Send Event Complete.
* De gebruikersinterface en foutafhandeling zijn over het algemeen verbeterd.

## Versie 2.5.0 - 1 juni 2021

Bevat versie 2.5.0 van de bibliotheek van SDK van het Web van Adobe Experience Platform.

* Toegevoegde `data` veld naar de handeling Verzendgebeurtenis. De komende documentatie zal beschrijven hoe dit in bepaalde scenario&#39;s kan worden gebruikt.
* In de gegevenselementweergave van het XDM-object is een probleem opgelost waarbij een fout is gegenereerd als de gebruiker toegang had tot Adobe Experience Platform-sandboxen, maar niet tot de sandbox die als standaard voor de organisatie is geconfigureerd.
* In de weergave van het gegevenselement XDM Object is een probleem opgelost waarbij een vereist schemaveld als ongeldig wordt beschouwd, zelfs als het bovenliggende object geen waarden bevat.

## Versie 2.4.0 - 9 maart 2021

Bevat versie 2.4.0 van de bibliotheek van SDK van het Web van Adobe Experience Platform.

* Toegevoegd [&quot;document wordt verwijderd&quot;](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) Schakel het selectievakje Send Event action UI in.
* Extra ondersteuning voor een `out` optie wanneer [standaardgoedkeuring configureren](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent) die alle gebeurtenissen stopzet totdat toestemming is ontvangen (de bestaande `pending` de optie vormt gebeurtenissen een rij en verzendt hen zodra de toestemming wordt ontvangen).
* Knopinfo is toegevoegd aan het veld Standaardtoestemming.
* Extra ondersteuning voor [Adobe 2](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* Er wordt nu een betere fout weergegeven in de gebruikersinterface van het XDM Object-gegevenselement als het toegangstoken van de gebruiker ongeldig is of niet correct is ingericht.
* Probleem verholpen waarbij een kruisoorsprongfout (die geen invloed heeft op de werking van de extensie) is verholpen die tijdens het weergeven van een XDM Object-gegevenselement in de browserontwikkelingsconsole werd weergegeven.

## Versie 2.3.0 - 4 november 2020

Bevat versie 2.3.0 van de bibliotheek van SDK van het Web van Adobe Experience Platform.

* Toegevoegde steun voor het gebruiken van een gegevenselement wanneer het vormen van standaardtoestemming.
* Toegevoegde mogelijkheid om te zoeken naar XDM-schema&#39;s met het gegevenstype XDM Object.
* Het toegevoegde klonen van XDM gegevens binnen het Send actietype van de Gebeurtenis om ervoor te zorgen dat om het even welke verdere veranderingen in het XDM gegevensvoorwerp niet in het verzoek zullen worden weerspiegeld.

## Versie 2.2.0 - 1 oktober 2020

* Wanneer klanten probeerden om een voorwerp XDM van zandbakschema&#39;s tot stand te brengen, kwamen zij in authentificatiekwesties in werking. API die Platform roept is zich nu bewust van milieu&#39;s zodat worden de gebruikers slechts voorgesteld van die schema&#39;s die zij toegang hebben om uit te geven.
* Wanneer u de `identityMap` data element, de namespaces is nu vooraf bevolkt in een dropdown zodat moet u dit niet manueel invullen.
* De interface voor de `xdmObject` gegevenselement. In de nieuwe UI, kunt u zien welke gebieden zijn bevolkt zonder het moeten elk punt in het voorwerp ingaan.

## Versie 2.1.1 - 26 augustus 2020

* Hiermee wordt een probleem verholpen waarbij Adobe Experience Platform-sandboxen in de weergave XDM-object onjuist worden weergegeven. Als bij het gebruik van deze versie van de extensie een verwachte sandbox niet in de lijst wordt weergegeven, moet de gebruiker bij de Adobe Experience Platform-beheerder controleren of de toegangsrechten correct zijn ingesteld.

## Versie 2.1.0 - 5 augustus 2020

* Wijziging van regeleinde: Verwijder de `syncIdentity` actie en ondersteuning voor het doorgeven van die id&#39;s in de `sendEvent` in plaats daarvan. Schakel bestaande regels met deze handeling uit voordat u de extensie upgradet.
* Bijwerken naar versie 2.1.0 ([Opmerkingen bij de release](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html))
* Ondersteuning voor IAB 2.0 Conceptstandaard in het dialoogvenster `setConsent` handeling.
* Ondersteuning voor het overschrijven van de id van de gegevensset in het dialoogvenster `sendEvent` handeling.
* Een nieuw gegevenselement van het type toevoegen `IdentityMap` die kunnen worden gebruikt om de `identityMap` -item in het XDM Object Data Element dat nu is ingeschakeld, en in het dialoogvenster `setConsent` handeling.
* Ondersteuning voor het doorgeven van een identiteitsoverzicht in het dialoogvenster `setConsent` handeling.
* Ondersteuning voor het kiezen van een Platform-sandbox in het XDM Object Data Element.

## Versie 1.0.0 - 26 mei 2020

* Steun die het milieu van de Dienst van de Configuratie selecteert.

## Versie 0.1.2 - 4 mei 2020

* Naam gewijzigd `configId` tot `edgeConfigId`.
* Naam gewijzigd `viewStart` tot `renderDecisions`, standaard ingesteld op false. Indien ingesteld op true, worden aanbiedingen voor personalisatie opgehaald en automatisch weergegeven.
* Wijzigingen in verband met `Get Decisions`:
   * De `getDecisions` gebruiken.
   * Toegevoegde `scopes` aan de `sendEvent` gebruiken. Besluiten worden geretourneerd in het `sendEvent` opgelost.
   * Ingebouwd `__view__` bereik dat leidt tot het retourneren van aanbiedingen voor de hele pagina/weergave. (VEC-aanbiedingen in Target bijvoorbeeld.)
Deze besluiten komen terug van de `sendEvent` alleen gebruiken als `renderDecisions` is ingesteld op false.
   * Toegevoegde `Decisions Received` gebeurtenis die wordt geactiveerd wanneer beslissingen beschikbaar komen.
* Gecombineerde veelvoudige berichten van de Personalisatie onder één enkele servervraag.
* Probleem opgelost in de samenvoegings-id voor gebeurtenissen waarbij het element telkens opnieuw werd ingesteld toen naar het gegevenselement werd verwezen.
* De naam van de `setCustomerIds` actie naar `syncIdentity`.
* Toegevoegde `getIdentity` gebruiken. Dit kan alleen voorlopig worden verbruikt via aangepaste code.
* Foutopsporing inschakelen met `_satellite` schakelt nu foutopsporing in de SDK van Adobe Experience Platform Web in.
* Toegevoegde ondersteuning voor getypte waarden in het XDM-object: Booleaanse cijfers, getallen en decimalen.

## Versie 0.0.10 - 16 maart 2020

* De concepten Opt-In en Opt-Out in combinatie `Consent`en voegt een nieuwe `setConsent` gebruiken.
* Nieuw gegevenselement van type toegevoegd `XDM Object` Hiermee kunt u JavaScript/JSON toewijzen aan XDM.

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

* De nieuwe gebieden van de Fusie ID en van het Type op de Send actie van de Gebeurtenis. Id-maps samenvoegen tot `xdm.eventMergeID` in het XDM-schema en -type worden toegewezen aan `xdm.eventType` in het XDM-schema.

## Versie 0.0.2 - 18 november 2019

* Eerste release

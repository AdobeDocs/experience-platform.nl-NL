---
title: Opmerkingen bij de release Adobe Experience Platform Web SDK
description: Adobe Experience Platform Web SDK Extension in Adobe Experience Platform Launch
seo-description: Adobe Experience Platform Web SDK Extension in Adobe Experience Platform Launch
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 1%

---


# Opmerkingen bij de release Adobe Experience Platform Web SDK

Dit document behandelt de releaseopmerkingen voor de Adobe Experience Platform Web SDK-extensie voor Adobe Experience Platform Launch. Voor de recentste versienota&#39;s op SDK zelf, zie [de versienota&#39;s van SDK van het Web van het Platform](https://docs.adobe.com/content/help/en/experience-platform/edge/release-notes.html).

## 4 november 2020

### Adobe Experience Platform Web SDK 2.3.0

Bevat versie 2.3.0 van de bibliotheek van SDK van het Web van Adobe Experience Platform.

#### Functies

* Toegevoegde steun voor het gebruiken van een gegevenselement wanneer het vormen van standaardtoestemming.
* Toegevoegde mogelijkheid om te zoeken naar XDM-schema&#39;s met het gegevenstype XDM Object.
* Het toegevoegde klonen van XDM gegevens binnen het Send actietype van de Gebeurtenis om ervoor te zorgen dat om het even welke verdere veranderingen in het XDM gegevensvoorwerp niet in het verzoek zullen worden weerspiegeld.

## 1 oktober 2020

### Adobe Experience Platform Web SDK 2.2.0

#### Opgeloste problemen

* Wanneer klanten probeerden om een voorwerp XDM van zandbakschema&#39;s tot stand te brengen, kwamen zij in authentificatiekwesties in werking. De API die AEP aanroept, is nu op de hoogte van omgevingen, zodat gebruikers alleen de schema&#39;s krijgen die ze kunnen bewerken.

#### Functies

* Wanneer u het gegevenselement `identityMap` gebruikt, worden de naamruimten nu vooraf ingevuld in een vervolgkeuzelijst, zodat u deze niet handmatig hoeft in te vullen.
* De interface voor het gegevenselement `xdmObject` is vernieuwd. In de nieuwe UI, kunt u zien welke gebieden zijn bevolkt zonder het moeten elk punt in het voorwerp ingaan.


## 26 augustus 2020

### Adobe Experience Platform Web SDK 2.1.1

#### Functies

* Hiermee wordt een probleem verholpen waarbij Adobe Experience Platform-sandboxen in de weergave XDM-object onjuist worden weergegeven. Als bij het gebruik van deze versie van de extensie een verwachte sandbox niet in de lijst wordt weergegeven, moet de gebruiker bij de Adobe Experience Platform-beheerder controleren of de toegangsrechten correct zijn ingesteld.


## 5 augustus 2020

### Adobe Experience Platform Web SDK 2.1.0

#### Functies

* Wijziging van regeleinde: Verwijder de `syncIdentity` actie en steun die IDs in de `sendEvent` actie in plaats daarvan overgaan. Schakel bestaande regels met deze handeling uit voordat u de extensie upgradet.
* Bijwerken naar versie 2.1.0 ([Opmerkingen bij de release](https://docs.adobe.com/content/help/en/experience-platform/edge/release-notes.html))
* Ondersteuning voor IAB 2.0 Consent Standard in de handeling `setConsent`.
* Ondersteuning voor het overschrijven van de gegevensset-id in de handeling `sendEvent`.
* Voeg een nieuw gegevenselement van type `IdentityMap` toe dat kan worden gebruikt om de `identityMap` ingang in het Element van de Gegevens van Objecten te bevolken XDM dat nu wordt toegelaten, en in `setConsent` actie.
* Ondersteuning voor het doorgeven van een identiteitsoverzicht in de handeling `setConsent`.
* Ondersteuning voor het kiezen van een AEP-sandbox in het XDM Object Data Element.


## 26 mei 2020

### Adobe Experience Platform Web SDK 1.0.0

#### Functies

* Steun die het milieu van de Dienst van de Configuratie selecteert.


## 4 mei 2020

### Adobe Experience Platform Web SDK 0.1.2

#### Functies

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
* Als u foutopsporing inschakelt met `_satellite`, wordt foutopsporing nu ingeschakeld in de AEP Web SDK.
* Toegevoegde ondersteuning voor getypte waarden in het XDM-object: Booleaanse cijfers, getallen en decimalen.

## 16 maart 2020

### Adobe Experience Platform Web SDK 0.0.10

#### Functies

* Gecombineerd de concepten Opt-In &amp; Opt-Out onder `Consent`, en voegde een nieuw `setConsent` bevel toe.
* Er is een nieuw gegevenselement van het type `XDM Object` toegevoegd dat toewijzing van JavaScript/JSON aan XDM toestaat.

## 18 februari 2020

### Adobe Experience Platform Web SDK 0.0.7

#### Functies

* Verwijderd idSyncContainerId, datasetId, schemaId, urlDestinationEnabled en cookieDesturesEnabled opties
* Toegevoegde ondersteuning voor afbreekstreepjes in de waarde van de optie edgeDomain
* Verzoek die tijdens de migratie van identiteitskaart wordt gemaakt wordt verzonden naar demdex eindpunt om dwars-domeinidentificatie te verbeteren wanneer de demdex koekje niet wordt geplaatst
* Aanvraag die tijdens de migratie van id&#39;s is gemaakt, verwacht altijd een reactie om ervoor te zorgen dat het identiteitscookie wordt ingesteld
* Wanneer het uitvoeren van een ongeldig bevel, zal een lijst van geldige bevelnamen in de console worden geregistreerd
* Selectievakje toegevoegd voor het schakelen van Cookie-ondersteuning van derden naar de Adobe Experience Platform Launch-extensie. Dit maakt vraag aan demdex.net onbruikbaar

## 20 december 2019

### Adobe Experience Platform Web SDK 0.0.5

#### Functies

* Activiteitenbeheer toevoegen vormt een Platform voor het starten van extensies
* EventType en EventMergeId beschikbaar maken voor de opdracht event
* OnBeforeEventSend config toevoegen aan Platform Launch Extension
* EdgeBasePath-configuratie toevoegen aan Platform Launch Extension

#### Bijwerken naar Alloy versie 0.0.10 met de volgende wijzigingen:

* Clientopslag implementeren: De status en cookies die logica naar de server zijn verplaatst
* EventType en EventMergeId beschikbaar maken voor de opdracht event
* Gebruik sendBeacon voor verbinding het volgen buiten uitgangsverbindingen
* ID-syntaxis na controle op vervaldatum terughalen
* setCustomerIds command not hashing ids on non-SSL (http) pages
* Geef het APEX-domein door aan de server die moet worden gebruikt voor het instellen van status/cookies
* De ECID van het antwoord oppakken met een nieuw type greep
* Standaardinstellingen voor activering en identiteitsconfiguratie verwijderen
* Naam wijzigen + queryopties verplaatsen naar meta
* Oudere ECID-migratie

#### Opgeloste problemen

* Voor onverwachte statuscode parseert en formatteert de reactielichaam voor foutenmelding
* Het runnen zuivert bevel of het gebruiken van alloy_debug wordt overschreven door configuratie

## 25 november 2019

### Adobe Experience Platform Web SDK 0.0.3

#### Functies

* De nieuwe gebieden van de Fusie ID en van het Type op de Send actie van de Gebeurtenis. Identiteitskaart van de fusie brengt aan `xdm.eventMergeID` in het XDM schema en het Type brengt aan `xdm.eventType` in het XDM schema in kaart.
* Verbeterde foutafhandeling en -rapportage
* Gebruikt nu `sendBeacon` voor alle koppelingen

#### Opgeloste problemen

* Probleem verholpen waarbij foutopsporing door een querytekenreeksparameter of de opdracht `debug` niet zou blijven bestaan tijdens de sessie.

## 18 november 2019

### Adobe Experience Platform Web SDK 0.0.2

#### Functies

* Extensie is in gebruik genomen
* ECID-ondersteuning zonder extra aanroepen van bibliotheken of netwerken
* Ondersteuning voor aanmelden
* Ondersteuning voor het verzenden van XDM naar AEP
* Ondersteuning voor eerste domein
* Browsercontext automatisch verzamelen
* Volledige open bron ([extension](https://github.com/adobe/reactor-extension-alloy), [SDK](https://github.com/adobe/reactor-extension-alloy))
* Gedetailleerde logboekregistratie
* Mogelijkheid om fouten in de productie te verbergen

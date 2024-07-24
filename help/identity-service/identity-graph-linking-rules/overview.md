---
title: Overzicht van regels voor identiteitsgrafiek
description: Leer over de Regels van de Vereniging van de Grafiek van Identiteit in de Dienst van de Identiteit.
badge: Beta
exl-id: 317df52a-d3ae-4c21-bcac-802dceed4e53
source-git-commit: 7daa9191f2e095f01c7c09f02f87aa8724e2e325
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 0%

---

# Overzicht van regels voor identiteitsgrafiek

>[!AVAILABILITY]
>
>De regels voor identiteitsgrafiekkoppelingen staan momenteel in bèta. Neem contact op met het accountteam van de Adobe voor meer informatie over de deelnemingscriteria. De functie en documentatie kunnen worden gewijzigd.

## Inhoudsopgave

* [Overzicht](./overview.md)
* [Algoritme voor identiteitsoptimalisatie](./identity-optimization-algorithm.md)
* [Prioriteit naamruimte](./namespace-priority.md)
* [UI voor grafieksimulatie](./graph-simulation.md)
* [Gebruikersinterface voor identiteitsinstellingen](./identity-settings-ui.md)
* [Voorbeelden van grafiekconfiguraties](./configuration.md)
* [Voorbeeldscenario&#39;s](./example-scenarios.md)

Met Adobe Experience Platform Identity Service en Real-Time Customer Profile is het eenvoudig om aan te nemen dat uw gegevens perfect zijn opgenomen en dat alle samengevoegde profielen één persoon vertegenwoordigen via een personenteken, zoals een CRM-id. Er zijn echter scenario&#39;s waarin bepaalde gegevens kunnen proberen meerdere verschillende profielen samen te voegen tot één profiel (grafiek samenvouwen). Om deze ongewenste samenvoegingen te verhinderen, kunt u configuraties gebruiken die door identiteitsgrafiek worden verstrekt die regels verbindt en voor nauwkeurige verpersoonlijking voor uw gebruikers toestaan.

## Voorbeeldscenario&#39;s waarbij een grafiek kan samenvouwen

* **Gedeeld apparaat**: Het gedeelde apparaat verwijst naar apparaten die door meer dan één individu worden gebruikt. Voorbeelden van een gedeeld apparaat zijn tablets, bibliotheekcomputers en kiosken.
* **Onjuiste e-mail en telefoonaantallen**: De slechte e-mail en telefoonaantallen verwijzen naar eind - gebruikers die ongeldige contactinformatie registreren, zoals &quot;test <span>@test.com&quot;voor e-mail, en &quot;+1-111-111-111&quot;voor telefoonaantal.
* **Onjuiste of slechte identiteitswaarden**: De onjuiste of slechte identiteitswaarden verwijzen naar niet-unieke identiteitswaarden die CRM IDs konden samenvoegen. Terwijl IDFA&#39;s bijvoorbeeld 36 tekens moeten hebben (32 alfanumerieke tekens en vier afbreekstreepjes), zijn er scenario&#39;s waarin een IDFA met de identiteitswaarde &quot;user_null&quot; kan worden opgenomen. Op dezelfde manier steunen de telefoonaantallen slechts numerieke karakters, maar een telefoonnamespace met een identiteitswaarde van &quot;niet-gespecificeerd&quot;kan worden opgenomen.

Voor meer informatie over gebruiksgevalscenario&#39;s voor identiteitsgrafiek die regels verbindt, lees het document op [ voorbeeldscenario&#39;s ](./example-scenarios.md).

## Koppelingsregels voor identiteitsgrafiek {#identity-graph-linking-rules}

Met de regels voor identiteitsgrafiek kunt u:

* Maak één identiteitsgrafiek/samengevoegd profiel voor elke gebruiker door unieke naamruimten te configureren, waardoor twee verschillende personen-id&#39;s niet in één identiteitsgrafiek kunnen worden samengevoegd.
* Online geverifieerde gebeurtenissen aan de persoon koppelen door prioriteiten te configureren

### Terminologie {#terminology}

| Terminologie | Beschrijving |
| --- | --- |
| Unieke naamruimte | Een unieke naamruimte is een naamruimte voor identiteiten die is ingesteld op scheiding binnen de context van een identiteitsgrafiek. U kunt een naamruimte zo configureren dat deze uniek is met behulp van de gebruikersinterface. Zodra een naamruimte als uniek is gedefinieerd, kan een grafiek slechts één identiteit hebben die die naamruimte bevat. |
| Prioriteit naamruimte | De prioriteit Namespace verwijst naar het relatieve belang van namespaces in vergelijking met elkaar. De prioriteit van Namespace is configureerbaar door UI. U kunt naamruimten in een bepaalde identiteitsgrafiek rangschikken. Zodra toegelaten, zal de namenprioriteit in diverse scenario&#39;s, zoals input voor het algoritme van de identiteitsoptimalisering en het bepalen van primaire identiteit voor de fragmenten van de ervaringsgebeurtenis worden gebruikt. |
| Algoritme voor identiteitsoptimalisatie | Het algoritme van de identiteitsoptimalisering zorgt ervoor dat de richtlijnen door unieke namespace en namespaceprioriteiten worden gecreeerd in een bepaalde identiteitsgrafiek worden afgedwongen. |

### Unieke naamruimte {#unique-namespace}

U kunt een naamruimte zo configureren dat deze uniek is met behulp van de gebruikersinterface voor identiteitsinstellingen. Hiermee wordt het algoritme voor identiteitsoptimalisatie aangegeven dat een bepaalde grafiek slechts één identiteit mag hebben die die unieke naamruimte bevat. Zo voorkomt u dat twee verschillende personen-id&#39;s in dezelfde grafiek worden samengevoegd.

Overweeg het volgende scenario:

* Scott gebruikt een tablet en opent zijn browser van Google Chrome om naar nike <span>.com te gaan, waar hij binnen ondertekent en voor nieuwe basketbalschoenen doorbladert.
   * In dit scenario worden achter de schermen de volgende identiteiten geregistreerd:
      * Een ECID-naamruimte en -waarde die het gebruik van de browser vertegenwoordigen
      * Een CRM ID namespace en waarde om de voor authentiek verklaarde gebruiker te vertegenwoordigen (Scott die binnen met zijn gebruikersbenaming en wachtwoordcombinatie wordt ondertekend).
* Zijn zoon Peter gebruikt dan hetzelfde tablet en gebruikt Google Chrome ook om naar nike <span>.com te gaan, waar hij zich aanmeldt voor zijn eigen rekening om naar voetbalapparatuur te zoeken.
   * In dit scenario worden achter de schermen de volgende identiteiten geregistreerd:
      * Dezelfde ECID-naamruimte en -waarde die de browser vertegenwoordigen.
      * Een nieuwe CRM-id-naamruimte en -waarde die de geverifieerde gebruiker vertegenwoordigen.

Als CRM-id is geconfigureerd als een unieke naamruimte, worden de CRM-id&#39;s door het algoritme voor identiteitsoptimalisatie gesplitst in twee afzonderlijke identiteitsgrafieken, in plaats van ze samen te voegen.

Als u geen unieke naamruimte configureert, kan het gebeuren dat er ongewenste grafieksamenvoegingen plaatsvinden, zoals twee identiteiten met dezelfde naamruimte voor CRM-id, maar verschillende identiteitswaarden (scenario&#39;s als deze vertegenwoordigen vaak twee verschillende persoonentiteiten in dezelfde grafiek).

U moet een unieke naamruimte configureren om het algoritme voor identiteitsoptimalisatie te informeren en beperkingen in te stellen op de identiteitsgegevens die in een bepaalde identiteitsgrafiek worden opgenomen.

### Prioriteit naamruimte {#namespace-priority}

De prioriteit Namespace verwijst naar het relatieve belang van namespaces in vergelijking met elkaar. De prioriteit Namespace is configureerbaar door UI en u kunt namespaces in een bepaalde identiteitsgrafiek rangschikken.

Één manier waarin namespace prioriteit wordt gebruikt is in het bepalen van de primaire identiteit van de fragmenten van de ervaringsgebeurtenis (gebruikersgedrag) in het Profiel van de Klant in real time. Als de prioritaire montages worden gevormd, dan zal het primaire identiteit plaatsen op Web SDK niet meer worden gebruikt om te bepalen welke profielfragmenten worden opgeslagen.

Unieke naamruimten en naamruimteprioriteiten kunnen beide worden geconfigureerd in de gebruikersinterface voor identiteitsinstellingen. De effecten van hun configuraties zijn echter anders:

| | Identiteitsservice | Klantprofiel in realtime |
| --- | --- | --- |
| Unieke naamruimte | In de Dienst van de Identiteit, verwijst het algoritme van de identiteitsoptimalisering naar unieke namespaces om de identiteitsgegevens te bepalen die aan een bepaalde identiteitsgrafiek worden opgenomen. | Unieke naamruimten zijn niet van invloed op het realtime klantprofiel. |
| Prioriteit naamruimte | In de Dienst van de Identiteit, voor grafieken die veelvoudige lagen hebben, zal namespace prioriteit bepalen dat de aangewezen verbindingen worden verwijderd. | Wanneer een ervaringsgebeurtenis in Profiel wordt opgenomen, wordt namespace met de hoogste prioriteit de primaire identiteit van het profielfragment. |

* De prioriteit Namespace heeft geen invloed op het grafiekgedrag wanneer de limiet van 50 identiteiten per grafiek wordt bereikt.
* **de prioriteit van Namespace is een numerieke waarde** die aan namespace wordt toegewezen die op zijn relatieve belang wijst. Dit is een eigenschap van een naamruimte.
* **Primaire identiteit is de identiteit waarin een profielfragment tegen** wordt opgeslagen. Een profielfragment is een record met gegevens waarin informatie over een bepaalde gebruiker wordt opgeslagen: kenmerken (gewoonlijk opgenomen via CRM-records) of gebeurtenissen (gewoonlijk opgenomen via ervaringsgebeurtenissen of online gegevens).
* De prioriteit Namespace bepaalt de primaire identiteit voor de fragmenten van de ervaringsgebeurtenis.
   * Voor profielverslagen, kunt u de schemawerkruimte in de UI van het Experience Platform gebruiken om identiteitsgebieden, met inbegrip van de primaire identiteit te bepalen. Lees de gids op [ bepalend identiteitsgebieden in UI ](../../xdm/ui/fields/identity.md) voor meer informatie.
* Als een ervaringsgebeurtenis twee of meer identiteiten van de hoogste namespace prioriteit in identityMap heeft, zal het van opname worden verworpen omdat het als &quot;slechte gegevens&quot;zal worden beschouwd. Als identityMap bijvoorbeeld `{ECID: 111, CRMID: John, CRMID: Jane}` bevat, wordt de gehele gebeurtenis als ongeldige gegevens afgewezen, omdat dit betekent dat de gebeurtenis tegelijkertijd aan zowel `CRMID: John` als `CRMID: Jane` wordt gekoppeld.

Voor meer informatie, lees de gids over [ namespace prioriteit ](./namespace-priority.md).

## Volgende stappen

Lees de volgende documentatie voor meer informatie over koppelingsregels voor identiteitsgrafieken:

* [ het optimalisatiealgoritme van de Identiteit ](./identity-optimization-algorithm.md).
* [ prioriteit Namespace ](./namespace-priority.md).
* [ de scenario&#39;s van het Voorbeeld om identiteitsgrafiek te vormen die regels ](./example-scenarios.md) verbindt.

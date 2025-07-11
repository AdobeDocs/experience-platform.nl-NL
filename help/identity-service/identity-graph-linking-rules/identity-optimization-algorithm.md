---
title: Algoritme voor identiteitsoptimalisatie
description: Leer over het Algoritme van de Optimalisering van de Identiteit in de Dienst van de Identiteit.
exl-id: 5545bf35-3f23-4206-9658-e1c33e668c98
source-git-commit: 0587ddf1012adb13e6d399953839735f73fe151e
workflow-type: tm+mt
source-wordcount: '1580'
ht-degree: 0%

---

# Algoritme voor identiteitsoptimalisatie {#identity-optimization-algorithm}

>[!CONTEXTUALHELP]
>id="platform_identities_uniquenamespace"
>title="Unieke naamruimte"
>abstract="Een grafiek kan geen twee identiteiten met een unieke naamruimte hebben. Als een grafiek probeert deze limiet te overschrijden, blijven de meest recente koppelingen behouden en worden de oudste koppelingen verwijderd."

Het algoritme van de Optimalisering van de Identiteit is een grafiekalgoritme op de Dienst van de Identiteit die helpt ervoor te zorgen dat een identiteitsgrafiek van één enkele persoon representatief is, en daarom, de ongewenste samenvoeging van identiteiten op het Profiel van de Klant in real time verhindert.

## Invoerparameters {#input-parameters}

Lees deze sectie voor informatie over unieke naamruimten en namespace prioriteit. Deze twee concepten dienen als inputparameters die door het Algoritme van de Optimalisering van de Identiteit worden vereist.

### Unieke naamruimte {#unique-namespace}

Een unieke naamruimte bepaalt de koppelingen die worden verwijderd als de grafiek samenvouwt.

Eén samengevoegd profiel en de bijbehorende identiteitsgrafiek moeten één persoon (persoon-entiteit) vertegenwoordigen. Eén individu wordt meestal vertegenwoordigd door CRMID&#39;s en/of aanmeldings-id&#39;s. De verwachting is dat geen twee individuen (CRMIDs) in één enkel profiel of grafiek worden samengevoegd.

U moet specificeren welke namespaces een persoonentiteit in de Dienst van de Identiteit gebruikend het Algoritme van de Optimalisering van de Identiteit vertegenwoordigen. Als een CRM-database bijvoorbeeld een gebruikersaccount definieert die aan één CRMID en één e-mailadres moet worden gekoppeld, zien de identiteitsinstellingen voor deze sandbox er als volgt uit:

* CRMID-naamruimte = uniek
* E-mailnaamruimte = uniek

Een naamruimte die u als uniek declareert, wordt automatisch geconfigureerd voor een maximumlimiet van één naamruimte binnen een bepaalde identiteitsgrafiek. Als u bijvoorbeeld een naamruimte CRMID als uniek declareert, kan een identiteitsgrafiek slechts één identiteit hebben die een naamruimte CRMID bevat. Als u een naamruimte niet als uniek declareert, kan de grafiek meer dan één identiteit met die naamruimte bevatten.

>[!NOTE]
>
>* Vertegenwoordiging van de huishoudelijke entiteit (&quot;huiselijke grafieken&quot;) wordt momenteel niet ondersteund.
>
>* Alle naamruimten die id&#39;s van personen zijn en die in de sandbox worden gebruikt om identiteitsgrafieken te genereren, moeten worden gemarkeerd als een unieke naamruimte. Anders ziet u mogelijk ongewenste koppelingsresultaten.

### Prioriteit naamruimte {#namespace-priority}

De prioriteit Namespace bepaalt hoe het Algoritme van de Optimalisering van de Identiteit verbindingen verwijdert.

Naamruimten in Identiteitsservice hebben een impliciete relatieve volgorde van belang. Bekijk een grafiek die gestructureerd is als een piramide. Er is één knoop op de hoogste laag, twee knopen op de middelste laag, en vier knopen op de bodemlaag. De prioriteit Namespace moet deze relatieve orde weerspiegelen om ervoor te zorgen dat een persoonentiteit correct wordt vertegenwoordigd.

Voor een diepgaande blik bij namespace prioriteit en zijn volledige functionaliteit en gebruik, lees de [ namespace prioritaire gids ](./namespace-priority.md).

![ de grafieklagen en namespace prioriteit.](../images/namespace-priority/graph-layers.png " de grafieklagen en namespace prioriteit."){zoomable="yes"}

## Proces {#process}

Bij het opnemen van nieuwe identiteiten, controleert de Dienst van de Identiteit als de nieuwe identiteiten en hun overeenkomstige namespaces aan unieke namespaceconfiguraties vasthouden. Als de configuraties worden gevolgd, gaat de opname verder en worden de nieuwe identiteiten aan de grafiek gekoppeld. Nochtans, als de configuraties niet worden gevolgd, dan zal het Algoritme van de Optimalisering van de Identiteit:

* Ontvang de meest recente gebeurtenis, terwijl het nemen van namespace prioriteit rekening houdt.
* Verwijder de koppeling waarmee twee personenentiteiten zouden worden samengevoegd uit de desbetreffende grafieklaag.

## Details van algoritme voor identiteitsoptimalisatie

Wanneer de unieke naamruimtebeperking wordt overtreden, worden de koppelingen opnieuw afgespeeld met het algoritme voor identiteitsoptimalisatie en wordt de grafiek helemaal opnieuw samengesteld.

* Koppelingen worden in de volgende volgorde gesorteerd:
   * Laatste gebeurtenis.
   * Tijdstempel op som van naamruimteprioriteit (lagere som = hogere volgorde).
* De grafiek zou op basis van de bovenstaande volgorde opnieuw tot stand komen. Als het toevoegen van de koppeling de limietbeperking schendt (de grafiek bevat bijvoorbeeld twee of meer identiteiten met een unieke naamruimte), worden de koppelingen verwijderd.
* De resulterende grafiek zal dan volgzaam met de unieke namespace beperking zijn die u vormde.

![ een diagram dat het Algoritme van de Optimalisering van de Identiteit visualiseert.](../images/ido_algorithm.png " een diagram dat het Algoritme van de Optimalisering van de Identiteit visualiseert."){zoomable="yes"}

## Voorbeeldscenario&#39;s voor algoritme voor identiteitsoptimalisatie

De volgende sectie beschrijft hoe het Algoritme van de Optimalisering van de Identiteit zich gedraagt, in scenario&#39;s zoals gedeeld apparaat of het opnemen van gegevens met zelfde timestamp.

### Gedeeld apparaat

Een gedeeld apparaat verwijst naar een apparaat dat door meerdere personen wordt gebruikt. Een gedeeld apparaat kan bijvoorbeeld een laptop of tablet zijn die u deelt met een partner of een familielid, een bibliotheekcomputer of een openbare schijf.

>[!BEGINTABS]

>[!TAB  Voorbeeld één ]

| Naamruimte | Unieke naamruimte |
| --- | --- |
| CRMID | Ja |
| Email | Ja |
| ECID | Nee |

In dit voorbeeld worden zowel CRMID als e-mail aangewezen als unieke naamruimten. Bij `timestamp=0` wordt een CRM-recorddataset opgenomen en worden twee verschillende grafieken gemaakt vanwege de unieke naamruimteconfiguratie. Elke grafiek bevat een CRMID en een e-mailnaamruimte.

* `timestamp=1`: Jane meldt zich met een laptop aan bij uw e-commercewebsite. Jane wordt vertegenwoordigd door haar CRMID en E-mail, terwijl de webbrowser op haar laptop die zij gebruikt wordt vertegenwoordigd door een ECID.
* `timestamp=2`: John meldt zich met dezelfde laptop aan bij uw e-commercewebsite. John wordt vertegenwoordigd door zijn CRMID en E-mail, terwijl Webbrowser hij gebruikte reeds door een ECID wordt vertegenwoordigd. Omdat dezelfde ECID aan twee verschillende grafieken is gekoppeld, kan de Identity Service weten dat dit apparaat (laptop) een gedeeld apparaat is.
* Vanwege de unieke naamruimteconfiguratie die een maximum van één CRMID-naamruimte en één E-mailnaamruimte per grafiek instelt, wordt de grafiek in tweeën gesplitst.
   * Ten slotte, omdat John de laatste geverifieerde gebruiker is, blijft de ECID die de laptop vertegenwoordigt gekoppeld aan zijn grafiek in plaats van aan Jane.

![ Geval één van gedeeld apparaat.](../images/identity-settings/shared-device-case-one.png " Geval één van gedeeld apparaat."){zoomable="yes"}

>[!TAB  Voorbeeld twee ]

| Naamruimte | Unieke naamruimte |
| --- | --- |
| CRMID | Ja |
| ECID | Nee |

In dit voorbeeld wordt de naamruimte CRMID aangewezen als een unieke naamruimte.

* `timestamp=1`: Jane meldt zich met een laptop aan bij uw e-commercewebsite. Ze wordt vertegenwoordigd door haar CRMID en de webbrowser op de laptop wordt vertegenwoordigd door de ECID.
* `timestamp=2`: John meldt zich met dezelfde laptop aan bij uw e-commercewebsite. Hij wordt vertegenwoordigd door zijn CRMID en de webbrowser die hij gebruikt wordt door dezelfde ECID vertegenwoordigd.
   * Deze gebeurtenis verbindt twee onafhankelijke CRMIDs aan zelfde ECID, die de gevormde grens van één CRMID overschrijdt.
   * Dientengevolge, verwijdert het Algoritme van de Optimalisering van de Identiteit de oudere verbinding, die in dit geval CRMID van Jane is die bij `timestamp=1` werd verbonden.
   * Nochtans, terwijl CRMID van Jane niet meer als grafiek op de Dienst van de Identiteit zal bestaan, zal het nog als profiel op het Profiel van de Klant in real time blijven. Dit komt omdat een identiteitsgrafiek minstens twee verbonden identiteiten moet bevatten, en als resultaat van het verwijderen van de verbindingen, heeft CRMID van Jane niet meer een andere identiteit om met te verbinden.

![ Geval twee van gedeeld apparaat.](../images/identity-settings/shared-device-case-two.png " Geval twee van gedeeld apparaat."){zoomable="yes"}

>[!ENDTABS]

### Onjuist e-mailbericht

Er zijn gevallen waarin een gebruiker ongeldige waarden kan invoeren voor zijn e-mail- en/of telefoonnummers.

| Naamruimte | Unieke naamruimte |
| --- | --- |
| CRMID | Ja |
| Email | Ja |
| ECID | Nee |

In dit voorbeeld worden de naamruimten CRMID en Email als uniek aangeduid. Overweeg het scenario dat Jane en John zich aan uw e-commercewebsite gebruikend een slechte e-mailwaarde (bijvoorbeeld, test <span> @test.com) hebben aangemeld.

* `timestamp=1`: Jane meldt zich aan bij uw e-commercewebsite gebruikend Safari op haar iPhone, opstellend haar CRMID (login informatie) en haar ECID (browser).
* `timestamp=2`: John meldt zich aan bij uw e-commercewebsite gebruikend Google Chrome op zijn iPhone, vestigend zijn CRMID (login informatie) en ECID (browser).
* `timestamp=3`: Uw gegevenstechnicus neemt het CRM-record van Jane op, wat ertoe leidt dat haar CRMID wordt gekoppeld aan het slechte e-mailbericht.
* `timestamp=4`: Uw gegevenstechnicus neemt het CRM-record van John in, wat ertoe leidt dat zijn CRMID wordt gekoppeld aan het slechte e-mailbericht.
   * Dit wordt dan een schending van de unieke namespaceconfiguratie aangezien het één enkele grafiek met twee CRMID namespaces leidt.
   * Dientengevolge, schrapt het Algoritme van de Optimalisering van de Identiteit de oudere verbinding, die in dit geval het verband tussen de identiteit van Jane met CRMID namespace en de identiteit met test <span>@test is.

Met het Algoritme van de Optimalisering van de Identiteit, worden de slechte identiteitswaarden zoals bogus e-mails of telefoonaantallen niet verspreid over verscheidene verschillende identiteitsgrafieken.

![ een diagram van een slechte e-mailopname.](../images/identity-settings/bad-email.png " een diagram van een slechte e-mailopname."){zoomable="yes"}

## Anonieme gebeurtenisassociatie

ECID&#39;s slaan niet-geverifieerde (anonieme) gebeurtenissen op, terwijl CRMID geverifieerde gebeurtenissen opslaat. In het geval van gedeelde apparaten, wordt ECID (drager van niet voor authentiek verklaarde gebeurtenissen) geassocieerd met de **laatste voor authentiek verklaarde gebruiker**.

Bekijk het onderstaande diagram om beter te begrijpen hoe anonieme gebeurtenisassociatie werkt:

* Kevin en Nora delen een tablet.
   * `timestamp=1`: Kevin meldt zich aan bij een e-commercewebsite gebruikend zijn rekening, daardoor vestigend zijn CRMID (login informatie) en ECID (browser). Op het moment van aanmelding wordt Kevin nu beschouwd als de laatst geverifieerde gebruiker.
   * `timestamp=2`: Nora meldt zich aan bij een e-commercewebsite gebruikend haar rekening, daardoor vestigend haar CRMID (login informatie) en zelfde ECID. Op het moment van aanmelding wordt Nora nu beschouwd als de laatst geverifieerde gebruiker.
   * `timestamp=3`: Kevin gebruikt het tablet om door de e-commercewebsite te bladeren, maar meldt zich niet aan met zijn account. Kevin&#39;s browseractiviteiten worden vervolgens opgeslagen in de ECID, die op haar beurt aan Nora is gekoppeld omdat ze de laatste geverifieerde gebruiker is. Op dit moment is Nora eigenaar van de anonieme gebeurtenissen.
      * Totdat Kevin zich opnieuw aanmeldt, wordt het samengevoegde profiel van Nora gekoppeld aan alle niet-geverifieerde gebeurtenissen die op basis van de ECID zijn opgeslagen (waarbij ECID de primaire identiteit is).
   * `timestamp=4`: Kevin meldt zich voor de tweede keer aan. Op dit punt wordt hij opnieuw de laatste geverifieerde gebruiker en is hij nu ook eigenaar van de niet-geverifieerde gebeurtenissen:
      * Vóór zijn eerste aanmelding vóór `timestamp=1`; en
      * Om het even welke activiteiten hij of Nora deed terwijl het doorbladeren anoniem in-tussen Kevin&#39;s eerste en tweede logins.

![ een diagram van anonieme gebeurtenisvereniging.](../images/identity-settings/anon-event-association.png " een diagram van anonieme gebeurtenisvereniging."){zoomable="yes"}


## Volgende stappen

Lees de volgende documentatie voor meer informatie over [!DNL Identity Graph Linking Rules] :

* [[!DNL Identity Graph Linking Rules]-overzicht](./overview.md)
* [Implementatiehandleiding](./implementation-guide.md)
* [Voorbeelden van grafiekconfiguraties](./example-configurations.md)
* [Problemen oplossen en veelgestelde vragen](./troubleshooting.md)
* [Prioriteit naamruimte](./namespace-priority.md)
* [UI voor grafieksimulatie](./graph-simulation.md)
* [Gebruikersinterface voor identiteitsinstellingen](./identity-settings-ui.md)
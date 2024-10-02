---
title: Algoritme voor identiteitsoptimalisatie
description: Leer over het Algoritme van de Optimalisering van de Identiteit in de Dienst van de Identiteit.
exl-id: 5545bf35-3f23-4206-9658-e1c33e668c98
source-git-commit: cfe0181104f09bfd91b22d165c23154a15cd5344
workflow-type: tm+mt
source-wordcount: '1528'
ht-degree: 0%

---

# Algoritme voor identiteitsoptimalisatie

>[!AVAILABILITY]
>
>Identiteitsgrafiek die regels verbindt is momenteel in Beperkte Beschikbaarheid. Neem contact op met het accountteam van de Adobe voor informatie over de toegang tot de functie in ontwikkelsandboxen.

Het algoritme voor identiteitsoptimalisatie is een grafiekalgoritme voor Identiteitsservice dat ervoor zorgt dat een identiteitsgrafiek representatief is voor één persoon, en dat daardoor ongewenste samenvoeging van identiteiten in Real-Time Klantprofiel voorkomt.

## Invoerparameters {#input-parameters}

Lees deze sectie voor informatie over unieke naamruimten en namespace prioriteit. Deze twee concepten fungeren als invoerparameters die door het algoritme voor identiteitsoptimalisatie worden vereist.

### Unieke naamruimte {#unique-namespace}

Een unieke naamruimte bepaalt de koppelingen die worden verwijderd als de grafiek samenvouwt.

Eén samengevoegd profiel en de bijbehorende identiteitsgrafiek moeten één persoon (persoon-entiteit) vertegenwoordigen. Eén individu wordt meestal vertegenwoordigd door CRMID&#39;s en/of aanmeldings-id&#39;s. De verwachting is dat geen twee individuen (CRMIDs) in één enkel profiel of grafiek worden samengevoegd.

U moet opgeven welke naamruimten een personenentiteit in Identiteitsservice vertegenwoordigen met behulp van het algoritme voor identiteitsoptimalisatie. Als een CRM-database bijvoorbeeld een gebruikersaccount definieert die aan één CRMID en één e-mailadres moet worden gekoppeld, zien de identiteitsinstellingen voor deze sandbox er als volgt uit:

* CRMID-naamruimte = uniek
* E-mailnaamruimte = uniek

Een naamruimte die u als uniek declareert, wordt automatisch geconfigureerd voor een maximumlimiet van één naamruimte binnen een bepaalde identiteitsgrafiek. Als u bijvoorbeeld een naamruimte CRMID als uniek declareert, kan een identiteitsgrafiek slechts één identiteit hebben die een naamruimte CRMID bevat. Als u een naamruimte niet als uniek declareert, kan de grafiek meer dan één identiteit met die naamruimte bevatten.

>[!NOTE]
>
>* Vertegenwoordiging van de huishoudelijke entiteit (&quot;huiselijke grafieken&quot;) wordt momenteel niet ondersteund.
>
>* Alle naamruimten die id&#39;s van personen zijn en die in de sandbox worden gebruikt om identiteitsgrafieken te genereren, moeten worden gemarkeerd als een unieke naamruimte. Anders ziet u mogelijk ongewenste koppelingsresultaten.

### Prioriteit naamruimte {#namespace-priority}

De prioriteit Namespace bepaalt hoe het algoritme van de identiteitsoptimalisering verbindingen verwijdert.

Naamruimten in Identiteitsservice hebben een impliciete relatieve volgorde van belang. Bekijk een grafiek die gestructureerd is als een piramide. Er is één knoop op de hoogste laag, twee knopen op de middelste laag, en vier knopen op de bodemlaag. De prioriteit Namespace moet deze relatieve orde weerspiegelen om ervoor te zorgen dat een persoonentiteit correct wordt vertegenwoordigd.

Voor een diepgaande blik bij namespace prioriteit en zijn volledige functionaliteit en gebruik, lees de [ namespace prioritaire gids ](./namespace-priority.md).

![ grafieklagen en namespace prioriteit ](../images/namespace-priority/graph-layers.png)

## Proces {#process}

Bij het opnemen van nieuwe identiteiten, controleert de Dienst van de Identiteit als de nieuwe identiteiten en hun overeenkomstige namespaces aan unieke namespaceconfiguraties vasthouden. Als de configuraties worden gevolgd, gaat de opname verder en worden de nieuwe identiteiten aan de grafiek gekoppeld. Nochtans, als de configuraties niet worden gevolgd, dan zal het algoritme van de identiteitsoptimalisering:

* Ontvang de meest recente gebeurtenis, terwijl het nemen van namespace prioriteit rekening houdt.
* Verwijder de koppeling waarmee twee personenentiteiten zouden worden samengevoegd uit de desbetreffende grafieklaag.

## Details van het algoritme voor identiteitsoptimalisatie

Wanneer de unieke naamruimtebeperking wordt overtreden, worden de koppelingen opnieuw afgespeeld en wordt de grafiek helemaal opnieuw samengesteld.

* Koppelingen worden in de volgende volgorde gesorteerd:
   * Laatste gebeurtenis.
   * Tijdstempel op som van naamruimteprioriteit (lagere som = hogere volgorde).
* De grafiek zou op basis van de bovenstaande volgorde opnieuw tot stand komen. Als het toevoegen van de koppeling de limietbeperking schendt (de grafiek bevat bijvoorbeeld twee of meer identiteiten met een unieke naamruimte), worden de koppelingen verwijderd.
* De resulterende grafiek zal dan volgzaam met de unieke namespace beperking zijn die u vormde.

![ A diagram dat identiteitsoptimaliseringsalgoritme visualiseert.](../images/ido_algorithm.png)

## Voorbeeldscenario&#39;s voor algoritme voor identiteitsoptimalisatie

In de volgende sectie wordt beschreven hoe het algoritme voor identiteitsoptimalisatie zich gedraagt, in situaties zoals een gedeeld apparaat of het opnemen van gegevens met dezelfde tijdstempel.

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
* Vanwege de unieke naamruimte-configuratie die maximaal één CRMID-naamruimte en één E-mailnaamruimte per grafiek instelt, wordt de grafiek door het algoritme voor identiteitsoptimalisatie in twee opgesplitst.
   * Ten slotte, omdat John de laatste geverifieerde gebruiker is, blijft de ECID die de laptop vertegenwoordigt gekoppeld aan zijn grafiek in plaats van aan Jane.

![ gedeelde apparatengeval één ](../images/identity-settings/shared-device-case-one.png)

>[!TAB  Voorbeeld twee ]

| Naamruimte | Unieke naamruimte |
| --- | --- |
| CRMID | Ja |
| ECID | Nee |

In dit voorbeeld wordt de naamruimte CRMID aangewezen als een unieke naamruimte.

* `timestamp=1`: Jane meldt zich met een laptop aan bij uw e-commercewebsite. Ze wordt vertegenwoordigd door haar CRMID en de webbrowser op de laptop wordt vertegenwoordigd door de ECID.
* `timestamp=2`: John meldt zich met dezelfde laptop aan bij uw e-commercewebsite. Hij wordt vertegenwoordigd door zijn CRMID en de webbrowser die hij gebruikt wordt door dezelfde ECID vertegenwoordigd.
   * Deze gebeurtenis verbindt twee onafhankelijke CRMIDs aan zelfde ECID, die de gevormde grens van één CRMID overschrijdt.
   * Als gevolg hiervan verwijdert het algoritme voor identiteitsoptimalisatie de oudere koppeling, wat in dit geval Jane&#39;s CRMID is die bij `timestamp=1` was gekoppeld.
   * Nochtans, terwijl CRMID van Jane niet meer als grafiek op de Dienst van de Identiteit zal bestaan, zal het nog als profiel op het Profiel van de Klant in real time blijven. Dit komt omdat een identiteitsgrafiek minstens twee verbonden identiteiten moet bevatten, en als resultaat van het verwijderen van de verbindingen, heeft CRMID van Jane niet meer een andere identiteit om met te verbinden.

![ delen-apparaat-geval-twee ](../images/identity-settings/shared-device-case-two.png)

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
   * Dientengevolge, schrapt het algoritme van de identiteitsoptimalisering de oudere verbinding, die in dit geval het verband tussen de identiteit van Jane met CRMID namespace en de identiteit met test <span>@test is.

Met algoritme voor identiteitsoptimalisatie worden onjuiste identiteitswaarden zoals bogus-e-mails of telefoonnummers niet verspreid over verschillende identiteitsgrafieken.

![ slecht-e-mail ](../images/identity-settings/bad-email.png)

### Anonieme gebeurtenisassociatie

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

![ anon-event-association ](../images/identity-settings/anon-event-association.png)


## Volgende stappen

Lees de volgende documentatie voor meer informatie over koppelingsregels voor identiteitsgrafieken:

* [Overzicht van regels voor identiteitsgrafiek](./overview.md)
* [Implementatiehandleiding](./implementation-guide.md)
* [Voorbeelden van grafiekconfiguraties](./example-configurations.md)
* [Problemen oplossen en veelgestelde vragen](./troubleshooting.md)
* [Prioriteit naamruimte](./namespace-priority.md)
* [UI voor grafieksimulatie](./graph-simulation.md)
* [Gebruikersinterface voor identiteitsinstellingen](./identity-settings-ui.md)
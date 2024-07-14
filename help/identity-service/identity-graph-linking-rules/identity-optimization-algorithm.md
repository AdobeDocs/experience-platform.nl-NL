---
title: Algoritme voor identiteitsoptimalisatie
description: Leer over het Algoritme van de Optimalisering van de Identiteit in de Dienst van de Identiteit.
badge: Beta
exl-id: 5545bf35-3f23-4206-9658-e1c33e668c98
source-git-commit: 5d19a22dc8d1b7f0151008d14b2f5bf89c85c638
workflow-type: tm+mt
source-wordcount: '1570'
ht-degree: 0%

---

# Algoritme voor identiteitsoptimalisatie

>[!AVAILABILITY]
>
>Deze functie is nog niet beschikbaar. Het bètaprogramma voor koppelingsregels voor identiteitsgrafieken zal naar verwachting in juli van start gaan voor ontwikkelingssandboxen. Neem contact op met het accountteam van de Adobe voor meer informatie over de deelnemingscriteria.

Het algoritme voor identiteitsoptimalisatie is een grafiekalgoritme voor Identiteitsservice dat ervoor zorgt dat een identiteitsgrafiek representatief is voor één persoon, en dat daardoor ongewenste samenvoeging van identiteiten in Real-Time Klantprofiel voorkomt.

## Invoerparameters {#input-parameters}

Lees deze sectie voor informatie over unieke naamruimten en namespace prioriteit. Deze twee concepten fungeren als invoerparameters die door het algoritme voor identiteitsoptimalisatie worden vereist.

### Unieke naamruimte {#unique-namespace}

Een unieke naamruimte bepaalt de koppelingen die worden verwijderd als de grafiek samenvouwt.

Eén samengevoegd profiel en de bijbehorende identiteitsgrafiek moeten één persoon (persoon-entiteit) vertegenwoordigen. Eén individu wordt gewoonlijk vertegenwoordigd door CRM-id&#39;s en/of aanmeldings-id&#39;s. De verwachting is dat geen twee individuen (CRM IDs) in één enkel profiel of grafiek worden samengevoegd.

U moet opgeven welke naamruimten een personenentiteit in Identiteitsservice vertegenwoordigen met behulp van het algoritme voor identiteitsoptimalisatie. Als een CRM-database bijvoorbeeld een gebruikersaccount definieert die moet worden gekoppeld aan één CRM-id en één e-mailadres, zien de identiteitsinstellingen voor deze sandbox er als volgt uit:

* CRM ID namespace = unique
* E-mailnaamruimte = uniek

Een naamruimte die u als uniek declareert, wordt automatisch geconfigureerd voor een maximumlimiet van één naamruimte binnen een bepaalde identiteitsgrafiek. Bijvoorbeeld, als u een identiteitskaart van CRM namespace als uniek verklaart, dan kan een identiteitsgrafiek slechts één identiteit hebben die een identiteitskaart van CRM namespace bevat. Als u een naamruimte niet als uniek declareert, kan de grafiek meer dan één identiteit met die naamruimte bevatten.

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

![ A diagram dat identiteitsoptimaliseringsalgoritme visualiseert.](../images/ido.png)

## Voorbeeldscenario&#39;s voor algoritme voor identiteitsoptimalisatie

In de volgende sectie wordt beschreven hoe het algoritme voor identiteitsoptimalisatie zich gedraagt, in situaties zoals een gedeeld apparaat of het opnemen van gegevens met dezelfde tijdstempel.

### Gedeeld apparaat

Een gedeeld apparaat verwijst naar een apparaat dat door meerdere personen wordt gebruikt. Een gedeeld apparaat kan bijvoorbeeld een laptop of tablet zijn die u deelt met een partner of een familielid, een bibliotheekcomputer of een openbare schijf.

>[!BEGINTABS]

>[!TAB  Voorbeeld één ]

| Naamruimte | Unieke naamruimte |
| --- | --- |
| CRM-id | Ja |
| Email | Ja |
| ECID | Nee |

In dit voorbeeld worden zowel CRM-id als e-mail aangewezen als unieke naamruimten. Bij `timestamp=0` wordt een CRM-recorddataset opgenomen en worden twee verschillende grafieken gemaakt vanwege de unieke naamruimteconfiguratie. Elke grafiek bevat een CRM-id en een e-mailnaamruimte.

* `timestamp=1`: Jane meldt zich met een laptop aan bij uw e-commercewebsite. Jane wordt vertegenwoordigd door haar CRM-id en e-mail, terwijl de webbrowser op haar laptop die ze gebruikt, wordt vertegenwoordigd door een ECID.
* `timestamp=2`: John meldt zich met dezelfde laptop aan bij uw e-commercewebsite. John wordt vertegenwoordigd door zijn CRM-id en e-mail, terwijl de webbrowser die hij gebruikt al wordt vertegenwoordigd door een ECID. Omdat dezelfde ECID aan twee verschillende grafieken is gekoppeld, kan de Identity Service weten dat dit apparaat (laptop) een gedeeld apparaat is.
* Maar vanwege de unieke naamruimte-configuratie die een maximum van één CRM-id-naamruimte en één e-mailnaamruimte per grafiek instelt, wordt de grafiek door het algoritme voor identiteitsoptimalisatie in twee opgesplitst.
   * Ten slotte, omdat John de laatste geverifieerde gebruiker is, blijft de ECID die de laptop vertegenwoordigt gekoppeld aan zijn grafiek in plaats van aan Jane.

![ gedeelde apparatengeval één ](../images/identity-settings/shared-device-case-one.png)

>[!TAB  Voorbeeld twee ]

| Naamruimte | Unieke naamruimte |
| --- | --- |
| CRM-id | Ja |
| ECID | Nee |

In dit voorbeeld wordt de naamruimte CRM-id aangewezen als een unieke naamruimte.

* `timestamp=1`: Jane meldt zich met een laptop aan bij uw e-commercewebsite. Ze wordt vertegenwoordigd door haar CRM-id en de webbrowser op de laptop wordt vertegenwoordigd door de ECID.
* `timestamp=2`: John meldt zich met dezelfde laptop aan bij uw e-commercewebsite. Hij wordt vertegenwoordigd door zijn CRM-id en de webbrowser die hij gebruikt wordt door dezelfde ECID vertegenwoordigd.
   * Deze gebeurtenis verbindt twee onafhankelijke identiteitskaart van CRM met zelfde ECID, die de gevormde grens van één identiteitskaart van CRM overschrijdt.
   * Dientengevolge, verwijdert het algoritme van de identiteitsoptimalisering de oudere verbinding, die in dit geval identiteitskaart van CRM van Jane is die bij `timestamp=1` werd verbonden.
   * Nochtans, terwijl identiteitskaart van CRM van Jane niet meer als grafiek op de Dienst van de Identiteit zal bestaan, zal het nog als profiel op het Profiel van de Klant in real time blijven. Dit komt omdat een identiteitsgrafiek minstens twee verbonden identiteiten moet bevatten, en als resultaat van het verwijderen van de verbindingen, heeft identiteitskaart van CRM van Jane niet meer een andere identiteit om met te verbinden.

![ delen-apparaat-geval-twee ](../images/identity-settings/shared-device-case-two.png)

>[!ENDTABS]

### Onjuist e-mailbericht

Er zijn gevallen waarin een gebruiker ongeldige waarden kan invoeren voor zijn e-mail- en/of telefoonnummers.

| Naamruimte | Unieke naamruimte |
| --- | --- |
| CRM-id | Ja |
| Email | Ja |
| ECID | Nee |

In dit voorbeeld worden de CRM-id en de e-mailnaamruimten als uniek aangeduid. Overweeg het scenario dat Jane en John zich aan uw e-commercewebsite gebruikend een slechte e-mailwaarde (bijvoorbeeld, test <span> @test.com) hebben aangemeld.

* `timestamp=1`: Jane meldt zich aan bij uw e-commercewebsite gebruikend Safari op haar iPhone, opstellend haar identiteitskaart van CRM (login informatie) en haar ECID (browser).
* `timestamp=2`: John meldt zich aan bij uw e-commercewebsite gebruikend Google Chrome op zijn iPhone, die zijn identiteitskaart van CRM (login informatie) en ECID (browser) vestigt.
* `timestamp=3`: Uw gegevenstechnicus neemt het CRM-record van Jane op, wat ertoe leidt dat haar CRM-id wordt gekoppeld aan het onjuiste e-mailbericht.
* `timestamp=4`: Uw gegevenstechnicus neemt het CRM-record van John in, wat ertoe leidt dat zijn CRM-id wordt gekoppeld aan het onjuiste e-mailbericht.
   * Dit wordt dan een schending van de unieke namespaceconfiguratie aangezien het één enkele grafiek met twee identiteitskaart van CRM namespaces leidt.
   * Dientengevolge, schrapt het algoritme van de identiteitsoptimalisering de oudere verbinding, die in dit geval het verband tussen de identiteit van Jane met identiteitskaart van CRM namespace en de identiteit met test <span>@test is.

Met algoritme voor identiteitsoptimalisatie worden onjuiste identiteitswaarden zoals bogus-e-mails of telefoonnummers niet verspreid over verschillende identiteitsgrafieken.

![ slecht-e-mail ](../images/identity-settings/bad-email.png)

### Anonieme gebeurtenisassociatie

ECIDs slaat unauthenticated (anonieme) gebeurtenissen op, terwijl identiteitskaart van CRM voor authentiek verklaarde gebeurtenissen opslaat. In het geval van gedeelde apparaten, wordt ECID (drager van niet voor authentiek verklaarde gebeurtenissen) geassocieerd met de **laatste voor authentiek verklaarde gebruiker**.

Bekijk het onderstaande diagram om beter te begrijpen hoe anonieme gebeurtenisassociatie werkt:

* Kevin en Nora delen een tablet.
   * `timestamp=1`: Kevin meldt zich aan bij een e-commercewebsite gebruikend zijn rekening, daardoor vestigend zijn identiteitskaart van CRM (login informatie) en een ECID (browser). Op het moment van aanmelding wordt Kevin nu beschouwd als de laatst geverifieerde gebruiker.
   * `timestamp=2`: Nora meldt zich aan bij een e-commercewebsite gebruikend haar rekening, daardoor vestigend haar identiteitskaart van CRM (login informatie) en zelfde ECID. Op het moment van aanmelding wordt Nora nu beschouwd als de laatst geverifieerde gebruiker.
   * `timestamp=3`: Kevin gebruikt het tablet om door de e-commercewebsite te bladeren, maar meldt zich niet aan met zijn account. Kevin&#39;s browseractiviteiten worden vervolgens opgeslagen in de ECID, die op haar beurt aan Nora is gekoppeld omdat ze de laatste geverifieerde gebruiker is. Op dit moment is Nora eigenaar van de anonieme gebeurtenissen.
      * Totdat Kevin zich opnieuw aanmeldt, wordt het samengevoegde profiel van Nora gekoppeld aan alle niet-geverifieerde gebeurtenissen die op basis van de ECID zijn opgeslagen (waarbij ECID de primaire identiteit is).
   * `timestamp=4`: Kevin meldt zich voor de tweede keer aan. Op dit punt wordt hij opnieuw de laatste geverifieerde gebruiker en is hij nu ook eigenaar van de niet-geverifieerde gebeurtenissen:
      * Vóór zijn eerste aanmelding vóór `timestamp=1`; en
      * Om het even welke activiteiten hij of Nora deed terwijl het doorbladeren anoniem in-tussen Kevin&#39;s eerste en tweede logins.

![ anon-event-association ](../images/identity-settings/anon-event-association.png)


## Volgende stappen

Lees de volgende documentatie voor meer informatie over koppelingsregels voor identiteitsgrafieken:

* [Overzicht van regels voor identiteitsgrafiek](./overview.md)
* [Voorbeeldscenario&#39;s voor het configureren van identiteitsgrafiek-koppelingsregels](./example-scenarios.md)
* [Logica voor identiteitskoppeling](../features/identity-linking-logic.md)
* [Identiteitsservice en realtime klantprofiel](../identity-and-profile.md)

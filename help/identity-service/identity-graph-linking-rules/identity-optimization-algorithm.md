---
title: Algoritme voor identiteitsoptimalisatie
description: Leer over het Algoritme van de Optimalisering van de Identiteit in de Dienst van de Identiteit.
hide: true
hidefromtoc: true
badge: Alfa
source-git-commit: 8f99dc633c87fa36cc0c5413d23b97b4fce7dbc3
workflow-type: tm+mt
source-wordcount: '1319'
ht-degree: 1%

---

# Algoritme voor identiteitsoptimalisatie

>[!IMPORTANT]
>
>Het algoritme voor identiteitsoptimalisatie is in Alpha. De functie en documentatie kunnen worden gewijzigd.

Het algoritme voor identiteitsoptimalisatie is een regel die helpt ervoor te zorgen dat een identiteitsgrafiek representatief is voor één persoon en daarom ongewenste samenvoeging van identiteiten in Real-Time Klantprofiel voorkomt.

## Invoerparameters

Eén samengevoegd profiel en de bijbehorende identiteitsgrafiek moeten één persoon (persoon-entiteit) vertegenwoordigen. Eén individu wordt gewoonlijk vertegenwoordigd door CRM-id&#39;s en/of aanmeldings-id&#39;s. De verwachting is dat geen twee individuen (CRM IDs) in één enkel profiel of grafiek worden samengevoegd.

U moet opgeven welke naamruimten een personenentiteit in Identiteitsservice vertegenwoordigen met behulp van het algoritme voor identiteitsoptimalisatie. Als een CRM-database bijvoorbeeld een gebruikersaccount definieert die moet worden gekoppeld aan één CRM-id en één e-mailadres, zien de identiteitsinstellingen voor deze sandbox er als volgt uit:

* CRM ID namespace = unique
* E-mailnaamruimte = uniek

Een naamruimte die u als uniek declareert, wordt automatisch geconfigureerd voor een maximumlimiet van één naamruimte binnen een bepaalde identiteitsgrafiek. Bijvoorbeeld, als u een identiteitskaart van CRM namespace als uniek verklaart, dan kan een identiteitsgrafiek slechts één identiteit hebben die een identiteitskaart van CRM namespace bevat.

>[!NOTE]
>
>* Momenteel ondersteunt het algoritme alleen het gebruik van één aanmeldingsidentificatie (één aanmeldingsnaamruimte). Meerdere aanmeldings-id&#39;s (meerdere naamruimten die worden gebruikt voor aanmelding), grafieken van huishoudelijke entiteiten en hiërarchische grafiekstructuren worden momenteel niet ondersteund.
>
>* Alle naamruimten die id&#39;s van personen zijn en die in de sandbox worden gebruikt om identiteitsgrafieken te genereren, moeten worden gemarkeerd als een unieke naamruimte. Anders ziet u mogelijk ongewenste koppelingsresultaten.

## Proces

Bij het opnemen van nieuwe identiteiten, controleert de Dienst van de Identiteit als de nieuwe identiteiten en hun overeenkomstige namespaces in het overschrijden van de gevormde grenzen zullen resulteren. Als de limieten niet worden overschreden, wordt de opname van nieuwe identiteiten voortgezet en worden deze identiteiten aan de grafiek gekoppeld. Als de limieten worden overschreden, werkt het algoritme voor identiteitsoptimalisatie de grafiek zodanig bij dat de meest recente tijdstempel wordt gerespecteerd en de oudste koppelingen met de naamruimten met lagere prioriteit worden verwijderd.

## Voorbeeldscenario&#39;s voor algoritme voor identiteitsoptimalisatie

In de volgende sectie wordt beschreven hoe het algoritme voor identiteitsoptimalisatie zich gedraagt, in situaties zoals een gedeeld apparaat of het opnemen van gegevens met dezelfde tijdstempel.

### Gedeeld apparaat

Een gedeeld apparaat verwijst naar een apparaat dat door meerdere personen wordt gebruikt. Een gedeeld apparaat kan bijvoorbeeld een laptop of tablet zijn die u deelt met een partner of een familielid, een bibliotheekcomputer of een openbare schijf.

>[!BEGINTABS]

>[!TAB Voorbeeld één]

| Naamruimte | Limiet |
| --- | --- |
| CRM-id | 1 |
| Email | 1 |
| ECID | N.v.t. |

In dit voorbeeld worden zowel CRM-id als e-mail aangewezen als unieke naamruimten. At `timestamp=0`, wordt een het recorddataset van CRM opgenomen en leidt tot twee verschillende grafieken wegens de limietconfiguratie. Elke grafiek bevat een CRM-id en een e-mailnaamruimte.

* `timestamp=1`: Jane meldt zich met een laptop aan bij uw e-commercewebsite. Jane wordt vertegenwoordigd door haar CRM-id en e-mail, terwijl de webbrowser op haar laptop die ze gebruikt, wordt vertegenwoordigd door een ECID.
* `timestamp=2`: John meldt zich met dezelfde laptop aan bij uw e-commercewebsite. John wordt vertegenwoordigd door zijn CRM-id en e-mail, terwijl de webbrowser die hij gebruikt al wordt vertegenwoordigd door een ECID. Omdat dezelfde ECID aan twee verschillende grafieken is gekoppeld, kan de Identity Service weten dat dit apparaat (laptop) een gedeeld apparaat is.
* Maar vanwege de limietconfiguratie die een maximum van één CRM-id-naamruimte en één e-mailnaamruimte per grafiek instelt, wordt de grafiek door het algoritme voor identiteitsoptimalisatie in twee opgesplitst.
   * Ten slotte, omdat John de laatste geverifieerde gebruiker is, blijft de ECID die de laptop vertegenwoordigt gekoppeld aan zijn grafiek in plaats van aan Jane.

![gedeelde apparaatcase één](../images/identity-settings/shared-device-case-one.png)

>[!TAB Voorbeeld twee]

| Naamruimte | Limiet |
| --- | --- |
| CRM-id | 1 |
| ECID | N.v.t. |

In dit voorbeeld wordt de naamruimte CRM-id aangewezen als een unieke naamruimte.

* `timestamp=1`: Jane meldt zich met een laptop aan bij uw e-commercewebsite. Ze wordt vertegenwoordigd door haar CRM-id en de webbrowser op de laptop wordt vertegenwoordigd door de ECID.
* `timestamp=2`: John meldt zich met dezelfde laptop aan bij uw e-commercewebsite. Hij wordt vertegenwoordigd door zijn CRM-id en de webbrowser die hij gebruikt wordt door dezelfde ECID vertegenwoordigd.
   * Deze gebeurtenis verbindt twee onafhankelijke identiteitskaart van CRM met zelfde ECID, die de gevormde grens van één identiteitskaart van CRM overschrijdt.
   * Dientengevolge, verwijdert het algoritme van de identiteitsoptimalisering de oudere verbinding, die in dit geval identiteitskaart van CRM van Jane is die werd verbonden bij `timestamp=1`.
   * Nochtans, terwijl identiteitskaart van CRM van Jane niet meer als grafiek op de Dienst van de Identiteit zal bestaan, zal het nog als profiel op het Profiel van de Klant in real time blijven. Dit komt omdat een identiteitsgrafiek minstens twee verbonden identiteiten moet bevatten, en als resultaat van het verwijderen van de verbindingen, heeft identiteitskaart van CRM van Jane niet meer een andere identiteit om met te verbinden.

![shared-device-case-two](../images/identity-settings/shared-device-case-two.png)

>[!ENDTABS]

### Onjuist e-mailbericht

Er zijn gevallen waarin een gebruiker ongeldige waarden kan invoeren voor zijn e-mail- en/of telefoonnummers.

| Naamruimte | Limiet |
| --- | --- |
| CRM-id | 1 |
| Email | 1 |
| ECID | N.v.t. |

In dit voorbeeld worden de CRM-id en de e-mailnaamruimten als uniek aangeduid. Overweeg het scenario dat Jane en John zich bij uw e-commercewebsite gebruikend een slechte e-mailwaarde (bijvoorbeeld, test hebben aangemeld<span>@test.com).

* `timestamp=1`: Jane meldt zich aan bij uw e-commercewebsite gebruikend Safari op haar iPhone, die haar identiteitskaart van CRM (login informatie) en haar ECID (browser) vestigt.
* `timestamp=2`: John meldt zich aan bij uw e-commercewebsite gebruikend Google Chrome op zijn iPhone, plaatsend zijn identiteitskaart van CRM (login informatie) en ECID (browser).
* `timestamp=3`: Uw gegevenstechnicus neemt het CRM-record van Jane op, wat ertoe leidt dat haar CRM-id wordt gekoppeld aan de slechte e-mail.
* `timestamp=4`: Uw gegevensengineer neemt het CRM-record van John in, wat ertoe leidt dat zijn CRM-id gekoppeld wordt aan het slechte e-mailbericht.
   * Dit wordt dan een schending van de gevormde grenzen aangezien het één enkele grafiek met twee identiteitskaart van CRM namespaces leidt.
   * Dientengevolge, schrapt het algoritme van de identiteitsoptimalisering de oudere verbinding, die in dit geval het verband tussen de identiteit van Jane met CRM identiteitskaart namespace en de identiteit met test is<span>@test.

Met algoritme voor identiteitsoptimalisatie worden onjuiste identiteitswaarden zoals bogus-e-mails of telefoonnummers niet verspreid over verschillende identiteitsgrafieken.

![slechte e-mail](../images/identity-settings/bad-email.png)

### Anonieme gebeurtenisassociatie

ECIDs slaat unauthenticated (anonieme) gebeurtenissen op, terwijl identiteitskaart van CRM voor authentiek verklaarde gebeurtenissen opslaat. In het geval van gedeelde apparaten wordt de ECID (draagster van niet-geverifieerde gebeurtenissen) gekoppeld aan de **laatst geverifieerde gebruiker**.

Bekijk het onderstaande diagram om beter te begrijpen hoe anonieme gebeurtenisassociatie werkt:

* Kevin en Nora delen een tablet.
   * `timestamp=1`: Kevin meldt zich met zijn account aan bij een e-commercewebsite en stelt daarbij zijn CRM-id (aanmeldingsgegevens) en een ECID (browser) in. Op het moment van aanmelding wordt Kevin nu beschouwd als de laatst geverifieerde gebruiker.
   * `timestamp=2`: Nora meldt zich aan bij een e-commercewebsite gebruikend haar rekening, daardoor plaatsend haar identiteitskaart van CRM (login informatie) en zelfde ECID. Op het moment van aanmelding wordt Nora nu beschouwd als de laatst geverifieerde gebruiker.
   * `timestamp=3`: Kevin gebruikt het tablet om door de e-commercewebsite te bladeren, maar meldt zich niet aan met zijn account. Kevin&#39;s browseractiviteiten worden vervolgens opgeslagen in de ECID, die op haar beurt aan Nora is gekoppeld omdat ze de laatste geverifieerde gebruiker is. Op dit moment is Nora eigenaar van de anonieme gebeurtenissen.
      * Totdat Kevin zich opnieuw aanmeldt, wordt het samengevoegde profiel van Nora gekoppeld aan alle niet-geverifieerde gebeurtenissen die op basis van de ECID zijn opgeslagen (waarbij ECID de primaire identiteit is).
   * `timestamp=4`: Kevin meldt zich voor de tweede keer aan. Op dit punt wordt hij opnieuw de laatste geverifieerde gebruiker en is hij nu ook eigenaar van de niet-geverifieerde gebeurtenissen:
      * Voor zijn eerste aanmelding vóór `timestamp=1`; en
      * Om het even welke activiteiten hij of Nora deed terwijl het doorbladeren anoniem in-tussen Kevin&#39;s eerste en tweede logins.

![non-event-association](../images/identity-settings/anon-event-association.png)


## Volgende stappen

Lees de volgende documentatie voor meer informatie over koppelingsregels voor identiteitsgrafieken:

* [Overzicht van regels voor identiteitsgrafiek](./overview.md)
* [Voorbeeldscenario&#39;s voor het configureren van identiteitsgrafiek-koppelingsregels](./example-scenarios.md)
* [Logica voor identiteitskoppeling](./identity-linking-logic.md)
* [Identiteitsservice en realtime klantprofiel](identity-and-profile.md)

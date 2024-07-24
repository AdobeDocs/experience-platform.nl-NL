---
title: Voorbeeldconfiguraties
description: Leer over voorbeeldconfiguraties met het gebruiken van het hulpmiddel van de grafieksimulatie.
badge: Beta
source-git-commit: 536770d0c3e7e93921fe40887dafa5c76e851f5e
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 2%

---

# Voorbeelden van grafiekconfiguraties

>[!AVAILABILITY]
>
>De regels voor identiteitsgrafiekkoppelingen staan momenteel in bèta. Neem contact op met het accountteam van de Adobe voor meer informatie over de deelnemingscriteria. De functie en documentatie kunnen worden gewijzigd.

>[!NOTE]
>
>* &#39;CRMID&#39; en &#39;loginID&#39; zijn aangepaste naamruimten. In dit document is &#39;CRMID&#39; een persoon-id en is &#39;loginID&#39; een aanmeldings-id die aan een bepaalde persoon is gekoppeld.
>* Als u de voorbeeldgrafiekscenario&#39;s wilt simuleren die in dit document worden beschreven, moet u eerst twee aangepaste naamruimten maken, een met het identiteitssymbool &quot;CRMID&quot; en een ander met het identiteitssymbool &quot;loginID&quot;. Identiteitssymbolen zijn hoofdlettergevoelig.

Dit document schetst voorbeeldgrafiekconfiguraties van gemeenschappelijke scenario&#39;s die u zou kunnen ontmoeten wanneer het werken met identiteitsgegevens.

## alleen CRMID

Dit is een voorbeeld van een eenvoudig implementatiescenario waarbij online gebeurtenissen (CRMID en ECID) worden opgenomen en offlinegebeurtenissen (profielrecords) alleen tegen de CRMID worden opgeslagen.

**Implementatie:**

| Gebruikte naamruimten | Webgedragsverzamelingsmethode |
| --- | --- |
| CRMID, ECID | Web SDK |

**Gebeurtenissen:**

U kunt dit scenario in grafieksimulatie tot stand brengen door de volgende gebeurtenissen aan tekstwijze te kopiëren:

* CRMID: Tom, ECID: 111

**configuratie van het Algoritme:**

U kunt dit scenario in grafieksimulatie tot stand brengen door de volgende opstelling voor uw algoritmeconfiguratie te vormen:

| Prioriteit | Weergavenaam | Identiteitstype | Uniek per grafiek |
| ---| --- | --- | --- |
| 1 | CRMID | CROSS_DEVICE | Ja |
| 2 | ECID | COOKIE | Nee |

**Primaire identiteitsselectie voor Real-Time Profiel van de Klant:**

Binnen de context van deze configuratie, zal de primaire identiteit als volgt worden bepaald:

| Verificatiestatus | Naamruimte(s) in gebeurtenissen | Primaire identiteit |
| --- | --- | --- |
| Geverifieerd | CRMID, ECID | CRMID |
| Niet geverifieerd | ECID | ECID |

>[!BEGINTABS]

>[!TAB  Ideaal single-person grafiekscenario ]

Hieronder ziet u een voorbeeld van een ideale eenpersoonsgrafiek, waarbij CRMID uniek is en de hoogste prioriteit krijgt.

![ A gesimuleerd voorbeeld van een ideale single-person grafiek, waar CRMID uniek is en de hoogste prioriteit wordt gegeven.](../images/graph-examples/crmid_only_single.png)

>[!TAB  multi-person grafiekscenario ]

Hier volgt een voorbeeld van een grafiek met meerdere personen. Dit voorbeeld toont een &quot;gedeeld apparaat&quot;scenario, waar er twee CRMIDs zijn en met de oudere gevestigde verbinding wordt verwijderd.

![ een gesimuleerd voorbeeld van een multi-persoongrafiek. Dit voorbeeld toont een gedeeld apparatenscenario, waar er twee CRMIDs zijn en de oudere gevestigde verbinding wordt verwijderd.](../images/graph-examples/crmid_only_multi.png)

>[!ENDTABS]

## CRMID met gehashte e-mail

In dit scenario wordt een CRMID opgenomen die zowel online (ervaringsgebeurtenis) als offline (profielrecord) gegevens vertegenwoordigt. Dit scenario impliceert ook de opname van een gehakt e-mail, die een andere namespace vertegenwoordigt die in de het recorddataset van CRM samen met CRMID wordt verzonden.

**Implementatie:**

| Gebruikte naamruimten | Webgedragsverzamelingsmethode |
| --- | --- |
| CRMID, Email_LC_SHA256, ECID | Web SDK |

**Gebeurtenissen:**

U kunt dit scenario in grafieksimulatie tot stand brengen door de volgende gebeurtenissen aan tekstwijze te kopiëren:

* CRMID: Tom, Email_LC_SHA256: tom<span>@acme.com
* CRMID: Tom, ECID: 111
* CRMID: zomer, email_LC_SHA256: zomer <span>@acme.com
* CRMID: Summer, ECID: 222

**configuratie van het Algoritme:**

U kunt dit scenario in grafieksimulatie tot stand brengen door de volgende opstelling voor uw algoritmeconfiguratie te vormen:

| Prioriteit | Weergavenaam | Identiteitstype | Uniek per grafiek |
| ---| --- | --- | --- |
| 1 | CRMID | CROSS_DEVICE | Ja |
| 2 | E-mails (SHA256, verlaagd) | Email | Nee |
| 3 | ECID | COOKIE | Nee |

**Primaire identiteitsselectie voor Profiel:**

Binnen de context van deze configuratie, zal de primaire identiteit als volgt worden bepaald:

| Verificatiestatus | Naamruimte(s) in gebeurtenissen | Primaire identiteit |
| --- | --- | --- |
| Geverifieerd | CRMID, ECID | CRMID |
| Niet geverifieerd | ECID | ECID |

>[!BEGINTABS]

>[!TAB  Ideaal single-person grafiekscenario ]

![ In dit voorbeeld, worden twee afzonderlijke grafieken geproduceerd, elk die een enig-persoonentiteit vertegenwoordigen.](../images/graph-examples/crmid_hashed_single.png)

>[!TAB  multi-persoongrafiek: gedeeld apparaat ]

![ In dit voorbeeld, toont de gesimuleerde grafiek een &quot;gedeeld apparaat&quot;scenario omdat zowel Tom als Zomer met zelfde ECID worden geassocieerd.](../images/graph-examples/crmid_hashed_shared_device.png)

>[!TAB  multi-persoongrafiek: niet-unieke e-mail ]

![ Dit scenario is gelijkaardig aan een &quot;gedeeld apparaat&quot;scenario. Nochtans, in plaats van het hebben van de persoonentiteiten ECID delen, zijn zij in plaats daarvan geassocieerd met het zelfde e-mailrekening.](../images/graph-examples/crmid_hashed_nonunique_email.png)

>[!ENDTABS]

## CRMID met gehashte e-mail, gehashte telefoon, GAID, en IDFA

Dit scenario is vergelijkbaar met het vorige scenario. Nochtans, in dit scenario, worden gehakt e-mail en de telefoon duidelijk als identiteiten om in segmentovereenkomst te gebruiken.

**Implementatie:**

| Gebruikte naamruimten | Webgedragsverzamelingsmethode |
| --- | --- |
| CRMID, Email_LC_SHA256, Phone_SHA256, GAID, IDFA, ECID | Web SDK |

**Gebeurtenissen:**

U kunt dit scenario in grafieksimulatie tot stand brengen door de volgende gebeurtenissen aan tekstwijze te kopiëren:

* CRMID: Tom, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
* CRMID: Tom, ECID: 111
* CRMID: Tom, ECID: 222, IDFA: A-A-A
* CRMID: Summer, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
* CRMID: zomer, ECID: 333
* CRMID: zomer, ECID: 444, GAID:B-B-B

**configuratie van het Algoritme:**

U kunt dit scenario in grafieksimulatie tot stand brengen door de volgende opstelling voor uw algoritmeconfiguratie te vormen:

| Prioriteit | Weergavenaam | Identiteitstype | Uniek per grafiek |
| ---| --- | --- | --- |
| 1 | CRMID | CROSS_DEVICE | Ja |
| 2 | E-mails (SHA256, verlaagd) | Email | Nee |
| 3 | Telefoon (SHA256) | Telefoon | Nee |
| 4 | Google-advertentie-ID (GAID) | APPARAAT | Nee |
| 5 | Apple IDFA (ID voor Apple) | APPARAAT | Nee |
| 6 | ECID | COOKIE | Nee |

**Primaire identiteitsselectie voor Profiel:**

Binnen de context van deze configuratie, zal de primaire identiteit als volgt worden bepaald:

| Verificatiestatus | Naamruimte(s) in gebeurtenissen | Primaire identiteit |
| --- | --- | --- |
| Geverifieerd | CRMID, IDFA, ECID | CRMID |
| Geverifieerd | CRMID, GAID, ECID | CRMID |
| Geverifieerd | CRMID, ECID | CRMID |
| Niet geverifieerd | GAID, ECID | GAID |
| Niet geverifieerd | IDFA, ECID | IDFA |
| Niet geverifieerd | ECID | ECID |

>[!BEGINTABS]

>[!TAB  Ideaal single-person grafiekscenario ]

![](../images/graph-examples/crmid_hashed_single_seg_match.png)

>[!ENDTABS]

<!-- 
## Single CRMID with multiple login IDs (simple)

In this scenario, there is a single CRMID that represents a person entity. However, a person entity may have multiple login identifiers:

* A given person entity can have different account account types (personal vs. business, account by state, account by brand, etc.)
* A given person entity may use different email addresses for any number of accounts.

Therefore, **it is crucial that the CRMID is always sent for every user**. Failure to do so may result in a "dangling" login ID scenario, where a single person entity is assumed to be sharing a device with another person.

**Implementation:**

| Namespaces used | Web behavior collection method |
| --- | --- |
| CRMID, loginID, ECID | Web SDK |

**Events:**

You can create this scenario in graph simulation by copying the following events to text mode:

* CRMID: John, loginID: ID_A
* CRMID: John, loginID: ID_B
* loginID: ID_A, ECID: 111
* CRMID: Jane, loginID: ID_C
* CRMID: Jane, loginID: ID_D
* loginID: ID_C, ECID: 222

**Algorithm configuration:**

You can create this scenario in graph simulation by configuring the following setup for your algorithm configuration:

| Priority | Display name | Identity symbol | Identity type | Unique per graph |
| ---| --- | --- | --- | --- |
| 1 | CRMID | CRMID | CROSS_DEVICE | Yes |
| 2 | loginID | loginID | CROSS_DEVICE | No |
| 3 | ECID | ECID | COOKIE | No |

## Single CRMID with multiple login IDs (complex)

In this scenario, there is a single CRMID that represents a person entity. However, a person entity may have multiple login identifiers:

* A given person entity can have different account account types (personal vs. business, account by state, account by brand, etc.)
* A given person entity may use different email addresses for any number of accounts.

The case of "dangling" loginID also applies for this scenario.

**Implementation:**

| Namespaces used | Web behavior collection method |
| --- | --- |
| CRMID, Email_LC_SHA256, Phone_SHA256, loginID, ECID, AAID | Adobe Analytics source connector |


**Events:**

You can create this scenario in graph simulation by copying the following events to text mode:

* CRMID: John, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
* CRMID: John, loginID: ID_A
* CRMID: John, loginID: ID_B
* loginID:ID_A, ECID: 111, AAID: AAA
* CRMID: Jane, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
* CRMID: Jane, loginID: ID_C
* CRMID: Jane, loginID: ID_D
* loginID: ID_C, ECID: 222, AAID: BBB

**Algorithm configuration:**

You can create this scenario in graph simulation by configuring the following setup for your algorithm configuration:

| Priority | Display name | Identity symbol | Identity type | Unique per graph |
| ---| --- | --- | --- | --- |
| 1 | CRMID | CRMID | CROSS_DEVICE | Yes |
| 2 | Email_LC_SHA256 | Email_LC_SHA256 | EMAIL | No |
| 3 | Phone_SHA256 | Phone_SHA256 | PHONE | No |
| 4 | loginID | loginID | CROSS_DEVICE | No |
| 5 | ECID | ECID | COOKIE | No |
| 6 | AAID | AAID | COOKIE | No |
 -->

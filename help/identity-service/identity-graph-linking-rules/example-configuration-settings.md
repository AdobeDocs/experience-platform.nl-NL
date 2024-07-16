---
title: Voorbeeldconfiguraties
description: Leer over voorbeeldconfiguraties met het gebruiken van het hulpmiddel van de grafieksimulatie.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: ba72abd9febc6d9e6491748519199b54a26ae1c5
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 5%

---

# Voorbeelden van grafiekconfiguraties

>[!NOTE]
>
>&#39;CRM ID&#39; is een aangepaste naamruimte. Daarom vereisen de voorbeelden hieronder u om een douanenamespace met een vertoningsnaam en identiteitssymbool van &quot;identiteitskaart van CRM te creëren.

De volgende sectievoorbeelden van grafiekscenario&#39;s u met de Simulatie van de Grafiek zou kunnen ontmoeten.

## Alleen CRM-id

Gebeurtenissen:

* CRM-ID: Tom, ECID: 111

Algoritmconfiguratie:

| Prioriteit | Weergavenaam | Identiteitssymbool | Identiteitstype | Uniek per grafiek |
| ---| --- | --- | --- | --- |
| 1 | CRM-id | CRM-id | CROSS_DEVICE | Ja |
| 2 | ECID | ECID | COOKIE | NEE |

+++Selecteren om gesimuleerde grafiek weer te geven

+++

## CRM-id met gehashte e-mail

In dit scenario wordt een CRM-id opgenomen die zowel online (ervaringsgebeurtenis) als offline (profielrecord) gegevens vertegenwoordigt. Dit scenario impliceert ook de opname van een gehakt e-mail, die een andere namespace vertegenwoordigt die in de het recorddataset van CRM samen met identiteitskaart van CRM wordt verzonden.

Gebeurtenissen:

* CRM-id: Tom, Email_LC_SHA256: tom<span>@acme.com
* CRM-ID: Tom, ECID: 111
* CRM-id: zomer, email_LC_SHA256: zomer<span>@acme.com
* CRM-ID: Summer, ECID: 222

Algoritmconfiguratie:

| Prioriteit | Weergavenaam | Identiteitssymbool | Identiteitstype | Uniek per grafiek |
| ---| --- | --- | --- | --- |
| 1 | CRM-id | CRM-id | CROSS_DEVICE | Ja |
| 2 | E-mails (SHA256, verlaagd) | Email_LC_SHA256 | Email | NEE |
| 3 | ECID | ECID | COOKIE | NEE |

+++Selecteren om gesimuleerde grafiek weer te geven

+++

## CRM-id met hashed-e-mail, hashtelefoon, GAID en IDFA

Gebeurtenissen:

* CRM-id: Tom, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
* CRM-ID: Tom, ECID: 111
* CRM-ID: Tom, ECID: 222, IDFA: A-A-A
* CRM-id: Summer, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
* CRM-ID: Summer, ECID: 333
* CRM-ID: Summer, ECID: 444, GAID:B-B-B

Algoritmconfiguratie:

| Prioriteit | Weergavenaam | Identiteitssymbool | Identiteitstype | Uniek per grafiek |
| ---| --- | --- | --- | --- |
| 1 | CRM-id | CRM-id | CROSS_DEVICE | Ja |
| 2 | E-mails (SHA256, verlaagd) | Email_LC_SHA256 | Email | NEE |
| 3 | Telefoon (SHA256) | Phone_SHA256 | Telefoon | NEE |
| 4 | Google-advertentie-ID (GAID) | GAID | APPARAAT | NEE |
| 5 | Apple IDFA (ID voor Apple) | IDFA | APPARAAT | NEE |
| 6 | ECID | ECID | COOKIE | NEE |

+++Selecteren om gesimuleerde grafiek weer te geven

+++
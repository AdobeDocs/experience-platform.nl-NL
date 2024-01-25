---
title: Identity Service Linking Logic
description: Leer hoe de Dienst van de Identiteit verschillende identiteiten verbindt om een uitvoerige mening van een klant tot stand te brengen.
exl-id: 1c958c0e-0777-48db-862c-eb12b2e7a03c
source-git-commit: 2b6700b2c19b591cf4e60006e64ebd63b87bdb2a
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 0%

---

# Identity Service linking-logica

Er wordt een koppeling tussen twee identiteiten tot stand gebracht wanneer de naamruimte van de identiteit en de identiteitswaarden overeenkomen.

Er zijn twee soorten identiteiten die aan elkaar worden gekoppeld:

* **Profielrecords**: Deze identiteiten komen gewoonlijk van CRM-systemen.
* **Experience Events**: Deze identiteiten komen gewoonlijk uit implementatie WebSDK of de bron van Adobe Analytics.

## Semantische betekenis van het tot stand brengen van verbindingen

Een identiteit vertegenwoordigt een echte entiteit. Als er een verband tussen twee identiteiten is vastgesteld, betekent dit dat de twee identiteiten aan elkaar zijn gekoppeld. Hieronder volgen enkele voorbeelden die dit concept illustreren:

| Actie | Koppelingen tot stand gebracht | Betekenis |
| --- | --- | --- |
| Een eindgebruiker meldt zich aan gebruikend een computer. | CRM-id en ECID zijn aan elkaar gekoppeld. | Een persoon (CRM-id) heeft een apparaat met een browser (ECID). |
| Een eindgebruiker bladert anoniem met een iPhone. | IDFA is gekoppeld aan ECID. | Het Apple-hardwareapparaat (IDFA), zoals een iPhone, is gekoppeld aan de browser (ECID). |
| Een eindgebruiker meldt zich aan gebruikend Google Chrome, en toen Firefox. | CRM-id is gekoppeld aan twee verschillende ECID&#39;s. | Een persoon (CRM-id) is gekoppeld aan twee webbrowsers (**Opmerking**: Elke browser heeft een eigen ECID). |
| Een gegevensingenieur neemt een verslag van CRM op dat twee gebieden duidelijk als identiteit omvat: identiteitskaart van CRM en E-mail. | CRM-id en e-mail zijn gekoppeld. | Een persoon (CRM-id) is gekoppeld aan het e-mailadres. |

## Understanding the Identity Service linking logic

Een identiteit bestaat uit een naamruimte van een identiteit en een identiteitswaarde.

* Een naamruimte voor identiteit is de context van een bepaalde identiteitswaarde die moet worden gebruikt. Veelvoorkomende voorbeelden van naamruimten zijn CRM-id, e-mail en telefoon.
* Een identiteitswaarde is de tekenreeks die een echte entiteit vertegenwoordigt. Bijvoorbeeld: &quot;julien<span>@acme.com&quot; kan een identiteitswaarde voor een naamruimte E-mail zijn en 555-555-1234 kan een overeenkomstige identiteitswaarde voor een naamruimte van de Telefoon zijn.

>[!TIP]
>
>Naamruimte is belangrijk omdat zonder naamruimte de identiteitswaarde zijn context verliest en niet genoeg informatie heeft om identiteiten met succes aan te passen.

Zie de volgende diagrammen voor een visuele vertegenwoordiging van hoe de Dienst die van de Identiteit verbindt logica werkt:

>[!BEGINTABS]

>[!TAB Bestaande grafiek]

Stel dat u een bestaande identiteitsgrafiek hebt met drie gekoppelde identiteiten:

* PHONE:(555)-555-1234
* EMAIL:julien<span>@acme.com
* CRM-ID:60013ABC

![bestaande grafiek](../images/identity-settings/existing-graph.png)

>[!TAB Binnenkomende gegevens]

Een paar identiteiten worden opgenomen in uw grafiek en dit paar bevat:

* CRM-ID:60013ABC
* ECID:100066526

![binnenkomende gegevens](../images/identity-settings/incoming-data.png)

>[!TAB Bijgewerkte grafiek]

De Dienst van de identiteit erkent dat CRM ID:60013ABC reeds binnen uw grafiek bestaat, en zo verbindt slechts nieuwe ECID

![bijgewerkte grafiek](../images/identity-settings/updated-graph.png)

>[!ENDTABS]

## Klantenscenario

U bent gegevensingenieur en u neemt de volgende dataset van CRM (het verslag van het Profiel) aan Experience Platform op.

| CRM-id** | Telefoon* | E-mail* | Voornaam | Achternaam |
| --- | --- | --- | --- | --- |
| 60013ABC | 555-555-1234 | julien<span>@acme.com | Julien | Smith |
| 31260XYZ | 777-777-6890 | evan<span>@acme.com | Evan | Smith |

>[!NOTE]
>
>* `**` - Denotes-veld dat is gemarkeerd als primaire identiteit.
>* `*` - Denotes-veld dat is gemarkeerd als secundaire identiteit.
>
>Identiteitsdienst maakt geen onderscheid tussen primaire en secundaire identiteit. Zolang een veld is gemarkeerd als een identiteit, wordt het veld ingesloten bij Identiteitsservice.

U hebt WebSDK ook uitgevoerd en een dataset WebSDK (de Gebeurtenis van de Ervaring) met de volgende gegevenslijsten opgenomen:

| Tijdstempel | Identiteiten van de gebeurtenis* | Gebeurtenis |
| --- | --- | --- |
| `t=1` | ECID:38652 | Homepage weergeven |
| `t=2` | ECID:38652, CRM-ID:31260XYZ | Zoeken naar schoenen |
| `t=3` | ECID:44675 | Homepage weergeven |
| `t=4` | ECID:44675, CRM-id: 31260XYZ | Aankoopgeschiedenis weergeven |

De primaire identiteit voor elke gebeurtenis wordt bepaald op basis van [hoe u gegevenselelementtypen configureert](../../tags/extensions/client/web-sdk/data-element-types.md).

>[!NOTE]
>
>* Als u identiteitskaart van CRM als primaire selecteert, dan voor authentiek verklaarde gebeurtenissen (gebeurtenissen met identiteitskaart die identiteitskaart en ECID bevatten) zal een primaire identiteit van identiteitskaart van CRM hebben. Voor niet-geverifieerde gebeurtenissen (gebeurtenissen met alleen de ECID in het identiteitsoverzicht) heeft de primaire identiteit van ECID. Adobe raadt deze optie aan.
>
>* Als u de ECID als primaire id selecteert, ongeacht de verificatiestatus, wordt de ECID de primaire identiteit.

In dit voorbeeld:

* `t=1`, gebruikt een desktopcomputer (ECID:38652) en om de homepage anoniem te bekijken.
* `t=2`gebruikt dezelfde desktopcomputer, aangemeld (CRM-id:31260XYZ) en vervolgens gezocht naar schoenen.
   * Zodra een gebruiker wordt het programma geopend, verzendt de gebeurtenis zowel ECID als identiteitskaart van CRM naar de Dienst van de Identiteit.
* `t=3`, gebruikt een laptopcomputer (ECID:44675) en anoniem gebladerd.
* `t=4`, gebruikte dezelfde laptopcomputer, aangemeld (CRM-id: 31260XYZ) en bekeken de aankoopgeschiedenis.


>[!BEGINTABS]

>[!TAB timestamp=0]

At `timestamp=0`, hebt u twee identiteitsgrafieken voor twee verschillende klanten. Beide zijn elk vertegenwoordigd door drie verbonden identiteiten.

| | CRM-id | Email | Telefoon |
| --- | --- | --- | --- |
| Klant één | 60013ABC | julien<span>@acme.com | 555-555-1234 |
| Klant twee | 31260XYZ | evan<span>@acme.com | 777-777-6890 |

![timestamp-zero](../images/identity-settings/timestamp-zero.png)

>[!TAB timestamp=1]

At `timestamp=1`, gebruikt een klant een laptop om uw e-commercewebsite te bezoeken, uw homepage te bekijken, en anoniem te doorbladeren. Deze anonieme browsergebeurtenis wordt ECID:38652 genoemd. Omdat de Dienst van de Identiteit slechts gebeurtenissen met minstens twee identiteiten opslaat, wordt deze informatie niet opgeslagen.

![timestamp-one](../images/identity-settings/timestamp-one.png)

>[!TAB timestamp=2]

At `timestamp=2`, gebruikt een klant dezelfde laptop om uw e-commercewebsite te bezoeken. Ze melden zich aan met hun gebruikersnaam en wachtwoord en zoeken naar schoenen. Identiteitsdienst identificeert de rekening van de klant wanneer zij login omdat het aan hun identiteitskaart van CRM beantwoordt: 31260XYZ. Daarnaast heeft Identity Service ECID:38562 betrekking op CRM ID:31260XYZ omdat beide dezelfde browser gebruiken op hetzelfde apparaat.

![timestamp-two](../images/identity-settings/timestamp-two.png)

>[!TAB timestamp=3]

At `timestamp=3` een klant gebruikt een tablet om uw e-commercewebsite te bezoeken en anoniem te doorbladeren. Deze anonieme browsergebeurtenis wordt aangeduid als ECID:44675. Omdat de Dienst van de Identiteit slechts gebeurtenissen met minstens twee identiteiten opslaat, wordt deze informatie niet opgeslagen.

![timestamp-three](../images/identity-settings/timestamp-three.png)

>[!TAB timestamp=4]

At `timestamp=4`, gebruikt een klant dezelfde tablet, meldt u zich aan bij zijn account (CRM-id:31260XYZ) en bekijkt de aankoopgeschiedenis. Deze gebeurtenis koppelt hun CRM-id:31260XYZ aan de cookie-id die is toegewezen aan anonieme browseractiviteit, ECID:44675 en koppelt ECID:44675 aan de twee identiteitsgrafieken van de klant.

![timestamp-four](../images/identity-settings/timestamp-four.png)

>[!ENDTABS]

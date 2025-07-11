---
solution: Experience Platform
title: Algemeen veld met voorkeursgegevens voor marketing met abonnementen
description: Meer informatie over het veld Algemene marketingvoorkeuren met XDM-gegevenstypen voor abonnementen.
exl-id: 170ea6ca-77fc-4b0a-87f9-6d4b6f32d953
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---

# [!UICONTROL Generic Marketing Preference Field with Subscriptions] gegevenstype

[!UICONTROL Generic Marketing Preference Field with Subscriptions] is een standaard XDM gegevenstype dat de selectie van een klant voor een bepaalde marketing voorkeur beschrijft.

>[!NOTE]
>
>Dit gegevenstype is bedoeld om te worden gebruikt om de structuur van de toestemmingsregelingen van uw organisatie aan te passen gebruikend de [[!UICONTROL Consents and Preferences] gebiedsgroep ](../field-groups/profile/consents.md) als basislijn.
>
>Als u geen a `subscriptions` kaart voor een bepaald marketing voorkeurgebied vereist, kunt u het [ basis marketing gebiedsgegevenstype ](./marketing-field.md) in plaats daarvan gebruiken.

![](../images/data-types/marketing-field-subscriptions.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `reason` | String | Wanneer een klant kiest uit een geval van het marketinggebruik, vertegenwoordigt dit koordgebied de reden waarom de klant uit opteerde. |
| `subscriptions` | Kaart | Een kaart van klant marketing voorkeur voor specifieke abonnementen. Zie de sectie op [ abonnementen ](#subscriptions) voor meer informatie. |
| `time` | DateTime | Een tijdstempel volgens ISO 8601 van het tijdstip waarop de voorkeur voor het in de handel brengen werd gewijzigd, indien van toepassing. |
| `val` | String | De door de klant opgegeven voorkeurskeuze voor dit marketinggeval. Zie de [ volgende sectie ](#val) voor erkende waarden en definities. |

{style="table-layout:auto"}

## `val` {#val}

In de volgende tabel worden de toegestane waarden voor `val` weergegeven:

| Waarde | Titel | Beschrijving |
| --- | --- | --- |
| `y` | Ja (opt-in) | De klant heeft zich aangemeld voor de voorkeur. Met andere woorden, stemmen zij **&#x200B;**&#x200B;toe met het gebruik van hun gegevens zoals die door de voorkeur in kwestie worden vermeld. |
| `n` | Nee (opt-out) | De klant heeft ervoor gekozen deze voorkeur niet toe te passen. Met andere woorden, zij **stemmen niet** toe met het gebruik van hun gegevens zoals die door de voorkeur in kwestie worden vermeld. |
| `p` | Verificatie in behandeling | Het systeem heeft nog geen definitieve voorkeurswaarde ontvangen. Dit wordt het vaakst gebruikt als deel van een toestemming die uit twee stappen controle vereist. Als een klant bijvoorbeeld ervoor kiest e-mailberichten te ontvangen, wordt die toestemming ingesteld op `p` totdat de klant een koppeling in een e-mailbericht selecteert om te controleren of hij het juiste e-mailadres heeft opgegeven. Op dat moment wordt de toestemming bijgewerkt naar `y` .<br><br> als deze voorkeur geen twee-reeks controleproces gebruikt, dan kan `p` keus worden gebruikt om erop te wijzen dat de klant nog niet op de toestemmingsherinnering heeft gereageerd. U kunt bijvoorbeeld automatisch de waarde instellen op `p` op de eerste pagina van een website, voordat de klant heeft gereageerd op de bevestigingsprompt. In rechtsgebieden waarvoor geen uitdrukkelijke toestemming vereist is, kunt u deze ook gebruiken om aan te geven dat de klant niet expliciet heeft aangegeven dat de toestemming is geweigerd (met andere woorden, er wordt aangenomen dat de toestemming is verleend). |
| `u` | Onbekend | De voorkeursgegevens van de klant zijn onbekend. |
| `dy` | Standaard van Ja (opt-in) | De klant heeft zelf geen waarde voor de toestemming opgegeven en wordt standaard als een opt-in (&quot;Yes&quot;) behandeld. Met andere woorden, instemming wordt verondersteld tot de klant anders aangeeft.<br><br> Merk op dat als de wetten of de veranderingen in het privacybeleid van uw bedrijf in veranderingen in de gebreken van sommige of alle gebruikers resulteren, u alle profielen manueel moet bijwerken die standaardwaarden bevatten. |
| `dn` | Standaard van Geen (opt-out) | De klant heeft zelf geen waarde voor de toestemming opgegeven en wordt standaard als een &quot;nee&quot; behandeld. Met andere woorden, de klant wordt verondersteld toestemming te hebben geweigerd tot zij anders aangeven.<br><br> Merk op dat als de wetten of de veranderingen in het privacybeleid van uw bedrijf in veranderingen in de gebreken van sommige of alle gebruikers resulteren, u alle profielen manueel moet bijwerken die standaardwaarden bevatten. |
| `LI` | Gewettigd belang | Het legitieme zakelijke belang om deze gegevens voor het opgegeven doel te verzamelen en te verwerken, weegt zwaarder dan de potentiële schade die het voor het individu oplevert. |
| `CT` | Slinken | De verzameling van gegevens voor het opgegeven doel is vereist om te voldoen aan contractuele verplichtingen met de betrokkene. |
| `CP` | Naleving van een wettelijke verplichting | De verzameling van gegevens voor het gespecificeerde doel is vereist om te voldoen aan de wettelijke verplichtingen van het bedrijf. |
| `VI` | vitaal belang van de individuele | Het verzamelen van gegevens voor het opgegeven doel is vereist om de vitale belangen van het individu te beschermen. |
| `PI` | Openbaar belang | Het verzamelen van gegevens voor het specifieke doel is vereist om een taak van algemeen belang of in de uitoefening van het openbaar gezag uit te voeren. |

{style="table-layout:auto"}

## `subscriptions` {#subscriptions}

Sommige ondernemingen staan klanten toe om binnen voor verschillende abonnementen te kiezen die met een bepaald marketing kanaal worden geassocieerd. Een bankbedrijf kan bijvoorbeeld klanten toestaan om te abonneren op telefoonwaarschuwingen voor te veel opgenomen rekeningen, of verkoopoproepen voor het indienen van een loyaliteitsprogramma ontvangen.

De volgende JSON vertegenwoordigt een voorbeeld marketing gebied voor een telefoonvraag marketing kanaal dat een `subscriptions` kaart bevat. Elke sleutel in het `subscriptions` -object vertegenwoordigt een individueel abonnement op het marketingkanaal. Elk abonnement bevat op zijn beurt een aanmeldingswaarde (`val`).

```json
"email-marketing-field": {
  "val": "y",
  "time": "2019-01-01T15:52:25+00:00",
  "subscriptions": {
    "loyalty-offers": {
      "val": "y",
      "type": "sales",
      "topics": ["discounts", "early-access"],
      "subscribers": {
        "jdoe@example.com": {
          "time": "2019-01-01T15:52:25+00:00",
          "source": "website"
        }
      }
    },
    "newsletters": {
      "val": "y",
      "type": "advertising",
      "topics": ["hardware"],
      "subscribers": {
        "jdoe@example.com": {
          "time": "2021-01-01T08:32:53+07:00",
          "source": "website"
        },
        "tparan@example.com": {
          "time": "2020-02-03T07:54:21+07:00",
          "source": "call center"
        }
      }
    }
  }
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `val` | De [ toestemmingswaarde ](#val) voor het abonnement. |
| `type` | Het abonnementstype. Dit kan elke beschrijvende tekenreeks zijn, op voorwaarde dat deze 15 tekens of minder is. |
| `topics` | Een array van tekenreeksen die de gebieden vertegenwoordigen waarop een klant zich heeft geabonneerd, en die kan worden gebruikt om relevante inhoud te verzenden. |
| `subscribers` | Een optioneel veld van het type map dat een set id&#39;s vertegenwoordigt (zoals e-mailadressen of telefoonnummers) die zijn geabonneerd op een bepaald abonnement. Elke sleutel in dit object vertegenwoordigt de id in kwestie en bevat twee subeigenschappen: <ul><li>`time`: Een tijdstempel volgens ISO 8601 van het moment waarop de identiteit is geabonneerd, indien van toepassing.</li><li>`source`: De bron waarvan de abonnee afkomstig is. Dit kan elke beschrijvende tekenreeks zijn, op voorwaarde dat deze 15 tekens of minder is.</li></ul> |

{style="table-layout:auto"}

## Aanvullende bronnen

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)

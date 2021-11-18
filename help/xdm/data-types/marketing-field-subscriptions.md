---
solution: Experience Platform
title: Algemeen veld met voorkeursgegevens voor marketing met abonnementen
topic-legacy: overview
description: Dit document biedt een overzicht van het veld Algemene marketingvoorkeur met XDM-gegevenstypen voor abonnementen.
exl-id: 170ea6ca-77fc-4b0a-87f9-6d4b6f32d953
source-git-commit: 0f39e9237185b49417f2af8dfc288ab1420cccae
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 1%

---

# [!UICONTROL Generic Marketing Preference Field with Subscriptions] gegevenstype

[!UICONTROL Generic Marketing Preference Field with Subscriptions] is een standaard XDM gegevenstype dat de selectie van een klant voor een bepaalde marketing voorkeur beschrijft.

>[!NOTE]
>
>Dit gegevenstype is bedoeld om de structuur van de toestemmingsschema&#39;s van uw organisatie aan te passen gebruikend [[!UICONTROL Consents and Preferences] veldgroep](../field-groups/profile/consents.md) als basislijn.
>
>Als u geen `subscriptions` kaart voor een bepaald voorkeursveld voor marketing, kunt u de optie [basistabel voor het in de handel brengen, gegevenstype](./marketing-field.md) in plaats daarvan.

![](../images/data-types/marketing-field-subscriptions.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `reason` | Tekenreeks | Wanneer een klant kiest uit een geval van het marketinggebruik, vertegenwoordigt dit koordgebied de reden waarom de klant uit opteerde. |
| `subscriptions` | Kaart | Een kaart van klant marketing voorkeur voor specifieke abonnementen. Zie de sectie over [abonnementen](#subscriptions) voor meer informatie . |
| `time` | DateTime | Een tijdstempel volgens ISO 8601 van het tijdstip waarop de voorkeur voor het in de handel brengen werd gewijzigd, indien van toepassing. |
| `val` | Tekenreeks | De door de klant opgegeven voorkeursoptie voor dit marketinggeval. Zie de [volgende sectie](#val) voor aanvaarde waarden en definities. |

{style=&quot;table-layout:auto&quot;}

## `val` {#val}

In de volgende tabel worden de toegestane waarden voor `val`:

| Waarde | Titel | Beschrijving |
| --- | --- | --- |
| `y` | Ja (opt-in) | De klant heeft zich aangemeld voor de voorkeur. Met andere woorden: **do** toestemming voor het gebruik van hun gegevens zoals aangegeven door de betrokken voorkeur. |
| `n` | Nee (opt-out) | De klant heeft ervoor gekozen deze voorkeur niet toe te passen. Met andere woorden: **niet** toestemming voor het gebruik van hun gegevens zoals aangegeven door de betrokken voorkeur. |
| `p` | Verificatie in behandeling | Het systeem heeft nog geen definitieve voorkeurswaarde ontvangen. Dit wordt het vaakst gebruikt als deel van een toestemming die uit twee stappen controle vereist. Als een klant bijvoorbeeld ervoor kiest e-mailberichten te ontvangen, wordt deze toestemming ingesteld op `p` totdat zij een koppeling in een e-mail selecteren om te controleren of zij het juiste e-mailadres hebben opgegeven, waarna de toestemming wordt bijgewerkt naar `y`.<br><br>Als bij deze voorkeur geen verificatieproces in twee sets wordt gebruikt, wordt het `p` in plaats daarvan kan de keuze worden gebruikt om aan te geven dat de klant nog niet heeft gereageerd op de bevestigingsprompt. U kunt de waarde bijvoorbeeld automatisch instellen op `p` op de eerste pagina van een website, voordat de klant heeft gereageerd op de vraag naar toestemming. In rechtsgebieden waarvoor geen uitdrukkelijke toestemming vereist is, kunt u deze ook gebruiken om aan te geven dat de klant niet expliciet heeft aangegeven dat de toestemming is geweigerd (met andere woorden, er wordt aangenomen dat de toestemming is verleend). |
| `u` | Onbekend | De voorkeursgegevens van de klant zijn onbekend. |
| `dy` | Standaard van Ja (opt-in) | De klant heeft zelf geen waarde voor de toestemming opgegeven en wordt standaard als een opt-in (&quot;Yes&quot;) behandeld. Met andere woorden, instemming wordt verondersteld tot de klant anders aangeeft.<br><br>Merk op dat als wetten of veranderingen in het privacybeleid van uw bedrijf in veranderingen in de gebreken van sommige of alle gebruikers resulteren, u alle profielen manueel moet bijwerken die standaardwaarden bevatten. |
| `dn` | Standaard van Geen (opt-out) | De klant heeft zelf geen waarde voor de toestemming opgegeven en wordt standaard als een &quot;nee&quot; behandeld. Met andere woorden, de klant wordt verondersteld toestemming te hebben geweigerd tot zij anders aangeven.<br><br>Merk op dat als wetten of veranderingen in het privacybeleid van uw bedrijf in veranderingen in de gebreken van sommige of alle gebruikers resulteren, u alle profielen manueel moet bijwerken die standaardwaarden bevatten. |
| `LI` | Gewettigd belang | Het legitieme zakelijke belang om deze gegevens voor het opgegeven doel te verzamelen en te verwerken, weegt zwaarder dan de potentiële schade die het voor het individu oplevert. |
| `CT` | Slinken | De verzameling van gegevens voor het opgegeven doel is vereist om te voldoen aan contractuele verplichtingen met de betrokkene. |
| `CP` | Naleving van een wettelijke verplichting | De verzameling van gegevens voor het gespecificeerde doel is vereist om te voldoen aan de wettelijke verplichtingen van het bedrijf. |
| `VI` | vitaal belang van de individuele | Het verzamelen van gegevens voor het opgegeven doel is vereist om de vitale belangen van het individu te beschermen. |
| `PI` | Openbaar belang | Het verzamelen van gegevens voor het specifieke doel is vereist om een taak van algemeen belang of in de uitoefening van het openbaar gezag uit te voeren. |

{style=&quot;table-layout:auto&quot;}

## `subscriptions` {#subscriptions}

Sommige ondernemingen staan klanten toe om binnen voor verschillende abonnementen te kiezen die met een bepaald marketing kanaal worden geassocieerd. Een bankbedrijf kan bijvoorbeeld klanten toestaan om te abonneren op telefoonwaarschuwingen voor te veel opgenomen rekeningen, of verkoopoproepen voor het indienen van een loyaliteitsprogramma ontvangen.

De volgende JSON vertegenwoordigt een voorbeeld marketing gebied voor een telefoonvraag marketing kanaal dat een `subscriptions` kaart. Elke toets in het dialoogvenster `subscriptions` object staat voor een individueel abonnement op het marketingkanaal. Elk abonnement bevat op zijn beurt een aanmeldingswaarde (`val`).

```json
"phone-marketing-field": {
  "val": "y",
  "time": "2019-01-01T15:52:25+00:00",
  "subscriptions": {
    "loyalty-offers": {
      "val": "y",
      "type": "sales",
      "subscribers": {
        "123-555-0928": {
          "time": "2019-01-01T15:52:25+00:00",
          "source": "website"
        }
      }
    },
    "overdrawn-account": {
      "val": "y",
      "type": "issues",
      "subscribers": {
        "123-555-0928": {
          "time": "2021-01-01T08:32:53+07:00",
          "source": "website"
        },
        "301-555-1527": {
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
| `type` | Het abonnementstype. Dit kan elke beschrijvende tekenreeks zijn, op voorwaarde dat deze 15 tekens of minder is. |
| `subscribers` | Een optioneel veld van het type map dat een set id&#39;s vertegenwoordigt (zoals e-mailadressen of telefoonnummers) die zijn geabonneerd op een bepaald abonnement. Elke sleutel in dit object vertegenwoordigt de id in kwestie en bevat twee subeigenschappen: <ul><li>`time`: Een tijdstempel volgens ISO 8601 van het tijdstip waarop de identiteit is geabonneerd, indien van toepassing.</li><li>`source`: De bron die de abonnee van voortkwam. Dit kan elke beschrijvende tekenreeks zijn, op voorwaarde dat deze 15 tekens of minder is.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Aanvullende bronnen

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)

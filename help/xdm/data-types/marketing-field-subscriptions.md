---
solution: Experience Platform
title: Algemeen veld met voorkeursgegevens voor marketing met abonnementen
topic: overview
description: Dit document biedt een overzicht van het veld Algemene marketingvoorkeur met XDM-gegevenstypen voor abonnementen.
translation-type: tm+mt
source-git-commit: 8c5ab298bad69305358ae961ebaf7836a90a0eaa
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 1%

---


# [!UICONTROL Generic Marketing Preference Field with Subscriptions] gegevenstype

[!UICONTROL Generic Marketing Preference Field with Subscriptions] is een standaard XDM gegevenstype dat de selectie van een klant voor een bepaalde marketing voorkeur beschrijft.

>[!NOTE]
>
>Dit gegevenstype is bedoeld om de structuur van de toestemmingsregelingen van uw organisatie aan te passen gebruikend [[!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)] mixin](../mixins/profile/consents.md) als basislijn.
>
>Als u geen `subscriptions` kaart voor een bepaald marketing voorkeurgebied vereist, kunt u [basistabel van het marketing gebiedsgegevenstype ](./marketing-field.md) in plaats daarvan gebruiken.

![](../images/data-types/marketing-field-subscriptions.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `reason` | Tekenreeks | Wanneer een klant kiest uit een geval van het marketinggebruik, vertegenwoordigt dit koordgebied de reden waarom de klant uit opteerde. |
| `subscriptions` | Kaart | Een kaart van klant marketing voorkeur voor specifieke abonnementen. Zie de sectie over [abonnementen](#subscriptions) voor meer informatie. |
| `time` | DateTime | Een tijdstempel volgens ISO 8601 van het tijdstip waarop de voorkeur voor het in de handel brengen werd gewijzigd, indien van toepassing. |
| `val` | Tekenreeks | De door de klant opgegeven voorkeursoptie voor dit marketinggeval. Zie [volgende sectie](#val) voor geaccepteerde waarden en definities. |

## `val` {#val}

In de volgende tabel worden de toegestane waarden voor `val` weergegeven:

| Value | Titel | Beschrijving |
| --- | --- | --- |
| `y` | Ja | De klant heeft zich aangemeld voor de voorkeur. Met andere woorden, zij **do** stemmen in met het gebruik van hun gegevens zoals aangegeven door de betrokken voorkeur. |
| `n` | Nee | De klant heeft ervoor gekozen deze voorkeur niet toe te passen. Met andere woorden, zij **stemmen niet** in met het gebruik van hun gegevens zoals aangegeven door de betrokken voorkeur. |
| `p` | Verificatie in behandeling | Het systeem heeft nog geen definitieve voorkeurswaarde ontvangen. Dit wordt het vaakst gebruikt als deel van een toestemming die uit twee stappen controle vereist. Als een klant bijvoorbeeld ervoor kiest e-mailberichten te ontvangen, wordt die toestemming ingesteld op `p` totdat de klant een koppeling in een e-mailbericht selecteert om te controleren of hij het juiste e-mailadres heeft opgegeven. Op dat moment wordt de toestemming bijgewerkt naar `y`.<br><br>Als deze voorkeur geen tweesets verificatieproces gebruikt, kan de  `p` keuze worden gebruikt om aan te geven dat de klant nog niet heeft gereageerd op de bevestigingsvraag. U kunt bijvoorbeeld automatisch de waarde instellen op `p` op de eerste pagina van een website, voordat de klant heeft gereageerd op de vraag naar toestemming. In rechtsgebieden waarvoor geen uitdrukkelijke toestemming vereist is, kunt u deze ook gebruiken om aan te geven dat de klant niet expliciet heeft aangegeven dat de toestemming is geweigerd (met andere woorden, er wordt aangenomen dat de toestemming is verleend). |
| `u` | Onbekend | De voorkeursgegevens van de klant zijn onbekend. |
| `LI` | Gewettigd belang | Het legitieme zakelijke belang om deze gegevens voor het opgegeven doel te verzamelen en te verwerken, weegt zwaarder dan de potentiële schade die het voor het individu oplevert. |
| `CT` | Slinken | De verzameling van gegevens voor het opgegeven doel is vereist om te voldoen aan contractuele verplichtingen met de betrokkene. |
| `CP` | Naleving van een wettelijke verplichting | De verzameling van gegevens voor het gespecificeerde doel is vereist om te voldoen aan de wettelijke verplichtingen van het bedrijf. |
| `VI` | vitaal belang van de individuele | Het verzamelen van gegevens voor het opgegeven doel is vereist om de vitale belangen van het individu te beschermen. |
| `PI` | Openbaar belang | Het verzamelen van gegevens voor het specifieke doel is vereist om een taak van algemeen belang of in de uitoefening van het openbaar gezag uit te voeren. |

## `subscriptions` {#subscriptions}

Sommige ondernemingen staan klanten toe om binnen voor verschillende abonnementen te kiezen die met een bepaald marketing kanaal worden geassocieerd. Een bankbedrijf kan bijvoorbeeld klanten toestaan om te abonneren op telefoonwaarschuwingen voor te veel opgenomen rekeningen, of verkoopoproepen voor het indienen van een loyaliteitsprogramma ontvangen.

De volgende JSON vertegenwoordigt een voorbeeld marketing gebied voor een telefoonvraag marketing kanaal dat een `subscriptions` kaart bevat. Elke toets in het object `subscriptions` vertegenwoordigt een individueel abonnement op het marketingkanaal. Elk abonnement bevat op zijn beurt een aanmeldingswaarde (`val`).

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

## Aanvullende bronnen

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
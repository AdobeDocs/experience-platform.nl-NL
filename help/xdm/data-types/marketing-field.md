---
solution: Experience Platform
title: Gegevenstype van voorkeursveld voor algemene marketing
topic: overview
description: Dit document biedt een overzicht van het XDM-gegevenstype van het veld Generic Marketing Preference.
translation-type: tm+mt
source-git-commit: f5ec59e609fda66d379847dca068d19d4cce8228
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 1%

---


# [!UICONTROL Generic Marketing Preference Field] gegevenstype

[!UICONTROL Generic Marketing Preference Field] is een standaard XDM gegevenstype dat de selectie van een klant voor een bepaalde marketing voorkeur beschrijft.

>[!NOTE]
>
>Dit gegevenstype is bedoeld om de structuur van de toestemmingsregelingen van uw organisatie aan te passen gebruikend [[!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)] mixin](../mixins/profile/consents.md) als basislijn.
>
>Als u een `subscriptions` kaart voor een bepaald marketing voorkeurgebied vereist, moet u [marketing gebied met abonnees gegevenstype](./marketing-field-subscriptions.md) in plaats daarvan gebruiken.

![](../images/data-types/marketing-field.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `reason` | Tekenreeks | Wanneer een klant kiest uit een geval van het marketinggebruik, vertegenwoordigt dit koordgebied de reden waarom de klant uit opteerde. |
| `time` | DateTime | Een tijdstempel volgens ISO 8601 van het tijdstip waarop de voorkeur voor het in de handel brengen werd gewijzigd, indien van toepassing. |
| `val` | Tekenreeks | De door de klant opgegeven voorkeursoptie voor dit marketinggeval. Zie de onderstaande tabel voor toegestane waarden en definities. |

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

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
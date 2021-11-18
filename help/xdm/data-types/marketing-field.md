---
solution: Experience Platform
title: Gegevenstype van voorkeursveld voor algemene marketing
topic-legacy: overview
description: Dit document biedt een overzicht van het XDM-gegevenstype van het veld Generic Marketing Preference.
exl-id: d4c53885-f34f-4721-aa34-1fe02dc7006f
source-git-commit: 0f39e9237185b49417f2af8dfc288ab1420cccae
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 0%

---

# [!UICONTROL Generic Marketing Preference Field] gegevenstype

[!UICONTROL Generic Marketing Preference Field] is een standaard XDM gegevenstype dat de selectie van een klant voor een bepaalde marketing voorkeur beschrijft.

>[!NOTE]
>
>Dit gegevenstype is bedoeld om de structuur van de toestemmingsschema&#39;s van uw organisatie aan te passen gebruikend [[!UICONTROL Consents and Preferences] veldgroep](../field-groups/profile/consents.md) als basislijn.
>
>Als u een `subscriptions` kaart voor een bepaald voorkeursveld voor marketing, moet u de optie [marketingveld met gegevenstype voor abonnementen](./marketing-field-subscriptions.md) in plaats daarvan.

![](../images/data-types/marketing-field.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `reason` | Tekenreeks | Wanneer een klant kiest uit een geval van het marketinggebruik, vertegenwoordigt dit koordgebied de reden waarom de klant uit opteerde. |
| `time` | DateTime | Een tijdstempel volgens ISO 8601 van het tijdstip waarop de voorkeur voor het in de handel brengen werd gewijzigd, indien van toepassing. |
| `val` | Tekenreeks | De door de klant opgegeven voorkeursoptie voor dit marketinggeval. Zie de onderstaande tabel voor toegestane waarden en definities. |

{style=&quot;table-layout:auto&quot;}

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

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)

---
solution: Experience Platform
title: Gegevenstype algemeen toestemmingsveld
topic-legacy: overview
description: Dit document biedt een overzicht van het XDM-gegevenstype van het veld Algemeen akkoord.
exl-id: f1f14eb7-21dd-45ca-8fb4-68f397cfa697
source-git-commit: bd312024a1a3fb6da840a38d6e9d19fcbd6eab5a
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 1%

---

# [!UICONTROL Generic Consent Field] gegevenstype

[!UICONTROL Generic Consent Field] is een standaard XDM gegevenstype dat de selectie van een klant voor een bepaalde toestemmingsvoorkeur beschrijft.

>[!NOTE]
>
>Dit gegevenstype is bedoeld om de structuur van de toestemmingsregelingen van uw organisatie aan te passen gebruikend [[!UICONTROL Consents and Preferences] gebiedsgroep](../field-groups/profile/consents.md) als basislijn.

![](../images/data-types/consent-field.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `val` | Tekenreeks | De klant-verstrekte toestemmingskeuze voor dit gebruiksgeval. Zie de onderstaande tabel voor toegestane waarden en definities. |

{style=&quot;table-layout:auto&quot;}

In de volgende tabel worden de toegestane waarden voor `val` weergegeven:

| Waarde | Titel | Beschrijving |
| --- | --- | --- |
| `y` | Ja | De klant heeft ervoor gekozen de toestemming te verlenen. Met andere woorden, zij **do** stemmen in met het gebruik van hun gegevens zoals aangegeven in de betreffende toestemming. |
| `n` | Nee | De klant heeft ervoor gekozen niet akkoord te gaan. Met andere woorden, zij **stemmen niet** in met het gebruik van hun gegevens zoals aangegeven door de betrokken toestemming. |
| `p` | Verificatie in behandeling | Het systeem heeft nog geen definitieve goedkeuringswaarde ontvangen. Dit wordt het vaakst gebruikt als deel van een toestemming die uit twee stappen controle vereist. Als een klant bijvoorbeeld ervoor kiest e-mailberichten te ontvangen, wordt die toestemming ingesteld op `p` totdat de klant een koppeling in een e-mailbericht selecteert om te controleren of hij het juiste e-mailadres heeft opgegeven. Op dat moment wordt de toestemming bijgewerkt naar `y`.<br><br>Als deze toestemming geen tweesets verificatieproces gebruikt, kan de  `p` keuze worden gebruikt om aan te geven dat de klant nog niet heeft gereageerd op de bevestigingsprompt. U kunt bijvoorbeeld automatisch de waarde instellen op `p` op de eerste pagina van een website, voordat de klant heeft gereageerd op de vraag naar toestemming. In rechtsgebieden waarvoor geen uitdrukkelijke toestemming vereist is, kunt u deze ook gebruiken om aan te geven dat de klant niet expliciet heeft aangegeven dat de toestemming is geweigerd (met andere woorden, er wordt aangenomen dat de toestemming is verleend). |
| `u` | Onbekend | De informatie over de toestemming van de klant is onbekend. |
| `LI` | Gewettigd belang | Het legitieme zakelijke belang om deze gegevens voor het opgegeven doel te verzamelen en te verwerken, weegt zwaarder dan de potentiële schade die het voor het individu oplevert. |
| `CT` | Slinken | De verzameling van gegevens voor het opgegeven doel is vereist om te voldoen aan contractuele verplichtingen met de betrokkene. |
| `CP` | Naleving van een wettelijke verplichting | De verzameling van gegevens voor het gespecificeerde doel is vereist om te voldoen aan de wettelijke verplichtingen van het bedrijf. |
| `VI` | vitaal belang van de individuele | Het verzamelen van gegevens voor het opgegeven doel is vereist om de vitale belangen van het individu te beschermen. |
| `PI` | Openbaar belang | Het verzamelen van gegevens voor het specifieke doel is vereist om een taak van algemeen belang of in de uitoefening van het openbaar gezag uit te voeren. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-field.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-field.schema.json)

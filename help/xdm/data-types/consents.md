---
keywords: Experience Platform;profiel;real-time klantprofiel;problemen;API;toestemming;Toestemming;Voorkeuren;privacyOptOuts;marketingVoorkeuren;optOutType;basisOfProcessing;toestemming;Toestemming
title: Gegevenstype Inhoud en Voorkeuren
description: Het gegevenstype Consent for Privacy, Personalization en Marketing Preferences is bedoeld ter ondersteuning van de verzameling van klantmachtigingen en -voorkeuren die worden gegenereerd door CMP's (Consent Management Platforms) en andere bronnen van uw gegevensbewerkingen.
exl-id: cdcc7b04-eeb9-40d3-b0b5-f736a5472621
source-git-commit: b08c6cf12a38f79e019544dea91913a77bd6490a
workflow-type: tm+mt
source-wordcount: '2235'
ht-degree: 0%

---

# [!UICONTROL Consents and Preferences] gegevenstype

Het [!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] gegevenstype (hierna genoemd &quot;[!UICONTROL Consents and Preferences] gegevenstype&quot;) is een [!DNL Experience Data Model] (XDM) gegevenstype dat bedoeld is om de inzameling van klantentoestemmingen en voorkeur te steunen die door de Platforms van het Beheer van de Toestemming (CMPs) en andere bronnen van uw gegevensverrichtingen worden geproduceerd.

In dit document worden de structuur en het beoogde gebruik beschreven van de velden die worden verschaft door het gegevenstype [!UICONTROL Consents and Preferences] .

## Vereisten {#prerequisites}

Dit document vereist een goed begrip van XDM en het gebruik van de schema&#39;s in [!DNL Experience Platform]. Lees de volgende documentatie voordat u verdergaat:

* [ XDM overzicht van het Systeem ](https://www.adobe.com/go/xdm-home-en)
* [ Grondbeginselen van schemacompositie ](https://www.adobe.com/go/xdm-schema-best-practices-en)

## Gegevenstypestructuur {#structure}

>[!IMPORTANT]
>
>Het gegevenstype [!UICONTROL Consents and Preferences] is ontworpen voor een reeks gevallen waarin toestemming wordt gegeven en het gebruik van voorkeursbeheer wordt uitgevoerd. Dit document beschrijft daarom in algemene termen het gebruik van de velden van het gegevenstype en geeft alleen suggesties voor de manier waarop u het gebruik van deze velden moet interpreteren. Neem contact op met het juridische team voor privacy om de structuur van het gegevenstype af te stemmen op de manier waarop uw organisatie deze toestemmings- en voorkeurskeuzen interpreteert en presenteert aan uw klanten.

Het [!UICONTROL Consents and Preferences] gegevenstype verstrekt verscheidene gebieden die worden gebruikt om **toestemming** en **voorkeur** informatie te vangen.

Een toestemming is een optie die een klant toestaat om te specificeren hoe hun gegevens kunnen worden gebruikt. De meeste toestemmingen hebben een juridisch aspect, in die zin dat sommige jurisdicties een vergunning vereisen alvorens de gegevens op een bepaalde manier kunnen worden gebruikt, of vereisen dat de klant een optie heeft om dat gebruik tegen te houden (opt-out) als de bevestigende toestemming niet wordt vereist.

Een voorkeur is een optie die de klant toestaat om te specificeren hoe de verschillende aspecten van hun ervaring met een merk zouden moeten worden behandeld. Deze vallen binnen twee categorieën:

* **voorkeur van Personalization**: Voorkeur betreffende hoe het merk ervaringen zou moeten personaliseren die aan een klant worden geleverd.
* **de voorkeur van de Marketing**: Voorkeur betreffende of een merk een klant door diverse kanalen mag contacteren.

De volgende schermafbeelding laat zien hoe de structuur van het gegevenstype wordt weergegeven in de interface van het platform:

![](../images/data-types/consents.png)

>[!TIP]
>
>Zie de gids op [ het onderzoeken van middelen XDM ](../ui/explore.md) aan voor stappen op hoe te om het even welk middel XDM op te zoeken en zijn structuur in Platform UI te inspecteren.

In het volgende voorbeeld van JSON ziet u het type gegevens dat het gegevenstype [!UICONTROL Consents and Preferences] kan verwerken. In de volgende secties wordt informatie gegeven over het specifieke gebruik van elk van deze velden.

```json
{
  "consents": {
    "collect": {
      "val": "VI",
    },
    "adID": {
      "idType": "IDFA",
      "val": "y"
    },
    "share": {
      "val": "y",
    },
    "personalize": {
      "content": {
        "val": "y"
      }
    },
    "marketing": {
      "preferred": "email",
      "any": {
        "val": "u"
      },
      "push": {
        "val": "n",
        "reason": "Too Frequent",
        "time": "2019-01-01T15:52:25+00:00"
      }
    },
    "metadata": {
      "time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

>[!TIP]
>
>U kunt steekproefJSON gegevens voor om het even welk XDM schema produceren dat u in Experience Platform bepaalt helpen visualiseren hoe uw klantentoestemming en voorkeursgegevens zouden moeten in kaart worden gebracht. Raadpleeg de volgende documentatie voor meer informatie:
>
>* [ produceer steekproefgegevens in UI ](../ui/sample.md)
>* [ produceer steekproefgegevens in API ](../api/sample-data.md)

## `consents` {#choices}

`consents` bevat verschillende velden die de toestemming en voorkeuren van een klant beschrijven. Deze velden worden in de onderstaande subsecties nader beschreven.

```json
"consents": {
  "collect": {
    "val": "VI",
  },
  "adID": {
    "idType": "IDFA",
    "val": "y"
  },
  "share": {
    "val": "y",
  },
  "personalize": {
    "content": {
      "val": "y"
    }
  },
  "marketing": {
    "preferred": "email",
    "any": {
      "val": "u"
    },
    "email": {
      "val": "n",
      "reason": "Too Frequent",
      "time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

### `collect`

`collect` staat voor de toestemming van de klant om de gegevens te laten verzamelen.

```json
"collect": {
  "val": "y"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `val` | De klant-verstrekte toestemmingskeuze voor dit gebruiksgeval. Zie [ bijlage ](#choice-values) voor erkende waarden en definities. |

{style="table-layout:auto"}

### `adID`

`adID` geeft aan dat de klant ermee instemt dat een adverteerder-id kan worden gebruikt om de klant te koppelen tussen apps op dit apparaat.

```json
"adID": {
  "idType": "IDFA",
  "val": "y"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `idType` | Het advertentie-id-type, `IDFA` voor Apple-id voor adverteerders of `GAID` voor Google Advertiser-id, ook wel Android Advertiser-id (AID) genoemd. |
| `val` | De klant-verstrekte toestemmingskeuze voor dit gebruiksgeval. Zie [ bijlage ](#choice-values) voor erkende waarden en definities. |

{style="table-layout:auto"}

### `share`

`share` staat voor de toestemming van de klant om te bepalen of zijn gegevens kunnen worden gedeeld met (of verkocht aan) derden of derden.

```json
"share": {
  "val": "y"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `val` | De klant-verstrekte toestemmingskeuze voor dit gebruiksgeval. Zie [ bijlage ](#choice-values) voor erkende waarden en definities. |

{style="table-layout:auto"}

### `personalize` {#personalize}

`personalize` legt de voorkeuren van klanten vast met betrekking tot de manier waarop hun gegevens kunnen worden gebruikt voor personalisatie. Klanten kunnen afzien van specifieke gevallen van persoonlijk gebruik of volledig afzien van personalisatie.

>[!IMPORTANT]
>
>`personalize` heeft geen betrekking op gevallen van marketinggebruik. Bijvoorbeeld, als een klant uit verpersoonlijking voor alle kanalen opteert, zouden zij niet moeten ophouden ontvangend mededelingen door die kanalen. De berichten die ze ontvangen, moeten eerder algemeen zijn en niet gebaseerd op hun profiel.
>
>Door het zelfde voorbeeld, als een klant uit direct marketing voor alle kanalen (door `marketing` kiest, verklaard in de [ volgende sectie ](#marketing)), dan zou die klant geen berichten moeten ontvangen, zelfs als verpersoonlijking wordt toegelaten.

```json
"personalize": {
  "content": {
    "val": "y",
  }
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `content` | Vertegenwoordigt de voorkeuren van de klant voor gepersonaliseerde inhoud op uw website of toepassing. |
| `val` | De door de klant opgegeven voorkeur voor personalisatie voor het opgegeven gebruiksgeval. In gevallen waarin de klant niet hoeft te worden gevraagd om toestemming te verlenen, moet in de waarde van dit veld worden aangegeven op welke basis de personalisatie moet plaatsvinden. Zie [ bijlage ](#choice-values) voor erkende waarden en definities. |

{style="table-layout:auto"}

### `marketing` {#marketing}

`marketing` legt de voorkeuren van klanten vast met betrekking tot welke marketingdoeleinden hun gegevens kunnen worden gebruikt. Klanten kunnen zich afmelden bij specifieke gevallen van marketinggebruik of de optie Afmelden bij direct marketing.

```json
"marketing": {
  "preferred": "email",
  "any": {
    "val": "u"
  },
  "email": {
    "val": "n",
    "reason": "Too Frequent"
  },
  "push": {
    "val": "y"
  },
  "sms": {
    "val": "y"
  }
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `preferred` | Wijst op het aangewezen kanaal van de klant voor het ontvangen van mededelingen. Zie [ bijlage ](#preferred-values) voor toegelaten waarden. |
| `any` | Vertegenwoordigt de voorkeur van de klant voor directe marketing als geheel. De voorkeur voor toestemming die in dit veld wordt gegeven, wordt beschouwd als de voorkeur voor een marketingkanaal, tenzij deze wordt overschreven door extra subvelden die onder `marketing` worden opgegeven. Als u meer opties voor korreligheid wilt gebruiken, wordt u aangeraden dit veld uit te sluiten.<br><br> als de waarde aan `n` wordt geplaatst, dan zouden alle specifiekere verpersoonlijkingsmontages moeten worden genegeerd. Als de waarde is ingesteld op `y` , moeten alle verpersoonlijkingsopties met fijnere korrel ook worden behandeld als `y` , tenzij deze expliciet zijn ingesteld op `n` . Als de waarde unset is, dan zouden de waarden voor elke verpersoonlijkingsoptie moeten worden gehonoreerd zoals gespecificeerd. |
| `email` | Geeft aan of de klant ermee instemt e-mailberichten te ontvangen. |
| `push` | Geeft aan of de klant het ontvangen van pushberichten toestaat. |
| `sms` | Geeft aan of de klant ermee instemt tekstberichten te ontvangen. |
| `val` | De voorkeur van de klant voor het gespecificeerde gebruiksgeval. In gevallen waarin de klant niet hoeft te worden gevraagd om toestemming te verlenen, moet in de waarde van dit veld worden aangegeven op welke basis het geval van het gebruik in de handel moet plaatsvinden. Zie [ bijlage ](#choice-values) voor erkende waarden en definities. |
| `time` | Een tijdstempel volgens ISO 8601 van het tijdstip waarop de voorkeur voor het in de handel brengen werd gewijzigd, indien van toepassing. Als de tijdstempel voor een bepaalde voorkeur gelijk is aan de tijdstempel die is opgegeven onder `metadata` , hoeft u dit veld niet in te stellen voor die voorkeur. |
| `reason` | Wanneer een klant kiest uit een geval van het marketinggebruik, vertegenwoordigt dit koordgebied de reden waarom de klant uit opteerde. |

{style="table-layout:auto"}

### `metadata`

`metadata` legt algemene metagegevens over de toestemmingen en voorkeuren van de klant vast wanneer deze voor het laatst zijn bijgewerkt.

```json
"metadata": {
  "time": "2019-01-01T15:52:25+00:00",
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `time` | Een ISO 8601-tijdstempel voor de laatste keer dat de toestemming en voorkeuren van de klant zijn bijgewerkt. Dit veld kan worden gebruikt in plaats van tijdstempels toe te passen op individuele voorkeuren om het laden en de complexiteit te verminderen. Als u een `time` -waarde opgeeft bij een individuele voorkeur, wordt de `metadata` -tijdstempel voor die bepaalde voorkeur genegeerd. |

{style="table-layout:auto"}

## Gegevens invoegen met het gegevenstype {#ingest}

Als u het gegevenstype [!UICONTROL Consents and Preferences] wilt gebruiken om gegevens met toestemming van uw klanten in te voeren, moet u een dataset maken die is gebaseerd op een schema dat dat gegevenstype bevat.

Zie het leerprogramma op [ creërend een schema in UI ](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) voor stappen op hoe te om gegevenstypes aan gebieden toe te wijzen. Zodra u een schema hebt gecreeerd dat een gebied met het [!UICONTROL Consents and Preferences] gegevenstype bevat, verwijs naar de sectie over [ het creëren van een dataset ](../../catalog/datasets/user-guide.md#create) in de gids van de datasetgebruiker, na de stappen om een dataset met een bestaand schema tot stand te brengen.

>[!IMPORTANT]
>
>Als u toestemmingsgegevens naar [!DNL Real-Time Customer Profile] wilt verzenden, is het vereist dat u een [!DNL Profile] -ingeschakeld schema maakt op basis van de [!DNL XDM Individual Profile] -klasse die het [!UICONTROL Consents and Preferences] -gegevenstype bevat. De dataset die u creeert die op dat schema wordt gebaseerd moet ook voor [!DNL Profile] worden toegelaten. Raadpleeg de zelfstudies die hierboven zijn gekoppeld voor specifieke stappen met betrekking tot [!DNL Real-Time Customer Profile] -vereisten voor schema&#39;s en gegevenssets.
>
>Bovendien moet u ook ervoor zorgen dat uw samenvoegingsbeleid wordt gevormd om aan de dataset(s) voorrang te geven die de recentste toestemmings en voorkeursgegevens bevatten, opdat de klantenprofielen correct worden bijgewerkt. Zie het overzicht op [ fusiebeleid ](../../rtcdp/profile/merge-policies.md) voor meer informatie.

## Verwerking van toestemmings- en preferenties

Wanneer een klant hun toestemmingen of voorkeur op uw website verandert, zouden deze veranderingen moeten worden verzameld en onmiddellijk worden afgedwongen gebruikend [ Adobe Experience Platform Web SDK ](../../web-sdk/commands/setconsent.md). Als een klant ervoor kiest geen gegevens meer te verzamelen, moet de gegevensverzameling onmiddellijk worden beëindigd. Als een klant ervoor kiest geen personalisatie meer te gebruiken, dan is er geen personalisatie aanwezig op de volgende pagina die zij bezoeken.

## Bijlage {#appendix}

In de onderstaande secties vindt u aanvullende informatie over het gegevenstype [!UICONTROL Consents and Preferences] .

### Geaccepteerde waarden voor `val` {#choice-values}

In de volgende tabel worden de toegestane waarden voor `val` weergegeven:

| Waarde | Titel | Beschrijving |
| --- | --- | --- |
| `y` | Ja (opt-in) | De klant heeft ervoor gekozen de toestemming of voorkeur te geven. Met andere woorden, stemmen zij **** toe met het gebruik van hun gegevens zoals die door de toestemming of voorkeur in kwestie worden vermeld. |
| `n` | Nee (opt-out) | De klant heeft ervoor gekozen geen toestemming of voorkeur te geven. Met andere woorden, zij **stemmen niet** toe met het gebruik van hun gegevens zoals die door de toestemming of voorkeur in kwestie worden vermeld. |
| `p` | Verificatie in behandeling | Het systeem heeft nog geen definitieve toestemming of voorkeurswaarde ontvangen. Dit wordt het vaakst gebruikt als deel van een toestemming die uit twee stappen controle vereist. Als een klant bijvoorbeeld ervoor kiest e-mailberichten te ontvangen, wordt die toestemming ingesteld op `p` totdat de klant een koppeling in een e-mailbericht selecteert om te controleren of hij het juiste e-mailadres heeft opgegeven. Op dat moment wordt de toestemming bijgewerkt naar `y` .<br><br> als deze toestemming of voorkeur geen twee-reeks controleproces gebruikt, dan kan `p` keus worden gebruikt om erop te wijzen dat de klant nog niet op de toestemmingsherinnering heeft gereageerd. U kunt bijvoorbeeld automatisch de waarde instellen op `p` op de eerste pagina van een website, voordat de klant heeft gereageerd op de bevestigingsprompt. In rechtsgebieden waarvoor geen uitdrukkelijke toestemming vereist is, kunt u deze ook gebruiken om aan te geven dat de klant niet expliciet heeft aangegeven dat de toestemming is geweigerd (met andere woorden, er wordt aangenomen dat de toestemming is verleend). |
| `u` | Onbekend | De instemming- of voorkeursgegevens van de klant zijn onbekend. |
| `dy` | Standaard van Ja (opt-in) | De klant heeft zelf geen waarde voor de toestemming opgegeven en wordt standaard als een opt-in (&quot;Yes&quot;) behandeld. Met andere woorden, instemming wordt verondersteld tot de klant anders aangeeft.<br><br> Merk op dat als de wetten of de veranderingen in het privacybeleid van uw bedrijf in veranderingen in de gebreken van sommige of alle gebruikers resulteren, u alle profielen manueel moet bijwerken die standaardwaarden bevatten. |
| `dn` | Standaard van Geen (opt-out) | De klant heeft zelf geen waarde voor de toestemming opgegeven en wordt standaard als een &quot;nee&quot; behandeld. Met andere woorden, de klant wordt verondersteld toestemming te hebben geweigerd tot zij anders aangeven.<br><br> Merk op dat als de wetten of de veranderingen in het privacybeleid van uw bedrijf in veranderingen in de gebreken van sommige of alle gebruikers resulteren, u alle profielen manueel moet bijwerken die standaardwaarden bevatten. |
| `LI` | Gewettigd belang | Het legitieme zakelijke belang om deze gegevens voor het opgegeven doel te verzamelen en te verwerken, weegt zwaarder dan de potentiële schade die het voor het individu oplevert. |
| `CT` | Slinken | De verzameling van gegevens voor het opgegeven doel is vereist om te voldoen aan contractuele verplichtingen met de betrokkene. |
| `CP` | Naleving van een wettelijke verplichting | De verzameling van gegevens voor het gespecificeerde doel is vereist om te voldoen aan de wettelijke verplichtingen van het bedrijf. |
| `VI` | vitaal belang van de individuele | Het verzamelen van gegevens voor het opgegeven doel is vereist om de vitale belangen van het individu te beschermen. |
| `PI` | Openbaar belang | Het verzamelen van gegevens voor het specifieke doel is vereist om een taak van algemeen belang of in de uitoefening van het openbaar gezag uit te voeren. |

{style="table-layout:auto"}

### Geaccepteerde waarden voor `preferred` {#preferred-values}

In de volgende tabel worden de toegestane waarden voor `preferred` weergegeven. De `preferred` waarden wijzen op het aangewezen kanaal van de klant voor het ontvangen van mededelingen die hen over gegevensinzameling, privacybeleid, en verpersoonlijkingsopties zouden informeren.

| Waarde | Beschrijving |
| --- | --- |
| `email` | Deze voorkeur geeft aan dat de klant ermee instemt om berichten via e-mail te ontvangen. |
| `push` | Deze voorkeur geeft aan dat de klant ermee instemt pushberichten te ontvangen. Dit zijn berichten of waarschuwingen die rechtstreeks naar hun apparaat worden verzonden, vaak een mobiele toepassing. |
| `inApp` | Deze voorkeur geeft aan dat de klant toestemming heeft om in-app berichten te ontvangen. Deze berichten worden geleverd in een mobiele of webtoepassing en bieden informatie terwijl de gebruiker actief betrokken is bij de app. |
| `sms` | Deze voorkeur geeft aan dat de klant ermee instemt om berichten via SMS (Short Message Service) te ontvangen. Dit zijn tekstberichten die naar hun mobiele telefoon worden verzonden. |
| `phone` | Deze voorkeur wijst op de toestemming van de klant om mededelingen door telefoongespreksinteractie te ontvangen. |
| `phyMail` | Deze voorkeur geeft de toestemming van de klant aan om materiaal via fysieke post te ontvangen. |
| `inVehicle` | Deze voorkeur geeft aan dat de klant ermee instemt om meldingen te ontvangen terwijl hij of zij zich in het voertuig bevindt. Deze berichten kunnen via voertuiginfotainment of andere communicatiekanalen in het voertuig worden verzonden. |
| `inHome` | Deze voorkeur geeft de toestemming van de klant aan om berichten te ontvangen terwijl thuis. Deze berichten kunnen door slimme huisapparaten of andere op huis-gebaseerde communicatiekanalen worden geleverd. |
| `iot` | Deze voorkeur geeft de toestemming van de klant aan om berichten met betrekking tot het Internet van Dingen (IoT) te ontvangen. Deze berichten kunnen via aangesloten apparaten en systemen binnen hun omgeving worden geleverd. |
| `social` | Deze voorkeur wijst op de toestemming van de klant om mededelingen door sociale media platforms te ontvangen. |
| `other` | Deze voorkeur omvat kanalen die niet in standaardcategorieën passen. Het vertegenwoordigt alternatieve of gespecialiseerde communicatiekanalen die specifiek kunnen zijn voor een bepaald bedrijf of een bepaalde industrie. |
| `none` | Deze voorkeur wijst erop dat de klant geen aangewezen communicatie kanaal heeft. |
| `unknown` | Deze voorkeur betekent dat het aangewezen communicatiekanaal van de klant niet gekend of niet gespecificeerd is. Dit kan zich voordoen als de klant geen uitdrukkelijke toestemming of voorkeursinformatie heeft verstrekt. |

{style="table-layout:auto"}

### Volledig schema [!UICONTROL Consents and Preferences] {#full-schema}

Om het volledige schema voor het [!UICONTROL Consents and Preferences] gegevenstype te bekijken, verwijs naar de [ officiële bewaarplaats XDM ](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-preferences.schema.json).

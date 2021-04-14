---
keywords: Experience Platform;profiel;real-time klantprofiel;problemen;API;toestemming;Toestemming;Voorkeuren;privacyOptOuts;marketingVoorkeuren;optOutType;basisOfProcessing;toestemming;Toestemming
title: Gegevenstype Inhoud en Voorkeuren
description: Het gegevenstype Consent for Privacy, Personalization and Marketing Preferences is bedoeld ter ondersteuning van de verzameling van klantmachtigingen en voorkeuren die worden gegenereerd door Platforms voor beheer van instemming (CMP's) en andere bronnen van uw gegevensbewerkingen.
topic: hulplijn
exl-id: cdcc7b04-eeb9-40d3-b0b5-f736a5472621
translation-type: tm+mt
source-git-commit: 4e9395b4551842cf75b0d1a4ec36c85930c42da5
workflow-type: tm+mt
source-wordcount: '1838'
ht-degree: 1%

---

# [!DNL Consents & Preferences] gegevenstype

Het gegevenstype [!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] (hierna genoemd &quot;[!DNL Consents & Preferences] gegevenstype&quot;) is een [!DNL Experience Data Model] (XDM) gegevenstype dat is bedoeld om de inzameling van klantentoestemmingen en voorkeur te steunen die door de Platforms van het Beheer van de Toestemming (CMPs) en andere bronnen van uw gegevensverrichtingen worden geproduceerd.

Dit document behandelt de structuur en het beoogde gebruik van de velden die worden verschaft door het gegevenstype [!DNL Consents & Preferences].

## Vereisten {#prerequisites}

Dit document vereist een werkend begrip van XDM en het gebruik van de schema&#39;s in [!DNL Experience Platform]. Lees de volgende documentatie voordat u verdergaat:

* [XDM System, overzicht](http://www.adobe.com/go/xdm-home-en)
* [Basisbeginselen van de schemacompositie](http://www.adobe.com/go/xdm-schema-best-practices-en)

## Structuur van gegevenstypen {#structure}

>[!IMPORTANT]
>
>Het gegevenstype [!DNL Consents & Preferences] is ontworpen voor een reeks gevallen waarin toestemming wordt gegeven en gebruik wordt gemaakt van voorkeursbeheer. Dit document beschrijft daarom in algemene termen het gebruik van de velden van het gegevenstype en geeft alleen suggesties voor de manier waarop u het gebruik van deze velden moet interpreteren. Neem contact op met het juridische team voor privacy om de structuur van het gegevenstype af te stemmen op de manier waarop uw organisatie deze toestemmings- en voorkeurskeuzen interpreteert en presenteert aan uw klanten.

Het gegevenstype [!DNL Consents & Preferences] biedt verschillende velden die worden gebruikt voor het vastleggen van **toestemmings**- en **preferentie**-informatie.

Een toestemming is een optie die een klant toestaat om te specificeren hoe hun gegevens kunnen worden gebruikt. De meeste toestemmingen hebben een juridisch aspect, in die zin dat sommige jurisdicties een vergunning vereisen alvorens de gegevens op een bepaalde manier kunnen worden gebruikt, of vereisen dat de klant een optie heeft om dat gebruik tegen te houden (opt-out) als de bevestigende toestemming niet wordt vereist.

Een voorkeur is een optie die de klant toestaat om te specificeren hoe de verschillende aspecten van hun ervaring met een merk zouden moeten worden behandeld. Deze vallen binnen twee categorieën:

* **Voorkeuren** voor personalisatie: Voorkeuren met betrekking tot de manier waarop het merk de ervaringen die aan een klant worden geleverd, moet aanpassen.
* **Marketingvoorkeuren**: Voorkeuren met betrekking tot de vraag of een merk via verschillende kanalen contact mag opnemen met een klant.

De volgende schermafbeelding laat zien hoe de structuur van het gegevenstype wordt weergegeven in de gebruikersinterface van het Platform:

![](../images/data-types/consents.png)

>[!TIP]
>
>Zie de gids op [het onderzoeken van de middelen XDM](../ui/explore.md) aan voor stappen op hoe te om het even welk middel van XDM op te zoeken en zijn structuur in het Platform UI te inspecteren.

Het volgende JSON toont een voorbeeld van het type gegevens dat het gegevenstype [!DNL Consents & Preferences] kan verwerken. In de volgende secties wordt informatie gegeven over het specifieke gebruik van elk van deze velden.

```json
{
  "consents": {
    "collect": {
      "val": "y",
    },
    "adID": {
      "val": "VI"
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
>* [Voorbeeldgegevens genereren in de gebruikersinterface](../ui/sample.md)
>* [Voorbeeldgegevens genereren in de API](../api/sample-data.md)


## `consents` {#choices}

`consents` bevat verschillende velden die de toestemmingen en voorkeuren van de klant beschrijven. Deze velden worden in de onderstaande subsecties nader beschreven.

```json
"consents": {
  "collect": {
    "val": "y",
  },
  "adID": {
    "val": "VI"
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

`collect` staat voor de toestemming van de klant om zijn gegevens te laten verzamelen.

```json
"collect" : {
  "val": "y"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `val` | De klant-verstrekte toestemmingskeuze voor dit gebruiksgeval. Zie [appendix](#choice-values) voor geaccepteerde waarden en definities. |

### `adID`

`adID` staat voor de toestemming van de klant om te bepalen of een adverteerder-id (IDFA of GAID) kan worden gebruikt om de klant te koppelen tussen apps op dit apparaat.

```json
"adID" : {
  "val": "y"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `val` | De klant-verstrekte toestemmingskeuze voor dit gebruiksgeval. Zie [appendix](#choice-values) voor geaccepteerde waarden en definities. |

### `share`

`share` staat voor de toestemming van de klant om te bepalen of zijn gegevens kunnen worden gedeeld met (of verkocht aan) derden of derden.

```json
"share" : {
  "val": "y"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `val` | De klant-verstrekte toestemmingskeuze voor dit gebruiksgeval. Zie [appendix](#choice-values) voor geaccepteerde waarden en definities. |

### `personalize` {#personalize}

`personalize` vangt klantenvoorkeur met betrekking tot welke manieren hun gegevens voor verpersoonlijking kunnen worden gebruikt. Klanten kunnen afzien van specifieke gevallen van persoonlijk gebruik of volledig afzien van personalisatie.

>[!IMPORTANT]
>
>`personalize` heeft geen betrekking op gevallen van gebruik bij het in de handel brengen. Bijvoorbeeld, als een klant uit verpersoonlijking voor alle kanalen opteert, zouden zij niet moeten ophouden ontvangend mededelingen door die kanalen. De berichten die ze ontvangen, moeten eerder algemeen zijn en niet gebaseerd op hun profiel.
>
>In hetzelfde voorbeeld geldt dat als een klant voor alle kanalen (via `marketing`, toegelicht in [volgende sectie](#marketing)) kiest voor het uit de directe marketing halen, die klant geen berichten mag ontvangen, zelfs niet als personalisatie is toegestaan.

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
| `val` | De door de klant opgegeven voorkeur voor personalisatie voor het opgegeven gebruiksgeval. In gevallen waarin de klant niet hoeft te worden gevraagd om toestemming te verlenen, moet in de waarde van dit veld worden aangegeven op welke basis de personalisatie moet plaatsvinden. Zie [appendix](#choice-values) voor geaccepteerde waarden en definities. |

### `marketing` {#marketing}

`marketing` legt klantenvoorkeuren vast met betrekking tot welke marketingdoeleinden hun gegevens kunnen worden gebruikt. Klanten kunnen zich afmelden bij specifieke gevallen van marketinggebruik of de optie Afmelden bij direct marketing.

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
| `preferred` | Wijst op het aangewezen kanaal van de klant voor het ontvangen van mededelingen. Zie [appendix](#preferred-values) voor geaccepteerde waarden. |
| `any` | Vertegenwoordigt de voorkeur van de klant voor directe marketing als geheel. De voorkeur voor toestemming die in dit veld wordt gegeven, wordt beschouwd als de &quot;standaardvoorkeur&quot; voor elk marketingkanaal, tenzij deze wordt overschreven door extra subvelden die onder `marketing` worden opgegeven. Als u meer opties voor korreligheid wilt gebruiken, wordt u aangeraden dit veld uit te sluiten.<br><br>Als de waarde wordt geplaatst aan  `n`, dan zouden alle specifiekere verpersoonlijkingsmontages moeten worden genegeerd. Als de waarde op `y` wordt geplaatst, dan zouden alle fijnkorrelige verpersoonlijkingsopties ook als `y` moeten worden behandeld, tenzij uitdrukkelijk geplaatst aan `n`. Als de waarde unset is, dan zouden de waarden voor elke verpersoonlijkingsoptie moeten worden gehonoreerd zoals gespecificeerd. |
| `email` | Geeft aan of de klant ermee instemt e-mailberichten te ontvangen. |
| `push` | Geeft aan of de klant het ontvangen van pushberichten toestaat. |
| `sms` | Geeft aan of de klant ermee instemt tekstberichten te ontvangen. |
| `val` | De voorkeur van de klant voor het gespecificeerde gebruiksgeval. In gevallen waarin de klant niet hoeft te worden gevraagd om toestemming te verlenen, moet in de waarde van dit veld worden aangegeven op welke basis het geval van het gebruik in de handel moet plaatsvinden. Zie [appendix](#choice-values) voor geaccepteerde waarden en definities. |
| `time` | Een tijdstempel volgens ISO 8601 van het tijdstip waarop de voorkeur voor het in de handel brengen werd gewijzigd, indien van toepassing. Als de tijdstempel voor een bepaalde voorkeur gelijk is aan de tijdstempel die wordt opgegeven onder `metadata`, hoeft dit veld niet te worden ingesteld voor die voorkeur. |
| `reason` | Wanneer een klant kiest uit een geval van het marketinggebruik, vertegenwoordigt dit koordgebied de reden waarom de klant uit opteerde. |

### `metadata`

`metadata` legt algemene metagegevens vast over de toestemmingen en voorkeuren van de klant wanneer deze voor het laatst zijn bijgewerkt.

```json
"metadata": {
  "time": "2019-01-01T15:52:25+00:00",
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `time` | Een ISO 8601-tijdstempel voor de laatste keer dat de toestemming en voorkeuren van de klant zijn bijgewerkt. Dit veld kan worden gebruikt in plaats van tijdstempels toe te passen op individuele voorkeuren om het laden en de complexiteit te verminderen. Als u een waarde `time` opgeeft onder een individuele voorkeur, wordt de tijdstempel `metadata` voor die bepaalde voorkeur genegeerd. |

## Gegevens invoegen met behulp van het gegevenstype {#ingest}

Als u het gegevenstype [!DNL Consents & Preferences] wilt gebruiken om gegevens met toestemming van uw klanten in te voeren, moet u een dataset maken die is gebaseerd op een schema dat dat gegevenstype bevat.

Zie de zelfstudie over [het creëren van een schema in UI](http://www.adobe.com/go/xdm-schema-editor-tutorial-en) voor stappen op hoe te om gegevenstypes aan gebieden toe te wijzen. Zodra u een schema hebt gecreeerd dat een gebied met [!DNL Consents & Preferences] gegevenstype bevat, verwijs naar de sectie over [het creëren van een dataset](../../catalog/datasets/user-guide.md#create) in de gids van de datasetgebruiker, die de stappen volgt om een dataset met een bestaand schema tot stand te brengen.

>[!IMPORTANT]
>
>Als u toestemmingsgegevens naar [!DNL Real-time Customer Profile] wilt verzenden, wordt het vereist dat u een [!DNL Profile]-Toegelaten schema op [!DNL XDM Individual Profile] klasse creeert die [!DNL Consents & Preferences] gegevenstype bevat. De dataset die u creeert die op dat schema wordt gebaseerd moet ook voor [!DNL Profile] worden toegelaten. Raadpleeg de bovenstaande zelfstudies voor specifieke stappen met betrekking tot [!DNL Real-time Customer Profile]-vereisten voor schema&#39;s en gegevenssets.
>
>Bovendien moet u ook ervoor zorgen dat uw samenvoegingsbeleid wordt gevormd om aan de dataset(s) voorrang te geven die de recentste toestemmings en voorkeursgegevens bevatten, opdat de klantenprofielen correct worden bijgewerkt. Zie het overzicht op [samenvoegbeleid](../../rtcdp/profile/merge-policies.md) voor meer informatie.

## Verwerking van toestemmings- en voorkeurswijzigingen

Wanneer een klant zijn toestemming of voorkeuren op uw website wijzigt, moeten deze wijzigingen worden verzameld en onmiddellijk worden doorgevoerd met de [Adobe Experience Platform Web SDK](../../edge/consent/supporting-consent.md). Als een klant ervoor kiest geen gegevens meer te verzamelen, moet de gegevensverzameling onmiddellijk worden beëindigd. Als een klant ervoor kiest geen personalisatie meer te gebruiken, dan is er geen personalisatie aanwezig op de volgende pagina die zij bezoeken.

## Bijlage {#appendix}

De onderstaande secties bevatten aanvullende informatie over het gegevenstype [!DNL Consents & Preferences].

### Geaccepteerde waarden voor `val` {#choice-values}

In de volgende tabel worden de toegestane waarden voor `val` weergegeven:

| Value | Titel | Beschrijving |
| --- | --- | --- |
| `y` | Ja | De klant heeft ervoor gekozen de toestemming of voorkeur te geven. Met andere woorden, zij **do** stemmen in met het gebruik van hun gegevens zoals aangegeven door de toestemming of voorkeur in kwestie. |
| `n` | Nee | De klant heeft ervoor gekozen geen toestemming of voorkeur te geven. Met andere woorden, zij **stemmen niet** in met het gebruik van hun gegevens zoals aangegeven door de toestemming of voorkeur in kwestie. |
| `p` | Verificatie in behandeling | Het systeem heeft nog geen definitieve toestemming of voorkeurswaarde ontvangen. Dit wordt het vaakst gebruikt als deel van een toestemming die uit twee stappen controle vereist. Als een klant bijvoorbeeld ervoor kiest e-mailberichten te ontvangen, wordt die toestemming ingesteld op `p` totdat de klant een koppeling in een e-mailbericht selecteert om te controleren of hij het juiste e-mailadres heeft opgegeven. Op dat moment wordt de toestemming bijgewerkt naar `y`.<br><br>Als deze toestemming of voorkeur geen tweesets verificatieproces gebruikt, kan in plaats daarvan de  `p` keuze worden gebruikt om aan te geven dat de klant nog niet heeft gereageerd op de bevestigingsprompt. U kunt bijvoorbeeld automatisch de waarde instellen op `p` op de eerste pagina van een website, voordat de klant heeft gereageerd op de vraag naar toestemming. In rechtsgebieden waarvoor geen uitdrukkelijke toestemming vereist is, kunt u deze ook gebruiken om aan te geven dat de klant niet expliciet heeft aangegeven dat de toestemming is geweigerd (met andere woorden, er wordt aangenomen dat de toestemming is verleend). |
| `u` | Onbekend | De instemming- of voorkeursgegevens van de klant zijn onbekend. |
| `LI` | Gewettigd belang | Het legitieme zakelijke belang om deze gegevens voor het opgegeven doel te verzamelen en te verwerken, weegt zwaarder dan de potentiële schade die het voor het individu oplevert. |
| `CT` | Slinken | De verzameling van gegevens voor het opgegeven doel is vereist om te voldoen aan contractuele verplichtingen met de betrokkene. |
| `CP` | Naleving van een wettelijke verplichting | De verzameling van gegevens voor het gespecificeerde doel is vereist om te voldoen aan de wettelijke verplichtingen van het bedrijf. |
| `VI` | vitaal belang van de individuele | Het verzamelen van gegevens voor het opgegeven doel is vereist om de vitale belangen van het individu te beschermen. |
| `PI` | Openbaar belang | Het verzamelen van gegevens voor het specifieke doel is vereist om een taak van algemeen belang of in de uitoefening van het openbaar gezag uit te voeren. |

### Geaccepteerde waarden voor `preferred` {#preferred-values}

In de volgende tabel worden de toegestane waarden voor `preferred` weergegeven:

| Waarde | Beschrijving |
| --- | --- |
| `email` | E-mailberichten. |
| `push` | Pushmeldingen. |
| `inApp` | In-app berichten. |
| `sms` | Sms-berichten. |
| `phone` | Telefoongesprekken. |
| `phyMail` | Fysieke post. |
| `inVehicle` | Berichten in het voertuig. |
| `inHome` | Berichten thuis. |
| `iot` | Internet of things (IoT) berichten. |
| `social` | Inhoud van sociale media. |
| `other` | Een kanaal dat niet in een standaardcategorie past. |
| `none` | Geen voorkeurskanaal. |
| `unknown` | Het voorkeurkanaal is onbekend. |

### Volledig [!DNL Consents & Preferences]-schema {#full-schema}

Als u het volledige schema voor het gegevenstype [!DNL Consents & Preferences] wilt weergeven, raadpleegt u de [officiële XDM-opslagruimte](https://github.com/adobe/xdm/blob/master/components/datatypes/consent-preferences.schema.json).

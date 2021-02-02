---
keywords: Experience Platform;profiel;real-time klantprofiel;problemen;API;toestemming;Toestemming;Voorkeuren;privacyOptOuts;marketingVoorkeuren;optOutType;basisOfProcessing;toestemming;Toestemming
title: Gegevenstype Inhoud en Voorkeuren
description: Het gegevenstype Privacy/Marketing Preferences (Consent) (Consent) is bedoeld ter ondersteuning van de verzameling van klantmachtigingen en -voorkeuren die worden gegenereerd door CMP's (Consent Management Platforms) en andere bronnen van uw gegevensbewerkingen.
topic: guide
translation-type: tm+mt
source-git-commit: caebdcd48e03bd8b91da624532569b55d8696fb4
workflow-type: tm+mt
source-wordcount: '2040'
ht-degree: 0%

---


# [!DNL Consents & Preferences] gegevenstype

Het gegevenstype [!DNL Privacy/Marketing Preferences (Consent)] (hierna genoemd &quot;[!DNL Consents & Preferences] gegevenstype&quot;) is een [!DNL Experience Data Model] (XDM) gegevenstype dat is bedoeld om de inzameling van klantentoestemmingen en voorkeur te steunen die door de Platforms van het Beheer van de Toestemming (CMPs) en andere bronnen van uw gegevensverrichtingen worden geproduceerd.

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

Het volgende JSON toont een voorbeeld van het type gegevens dat het gegevenstype [!DNL Consents & Preferences] kan verwerken. In de volgende secties wordt informatie gegeven over het specifieke gebruik van elk van deze velden.

```json
{
  "xdm:consents": {
    "xdm:collect": {
      "xdm:val": "y",
    },
    "xdm:adID": {
      "xdm:val": "VI"
    },
    "xdm:share": {
      "xdm:val": "y",
    },
    "xdm:personalize": {
      "xdm:content": {
        "xdm:val": "y"
      }
    },
    "xdm:marketing": {
      "xdm:preferred": "email",
      "xdm:any": {
        "xdm:val": "u"
      },
      "xdm:push": {
        "xdm:val": "n",
        "xdm:reason": "Too Frequent",
        "xdm:time": "2019-01-01T15:52:25+00:00"
      }
    },
    "xdm:idSpecific": {
      "email": {
        "jdoe@example.com": {
          "xdm:marketing": {
            "xdm:email": {
              "xdm:val": "n"
            }
          }
        }
      }
    }
  },
  "xdm:metadata": {
    "xdm:time": "2019-01-01T15:52:25+00:00"
  }
}
```

>[!NOTE]
>
>Het bovenstaande voorbeeld is bedoeld om de structuur van de gegevens te illustreren die via het gegevenstype [!DNL Consents & Preferences] naar [!DNL Platform] worden verzonden, om context te geven aan de rest van dit document waarin de belangrijkste velden worden uitgelegd die door het gegevenstype worden verschaft. Het volledige schema voor de structuur van het gegevenstype is te vinden in [appendix](#full-schema) ter verwijzing.

## xdm:toestemmingen {#choices}

`xdm:consents` bevat verschillende velden die de toestemmingen en voorkeuren van de klant beschrijven. Deze velden worden in de onderstaande subsecties nader beschreven.

```json
"xdm:consents": {
  "xdm:collect": {
    "xdm:val": "y",
  },
  "xdm:adID": {
    "xdm:val": "VI"
  },
  "xdm:share": {
    "xdm:val": "y",
  },
  "xdm:personalize": {
    "xdm:content": {
      "xdm:val": "y"
    }
  },
  "xdm:marketing": {
    "xdm:preferred": "email",
    "xdm:any": {
      "xdm:val": "u"
    },
    "xdm:email": {
      "xdm:val": "n",
      "xdm:reason": "Too Frequent",
      "xdm:time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

### xdm:verzamelen

`xdm:collect` staat voor de toestemming van de klant om zijn gegevens te laten verzamelen.

```json
"xdm:collect" : {
  "xdm:val": "y"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `xdm:val` | De klant-verstrekte toestemmingskeuze voor dit gebruiksgeval. Zie [appendix](#choice-values) voor geaccepteerde waarden en definities. |

### xdm:adID

`xdm:adID` staat voor de toestemming van de klant om te bepalen of een adverteerder-id (IDFA of GAID) kan worden gebruikt om de klant te koppelen tussen apps op dit apparaat.

```json
"xdm:adID" : {
  "xdm:val": "y"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `xdm:val` | De klant-verstrekte toestemmingskeuze voor dit gebruiksgeval. Zie [appendix](#choice-values) voor geaccepteerde waarden en definities. |

### xdm:delen

`xdm:share` staat voor de toestemming van de klant om te bepalen of zijn gegevens kunnen worden gedeeld met (of verkocht aan) derden of derden.

```json
"xdm:share" : {
  "xdm:val": "y"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `xdm:val` | De klant-verstrekte toestemmingskeuze voor dit gebruiksgeval. Zie [appendix](#choice-values) voor geaccepteerde waarden en definities. |

### xdm:personaliseren {#personalize}

`xdm:personalize` vangt klantenvoorkeur met betrekking tot welke manieren hun gegevens voor verpersoonlijking kunnen worden gebruikt. Klanten kunnen afzien van specifieke gevallen van persoonlijk gebruik of volledig afzien van personalisatie.

>[!IMPORTANT]
>
>`xdm:personalize` heeft geen betrekking op gevallen van gebruik bij het in de handel brengen. Bijvoorbeeld, als een klant uit verpersoonlijking voor alle kanalen opteert, zouden zij niet moeten ophouden ontvangend mededelingen door die kanalen. De berichten die ze ontvangen, moeten eerder algemeen zijn en niet gebaseerd op hun profiel.
>
>In hetzelfde voorbeeld geldt dat als een klant voor alle kanalen (via `xdm:marketing`, toegelicht in [volgende sectie](#marketing)) kiest voor het uit de directe marketing halen, die klant geen berichten mag ontvangen, zelfs niet als personalisatie is toegestaan.

```json
"xdm:personalize": {
  "xdm:content": {
    "xdm:val": "y",
  }
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `xdm:content` | Vertegenwoordigt de voorkeuren van de klant voor gepersonaliseerde inhoud op uw website of toepassing. |
| `xdm:val` | De door de klant opgegeven voorkeur voor personalisatie voor het opgegeven gebruiksgeval. In gevallen waarin de klant niet hoeft te worden gevraagd om toestemming te verlenen, moet in de waarde van dit veld worden aangegeven op welke basis de personalisatie moet plaatsvinden. Zie [appendix](#choice-values) voor geaccepteerde waarden en definities. |

### xdm:marketing {#marketing}

`xdm:marketing` legt klantenvoorkeuren vast met betrekking tot welke marketingdoeleinden hun gegevens kunnen worden gebruikt. Klanten kunnen zich afmelden bij specifieke gevallen van marketinggebruik of de optie Afmelden bij direct marketing.

```json
"xdm:marketing": {
  "xdm:preferred": "email",
  "xdm:any": {
    "xdm:val": "u"
  },
  "xdm:email": {
    "xdm:val": "n",
    "xdm:reason": "Too Frequent"
  },
  "xdm:push": {
    "xdm:val": "y"
  },
  "xdm:sms": {
    "xdm:val": "y"
  }
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `xdm:preferred` | Wijst op het aangewezen kanaal van de klant voor het ontvangen van mededelingen. Zie [appendix](#preferred-values) voor geaccepteerde waarden. |
| `xdm:any` | Vertegenwoordigt de voorkeur van de klant voor directe marketing als geheel. De voorkeur voor toestemming die in dit veld wordt gegeven, wordt beschouwd als de &quot;standaardvoorkeur&quot; voor elk marketingkanaal, tenzij deze wordt overschreven door extra subvelden die onder `xdm:marketing` worden opgegeven. Als u meer opties voor korreligheid wilt gebruiken, wordt u aangeraden dit veld uit te sluiten.<br><br>Als de waarde wordt geplaatst aan  `n`, dan zouden alle specifiekere verpersoonlijkingsmontages moeten worden genegeerd. Als de waarde op `y` wordt geplaatst, dan zouden alle fijnkorrelige verpersoonlijkingsopties ook als `y` moeten worden behandeld, tenzij uitdrukkelijk geplaatst aan `n`. Als de waarde unset is, dan zouden de waarden voor elke verpersoonlijkingsoptie moeten worden gehonoreerd zoals gespecificeerd. |
| `xdm:email` | Geeft aan of de klant ermee instemt e-mailberichten te ontvangen. |
| `xdm:push` | Geeft aan of de klant het ontvangen van pushberichten toestaat. |
| `xdm:sms` | Geeft aan of de klant ermee instemt tekstberichten te ontvangen. |
| `xdm:val` | De voorkeur van de klant voor het gespecificeerde gebruiksgeval. In gevallen waarin de klant niet hoeft te worden gevraagd om toestemming te verlenen, moet in de waarde van dit veld worden aangegeven op welke basis het geval van het gebruik in de handel moet plaatsvinden. Zie [appendix](#choice-values) voor geaccepteerde waarden en definities. |
| `xdm:time` | Een tijdstempel volgens ISO 8601 van het tijdstip waarop de voorkeur voor het in de handel brengen werd gewijzigd, indien van toepassing. Als de tijdstempel voor een bepaalde voorkeur gelijk is aan de tijdstempel die wordt opgegeven onder `xdm:metadata`, hoeft dit veld niet te worden ingesteld voor die voorkeur. |
| `xdm:reason` | Wanneer een klant kiest uit een geval van het marketinggebruik, vertegenwoordigt dit koordgebied de reden waarom de klant uit opteerde. |

### xdm:idSpecific

`xdm:idSpecific` kan worden gebruikt wanneer een bepaalde toestemming of voorkeur niet universeel op een klant van toepassing is, maar tot één enkel apparaat of identiteitskaart beperkt is. Zo kan een klant ervoor kiezen geen e-mails naar het ene adres te ontvangen, terwijl e-mails naar een ander adres mogelijk worden toegestaan.

>[!IMPORTANT]
>
>De toestemmingen en de voorkeur op kanaalniveau (d.w.z. die onder `xdm:consents` buiten `xdm:idSpecific` worden verstrekt) zijn op identiteitskaart binnen dat kanaal van toepassing. Alle toestemming en voorkeuren op kanaalniveau worden daarom rechtstreeks toegepast, ongeacht of de equivalente id- of apparaatspecifieke instellingen worden gerespecteerd:
>
>* Als de klant ervoor kiest om op kanaalniveau uit te schakelen, worden gelijkwaardige toestemmingen of voorkeuren in `xdm:idSpecific` genegeerd.
>* Als de toestemming of voorkeur op kanaalniveau niet is ingesteld, of de klant heeft ervoor gekozen, worden de equivalente toestemmingen of voorkeuren in `xdm:idSpecific` gerespecteerd.


Elke sleutel in het `xdm:idSpecific`-object vertegenwoordigt een specifieke naamruimte die wordt herkend door de Adobe Experience Platform Identity Service. Hoewel u uw eigen aangepaste naamruimten kunt definiëren om verschillende id&#39;s te categoriseren, wordt u aangeraden een van de standaardnaamruimten van Identity Service te gebruiken om opslaggrootten voor Real-time klantprofiel te reduceren. Zie [Naamruimte overzicht van naamruimte](../../identity-service/namespaces.md) in de documentatie bij Identiteitsservice voor meer informatie over naamruimten.

De sleutels voor elk namespacevoorwerp vertegenwoordigen de unieke identiteitswaarden waarvoor de klant voorkeur heeft geplaatst. Elke identiteitswaarde kan een volledige reeks toestemmingen en voorkeur bevatten, die op de zelfde manier zoals `xdm:consents` wordt geformatteerd.

```json
"xdm:idSpecific": {
  "email": {
    "jdoe@example.com": {
      "xdm:marketing": {
        "xdm:email": {
          "xdm:val": "n"
        }
      }
    }
  }
}
```

## xdm:metagegevens

`xdm:metadata` legt algemene metagegevens vast over de toestemmingen en voorkeuren van de klant wanneer deze voor het laatst zijn bijgewerkt.

```json
"xdm:metadata": {
  "xdm:time": "2019-01-01T15:52:25+00:00",
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `xdm:time` | Een tijdstempel voor de laatste keer dat een van de toestemmingen en voorkeuren van de klant is bijgewerkt. Dit veld kan worden gebruikt in plaats van tijdstempels toe te passen op individuele voorkeuren om het laden en de complexiteit te verminderen. Als u een waarde `xdm:time` opgeeft onder een individuele voorkeur, wordt de tijdstempel `xdm:metadata` voor die bepaalde voorkeur genegeerd. |

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

### Geaccepteerde waarden voor xdm:val {#choice-values}

In de volgende tabel worden de toegestane waarden voor `xdm:val` weergegeven:

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

### Geaccepteerde waarden voor xdm:preferred {#preferred-values}

In de volgende tabel worden de toegestane waarden voor `xdm:preferred` weergegeven:

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

---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;consent;Consent;preferences;Preferences;privacyOptOuts;marketingPreferences;optOutType;basisOfProcessing;
solution: Adobe Experience Platform
title: Overzicht van het mixen van privacy
description: De combinatie van de Voorkeur van de Privacy/van de Marketing (Toestemming) is een mengsel van de Gegevens van de Ervaring (XDM) dat bedoeld is om de inzameling van gebruikerstoestemmingen en voorkeur te steunen die door CMPs en andere bronnen van klanten worden geproduceerd. Dit document behandelt de structuur en het beoogde gebruik van de verschillende velden die door de vermenging worden verschaft.
topic: guide
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '1827'
ht-degree: 0%

---


# [!DNL Privacy Consent] Overzicht van mixen

De [!DNL Privacy/Marketing Preferences (Consent)] mixin (hierna genoemd &quot;[!DNL Privacy Consent] mixin&quot;) is een [!DNL Experience Data Model] (XDM) mengeling die bedoeld is om de inzameling van gebruikerstoestemmingen en voorkeur te steunen die door CMPs en andere bronnen van klanten wordt geproduceerd. Dit document behandelt de structuur en het beoogde gebruik van de verschillende velden die door de vermenging worden verschaft.

## Vereisten {#prerequisites}

Dit document vereist een werkend begrip van [!DNL Experience Data Model] (XDM) en het gebruik van de schema&#39;s in [!DNL Experience Platform]. Lees de volgende documentatie voordat u verdergaat:

* [XDM System, overzicht](http://www.adobe.com/go/xdm-home-en)
* [Basisbeginselen van de schemacompositie](http://www.adobe.com/go/xdm-schema-best-practices-en)

## Voorbeeld van schema {#schema}

>[!NOTE]
>
>In het onderstaande voorbeeld wordt de structuur getoond van de gegevens die [!DNL Platform] via het [!DNL Privacy Consent] mixin worden verzonden, om context te geven aan de volgende sectie in dit document waarin de belangrijkste velden worden beschreven die door het mixin worden verschaft. Een volledig voorbeeld van de structuur van het schema vindt u ter referentie in de [bijlage](#full-schema) .

In het volgende JSON-voorbeeld ziet u het type gegevens dat de [!DNL Privacy Consent] mix kan verwerken. In de volgende sectie wordt informatie gegeven over het specifieke gebruik van elk van deze velden.

```json
{
  "xdm:privacyOptOuts": [
     {
        "xdm:optOutType": "general_opt_out",
        "xdm:optOutValue": "in",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "legitimate_interest"
     },
     {
        "xdm:optOutType": "device_linking",
        "xdm:optOutValue": "not_provided",
        "xdm:basisOfProcessing": "vital_interest"
     },
     {
        "xdm:optOutType": "anonymous_analysis",
        "xdm:optOutValue": "out"
     }
  ],
  "xdm:personalizationPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "consent"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in"
        },
        {
           "xdm:type": "push_notifications",
           "xdm:choice": "out",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00"
        }
     ]
  },
  "xdm:marketingPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in",
           "xdm:subscriptions": {
              "weekly_mailer": {
                 "xdm:choice": "out",
                 "xdm:timestamp": "2019-02-03T15:52:25+00:00"
              },
              "daily_newsletter": {
                 "xdm:choice": "pending"
              }
           }
        },
        {
           "xdm:type": "iot",
           "xdm:choice": "out",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:subscriptions": {
              "out_of_milk": {
                 "xdm:choice": "in"
              }
           }
        }
     ]
  },
  "xdm:version": "1.0.0",
  "xdm:timestamp": "2019-01-01T15:52:25+00:00",
  "xdm:userLocale": "UK",
  "xdm:localeSource": "ip"
}
```

## Velden {#fields}

In de onderstaande secties wordt ingegaan op het gebruik van elk van de belangrijkste velden die door de [!DNL Privacy Consent] mix worden verschaft en op de structuur van de subvelden ervan.

### xdm:privacyOptOuts {#privacyOptOuts}

`xdm:privacyOptOuts` is een array die algemene instellingen voor weigeren vertegenwoordigt die door de klant zijn geselecteerd. Er kunnen verschillende objecten in deze array worden opgenomen, die elk een specifiek type opt-out vertegenwoordigen en de voorkeuren die de klant voor dat type heeft geselecteerd.

```json
"xdm:privacyOptOuts": [
     {
        "xdm:optOutType": "general_opt_out",
        "xdm:optOutValue": "in",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "legitimate_interest"
     },
     {
        "xdm:optOutType": "device_linking",
        "xdm:optOutValue": "not_provided",
        "xdm:basisOfProcessing": "vital_interest"
     },
     {
        "xdm:optOutType": "anonymous_analysis",
        "xdm:optOutValue": "out"
     }
  ]
```

| Eigenschap | Beschrijving |
| --- | --- |
| `xdm:optOutType` | Het type opt-out. Zie de [bijlage](#optOutType-values) voor toegestane waarden en definities. |
| `xdm:optOutValue` | De geselecteerde voorkeur die de klant heeft gekozen voor dit bepaalde type van niet-deelname. Zie de [bijlage](#choice-optOutValue-values) voor toegestane waarden en definities. |
| `xdm:timestamp` | Een tijdstempel volgens ISO 8601 van het tijdstip waarop de voorkeur voor niet-deelname werd gewijzigd, indien van toepassing. |
| `xdm:basisOfProcessing` | Geeft de privacygerelateerde basis aan waarop de gegevens moeten worden verzameld en verwerkt. Standaard is dit veld ingesteld op `consent`, wat aangeeft dat de gegevens alleen mogen worden verwerkt als de gebruiker toestemming heeft gegeven (zoals weergegeven in `xdm:optOutValue`).<br><br>In sommige gevallen hoeven klanten niet te worden gevraagd toestemming te verlenen voor gegevensverwerking. `xdm:basisOfProcessing` moet in deze gevallen in het opt-out-object worden opgenomen, met vermelding van de reden waarom geen verzoeken om toestemming zijn ingediend. Zie de [bijlage](#basisOfProcessing-values) voor toegestane waarden en definities. |

### xdm:personalizationPreferences {#personalizationPreferences}

`xdm:personalizationPreferences` vangt klantenvoorkeur met betrekking tot welke manieren hun gegevens voor verpersoonlijking kunnen worden gebruikt. Gebruikers kunnen zich afmelden bij specifieke gevallen van gebruik van personalisatie of zich volledig afmelden voor personalisatie.

>[!IMPORTANT]
>
>`xdm:personalizationPreferences` heeft geen betrekking op gevallen van gebruik bij het in de handel brengen. Als een klant bijvoorbeeld voor e-mails kiest voor personalisatie, ontvangen deze geen e-mailberichten meer. De e-mails die ze ontvangen, zijn eerder algemeen en niet gebaseerd op hun profiel.
>
>In hetzelfde voorbeeld, als een klant kiest voor e-mailmarketing (via `xdm:marketingPreferences`, uitgelegd in de [volgende sectie](#marketingPreferences)), ontvangt die klant geen e-mailberichten, zelfs niet als personalisatie via e-mail is toegestaan.

```json
"xdm:personalizationPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "consent"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in"
        },
        {
           "xdm:type": "push_notifications",
           "xdm:choice": "out",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00"
        }
     ]
  }
```

| Eigenschap | Beschrijving |
| --- | --- |
| `xdm:default` | De gegevens die in dit object worden verstrekt, vertegenwoordigen de voorkeuren van de klant voor personalisatie als geheel. |
| `xdm:details` | Een array van objecten, één voor elk specifiek type personalisatie waarvoor de klant voorkeuren heeft opgegeven. |
| `xdm:choice` | De voorkeur van de klant-verstrekte toestemming voor verpersoonlijking in het algemeen, of een specifiek verpersoonlijkingstype, afhankelijk van of het onder `xdm:default` of `xdm:details`, respectievelijk wordt verstrekt. Zie de [bijlage](#choice-optOutValue-values) voor toegestane waarden en definities. |
| `xdm:type` | Objecten in de `xdm:details` array moeten dit veld opgeven om aan te geven voor welk specifiek verpersoonlijkingsgebruik de klant toestemmingsgegevens verstrekt. Zie de [bijlage](#type-values) voor toegestane waarden en definities. |
| `xdm:timestamp` | Een tijdstempel volgens ISO 8601 van het tijdstip waarop de voorkeur voor niet-deelname werd gewijzigd, indien van toepassing. |
| `xdm:basisOfProcessing` | Geeft de privacygerelateerde basis aan waarop de gegevens moeten worden verzameld en verwerkt. Standaard is dit veld ingesteld op `consent`, wat aangeeft dat de gegevens alleen mogen worden verwerkt als de gebruiker toestemming heeft gegeven (zoals weergegeven in `xdm:choice`).<br><br>In sommige omstandigheden zijn klanten niet gevraagd toestemming te geven voor personalisatie. `xdm:basisOfProcessing` moet in deze gevallen in het opt-out-object worden opgenomen, met vermelding van de reden waarom geen verzoeken om toestemming zijn ingediend. Zie de [bijlage](#basisOfProcessing-values) voor toegestane waarden en definities. |


### xdm:marketingPreferences {#marketingPreferences}

`xdm:marketingPreferences` legt klantenvoorkeuren vast met betrekking tot welke marketingdoeleinden hun gegevens kunnen worden gebruikt. Gebruikers kunnen zich afmelden bij specifieke gevallen van gebruik voor marketingdoeleinden, of ze kunnen afzien van rechtstreekse marketing.

```json
"xdm:marketingPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in",
           "xdm:subscriptions": {
              "weekly_mailer": {
                 "xdm:choice": "out",
                 "xdm:timestamp": "2019-02-03T15:52:25+00:00"
              },
              "daily_newsletter": {
                 "xdm:choice": "pending"
              }
           }
        },
        {
           "xdm:type": "iot",
           "xdm:choice": "out",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:subscriptions": {
              "out_of_milk": {
                 "xdm:choice": "in"
              }
           }
        }
     ]
  }
```

| Eigenschap | Beschrijving |
| --- | --- |
| `xdm:default` | De gegevens die in dit object worden verstrekt, vertegenwoordigen de voorkeuren van de klant voor directe marketing als geheel. |
| `xdm:details` | Een array met objecten, één voor elk specifiek geval van marketinggebruik waarvoor de klant voorkeuren heeft opgegeven. |
| `xdm:choice` | De voorkeur van de door de klant verleende toestemming voor marketing in het algemeen, of een specifiek geval van marketinggebruik, afhankelijk van of het wordt verstrekt onder `xdm:default` of `xdm:details`, respectievelijk. Zie de [bijlage](#choice-optOutValue-values) voor toegestane waarden en definities. |
| `xdm:subscriptions` | Een object waarvan de sleutels bedrijfsspecifieke abonnementen vertegenwoordigen, zoals mailinglijsten of nieuwsbrieven. Elk abonnementsobject moet op zijn beurt een `xdm:choice` waarde voor het desbetreffende abonnement bevatten. |
| `xdm:type` | Objecten in de `xdm:details` array moeten dit veld opgeven om het specifieke geval van marketinggebruik aan te geven waarvoor de klant toestemmingsgegevens verstrekt. Zie de [bijlage](#type-values) voor toegestane waarden en definities. |
| `xdm:timestamp` | Een tijdstempel volgens ISO 8601 van het tijdstip waarop de voorkeur voor niet-deelname werd gewijzigd, indien van toepassing. |
| `xdm:basisOfProcessing` | Geeft de privacygerelateerde basis aan waarop de gegevens moeten worden verzameld en verwerkt. Standaard is dit veld ingesteld op `consent`, wat aangeeft dat de gegevens alleen mogen worden verwerkt als de gebruiker toestemming heeft gegeven (zoals weergegeven in `xdm:choice`).<br><br>In sommige omstandigheden is de klant niet gevraagd toestemming te verlenen voor het direct in de handel brengen. `xdm:basisOfProcessing` moet in deze gevallen in het opt-out-object worden opgenomen, met vermelding van de reden waarom geen verzoeken om toestemming zijn ingediend. Zie de [bijlage](#basisOfProcessing-values) voor toegestane waarden en definities. |

## Gegevens over de toestemming worden geïnjecteerd met de mix {#ingest}

Om de [!DNL Privacy Consent] mengeling te gebruiken om toestemmingsgegevens van uw klanten in te voeren, moet u de mengeling aan een nieuw of bestaand schema toevoegen, en een dataset creëren die op dat schema wordt gebaseerd.

Zie de zelfstudie bij het [creëren van een schema in UI](http://www.adobe.com/go/xdm-schema-editor-tutorial-en) voor stappen op hoe te om mengen aan een schema toe te voegen. Het[!DNL  Privacy Consent] mengsel is compatibel met schema&#39;s die op de klassen [!DNL XDM Individual Profile] of [!DNL XDM ExperienceEvent]worden gebaseerd.

Nadat u een schema hebt gemaakt dat de [!DNL Privacy Consent] mix bevat, raadpleegt u de sectie over het [maken van een gegevensset](../../catalog/datasets/user-guide.md#create) in de gebruikershandleiding van de gegevensset, die de stappen volgt om een gegevensset met een bestaand schema te maken.

>[!IMPORTANT]
>
>Als u toestemmingsgegevens naar wilt verzenden [!DNL Real-time Customer Profile], wordt het vereist dat u een [!DNL Profile]-toegelaten schema creeert dat op de [!DNL XDM Individual Profile] klasse wordt gebaseerd die de [!DNL Privacy Consent] mixin bevat. De dataset die u creeert die op dat schema wordt gebaseerd moet ook voor worden toegelaten [!DNL Profile]. Raadpleeg de bovenstaande zelfstudies voor specifieke stappen met betrekking tot [!DNL Real-time Customer Profile] vereisten.

## Aanhangsel {#appendix}

De onderstaande punten bevatten aanvullende informatie over het [!DNL Privacy Consent] mengsel.

### Geaccepteerde waarden voor xdm:optOutType {#optOutType-values}

In de volgende tabel worden de toegestane waarden voor `xdm:optOutType`:

| Waarde | Beschrijving |
| --- | --- |
| `general_opt_out` | De gegevens kunnen voor geen enkel doel worden gebruikt. Dit blokkeert doorgaans de gegevensverzameling, behalve wanneer de verwerkingsbasis niet &quot;toestemming&quot; is.<br><br>Bij gebruik van dit type opt-out krijgen de geaccepteerde waarden `in` `out` en de volgende contextafhankelijke betekenis:<ul><li>`in`: De gebruiker **heeft toestemming** gegeven voor het gebruik van zijn gegevens voor algemene verwerking.</li><li>`out`: De gebruiker gaat **niet akkoord** met het gebruik van de gegevens voor algemene verwerking.</li></ul>Zie de tabel met [toegestane waarden voor xdm:optOutValue](#choice-optOutValue-values) voor meer informatie. |
| `anonymous_analysis` | De gegevens kunnen niet worden gebruikt voor algemene webmetriek waarvoor geen gebruikersnaam vereist is, zoals het aantal keren dat een bepaalde pagina is weergegeven. |
| `device_linking` | De gegevens van het ene apparaat dat door een bezoeker wordt gebruikt, kunnen niet worden gecombineerd met gegevens van een ander apparaat dat door dezelfde bezoeker wordt gebruikt. Apparaten worden gekoppeld met behulp van technieken zoals een algemene gebruikersnaam of e-mailadres, vaak via de Adobe-apparaatcoop of een persoonlijke apparaatgrafiek. |
| `pseudonymous_analysis` | De gegevens kunnen niet worden gebruikt voor webmetriek die door Adobe Analytics wordt geleverd. Hiervoor moeten pseudoniem-id&#39;s worden gebruikt om paden te identificeren die gebruikers via een website volgen (zoals een fallout-rapport), om sessies te maken en voor toewijzingsdoeleinden. |
| `sales_sharing_opt_out` | De gegevens kunnen niet worden gebruikt voor verkoopdoeleinden of voor het delen met derden.<br><br>Bij gebruik van dit type opt-out krijgen de geaccepteerde waarden `in` `out` en de volgende contextafhankelijke betekenis:<ul><li>`in`: De gebruiker **heeft toestemming** gegeven voor het gebruik van zijn gegevens voor verkoop- en deeldoeleinden.</li><li>`out`: De gebruiker gaat **niet akkoord** met het gebruik van zijn gegevens voor verkoop- en deeldoeleinden.</li></ul>Zie de tabel met [toegestane waarden voor xdm:optOutValue](#choice-optOutValue-values) voor meer informatie. |

### Geaccepteerde waarden voor xdm:basisOfProcessing {#basisOfProcessing-values}

In de volgende tabel worden de toegestane waarden voor `xdm:basisOfProcessing`:

| Waarde | Beschrijving |
| --- | --- |
| `consent` **(Standaard)** | Het verzamelen van gegevens voor het opgegeven doel is toegestaan, aangezien de persoon hiervoor uitdrukkelijk toestemming heeft gegeven. Dit is de standaardwaarde van `xdm:basisOfProcessing` als geen andere waarde wordt verstrekt. <br><br>**BELANGRIJK**: De waarden voor `xdm:choice` en `xdm:optOutValue` worden alleen ondersteund wanneer `xdm:basisOfProcessing` deze zijn ingesteld op `consent`. Als in `xdm:basisOfProcessing` plaats daarvan een van de andere waarden in deze tabel wordt gebruikt, worden de keuzes voor toestemming van het individu genegeerd. |
| `compliance` | De verzameling van gegevens voor het gespecificeerde doel is vereist om te voldoen aan de wettelijke verplichtingen van het bedrijf. |
| `contract` | De verzameling van gegevens voor het opgegeven doel is vereist om te voldoen aan contractuele verplichtingen met de betrokkene. |
| `legitimate_interest` | Het legitieme zakelijke belang om deze gegevens voor het opgegeven doel te verzamelen en te verwerken, weegt zwaarder dan de potentiële schade die het voor het individu oplevert. |
| `public_interest` | Het verzamelen van gegevens voor het specifieke doel is vereist om een taak van algemeen belang of in de uitoefening van het openbaar gezag uit te voeren. |
| `vital_interest` | Het verzamelen van gegevens voor het opgegeven doel is vereist om de vitale belangen van het individu te beschermen. |

### Geaccepteerde waarden voor xdm:choice en xdm:optOutValue {#choice-optOutValue-values}

In de volgende tabel worden de toegestane waarden voor `xdm:choice` en `xdm:optOutValue`:

| Waarde | Beschrijving |
| --- | --- |
| `pending` | Het systeem heeft nog geen toestemming-voorkeur informatie van de klant ontvangen. Kan worden gebruikt voor de eerste pagina van een website terwijl toestemming wordt verkregen. Het kan ook worden gebruikt om aan te geven dat de toestemming wordt &quot;verondersteld&quot; in plaats van expliciet wordt verstrekt. |
| `in` | De gebruiker heeft zich aangemeld bij de voorkeur voor toestemming. Met andere woorden, zij **stemmen** in met het gebruik van hun gegevens zoals aangegeven in de betrokken voorkeur voor toestemming. |
| `out` | De gebruiker heeft ervoor gekozen niet aan de voorkeur voor toestemming deel te nemen. Met andere woorden, zij **geven geen** toestemming voor het gebruik van hun gegevens zoals aangegeven in de betrokken voorkeur voor toestemming. |
| `not_applicable` | De voorkeur voor toestemming in kwestie geldt niet voor de klant. |
| `not_provided` | De klant heeft geen informatie over toestemming-voorkeur verstrekt. |
| `unknown` | De informatie over de toestemming-voorkeur van de klant is onbekend. |

### Geaccepteerde waarden voor xdm:type {#type-values}

In de volgende tabel worden de toegestane waarden voor `xdm:type`:

| Waarde | Beschrijving |
| --- | --- |
| `ads` | Advertenties die kunnen worden weergegeven via niet-verbonden websites. |
| `content` | Inhoud die op uw website wordt weergegeven. |
| `customer_support` | Gegevens met betrekking tot klantenondersteuning. |
| `email` | E-mailberichten. |
| `iot` | Gegevens met betrekking tot het &quot;internet van dingen&quot; (IoT). |
| `in_app_messages` | In-app berichten. |
| `in_home` | Berichten thuis. |
| `in_store` | In-store berichten. |
| `in_vehicle` | Berichten in het voertuig. |
| `offers` | Speciale aanbiedingen. |
| `phone_calls` | Gegevens met betrekking tot telefoongesprekken. |
| `push_notifications` | Pushmeldingen. |
| `sms` | Sms-berichten. |
| `social_media` | Inhoud van sociale media. |
| `snail_mail` | Berichten die via conventionele postbezorging worden verzonden. |
| `third_party_content` | Inhoud of artikelen die op uw website worden weergegeven en die door een niet-verwante entiteit worden aangeboden. |
| `third_party_offers` | Aanbiedingen of advertenties van een niet-verbonden entiteit die op uw website worden weergegeven. |

### Volledig [!DNL Privacy Consent] schema {#full-schema}

Het volgende JSON vertegenwoordigt het volledige [!DNL Privacy Consent] schema zoals het in de Registratie van het Schema verschijnt:

```json
{
  "meta:license": [
    "Copyright 2019 Adobe Systems Incorporated. All rights reserved.",
    "This work is licensed under a Creative Commons Attribution 4.0 International (CC BY 4.0) license",
    "you may not use this file except in compliance with the License. You may obtain a copy",
    "of the License at https://creativecommons.org/licenses/by/4.0/"
  ],
  "$id": "https://ns.adobe.com/xdm/context/consent-preferences",
  "$schema": "http://json-schema.org/draft-06/schema#",
  "title": "Privacy/Marketing Preferences (Consent)",
  "description": "This schema captures privacy, personalization and marketing preferences (consents).",
  "type": "object",
  "meta:extensible": true,
  "meta:abstract": true,
  "definitions": {
    "consentValue": {
      "type": "string",
      "enum": [
        "not_provided",
        "pending",
        "in",
        "out",
        "unknown",
        "not_applicable"
      ],
      "meta:enum": {
        "not_provided": "Not provided",
        "pending": "Pending verification",
        "in": "Opt-in",
        "out": "Opt-out",
        "unknown": "Unknown",
        "not_applicable": "Not Applicable"
      }
    },
    "basisOfProcessing": {
      "title": "Basis Of Processing",
      "type": "string",
      "description": "Basis of Processing",
      "enum": [
        "consent",
        "legitimate_interest",
        "contract",
        "vital_interest",
        "compliance",
        "public_interest"
      ],
      "meta:enum": {
        "consent": "User Consent",
        "legitimate_interest": "Legitimate Interest",
        "contract": "Contract",
        "vital_interest": "Vital Interest of the Individual",
        "compliance": "Compliance with a Legal Obligation",
        "public_interest": "Public Interest"
      }
    },
    "timestamp": {
      "title": "Preference timestamp",
      "description": "Timestamp of this specific opt out or preference.",
      "type": "string",
      "format": "date-time"
    },
    "consent-preferences": {
      "properties": {
        "xdm:privacyOptOuts": {
          "title": "Privacy Preferences",
          "description": "Encapsulates data privacy preferences.",
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "xdm:optOutType": {
                "title": "Opt-out type",
                "type": "string",
                "description": "The type of user permission.",
                "enum": [
                  "general_opt_out",
                  "sales_sharing_opt_out",
                  "anonymous_analysis",
                  "pseudonymous_analysis",
                  "device_linking"
                ],
                "meta:enum": {
                  "general_opt_out": "General opt-out",
                  "sales_sharing_opt_out": "Sales/sharing opt-out",
                  "anonymous_analysis": "Anonymous Analysis",
                  "pseudonymous_analysis": "Pseudonymous Analysis",
                  "device_linking": "Device Linking"
                }
              },
              "xdm:optOutValue": {
                "title": "Opt Out Value",
                "description": "The value of the specific opt out.",
                "$ref": "#/definitions/consentValue"
              },
              "xdm:basisOfProcessing": {
                "$ref": "#/definitions/basisOfProcessing"
              },
              "xdm:timestamp": {
                "$ref": "#/definitions/timestamp"
              }
            }
          }
        },
        "xdm:personalizationPreferences": {
          "title": "Personalization Preferences",
          "description": "User's Personalization Preferences",
          "type": "object",
          "properties": {
            "xdm:default": {
              "title": "Global Personalization Preferences",
              "description": "User's Default Personalization Preference",
              "type": "object",
              "properties": {
                "xdm:choice": {
                  "title": "Default Personalization Preferences Value",
                  "description": "The default value for personalization",
                  "$ref": "#/definitions/consentValue"
                },
                "xdm:basisOfProcessing": {
                  "$ref": "#/definitions/basisOfProcessing"
                },
                "xdm:timestamp": {
                  "$ref": "#/definitions/timestamp"
                }
              }
            },
            "xdm:details": {
              "title": "Itemized Personalization Preferences",
              "description": "Preferences for specific types of personalization",
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "meta:enum": {
                    "content": "Personalize Content",
                    "in_app": "Personalize In App Messages",
                    "offers": "Personalize Offers",
                    "email": "Personalize eMail",
                    "snail_mail": "Personalize Regular Mail",
                    "phone_calls": "Personalize Phone Calls",
                    "push_notifications": "Personalize Push Notifications",
                    "sms": "Personalize SMS",
                    "customer_support": "Personalize Customer Support",
                    "in_store": "Personalize In Store",
                    "in_vehicle": "Personalize In Vehicle",
                    "in_home": "Personalize In Home",
                    "iot": "Personalize IoT",
                    "social_media": "Personalize Social Media",
                    "third_party_offers": "Personalize Third-party Offers",
                    "third_party_content": "Personalize Third-party Content",
                    "ads": "Personalize My Business's Ads on Other Sites"
                  }
                },
                "xdm:choice": {
                  "title": "Personalization Preference Value",
                  "description": "The value for this specific personalization preference",
                  "$ref": "#/definitions/consentValue"
                },
                "xdm:basisOfProcessing": {
                  "$ref": "#/definitions/basisOfProcessing"
                },
                "xdm:timestamp": {
                  "$ref": "#/definitions/timestamp"
                }
              }
            }
          }
        }
      },
      "xdm:marketingPreferences": {
        "title": "Marketing Preferences",
        "description": "User's Direct Marketing Preferences",
        "type": "object",
        "properties": {
          "xdm:default": {
            "title": "Default Direct Marketing Preference",
            "description": "User's Default Marketing Preference",
            "type": "object",
            "properties": {
              "xdm:choice": {
                "title": "Default Marketing Preferences Value",
                "description": "The default value for direct marketing preferences",
                "$ref": "#/definitions/consentValue"
              },
              "xdm:basisOfProcessing": {
                "$ref": "#/definitions/basisOfProcessing"
              },
              "xdm:timestamp": {
                "$ref": "#/definitions/timestamp"
              }
            }
          },
          "xdm:details": {
            "title": "Itemized Direct Marketing Preferences",
            "description": "Preferences for specific types of direct marketing",
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "xdm:type": {
                  "title": "Marketing Preference",
                  "type": "string",
                  "description": "The specific marketing preference.",
                  "enum": [
                    "email",
                    "push_notifications",
                    "in_app_messages",
                    "sms",
                    "phone_calls",
                    "snail_mail",
                    "in_vehicle_messages",
                    "in_home_messages",
                    "iot",
                    "social_media"
                  ],
                  "meta:enum": {
                    "email": "Receive eMail",
                    "push_notifications": "Receive Push Notifications",
                    "in_app_messages": "Receive In App Messages",
                    "sms": "Receive SMS",
                    "phone_calls": "Receive Phone Calls",
                    "snail_mail": "Receive Regular Mail",
                    "in_vehicle_messages": "Receive In Vehicle Messages",
                    "in_home_messages": "Receive In Home Messages",
                    "iot": "Receive IoT",
                    "social_media": "Receive Social Media Messages"
                  }
                },
                "xdm:choice": {
                  "title": "Marketing Preference Value",
                  "description": "The value for this specific marketing preference",
                  "$ref": "#/definitions/consentValue"
                },
                "xdm:basisOfProcessing": {
                  "$ref": "#/definitions/basisOfProcessing"
                },
                "xdm:timestamp": {
                  "$ref": "#/definitions/timestamp"
                },
                "xdm:subscriptions": {
                  "title": "Company-specific subscriptions",
                  "description": "Company-specific subscriptions, such as mailing lists or newsletters",
                  "type": "object",
                  "meta:xdmType": "map",
                  "additionalProperties": {
                    "xdm:choice": {
                      "title": "Marketing Preference Value",
                      "description": "The value for this specific marketing preference",
                      "$ref": "#/definitions/consentValue"
                    },
                    "xdm:timestamp": {
                      "$ref": "#/definitions/timestamp"
                    }
                  }
                }
              }
            }
          }
        }
      },
      "xdm:timestamp": {
        "title": "Consent Preferences timestamp",
        "description": "Timestamp of the complete set of user consent preferences.",
        "type": "string",
        "format": "date-time"
      },
      "xdm:version": {
        "title": "Preferences Version",
        "description": "Version of the Privacy Preferences Standard",
        "type": "string"
      },
      "xdm:userLocale": {
        "title": "User Locale",
        "description": "User location or jurisdiction that applies to the consents for this user",
        "type": "string"
      },
      "xdm:localeSource": {
        "title": "Locale Source",
        "description": "Method used to determine the user's locale",
        "enum": [
          "ip",
          "gps",
          "user_provided",
          "website_location",
          "inferred",
          "other"
        ],
        "meta:enum": {
          "ip": "IP Address",
          "gps": "Device GPS",
          "user_provided": "User Provided",
          "website_location": "Website eTDL",
          "inferred": "Inferred",
          "other": "Other"
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/common/extensible#/definitions/@context"
    },
    {
      "$ref": "#/definitions/consent-preferences"
    }
  ],
  "meta:status": "experimental"
}
```

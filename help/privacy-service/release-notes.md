---
keywords: Experience Platform;startpagina;populaire onderwerpen
solution: Experience Platform
title: Aanvullende informatie bij de Privacy Service
description: De nieuwste aanvullende informatie voor Adobe Experience Platform Service.
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: ht
source-wordcount: '552'
ht-degree: 100%

---

# Aanvullende informatie voor [!DNL Privacy Service]

Dit document bevat informatie over nieuwe functies voor Adobe Experience Platform [!DNL Privacy Service]en over verbeteringen en belangrijke opgeloste problemen.

>[!NOTE]
>
>De meest recente aanvullende informatie voor andere [!DNL Experience Platform]-services vindt u [hier](../release-notes/latest/latest.md).

## 9 september 2020

### Nieuwe functies

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor LGPD (Brazilië) | Privacybanen kunnen nu worden gecreëerd onder de Braziliaanse [!DNL Lei Geral de Proteção de Dados] (LGPD)-verordening. Deze taken worden bijgehouden met de code `lgpd_bra` voor regelgeving. |

## 8 april 2020

### Nieuwe functies

| Functie | Beschrijving |
| --- | --- |
| PDPA-ondersteuning | [!DNL Privacy]-aanvragen kunnen nu worden gedaan en bijgehouden op basis van de Personal Data Protection Act (PDPA) in Thailand. Wanneer u privacyverzoeken indient in de API, accepteert de array `regulation` de waarde &#39;pdpa_tha&#39;. |
| Naamruimtetypen in de gebruikersinterface | U kunt nu verschillende naamruimtetypen opgeven in de Request Builder in de gebruikersinterface van [!DNL Privacy Service]. Raadpleeg het [handboek](ui/user-guide.md) voor meer informatie. |
| Afschaffing van het oude eindpunt | Het oude API-eindpunt (`data/privacy/gdpr`) is afgeschaft. |

## 14 januari 2020

### Nieuwe functies

| Functie | Beschrijving |
| --- | --- |
| [!DNL Privacy Service]-rebranding | De eerdere naam &#39;GDPR-service&#39; is vervangen door [!DNL Privacy Service] omdat de service inmiddels ook andere regels ondersteunt naast GDPR. |
| Nieuwe API-eindpunten | Het basispad voor de [!DNL Privacy Service]-API is bijgewerkt van `/data/privacy/gdpr` naar `/data/core/privacy/jobs` |
| Nieuwe vereiste `regulation`-eigenschap | Wanneer u nieuwe taken maakt in de [!DNL Privacy Service]-API, moet de eigenschap `regulation` in de payload van de aanvraag worden opgegeven om aan te geven onder welke regeling de taak moet worden bijgehouden. Geaccepteerde waarden zijn `gdpr` en `ccpa`. Zie het document over [privacybanen ](api/privacy-jobs.md) in de [!DNL Privacy Service] API-gids voor meer informatie. |
| Ondersteuning voor Adobe Primetime-verificatie | [!DNL Privacy Service] accepteert nu toegangs-/verwijderingsaanvragen van Adobe Primetime-verificatie, waarbij `primetimeAuthentication` wordt gebruikt als de productwaarde. Raadpleeg de [productdocumentatie voor Primetime-verificatie](https://tve.helpdocsonline.com/how-to-make-a-privacy-request) voor meer informatie. |

### Verbeteringen

* Verbeteringen van de [!DNL Privacy Service]-gebruikersinterface:
   * Afzonderlijke pagina&#39;s voor het volgen van taken voor GDPR- en CCPA-verordeningen.
   * Nieuwe vervolgkeuzelijst *Reguleringstype* om te schakelen tussen trackinggegevens voor AVG en CCPA.

## 25 juli 2019

### Nieuwe functies

| Functie | Beschrijving |
| --- | --- |
| Statistisch dashboard aanvragen | Het nieuwe dashboard met statistieken in de [!DNL Privacy Service]-gebruikersinterface biedt inzicht in verzonden, foutieve en voltooide AVG-verzoeken. |
| Builder aanvragen | Om organisaties van dienst te zijn die zowel technische als niet-technische gebruikers hebben die AVG-verzoeken verzenden, is de functionaliteit Aanvraag maken aan de gebruikersinterface toegevoegd. De mogelijkheid om JSON-bestanden in te te verzenden is nog steeds beschikbaar in de [!DNL Privacy Service]-gebruikersinterface voor organisaties die deze liever willen blijven gebruiken. |
| Gebeurtenismeldingen over GDPR-taken | Gebeurtenismeldingen over GDPR-taakstatussen zijn voor veel workflows van essentieel belang. Vroeger werden meldingen via afzonderlijke e-mailberichten verzonden, maar nu zijn GDPR-gebeurtenismeldingen berichten die gebruikmaken van Adobe I/O-gebeurtenissen, die worden verzonden naar een geconfigureerde webhook die de automatisering van taakaanvragen mogelijk maakt. Gebruikers van de [!DNL Privacy Service]-gebruikersinterface kunnen zich abonneren op Adobe I/O GDPR-gebeurtenissen om updates te ontvangen wanneer een product of de GDPR-taak is voltooid. |

## 18 april 2019

### Verbeteringen

* Het standaardbereik voor de statustabel in de [!DNL Privacy Service]-gebruikersinterface is gewijzigd naar een periode van 7 dagen.
* Betere interne afhandeling van uitzonderingen.
* Verbeterde prestaties door caching voor algemene interne aanroepen met lage snelheid van gegevenswijzigingen.

### Opgeloste problemen

* Ontbrekende logboekgegevens toegevoegd voor gefilterde zoekopdrachten voor het `GET /`-eindpunt in de [!DNL Privacy Service]-API.

## 11 april 2019

### Verbeteringen

* Bijgewerkte gebruikersinterface ter ondersteuning van nieuwe functionaliteit voor betaklanten
* Nieuwe API voor meetgegevens ter ondersteuning van functies van UI 2.0 in beta

## 9 april 2019

### Verbeteringen

* Alle (GET) API-opzoekaanroepen zijn bijgewerkt naar de standaardwaarden voor een terugzoekbereik van 30 dagen
* Beperkt API-gebruik voor een maximaal terugzoekbereik van 45 dagen

## 14 februari 2019

### Verbeteringen

* Het veld `include` afdwingen telkens wanneer POST wordt verzonden.
* Het veld `include` afdwingen tijdens het uploaden van JSON.

### Opgeloste problemen

* Er is een probleem opgelost waarbij klanten de gebruikersinterface van [!DNL Privacy Service] niet konden laden.

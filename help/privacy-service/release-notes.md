---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Opmerkingen bij de release Privacy Service
description: De meest recente releaseopmerkingen voor Adobe Experience Platform Privacy Service.
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 3%

---

# Aanvullende informatie voor [!DNL Privacy Service]

Dit document bevat informatie over nieuwe functies voor Adobe Experience Platform [!DNL Privacy Service] en over verbeteringen en belangrijke opgeloste problemen.

>[!NOTE]
>
>De recentste versienota&#39;s voor andere [!DNL Experience Platform] diensten kunnen [ hier ](../release-notes/latest/latest.md) worden gevonden.

## 9 september 2020

### Nieuwe functies

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor LGPD (Brazilië) | Privacy-banen kunnen nu worden gecreëerd onder de Braziliaanse [!DNL Lei Geral de Proteção de Dados] (LGPD)-verordening. Deze taken worden bijgehouden met de code voor regelgeving `lgpd_bra` . |

## donderdag 8 april 2020

### Nieuwe functies

| Functie | Beschrijving |
| --- | --- |
| PDPA-ondersteuning | [!DNL Privacy] -aanvragen kunnen nu worden gemaakt en bijgehouden op basis van de Personal Data Protection Act (PDPA) in Thailand. Wanneer u privacyverzoeken indient in de API, accepteert de array `regulation` de waarde &quot;pdpa_tha&quot;. |
| Naamruimtetypen in de gebruikersinterface | U kunt nu verschillende naamruimtetypen opgeven in de Request Builder in de gebruikersinterface van [!DNL Privacy Service] . Zie de [ gebruikersgids ](ui/user-guide.md) voor meer informatie. |
| Oude afleiding van eindpunt | Het oude API eindpunt (`data/privacy/gdpr`) is afgekeurd. |

## woensdag 14 januari 2020

### Nieuwe functies

| Functie | Beschrijving |
| --- | --- |
| [!DNL Privacy Service] herbranding | De voormalige naam &quot;GDPR-service&quot; is vervangen door [!DNL Privacy Service] omdat de service is gegroeid om andere regels te ondersteunen naast GDPR. |
| Nieuwe API-eindpunten | Het basispad voor de [!DNL Privacy Service] API is bijgewerkt van `/data/privacy/gdpr` tot `/data/core/privacy/jobs` |
| Nieuwe vereiste eigenschap `regulation` | Wanneer u nieuwe taken maakt in de [!DNL Privacy Service] API, moet de eigenschap `regulation` in de payload van de aanvraag worden opgegeven om aan te geven onder welke regeling de taak moet worden bijgehouden. Accepteerde waarden zijn `gdpr` en `ccpa` . Zie het document op [ privacybanen ](api/privacy-jobs.md) in de [!DNL Privacy Service] API gids voor meer informatie. |
| Ondersteuning voor Adobe Primetime-verificatie | [!DNL Privacy Service] accepteert nu toegang-/verwijderaanvragen van Adobe Primetime-verificatie, waarbij `primetimeAuthentication` wordt gebruikt als de productwaarde. Zie de [ documentatie van de Authentificatie Primetime ](https://tve.helpdocsonline.com/how-to-make-a-privacy-request) voor meer informatie. |

### Verbeteringen

* [!DNL Privacy Service] Verbeteringen van de gebruikersinterface:
   * Afzonderlijke pagina&#39;s voor het volgen van taken voor GDPR en CCPA verordeningen.
   * Het nieuwe *dropdown van het Type van Reglement 0} om tussen het volgen gegevens voor GDPR en CCPA te schakelen.*

## vrijdag 25 juli 2019

### Nieuwe functies

| Functie | Beschrijving |
| --- | --- |
| Metrische dashboard aanvragen | Het nieuwe dashboard voor metriek in [!DNL Privacy Service] UI verstrekt zicht in voorgelegde, geëiste, en voltooide GDPR- verzoeken. |
| Request Builder | Aan de dienstorganisaties met zowel technische als niet-technische gebruikers die GDPR- verzoeken indienen, is een functionaliteit &quot;Create Verzoek&quot;toegevoegd aan UI. De mogelijkheid voor het indienen van JSON-bestanden is nog steeds beschikbaar in de gebruikersinterface van [!DNL Privacy Service] voor organisaties die het bestand liever blijven gebruiken. |
| GDPR-berichten over taakgebeurtenissen | Gebeurtenismeldingen over GDPR-taakstatussen zijn voor veel workflows van essentieel belang. Terwijl meldingen eerder via afzonderlijke e-mailberichten werden verzonden, zijn GDPR-gebeurtenismeldingen berichten berichten die gebruikmaken van Adobe I/O-gebeurtenissen, die worden verzonden naar een geconfigureerde webhaak die de automatisering van taakaanvragen vergemakkelijkt. [!DNL Privacy Service] Gebruikers met een gebruikersinterface kunnen zich abonneren op Adobe I/O GDPR-gebeurtenissen om updates te ontvangen wanneer een product of de GDPR-taak is voltooid. |

## vrijdag 18 april 2019

### Verbeteringen

* Het standaardbereik voor de statustabel in de [!DNL Privacy Service] -gebruikersinterface is gewijzigd in een periode van 7 dagen.
* Betere interne afhandeling van uitzonderingen.
* Verbeterde prestaties door caching voor gemeenschappelijke interne vraag met lage tarieven van de gegevensverandering in te voeren.

### Bugfixes

* Ontbrekende logboekgegevens voor gefilterde query&#39;s voor het eindpunt `GET /` in de [!DNL Privacy Service] API toegevoegd.

## vrijdag 11 april 2019

### Verbeteringen

* Bijgewerkte gebruikersinterface ter ondersteuning van nieuwe functionaliteit voor bètaklanten
* Nieuwe API voor meetgegevens ter ondersteuning van functies van UI 2.0 in bèta

## woensdag 9 april 2019

### Verbeteringen

* Alle opzoeken (GET) API-aanroepen zijn standaard bijgewerkt naar een opzoekbereik van 30 dagen
* Beperkt API-gebruik voor een maximaal terugzoekbereik van 45 dagen

## 14 februari 2019

### Verbeteringen

* Het veld `include` afdwingen bij elke POST die wordt verzonden.
* Het veld `include` afdwingen tijdens het uploaden van JSON.

### Bugfixes

* Het probleem waarbij klanten de gebruikersinterface van [!DNL Privacy Service] niet konden laden, is opgelost.

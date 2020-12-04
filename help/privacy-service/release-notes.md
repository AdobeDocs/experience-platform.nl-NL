---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Opmerkingen bij de release Privacy Service
topic: release notes
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 5%

---


# [!DNL Privacy Service] releaseopmerkingen

Dit document bevat informatie over nieuwe functies voor Adobe Experience Platform [!DNL Privacy Service]en over verbeteringen en belangrijke opgeloste problemen.

>[!NOTE]
>
>De meest recente releaseopmerkingen voor andere [!DNL Experience Platform] services zijn [hier](../release-notes/latest/latest.md)te vinden.

## 9 september 2020

### Nieuwe functies

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor LGPD (Brazilië) | Privacy jobs kunnen nu worden gecreëerd in het kader van de Braziliaanse [!DNL Lei Geral de Proteção de Dados] (LGPD) verordening. Deze banen worden bijgehouden onder de code van de verordening `lgpd_bra`. |

## 8 april 2020

### Nieuwe functies

| Functie | Beschrijving |
| --- | --- |
| PDPA-ondersteuning | [!DNL Privacy] verzoeken kunnen nu worden opgesteld en bijgehouden op grond van de Personal Data Protection Act (PDPA) in Thailand. Wanneer u privacyverzoeken indient in de API, accepteert de `regulation` array de waarde &quot;pdpa_tha&quot;. |
| Naamruimtetypen in de gebruikersinterface | U kunt nu verschillende naamruimtetypen opgeven in de [!DNL Privacy Service] gebruikersinterface van Request Builder. Raadpleeg de [gebruikershandleiding](ui/user-guide.md) voor meer informatie. |
| Oude afleiding van eindpunt | Het oude API-eindpunt (`data/privacy/gdpr`) is vervangen. |

## 14 januari 2020

### Nieuwe functies

| Functie | Beschrijving |
| --- | --- |
| [!DNL Privacy Service] herbranding | De voormalige naam &quot;GDPR Service&quot; is omgedoopt [!DNL Privacy Service] omdat de dienst is gegroeid om andere regels naast GDPR te ondersteunen. |
| Nieuwe API-eindpunten | Het basispad voor de [!DNL Privacy Service] API is bijgewerkt van `/data/privacy/gdpr` naar `/data/core/privacy/jobs` |
| Nieuwe vereiste `regulation` eigenschap | Bij het maken van nieuwe taken in de [!DNL Privacy Service] API moet een `regulation` eigenschap worden opgegeven in de payload van de aanvraag om aan te geven welke regelgeving moet worden gebruikt om de taak onder te volgen. Accepteerde waarden zijn `gdpr` en `ccpa`. Zie het document over [privacytaken](api/privacy-jobs.md) in de [!DNL Privacy Service] ontwikkelaarsgids voor meer informatie. |
| Ondersteuning voor Adobe Primetime-verificatie | [!DNL Privacy Service] Accepteert nu toegang-/verwijderaanvragen van Adobe Primetime-verificatie, die `primetimeAuthentication` als productwaarde worden gebruikt. Zie de documentatie [van de Authentificatie](http://tve.helpdocsonline.com/how-to-make-a-privacy-request) Primetime voor meer informatie. |

### Verbeteringen

* [!DNL Privacy Service] Verbeteringen voor gebruikersinterface:
   * Afzonderlijke pagina&#39;s voor het volgen van taken voor GDPR en CCPA verordeningen.
   * Het nieuwe *Regeltype* dropdown om tussen het volgen gegevens voor GDPR en CCPA te schakelen.

## 25 juli 2019

### Nieuwe functies

| Functie | Beschrijving |
| --- | --- |
| Metrische dashboard aanvragen | Het nieuwe dashboard van metriek in [!DNL Privacy Service] UI verstrekt zicht in voorgelegde, geëiste, en voltooide GDPR- verzoeken. |
| Request Builder | Aan de dienstorganisaties met zowel technische als niet-technische gebruikers die GDPR- verzoeken indienen, is een functionaliteit &quot;Create Verzoek&quot;toegevoegd aan UI. De mogelijkheid voor het indienen van JSON-bestanden is nog steeds beschikbaar in de [!DNL Privacy Service] gebruikersinterface voor organisaties die het bestand liever blijven gebruiken. |
| GDPR-berichten over taakgebeurtenissen | Gebeurtenismeldingen over GDPR-taakstatussen zijn voor veel workflows van essentieel belang. Terwijl meldingen eerder via afzonderlijke e-mailberichten werden verzonden, zijn GDPR-gebeurtenismeldingen berichten berichten die gebruikmaken van Adobe I/O-gebeurtenissen, die worden verzonden naar een geconfigureerde webhaak die de automatisering van taakaanvragen vergemakkelijkt. [!DNL Privacy Service] UI-gebruikers kunnen zich abonneren op Adobe I/O GDPR-gebeurtenissen om updates te ontvangen wanneer een product of de GDPR-taak is voltooid. |

## 18 april 2019

### Verbeteringen

* Het standaardbereik voor de statustabel in de [!DNL Privacy Service] UI is gewijzigd in een bereik van 7 dagen.
* Betere interne uitzonderingsbehandeling.
* Verbeterde prestaties door caching voor gemeenschappelijke interne vraag met lage tarieven van de gegevensverandering in te voeren.

### Bugfixes

* Ontbrekende logboekinformatie voor gefilterde vragen voor het `GET /` eindpunt in [!DNL Privacy Service] API toegevoegd.

## 11 april 2019

### Verbeteringen

* Bijgewerkte gebruikersinterface ter ondersteuning van nieuwe functionaliteit voor bètaklanten
* Nieuwe API voor meetgegevens ter ondersteuning van functies van UI 2.0 in bèta

## 9 april 2019

### Verbeteringen

* Alle opzoeken (GET) API-aanroepen zijn standaard bijgewerkt naar een opzoekbereik van 30 dagen
* Beperkt API-gebruik voor een maximaal terugzoekbereik van 45 dagen

## 14 februari 2019

### Verbeteringen

* Het `include` veld afdwingen bij elke POST die wordt verzonden.
* Het `include` veld tijdens het uploaden van JSON afdwingen.

### Bugfixes

* Probleem verholpen waarbij klanten de [!DNL Privacy Service] gebruikersinterface niet konden laden.
---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Opmerkingen bij de release Privacy Service
topic: release notes
description: De meest recente releaseopmerkingen voor Adobe Experience Platform Privacy Service.
translation-type: tm+mt
source-git-commit: 5dad1fcc82707f6ee1bf75af6c10d34ff78ac311
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 5%

---


# [!DNL Privacy Service] releaseopmerkingen

Dit document bevat informatie over nieuwe functies voor Adobe Experience Platform [!DNL Privacy Service] en over verbeteringen en belangrijke opgeloste problemen.

>[!NOTE]
>
>De meest recente releaseopmerkingen voor andere [!DNL Experience Platform]-services vindt u [hier](../release-notes/latest/latest.md).

## 9 september 2020

### Nieuwe functies

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor LGPD (Brazilië) | De banen van de privacy kunnen nu onder de [!DNL Lei Geral de Proteção de Dados] (LGPD) verordening van Brazilië worden gecreeerd. Deze taken worden bijgehouden onder de regelgevingscode `lgpd_bra`. |

## 8 april 2020

### Nieuwe functies

| Functie | Beschrijving |
| --- | --- |
| PDPA-ondersteuning | [!DNL Privacy] verzoeken kunnen nu worden opgesteld en bijgehouden op grond van de Personal Data Protection Act (PDPA) in Thailand. Bij het indienen van privacyverzoeken in de API accepteert de `regulation`-array de waarde &quot;pdpa_tha&quot;. |
| Naamruimtetypen in de gebruikersinterface | U kunt nu verschillende naamruimtetypen opgeven in de interface [!DNL Privacy Service]. Zie [gebruikershandleiding](ui/user-guide.md) voor meer informatie. |
| Oude afleiding van eindpunt | Het oude API eindpunt (`data/privacy/gdpr`) is afgekeurd. |

## 14 januari 2020

### Nieuwe functies

| Functie | Beschrijving |
| --- | --- |
| [!DNL Privacy Service] herbranding | De voormalige naam &quot;GDPR-service&quot; is vervangen door [!DNL Privacy Service] omdat de service is gegroeid om andere regels naast GDPR te ondersteunen. |
| Nieuwe API-eindpunten | Het basispad voor de [!DNL Privacy Service]-API is bijgewerkt van `/data/privacy/gdpr` naar `/data/core/privacy/jobs` |
| Nieuwe vereiste `regulation`-eigenschap | Wanneer u nieuwe taken maakt in de [!DNL Privacy Service]-API, moet een `regulation`-eigenschap worden opgegeven in de payload van de aanvraag om aan te geven onder welke verordening de taak moet worden bijgehouden. Accepteerde waarden zijn `gdpr` en `ccpa`. Zie het document over [privacytaken](api/privacy-jobs.md) in de [!DNL Privacy Service]-handleiding voor ontwikkelaars voor meer informatie. |
| Ondersteuning voor Adobe Primetime-verificatie | [!DNL Privacy Service] Accepteert nu toegang-/verwijderaanvragen van Adobe Primetime-verificatie,  `primetimeAuthentication` die worden gebruikt als de productwaarde. Zie [Primetime-verificatiedocumentatie](http://tve.helpdocsonline.com/how-to-make-a-privacy-request) voor meer informatie. |

### Verbeteringen

* [!DNL Privacy Service] Verbeteringen voor gebruikersinterface:
   * Afzonderlijke pagina&#39;s voor het volgen van taken voor GDPR en CCPA verordeningen.
   * Nieuwe *Regeltype* dropdown om tussen het volgen gegevens voor GDPR en CCPA te schakelen.

## 25 juli 2019

### Nieuwe functies

| Functie | Beschrijving |
| --- | --- |
| Metrische dashboard aanvragen | Het nieuwe dashboard van metriek in [!DNL Privacy Service] UI verstrekt zicht in voorgelegde, errored, en voltooide GDPR- verzoeken. |
| Request Builder | Aan de dienstorganisaties met zowel technische als niet-technische gebruikers die GDPR- verzoeken indienen, is een functionaliteit &quot;Create Verzoek&quot;toegevoegd aan UI. De mogelijkheid voor het indienen van JSON-bestanden is nog steeds beschikbaar in de gebruikersinterface van [!DNL Privacy Service] voor organisaties die deze functie liever blijven gebruiken. |
| GDPR-berichten over taakgebeurtenissen | Gebeurtenismeldingen over GDPR-taakstatussen zijn voor veel workflows van essentieel belang. Terwijl meldingen eerder via afzonderlijke e-mailberichten werden verzonden, zijn GDPR-gebeurtenismeldingen berichten berichten die gebruikmaken van Adobe I/O-gebeurtenissen, die worden verzonden naar een geconfigureerde webhaak die de automatisering van taakaanvragen vergemakkelijkt. [!DNL Privacy Service] UI-gebruikers kunnen zich abonneren op Adobe I/O GDPR-gebeurtenissen om updates te ontvangen wanneer een product of de GDPR-taak is voltooid. |

## 18 april 2019

### Verbeteringen

* Het standaardbereik voor de statustabel in de gebruikersinterface van [!DNL Privacy Service] is gewijzigd in een bereik van 7 dagen.
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

* Het veld `include` in elke POST-verzending afdwingen.
* Het veld `include` tijdens het uploaden van JSON afdwingen.

### Bugfixes

* Probleem verholpen waarbij klanten de interface [!DNL Privacy Service] niet konden laden.
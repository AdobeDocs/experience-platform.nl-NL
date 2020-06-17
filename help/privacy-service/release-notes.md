---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Opmerkingen bij de release Privacy Service
topic: release notes
translation-type: tm+mt
source-git-commit: 580cce74ab7da9547417a9e74e88b5ddab52171f
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 5%

---


# Opmerkingen bij de release Privacy Service

Dit document bevat informatie over nieuwe functies voor Adobe Experience Platform Privacy Service en over verbeteringen en belangrijke opgeloste problemen.

>[!NOTE] De meest recente releaseopmerkingen voor andere services van Experience Platforms vindt u [hier](../release-notes/latest/latest.md).

## 8 april 2020

### Nieuwe functies

| Functie | Beschrijving |
| --- | --- |
| PDPA-ondersteuning | De verzoeken van de privacy kunnen nu worden gecreeerd en worden gevolgd onder de Wet van de Bescherming van Persoonlijke Gegevens (PDPA) in Thailand. Wanneer u privacyverzoeken indient in de API, accepteert de `regulation` array de waarde &quot;pdpa_tha&quot;. |
| Naamruimtetypen in de gebruikersinterface | U kunt nu verschillende naamruimtetypen opgeven in de Aanvraag Builder in de gebruikersinterface van de Privacy Service. Raadpleeg de [gebruikershandleiding](ui/user-guide.md) voor meer informatie. |
| Oude afleiding van eindpunt | Het oude API-eindpunt (`data/privacy/gdpr`) is vervangen. |

## 14 januari 2020

### Nieuwe functies

| Functie | Beschrijving |
| --- | --- |
| Privacy Service herbranding | De voormalige naam &quot;GDPR-dienst&quot; is hernoemd tot Privacy Service, aangezien de dienst is gegroeid om andere voorschriften naast GDPR te ondersteunen. |
| Nieuwe API-eindpunten | Het basispad voor de Privacy Service-API is bijgewerkt van `/data/privacy/gdpr` naar `/data/core/privacy/jobs` |
| Nieuwe vereiste `regulation` eigenschap | Bij het creëren van nieuwe banen in Privacy Service API, moet een `regulation` bezit in de verzoeklading worden geleverd om te wijzen op welke regeling om de baan onder te volgen. Accepteerde waarden zijn `gdpr` en `ccpa`. Zie het document over [privacytaken](api/privacy-jobs.md) in de ontwikkelaarsgids voor Privacys Service voor meer informatie. |
| Ondersteuning voor Adobe Primetime-verificatie | Privacy Service accepteert nu toegang-/verwijderaanvragen van Adobe Primetime-verificatie, die worden gebruikt `primetimeAuthentication` als de productwaarde. Zie de documentatie [van de Authentificatie](http://tve.helpdocsonline.com/how-to-make-a-privacy-request) Primetime voor meer informatie. |

### Verbeteringen

* Verbeteringen in de gebruikersinterface van Privacy Service:
   * Afzonderlijke pagina&#39;s voor het volgen van taken voor GDPR en CCPA verordeningen.
   * Het nieuwe _Regeltype_ dropdown om tussen het volgen gegevens voor GDPR en CCPA te schakelen.

## 25 juli 2019

### Nieuwe functies

| Functie | Beschrijving |
| --- | --- |
| Metrische dashboard aanvragen | Het nieuwe dashboard van metriek in UI van de Privacy Service verstrekt zicht in voorgelegde, geëiste, en voltooide GDPR- verzoeken. |
| Request Builder | Aan de dienstorganisaties met zowel technische als niet-technische gebruikers die GDPR- verzoeken indienen, is een functionaliteit &quot;Create Verzoek&quot;toegevoegd aan UI. De mogelijkheid voor het indienen van JSON-bestanden is nog steeds beschikbaar in de gebruikersinterface van de Privacy Service voor organisaties die het bestand liever blijven gebruiken. |
| GDPR-berichten over taakgebeurtenissen | Gebeurtenismeldingen over GDPR-taakstatussen zijn voor veel workflows van essentieel belang. Hoewel meldingen eerder via afzonderlijke e-mailberichten zijn verzonden, zijn GDPR-gebeurtenismeldingen berichten die gebruikmaken van Adobe I/O-gebeurtenissen. Deze berichten worden verzonden naar een geconfigureerde webhaak die de automatisering van taakaanvragen vergemakkelijkt. Gebruikers in de gebruikersinterface van Privacys Service kunnen zich abonneren op Adobe I/O GDPR-gebeurtenissen om updates te ontvangen wanneer een product of de GDPR-taak is voltooid. |

## 18 april 2019

### Verbeteringen

* Het standaardbereik voor de statustabel in de gebruikersinterface van de Privacy Service is gewijzigd in een bereik van 7 dagen.
* Betere interne uitzonderingsbehandeling.
* Verbeterde prestaties door caching voor gemeenschappelijke interne vraag met lage tarieven van de gegevensverandering in te voeren.

### Bugfixes

* Ontbrekende logboekinformatie voor gefilterde vragen voor het `GET /` eindpunt in Privacy Service API toegevoegd.

## 11 april 2019

### Verbeteringen

* Bijgewerkte gebruikersinterface ter ondersteuning van nieuwe functionaliteit voor bètaklanten
* Nieuwe API voor meetgegevens ter ondersteuning van functies van UI 2.0 in bèta

## 9 april 2019

### Verbeteringen

* Alle opzoekings (GET) API-aanroepen zijn standaard bijgewerkt naar een opzoekbereik van 30 dagen
* Beperkt API-gebruik voor een maximaal terugzoekbereik van 45 dagen

## 14 februari 2019

### Verbeteringen

* Het `include` veld afdwingen bij elke POST-verzending.
* Het `include` veld tijdens het uploaden van JSON afdwingen.

### Bugfixes

* Probleem verholpen waarbij klanten de interface van de Privacy Service niet konden laden.
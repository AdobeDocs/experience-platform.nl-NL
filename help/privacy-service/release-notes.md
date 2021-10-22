---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Opmerkingen bij de release Privacy Service
topic-legacy: release notes
description: De meest recente releaseopmerkingen voor Adobe Experience Platform Privacy Service.
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: 82dea48c732b3ddea957511c22f90bbd032ed9b7
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 6%

---

# [!DNL Privacy Service] - aanvullende informatie

Dit document bevat informatie over nieuwe functies voor Adobe Experience Platform [!DNL Privacy Service], alsmede verbeteringen en belangrijke opgeloste problemen.

>[!NOTE]
>
>De meest recente releaseopmerkingen voor andere [!DNL Experience Platform] de diensten kunnen worden gevonden [hier](../release-notes/latest/latest.md).

## 9 september 2020

### Nieuwe functies

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor LGPD (Brazilië) | In Brazilië kunnen nu privacybanen worden gecreëerd [!DNL Lei Geral de Proteção de Dados] (LGPD) regelgeving. Deze banen worden bijgehouden in het kader van de regelgevingscode `lgpd_bra`. |

## 8 april 2020

### Nieuwe functies

| Functie | Beschrijving |
| --- | --- |
| PDPA-ondersteuning | [!DNL Privacy] verzoeken kunnen nu worden opgesteld en bijgehouden op grond van de Personal Data Protection Act (PDPA) in Thailand. Wanneer u een privacyverzoek indient in de API, wordt de `regulation` array accepteert de waarde &quot;pdpa_tha&quot;. |
| Naamruimtetypen in de gebruikersinterface | U kunt nu verschillende naamruimtetypen opgeven in de Request Builder in het dialoogvenster [!DNL Privacy Service] UI. Zie de [gebruikershandleiding](ui/user-guide.md) voor meer informatie . |
| Oude afleiding van eindpunt | Het oude API-eindpunt (`data/privacy/gdpr`) is vervangen. |

## 14 januari 2020

### Nieuwe functies

| Functie | Beschrijving |
| --- | --- |
| [!DNL Privacy Service] herbranding | De voormalige naam &quot;GDPR Service&quot; is hernoemd naar [!DNL Privacy Service] aangezien de dienst is gegroeid om andere voorschriften naast de GDPR te ondersteunen. |
| Nieuwe API-eindpunten | Basispad voor de [!DNL Privacy Service] API is bijgewerkt vanaf `/data/privacy/gdpr` tot `/data/core/privacy/jobs` |
| Nieuw vereist `regulation` eigenschap | Wanneer u nieuwe taken maakt in het dialoogvenster [!DNL Privacy Service] API, a `regulation` de goederen moeten in de lading van het verzoek worden geleverd om aan te geven welke regeling moet worden toegepast om de functie onder te houden. Accepteerde waarden zijn `gdpr` en `ccpa`. Document weergeven op [privacytaken](api/privacy-jobs.md) in de [!DNL Privacy Service] API-handleiding voor meer informatie. |
| Ondersteuning voor Adobe Primetime-verificatie | [!DNL Privacy Service] accepteert nu toegang-/verwijderaanvragen van Adobe Primetime-verificatie, met `primetimeAuthentication` als productwaarde. Zie de [Primetime-verificatiedocumentatie](http://tve.helpdocsonline.com/how-to-make-a-privacy-request) voor meer informatie . |

### Verbeteringen

* [!DNL Privacy Service] Verbeteringen voor gebruikersinterface:
   * Afzonderlijke pagina&#39;s voor het volgen van taken voor GDPR en CCPA verordeningen.
   * Nieuw *Type verordening* dropdown om tussen het volgen gegevens voor GDPR en CCPA te schakelen.

## 25 juli 2019

### Nieuwe functies

| Functie | Beschrijving |
| --- | --- |
| Metrische dashboard aanvragen | Het nieuwe metrieke dashboard in het dialoogvenster [!DNL Privacy Service] UI verstrekt zicht in voorgelegde, errored, en voltooide GDPR- verzoeken. |
| Request Builder | Aan de dienstorganisaties met zowel technische als niet-technische gebruikers die GDPR- verzoeken indienen, is een functionaliteit &quot;Create Verzoek&quot;toegevoegd aan UI. De JSON-mogelijkheid voor het indienen van bestanden is nog steeds beschikbaar in de [!DNL Privacy Service] UI voor die organisaties die het verkiezen blijven gebruiken. |
| GDPR-berichten over taakgebeurtenissen | Gebeurtenismeldingen over GDPR-taakstatussen zijn voor veel workflows van essentieel belang. Terwijl meldingen eerder via afzonderlijke e-mailberichten werden verzonden, zijn GDPR-gebeurtenismeldingen berichten berichten die gebruikmaken van Adobe I/O-gebeurtenissen, die worden verzonden naar een geconfigureerde webhaak die de automatisering van taakaanvragen vergemakkelijkt. [!DNL Privacy Service] UI-gebruikers kunnen zich abonneren op Adobe I/O GDPR-gebeurtenissen om updates te ontvangen wanneer een product of de GDPR-taak is voltooid. |

## 18 april 2019

### Verbeteringen

* Standaardbereik voor de statustabel in het dialoogvenster [!DNL Privacy Service] De gebruikersinterface is gewijzigd in een periode van 7 dagen.
* Betere interne uitzonderingsbehandeling.
* Verbeterde prestaties door caching voor gemeenschappelijke interne vraag met lage tarieven van de gegevensverandering in te voeren.

### Bugfixes

* Ontbrekende logboekinformatie voor gefilterde query&#39;s voor de code toegevoegd `GET /` in de [!DNL Privacy Service] API.

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

* De `include` in elke POST die wordt ingediend.
* De `include` veld tijdens het uploaden van JSON.

### Bugfixes

* Het probleem waarbij klanten de [!DNL Privacy Service] UI.

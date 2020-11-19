---
keywords: facebook extensions;facebook extension;facebook destinations;facebook;instagram;messenger;facebook messenger
title: Facebook-bestemming
seo-title: Facebook-bestemming
description: Activeer profielen voor uw Facebook-campagnes voor doelgroepen, personalisatie en onderdrukking op basis van gehakte e-mails.
seo-description: Activeer profielen voor uw Facebook-campagnes voor doelgroepen, personalisatie en onderdrukking op basis van gehakte e-mails.
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 4%

---


# [!DNL Facebook] Bestemming

## Overzicht {#overview}

Activeer profielen voor uw [!DNL Facebook] campagnes voor doelgroepen, personalisatie en onderdrukking op basis van gehakte e-mails.

U kunt deze bestemming gebruiken voor doelgroepen voor verschillende [!DNL Facebook’s] apps die worden ondersteund door [!DNL Custom Audiences], inclusief [!DNL Facebook], [!DNL Instagram][!DNL Audience Network] en [!DNL Messenger]. De selectie van de app waarin u de campagne wilt voeren, wordt aangegeven op het plaatsingsniveau in [!DNL Facebook Ads Manager].

![De bestemming van Facebook in Echte - tijd CDP UI](/help/rtcdp/destinations/assets/facebook-destination.png)


## Gevallen gebruiken

Om u beter te helpen begrijpen hoe en wanneer u de [!DNL Facebook] bestemming zou moeten gebruiken, zijn hier twee gevallen van het steekproefgebruik die de klanten in real time van de Gegevens van de Klant kunnen oplossen door deze eigenschap te gebruiken.


### Hoofdletters en kleine letters gebruiken 1


Een online detailhandelaar wil bestaande klanten door sociale platforms bereiken en hen gepersonaliseerde aanbiedingen tonen die op hun vorige orden worden gebaseerd. De online detailhandelaar kan e-mailadressen van hun eigen CRM aan Adobe in real time CDP opnemen, segmenten van hun eigen off-line gegevens bouwen, en deze segmenten naar het [!DNL Facebook] sociale platform verzenden, die hun reclame-uitgaven optimaliseren.


### Hoofdletters en kleine letters gebruiken 2


Een luchtvaartmaatschappij heeft verschillende klantniveaus (Bronze, Silver en Gold) en wil elk niveau via sociale platforms voorzien van persoonlijke aanbiedingen. Niet alle klanten gebruiken echter de mobiele app van de luchtvaartmaatschappij en sommige van hen hebben zich niet aangemeld bij de website van het bedrijf. De enige id&#39;s die het bedrijf over deze klanten heeft, zijn id&#39;s voor lidmaatschap en e-mailadressen.

Om hen over sociale media te richten, kunnen zij de klantengegevens van hun CRM in Adobe in real time CDP betreden, gebruikend de e-mailadressen als herkenningstekens.

Daarna, kunnen zij hun off-line gegevens met inbegrip van bijbehorende lidmaatschap IDs en klantenrijen gebruiken om nieuwe publiekssegmenten te bouwen die zij door de [!DNL Facebook] bestemming kunnen richten.

## Doelspecificaties {#destination-specs}

### Gegevensbeheer voor [!DNL Facebook] bestemmingen {#data-governance}

>[!IMPORTANT]
>
>De gegevens die naar [!DNL Facebook] worden verzonden, mogen geen gestippelde identiteiten bevatten. U bent verantwoordelijk voor het nakomen van deze verplichting en kunt dit doen door ervoor te zorgen dat de segmenten die voor activering worden geselecteerd geen het stitching optie in hun fusiebeleid gebruiken. Meer weten over [samenvoegbeleid](/help/profile/ui/merge-policies.md)?

### Exporttype {#export-type}

**Segmentexport** - u exporteert alle leden van een segment (publiek) met de id&#39;s (naam, telefoonnummer, enzovoort) gebruikt in de Facebook-bestemming.

### Voorwaarden voor Facebook-accounts {#facebook-account-prerequisites}

Voordat u publiekssegmenten kunt verzenden naar [!DNL Facebook], moet u controleren of aan de volgende vereisten wordt voldaan:

1. Voor uw [!DNL Facebook] gebruikersaccount moet de **[!DNL Manage campaigns]** machtiging zijn ingeschakeld voor de advertentieaccount die u wilt gebruiken.
2. Add the **Adobe Experience Cloud** business account as an advertising partner in your [!DNL Facebook Ad Account]. Gebruik `business ID=206617933627973`. Zie Partners [toevoegen aan uw Business Manager](https://www.facebook.com/business/help/1717412048538897) in de Facebook-documentatie voor meer informatie.
   >[!IMPORTANT]
   >
   > When configuring the permissions for Adobe Experience Cloud, you must enable the **Manage campaigns** permission. Dit is nodig voor de [!DNL Adobe Real-time CDP]-integratie.
3. Lees en onderteken de [!DNL Facebook Custom Audiences] Servicevoorwaarden. Ga daarvoor naar `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, waarbij `accountID` uw [!DNL Facebook Ad Account ID] is.

### Vereisten voor e-mailhashing {#email-hashing-requirements}

[!DNL Facebook] vereist dat er geen duidelijk identificeerbare informatie (PII) wordt verstrekt. Daarom [!DNL Facebook] moet het publiek dat wordt geactiveerd om *gehashte* e-mailadressen worden afgevinkt. U kunt ervoor kiezen e-mailadressen te hashen alvorens hen in Adobe Experience Platform op te nemen, of u kunt verkiezen om met e-mailadressen in duidelijk Experience Platform te werken en onze algoritme te hebben hen op activering hakt.

Als u meer wilt weten over het invoeren van e-mailadressen in Experience Platforms, raadpleegt u het [overzicht](/help/ingestion/batch-ingestion/overview.md) van het gebruik van batches en het [overzicht](/help/ingestion/streaming-ingestion/overview.md)van het opnemen van tags.

Als u ervoor kiest om de e-mailadressen zelf te hashen, moet u aan de volgende vereisten voldoen:

* Alle spaties aan het begin en aan het einde uit de e-mailtekenreeks bijsnijden. voorbeeld: `johndoe@example.com`, niet `<space>johndoe@example.com<space>`;
* Wanneer u de e-mailtekenreeksen hasht, moet u de kleine-lettertekenreeks hashen.
   * Voorbeeld: `example@email.com`, niet `EXAMPLE@EMAIL.COM`;
* Controleer of de hashtekenreeks in kleine letters staat
   * Voorbeeld: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, niet `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Zilp de tekenreeks niet.


>[!IMPORTANT]
>
>Als u ervoor kiest geen e-mailadressen te hacken, zal Adobe in real time CDP dat voor u doen wanneer u segmenten aan activeert. [!DNL Facebook] Selecteer in de [activeringsworkflow](/help/rtcdp/destinations/activate-destinations.md#activate-data) (zie stap 5) de `Email` optie die hieronder wordt weergegeven voor *onbewerkte e-mailadressen* en `Email_LC_SHA256` voor *gehashte e-mailadressen*.


![Hashing bij activering](/help/rtcdp/destinations/assets/identity-mapping.png)

## Verbinden met doel {#connect-destination}

Om met de [!DNL Facebook] bestemming te verbinden, zie het de authentificatiewerkschema [van](/help/rtcdp/destinations/social-network-destinations-workflow.md)Sociale netwerkbestemmingen.


## Segmenten activeren om [!DNL Facebook] {#activate-segments}

Voor instructies op hoe te om segmenten te activeren, zie [!DNL Facebook]Gegevens aan Doelen [](/help/rtcdp/destinations/activate-destinations.md)activeren.

## Geëxporteerde gegevens {#exported-data}

Een geslaagde activering betekent [!DNL Facebook]bijvoorbeeld dat er via programmacode een [!DNL Facebook] aangepast publiek wordt gemaakt [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Het lidmaatschap van een segment in het publiek zou worden toegevoegd en verwijderd aangezien de gebruikers voor de geactiveerde segmenten worden gekwalificeerd of worden uitgesloten.

>[!TIP]
>
>De integratie tussen Adobe in real time CDP en [!DNL Facebook] steunt historische publieksbackfills. Alle historische segmentkwalificaties worden verzonden naar [!DNL Facebook] wanneer u de segmenten naar de bestemming activeert.
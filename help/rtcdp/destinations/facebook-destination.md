---
title: Facebook-bestemming
seo-title: Facebook-bestemming
description: Activeer profielen voor uw Facebook-campagnes voor doelgroepen, personalisatie en onderdrukking op basis van gehakte e-mails.
seo-description: Activeer profielen voor uw Facebook-campagnes voor doelgroepen, personalisatie en onderdrukking op basis van gehakte e-mails.
translation-type: tm+mt
source-git-commit: 79aecf4955507622ac7879c148cdcd23e893dd65
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---


# Facebook-bestemming

## Overzicht {#overview}

Activeer profielen voor uw Facebook-campagnes voor doelgroepen, personalisatie en onderdrukking op basis van gehakte e-mails.

![De bestemming van Facebook in Echte - tijd CDP UI](/help/rtcdp/destinations/assets/facebook-destination.png)

## Gevallen gebruiken

Om u beter te helpen begrijpen hoe en wanneer u de bestemming van Facebook zou moeten gebruiken, zijn er twee voorbeelden van gebruiksgevallen die de klanten van het Platform van de Gegevens van de Klant van Adobe in real time door deze eigenschap kunnen oplossen.


### Hoofdletters en kleine letters gebruiken 1


Een online detailhandelaar wil bestaande klanten door sociale platforms bereiken en hen gepersonaliseerde aanbiedingen tonen die op hun vorige orden worden gebaseerd. De online detailhandelaar kan e-mailadressen van hun eigen CRM aan Adobe in real time CDP opnemen, segmenten van hun eigen off-line gegevens bouwen, en deze segmenten naar het sociale platform van Facebook verzenden, die hun reclame-uitgaven optimaliseren.


### Hoofdletters en kleine letters gebruiken 2


Een luchtvaartmaatschappij heeft verschillende klantniveaus (Bronze, Silver en Gold) en wil elk niveau via sociale platforms voorzien van persoonlijke aanbiedingen. Niet alle klanten gebruiken echter de mobiele app van de luchtvaartmaatschappij en sommige van hen hebben zich niet aangemeld bij de website van het bedrijf. De enige id&#39;s die het bedrijf over deze klanten heeft, zijn id&#39;s voor lidmaatschap en e-mailadressen.

Als ze zich op sociale media willen richten, kunnen ze de klantgegevens van hun CRM in Adobe Real-time CDP opnemen, waarbij de e-mailadressen als id&#39;s worden gebruikt.

Vervolgens kunnen ze hun offlinegegevens gebruiken, inclusief de bijbehorende id&#39;s voor lidmaatschap en klantlagen, om nieuwe publiekssegmenten te maken die ze via de Facebook-bestemming kunnen gebruiken.

## Doelspecificaties {#destination-specs}

### Gegevensbeheer voor Facebook-bestemmingen {#data-governance}

>[!IMPORTANT]
>
>Gegevens die naar Facebook worden verzonden, mogen geen naastgelegen identiteiten bevatten. U bent verantwoordelijk voor het nakomen van deze verplichting en kunt dit doen door ervoor te zorgen dat de segmenten die voor activering worden geselecteerd geen het stitching optie in hun fusiebeleid gebruiken. Meer weten over [samenvoegbeleid](/help/profile/ui/merge-policies.md)?

### Activeringstype {#activation-type}

**Segmentexport** - u exporteert alle leden van een segment (publiek) met de id&#39;s (naam, telefoonnummer, enzovoort) gebruikt in de Facebook-bestemming.

### Voorwaarden voor Facebook-accounts {#facebook-account-prerequisites}

Voordat u publiekssegmenten kunt verzenden naar [!DNL Facebook], moet u controleren of aan de volgende vereisten wordt voldaan:

1. Voor uw [!DNL Facebook] gebruikersaccount moet de **[!DNL Manage campaigns]** machtiging zijn ingeschakeld voor de advertentieaccount die u wilt gebruiken.
2. Voeg het **Adobe Experience Cloud** -bedrijfsaccount toe als een advertentiepartner in uw [!DNL Facebook Ad Account]. Gebruik `business ID=206617933627973`. Zie Partners [toevoegen aan uw Business Manager](https://www.facebook.com/business/help/1717412048538897) in de Facebook-documentatie voor meer informatie.
   >[!IMPORTANT]
   > Wanneer u de machtigingen voor Adobe Experience Cloud configureert, moet u de machtiging **Campagnes** beheren inschakelen. Dit is nodig voor de [!DNL Adobe Real-time CDP] integratie.
3. Lees en onderteken de [!DNL Facebook Custom Audiences] Servicevoorwaarden. Om dit te doen, ga naar `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, waar `accountID` is je [!DNL Facebook Ad Account ID].

### Vereisten voor e-mailhashing {#email-hashing-requirements}

Facebook vereist dat geen PII (Personal Identified Information) duidelijk wordt verzonden. Het publiek dat op Facebook wordt geactiveerd, moet daarom worden afgevinkt van *gehashte* e-mailadressen. U kunt ervoor kiezen e-mailadressen te hacken voordat u ze in het Adobe Experience Platform opneemt. U kunt er ook voor kiezen om met e-mailadressen te werken in het Experience Platform en deze bij activering door onze algoritme te laten hashen.

Als u meer wilt weten over het invoeren van e-mailadressen in het Experience Platform, raadpleegt u het [overzicht](/help/ingestion/batch-ingestion/overview.md) van het gebruik van batches en het [overzicht](/help/ingestion/streaming-ingestion/overview.md)van het opnemen van tags.

Als u ervoor kiest om de e-mailadressen zelf te hashen, moet u aan de volgende vereisten voldoen:

* Alle spaties aan het begin en aan het einde uit de e-mailtekenreeks bijsnijden. voorbeeld: `johndoe@example.com`, niet `<space>johndoe@example.com<space>`;
* Wanneer u de e-mailtekenreeksen hasht, moet u de kleine-lettertekenreeks hashen.
   * Voorbeeld: `example@email.com`, niet `EXAMPLE@EMAIL.COM`;
* Controleer of de hashtekenreeks in kleine letters staat
   * Voorbeeld: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, niet `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Zilp de tekenreeks niet.


>[!IMPORTANT]
>
>Als u ervoor kiest geen e-mailadressen te hashen, doet Adobe Real-time CDP dat voor u wanneer u segmenten op Facebook activeert. Selecteer in de [activeringsworkflow](/help/rtcdp/destinations/activate-destinations.md#activate-data) (zie stap 5) de `Email` optie die hieronder wordt weergegeven voor *onbewerkte e-mailadressen* en `Email_LC_SHA256` voor *gehashte e-mailadressen*.


![Hashing bij activering](/help/rtcdp/destinations/assets/identity-mapping.png)

## Verbinden met doel {#connect-destination}

Als u verbinding wilt maken met de Facebook-bestemming, raadpleegt u de verificatieworkflow voor [sociale netwerkdoelen](/help/rtcdp/destinations/social-network-destinations-workflow.md).


## Segmenten activeren op Facebook {#activate-segments}

Zie Gegevens [naar doelen](/help/rtcdp/destinations/activate-destinations.md)activeren voor instructies over het activeren van segmenten op Facebook.
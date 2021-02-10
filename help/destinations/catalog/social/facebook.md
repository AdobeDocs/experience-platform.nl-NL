---
keywords: facebook extensies;facebook extension;facebook bestemmingen;facebook;instagram;messenger;facebook messenger
title: Facebook-extensie
description: Activeer profielen voor uw Facebook-campagnes voor doelgroepen, personalisatie en onderdrukking op basis van gehakte e-mails.
translation-type: tm+mt
source-git-commit: e13a19640208697665b0a7e0106def33fd1e456d
workflow-type: tm+mt
source-wordcount: '951'
ht-degree: 3%

---


# [!DNL Facebook] extension

>[!IMPORTANT]
>
>De migratie van de klant naar de nieuwe doelversies wordt momenteel uitgevoerd. Totdat de migratie is voltooid, ziet u alleen de [!UICONTROL EMAIL] en [!UICONTROL EMAIL_LC_SHA_256] beschikbare identiteiten voor deze bestemming.

Activeer profielen voor uw [!DNL Facebook] campagnes voor doelgroepen, personalisatie en onderdrukking op basis van gehakte e-mails.

U kunt deze bestemming voor publiek gebruiken richtend zich over [!DNL Facebook’s] familie van apps die door [!DNL Custom Audiences], met inbegrip van [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] en [!DNL Messenger] worden gesteund. De selectie van de app waarin u de campagne wilt voeren, wordt aangegeven op het plaatsingsniveau in [!DNL Facebook Ads Manager].

![Facebook-bestemming in de gebruikersinterface van Adobe Experience Platform](../../assets/catalog/social/facebook/catalog.png)

## Gevallen gebruiken

Om u beter te helpen begrijpen hoe en wanneer u [!DNL Facebook] bestemming zou moeten gebruiken, zijn hier twee voorbeelden gebruiksgevallen die de klanten van Adobe Experience Platform door deze eigenschap kunnen oplossen.

### Hoofdletters en kleine letters gebruiken 1

Een online detailhandelaar wil bestaande klanten door sociale platforms bereiken en hen gepersonaliseerde aanbiedingen tonen die op hun vorige orden worden gebaseerd. De online detailhandelaar kan e-mailadressen van hun eigen CRM aan Adobe Experience Platform opnemen, segmenten van hun eigen off-line gegevens bouwen, en deze segmenten naar het [!DNL Facebook] sociale platform verzenden, die hun reclame-uitgaven optimaliseren.

### Hoofdletters en kleine letters gebruiken 2

Een luchtvaartmaatschappij heeft verschillende klantniveaus (Bronze, Silver en Gold) en wil elk niveau via sociale platforms voorzien van persoonlijke aanbiedingen. Niet alle klanten gebruiken echter de mobiele app van de luchtvaartmaatschappij en sommige van hen hebben zich niet aangemeld bij de website van het bedrijf. De enige id&#39;s die het bedrijf over deze klanten heeft, zijn id&#39;s voor lidmaatschap en e-mailadressen.

Om hen over sociale media te richten, kunnen zij de klantengegevens van hun CRM aan boord nemen in Adobe Experience Platform, gebruikend de e-mailadressen als herkenningstekens.

Daarna, kunnen zij hun off-line gegevens met inbegrip van bijbehorende lidmaatschap IDs en klantenrijen gebruiken om nieuwe publiekssegmenten te bouwen die zij door de [!DNL Facebook] bestemming kunnen richten.

## Doelspecificaties {#destination-specs}

### Gegevensbeheer voor [!DNL Facebook] doelen {#data-governance}

>[!IMPORTANT]
>
>Gegevens die naar [!DNL Facebook] worden verzonden, mogen geen naastgelegen identiteiten bevatten. U bent verantwoordelijk voor het nakomen van deze verplichting en kunt dit doen door ervoor te zorgen dat de segmenten die voor activering worden geselecteerd geen het stitching optie in hun fusiebeleid gebruiken. Meer informatie over [samenvoegbeleid](/help/profile/ui/merge-policies.md).

### Exporttype {#export-type}

**Segmentexport** : u exporteert alle leden van een segment (publiek) met de id&#39;s (naam, telefoonnummer, enzovoort) gebruikt in de Facebook-bestemming.

### Voorwaarden voor Facebook-account {#facebook-account-prerequisites}

Voordat u publiekssegmenten kunt verzenden naar [!DNL Facebook], moet u controleren of aan de volgende vereisten is voldaan:

- Voor uw [!DNL Facebook]-gebruikersaccount moet de **[!DNL Manage campaigns]**-machtiging zijn ingeschakeld voor de advertentiaccount die u wilt gebruiken.
- De **Adobe Experience Cloud** bedrijfsrekening moet als advertentiepartner in uw [!DNL Facebook Ad Account] worden toegevoegd. Gebruik `business ID=206617933627973`. Zie [Partners toevoegen aan uw Business Manager](https://www.facebook.com/business/help/1717412048538897) in de Facebook-documentatie voor meer informatie.
   >[!IMPORTANT]
   >
   > Wanneer het vormen van de toestemmingen voor Adobe Experience Cloud, moet u **Manage campagnes** toestemming toelaten. Dit is nodig voor de [!DNL Adobe Experience Platform]-integratie.
- Lees en onderteken de [!DNL Facebook Custom Audiences] Servicevoorwaarden. Ga daarvoor naar `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, waarbij `accountID` uw [!DNL Facebook Ad Account ID] is.

### Overeenkomende vereisten {#id-matching-requirements}

[!DNL Facebook] vereist dat er geen duidelijk identificeerbare informatie (PII) wordt verstrekt. Daarom kan het publiek dat aan [!DNL Facebook] wordt geactiveerd *hashed* herkenningstekens, zoals e-mailadressen of telefoonaantallen worden afgevinkt.

Afhankelijk van het type id&#39;s dat u in Adobe Experience Platform invoert, moet u aan de desbetreffende vereisten voldoen.

#### Vereisten voor hashing voor telefoonnummers {#phone-number-hashing-requirements}

Er zijn twee methodes om telefoonaantallen in [!DNL Facebook] te activeren:

- **Onbewerkte telefoonnummers** worden geïnstalleerd: u kunt onbewerkte telefoonnummers in de  [!DNL E.164] notatie invoeren  [!DNL Platform], die na activering automatisch worden gehasht. Als u deze optie kiest, zorg ervoor om uw ruwe telefoonaantallen in `Phone_E.164` namespace altijd in te nemen.
- **Hashed-telefoonnummers** invoegen: U kunt uw telefoonaantallen pre-hash alvorens in te gaan  [!DNL Platform]. Als u deze optie kiest, zorg ervoor om uw gehakt telefoonaantallen in `Phone_SHA256` namespace altijd in te nemen.

>[!NOTE]
>
>Telefoonnummers die worden ingevoerd in de naamruimte `Phone` kunnen niet worden geactiveerd in [!DNL Facebook].


#### Vereisten voor e-mailhashing {#email-hashing-requirements}

U kunt ervoor kiezen e-mailadressen te hashen alvorens hen in Adobe Experience Platform op te nemen, of u kunt verkiezen om met e-mailadressen in duidelijk Experience Platform te werken en onze algoritme te hebben hen op activering hakt.

Als u meer wilt weten over het invoeren van e-mailadressen in Experience Platform, raadpleegt u het [batchoverzicht](/help/ingestion/batch-ingestion/overview.md) en het [overzicht van het opnemen van gegevens via plakken](/help/ingestion/streaming-ingestion/overview.md).

Als u ervoor kiest om de e-mailadressen zelf te hashen, moet u aan de volgende vereisten voldoen:

- Alle spaties aan het begin en aan het einde uit de e-mailtekenreeks bijsnijden. voorbeeld: `johndoe@example.com`, niet `<space>johndoe@example.com<space>`;
- Wanneer u de e-mailtekenreeksen hasht, moet u de kleine-lettertekenreeks hashen.
   - Voorbeeld: `example@email.com`, niet `EXAMPLE@EMAIL.COM`;
- Controleer of de hashtekenreeks in kleine letters staat
   - Voorbeeld: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, niet `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
- Zilp de tekenreeks niet.

Gegevens uit naamruimten zonder hashing worden na activering automatisch gehasht door [!DNL Platform].

Kenmerkbrongegevens worden niet automatisch gehasht. Wanneer het bronveld niet-gehashte kenmerken bevat, schakelt u de optie **[!UICONTROL Transformatie toepassen]** in om [!DNL Platform] automatisch te laten hashen bij de activering.
![Transformatie identiteitstoewijzing](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

#### Aangepaste naamruimten gebruiken {#custom-namespaces}

Voordat u de naamruimte `Extern_ID` kunt gebruiken om gegevens te verzenden naar [!DNL Facebook], moet u uw eigen id&#39;s synchroniseren met [!DNL Facebook Pixel]. Zie de [officiële documentatie](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers) voor gedetailleerde informatie.

## Verbinden met doel {#connect-destination}

Als u verbinding wilt maken met de [!DNL Facebook]-bestemming, raadpleegt u [Workflow voor verificatie van sociale netwerkdoelen](./workflow.md).

## Segmenten activeren naar [!DNL Facebook] {#activate-segments}

Zie [Gegevens naar doelen activeren](../../ui/activate-destinations.md) voor instructies over het activeren van segmenten naar [!DNL Facebook].

In **[!UICONTROL Segmentprogramma]** stap, moet u [!UICONTROL Oorsprong van publiek] verstrekken wanneer het verzenden van segmenten naar [!DNL Facebook Custom Audiences].

![Facebook Origin of Audience](../../assets/catalog/social/facebook/facebook-origin-audience.png)

## Geëxporteerde gegevens {#exported-data}

Voor [!DNL Facebook], betekent een succesvolle activering dat een [!DNL Facebook] douanepubliek programmatically in [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/) zou worden gecreeerd. Het lidmaatschap van een segment in het publiek zou worden toegevoegd en verwijderd aangezien de gebruikers voor de geactiveerde segmenten worden gekwalificeerd of worden uitgesloten.

>[!TIP]
>
>De integratie tussen Adobe Experience Platform en [!DNL Facebook] steunt historische publieksbackfills. Alle historische segmentkwalificaties worden naar [!DNL Facebook] verzonden wanneer u de segmenten naar de bestemming activeert.
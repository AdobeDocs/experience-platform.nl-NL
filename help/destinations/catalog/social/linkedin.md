---
keywords: gekoppeld in verbinding;gekoppeld in verbinding;gekoppeld in doelen;gekoppeld in;
title: Koppeling in verbinding met passend publiek
description: Activeer profielen voor uw LinkedIn-campagnes voor doelgroepen, personalisatie en onderdrukking op basis van gehakte e-mails.
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
translation-type: tm+mt
source-git-commit: 95ca7112d1f2655bf33e8a1c549e886ced244a5d
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 1%

---

# [!DNL LinkedIn Matched Audiences] verbinding

## Overzicht {#overview}

Activeer profielen voor uw [!DNL LinkedIn] campagnes voor doelgroepen, personalisatie, en onderdrukking, die op gehakte e-mail en mobiele IDs worden gebaseerd.

![linkedIn-bestemming in de gebruikersinterface van Adobe Experience Platform](../../assets/catalog/social/linkedin/catalog.png)

## Gebruiksscenario’s

Om u beter te helpen begrijpen hoe en wanneer om de [!DNL LinkedIn Matched Audiences] bestemming te gebruiken, is hier een gebruiksgeval dat de klanten van Adobe Experience Platform door deze eigenschap kunnen oplossen.

Een softwarebedrijf organiseert een conferentie en wil contact houden met deelnemers, en hen gepersonaliseerde aanbiedingen tonen die op hun status van de conferentieaanwezigheid worden gebaseerd. Het bedrijf kan e-mailadressen of mobiele apparaat-id&#39;s van eigen [!DNL CRM] invoeren in Adobe Experience Platform. Vervolgens kunnen ze segmenten van hun eigen offlinegegevens maken en deze segmenten naar het sociale platform [!DNL LinkedIn] sturen, zodat hun advertentie-uitgaven worden geoptimaliseerd.

## Ondersteunde identiteiten {#supported-identities}

[!DNL LinkedIn Matched Audiences] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | Google-advertentie-id | Selecteer deze doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | Apple ID for Advertisers | Selecteer deze doelidentiteit wanneer uw bronidentiteit een IDFA-naamruimte is. |
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-e-mailadressen met hashing. Volg de instructies in de [ID passende vereisten](#id-matching-requirements-id-matching-requirements) sectie en gebruik aangewezen namespaces voor gewone teksten en gehakte e-mails, respectievelijk. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om [!DNL Platform] de gegevens automatisch te laten hashen bij activering. |


## Type exporteren {#export-type}

**De Uitvoer**  van het segment - u exporteert alle leden van een segment (publiek) met de herkenningstekens (naam, telefoonaantal, en anderen) die in de  [!DNL LinkedIn Matched Audiences] bestemming worden gebruikt.

## linkedIn-accountvoorwaarden {#LinkedIn-account-prerequisites}

Voordat u de bestemming [!UICONTROL LinkedIn Matched Audience] kunt gebruiken, moet u ervoor zorgen dat uw [!DNL LinkedIn Campaign Manager]-account het machtigingsniveau [!DNL Creative Manager] of hoger heeft.

Zie [Gebruikersmachtigingen toevoegen, bewerken en verwijderen voor meer informatie over het bewerken van uw [!DNL LinkedIn Campaign Manager]-gebruikersmachtigingen in de documentatie van LinkedIn.](https://www.linkedin.com/help/lms/answer/5753)

## Overeenkomende vereisten {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] vereist dat er geen duidelijk identificeerbare informatie (PII) wordt verstrekt. Daarom kan het publiek dat aan [!DNL LinkedIn Matched Audiences] wordt geactiveerd *hashed* herkenningstekens, zoals e-mailadressen of mobiele apparaat IDs worden afgevinkt.

Afhankelijk van het type id&#39;s dat u in Adobe Experience Platform invoert, moet u aan de desbetreffende vereisten voldoen.

## Vereisten voor e-mailhashing {#email-hashing-requirements}

U kunt e-mailadressen hashen alvorens hen in Adobe Experience Platform op te nemen, of e-mailadressen gebruiken duidelijk in Experience Platform, en hebben [!DNL Platform] hen op activering hakt.

Als u meer wilt weten over het invoeren van e-mailadressen in Experience Platform, raadpleegt u het [batchoverzicht](/help/ingestion/batch-ingestion/overview.md) en het [streamingoverzicht](/help/ingestion/streaming-ingestion/overview.md).

Als u ervoor kiest om de e-mailadressen zelf te hashen, moet u aan de volgende vereisten voldoen:

- Snijd alle spaties aan het begin en aan het einde van de e-mailtekenreeks bij. Bijvoorbeeld: `johndoe@example.com`, niet `<space>johndoe@example.com<space>`;
- Wanneer u de e-mailtekenreeksen hasht, moet u de kleine-lettertekenreeks hashen.
   - Voorbeeld: `example@email.com`, niet `EXAMPLE@EMAIL.COM`;
- Zorg ervoor dat de hashtekenreeks alleen in kleine letters wordt weergegeven
   - Voorbeeld: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, niet `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
- Zilp de tekenreeks niet.

>[!NOTE]
>
>Gegevens uit naamruimten zonder hashing worden na activering automatisch gehasht door [!DNL Platform].
> Kenmerkbrongegevens worden niet automatisch gehasht.
> 
> Tijdens de stap [Identiteitstoewijzing](../../ui/activate-destinations.md#identity-mapping), wanneer uw brongebied ongehakte attributen bevat, controleer **[!UICONTROL Apply transformation]** optie, om [!DNL Platform] automatisch te hebben de gegevens over activering hakt.
> 
> De optie **[!UICONTROL Apply transformation]** wordt alleen weergegeven wanneer u kenmerken als bronvelden selecteert. Deze wordt niet weergegeven wanneer u naamruimten kiest.

![Transformatie identiteitstoewijzing](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Verbinden met doel {#connect-destination}

Als u verbinding wilt maken met de [!DNL LinkedIn Matched Audiences]-bestemming, raadpleegt u [Workflow voor verificatie van sociale netwerkdoelen](./workflow.md).

In de onderstaande video ziet u ook de stappen voor het configureren van een [!DNL LinkedIn Matched Audiences]-bestemming en het activeren van segmenten.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

## Segmenten activeren naar [!DNL LinkedIn Matched Audiences] {#activate-segments}

Zie [Gegevens naar doelen activeren](../../ui/activate-destinations.md) voor instructies over het activeren van segmenten naar [!DNL LinkedIn Matched Audiences].

## Geëxporteerde gegevens {#exported-data}

Een succesvolle activering betekent dat een [!DNL LinkedIn] douanepubliek programmatically in [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login) zou worden gecreeerd. Het lidmaatschap van een segment in het publiek zou worden toegevoegd en verwijderd aangezien de gebruikers voor de geactiveerde segmenten worden gekwalificeerd of worden uitgesloten.

>[!TIP]
>
>De integratie tussen Adobe Experience Platform en [!DNL LinkedIn Matched Audiences] steunt historische publieksbackfills. Alle historische segmentkwalificaties worden naar [!DNL LinkedIn] verzonden wanneer u de segmenten naar de bestemming activeert.

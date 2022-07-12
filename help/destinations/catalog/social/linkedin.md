---
keywords: gekoppeld in verbinding;gekoppeld in verbinding;gekoppeld in doelen;gekoppeld in;
title: Koppeling in verbinding met passend publiek
description: Activeer profielen voor uw LinkedIn-campagnes voor doelgroepen, personalisatie en onderdrukking op basis van gehakte e-mails.
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 1%

---

# [!DNL LinkedIn Matched Audiences] verbinding

## Overzicht {#overview}

Profielen activeren voor uw [!DNL LinkedIn] campagnes voor doelgroepen, personalisatie en onderdrukking op basis van gehakte e-mails en mobiele id&#39;s.

![linkedIn-bestemming in de gebruikersinterface van Adobe Experience Platform](../../assets/catalog/social/linkedin/catalog.png)

## Gebruiksscenario’s

Om u te helpen beter begrijpen hoe en wanneer gebruiken [!DNL LinkedIn Matched Audiences] doel, hier is een gebruiksgeval dat Adobe Experience Platform klanten kunnen oplossen door deze eigenschap te gebruiken.

Een softwarebedrijf organiseert een conferentie en wil contact houden met deelnemers, en hen gepersonaliseerde aanbiedingen tonen die op hun status van de conferentieaanwezigheid worden gebaseerd. Het bedrijf kan e-mailadressen of mobiele apparaat-id&#39;s van zijn eigen server invoeren [!DNL CRM] naar Adobe Experience Platform. Dan, kunnen zij segmenten van hun eigen off-line gegevens bouwen, en deze segmenten verzenden naar [!DNL LinkedIn] sociaal platform, optimalisering van hun reclame-uitgaven.

## Ondersteunde identiteiten {#supported-identities}

[!DNL LinkedIn Matched Audiences] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | Google-advertentie-id | Selecteer deze doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | Apple-id voor adverteerders | Selecteer deze doelidentiteit wanneer uw bronidentiteit een IDFA-naamruimte is. |
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-e-mailadressen met hashing. Volg de instructies in de [Vereisten voor id-afstemming](#id-matching-requirements-id-matching-requirements) en gebruikt de juiste naamruimten voor respectievelijk platte tekst en gehakte e-mails. Wanneer het bronveld hashkenmerken bevat, controleert u de **[!UICONTROL Apply transformation]** optie, om [!DNL Platform] de gegevens bij activering automatisch hashen. |

{style=&quot;table-layout:auto&quot;}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Segment export]** | U exporteert alle leden van een segment (publiek) met de id&#39;s (naam, telefoonnummer en andere) die worden gebruikt in het dialoogvenster [!DNL LinkedIn Matched Audiences] bestemming. |
| Uitvoerfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Voorwaarden voor linkedIn-accounts {#LinkedIn-account-prerequisites}

Voordat u de [!UICONTROL LinkedIn Matched Audience] doel, zorg ervoor uw [!DNL LinkedIn Campaign Manager] account bevat [!DNL Creative Manager] machtigingsniveau of hoger.

Meer informatie over het bewerken van uw [!DNL LinkedIn Campaign Manager] gebruikersmachtigingen, zie [Gebruikersmachtigingen toevoegen, bewerken en verwijderen voor advertentieaccounts](https://www.linkedin.com/help/lms/answer/5753) in de documentatie van LinkedIn.

## Vereisten voor id-afstemming {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] vereist dat er geen duidelijk identificeerbare informatie (PII) wordt verstrekt. Daarom wordt het publiek geactiveerd tot [!DNL LinkedIn Matched Audiences] kan worden uitgeschakeld *hashed* id&#39;s, zoals e-mailadressen of id&#39;s van mobiele apparaten.

Afhankelijk van het type id&#39;s dat u in Adobe Experience Platform invoert, moet u aan de desbetreffende vereisten voldoen.

## Vereisten voor e-mailhashing {#email-hashing-requirements}

U kunt e-mailadressen hashen alvorens hen in Adobe Experience Platform op te nemen, of e-mailadressen gebruiken duidelijk in Experience Platform, en hebben [!DNL Platform] hash deze na activering.

Als u meer wilt weten over het invoeren van e-mailadressen in Experience Platform, raadpleegt u de [overzicht van batch-opname](/help/ingestion/batch-ingestion/overview.md) en de [overzicht van streaming opname](/help/ingestion/streaming-ingestion/overview.md).

Als u ervoor kiest om de e-mailadressen zelf te hashen, moet u aan de volgende vereisten voldoen:

* Snijd alle spaties aan het begin en aan het einde van de e-mailtekenreeks bij. Bijvoorbeeld: `johndoe@example.com`, niet `<space>johndoe@example.com<space>`;
* Wanneer u de e-mailtekenreeksen hasht, moet u de kleine-lettertekenreeks hashen.
   * Voorbeeld: `example@email.com`, niet `EXAMPLE@EMAIL.COM`;
* Zorg ervoor dat de hashtekenreeks alleen in kleine letters wordt weergegeven
   * Voorbeeld: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, niet `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Zilp de tekenreeks niet.

>[!NOTE]
>
>Gegevens uit naamruimten zonder hashing worden automatisch gehasht door [!DNL Platform] na activering.
> Kenmerkbrongegevens worden niet automatisch gehasht.
> 
> Tijdens de [Identiteitstoewijzing](../../ui/activate-segment-streaming-destinations.md#mapping) als uw bronveld hashkenmerken bevat, controleert u de **[!UICONTROL Apply transformation]** optie, om [!DNL Platform] de gegevens bij activering automatisch hashen.
> 
> De **[!UICONTROL Apply transformation]** Deze optie wordt alleen weergegeven wanneer u kenmerken selecteert als bronvelden. Deze wordt niet weergegeven wanneer u naamruimten kiest.

![Transformatie identiteitstoewijzing](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

In de onderstaande video ziet u ook de stappen voor het configureren van een [!DNL LinkedIn Matched Audiences] doel en activeer segmenten.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>De gebruikersinterface van het Experience Platform wordt vaak bijgewerkt en kan sinds de opname van deze video zijn veranderd. Raadpleeg voor de meest recente informatie de [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

### Verifiëren voor bestemming {#authenticate}

1. Zoek de [!DNL LinkedIn Matched Audiences] doel in de doelcatalogus en selecteer **[!UICONTROL Set Up]**.
2. Selecteer **[!UICONTROL Connect to destination]**.
   ![Verifiëren voor LinkedIn](/help/destinations/assets/catalog/social/linkedin/authenticate-linkedin-destination.png)
3. Voer uw LinkedIn-gegevens in en selecteer **Aanmelden**.

### Doelgegevens invullen {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_linkedin_accountid"
>title="Account-id"
>abstract="Je account-id voor LinkedIn Campagne Manager. U kunt deze id vinden in uw LinkedIn Campaign Manager-account."

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Een naam waarmee u deze bestemming in de toekomst zult erkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Account ID]**: Uw [!DNL LinkedIn Campaign Manager Account ID]. U kunt deze id vinden in uw [!DNL LinkedIn Campaign Manager] account.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over waarschuwingen raadpleegt u de handleiding over [het abonneren aan bestemmingen alarm gebruikend UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Zie [De publieksgegevens van de activering aan het stromen segment de uitvoerbestemmingen](../../ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

## Geëxporteerde gegevens {#exported-data}

Een geslaagde activering betekent dat een [!DNL LinkedIn] aangepaste doelgroep wordt programmatisch gemaakt in [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). Het lidmaatschap van een segment in het publiek zou worden toegevoegd en verwijderd aangezien de gebruikers voor de geactiveerde segmenten worden gekwalificeerd of worden uitgesloten.

>[!TIP]
>
>De integratie tussen Adobe Experience Platform en [!DNL LinkedIn Matched Audiences] ondersteunt historische publieksbackfills. Alle historische segmentkwalificaties worden verzonden naar [!DNL LinkedIn] wanneer u de segmenten naar het doel activeert.

---
title: Aangepaste doelpubliek Twitter-verbinding
description: Richt uw bestaande volgers en klanten in Twitter en creeer relevante re-marketing campagnes door uw publiek te activeren dat binnen Adobe Experience Platform wordt gebouwd
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: ee7e85afd48f7b1c40f0152ad76c8c718b8f1432
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 1%

---

# [!DNL Twitter Custom Audiences]-verbinding

## Overzicht {#overview}

Richt uw bestaande volgers en klanten in Twitter en creeer relevante re-marketing campagnes door uw publiek te activeren dat binnen Adobe Experience Platform wordt gebouwd.

## Vereisten {#prerequisites}

Voordat u de [!DNL Twitter Custom Audiences] -bestemming configureert, moet u controleren of aan de volgende Twitter-voorwaarden is voldaan.

1. Uw [!DNL Twitter Ads] -account moet in aanmerking komen voor advertenties. Nieuwe [!DNL Twitter Ads] -accounts komen de eerste twee weken nadat ze zijn gemaakt niet in aanmerking voor reclame.
2. Voor uw Twitter-gebruikersaccount waarvoor u toegang hebt toegestaan in [!DNL Twitter Audience Manager] , moet de machtiging *[!DNL Partner Audience Manager]* zijn ingeschakeld.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Twitter Custom Audiences] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [&#x200B; identiteiten &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=nl-NL#getting-started).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| device_id | IDFA/AdID/Android ID | Google Advertising ID (GAID) en Apple ID for Advertisers (IDFA) worden ondersteund in Adobe Experience Platform. Gelieve deze namespaces en/of attributen van uw bronschema dienovereenkomstig in de [&#x200B; toewijzingsstap &#x200B;](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) van het werkschema van de bestemmingsactivering in kaart te brengen. |
| email | E-mailadres(sen) voor de gebruiker | Wijs uw e-mailadressen met onbewerkte tekst en uw SHA256-hashed-e-mailadressen toe aan dit veld. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om de gegevens automatisch te laten hashen bij activering door [!DNL Experience Platform] . Als u uw klanten e-mailadressen alvorens hen aan Adobe Experience Platform te uploaden verbergt, gelieve te merken dat deze identiteiten moeten worden gehakt gebruikend SHA256, zonder zout. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#128279;](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s die worden gebruikt in de bestemming Aangepast publiek van Twitter. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [&#x200B; het stromen bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de [!DNL Twitter Custom Audiences] bestemming zou moeten gebruiken, zijn hier voorbeelden van gebruiksgevallen die de klanten van Adobe Experience Platform door deze bestemming kunnen oplossen.

### Hoofdletters en kleine letters gebruiken 1

Richt uw bestaande volgers en klanten in Twitter en creeer relevante re-marketing campagnes door uw publiek te activeren dat in Adobe Experience Platform als [!DNL List Custom Audiences] in Twitter wordt gebouwd.

## Verbinden met doel {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

1. Zoek het doel [!DNL Twitter Custom Audiences] in de doelcatalogus en selecteer **[!UICONTROL Set Up]** .
2. Selecteer **[!UICONTROL Connect to destination]**.
   ![&#x200B; verifieer aan LinkedIn &#x200B;](/help/destinations/assets/catalog/social/twitter/authenticate-twitter-destination.png)
3. Ga uw geloofsbrieven Twitter in en selecteer **Login**.

### Doelgegevens invullen {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_twitter_accountid"
>title="Account-id"
>abstract="Je account-id voor Twitter Adds. Dit vindt u in de instellingen voor Twitter-advertenties."

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Account ID]**: Uw [!DNL Twitter Ads] account-id. Dit vindt u in uw [!DNL Twitter Ads] -instellingen.

>[!IMPORTANT]
>
>Gebruik geen speciale tekens (+ &amp; , % : ; @ / = ? $ \n) in namen voor publiek, beschrijving en publiekstoewijzing. Als de naam van uw Experience Platform-publiek deze tekens bevat, verwijdert u deze voordat u het publiek toewijst aan een Twitter-bestemming.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [&#x200B; activeer profielen en publiek aan het stromen publiek uitvoerbestemmingen &#x200B;](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

### Toewijzingsoverwegingen {#mapping-considerations}

Wanneer u doelgroepen toewijst aan Twitter, geeft u voor mensen leesbare toewijzingsnamen voor de doelgroep op. We raden u aan dezelfde naam te gebruiken als voor de Experience Platform-segmenten.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, zie het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=nl-NL).

## Aanvullende bronnen {#additional-resources}

Meer informatie over [!DNL List Custom Audiences] in Twitter kan in de [&#x200B; documentatie Twitter &#x200B;](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html) worden gevonden.

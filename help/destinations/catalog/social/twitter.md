---
title: Twitter Aangepast publiek, verbinding
description: Richt uw bestaande volgers en klanten in Twitter en creeer relevante re-marketing campagnes door uw publiek te activeren dat binnen Adobe Experience Platform wordt gebouwd
source-git-commit: 3ea3f9ed156ba3a1fbc790153a4b8fa193d5e2da
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 1%

---


# [!DNL Twitter Custom Audiences] verbinding

## Overzicht {#overview}

Richt uw bestaande volgers en klanten in Twitter en creeer relevante re-marketing campagnes door uw publiek te activeren dat binnen Adobe Experience Platform wordt gebouwd.

## Vereisten {#prerequisites}

Voordat u de bestemming [!DNL Twitter Custom Audiences] configureert, moet u controleren of aan de volgende Twitter-voorwaarden is voldaan.

1. Uw [!DNL Twitter Ads]-account moet in aanmerking komen voor advertenties. Nieuwe [!DNL Twitter Ads]-accounts komen niet in aanmerking voor reclame in de eerste twee weken nadat ze zijn gemaakt.
2. Voor uw Twitter-gebruikersaccount waarvoor u toegang hebt toegestaan in [!DNL Twitter Audience Manager], moet *[!DNL Partner Audience Manager]* toestemming zijn ingeschakeld.


## Ondersteunde identiteiten {#supported-identities}

[!DNL Twitter Custom Audiences] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| device_id | IDFA/AdID/Android-id | Google Advertising ID (GAID) en Apple ID for Advertisers (IDFA) worden ondersteund in Adobe Experience Platform. Wijs deze naamruimten en/of kenmerken vanuit uw bronschema dienovereenkomstig toe in de [toewijzingsstap](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) van de workflow voor doelactivering. |
| email | E-mailadres(sen) voor de gebruiker | Wijs uw e-mailadressen met onbewerkte tekst en uw SHA256-hashed-e-mailadressen toe aan dit veld. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om [!DNL Platform] de gegevens automatisch te laten hashen bij activering. Als u uw klanten e-mailadressen alvorens hen aan Adobe Experience Platform te uploaden verbergt, gelieve te merken dat deze identiteiten moeten worden gehakt gebruikend SHA256, zonder zout. |

{style=&quot;table-layout:auto&quot;}

## Exporttype {#export-type}

**Segmentexport** : u exporteert alle leden van een segment (publiek) met de id&#39;s die worden gebruikt in de bestemming Aangepast publiek van Twitter.

## Gevallen gebruiken {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u [!DNL Twitter Custom Audiences] bestemming zou moeten gebruiken, zijn hier voorbeelden van gebruiksgevallen die de klanten van Adobe Experience Platform door deze bestemming kunnen oplossen.

### Hoofdletters en kleine letters gebruiken 1

Richt uw bestaande volgers en klanten in Twitter en creeer relevante re-marketing campagnes door uw publiek te activeren dat binnen Adobe Experience Platform als [!DNL List Custom Audiences] in Twitter wordt gebouwd.

## Verbinden met doel {#connect}

Om met deze bestemming te verbinden, volg de stappen in [het leerprogramma van de bestemmingsconfiguratie](../../ui/connect-destination.md) worden beschreven.

### Verbindingsparameters {#parameters}

Terwijl [vestiging](../../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

* **[!UICONTROL Name]**: Een naam waarmee u deze bestemming in de toekomst zult erkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Account ID]**: Je  [!DNL Twitter Ads] account-id. Dit vindt u in uw [!DNL Twitter Ads]-instellingen.

## Segmenten naar dit doel activeren {#activate}

Lees [Activate profielen en segmenten aan het stromen segment de uitvoerbestemmingen ](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies op het activeren van publiekssegmenten aan deze bestemming.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Zie [Overzicht gegevensbeheer](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html) voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt.

## Aanvullende bronnen {#additional-resources}

Wanneer het in kaart brengen van publiekssegmenten aan Twitter, zorg ervoor om aan de volgende segment noemende vereisten te voldoen:

1. Verstrek de mens-leesbare namen van de segmentafbeelding. Wij adviseren gebruikend de zelfde naam die u voor de segmenten van het Experience Platform gebruikte.
2. Gebruik geen speciale tekens (+ &amp; , % : ; @ / = ? $) in segment en segmenttoewijzingsnamen. Als de segmentnaam van het Experience Platform deze tekens bevat, verwijdert u deze voordat u het segment toewijst aan een Twitter-bestemming.

Meer informatie over [!DNL List Custom Audiences] in Twitter vindt u in de [Twitter-documentatie](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).
---
title: Twitter Aangepast publiek, verbinding
description: Richt uw bestaande volgers en klanten in Twitter en creeer relevante re-marketing campagnes door uw publiek te activeren dat binnen Adobe Experience Platform wordt gebouwd
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 1%

---

# [!DNL Twitter Custom Audiences] verbinding

## Overzicht {#overview}

Richt uw bestaande volgers en klanten in Twitter en creeer relevante re-marketing campagnes door uw publiek te activeren dat binnen Adobe Experience Platform wordt gebouwd.

## Vereisten {#prerequisites}

Voordat u uw [!DNL Twitter Custom Audiences] -bestemming, controleert u of u de volgende Twitter-voorwaarden hebt waaraan u moet voldoen.

1. Uw [!DNL Twitter Ads] account moet in aanmerking komen voor reclame. Nieuw [!DNL Twitter Ads] de rekeningen komen niet in aanmerking voor reclame in de eerste twee weken nadat zij zijn gemaakt.
2. Je Twitter-gebruikersaccount waarvoor je toegang hebt geautoriseerd in [!DNL Twitter Audience Manager] moet de *[!DNL Partner Audience Manager]* machtiging ingeschakeld.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Twitter Custom Audiences] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| device_id | IDFA/AdID/Android-id | Google Advertising ID (GAID) en Apple ID for Advertisers (IDFA) worden ondersteund in Adobe Experience Platform. Wijs deze naamruimten en/of kenmerken vanuit het bronschema dienovereenkomstig toe in het dialoogvenster [toewijzingsstap](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) van de workflow voor doelactivering. |
| email | E-mailadres(sen) voor de gebruiker | Wijs uw e-mailadressen met onbewerkte tekst en uw SHA256-hashed-e-mailadressen toe aan dit veld. Wanneer het bronveld hashkenmerken bevat, controleert u de **[!UICONTROL Apply transformation]** optie, om [!DNL Platform] de gegevens bij activering automatisch hashen. Als u uw klanten e-mailadressen alvorens hen aan Adobe Experience Platform te uploaden verbergt, gelieve te merken dat deze identiteiten moeten worden gehakt gebruikend SHA256, zonder zout. |

{style=&quot;table-layout:auto&quot;}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Segment export]** | U exporteert alle leden van een segment (publiek) met de id&#39;s die worden gebruikt in de bestemming Aangepast publiek van Twitter. |
| Uitvoerfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Gevallen gebruiken {#use-cases}

Om u te helpen beter begrijpen hoe en wanneer u het [!DNL Twitter Custom Audiences] doel, hier zijn de gevallen van het steekproefgebruik die de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

### Hoofdletters en kleine letters gebruiken 1

Richt uw bestaande volgers en klanten in Twitter en creeer relevante re-marketing campagnes door uw publiek te activeren dat binnen Adobe Experience Platform wordt gebouwd als [!DNL List Custom Audiences] in Twitter.

## Verbinden met doel {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

### Verbindingsparameters {#parameters}

while [opzetten](../../ui/connect-destination.md) voor deze bestemming moet u de volgende informatie opgeven:

* **[!UICONTROL Name]**: Een naam waarmee u deze bestemming in de toekomst zult erkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Account ID]**: Uw [!DNL Twitter Ads] account-id. Dit is te vinden in uw [!DNL Twitter Ads] instellingen.

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Lezen [Profielen en segmenten activeren voor streaming segmentexportdoelen](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] handhaaft gegevensbeheer, zie [Overzicht van gegevensbeheer](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Aanvullende bronnen {#additional-resources}

Wanneer het in kaart brengen van publiekssegmenten aan Twitter, zorg ervoor om aan de volgende segment noemende vereisten te voldoen:

1. Verstrek de mens-leesbare namen van de segmentafbeelding. Wij adviseren gebruikend de zelfde naam die u voor de segmenten van het Experience Platform gebruikte.
2. Gebruik geen speciale tekens (+ &amp; , % : ; @ / = ? $) in segment en segmenttoewijzingsnamen. Als de segmentnaam van het Experience Platform deze tekens bevat, verwijdert u deze voordat u het segment toewijst aan een Twitter-bestemming.

Meer informatie over [!DNL List Custom Audiences] in Twitter vindt u in het [Twitter-documentatie](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).

---
title: Verbinding met pinterest Customer List
description: Maak een publiek op basis van uw klantlijsten, personen die uw site hebben bezocht of personen die al met uw inhoud hebben gewerkt op Pinterest.
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 1%

---

# [!DNL Pinterest Customer List] verbinding

## Overzicht {#overview}

Maak een publiek op basis van uw klantlijsten, personen die uw site hebben bezocht of personen die al met uw inhoud hebben gewerkt op Pinterest.

>[!IMPORTANT]
>
>Deze bestemming werd gebouwd door het team van Pinterest. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen met de afdeling https://help.pinterest.com/en/contact.

## Vereisten {#prerequisites}

* De gebruiker moet zich verifiëren met een Pinterest-account dat toegang heeft tot het advertentieaccount waaraan hij of zij een publiek wil toevoegen. Meer informatie over het delen van adverteerderaccounts vindt u [hier](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts). Specifiek, zou de gebruiker de &quot;publiek&quot;toegangsniveaus nodig hebben.
* Gegevens over identiteitsindelingen van klantenlijsten zijn te vinden [hier](https://help.pinterest.com/en/business/article/audience-targeting).


## Ondersteunde identiteiten {#supported-identities}

De [!DNL Pinterest Customer List] doel ondersteunt de activering van de identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

In de [toewijzingsstap](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) van de workflow voor doelactivering de gewenste identiteiten aan het doelveld toewijzen *pinterest_publiek*. Identiteiten worden onderscheiden en opgelost na gegevensinvoer in Pinterest.

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Wijs de *GAID* naamruimte van bronidentiteit naar het doelidentiteitsveld *pinterest_publiek*. Identiteiten worden onderscheiden en opgelost na gegevensinvoer in Pinterest. |
| IDFA | [!DNL Apple ID for Advertisers] | Wijs de *IDFA* naamruimte van bronidentiteit naar het doelidentiteitsveld *pinterest_publiek*. Identiteiten worden onderscheiden en opgelost na gegevensinvoer in Pinterest. |
| EMAIL | E-mailadressen (tekst wissen of hashed met het algoritme SHA256) | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-e-mailadressen met hashing. <br> Wijs de *E-mail* of *Email_LC_SHA256* naamruimte van bronidentiteit naar het doelidentiteitsveld *pinterest_publiek*. |

{style=&quot;table-layout:auto&quot;}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Segment export]** | U exporteert alle leden van een segment (publiek) met de id&#39;s (naam, telefoonnummer of andere) die worden gebruikt in de Pinterest Customer List-bestemming. |
| Uitvoerfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Gevallen gebruiken {#use-cases}

Om u te helpen beter begrijpen hoe en wanneer u het [!DNL Pinterest Customer List] doel, hier zijn de gevallen van het steekproefgebruik die de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

### Hoofdletters en kleine letters gebruiken 1

Maak een publiek op basis van uw klantlijsten, personen die uw site hebben bezocht of personen die al met uw inhoud hebben gewerkt op Pinterest.

## Verbinden met doel {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

### Verbindingsparameters {#parameters}

while [opzetten](../../ui/connect-destination.md) voor deze bestemming moet u de volgende informatie opgeven:

* **[!UICONTROL Name]**: Een naam waarmee u deze bestemming in de toekomst zult erkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Advertiser ID]**: Je Pinterest-adverteerder-id.

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Lezen [Profielen en segmenten activeren voor streaming segmentexportdoelen](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] handhaaft gegevensbeheer, zie [Overzicht van gegevensbeheer](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Aanvullende bronnen {#additional-resources}

Raadpleeg de [Pinterest Help Center-pagina](https://help.pinterest.com/en/business/article/audience-targeting) voor aanvullende informatie.

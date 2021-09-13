---
title: Verbinding met pinterest Customer List
description: Maak een publiek op basis van uw klantlijsten, personen die uw site hebben bezocht of personen die al met uw inhoud hebben gewerkt op Pinterest.
source-git-commit: e6fa353c74c652f82ff187692de8784463d0fd01
workflow-type: tm+mt
source-wordcount: '512'
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
* Nadere gegevens over de identiteitsindelingen van de klantenlijst vindt u [hier](https://help.pinterest.com/en/business/article/audience-targeting).


## Ondersteunde identiteiten {#supported-identities}

De bestemming [!DNL Pinterest Customer List] steunt de activering van identiteiten die in de hieronder lijst worden beschreven. Meer informatie over [identiteiten](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

Wijs in [toewijzingsstap](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) van de workflow voor doelactivering de gewenste identiteiten toe aan het doelveld *pinterest_publiek*. Identiteiten worden onderscheiden en opgelost na gegevensinvoer in Pinterest.

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Wijs *GAID* bronidentiteitsnaamruimte toe aan het doelidentiteitsveld *pinterest_publiek*. Identiteiten worden onderscheiden en opgelost na gegevensinvoer in Pinterest. |
| IDFA | [!DNL Apple ID for Advertisers] | Wijs *IDFA* bronidentiteitsnaamruimte toe aan het doelidentiteitsveld *pinterest_publiek*. Identiteiten worden onderscheiden en opgelost na gegevensinvoer in Pinterest. |
| EMAIL | E-mailadressen (tekst wissen of hashed met het algoritme SHA256) | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-e-mailadressen met hashing. <br> Wijs de naamruimte  ** van de  *bronidentiteit van de e-mail_LC_SHA256* aan het veld  *pinterest_publiek* van de doelidentiteit toe. |

{style=&quot;table-layout:auto&quot;}

## Exporttype {#export-type}

**De Uitvoer**  van het segment - u exporteert alle leden van een segment (publiek) met de herkenningstekens (naam, telefoonaantal, of anderen) die in de bestemming van de Lijst van de Klant van Pinterest worden gebruikt.

## Gevallen gebruiken {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u [!DNL Pinterest Customer List] bestemming zou moeten gebruiken, zijn hier voorbeelden van gebruiksgevallen die de klanten van Adobe Experience Platform door deze bestemming kunnen oplossen.


### Hoofdletters en kleine letters gebruiken 1

Maak een publiek op basis van uw klantlijsten, personen die uw site hebben bezocht of personen die al met uw inhoud hebben gewerkt op Pinterest.

## Verbinden met doel {#connect}

Om met deze bestemming te verbinden, volg de stappen in [het leerprogramma van de bestemmingsconfiguratie](../../ui/connect-destination.md) worden beschreven.



### Verbindingsparameters {#parameters}

Terwijl [vestiging](../../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

* **[!UICONTROL Name]**: Een naam waarmee u deze bestemming in de toekomst zult erkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Account ID]**: Je Pinterest-advertentie-ID.

## Segmenten naar dit doel activeren {#activate}

Lees [Activate profielen en segmenten aan het stromen segment de uitvoerbestemmingen ](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies op het activeren van publiekssegmenten aan deze bestemming.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Zie [Overzicht gegevensbeheer](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html) voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt.

## Aanvullende bronnen {#additional-resources}

Raadpleeg de pagina [Pinterest Help Center](https://help.pinterest.com/en/business/article/audience-targeting) voor meer informatie.

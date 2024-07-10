---
title: PX-verbinding ophalen
description: Gebruik de PX-bestemming van Gainsight om segmentatiegegevens naar het PX-platform van Gainsight te verzenden.
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 0ca0d34f-f866-4f59-80f8-60198fbb86be
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 1%

---

# PX-verbinding ophalen {#gainsight-px}

## Overzicht {#overview}

[[!DNL Gainsight PX]](https://www.gainsight.com/product-experience/) is een platform voor productervaring dat productteams in staat stelt te begrijpen hoe gebruikers hun producten gebruiken, feedback te verzamelen en in-app-contracten zoals productdoorlopen te maken om gebruikers aan boord te krijgen en producten te adopteren.

>[!IMPORTANT]
>
>De bestemmingsschakelaar en documentatiepagina worden gecreeerd en door *Gainsight PX* team. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen via *`pxsupport@gainsight.com`*.

## Gebruiksscenario’s {#use-cases}

Om u te helpen beter begrijpen hoe en wanneer u het *Gainsight PX* doel, hier zijn de gevallen van het steekproefgebruik die de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

### Doelstellingen voor in-app-services {#targeting-in-app-engagements}

Een SaaS-bedrijf wil zijn klanten betrekken via een handleiding in de toepassing die op Gainsight PX is samengesteld. Een publiek dat deze betrokkenheid ontvangt, is gebaseerd op Adobe Experience Platform. De bestemming van PX van de Markering ontvangt het publiek en stelt het binnen het milieu van PX van de Markering ter beschikking.

## Vereisten {#prerequisites}

* Contact opnemen met de [!DNL Gainsight] supportteam en verzoek om activering van externe segmentfuncties voor uw abonnement.
* Genereer een OAuth Secret-waarde voor uw PX-abonnement met de opdracht **[!UICONTROL Generate New Secret]** onder aan het dialoogvenster [pagina Bedrijfsgegevens](https://app.aptrinsic.com/settings/subscription)
  ![Het scherm van de Details van het bedrijf in Gegineerde PX die Nieuwe Geheime knoop tonen](../../assets/catalog/analytics/gainsight-px/generate_oauth_secret.png)

## Ondersteunde identiteiten {#supported-identities}

Gainsight PX ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](../../../identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving |
|---|----|
| IdentifyID | Algemene gebruikersnaam die een gebruiker op unieke wijze identificeert in Gainsight PX en Adobe Experience Platform |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welk type publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---|---|---|
| [!DNL Segmentation Service] | ✓ | Door het Experience Platform gegenereerde soorten publiek [Segmenteringsservice](../../../segmentation/home.md). |
| Aangepaste uploads | X | Soorten publiek [geïmporteerd](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van CSV-bestanden. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---|---|---|
| Exporttype | **[!UICONTROL Segment export]** | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer of andere) die worden gebruikt in het dialoogvenster [!DNL Gainsight PX] bestemming. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Wanneer een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). Vul in de workflow voor doelconfiguratie de velden in die in de twee onderstaande secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u zich wilt verifiëren bij de bestemming, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]**.

![Verificatiescherm](../../assets/catalog/analytics/gainsight-px/auth-screen.png)

* **[!UICONTROL Password]**: Het wachtwoord waarmee u zich kunt aanmelden bij [[!DNL Gainsight PX]](https://app.aptrinsic.com)
* **[!UICONTROL Client ID]**: De Gronght PX-abonnements-id op de [pagina Bedrijfsgegevens](https://app.aptrinsic.com/settings/subscription)
* **[!UICONTROL Client secret]**: Het OAuth-geheim dat onder aan het dialoogvenster [pagina Bedrijfsgegevens](https://app.aptrinsic.com/settings/subscription) in de [!DNL Gainsight PX] UI.
* **[!UICONTROL Username]**: De e-mail die wordt gebruikt voor aanmelding bij de [[!DNL Gainsight PX]](https://app.aptrinsic.com) UI

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![Scherm Doeldetails in de gebruikersinterface van het Experience Platform waarin wordt weergegeven hoe de velden Naam en Beschrijving moeten worden ingevuld](../../assets/catalog/analytics/gainsight-px/destination_details.png)

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst wilt herkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
>
>* Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.
>* Om te exporteren *identiteiten*, hebt u de **[!UICONTROL View Identity Graph]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). <br> ![Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren."){width="100" zoomable="yes"}

Lezen [Profielen en segmenten activeren voor streaming segmentexportdoelen](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

### Identiteiten toewijzen {#map}

Dit doel ondersteunt het toewijzen van profielkenmerken en naamruimten. De doeltoewijzing moet altijd de **[!UICONTROL IDENTIFY_ID]** naamruimte identiteit.

Zie de voorbeelden hieronder om beter te begrijpen hoe te om afbeelding te vormen.

#### Een profielkenmerk toewijzen {#map-profile-attribute}

In het onderstaande voorbeeld is het bronveld een XDM-profielkenmerk dat wordt toegewezen aan de doelnaamruimte IDENTIFY_ID.

![Het voorbeeldtoewijzingsscherm voor naamruimte weergeven waarin wordt aangegeven hoe de bron- en doelwaarden moeten worden geselecteerd](../../assets/catalog/analytics/gainsight-px/mapping_attribute.png)

#### Een naamruimte toewijzen {#map-identity-namespace}

In het onderstaande voorbeeld is het bronveld een naamruimte voor identiteit (**[!UICONTROL ECID]**) die aan de **[!UICONTROL IDENTIFY_ID]** target namespace.

![Kenmerkvoorbeeld met toewijzingsscherm waarin wordt getoond hoe de bron- en doelwaarden moeten worden geselecteerd](../../assets/catalog/analytics/gainsight-px/mapping_identities.png)

## Geëxporteerde gegevens/Gegevens valideren bij exporteren {#exported-data}

De gegevens van de segmentatie worden gestroomd van het Experience Platform aan Gainsight PX.

Metagegevens van segmenten zijn zichtbaar in het scherm Segmenten binnen het dialoogvenster [!DNL Gainsight PX] UI.

![Scherm Segmentlijst in Gainsight PX met externe segmenten.](../../assets/catalog/analytics/gainsight-px/segment_metadata.png)

De informatie over het segmentlidmaatschap is zichtbaar op het tabblad Segmenten van het scherm Audience Explorer van het dialoogvenster [!DNL Gainsight PX] UI.

![Het scherm van de Ontdekkingsreiziger van het publiek in PX van het inzicht van de Vraag die bijbehorende segmenten voor een gebruiker toont.](../../assets/catalog/analytics/gainsight-px/PX_Segments.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] dwingt gegevensbeheer af, lees de [Overzicht van gegevensbeheer](/help/data-governance/home.md).

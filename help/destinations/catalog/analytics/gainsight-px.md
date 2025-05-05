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

[[!DNL Gainsight PX] ](https://www.gainsight.com/product-experience/) is een platform van de productervaring dat productteams toelaat om te begrijpen hoe de gebruikers hun producten gebruiken, terugkoppelen verzamelen, en in-app overeenkomsten zoals productanalyses tot stand brengen om gebruiker aan boord te drijven en product adoptie te drijven.

>[!IMPORTANT]
>
>De bestemmingsschakelaar en de documentatiepagina worden gecreeerd en door het *team van Gaten PX* gehandhaafd. Voor vragen of updateverzoeken kunt u rechtstreeks contact opnemen via *`pxsupport@gainsight.com`* .

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de *bestemming van PX van 0&rbrace; Gainsight zou moeten gebruiken, zijn hier de gevallen van het steekproefgebruik die de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.*

### Doelstellingen voor in-app-services {#targeting-in-app-engagements}

Een SaaS-bedrijf wil zijn klanten betrekken via een handleiding in de toepassing die op Gainsight PX is samengesteld. Een publiek dat deze betrokkenheid ontvangt, is gebaseerd op Adobe Experience Platform. De bestemming van PX van de Markering ontvangt het publiek en stelt het binnen het milieu van PX van de Markering ter beschikking.

## Vereisten {#prerequisites}

* Neem contact op met het ondersteuningsteam van [!DNL Gainsight] en verzoek om activering van externe segmentfuncties voor uw abonnement.
* Produceer een Geheime waarde OAuth voor uw abonnement van PX, gebruikend de **[!UICONTROL Generate New Secret]** knoop bij de bodem van de [ pagina van de Details van het Bedrijf ](https://app.aptrinsic.com/settings/subscription)
  ![ het scherm van de Details van het Bedrijf in PX die van de Revisie toont Nieuwe Geheime knoop ](../../assets/catalog/analytics/gainsight-px/generate_oauth_secret.png)

## Ondersteunde identiteiten {#supported-identities}

Gainsight PX ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [ identiteiten ](../../../identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving |
|---|----|
| IdentifyID | Algemene gebruikersnaam die een gebruiker op unieke wijze identificeert in Gainsight PX en Adobe Experience Platform |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welk type publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---|---|---|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van het Experience Platform [&#128279;](../../../segmentation/home.md). |
| Aangepaste uploads | X | Het publiek [ ingevoerde ](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---|---|---|
| Exporttype | **[!UICONTROL Segment export]** | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer of andere) die in de [!DNL Gainsight PX] -bestemming worden gebruikt. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Wanneer een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u de **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven. Vul in de workflow voor doelconfiguratie de velden in die in de twee onderstaande secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u voor verificatie bij het doel wilt zorgen, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]** .

![ het schermschot van de Authentificatie ](../../assets/catalog/analytics/gainsight-px/auth-screen.png)

* **[!UICONTROL Password]**: Het wachtwoord dat wordt gebruikt om u aan te melden bij [[!DNL Gainsight PX] ](https://app.aptrinsic.com)
* **[!UICONTROL Client ID]**: De PX-abonnementsidentiteitskaart van Gronght op de [ pagina van de Details van het Bedrijf ](https://app.aptrinsic.com/settings/subscription)
* **[!UICONTROL Client secret]**: Het geheim OAuth dat bij de bodem van de [ pagina van de Details van het Bedrijf ](https://app.aptrinsic.com/settings/subscription) in [!DNL Gainsight PX] UI wordt geproduceerd.
* **[!UICONTROL Username]**: De e-mail die wordt gebruikt om zich aan te melden bij [[!DNL Gainsight PX] ](https://app.aptrinsic.com) UI

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![ de detailsscherm van de Bestemming in het gebruikersinterface die van het Experience Platform tonen hoe te om de gebieden van de Naam en van de Beschrijving in te vullen ](../../assets/catalog/analytics/gainsight-px/destination_details.png)

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
>
>* Om gegevens te activeren, hebt u **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [ activeer profielen en segmenten aan het stromen segment de uitvoerbestemmingen ](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

### Identiteiten toewijzen {#map}

Dit doel ondersteunt het toewijzen van profielkenmerken en naamruimten. De doeltoewijzing moet altijd de naamruimte **[!UICONTROL IDENTIFY_ID]** van de identiteit zijn.

Zie de voorbeelden hieronder om beter te begrijpen hoe te om afbeelding te vormen.

#### Een profielkenmerk toewijzen {#map-profile-attribute}

In het onderstaande voorbeeld is het bronveld een XDM-profielkenmerk dat wordt toegewezen aan de doelnaamruimte IDENTIFY_ID.

![ het voorbeeldafbeeldingsscherm van Namespace van de Identiteit die hoe te om de bron en doelwaarden te selecteren ](../../assets/catalog/analytics/gainsight-px/mapping_attribute.png)

#### Een naamruimte toewijzen {#map-identity-namespace}

In het onderstaande voorbeeld is het bronveld een naamruimte voor identiteit (**[!UICONTROL ECID]**) die wordt toegewezen aan de **[!UICONTROL IDENTIFY_ID]** doelnaamruimte.

![ het voorbeeldafbeeldingsscherm van Attributen die hoe te om de bron en doelwaarden te selecteren ](../../assets/catalog/analytics/gainsight-px/mapping_identities.png)

## Geëxporteerde gegevens/Gegevens valideren bij exporteren {#exported-data}

De gegevens van de segmentatie worden gestroomd van het Experience Platform aan Gainsight PX.

Segmentmetagegevens zijn zichtbaar in het scherm Segmenten in de gebruikersinterface van [!DNL Gainsight PX] .

![ de lijstscherm van het Segment in PX van het Hoogtepunt die externe segmenten tonen.](../../assets/catalog/analytics/gainsight-px/segment_metadata.png)

De informatie over het segmentlidmaatschap is zichtbaar op het tabblad Segmenten van het scherm Audience Explorer van de [!DNL Gainsight PX] UI.

![ het scherm van de Ontdekkingsreiziger van het publiek in PX van de Verkenner die van de Verkenner van de Verzameling bijbehorende segmenten voor een gebruiker tonen.](../../assets/catalog/analytics/gainsight-px/PX_Segments.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, lees het [ overzicht van het Beleid van Gegevens ](/help/data-governance/home.md).

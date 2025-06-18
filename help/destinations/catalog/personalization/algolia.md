---
title: Algolië
description: Gebruik deze connector om het publiek naar Algolië te activeren voor personalisatie en gebruik in zoekopdrachten en aanbevelingen. Vervolgens kunt u de bronconnector van het Algoliegebruikersprofiel gebruiken om de profielen te importeren in Real-Time CDP om een rijk publiek te maken.
source-git-commit: 01e8739952ce2f56eaafcbb0731fb88d5961b21d
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 0%

---


# [!DNL Algolia] verbinding

## Overzicht {#overview}

>[!IMPORTANT]
>
>De [!DNL Algolia] bestemmings schakelaar en documentatiepagina worden gecreeerd en door het team van de Diensten van de Integratie van Algolia gehandhaafd. Voor onderzoeken of updateverzoeken, contacteer hen in [ adobe-algolia-solutions@algolia.com ](mailto:adobe-algolia-solutions@algolia.com).

Gebruik de [!DNL Algolia] doelverbinding om Adobe Experience Platform-publiek naar Algolië te sturen voor gepersonaliseerde zoekopdrachten en aanbevelingen. Voordat u de [!DNL Algolia] doelconnector kunt gebruiken, moet u eerst de [[!DNL Algolia User Profiles]](/help/sources/connectors/data-partners/algolia-user-profiles.md) bronconnector instellen. Tijdens het programma voor het instellen van de bronaansluiting maakt u de identiteit van het token van de gebruiker Algolia. Deze identiteit wordt vereist voor afbeelding wanneer u de bestemmingsschakelaar vormt.

Deze zelfstudie bevat stappen voor het maken van een [!DNL Algolia] doelverbinding en gegevensstroom via de Adobe Experience Platform-gebruikersinterface.

![ de bestemmingscatalogus met de bestemming Algolië.](../../assets/catalog/personalization/algolia/catalog.png)

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de [!DNL Algolia] bestemming zou moeten gebruiken, zijn hier voorbeelden van gebruiksgevallen die de klanten van Adobe Experience Platform door deze bestemming kunnen oplossen.

### Personalization-consistentie {#personalization-consistency}

Gebruik deze bestemmingsschakelaar om een verenigbare verpersoonlijking over uw plaats van homepage aan onderzoek te leveren.

Als markeerteken wilt u bijvoorbeeld een uitgebreid publiek in Adobe Experience Platform maken op basis van meerdere gegevensbronnen voor gebruikers, waaronder Algolië. U kunt de [!DNL Algolia] bestemmingsschakelaar gebruiken om het publiek voor het richten van strategieën te delen, die tot een verhoging van campagneverpersoonlijking en omzetting leiden.

Voor het implementeren van dit gebruiksscenario moet u zowel de [[!DNL Algolia User Profiles]](/help/sources/connectors/data-partners/algolia-user-profiles.md) bron- als [!DNL Algolia] doelconnectors gebruiken.

Eerst importeert u uw bestaande [!DNL Algolia] -gebruikersprofielen naar Adobe Experience Platform Real-Time CDP en andere bronnen om een rijk publiek te maken met de bronaansluiting. Marketers zouden een publiek maken met behulp van de profielgegevens die naar Algolië kunnen worden verzonden voor personalisatie van zoekopdrachten en aanbevelingen.

Gebruik vervolgens de bijbehorende [[!DNL Algolia User Profiles]](/help/sources/connectors/data-partners/algolia-user-profiles.md) bronconnector om de klantprofielen weer in Real-Time CDP in te voeren en te vergroten.

## Vereisten {#prerequisites}

>[!IMPORTANT]
>
>* Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** nodig, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions). Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

## Ondersteunde identiteiten {#supported-identities}

[!DNL Algolia] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [ identiteiten ](https://experienceleague.adobe.com/nl/docs/experience-platform/identity/features/namespaces).

| Doelidentiteit | Beschrijving | Overwegingen |
|---------|---------|----------|
| userId | [!DNL Algolia] gebruikerstoken | Selecteer deze doelidentiteit om de `AlgoliaUserToken` bronidentiteit toe te wijzen aan `userToken` in het [!DNL Algolia] -platform. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welk type publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|---------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#128279;](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [ ingevoerde ](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!DNL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer of andere) die in de [!DNL Algolia] -bestemming worden gebruikt. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage and Activate Dataset Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven. Vul in de workflow voor doelconfiguratie de velden in die in de twee onderstaande secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u voor verificatie bij het doel wilt zorgen, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]** .

* **[!UICONTROL Application ID]**: De [!DNL Algolia] toepassings-id is een unieke id die is toegewezen aan uw [!DNL Algolia] -account.
* **[!UICONTROL API Key]**: De [!DNL Algolia] API-sleutel is een referentie die wordt gebruikt voor het verifiëren en autoriseren van API-aanvragen bij de zoek- en indexservices van [!DNL Algolia] .

Voor meer informatie over deze geloofsbrieven, zie [!DNL Algolia] [ authentificatiedocumentatie ](https://www.algolia.com/doc/tools/cli/get-started/authentication/).

![ Nieuwe Rekening ](../../assets/catalog/personalization/algolia/connection.png)

### Doelgegevens invullen

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Description]**: korte uitleg van het doel van de bestemming.
* **[!UICONTROL Region]**: De opties zijn **US** of **EU**. Selecteer het gebied waar de klantgegevens worden opgeslagen.


![ de details van de Rekening ](../../assets/catalog/personalization/algolia/account.png)

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om identiteiten uit te voeren, hebt u de Grafiek van de Identiteit van de Mening [ toegangsbeheertoestemming ](https://experienceleague.adobe.com/nl/docs/experience-platform/access-control/home#permissions) nodig.

Lees [ activeer profielen en publiek aan het stromen publiek uitvoerbestemmingen ](https://experienceleague.adobe.com/nl/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations) voor instructies bij het activeren van publiek aan deze bestemming.

### Kenmerken en identiteiten toewijzen {#mapping-attributes-identities}

Tijdens [!UICONTROL Mapping step], moet u de AlgoliaUserToken bronidentiteit aan de userId doelidentiteit in kaart brengen.

![ Volledige Afbeelding van de afbeelding ](../../assets/catalog/personalization/algolia/mapping-complete.png)

## Gegevens exporteren valideren {#exported-data}

Als u wilt controleren of het publiek naar de gebruikersprofielen is geëxporteerd, controleert u het dashboard van [!DNL Algolia] , navigeert u naar **[!UICONTROL Advanced Personalization]** en klikt u op **[!UICONTROL User Inspector]** . Zoek een gebruikersprofiel dat is gekoppeld aan het geëxporteerde Adobe Experience Platform-publiek en zoek het in de gebruikerscontrole. U zult publiek identiteitskaart in de segmentsectie zien.

![ de Inspecteur van de Gebruiker van Algolië ](../../assets/catalog/personalization/algolia/verify-segment-user-profile.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, lees het [ overzicht van het Beleid van Gegevens ](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=nl-NL).

## Aanvullende bronnen {#additional-resources}

Raadpleeg de volgende [!DNL Algolia] -documentatie voor meer informatie:

* [ wat is Geavanceerde Personalization?](https://www.algolia.com/doc/guides/personalization/advanced-personalization/what-is-advanced-personalization/)
* [ Profielen van de Gebruiker ](https://www.algolia.com/doc/guides/personalization/advanced-personalization/what-is-advanced-personalization/concepts/user-profiles/)
* [ de gebruikers van het segment met regelcontexten ](https://www.algolia.com/doc/guides/personalization/advanced-personalization/implement/guides/segment-users-with-rule-contexts/#assign-a-segment-context-at-query-time)

## Volgende stappen {#next-steps}

Aan de hand van deze zelfstudie hebt u een gegevensstroom gemaakt om een publiek van Experience Platform naar uw [!DNL Algolia] -toepassing te exporteren. Voor meer informatie over het [!DNL Algolia] platform, zie de [ documentatie van Algolië ](https://www.algolia.com/doc/).
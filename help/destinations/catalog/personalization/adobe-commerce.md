---
title: Adobe Commerce-bestemmingsconnector
description: Leer hoe verkopers van Adobe Commerce en Real-Time CDP de winkelervaring kunnen aanpassen door zeer relevante site-inhoud en -promoties te leveren, aangepast aan klanten die in Real-Time CDP zijn gebouwd en beheerd.
exl-id: f7aa3c6c-ba7a-440c-a4d7-5d7b50dbbc0d
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 0%

---

# Adobe Commerce-verbinding {#adobe-commerce}

## Overzicht {#overview}

Gebruik de [!DNL Adobe Commerce] doelconnector om een of meer [!DNL Real-Time CDP] soorten publiek te selecteren dat moet worden geactiveerd voor uw [!DNL Adobe Commerce] -account voor een dynamische, gepersonaliseerde ervaring voor uw kopers. Binnen [!DNL Adobe Commerce] kunt u die [!DNL Real-Time CDP] soorten publiek selecteren om unieke aanbiedingen in het winkelwagentje aan te passen, zoals &#39;Koop 2 krijg 1 gratis,&#39;. U kunt ook hoofdbanners weergeven en de prijzen van producten wijzigen via promotieaanbiedingen, die allemaal zijn aangepast aan het Adobe [!DNL Real-Time CDP] -publiek.

## Vereisten {#prerequisites}

Deze connector is beschikbaar in de doelcatalogus voor klanten die [!DNL Real-Time CDP] Prime of Ultimate en Adobe Commerce hebben aangeschaft.

Om deze bestemmingsverbinding te gebruiken, zorg ervoor dat u toegang hebt tot:

- [&#x200B; Adobe Experience Platform &#x200B;](https://experience.adobe.com/)
- [&#x200B; Adobe Developer Console &#x200B;](https://developer.adobe.com/developer-console/docs/guides/getting-started/). Met toegang tot de ontwikkelaarsconsole, kunt u de dienstrekening en credentieinformatie bekijken die nodig is om [&#x200B; de configuratie &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html#configure-the-extension) van de uitbreiding in Adobe Commerce te voltooien.
- [&#x200B; versie van Adobe Commerce 2.4.4 of hoger &#x200B;](https://business.adobe.com/products/commerce.html)

In Experience Platform maakt u het volgende:

- [&#x200B; Schema &#x200B;](../../../xdm/schema/composition.md). Het schema dat u maakt, vertegenwoordigt de gegevens die u vanuit Adobe Commerce wilt invoeren. [&#x200B; leer meer &#x200B;](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html) over hoe te om een schema tot stand te brengen dat Commerce-Specifieke gebiedsgroepen bevat.
- [&#x200B; Dataset &#x200B;](../../../catalog/datasets/user-guide.md#create). Een dataset is een opslag en beheersconstructie voor een inzameling van gegevens. U creeert deze dataset van het schema dat u hierboven creeerde.
- [&#x200B; DataStream &#x200B;](../../../datastreams/configure.md#create). ID waarmee gegevens kunnen worden verzonden van [!DNL Adobe Experience Platform] naar andere Adobe DX-producten. Deze id moet zijn gekoppeld aan een specifieke website in uw specifieke Adobe Commerce-exemplaar. Wanneer u deze gegevensstroom creeert, specificeer het XDM schema u hierboven creeerde.

Maak verbinding met het doel [!DNL Commerce] nadat u aan de voorwaarden hebt voldaan.

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#x200B; &#x200B;](../../../segmentation/home.md). |
| Alle andere doelgroepen | Ja | Deze categorie omvat alle oorsprong van het publiek buiten het publiek dat via [!DNL Segmentation Service] wordt gegenereerd. Lees over de [&#x200B; diverse publieksoorsprong &#x200B;](/help/segmentation/ui/audience-portal.md#customize). Voorbeelden zijn: <ul><li> de douane uploadt publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers,</li><li> gelijksoortige doelgroepen, </li><li> federaal publiek, </li><li> publiek dat wordt gegenereerd in andere Experience Platform-toepassingen, zoals [!DNL Adobe Journey Optimizer] , </li><li> en meer. </li></ul> |

{style="table-layout:auto"}



Ondersteund publiek per type publieksgegevens:

| Gegevenstype Publiek | Ondersteund | Beschrijving | Gebruiksscenario&#39;s |
|--------------------|-----------|-------------|-----------|
| [&#x200B; het publiek van Mensen &#x200B;](/help/segmentation/types/people-audiences.md) | Ja | Gebaseerd op klantenprofielen, die u toestaan om specifieke groepen mensen voor marketing campagnes te richten. | Frequente kopers, winkeliers |
| [&#x200B; publiek van de Rekening &#x200B;](/help/segmentation/types/account-audiences.md) | Nee | Doelpersonen binnen specifieke organisaties voor marketingstrategieën op basis van account. | B2B-marketing |
| [&#x200B; Het publiek van het Vooruitzicht &#x200B;](/help/segmentation/types/prospect-audiences.md) | Nee | De individuen van het doel die nog geen klanten zijn maar eigenschappen met uw doelpubliek delen. | Waarschuwing met gegevens van derden |
| [&#x200B; de uitvoer van de Dataset &#x200B;](/help/catalog/datasets/overview.md) | Nee | Verzamelingen gestructureerde gegevens die zijn opgeslagen in het [!DNL Adobe Experience Platform] Data Lake. | Rapportage, workflows voor gegevenswetenschap |

{style="table-layout:auto"}


## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Als u verbinding wilt maken met het doel [!DNL Adobe Commerce] :

1. In de [&#x200B; interface van Experience Platform &#x200B;](https://experience.adobe.com/platform/), ga **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.
1. Selecteer **[!UICONTROL Personalization]**.
1. Selecteer de Adobe Commerce-bestemming om deze te markeren en selecteer vervolgens **[!UICONTROL Set up]** .
1. Volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven.

### Verbindingsparameters {#parameters}

Terwijl [&#x200B; vestiging &#x200B;](../../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

- **[!UICONTROL Name]**: vul de voorkeursnaam voor dit doel in.
- **[!UICONTROL Description]**: voer een beschrijving in voor uw doel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken. Dit veld is optioneel.
- **[!UICONTROL Integration alias]**: deze waarde wordt als een JSON-objectnaam verzonden naar de Experience Platform Web SDK.
- **[!UICONTROL Datastream ID]**: hiermee wordt bepaald welke gegevensstroom voor gegevensverzameling het publiek bevat dat wordt opgenomen in het antwoord op de pagina. Het drop-down menu toont slechts gegevensstromen die de toegelaten bestemmingsconfiguratie hebben. Zie [&#x200B; Vormend een datastream &#x200B;](../../../datastreams/overview.md) voor meer details.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar [!DNL Commerce] doel activeren {#activate}

>[!IMPORTANT]
>
>Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Lees [&#x200B; activeer profielen en publiek aan de bestemmingen van het profielverzoek &#x200B;](../../ui/activate-edge-personalization-destinations.md) voor instructies bij het activeren van publiek aan de [!DNL Commerce] bestemming.

## Volgende stappen in [!DNL Adobe Commerce] {#next-steps-adobe-commerce}

Nu u het doel [!DNL Commerce] hebt geconfigureerd in Experience Platform, moet u de extensie [!DNL Audience Activation] installeren in [!DNL Commerce] en [!DNL Commerce Admin] configureren om het gemaakte publiek [!DNL Real-Time CDP] te importeren. Zie de [[!DNL Commerce]  documentatie &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html) om meer te leren.

## Activering van publiek valideren in Commerce {#exported-data}

Nadat u [!DNL Real-Time CDP] publiek aan uw [!DNL Adobe Commerce] rekening activeert, zult u die publiek zien beschikbaar wanneer u naar _Admin_ sidebar gaat, dan **[!UICONTROL Customers]** > **[!UICONTROL Real-Time CDP Audience]** gaan.

![&#x200B; het Dashboard van het Soorten Soorten publiek van Real-Time CDP &#x200B;](../../assets/catalog/personalization/adobe-commerce/audience-library.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, lees het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](/help/data-governance/home.md).

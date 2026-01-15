---
title: Adobe Commerce-bestemmingsconnector
description: Leer hoe verkopers van Adobe Commerce en Real-Time CDP de winkelervaring kunnen aanpassen door zeer relevante site-inhoud en -promoties te leveren, aangepast aan klanten die in Real-Time CDP zijn gebouwd en beheerd.
exl-id: f7aa3c6c-ba7a-440c-a4d7-5d7b50dbbc0d
source-git-commit: 70556134a96260ae111c71ee288d4d646481270b
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 0%

---

# Adobe Commerce-verbinding {#adobe-commerce}

## Overzicht {#overview}

Met de [!DNL Adobe Commerce] -doelconnector kunt u een of meer Real-Time CDP-soorten publiek selecteren om te activeren naar uw [!DNL Adobe Commerce] -account voor een dynamische, gepersonaliseerde ervaring voor uw klanten. Binnen [!DNL Adobe Commerce] kunt u vervolgens die Real-Time CDP-doelgroepen selecteren om unieke aanbiedingen in het winkelwagentje aan te passen, zoals &#39;Koop 2 krijg 1 gratis,&#39;. U kunt ook hoofdbanners weergeven en de productprijzen aanpassen aan de hand van promotieaanbiedingen die allemaal zijn aangepast aan het Adobe Real-Time CDP-publiek.

## Vereisten {#prerequisites}

Deze connector is beschikbaar in de catalogus met doelen voor klanten die Real-Time CDP Prime of Ultimate en Adobe Commerce hebben aangeschaft.

Om deze bestemmingsverbinding te gebruiken, zorg ervoor dat u toegang hebt tot:

- [ Adobe Experience Platform ](https://experience.adobe.com/)
- [ Adobe Developer Console ](https://developer.adobe.com/developer-console/docs/guides/getting-started/). Met toegang tot de ontwikkelaarsconsole, kunt u de dienstrekening en credentieinformatie bekijken die nodig is om [ de configuratie ](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html#configure-the-extension) van de uitbreiding in Adobe Commerce te voltooien.
- [ versie van Adobe Commerce 2.4.4 of hoger ](https://business.adobe.com/products/commerce.html)

In Experience Platform maakt u het volgende:

- [ Schema ](../../../xdm/schema/composition.md). Het schema dat u maakt, vertegenwoordigt de gegevens die u vanuit Adobe Commerce wilt invoeren. [ leer meer ](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html) over hoe te om een schema tot stand te brengen dat Commerce-Specifieke gebiedsgroepen bevat.
- [ Dataset ](../../../catalog/datasets/user-guide.md#create). Een dataset is een opslag en beheersconstructie voor een inzameling van gegevens. U creeert deze dataset van het schema dat u hierboven creeerde.
- [ DataStream ](../../../datastreams/overview.md#create). ID waarmee gegevens kunnen worden verzonden van Adobe Experience Platform naar andere Adobe DX-producten. Deze id moet zijn gekoppeld aan een specifieke website in uw specifieke Adobe Commerce-exemplaar. Wanneer u deze gegevensstroom creeert, specificeer het XDM schema u hierboven creeerde.

Maak verbinding met het doel [!DNL Commerce] nadat u aan de voorwaarden hebt voldaan.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Als u verbinding wilt maken met het doel [!DNL Adobe Commerce] :

1. In de [ interface van Experience Platform ](https://experience.adobe.com/platform/), ga **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.
1. Selecteer **[!UICONTROL Personalization]**.
1. Selecteer de Adobe Commerce-bestemming om deze te markeren en selecteer vervolgens **[!UICONTROL Set up]** .
1. Volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven.

### Verbindingsparameters {#parameters}

Terwijl [ vestiging ](../../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

- **[!UICONTROL Name]**: vul de voorkeursnaam voor dit doel in.
- **[!UICONTROL Description]**: voer een beschrijving in voor uw doel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken. Dit veld is optioneel.
- **[!UICONTROL Integration alias]**: deze waarde wordt als een JSON-objectnaam verzonden naar de Experience Platform Web SDK.
- **[!UICONTROL Datastream ID]**: hiermee wordt bepaald welke gegevensstroom voor gegevensverzameling het publiek bevat dat wordt opgenomen in het antwoord op de pagina. Het drop-down menu toont slechts gegevensstromen die de toegelaten bestemmingsconfiguratie hebben. Zie [ Vormend een datastream ](../../../datastreams/overview.md) voor meer details.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar [!DNL Commerce] doel activeren {#activate}

>[!IMPORTANT]
> 
>Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Lees [ activeer profielen en publiek aan de bestemmingen van het profielverzoek ](../../ui/activate-edge-personalization-destinations.md) voor instructies bij het activeren van publiek aan de [!DNL Commerce] bestemming.

## Volgende stappen in [!DNL Adobe Commerce]

Nu u de [!DNL Commerce] -bestemming hebt geconfigureerd in Experience Platform, moet u de [!DNL Audience Activation] -extensie installeren in [!DNL Commerce] en de [!DNL Commerce Admin] configureren om het door u gemaakte Real-Time CDP-publiek te importeren. Zie de [[!DNL Commerce]  documentatie ](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html) om meer te leren.

## Activering van publiek valideren in Commerce {#exported-data}

Nadat u het publiek van Real-Time CDP aan uw [!DNL Adobe Commerce] rekening activeert, zult u die publiek zien beschikbaar wanneer u naar _Admin_ sidebar gaat, dan **[!UICONTROL Customers]** > **[!UICONTROL Real-Time CDP Audience]** gaan.

![ het Dashboard van het Soorten Soorten publiek van Real-Time CDP ](../../assets/catalog/personalization/adobe-commerce/audience-library.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, lees het [ overzicht van het Beleid van Gegevens ](/help/data-governance/home.md).

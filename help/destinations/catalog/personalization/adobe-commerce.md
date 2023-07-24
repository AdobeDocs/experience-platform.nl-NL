---
title: Adobe Commerce-bestemmingsconnector
description: Leer hoe verkopers van Adobe Commerce en Real-Time CDP de winkelervaring kunnen aanpassen door zeer relevante site-inhoud en -promoties te leveren, aangepast aan klanten die in Real-Time CDP zijn gebouwd en beheerd.
exl-id: f7aa3c6c-ba7a-440c-a4d7-5d7b50dbbc0d
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 1%

---

# Adobe Commerce-verbinding {#adobe-commerce}

## Overzicht {#overview}

De [!DNL Adobe Commerce] met de doelconnector kunt u een of meer Real-Time CDP-soorten publiek selecteren die u voor uw [!DNL Adobe Commerce] -account voor een dynamische, op maat gesneden ervaring voor kopers. Within [!DNL Adobe Commerce], kunt u die Real-Time CDP-publiek selecteren om unieke aanbiedingen in de winkelwagen aan te passen, zoals &#39;Koop 2 krijg 1 gratis,&#39;. U kunt ook hoofdbanners weergeven en de productprijzen aanpassen aan de hand van promotieaanbiedingen die allemaal zijn aangepast aan het Adobe Real-Time CDP-publiek.

## Vereisten {#prerequisites}

Deze aansluiting is beschikbaar in de catalogus met doelen voor klanten die Real-Time CDP Premiere of Ultimate en Adobe Commerce hebben aangeschaft.

Om deze bestemmingsverbinding te gebruiken, zorg ervoor dat u toegang hebt tot:

- [Adobe Experience Platform](https://experience.adobe.com/)
- [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started/). Met toegang tot de ontwikkelaarsconsole, kunt u de dienstrekening en de referentie informatie bekijken die nodig is aan [voltooi de configuratie](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html#configure-the-extension) van de verlenging in Adobe Commerce.
- [Adobe Commerce Cloud versie 2.4.4 of hoger](https://business.adobe.com/products/magento/magento-commerce.html)

In Experience Platform, creeer het volgende:

- [Schema](../../../xdm/schema/composition.md). Het schema dat u maakt, vertegenwoordigt de gegevens die u vanuit Adobe Commerce wilt invoeren. [Meer informatie](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/update-xdm.html) over hoe te om een schema tot stand te brengen dat handel-specifieke gebiedsgroepen bevat.
- [Gegevensset](../../../catalog/datasets/user-guide.md#create). Een dataset is een opslag en beheersconstructie voor een inzameling van gegevens. U creeert deze dataset van het schema dat u hierboven creeerde.
- [DataStream](../../../datastreams/overview.md#create). ID die gegevens om van Adobe Experience Platform aan andere Adobe DX producten toestaat te stromen. Deze id moet zijn gekoppeld aan een specifieke website in uw specifieke Adobe Commerce-exemplaar. Wanneer u deze gegevensstroom creeert, specificeer het XDM schema u hierboven creeerde.

Nadat u de eerste vereisten hebt voltooid, maakt u verbinding met de [!DNL Commerce] bestemming.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met de [!DNL Adobe Commerce] bestemming:

1. In de [Interface Platform](https://experience.adobe.com/platform/), ga naar **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.
1. Selecteer **[!UICONTROL Personalization]**.
1. Selecteer de Adobe Commerce-bestemming om deze te markeren en selecteer vervolgens **[!UICONTROL Set up]**.
1. Voer de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

### Verbindingsparameters {#parameters}

while [opzetten](../../ui/connect-destination.md) voor deze bestemming moet u de volgende informatie opgeven:

- **[!UICONTROL Name]**: Vul de voorkeursnaam voor dit doel in.
- **[!UICONTROL Description]**: Voer een beschrijving in voor uw bestemming. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken. Dit veld is optioneel.
- **[!UICONTROL Integration alias]**: Deze waarde wordt verzonden naar het Web SDK van het Experience Platform als JSON objecten naam.
- **[!UICONTROL Datastream ID]**: Dit bepaalt welke gegevensstroom van de Inzameling van Gegevens het publiek bevat dat in de reactie op de pagina inbegrepen is. Het drop-down menu toont slechts gegevensstromen die de toegelaten bestemmingsconfiguratie hebben. Zie [Een gegevensstroom configureren](../../../datastreams/overview.md) voor meer informatie .

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over waarschuwingen raadpleegt u de handleiding over [het abonneren aan bestemmingen alarm gebruikend UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek activeren voor de [!DNL Commerce] doel {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Lezen [Profielen en publiek activeren om aanvraagdoelen voor profielen te bepalen](../../ui/activate-edge-personalization-destinations.md) voor instructies over het activeren van het publiek aan de [!DNL Commerce] bestemming.

## Volgende stappen in [!DNL Adobe Commerce]

Nu u hebt gevormd [!DNL Commerce] doel binnen Experience Platform, moet u installeren [!DNL Audience Activation] extensie in [!DNL Commerce] en configureert u de [!DNL Commerce Admin] om het Real-Time CDP-publiek dat u hebt gemaakt te importeren. Zie de [[!DNL Commerce] documentatie](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html) voor meer informatie.

## Activering van publiek valideren bij Handel {#exported-data}

Nadat u Real-Time CDP-publiek hebt geactiveerd voor uw [!DNL Adobe Commerce] -account, worden de publiek beschikbare soorten publiek weergegeven wanneer u naar de _Beheer_ zijbalk, ga vervolgens naar **[!UICONTROL Customers]** > **[!UICONTROL Real-time CDP Audience]**.

![Real-Time CDP-dashboard Soorten publiek](../../assets/catalog/personalization/adobe-commerce/audience-library.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] dwingt gegevensbeheer af, lees de [Overzicht van gegevensbeheer](/help/data-governance/home.md).

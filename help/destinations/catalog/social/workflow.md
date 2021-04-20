---
keywords: Facebook;facebook;Sociaal netwerk;Sociaal netwerk;Sociale authenticatie;Sociale netwerkverificatie
title: Een sociale bestemming maken
type: Tutorial
description: Leer hoe u verbinding kunt maken met uw sociale-advertentierekeningen in Adobe Experience Platform.
exl-id: a0cdf2b7-b1e8-4a8e-9d5b-58a118e7b689
translation-type: tm+mt
source-git-commit: e2af4fcfe232889f3f928c00c9f9b37cf9754ca1
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# Een sociale bestemming maken {#social-network-destinations-workflow}

## Overzicht {#overview}

Deze zelfstudie gebruikt [!DNL Facebook] als voorbeeld, maar de Adobe Experience Platform-workflow is hetzelfde voor alle sociale doelen.

## Vorm sociale bestemming - videoanalyse {#video}

In de onderstaande video ziet u hoe u een sociale bestemming configureert en segmenten activeert in Adobe Experience Platform. De stappen worden ook achtereenvolgens beschreven in de volgende secties.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

## Sociale bestemming {#select-destination} selecteren

Blader in **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** naar de categorie **[!UICONTROL Social]**. Selecteer uw voorkeur voor sociale bestemming en selecteer **[!UICONTROL Configure]**.

![Verbinden met sociale bestemming](../../assets/catalog/social/workflow/catalog.png)

>[!NOTE]
>
>Als er al een verbinding met dit doel bestaat, kunt u een **[!UICONTROL Activate]** knop op de doelkaart zien. Raadpleeg voor meer informatie over het verschil tussen **[!UICONTROL Activate]** en **[!UICONTROL Configure]** de sectie [Catalog](../../ui/destinations-workspace.md#catalog) van de documentatie van de doelwerkruimte.

## Accountstap {#account}

Als u in de stap **Account** eerder een verbinding met uw sociale bestemming hebt ingesteld, selecteert u **[!UICONTROL Existing Account]** en selecteert u de bestaande verbinding. U kunt ook **[!UICONTROL New Account]** selecteren om een nieuwe verbinding met uw sociale bestemming in te stellen. Selecteer **[!UICONTROL Connect to destination]** en hiermee gaat u naar de geselecteerde sociale bestemming om u aan te melden en Adobe Experience Cloud te verbinden met uw account voor sociale advertenties.

>[!NOTE]
>
>Platform ondersteunt validatie van gebruikersgegevens in het verificatieproces en geeft een foutbericht weer als u onjuiste gegevens hebt ingevoerd voor uw sociale account-id. Dit zorgt ervoor dat u de werkstroom niet met onjuiste geloofsbrieven voltooit.

![Verbinden met sociale bestemming - authentificatiestap](../../assets/catalog/social/workflow/pre-connect.png)

Nadat uw aanmeldingsgegevens zijn bevestigd en Adobe Experience Cloud is aangesloten op uw sociale netwerk, kunt u **[!UICONTROL Next]** selecteren om door te gaan naar de stap **[!UICONTROL Authentication]**.

![Credentials bevestigd](../../assets/catalog/social/workflow/post-connect.png)

## Verificatiestap {#authentication}

Voer in de stap **[!UICONTROL Authentication]** een [!UICONTROL Name] en een [!UICONTROL Description] in voor uw activeringsstroom en vul [!UICONTROL Account ID] van uw sociale netwerk en account in.

>[!IMPORTANT]
>
> * Voor [!DNL Facebook] bestemmingen, **[!UICONTROL Account ID]** is uw [!DNL Facebook Ad Account ID]. U kunt deze id vinden in [!DNL Facebook Ads Manager]. Plaats een voorvoegsel voor de id `act_`, zoals in de onderstaande afbeelding wordt weergegeven.
> * Voor [!DNL LinkedIn] bestemmingen, **[!UICONTROL Account ID]** is uw [!DNL LinkedIn Campaign Manager Account ID]. U kunt deze id vinden in [!DNL LinkedIn Campaign Manager].


![Verbinden met sociale bestemming - authentificatiestap](../../assets/catalog/social/workflow/authentication.png)

In deze stap kunt u ook elke **[!UICONTROL Marketing action]** selecteren die op dit doel moet worden toegepast. Marketingsacties geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door Adobe gedefinieerde marketingacties of u kunt uw eigen marketingactie maken. Voor meer informatie over marketing acties, zie [Overzicht van het beleid van het gebruik van Gegevens](../../../data-governance/policies/overview.md).

Selecteer **[!UICONTROL Create Destination]** nadat u de bovenstaande velden hebt ingevuld.

Uw doel is nu gemaakt. U kunt **[!UICONTROL Save & Exit]** selecteren als u segmenten later wilt activeren of u kunt **[!UICONTROL Next]** selecteren om de workflow voort te zetten en segmenten te selecteren om te activeren. In beide gevallen, zie de volgende sectie, [Activate segmenten aan sociale bestemmingen](#activate-segments), voor de rest van het werkschema.

## Segmenten naar sociale doelen activeren {#activate-segments}

Voor instructies op hoe te om segmenten aan sociale bestemmingen te activeren, zie [Gegevens aan Doelen activeren](../../ui/activate-destinations.md).

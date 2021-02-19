---
keywords: Facebook;Facebook;Sociaal netwerk;Sociaal netwerk;Sociale netwerkverificatie;Sociale netwerkverificatie;Sociale netwerkverificatie
title: Een sociale netwerkbestemming maken
type: Tutorial
description: Leer hoe u verbinding maakt met uw sociale netwerk en accounts in Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 6e7ecfdc0b2cbf6f07e6b2220ec163289511375e
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---


# Een sociale netwerkbestemming maken {#social-network-destinations-workflow}

In deze zelfstudie wordt [!DNL Facebook] als voorbeeld gebruikt, maar de workflow in Adobe Experience Platform is hetzelfde voor alle sociale netwerkbestemmingen, en deze wordt opnieuw aan het product toegevoegd.

Blader in **[!UICONTROL Doelen]** > **[!UICONTROL Catalogus]** naar de categorie **[!UICONTROL Sociaal]**. Selecteer uw aangewezen sociale netwerkbestemming, dan uitgezocht **[!UICONTROL vorm]**.

![Verbinden met sociale netwerkbestemming](../../assets/catalog/social/workflow/catalog.png)

>[!NOTE]
>
>Als er al een verbinding met dit doel bestaat, kunt u een **[!UICONTROL knop Activeer]** op de doelkaart zien. Voor meer informatie over het verschil tussen **[!UICONTROL Activate]** en **[!UICONTROL Configure]**, verwijs naar [Catalog](../../ui/destinations-workspace.md#catalog) sectie van de documentatie van de bestemmingswerkruimte.

Als u in de stap **Verificatie** eerder een verbinding met uw sociale netwerkbestemming had ingesteld, selecteert u **[!UICONTROL Bestaande account]** en selecteert u de bestaande verbinding. U kunt ook **[!UICONTROL Nieuwe account]** selecteren om een nieuwe verbinding met uw sociale netwerkbestemming in te stellen. Selecteer **[!UICONTROL Verbinding maken met doel]**. Hiermee gaat u naar de geselecteerde sociale netwerkbestemming om u aan te melden en Adobe Experience Cloud te verbinden met uw sociale netwerk-advertentieaccount.

>[!NOTE]
>
>Platform ondersteunt validatie van gebruikersgegevens in het verificatieproces en geeft een foutbericht weer als u onjuiste gegevens hebt ingevoerd voor uw sociale-netwerkaccount-id. Dit zorgt ervoor dat u de werkstroom niet met onjuiste geloofsbrieven voltooit.

![Verbinden met sociale netwerkbestemming - authentificatiestap](../../assets/catalog/social/workflow/pre-connect.png)

Nadat uw aanmeldingsgegevens zijn bevestigd en Adobe Experience Cloud is aangesloten op uw sociale netwerk, kunt u **[!UICONTROL Next]** selecteren om door te gaan naar de stap **[!UICONTROL Setup]**.

![Credentials bevestigd](../../assets/catalog/social/workflow/post-connect.png)

Voer in de stap **[!UICONTROL Setup]** een [!UICONTROL Naam] en een [!UICONTROL Beschrijving] in voor uw activeringsstroom en vul [!UICONTROL Account ID] van uw sociale netwerk en account in.

Ook in deze stap, kunt u om het even welke **[!UICONTROL Handeling van de Marketing]** selecteren die op deze bestemming zou moeten van toepassing zijn. Marketingsacties geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door Adobe gedefinieerde marketingacties of u kunt uw eigen marketingactie maken. Voor meer informatie over marketing acties, zie [Overzicht van het beleid van het gebruik van Gegevens](../../../data-governance/policies/overview.md).

Selecteer **[!UICONTROL Doel maken]** nadat u de bovenstaande velden hebt ingevuld.

>[!IMPORTANT]
>
> * Voor [!DNL Facebook] doelen. **[!UICONTROL Account-]** id is uw  [!DNL Facebook Ad Account ID]. U kunt deze id vinden in [!DNL Facebook Ads Manager]. Plaats de id vooraf in `act_`, zoals hieronder wordt weergegeven:


![Verbinden met sociale netwerkbestemming - opstellingsstap](../../assets/catalog/social/workflow/setup.png)

Uw doel is nu gemaakt. U kunt **[!UICONTROL Opslaan en afsluiten]** selecteren als u segmenten later wilt activeren of u kunt **[!UICONTROL Volgende]** selecteren om door te gaan met de workflow en segmenten te selecteren om te activeren. In beide gevallen, zie de volgende sectie, [Activate segmenten aan sociale netwerken](#activate-segments), voor de rest van het werkschema.

## Segmenten activeren op sociale netwerken {#activate-segments}

Voor instructies op hoe te om segmenten aan sociale netwerken te activeren, zie [Gegevens aan Doelen activeren](../../ui/activate-destinations.md).
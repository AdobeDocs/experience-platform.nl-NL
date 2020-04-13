---
title: Workflow voor sociale netwerkdoelen
seo-title: Workflow voor sociale netwerkdoelen
description: Instructies om verbinding te maken met uw sociale netwerk en accounts
seo-description: Instructies om verbinding te maken met uw sociale netwerk en accounts
translation-type: tm+mt
source-git-commit: bfcbc56f05fa1c3b5fafd57b1166e50130b6007d

---


# (bèta) Workflow voor verificatie van sociale netwerkdoelen {#social-network-destinations-workflow}


>[!IMPORTANT]
>
>De workflow voor het maken van sociale netwerkdoelen in Adobe Real-time CDP bevindt zich momenteel in de bètaversie en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

## Workflow voor het maken van cloudopslagdoelen

In deze zelfstudie wordt Facebook als voorbeeld gebruikt, maar de workflow in het Adobe Real-time Customer Data Platform is hetzelfde voor alle sociale netwerkdoelen, wanneer het product opnieuw wordt toegevoegd.

1. Blader in **[!UICONTROL Connections > Destinations]** naar de **[!UICONTROL Social]** categorie. Selecteer uw voorkeur sociale netwerkbestemming, dan uitgezocht **[!UICONTROL Connect destination]**.

   ![Verbinden met sociale netwerkbestemming](/help/rtcdp/destinations/assets/facebook-catalog-view.png)

2. Als u in de stap **Verificatie** eerder een verbinding met uw sociale netwerkbestemming had ingesteld, selecteert **[!UICONTROL Existing Account]** en selecteert u de bestaande verbinding. U kunt ook een nieuwe verbinding **[!UICONTROL New Account]** met uw sociale netwerkbestemming instellen. Selecteer **[!UICONTROL Connect to destination]** en hiermee gaat u naar de geselecteerde sociale netwerkbestemming om u aan te melden en Adobe Experience Cloud te verbinden met uw sociale netwerk Ad-account.

   >[!NOTE]
   >
   >Adobe CDP in real-time ondersteunt aanmeldingsvalidatie in het verificatieproces en geeft een foutbericht weer als u onjuiste gegevens hebt ingevoerd in de id van uw sociale netwerkaccount. Dit zorgt ervoor dat u de werkstroom niet met onjuiste geloofsbrieven voltooit.

   ![Verbinden met sociale netwerkbestemming - authentificatiestap](/help/rtcdp/destinations/assets/facebook-pre-connect-view.png)

3. Nadat uw referenties zijn bevestigd en Adobe Experience Cloud is verbonden met uw sociale netwerk, kunt u kiezen **[!UICONTROL Next]** om door te gaan naar de **[!UICONTROL Setup]** stap.

   ![Credentials bevestigd](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

4. Voer in de **[!UICONTROL Setup]** stap een **[!UICONTROL Name]** en een **[!UICONTROL Description]** waarde in voor de activeringsstroom en vul de **[!UICONTROL Account ID]** van uw sociale netwerk en account in. Selecteer deze optie **[!UICONTROL Create Destination]** nadat u de bovenstaande velden hebt ingevuld.

   >[!IMPORTANT]
   >
   >Voor Facebook-bestemmingen. **[!UICONTROL Account ID]** is uw Facebook advertentie-account-id. U vindt deze id in Facebook Ads Manager. Plaats de id vooraf in de `act_` onderstaande afbeelding:

   ![Verbinden met sociale netwerkbestemming - opstellingsstap](/help/rtcdp/destinations/assets/social-network-step.png)

5. Uw doel is nu gemaakt. U kunt selecteren **[!UICONTROL Save & Exit]** als u segmenten later wilt activeren of u kunt selecteren **[!UICONTROL Next]** om de workflow voort te zetten en segmenten te selecteren om te activeren. In beide gevallen raadpleegt u de volgende sectie Segmenten [activeren voor sociale netwerken](#activate-segments)voor de rest van de workflow.

## Segmenten activeren op sociale netwerken {#activate-segments}

Voor instructies op hoe te om segmenten aan sociale netwerken te activeren, zie Gegevens aan Doelen [activeren](/help/rtcdp/destinations/activate-destinations.md).
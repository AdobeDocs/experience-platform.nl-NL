---
title: Workflow voor sociale netwerkdoelen
seo-title: Workflow voor sociale netwerkdoelen
description: Instructies om verbinding te maken met uw sociale netwerk en accounts
seo-description: Instructies om verbinding te maken met uw sociale netwerk en accounts
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 0%

---


# Verificatieworkflow voor bestemmingen voor sociale netwerken {#social-network-destinations-workflow}

## Workflow om sociale netwerkdoelen te maken

Deze zelfstudie gebruikt [!DNL Facebook] als voorbeeld, maar de workflow in het Adobe Real-time Platform van klantgegevens zal hetzelfde zijn voor alle sociale netwerkbestemmingen, wanneer er nog meer aan het product wordt toegevoegd.

1. Blader in **[!UICONTROL Doelen > Catalogus]** naar de categorie **[!UICONTROL Sociaal]** . Selecteer de gewenste sociale netwerkbestemming en selecteer vervolgens de **[!UICONTROL Connect-bestemming]**.

   ![Verbinden met sociale netwerkbestemming](/help/rtcdp/destinations/assets/facebook-catalog-view.png)

2. Als u in de stap **Verificatie** eerder een verbinding met uw sociale netwerkbestemming had ingesteld, selecteert u **[!UICONTROL Bestaande account]** en selecteert u de bestaande verbinding. U kunt ook **[!UICONTROL Nieuwe account]** selecteren om een nieuwe verbinding met uw sociale netwerkbestemming in te stellen. Selecteer **[!UICONTROL Verbinding maken met doel]** . Hiermee gaat u naar de geselecteerde sociale netwerkbestemming om u aan te melden en Adobe Experience Cloud te verbinden met uw sociale netwerk en account Advertentie.

   >[!NOTE]
   >
   >Adobe CDP in real time steunt geloofsbevestiging in het authentificatieproces en toont een foutenmelding als u onjuiste geloofsbrieven aan uw identiteitskaart van de sociale netwerkrekening invoert. Dit zorgt ervoor dat u de werkstroom niet met onjuiste geloofsbrieven voltooit.

   ![Verbinden met sociale netwerkbestemming - authentificatiestap](/help/rtcdp/destinations/assets/facebook-pre-connect-view.png)

3. Zodra uw geloofsbrieven worden bevestigd en Adobe Experience Cloud wordt aangesloten aan uw sociaal netwerk, kunt u **[!UICONTROL Volgende]** selecteren om aan de stap van de **[!UICONTROL Opstelling]** te werk te gaan.

   ![Credentials bevestigd](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

4. Voer in de stap **[!UICONTROL Setup]** een **[!UICONTROL naam]** en een **[!UICONTROL beschrijving]** in voor de activeringsstroom en vul de **[!UICONTROL account-id]** van uw sociale netwerk en account in. <br> Ook in deze stap kunt u elke **[!UICONTROL Gebruikszaak]** voor marketingdoeleinden selecteren die op deze bestemming moet worden toegepast. Gebruiksgevallen voor marketingdoeleinden geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door de Adobe gedefinieerde gebruiksgevallen voor marketingdoeleinden of u kunt uw eigen gebruiksscenario voor marketingdoeleinden maken. Voor meer informatie over het op de markt brengen van gebruiksgevallen, zie de [Governance van Gegevens in Echte tijd CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) pagina. Voor informatie over de individuele Adobe-bepaalde het in de handel brengen gebruiksgevallen, zie het overzicht [van het het gebruiksbeleid van](/help/data-governance/policies/overview.md#core-actions)Gegevens. <br> Selecteer Doel **** maken nadat u de bovenstaande velden hebt ingevuld.

   >[!IMPORTANT]
   >
   > * Het marketinggeval *Single Identity Personalization* wordt standaard geselecteerd voor sociale netwerkdoelen en kan niet worden verwijderd.
   > * Voor [!DNL Facebook] bestemmingen. **[!UICONTROL Account ID]** is je [!DNL Facebook Ad Account ID]. U vindt deze id in de [!DNL Facebook Ads Manager]lijst. Plaats de id vooraf in de `act_` onderstaande afbeelding:


   ![Verbinden met sociale netwerkbestemming - opstellingsstap](/help/rtcdp/destinations/assets/social-networks-setup-step.png)

5. Uw doel is nu gemaakt. U kunt **[!UICONTROL Opslaan en afsluiten]** selecteren als u segmenten later wilt activeren of u kunt **[!UICONTROL Volgende]** selecteren om de workflow voort te zetten en segmenten te selecteren om te activeren. In beide gevallen raadpleegt u de volgende sectie Segmenten [activeren voor sociale netwerken](#activate-segments)voor de rest van de workflow.

## Segmenten activeren op sociale netwerken {#activate-segments}

Voor instructies op hoe te om segmenten aan sociale netwerken te activeren, zie Gegevens aan Doelen [activeren](/help/rtcdp/destinations/activate-destinations.md).
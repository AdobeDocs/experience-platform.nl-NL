---
title: Workflow voor opslagdoelen voor cloud
seo-title: Workflow voor opslagdoelen voor cloud
description: Instructies voor het maken van verbinding met de opslaglocaties van uw cloud
seo-description: Instructies voor het maken van verbinding met de opslaglocaties van uw cloud
translation-type: tm+mt
source-git-commit: 225f18bd0d092bdae7b4cc99c278e850be9cfd56

---


# Workflow voor het maken van cloudopslagdoelen

## Overzicht

Op deze pagina wordt uitgelegd hoe u verbinding kunt maken met cloudopslaglocaties in het Adobe Real-time Customer Data Platform.

1. Kies in **[!UICONTROL Verbindingen > Doelen]** de gewenste bestemming voor cloudopslag en selecteer **[!UICONTROL Verbindingsbestemming]**.

   ![Verbinding maken met bestemming voor cloudopslag](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

2. Als u in de stap **Verificatie** eerder een verbinding met uw bestemming voor cloudopslag had ingesteld, selecteert u **[!UICONTROL Bestaande account]** en selecteert u de bestaande verbinding. U kunt ook **[!UICONTROL Nieuwe account]** selecteren om een nieuwe verbinding met de bestemming voor cloudopslag in te stellen. Vul de verificatiereferenties van uw account in en selecteer **[!UICONTROL Verbinding maken met doel]**.

   >[!NOTE]
   >
   >Adobe CDP in real-time ondersteunt aanmeldingsvalidatie in het verificatieproces en geeft een foutbericht weer als u onjuiste gegevens hebt ingevoerd op de opslaglocatie in de cloud. Dit zorgt ervoor dat u de werkstroom niet met onjuiste geloofsbrieven voltooit.

   ![Verbinding maken met bestemming voor cloudopslag - verificatiestap](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

3. Voer in de stap **[!UICONTROL Instellen]** een **[!UICONTROL naam]** en een **[!UICONTROL bestemming]** in voor de activeringsstroom en voeg het pad **[!UICONTROL naar de]** map in de opslagbestemming van de cloud in waar de bestanden worden geleverd. Selecteer Doel **** maken nadat u de bovenstaande velden hebt ingevuld.

   ![Verbinding maken met bestemming voor cloudopslag - verificatiestap](/help/rtcdp/destinations/assets/cloud-destinations-setup-step.png)

4. Uw doel is nu gemaakt. U kunt **[!UICONTROL Opslaan en afsluiten]** selecteren als u segmenten later wilt activeren of u kunt **[!UICONTROL Volgende]** selecteren om de workflow voort te zetten en segmenten te selecteren om te activeren. In beide gevallen raadpleegt u de volgende sectie Segmenten [](#activate-segments)activeren voor de rest van de workflow.

## Segmenten activeren {#activate-segments}

Zie Profielen en segmenten [activeren naar een doel](/help/rtcdp/destinations/activate-destinations.md) voor informatie over de workflow voor segmentactivering.
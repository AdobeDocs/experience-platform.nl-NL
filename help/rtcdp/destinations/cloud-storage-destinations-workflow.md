---
title: Workflow voor opslagdoelen voor cloud
seo-title: Workflow voor opslagdoelen voor cloud
description: Instructies voor het maken van verbinding met de opslaglocaties van uw cloud
seo-description: Instructies voor het maken van verbinding met de opslaglocaties van uw cloud
translation-type: tm+mt
source-git-commit: 9221c11a30bda3a155d73afec16be55ef8f5d133

---


# Workflow voor het maken van cloudopslagdoelen

## Overzicht

Op deze pagina wordt uitgelegd hoe u verbinding kunt maken met cloudopslaglocaties in het Adobe Real-time Customer Data Platform.

1. Selecteer **[!UICONTROL Connections > Destinations]** in de optie de voorkeursbestemming voor cloudopslag en selecteer **[!UICONTROL Connect destination]**.

   ![Verbinding maken met bestemming voor cloudopslag](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

2. Als u in de stap **Verificatie** eerder een verbinding met de bestemming voor cloudopslag hebt ingesteld, selecteert **[!UICONTROL Existing Account]** en selecteert u de bestaande verbinding. U kunt ook een nieuwe verbinding met de opslaglocatie van de cloud instellen **[!UICONTROL New Account]** . Vul de verificatiereferenties van uw account in en selecteer **[!UICONTROL Connect to destination]**.

   >[!NOTE]
   >
   >Adobe CDP in real-time ondersteunt aanmeldingsvalidatie in het verificatieproces en geeft een foutbericht weer als u onjuiste gegevens hebt ingevoerd op de opslaglocatie in de cloud. Dit zorgt ervoor dat u de werkstroom niet met onjuiste geloofsbrieven voltooit.

   ![Verbinding maken met bestemming voor cloudopslag - verificatiestap](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

3. Voer in de **[!UICONTROL Setup]** stap een **[!UICONTROL Name]** en een **[!UICONTROL Description]** waarde in voor de activeringsstroom.
   1. Voeg voor Amazon S3-doelen de **[!UICONTROL Bucket name]** en de **[!UICONTROL Folder path]** gegevens in de opslaglocatie van de cloud in waar de bestanden worden geleverd. Selecteer deze optie **[!UICONTROL Create Destination]** nadat u de bovenstaande velden hebt ingevuld.
   2. Voor bestemmingen SFTP, neem het **[!UICONTROL Folder path]**
   ![Verbinding maken met bestemming voor cloudopslag - verificatiestap](/help/rtcdp/destinations/assets/cloud-destinations-setup-step.png)

4. Uw doel is nu gemaakt. U kunt selecteren **[!UICONTROL Save & Exit]** als u segmenten later wilt activeren of u kunt selecteren **[!UICONTROL Next]** om de workflow voort te zetten en segmenten te selecteren om te activeren. In beide gevallen raadpleegt u de volgende sectie Segmenten [](#activate-segments)activeren voor de rest van de workflow om gegevens te exporteren.

## Segmenten activeren {#activate-segments}

Zie Profielen en segmenten [activeren naar een doel](/help/rtcdp/destinations/activate-destinations.md) voor informatie over de workflow voor segmentactivering.
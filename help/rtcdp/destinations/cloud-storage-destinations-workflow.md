---
title: Workflow voor opslagdoelen voor cloud
seo-title: Workflow voor opslagdoelen voor cloud
description: Instructies voor het maken van verbinding met de opslaglocaties van uw cloud
seo-description: Instructies voor het maken van verbinding met de opslaglocaties van uw cloud
translation-type: tm+mt
source-git-commit: 37c51435ce8330dbd61857bda408df03ff21a491
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---


# Workflow voor het maken van cloudopslagdoelen

## Overzicht

Op deze pagina wordt uitgelegd hoe u verbinding kunt maken met cloudopslaglocaties in het Adobe Real-time Customer Data Platform.

1. Kies in **[!UICONTROL Verbindingen > Doelen]** de gewenste bestemming voor cloudopslag en selecteer **[!UICONTROL Verbindingsbestemming]**.

   ![Verbinding maken met bestemming voor cloudopslag](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

2. Als u in de stap **[!UICONTROL Verificatie]** eerder een verbinding met uw bestemming voor cloudopslag had ingesteld, selecteert u **[!UICONTROL Bestaande account]** en selecteert u de bestaande verbinding. U kunt ook **[!UICONTROL Nieuwe account]** selecteren om een nieuwe verbinding met de bestemming voor cloudopslag in te stellen. Vul de verificatiereferenties van uw account in en selecteer **[!UICONTROL Verbinding maken met doel]**. <br> Zie [bestemming Amazon S3](/help/rtcdp/destinations/amazon-s3-destination.md) , bestemming [Amazon Kinesis](/help/rtcdp/destinations/amazon-kinesis-destination.md) , [Azure Event Hubs](/help/rtcdp/destinations/azure-event-hubs-destination.md) bestemming, en bestemming [SFTP](/help/rtcdp/destinations/sftp-destination.md) voor details rond geloofsbrieven input in de stap van de **Authentificatie** .

   >[!NOTE]
   >
   >Adobe CDP in real-time ondersteunt aanmeldingsvalidatie in het verificatieproces en geeft een foutbericht weer als u onjuiste gegevens hebt ingevoerd op de opslaglocatie in de cloud. Dit zorgt ervoor dat u de werkstroom niet met onjuiste geloofsbrieven voltooit.

   ![Verbinding maken met bestemming voor cloudopslag - verificatiestap](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

3. Voer in de stap **[!UICONTROL Setup]** een **[!UICONTROL naam]** en een **[!UICONTROL beschrijving]** in voor de activeringsstroom. <br>
Voor Amazon S3-doelen voegt u de naam **[!UICONTROL van de]** emmertje en het pad naar de **[!UICONTROL map]** in de opslaglocatie van de cloud in waar de bestanden worden geleverd. Selecteer Doel **** maken nadat u de bovenstaande velden hebt ingevuld.

   ![Verbinding maken met Amazon S3-bestemming voor cloudopslag - verificatiestap](/help/rtcdp/destinations/assets/cloud-destinations-setup-step.png)

   Voeg voor SFTP-doelen het **[!UICONTROL mappad]** in waarin de bestanden worden geleverd.

   ![Verbinding maken met SFTP-cloudopslagbestemming - verificatiestap](/help/rtcdp/destinations/assets/sftp-destinations-setup-step.png)

4. Uw doel is nu gemaakt. U kunt **[!UICONTROL Opslaan en afsluiten]** selecteren als u segmenten later wilt activeren of u kunt **[!UICONTROL Volgende]** selecteren om de workflow voort te zetten en segmenten te selecteren om te activeren. In beide gevallen raadpleegt u de volgende sectie Segmenten [](#activate-segments)activeren voor de rest van de workflow om gegevens te exporteren.

## Segmenten activeren {#activate-segments}

Zie Profielen en segmenten [activeren naar een doel](/help/rtcdp/destinations/activate-destinations.md) voor informatie over de workflow voor segmentactivering.
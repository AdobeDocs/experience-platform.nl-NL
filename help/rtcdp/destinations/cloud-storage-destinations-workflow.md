---
title: Workflow voor opslagdoelen voor cloud
seo-title: Workflow voor opslagdoelen voor cloud
description: Instructies voor het maken van verbinding met de opslaglocaties van uw cloud
seo-description: Instructies voor het maken van verbinding met de opslaglocaties van uw cloud
translation-type: tm+mt
source-git-commit: 3c598454a868139b7604c5c7ca2b98fa0f1bb961
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---


# Workflow voor het maken van cloudopslagdoelen

## Overzicht

Op deze pagina wordt uitgelegd hoe u verbinding kunt maken met cloudopslaglocaties in Adobe Real-time Customer Data Platform.

1. Kies in **[!UICONTROL Verbindingen > Doelen]** de gewenste bestemming voor cloudopslag en selecteer **[!UICONTROL Verbindingsbestemming]**.

   ![Verbinding maken met bestemming voor cloudopslag](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

2. Als u in de stap **[!UICONTROL Verificatie]** eerder een verbinding met uw bestemming voor cloudopslag had ingesteld, selecteert u **[!UICONTROL Bestaande account]** en selecteert u de bestaande verbinding. U kunt ook **[!UICONTROL Nieuwe account]** selecteren om een nieuwe verbinding met de bestemming voor cloudopslag in te stellen. Vul de verificatiereferenties van uw account in en selecteer **[!UICONTROL Verbinding maken met doel]**. <br> Zie [bestemming Amazon S3](/help/rtcdp/destinations/amazon-s3-destination.md) , bestemming [Amazon Kinesis](/help/rtcdp/destinations/amazon-kinesis-destination.md) , [Azure Event Hubs](/help/rtcdp/destinations/azure-event-hubs-destination.md) bestemming, en bestemming [SFTP](/help/rtcdp/destinations/sftp-destination.md) voor details rond geloofsbrieven input in de stap van de **Authentificatie** .

   >[!NOTE]
   >
   >Adobe CDP in real-time ondersteunt aanmeldingsvalidatie in het verificatieproces en geeft een foutbericht weer als u onjuiste gegevens hebt ingevoerd op de opslaglocatie in de cloud. Dit zorgt ervoor dat u de werkstroom niet met onjuiste geloofsbrieven voltooit.

   ![Verbinding maken met bestemming voor cloudopslag - verificatiestap](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

3. Voer in de stap **[!UICONTROL Setup]** een **[!UICONTROL naam]** en een **[!UICONTROL beschrijving]** in voor de activeringsstroom. <br>
Ook in deze stap kunt u elke **[!UICONTROL Gebruikszaak]** voor marketingdoeleinden selecteren die op deze bestemming moet worden toegepast. Gebruiksgevallen voor marketingdoeleinden geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door Adobe gedefinieerde gevallen voor marketinggebruik of u kunt uw eigen gebruiksscenario voor marketingdoeleinden maken. Voor meer informatie over het op de markt brengen van gebruiksgevallen, zie de [Governance van Gegevens in Echte tijd CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) pagina. Zie het overzicht [van het beleid voor](/help/data-governance/policies/overview.md#core-actions)gegevensgebruik voor informatie over de afzonderlijke door Adobe gedefinieerde gevallen van marketinggebruik. <br>
Voor Amazon S3-doelen voegt u de naam **[!UICONTROL van de]** emmertje en het pad naar de **[!UICONTROL map]** in de opslaglocatie van de cloud in waar de bestanden worden geleverd. Selecteer Doel **** maken nadat u de bovenstaande velden hebt ingevuld.

   ![Verbinding maken met Amazon S3-bestemming voor cloudopslag - verificatiestap](/help/rtcdp/destinations/assets/amazon-s3-setup-step.png)

   Voeg voor SFTP-doelen het **[!UICONTROL mappad]** in waarin de bestanden worden geleverd. Selecteer Doel **** maken nadat u de bovenstaande velden hebt ingevuld.

   ![Verbinding maken met SFTP-cloudopslagbestemming - verificatiestap](/help/rtcdp/destinations/assets/sftp-destinations-setup-step.png)

   Geef voor Amazon Kinesis-doelen de naam van uw bestaande gegevensstroom op in uw [!DNL Amazon Kinesis] account. Adobe Real-time CDP exporteert gegevens naar deze stream. Selecteer Doel **** maken nadat u de bovenstaande velden hebt ingevuld.

   ![Verbinding maken met bestemming Kinesis-cloudopslag - verificatiestap](/help/rtcdp/destinations/assets/kinesis-destinations-setup-step.png)

   Geef voor Azure Event Hubs-bestemmingen de naam van uw bestaande gegevensstroom op in uw [!DNL Amazon Kinesis] account. Adobe Real-time CDP exporteert gegevens naar deze stream. Selecteer Doel **** maken nadat u de bovenstaande velden hebt ingevuld.

   ![Verbinding maken met bestemming Kinesis-cloudopslag - verificatiestap](/help/rtcdp/destinations/assets/eventhubs-destinations-setup-step.png)

4. Uw doel is nu gemaakt. U kunt **[!UICONTROL Opslaan en afsluiten]** selecteren als u segmenten later wilt activeren of u kunt **[!UICONTROL Volgende]** selecteren om de workflow voort te zetten en segmenten te selecteren om te activeren. In beide gevallen raadpleegt u de volgende sectie Segmenten [](#activate-segments)activeren voor de rest van de workflow om gegevens te exporteren.

## Segmenten activeren {#activate-segments}

Zie Profielen en segmenten [activeren naar een doel](/help/rtcdp/destinations/activate-destinations.md) voor informatie over de workflow voor segmentactivering.
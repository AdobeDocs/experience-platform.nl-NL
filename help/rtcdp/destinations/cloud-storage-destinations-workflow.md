---
keywords: cloud storage destination;cloud storage
title: Workflow voor opslagdoelen voor cloud
seo-title: Workflow voor opslagdoelen voor cloud
type: Tutorial
description: Instructies voor het maken van verbinding met de opslaglocaties van uw cloud
seo-description: Instructies voor het maken van verbinding met de opslaglocaties van uw cloud
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---


# Workflow voor het maken van cloudopslagdoelen

## Overzicht

Op deze pagina wordt uitgelegd hoe u verbinding kunt maken met cloudopslaglocaties in Real-time Customer Data Platform.

1. Selecteer in **[!UICONTROL Verbindingen]** > **[!UICONTROL Doelen]** uw voorkeursbestemming voor cloudopslag en selecteer vervolgens **[!UICONTROL Configureren]**.

   ![Verbinding maken met bestemming voor cloudopslag](./assets/connect-cloud-destination.png)

   >[!NOTE]
   >
   >Als er al een verbinding met dit doel bestaat, ziet u een knop **[!UICONTROL Activeren]** op de doelkaart. Voor meer informatie over het verschil tussen **[!UICONTROL Activate]** en **[!UICONTROL Configure]**, verwijs naar de sectie van de [Catalogus](/help/rtcdp/destinations/destinations-workspace.md#catalog) van de documentatie van de bestemmingswerkruimte.

2. Als u in de stap **[!UICONTROL Verificatie]** eerder een verbinding met uw bestemming voor cloudopslag had ingesteld, selecteert u **[!UICONTROL Bestaande account]** en selecteert u de bestaande verbinding. U kunt ook **[!UICONTROL Nieuwe account]** selecteren om een nieuwe verbinding met de bestemming voor cloudopslag in te stellen. Vul de verificatiereferenties van uw account in en selecteer **[!UICONTROL Verbinding maken met doel]**. U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Merk op dat deze openbare sleutel **als Base64 gecodeerde koord moet** worden geschreven. <br> Zie [bestemming Amazon S3](/help/rtcdp/destinations/amazon-s3-destination.md) , [[!DNL Amazon Kinesis]](/help/rtcdp/destinations/amazon-kinesis-destination.md) bestemming, [[!DNL Azure Event Hubs]](/help/rtcdp/destinations/azure-event-hubs-destination.md) bestemming, en bestemming [SFTP](/help/rtcdp/destinations/sftp-destination.md) voor details rond geloofsbrieven input in de stap van de **Authentificatie** .

   >[!NOTE]
   >
   >Adobe CDP in real time steunt geloofsbevestiging in het authentificatieproces en toont een foutenmelding als u onjuiste geloofsbrieven aan uw plaats van de wolkenopslag invoert. Dit zorgt ervoor dat u de werkstroom niet met onjuiste geloofsbrieven voltooit.

   ![Verbinding maken met bestemming voor cloudopslag - verificatiestap](./assets/csdw/destination-account.png)

3. Voer in de stap **[!UICONTROL Setup]** een **[!UICONTROL naam]** en een **[!UICONTROL beschrijving]** in voor de activeringsstroom. <br>
Ook in deze stap kunt u elke **[!UICONTROL Gebruikszaak]** voor marketingdoeleinden selecteren die op deze bestemming moet worden toegepast. Gebruiksgevallen voor marketingdoeleinden geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door de Adobe gedefinieerde gebruiksgevallen voor marketingdoeleinden of u kunt uw eigen gebruiksscenario voor marketingdoeleinden maken. Voor meer informatie over het op de markt brengen van gebruiksgevallen, zie de [Governance van Gegevens in Echte tijd CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) pagina. Voor informatie over de individuele Adobe-bepaalde het in de handel brengen gebruiksgevallen, zie het overzicht [van het het gebruiksbeleid van](/help/data-governance/policies/overview.md#core-actions)Gegevens. <br>
Voor Amazon S3-doelen voegt u de naam **[!UICONTROL van het]** emmertje en het **[!UICONTROL mappad]** in de opslaglocatie van de cloud in waar de bestanden worden geleverd. Selecteer Doel **** maken nadat u de bovenstaande velden hebt ingevuld.

   ![Verbinding maken met Amazon S3-bestemming voor cloudopslag - stap voor verificatie](./assets/amazon-s3-setup-step.png)

   Voeg voor SFTP-doelen het **[!UICONTROL mappad]** in waarin de bestanden worden geleverd. Selecteer Doel **** maken nadat u de bovenstaande velden hebt ingevuld.

   ![Verbinding maken met SFTP-cloudopslagbestemming - verificatiestap](./assets/sftp-destinations-setup-step.png)

   Geef voor [!DNL Amazon Kinesis] doelen de naam van uw bestaande gegevensstroom op in uw [!DNL Amazon Kinesis] account. Adobe In real time CDP zal gegevens naar deze stroom uitvoeren. Selecteer Doel **** maken nadat u de bovenstaande velden hebt ingevuld.

   ![Verbinding maken met Kinesis-bestemming voor cloudopslag - stap voor verificatie](./assets/kinesis-destinations-setup-step.png)

   Geef voor [!DNL Azure Event Hubs] doelen de naam van uw bestaande gegevensstroom op in uw [!DNL Amazon Kinesis] account. Adobe In real time CDP zal gegevens naar deze stroom uitvoeren. Selecteer Doel **** maken nadat u de bovenstaande velden hebt ingevuld.

   ![Verbinding maken met Kinesis-bestemming voor cloudopslag - stap voor verificatie](./assets/eventhubs-destinations-setup-step.png)

4. Uw doel is nu gemaakt. U kunt **[!UICONTROL Opslaan en afsluiten]** selecteren als u segmenten later wilt activeren of u kunt **[!UICONTROL Volgende]** selecteren om de workflow voort te zetten en segmenten te selecteren om te activeren. In beide gevallen raadpleegt u de volgende sectie Segmenten [](#activate-segments)activeren voor de rest van de workflow om gegevens te exporteren.

## Segmenten activeren {#activate-segments}

Zie Profielen en segmenten [activeren naar een doel](/help/rtcdp/destinations/activate-destinations.md) voor informatie over de workflow voor segmentactivering.
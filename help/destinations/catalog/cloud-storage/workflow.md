---
keywords: cloudopslag;cloudopslag
title: Een bestemming voor cloudopslag maken
type: Tutorial
description: Instructies voor het maken van verbinding met de opslaglocaties van uw cloud
seo-description: Instructies voor het maken van verbinding met de opslaglocaties van uw cloud
translation-type: tm+mt
source-git-commit: 6e7ecfdc0b2cbf6f07e6b2220ec163289511375e
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---


# Een bestemming voor cloudopslag maken

Op deze pagina wordt uitgelegd hoe u verbinding kunt maken met cloudopslaglocaties in Adobe Experience Platform.

Selecteer in **[!UICONTROL Verbindingen]** > **[!UICONTROL Doelen]** de gewenste bestemming voor cloudopslag en selecteer **[!UICONTROL Configureren]**.

![Verbinding maken met bestemming voor cloudopslag](../../assets/catalog/cloud-storage/workflow/connect.png)

>[!NOTE]
>
>Als er al een verbinding met dit doel bestaat, kunt u een **[!UICONTROL knop Activeer]** op de doelkaart zien. Voor meer informatie over het verschil tussen **[!UICONTROL Activate]** en **[!UICONTROL Configure]**, verwijs naar [Catalog](../../ui/destinations-workspace.md#catalog) sectie van de documentatie van de bestemmingswerkruimte.

Selecteer **[!UICONTROL Bestaande account]** in de stap **[!UICONTROL Verificatie]** als u eerder een verbinding met de opslagbestemming van de cloud had ingesteld. Selecteer vervolgens uw bestaande verbinding. Of u kunt **[!UICONTROL New Account]** selecteren om een nieuwe verbinding met uw bestemming voor cloudopslag in te stellen. Vul de verificatiereferenties van uw account in en selecteer **[!UICONTROL Verbinding maken met doel]**. U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Merk op dat deze openbare sleutel **must** als Base64 wordt geschreven gecodeerd koord.

Zie [Amazon S3](./amazon-s3.md) bestemming, [[!DNL Amazon Kinesis]](./amazon-kinesis.md) bestemming, [[!DNL Azure Event Hubs]](./azure-event-hubs.md) bestemming, en [SFTP](./sftp.md) bestemming voor details rond geloofsbrieven input in **Authentificatie** stap.

>[!NOTE]
>
>Platform ondersteunt validatie van referenties tijdens het verificatieproces en geeft een foutbericht weer als u onjuiste gegevens hebt ingevoerd op de locatie van uw cloudopslag. Dit zorgt ervoor dat u de werkstroom niet met onjuiste geloofsbrieven voltooit.

![Verbinding maken met bestemming voor cloudopslag - verificatiestap](../../assets/catalog/cloud-storage/workflow/destination-account.png)

Voer in de stap **[!UICONTROL Setup]** een **[!UICONTROL Naam]** en een **[!UICONTROL Beschrijving]** voor uw activeringsstroom in.

Ook in deze stap, kunt u om het even welke **[!UICONTROL Handeling van de Marketing]** selecteren die op deze bestemming zou moeten van toepassing zijn. Marketingsacties geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door Adobe gedefinieerde marketingacties of u kunt uw eigen marketingactie maken. Voor meer informatie over marketing acties, zie [Overzicht van het beleid van het gebruik van Gegevens](../../../data-governance/policies/overview.md).

Voor Amazon S3-doelen voegt u de **[!UICONTROL Naam emmertje]** en het **[!UICONTROL Mappad]** in in de bestemming voor cloudopslag waar de bestanden worden geleverd. Selecteer **[!UICONTROL Doel maken]** nadat u de bovenstaande velden hebt ingevuld.

![Verbinding maken met Amazon S3-bestemming voor cloudopslag - stap voor verificatie](../../assets/catalog/cloud-storage/workflow/amazon-s3-setup.png)

Voor bestemmingen SFTP, neem **[!UICONTROL de weg van de Omslag]** op waar de dossiers zullen worden geleverd. Selecteer **[!UICONTROL Doel maken]** nadat u de bovenstaande velden hebt ingevuld.

![Verbinding maken met SFTP-cloudopslagbestemming - verificatiestap](../../assets/catalog/cloud-storage/workflow/sftp-setup.png)

Geef voor [!DNL Amazon Kinesis]-doelen de naam van uw bestaande gegevensstroom op in uw [!DNL Amazon Kinesis]-account. Platform exporteert gegevens naar deze stream. Selecteer **[!UICONTROL Doel maken]** nadat u de bovenstaande velden hebt ingevuld.

![Verbinding maken met Kinesis-bestemming voor cloudopslag - stap voor verificatie](../../assets/catalog/cloud-storage/workflow/kinesis-setup.png)

Geef voor [!DNL Azure Event Hubs]-doelen de naam van uw bestaande gegevensstroom op in uw [!DNL Amazon Event Hubs]-account. Platform exporteert gegevens naar deze stream. Selecteer **[!UICONTROL Doel maken]** nadat u de bovenstaande velden hebt ingevuld.

![Verbinden met de bestemming van de cloudopslag van de Hubs van de Gebeurtenis - authentificatiestap](../../assets/catalog/cloud-storage/workflow/event-hubs-setup.png)

Uw doel is nu gemaakt. U kunt **[!UICONTROL Opslaan en afsluiten]** selecteren als u segmenten later wilt activeren of u kunt **[!UICONTROL Volgende]** selecteren om door te gaan met de workflow en segmenten te selecteren om te activeren. In beide gevallen raadpleegt u de volgende sectie [Segmenten activeren](#activate-segments) voor de rest van de workflow om gegevens te exporteren.

## Segmenten {#activate-segments} activeren

Zie [Profielen en segmenten activeren naar een doel](../../ui/activate-destinations.md) voor informatie over de workflow voor segmentactivering.
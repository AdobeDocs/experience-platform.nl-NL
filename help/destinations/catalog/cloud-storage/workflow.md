---
keywords: cloudopslag;cloudopslag
title: Een bestemming voor cloudopslag maken
type: Tutorial
description: Instructies voor het maken van verbinding met de opslaglocaties van uw cloud
seo-description: Instructies voor het maken van verbinding met de opslaglocaties van uw cloud
translation-type: tm+mt
source-git-commit: 02754055e2be8a45a0699386cb559dad8f25717c
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---


# Een bestemming voor cloudopslag maken

## Overzicht {#overview}

Op deze pagina wordt uitgelegd hoe u verbinding kunt maken met cloudopslaglocaties in Adobe Experience Platform.

Selecteer in **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** de voorkeursbestemming voor cloudopslag en selecteer **[!UICONTROL Configure]**.

![Verbinding maken met bestemming voor cloudopslag](../../assets/catalog/cloud-storage/workflow/connect.png)

>[!NOTE]
>
>Als er al een verbinding met dit doel bestaat, kunt u een **[!UICONTROL Activate]** knop op de doelkaart zien. Raadpleeg voor meer informatie over het verschil tussen **[!UICONTROL Activate]** en **[!UICONTROL Configure]** de sectie [Catalog](../../ui/destinations-workspace.md#catalog) van de documentatie van de doelwerkruimte.

## Verificatiestap {#authentication}

Als u in de stap **[!UICONTROL Authentication]** eerder een verbinding met uw bestemming voor cloudopslag had ingesteld, selecteert u **[!UICONTROL Existing Account]** en selecteert u de bestaande verbinding. U kunt ook **[!UICONTROL New Account]** selecteren om een nieuwe verbinding met uw bestemming voor cloudopslag in te stellen. Vul de verificatiereferenties van uw account in en selecteer **[!UICONTROL Connect to destination]**. U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Uw openbare sleutel moet als [!DNL Base64] gecodeerde koord worden geschreven.

Zie [Amazon S3](./amazon-s3.md) bestemming, [[!DNL Amazon Kinesis]](./amazon-kinesis.md) bestemming, [[!DNL Azure Event Hubs]](./azure-event-hubs.md) bestemming, en [SFTP](./sftp.md) bestemming voor details rond geloofsbrieven input in **Authentificatie** stap.

>[!NOTE]
>
>Platform ondersteunt validatie van referenties tijdens het verificatieproces en geeft een foutbericht weer als u onjuiste gegevens hebt ingevoerd op de locatie van uw cloudopslag. Dit zorgt ervoor dat u de werkstroom niet met onjuiste geloofsbrieven voltooit.

![Verbinding maken met bestemming voor cloudopslag - verificatiestap](../../assets/catalog/cloud-storage/workflow/destination-account.png)

## Stap {#setup} instellen

Voer in de stap **[!UICONTROL Setup]** een **[!UICONTROL Name]** en een **[!UICONTROL Description]** in voor de activeringsstroom.

Bij deze stap kunt u ook elke **[!UICONTROL Marketing action]** selecteren die op dit doel moet worden toegepast. Marketingsacties geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door Adobe gedefinieerde marketingacties of u kunt uw eigen marketingactie maken. Voor meer informatie over marketing acties, zie [Overzicht van het beleid van het gebruik van Gegevens](../../../data-governance/policies/overview.md).

Voor Amazon S3-doelen voegt u **[!UICONTROL Bucket name]** en **[!UICONTROL Folder path]** in de opslaglocatie van de cloud in waar de bestanden worden geleverd. Selecteer **[!UICONTROL Create Destination]** nadat u de bovenstaande velden hebt ingevuld.

![Verbinding maken met Amazon S3-bestemming voor cloudopslag - stap voor verificatie](../../assets/catalog/cloud-storage/workflow/amazon-s3-setup.png)

Voor bestemmingen SFTP, neem **[!UICONTROL Folder path]** op waar de dossiers zullen worden geleverd. Selecteer **[!UICONTROL Create Destination]** nadat u de bovenstaande velden hebt ingevuld.

![Verbinding maken met SFTP-cloudopslagbestemming - verificatiestap](../../assets/catalog/cloud-storage/workflow/sftp-setup.png)

Geef voor [!DNL Amazon Kinesis]-doelen de naam van uw bestaande gegevensstroom op in uw [!DNL Amazon Kinesis]-account. Platform exporteert gegevens naar deze stream. Selecteer **[!UICONTROL Create Destination]** nadat u de bovenstaande velden hebt ingevuld.

![Verbinding maken met Kinesis-bestemming voor cloudopslag - stap voor verificatie](../../assets/catalog/cloud-storage/workflow/kinesis-setup.png)

Geef voor [!DNL Azure Event Hubs]-doelen de naam van uw bestaande gegevensstroom op in uw [!DNL Amazon Event Hubs]-account. Platform exporteert gegevens naar deze stream. Selecteer **[!UICONTROL Create Destination]** nadat u de bovenstaande velden hebt ingevuld.

![Verbinden met de bestemming van de cloudopslag van de Hubs van de Gebeurtenis - authentificatiestap](../../assets/catalog/cloud-storage/workflow/event-hubs-setup.png)

Uw doel is nu gemaakt. U kunt **[!UICONTROL Save & Exit]** selecteren als u segmenten later wilt activeren of u kunt **[!UICONTROL Next]** selecteren om de workflow voort te zetten en segmenten te selecteren om te activeren. In beide gevallen raadpleegt u de volgende sectie [Segmenten activeren](#activate-segments) voor de rest van de workflow om gegevens te exporteren.

## Segmenten {#activate-segments} activeren

Zie [Profielen en segmenten activeren naar een doel](../../ui/activate-destinations.md) voor informatie over de workflow voor segmentactivering.
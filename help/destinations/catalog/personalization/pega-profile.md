---
title: Pega Profile Connector
description: Gebruik de Pega Profile Connector voor Amazon S3 in Adobe Experience Platform om profielgegevens volledig of incrementeel of beide te exporteren naar de Amazon S3-cloudopslag. In de Hub van het Beslissingsbesluit van de Klant van Pega, kunnen de gegevensbanen in de Ontwerper van het Profiel van de Klant worden gepland om profielgegevens van de opslag van Amazon S3 periodiek in te voeren.
last-substantial-update: 2023-01-25T00:00:00Z
source-git-commit: 83778bc5d643f69e0393c0a7767fef8a4e8f66e9
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 0%

---


# Pega Profile Connector

## Overzicht {#overview}

Gebruik de [!DNL Pega Profile Connector] in Adobe Experience Platform om een live uitgaande verbinding met uw [!DNL Amazon Web Services] (AWS) S3-opslag om profielgegevens periodiek naar CSV-bestanden vanuit Adobe Experience Platform naar uw eigen S3-emmers te exporteren. In [!DNL Pega Customer Decision Hub], kunt u gegevenstaken plannen om deze profielgegevens uit S3-opslag te importeren om de [!DNL Pega Customer Decision Hub] profiel.

Deze aansluiting helpt bij het instellen van de eerste export van profielgegevens en helpt bij het regelmatig synchroniseren van nieuwe profielen naar [!DNL Pega Customer Decision Hub].  Het hebben van bijgewerkte gegevens in de Hub van het Besluit van de Klant verstrekt een betere en bijgewerkte mening van uw klantenbasis voor volgende-best-actie beslissing.

>[!IMPORTANT]
>
>Deze documentatiepagina is gemaakt door Pegasystems. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen met Pega [hier](mailto:support@pega.com).

## Gebruiksscenario’s

Om u te helpen beter begrijpen hoe en wanneer u het [!DNL Pega Profile Connector] doel, hier zijn de gevallen van het steekproefgebruik die de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

### Hoofdlettergebruik 1

Een markeerteken wil aanvankelijk instellen [!DNL Pega Customer Decision Hub] met profielgegevens die vanuit Adobe Experience Platform zijn geladen. Dit is een eerste volledige lading, gevolgd door deltabelastingen op geplande basis.

### Hoofdlettergebruik 2

Een markering wil bijgewerkte profielgegevens van Adobe Experience Platform beschikbaar in [!DNL Pega Customer Decision Hub] dat de Pega-inzichten met betrekking tot klantprofielen voortdurend verbetert.

## Vereisten {#prerequisites}

Voordat u deze bestemming kunt gebruiken om gegevens uit Adobe Experience Platform te exporteren en profielen te importeren naar [!DNL Pega Customer Decision Hub], zorg ervoor u de volgende eerste vereisten voltooit:

* Configureren [!DNL Amazon S3] emmertje en het omslagpad dat moet worden gebruikt voor het exporteren en importeren van gegevensbestanden.
* Configureer de [!DNL Amazon S3] toegangssleutel en [!DNL Amazon S3] geheime sleutel: In [!DNL Amazon S3], een `access key - secret access key` paar om Platform toegang tot uw te verlenen [!DNL Amazon S3] account.
* Om gegevens met succes te verbinden en uit te voeren aan uw [!DNL Amazon S3] opslaglocatie, een gebruiker voor Identiteit en Toegangsbeheer (IAM) maken voor [!DNL Platform] in [!DNL Amazon S3] en wijs toestemmingen zoals toe `s3:DeleteObject`, `s3:GetBucketLocation`, `s3:GetObject`, `s3:ListBucket`, `s3:PutObject`, `s3:ListMultipartUploadParts`
* Zorg ervoor dat u [!DNL Pega Customer Decision Hub] -instantie wordt bijgewerkt naar versie 8.8 of hoger.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Pega Customer Decision Hub] biedt ondersteuning voor de activering van aangepaste gebruikers-id&#39;s die in de onderstaande tabel worden beschreven. Zie voor meer informatie [identiteiten](/help/identity-service/namespaces.md).

| Doelidentiteit | Beschrijving |
|---|---|
| *CustomerID* | Algemene gebruikersnaam die een profiel op unieke wijze identificeert in [!DNL Pega Customer Decision Hub] en Adobe Experience Platform |

{style=&quot;table-layout:auto&quot;}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals gekozen in het scherm met de kenmerken van het geselecteerde profiel [doelactiveringsworkflow](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Uitvoerfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Meer informatie over [batchbestandsgebaseerde doelen](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). Vul in de workflow voor doelconfiguratie de velden in die in de twee onderstaande secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u zich wilt verifiëren bij de bestemming, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]**.

* **[!DNL Amazon S3]toegangstoets** en **[!DNL Amazon S3]geheime sleutel**: In [!DNL Amazon S3], een `access key - secret access key` paar om Adobe Experience Platform toegang te geven tot je [!DNL Amazon S3] account. Meer informatie in het dialoogvenster [Amazon Web Services-documentatie](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### Doelgegevens invullen {#destination-details}

Na het vestigen van de authentificatieverbinding aan [!DNL Amazon S3], verstrekt de volgende informatie voor de bestemming:

![Afbeelding van het UI-scherm met de voltooide velden voor de doelgegevens van de Pega Profile Connector](../../assets/catalog/personalization/pega-profile/pega-profile-connect-destination.png)

Om details voor de bestemming te vormen, vul de vereiste gebieden in en selecteer **[!UICONTROL Next]**. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Voer een naam in die u helpt deze bestemming te identificeren.
* **[!UICONTROL Description]**: Voer een beschrijving van deze bestemming in.
* **[!UICONTROL Bucket name]**: Voer de naam in van de [!DNL Amazon S3] emmer die door deze bestemming moet worden gebruikt.
* **[!UICONTROL Folder path]**: Voer het pad in naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen.
* **[!UICONTROL Compression Type]**: Selecteer het compressietype GZIP of NONE.

>[!TIP]
>
>In de Connect-doelworkflow kunt u per geëxporteerd segmentbestand een aangepaste map in uw Amazon S3-opslagruimte maken. Lezen [Macro&#39;s gebruiken om een map te maken op uw opslaglocatie](/help/destinations/catalog/cloud-storage/overview.md#use-macros) voor instructies.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over waarschuwingen raadpleegt u de handleiding over [het abonneren aan bestemmingen alarm gebruikend UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Zie [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](../../ui/activate-batch-profile-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

### Kenmerken en identiteiten toewijzen {#map}

In de **[!UICONTROL Mapping]** U kunt kiezen welke kenmerken en identiteitsvelden u wilt exporteren voor uw profielen. U kunt ook selecteren om de kopteksten in het geëxporteerde bestand te wijzigen in een gewenste vriendelijke naam. Voor meer informatie bekijkt u de [toewijzingsstap](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) in activeer partijbestemmingen UI zelfstudie.

## Gegevens exporteren valideren {#exported-data}

Voor [!DNL Pega Profile Connector] bestemmingen, [!DNL Platform] maakt een `.csv` bestand in de opslaglocatie van Amazon S3 die u hebt opgegeven. Voor meer informatie over de bestanden raadpleegt u [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](../../ui/activate-batch-profile-destinations.md) in de zelfstudie voor segmentactivering.

Wanneer de import van profielgegevens uit S3 is gelukt, worden gegevens ingevoegd in de [!DNL Pega Customer] profieldatastore. De geïmporteerde klantprofielgegevens kunnen worden gevalideerd in [!DNL Pega Customer Profile Designer] , zoals weergegeven in de volgende afbeelding.
![Afbeelding van het UI-scherm waar u gegevens van het Adobe-profiel kunt valideren in Customer Profile Designer](../../assets/catalog/personalization/pega-profile/pega-profile-data.png)

In [!DNL Pega Customer Decision Hub], gegevensbeheerders kunnen gegevenstaken configureren in [!DNL Customer Profile Designer] om profielgegevens periodiek van S3 zoals aangetoond in het volgende cijfer in te voeren. Zie de [extra middelen](#additional-resources) voor meer informatie over hoe u gegevenstaken kunt configureren om profielgegevens te importeren van [!DNL Amazon S3].
![Image of the UI screen to configure data jobs in Customer Profile Designer](../../assets/catalog/personalization/pega-profile/pega-profile-screen-image1.png)

## Aanvullende bronnen {#additional-resources}

Zie [Gegevenstaken importeren](https://academy.pega.com/topic/import-data-jobs/v1) in [!DNL Pega Customer Decision Hub].

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] handhaaft gegevensbeheer, zie [Overzicht van gegevensbeheer](/help/data-governance/home.md).




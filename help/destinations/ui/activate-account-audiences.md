---
title: Accountpubliek naar doelen activeren
type: Tutorial
description: Leer hoe u het publiek van een account activeert voor doelen
badgeLimitedAvailability: label="Beperkte beschikbaarheid" type="Caution"
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
source-git-commit: 77ba3bd55c2f2ac217612880b83b731919aa14af
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 0%

---

# Accountsoorten activeren

>[!AVAILABILITY]
>
>De functionaliteit om accountpubliek naar doelen te activeren is alleen beschikbaar in het dialoogvenster [B2B Edition van Real-time Customer Data Platform](../../rtcdp/b2b-overview.md). Bovendien is de functionaliteit voor het accountpubliek momenteel in **beperkte beschikbaarheid**. Neem contact op met de klantenservice van de Adobe of uw Adobe om toegang tot deze functie te vragen.

In dit artikel wordt uitgelegd welke workflow nodig is om te exporteren [accountpubliek](/help/segmentation/ui/account-audiences.md) van Adobe Experience Platform naar uw voorkeursbestemming.

## Ondersteunde doelen {#supported-destinations}

Ga naar **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** en selecteert u de **[!UICONTROL Catalog]** tab. Gebruik de **[!UICONTROL Data types]** filter en selecteer **[!UICONTROL Accounts]** de bestemmingen te zien die de activering van het accountantspubliek ondersteunen. Momenteel is het exporteren van accountsoorten alleen beschikbaar voor bepaalde cloudopslagdoelen ([Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [ADLS Gen 2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [Azure Blob Storage](/help/destinations/catalog/cloud-storage/azure-blob.md), [Gegevenslandingszone](/help/destinations/catalog/cloud-storage/data-landing-zone.md), en [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)) en de [(Bedrijven) LinkedIn Gelijktijdig publiek](/help/destinations/catalog/social/linkedin.md) bestemming.

![Doelen die het publiek van de rekening steunen.](/help/destinations/assets/ui/activate-account-audiences/data-types-filter.png)

## Vereisten {#prerequisites}

* U moet eerst innemen [accountprofielen](/help/rtcdp/accounts/account-profile-overview.md) en maken [accountpubliek](/help/segmentation/ui/account-audiences.md) voordat u ze kunt activeren naar downstreamdoelen.
* Als u het publiek van een account naar bestemmingen wilt activeren, moet u verbinding hebben met een doel. Als u dat nog niet hebt gedaan, gaat u naar de [doelcatalogus](../catalog/overview.md), doorblader de gesteunde bestemmingen, en vorm de bestemming die u wilt gebruiken. De zelfstudie UI lezen op [verbinden met bestemmingen](./connect-destination.md) voor meer informatie .

### Vereiste machtigingen {#permissions}

Als u het publiek van een account wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Blader in de doelcatalogus om ervoor te zorgen dat u over de benodigde machtigingen beschikt om het accountpubliek te activeren. Als een doel een **[!UICONTROL Activate]** controle, dan hebt u de aangewezen toestemmingen.

## Kies uw bestemming {#select-destination}

Volg de instructies om een bestemming te selecteren waar u uw datasets kunt uitvoeren:

1. Ga naar **[!UICONTROL Connections > Destinations]** en selecteert u de **[!UICONTROL Catalog]** tab.

   ![Tabblad Doelcatalogus met besturingselement Catalogus gemarkeerd.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Selecteren **[!UICONTROL Activate]** op de kaart die aan de bestemming beantwoordt dat u datasets naar wilt uitvoeren.

>[!TIP]
>
>De bestemmingen die rekeningspubliek kunnen uitvoeren zijn vermeld met een pictogram in de hogere juiste hoek van de kaart, gelijkend op hieronder benadrukt doel, of u kunt de filter van het gegevenstype gebruiken om bestemmingen slechts te tonen die rekeningspubliek kunnen uitvoeren, zoals [hoger weergegeven op de pagina](#supported-destinations).

![Amazon S3 bestemmingspagina die gemarkeerde profielsoorten kan exporteren.](/help/destinations/assets/ui/activate-account-audiences/amazon-s3-icon-activate-account-audiences.png)

1. Selecteren **[!UICONTROL Data type Accounts]**, gevolgd door de doelverbinding waarnaar u datasets wilt exporteren, en vervolgens selecteren **[!UICONTROL Next]**.

>[!TIP]
> 
>Als u een nieuwe bestemming wilt instellen om het accountpubliek te activeren, selecteert u **[!UICONTROL Configure new destination]** om de [Verbinden met doel](/help/destinations/ui/connect-destination.md) werkschema en [accounts selecteren als gegevenstype](/help/destinations/ui/connect-destination.md#segment-activation-or-dataset-exports).

![Workflow voor doelactivering gemarkeerd met accountbesturingselement.](/help/destinations/assets/ui/activate-account-audiences/activate-account-audiences-highlighted.png)

1. Ga naar de volgende sectie tot [uw accountpubliek selecteren](#select-profile-audiences) voor uitvoer.

## Uw accountpubliek selecteren {#select-account-audiences}

Gebruik de selectievakjes links van de namen van accountpubliek om het publiek te selecteren dat u naar het doel wilt exporteren en selecteer vervolgens **[!UICONTROL Next]**. Let alleen op: *accountpubliek* worden weergegeven in deze weergave en er worden geen andere publiekstypen weergegeven.

![Workflow voor het exporteren van gegevenssets met de stap Soorten publiek selecteren waarin u kunt selecteren welk accountpubliek u wilt exporteren.](/help/destinations/assets/ui/activate-account-audiences/select-account-audiences.png)

## Planning en volgende stappen

Lees de zelfstudie over het activeren van gegevens naar bestandsbestemmingen voor de rest van de activeringsworkflow voor het exporteren van accountsoorten. Doorgaan vanaf het tabblad [exportstap voor doelgroep plannen](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling). Als u accountpubliek activeert voor de **[!UICONTROL (Companies) LinkedIn Matched Audiences]** doel, lees de zelfstudie over het activeren van streamingdoelen. Doorgaan vanaf het tabblad [toewijzingsstap](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping).

>[!NOTE]
>
>Houd er rekening mee dat in de planningsstap bij het exporteren van accountsoorten naar cloudopslagdoelen de workflow voor het activeren van het accountpubliek alleen de mogelijkheid biedt om te exporteren [volledige bestanden](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) en [incrementele bestanden](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) _volgens een dagelijks schema_. Uuruitvoer wordt niet ondersteund. Let ook op: **[!UICONTROL After audience evaluation]** is het enige gesteunde evaluatietype.

## Belangrijke callouts en bekende beperkingen {#important-callouts-known-limitations}

Let op de volgende belangrijke callouts en bekende beperkingen voor de beperkte beschikbaarheidsversie van de functionaliteit om accountpubliek te activeren.

### Vereiste toewijzingsparen in de toewijzingsstap bij het activeren van het accountpubliek voor de **[!UICONTROL (Companies) LinkedIn Matched Audiences]** doel {#required-mappings}

Bij het activeren van accountpubliek naar de **[!UICONTROL (Companies) LinkedIn Matched Audiences]** doel, merk op dat de volgende twee kaartparen verplicht zijn om gegevens met succes uit te voeren:

![Toewijzing van linkedIn-velden is vereist.](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| Bronveld | Doelveld |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` (selecteer dit veld in het dialoogvenster **[!UICONTROL Select Identity namespace]** weergave) |

### Handhaving van gegevensbeheer {#data-governance-enforcement}

[Goedkeuring van het beleid](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) wordt momenteel niet ondersteund bij het activeren van accountpubliek naar doelen. In de revisiestap van de activeringsworkflow kunt u een gegraveerd besturingselement zien voor **[!UICONTROL View applicable consent policies]**.

![De stap van het overzicht van de workflow voor het activeren van accountpubliek met de controle voor het afdwingen van toestemming is uitgeschakeld.](/help/destinations/assets/ui/activate-account-audiences/consent-checks-greyed-out.png)

Andere mechanismen voor gegevensbeheer in Real-Time CDP, zoals [beleidscontroles voor gegevensgebruik](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) en [attribuut-based toegangsbeheer](/help/destinations/home.md#attribute-based-access) worden ondersteund.
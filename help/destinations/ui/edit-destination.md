---
title: Doelen bewerken
type: Tutorial
description: Leer hoe u bestaande bestemmingsaccounts kunt bewerken en bijwerken in de gebruikersinterface van Adobe Experience Platform
badgeBeta: label="Beta" type="Informative"
exl-id: f3298836-668b-43fb-b4f3-85a650766f05
source-git-commit: 990fe9162c5b2970f269a5b0668916b7b6e61f44
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Doelen bewerken

Leer hoe u verschillende componenten van een bestaande doelverbinding kunt bewerken, zoals het bijwerken van verificatiereferenties, de exportlocatie en meer met de gebruikersinterface van Experience Platform.

>[!IMPORTANT]
>
>Deze functionaliteit is in bèta beschikbaar en alleen voor bepaalde klanten. Neem contact op met uw Adobe-vertegenwoordiger om toegang aan te vragen.

>[!NOTE]
>
> De bewerkingen die in deze zelfstudie worden beschreven, worden ook ondersteund via API-bewerkingen. Lees het leerprogramma op hoe te [ bestemmingen in API ](/help/destinations/api/edit-destination.md) voor meer informatie uitgeven.

Verschillende componenten van een bestaande doelverbinding bewerken:

1. Ga naar **[!UICONTROL Destinations]** > **[!UICONTROL Browse]**.
2. Selecteer het gewenste doel dat u wilt bewerken.
3. Selecteer de ellips (`...`) in de [!UICONTROL Name] kolom en gebruik ![ uitgeven bestemmingscontrole ](/help/images/icons/edit.png)**[!UICONTROL Edit destination]**controle om bestaande bestemmingsverbindingen uit te geven.
4. Bewerk de gewenste instellingen in het modale venster. Selecteer **[!UICONTROL Save]** wanneer gereed.

In het bewerkingsbestemmingsvenster, kunt u om het even welke montages bijwerken die u vormde toen u aanvankelijk met de bestemming verbond. Deze instellingen zijn anders op basis van het doelplatform dat u bijwerkt.

Afhankelijk van hoe de bestemming werd gevormd, zouden sommige gebieden read-only kunnen zijn en kunnen niet worden uitgegeven. Om de waarde van read-only gebieden te veranderen, moet u [ een nieuwe bestemmingsverbinding ](../ui/connect-destination.md) met de nieuwe gebiedswaarden tot stand brengen.

![ Schermafbeelding die een read-only gebied tonen.](../assets/ui/edit-destinations/read-only.png)

Hieronder zijn sommige voorbeelden van de montages die u voor [ Amazon S3 ](../catalog/cloud-storage/amazon-s3.md) kunt bijwerken, [ Azure de Hubs van de Gebeurtenis ](../catalog/cloud-storage/azure-event-hubs.md), en [ Google Adds ](../catalog/advertising/google-ads-destination.md) bestemmingen.

<div style="display: flex; gap: 12px; justify-content: flex-start; align-items: flex-start;">
  <img class="modal-image" src="../assets/ui/edit-destinations/edit-amazon-s3-connection.png" alt="Bewerk het doelscherm voor de Amazon S3-bestemming." style="max-width: 200px; height: auto; border: 1px solid #ccc;">
  <img class="modal-image" src="../assets/ui/edit-destinations/edit-eventhubs-connection.png" alt="Bewerk het doelscherm voor de Azure EventHubs-bestemming." style="max-width: 200px; height: auto; border: 1px solid #ccc;">
  <img class="modal-image" src="../assets/ui/edit-destinations/edit-google-ads-connection.png" alt="Doelscherm bewerken voor de bestemming Google Ads." style="max-width: 200px; height: auto; border: 1px solid #ccc;">
</div>

>[!SUCCESS]
>
>De instellingen voor de doelverbinding worden nu bijgewerkt.

## Andere bewerkingsopties

Met de Experience Platform UI of de Flow Service API kunt u verschillende doelconfiguraties bewerken, zoals in de onderstaande koppelingen wordt beschreven:

| De gebruikersinterface van Experience Platform gebruiken | De Flow Service API gebruiken |
|---------|----------|
| Doelverbindingen bewerken (deze pagina) | [ geef de componenten van de doelverbinding (opslagplaats en andere componenten) uit ](/help/destinations/api/edit-destination.md#patch-target-connection) |
| [ geeft rekeningen ](/help/destinations/ui/update-accounts.md) uit | [ geeft de componenten van de basisverbinding (authentificatieparameters en andere componenten) uit ](/help/destinations/api/edit-destination.md#patch-base-connection) |
| [ geef activeringsgegevens ](/help/destinations/ui/edit-activation.md) uit | [ de bestemmingsgegevens van de Update ](/help/destinations/api/update-destination-dataflows.md) |

## Volgende stappen

Aan de hand van deze zelfstudie hebt u de **[!UICONTROL destinations]** -werkruimte gebruikt om bestaande doelverbindingen bij te werken.

Voor meer informatie over bestemmingen, verwijs naar het [ overzicht van bestemmingen ](../catalog/overview.md).

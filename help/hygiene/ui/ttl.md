---
title: TTL's voor gegevenssets beheren
description: Leer hoe te om een tijd te plannen om (TTL) voor een dataset in Adobe Experience Platform UI te leven.
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: 22da9e39e168d9a995c7c134733aa7a1b3587749
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# Gegevensset-TTL&#39;s beheren

>[!IMPORTANT]
>
>De mogelijkheden voor gegevenshygiëne in Adobe Experience Platform zijn momenteel alleen beschikbaar voor organisaties die Adobe Shield voor gezondheidszorg hebben aangeschaft.

De [[!UICONTROL Data Hygiene] werkruimte](./overview.md) in Adobe Experience Platform UI staat u toe om een tijd te plannen om (TTL) voor een dataset te leven.

Dit document behandelt hoe te om dataset TTLs in de UI van het Platform te plannen en te beheren.

## Plan een TTL

Als u een nieuwe aanvraag wilt maken, selecteert u **[!UICONTROL Create request]** van de hoofdpagina in de werkruimte.

![Afbeelding die de [!UICONTROL Create request] knop die wordt geselecteerd](../images/ui/ttl/create-request-button.png)

<!-- The request creation dialog appears. Under the **[!UICONTROL Action]** section, select **[!UICONTROL Dataset]** to update the available controls for TTL scheduling-->

### Selecteer een datum en een dataset

Het dialoogvenster Aanvragen wordt geopend. Onder de **[!UICONTROL Action]** selecteert u een datum waarop de gegevensset moet worden verwijderd. U kunt de datum handmatig invoeren (in de notatie `mm/dd/yyyy`) of selecteer het kalenderpictogram (![Afbeelding van het kalenderpictogram](../images/ui/ttl/calendar-icon.png)) om de datum in een dialoogvenster te selecteren.

![Afbeelding met een vervaldatum die wordt ingesteld voor de TTL](../images/ui/ttl/select-date.png)

Volgende, onder **[!UICONTROL Dataset Details]**, selecteert u het databasepictogram (![Afbeelding van het databasepictogram](../images/ui/ttl/database-icon.png)) om een dialoogvenster voor de selectie van gegevenssets te openen. Kies een dataset van de lijst om TTL op toe te passen, dan selecteren **[!UICONTROL Done]**.

![Afbeelding met een gegevensset die wordt geselecteerd](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
>Alleen gegevenssets die tot de huidige sandbox behoren, worden weergegeven.

### De aanvraag verzenden

Zodra u een dataset en een datum van TTL hebt geselecteerd, selecteer **[!UICONTROL Submit]**.

![Afbeelding die de [!UICONTROL Submit] knop die wordt geselecteerd](../images/ui/ttl/submit.png)

U wordt gevraagd de datum te bevestigen dat de dataset door zal worden geschrapt. Selecteren **[!UICONTROL Submit]** om door te gaan.

Nadat het verzoek is verzonden, wordt een werkorder gemaakt en wordt deze weergegeven op het hoofdtabblad van het dialoogvenster [!UICONTROL Data Hygiene] werkruimte. Van hier, kunt u de status van de het werkorde controleren aangezien het het verzoek verwerkt.

## Een TTL bewerken of annuleren

Selecteer **[!UICONTROL Dataset]** op de hoofdpagina van de werkruimte en selecteer de TTL in de lijst.

Op de detailpagina van TTL, toont de juiste spoorstaaf controles om de geplande schrapping uit te geven of te annuleren.

## Volgende stappen

Dit document behandelde hoe te om dataset TTLs in de UI van het Experience Platform te plannen. Leren hoe te om datasetTTLs te plannen gebruikend de Hygiene API van Gegevens, verwijs naar [dataset TTL eindpuntgids](../api/ttl.md).

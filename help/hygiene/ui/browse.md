---
title: Bladeren in werkorders voor gegevenshygiëne
description: Leer hoe u bestaande werkorders voor gegevenshygiëne in de Adobe Experience Platform-gebruikersinterface kunt weergeven en beheren.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: 7f1e4bdf54314cab1f69619bcbb34216da94b17e
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Bladeren door werkorders voor gegevenshygiëne {#browse-work-orders}

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="Werkorder-id&#39;s"
>abstract="Wanneer een verzoek om gegevenshygiëne naar het systeem wordt verzonden, wordt een het werkorde gecreeerd om de gevraagde taak uit te voeren. Met andere woorden, een werkorder is een specifiek proces voor gegevenshygiëne, dat de huidige status en andere gerelateerde details omvat. Aan elke werkorder wordt automatisch een eigen unieke id toegewezen."
>text="See the data hygiene UI guide to learn more."

>[!IMPORTANT]
>
>De mogelijkheden voor gegevenshygiëne in Adobe Experience Platform zijn momenteel alleen beschikbaar voor organisaties die een gezondheidsschild hebben aangeschaft.

Wanneer een verzoek om gegevenshygiëne naar het systeem wordt verzonden, wordt een het werkorde gecreeerd om de gevraagde taak uit te voeren. Een werkorder vertegenwoordigt een specifiek proces van de gegevenshygiëne, zoals een geplande tijd te leven (TTL) voor een dataset, die zijn huidige status en andere verwante details omvat.

In deze handleiding wordt uitgelegd hoe u bestaande werkorders in de gebruikersinterface van Adobe Experience Platform kunt weergeven en beheren.

## Bestaande werkorders weergeven en filteren

Wanneer u voor het eerst toegang krijgt tot **[!UICONTROL Data Hygiene]** in de UI, wordt een lijst van bestaande het werkorden getoond samen met hun basisdetails.

![Afbeelding die de [!UICONTROL Data Hygiene] werkruimte in de gebruikersinterface van het Platform](../images/ui/browse/work-order-list.png)

<!-- The list only shows work orders for one category at a time. Select **[!UICONTROL Consumer]** to view a list of consumer deletion tasks, and **[!UICONTROL Dataset]** to view a list of time-to-live (TTL) schedules for datasets.

![Image showing the [!UICONTROL Dataset] tab](../images/ui/browse/dataset-tab.png) -->

Selecteer het trechter-pictogram (![Afbeelding van het trechter-pictogram](../images/ui/browse/funnel-icon.png)) om een lijst weer te geven met filters voor de weergegeven werkorders.

![Afbeelding van de weergegeven werkorderfilters](../images/ui/browse/filters.png)

| Filter | Beschrijving |
| --- | --- |
| [!UICONTROL Status] | Filter op basis van de huidige status van de werkorder. |
| [!UICONTROL Date created] | Filter op basis van de datum waarop het TTL-verzoek voor de gegevensset is ingediend. |
| [!UICONTROL Deletion date] | Filter dat op de schrappingsdatum wordt gebaseerd dat TTL gepland heeft. |
| [!UICONTROL Date updated] | Filter op basis van de datum waarop de dataset-TTL voor het laatst is bijgewerkt. De creaties en vervalsingen van TTL worden geteld als updates. |

{style=&quot;table-layout:auto&quot;}

## De details van een werkorder weergeven

Selecteer de id van een vermelde werkorder om de details ervan weer te geven.

![Afbeelding met een werkorder-id die is geselecteerd](../images/ui/browse/select-work-order.png)

<!-- Depending on the type of work order selected, different information and controls are provided. These are covered in the sections below.

### Consumer delete details

>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="Consumer delete response"
>abstract="When a consumer deletion process receives a response from the system, these messages are displayed under the **[!UICONTROL Result]** section. If a problem occurs while a work order is processing, any relevant error messages will appear in this section to help you troubleshoot the issue. To learn more, see the data hygiene UI guide."


The details of a consumer delete request are read-only, displaying its basic attributes such as its current status and the time elapsed since the request was made.

![Image showing the details page for a consumer delete work order](../images/ui/browse/consumer-delete-details.png)

### Dataset TTL details -->

De detailspagina voor een dataset TTL verstrekt informatie over zijn basisattributen, met inbegrip van de geplande vervaldatum op de dagen die resteren alvorens de schrapping voorkomt. In de juiste rail, kunt u controles gebruiken om TTL uit te geven of te annuleren.

![Afbeelding die de detailpagina voor een gegevensset-TTL-werkvolgorde weergeeft](../images/ui/browse/ttl-details.png)

## Volgende stappen

Deze handleiding besprak hoe u bestaande werkorders voor gegevenshygiëne in de gebruikersinterface van het Platform kunt weergeven en beheren. Zie de handleiding voor informatie over het maken van uw eigen werkorders [het plannen van een dataset TTL](./ttl.md).

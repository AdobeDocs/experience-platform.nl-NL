---
title: Bladeren in werkorders voor gegevenshygiëne
description: Leer hoe u bestaande werkorders voor gegevenshygiëne in de Adobe Experience Platform-gebruikersinterface kunt weergeven en beheren.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: f246a014de7869b627a677ac82e98d4556065010
workflow-type: tm+mt
source-wordcount: '0'
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

Wanneer een verzoek om gegevenshygiëne naar het systeem wordt verzonden, wordt een het werkorde gecreeerd om de gevraagde taak uit te voeren. Een werkorder vertegenwoordigt een specifiek proces van de gegevenshygiëne, zoals een geplande gegevenssetvervaldatum, die zijn huidige status en andere verwante details omvat.

In deze handleiding wordt uitgelegd hoe u bestaande werkorders in de gebruikersinterface van Adobe Experience Platform kunt weergeven en beheren.

## Bestaande werkorders weergeven en filteren

Wanneer u voor het eerst toegang krijgt tot **[!UICONTROL Data Hygiene]** in de UI, wordt een lijst van bestaande het werkorden getoond samen met hun basisdetails.

![Afbeelding die de [!UICONTROL Data Hygiene] werkruimte in de gebruikersinterface van het Platform](../images/ui/browse/work-order-list.png)

<!-- The list only shows work orders for one category at a time. Select **[!UICONTROL Consumer]** to view a list of consumer deletion tasks, and **[!UICONTROL Dataset]** to view a list of scheduled dataset expirations.

![Image showing the [!UICONTROL Dataset] tab](../images/ui/browse/dataset-tab.png) -->

Selecteer het trechter-pictogram (![Afbeelding van het trechter-pictogram](../images/ui/browse/funnel-icon.png)) om een lijst weer te geven met filters voor de weergegeven werkorders.

![Afbeelding van de weergegeven werkorderfilters](../images/ui/browse/filters.png)

| Filter | Beschrijving |
| --- | --- |
| [!UICONTROL Status] | Filter op basis van de huidige status van de werkorder:<ul><li>**[!UICONTROL Completed]**: De taak is voltooid.</li><li>**[!UICONTROL Pending]**: De taak is gemaakt, maar is nog niet uitgevoerd. A [Vervalaanvraag gegevensset](./dataset-expiration.md) neemt deze status aan vóór de geplande verwijderingsdatum. Zodra de verwijderingsdatum is bereikt, wordt de status bijgewerkt naar [!UICONTROL Executing] tenzij de taak vooraf wordt geannuleerd.</li><li>**[!UICONTROL Executing]**: Het verzoek van de datasetvervaldatum is begonnen en verwerkt momenteel.</li><li>**[!UICONTROL Cancelled]**: De taak is geannuleerd als onderdeel van een handmatig gebruikersverzoek.</li></ul> |
| [!UICONTROL Date created] | Filter op basis van de datum waarop de werkorder is gemaakt. |
| [!UICONTROL Expiration date] | Verzoeken voor de vervaldatum van de gegevensset voor filters op basis van de geplande verwijderingsdatum voor de gegevensset in kwestie. |
| [!UICONTROL Date updated] | Verzoeken van de de gegevenssetvervaldatum van de filter die op toen de het werkorde het laatst werd bijgewerkt worden gebaseerd. Ontwerpen en vervaldatums worden als updates geteld. |

{style=&quot;table-layout:auto&quot;}

## De details van een werkorder weergeven {#view-details}

>[!CONTEXTUALHELP]
>id="platform_hygiene_statusbyservice"
>title="Status per service"
>abstract="Verzoeken om gegevenshygiëne worden onafhankelijk door meerdere diensten van de Experience Platform verwerkt. Deze sectie schetst de huidige verwerkingsstatus van het verzoek voor elke respectieve dienst. Raadpleeg de gebruikershandleiding voor gegevenshygiëne voor meer informatie."

>[!CONTEXTUALHELP]
>id="platform_hygiene_numberofidentities"
>title="Aantal identiteiten"
>abstract="Het aantal identiteiten waarvoor is gevraagd dat ze in deze werkorder moeten worden verwijderd. De in de telling opgenomen identiteiten hoeven niet noodzakelijkerwijs in de betrokken gegevensbestanden te bestaan. Raadpleeg de gebruikershandleiding voor gegevenshygiëne voor meer informatie."

>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="Reactie verwijderen door consument"
>abstract="Wanneer een proces van de consumentenschrapping een reactie van het systeem ontvangt, worden deze berichten getoond onder **[!UICONTROL Result]** sectie. Als er een probleem optreedt terwijl een werkorder wordt verwerkt, worden in deze sectie foutberichten weergegeven die u helpen bij het oplossen van het probleem. Raadpleeg de gebruikershandleiding voor gegevenshygiëne voor meer informatie."

Selecteer de id van een vermelde werkorder om de details ervan weer te geven.

![Afbeelding met een werkorder-id die is geselecteerd](../images/ui/browse/select-work-order.png)

<!-- Depending on the type of work order selected, different information and controls are provided. These are covered in the sections below.

### Consumer delete details {#consumer-delete}

The details of a consumer delete request are read-only, displaying its basic attributes such as its current status and the time elapsed since the request was made.

![Image showing the details page for a consumer delete work order](../images/ui/browse/consumer-delete-details.png)

### Dataset expiration details {#dataset-expiration} -->

De detailspagina voor een datasetvervaldatum verstrekt informatie over zijn basisattributen, met inbegrip van de geplande vervaldatum op de dagen die resteren alvorens de schrapping voorkomt. In het rechterspoor kunt u besturingselementen gebruiken om de vervaldatum te bewerken of te annuleren.

![Afbeelding die de detailpagina voor een werkorder voor het verlopen van een gegevensset weergeeft](../images/ui/browse/ttl-details.png)

## Volgende stappen

Deze handleiding besprak hoe u bestaande werkorders voor gegevenshygiëne in de gebruikersinterface van het Platform kunt weergeven en beheren. Zie de handleiding voor informatie over het maken van uw eigen werkorders [het plannen van een datasetvervaldatum](./dataset-expiration.md).

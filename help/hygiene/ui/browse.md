---
title: Bladeren in werkorders voor gegevenshygiëne
description: Leer hoe u bestaande werkorders voor gegevenshygiëne in de Adobe Experience Platform-gebruikersinterface kunt weergeven en beheren.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: 18ef55a084ced8c26e583598f9016dd9f4741153
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---

# Bladeren door werkorders voor gegevenshygiëne

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="Werkorder-id&#39;s"
>abstract="Wanneer een verzoek om gegevenshygiëne naar het systeem wordt verzonden, wordt een het werkorde gecreeerd om de gevraagde taak uit te voeren. Met andere woorden, een werkorder is een specifiek proces voor gegevenshygiëne, dat de huidige status en andere gerelateerde details omvat. Aan elke werkorder wordt automatisch een eigen unieke id toegewezen. Raadpleeg de gebruikershandleiding voor gegevenshygiëne voor meer informatie."

>[!IMPORTANT]
>
>De mogelijkheden voor gegevenshygiëne in Adobe Experience Platform zijn momenteel alleen beschikbaar voor organisaties die Adobe Shield voor gezondheidszorg hebben aangeschaft.

Wanneer een verzoek om gegevenshygiëne naar het systeem wordt verzonden, wordt een het werkorde gecreeerd om de gevraagde taak uit te voeren. Een werkorder vertegenwoordigt een specifiek proces voor gegevenshygiëne (zoals het verwijderen van consumentengegevens), dat de huidige status en andere gerelateerde details omvat.

In deze handleiding wordt uitgelegd hoe u bestaande werkorders in de gebruikersinterface van Adobe Experience Platform kunt weergeven en beheren.

## Bestaande werkorders weergeven en filteren

Wanneer u voor het eerst toegang krijgt tot **[!UICONTROL Data Hygiene]** in de UI, wordt een lijst van bestaande het werkorden getoond samen met hun basisdetails.

![Afbeelding die de [!UICONTROL Data Hygiene] werkruimte in de gebruikersinterface van het Platform](../images/ui/browse/work-order-list.png)

In de lijst worden alleen de werkorders voor één categorie tegelijk weergegeven. Selecteren **[!UICONTROL Consumer]** een lijst te bekijken van verwijderingstaken voor consumenten, en **[!UICONTROL Dataset]** om een lijst van tijd-aan-levende (TTL) programma&#39;s voor datasets te bekijken.

![Afbeelding die de [!UICONTROL Dataset] tab](../images/ui/browse/dataset-tab.png)

Selecteer het trechter-pictogram (![Afbeelding van het trechter-pictogram](../images/ui/browse/funnel-icon.png)) om een lijst weer te geven met filters voor de weergegeven werkorders.

![Afbeelding van de weergegeven werkorderfilters](../images/ui/browse/filters.png)

Afhankelijk van het tabblad dat u bekijkt, zijn er verschillende filters beschikbaar:

| Filter | Categorie | Beschrijving |
| --- | --- | --- |
| [!UICONTROL Status] | [!UICONTROL Consumer] &amp; [!UICONTROL Dataset] | Filter op basis van de huidige status van de werkorder. |
| [!UICONTROL Date created] | [!UICONTROL Consumer] | Filter op basis van de datum waarop het verzoek tot verwijderen door de consument is gedaan. |
| [!UICONTROL Date created] | [!UICONTROL Dataset] | Filter op basis van de datum waarop het verzoek tot verwijderen door de consument is gedaan. |
| [!UICONTROL Deletion date] | [!UICONTROL Dataset] | Filter dat op de schrappingsdatum wordt gebaseerd dat TTL gepland heeft. |
| [!UICONTROL Date updated] | [!UICONTROL Dataset] | Filter op basis van de datum waarop de dataset-TTL voor het laatst is bijgewerkt. De creaties en vervalsingen van TTL worden geteld als updates. |

{style=&quot;table-layout:auto&quot;}

## De details van een werkorder weergeven

Selecteer de id van een vermelde werkorder om de details ervan weer te geven.

![Afbeelding met een werkorder-id die is geselecteerd](../images/ui/browse/select-work-order.png)

Afhankelijk van het type geselecteerde werkorder, worden verschillende informatie en controles verstrekt. Deze worden behandeld in de onderstaande secties.

### Details verwijderen van consumenten

<!-- (Not available for initial release)
>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="Consumer delete response"
>abstract="When a consumer deletion process receives a response from the system, these messages are displayed under the **[!UICONTROL Result]** section. If a problem occurs while a work order is processing, any relevant error messages will appear in this section to help you troubleshoot the issue. To learn more, see the data hygiene UI guide."
-->

De details van een verzoek tot verwijdering door een consument zijn alleen-lezen, waarbij de basiskenmerken van het verzoek, zoals de huidige status, en de tijd die is verstreken sinds het verzoek is ingediend, worden weergegeven.

![Afbeelding met de detailpagina van een werkorder voor verwijderen door consumenten](../images/ui/browse/consumer-delete-details.png)

### Gegevens van TTL-gegevensset

De detailspagina voor een dataset TTL verstrekt informatie over zijn basisattributen, met inbegrip van de geplande vervaldatum op de dagen die resteren alvorens de schrapping voorkomt. In de juiste rail, kunt u controles gebruiken om TTL uit te geven of te annuleren.

![Afbeelding die de detailpagina voor een gegevensset-TTL-werkvolgorde weergeeft](../images/ui/browse/ttl-details.png)

## Volgende stappen

Deze handleiding besprak hoe u bestaande werkorders voor gegevenshygiëne in de gebruikersinterface van het Platform kunt weergeven en beheren. Raadpleeg de volgende documentatie voor informatie over het maken van uw eigen werkorders:

* [Een consument verwijderen](./delete-consumer.md)
* [Plan een dataset TTL](./ttl.md)

---
title: Door werkorders voor de levenscyclus van gegevens bladeren
description: Leer hoe u bestaande werkorders voor de levenscyclus van gegevens kunt weergeven en beheren in de Adobe Experience Platform-gebruikersinterface.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: 566f1b6478cd0de0691cfb2301d5b86fbbfece52
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 0%

---

# Zoeken naar werkorders tijdens de gegevenslevenscyclus {#browse-work-orders}

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="Werkorder-id&#39;s"
>abstract="Wanneer een verzoek om de gegevenslevenscyclus naar het systeem wordt verzonden, wordt een werkorder gecreeerd om de gevraagde taak uit te voeren. Met andere woorden, een werkorder vertegenwoordigt een specifiek proces van de gegevenslevenscyclus, dat zijn huidige status en andere verwante details omvat. Aan elke werkorder wordt automatisch een eigen unieke id toegewezen."
>text="See the data lifecycle UI guide to learn more."

Wanneer een verzoek om de gegevenslevenscyclus naar het systeem wordt verzonden, wordt een werkorder gecreeerd om de gevraagde taak uit te voeren. Een werkorder vertegenwoordigt een specifiek proces van de gegevenslevenscyclus, zoals een geplande datasetvervaldatum, die zijn huidige status en andere verwante details omvat.

In deze handleiding wordt uitgelegd hoe u bestaande werkorders in de gebruikersinterface van Adobe Experience Platform kunt weergeven en beheren.

## Bestaande werkorders weergeven en filteren

Wanneer u voor het eerst toegang krijgt tot **[!UICONTROL Data Lifecycle]** in de UI, wordt een lijst van bestaande het werkorden getoond samen met hun basisdetails.

![Afbeelding die de [!UICONTROL Data Lifecycle] werkruimte in de gebruikersinterface van het platform](../images/ui/browse/work-order-list.png)

In de lijst worden alleen de werkorders voor één categorie tegelijk weergegeven. Selecteren **[!UICONTROL Consumer]** een lijst met taken voor het verwijderen van records weergeven, en **[!UICONTROL Dataset]** om een lijst van geplande datasettermijnen te bekijken.

![Afbeelding die de [!UICONTROL Dataset] tab](../images/ui/browse/dataset-tab.png)

Selecteer het trechter-pictogram (![Afbeelding van het trechter-pictogram](../images/ui/browse/funnel-icon.png)) om een lijst weer te geven met filters voor de weergegeven werkorders.

![Afbeelding van de weergegeven werkorderfilters](../images/ui/browse/filters.png)

Afhankelijk van het type werkorder dat u bekijkt, zijn verschillende filteropties beschikbaar.

### Filters voor het verwijderen van records

De volgende filters zijn van toepassing op recordverwijderingsverzoeken:

| Filter | Beschrijving |
| --- | --- |
| [!UICONTROL Status] | Filter op basis van de huidige status van de werkorder:<ul><li>**[!UICONTROL Completed]**: De taak is voltooid.</li><li>**[!UICONTROL Failed]**: De taak heeft een fout aangetroffen en kan niet worden voltooid.</li><li>**[!UICONTROL Processing]**: Het verzoek is gestart en wordt momenteel verwerkt.</li></ul> |
| [!UICONTROL Date created] | Filter op basis van de datum waarop de werkorder is gemaakt. |
| [!UICONTROL Date updated] | Filter op basis van de datum waarop de werkorder voor het laatst is bijgewerkt. Creaties worden geteld als updates. |

### Filters voor gegevenssetverlopen

De volgende filters zijn van toepassing op verzoeken om gegevenssetvervaldatum:

| Filter | Beschrijving |
| --- | --- |
| [!UICONTROL Status] | Filter op basis van de huidige status van de werkorder:<ul><li>**[!UICONTROL Completed]**: De taak is voltooid.</li><li>**[!UICONTROL Pending]**: De taak is gemaakt, maar is nog niet uitgevoerd. A [Vervalaanvraag gegevensset](./dataset-expiration.md) neemt deze status aan vóór de geplande verwijderingsdatum. Zodra de verwijderingsdatum is bereikt, wordt de status bijgewerkt naar [!UICONTROL Executing] tenzij de taak vooraf wordt geannuleerd.</li><li>**[!UICONTROL Executing]**: Het verzoek om de gegevensset te vervalsen is gestart en wordt momenteel verwerkt.</li><li>**[!UICONTROL Cancelled]**: De taak is geannuleerd als onderdeel van een handmatig gebruikersverzoek.</li></ul> |
| [!UICONTROL Date created] | Filter op basis van de datum waarop de werkorder is gemaakt. |
| [!UICONTROL Expiration date] | Verzoeken voor de vervaldatum van de gegevensset voor filters op basis van de geplande verwijderingsdatum voor de gegevensset in kwestie. |
| [!UICONTROL Date updated] | Filter op basis van de datum waarop de werkorder voor het laatst is bijgewerkt. Ontwerpen en vervaldatums worden als updates geteld. |

{style="table-layout:auto"}

## De details van een werkorder weergeven {#view-details}

>[!CONTEXTUALHELP]
>id="platform_hygiene_statusbyservice"
>title="Status per service"
>abstract="Aanvragen voor de levenscyclus van gegevens worden onafhankelijk verwerkt door meerdere services van Experience Platforms. Deze sectie schetst de huidige verwerkingsstatus van het verzoek voor elke respectieve dienst. Raadpleeg de gebruikershandleiding bij de levenscyclus van gegevens voor meer informatie."

>[!CONTEXTUALHELP]
>id="platform_hygiene_numberofidentities"
>title="Aantal identiteiten"
>abstract="Het aantal identiteiten waarvan de verslagen werden verzocht om als deel van deze het werkorde te worden bijgewerkt of te worden geschrapt. De in de telling opgenomen identiteiten hoeven niet noodzakelijkerwijs in de betrokken gegevensbestanden te bestaan. Raadpleeg de gebruikershandleiding bij de levenscyclus van gegevens voor meer informatie."

>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="Reactie record verwijderen"
>abstract="Wanneer een record-verwijderingsproces een reactie van het systeem ontvangt, worden deze berichten onder het **[!UICONTROL Result]** sectie. Als er een probleem optreedt terwijl een werkorder wordt verwerkt, worden in deze sectie foutberichten weergegeven die u helpen bij het oplossen van het probleem. Raadpleeg de gebruikershandleiding bij de gegevenslevenscyclus voor meer informatie."

Selecteer de id van een vermelde werkorder om de details ervan weer te geven.

![Afbeelding met een werkorder-id die is geselecteerd](../images/ui/browse/select-work-order.png)

Afhankelijk van het type geselecteerde werkorder, worden verschillende informatie en controles verstrekt. Deze worden behandeld in de onderstaande secties.

### Gegevens opnemen {#record-delete}

De details van een verzoek om een record te schrappen omvatten zijn huidige status en de tijd die is verstreken sinds het verzoek werd gemaakt. Elke aanvraag bevat ook een **[!UICONTROL Status by service]** sectie die individuele statusdetails over elke stroomafwaartse dienst verstrekt die bij de schrapping betrokken is. Op het juiste spoor, kunt u controles gebruiken om de naam en beschrijving van de het werkorde bij te werken.

![Afbeelding met de detailpagina voor een werkvolgorde voor het verwijderen van records](../images/ui/browse/record-delete-details.png)

### Gegevens betreffende de vervaldatum van de gegevensset {#dataset-expiration}

De detailspagina voor een datasetvervaldatum verstrekt informatie over zijn basisattributen, met inbegrip van de geplande vervaldatum op de dagen die resteren alvorens de schrapping voorkomt. In het rechterspoor, kunt u controles gebruiken om de vervaldatum uit te geven of te annuleren.

![Afbeelding die de detailpagina voor een werkorder voor het verlopen van een gegevensset weergeeft](../images/ui/browse/ttl-details.png)

## Volgende stappen

Deze handleiding besprak hoe u bestaande werkorders voor de levenscyclus van gegevens kunt weergeven en beheren in de interface van het platform. Raadpleeg de volgende documentatie voor informatie over het maken van uw eigen werkorders:

* [Verlopen gegevenssets beheren](./dataset-expiration.md)
* [Record verwijderen beheren](./record-delete.md)

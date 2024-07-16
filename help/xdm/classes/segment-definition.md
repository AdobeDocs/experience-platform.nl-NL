---
solution: Experience Platform
title: Segmentdefinitieklasse
description: Leer over de de definitieklasse van het Segment in het Model van Gegevens van de Ervaring (XDM).
exl-id: c0f7b04c-2266-4d08-89a1-67ba758a51a7
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# [!UICONTROL Segment definition] -klasse

&quot;[!UICONTROL Segment definition]&quot;is een standaard klasse van de Gegevens van de Ervaring van het Model (XDM) die de details van een segmentdefinitie vangt. De klasse bevat verplichte velden zoals de id en de naam van een publiek, samen met andere optionele kenmerken. Deze klasse moet worden gebruikt als u segmentdefinities van externe systemen naar Adobe Experience Platform importeert.

>[!NOTE]
>
>Deze klasse zou slechts moeten worden gebruikt om informatie over segmentdefinities zelf te vangen. Om de informatie van het publiekslidmaatschap binnen uw profielgegevens te vangen, zou u de [ het gebiedsgroep van de Details van het Lidmaatschap van het Segment ](../field-groups/profile/segmentation.md) in uw [!UICONTROL XDM Individual Profile] schema moeten gebruiken.

![](../images/classes/segment-definition.png)

| Eigenschap | Beschrijving |
| --- | --- |
| `_repo` | Een object dat de volgende [!UICONTROL DateTime] -velden bevat: <ul><li>`createDate`: De datum en tijd waarop de bron in de gegevensopslag is gemaakt, bijvoorbeeld wanneer de gegevens voor het eerst werden ingevoerd.</li><li>`modifyDate`: De datum en tijd waarop de bron voor het laatst is gewijzigd.</li></ul> |
| `_id` | Een unieke, door het systeem gegenereerde tekenreeks-id voor de record. Dit veld wordt gebruikt om het unieke karakter van een individueel record te volgen, om te voorkomen dat gegevens dubbel worden opgeslagen en om dat record op te zoeken in downstreamdiensten.<br><br> Aangezien dit gebied systeem-geproduceerd is, wordt het geen expliciete waarde geleverd tijdens gegevensopname. U kunt er echter desgewenst nog voor kiezen om uw eigen unieke id-waarden op te geven.<br><br> het is belangrijk om te onderscheiden dat dit gebied **niet** een identiteit met betrekking tot een individuele persoon vertegenwoordigt, maar eerder het verslag van gegevens zelf. Identiteitsgegevens met betrekking tot een persoon zouden aan [ identiteitsgebieden ](../schema/composition.md#identity) in plaats daarvan moeten worden beperkt. |
| `createdByBatchID` | De id van de opgenomen batch die ervoor heeft gezorgd dat de record is gemaakt. |
| `description` | Een beschrijving voor de segmentdefinitie. |
| `identityMap` | Een kaartveld dat een set naamloze identiteiten bevat voor de personen waarop het publiek van toepassing is. Zie de sectie over identiteitskaarten in de [ grondbeginselen van schemacompositie ](../schema/composition.md#identityMap) voor meer informatie over hun gebruiksgeval. |
| `modifiedByBatchID` | De id van de laatst opgenomen batch die ervoor zorgde dat de record werd bijgewerkt. |
| `repositoryCreatedBy` | De id van de gebruiker die de record heeft gemaakt. |
| `repositoryLastModifiedBy` | De id van de gebruiker die de record als laatste heeft gewijzigd. |
| `segmentName` | **(Vereist)** een naam voor de segmentdefinitie. |
| `segmentStatus` | De status van het publiek vanuit het externe systeem. De volgende waarden worden geaccepteerd: <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | Het recentste versienummer van de segmentdefinitie. |

{style="table-layout:auto"}

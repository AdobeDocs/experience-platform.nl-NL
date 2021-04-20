---
solution: Experience Platform
title: Segmentdefinitieklasse
topic: overview
description: Dit document biedt een overzicht van de definitieklasse Segment in het XDM (Experience Data Model).
translation-type: tm+mt
source-git-commit: f4e80cc6a5e5e135bedb77b2d56ae5cb2c8d8c53
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---


# [!UICONTROL Segment definition] class

&quot;[!UICONTROL Segment definition]&quot;is een standaard klasse van de Gegevens van de Ervaring van het Model (XDM) die de details van een segmentdefinitie vangt. De klasse bevat verplichte velden zoals de id en de naam van een segment, samen met andere optionele kenmerken. Deze klasse moet worden gebruikt als u segmentdefinities van externe systemen naar Adobe Experience Platform importeert.

>[!NOTE]
>
>Deze klasse zou slechts moeten worden gebruikt om informatie over segmentdefinities zelf te vangen. Om de informatie van het segmentlidmaatschap binnen uw profielgegevens te vangen, zou u [de Mengsel van de Details van het Lidmaatschap van het Segment](../mixins/profile/segmentation.md) in uw [!UICONTROL XDM Individual Profile] schema moeten gebruiken.

![](../images/classes/segment-definition.png)

| Eigenschap | Beschrijving |
| --- | --- |
| `_repo` | Een object met de volgende velden [!UICONTROL DateTime]: <ul><li>`createDate`: De datum en tijd waarop de bron in de gegevensopslag werd gemaakt, bijvoorbeeld wanneer gegevens voor het eerst werden ingevoerd.</li><li>`modifyDate`: De datum en het tijdstip waarop de bron voor het laatst is gewijzigd.</li></ul> |
| `_id` | Een unieke, door het systeem gegenereerde tekenreeks-id voor de record. Dit veld wordt gebruikt om het unieke karakter van een individueel record te volgen, om te voorkomen dat gegevens dubbel worden opgeslagen en om dat record op te zoeken in downstreamdiensten.<br><br>Aangezien dit veld door het systeem wordt gegenereerd, wordt er geen expliciete waarde opgegeven tijdens het invoeren van gegevens. U kunt er echter desgewenst nog voor kiezen om uw eigen unieke id-waarden op te geven.<br><br>Het is belangrijk te onderscheiden dat dit veld  **geen identiteit** bevat die verband houdt met een individuele persoon, maar eerder met de gegevens zelf. Identiteitsgegevens die betrekking hebben op een persoon moeten in plaats daarvan worden beperkt tot [identiteitsvelden](../schema/composition.md#identity). |
| `createdByBatchID` | De id van de opgenomen batch die ervoor heeft gezorgd dat de record is gemaakt. |
| `description` | Een beschrijving voor de segmentdefinitie. |
| `identityMap` | Een kaartveld dat een set naamloze identiteiten bevat voor de personen waarop het segment van toepassing is. Dit veld wordt automatisch door het systeem bijgewerkt wanneer er identiteitsgegevens worden ingevoerd.<br /><br />Zie de sectie over identiteitskaarten in de  [grondbeginselen van schemacompositie voor meer informatie ](../schema/composition.md#identityMap) over hun gebruiksgeval. |
| `modifiedByBatchID` | De id van de laatst opgenomen batch die ervoor zorgde dat de record werd bijgewerkt. |
| `repositoryCreatedBy` | De id van de gebruiker die de record heeft gemaakt. |
| `repositoryLastModifiedBy` | De id van de gebruiker die de record als laatste heeft gewijzigd. |
| `segmentName` | **(Vereist)** Een naam voor de segmentdefinitie. |
| `segmentStatus` | De status van het segment van het externe systeem. De volgende waarden worden geaccepteerd: <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | Het recentste versienummer van de segmentdefinitie. |

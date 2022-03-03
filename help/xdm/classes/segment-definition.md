---
solution: Experience Platform
title: Segmentdefinitieklasse
topic-legacy: overview
description: Dit document biedt een overzicht van de definitieklasse Segment in het XDM (Experience Data Model).
exl-id: c0f7b04c-2266-4d08-89a1-67ba758a51a7
source-git-commit: c0437b8f9d93c46dbec991a33a893a5b9e0cdf2c
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# [!UICONTROL Segment definition] class

&quot;[!UICONTROL Segment definition]&quot; is een standaardklasse van het Gegevensmodel van de Ervaring (XDM) die de details van een segmentdefinitie vangt. De klasse bevat verplichte velden zoals de id en de naam van een segment, samen met andere optionele kenmerken. Deze klasse moet worden gebruikt als u segmentdefinities van externe systemen naar Adobe Experience Platform importeert.

>[!NOTE]
>
>Deze klasse zou slechts moeten worden gebruikt om informatie over segmentdefinities zelf te vangen. Als u informatie over segmentlidmaatschap wilt vastleggen in uw profielgegevens, moet u de opdracht [Segment Membership Details veld groep](../field-groups/profile/segmentation.md) in uw [!UICONTROL XDM Individual Profile] schema.

![](../images/classes/segment-definition.png)

| Eigenschap | Beschrijving |
| --- | --- |
| `_repo` | Een object dat het volgende bevat [!UICONTROL DateTime] velden: <ul><li>`createDate`: De datum en tijd waarop de bron in de gegevensopslag werd gemaakt, bijvoorbeeld wanneer gegevens voor het eerst werden ingevoerd.</li><li>`modifyDate`: De datum en het tijdstip waarop de bron voor het laatst is gewijzigd.</li></ul> |
| `_id` | Een unieke, door het systeem gegenereerde tekenreeks-id voor de record. Dit veld wordt gebruikt om het unieke karakter van een individueel record te volgen, om te voorkomen dat gegevens dubbel worden opgeslagen en om dat record op te zoeken in downstreamdiensten.<br><br>Aangezien dit veld door het systeem wordt gegenereerd, wordt er geen expliciete waarde opgegeven tijdens het invoeren van gegevens. U kunt er echter desgewenst nog voor kiezen om uw eigen unieke id-waarden op te geven.<br><br>Het is belangrijk te onderscheiden dat dit veld **niet** een identiteit vertegenwoordigen die verband houdt met een individuele persoon, maar eerder met de gegevens zelf. Identiteitsgegevens betreffende een persoon moeten worden beperkt tot [identiteitsvelden](../schema/composition.md#identity) in plaats daarvan. |
| `createdByBatchID` | De id van de opgenomen batch die ervoor heeft gezorgd dat de record is gemaakt. |
| `description` | Een beschrijving voor de segmentdefinitie. |
| `identityMap` | Een kaartveld dat een set naamloze identiteiten bevat voor de personen waarop het segment van toepassing is. Zie de sectie over identiteitskaarten in het dialoogvenster [grondbeginselen van de schemacompositie](../schema/composition.md#identityMap) voor meer informatie over het gebruik ervan . |
| `modifiedByBatchID` | De id van de laatst opgenomen batch die ervoor zorgde dat de record werd bijgewerkt. |
| `repositoryCreatedBy` | De id van de gebruiker die de record heeft gemaakt. |
| `repositoryLastModifiedBy` | De id van de gebruiker die de record als laatste heeft gewijzigd. |
| `segmentName` | **(Vereist)** Een naam voor de segmentdefinitie. |
| `segmentStatus` | De status van het segment van het externe systeem. De volgende waarden worden geaccepteerd: <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | Het recentste versienummer van de segmentdefinitie. |

{style=&quot;table-layout:auto&quot;}

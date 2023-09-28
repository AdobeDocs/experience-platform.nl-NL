---
title: Afzonderlijke XDM-perspectiefprofielklasse
description: Dit document biedt een overzicht van de klasse XDM Individual Prospect Profile in Experience Data Model (XDM).
source-git-commit: 7562da0f07a2109a2030653927d8d2639685e442
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# [!UICONTROL XDM Individual Prospect Profile] class

In Experience Data Model (XDM), [!UICONTROL XDM Individual Prospect Profile] de klasse vangt perspectiefprofielen typisch die van gegevenspartners voor top-of-de-kanaalklant gebruiksgevallen worden gedownload.

![Het schemadiagram van de klasse XDM Prospect.](../images/classes/individual-prospect-profile.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `_repo` | Object | Deze klasse laat u toe om perspectiefprofielen in te brengen die van gegevensverkopers aan de gebruiksgevallen van de de acquisitie van de steenklant worden aangekocht. |
| `_repo.createDate` | [!UICONTROL DateTime] | De serverdatum en -tijd waarop de bron in de opslagplaats is gemaakt. De aanmaaktijd kan zijn wanneer een elementbestand voor het eerst wordt geüpload of wanneer de server een map maakt als het bovenliggende element van een nieuw element. De datetime-eigenschap moet voldoen aan de ISO 8601-standaard. Een voorbeeld van deze notatie is &quot;2004-10-23T12:00:00-06:00&quot;. |
| `_repo.modifyDate` | [!UICONTROL DateTime] | De serverdatum en tijd waarop de bron voor het laatst in de opslagplaats is gewijzigd, bijvoorbeeld wanneer een nieuwe versie van een element wordt geüpload of de onderliggende bron van een map wordt toegevoegd of verwijderd. De datetime-eigenschap moet voldoen aan de ISO 8601-standaard. Een voorbeeldformulier is &quot;2004-10-23T12:00:00-06:00&quot;. |
| `_id` | [!UICONTROL String] | Een unieke, door het systeem gegenereerde tekenreeks-id voor de record. Dit veld wordt gebruikt om het unieke karakter van een individueel record te volgen, om te voorkomen dat gegevens dubbel worden opgeslagen en om dat record op te zoeken in downstreamdiensten.<br><br>Aangezien dit veld door het systeem wordt gegenereerd, levert het tijdens het invoeren van gegevens geen expliciete waarde op. U kunt echter desgewenst ook uw eigen unieke id-waarden opgeven. |
| `createdByBatchID` | [!UICONTROL String] | De id van de opgenomen batch die ervoor heeft gezorgd dat de record is gemaakt. |
| `modifiedByBatchID` | [!UICONTROL String] | De id van de laatst opgenomen batch die ervoor zorgde dat de record werd bijgewerkt. |
| `partnerID` | [!UICONTROL String] | Typisch, een uniek pseudoniem herkenningsteken dat een individueel vooruitzicht identificeert. Zie de documentatie op [identiteitstypen](../../identity-service/namespaces.md#identity-type) voor meer informatie over de Partner ID en de andere identiteitstypen die beschikbaar zijn in Adobe Experience Platform. |
| `repositoryCreatedBy` | [!UICONTROL String] | De id van de gebruiker die de record heeft gemaakt. |
| `repositoryLastModifiedBy` | [!UICONTROL String] | De id van de gebruiker die de record als laatste heeft gewijzigd. Wanneer de record wordt gemaakt, worden de `modifiedByUser` waarde wordt ingesteld als de `createdByUser` waarde. |

{style="table-layout:auto"}

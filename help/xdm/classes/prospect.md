---
title: Afzonderlijke XDM-perspectiefprofielklasse
description: Leer meer over de klasse van het Profiel van het Individuele Vooruitzicht XDM in het Model van de Gegevens van de Ervaring (XDM).
exl-id: 10fd9d16-4123-4ad4-971f-b715231ee6a9
source-git-commit: f4ddcf14de7a5cec42b5ebc521203cfdd1498a9f
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---

# [!UICONTROL XDM Individual Prospect Profile] -klasse

In het Model van Gegevens van de Ervaring (XDM), vangt de [!UICONTROL XDM Individual Prospect Profile] klasse perspectiefprofielen typisch die van gegevenspartners voor top-of-de-kanaalklant gebruiksgevallen worden gedownload.

>[!NOTE]
>
>Om een gebied in het Individuele Profiel van het Vooruitzicht XDM als entiteit te plaatsen, moet u minstens één identiteitskaart van de Partner eerst creëren namespace. Lees meer over identiteitskaart van de Partner namespaces in de [&#x200B; sectie van identiteitstypes &#x200B;](../../identity-service/features/namespaces.md).

![&#x200B; het schemadiagram van de klasse van het Vooruitzicht XDM.](../images/classes/individual-prospect-profile.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `_repo` | Object | Deze klasse laat u toe om perspectiefprofielen in te brengen die van gegevensverkopers aan de gebruiksgevallen van de de acquisitie van de steenklant worden aangekocht. |
| `_repo.createDate` | [!UICONTROL DateTime] | De serverdatum en -tijd waarop de bron in de opslagplaats is gemaakt. De aanmaaktijd kan zijn wanneer een elementbestand voor het eerst wordt geüpload of wanneer de server een map maakt als het bovenliggende element van een nieuw element. De datetime-eigenschap moet voldoen aan de ISO 8601-standaard. Een voorbeeld van dit formaat is &quot;2004-10-23T12 :00: 00-06:00&quot;. |
| `_repo.modifyDate` | [!UICONTROL DateTime] | De serverdatum en tijd waarop de bron voor het laatst in de opslagplaats is gewijzigd, bijvoorbeeld wanneer een nieuwe versie van een element wordt geüpload of de onderliggende bron van een map wordt toegevoegd of verwijderd. De datetime-eigenschap moet voldoen aan de ISO 8601-standaard. Een voorbeeldvorm is &quot;2004-10-23T12 :00: 00-06:00&quot;. |
| `_id` | [!UICONTROL String] | Een unieke, door het systeem gegenereerde tekenreeks-id voor de record. Dit veld wordt gebruikt om het unieke karakter van een individueel record te volgen, om te voorkomen dat gegevens dubbel worden opgeslagen en om dat record op te zoeken in downstreamdiensten.<br><br> Aangezien dit gebied systeem-geproduceerd is, levert het geen expliciete waarde tijdens gegevensopname. U kunt echter desgewenst ook uw eigen unieke id-waarden opgeven. |
| `createdByBatchID` | [!UICONTROL String] | De id van de opgenomen batch die ervoor heeft gezorgd dat de record is gemaakt. |
| `modifiedByBatchID` | [!UICONTROL String] | De id van de laatst opgenomen batch die ervoor zorgde dat de record werd bijgewerkt. |
| `partnerID` | [!UICONTROL String] | Typisch, een uniek pseudoniem herkenningsteken dat een individueel vooruitzicht identificeert. Zie de documentatie op [&#x200B; identiteitstypes &#x200B;](../../identity-service/features/namespaces.md#identity-type) om meer over identiteitskaart van de Partner en de andere identiteitstypes te leren die binnen Adobe Experience Platform beschikbaar zijn. |
| `repositoryCreatedBy` | [!UICONTROL String] | De id van de gebruiker die de record heeft gemaakt. |
| `repositoryLastModifiedBy` | [!UICONTROL String] | De id van de gebruiker die de record als laatste heeft gewijzigd. Wanneer de record wordt gemaakt, wordt de `modifiedByUser` -waarde ingesteld als de `createdByUser` -waarde. |

{style="table-layout:auto"}

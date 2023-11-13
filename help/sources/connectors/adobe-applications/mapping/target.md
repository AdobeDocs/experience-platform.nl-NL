---
solution: Experience Platform
title: Adobe Target-gebeurtenisgegevens toewijzen aan XDM
description: Leer hoe u Adobe Target-gebeurtenisvelden kunt toewijzen aan een XDM-schema (Experience Data Model) voor gebruik in Adobe Experience Platform.
exl-id: dab08ab6-6c1c-460a-bb52-8dcdb5709a34
source-git-commit: 81412493b096264ce7a89e3ca2348edb2dcd1798
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# Toewijzingen doelveld

In de volgende tabel worden de velden van een XDM-ervaringsgebeurtenisschema (Experience Data Model) en de bijbehorende velden uit Adobe Target weergegeven waaraan ze moeten worden toegewezen. Er worden ook aanvullende opmerkingen voor bepaalde toewijzingen gegeven.

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| XDM ExperienceEvent-veld | Veld voor doelaanvraag | Notities |
| ------------------------- | -------------------- | ----- |
| **`id`** | Een unieke aanvraag-id |
| **`dataSource`** | | Gevormd aan &quot;1&quot;voor alle cliënten. |
| `dataSource._id` | Een door het systeem gegenereerde waarde die niet kan worden doorgegeven met de aanvraag. | De unieke id van deze gegevensbron. Dit zou worden verstrekt door het individu of het systeem dat de gegevensbron creeerde. |
| `dataSource.code` | Een door het systeem gegenereerde waarde die niet kan worden doorgegeven met de aanvraag. | Een sneltoets naar de volledige @id. U kunt ten minste een van de code of @id gebruiken. Soms wordt deze code de integratiecode van de gegevensbron genoemd. |
| `dataSource.tags` | Een door het systeem gegenereerde waarde die niet kan worden doorgegeven met de aanvraag. | Tags worden gebruikt om aan te geven hoe aliassen die door een bepaalde gegevensbron worden vertegenwoordigd, door toepassingen met die aliassen moeten worden geïnterpreteerd.<br><br>Voorbeelden:<br><ul><li>`isAVID`: Gegevensbronnen die analytische bezoeker-id&#39;s vertegenwoordigen.</li><li>`isCRSKey`: Gegevensbronnen die aliassen vertegenwoordigen die als sleutels in CRS zouden moeten worden gebruikt.</li></ul>De markeringen worden geplaatst wanneer de gegevensbron wordt gecreeerd maar zij zijn ook inbegrepen in pijpleidingsberichten wanneer het van verwijzingen voorzien van een bepaalde gegevensbron. |
| **`timestamp`** | Tijdstempel voor gebeurtenis |
| **`channel`** | `context.channel` | Werkt alleen met weergave. De opties zijn &quot;web&quot; en &quot;mobiel&quot;, waarbij &quot;web&quot; de standaardwaarde is. |
| **`endUserIds`** |
| `endUserIds.experience.tntId` | `tntId/mboxPC` |
| `endUserIds.experience.mcId` | `marketingCloudVisitorId` | De Experience Cloud-id (ECID) wordt ook wel MCID genoemd en wordt nog steeds gebruikt in naamruimten. |
| **`environment`** |
| `environment.browserDetails.userAgent` | `mboxRequest.userAgent` |
| `environment.browserDetails.viewPortHeight` | `mboxRequest.browserHeight` |
| `environment.browserDetails.viewPortWidth` | `mboxRequest.browserWidth` |
| `environment.operatingSystem` | `deviceAtlas.osName` |
| `environment.operatingSystemVersion` | `deviceAtlas.osVersion` |
| `environment.viewportHeight` | `mboxRequest.screenHeight` |
| `environment.viewportWidth` | `mboxRequest.screenWidth` |
| `environment.colorDepth` | `mboxRequest.colorDepth` |
| `environment.carrier` | De naam van de mobiele provider is opgelost op basis van het IP-adres van het verzoek. |
| `environment.ipV4` | `mboxRequest.ipAddress` (indien in V4-indeling) |
| `environment.ipV6` | `mboxRequest.ipAddress` (indien in V6-indeling) |
| **`experience`** |
| `experience.target.clientCode` | `mboxRequest.client` |
| `experience.target.mboxName` | `mboxRequest.mboxName` |
| `experience.target.mboxVersion` | `mboxRequest.mboxVersion` |
| `experience.target.sessionId` | `mboxRequest.sessionId` |
| `experience.target.environmentID` | Interne toewijzing van het doel voor klant-bepaalde milieu&#39;s (zoals dev, qa, of prod). |
| `experience.target.supplementalDataID` | Id die wordt gebruikt om doelgebeurtenissen aan te sluiten met analytische gebeurtenissen |
| `experience.target.pageDetails.pageId` | `mboxRequest.pageId` |
| `experience.target.pageDetails.pageScore` | `mboxRequest.mboxPageValue` |
| `experience.target.activities` | Lijst (array) van activiteiten waarvoor de bezoeker in aanmerking komt |
| `experience.target.activities[i].activityID` | De id van een bepaalde activiteit waarvoor de bezoeker in aanmerking kwam |
| `experience.target.activities[i].version` | De versie van een bepaalde activiteit waarvoor de bezoeker in aanmerking kwam |
| `experience.target.activities[i].activityEvents` | Bevat de details van activiteitengebeurtenissen die de gebruiker met deze gebeurtenis heeft getroffen. |
| **`device`** |
| `device.typeIDService` | `XDMDevice.Device.TypeIDService.typeIDService_deviceatlas` |
| `device.type` | Een van de volgende eigenschappen van `deviceAtlas` (of NULL): <ul><li>`type_mobile`</li><li>`type_tablet`</li><li>`type_desktop`</li><li>`type_ereader`</li><li>`type_television`</li><li>`type_settop`</li><li>`type_mediaplayer`</li></ul> |
| `device.typeID` | (lege tekenreeks) |
| `device.manufacturer` | `deviceAtlas.manufacturer` |
| `device.model` | `deviceAtlas.model` |
| `device.modelNumber` | (lege tekenreeks) |
| `device.screenHeight` | `deviceAtlas.displayHeight` |
| `device.screenWidth` | `deviceAtlas.displayWidth` |
| `device.colorDepth` | `deviceAtlas.displayColorDepth` |
| **`placeContext`** |
| `placeContext.geo.id` | Willekeurige UUID (verplicht) |
| `placeContext.geo.city` | De plaatsnaam is opgelost op basis van het IP-adres van het verzoek. |
| `placeContext.geo.countryCode` | Landcode opgelost op basis van het IP-adres van het verzoek. |
| `placeContext.geo.dmaId` | Aangewezen code van het Gebied van de Markt die op het IP van het verzoek adres wordt opgelost. |
| `placeContext.geo.postalCode` | Postcode is opgelost op basis van het IP-adres van het verzoek. |
| `placeContext.geo.stateProvince` | Staat of provincie opgelost op basis van het IP-adres van het verzoek. |
| `placeContext.localTime` | `mboxRequest.offsetTime` + `mboxRequest.currentServerTime` |
| **`commerce`** | | Stel dit alleen in als de aanvraag ordergegevens bevat. |
| `commerce.order.priceTotal` | `mboxRequest.orderTotal` |
| `commerce.order.purchaseOrderNumber` | `mboxRequest.orderId` |
| `commerce.order.purchaseID` | `mboxRequest.orderId` |
| **`web`** |
| `web.withWebPageDetails.url` | `mboxURL.context.address.url` |
| `web.webReferrer.url` | `mboxReferrer.context.address.url` |
| **`identityMap`** |
| `identityMap.TNTID` | `tntId.mboxPC` |
| `identityMap.ECID` | `marketingCloudVisitorId` |

{style="table-layout:auto"}

---
title: Opmerkingen bij de release van Adobe Experience Platform, oktober 2022
description: In de releaseopmerkingen van oktober 2022 voor Adobe Experience Platform.
source-git-commit: 098b4b7a0dcd3ddfcd13f7dd473c4fa6832d23df
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 1%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 26 oktober 2022**

Nieuwe functies in Adobe Experience Platform:

- [Door de klant beheerde sleutels](#cmk)

Updates voor bestaande functies in Adobe Experience Platform:

- [Gegevensverzameling](#data-collection)
- [Experience Data Model (XDM)](#xdm)
- [Bronnen](#sources)

## Door de klant beheerde sleutels {#cmk}

Alle gegevens die op Adobe Experience Platform zijn opgeslagen, worden in rust gecodeerd met systeemtoetsen. Als u een toepassing gebruikt die bovenop Platform wordt gebouwd, kunt u nu ervoor kiezen om uw eigen encryptiesleutels in plaats daarvan te gebruiken, die u grotere controle over uw gegevensveiligheid geven.

Zie het overzicht op [door de klant beheerde sleutels](../../landing/governance-privacy-security/customer-managed-keys.md) voor meer informatie over de functie.

## Gegevensverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar het Adobe Experience Platform Edge Network kunt verzenden waar deze kunnen worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Gevoelige gegevensverwerking voor gegevensstromen | De gegevensstromen gebruiken nu verscheidene technologieën van de Platform om gevoelige gegevens zoals die door verordeningen zoals de Wet van de Portabiliteit en van de Verantwoording van de Ziekteverzekering (HIPAA) worden afgedwongen adequaat te behandelen. Zie de sectie over [verwerking van gevoelige gegevens in gegevensstreams](../../edge/datastreams/overview.md#sensitive) voor meer informatie . |
| [!DNL Splunk] extensie voor het doorsturen van gebeurtenissen | U kunt nu gegevens verzenden naar [!DNL Splunk] met een [gebeurtenis doorsturen](../../tags/ui/event-forwarding/overview.md) extensie. Zie de [[!DNL Splunk] extensieoverzicht](../../tags/extensions/web/splunk/overview.md) voor meer informatie . |
| [!DNL Zendesk] extensie voor het doorsturen van gebeurtenissen | U kunt nu gegevens verzenden naar [!DNL Zendesk] met een [gebeurtenis doorsturen](../../tags/ui/event-forwarding/overview.md) extensie. Zie de [[!DNL Zendesk] extensieoverzicht](../../tags/extensions/web/zendesk/overview.md) voor meer informatie . |

{style=&quot;table-layout:auto&quot;}

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Adobe Experience Platform worden gebracht. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Bijgewerkte XDM-componenten**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Gegevenstype | [[!UICONTROL Session details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | De `authorized` van een booleaanse tekst naar een tekenreeks. `season` en `episode` zijn gewijzigd van gehele getallen in tekenreeksen. |
| Gegevenstype | [[!UICONTROL Advertising details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `name` is hernoemd naar `friendlyName`, en `ID` is hernoemd naar `name`. |
| Gegevenstype | [[!UICONTROL Error details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | `ID` is hernoemd naar `name`. |

{style=&quot;table-layout:auto&quot;}

Voor meer informatie over XDM in Platform, zie [XDM System, overzicht](../../xdm/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- | 
| Beta-beschikbaarheid van Adobe Workfront-bron | Gebruik de [Adobe Workfront-bron](../../sources/connectors/adobe-applications/workfront.md) om uw gegevens van Workfront aan Experience Platform te brengen en gebruiksgevallen uit te voeren zoals het combineren van uw werkverslagen met derdengegevens, het toepassen van historische en tijdreeksanalyses op het werkverslagen, en het vragen van het werkgegevens gebruikend standaardSQL. Lees voor meer informatie de handleiding op [een Workfront-bronverbinding maken in de gebruikersinterface](../../sources/tutorials/ui/create/adobe-applications/workfront.md). |
| Beta beschikbaarheid van Oracle Service Cloud-bron | Gebruik de Cloud-bron van de service Oracle om gegevens van uw Oracle Service Cloud-account in te voeren naar Experience Platform. Voor meer informatie leest u de documentatie op het tabblad [Cloud-bron voor oracle Service](../../sources/connectors/customer-success/oracle-service-cloud.md). |

Voor meer informatie over bronnen leest u de [overzicht van bronnen](../../sources/home.md).

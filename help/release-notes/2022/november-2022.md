---
title: Aanvullende informatie voor Adobe Experience Platform, november 2022
description: Aanvullende informatie voor Adobe Experience platform, november 2022.
exl-id: 1048cfae-6e7a-4d05-a004-c5c095a17fc4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 52%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum: donderdag 23 november 2022**

Updates voor bestaande functies in Adobe Experience Platform:

- [Dataverzameling](#data-collection)
- [Experience-datamodel (XDM)](#xdm)
- [Bronnen](#sources)

## Dataverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u klantervaringsgegevens aan de klantzijde kunt verzamelen en deze naar het Adobe Experience Platform Edge Network kunt verzenden. Daar kunnen ze worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| [!DNL AWS] extensie voor het doorsturen van gebeurtenissen | U kunt gegevens [!DNL Amazon Web Services] ([!DNL AWS]) nu verzenden gebruikend een [ gebeurtenis die ](../../tags/ui/event-forwarding/overview.md) uitbreiding door:sturen. Zie het [[!DNL AWS] extensieoverzicht](../../tags/extensions/server/aws/overview.md) voor meer informatie. |
| [!DNL Google Ads Enhanced Conversions] extensie voor het doorsturen van gebeurtenissen | U kunt omzettingsgegevens aan [!DNL Google Ads] nu verzenden gebruikend een [ gebeurtenis die ](../../tags/ui/event-forwarding/overview.md) uitbreiding door:sturen. Zie het [[!DNL Google Ads Enhanced Conversions] extensieoverzicht](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) voor meer informatie. |
| [!DNL Microsoft Azure] extensie voor het doorsturen van gebeurtenissen | U kunt gegevens aan [!DNL Microsoft Azure] nu verzenden gebruikend een [ gebeurtenis die ](../../tags/ui/event-forwarding/overview.md) uitbreiding door:sturen. Zie het [[!DNL Microsoft Azure] extensieoverzicht](../../tags/extensions/server/azure/overview.md) voor meer informatie. |

Voor meer informatie over de mogelijkheden van de gegevensinzameling van Experience Platform, zie het [ overzicht van de gegevensinzameling ](../../collection/home.md).

## Experience-datamodel (XDM) {#xdm}

XDM is een open-bronspecificatie die algemene structuren en definities (schema&#39;s) biedt voor gegevens die in Adobe Experience Platform worden geïmporteerd. Door de XDM-standaarden te hanteren, kunnen alle gegevens over de klantervaring worden opgenomen in een gemeenschappelijke weergave. Zo worden inzichten sneller en beter geïntegreerd verkregen. U kunt waardevolle inzichten verkrijgen uit klantacties, klantdoelgroepen definiëren via segmenten en klantkenmerken gebruiken voor personalisatiedoeleinden.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Velden toewijzen aan aangepaste klassen wanneer deze rechtstreeks aan een schema worden toegevoegd | Wanneer [ toevoegend direct een individueel gebied aan een schema ](../../xdm/ui/resources/schemas.md#add-individual-fields), eerder kon u het gebied aan een gebiedsgroep als zijn oudermiddel slechts toewijzen. Nu, naast gebiedsgroepen, kunt u [ het gebied aan een douaneklasse ](../../xdm/ui/resources/schemas.md#add-to-class) als zijn oudermiddel in plaats daarvan toewijzen. |

{style="table-layout:auto"}

Voor meer informatie over XDM in Experience Platform, zie het [ XDM overzicht van het Systeem ](../../xdm/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens opnemen uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- | 
| Beta-beschikbaarheid van Oracle Service Cloud-bron | Gebruik de Oracle Service Cloud-bron om gegevens van uw Oracle Service Cloud-account in te voeren naar Experience Platform. Voor meer informatie, lees de documentatie over de [ bron van de Wolk van de Dienst van Oracle ](../../sources/connectors/customer-success/oracle-service-cloud.md). |

Voor meer informatie over bronnen leest u het [overzicht van bronnen](../../sources/home.md).

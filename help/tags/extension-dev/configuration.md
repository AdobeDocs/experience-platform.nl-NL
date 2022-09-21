---
title: Extensieconfiguratie
description: Leer hoe te om een markeringsuitbreiding te vormen om globale montages van een gebruiker in de UI van Adobe Experience Platform of UI van de Inzameling van Gegevens te verzamelen.
exl-id: 2bf33617-1398-499f-8325-3849dbdb1f97
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Extensieconfiguratie

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

De configuratie van de uitbreiding is de manier waardoor een uitbreiding globale montages van een gebruiker verzamelt. Bijvoorbeeld, overweeg een uitbreiding die de gebruiker toestaat om een baken te verzenden gebruikend een Send actie van het Bandje, en het baken moet altijd een rekeningsidentiteitskaart bevatten. We willen gebruikers niet lastig maken door hen elke keer om de account-id te vragen wanneer ze een handeling Send Beacon configureren. In plaats daarvan moet de extensie eenmaal om de account-id vragen vanuit de configuratieweergave van de extensie. Telkens wanneer een baken moet worden verzonden, kan de Send module van de de actielobiebibliotheek van het Baken rekeningsidentiteitskaart van de uitbreidingsconfiguratie trekken en het toevoegen aan het baken.

Wanneer gebruikers een extensie installeren op een eigenschap tag in Adobe Experience Platform, wordt hun de configuratieweergave van de extensie getoond die uw extensie biedt. Ze kunnen de installatie van de extensie niet voltooien zonder de extensieconfiguratie te voltooien. Document weergeven op [views](./web/views.md) leren hoe te om een mening voor uitbreidingsconfiguratie tot stand te brengen.

Nadat de instellingen zijn opgeslagen vanuit een configuratieweergave voor extensies, worden deze weergegeven in de runtimebibliotheek van de tag. U kunt tot deze montages van de modules van de uitbreidingsbibliotheek dan toegang hebben door te roepen [`turbine.getExtensionSettings()`](./turbine.md#get-extension-settings).

De configuratie van de uitbreiding is een facultatieve eigenschap die u aan hefboomwerking kunt verkiezen.

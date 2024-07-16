---
title: Extensieconfiguratie
description: Leer hoe te om een markeringsuitbreiding te vormen om globale montages van een gebruiker in de UI van Adobe Experience Platform of UI van de Inzameling van Gegevens te verzamelen.
exl-id: 2bf33617-1398-499f-8325-3849dbdb1f97
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Extensieconfiguratie

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Gelieve te verwijzen naar het volgende [ document ](../term-updates.md) voor een geconsolideerde verwijzing van de terminologieveranderingen.

De configuratie van de uitbreiding is de manier waardoor een uitbreiding globale montages van een gebruiker verzamelt. Bijvoorbeeld, overweeg een uitbreiding die de gebruiker toestaat om een baken te verzenden gebruikend een Send actie van het Bandje, en het baken moet altijd een rekeningsidentiteitskaart bevatten. We willen gebruikers niet lastig maken door hen elke keer om de account-id te vragen wanneer ze een handeling Send Beacon configureren. In plaats daarvan moet de extensie eenmaal om de account-id vragen vanuit de configuratieweergave van de extensie. Telkens wanneer een baken moet worden verzonden, kan de Send module van de de actielobiebibliotheek van het Baken rekeningsidentiteitskaart van de uitbreidingsconfiguratie trekken en het toevoegen aan het baken.

Wanneer gebruikers een extensie installeren op een eigenschap tag in Adobe Experience Platform, wordt hun de configuratieweergave van de extensie getoond die uw extensie biedt. Ze kunnen de installatie van de extensie niet voltooien zonder de extensieconfiguratie te voltooien. Zie het document op [ meningen ](./web/views.md) leren hoe te om een mening voor uitbreidingsconfiguratie tot stand te brengen.

Nadat de instellingen zijn opgeslagen vanuit een configuratieweergave voor extensies, worden deze weergegeven in de runtimebibliotheek van de tag. U kunt deze instellingen vervolgens openen vanuit de modules van de extensiebibliotheek door [`turbine.getExtensionSettings()`](./turbine.md#get-extension-settings) aan te roepen.

De configuratie van de uitbreiding is een facultatieve eigenschap die u aan hefboomwerking kunt verkiezen.

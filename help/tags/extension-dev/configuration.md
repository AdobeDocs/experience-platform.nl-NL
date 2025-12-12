---
title: Extensieconfiguratie
description: Leer hoe te om een markeringsuitbreiding te vormen om globale montages van een gebruiker in de UI van Adobe Experience Platform of UI van de Inzameling van Gegevens te verzamelen.
exl-id: 2bf33617-1398-499f-8325-3849dbdb1f97
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# Extensieconfiguratie

De configuratie van de uitbreiding is de manier waardoor een uitbreiding globale montages van een gebruiker verzamelt. Bijvoorbeeld, overweeg een uitbreiding die de gebruiker toestaat om een baken te verzenden gebruikend een Send actie van het Bandje, en het baken moet altijd een rekeningsidentiteitskaart bevatten. We willen gebruikers niet lastig maken door hen elke keer om de account-id te vragen wanneer ze een handeling Send Beacon configureren. In plaats daarvan moet de extensie eenmaal om de account-id vragen vanuit de configuratieweergave van de extensie. Telkens wanneer een baken moet worden verzonden, kan de Send module van de de actielobiebibliotheek van het Baken rekeningsidentiteitskaart van de uitbreidingsconfiguratie trekken en het toevoegen aan het baken.

Wanneer gebruikers een extensie installeren op een eigenschap tag in Adobe Experience Platform, wordt hun de configuratieweergave van de extensie getoond die uw extensie biedt. Ze kunnen de installatie van de extensie niet voltooien zonder de extensieconfiguratie te voltooien. Zie het document op [ meningen ](./web/views.md) leren hoe te om een mening voor uitbreidingsconfiguratie tot stand te brengen.

Nadat de instellingen zijn opgeslagen vanuit een configuratieweergave voor extensies, worden deze weergegeven in de runtimebibliotheek van de tag. U kunt deze instellingen vervolgens openen vanuit de modules van de extensiebibliotheek door [`turbine.getExtensionSettings()`](./turbine.md#get-extension-settings) aan te roepen.

De configuratie van de uitbreiding is een facultatieve eigenschap die u aan hefboomwerking kunt verkiezen.

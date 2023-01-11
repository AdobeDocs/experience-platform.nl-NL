---
solution: Experience Platform
title: Voorbeeldgegevens genereren voor een XDM-schema in de gebruikersinterface
description: Leer hoe u voorbeeld-JSON-gegevens kunt genereren op basis van een bestaand schema in de Adobe Experience Platform-gebruikersinterface.
exl-id: e60eedb2-2245-42cd-b574-43caf9e3426c
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# Voorbeeldgegevens genereren voor een XDM-schema in de gebruikersinterface

Om gegevens in Adobe Experience Platform in te voeren, moeten de indeling en de structuur van de gegevens voldoen aan een bestaand schema van het Experience Data Model (XDM). Afhankelijk van de ingewikkeldheid van het schema voor een bepaalde dataset, kan het moeilijk zijn om de nauwkeurige vorm van de gegevens te bepalen die de dataset op opneming verwacht.

Voor elk schema dat u in de interface van het Experience Platform definieert, kunt u een voorbeeld-JSON-object genereren dat voldoet aan de structuur van het schema. Dit voorwerp kan als malplaatje voor om het even welke gegevens dienen die in datasets worden opgenomen die het betrokken schema in dienst nemen.

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Schemas]** in de linkernavigatie. Onder de **[!UICONTROL Browse]** Zoek het schema waarvoor u voorbeeldgegevens wilt genereren. Selecteer het uit de lijst, en de juiste spoorupdates om details over het schema te tonen. Selecteer **[!UICONTROL Download sample file]**.

![](../images/ui/sample/sample-data.png)

Een voorbeeld-JSON-bestand wordt gedownload door de browser. U kunt dit dossier nu als verwijzing voor gebruiken hoe te om uw gegevens te structureren wanneer het opnemen in datasets die dit schema gebruiken.

## Volgende stappen

Deze handleiding besprak hoe u een voorbeeld-JSON-bestand kunt genereren op basis van een XDM-schema in de gebruikersinterface van het Platform. Zie voor meer informatie over het genereren van voorbeeldgegevens met de API voor schemaregistratie [eindgids met voorbeeldgegevens](../api/sample-data.md).

Als u klaar bent om gegevens in te voeren, raadpleegt u de zelfstudie [een CSV-bestand toewijzen aan XDM](../../ingestion/tutorials/map-csv/overview.md) om te leren hoe u een vlak gegevensbestand (zoals een CSV) kunt toewijzen aan een XDM-schema en dit kunt opnemen in het Platform. U kunt ook een [bronverbinding](../../sources/home.md) om uw gegevens van een externe bron in te brengen en het in kaart te brengen aan XDM.

Voor meer informatie over de mogelijkheden van de [!UICONTROL Schemas] in de gebruikersinterface, raadpleegt u de [[!UICONTROL Schemas] werkruimte - overzicht](./overview.md).

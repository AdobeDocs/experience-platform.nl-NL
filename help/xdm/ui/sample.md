---
solution: Experience Platform
title: Voorbeeldgegevens genereren voor een XDM-schema in de gebruikersinterface
description: Leer hoe u voorbeeld-JSON-gegevens kunt genereren op basis van een bestaand schema in de Adobe Experience Platform-gebruikersinterface.
topic: user guide
translation-type: tm+mt
source-git-commit: 87497ef8a0ebf8de8b6c2dff1650c0b982299e8a
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---


# Voorbeeldgegevens genereren voor een XDM-schema in de gebruikersinterface

Om gegevens in Adobe Experience Platform in te voeren, moeten de indeling en de structuur van de gegevens voldoen aan een bestaand schema van het Experience Data Model (XDM). Afhankelijk van de ingewikkeldheid van het schema voor een bepaalde dataset, kan het moeilijk zijn om de nauwkeurige vorm van de gegevens te bepalen die de dataset op opneming verwacht.

Voor elk schema dat u in de interface van het Experience Platform definieert, kunt u een voorbeeld-JSON-object genereren dat voldoet aan de structuur van het schema. Dit voorwerp kan als malplaatje voor om het even welke gegevens dienen die in datasets worden opgenomen die het betrokken schema in dienst nemen.

Selecteer **[!UICONTROL Schema&#39;s]** in de linkernavigatie in de interface van het Platform. Zoek onder het tabblad **[!UICONTROL Bladeren]** het schema waarvoor u voorbeeldgegevens wilt genereren. Selecteer het uit de lijst, en de juiste spoorupdates om details over het schema te tonen. Selecteer **[!UICONTROL Voorbeeldbestand downloaden].**

![](../images/ui/sample/sample-data.png)

Een voorbeeld-JSON-bestand wordt gedownload door de browser. U kunt dit dossier nu als verwijzing voor gebruiken hoe te om uw gegevens te structureren wanneer het opnemen in datasets die dit schema gebruiken.

## Volgende stappen

Deze handleiding besprak hoe u een voorbeeld-JSON-bestand kunt genereren op basis van een XDM-schema in de gebruikersinterface van het Platform. Leren hoe te om steekproefgegevens te produceren gebruikend de Registratie API van het Schema, zie [de gids van het eindpunt van steekproefgegevens](../api/sample-data.md).

Als u klaar bent om met het opnemen van gegevens te beginnen, raadpleegt u de zelfstudie over [het toewijzen van een CSV-bestand aan XDM](../../ingestion/tutorials/map-a-csv-file.md) om te leren hoe u een plat gegevensbestand (zoals een CSV) kunt toewijzen aan een XDM-schema en het in Platform kunt opnemen. Alternatief, kunt u [bronverbinding ](../../sources/home.md) vestigen om uw gegevens van een externe bron in te brengen en het in kaart te brengen aan XDM.

Voor meer informatie over de mogelijkheden van de [!UICONTROL Werkruimte van Schema] in UI, verwijs naar [[!UICONTROL Schemas] werkruimteoverzicht](./overview.md).
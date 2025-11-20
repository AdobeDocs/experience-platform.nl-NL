---
solution: Experience Platform
title: Voorbeeldgegevens genereren voor een XDM-schema in de gebruikersinterface
description: Leer hoe u voorbeeld-JSON-gegevens kunt genereren op basis van een bestaand schema in de Adobe Experience Platform-gebruikersinterface.
exl-id: e60eedb2-2245-42cd-b574-43caf9e3426c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# Voorbeeldgegevens genereren voor een XDM-schema in de gebruikersinterface {#generate-sample-data-for-an-xdm-schema}

>[!CONTEXTUALHELP]
>id="platform_xdm_downloadsamplefile"
>title="Voorbeeldbestand downloaden"
>abstract="Genereer een voorbeeld-JSON-object dat voldoet aan de structuur van het gekozen schema. Dit voorwerp kan als malplaatje dienen om uw gegevens correct geformatteerd voor opneming in datasets te verzekeren die dat schema gebruiken. Het JSON-voorbeeldbestand wordt gedownload door uw browser."

Om gegevens in Adobe Experience Platform in te voeren, moeten de indeling en de structuur van de gegevens voldoen aan een bestaand schema van het Experience Data Model (XDM). Afhankelijk van de ingewikkeldheid van het schema voor een bepaalde dataset, kan het moeilijk zijn om de nauwkeurige vorm van de gegevens te bepalen die de dataset op opneming verwacht.

Voor elk schema dat u in de gebruikersinterface van Experience Platform definieert, kunt u een voorbeeld-JSON-object genereren dat voldoet aan de structuur van het schema. Dit voorwerp kan als malplaatje voor om het even welke gegevens dienen die in datasets worden opgenomen die het betrokken schema in dienst nemen.

Selecteer **[!UICONTROL Schemas]** in de gebruikersinterface van Experience Platform in de linkernavigatie. Zoek onder het tabblad **[!UICONTROL Browse]** het schema waarvoor u voorbeeldgegevens wilt genereren. Selecteer het uit de lijst, en de juiste spoorupdates om details over het schema te tonen. Selecteer **[!UICONTROL Download sample file]** van hier.

![&#x200B; het Browse lusje van de werkruimte van Schema&#39;s met een geselecteerd schema en benadrukt dossier van de downloadsteekproef.](../images/ui/sample/sample-data.png)

Een voorbeeld-JSON-bestand wordt gedownload door de browser. U kunt dit dossier nu als verwijzing voor gebruiken hoe te om uw gegevens te structureren wanneer het opnemen in datasets die dit schema gebruiken.

## Volgende stappen

Deze handleiding besprak hoe u een voorbeeld-JSON-bestand kunt genereren op basis van een XDM-schema in de gebruikersinterface van Experience Platform. Leren hoe te om steekproefgegevens te produceren gebruikend de Registratie API van het Schema, zie de [&#x200B; gids van het het eindpunt van steekproefgegevens &#x200B;](../api/sample-data.md).

Zodra u bereid bent om gegevens in te voeren, zie het leerprogramma op [&#x200B; in kaart brengen een Csv- dossier aan XDM &#x200B;](../../ingestion/tutorials/map-csv/overview.md) om te leren hoe te om een vlak gegevensdossier (zoals CSV) aan een XDM- schema in kaart te brengen en het in Experience Platform in te voeren. Alternatief, kunt u a [&#x200B; bronverbinding &#x200B;](../../sources/home.md) vestigen om uw gegevens van een externe bron in te brengen en het in kaart te brengen aan XDM.

Voor meer informatie over de mogelijkheden van de [!UICONTROL Schemas] werkruimte in UI, verwijs naar het [[!UICONTROL Schemas] overzicht van de werkruimte &#x200B;](./overview.md).

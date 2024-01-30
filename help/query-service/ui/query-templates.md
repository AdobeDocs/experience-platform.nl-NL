---
title: Query-sjablonen
description: Zoeksjablonen zijn herbruikbare opgeslagen SQL-query's die andere gebruikers opnieuw kunnen gebruiken om tijd en moeite te besparen. Zij kunnen worden gecreeerd gebruikend de Redacteur van de Vraag of de Dienst API van de Vraag en zijn beschikbaar voor gebruik op alle datasets van het Experience Platform.
exl-id: e74d058f-bb89-45ed-83cc-2e3a33401270
source-git-commit: 1a44be939a4678078b414658199472e07dee153b
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---

# Query-sjablonen

Met Adobe Experience Platform Query Service kunt u SQL-code opslaan en opnieuw gebruiken in de vorm van querysjablonen. De malplaatjes sparen inspanning door de herhaling van algemeen uitgevoerde taken te vermijden. U kunt sjablonen delen binnen uw organisatie en eenvoudig de querywaarden wijzigen zonder dat u toegang hoeft te krijgen tot de onderliggende SQL.

Dit document verstrekt de informatie die wordt vereist om vraagmalplaatjes in de Dienst van de Vraag tot stand te brengen.

## Vereisten

U moet beschikken over [!UICONTROL Manage queries] Toestemming die wordt toegelaten om tot de Redacteur van de Vraag toegang te hebben en het vraagdashboard binnen het Platform UI te bekijken. De toestemming wordt toegelaten door de Adobe [Admin Console](https://adminconsole.adobe.com/). Neem contact op met de beheerder van uw organisatie als u geen beheerdersrechten hebt om deze machtiging in te schakelen. Zie de documentatie van het toegangsbeheer voor [volledige instructies over het toevoegen van toestemmingen door Admin Console](../../access-control/home.md).

## Een querysjabloon maken

U kunt vraagmalplaatjes door twee methodes tot stand brengen, of door een verzoek van de POST aan de Dienst API van de Vraag te doen `query-templates` eindpunt, of door het schrijven, het noemen, en het bewaren van een vraag door de Redacteur van de Vraag.

### Gebruik de Redacteur van de Vraag om een vraag te ontwerpen en als malplaatje op te slaan

Zie de documentatie voor instructies op hoe te om de Redacteur van de Vraag te gebruiken aan [schrijven](./user-guide.md#query-authoring) en [query&#39;s opslaan](./user-guide.md#saving-queries). Nadat u een naam hebt gegeven aan de query en de query hebt opgeslagen, kunt u deze opnieuw gebruiken als een querysjabloon in het menu [!UICONTROL Templates] tab.

>[!TIP]
>
>Als u een query opslaat in de Query Editor, verschijnt er een bevestigingsbericht om u op de hoogte te brengen van de geslaagde actie. Dit popup bericht bevat een verbinding die een geschikte manier verstrekt om aan de vragen te navigeren die werkruimte plannen. Zie de [documentatie met planningquery&#39;s](./query-schedules.md) om te leren hoe vragen op een douanecadence in werking te stellen.

## Zoeksjablonen zoeken {#browse}

Selecteer in de werkruimte Query&#39;s van de gebruikersinterface van het platform de optie **[!UICONTROL Templates]** om de lijst met beschikbare opgeslagen query&#39;s weer te geven.

![De zoekwerkruimte met het tabblad Sjablonen gemarkeerd.](../images/ui/query-templates/query-templates.png)

Als u relevante sjabloongegevens wilt zoeken, selecteert u een querysjabloon in de lijst die beschikbaar is om het deelvenster Details te openen.

![Het detailpaneel in de zoekwerkruimte met de query-id gemarkeerd.](../images/ui/query-templates/details-panel.png)

In het deelvenster Details kunt u de volgende handelingen uitvoeren:

* Selecteren **[!UICONTROL Run as CTAS]** om een nieuwe tabel te maken door gegevens te selecteren uit een bestaande tabel of tabellen. Deze optie is alleen beschikbaar als u een SELECT-query hebt.
* Selecteren **[!UICONTROL Add schedule]** om met het uitgeven van uw programma voor uw vraagmalplaatje te beginnen.
* Selecteren **[!UICONTROL View schedule]** om naar de [!UICONTROL Schedules] tabblad van de Query-editor. Deze mening bevat om het even welke planningsinformatie verbonden aan de vraag.
* Selecteren **[!UICONTROL Delete query]** de sjabloon verwijderen.
* Selecteer de sjabloonnaam om naar de Query Editor te navigeren waar de SQL al is ingevuld voor bewerking.

### Gebruik de API van de Dienst van de Vraag om een malplaatje te creëren

Zie de documentatie voor instructies op [hoe te om een vraagmalplaatje te maken](../api/query-templates.md#create-a-query-template) met de API van de Query-service. De details voor een onlangs gecreeerd vraagmalplaatje zijn bevat in het reactievermogen.

>[!NOTE]
>
>Sjablonen die zijn gemaakt met de API zijn ook zichtbaar op het tabblad Sjablonen voor de query-service van het platform.

## Volgende stappen

Door dit document te lezen, hebt u nu een beter inzicht in hoe te om vraagmalplaatjes in de Dienst van de Vraag tot stand te brengen. Zie de [Overzicht van gebruikersinterface](./overview.md)of de [API-handleiding voor query-service](../api/getting-started.md) om meer over de mogelijkheden van de Dienst van de Vraag te leren.

Zie de [de geplande gids van het vraageindpunt](../api/scheduled-queries.md) om te leren hoe te vragen plannen gebruikend API, of [Handleiding voor Query-editor](./user-guide.md#scheduled-queries) voor de gebruikersinterface.

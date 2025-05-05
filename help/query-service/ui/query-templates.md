---
title: Query-sjablonen
description: Zoeksjablonen zijn herbruikbare opgeslagen SQL-query's die andere gebruikers opnieuw kunnen gebruiken om tijd en moeite te besparen. Zij kunnen worden gecreeerd gebruikend de Redacteur van de Vraag of de Dienst API van de Vraag en zijn beschikbaar voor gebruik op alle datasets van Experience Platform.
exl-id: e74d058f-bb89-45ed-83cc-2e3a33401270
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---

# Query-sjablonen

Met Adobe Experience Platform Query Service kunt u SQL-code opslaan en opnieuw gebruiken in de vorm van querysjablonen. De malplaatjes sparen inspanning door de herhaling van algemeen uitgevoerde taken te vermijden. U kunt sjablonen delen binnen uw organisatie en eenvoudig de querywaarden wijzigen zonder dat u toegang hoeft te krijgen tot de onderliggende SQL.

Dit document verstrekt de informatie die wordt vereist om vraagmalplaatjes in de Dienst van de Vraag tot stand te brengen.

## Vereisten

U moet [!UICONTROL Manage queries] toestemming hebben om tot de Redacteur van de Vraag toegang te hebben en het dashboard van vragen binnen Experience Platform UI te bekijken. De toestemming wordt toegelaten door Adobe [ Admin Console ](https://adminconsole.adobe.com/). Neem contact op met de beheerder van uw organisatie als u geen beheerdersrechten hebt om deze machtiging in te schakelen. Zie de documentatie van de toegangscontrole voor [ volledige instructies bij het toevoegen van toestemmingen door Admin Console ](../../access-control/home.md).

## Een querysjabloon maken

U kunt vraagmalplaatjes door twee methodes tot stand brengen, of door een POST- verzoek aan het eindpunt van de Dienst van de Vraag te doen API `query-templates`, of door te schrijven, een naam te geven, en een vraag door de Redacteur van de Vraag te bewaren.

### Gebruik de Redacteur van de Vraag om een vraag te ontwerpen en als malplaatje op te slaan

Zie de documentatie voor instructies op hoe te om de Redacteur van de Vraag te gebruiken [&#128279;](./user-guide.md#query-authoring) schrijven en [ sparen vragen ](./user-guide.md#saving-queries). Nadat u een naam hebt gegeven aan de query en deze hebt opgeslagen, kunt u deze opnieuw gebruiken als een querysjabloon op het tabblad [!UICONTROL Templates] .

>[!TIP]
>
>Als u een query opslaat in de Query Editor, verschijnt er een bevestigingsbericht om u op de hoogte te brengen van de geslaagde actie. Dit popup bericht bevat een verbinding die een geschikte manier verstrekt om aan de vragen te navigeren die werkruimte plannen. Zie de [ documentatie van planningsvragen ](./query-schedules.md) leren hoe te om vragen op een douanecadence in werking te stellen.

## Zoeksjablonen zoeken {#browse}

Selecteer **[!UICONTROL Templates]** in de werkruimte Query&#39;s van de gebruikersinterface van Experience Platform om de lijst met beschikbare opgeslagen query&#39;s weer te geven.

![ de werkruimte van vragen met het benadrukte lusje van Malplaatjes.](../images/ui/query-templates/query-templates.png)

Als u relevante sjabloongegevens wilt zoeken, selecteert u een querysjabloon in de lijst die beschikbaar is om het deelvenster Details te openen.

![ het detailspaneel in de vraagwerkruimte met benadrukte vraagidentiteitskaart.](../images/ui/query-templates/details-panel.png)

In het deelvenster Details kunt u de volgende handelingen uitvoeren:

* Selecteer **[!UICONTROL Run as CTAS]** om een nieuwe tabel te maken door gegevens te selecteren uit een bestaande tabel of tabellen. Deze optie is alleen beschikbaar als u een SELECT-query hebt.
* Selecteer **[!UICONTROL Add schedule]** om te beginnen met het uitgeven van uw programma voor uw vraagmalplaatje.
* Selecteer **[!UICONTROL View schedule]** om naar het tabblad [!UICONTROL Schedules] van de Query-editor te navigeren. Deze mening bevat om het even welke planningsinformatie verbonden aan de vraag.
* Selecteer **[!UICONTROL Delete query]** om de sjabloon te verwijderen.
* Selecteer de sjabloonnaam om naar de Query Editor te navigeren waar de SQL al is ingevuld voor bewerking.

### Gebruik de API van de Dienst van de Vraag om een malplaatje te creëren

Zie de documentatie voor instructies op [ hoe te om een vraagmalplaatje ](../api/query-templates.md#create-a-query-template) te maken gebruikend de Dienst API van de Vraag. De details voor een onlangs gecreeerd vraagmalplaatje zijn bevat in het reactievermogen.

>[!NOTE]
>
>Sjablonen die zijn gemaakt met de API zijn ook zichtbaar op het tabblad Sjablonen voor zoekopdrachten in de gebruikersinterface van Experience Platform.

## Volgende stappen

Door dit document te lezen, hebt u nu een beter inzicht in hoe te om vraagmalplaatjes in de Dienst van de Vraag tot stand te brengen. Zie het [ overzicht UI ](./overview.md), of de [ gids van de Dienst API van de Vraag ](../api/getting-started.md) om meer over de mogelijkheden van de Dienst van de Vraag te leren.

Zie de [ geplande gids van het vraageindpunt ](../api/scheduled-queries.md) leren hoe te vragen gebruikend API, of de [ gids van de Redacteur van de Vraag ](./user-guide.md#scheduled-queries) voor UI te plannen.

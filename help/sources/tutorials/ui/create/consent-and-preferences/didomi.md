---
title: Connect Didomi naar Experience Platform
description: Leer hoe u uw Didomi-account met Experience Platform kunt verbinden via de gebruikersinterface.
hide: true
hidefromtoc: true
source-git-commit: 44c01678e96f2649dbf731dd4531004c1df28058
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 0%

---

# Verbinden [!DNL Didomi] met Experience Platform

Lees deze handleiding voor informatie over hoe u uw [!DNL Didomi] -account kunt verbinden met Adobe Experience Platform via de werkruimte voor bronnen in de gebruikersinterface.

>[!IMPORTANT]
>
>* Deze documentatiepagina werd gecreeerd door het *Didomi* team. Voor om het even welke onderzoeken of updateverzoeken, gelieve hen direct in *support@didomi.io* te contacteren.
>* Voor geleidelijke instructies bij het produceren van de verbinding, verwijs naar de [ Didomi Adobe bronschakelaardocumentatie ](https://developers.didomi.io/integrations/third-party-apps/preference-management-platform-integrations/Adobe-source-connector).

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

### Uw [!DNL Didomi] -account instellen

Alvorens u kunt te werk gaan, zorg ervoor dat u de in de eerste plaats vereiste stappen leest en voltooit die in het [[!DNL Didomi]  overzicht ](../../../../connectors/consent-and-preferences/didomi.md#prerequisites) worden geschetst om uw rekening met Experience Platform met succes te verbinden.

## Navigeren door de catalogus met bronnen

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van *[!UICONTROL Sources]* . Kies een categorie of gebruik de zoekbalk om de bron te zoeken.

Als u verbinding wilt maken met [!DNL Didomi] , gaat u naar de categorie *[!UICONTROL Databases]* , selecteert u de **[!UICONTROL Didomi]** bronkaart en selecteert u vervolgens **[!UICONTROL Set up]** .

>[!TIP]
>
>Bronnen in de catalogus met bronnen geven de optie **[!UICONTROL Set up]** weer wanneer een bepaalde bron nog geen geverifieerde account heeft. Zodra een geverifieerd account is gemaakt, verandert deze optie in **[!UICONTROL Add data]** .

![ bron-schakelaar-lijst ](../../../../images/tutorials/create/didomi/source-connector-list.png)

## Het schema voor brongegevens toevoegen

Daarna, gebruik de *[!UICONTROL Select data]* interface om het JSON- dossier te uploaden dat [ in de eerste vereiste stappen ](../../../../connectors/consent-and-preferences/didomi.md#download-the-sample-payload-file) werd gedownload.

U kunt de voorvertoningsinterface gebruiken om de bestandsstructuur van de laadbewerking weer te geven. Selecteer **[!UICONTROL Next]** als u klaar bent.

![ toe:voegen-gegeven-schema ](../../../../images/tutorials/create/didomi/add-data-schema.png)

## Gegevens over gegevensstroom opgeven

Daarna, moet u informatie betreffende uw dataset en uw gegevensstroom verstrekken.

### Gegevens over gegevensset

Een dataset is een opslag en beheersconstructie voor een inzameling van gegevens, typisch een lijst, die een schema (kolommen) en gebieden (rijen) bevat. De gegevens die met succes in Experience Platform worden opgenomen worden voortgeduurd binnen het gegevensmeer als datasets.

Tijdens deze stap, kunt u of een bestaande dataset gebruiken of een nieuwe dataset creëren.

>[!NOTE]
>
>Ongeacht of u een bestaande dataset gebruikt of een nieuwe dataset creeert, moet u ervoor zorgen dat uw dataset **voor de opname van het Profiel** wordt toegelaten.

+++Selecteer voor stappen om de opname van het Profiel, de diagnostiek van de fout, en gedeeltelijke opname toe te laten.

Als uw dataset voor het Profiel van de Klant in real time wordt toegelaten, dan tijdens deze stap, kunt u **[!UICONTROL Profile dataset]** van een knevel voorzien om uw gegevens voor Profiel-opname toe te laten. U kunt deze stap ook gebruiken om **[!UICONTROL Error diagnostics]** en **[!UICONTROL Partial ingestion]** in te schakelen.

* **[!UICONTROL Error diagnostics]**: Selecteer **[!UICONTROL Error diagnostics]** om de bron de instructie te geven foutdiagnostiek te produceren waarnaar u later kunt verwijzen bij het controleren van de gegevenssetactiviteit en de status van de gegevensstroom.
* **[!UICONTROL Partial ingestion]**: Gedeeltelijke batch-opname is de mogelijkheid om gegevens met fouten in te voeren tot een bepaalde configureerbare drempel. Met deze functie kunt u al uw nauwkeurige gegevens in Experience Platform opnemen, terwijl al uw onjuiste gegevens afzonderlijk worden opgeslagen met informatie over waarom deze niet geldig zijn.

+++

### Gegevens gegevensstroom

Zodra uw dataset wordt gevormd, moet u details op uw gegevensstroom, met inbegrip van een naam, een facultatieve beschrijving, en waakzame configuraties dan verstrekken.

![ dataflow-details ](../../../../images/tutorials/create/didomi/dataflow-details.png)

| Dataflow-configuraties | Beschrijving |
| --- | --- |
| Naam gegevensstroom | De naam van de gegevensstroom.  Standaard wordt hiervoor de naam gebruikt van het bestand dat wordt geïmporteerd. |
| Beschrijving | (Optioneel) Een korte beschrijving van uw gegevensstroom. |
| Waarschuwingen | Experience Platform kan op gebeurtenissen gebaseerde waarschuwingen produceren waarop gebruikers zich kunnen abonneren. Deze opties zijn allemaal een doorlopende gegevensstroom om deze waarschuwingen te activeren.  Voor meer informatie, lees het [ alarm overzicht ](../../alerts.md) <ul><li>**het Begin van de Looppas van Bronnen Dataflow**: Selecteer dit alarm om een bericht te ontvangen wanneer uw dataflow looppas begint.</li><li>**Bronnen Dataflow de Succes van de Looppas**: Selecteer dit alarm om een bericht te ontvangen als uw dataflow zonder enige fouten beëindigt.</li><li>**de Uitval van de Looppas van Gegevensstroom van Bronnen**: Selecteer dit alarm om een bericht te ontvangen als uw dataflow looppas met om het even welke fouten beëindigt.</li></ul> |

{style="table-layout:auto"}

## Toewijzing

Gebruik de toewijzingsinterface om uw brongegevens toe te wijzen aan de aangewezen schemagebieden alvorens gegevens aan Experience Platform in te voeren.  Voor meer informatie, lees de [ kaartgids in UI ](../../../../../data-prep/ui/mapping.md)

De afbeelding wordt specifiek gebruikt om **doelgegevens** van [!DNL Didomi] in de dataset van Experience Platform over te brengen. Deze doelen vertegenwoordigen de keuze van de gebruiker voor toestemming (zoals voor analyses, personalisatie, reclame, enz.) en zijn de enige aanvaarde kaartvelden in deze integratie.

Gebruik de [ gedownloade steekproef WebHaaklading ](../../../../connectors/consent-and-preferences/didomi.md#download-the-sample-payload-file) van de [!DNL Didomi] WebHaak montages om elk [!DNL Didomi] doel aan de aangewezen gebieden in uw dataset van Adobe in kaart te brengen.

Selecteer **[!UICONTROL Next]** als u klaar bent.

![ afbeelding-details ](../../../../images/tutorials/create/didomi/mapping-details.png)

## Controleren

De stap *[!UICONTROL Review]* wordt weergegeven, zodat u de details van de gegevensstroom kunt bekijken voordat deze wordt gemaakt. De details zijn groep binnen de volgende categorieën:

* **[!UICONTROL Connection]**: geeft de accountnaam, het bronplatform en de bronnaam weer.
* **[!UICONTROL Assign dataset and map fields]**: toont de doeldataset en het schema dat de dataset volgt.

Selecteer **[!UICONTROL Finish]** nadat u hebt bevestigd dat de details juist zijn.

## De URL van het streamingeindpunt ophalen

Als de verbinding is gemaakt, wordt de pagina met brondetails weergegeven. Deze pagina bevat details van de zojuist gemaakte verbinding, waaronder eerder uitgevoerde dataflows, ID en URL van het streamingeindpunt.

## De configuratie op Adobe voltooien

Nadat u de gegevensstroom hebt gemaakt, navigeert u naar de catalogus *[!UICONTROL Sources]* en selecteert u **[!UICONTROL Dataflows]** . Gebruik de gegevensstroommap om de [!DNL Didomi] -gegevensstroom te zoeken en toegang te krijgen tot de *[!UICONTROL Dataflow activity]* -interface. Gebruik vervolgens het deelvenster *[!UICONTROL Properties]* in de rechtertrack en haalt u waarden op voor het volgende:

* [!UICONTROL Streaming endpoint]
* [!UICONTROL Dataflow ID]

In de gebruikersinterface van Experience Platform:

1. Na de voltooiing van de configuratie, herzie de configuratieparameters die van de aanvankelijke WebHaak opstelling ontbraken.
2. Als deze waarden beschikbaar zijn, gaat u terug naar Didomi en werkt u de webshconfiguratie bij.

![ configuratie-geklaard ](../../../../images/tutorials/create/didomi/configuration-done.png)

## Werk de Configuratie Webhaak bij

Zodra uw configuratie volledig is, navigeer terug naar de [!DNL Didomi] console en werk uw webhaconfiguratie met uw **het stromen eindpunt URL** en **dataflow identiteitskaart** bij.

Zodra dit volledig is, [!DNL Didomi] zal beginnen verzendend toestemmingsbeheer en voorkeur beheersgebeurtenissen door de integratie, en de gegevens zullen in uw dataset van Adobe worden opgeslagen.

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een gegevensstroom gemaakt om batchgegevens van uw [!DNL Didomi] -bron naar Experience Platform te verzenden. Voor extra bronnen raadpleegt u de documentatie die hieronder wordt beschreven.

### Uw gegevensstroom controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over innamesnelheden, succes, en fouten te bekijken. Voor meer informatie over hoe te om dataflow te controleren, bezoek het leerprogramma op [ controlerekeningen en dataflows in UI ](../../../../../dataflows/ui/monitor-sources.md).

### Uw gegevensstroom bijwerken

Om configuraties voor uw dataflows bij te werken die, afbeelding, en algemene informatie plannen, bezoek het leerprogramma op [ bijwerken brondataflows in UI ](../../update-dataflows.md).

### Uw gegevensstroom verwijderen

U kunt gegevensstromen verwijderen die niet meer nodig zijn of die onjuist zijn gemaakt met de functie **[!UICONTROL Delete]** die beschikbaar is in de **[!UICONTROL Dataflows]** -werkruimte. Voor meer informatie over hoe te om dataflows te schrappen, bezoek het leerprogramma bij [ het schrappen van dataflows in UI ](../../delete.md).
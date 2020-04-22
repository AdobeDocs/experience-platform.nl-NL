---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een Adobe Analytics-bronconnector maken in de gebruikersinterface
topic: overview
translation-type: tm+mt
source-git-commit: ac1e5dbe435d9e85e8ce3ad90c60dd31ba9248ff

---


# Een Adobe Analytics-bronconnector maken in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een Adobe Analytics-bronconnector in de gebruikersinterface om consumentengegevens over te brengen naar het Adobe Experience Platform.

## Een bronverbinding maken met Adobe Analytics

Meld u aan bij <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> en selecteer vervolgens **Bronnen** in de linkernavigatiebalk voor toegang tot de werkruimte Bronnen. In het scherm *Catalogus* worden beschikbare bronnen weergegeven om ingebouwde verbindingen te maken met. Elke bron toont het aantal bestaande verbindingen dat aan deze verbindingen is gekoppeld. Selecteer de optie voor **Adobe Analytics** en klik vervolgens op **Bron** weergeven om alle gevestigde interne verbindingen met de bron weer te geven.

![](../../../../images/tutorials/create/analytics/AA-sources_catalog.png)

In het scherm *Bronactiviteit* worden alle eerder ingestelde verbindingen met Adobe Analytics weergegeven. U kunt een nieuwe verbinding maken door op Gegevens **** selecteren te klikken.

>[!NOTE] Er kunnen meerdere interne verbindingen met een bron worden gemaakt om verschillende gegevens in te voeren.

![](/help/sources/images/tutorials/create/analytics/AA-source_activity.png)

Van de lijst van beschikbare rapportreeksen, selecteer één u in Platform wilt brengen en **daarna** klikken.

>[!NOTE] Per analytische bronverbinding kan slechts één rapportsuite worden geselecteerd. Bovendien kan slechts één rapportsuite bestaan in één sandbox.

![](../../../../images/tutorials/create/analytics/AA-select_data.png)

De stap *Revisie* wordt weergegeven, zodat u de nieuwe geïntegreerde verbinding voor Analytics kunt controleren voordat deze wordt gemaakt. De details van de verbinding worden gegroepeerd per categorieën, die omvatten:

* *Brongegevens*: Toont het type van de bronverbinding en de geselecteerde rapportreeks.
* *Doelgegevens*: Wanneer het creëren van andere bronschakelaars, toont deze container welke dataset de brongegevens opnemen in, met inbegrip van het schema de dataset zich aan houdt. De analysegegevens worden automatisch in kaart gebracht en in Profielen van de Klant in real time opgenomen.

![](../../../../images/tutorials/create/analytics/AA-review.png)

## Volgende stappen

Zodra de verbinding wordt gecreeerd, wordt een doelschema en een dataset automatisch gecreeerd om de inkomende gegevens te bevatten. Bovendien vindt de terugvulling van gegevens plaats en neemt deze tot 13 maanden aan historische gegevens in. Als de eerste opname is voltooid, worden de analysegegevens gebruikt door de services van het downstream Platform, zoals Real-time klantprofiel en Segmenteringsservice. Raadpleeg de volgende documenten voor meer informatie:

* [Overzicht van het realtime klantprofiel](../../../../../profile/home.md)
* [Overzicht van segmentatieservice](../../../../../segmentation/home.md)
* [Overzicht van de Data Science Workspace](../../../../../data-science-workspace/home.md)
* [Overzicht van Query Service](../../../../../query-service/home.md)


---
title: AI Assistant (verouderd) in Adobe Experience Platform - Overzicht
description: Leer meer over AI Assistant (verouderd), de nuances en gebruiksgevallen en hoe u deze kunt gebruiken om uw workflow met Adobe Experience Platform en Real-Time Customer Data Platform te versnellen.
exl-id: cfd4ac22-fff3-4b50-bbc2-85b6328f603c
source-git-commit: 68c55e370cab58ce5c93359520bf4ce671282a1b
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 2%

---

# AI Assistant (verouderd) in Adobe Experience Platform

>[!IMPORTANT]
>
>Dit document is van toepassing op AI Assistant (verouderd). Voor informatie over AI Medewerker (volgende-Gen), lees de [ AI HulpUI gids ](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/ai-assistant/ai-assistant-ui) in [ AI in Experience Cloud ](https://experienceleague.adobe.com/nl/docs/experience-cloud-ai/experience-cloud-ai/home) documentatie.

Raadpleeg de volgende tabel voor een vergelijking van AI Assistant (Legacy) en AI Assistant (Next-Gen):

| Functiegebied | AI Assistant (verouderd) | AI-assistent (Next-Gen) |
| --- | --- | --- |
| Gebruikerservaring | AI Assistant (verouderd) is alleen beschikbaar in een panel voor rechtse spoorwegsystemen. | AI Assistant (Next-Gen) is zowel beschikbaar in het rechterdeelvenster als in een indrukwekkende ervaring op volledig scherm. |
| Toepassingsgebied van de mogelijkheden | U kunt AI Assistant (Verouderd) gebruiken voor zowel productkennis als operationele inzichten. | U kunt de Medewerker van AI (Next-Gen) voor productkennis, operationele inzichten, evenals geavanceerde agentische vaardigheden en multi-step taakuitvoering gebruiken. |
| Platformarchitectuur | AI Assistant (Verouderd) is niet op de Agent Orchestrator-stapel gebaseerd. | De Medewerker van AI (Volgende-Gen) wordt aangedreven door [ Adobe Experience Platform Agent Orchestrator ](https://experienceleague.adobe.com/nl/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator), toelatend rekbaarheid en geavanceerde coördinatie over mogelijkheden. |
| Toepassingsdekking | AI Assistant (Legacy) is een toepassingsspecifieke implementatie. | U kunt AI Assistant (Next-Gen) gebruiken voor een uniforme AI Assistant-ervaring in alle Adobe Experience Cloud-toepassingen. |
| Toegangsmodel en machtigingsmodel | Toepassingsbereik toegangsmodel uitgelijnd op individuele productgrenzen. | Alle gebruikers krijgen toegang tot AI Assistant (Next-Gen) en bijbehorende Experience Platform-agents. **Nota**: <ul><li>**Adobe Experience Manager**: Uw beheerder moet u de toestemming verlenen om tot Medewerker (Volgende-Gen) door [ Adobe Admin Console ](https://helpx.adobe.com/nl/enterprise/using/admin-console.html) toegang te hebben.</li><li>**Customer Journey Analytics**: Uw beheerder moet u de toestemming verlenen om tot AI Medewerker door [ het Toegangsbeheer van Customer Journey Analytics ](https://experienceleague.adobe.com/en/docs/analytics-platform/using/technotes/access-control?lang=en) toegang te hebben. Hierdoor kunt u vragen stellen over productkennis en gegevensinzichten. |

De volgende video is bedoeld als ondersteuning voor uw begrip van AI Assistant.

>[!VIDEO](https://video.tv.adobe.com/v/3429845?learn=on)

Lees dit document voor meer informatie over AI Assistant (Legacy) in Adobe Experience Platform.

AI Assistant (verouderd) in Adobe Experience Platform is een belevenis die u kunt gebruiken om uw workflows in Adobe-toepassingen te versnellen. U kunt de Medewerker van AI (Verouderd) gebruiken om productkennis beter te begrijpen, problemen op te lossen, of door informatie te zoeken en operationele inzichten te vinden. AI Assistant (verouderd) ondersteunt Experience Platform, Real-Time Customer Data Platform, Adobe Journey Optimizer en Customer Journey Analytics.

![ de AI Hulp interface met de eerste getriggerde gebruikerservaring.](./images/ai-assistant-full.png)

>[!IMPORTANT]
>
>U moet met a [ gebruikersovereenkomst ](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html) akkoord gaan alvorens u AI Medewerker (Verouderd) kunt gebruiken. De gebruikersovereenkomst bevat ook de openbare bètaovereenkomst. Op deze manier kunt u extra AI Assistant-functies (verouderd) gebruiken wanneer deze in bètacapaciteit worden geïmplementeerd.

+++Selecteren om interface voor gebruikersovereenkomst weer te geven

![ de eerste pagina van de gebruikersovereenkomst.](./images/user-agreement-1.png)

![ De laatste pagina van de gebruikersovereenkomst.](./images/user-agreement-2.png)

+++

## AI-assistent begrijpen {#understanding-ai-assistant}

De Medewerker van AI (Verouderd) antwoordt aan uw voorgelegde vragen door een gegevensbestand te vragen en dan gegevens van het gegevensbestand in een leesbaar antwoord te vertalen.

Deze interne representatie van onderliggende gegevens wordt ook wel **[!DNL Knowledge Graph]** genoemd. Dit is een uitgebreid web van concepten, gegevens en metagegevens voor een bepaald antwoord.

De [!DNL Knowledge Graph] bestaat uit subgrafieken waarnaar wordt verwezen wanneer query&#39;s worden verzonden:

* Operationele inzichten van de klant.
* Operationele inzichten van de klant in verschillende meta-winkels.
* Experience League-documentatie.

Er zijn twee klassen vragen om te overwegen alvorens AI Medewerker (Verouderd) te vragen:

### Productkennis {#product-knowledge}

Productkennis verwijst naar concepten en onderwerpen die zijn gebaseerd op Experience League-documentatie. Vragen over productkennis kunnen nader worden omschreven in de volgende subgroepen:

| Productkennis | Voorbeelden |
| --- | --- |
| Aanbevolen lessen | <ul><li>Wat is het verschil tussen een identiteit en een primaire of buitenlandse sleutel?</li><li>Wat zijn lookalike doelgroepen?</li></ul> |
| Openbare detectie | <ul><li>Hoe kan ik deze dataset uitvoeren?</li><li>Zijn er regelingen voor klanten in de gezondheidszorg?</li></ul> |
| Problemen oplossen | <ul><li>Waarom kan ik geen schema inschakelen dat eigendom is van Adobe voor profiel?</li><li>Waarom kan ik een segment niet verwijderen?</li></ul> |

{style="table-layout:auto"}

Bekijk de volgende video voor aanvullende informatie over productkennis van AI Assistant (Legacy):

>[!VIDEO](https://video.tv.adobe.com/v/3438032/?learn=on)

### Operationele inzichten {#operational-insights}

De operationele inzichten verwijzen naar antwoorden AI Medewerker (Verouderd) produceert over uw meta- gegevensvoorwerpen (attributen, publiek, dataflows, datasets, bestemmingen, reizen, schema&#39;s, en bronnen), met inbegrip van tellingen, raadplegingen, en lijneffect. Er worden geen gegevens in de sandbox weergegeven.

* Hoeveel datasets heb ik?
* Hoeveel schemakenmerken zijn nooit gebruikt?
* Welk publiek is geactiveerd?

U kunt AI Assistant (verouderd) vragen stellen over uw operationele inzichten op de volgende domeinen:

| Domein | Ondersteunde metagegevens | Niet-ondersteunde metagegevens |
| --- | --- | --- |
| Attributen | <ul><li>Zoeken naar kenmerknaam</li><li>Kenmerk - schemaverhouding</li><li>Kenmerk - gegevenssetrelatie</li><li>Kenmerk - publieksrelatie</li><li>Kenmerk - bestemmingsverhouding</li></ul> | <ul><li>Kenmerkklasse</li><li>Audit</li><li>Vervalstatus</li><li>Labels</li><li>Waarde opgeslagen in kenmerken</li></ul> |
| Doelgroepen | <ul><li>Aantal deelnemers</li><li>Type publiek (streaming of batch)</li><li>Aanmaakdatum/wijzigingsdatum</li><li>Activeringsstatus</li><li>Aantal profielen</li><li>Soorten publiek dupliceren</li><li>Zoekopdracht naar definitie van publiek</li><li>Publiek - publieksrelatie</li><li>Publiek - kenmerkrelatie</li><li>Publiek - gegevenssetrelatie</li><li>Publiek - bestemmingsverhouding</li><li>Naam zoeken</li><li>Naam en id zoeken | <ul><li>Overlap door publiek</li><li>Activering publiek</li><li>Publiek - campagnerelaties</li><li>Audit</li><li>Maken/wijzigen</li><li>Labels</li><li>Profielkwalificatietendensen</li></ul> |
| Gegevensstromen | <ul><li>Aantal gegevensstromen</li><li>Status DataFlow</li><li>Dataflow - relatie gegevensset</li><li>Dataflow - bronrelatie</li></ul> | <ul><li>Maken/wijzigen</li><li>Dataflow-batch-relaties</li><li>Aantal hoogste profielen</li></ul> |
| Gegevenssets | <ul><li>Aantal gegevenssets</li><li>Status profiel inschakelen</li><li>Aanmaakdatum/wijzigingsdatum</li><li>Gegevensset - schema-relatie</li><li>Gegevensset - publieksrelatie</li><li>Gegevensset - kenmerkrelatie</li><li>Dataset - gegevensstroomrelatie</li><li>Gegevensgrootte</li><li>Aantal rijen</li><li>Naam zoeken </li><li>Naam en id zoeken</li></ul> | <ul><li>Audit</li><li>Gemaakt door</li><li>Gegevensset - batch-relatie</li><li>Maken en wijzigen van gegevensset</li><li>Aantal profielen</li><li>Waardezoekopdracht</li></ul> |
| Bestemmingen | <ul><li>Gevormde doelaantallen</li><li>Doel - publieksrelatie</li><li>Relatie doelkenmerk</li></ul> | <ul><li>Account ingesteld</li><li>Accountreferentie-informatie</li><li>Unieke profielen geactiveerd</li></ul> |
| Journeys | <ul><li>Aantal</li><li>Naam zoeken</li><li>Naam en id zoeken</li><li>Reisstatus</li><li>Status activering (publiek versus gebeurtenissen)</li><li>Aanmaakdatum/wijzigingsdatum</li><li>Herhalingsfrequentie</li></ul> | <ul><li>Attributen - reisrelaties</li><li>Audit</li><li>Maken/wijzigen</li><li>Gemaakt door</li><li>Gebeurtenissen</li><li>Reis - dataset</li><li>Reis - schema</li><li>Aanbiedingen</li><li>Profielkwalificatietendensen</li><li>Stapgebeurtenissen</li></ul> |
| Schema&#39;s | <ul><li>Schema aantallen</li><li>Aanmaakdatum/wijzigingsdatum</li><li>Schema - kenmerkrelatie</li><li>Schema - gegevenssetrelatie</li><li>Schema - publieksrelatie</li><li>Status profiel inschakelen</li><li>Naam zoeken</li><li>Naam en id zoeken</li></ul> | <ul><li>Audit</li><li>Maken/wijzigen</li><li>Gemaakt door</li><li>Veldgroepen</li><li>Identiteiten</li><li>Identiteitsnaamruimten</li><li>Labels</li><li>Aantal profielen</li></ul> |
| Bronnen | <ul><li>Rekentelling</li><li>Accountstatus</li><li>Actieve/inactieve gegevensstromen voor elke rekening</li><li>Source-connector - gegevensstroomrelatie</li><li>Source-account - gegevensstroomrelatie</li></ul> | <ul><li>Accountverificatiegegevens</li><li>Account ingesteld</li><li>Metrische gegevens over gegevensinvoer</li><li>Aantal profielen</li><li>Source - batch-relaties</li></ul> |

{style="table-layout:auto"}

Voor vragen over operationele inzichten weerspiegelen de antwoorden mogelijk niet de huidige status van de gebruikersinterface. De gegevens die deze vragen ondersteunen, worden om de 24 uur bijgewerkt. Zo worden wijzigingen die gebruikers overdag aanbrengen in Real-Time CDP gesynchroniseerd met de gegevensopslag &#39;s nachts, waarna ze &#39;s ochtends beschikbaar komen voor vragen van gebruikers. U moet zich aanmelden bij een sandbox voor informatie over specifieke gegevens die betrekking hebben op objecten.

Bekijk de volgende video voor aanvullende informatie over operationele inzichten van AI Assistant (Legacy):

>[!VIDEO](https://video.tv.adobe.com/v/3444031?learn=on&enablevpops)

### Functiebereik {#feature-scope}

Momenteel is het bereik van AI Assistant (Legacy) als volgt:

* [ de kennis van het Product ](./home.md#product-knowledge): De Medewerker van AI (Verouderd) kan de vragen van de productkennis voor Experience Platform, Real-Time Customer Data Platform en Adobe Journey Optimizer beantwoorden. U kunt ook onderwerpen over productkennis voor Customer Journey Analytics bespreken, maar alleen via de interface van Customer Journey Analytics.
* [ Operationele inzichten ](./home.md#operational-insights): U kunt AI Medewerker (Verouderd) met vragen over operationele inzichten op de volgende gegevensvoorwerpen vragen: attributen, publiek, dataflows, datasets, bestemmingen, reizen, schema&#39;s, en bronnen.

## Volgende stappen

Nu u een algemeen begrip van AI Medewerker (Verouderd) hebt, kunt u nu verdergaan en AI Medewerker (Verouderd) tijdens uw werkschema&#39;s gebruiken. Raadpleeg de volgende documentatie voor meer informatie:

* [Handleiding voor de gebruikersinterface van AI Assistant (verouderd)](./ui-guide.md)
* [Toegang tot functies](./access.md)
* [Vraag](./questions.md)
* [Privacy, beveiliging en bestuur in AI Assistant (verouderd)](./privacy.md)
* [Veelgestelde vragen](./faq.md)

---
title: Opmerkingen bij de release Experience Platform
description: Een voorvertoning van de meest recente releaseopmerkingen voor Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: b8c257ad9ab4e7ee085687f6c03cf55d7fb83ef0
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 37%

---

# Opmerkingen bij de release Adobe Experience Platform

>[!IMPORTANT]
>
>Dit document is voorgenomen als a **voorproef** van de versienota&#39;s voor de huidige maand. Release-items kunnen worden gewijzigd en worden toegevoegd of verwijderd in de definitieve versie.

>[!TIP]
>
>Raadpleeg de volgende documentatie voor aanvullende informatie voor andere Adobe Experience Platform-toepassingen:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/releases/latest)
>- [Samenstelling van Federated-doelgroep](https://experienceleague.adobe.com/nl/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/nl/docs/real-time-cdp-collaboration/using/latest)

**de datum van de Versie: Februari 2026**

Nieuwe functies en updates van bestaande functies in Adobe Experience Platform:

- [Agent Orchestrator](#agent-orchestrator)
- [Waarschuwingen](#alerts)
- [Dataverzameling](#data-collection)
- [Bestemmingen](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Queryservice](#query-service)
- [Bronnen](#sources)

## Agent Orchestrator {#agent-orchestrator}

Met Agent Orchestrator kunt u op AI gebaseerde agents maken en implementeren die workflows kunnen automatiseren en op meerdere kanalen met klanten kunnen communiceren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Data On-boarding Agent | Gebruik de Data On-boarding Agent om bronverbindingen te vormen, gegevenskwaliteit te bevestigen, semantische verrijking toe te passen, schema&#39;s te herzien en te bevestigen, en gegevensopname in werking te stellen. Volg stap voor stap werkschema&#39;s voor zowel B2C als B2B stromen, herzie verwachte output, en los gemeenschappelijke kwesties problemen op. |
| Data Distiller Agent | Met de Data Distiller Agent kunt u SQL-taken maken vanuit de natuurlijke taal, SQL-prestaties optimaliseren, herstellen van SQL-fouten, SQL-taken plannen en beheren en de taakstatus controleren. Lees handleidingen, vereiste machtigingen en richtlijnen voor het oplossen van problemen om aan de slag te gaan. |
| Gegevensverzamelingsagent | Gebruik de Agent van de Inzameling van Gegevens om in-context begeleiding voor complexe configuraties van de gegevensinzameling te krijgen en lijn, gebiedsdelen, en verhoudingen over uw voorwerpen van de gegevensinzameling door conversationele inzichten te onderzoeken. |

{style="table-layout:auto"}

Voor meer informatie, zie de [&#x200B; documentatie van Agent Orchestrator &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Waarschuwingen {#alerts}

Met Experience Platform kunt u zich aanmelden voor gebeurtenisgebaseerde waarschuwingen voor verschillende Experience Platform-activiteiten. U kunt zich aanmelden voor verschillende waarschuwingsregels via het tabblad [!UICONTROL Alerts] in de gebruikersinterface van Experience Platform, en u kunt ervoor kiezen waarschuwingsmeldingen te ontvangen in de gebruikersinterface zelf of via e-mailberichten.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| [!DNL Slack] integratie voor klantgerichte waarschuwingen | U kunt nu klantgerichte waarschuwingen naar [!DNL Slack] verzenden. Volg de stapsgewijze zelfstudie om de [!DNL Slack] -integratie in te stellen en waarschuwingsberichten rechtstreeks in uw [!DNL Slack] -werkruimte te ontvangen. |

{style="table-layout:auto"}

Voor meer informatie raadpleegt u het [[!DNL Observability Insights] overzicht](../observability/home.md).

## Dataverzameling {#data-collection}

Adobe Experience Platform Data Collection verstrekt een reeks technologieën die u toestaan om cliënt-zijgegevens van de klantenervaring te verzamelen en het te verzenden naar Adobe Experience Platform Edge Network en andere bestemmingen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Extensiebeheer Adobe Platform Tags | Met de nieuwe Extension Management-functie kunt u de extensies van uw organisatie uploaden, verpakken en vrijgeven voor ontwikkeling, privédistributie en openbare distributie. Zoek naar gedeelde privé uitbreidingen naast uw eigen uitbreidingen in de top-level bedrijfmening. Deze functie ondersteunt web-, edge- en mobiele extensies. |

{style="table-layout:auto"}

Voor meer informatie, lees de [&#x200B; documentatie van de Inzameling van Gegevens &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/collection/home).

## Bestemmingen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met bestemmingsplatforms waarmee gegevens uit Experience Platform naadloos kunnen worden geactiveerd. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte bestemmingen**

| Bestemming | Beschrijving |
| --- | --- |
| [!DNL Snowflake] Batch algemeen beschikbaar | De batchbestemming [!DNL Snowflake] is verplaatst naar de algemene beschikbaarheid. U kunt nu de kolom van identiteitskaart van het fusiebeleid in uw uitgevoerde gegevens naast bestaande kolommen zoals timestamp, toewijzingsattributen, en publiekslidmaatschap bekijken. |
| AES256 encryptiesteun voor [&#x200B; Amazon S3 &#x200B;](../destinations/catalog/cloud-storage/amazon-s3.md#destination-details) bestemmingen | U kunt nu AES256-codering configureren voor uw Amazon S3-export. Kies uit twee opties: <ul><li>**[!UICONTROL Default]**: Experience Platform codeert gegevens in rust met het standaardversleutelingsalgoritme dat op uw emmertje is ingesteld.</li><li>**[!UICONTROL SSE-S3/AES256]**: Experience Platform voegt de header `s3:x-amz-server-side-encryption": "AES256` toe aan het exporteren en versleutelt gegevens in rust met het algoritme AES256 wanneer het land in S3. **Deze optie neemt belangrijkheid over om het even welk standaardencryptiealgoritme u op uw S3 emmertje** vormt.</li></ul> |

{style="table-layout:auto"}

Voor meer informatie leest u het [overzicht van bestemmingen](../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die algemene structuren en definities (schema&#39;s) biedt voor gegevens die in Experience Platform worden geïmporteerd. Door de XDM-standaarden te hanteren, kunnen alle gegevens over de klantervaring worden opgenomen in een gemeenschappelijke weergave. Zo worden inzichten sneller en beter geïntegreerd verkregen. U kunt waardevolle inzichten verkrijgen uit klantacties, klantdoelgroepen definiëren via segmenten en klantkenmerken gebruiken voor personalisatiedoeleinden.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Organisatie en zoekfunctie voor schema-inventarisatie | De bladerpagina van het schema omvat nu verbeterde onderzoek en het filtreren, gealigneerde acties, en steun voor user-defined markeringen en omslagen. Deze updates maken het gemakkelijker om schema&#39;s over sandboxen te vinden, te organiseren en te beheren terwijl het verminderen van handmatige navigatie en onderhoud. |

Voor meer informatie raadpleegt u het [[!DNL XDM] overzicht](../xdm/home.md).

## Query-service {#query-service}

Met de Query-service kunt u standaard SQL gebruiken om query&#39;s uit te voeren op gegevens in Adobe Experience Platform [!DNL Data Lake]. U kunt willekeurige datasets van [!DNL Data Lake] combineren en de queryresultaten vastleggen als nieuwe dataset voor gebruik in rapportage, de werkruimte voor datawetenschappen, of voor opname in het Real-Time Customer Profile.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Data Distiller Annual compute reset date alignment (Limited Release) | De gegevens die Distiller jaarlijks verwerkt, worden nu opnieuw ingesteld op de inschrijvingsdatum van uw Data Distiller-contract, op basis van het tijdstip waarop de licentie werd aangeschaft of vernieuwd. Hierdoor wordt het gebruik van licenties afgestemd op de contractvoorwaarden en kan het zijn dat de gebruikswaarden eenmalig worden aangepast. |
| Distiller-sessiebeheer voor gegevens (beperkte release) | Als geautoriseerde beheerder kunt u via de gebruikersinterface de actieve Query Service- en Data Distiller-sessies binnen uw organisatie en sandbox weergeven en beheren. Gebruik sessiebeheer om inactieve sessies te identificeren en te beëindigen om capaciteit vrij te maken. De ingebouwde waarborgen verhinderen u om zittingen met actieve vragen te beëindigen. De eigenschap registreert alle uitzettingsacties voor controle en brengt betrokken gebruikers op de hoogte. U hebt **nodig beheert de Zittingen van de Vraag** toestemming om tot deze eigenschap toegang te hebben. |

{style="table-layout:auto"}

Voor meer informatie, lees het [&#x200B; overzicht van de Dienst van de Vraag &#x200B;](../query-service/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Nieuwe of bijgewerkte bronnen**

| Bron | Beschrijving |
| --- | --- |
| Ondersteuning voor Unity Catalog in [!DNL Databricks] bronconnector | De [!DNL Databricks] bronaansluiting ondersteunt nu de catalogus Eenheid. Lees de bijgewerkte [[!DNL Databricks]](../sources/connectors/databases/databricks.md) documentatie om te leren hoe te om de Catalogus van de Eenheid te gebruiken wanneer u uw bronverbinding vormt. |

{style="table-layout:auto"}

Voor meer informatie raadpleegt u het [overzicht van bronnen](../sources/home.md).

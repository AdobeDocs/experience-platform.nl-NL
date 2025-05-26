---
title: Aanvullende informatie voor Adobe Experience Platform mei 2025
description: Aanvullende informatie van mei 2025 voor Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: cf88ed1082085fac28553dcc7c7be27c517adb22
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 81%

---

# Aanvullende informatie voor Adobe Experience Platform

>[!TIP]
>
>Raadpleeg de volgende documentatie voor aanvullende informatie voor andere Adobe Experience Platform-toepassingen:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/releases/latest)
>- [Samenstelling van Federated-doelgroep](https://experienceleague.adobe.com/nl/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/nl/docs/real-time-cdp-collaboration/using/latest)

**Releasedatum: woensdag 20 mei 2025**

Updates van bestaande functies en documentatie in Adobe Experience Platform:

- [Catalogusservice](#catalog-service)
- [Gegevensvoorbereiding](#data-prep)
- [Bestemmingen](#destinations)
- [Identiteitsservice](#identity)
- [Query-service](#query-service)
- [Sandboxes](#sandboxes)
- [Segmentatieservice](#segmentation-service)
- [Bronnen](#sources)

## Catalogusservice {#catalog-service}

Catalogusservice is het systeem voor het vastleggen van de locatie en herkomst van gegevens binnen Adobe Experience Platform. Alle gegevens die in Experience Platform worden opgenomen, worden in een datalake opgeslagen als bestanden en mappen. De catalogus bevat daarentegen de metagegevens en beschrijvingen van die bestanden en mappen voor opzoek- en controledoeleinden.

| Functie | Beschrijving |
| --- | --- |
| Gegevensopslag optimaliseren met regels voor gegevensopslag op datasetniveau | Efficiënt gegevensopslag beheren met het beleid voor het bewaren van gegevens waarmee verouderde gegevens worden verwijderd op basis van het opgegeven tijdschema. <ul><li>**Datasetretentie**: bepaal datasetregels om verouderde gegevens uit het data lake en de profielopslag te verwijderen.</li><li>**Opslaginzichten**: monitor het gebruik en zorg voor naleving van licentierechten via inlinestatistieken.</li><li>**Verbeterde zichtbaarheid**: volg de activiteit van de dataset van opname tot verwijdering met verbeterde monitoring.</li><li>**Gestroomlijnd beheer**: krijg toegang tot bewaarinstellingen, monitoring, auditlogboekbestanden en inzichten in één uniform overzicht.</li></ul> Raadpleeg de handleiding over [regels voor datasetretentie](../../catalog/datasets/user-guide.md#data-retention-policy) voor meer informatie. |

{style="table-layout:auto"}

Voor meer informatie raadpleegt u het [overzicht van de Catalogus-service](../../catalog/home.md).

## Gegevensvoorbereiding {#data-prep}

Gebruik gegevensvoorbereiding om gegevens toe te wijzen, te transformeren en te valideren van en naar Experience-datamodel (XDM).

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor import- en exporttoewijzingen voor Adobe Analytics | U kunt nu toewijzingsmogelijkheden voor importeren en exporteren gebruiken voor de gegevens van uw Adobe Analytics-rapportsuite wanneer u de Adobe Analytics-bronconnector gebruikt. <br><br>Exporteer uw toewijzingen naar een CSV-bestand en configureer ze lokaal in een spreadsheet. U kunt uw bijgewerkte toewijzingen vervolgens naar Experience Platform importeren met de toewijzingsinterface in de gebruikersinterface. U kunt dit vermogen gebruiken om grote aantallen toewijzingen te configureren zonder dat u ze handmatig in de gebruikersinterface hoeft samen te stellen. Wanneer u een nieuwe gegevensstroom maakt, kunt u bovendien een kopie van uw toewijzingen rechtstreeks naar Experience Platform uploaden om uw workflow te versnellen. <br><br>Voor meer informatie raadpleegt u de handleiding over het [koppelen van Adobe Analytics aan Experience Platform](../../sources/tutorials/ui/create/adobe-applications/analytics.md).</br> |

{style="table-layout:auto"}

Voor meer informatie, raadpleegt u het [Overzicht van Gegevensvoorbereiding](../../data-prep/home.md).

## Bestemmingen {#destinations}

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functie | Beschrijving |
| --- | --- |
| ](../../destinations/catalog/social/facebook.md) verbetering en steun van de Aangepaste Publiek van Facebook voor adres-verwante herkenningstekens[ | Vanaf 23 mei 2025 en gedurende juni 2025 ziet u wellicht tijdelijk twee **[!DNL Facebook Custom Audience]** doelkaarten in de lijst met bestemmingen, voor maximaal een paar uur. Dit is het gevolg van een interne upgrade naar de service voor doelen en de ondersteuning van nieuwe velden voor betere doelgerichtheid en betere overeenkomsten met profielen op Facebook-eigenschappen. Voor details over de nieuwe adres-verwante gebieden, zie de [ gesteunde identiteiten ](#supported-identities) sectie. <br><br> als u een kaart geëtiketteerd **[!UICONTROL (New) Facebook Custom Audience]** ziet, gebruik deze kaart voor nieuwe stromen van activeringsgegevens. De bestaande gegevensstromen worden automatisch bijgewerkt, dus u hoeft niets te doen. Wijzigingen die u aanbrengt in bestaande gegevensstromen tijdens deze periode, blijven na de upgrade behouden. Zodra de upgrade is voltooid, wordt de naam van de **[!UICONTROL (New) Facebook Custom Audience]** -doelkaart gewijzigd in **[!DNL Facebook Custom Audience]** . <br><br> als u dataflows gebruikend de [ Dienst API van de Stroom ](https://developer.adobe.com/experience-platform-apis/references/destinations/) creeert, moet u uw [!DNL flow spec ID] en [!DNL connection spec ID] aan de volgende waarden bijwerken: <ul><li>Stroomspecificatie-ID: `bb181d00-58d7-41ba-9c15-9689fdc831d3`</li><li>Verbindingsspecificatie-ID: `c8b97383-2d65-4b7a-9913-db0fbfc71727`</li></ul> |
| Mobiele reclame-id steun voor de [ Klantovereenkomst van Google + Vertoning &amp; Video 360 ](../../destinations/catalog/advertising/google-customer-match-dv360.md#supported-identities) bestemming | U kunt publiek aan de [ Klantovereenkomst van Google nu activeren + Vertoning &amp; Video 360 ](../../destinations/catalog/advertising/google-customer-match-dv360.md#supported-identities) bestemming die op mobiele reclame IDs, zoals [!DNL GAID] en [!DNL IDFA] wordt gebaseerd. |
| Ondersteuning voor aanvullende identificatiegegevens voor [Google Customer Match](../../destinations/catalog/advertising/google-customer-match.md) | De Google Customer Match-bestemming ondersteunt nu het toewijzen van adresgerelateerde velden voor verbeterde afstemmingspercentages in het Google-platform. <br><br>Als u wilt dat Google het adres matcht, moet u alle vier de adresvelden in kaart brengen (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` en `address_info_postal_code`) en controleren of er in deze velden geen gegevens in de geëxporteerde profielen ontbreken. <br> Als een veld niet is toegewezen of als er gegevens ontbreken, matcht Google het adres niet. |
| De kolom voor het verlopen van accounts voor [Facebook](../../destinations/catalog/social/facebook.md)-verbindingen | U kunt de verloopdatums voor Facebook-accounttokens nu zien in de tabbladen [Verkennen](../../destinations/ui/destinations-workspace.md#browse) en [Accounts](../../destinations/ui/destinations-workspace.md#accounts). |
| Met API gemaakte datasets exporteren | U kunt met API gemaakte datasets nu exporteren. De eerdere beperking waarbij alleen in de gebruikersinterface gemaakte gegevenssets beschikbaar waren voor export, is opgeheven. Lees meer over [het exporteren van datasets](../../destinations/ui/export-datasets.md). |

{style="table-layout:auto"}

Voor meer informatie leest u het [overzicht van bestemmingen](../../destinations/home.md).

## Identiteitsservice {#identity}

Met Identity Service van Adobe Experience Platform krijgt u een uitgebreid beeld van uw klanten en hun gedrag door identiteiten op verschillende apparaten en systemen te koppelen, zodat u in real-time een impactvolle, persoonlijke digitale ervaring kunt bieden.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| [!DNL Identity Graph Linking Rules] | [!DNL Identity Graph Linking Rules] is nu algemeen beschikbaar. [!DNL Identity Graph Linking Rules] voorkomt &#39;grafieken samenvouwen&#39;, zodat duidelijke en nauwkeurige klantprofielen worden gebruikt voor gepersonaliseerde marketing in Experience Platform en toepassingen. Belangrijkste kenmerken zijn:<ul><li>[ Hulpmiddel van de Simulatie van de Grafiek ](../../identity-service/identity-graph-linking-rules/graph-simulation.md): Onderzoek het algoritme en test de Plaatsende configuraties van de Identiteit.</li><li> [ Montages van de Identiteit ](../../identity-service/identity-graph-linking-rules/identity-settings-ui.md): Vorm unieke namespaces en plaats prioriteiten.</li><li>[ Dashboard van de Identiteit ](../../identity-service/identity-graph-linking-rules/implementation-guide.md#validate-your-graphs): De grafieken van de monitor en bevestigt de Montages van de Identiteit.</li></ul> **Nota**: Er zullen geen veranderingen in uw gegevens zijn tot u manueel uw identiteitsmontages vormt. |

{style="table-layout:auto"}

Voor meer informatie raadpleegt u het [Identity Service-overzicht](../../identity-service/home.md).

## Query-service {#query-service}

Voer query&#39;s uit op gegevens in het Adobe Experience Platform-data lake met behulp van standaard SQL met Query Service. Combineer naadloos datasets en genereer nieuwe op basis van de queryresultaten om rapportage, datawetenschapworkflows of opname in het realtimeklantprofiel mogelijk te maken. U kunt bijvoorbeeld de gegevens van de klantentransactie samenvoegen met de gedragsgegevens om hoogwaardige doelgroepen te identificeren voor gerichte marketingcampagnes.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
|--------|-------------|
| JWT naar OAuth Credential Migration | De niet-vervallende JWT-referenties moeten uiterlijk 30 juni 2025 worden gemigreerd naar OAuth Server-to-Server om serviceonderbrekingen te vermijden. Deze wijziging verbetert de beveiliging en de consistentie van het platform. Zie de gids [Migreren van JWT naar OAuth Server-to-Server-referenties](../../query-service/ui/migrate-jwt-to-oauth.md) voor meer details. |
| Verouderde resultatentabel (beperkte beschikbaarheid) | Gebruikers die gebruikmaken van workflows voor slepen en selecteren, kunnen toegang aanvragen tot een oudere resultatentabel die browser-native selectie- en kopieergedrag ondersteunt. De geplakte output is door tabbladen gescheiden, waardoor kolommen uitgelijnd en leesbaar blijven in Excel. Dit vereenvoudigt de controle van spreadsheets en de processen voor kwaliteitsborging. Zie de [handleiding voor de gebruikersinterface van Query-editor](../../query-service/ui/user-guide.md#legacy-results-table) voor meer informatie. |

Voor meer informatie over [!DNL Query Service] raadpleegt u het [[!DNL Query Service] overzicht](../../query-service/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform is ontworpen om digitale ervaringstoepassingen wereldwijd te verrijken. Bedrijven gebruiken vaak meerdere digitale ervaringstoepassingen parallel en moeten de ontwikkeling, het testen en de implementatie van deze toepassingen verzorgen en tegelijkertijd de operationele naleving waarborgen. Om aan deze behoefte te voldoen biedt Experience Platform sandboxes die één Experience Platform-instantie opsplitsen in afzonderlijke virtuele omgevingen, zodat digitale ervaringstoepassingen kunnen worden ontwikkeld en verbeterd.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning van plug-in voor sandbox-tools uitgebreid | Campagnes kunnen nu met extra afhankelijke objecten worden gemigreerd met behulp van sandboxtools, zoals kanaalconfiguratie, uniforme beslissing, experimentele instellingen/varianten en meer. Voor een volledige lijst met ondersteunde campagneobjecten en alle ondersteunde Adobe Journey Optimizer-objecten raadpleegt u de handleiding voor [sandboxtools](../../sandboxes/ui/sandbox-tooling.md#adobe-journey-optimizer-objects). |

{style="table-layout:auto"}

Voor meer informatie over sandboxes, lees het [ overzicht van sandboxes](../../sandboxes/home.md).

## Segmentatieservice {#segmentation-service}

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Doelgroepen kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Criteria voor segmentatie van streaming bijwerken | Vanaf de release van mei 2025 zijn de criteria voor uw doelgroepen om in aanmerking te komen voor segmentatie van streaming bijgewerkt. Meer informatie over deze wijzigingen vindt u in de [update van de criteria voor het bepalen van de geschiktheid voor segmentatie van streaming](../../segmentation/eligibility-criteria-update.md). |

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

Gebruik bronnen in Experience Platform om gegevens vanuit een Adobe-applicatie of een databron van derden toe te voegen.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor basisverificatie voor [!DNL MySQL] | U kunt nu basisverificatie gebruiken om uw [!DNL MySQL]-database te verbinden met Experience Platform. Lees het [[!DNL MySQL] bronoverzicht](../../sources/connectors/databases/mysql.md) voor meer informatie. |

{style="table-layout:auto"}

Voor meer informatie raadpleegt u het [overzicht van bronnen](../../sources/home.md).
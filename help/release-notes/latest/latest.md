---
title: Opmerkingen bij de release van Adobe Experience Platform, mei 2024
description: De release van mei 2024 bevat opmerkingen voor Adobe Experience Platform.
source-git-commit: 85acffec03986cf56aeba6b8973ac1edf56a9cd6
workflow-type: tm+mt
source-wordcount: '1546'
ht-degree: 2%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: woensdag 21 mei 2024**

>[!TIP]
>
>De [Experience Platform API-documentatie](https://developer.adobe.com/experience-platform-apis/) is nu interactief. Verken de API eindpunten rechtstreeks van de documentatiepagina&#39;s om directe feedback te krijgen en uw technische implementatie te versnellen. [Meer informatie](#interactive-api-documentation) over de nieuwe functionaliteit.

Updates voor bestaande functies in Experience Platform:

- [Catalogusservice](#catalog-service)
- [Dashboards](#dashboards)
- [Gegevensbeheer](#governance)
- [Doelen](#destinations)
- [Query-service](#query-service)
- [Segmenteringsservice](#segmentation)
- [Bronnen](#sources)

Overige updates in Adobe Experience Platform:

- [Documentatie-updates](#documentation-updates)

## Catalogusservice {#catalog-service}

Catalogusservice is het systeem voor het vastleggen van de locatie van gegevens en de gegevensverbinding in Adobe Experience Platform. Terwijl alle gegevens die in Experience Platform worden opgenomen in het gegevensmeer als dossiers en folders worden opgeslagen, houdt de Catalogus de meta-gegevens en de beschrijving van die dossiers en folders voor raadpleging en controledoeleinden.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Bulkacties | De inventarisatie van de gegevensset ondersteunt nu acties in grote hoeveelheden. Stroomlijn uw processen van het gegevensbeheer en zorg voor het efficiënte beheer van uw datasets met bulkacties. De bulkacties van het gebruik om tijd te besparen door veelvoudige acties op talrijke datasets gelijktijdig uit te voeren.  Bulkacties omvatten [Verplaatsen naar map](../../catalog/datasets/user-guide.md#move-to-folders), [Codes bewerken](../../catalog/datasets/user-guide.md#manage-tags), en [Verwijderen](../../catalog/datasets/user-guide.md#delete) datasets. <br> ![Bulkacties in de werkruimte van de UI van Datasets.](../2024/assets/may/bulk-actions.png "Bulkacties in de werkruimte van de UI van Datasets."){width="100" zoomable="yes"} <br> Voor meer informatie over deze functie leest u de [UI-gids voor gegevensbestanden](../../catalog/datasets/user-guide.md#bulk-actions). |

{style="table-layout:auto"}

## Dashboards {#dashboards}

Adobe Experience Platform biedt meerdere dashboards waarmee u belangrijke inzichten over de gegevens van uw organisatie kunt bekijken, zoals vastgelegd tijdens dagelijkse momentopnamen.

**Nieuwe of bijgewerkte functies**
| Functie | Beschrijving | | — | — | | Aanpasbare inzichten voor uitgebreide toepassingsrapportage | Naadloos [overgang de output van SQL analyse in begrijpelijke, bedrijfsvriendelijke visuele formaten](../../dashboards/data-distiller/customizable-insights/overview.md). Gebruik aangepaste SQL-query&#39;s voor nauwkeurige gegevensmanipulatie en het maken van dynamische grafieken op basis van diverse gestructureerde datasets. U kunt vraag pro wijze gebruiken om complexe analyse met SQL uit te voeren en dan deze analyse met niet-technische gebruikers door grafieken op uw douanedashboard te delen of hen uit te voeren in Csv- dossiers. |

{style="table-layout:auto"}

## Gegevensbeheer {#governance}

Adobe Experience Platform Data Governance is een reeks strategieën en technologieën die worden gebruikt om klantgegevens te beheren en naleving van regelgeving, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik te waarborgen. Het speelt een sleutelrol binnen [!DNL Experience Platform] op verschillende niveaus, waaronder catalogisering, gegevenskoppeling, etikettering van het gegevensgebruik, beleid inzake gegevenstoegang en toegangscontrole voor marketingacties.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| mTLS-ondersteuning voor HTTP API-doelen en aangepaste Adobe Journey Optimizer-acties | Bouw klantenvertrouwen met de versterkte veiligheidsmaatregelen van het Wederzijdse Protocol van de Veiligheid van de Laag van het Vervoer (mTLS). De [HTTP-API-doel Experience Platform](../../destinations/catalog/streaming/http-destination.md#mtls-protocol-support) en [Aangepaste Adobe Journey Optimizer-acties](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions) biedt nu ondersteuning voor het mTLS-protocol bij het verzenden van gegevens naar geconfigureerde eindpunten. Er is geen aanvullende configuratie vereist in uw aangepaste handeling of HTTP API-bestemming om mTLS te activeren. Dit proces treedt automatisch op wanneer een mTLS-ingeschakeld eindpunt wordt gedetecteerd. U kunt [Download hier het Adobe Journey Optimizer-openbare certificaat](../../landing/governance-privacy-security/encryption.md#download-certificates) en de [Openbaar certificaat van de Dienst van bestemmingen hier](../../landing/governance-privacy-security/encryption.md#download-certificates).<br>Zie de [Documentatie voor gegevenscodering van Experience Platforms](../../landing/governance-privacy-security/encryption.md#mtls-protocol-support) voor meer informatie over de protocollen van de netwerkverbinding wanneer het uitvoeren van gegevens naar derdesystemen. |

{style="table-layout:auto"}

## Doelen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functionaliteit | Beschrijving |
| ----------- | ----------- |
| Toewijzingsvelden opnieuw ordenen voor batchdoelen | U kunt nu de volgorde van de kolommen in uw CSV-export wijzigen door de toewijzingsvelden in het dialoogvenster [toewijzingsstap](../../destinations/ui/activate-batch-profile-destinations.md#mapping). De volgorde van de toegewezen velden in de gebruikersinterface is afhankelijk van de volgorde van de kolommen in het geëxporteerde CSV-bestand, van boven naar beneden, waarbij de bovenste rij de meest linkse kolom in het CSV-bestand is. |
| Vooraf geselecteerde standaard exportschema&#39;s voor batchbestemmingen | Experience Platform stelt nu automatisch een standaardschema in voor elke bestandsuitvoer. Zie de documentatie op [exporteren van publiek plannen](../../destinations/ui/activate-batch-profile-destinations.md#scheduling) leren hoe te om het standaardprogramma te wijzigen. |
| Meerdere publieksactiveringsschema&#39;s voor batchdoelen bewerken | U kunt het activeringsschema voor meerdere soorten publiek nu bewerken via het menu [pagina met doelgegevens](../../destinations/ui/destination-details-page.md#bulk-edit-schedule). |
| Meerdere doelgroepen op aanvraag exporteren naar batchbestemmingen | U kunt nu meerdere soorten publiek selecteren en exporteren naar batchbestemmingen, via het dialoogvenster [bestanden op aanvraag exporteren](../../destinations/ui/export-file-now.md) functionaliteit. |

{style="table-layout:auto"}

Voor meer algemene informatie over bestemmingen raadpleegt u de [Overzicht van doelen](../../destinations/home.md).

## Query-service {#query-service}

Met Query Service kunt u standaard-SQL gebruiken om gegevens in Adobe Experience Platform op te vragen [!DNL Data Lake]. U kunt zich bij om het even welke datasets van aansluiten [!DNL Data Lake] en leg de vraagresultaten als nieuwe dataset voor gebruik in rapportering, de Werkruimte van de Wetenschap van Gegevens, of voor opname in het Profiel van de Klant in real time vast.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Legacy Editor is vervangen | De verouderde editor is vervangen en is niet meer beschikbaar voor gebruik. U kunt de opdracht [verbeterde functies van de Query Editor](../../query-service/ui/user-guide.md#query-authoring) om uw vragen te schrijven, te bevestigen en in werking te stellen. |
| Vertraging bij uitvoeren query | Houd de controle over uw computeruren door alarm voor vertragingen aan uw vraaglooppas te plaatsen. U kunt ervoor kiezen waarschuwingen te ontvangen als de status van een query na een bepaalde periode niet verandert. Plaats enkel uw gewenste vertragingstijd in de UI van het Platform om op de hoogte te blijven van uw vraagvooruitgang. Als u wilt weten hoe u deze waarschuwing instelt in de gebruikersinterface, raadpleegt u de [documentatie met queryplanningen](../../query-service/ui/query-schedules.md#alerts-for-query-status) of de [hulplijn voor inline queryhandelingen](../../query-service/ui/monitor-queries.md#query-run-delay). |
| Gestroomlijnde inventarisatie van querylogbestanden | U kunt nu een verbeterde efficiëntie voor probleemoplossing en taakbewaking gebruiken met een [gebruikersinterface voor gestroomlijnde querylogbestanden](../../query-service/ui/query-logs.md#filter-logs): <ul><li> De gebruikersinterface van het platform sluit nu standaard alle &quot;Systeemquery&#39;s&quot; uit van het tabblad Logboeken. </li><li> Systeemquery&#39;s weergeven door de controle ongedaan te maken **Systeemquery&#39;s uitsluiten**. </li></ul> <br> ![Het lusje van logboeken in de werkruimte UI van Vragen.](../2024/assets/may/query-log.png "Het lusje van logboeken in de werkruimte UI van Vragen."){width="100" zoomable="yes"} <br> Gebruik de gestroomlijnde gebruikersinterface voor querylogbestanden voor een meer focusweergave waarmee u de relevante logbestanden snel kunt identificeren en analyseren. |
| Databasekiezer | Gebruik het vervolgkeuzemenu van de nieuwe databaseselector om [hebben gemakkelijk toegang tot de gegevensmeningen van de Customer Journey Analytics van Power BI of Tableau](../../query-service/ui/credentials.md#connect-to-customer-journey-analytics). U kunt nu uw gewenste database rechtstreeks selecteren via de platforminterface voor een naadloze integratie van uw BI-gereedschappen. <br> ![Tabblad Referenties in de gebruikersinterface van query&#39;s.](../2024/assets/may/database-selector.png "Tabblad Referenties in de gebruikersinterface van query&#39;s."){width="100" zoomable="yes"} <br> |

{style="table-layout:auto"}

## Segmenteringsservice {#segmentation}

[!DNL Segmentation Service] staat u toe om gegevens te segmenteren die in worden opgeslagen [!DNL Experience Platform] die betrekking heeft op personen (zoals klanten, vooruitzichten, gebruikers of organisaties) die het publiek bereiken. U kunt publiek door segmentdefinities of andere bronnen van uw tot stand brengen [!DNL Real-Time Customer Profile] gegevens. Deze doelgroepen worden centraal geconfigureerd en onderhouden op [!DNL Platform]en gemakkelijk toegankelijk zijn via een Adobe-oplossing.

**Bijgewerkte functie**

| Functie | Beschrijving |
| --- | --- |
| Extern gegenereerde soorten publiek importeren | Voor het importeren van extern gegenereerde soorten publiek is nu de machtiging &#39;Deelvenster importeren&#39; vereist. Voor meer informatie over machtigingen leest u de [gebruikershandleiding voor machtigingen](../../access-control/home.md#permissions). |

{style="table-layout:auto"}

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

Gebruik bronnen in Experience Platform om gegevens van een Adobe of een gegevensbron van derden in te voeren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| OAuth2-clientreferentie voor [!DNL Salesforce] bron | U kunt nu OAuth2 Client Credential gebruiken om uw [!DNL Salesforce] account op Experience Platform. Lees de [!DNL Salesforce] bron [API-handleiding](../../sources/tutorials/api/create/crm/salesforce.md) en [UI-hulplijn](../../sources/tutorials/ui/create/crm/salesforce.md) voor meer informatie . |
| Ondersteuning voor voorbeeldgegevensstroom voor de [!DNL Marketo Engage] bron | De [!DNL Marketo Engage] De bron ondersteunt nu voorbeeldgegevens. Laat de configuratie van de steekproefgegevens toe om uw innamesnelheid te beperken en uit de eigenschappen van het Experience Platform zonder het moeten grote hoeveelheden gegevens innemen. Lees voor meer informatie de handleiding op [een gegevensstroom maken voor [!DNL Marketo Engage] in de gebruikersinterface](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |
| Updates voor IP-adreslijst van gewenste personen | Afhankelijk van uw locatie moet u een set nieuwe IP-adressen aan de lijst van gewenste personen toevoegen om streaming bronnen te kunnen gebruiken. Voor een uitvoerige lijst van de nieuwe IP adressen, lees [IP de gids van de lijst van gewenste personen van het adres](../../sources/ip-address-allow-list.md). |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte documentatie**

| Bijgewerkte documentatie | Beschrijving |
| --- | --- |
| Documentatie-updates voor [!DNL Google PubSub] | De [!DNL Google PubSub] de brondocumentatie is bijgewerkt met een uitvoerige in de eerste plaats vereiste gids. Gebruik de nieuwe eerste vereisten sectie om te leren hoe te om uw de dienstrekening tot stand te brengen, toestemmingen op het onderwerp of abonnementsniveau te verlenen, en configuraties te plaatsen om uw gebruik van te optimaliseren [!DNL Google PubSub] bron. Lees de [[!DNL Google PubSub] overzicht](../../sources/connectors/cloud-storage/google-pubsub.md) voor meer informatie . |

{style="table-layout:auto"}

Lees voor meer informatie over bronnen de [overzicht van bronnen](../../sources/home.md).

## Documentatie-updates {#documentation-updates}

### Interactieve API-documentatie voor Experience Platforms {#interactive-api-documentation}

De [Experience Platform API-documentatie](https://developer.adobe.com/experience-platform-apis/) is nu interactief. Alle API-referentiepagina&#39;s hebben nu een **Probeer het** .functionaliteit die u kunt gebruiken om API vraag rechtstreeks op de documentpagina van de website te testen. [Verkrijg de vereiste authentificatiegeloofsbrieven](/help/landing/api-authentication.md) en de functionaliteit te gebruiken om de API-eindpunten te verkennen.

Gebruik deze nieuwe functionaliteit om de verzoeken aan en de reacties van API eindpunten te onderzoeken, om directe feedback te krijgen en uw technische implementatie te versnellen. Ga bijvoorbeeld naar de [Identity Service API](https://developer.adobe.com/experience-platform-apis/references/identity-service/) of de [Schema-register-API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/) eindpunten om de nieuwe **Probeer het** functionaliteit in de rechtertrein.

![Schermopname die een API-aanroep weergeeft die rechtstreeks vanaf de documentatiewebsite is gemaakt.](../2024/assets/may/api-playground-demo.gif)

>[!CAUTION]
>
>Houd er rekening mee dat u met de interactieve API-functionaliteit op de documentatiepagina&#39;s echte API-aanroepen uitvoert naar de eindpunten. Houd dit in gedachten wanneer u experimenteert met productiesandboxen.

### Persoonlijke inzichten en betrokkenheid {#personalized-insights-engagement}

Een nieuwe gebruiksdocumentatiepagina van begin tot eind voor [evoluerend éénmalige waarde aan levenwaarde](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/evolve-one-time-value-to-lifetime-value.md) is nu live. Lees deze documentatie om te begrijpen hoe u Real-Time CDP en Adobe Journey Optimizer kunt gebruiken om sporadische bezoekers om te zetten in uw wegeigenschappen naar loyale klanten.

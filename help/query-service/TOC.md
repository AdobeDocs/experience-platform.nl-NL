---
audience: user
user-guide-title: Adobe Experience Platform Query Service Help
breadcrumb-title: Gids voor Query Service
user-guide-description: Gebruik standaard SQL om gegevens te doorzoeken binnen de data lake in Experience Platform.
feature: Queries
source-git-commit: 113e74b3a4783a11bc88dc2d16134b68638604e5
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 14%

---


# Adobe Experience Platform Query Service {#query}

- [Overzicht van Query Service](home.md)
- [Query Service verpakken](packages.md)
- [Query Service-handleidingen](guardrails.md)
- Aan de slag {#get-started}
   - [Vereisten](get-started/prerequisites.md)
- Data Distiller {#data-distiller}
   - [Overzicht](data-distiller/overview.md)
   - [Licentiegebruik](data-distiller/license-usage.md)
   - Winkel met query-versnelling {#query-accelerated-store}
      - [Verstuur versnelde vragen](data-distiller/query-accelerated-store/send-accelerated-queries.md)
      - [Handleiding voor het rapporteringsmodel voor inzichten](data-distiller/query-accelerated-store/reporting-insights-data-model.md)
   - Afgeleide kenmerken {#derived-attributes}
      - [Overzicht](data-distiller/derived-attributes/overview.md)
      - [Naadloze SQL-stroom](data-distiller/derived-attributes/seamless-sql-flow.md)
      - [Op decile gebaseerde afgeleide kenmerken maken](data-distiller/derived-attributes/decile-based-derived-attributes.md)
   - Pijpleidingen met I/ML-functies {#ml-feature-pipelines}
      - [Overzicht](data-distiller/ml-feature-pipelines/overview.md)
      - [Verbinding maken met Jupyter-laptops](data-distiller/ml-feature-pipelines/establish-connection.md)
      - [Verkennende gegevensanalyse](data-distiller/ml-feature-pipelines/exploratory-analysis.md)
      - [Engineer-functies voor ML](data-distiller/ml-feature-pipelines/feature-engineering.md)
      - [Gegevens exporteren naar XML-omgevingen](data-distiller/ml-feature-pipelines/export-data.md)
      - [Verrijking van end-to-end workflow voor de AI/ML-gegevenspijpleiding](data-distiller/ml-feature-pipelines/end-to-end-notebook-workflow.md)
- Gebruiksscenario’s {#use-cases}
   - [Verlaten browsers](use-cases/abandoned-browse.md)
   - [Attributieanalyse](use-cases/attribution-analysis.md)
   - [Bot filteren](use-cases/bot-filtering.md)
   - [Een trended-rapport van gebeurtenissen maken](use-cases/trended-report-of-events.md)
   - [Conceptanalyse](use-cases/consent-analysis.md)
   - [Levensduurwaarde van klant](use-cases/customer-lifetime-value.md)
   - [Afgeleide kenmerken op basis van een bestand](use-cases/deciles-use-case.md)
   - [Fuzzy match](use-cases/fuzzy-match.md)
   - [De paginaweergaven van een gebruiker weergeven](use-cases/list-visitor-sessions.md)
   - [Bezoekers weergeven op hun paginaweergaven](use-cases/visitors-by-number-of-page-views.md)
   - [Propensiteitsscore](use-cases/propensity-score.md)
   - [SQLAlchemy](use-cases/sqlalchemy.md)
   - [Commerciële variabelen uit analysegegevens retourneren en gebruiken](use-cases/merchandising-variables.md)
   - [Het roll-uprapport voor een bezoeker weergeven](use-cases/roll-up-report-of-a-visitor.md)
   - [Web- en mobiele analysemogelijkheden](use-cases/analytics-insights.md)
- Client verbinden met Query-service {#clients}
   - [Overzicht van clientverbindingen](clients/overview.md)
   - [SSL-modi](./clients/ssl-modes.md)
   - [Aqua Data Studio](clients/aqua-data-studio.md)
   - [DbVisualizer](./clients/dbvisulaizer.md)
   - [Jupyter-laptop](clients//jupyter-notebook.md)
   - [Liniaal](clients/looker.md)
   - [Postico](clients/postico.md)
   - [Power BI](clients/power-bi.md)
   - [PSQL](clients/psql.md)
   - [RStudio](clients/rstudio.md)
   - [Tableau](clients/tableau.md)
- Gebruikersinterface Query Service {#ui}
   - [Overzicht van gebruikersinterface](ui/overview.md)
   - [Gebruikershandleiding voor de Query Editor](ui/user-guide.md)
   - [Zoeksjablonen](ui/query-templates.md)
   - [Parameterized vragen (beperkt)](ui/parameterized-queries.md)
   - [Zoekprogramma&#39;s](ui/query-schedules.md)
   - [Zoekopdrachtlogs](ui/query-logs.md)
   - [Geplande query&#39;s controleren](ui/monitor-queries.md)
   - [Referentiegids](ui/credentials.md)
   - [Uitvoerdatasets genereren op basis van queryresultaten](ui/create-datasets.md)
- API-eindpunten voor query-service {#api}
   - [Aan de slag](api/getting-started.md)
   - [Zoekopdrachten](api/queries.md)
   - [Verbindingsparameters](api/connection-parameters.md)
   - [Planningen](api/scheduled-queries.md)
   - [Runs voor geplande vragen](api/runs-scheduled-queries.md)
   - [Zoeksjablonen](api/query-templates.md)
   - [Versnelde query&#39;s](api/accelerated-queries.md)
   - [Waarschuwingsabonnementen](api/alert-subscriptions.md)
- Gegevensbeheer {#data-governance}
   - [Overzicht](data-governance/overview.md)
   - [Handleiding controlelogboek](data-governance/audit-log-guide.md)
   - [Identiteiten in gegevenssets van ad-hocschema](data-governance/ad-hoc-schema-identities.md)
   - [Op kenmerken gebaseerde ondersteuning voor toegangsbeheer voor ad-hocschema&#39;s](./data-governance/ad-hoc-schema-labels.md)
- Best practices {#best-practices}
   - [Zoekopdracht uitvoeren](best-practices/writing-queries.md)
   - [Gegevensmiddelenorganisatie](./best-practices/organize-data-assets.md)
- Essentiële concepten {#essential-concepts}
   - [Werken met geneste gegevensstructuren](essential-concepts/nested-data-structures.md)
   - [Geneste gegevensstructuren samenvoegen](essential-concepts/flatten-nested-data.md)
   - [Anoniem blok](essential-concepts/anonymous-block.md)
   - [Inline-sjabloon](essential-concepts/inline-templates.md)
   - [Incrementeel laden](essential-concepts/incremental-load.md)
   - [Gegevensdeduplicatie](essential-concepts/deduplication.md)
   - [Gegevenssetvoorbeelden](essential-concepts/dataset-samples.md)
   - [Berekening van gegevenssetstatistieken](essential-concepts/dataset-statistics.md)
- SQL-referentie {#sql}
   - [SQL-overzicht](sql/overview.md)
   - [SQL-syntaxis](sql/syntax.md)
   - [Adobe-gedefinieerde functies](sql/adobe-defined-functions.md)
   - [SQL-functies in Spark](sql/spark-sql-functions.md)
   - [Opdrachten Metagegevens](sql/metadata.md)
   - [Vooraf voorbereide instructies](sql/prepared-statements.md)
- [Veelgestelde vragen](troubleshooting-guide.md)
- [IP adres lijst van gewenste personen](ip-address-allowlist.md)
- [API-referentie](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [Opmerkingen bij de release van Platform](https://www.adobe.com/go/platform-release-notes-en)

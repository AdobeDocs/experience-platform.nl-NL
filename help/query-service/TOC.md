---
audience: user
user-guide-title: Adobe Experience Platform Query Service Help
breadcrumb-title: Gids voor Query Service
user-guide-description: Gebruik standaard SQL om gegevens te doorzoeken binnen de data lake in Experience Platform.
feature: Queries
role: User,Developer
source-git-commit: e63ecbd14db2e9e4f35fb89aaaa406a4c584416a
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 11%

---


# Adobe Experience Platform Query Service {#query}

- [Overzicht van Query Service](home.md)
- [Query Service verpakken](packaging.md)
- [Query Service-handleidingen](guardrails.md)
- Aan de slag {#get-started}
   - [Vereisten](get-started/prerequisites.md)
- Data Distiller {#data-distiller}
   - [Overzicht](data-distiller/overview.md)
   - [Licentiegebruik](data-distiller/license-usage.md)
   - [Knopinfo voor maximale waarde](data-distiller/top-tips-to-maximize-value.md)
   - Afgeleide gegevenssets {#derived-datasets}
      - [Overzicht](data-distiller/derived-datasets/overview.md)
      - [Afgeleide datasets maken met SQL](data-distiller/derived-datasets/create-derived-datasets-with-sql.md)
      - [Op decile gebaseerde afgeleide gegevenssets maken](data-distiller/derived-datasets/decile-based-derived-attributes.md)
   - SQL-inzichten voor uitgebreide toepassingsrapportage {#sql-insights}
      - [Overzicht](data-distiller/sql-insights/overview.md)
      - [Query Pro-modus](data-distiller/sql-insights/query-pro-mode.md)
      - [Verstuur versnelde vragen](data-distiller/sql-insights/send-accelerated-queries.md)
      - [Handleiding voor het rapporteringsmodel voor inzichten](data-distiller/sql-insights/reporting-insights-data-model.md)
   - Pijpleidingen met functies voor AI/ML {#ml-feature-pipelines}
      - [Overzicht](data-distiller/ml-feature-pipelines/overview.md)
      - [Verbinding maken met Jupyter-laptops](data-distiller/ml-feature-pipelines/establish-connection.md)
      - [Verkennende gegevensanalyse](data-distiller/ml-feature-pipelines/exploratory-analysis.md)
      - [Engineer-functies voor ML](data-distiller/ml-feature-pipelines/feature-engineering.md)
      - [Gegevens exporteren naar XML-omgevingen](data-distiller/ml-feature-pipelines/export-data.md)
      - [Verrijking van end-to-end workflow voor de AI/ML-gegevenspijpleiding](data-distiller/ml-feature-pipelines/end-to-end-notebook-workflow.md)
- Distiller-statistieken over gegevens en leren van machines {#advanced-statistics}
   - [Overzicht](advanced-statistics/overview.md)
   - [Functietechniek](advanced-statistics/feature-engineering.md)
   - [Modellen](advanced-statistics/models.md)
   - [Eigenschaptransformatie](advanced-statistics/feature-transformation.md)
   - Modellen implementeren {#implement-models}
      - [Modellen implementeren](advanced-statistics/implement-models/implement-models.md)
      - [Regressie](advanced-statistics/implement-models/regression.md)
      - [Classificatie](advanced-statistics/implement-models/classification.md)
      - [Clustering](advanced-statistics/implement-models/clustering.md)
   - Voorbeelden {#examples}
      - [Bot filteren met behulp van statistieken en machinaal leren](advanced-statistics/examples/statistics-and-ml-bot-filtering.md)
      - [Klantenvertrouwen voorspellen met behulp van op SQL gebaseerde logistieke regressie](advanced-statistics/examples/predict-customer-churn.md)
- Distiller-publiek voor gegevens {#data-distiller-audiences}
   - [Extern publiek opbouwen met SQL](data-distiller-audiences/overview.md)
- Voorbeelden {#use-cases}
   - [Overzicht](use-cases/overview.md)
   - [Verlaten browsers](use-cases/abandoned-browse.md)
   - [Attributieanalyse](use-cases/attribution-analysis.md)
   - [Bot filteren](use-cases/bot-filtering.md)
   - [Bot filteren met behulp van statistieken en introductie van machinaal leren](use-cases/statistics-and-ml-bot-filtering-stub.md)
   - [Een trended-rapport van gebeurtenissen maken](use-cases/trended-report-of-events.md)
   - [Conceptanalyse](use-cases/consent-analysis.md)
   - [Levensduurwaarde van klant](use-cases/customer-lifetime-value.md)
   - [Gegevensexploratie](./use-cases/data-exploration.md)
   - [Op decile gebaseerde afgeleide datasets](use-cases/deciles-use-case.md)
   - [Fuzzy match](use-cases/fuzzy-match.md)
   - [De paginaweergaven van een gebruiker weergeven](use-cases/list-visitor-sessions.md)
   - [Bezoekers weergeven op hun paginaweergaven](use-cases/visitors-by-number-of-page-views.md)
   - [Klantenvertrouwen voorspellen met SQL](use-cases/predict-customer-churn-stub.md)
   - [Propensiteitsscore](use-cases/propensity-score.md)
   - [Verdien gelijkbare verslagen met hogere orde functies](use-cases/retrieve-similar-records.md)
   - [Commerciële variabelen uit analysegegevens retourneren en gebruiken](use-cases/merchandising-variables.md)
   - [SQLAlchemy](use-cases/sqlalchemy.md)
   - [Het roll-uprapport voor een bezoeker weergeven](use-cases/roll-up-report-of-a-visitor.md)
   - [Web- en mobiele analysemogelijkheden](use-cases/analytics-insights.md)
- Belangrijkste concepten {#key-concepts}
   - [Werken met geneste gegevensstructuren](key-concepts/nested-data-structures.md)
   - [Geneste gegevensstructuren samenvoegen](key-concepts/flatten-nested-data.md)
   - [Anoniem blok](key-concepts/anonymous-block.md)
   - [Inline-sjabloon](key-concepts/inline-templates.md)
   - [Incrementeel laden](key-concepts/incremental-load.md)
   - [Gegevensdeduplicatie](key-concepts/deduplication.md)
   - [Gegevenssetvoorbeelden](key-concepts/dataset-samples.md)
   - [Berekening van gegevenssetstatistieken](key-concepts/dataset-statistics.md)
- Distiller-hyperkubussen voor gegevens {#hypercubes}
   - [Efficiënte grote gegevensanalyse met hyperkubussen](hypercubes/overview.md)
- Clients verbinden met Query Service {#clients}
   - [Overzicht van clientverbindingen](clients/overview.md)
   - [SSL-modi](./clients/ssl-modes.md)
   - [Aqua Data Studio](clients/aqua-data-studio.md)
   - [DbVisualizer](./clients/dbvisulaizer.md)
   - [GitHub Copilot](./clients/github-copilot.md)
   - [Jupyter-laptop](clients//jupyter-notebook.md)
   - [Liniaal](clients/looker.md)
   - [Postico](clients/postico.md)
   - [Power BI](clients/power-bi.md)
   - [PSQL](clients/psql.md)
   - [RStudio](clients/rstudio.md)
   - [Tableau](clients/tableau.md)
- Gebruikersinterface van Query-service {#ui}
   - [Overzicht van gebruikersinterface](ui/overview.md)
   - [Gebruikershandleiding voor de Query Editor](ui/user-guide.md)
   - [Zoeksjablonen](ui/query-templates.md)
   - [Parameterized vragen](ui/parameterized-queries.md)
   - [Zoekprogramma&#39;s](ui/query-schedules.md)
   - [Zoekopdrachtlogs](ui/query-logs.md)
   - [Geplande query&#39;s controleren](ui/monitor-queries.md)
   - [Referentiegids](ui/credentials.md)
   - [Uitvoerdatasets genereren op basis van queryresultaten](ui/create-datasets.md)
- Query Service-API {#api}
   - [Aan de slag](api/getting-started.md)
   - [Zoekopdrachten](api/queries.md)
   - [Verbindingsparameters](api/connection-parameters.md)
   - [Planningen](api/scheduled-queries.md)
   - [Runs voor geplande vragen](api/runs-scheduled-queries.md)
   - [Zoeksjablonen](api/query-templates.md)
   - [Versnelde query&#39;s](api/accelerated-queries.md)
   - [Waarschuwingsabonnementen](api/alert-subscriptions.md)
- API voor Distiller-verificatie van gegevens {#auth-api}
   - [Overzicht](auth-api/overview.md)
   - [Aan de slag](auth-api/getting-started.md)
   - [IP-toegang](auth-api/ip-access.md)
   - [Valideren](auth-api/validate.md)
- Gegevensbeheer {#data-governance}
   - [Overzicht](data-governance/overview.md)
   - [Handleiding controlelogboek](data-governance/audit-log-guide.md)
   - [Identiteiten in gegevenssets van ad-hocschema](data-governance/ad-hoc-schema-identities.md)
   - [Op kenmerken gebaseerde ondersteuning voor toegangsbeheer voor ad-hocschema&#39;s](./data-governance/ad-hoc-schema-labels.md)
- Aanbevolen procedures {#best-practices}
   - [Zoekopdracht uitvoeren](best-practices/writing-queries.md)
   - [Gegevensmiddelenorganisatie](./best-practices/organize-data-assets.md)
- SQL-referentie {#sql}
   - [SQL-overzicht](sql/overview.md)
   - [SQL-syntaxis](sql/syntax.md)
   - [Adobe-gedefinieerde functies](sql/adobe-defined-functions.md)
   - [Functies met hogere volgorde](sql/higher-order-functions.md)
   - [SQL-functies in Spark](sql/spark-sql-functions.md)
   - [Opdrachten Metagegevens](sql/metadata.md)
   - [Vooraf voorbereide instructies](sql/prepared-statements.md)
- [Veelgestelde vragen](troubleshooting-guide.md)
- [IP adres lijst van gewenste personen](ip-address-allowlist.md)
- [ API verwijzing ](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [ de versienota&#39;s van het Platform ](https://experienceleague.adobe.com/en/docs/experience-platform/release-notes/latest)

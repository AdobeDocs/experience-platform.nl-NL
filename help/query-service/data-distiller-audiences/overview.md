---
title: Stimuleer soorten publiek met SQL
description: Leer hoe u de SQL-publieksextensie in Adobe Experience Platform Data Distiller kunt gebruiken voor het maken, beheren en publiceren van soorten publiek met SQL-opdrachten. In deze handleiding worden alle aspecten van de levenscyclus van de doelgroep behandeld, zoals het maken, bijwerken en verwijderen van profielen en het gebruik van gegevensgestuurde publieksdefinities voor doelbestemmingen op basis van bestanden.
source-git-commit: fbfd232c4e101f29ae01328c33763786a0e4a8cb
workflow-type: tm+mt
source-wordcount: '1266'
ht-degree: 0%

---

# Stimuleer soorten publiek met SQL

In dit document wordt beschreven hoe u de SQL-publieksextensie in Adobe Experience Platform Data Distiller kunt gebruiken voor het maken, beheren en publiceren van soorten publiek met SQL-opdrachten.

Gebruik de SQL publieksuitbreiding om publiek met gegevens van het gegevensmeer, met inbegrip van om het even welke bestaande afmetingsentiteiten te bouwen. Met deze extensie kunt u publiekssegmenten rechtstreeks met SQL definiëren, zodat u over flexibiliteit beschikt zonder dat u onbewerkte gegevens in uw profielen nodig hebt. Het publiek dat met deze methode wordt gecreeerd wordt automatisch geregistreerd in de werkruimte van het Publiek, waar u hen aan op dossier-gebaseerde bestemmingen kunt verder richten.

![ Infographic die het SQL werkschema van de publieksuitbreiding tonen. De stadia omvatten; het bouwen van publiek met de Dienst van de Vraag die SQL bevelen gebruiken, die hen in Platform UI beheren, om hen in op dossier-gebaseerde bestemmingen te activeren.](../images/data-distiller/sql-audiences/sql-audience-extension-workflow.png)

## Levenscyclus voor het maken van publiek in Data Distiller {#audience-creation-lifecycle}

Voer de volgende stappen uit om uw publiek effectief te beheren. Gemaakt publiek integreert naadloos in de publieksstroom, waardoor u segmenten van deze basispubliek en doelbestandsgebaseerde doelen voor klantgerichtheid kunt bouwen. Gebruik de volgende SQL bevelen om ](#create-audience) tot stand te brengen [ ](#add-profiles-to-audience) wijzigen, en [ schrappen ](#delete-audience) publiek binnen Adobe Experience Platform.[

### Een publiek maken {#create-audience}

Gebruik de opdracht `CREATE AUDIENCE AS SELECT` om een nieuw publiek te definiëren. Het gemaakte publiek wordt opgeslagen in een gegevensset en geregistreerd in de [!UICONTROL Audiences] -werkruimte onder Data Distiller.

```sql
CREATE AUDIENCE table_name  
WITH (primary_identity='IdentitycolName', identity_namespace='Namespace for the identity used', [schema='target_schema_title']) 
AS (select_query)
```

**Parameters**

Gebruik deze parameters om uw SQL vraag van de publieksverwezenlijking te bepalen:

| Parameter | Beschrijving |
|--------------------|------------------------------------------------------------------|
| `schema` | Optioneel. Bepaalt het schema XDM voor de dataset die door de vraag wordt gecreeerd. |
| `table_name` | Naam van de tabel en het publiek. |
| `primary_identity` | Hiermee geeft u de primaire identiteitskolom voor het publiek op. |
| `identity_namespace` | Naamruimte van de identiteit. |
| `select_query` | Een SELECT-instructie die het publiek definieert. De syntaxis van de UITGEZOCHTE vraag kan in de [ UITGEZOCHTE vragen ](../sql/syntax.md#select-queries) sectie worden gevonden. |

{style="table-layout:auto"}

**Voorbeeld:**

In het volgende voorbeeld wordt getoond hoe u de query voor het maken van uw SQL-publiek kunt structureren:

```sql
CREATE Audience aud_test 
WITH (primary_identity=month, identity_namespace=queryService) 
AS SELECT month FROM profile_dim_date LIMIT 5;
```

**Beperkingen:**

Houd rekening met de volgende beperkingen wanneer u SQL gebruikt voor het maken van publiek:

- De primaire identiteitskolom **moet** op het wortelniveau zijn.
- De nieuwe partijen beschrijven bestaande datasets; toevoegt functionaliteit is momenteel niet gesteund.
- Geneste kenmerken worden momenteel niet ondersteund.

### Profielen toevoegen aan een bestaand publiek {#add-profiles-to-audience}

Gebruik de opdracht `INSERT INTO` om profielen toe te voegen aan een bestaand publiek.

```sql
INSERT INTO table_name 
SELECT select_query
```

**Parameters**

In de volgende tabel worden de parameters beschreven die voor de opdracht `INSERT INTO` zijn vereist:

| Parameter | Beschrijving |
|----------------|--------------------------------------------------------------------------------|
| `table_name` | De naam van de lijst die als deel van creeer publieksbevel werd gecreeerd. |
| `select_query` | Een SELECT-instructie. De syntaxis van de SELECT-query vindt u in de sectie met SELECT-query&#39;s. |

{style="table-layout:auto"}

**Voorbeeld:**

In het volgende voorbeeld wordt getoond hoe u profielen aan een bestaand publiek kunt toevoegen met de opdracht `INSERT INTO` :

```sql
INSERT INTO Audience aud_test 
SELECT month FROM profile_dim_date LIMIT 10;
```

### Een publiek verwijderen (DROP-PUBLIEK) {#delete-audience}

Gebruik de opdracht `DROP AUDIENCE` om een bestaand publiek te verwijderen. Als het publiek niet bestaat, treedt een uitzondering op, tenzij `IF EXISTS` wordt opgegeven.

```sql
DROP AUDIENCE [IF EXISTS] [db_name.]table_name
```

**Parameters**

De tabel bevat de parameters die voor de opdracht `DROP AUDIENCE` zijn vereist:

| Parameter | Beschrijving |
|----------------|----------------------------------------------------------------------------------------|
| `IF EXISTS` | Optioneel. Indien gespecificeerd, als de lijst niet wordt gevonden, wordt geen uitzondering opgeheven. |
| `db_name` | Specificeert de gegevensgroep die wordt gebruikt om de publieksdataset te kwalificeren. |
| `table_name` | De naam van de lijst die als deel van creeer publieksbevel werd gecreeerd. |

{style="table-layout:auto"}

**Voorbeeld:**

In het volgende voorbeeld ziet u hoe u een publiek verwijdert met de opdracht DROP AUDIENCE:

```sql
DROP AUDIENCE IF EXISTS aud_test;
```

### Soorten publiek automatisch publiceren {#auto-publish-audiences}

Soorten publiek dat met de SQL-extensie is gemaakt, registreren zich automatisch onder Data Distiller in de werkruimte Publiek. Zodra geregistreerd, zijn deze publiek beschikbaar voor het richten en kunnen in op dossier-gebaseerde bestemmingen worden gebruikt, die uw segmentatie en het richten van strategieën verbeteren.

![ de werkruimte van het Publiek in Adobe Experience Platform, die het publiek van Distiller van Gegevens toont automatisch gepubliceerd en klaar voor gebruik.](../images/data-distiller/sql-audiences/audiences.png)

## Soorten publiek naar doelen activeren {#activate-audiences}

Activeer uw doelgroepen door deze naar een bestandsdoel te sturen, zoals [!DNL Amazon S3] , [!DNL SFTP] of [!DNL Azure Blob] . De verrijkte publieksattributen zijn beschikbaar voor verdere verfijning en het filtreren zoals nodig.

![ Stroomschema van de bestemmingstypes van Adobe Experience Platform, die openbare en privé/douanebestemmingen, met inbegrip van partij en het stromen opties tonen.](../images/data-distiller/sql-audiences/destination-types.png)

## Specificaties {#faqs}

In deze sectie worden veelgestelde vragen over het maken en beheren van een extern publiek met SQL in Data Distiller behandeld.

+++Selecteren om vragen en antwoorden weer te geven

- Wordt het creëren van het publiek gesteund slechts voor vlakke datasets?
- Geneste datasets worden ook ondersteund, maar alleen platte kenmerken zijn beschikbaar in het publiek.

- Resulteert de publieksverwezenlijking in één enkele dataset of veelvoudige datasets, of varieert het afhankelijk van de configuratie?
- Er is een één-op-één afbeelding tussen een publiek en een dataset.

- Wordt de dataset gecreeerd tijdens publieksverwezenlijking duidelijk voor Profiel?
- Nr, wordt de dataset die tijdens publieksverwezenlijking wordt gecreeerd niet duidelijk voor Profiel.

- Is de dataset gecreeerd op het gegevensmeer?
- Ja, de dataset wordt gecreeerd op het gegevens meer.

- Zijn de attributen in het publiek beperkt tot gebruik slechts in onderneming op dossier-gebaseerde bestemmingen? (Ja of Nee)
- Ja, zijn de attributen in het publiek beperkt tot gebruik slechts in onderneming op dossier-gebaseerde bestemmingen.

- Kan ik een publiek van publiek creëren dat een publiek van Gegevens Distiller gebruikt?
- Ja, u kunt een publiek van publiek tot stand brengen dat een publiek van Gegevens Distiller gebruikt.

- Worden deze soorten publiek in Adobe Journey Optimizer weergegeven? Als niet, wat gebeurt wanneer ik een nieuw publiek in de regelbouwer creeer die alle leden van dit publiek omvat?
- Het publiek van de gegevensdistilleerder is momenteel niet beschikbaar in Adobe Journey Optimizer. U moet een nieuw publiek maken in de Adobe Journey Optimizer-ontwikkelaar voor regels die beschikbaar zijn in Adobe Journey Optimizer.

- Hoe zou ik twee publiek van Gegevens Distiller met verschillende programma&#39;s moeten creëren? Hoeveel datasets worden gecreeerd, en worden zij duidelijk voor Profiel?
- Twee datasets zullen worden gecreeerd aangezien elk publiek een onderliggende dataset heeft. Deze gegevenssets zijn echter niet gemarkeerd voor Profiel. De twee datasets worden beheerd op hun eigen individuele programma&#39;s.

- Hoe verwijder ik een publiek?
- Om een publiek te schrappen, kunt u het [`DROP AUDIENCE` bevel ](#delete-audience) in de interface van de bevellijn gebruiken of de [ Snelle acties van de werkruimte van Soorten publiek ](../../segmentation/ui/audience-portal.md#quick-actions) gebruiken. OPMERKING: publiek dat wordt gebruikt in downstreambestemmingen of dat afhankelijk is van een ander publiek, kan niet worden verwijderd.

- Wanneer ik een publiek aan Profiel publiceert, hoe spoedig is het beschikbaar in de segment bouwer UI, en wanneer wordt het beschikbaar in Doelen?
- Wanneer het exporteren van de profielmomentopname is voltooid, kunnen de profielen in het publiek worden weergegeven.

- Worden Distiller-doelgroepen om de 30 dagen verwijderd omdat ze een extern publiek zijn?
- Ja, het publiek van Data Distiller wordt om de 30 dagen verwijderd omdat het een extern publiek is.

- Worden data-Distiller-soorten publiek weergegeven in de lijst Soorten publiek?
- Ja, data-Distiller-soorten publiek worden in de lijst Soorten publiek weergegeven onder de oorspronkelijke naam &#39;Data Distiller&#39;.

+++

## Volgende stappen

Nadat u dit document hebt gelezen, hebt u geleerd hoe u de SQL-publieksextensie in Data Distiller kunt gebruiken om een publiek met SQL-opdrachten te maken, te beheren en te publiceren. U kunt publieksdefinities nu aanpassen die op uw unieke bedrijfsvereisten worden gebaseerd en hen over diverse bestemmingen activeren, die uw marketing strategieën en gegeven-gedreven besluiten optimaliseren.

Vervolgens kunt u de volgende documentatie lezen om uw publieksbeheerstrategieën voor het platform verder te ontwikkelen en te optimaliseren:

- **Onderzoek de Evaluatie van het publiek**: Leer over de [ methodes van de publieksevaluatie in Adobe Experience Platform ](../../segmentation/home.md#evaluate-segments): het stromen segmentatie voor updates in real time, partijsegmentatie voor geplande of verwerking op bestelling, en randsegmentatie voor onmiddellijke evaluatie op de Edge Network.
- **integreer met Doelen**: Lees de gids op hoe te [ dossiers op bestelling uitvoeren aan partijbestemmingen ](../../destinations/ui/export-file-now.md) gebruikend de Doelen UI van het Platform.
- **Prestaties van het publiek van het Overzicht**: Analyseer hoe uw SQL-bepaald publiek over verschillende kanalen presteert. Gebruik gegevensinzichten om uw publieksdefinities en doelstrategieën aan te passen en te verbeteren. Lees het document op [ de inzichten van het Publiek ](../../dashboards/insights/audiences.md) om te leren hoe te om tot de SQL vragen voor publieksinzichten in Adobe Real-time Customer Data Platform toegang te hebben en aan te passen. Vervolgens kunt u uw eigen inzichten maken en onbewerkte gegevens transformeren in activeerbare informatie door het dashboard Soorten publiek aan te passen en deze inzichten effectief te visualiseren en te gebruiken voor een betere besluitvorming.

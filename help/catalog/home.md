---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Overzicht van Catalog Service
topic: overview
translation-type: tm+mt
source-git-commit: eec5b07427aa9daa44d23f09cfaf1b38f8e811f3

---


# Overzicht van Catalog Service

Catalog Service is het recordsysteem voor gegevenslocatie en -lijn in het Adobe Experience Platform. Terwijl alle gegevens die in het Platform van de Ervaring worden opgenomen in het meer van Gegevens als dossiers en folders worden opgeslagen, houdt de Catalogus de meta-gegevens en de beschrijving van die dossiers en folders voor raadpleging en controledoeleinden.

Eenvoudig gezet, werkt Catalog als meta-gegevensopslag of &quot;catalogus&quot;waar u informatie over uw gegevens binnen het Platform van de Ervaring kunt vinden. U kunt Catalog gebruiken om de volgende vragen te beantwoorden:

* Waar bevinden mijn gegevens zich?
* In welk stadium van verwerking bevinden deze gegevens zich?
* Welke systemen of processen hebben op mijn gegevens gehandeld?
* Hoeveel gegevens zijn verwerkt?
* Welke fouten zijn tijdens de verwerking opgetreden?

Catalog verstrekt een RESTful API die u toestaat om de meta-gegevens van het Platform programmatically te beheren gebruikend basisCRUD verrichtingen. Zie de [ontwikkelaarsgids](api/getting-started.md) van de Catalogus voor meer informatie.

## Diensten van het Catalogus- en ervaringsplatform

De middelen die de sporen van de Dienst van de Catalogus worden gebruikt door de veelvoudige diensten van het Platform van de Ervaring. Om de mogelijkheden van de Catalogus optimaal te maken, adviseert men dat u met deze diensten vertrouwd wordt en hoe zij met Catalogus in wisselwerking staan.

### XDM-systeem (Experience Data Model)

Het Systeem van de Gegevens van de ervaring Model (XDM) is het gestandaardiseerde kader waardoor het Platform gegevens van de klantenervaring organiseert. De hefboomwerkingen van het Platform van de ervaring XDM schema&#39;s om de structuur van gegevens op een verenigbare en herbruikbare manier te beschrijven.

Wanneer het gegeven in Platform wordt opgenomen, wordt de structuur van die gegevens in kaart gebracht aan een XDM schema en binnen het meer van Gegevens als deel van een **dataset** opgeslagen. De meta-gegevens voor elke dataset wordt gevolgd door de Dienst van de Catalogus, die een verwijzing naar het XDM schema omvat dat de dataset met in overeenstemming is.

Voor meer algemene informatie over XDM System, gelieve te zien het [XDM systeemoverzicht](../xdm/home.md).

### Gegevensinname

Het Platform van de ervaring neemt gegevens uit veelvoudige bronnen op en handhaaft verslagen als datasets binnen het meer van Gegevens. De catalogus volgt de meta-gegevens voor deze datasets, ongeacht hun bron of methode van opname.

Als u de methode voor het toevoegen van batches gebruikt, worden in Catalog ook aanvullende metagegevens bijgehouden voor **batchbestanden** . Batches zijn gegevenseenheden die bestaan uit een of meer bestanden die als één eenheid moeten worden ingevoerd. De catalogus volgt de meta-gegevens voor deze partijdossiers, evenals de datasets zij binnen na opname worden voortgeduurd. De meta-gegevens van de partij omvatten informatie over het aantal met succes opgenomen verslagen, evenals om het even welke ontbroken verslagen en bijbehorende foutenmeldingen.

Zie het overzicht [van](../ingestion/home.md) gegevensinvoer voor meer informatie.

## Catalogusobjecten

Zoals geschetst in de vorige sectie, volgt de Catalogus meta-gegevens voor verscheidene soorten middelen en verrichtingen die door andere diensten van het Platform worden gebruikt. In Catalog wordt een eigen opslagruimte van &#39;objecten&#39; bijgehouden waarin deze metagegevens worden ingekapseld. De voorwerpen van de catalogus zijn queryable vertegenwoordiging van de gegevens van het Platform die u toestaan om, uw gegevens te zoeken te controleren en te etiketteren zonder het moeten tot de gegevens zelf toegang hebben.

In de volgende tabel worden de verschillende objecttypen weergegeven die door Catalog worden ondersteund:

| Object | API-eindpunt | Definitie |
|---|---|---|
| Account | `/accounts` | Bij het maken van bronverbindingen moeten verificatiereferenties worden opgegeven. Een rekening vertegenwoordigt een inzameling van authentificatiegeloofsbrieven die werden gebruikt om een verbinding van een specifiek type tot stand te brengen. Elke verbinding heeft een reeks unieke parameters die door Catalog worden voortgeduurd en in een Azure Key Vault worden beveiligd. |
| Batch | `/batches` | Batches zijn gegevenseenheden die bestaan uit een of meer bestanden die als één eenheid moeten worden ingevoerd. Een partijvoorwerp in Catalogus schetst de innamemetriek van de partij (zoals het aantal verwerkte verslagen of grootte op schijf) en kan verbindingen aan datasets, meningen, en andere middelen omvatten die door de partijverrichting werden beïnvloed. |
| Verbinding | `/connections` | Een verbinding is één enkel geval van een bronschakelaar, uniek aan uw organisatie en gevormd gebruikend de aangewezen authentificatiereferenties voor het schakelaartype. |
| Connector | `/connectors` | Connectors definiëren hoe bronverbindingen gegevens moeten verzamelen van andere Adobe-toepassingen (zoals Adobe Analytics en Adobe Audience Manager), bronnen voor cloudopslag van derden (zoals Azure Blob, Amazon S3, FTP-servers en SFTP-servers) en CRM-systemen van derden (zoals Microsoft Dynamics en Salesforce). |
| Gegevensset | `/dataSets` | Een dataset is een opslag en beheersconstructie die voor de inzameling van gegevens (typisch een lijst) wordt gebruikt die een schema (kolommen) en gebieden (rijen) bevat. |
| Gegevensbestand | `/datasetFiles` | Gegevensbestanden vertegenwoordigen gegevensblokken die zijn opgeslagen op het platform. Als verslagen van letterlijke dossiers, zijn deze waar u de grootte van het dossier, het aantal verslagen kunt vinden het bevat, en een verwijzing naar de partij die het dossier opnam. |

## Volgende stappen

Dit document gaf een inleiding aan de Dienst van de Catalogus en hoe het binnen het grotere werkingsgebied van het Platform van de Ervaring functioneert. Zie de ontwikkelaarsgids [van de](api/getting-started.md) Catalogus voor stappen bij het in wisselwerking staan met de verschillende eindpunten van die Catalogus API. U wordt aangeraden ook naar de handleiding voor het [filteren van catalogusgegevens](api/filter-data.md) te verwijzen om de best practices voor het beperken van de gegevens die worden geretourneerd in API-reacties te volgen.
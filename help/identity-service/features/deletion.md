---
title: Verwijderen in identiteitsservice
description: Dit document biedt een overzicht van de verschillende methoden waarmee u uw identiteitsgegevens in Experience Platform kunt verwijderen en om duidelijk te maken hoe identiteitsgrafieken worden beïnvloed.
exl-id: 0619d845-71c1-4699-82aa-c6436815d5b3
source-git-commit: 2a2e3fcc4c118925795951a459a2ed93dfd7f7d7
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 0%

---

# Verwijderen in identiteitsservice

Adobe Experience Platform Identity Service genereert identiteitsgrafieken door identiteiten op deterministische wijze te koppelen tussen apparaten en systemen voor een individuele persoon. Identiteitsgrafiekkoppelingen worden tot stand gebracht wanneer twee of meer gemarkeerde identiteiten binnen dezelfde gegevensrij worden ontvangen.

Identiteitsgrafieken worden gebruikt door het profiel van de Klant in real time om een uitvoerige en unieke mening van uw klantenattributen en gedrag tot stand te brengen, toelatend u om impactvolle, persoonlijke digitale ervaringen in real time, aan mensen, en niet apparaten te leveren.

Dit document biedt een overzicht van de verschillende methoden waarmee u uw identiteitsgegevens in Experience Platform kunt verwijderen en om duidelijk te maken hoe identiteitsgrafieken worden beïnvloed.

## Aan de slag

In het onderstaande document wordt verwezen naar de volgende kenmerken van Experience Platform:

* [ Dienst van de Identiteit ](../home.md): Verkrijg een betere mening van individuele klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen.
   * [ Grafiek van de Identiteit ](./identity-graph-viewer.md): Een identiteitsgrafiek is een kaart van verhoudingen tussen verschillende identiteiten voor een bepaalde klant, die u van een visuele vertegenwoordiging voorziet van hoe uw klant met uw merk over verschillende kanalen interactie aangaat.
   * [ Identiteitsnaamruimten ](./namespaces.md): Identiteitsnaamruimten zijn een component van de Dienst van de Identiteit die als indicatoren van de context dienen waarop een identiteit betrekking heeft. Ze onderscheiden bijvoorbeeld een waarde van &quot;name<span>@email.com&quot; als e-mailadres of &quot;443522&quot; als een numerieke CRMID.
* [ de Dienst van de Catalogus ](../../catalog/home.md): Onderzoek de gegevenslijn, meta-gegevens, dossierbeschrijvingen, folders, en datasets binnen het gegevensmeer.
* [ de hygiëne van Gegevens ](../../hygiene/home.md): Beheer uw opgeslagen consumentengegevens door geautomatiseerde datasettermijnen te plannen of individuele verslagen van één dataset of alle datasets te schrappen.
* [ Adobe Experience Platform Privacy Service ](../../privacy-service/home.md): Beheer klantenverzoeken om tot toegang te hebben, uit verkoop te kiezen, of hun persoonlijke gegevens over de toepassingen van Adobe Experience Cloud te schrappen.
* [ Real-Time Profiel van de Klant ](../../profile/home.md): Verstrekt een verenigd, klantenprofiel in real time gebaseerd op samengevoegde gegevens van veelvoudige bronnen.

## Eén enkele identiteitsschrapping

Met één aanvraag voor het verwijderen van identiteiten kunt u een identiteit binnen een grafiek verwijderen. Dit leidt tot het verwijderen van koppelingen die zijn gekoppeld aan één gebruikersidentiteit die is gekoppeld aan een naamruimte voor identiteiten. U kunt mechanismen gebruiken die door [ worden verstrekt Privacy Service ](../../privacy-service/home.md) voor gebruiksgevallen zoals klantenverzoeken om gegevensschrapping en naleving van privacyverordeningen zoals de Algemene Verordening van de Bescherming van Gegevens (GDPR).

In de volgende secties worden de mechanismen beschreven die u kunt gebruiken voor verzoeken om één identiteit te verwijderen in Experience Platform.

### Eén identiteitsverwijdering in Privacy Service

Privacy Service verwerkt verzoeken van klanten om toegang, om zich uit verkoop te laten of om hun persoonsgegevens te verwijderen, zoals die zijn omschreven in privacyregels zoals de General Data Protection Regulation (GDPR) en de California Consumer Privacy Act (CCPA). Met Privacy Service kunt u taakaanvragen verzenden via de API of de gebruikersinterface. Wanneer het Experience Platform een schrappingsverzoek van Privacy Service ontvangt, verzendt het Platform bevestiging aan Privacy Service dat het verzoek is ontvangen en de beïnvloede gegevens voor schrapping duidelijk zijn gemaakt. De verwijdering van de individuele identiteit is gebaseerd op de opgegeven naamruimte en/of ID-waarde. Bovendien worden alle sandboxen die bij een bepaalde organisatie horen, verwijderd. Voor meer informatie, lees de gids op [ verwerking van het privacyverzoek in de Dienst van de Identiteit ](../privacy.md).

In de onderstaande tabel wordt een uitsplitsing gegeven van één enkele identiteitsschrapping in de Privacy Service:

| Eén identiteit verwijderen | Privacyservice |
| --- | --- |
| Gebruikskwesties | Alleen gegevensprivacyverzoeken (GDPR, CCPA). |
| Geschatte latentie | Dagen tot weken |
| Betrokken services | Eén identiteitsverwijdering in Privacy Service stelt u in staat te selecteren of gegevens worden verwijderd uit Identiteitsservice, Real-Time Klantprofiel of Gegevensbestand. |
| Verwijderingspatronen | Verwijder een identiteit uit Identiteitsservice. |

{style="table-layout:auto"}

## Gegevensset verwijderen

In de volgende secties worden de mechanismen beschreven die kunnen worden gebruikt om gegevenssets en bijbehorende identiteitskoppelingen in Experience Platform te verwijderen.

### Gegevensset verwijderen in Catalog Service

U kunt de Dienst van de Catalogus gebruiken om verzoeken om datasetschrapping voor te leggen. Voor meer informatie over hoe te om datasets met de Dienst van de Catalogus te schrappen, lees de gids bij [ schrappend voorwerpen gebruikend de Dienst API van de Catalogus ](../../catalog/api/delete-object.md). Alternatief, kunt u Platform UI gebruiken om verzoeken om datasetschrapping voor te leggen. Voor meer informatie, leest de [ gids van de datasetgebruiker ](../../catalog/datasets/user-guide.md#delete-a-dataset).

### Vervaldatum gegevensset in gegevenshygiëne

De [[!UICONTROL Data Hygiene] werkruimte ](../../hygiene/ui/overview.md) in Adobe Experience Platform UI staat u toe om termijnen voor datasets te plannen. Wanneer een dataset zijn vervaldatum bereikt, beginnen het gegevens meer, de Dienst van de Identiteit, en het Profiel van de Klant in real time afzonderlijke processen om de inhoud van de dataset uit hun respectieve diensten te verwijderen. Voor meer informatie, lees de gids over [ het leiden gegevenssetvervalsingen gebruikend de [!UICONTROL Data Hygiene] werkruimte ](../../hygiene/ui/dataset-expiration.md).

De onderstaande tabel geeft een overzicht van de verschillen tussen gegevenssetverwijdering in Catalog Service en gegevenshygiëne:

| Gegevensset verwijderen | Catalogusservice | Gegevenshygiëne |
| --- | --- | --- |
| Gebruikskwesties | Schrap volledige datasets en hun bijbehorende identiteitsinformatie in Platform. | Beheer van in Experience Platform opgeslagen gegevens. |
| Geschatte latentie | Dagen | Dagen |
| Betrokken services | De schrapping van de gegevensreeks door de Dienst van de Catalogus schrapt gegevens van de Dienst van de Identiteit, het Profiel van de Klant in real time, en het gegevenspeer. | De schrapping van de gegevensreeks door de hygiëne van Gegevens schrapt gegevens van de Dienst van de Identiteit, het Profiel van de Klant in real time, en het gegevenspeer. |
| Verwijderingspatroon | Verbonden identiteiten verwijderen uit de identiteitsdienst die door een bepaalde gegevensset is ingesteld. | Schrap verbonden identiteiten van de Dienst van de Identiteit die door een bepaalde dataset wordt gevestigd, die op vervalprogramma wordt gebaseerd. |

{style="table-layout:auto"}

## Verschillende statussen van identiteitsgrafieken na verwijdering

Alle schrappingen van identiteitsgrafieken resulteren in het verwijderen van verbindingen tussen twee of meer identiteiten, zoals gespecificeerd in het verwijderingsverzoek. Voor verzoeken tot schrapping van gegevenssets worden alle identiteitskoppelingen die door de opgegeven gegevensset zijn vastgesteld, verwijderd en kunnen al dan niet identiteiten uit grafieken worden verwijderd. Voor individuele identiteitsschrappingsverzoeken worden de identiteitskoppelingen verwijderd voor de gespecificeerde identiteit, en bijgevolg wordt de identiteitswaarde zelf verwijderd uit alle identiteitsgrafieken. Identiteiten zonder één koppeling naar een andere identiteit worden niet opgeslagen in Identiteitsservice.

Hieronder ziet u een overzicht van de mogelijke effecten die verwijderingen kunnen hebben op de status van identiteitsgrafieken.

| Identiteitsgrafiekstatus | Beschrijving |
| --- | --- |
| Gedeeltelijke update | Een gedeeltelijke update van een grafiek gebeurt wanneer minstens twee identiteiten binnen een grafiek verbonden blijven nadat een schrappingsverzoek met succes wordt verwerkt. Na het verwijderen kunnen de resterende identiteitskoppelingen met elkaar verbonden blijven of worden gesplitst in twee of meer afzonderlijke grafieken, afhankelijk van de identiteiten die zijn verwijderd. |
| Volledige verwijdering | Een grafiek moet minstens twee gekoppelde identiteiten hebben om te bestaan. Daarom als een schrappingsverzoek in de verwijdering van alle bestaande verbindingen binnen een grafiek resulteert, dan zal de grafiek volledig worden verwijderd. |
| Geen wijziging | Een grafiek zal niet beïnvloed worden als een bepaald schrappingsverzoek een identiteit of dataset bevat die niet met om het even welk lid van de grafiek wordt geassocieerd. Bovendien, wordt een grafiek niet bijgewerkt zelfs als het schrappingsverzoek een verband tussen een dataset of een identiteit-datasetcombinatie verwijdert, gegeven dat de verbinding door een andere verbinding werd gevestigd die niet werd geschrapt. Dit betekent dat als een verbinding in twee verschillende datasets bestaat, de grafiek niet zal worden bijgewerkt omdat slechts één van de datasets wordt verwijderd. |

{style="table-layout:auto"}

## Volgende stappen

Dit document behandelde de diverse mechanismen die u kunt gebruiken om identiteiten en datasets op Experience Platform te schrappen. In dit document wordt ook beschreven hoe het verwijderen van identiteits- en gegevenssets invloed kan hebben op identiteitsgrafieken. Voor meer informatie over de Dienst van de Identiteit, lees het [ overzicht van de Dienst van de Identiteit ](../home.md).

<!--

You can use [Data hygiene](../hygiene/home.md) for data cleansing, removing anonymous data, or data minimization for the data that you have collected.

### Single identity deletion in the [!UICONTROL Data Hygiene] workspace

The [[!UICONTROL Data Hygiene] workspace](../hygiene/ui/overview.md) in the Platform UI allows you to delete consumer records that are participating in Identity Service and Real-Time Customer Profile. For a comprehensive guide on using the [!UICONTROL Data Hygiene] workspace, see the tutorial on [deleting consumer records](../hygiene/ui/record-delete.md).

The table below provides a breakdown of differences between single identity deletion in Privacy Service and Data hygiene:

| Single identity deletion | Privacy Service | Data hygiene |
| --- | --- | --- |
| Accepted use cases | Data privacy requests (GDPR, CCPA) only. | Management of data stored in Experience Platform. |
| Estimated latency | Days to weeks | Days |
| Services impacted | Single identity deletion in Privacy Service allows you to select whether data will be deleted from Identity Service, Real-Time Customer Profile, or data lake. | Single identity deletion in Data hygiene deletes the selected data across Identity Service, Real-Time Customer Profile, and data lake. |
| Deletion patterns | Delete an identity from Identity Service. | Delete an identity from Identity Service. |

-->

---
keywords: Experience Platform;home;populaire onderwerpen;CJA;reisanalyse;analyse van de klantenreis;campagneorkest;orchestratie;reis;reis;reis orchestratie;capaciteit;regio
title: Adobe Experience Platform End-to-end voorbeeldworkflow
description: Leer op hoog niveau de standaard end-to-end workflow voor Adobe Experience Platform.
exl-id: 0a4d3b68-05a5-43ef-bf0d-5738a148aa77
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1858'
ht-degree: 0%

---

# Adobe Experience Platform end-to-end voorbeeldworkflow

Adobe Experience Platform is het krachtigste, meest flexibele en open systeem op de markt voor het ontwikkelen en beheren van volledige oplossingen die de ervaring van klanten stimuleren. Experience Platform stelt organisaties in staat om klantgegevens en -inhoud van elk systeem te centraliseren en te standaardiseren en datamateriaal en computerleren toe te passen om het ontwerp en de levering van rijke, persoonlijke ervaringen drastisch te verbeteren.

Experience Platform is gebaseerd op RESTful-API&#39;s en stelt de volledige functionaliteit van het systeem beschikbaar voor ontwikkelaars, zodat bedrijfsoplossingen eenvoudig kunnen worden geïntegreerd met behulp van vertrouwde tools. Met Experience Platform kunt u een holistische weergave van uw klanten afleiden door uw klantgegevens in te voeren, uw gegevens te segmenteren naar het publiek dat u wilt richten en deze doelgroepen te activeren naar een externe bestemming. In de volgende zelfstudie wordt een end-to-end workflow getoond, waarin alle stappen worden getoond van opname via bronnen tot activering van het publiek via doelen.

![&#x200B; het werkschema van begin tot eind van Experience Platform &#x200B;](./images/end-to-end-tutorial/platform-end-2-end-workflow.png)

## Aan de slag

Voor deze end-to-end workflow worden meerdere Adobe Experience Platform-services gebruikt. Hieronder volgt een lijst met services die in deze workflow worden gebruikt en koppelingen bevatten naar de bijbehorende overzichten:

- [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Het gestandaardiseerde framework waarmee [!DNL Experience Platform] gegevens voor de klantervaring indeelt. Om het beste gebruik van Segmentatie te maken, gelieve te verzekeren uw gegevens als profielen en gebeurtenissen volgens de [&#x200B; beste praktijken voor gegevens modellering &#x200B;](../xdm/schema/best-practices.md) worden opgenomen.
- [[!DNL Identity Service]](../identity-service/home.md): biedt u een uitgebreide weergave van uw klanten en hun gedrag door identiteiten te overbruggen tussen apparaten en systemen.
- [&#x200B; Bronnen &#x200B;](../sources/home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
- [[!DNL Segmentation Service]](../segmentation/home.md) [!DNL Segmentation Service] : hiermee kunt u gegevens die zijn opgeslagen in [!DNL Experience Platform] en die betrekking hebben op individuen (zoals klanten, vooruitzichten, gebruikers of organisaties), opsplitsen in kleinere groepen.
- [[!DNL Real-Time Customer Profile]](../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.
- [&#x200B; Datasets &#x200B;](../catalog/datasets/overview.md): De opslag en beheersconstructie voor gegevenspersistentie in [!DNL Experience Platform].
- [&#x200B; Doelen &#x200B;](../destinations/home.md): De bestemmingen zijn pre-gebouwde integratie met algemeen gebruikte toepassingen die voor de naadloze activering van gegevens van Experience Platform voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen toestaan.

## Een XDM-schema maken

Voordat u gegevens in Experience Platform invoert, moet u eerst een XDM-schema maken om de structuur van die gegevens te beschrijven. Wanneer u uw gegevens in de volgende stap opneemt, zult u uw inkomende gegevens aan dit schema in kaart brengen. Leren hoe te om een voorbeeldXDM schema tot stand te brengen, te lezen gelieve het leerprogramma op [&#x200B; creërend een schema gebruikend de Redacteur van het Schema &#x200B;](../xdm/tutorials/create-schema-ui.md).

De bovenstaande zelfstudie laat zien hoe u identiteitsvelden kunt instellen voor uw schema&#39;s. Een identiteitsveld vertegenwoordigt een veld dat kan worden gebruikt om een individuele persoon te identificeren die gerelateerd is aan een record- of tijdreeksgebeurtenis. Identiteitsvelden vormen een cruciaal onderdeel van de manier waarop identiteitsgrafieken van klanten in Experience Platform worden samengesteld. Dit beïnvloedt uiteindelijk de manier waarop in Real-Time Customer Profile verschillende gegevensfragmenten worden samengevoegd om een volledig beeld van de klant te krijgen. Voor meer details op hoe te om identiteitsgrafieken in Experience Platform te bekijken, zie het leerprogramma op [&#x200B; hoe te om de kijker van de identiteitsgrafiek te gebruiken &#x200B;](../identity-service/features/identity-graph-viewer.md).

U moet uw schema voor gebruik in het Profiel van de Klant in real time toelaten zodat de klantenprofielen van de gegevens kunnen worden geconstrueerd die op uw schema worden gebaseerd. Zie de sectie op [&#x200B; toelatend een schema voor Profiel &#x200B;](../xdm/ui/resources/schemas.md#profile) in de schema&#39;s UI gids voor meer informatie.

## Gegevens in Experience Platform plaatsen

Nadat u een XDM-schema hebt gemaakt, kunt u uw gegevens in het systeem opnemen.

Alle gegevens die naar Experience Platform worden gebracht, worden bij inname opgeslagen op individuele gegevenssets. Een dataset is een inzameling van gegevensverslagen die aan een specifiek schema XDM in kaart brengen. Voordat uw gegevens door [!DNL Real-Time Customer Profile] kunnen worden gebruikt, moet de desbetreffende gegevensset specifiek zijn geconfigureerd. Voor volledige instructies op hoe te om een dataset voor Profiel toe te laten, zie de [&#x200B; gids UI van Datasets &#x200B;](../catalog/datasets/user-guide.md#enable-profile) en het [&#x200B; leerprogramma van de datasetconfiguratie API &#x200B;](../profile/tutorials/dataset-configuration.md). Zodra de dataset is gevormd, kunt u beginnen gegevens in het op te nemen.

Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen en biedt u de mogelijkheid om inkomende gegevens te structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, opslag in de cloud, databases en vele andere. Bijvoorbeeld, kunt u uw gegevens opnemen door [&#x200B; Amazon S3 &#x200B;](../sources/tutorials/api/create/cloud-storage/s3.md) te gebruiken. Een volledige lijst van beschikbare bronnen kan in het [&#x200B; overzicht van bronschakelaars &#x200B;](../sources/home.md) worden gevonden.

Als u Amazon S3 als uw bronschakelaar gebruikt, kunt u de instructies in of het API leerprogramma volgen op [&#x200B; het creëren van een schakelaar van Amazon S3 &#x200B;](../sources/tutorials/api/create/cloud-storage/s3.md) of het leerprogramma UI op [&#x200B; het creëren van een schakelaar van Amazon S3 &#x200B;](../sources/tutorials/ui/create/cloud-storage/s3.md) om te leren hoe te om, met, en gegevens binnen de schakelaar tot stand te brengen te verbinden.

Voor meer gedetailleerde instructies op bronschakelaars, te lezen gelieve het [&#x200B; overzicht van bronschakelaars &#x200B;](../sources/home.md). Om meer over de Dienst van de Stroom te leren, API die de bronnen van zijn gebaseerd, te lezen gelieve de [&#x200B; Verwijzing van de Dienst API van de Stroom &#x200B;](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Zodra uw gegevens in Experience Platform door de bronschakelaar worden gebracht en in uw profiel-Toegelaten dataset worden opgeslagen, worden de klantenprofielen automatisch gecreeerd gebaseerd op de identiteitsgegevens u in uw schema XDM vormde.

Wanneer het uploaden van gegevens aan een nieuwe dataset voor het eerst, of wanneer het opzetten van een nieuw proces ETL of een gegevensbron, wordt geadviseerd om de gegevens zorgvuldig te controleren om ervoor te zorgen het correct is geupload en dat de geproduceerde profielen de gegevens bevatten u verwacht. Voor meer informatie over hoe te om tot klantenprofielen in Experience Platform UI toegang te hebben, zie de [&#x200B; gids UI van het Profiel van de Klant in real time &#x200B;](../profile/ui/user-guide.md). Voor de details op hoe te om tot profielen toegang te hebben die Real-Time API van het Profiel van de Klant gebruiken, zie de gids op [&#x200B; gebruikend het entiteitseindpunt &#x200B;](../profile/api/entities.md).

## Uw gegevens evalueren

Nadat de gegenereerde profielen zijn gegenereerd op basis van de gegevens die u hebt ingevoerd, kunt u de gegevens evalueren met behulp van segmentatie. De segmentatie is het proces om specifieke attributen of gedrag te bepalen die door een ondergroep van individuen van uw opslag van het Profiel worden gedeeld, om een verhandelbare groep mensen van uw klantenbasis te onderscheiden. Om meer over segmentatie te leren, te lezen gelieve het [&#x200B; overzicht van de segmentatiedienst &#x200B;](../segmentation/home.md).

### Een segmentdefinitie maken

Om te beginnen, moet u een segmentdefinitie creëren om uw klanten te groeperen om uw doelpubliek tot stand te brengen. Een segmentdefinitie is een inzameling van regels die u kunt gebruiken om het publiek te bepalen u wilt richten. Om een segmentdefinitie tot stand te brengen, kunt u de instructies in of UI gids volgen bij het gebruiken van [&#x200B; de Bouwer van het Segment &#x200B;](../segmentation/ui/segment-builder.md) of het API leerprogramma op [&#x200B; creërend een segment &#x200B;](../segmentation/tutorials/create-a-segment.md).

Zodra u een segmentdefinitie hebt gecreeerd, zorg ervoor dat u nota van identiteitskaart van de segmentdefinitie houdt.

### Uw segmentdefinitie evalueren

Na het creëren van uw segmentdefinitie, kunt u of een segmentbaan tot stand brengen om het segment als éénmalige instantie te evalueren of een programma tot stand te brengen om het segment op een aan de gang zijnde basis te evalueren.

Om een segmentdefinitie op bestelling te evalueren, kunt u een segmentbaan tot stand brengen. Een segmentbaan is een asynchroon proces dat tot een nieuw publiekssegment leidt dat op de waarnaar wordt verwezen segmentdefinitie en samenvoegbeleid wordt gebaseerd. Een samenvoegingsbeleid is een reeks regels die Experience Platform gebruikt om te bepalen welke gegevens zullen worden gebruikt om klantenprofielen tot stand te brengen, en welke gegevens voorrang zullen krijgen wanneer er discrepanties tussen bronnen zijn. Leren hoe te met samenvoegbeleid te werken, zie de [&#x200B; gids UI van het samenvoegingsbeleid &#x200B;](../profile/merge-policies/ui-guide.md).

Zodra de segmentbaan wordt gecreeerd en geëvalueerd, kunt u informatie over het segment, zoals de grootte van uw publiek of fouten krijgen die tijdens verwerking kunnen zijn voorgekomen. Leren hoe te om een segmentbaan tot stand te brengen, met inbegrip van alle details u moet verstrekken, te lezen gelieve de [&#x200B; gids van de de baanontwikkelaar van het segment &#x200B;](../segmentation/api/segment-jobs.md).

Om een segmentdefinitie op een aan de gang zijnde basis te evalueren, kunt u een programma tot stand brengen en toelaten. Een schema is een hulpmiddel dat kan worden gebruikt om een segmentbaan eens per dag op een gespecificeerde tijd automatisch in werking te stellen. Leren om een programma tot stand te brengen en toe te laten, kunt u de instructies in de API gids op het [&#x200B; planneneindpunt &#x200B;](../segmentation/api/schedules.md) volgen.

## Uw geëvalueerde gegevens exporteren

Na het creëren van uw eenmalig segmentbaan of uw aan de gang zijnde programma, kunt u of een baan van de segmentuitvoer tot stand brengen om de resultaten naar een dataset uit te voeren of de resultaten naar een bestemming uit te voeren. In de volgende secties vindt u een overzicht van beide opties.

### Uw geëvalueerde gegevens exporteren naar een gegevensset

Nadat u een eenmalige segmenttaak of uw doorlopende planning hebt gemaakt, kunt u de resultaten exporteren door een segmentexporttaak te maken. Een segmentexporttaak is een asynchrone taak die informatie over het geëvalueerde publiek naar een dataset verzendt.

Voordat u een exporttaak maakt, moet u eerst een gegevensset maken waarin u de gegevens wilt exporteren. Leren hoe te om een dataset tot stand te brengen, te lezen gelieve de sectie op [&#x200B; creërend een doeldataset &#x200B;](../segmentation/tutorials/evaluate-a-segment.md#create-dataset) in het leerprogramma bij het evalueren van een segment, die u nota neemt van dataset identiteitskaart na verwezenlijking. Nadat u een gegevensset hebt gemaakt, kunt u een exporttaak maken. Leren hoe te om een uitvoerbaan tot stand te brengen, kunt u de instructies in de API gids op het [&#x200B; eindpunt van de de uitvoerbanen &#x200B;](../segmentation/api/export-jobs.md) volgen.

### Uw geëvalueerde gegevens exporteren naar een bestemming

Alternatief, na het creëren van uw eenmalig segmentbaan of uw aan de gang zijnde programma, kunt u de resultaten naar een bestemming uitvoeren. Een bestemming is een eindpunt, zoals een toepassing van Adobe op de externe dienst, waar een publiek kan worden geactiveerd en worden geleverd. Een volledige lijst van beschikbare bestemmingen kan in de [&#x200B; catalogus van bestemmingen &#x200B;](../destinations/catalog/overview.md) worden gevonden.

Voor instructies op hoe te om gegevens aan partij of e-mail marketing bestemmingen te activeren, zie het leerprogramma op [&#x200B; hoe te om publieksgegevens aan de uitvoer van het partijprofiel bestemmingen te activeren gebruikend Experience Platform UI &#x200B;](../destinations/ui/activate-batch-profile-destinations.md) en de [&#x200B; gids op hoe te met partijbestemmingen te verbinden en gegevens te activeren gebruikend de Dienst API van de Stroom &#x200B;](../destinations/api/connect-activate-batch-destinations.md).

## Experience Platform-gegevensactiviteiten bewaken

Met Experience Platform kunt u bijhouden hoe gegevens worden verwerkt met behulp van gegevensstromen. Dit zijn weergaven van taken die gegevens over verschillende Experience Platform-componenten verplaatsen. Deze gegevensstromen worden gevormd over de verschillende diensten, die gegevens van bronschakelaars aan doeldatasets helpen bewegen, waar het dan door [!DNL Identity Service] en [!DNL Real-Time Customer Profile] wordt gebruikt alvorens uiteindelijk aan bestemmingen wordt geactiveerd. Het controledashboard voorziet u van een visuele vertegenwoordiging van de reis van een gegevensstroom. Leren hoe te om dataflows binnen Experience Platform UI te controleren, de leerprogramma&#39;s op [&#x200B; controledataflows voor bronnen &#x200B;](../dataflows/ui/monitor-sources.md) en [&#x200B; controledata voor bestemmingen &#x200B;](../dataflows/ui/monitor-destinations.md) zien.

U kunt de Experience Platform-activiteiten ook controleren met behulp van statistische gegevens en gebeurtenismeldingen met behulp van [!DNL Observability Insights] . U kunt zich abonneren op waarschuwingsmeldingen via de gebruikersinterface van Experience Platform of deze verzenden naar een geconfigureerde webhaak. Voor meer details op hoe te om, toe te laten, onbruikbaar te maken en aan beschikbare alarm van Experience Platform UI in te tekenen, zie de [[!UICONTROL Alerts] gids UI &#x200B;](../observability/alerts/ui.md). Voor details op hoe te om alarm door websites te ontvangen, zie de gids bij [&#x200B; het intekenen aan de berichten van de Gebeurtenis van Adobe I/O &#x200B;](../observability/alerts/subscribe.md).

## Volgende stappen

Door deze zelfstudie te lezen, hebt u een basisinleiding gekregen op een eenvoudige end-to-end flow voor Experience Platform. Meer over Adobe Experience Platform leren, gelieve het [&#x200B; overzicht van Experience Platform &#x200B;](./home.md) te lezen. Om meer over het gebruiken van Experience Platform UI en Experience Platform API te leren, te lezen gelieve de [&#x200B; gids van Experience Platform UI &#x200B;](./ui-guide.md) en de [&#x200B; gids van Experience Platform API &#x200B;](./api-guide.md) respectievelijk.

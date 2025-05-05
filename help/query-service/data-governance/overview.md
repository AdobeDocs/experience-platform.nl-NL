---
title: Gegevensbeheer in Query-service
description: Dit overzicht behandelt de belangrijkste elementen van gegevensbeheer in de Dienst van de Vraag van Experience Platform.
exl-id: 37543d43-bd8c-4bf9-88e5-39de5efe3164
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '3131'
ht-degree: 0%

---

# Gegevensbeheer in Query-service

Adobe Experience Platform brengt gegevens van meerdere bedrijfssystemen samen en stelt u in staat de gegevens te opschonen, vorm te geven, te manipuleren en te verrijken via Query Service, afhankelijk van uw behoeften. Dit staat marketers toe om, klanten op een betere manier te identificeren te begrijpen en in dienst te nemen. Het waarborgen van een adequaat beheer van gegevens is een cruciaal aspect bij de verwerking van persoonlijke informatie, aangezien bepaalde gegevens onderworpen kunnen zijn aan gebruiksbeperkingen op basis van organisatiebeleid en wettelijke voorschriften. Het is essentieel om ervoor te zorgen dat uw ingesloten gegevens en de bijbehorende bewerkingen voldoen aan het gedefinieerde beleid voor gegevensgebruik.

Het beheer van gegevens binnen de Dienst van de Vraag staat u toe om klantengegevens te beheren en naleving van verordeningen, beperkingen, en beleid te verzekeren toepasselijk op gegevensgebruik. Dit speelt een zeer belangrijke rol wanneer het verzekeren van het gebruiksbeleid is toegepast volgens de verordeningen die door uw zaken worden bepaald.

Organisaties die routinematig gegevensverwerking uitvoeren, wordt aangeraden deze richtlijnen te omschrijven, te gebruiken en af te dwingen om een privacybewuste omgeving voor alle gebruikers te maken.

De volgende categorieën zijn nuttig in het naleven van gegevensnalevingsverordeningen wanneer het gebruiken van de Dienst van de Vraag:

1. Beveiliging
1. Audit
1. Gegevensgebruik
1. Privacy
1. Gegevenshygiëne

Dit document onderzoekt elk van de verschillende gebieden van bestuur en toont aan hoe te om gegevensnaleving te vergemakkelijken wanneer het gebruiken van de Dienst van de Vraag. Zie [ bestuur, privacy, en veiligheidsoverzicht ](../../landing/governance-privacy-security/overview.md) voor bredere informatie over hoe Experience Platform u toestaat om klantengegevens te beheren en naleving te verzekeren.

## Beveiliging {#security}

De veiligheid van gegevens is het proces om gegevens tegen onbevoegde toegang te beschermen en veilige toegang door zijn levenscyclus te verzekeren. De veilige toegang wordt gehandhaafd in Experience Platform door de toepassing van rollen en toestemmingen door mogelijkheden zoals op rol-gebaseerd toegangsbeheer en op attribuut-gebaseerde toegangsbeheer. Credentials, SSL en gegevenscodering worden ook gebruikt om gegevensbeveiliging in Experience Platform te garanderen.

De veiligheid met betrekking tot de Dienst van de Vraag is verdeeld in de volgende categorieën:

* [ controle van de Toegang ](#access-control): De toegang wordt gecontroleerd door rollen en toestemmingen met inbegrip van dataset en kolom-vlakke toestemmingen.
* Het beveiligen van gegevens door [ connectiviteit ](#connectivity): Het gegeven wordt beveiligd door Experience Platform en externe cliënten door een beperkte verbinding met het verlopen van geloofsbrieven te bereiken, of niet-het verlopen geloofsbrieven.
* Het beveiligen van gegevens door [ encryptie en klant-beheerde sleutels (CMK) ](#encryption-and-customer-managed-keys): Toegang die door encryptie wordt gecontroleerd wanneer het gegeven in rust is.

### Toegangsbeheer {#access-control}

De controle van de toegang in Adobe Experience Platform laat u [ Adobe Admin Console ](https://adminconsole.adobe.com/) gebruiken om toegang tot de eigenschappen van de Dienst van de Vraag te beheren gebruikend op rol-gebaseerde toestemmingen. Op dezelfde manier kunt u toegang tot specifieke gegevensattributen door etiketbeheer op schema&#39;s en gegevensgebieden controleren.

Deze sectie schetst de vereiste toegangsbeheertoestemmingen die een gebruiker moet hebben om de eigenschappen van de Dienst van de Vraag volledig te gebruiken. Zie de documenten op [ het leiden toestemmingen ](../../access-control/ui/permissions.md) en [ het leiden gebruikers ](../../access-control/ui/users.md) voor gedetailleerde instructies bij het toewijzen van toegang tot een productprofiel.

#### Relevante machtigingen

De relevante toegangsbeheertoestemmingen worden bepaald in de lijsten hieronder op hun niveau van werkingsgebied.

**de uitvoeringstoestemmingen van de Vraag**

Om vragen binnen de Dienst van de Vraag in werking te stellen, moet een gebruiker een rol met de volgende toestemming worden toegewezen:

| Machtiging | Beschrijving |
|---|---|
| [!UICONTROL Manage Queries] | Deze toestemming staat gebruikers toe om gegevensexploratie en partijvragen uit te voeren, die of een bestaande dataset kan lezen of gegevens over datasets schrijven. Dit omvat zowel `CREATE TABLE AS SELECT` (`CTAS`) als `INSERT INTO AS SELECT` (`ITAS`) vragen. |

**toestemmingen van de Dataset**

Deze sectie dient als gids voor de op middel-gebaseerde toegang die wordt vereist om tot datasets toegang te hebben terwijl het vragen van gegevens door de Dienst van de Vraag.

Door de interface van Toestemmingen kunt u op middel-gebaseerde toegangsbeheer voor een dataset en schema met de volgende toestemmingen bepalen:

| Machtiging | Beschrijving |
|---|---|
| [!UICONTROL Manage Datasets] | Deze toestemming verleent read-only toegang voor schema&#39;s en verleent toegang om, datasets voor gebruik met de Dienst van de Vraag te lezen tot stand te brengen, uit te geven en te schrappen. |
| [!UICONTROL View Datasets] | Deze toestemming verleent read-only toegang voor datasets en schema&#39;s voor gebruik met de Dienst van de Vraag. |

#### Toegangsbeheer voor kolommen/velden

De op attribuut-gebaseerde eigenschap van het toegangsbeheer laat de gebruikers van de Dienst van de Vraag toe om toegang tot kritieke gebruikersgegevens te beperken. De toegang kan worden verleend of worden beperkt gebaseerd op de toestemmingen die aan een rol worden toegewezen. De toegang van de gebruiker tot individuele kolommen wordt gecontroleerd door de relevante etiketten van het gegevensgebruik en de toestemmingsreeksen die op de rollen worden toegepast die aan gebruikers worden toegewezen.

Als u schemaveldgroepen en -klassen codeert met labels voor gegevensgebruik, worden beperkingen voor gegevensgebruik toegepast op alle schema&#39;s met dezelfde veldgroepen en klassen. Zie het overzicht op [ op attributen-gebaseerde toegangsbeheer ](../../access-control/abac/overview.md) voor uitvoerige informatie over deze eigenschap.

Met deze functie kunt u toegangsrechten verlenen voor vertrouwelijke kolommen aan de gebruikersgroepen van uw keuze. Toegangsbeheer voor een kolom kan zowel de lees- als schrijfmogelijkheden voor een bepaald type gebruiker beperken.

Toegangsbeheer voor kolommen kan op schemaniveau voor zowel standaard als ad hoc schema&#39;s worden toegepast. Pas de etiketten van het gegevensgebruik op schema&#39;s XDM toe om toegang tot één of meerdere kolommen te beperken. Gegevenslabels worden consistent toegepast, zelfs voor datasets die via de Dienst van de Vraag worden gecreeerd gebruikend of een vooraf bepaald schema of een ad hoc schema dat als deel van verrichting CTAS wordt geproduceerd.

Zodra het aangewezen niveau van toegang gebruikend etiketten en rollen is toegepast, komt het volgende systeemgedrag voor wanneer een gebruiker probeert om tot de niet toegankelijke gegevens toegang te hebben:

1. Als een gebruiker toegang tot één van de kolommen binnen een schema is ontzegd, wordt de gebruiker ook toestemming ontzegd om op de beperkte kolom te lezen of te schrijven. Dit geldt voor de volgende algemene scenario&#39;s:

   * **Geval 1**: Wanneer een gebruiker probeert om een vraag uit te voeren die slechts een beperkte kolom beïnvloedt, werpt het systeem een fout dat de kolom niet bestaat.
   * **Geval 2**: Wanneer een gebruiker probeert om een vraag met veelvoudige kolommen met inbegrip van een beperkte kolom uit te voeren, keert het systeem output voor alle niet-beperkte slechts kolommen terug.

1. Als een gebruiker probeert om tot een berekend gebied toegang te hebben, wordt de gebruiker vereist om toegang tot alle gebieden te hebben die in de samenstelling worden gebruikt of het systeem ontkent ook toegang tot het berekende gebied.

#### Toegangsbesturingselementen voor weergaven

De Dienst van de vraag verstrekt de capaciteit om standaardANSI SQL voor [`CREATE VIEW`](../sql/syntax.md#create-view) verklaringen te gebruiken. Voor zeer gevoelige gegevenswerkstromen, moet u aangewezen controles afdwingen wanneer het creëren van meningen.

Het trefwoord `CREATE VIEW` definieert een weergave van een query, maar de weergave wordt niet fysiek weergegeven. In plaats daarvan, wordt de vraag in werking gesteld telkens als de mening in een vraag van verwijzingen wordt voorzien. Wanneer een gebruiker een mening van een dataset creeert, worden de op rol en eigenschap-gebaseerde toegangsbeheerregels voor de ouderdataset **niet** hiërarchisch toegepast. Dientengevolge, moet u toestemmingen op elk van de kolommen uitdrukkelijk plaatsen wanneer een mening wordt gecreeerd.

#### Creeer op gebied-gebaseerde toegangsbeperkingen op versnelde datasets {#create-field-based-access-restrictions-on-accelerated-datasets}

Met het [ op attribuut-gebaseerde vermogen van de toegangscontrole ](../../access-control/abac/overview.md) kunt u organisatorische of gegevensgebruikswerkingsgebieden op feit en afmetingsdatasets in de [ versnelde opslag ](../data-distiller/sql-insights/send-accelerated-queries.md) bepalen. Dit staat beheerders toe om toegang tot specifieke segmenten te beheren en beter de toegang te beheren die aan gebruikers of groepen gebruikers wordt gegeven.

Om op gebied-gebaseerde toegangsbeperkingen op versnelde datasets tot stand te brengen, kunt u de vragen van de Dienst CTAS van de Vraag gebruiken om versnelde datasets tot stand te brengen en deze datasets te structureren die op bestaande XDM schema&#39;s of ad hoc schema&#39;s worden gebaseerd. De beheerders kunnen dan [ gegevensgebruiksetiketten voor het schema ](../../xdm/tutorials/labels.md#edit-the-labels-for-the-schema-or-field) of [ ad hoc schema ](./ad-hoc-schema-labels.md#edit-governance-labels) toevoegen en uitgeven. U kunt labels toepassen, maken en bewerken op uw schema&#39;s vanuit de [!UICONTROL Labels] -werkruimte in de [!UICONTROL Schemas] -gebruikersinterface.

De etiketten van het gebruik van gegevens kunnen ook [ worden toegepast of direct op de dataset ](../../data-governance/labels/user-guide.md#add-labels) door de Datasets UI worden uitgegeven, of van de 2&rbrace; werkruimte van het Toegangsbeheer worden gecreeerd. [!UICONTROL Labels] Zie de gids op hoe te [ een nieuw etiket ](../../access-control/abac/ui/labels.md) voor meer informatie tot stand brengen.

De toegang van de gebruiker tot individuele kolommen kan dan door de etiketten van het gegevensgebruik in bijlage worden gecontroleerd en de toestemmingsreeksen die op de rollen worden toegepast die aan gebruikers worden toegewezen.

### Connectiviteit {#connectivity}

De Dienst van de vraag is toegankelijk door Experience Platform UI of door een verbinding met externe compatibele cliënten te vormen. De toegang tot alle beschikbare fronten wordt gecontroleerd door een reeks geloofsbrieven.

#### Connectiviteit via externe clients

De toegang tot de Dienst van de Vraag die een derdecliënt gebruikt vereist geloofsbrieven voor vergunning. Deze geloofsbrieven zijn verplicht om tot de Dienst van de Vraag met om het even welke compatibele externe cliënten toegang te hebben. U kunt met externe cliënten verbinden door of [ het verlopen geloofsbrieven ](#expiring-credentials) of [ niet-het verlopen geloofsbrieven ](#non-expiring-credentials) te gebruiken.

#### Beperkte verbindingstijd via verlopen van referenties {#expiring-credentials}

[ Vervalsende geloofsbrieven ](../ui/credentials.md) staan gebruikers toe om een tijdelijke verbinding met een externe cliënt te vormen. Deze set referenties is slechts 24 uur geldig. Het verstrijken van deze soorten geloofsbrieven kan samen met het credentielusje in het dashboard van de Dienst van de Vraag worden gezien.

![ het geloofsbrieven lusje in de werkruimte van de Dienst van de Vraag met het verlopen benadrukte geloofsbrieven.](../images/data-governance/overview/expiring-credentials.png)

#### Niet-verlopen referenties {#non-expiring-credentials}

[ Niet-vervallende geloofsbrieven ](../ui/credentials.md#non-expiring-credentials) staan u toe om een permanente verbinding met een externe cliënt te vormen, makend het gemakkelijker om met de Dienst van de Vraag zonder de behoefte aan een handwachtwoord te verbinden.

Om de optie toe te laten om niet-het verlopen geloofsbrieven te produceren, moet u het geschetste [ noodzakelijke werkschema ](../ui/credentials.md#prerequisites) volgen. Als deel van dit proces, wordt uw organisatiebeheerder vereist om toestemmingen voor het productprofiel te vormen, die de beheerdercontrole geven over welke rekeningen toegang hebben om niet-vervallende geloofsbrieven te gebruiken.

Technische gebruikersrekeningen die met niet-vervallende geloofsbrieven worden toegelaten kunnen rollen worden toegewezen om aangewezen gegevensbeheer te verzekeren door het werkingsgebied van hun lees te bepalen en toegang te schrijven die op hun verantwoordelijkheden en behoeften wordt gebaseerd. Zie de vroegere sectie op [ gebruikend op rol-gebaseerde toestemmingen door toegangsbeheer ](#access-control) om toegang tot de Dienst van de Vraag te beheren.

Zodra het in eerste instantie vereiste werkschema is voltooid, kunnen de erkende gebruikers [ de vereiste verbindingsgeloofsbrieven ](../ui/credentials.md#generate-credentials) nu produceren.

#### SSL-gegevenscodering

Voor verhoogde veiligheid, verleent de Dienst van de Vraag inheemse steun voor SSL verbindingen om cliënt/servermededelingen te coderen. Experience Platform biedt ondersteuning voor verschillende SSL-opties die zijn afgestemd op uw behoeften op het gebied van gegevensbeveiliging en die de verwerkingsoverhead van codering en sleuteluitwisseling op elkaar afstemmen.

Zie de gids op beschikbare [ SSL opties voor derdecliënt verbindingen aan de Dienst van de Vraag ](../clients/ssl-modes.md) voor meer informatie, met inbegrip van hoe te om het gebruiken van de `verify-full` SSL parameterwaarde te verbinden.

### Codering en door de klant beheerde sleutels (CMK) {#encryption-and-customer-managed-keys}

Codering is het gebruik van een algoritmisch proces om gegevens om te zetten in gecodeerde en onleesbare tekst om ervoor te zorgen dat de informatie zonder een decoderingssleutel wordt beschermd en ontoegankelijk is.

De de gegevensnaleving van de Dienst van de vraag zorgt ervoor dat het gegeven altijd wordt gecodeerd. Data-in-transit is altijd HTTPS-compatibel en data-at-rest wordt gecodeerd in een Azure Data Lake Store met systeemtoetsen. Zie de documentatie op [ hoe het gegeven in Adobe Experience Platform ](../../landing/governance-privacy-security/encryption.md) voor meer informatie wordt gecodeerd. Voor details op hoe de gegevens in rust in de Azure Opslag van het meer van Gegevens worden gecodeerd, zie de [ officiële Azure documentatie ](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption).

De gegevens-in-doorreis is altijd volgzaam HTTPS en zo ook wanneer de gegevens in rust in het gegevensmeer zijn, wordt de encryptie gedaan met Sleutel van het Beheer van de Klant (CMK), die reeds door het Beheer van het meer van Gegevens wordt gesteund. De momenteel ondersteunde versie is TLS1.2. Zie de [ klant-beheerde sleutels (CMK) documentatie ](../../landing/governance-privacy-security/customer-managed-keys/overview.md) om te leren hoe te opstelling uw eigen encryptiesleutels voor gegevens die in Adobe Experience Platform worden opgeslagen.


## Audit {#audit}

De Dienst van de vraag registreert gebruikersactiviteit en categoriseert die activiteit in verschillende logboektypes. Logs verstrekt informatie over **die** **uitvoerde wat** actie, en **wanneer**. Elke actie die in een logboek wordt geregistreerd bevat meta-gegevens die op het actietype, datum en tijd, e-mailidentiteitskaart van de gebruiker die de actie, en extra attributen relevant voor het actietype uitvoerde.

Een Experience Platform-gebruiker kan naar wens om een van de logcategorieën vragen. Deze sectie verstrekt details over het type van informatie die voor de Dienst van de Vraag wordt gevangen en waar deze informatie kan worden betreden.

### Zoekopdrachtlogs {#query-logs}

De UI van vraaglogboeken staat u toe om uitvoeringsdetails voor alle vragen te controleren en te herzien die of via de Redacteur van de Vraag of de Dienst API van de Vraag in werking zijn gesteld. Dit brengt transparantie aan de activiteiten van de Dienst van de Vraag, toestaand u om de meta-gegevens voor **alle** te controleren de vragen die over de Dienst van de Vraag zijn uitgevoerd. Het omvat alle types van vragen of het een verkennende, partij, of geplande vraag is.

U hebt toegang tot querylogboeken via de gebruikersinterface van Experience Platform op het tabblad [!UICONTROL Logs] van de werkruimte van [!UICONTROL Queries] .

![ het logboeklusje van Vragen met het benadrukte detailspaneel.](../images/data-governance/overview/queries-log.png)

### Controlelogboeken {#audit-logs}

De logboeken van de controle bevatten meer gedetailleerde informatie dan vraaglogboeken en laten u toe om logboeken te filtreren die op attributen zoals gebruiker, datum, type van vraag, etc. worden gebaseerd. Buiten de details beschikbaar in vraaglogboek UI, slaat de Logboeken van de Controle details op individuele gebruikers samen met hun zittingsgegevens of connectiviteit aan een derde cliënt op.

Door een nauwkeurige staat van dienst van gebruikersacties te verstrekken, kan een controletraject helpen bij het oplossen van problemenkwesties en uw zaken effectief helpen aan het beleid van het collectieve gegevensbeheer en regelgevende vereisten voldoen. Auditlogboeken bevatten een overzicht van alle Experience Platform-activiteiten. Gebruikend controlelogboeken kunt u gebruikersacties met betrekking tot vraaguitvoering, malplaatjes, en geplande vragen controleren om de transparantie en de zichtbaarheid van acties te verhogen die door gebruikers in de Dienst van de Vraag worden uitgevoerd.

De volgende lijst wijst op de vraagcategorieën die door controlelogboeken worden gevangen en de actietypes die zij registreren:

| Categorie | Type handeling |
|---|---|
| Query | Uitvoeren |
| Zoeksjabloon | Maken, verwijderen, bijwerken |
| Geplande query | Maken, verwijderen, bijwerken |

Hieronder ziet u een lijst met drie logboeken voor uitgebreide servers die meer details bevatten dan de logbestanden voor query&#39;s. De uitgebreide logboeken worden gevonden binnen de de vraagcategorieën van de controlelogboeken:

1. **de vraaglogboeken van Meta**: Wanneer een vraag wordt uitgevoerd, worden diverse bijbehorende achterste sub-query&#39;s (zoals het ontleden) uitgevoerd. Deze soorten vragen zijn genoemd geworden &quot;meta-gegevens&quot;vragen. De relevante gegevens zijn te vinden in de auditlogboeken.
1. **Logboeken van de Zitting**: Het systeem leidt tot een logboek van de zittingsingang voor een gebruiker wanneer zij in de Dienst van de Vraag registreren ongeacht of zij een vraag uitvoeren.
1. **Logboeken van de de cliëntverbinding van de derde**: Een logboek van de connectiviteitscontrole wordt geproduceerd wanneer een gebruiker met succes de Dienst van de Vraag met een derdecliënt verbindt.

Zie het [ overzicht van controlelogboeken ](../../landing/governance-privacy-security/audit-logs/overview.md) voor meer informatie over hoe de controlelogboeken uw naleving van organisatiegegevens kunnen helpen.

## Gegevensgebruik {#data-usage}

Het gegevensbeheerkader in Experience Platform biedt een uniforme manier om gegevens op verantwoorde wijze te gebruiken voor alle Adobe-oplossingen, -services en -platforms. Het coördineert de systemische benadering om, meta-gegevens over het volledige Adobe Experience Cloud te vangen, mee te delen en te gebruiken. Hierdoor kunnen de verantwoordelijken voor de verwerking van gegevens gegevens etiketteren op basis van de marketingacties die nodig zijn en de beperkingen die aan die gegevens zijn gesteld door deze beoogde marketingacties. Zie het overzicht op [ de etiketten van het gegevensgebruik ](../../data-governance/labels/overview.md) voor meer informatie over hoe het Beleid van Gegevens u toestaat om de etiketten van het gegevensgebruik op datasets en gebieden toe te passen.

Het is de beste praktijk om in elke fase van de gegevensreis te werken aan de naleving van de gegevensvereisten. Daartoe moeten afgeleide gegevensreeksen die ad-hocschema&#39;s gebruiken, op passende wijze worden geëtiketteerd als onderdeel van het kader voor gegevensbeheer. Er zijn twee soorten afgeleide datasets die door de Dienst van de Vraag worden gevormd: datasets die een standaardschema en datasets gebruiken die een ad hoc schema gebruiken.

>[!NOTE]
>
>Datasets die gebruikend de Dienst van de Vraag worden gecreeerd worden bedoeld als &quot;afgeleide datasets&quot;.

Aangezien de ad hoc regelingen door een individuele gebruiker voor een specifiek doel worden gecreeerd, worden de XDM schemagebieden namespaced voor die bepaalde dataset en niet bedoeld voor gebruik over verschillende datasets. Het resultaat is dat ad-hocschema&#39;s standaard niet zichtbaar zijn in de gebruikersinterface van Experience Platform. Hoewel er geen verschil in de toepassing van de etiketten van het gegevensgebruik tussen zowel standaard als ad hoc regelingen is, moeten de ad hoc regelingen die door de Dienst van de Vraag voor het etiketteren worden gecreeerd eerst zichtbaar in Experience Platform UI worden gemaakt. Zie de gids op [ ontdekkend ad hoc schema&#39;s binnen Experience Platform UI ](./ad-hoc-schema-labels.md#discover-ad-hoc-schemas) voor meer details.

Nadat u het schema hebt betreden, kunt u [ etiketten op individuele gebieden ](../../xdm/tutorials/labels.md) toepassen. Zodra een schema is geëtiketteerd, erven alle datasets die uit dat schema voortkomen die etiketten. Van hier, kunt u beleid van het opstellingsgegevensgebruik dat gegevens met bepaalde etiketten kan beperken van worden geactiveerd aan bepaalde bestemmingen. Voor meer informatie, zie het overzicht over [ beleid van het gegevensgebruik ](../../data-governance/policies/overview.md).

## Privacy {#privacy}

[ Privacy Service ](../../privacy-service/home.md) helpt u klantenverzoeken beheren om tot hun gegevens in overeenstemming met wettelijke privacyverordeningen toegang te hebben en te schrappen. Dit gebeurt door de gegevens te zoeken op bestaande id&#39;s en deze gegevens te openen of te verwijderen, afhankelijk van de gevraagde privacytaak. De gegevens moeten correct geëtiketteerd zijn opdat de dienst kan bepalen welke gebieden om tijdens privacybanen toegang te hebben of te schrappen. Gegevens waarop privacyverzoeken betrekking hebben, moeten identiteitsgegevens van de klant bevatten om de verschillende gegevens te koppelen aan de individuele persoon op wie het privacyverzoek van toepassing is. De Dienst van de vraag kan de gegevens verrijken het met een uniek herkenningsteken voor het voldoen aan privacybanen gebruikt.

De verzoeken van de privacy kunnen worden verzonden naar het gegevens meer of de gegevensopslag van het Profiel. Records die uit het datumpeer zijn verwijderd, leiden niet tot het verwijderen van profielen die uit deze records zijn gemaakt. Bovendien verwijdert een privacytaak om persoonlijke gegevens uit het datumpomeer te verwijderen hun profiel niet, zodat alle informatie (die die profiel-id bevat) die wordt opgenomen nadat de privacytaak is voltooid, dat profiel normaal bijwerken. Dit bevestigt opnieuw de noodzaak om gegevens die worden gebruikt in ad-hocschema&#39;s naar behoren te identificeren.

Zie de documentatie van Privacy Service voor meer informatie over [ identiteitsgegevens voor privacyverzoeken ](../../privacy-service/identity-data.md) en hoe te om uw gegevensverrichtingen en technologieën van hefboomwerkingAdobe te vormen om de aangewezen identiteitsinformatie voor de verzoeken van de klantenprivacy effectief terug te winnen.

De eigenschappen van de Dienst van de vraag voor gegevensbeheer vereenvoudigen en stroomlijnen het proces van gegevenscategorisering en naleving van de verordeningen van het gegevensgebruik. Zodra het gegeven is geïdentificeerd, laat de Dienst van de Vraag u toe om de primaire identiteit op alle outputdatasets toe te wijzen. U **moet** identiteiten in de dataset toevoegen om de verzoeken van de gegevensprivacy te vergemakkelijken en aan gegevensnaleving te werken.

De gegevensgebieden van het schema kunnen als identiteitsgebied door Experience Platform UI en de Dienst van de Vraag worden geplaatst staat u ook toe om de primaire identiteiten te merken door SQL bevel &quot;ALTER TABLE&quot;te gebruiken [&#128279;](../sql/syntax.md#alter-table).  Het instellen van een identiteit met de opdracht `ALTER TABLE` is vooral handig wanneer gegevenssets worden gemaakt met SQL in plaats van rechtstreeks via een schema via de gebruikersinterface van Experience Platform. Zie de documentatie voor instructies op hoe te [ identiteitsgebieden in UI ](../../xdm/ui/fields/identity.md) bepalen wanneer het gebruiken van standaardschema&#39;s.

## Gegevenshygiëne {#data-hygiene}

Met &quot;gegevenshygiëne&quot; wordt bedoeld het repareren of verwijderen van gegevens die verouderd, onjuist, onjuist opgemaakt, gedupliceerd of onvolledig kunnen zijn. Deze processen zorgen ervoor dat de datasets over alle systemen nauwkeurig en verenigbaar zijn. Het is van belang te zorgen voor adequate gegevenshygiëne tijdens elke stap van de reis van de gegevens en zelfs vanaf de eerste plaats van gegevensopslag. In de Dienst van de Vraag van Experience Platform, is dit of het gegevens meer of de versnelde opslag.

U kunt een identiteit aan een afgeleide dataset toewijzen om hun gegevensbeheer na de gecentraliseerde diensten van de de gegevenshygiëne van Experience Platform toe te staan.

Omgekeerd, wanneer u een samengevoegde dataset op de versnelde opslag creeert, kunnen de samengevoegde gegevens niet worden gebruikt om de originele gegevens af te leiden. Als gevolg van deze gegevensaggregatie wordt de noodzaak om verzoeken om gegevenshygiëne te verzamelen, weggenomen.

Een uitzondering op dit scenario is het geval van schrapping. Als een gegevenshygiëneschrapping op een dataset wordt gevraagd en alvorens de schrapping wordt voltooid, wordt een andere afgeleide datasetvraag uitgevoerd, dan zal de afgeleide dataset informatie van de originele dataset vangen. In dit geval, moet u erop letten dat als een verzoek om een dataset te schrappen is verzonden, u geen onlangs afgeleide datasetvragen moet uitvoeren gebruikend de zelfde datasetbron.

Zie het [ overzicht van de gegevenshygiëne ](../../hygiene/home.md) voor meer informatie over gegevenshygiëne in Adobe Experience Platform.

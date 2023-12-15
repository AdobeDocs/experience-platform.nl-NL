---
title: Gegevensbeheer in Query-service
description: Dit overzicht behandelt de belangrijkste elementen van gegevensbeheer in de Dienst van de Vraag van het Experience Platform.
exl-id: 37543d43-bd8c-4bf9-88e5-39de5efe3164
source-git-commit: 18c1d32bbc2732c38a9c37ee8fb9d36a23d4e515
workflow-type: tm+mt
source-wordcount: '3118'
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

Dit document onderzoekt elk van de verschillende gebieden van bestuur en toont aan hoe te om gegevensnaleving te vergemakkelijken wanneer het gebruiken van de Dienst van de Vraag. Zie de [beheer, privacy en beveiligingsoverzicht](../../landing/governance-privacy-security/overview.md) voor uitgebreidere informatie over hoe u met Experience Platform klantgegevens kunt beheren en naleving kunt garanderen.

## Beveiliging {#security}

De veiligheid van gegevens is het proces om gegevens tegen onbevoegde toegang te beschermen en veilige toegang door zijn levenscyclus te verzekeren. De veilige toegang wordt gehandhaafd in Experience Platform door de toepassing van rollen en toestemmingen door mogelijkheden zoals op rol-gebaseerd toegangsbeheer en op attribuut-gebaseerde toegangsbeheer. De geloofsbrieven, SSL, en de gegevensencryptie worden ook gebruikt om gegevensbescherming over Platform te verzekeren.

De veiligheid met betrekking tot de Dienst van de Vraag is verdeeld in de volgende categorieën:

* [Toegangsbeheer](#access-control): De toegang wordt gecontroleerd door rollen en toestemmingen met inbegrip van dataset en kolom-vlakke toestemmingen.
* Gegevens beveiligen via [connectiviteit](#connectivity): De gegevens worden beveiligd door Platform en externe cliënten door een beperkte verbinding met het verlopen van geloofsbrieven te bereiken, of niet-vervallende geloofsbrieven.
* Gegevens beveiligen via [codering en door de klant beheerde sleutels (CMK)](#encryption-and-customer-managed-keys): Toegang die wordt beheerd door versleuteling wanneer gegevens in rust zijn.

### Toegangsbeheer {#access-control}

Met toegangsbeheer in Adobe Experience Platform kunt u [Adobe Admin Console](https://adminconsole.adobe.com/) om toegang tot de eigenschappen van de Dienst van de Vraag te beheren gebruikend op rol-gebaseerde toestemmingen. Op dezelfde manier kunt u toegang tot specifieke gegevensattributen door etiketbeheer op schema&#39;s en gegevensgebieden controleren.

Deze sectie schetst de vereiste toegangsbeheertoestemmingen die een gebruiker moet hebben om de eigenschappen van de Dienst van de Vraag volledig te gebruiken. Zie de documenten op [machtigingen beheren](../../access-control/ui/permissions.md) en [gebruikers beheren](../../access-control/ui/users.md) voor gedetailleerde instructies voor het toewijzen van toegang tot een productprofiel.

#### Relevante machtigingen

De relevante toegangsbeheertoestemmingen worden bepaald in de lijsten hieronder op hun niveau van werkingsgebied.

**Machtigingen voor het uitvoeren van query**

Om vragen binnen de Dienst van de Vraag in werking te stellen, moet een gebruiker een rol met de volgende toestemming worden toegewezen:

| Machtiging | Beschrijving |
|---|---|
| [!UICONTROL Manage Queries] | Deze toestemming staat gebruikers toe om gegevensexploratie en partijvragen uit te voeren, die of een bestaande dataset kan lezen of gegevens over datasets schrijven. Dit omvat beide `CREATE TABLE AS SELECT` (`CTAS`) en `INSERT INTO AS SELECT` (`ITAS`). |

**Machtigingen gegevensset**

Deze sectie dient als gids voor de op middel-gebaseerde toegang die wordt vereist om tot datasets toegang te hebben terwijl het vragen van gegevens door de Dienst van de Vraag.

Door de interface van Toestemmingen kunt u op middel-gebaseerde toegangsbeheer voor een dataset en schema met de volgende toestemmingen bepalen:

| Machtiging | Beschrijving |
|---|---|
| [!UICONTROL Manage Datasets] | Deze toestemming verleent read-only toegang voor schema&#39;s en verleent toegang om, datasets voor gebruik met de Dienst van de Vraag te lezen tot stand te brengen, uit te geven en te schrappen. |
| [!UICONTROL View Datasets] | Deze toestemming verleent read-only toegang voor datasets en schema&#39;s voor gebruik met de Dienst van de Vraag. |

#### Toegangsbeheer voor kolommen/velden

De op attribuut-gebaseerde eigenschap van het toegangsbeheer laat de gebruikers van de Dienst van de Vraag toe om toegang tot kritieke gebruikersgegevens te beperken. De toegang kan worden verleend of worden beperkt gebaseerd op de toestemmingen die aan een rol worden toegewezen. De toegang van de gebruiker tot individuele kolommen wordt gecontroleerd door de relevante etiketten van het gegevensgebruik en de toestemmingsreeksen die op de rollen worden toegepast die aan gebruikers worden toegewezen.

Als u schemaveldgroepen en -klassen codeert met labels voor gegevensgebruik, worden beperkingen voor gegevensgebruik toegepast op alle schema&#39;s met dezelfde veldgroepen en klassen. Zie het overzicht op [attribuut-based toegangsbeheer](../../access-control/abac/overview.md) voor uitgebreide informatie over deze functie.

Met deze functie kunt u toegangsrechten verlenen voor vertrouwelijke kolommen aan de gebruikersgroepen van uw keuze. Toegangsbeheer voor een kolom kan zowel de lees- als schrijfmogelijkheden voor een bepaald type gebruiker beperken.

Toegangsbeheer voor kolommen kan op schemaniveau voor zowel standaard als ad hoc schema&#39;s worden toegepast. Pas de etiketten van het gegevensgebruik op schema&#39;s XDM toe om toegang tot één of meerdere kolommen te beperken. Gegevenslabels worden consistent toegepast, zelfs voor datasets die via de Dienst van de Vraag worden gecreeerd gebruikend of een vooraf bepaald schema of een ad hoc schema dat als deel van verrichting CTAS wordt geproduceerd.

Zodra het aangewezen niveau van toegang gebruikend etiketten en rollen is toegepast, komt het volgende systeemgedrag voor wanneer een gebruiker probeert om tot de niet toegankelijke gegevens toegang te hebben:

1. Als een gebruiker toegang tot één van de kolommen binnen een schema is ontzegd, wordt de gebruiker ook toestemming ontzegd om op de beperkte kolom te lezen of te schrijven. Dit geldt voor de volgende algemene scenario&#39;s:

   * **Geval 1**: Wanneer een gebruiker een query probeert uit te voeren die alleen van invloed is op een beperkte kolom, genereert het systeem een fout die de kolom niet bestaat.
   * **Zaak 2**: Wanneer een gebruiker een query probeert uit te voeren met meerdere kolommen inclusief een beperkte kolom, retourneert het systeem alleen uitvoer voor alle niet-beperkte kolommen.

1. Als een gebruiker probeert om tot een berekend gebied toegang te hebben, wordt de gebruiker vereist om toegang tot alle gebieden te hebben die in de samenstelling worden gebruikt of het systeem ontkent ook toegang tot het berekende gebied.

#### Toegangsbesturingselementen voor weergaven

De Dienst van de vraag verstrekt de capaciteit standaardANSI SQL voor te gebruiken [`CREATE VIEW`](../sql/syntax.md#create-view) instructies. Voor zeer gevoelige gegevenswerkstromen, moet u aangewezen controles afdwingen wanneer het creëren van meningen.

De `CREATE VIEW` het sleutelwoord bepaalt een mening van een vraag maar de mening is fysisch niet materialized. In plaats daarvan, wordt de vraag in werking gesteld telkens als de mening in een vraag van verwijzingen wordt voorzien. Wanneer een gebruiker een mening van een dataset creeert, zijn de op rol en attribuut-gebaseerde toegangsbeheerregels voor de ouderdataset **niet** hiërarchisch toegepast. Dientengevolge, moet u toestemmingen op elk van de kolommen uitdrukkelijk plaatsen wanneer een mening wordt gecreeerd.

#### Creeer op gebied-gebaseerde toegangsbeperkingen op versnelde datasets {#create-field-based-access-restrictions-on-accelerated-datasets}

Met de [attribuut-based toegangsbeheervermogen](../../access-control/abac/overview.md) u kunt organisatorische of gegevensgebruikswerkingsgebieden op feiten en afmetingsdatasets in bepalen [versnelde opslag](../data-distiller/customizable-insights/send-accelerated-queries.md). Dit staat beheerders toe om toegang tot specifieke segmenten te beheren en beter de toegang te beheren die aan gebruikers of groepen gebruikers wordt gegeven.

Om op gebied-gebaseerde toegangsbeperkingen op versnelde datasets tot stand te brengen, kunt u de vragen van de Dienst CTAS van de Vraag gebruiken om versnelde datasets tot stand te brengen en deze datasets te structureren die op bestaande XDM schema&#39;s of ad hoc schema&#39;s worden gebaseerd. Beheerders kunnen vervolgens [labels voor gegevensgebruik toevoegen en bewerken voor het schema](../../xdm/tutorials/labels.md#edit-the-labels-for-the-schema-or-field) of [ad-hocschema](./ad-hoc-schema-labels.md#edit-governance-labels). U kunt labels op uw schema&#39;s toepassen, maken en bewerken via het menu [!UICONTROL Labels] werkruimte in de [!UICONTROL Schemas] UI.

Met labels voor gegevensgebruik kunt u ook [rechtstreeks toegepast of bewerkt op de gegevensset](../../data-governance/labels/user-guide.md#add-labels) door Datasets UI, of gecreeerd van het Toegangsbeheer [!UICONTROL Labels] werkruimte. Zie de handleiding over hoe u [een nieuw label maken](../../access-control/abac/ui/labels.md) voor meer informatie .

De toegang van de gebruiker tot individuele kolommen kan dan door de etiketten van het gegevensgebruik in bijlage worden gecontroleerd en de toestemmingsreeksen die op de rollen worden toegepast die aan gebruikers worden toegewezen.

### Connectiviteit {#connectivity}

De Dienst van de vraag is toegankelijk door Platform UI of door een verbinding met externe compatibele cliënten te vormen. De toegang tot alle beschikbare fronten wordt gecontroleerd door een reeks geloofsbrieven.

#### Connectiviteit via externe clients

De toegang tot de Dienst van de Vraag die een derdecliënt gebruikt vereist geloofsbrieven voor vergunning. Deze geloofsbrieven zijn verplicht om tot de Dienst van de Vraag met om het even welke compatibele externe cliënten toegang te hebben. U kunt verbinding maken met externe clients met behulp van [verlopen van referenties](#expiring-credentials) of [niet-verlopen referenties](#non-expiring-credentials).

#### Beperkte verbindingstijd via verlopen van referenties {#expiring-credentials}

[Referenties vervallen](../ui/credentials.md) gebruikers toestaan een tijdelijke verbinding met een externe client te maken. Deze set referenties is slechts 24 uur geldig. Het verstrijken van deze soorten geloofsbrieven kan samen met het credentielusje in het dashboard van de Dienst van de Vraag worden gezien.

![Het lusje van geloofsbrieven in de werkruimte van de Dienst van de Vraag met benadrukte het verlopen geloofsbrieven.](../images/data-governance/overview/expiring-credentials.png)

#### Niet-verlopen referenties {#non-expiring-credentials}

[Niet-verlopen referenties](../ui/credentials.md#non-expiring-credentials) kunt u een permanente verbinding met een externe cliënt vormen, die het gemakkelijker maakt om met de Dienst van de Vraag zonder de behoefte aan een handwachtwoord te verbinden.

Als u de optie voor het genereren van niet-vervallende gegevens wilt inschakelen, moet u de [vereiste workflow](../ui/credentials.md#prerequisites). Als deel van dit proces, wordt uw organisatiebeheerder vereist om toestemmingen voor het productprofiel te vormen, die de beheerdercontrole geven over welke rekeningen toegang hebben om niet-vervallende geloofsbrieven te gebruiken.

Technische gebruikersrekeningen die met niet-vervallende geloofsbrieven worden toegelaten kunnen rollen worden toegewezen om aangewezen gegevensbeheer te verzekeren door het werkingsgebied van hun lees te bepalen en toegang te schrijven die op hun verantwoordelijkheden en behoeften wordt gebaseerd. Zie de vorige sectie over [het gebruiken van op rol-gebaseerde toestemmingen door toegangsbeheer](#access-control) om toegang tot de Dienst van de Vraag te beheren.

Zodra de vereiste workflow is voltooid, kunnen geautoriseerde gebruikers nu [de vereiste verbindingsgegevens genereren](../ui/credentials.md#generate-credentials).

#### SSL-gegevenscodering

Voor verhoogde veiligheid, verleent de Dienst van de Vraag inheemse steun voor SSL verbindingen om cliënt/servermededelingen te coderen. Platform ondersteunt verschillende SSL-opties die aansluiten bij uw behoeften op het gebied van gegevensbeveiliging en die een evenwicht vormen tussen de verwerkingsoverhead van codering en sleuteluitwisseling.

Zie de handleiding op beschikbaar [SSL-opties voor clientverbindingen van derden met Query Service](../clients/ssl-modes.md) voor meer informatie, zoals hoe u verbinding kunt maken met de `verify-full` SSL-parameterwaarde.

### Codering en door de klant beheerde sleutels (CMK) {#encryption-and-customer-managed-keys}

Codering is het gebruik van een algoritmisch proces om gegevens om te zetten in gecodeerde en onleesbare tekst om ervoor te zorgen dat de informatie zonder een decoderingssleutel wordt beschermd en ontoegankelijk is.

De de gegevensnaleving van de Dienst van de vraag zorgt ervoor dat het gegeven altijd wordt gecodeerd. Data-in-transit is altijd HTTPS-compatibel en data-at-rest wordt gecodeerd in een Azure Data Lake Store met systeemtoetsen. Zie de documentatie op [hoe gegevens in Adobe Experience Platform worden gecodeerd](../../landing/governance-privacy-security/encryption.md) voor meer informatie . Zie voor meer informatie over hoe gegevens in rust in Azure Data Lake Storage gecodeerd zijn [officiële Azure-documentatie](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption).

De gegevens-in-doorreis is altijd volgzaam HTTPS en zo ook wanneer de gegevens in rust in het gegevensmeer zijn, wordt de encryptie gedaan met Sleutel van het Beheer van de Klant (CMK), die reeds door het Beheer van het meer van Gegevens wordt gesteund. De momenteel ondersteunde versie is TLS1.2. Zie de [documentatie over door de klant beheerde sleutels (CMK)](../../landing/governance-privacy-security/customer-managed-keys/overview.md) om te leren hoe u uw eigen coderingssleutels instelt voor gegevens die in Adobe Experience Platform zijn opgeslagen.


## Audit {#audit}

De Dienst van de vraag registreert gebruikersactiviteit en categoriseert die activiteit in verschillende logboektypes. Logboeken verstrekken informatie over **wie** uitgevoerd **wat** actie, en **wanneer**. Elke actie die in een logboek wordt geregistreerd bevat meta-gegevens die op het actietype, datum en tijd, e-mailidentiteitskaart van de gebruiker die de actie, en extra attributen relevant voor het actietype uitvoerde.

Om het even welke logboekcategorieën kunnen worden gevraagd zoals gewenst door een gebruiker van het Platform. Deze sectie verstrekt details over het type van informatie die voor de Dienst van de Vraag wordt gevangen en waar deze informatie kan worden betreden.

### Zoekopdrachtlogs {#query-logs}

De UI van vraaglogboeken staat u toe om uitvoeringsdetails voor alle vragen te controleren en te herzien die of via de Redacteur van de Vraag of de Dienst API van de Vraag in werking zijn gesteld. Dit brengt transparantie aan de activiteiten van de Dienst van de Vraag, toestaand u de meta-gegevens voor controleren **alles** de vragen die over de Dienst van de Vraag zijn uitgevoerd. Het omvat alle types van vragen of het een verkennende, partij, of geplande vraag is.

U kunt de logboeken van de query openen via de interface van het platform in het dialoogvenster [!UICONTROL Logs] tabblad van het [!UICONTROL Queries] werkruimte.

![Het tabblad Vragenlijsten met het deelvenster Details gemarkeerd.](../images/data-governance/overview/queries-log.png)

### Controlelogboeken {#audit-logs}

De logboeken van de controle bevatten meer gedetailleerde informatie dan vraaglogboeken en laten u toe om logboeken te filtreren die op attributen zoals gebruiker, datum, type van vraag, etc. worden gebaseerd. Buiten de details beschikbaar in vraaglogboek UI, slaat de Logboeken van de Controle details op individuele gebruikers samen met hun zittingsgegevens of connectiviteit aan een derde cliënt op.

Door een nauwkeurige staat van dienst van gebruikersacties te verstrekken, kan een controletraject helpen bij het oplossen van problemenkwesties en uw zaken effectief helpen aan het beleid van het collectieve gegevensbeheer en regelgevende vereisten voldoen. De logboeken van de controle verstrekken een verslag van alle activiteiten van het Platform. Gebruikend controlelogboeken kunt u gebruikersacties met betrekking tot vraaguitvoering, malplaatjes, en geplande vragen controleren om de transparantie en de zichtbaarheid van acties te verhogen die door gebruikers in de Dienst van de Vraag worden uitgevoerd.

De volgende lijst wijst op de vraagcategorieën die door controlelogboeken worden gevangen en de actietypes die zij registreren:

| Categorie | Type handeling |
|---|---|
| Query | Uitvoeren |
| Zoeksjabloon | Maken, verwijderen, bijwerken |
| Geplande query | Maken, verwijderen, bijwerken |

Hieronder ziet u een lijst met drie logboeken voor uitgebreide servers die meer details bevatten dan de logbestanden voor query&#39;s. De uitgebreide logboeken worden gevonden binnen de de vraagcategorieën van de controlelogboeken:

1. **Meta-querylogs**: Wanneer een vraag wordt uitgevoerd, worden diverse bijbehorende achterste sub-query&#39;s (zoals het ontleden) uitgevoerd. Deze soorten vragen zijn genoemd geworden &quot;meta-gegevens&quot;vragen. De relevante gegevens zijn te vinden in de auditlogboeken.
1. **Sessielogboeken**: Het systeem leidt tot een logboek van de zittingsingang voor een gebruiker wanneer zij login de Dienst van de Vraag ongeacht of zij een vraag uitvoeren.
1. **Logbestanden van clientverbindingen van derden**: Een logboek van de connectiviteitscontrole wordt geproduceerd wanneer een gebruiker met succes de Dienst van de Vraag met een derdecliënt verbindt.

Zie de [overzicht van auditlogboeken](../../landing/governance-privacy-security/audit-logs/overview.md) voor meer informatie over hoe de controlelogboeken uw organisatie kunnen helpen gegevensnaleving benaderen.

## Gegevensgebruik {#data-usage}

Het gegevensgovernancekader in Platform biedt een uniforme manier om gegevens op verantwoordelijke wijze te gebruiken voor alle oplossingen, services en platforms van de Adobe. Het coördineert de systemische benadering om, meta-gegevens over het volledige Adobe Experience Cloud te vangen, mee te delen en te gebruiken. Hierdoor kunnen de verantwoordelijken voor de verwerking van gegevens gegevens etiketteren op basis van de marketingacties die nodig zijn en de beperkingen die aan die gegevens zijn gesteld door deze beoogde marketingacties. Zie het overzicht op [gegevensgebruikslabels](../../data-governance/labels/overview.md) voor meer informatie over hoe het Beleid van Gegevens u toestaat om de etiketten van het gegevensgebruik op datasets en gebieden toe te passen.

Het is de beste praktijk om in elke fase van de gegevensreis te werken aan de naleving van de gegevensvereisten. Daartoe moeten afgeleide gegevensreeksen die ad-hocschema&#39;s gebruiken, op passende wijze worden geëtiketteerd als onderdeel van het kader voor gegevensbeheer. Er zijn twee soorten afgeleide datasets die door de Dienst van de Vraag worden gevormd: datasets die een standaardschema en datasets gebruiken die een ad hoc schema gebruiken.

>[!NOTE]
>
>Datasets die gebruikend de Dienst van de Vraag worden gecreeerd worden bedoeld als &quot;afgeleide datasets&quot;.

Aangezien de ad hoc regelingen door een individuele gebruiker voor een specifiek doel worden gecreeerd, worden de XDM schemagebieden namespaced voor die bepaalde dataset en niet bedoeld voor gebruik over verschillende datasets. Het resultaat is dat ad-hocschema&#39;s standaard niet zichtbaar zijn in de gebruikersinterface van het Experience Platform. Hoewel er geen verschil in de toepassing van de etiketten van het gegevensgebruik tussen zowel standaard als ad hoc regelingen is, moeten de ad hoc regelingen die door de Dienst van de Vraag voor het etiketteren worden gecreeerd eerst in Platform UI zichtbaar worden gemaakt. Zie de handleiding op [ontdekken van ad-hocschema&#39;s binnen de interface van het platform](./ad-hoc-schema-labels.md#discover-ad-hoc-schemas) voor meer informatie .

Nadat u het schema hebt geopend, kunt u [labels toepassen op afzonderlijke velden](../../xdm/tutorials/labels.md). Zodra een schema is geëtiketteerd, erven alle datasets die uit dat schema voortkomen die etiketten. Van hier, kunt u beleid van het opstellingsgegevensgebruik dat gegevens met bepaalde etiketten kan beperken van worden geactiveerd aan bepaalde bestemmingen. Zie het overzicht over [beleid voor gegevensgebruik](../../data-governance/policies/overview.md).

## Privacy {#privacy}

[Privacy Service](../../privacy-service/home.md) helpt u klantenverzoeken te beheren om tot hun gegevens toegang te hebben en te schrappen in overeenstemming met wettelijke privacyverordeningen. Dit gebeurt door de gegevens te zoeken op bestaande id&#39;s en deze gegevens te openen of te verwijderen, afhankelijk van de gevraagde privacytaak. De gegevens moeten correct geëtiketteerd zijn opdat de dienst kan bepalen welke gebieden om tijdens privacybanen toegang te hebben of te schrappen. Gegevens waarop privacyverzoeken betrekking hebben, moeten identiteitsgegevens van de klant bevatten om de verschillende gegevens te koppelen aan de individuele persoon op wie het privacyverzoek van toepassing is. De Dienst van de vraag kan de gegevens verrijken het met een uniek herkenningsteken voor het voldoen aan privacybanen gebruikt.

De verzoeken van de privacy kunnen worden verzonden naar het gegevens meer of de gegevensopslag van het Profiel. Records die uit het datumpeer zijn verwijderd, leiden niet tot het verwijderen van profielen die uit deze records zijn gemaakt. Bovendien verwijdert een privacytaak om persoonlijke gegevens uit het datumpomeer te verwijderen hun profiel niet, zodat alle informatie (die die profiel-id bevat) die wordt opgenomen nadat de privacytaak is voltooid, dat profiel normaal bijwerken. Dit bevestigt opnieuw de noodzaak om gegevens die worden gebruikt in ad-hocschema&#39;s naar behoren te identificeren.

Raadpleeg de documentatie bij de Privacy Service voor meer informatie over [identiteitsgegevens voor privacyverzoeken](../../privacy-service/identity-data.md) en hoe te om uw gegevensverrichtingen en hefboomwerking Adobe technologieën te vormen om de aangewezen identiteitsinformatie voor de verzoeken van de klantenprivacy effectief terug te winnen.

De eigenschappen van de Dienst van de vraag voor gegevensbeheer vereenvoudigen en stroomlijnen het proces van gegevenscategorisering en naleving van de verordeningen van het gegevensgebruik. Zodra het gegeven is geïdentificeerd, laat de Dienst van de Vraag u toe om de primaire identiteit op alle outputdatasets toe te wijzen. U **moet** toevoegen van identiteiten aan de dataset om verzoeken om privacy van gegevens te vergemakkelijken en te werken aan de naleving van de gegevensvereisten.

De de gegevensgebieden van het schema kunnen als identiteitsgebied door Platform UI en de Dienst van de Vraag ook worden geplaatst staat u toe om [markeer de primaire identiteiten door het SQL bevel &quot;ALTER TABLE&quot;te gebruiken](../sql/syntax.md#alter-table). Een identiteit instellen met de opdracht `ALTER TABLE` bevel is vooral nuttig wanneer datasets gebruikend SQL eerder dan direct van een schema door Platform UI worden gecreeerd. Zie de documentatie voor instructies over hoe u kunt [identiteitsvelden definiëren in de gebruikersinterface](../../xdm/ui/fields/identity.md) bij het gebruik van standaardschema&#39;s.

## Gegevenshygiëne {#data-hygiene}

Met &quot;gegevenshygiëne&quot; wordt bedoeld het repareren of verwijderen van gegevens die verouderd, onjuist, onjuist opgemaakt, gedupliceerd of onvolledig kunnen zijn. Deze processen zorgen ervoor dat de datasets over alle systemen nauwkeurig en verenigbaar zijn. Het is van belang te zorgen voor adequate gegevenshygiëne tijdens elke stap van de reis van de gegevens en zelfs vanaf de eerste plaats van gegevensopslag. In de Dienst van de Vraag van het Experience Platform, is dit of het gegevens meer of de versnelde opslag.

U kunt een identiteit aan een afgeleide dataset toewijzen om hun gegevensbeheer na de gecentraliseerde diensten van de Gegevenshygiëne van het Platform toe te staan.

Omgekeerd, wanneer u een samengevoegde dataset op de versnelde opslag creeert, kunnen de samengevoegde gegevens niet worden gebruikt om de originele gegevens af te leiden. Als gevolg van deze gegevensaggregatie wordt de noodzaak om verzoeken om gegevenshygiëne te verzamelen, weggenomen.

Een uitzondering op dit scenario is het geval van schrapping. Als een gegevenshygiëneschrapping op een dataset wordt gevraagd en alvorens de schrapping wordt voltooid, wordt een andere afgeleide datasetvraag uitgevoerd, dan zal de afgeleide dataset informatie van de originele dataset vangen. In dit geval, moet u erop letten dat als een verzoek om een dataset te schrappen is verzonden, u geen onlangs afgeleide datasetvragen moet uitvoeren gebruikend de zelfde datasetbron.

Zie de [overzicht van de gegevenshygiëne](../../hygiene/home.md) voor meer informatie over gegevenshygiëne in Adobe Experience Platform.

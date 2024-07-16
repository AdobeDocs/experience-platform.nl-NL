---
title: Opmerkingen bij de release van Adobe Experience Platform november 2020
description: De release van november 2020 bevat notities voor Adobe Experience Platform.
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
exl-id: 29179b56-e49a-44e8-8c64-a7c383c2eaaf
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '2153'
ht-degree: 2%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: donderdag 11 november 2020**

Nieuwe functies in Adobe Experience Platform:

- [Adobe Experience Platform Data Lake-migratie](#migration)
- [[!DNL Access control]](#access-control)
- [[!DNL Offer Decisioning]](#offer-decisioning)
- [[!DNL Sandboxes]](#sandboxes)

Updates voor bestaande functies:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations] Service](#destinations)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Adobe Experience Platform Data Lake-migratie {#migration}

Terwijl Adobe het Data Lake van Gen1 naar Gen2 migreert, zullen gebruikers van het Data Lake kunnen lezen, maar alle mogelijkheden die in het Data Lake schrijven, zullen worden beïnvloed. De Adobe zal contact opnemen met systeembeheerders om de gevolgen van de migratie in detail te bespreken en de migratiedata en -tijden voor specifieke organisaties te bevestigen.

Voor meer informatie, te lezen gelieve de [ gids van de Migratie van het Leer van Gegevens ](../../landing/adls2-gen2-migration.md).

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] hefboomwerkingen [ Adobe Admin Console ](https://adminconsole.adobe.com) productprofielen om gebruikers met toestemmingen en zandbakken te verbinden. De toestemmingen controleren toegang tot een verscheidenheid van de mogelijkheden van het Platform, met inbegrip van gegevensmodellering, profielbeheer, en zandbakbeleid.

**Belangrijkste kenmerken**

| Functie | Beschrijving |
| ------- | ----------- |
| Machtigingen | In de [!DNL Admin Console] kunt u op de tab in een [!DNL Platform] productprofiel aanpassen welke [!DNL Platform] -mogelijkheden beschikbaar zijn voor de gebruikers die aan dat profiel zijn gekoppeld. Beschikbare machtigingscategorieën zijn: **[!UICONTROL Data Modeling]** , **[!UICONTROL Data Management]** , **[!UICONTROL Profile Management]** , **[!UICONTROL Identity Management]** , **[!UICONTROL Data Monitoring]** , **[!UICONTROL Sandbox Administration]** , **[!UICONTROL Destinations]** , **[!UICONTROL Data Ingestion]** , **[!UICONTROL Data Science Workspace]** , **[!UICONTROL Query Service]** en **[!UICONTROL Data Governance]** . |
| Toegang tot sandboxen | Het tabblad **[!UICONTROL Permissions]** in een [!DNL Platform] -productprofiel kan gebruikers toegang geven tot specifieke sandboxen. Zie de sectie op [ zandbakken ](#sandboxes) hieronder voor meer informatie. |

Voor meer informatie, te zien gelieve het [ overzicht van de toegangscontrole ](../../access-control/home.md).

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] is een toepassingsservice die is geïntegreerd met [!DNL Experience Platform] . Hiermee kunt u [!DNL Platform] gebruiken om uw klanten de beste aanbieding en ervaring te bieden op alle aanraakpunten op het juiste moment.

**Belangrijkste kenmerken**

| Functie | Beschrijving |
| ------- | ----------- |
| Gecentraliseerde aanbiedingsbibliotheek | De interface waar u creeert en de verschillende elementen beheert die uw aanbiedingen vormen, en hun regels en beperkingen bepalen. |
| Beslissingsengine voorstellen | De Offertebeslissingsengine maakt gebruik van [!DNL Platform] data en [!DNL Real-Time Customer Profiles] , samen met de aanbiedingsbibliotheek, om de juiste tijd, klanten en kanalen te selecteren waaraan aanbiedingen worden geleverd. |

Zie de [[!DNL Offer Decisioning] ](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=nl) -documentatie voor meer informatie.

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] is ontworpen om toepassingen voor digitale beleving wereldwijd te verrijken. Bedrijven voeren vaak meerdere digitale-ervaringstoepassingen parallel uit en moeten rekening houden met de ontwikkeling, het testen en de implementatie van deze toepassingen en tegelijk de operationele compatibiliteit garanderen. Om aan deze behoefte tegemoet te komen, biedt [!DNL Experience Platform] sandboxen die één [!DNL Platform] -instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

**Belangrijkste kenmerken**

| Functie | Beschrijving |
| ------- | ----------- |
| Productiesandbox | [!DNL Experience Platform] biedt één productiesandbox die niet kan worden verwijderd of opnieuw ingesteld. Het totale aantal beschikbare sandboxen, productie en niet-productie, wordt bepaald door de verkregen licentie. |
| Niet-productie sandboxen | Er kunnen meerdere niet-productiesandboxen worden gemaakt voor één [!DNL Platform] -instantie, zodat u functies kunt testen, experimenten kunt uitvoeren en aangepaste configuraties kunt maken zonder dat dit van invloed is op uw productiesandbox. |
| Sandboxschakelaar | In de gebruikersinterface van [!DNL Experience Platform] kunt u met de sandboxschakelaar in de linkerbovenhoek van het scherm schakelen tussen beschikbare sandboxen via een vervolgkeuzemenu. De sandboxswitch biedt ook een zoekfunctie waarmee u door beschikbare sandboxen kunt filteren. |
| `x-sandbox-name` header | Alle aanroepen van [!DNL Experience Platform] API&#39;s moeten nu de nieuwe `x-sandbox-name` -header bevatten, waarvan de waarde verwijst naar het `name` -kenmerk van de sandbox waarin de bewerking plaatsvindt. |

Voor meer informatie, te zien gelieve het [ overzicht van zandbakken ](../../sandboxes/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om gegevens in kaart te brengen, om te zetten en te bevestigen aan en van het Model van de Gegevens van de Ervaring (XDM).

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| ------- | ----------- |
| Iteratieve handelingen | [!DNL Data Prep] Mapper ondersteunt nu het uitvoeren van herhalende bewerkingen in een hiërarchie. |
| Mapper, functie | [!DNL Data Prep] Mapper heeft nu de capaciteit om **** geen attribuut van de bron aan het doel XDM te kopiëren. |

Voor meer informatie, gelieve te zien het [[!DNL Data Prep]  overzicht ](../../data-prep/home.md).

## Data Science-werkruimte {#dsw}

Data Science Workspace maakt gebruik van machinaal leren en kunstmatige intelligentie om inzichten te creëren op basis van uw gegevens. Met Data Science Workspace, dat in Adobe Experience Platform is geïntegreerd, kunt u voorspellingen maken met behulp van uw inhoud en gegevenselementen voor alle Adobe oplossingen. Een van de manieren waarop Data Science Workspace dit doet, is door het gebruik van [!DNL JupyterLab] . [!DNL JupyterLab] is een web-based gebruikersinterface voor [[!DNL Project Jupyter] ](https://jupyter.org/) en is strak geïntegreerd in Adobe Experience Platform. Het biedt een interactieve ontwikkelomgeving voor gegevenswetenschappers die werken met [!DNL Jupyter] -laptops, -code en -gegevens.

**Belangrijkste kenmerken**

| Functie | Beschrijving |
| ------- | ----------- |
| [!DNL JupyterLab] Recipe Builder-sjabloon | Gebruik van de vereisten voor laptops om recept te maken en versies bijgewerkt. [!DNL Python] In ML Runtime is de basisafbeelding bijgewerkt en worden alleen [!DNL Python] 3.6.7 en een [!DNL Conda] -omgeving gebruikt. |

Voor meer informatie, te lezen gelieve het document op [ creërend een recept gebruikend de Notities van de Jupyter ](../../data-science-workspace/jupyterlab/create-a-model.md).

## [!DNL Destinations] Service {#destinations}

In [ Real-time Customer Data Platform ](../../rtcdp/overview.md), zijn de bestemmingen pre-gebouwde integratie met bestemmingsplatforms die gegevens aan die partners op een naadloze manier activeren.

**Nieuwe bestemmingen**

| Doel | Beschrijving |
| ----------- | ----------- |
| Braze | Braze is een uitgebreid platform voor klantbetrokkenheid dat relevante en gedenkwaardige ervaringen tussen klanten en de merken die ze leuk vinden, mogelijk maakt. |
| Microsoft Bing | Met de Microsoft Bing-bestemming kunt u doelgerichte digitale campagnes uitvoeren op Microsoft Display Advertising. |
| De handelsbank | De Trade Desk is een zelfbedieningsplatform waarmee adverteerders doelgerichte digitale campagnes kunnen voeren op het hele scherm, de video en mobiele inventarisatiebronnen. |

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| ------- | ----------- |
| Doeldetails UX-updates | De bestemmingswerkstroom van Real-Time CDP omvat nu gealigneerde controle zodat kunt u zien welke batch-activeringen succesvol waren. Met deze functie kunnen gebruikers problemen rechtstreeks in de workflow voor batchbestemmingen oplossen via waarschuwingen en een controledashboard om fouten in de verwerkingspijplijn bij te houden. |
| Bestandsversleuteling | Voor op bestanden gebaseerde doelen kunnen gebruikers nu versleuteling toevoegen aan hun geëxporteerde bestanden. |
| Bestanden plannen | Voor zowel e-mailopslagdoelen als cloudopslagdoelen kunnen gebruikers een eenmalige export maken of dagelijkse momentopnamen maken. |
| Verplichte velden | Gebruikers kunnen velden markeren als verplicht, zodat alleen velden die het verplichte veld bevatten, worden geëxporteerd. |

Voor meer informatie, gelieve te zien het [ overzicht van Doelen ](../../destinations/home.md).

## Intelligente services {#intelligent-services}

Intelligente services stellen marketinganalisten en praktijkmensen in staat om gebruik te maken van de kracht van kunstmatige intelligentie en het leren van machines in gebruiksgevallen van de klantervaring. Dit staat voor marketing analisten toe om voorspellingen op te zetten specifiek voor de behoeften van een bedrijf gebruikend zaken-vlakke configuraties zonder de behoefte aan de deskundigheid van de gegevenswetenschap.

**Belangrijkste kenmerken**

| Functie | Beschrijving |
| ------- | ----------- |
| Gegevensset met consumentenervaringen (CEE) | Het creëren van een CEE dataset steunt nu het toevoegen van identiteitsgebieden aan de dataset met de Redacteur van het Schema. Attribution AI en Customer AI gebruiken de primaire identiteit voor het combineren van gebeurtenissen. |

Voor meer informatie, te lezen gelieve de sectie over [ toevoegend identiteitsgebieden aan een dataset ](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset) in de Intelligente gids van de de gegevensvoorbereiding van de Diensten.

### Attribution AI

Attribution AI, als onderdeel van Intelligente Diensten is een multi-channel, algoritmische attributiedienst die de invloed en de stijgende invloed van klanteninteractie tegen gespecificeerde resultaten berekent.

**Belangrijkste kenmerken**

| Functie | Beschrijving |
| ------- | ----------- |
| Gegevensbronkoppeling | De verbinding aan de originele datasetbron kan van de juiste spoorstaaf van een geselecteerde de dienstinstantie worden bekeken en worden genavigeerd. |
| Instantienaam bewerken | U kunt nu de naam van een bestaande Attribution AI-instantie wijzigen. |
| instantie Klonen | Kopieert de momenteel geselecteerde opstelling van de de dienstinstantie en staat voor wijzigingen toe. |
| Instantieconfiguratieparameters wijzigen | U kunt de configuratie van een bestaande instantie van de Attribution AI nu wijzigen als het nog niet begonnen is te scoren. |
| Eén scoring | U kunt nu de scoring van ad-hocmodellen in uw Attribution AI-instanties activeren. |
| Door kolommen bladeren | U kunt nu extra kolommen configureren die worden toegevoegd aan de onbewerkte uitvoerscore-bestanden om extra dimensies toe te voegen aan de BI-gereedschapsweergaven. |
| Instantie activeren en deactiveren | U kunt nu de geplande modeltraining en de scoring van uw Attribution AI-exemplaren activeren en deactiveren. |
| Reeksspatiëring | U kunt de totale hoeveelheid Attribution-inzichten vinden die door uw account wordt verbruikt in de container create instance. |
| Uitsplitsing naar aanraakpunt per positie | Een nieuwe inzichtsgrafiek die een analyse van aanraakpunten door de posities van de omschakelingspad verstrekt. |
| Bovenste omzetpaden | Een nieuwe die inzichten grafiek in het lusje van de Analyse van de Weg wordt gevestigd. De grafiek bevat een lijst met de bovenste vijf conversiepaden die de reeks aanraakpunten met marketingkanalen weergeven die tot de meeste conversies heeft geleid. |
| Efficiëntie van aanraakpunten | Verstrekt diepgaande inzichten van de drie belangrijkste variabelen die uw model touchpoint doeltreffendheid door meet. De variabelen zijn de verhouding tussen positieve en negatieve paden die zijn aangeraakt, de efficiëntie van aanraakpunten en het aanraakpuntvolume. |

Voor meer informatie, gelieve het [ overzicht van de Attribution AI ](../../intelligent-services/attribution-ai/overview.md) te lezen.

### Customer AI

De AI van de klant, als deel van de Intelligente Diensten verstrekt marketers de macht om klantenvoorspellingen op het individuele niveau met verklaringen te produceren. Met behulp van invloedrijke factoren kan de AI van de Klant u vertellen wat een klant waarschijnlijk zal doen en waarom. Bovendien kunnen marketers profiteren van de voorspellingen en inzichten van de klant van AI om de ervaringen van klanten aan te passen door de meest geschikte aanbiedingen en berichten te bedienen.

**Belangrijkste kenmerken**

| Functie | Beschrijving |
| ------- | ----------- |
| Gegevensbronkoppeling | De verbinding aan de originele datasetbron kan van de juiste spoorstaaf van een geselecteerde de dienstinstantie worden bekeken en worden genavigeerd. |
| Instantienaam bewerken | U kunt de naam van een bestaande AI-instantie van de Klant wijzigen. |
| Instantieconfiguratieparameters wijzigen | U kunt de configuratie van een bestaande AI-instantie van de Klant nu wijzigen als deze nog geen scoring heeft gestart. |
| instantie Klonen | Kopieert de momenteel geselecteerde opstelling van de de dienstinstantie en staat voor wijzigingen toe. |
| Reeksspatiëring | U kunt het totale aantal profielen dat door de AI van de Klant voor uw rekening wordt gescoord in de aanmaakinstantiecontainer vinden. |
| Voorspeldoel | De flexibiliteit bij het creëren van een vooruitgangsdoel is verhoogd met nieuwe opties om te voorspellen of &quot;zal voorkomen&quot;of &quot;niet zal voorkomen&quot;. Bovendien zijn de opties toegevoegd waarmee u kunt voorspellen of &quot;alle gebeurtenissen&quot; plaatsvinden of dat &quot;alle gebeurtenissen&quot; plaatsvinden wanneer meerdere gebeurtenissen worden gebruikt. |
| Influentiefactor-drilldown | Propensiteit bovenaan invloedrijke factoremmers bevatten nu boor downs. Boor downs is een dieper niveauoverzicht van waarden voor elk van de hoogste invloedrijke factoren binnen een aandrijvingsemmer. |

Voor meer informatie, te lezen gelieve het [ overzicht van AI van de Klant ](../../intelligent-services/customer-ai/overview.md).

## Klantprofiel in realtime {#profile}

Met Adobe Experience Platform kunt u zorgen voor gecoördineerde, consistente en relevante ervaringen voor uw klanten, ongeacht waar of wanneer ze met uw merk communiceren. Met het Profiel van de Klant in real time, kunt u een holistische mening van elke individuele klant zien die gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derdegegevens combineert. Met [!DNL Profile] kunt u uw verschillende klantgegevens consolideren in een uniforme weergave die een actionabel, tijdstempelaccount voor elke klantinteractie biedt.

**Belangrijkste kenmerken**

| Functie | Beschrijving |
| ------- | ----------- |
| Workflow voor bijgewerkte samenvoegbeleidsregels | Het platform heeft de configuratie van het fusiebeleid aan een nieuwe stapsgewijze werkschema bevorderd. Dit werkschema laat gebruikers toe om gegevensfragmenten van veelvoudige datasets van het Profiel samen te brengen en prioriteit te plaatsen voor hoe het gegeven over die datasets wordt samengevoegd om een uitvoerige mening van elk individu tot stand te brengen. De gebruikers kunnen geselecteerde datasets van het Profiel van XDM Individuele samenvoegen door de aangewezen samenvoegmethode (de Chronologie bevolen of de voorkeur van Dataset) te selecteren en datasets van ExperienceEvent aan de datasets van het Profiel toe te voegen. |
| Weergave Unieschema | In het Experience Platform UI, kunnen de gebruikers informatie over alle schema&#39;s en datasets gemakkelijker vinden die tot het unieschema bijdragen, evenals oppervlakte zeer belangrijke attributen zoals identiteit en relatievelden. Deze updates verbeteren de capaciteit om problemen op te lossen en te bevestigen dat de profielen correct worden gevormd, worden de identiteiten correct vastgemaakt, en de gegevens zijn met succes opgenomen. |

Voor meer informatie over het Profiel van de Klant in real time, met inbegrip van leerprogramma&#39;s en beste praktijken voor het werken met [!DNL Profile] gegevens, te lezen gelieve het [ overzicht van het Profiel van de Klant in real time ](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met [!DNL Platform] -services. U kunt gegevens van een verscheidenheid van bronnen zoals de toepassingen van de Adobe, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe bronnen**

| Functie | Beschrijving |
| ------- | ----------- |
| [!DNL Shopify] | U kunt nu verbinding maken met [!DNL Shopify] via de [!DNL Experience Platform] API of de gebruikersinterface. [!DNL Flow Service] Zie [ schakelaarOverzicht ](../../sources/connectors/ecommerce/shopify.md) voor meer informatie schopify. |

**Belangrijkste kenmerken**

| Functie | Beschrijving |
| ------- | ----------- |
| Verbindingsgegevens bijwerken | U kunt de namen, beschrijvingen en referenties van bestaande batchverbindingen nu bijwerken met de API van [!DNL Flow Service] en de gebruikersinterface. Voor meer informatie, zie het leerprogramma op [ het bijwerken verbindingen gebruikend de Dienst API van de Stroom ](../../sources/tutorials/api/update.md) en [ het uitgeven rekeningsdetails gebruikend UI ](../../sources/tutorials/ui/monitor.md). |
| Verbindingen verwijderen | Batchverbindingen die fouten bevatten of onnodig zijn geworden, kunnen nu worden verwijderd met de API van [!DNL Flow Service] en de UI. Voor meer informatie, zie het leerprogramma bij [ het schrappen van verbindingen gebruikend de Dienst API van de Stroom ](../../sources/tutorials/api/delete.md) en [ het schrappen van rekeningen gebruikend UI ](../../sources/tutorials/ui/delete-accounts.md). |
| Hiërarchische toewijzing | U kunt een hiërarchisch bronbestand, zoals JSON of Parquet, voorvertonen tijdens het invoeren van gegevens. Zie het leerprogramma op [ vormend een dataflow voor de schakelaars van de wolkenopslag in UI ](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) voor meer informatie. |
| API-ondersteuning voor toewijzing in streamingbronnen | U kunt nu API&#39;s gebruiken om toewijzingsfuncties uit te voeren met streamingbronnen. |
| API-ondersteuning voor aangepaste scheidingstekens voor bronnen voor cloudopslag | U kunt bestanden die niet door CSV zijn gescheiden nu verzamelen met bronnen voor cloudopslag. U kunt elk scheidingsteken voor één kolom gebruiken, zoals een tab, komma, pipe, puntkomma of hash, om platte bestanden in elke gewenste indeling te verzamelen. |
| Sandbox-ondersteuning voor Adobe Audience Manager-connector | De Audience Manager-aansluiting is nu bekend met de sandbox. De gebruikers kunnen de schakelaar toelaten om de datasets van de Audience Manager aan de zandbak van hun kiezen (met inbegrip van niet productiesandboxen) te leiden. De configuratie is beperkt tot één sandbox per organisatie. |
| UX-verbeteringen | Op bestanden gebaseerde inname is nu toegankelijk via de broncatalogus. |

Meer over bronnen leren, zie het [ overzicht van bronnen ](../../sources/home.md).

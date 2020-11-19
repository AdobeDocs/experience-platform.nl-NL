---
title: Opmerkingen bij de release van Adobe Experience Platform
description: Opmerkingen bij de release van Experience Platform 11 november 2020
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: 5aa8dbcd85fa506f90515ce3e01d35993dd99c10
workflow-type: tm+mt
source-wordcount: '2077'
ht-degree: 2%

---


# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 11 november 2020**

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
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Adobe Experience Platform Data Lake-migratie {#migration}

Terwijl Adobe het Data Lake van Gen1 naar Gen2 migreert, zullen gebruikers van het Data Lake kunnen lezen, maar alle mogelijkheden die in het Data Lake schrijven, zullen worden beïnvloed. Adobe zal contact opnemen met systeembeheerders om de gevolgen van de migratie in detail te bespreken en de migratiedata en -tijden voor specifieke IMS-organisaties te bevestigen.

Lees voor meer informatie de migratiehandleiding [van het](../../landing/adls2-gen2-migration.md)Data Lake.

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] Gebruikt [Adobe Admin Console](https://adminconsole.adobe.com) -productprofielen om gebruikers te koppelen aan machtigingen en sandboxen. Machtigingen beheren de toegang tot verschillende mogelijkheden van Platforms, waaronder gegevensmodellering, profielbeheer en sandboxbeheer.

**Belangrijkste kenmerken**

| Functie | Beschrijving |
| ------- | ----------- |
| Toestemmingen | Op de [!DNL Admin Console]tab in een [!DNL Platform] productprofiel kunt u aanpassen welke [!DNL Platform] mogelijkheden beschikbaar zijn voor de gebruikers die aan dat profiel zijn gekoppeld. Beschikbare machtigingscategorieën zijn: **[!UICONTROL Gegevensmodellering]**, **[!UICONTROL gegevensbeheer]**, **[!UICONTROL Profielbeheer]**, **[!UICONTROL Identity Management]**, **[!UICONTROL gegevenscontrole]**, ************************ Sandbox-beheer, DestinationData Ingestie, Data Science Workspace, Query Service, en Data Governance. |
| Toegang tot sandboxen | Met het tabblad **[!UICONTROL Machtigingen]** in een [!DNL Platform] productprofiel kunnen gebruikers toegang krijgen tot specifieke sandboxen. Zie de sectie over [sandboxen](#sandboxes) hieronder voor meer informatie. |

Zie het overzicht [van](../../access-control/home.md)toegangsbeheer voor meer informatie.

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] is een toepassingsservice geïntegreerd met [!DNL Experience Platform]. Hierdoor kunt u uw klanten de beste aanbieding en ervaring op alle aanraakpunten op het juiste moment aanbieden. [!DNL Platform]

**Belangrijkste kenmerken**

| Functie | Beschrijving |
| ------- | ----------- |
| Centrale aanbiedingenbibliotheek | De interface waar u creeert en de verschillende elementen beheert die uw aanbiedingen vormen, en hun regels en beperkingen bepalen. |
| Beslissingsengine voorstellen | De Offertenbeslissingsengine maakt gebruik van [!DNL Platform] gegevens en [!DNL Real-time Customer Profiles], samen met de aanbiedingsbibliotheek, om de juiste tijd, klanten en kanalen te selecteren waaraan aanbiedingen worden geleverd. |

Raadpleeg de [[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=en) documentatie voor meer informatie.

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] is ontworpen om toepassingen voor digitale ervaring wereldwijd te verrijken. Bedrijven voeren vaak meerdere digitale-ervaringstoepassingen parallel uit en moeten rekening houden met de ontwikkeling, het testen en de implementatie van deze toepassingen en tegelijk de operationele compatibiliteit garanderen. Om aan deze behoefte tegemoet te komen, [!DNL Experience Platform] verstrekt zandbakken die één enkele [!DNL Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

**Belangrijkste kenmerken**

| Functie | Beschrijving |
| ------- | ----------- |
| Productiesandbox | [!DNL Experience Platform] biedt één productiesandbox die niet kan worden verwijderd of opnieuw ingesteld. Het totale aantal beschikbare sandboxen, productie en niet-productie, wordt bepaald door de verkregen licentie. |
| Niet-productie sandboxen | Er kunnen meerdere niet-productiesandboxen voor één [!DNL Platform] instantie worden gemaakt, zodat u functies kunt testen, experimenten kunt uitvoeren en aangepaste configuraties kunt maken zonder dat dit invloed heeft op de productiesandbox. |
| Sandboxschakelaar | In de [!DNL Experience Platform] gebruikersinterface kunt u met de sandboxschakelaar in de linkerbovenhoek van het scherm schakelen tussen beschikbare sandboxen via een vervolgkeuzemenu. De sandboxswitch biedt ook een zoekfunctie waarmee u door beschikbare sandboxen kunt filteren. |
| `x-sandbox-name` header | Alle aanroepen van [!DNL Experience Platform] API&#39;s moeten nu de nieuwe `x-sandbox-name` header bevatten, waarvan de waarde verwijst naar het `name` kenmerk van de sandbox waarin de bewerking plaatsvindt. |

Zie het [sandboxoverzicht](../../sandboxes/home.md)voor meer informatie.

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om, gegevens aan en van het Model van Gegevens van de Ervaring in kaart te brengen om te zetten en te bevestigen (XDM).

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Iteratieve handelingen | [!DNL Data Prep] Mapper ondersteunt nu het uitvoeren van iteratieve bewerkingen in een hiërarchie. |
| Mapper, functie | [!DNL Data Prep] Mapper heeft nu de capaciteit om een attribuut van de bron aan doelXDM **niet** te kopiëren. |

Zie het [[!DNL Data Prep] overzicht](../../data-prep/home.md)voor meer informatie.

## Werkruimte voor gegevenswetenschap {#dsw}

De Werkruimte van de Wetenschap van Gegevens gebruikt machine het leren en kunstmatige intelligentie om inzichten van uw gegevens tot stand te brengen. De Data Science Workspace is geïntegreerd in Adobe Experience Platform en helpt u om voorspellingen te maken met behulp van uw inhoud en gegevenselementen voor verschillende Adobe-oplossingen. Een van de manieren waarop de Werkruimte van de Wetenschap van Gegevens dit verwezenlijkt is door het gebruik van [!DNL JupyterLab]. [!DNL JupyterLab] is een webgebaseerde gebruikersinterface voor [[!DNL Project Jupyter]](https://jupyter.org/) en is nauw geïntegreerd in Adobe Experience Platform. Het verstrekt een interactieve ontwikkelomgeving voor gegevenswetenschappers om met [!DNL Jupyter] notitieboekjes, code, en gegevens te werken.

**Belangrijkste kenmerken**

| Functie | Beschrijving |
| ------- | ----------- |
| [!DNL JupyterLab] Recipe Builder-sjabloon | Vereisten voor notebooks om te recept gebruiken en versies bijgewerkt. [!DNL Python] In ML Runtime is de basisafbeelding bijgewerkt om uitsluitend [!DNL Python] 3.6.7 en een [!DNL Conda] omgeving te gebruiken. |

Lees voor meer informatie het document over het [maken van een recept met Jupyter-laptops](../../data-science-workspace/jupyterlab/create-a-recipe.md).

## [!DNL Destinations] Service {#destinations}

In het Platform [van Gegevens van de Klant in](../../rtcdp/overview.md)real time, zijn de bestemmingen prebuilt integratie met bestemmingsplatforms die gegevens aan die partners op een naadloze manier activeren.

**Nieuwe bestemmingen**

| Bestemming | Beschrijving |
| ----------- | ----------- |
| Microsoft Bing | De bestemming van de Bing van Microsoft helpt u het opnieuw richten en publiek gerichte digitale campagnes over de Reclame van de Vertoning van Microsoft uitvoeren. |
| De handelsbank | De Trade Desk is een zelfbedieningsplatform waarmee adverteerders doelgerichte digitale campagnes kunnen voeren op het hele scherm, de video en mobiele inventarisatiebronnen. |

<!-- | Braze | Braze is a comprehensive customer engagement platform that power relevant and memorable experiences between customers and the brands they love. |  -->

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Verplichte velden | Gebruikers kunnen velden markeren als verplicht, zodat alleen velden die het verplichte veld bevatten, worden geëxporteerd. |

<!-- | File scheduling | For both email based and cloud storage destinations, users can create a one-time export or create daily snapshots. |
| File encryption | For file based destinations, users can now add encryption to their exported files. | -->

Zie het overzicht [](../../rtcdp/destinations/destinations-overview.md)Doelen voor meer informatie.

## Intelligente services {#intelligent-services}

Intelligente services stellen marketinganalisten en praktijkmensen in staat om gebruik te maken van de kracht van kunstmatige intelligentie en het leren van machines in gebruiksgevallen van de klantervaring. Dit staat voor marketing analisten toe om voorspellingen op te zetten specifiek voor de behoeften van een bedrijf gebruikend zaken-vlakke configuraties zonder de behoefte aan de deskundigheid van de gegevenswetenschap.

**Belangrijkste kenmerken**

| Functie | Beschrijving |
| ------- | ----------- |
| Gegevensset met consumentenervaringen (CEE) | Het creëren van een CEE dataset steunt nu het toevoegen van identiteitsgebieden aan de dataset met de Redacteur van het Schema. Attribution AI en Customer AI gebruiken de primaire identiteit voor het combineren van gebeurtenissen. |

Voor meer informatie, gelieve de sectie over het [toevoegen van identiteitsgebieden aan een dataset](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset) in de Intelligente gids van de de gegevensvoorbereiding van de Diensten te lezen.

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
| Uitsplitsing naar aanraakpunt per positie | Een nieuwe inzichten grafiek die een analyse van aanraakpunten door de posities van de omschakelingspad verstrekt. |
| Bovenste omzetpaden | Een nieuwe die inzichten grafiek in het lusje van de Analyse van de Weg wordt gevestigd. De grafiek bevat een lijst met de bovenste vijf conversiepaden die de reeks aanraakpunten met marketingkanalen weergeven die tot de meeste conversies heeft geleid. |
| Efficiëntie van aanraakpunten | Verstrekt diepgaande inzichten van de drie belangrijkste variabelen die uw model touchpoint doeltreffendheid door meet. De variabelen zijn de verhouding tussen positieve en negatieve paden die zijn aangeraakt, de efficiëntie van aanraakpunten en het aanraakpuntvolume. |

Lees het overzicht [van de](../../intelligent-services/attribution-ai/overview.md)Attribution AI voor meer informatie.

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
| Influentiefactor drilldown | Propensiteit bovenaan invloedrijke factoremmers bevatten nu boor downs. Boor downs is een dieper niveauoverzicht van waarden voor elk van de hoogste invloedrijke factoren binnen een aandrijvingsemmer. |

Lees voor meer informatie het AI-overzicht [van de](../../intelligent-services/customer-ai/overview.md)klant.

## Klantprofiel in realtime {#profile}

Met Adobe Experience Platform kunt u zorgen voor gecoördineerde, consistente en relevante ervaringen voor uw klanten, ongeacht waar of wanneer ze met uw merk communiceren. Met het Profiel van de Klant in real time, kunt u een holistische mening van elke individuele klant zien die gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derdegegevens combineert. [!DNL Profile] staat u toe om uw ongelijke klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

**Belangrijkste kenmerken**

| Functie | Beschrijving |
| ------- | ----------- |
| Workflow voor bijgewerkte samenvoegbeleidsregels | Platform heeft de configuratie van het fusiebeleid aan een nieuwe stapsgewijze werkschema bevorderd. Dit werkschema laat gebruikers toe om gegevensfragmenten van veelvoudige datasets van het Profiel samen te brengen en prioriteit te plaatsen voor hoe het gegeven over die datasets wordt samengevoegd om een uitvoerige mening van elk individu tot stand te brengen. De gebruikers kunnen geselecteerde datasets van het Profiel van XDM Individuele samenvoegen door de aangewezen samenvoegmethode (de Chronologie bevolen of de voorkeur van Dataset) te selecteren en datasets van ExperienceEvent aan de datasets van het Profiel toe te voegen. |
| Weergave Unieschema | In het Experience Platform UI, kunnen de gebruikers informatie over alle schema&#39;s en datasets gemakkelijker vinden die tot het unieschema bijdragen, evenals oppervlakte zeer belangrijke attributen zoals identiteit en relatievelden. Deze updates verbeteren de capaciteit om problemen op te lossen en te bevestigen dat de profielen correct worden gevormd, worden de identiteiten correct vastgemaakt, en de gegevens zijn met succes opgenomen. |

Lees voor meer informatie over het profiel van de klant in real time, waaronder zelfstudies en best practices voor het werken met [!DNL Profile] gegevens, het overzicht [van het profiel van de klant in](../../profile/home.md)realtime.

## [!DNL Sources] {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met [!DNL Platform] services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe bronnen**
| Functie | Beschrijving |
| — | — |
| [!DNL Shopify] | U kunt nu verbinding maken [!DNL Shopify] met [!DNL Experience Platform] de [!DNL Flow Service] API of de interface. Zie het [verbindingsoverzicht](../../sources/connectors/ecommerce/shopify.md) Shopify voor meer informatie. |

**Belangrijkste kenmerken**

| Functie | Beschrijving |
| ------- | ----------- |
| Verbindingsgegevens bijwerken | U kunt de namen, beschrijvingen en referenties van bestaande batchverbindingen nu bijwerken met de API en de gebruikersinterface [!DNL Flow Service] . Zie de zelfstudie over het [bijwerken van verbindingen met de Flow Service API](../../sources/tutorials/api/update.md) en het [bewerken van accountgegevens met de UI](../../sources/tutorials/ui/monitor.md)voor meer informatie. |
| Verbindingen verwijderen | Batchverbindingen die fouten bevatten of onnodig zijn geworden, kunnen nu worden verwijderd met de API en de UI. [!DNL Flow Service] Voor meer informatie, zie de zelfstudie over het [schrappen van verbindingen gebruikend de Dienst API](../../sources/tutorials/api/delete.md) van de Stroom en het [schrappen van rekeningen gebruikend UI](../../sources/tutorials/ui/delete-accounts.md). |
| Hiërarchische toewijzing | U kunt een hiërarchisch bronbestand, zoals JSON of Parquet, voorvertonen tijdens het invoeren van gegevens. Zie de zelfstudie over het [configureren van een gegevensstroom voor cloudopslagconnectors in de gebruikersinterface](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) voor meer informatie. |
| API-ondersteuning voor toewijzing in streamingbronnen | U kunt nu API&#39;s gebruiken om toewijzingsfuncties uit te voeren met streamingbronnen. |
| API-ondersteuning voor aangepaste scheidingstekens voor bronnen voor cloudopslag | U kunt bestanden die niet door CSV zijn gescheiden nu verzamelen met bronnen voor cloudopslag. U kunt elk scheidingsteken voor één kolom gebruiken, zoals een tab, komma, pipe, puntkomma of hash, om platte bestanden in elke gewenste indeling te verzamelen. |
| Sandbox-ondersteuning voor Adobe Audience Manager-connector | De Audience Manager-aansluiting is nu bekend met de sandbox. De gebruikers kunnen de schakelaar toelaten om de datasets van de Audience Manager aan de zandbak van hun kiezen (met inbegrip van niet productiesandboxen) te leiden. De configuratie is beperkt tot één sandbox per IMS Org. |
| UX-verbeteringen | Op bestanden gebaseerde inname is nu toegankelijk via de broncatalogus. |

Zie het [bronoverzicht](../../sources/home.md)voor meer informatie over bronnen.
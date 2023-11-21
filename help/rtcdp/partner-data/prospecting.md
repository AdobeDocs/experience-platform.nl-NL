---
title: Nieuwe klanten aantrekken en aanschaffen zonder afhankelijk te zijn van cookies van derden
description: Leer hoe u nieuwe klanten kunt aantrekken en aanwerven via het zoeken naar gebruiksgevallen, zonder te vertrouwen op cookies van derden.
feature: Use Cases, Customer Acquisition
exl-id: b9e7b3af-2a13-4904-bd12-e3ed05a1988e
source-git-commit: 3353866aa2d52c784663f355183e940e727b2af7
workflow-type: tm+mt
source-wordcount: '2030'
ht-degree: 1%

---

# Nieuwe klanten aantrekken en aanschaffen zonder afhankelijk te zijn van cookies van derden

>[!AVAILABILITY]
>
>* Deze functionaliteit is beschikbaar voor klanten die een licentie hebben verkregen voor Real-Time CDP (App Service), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Premiere, Real-Time CDP Ultimate. Meer informatie over deze pakketten vindt u in de [productbeschrijvingen](https://helpx.adobe.com/legal/product-descriptions.html) en neem contact op met uw Adobe voor meer informatie.

Gebruik gegevensondersteuning van derden in Real-Time CDP om uw profielbasis uit te breiden met perspectiefprofielen van gegevenspartners en met hen in gesprek te gaan om nieuwe klanten te verkrijgen of te bereiken.

![Overzicht van het gebruik op hoog niveau door de klant bij prospectie.](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-overview.png)

## Waarom dit gebruiksgeval overwegen {#why-this-use-case}

Merken worden tegelijkertijd geconfronteerd met enorme uitdagingen van verantwoord het uitvoeren van top-of-the-funnel gebruiksgevallen van de klantenverwerving zonder afhankelijkheid van derdekoekjes, beperkte begrotingen, en hogere vraag naar transparantie en terugkeer op ad-uitgavenpost.

Adobe Real-time Customer Data Platform kan merken helpen hun door DMP (Data Management Platform) ondersteunde gebruiksscenario&#39;s veilig om te zetten in alternatieven waarvoor geen cookie nodig is, en dit op een manier die de volledige verfijning en kracht van zelfserversegmentatie, publieksbeperking en activering in één systeem brengt. Dit alles zonder afbreuk te doen aan de onafgebroken aandacht van de Adobe voor een verantwoord gebruik van gegevens via een geoctrooieerd kader voor gegevensbeheer en instemming.

Volg bijvoorbeeld de stappen die in dit gebruiksgeval worden beschreven wanneer u een campagne moet uitvoeren om vooruitzichten aan te trekken om gebruikers of bekende klanten te worden.

## Vereisten en planning {#prerequisites-and-planning}

Aangezien u het bereiken aan en het verwerven van nieuwe klanten overweegt, overweeg de volgende eerste vereisten in uw planningsproces:

* Wat is het gemak waarmee u partner-verstrekte profielen om in Real-Time CDP wordt opgenomen en worden verfrist?
* Welke identiteiten vereisen uw stroomafwaartse bestemmingen?
* Zorg ervoor dat de ingesloten id id&#39;s stroomafwaarts kunnen worden uitgevoerd
* Is het partnergegeven dat u gebonden bent aan een wijd geaccepteerde duurzame herkenningsteken, zoals Persoonlijke Identificeerbare Informatie (PII), gehakt PII, of een partnerherkenningsteken?
* Welk beleid van het gegevensgebruik moet u van het partnerperspectief en van uw eigen wettelijk, privacy, of nalevingsteam bewust zijn?

## Hoe het gebruiksgeval te bereiken: overzicht op hoog niveau {#achieve-the-use-case-high-level}

Voordat u Real-Time CDP uitbreidt om nieuwe klanten aan te trekken, moet u ervoor zorgen dat u Real-Time CDP gebruikt om een robuuste basis voor uw eerste gegevens te bouwen. De workflows om dit gebruiksgeval te bereiken zijn gelijkaardig aan werkschema&#39;s om met uw bekende klanten in dienst te nemen.

![Overzicht van het gebruik op hoog niveau door de klant bij prospectie.](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-steps.png)

1. Als **klant**, geeft u een licentie voor perspectiefprofielen van een of meer **gegevenspartners** om de top van de aanschaf van de trechter door de klant te helpen bepalen.
2. Als **klant**, breidt u uw profielgegevens en governancemodel uit om het **partner**- lijst met perspectiefprofielen.
3. Als **klant**, laadt u perspectiefprofielen in Real-Time CDP en bouwt u beleidsregels voor verantwoord gebruik.
4. Als **klant**, maakt u doelgroepen op basis van de lijst met perspectiefprofielen.
5. Als **klant**, activeert u het potentiële publiek aan bestemmingen die van de identiteiten beschikbaar in uw perspectieflijst goedkeuren.
6. Werk zo nodig met de **gegevenspartner** voor de activering van het publiek naar de gewenste betaalmedia-bestemmingen in de laatste mijl.

## Video doorloopt {#video-walkthrough}

Bekijk hieronder de videozelfstudie voor een analyse van hoe te om perspectiefpubliek te bereiken en in dienst te nemen:

>[!VIDEO](https://video.tv.adobe.com/v/3423071/?learn=on)

## Hoe het gebruiksgeval te bereiken: Step-by-step instructies {#step-by-step-instructions}

Lees de onderstaande secties door, die koppelingen naar verdere documentatie bevatten, om alle stappen in het bovenstaande overzicht op hoog niveau te voltooien.

### UI-functionaliteit en elementen die u gebruikt {#ui-functionality-and-elements}

Wanneer u de stappen voor het implementeren van het gebruiksscenario uitvoert, maakt u gebruik van de volgende Real-Time CDP-functionaliteit en UI-elementen (vermeld in de volgorde waarin u deze wilt gebruiken). Zorg ervoor dat u de noodzakelijke op attribuut-gebaseerde toegangsbeheertoestemmingen voor al deze gebieden hebt of vraag uw systeembeheerder om u de noodzakelijke toestemmingen te verlenen.

* [Identiteiten](/help/identity-service/namespaces.md)
* [Schema&#39;s](/help/xdm/home.md)
* [Labels voor gegevensgebruik](/help/data-governance/labels/overview.md)
* [Gegevenssets](/help/catalog/datasets/overview.md)
* [Bronnen](/help/sources/home.md)
* [Prospectieprofielen](/help/profile/ui/prospect-profile.md)
* [Doelgroepen](/help/segmentation/ui/prospect-audience.md)
* [Doelen](/help/destinations/home.md)

### De details van het het profielprofiel van de vergunning derde van de partner {#license-profiles-from-partner}

Deze stap wordt behandeld in [voorwaarden](#prerequisites-and-planning) en de Adobe veronderstelt dat u de juiste contractuele overeenkomsten met vertrouwde op gegevensverkopers hebt om perspectiefprofielen in te voeren die door de gegevenspartner worden verstrekt.

### Breid uw profielgegevens en governancemodel uit om partner-verstrekte perspectiefprofielen aan te passen {#extend-governance-model}

Als u perspectiefprofielen wilt ontvangen van uw gegevenspartner, moet u uw gegevensbeheerframework in Real-Time CDP uitbreiden om dit nieuwe profieltype te kunnen gebruiken.

De volgende componenten worden gebruikt voor identiteit, gegevensbeheer en beheer:

* Een nieuwe **[!UICONTROL Partner ID]** het identiteitstype voor de partner verstrekte profielen
* Een nieuwe **[!UICONTROL XDM Individual Prospect Profile]** XDM-klasse
* **(Documentatie binnenkort beschikbaar)** Veldgroepen die zijn aangepast aan ondersteuning van partnergegevens
* **(Documentatie binnenkort beschikbaar)** De etiketten van de derde die u op de attributen zult toevoegen die uit partners komen

#### Creeer een identiteitskaart van de Partner identiteitskaart namespace {#create-partner-id-namespace}

Begin door een nieuw identiteitstype voor de profielen te creëren die u van de partner zult ontvangen. Hiervoor moet u in het gedeelte Identiteit een nieuwe naamruimte maken van het type **[!UICONTROL Partner ID]**.

![Creeer een nieuwe identiteitskaart van identiteitskaart van de Partner namespace.](/help/rtcdp/assets/partner-data/prospecting/create-partner-identity-namespace.png)

* Meer informatie over naamruimten voor partnerid vindt u in het dialoogvenster [sectie met identiteitstypen](/help/identity-service/namespaces.md).
* Meer informatie [identiteitsvelden definiëren](/help/xdm/ui/fields/identity.md) in de gebruikersinterface van het Experience Platform.

#### Een nieuw schema maken met de opdracht **[!UICONTROL XDM Individual Prospect Profile]** class

Volgende, in **[!UICONTROL Data Management]** > **[!UICONTROL Schemas]**, maakt u een nieuw schema en wijst u dit toe aan het **[!UICONTROL XDM Individual Prospect Profile]** klasse.

![Zoeken naar de klasse XDM Individual Prospect Profile in de XDM schema builder.](/help/rtcdp/assets/partner-data/prospecting/xdm-individual-prospect-class.png)

Lees hoe te [schema&#39;s maken en bewerken in de gebruikersinterface](/help/xdm/ui/resources/schemas.md) en krijgt volledige informatie over de klasse van het Profiel van het Individuele Vooruitzicht XDM (verbinding aanstaande).

De **[!UICONTROL XDM Individual Prospect Profile]** De klasse wordt vooraf geconfigureerd met de onderstaande velden. Om uw schema met partner-verstrekte attributen voor de perspectiefprofielen te verrijken, kunt u of een nieuwe gebiedsgroep met de attributen tot stand brengen die u verwacht en het aan het schema toevoegt, of u kunt één van de pre-gevormde gebiedsgroepen gebruiken die door Adobe worden verstrekt.

![Vooraf geconfigureerde velden voor de XDM-klasse Individual Prospect Profile.](/help/rtcdp/assets/partner-data/prospecting/preconfigured-fields-individual-prospect-class.png)

Daarna, moet u de partnerID identiteit selecteren die u vroeger als primaire identiteit voor het schema creeerde. Profielrecords moeten een primaire id bevatten. Deze stap wordt vereist om ervoor te zorgen dat de perspectiefgegevens in de profielopslag kunnen worden geladen en voor segmentatie en activering beschikbaar worden gesteld.

>[!AVAILABILITY]
>
>De profielen van het vooruitzicht worden automatisch beperkt tot gebruiken identiteitskaart namespaces van het type van identiteitskaart van de Partner. Dit is door ontwerp en verzekert schone scheiding tussen uw eerste-partij en perspectiefprofielen.

![Selecteer eerder gevormde identiteitskaart van de Partner als primaire identiteit in het schema.](/help/rtcdp/assets/partner-data/prospecting/select-partner-id-as-primary-identity.gif)

Het schema is nog niet ingeschakeld voor het profiel. Schakel de profielknop in of uit om dit schema in te schakelen voor opname in de profielservice. Voor meer informatie over het toelaten van het schema voor gebruik in het Profiel van de Klant In real time, lees [Schema-zelfstudie maken.](/help/xdm/tutorials/create-schema-ui.md#profile)

![Schema inschakelen voor profiel.](/help/rtcdp/assets/partner-data/prospecting/enable-schema-for-profile.png)

#### Het label voor gegevensbeheer van derden toevoegen aan alle velden in het schema

Overweeg labels voor gegevensbeheer van derden toe te voegen aan alle velden die het schema vormen. Dit is belangrijk om een verantwoord gebruik van gegevens van derden te waarborgen en het risico van gegevenslekkage tot een minimum te beperken. Meer informatie over [labels voor gegevensbeheer van derden](../../data-governance/labels/reference.md#partner-ecosystem-labels).

Volg de onderstaande stappen om dit te doen:

1. Ga naar het schema dat u hebt gemaakt en selecteer het **[!UICONTROL Labels]** tab.
2. Selecteer alle gebieden in dit schema gebruikend checkbox knoop bij zeer bovenkant en klik dan het potloodpictogram op het recht om de etiketten van het gegevensbeheer op dit schema toe te passen.
3. Selecteer de **[!UICONTROL Partner Ecosystem]** Label van de categorieën aan de linkerkant.
4. Kies het label dat wordt aangeroepen **[!UICONTROL Third Party]** en selecteert u **[!UICONTROL Save]**.
5. U ziet dat alle velden in het schema nu het label hebben dat u in de vorige stap hebt geselecteerd.

>[!SUCCESS]
>
>Uw schema is nu klaar aan gebruik en u kunt aan de volgende stap te werk gaan om perspectiefgegevens van uw gegevenspartner in te voeren.

Ook in deze stap, denk over hoe uw model van gegevensbeheer verandert aangezien u uw gegevensbeheerstrategie uitbreidt om dergegevens te omvatten die door de partner worden verstrekt. Verken de overwegingen in de documentatiekoppelingen hieronder:

* (**Binnenkort beschikbaar**) Houd gegevens van derden in een aparte gegevensset, zodat u deze gegevens eenvoudig kunt verwijderen en integraties ongedaan kunt maken.
* (**Binnenkort beschikbaar**) Gebruik de [gegevenssetvervaldatum](/help/hygiene/ui/dataset-expiration.md) functionaliteit op de dataset voor cliënten die de toe:voegen-op van de gegevenshygiëne kochten.
* (**Binnenkort beschikbaar**) Wees voorzichtig bij het maken van afgeleide gegevenssets die gegevens van derden opvragen, omdat de enige oplossing om de gegevens van derden te verwijderen, na elkaar is dat de gehele afgeleide gegevensset wordt verwijderd.

### Laad de lijst met perspectiefprofielen en inspecteer de weergave met perspectiefprofielen

Nadat u uw gegevensmodel hebt voorbereid voor het beheren van perspectiefprofielen, is het tijd om gegevens in te voeren.

#### Creeer een dataset en laad de gegevens van het steekproefperspectief

Om sommige steekproefgegevens te laden en perspectiefprofielen te bevolken, creeer een dataset en upload een dossier dat u van de gegevenspartner ontving. Voer de onderstaande stappen uit:

1. Navigeren naar **[!UICONTROL Data Management]** > **[!UICONTROL Datasets]** en selecteert u **[!UICONTROL Create dataset]**.
2. Gegevensset maken van schema
3. Selecteer het schema dat u in een vorige stap hebt gemaakt
4. Geef uw dataset een naam en naar keuze een beschrijving.
5. Selecteer **[!UICONTROL Finish]**.

![Een opname van de stappen om een dataset voor perspectiefprofielen tot stand te brengen.](/help/rtcdp/assets/partner-data/prospecting/create-dataset-for-prospect-profiles.gif)

Merk op dat gelijkend op de stap om een schema tot stand te brengen, u de dataset moet toelaten om in het Profiel van de Klant in real time worden omvat. Voor meer informatie over het toelaten van de dataset voor gebruik in het Profiel van de Klant In real time, lees [Schema-zelfstudie maken.](/help/xdm/tutorials/create-schema-ui.md#profile)

![Gegevensset inschakelen voor profiel.](/help/rtcdp/assets/partner-data/prospecting/enable-dataset-for-profile.png)

Om een dossier te laden dat u van de partner in de dataset hebt ontvangen, selecteer de dataset, scroll neer in het juiste spoor, en selecteer **[!UICONTROL Add data]**. U kunt neerzetten slepen of **[!UICONTROL Choose files]** om naar de bestandslocatie te navigeren en deze te selecteren.

![Bestand toevoegen aan gegevensset.](/help/rtcdp/assets/partner-data/prospecting/add-file-to-dataset.png)

Nadat u de lijst met profielen van de gegevenspartner in Real-Time CDP hebt geladen, gaat u verder naar de [De sectie met geladen perspectiefprofielen Inspect](#inspect-profiles) om te controleren dat de perspectiefprofielen in UI bevolken.

#### Opzienbare gegevens door bronschakelaars

U kunt de terugkomende dossierinvoer aan ingelezen gegevens van de partner door een bronschakelaar plaatsen en de lijst van perspectiefprofielen in Real-Time CDP brengen.

Sommige geadviseerde bronschakelaars voor dit doel zijn vermeld hieronder maar merk op dat om het even welke dossier-gebaseerde insluitingsmethode in Real-Time CDP voor uw doel werkt.

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

Na het laden van de lijst met profielen van de gegevenspartner in Real-Time CDP, ga aan de volgende sectie te werk om te controleren dat de perspectiefprofielen in UI bevolken.

#### De geladen perspectiefprofielen Inspect {#inspect-profiles}

Als u de lijst met perspectiefprofielen wilt weergeven, navigeert u naar **[!UICONTROL Prospects]** > **[!UICONTROL Profiles]** in het linkerspoor.

Het kan maximaal twee uur duren voordat de perspectiefprofielen die u net in Real-Time CDP hebt geladen, worden weergegeven in het dialoogvenster **[!UICONTROL Browse]** weergave van het scherm Prospectprofiel. Als op de pagina het bericht &quot;Er zijn geen perspectiefprofielen om nu te doorbladeren&quot; wordt weergegeven, probeert u het later opnieuw. Na wat wacht, zouden de perspectiefprofielen in moeten verschijnen **[!UICONTROL Browse]** weergeven.

>[!TIP]
>
>De aanwezigheid van de **[!UICONTROL Identity Namespace]** kolom. Als u met veelvoudige gegevensverkopers werkt, gebruik deze kolom om de oorsprong van perspectiefprofielen af te leiden.

![Bekijk de perspectiefprofielen die in Real-Time CDP zijn geladen.](/help/rtcdp/assets/partner-data/prospecting/prospect-profiles-view.png)

U kunt ook elk perspectiefprofiel selecteren voor verdere inspectie, zoals hieronder wordt weergegeven.

![Weergave van hoe u perspectiefprofielen kunt inspecteren.](/help/rtcdp/assets/partner-data/prospecting/inspect-prospect-profile.gif)

Meer informatie over [perspectiefprofielen](/help/profile/ui/prospect-profile.md).

### Perspectiefpubliek maken {#create-prospect-audiences}

Gebruik de segmentatiefunctionaliteit in Real-Time CDP om een publiek te maken op basis van uw perspectiefprofielen. Gebruik de gewenste segmentatieregels om een op maat gemaakt publiek te maken.

Als u aan de slag wilt en een publiek wilt maken dat is samengesteld uit perspectiefprofielen, navigeert u naar **[!UICONTROL Prospects]** > **[!UICONTROL Audiences]**.

![Weergave van het beoogde publiek.](/help/rtcdp/assets/partner-data/prospecting/prospect-audiences.png)

Merk op dat de ervaring van de publieksopbouw voor perspectiefprofielen van de ervaring verschilt om publiek van uw bekende, eerste partijklanten te bouwen. Deze weergave is beperkt tot:

* Attributen van de klasse van het vooruitzicht die u vroeger creeerde.
* Alleen batchprofielevaluatie.
* Steunt niet het bouwen van publiek dat op tijd-reeksgebeurtenissen wordt gebaseerd.

Meer informatie over [publiek perspectief](/help/segmentation/ui/prospect-audience.md).

### Activeren perspectiefprofielen aan bestemmingen {#activate-to-destinations}

Maak gebruik van het potentiële publiek door hen naar bestemmingen uit te voeren. Momenteel ondersteunen alleen bepaalde cloudopslagdoelen activering van perspectiefprofielen.

![Doelen die het potentiële publiek steunen.](/help/destinations/assets/ui/activate-prospect-audiences/data-types-filter.png)

[Meer informatie](/help/destinations/ui/activate-prospect-audiences.md) over het activeren van vooruitzichten voor cloudopslagbestemmingen.

## Andere gebruiksgevallen die worden bereikt via ondersteuning van partnergegevens {#other-use-cases}

Verken verdere gebruiksgevallen die door de steun van partnergegevens in Real-Time CDP worden toegelaten:

* [Eerste-partijprofielen met attributen van vertrouwde op gegevenspartners aanvullen](/help/rtcdp/partner-data/supplement-first-party-profiles.md) om uw gegevensstichting te verbeteren en nieuwe inzichten in uw klantenbasis te krijgen en betere publieksoptimalisering te bereiken.
* [Onsite ervaringen voor onbekende bezoekers personaliseren met de erkenning van bezoekers met hulp van partners](/help/rtcdp/partner-data/onsite-personalization.md) tijdens het bezoek zonder dat de gebruiker dit heeft geverifieerd of dat hij of zij een eerdere geschiedenis heeft met uw merk.
* [Uitgebreide activering van perspectiefprofielen en perspectiefpubliek](/help/destinations/ui/activate-prospect-audiences.md) om doelen te selecteren.

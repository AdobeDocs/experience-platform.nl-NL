---
keywords: Experience Platform;home;IAB;IAB 2.0;toestemming;toestemming
solution: Experience Platform
title: Datasets maken voor het vastleggen van gegevens met IAB TCF 2.0-toestemming
topic-legacy: privacy events
description: Dit document verstrekt stappen voor vestiging de twee vereiste datasets om IAB TCF 2.0 toestemmingsgegevens te verzamelen.
exl-id: 36b2924d-7893-4c55-bc33-2c0234f1120e
source-git-commit: 656d772335c2f5ae58b471b31bfbd6dfa82490cd
workflow-type: tm+mt
source-wordcount: '1566'
ht-degree: 0%

---

# Gegevenssets maken voor het vastleggen van gegevens met IAB TCF 2.0-toestemming

Adobe Experience Platform kan gegevens over toestemming van klanten verwerken in overeenstemming met IAB [!DNL Transparency & Consent Framework] (TCF) 2.0, dan moeten die gegevens worden verzonden naar gegevenssets waarvan de schema&#39;s TCF 2.0 toestemmingsvelden bevatten.

Specifiek, worden twee datasets vereist voor het vangen van TCF 2.0 toestemmingsgegevens:

* Een dataset die op de [!DNL XDM Individual Profile] klasse wordt gebaseerd, voor gebruik in [!DNL Real-time Customer Profile] wordt toegelaten.
* Een dataset die op de [!DNL XDM ExperienceEvent] klasse wordt gebaseerd.

>[!IMPORTANT]
>
>Platform dwingt slechts de koorden TCF die in de Individuele dataset van het Profiel worden verzameld af. Terwijl een dataset ExperienceEvent nog wordt vereist om een gegevensstroom als deel van dit werkschema tot stand te brengen, moet u slechts gegevens in de profieldataset opnemen. De dataset ExperienceEvent kan nog worden gebruikt als u gebeurtenissen van de toestemmingsverandering in tijd wilt volgen, maar deze waarden worden niet gebruikt binnen wanneer het afdwingen op segmentactivering.

Dit document verstrekt stappen voor vestiging deze twee datasets. Voor een overzicht van het volledige werkschema om uw verrichtingen van de gegevens van het Platform voor TCF 2.0 te vormen, verwijs naar [IAB TCF 2.0 nalevingsoverzicht](./overview.md).

## Vereisten

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [XDM (Experience Data Model)](../../../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Experience Platform] klantenervaring worden georganiseerd.
   * [Basisbeginselen van de schemacompositie](../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM.
* [Adobe Experience Platform Identity Service](../../../../identity-service/home.md): Staat u toe om klantenidentiteiten van uw verschillende gegevensbronnen over apparaten en systemen te overbruggen.
   * [Naamruimten](../../../../identity-service/namespaces.md) van identiteit: De identiteitsgegevens van de klant moeten worden verstrekt onder een specifieke naamruimte die door de Identiteitsdienst wordt erkend.
* [Klantprofiel](../../../../profile/home.md) in realtime: Hefboomwerkingen  [!DNL Identity Service] om u gedetailleerde klantenprofielen van uw datasets in real time te laten tot stand brengen. [!DNL Real-time Customer Profile] trekt gegevens van het meer van Gegevens en handhaaft klantenprofielen in zijn eigen afzonderlijke gegevensopslag.

## TCF 2.0 veldgroepen {#field-groups}

De [!UICONTROL IAB TCF 2.0 Consent Details] schemagebiedgroep verstrekt de gebieden van de klantentoestemming die voor TCF 2.0 steun worden vereist. Er zijn twee versies van deze veldgroep: één compatibel met de [!DNL XDM Individual Profile] klasse, en andere met de [!DNL XDM ExperienceEvent] klasse.

In de volgende secties wordt de structuur van elk van deze veldgroepen uitgelegd, inclusief de gegevens die ze tijdens inname verwachten.

### Profielveldgroep {#profile-field-group}

Voor schema&#39;s die op [!DNL XDM Individual Profile] worden gebaseerd, verstrekt de [!UICONTROL IAB TCF 2.0 Consent Details] gebiedsgroep één enkel kaart-type gebied, `identityPrivacyInfo`, dat klantenidentiteiten aan hun TCF toestemmingsvoorkeur in kaart brengt. Deze veldgroep moet in een op record gebaseerd schema worden opgenomen dat voor het Profiel van de Klant in real time wordt toegelaten voor automatische handhaving.

Zie [verwijzingsgids](../../../../xdm/field-groups/profile/iab.md) voor deze gebiedsgroep om meer over zijn structuur en gebruiksgeval te leren.

### Groep Gebeurtenisvelden {#event-field-group}

Als u toestemming-verandering gebeurtenissen in tijd wilt volgen, kunt u [!UICONTROL IAB TCF 2.0 Consent Details] gebiedsgroep aan uw [!UICONTROL XDM ExperienceEvent] schema toevoegen.

Als u niet van plan bent om gebeurtenissen van de toestemmingsverandering in tijd te volgen, te hoeven u om deze gebiedsgroep niet in uw gebeurtenisschema te omvatten. Bij het automatisch afdwingen van TCF toestemmingswaarden, gebruikt het Experience Platform slechts de recentste toestemmingsinformatie die in de [profielgebiedgroep wordt opgenomen](#profile-field-group). Goedkeuringswaarden die door gebeurtenissen worden vastgelegd, nemen niet deel aan automatische workflows voor handhaving.

Zie [verwijzingsgids](../../../../xdm/field-groups/event/iab.md) voor deze gebiedsgroep voor meer informatie over zijn structuur en gebruiksgeval.

## Goedkeuringsschema&#39;s voor klanten maken {#create-schemas}

Om datasets tot stand te brengen die toestemmingsgegevens vangen, moet u XDM schema&#39;s eerst creëren om die datasets op te baseren.

Zoals vermeld in de vorige sectie, wordt een schema dat de [!UICONTROL XDM Individual Profile] klasse gebruikt vereist om toestemming in stroomafwaartse werkschema&#39;s van het Platform af te dwingen. U kunt desgewenst ook een afzonderlijk schema maken op basis van [!UICONTROL XDM ExperienceEvent] als u wijzigingen in de toestemming wilt bijhouden. Beide schema&#39;s moeten een `identityMap` gebied en een aangewezen TCF 2.0 gebiedsgroep bevatten.

Selecteer **[!UICONTROL Schemas]** in de linkernavigatie in de interface van het Platform om de werkruimte [!UICONTROL Schemas] te openen. Voer van hieruit de stappen in de onderstaande secties uit om elk vereist schema te maken.

>[!NOTE]
>
>Als u bestaande XDM-schema&#39;s hebt die u wilt gebruiken om toestemmingsgegevens in plaats daarvan te vangen, kunt u die schema&#39;s uitgeven in plaats van nieuwe te creëren. Als een bestaand schema echter is ingeschakeld voor gebruik in Real-time klantprofiel, kan de primaire identiteit van het schema geen rechtstreeks identificeerbaar veld zijn dat niet mag worden gebruikt in op rente gebaseerde reclame, zoals een e-mailadres. Raadpleeg uw juridische adviseur als u niet zeker weet welke velden beperkt zijn.
>
>Bovendien kunnen bij het bewerken van bestaande schema&#39;s alleen additieve (vaste) wijzigingen worden aangebracht. Zie de sectie over [principes van schemaevolutie](../../../../xdm/schema/composition.md#evolution) voor meer informatie.

### Een schema voor profieltoestemming maken {#profile-schema}

Selecteer **[!UICONTROL Create schema]** en kies **[!UICONTROL XDM Individual Profile]** in het vervolgkeuzemenu.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-profile.png)

Het dialoogvenster **[!UICONTROL Add field groups]** wordt weergegeven, zodat u meteen veldgroepen aan het schema kunt toevoegen. Selecteer **[!UICONTROL IAB TCF 2.0 Consent Details]** in de lijst. U kunt de zoekbalk desgewenst gebruiken om de resultaten te beperken en zo de veldgroep gemakkelijker te vinden.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-privacy.png)

Zoek vervolgens de **[!UICONTROL IdentityMap]**-veldgroep in de lijst en selecteer deze ook. Selecteer **[!UICONTROL Add field groups]** als beide veldgroepen in de rechtertrack worden vermeld.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-identitymap.png)

Het canvas verschijnt weer en geeft aan dat de velden `identityPrivacyInfo` en `identityMap` zijn toegevoegd aan de schemastructuur.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-privacy-structure.png)

Voordat u meer velden aan het schema toevoegt, selecteert u het basisveld dat **[!UICONTROL Schema properties]** in de rechtertrack moet worden weergegeven, waar u een naam en een beschrijving voor het schema kunt opgeven.

![](../../../images/governance-privacy-security/consent/iab/dataset/schema-details-profile.png)

Nadat u een naam en een beschrijving hebt verstrekt, kunt u naar keuze meer gebieden aan het schema toevoegen door **[!UICONTROL Add]** onder de **[!UICONTROL Field groups]** sectie op de linkerkant van het canvas te selecteren.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-profile.png)

Als u een bestaand schema uitgeeft dat reeds voor gebruik in [!DNL Real-time Customer Profile] is toegelaten, uitgezocht **[!UICONTROL Save]** om uw veranderingen te bevestigen alvorens vooruit naar de sectie op [creërend een dataset op uw toestemmingsschema](#dataset) te slaan. Als u een nieuw schema maakt, gaat u verder met de stappen in de onderstaande subsectie.

#### Het schema inschakelen voor gebruik in [!DNL Real-time Customer Profile]

Om het Platform in staat te stellen de toestemmingsgegevens te associëren het aan specifieke klantenprofielen ontvangt, moet het toestemmingsschema voor gebruik in [!DNL Real-time Customer Profile] worden toegelaten.

>[!NOTE]
>
>Het voorbeeldschema dat in deze sectie wordt getoond gebruikt zijn `identityMap` gebied als zijn primaire identiteit. Als u een ander veld wilt instellen als primaire identiteit, moet u ervoor zorgen dat u een indirecte id gebruikt, zoals een cookie-id, en niet een rechtstreeks identificeerbaar veld dat niet mag worden gebruikt in op rente gebaseerde reclame, zoals een e-mailadres. Raadpleeg uw juridische adviseur als u niet zeker weet welke velden beperkt zijn.
>
>De stappen op hoe te om een primair identiteitsgebied voor een schema te plaatsen kunnen in [[!UICONTROL Schemas] UI gids](../../../../xdm/ui/fields/identity.md) worden gevonden.

Als u het schema voor [!DNL Profile] wilt inschakelen, selecteert u de naam van het schema in de linkertrack om de sectie **[!UICONTROL Schema properties]** te openen. Van hier, selecteer **[!UICONTROL Profile]** knevelknoop.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-enable-profile.png)

Er wordt een pop-up weergegeven die aangeeft dat de primaire identiteit ontbreekt. Schakel het selectievakje in voor het gebruik van een andere primaire identiteit, aangezien de primaire identiteit zich in het veld `identityMap` bevindt.

![](../../../images/governance-privacy-security/consent/iab/dataset/missing-primary-identity.png)

Tot slot selecteer **[!UICONTROL Save]** om uw veranderingen te bevestigen.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-save.png)

### Een schema voor gebeurtenismachtigingen maken {#event-schema}

>[!NOTE]
>
>Regelingen voor toestemming voor gebeurtenissen worden alleen gebruikt om gebeurtenissen met betrekking tot wijziging van de toestemming in de loop der tijd te volgen en nemen niet deel aan workflows voor afdwinging stroomafwaarts. Als u toestemmingsveranderingen in tijd niet wilt volgen, kunt u vooruit naar de volgende sectie over [het creëren van toestemmingsdatasets](#datasets) overslaan.

Selecteer **[!UICONTROL Schemas]** in de werkruimte **[!UICONTROL Create schema]** en kies **[!UICONTROL XDM ExperienceEvent]** in het vervolgkeuzemenu.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-event.png)

Het dialoogvenster **[!UICONTROL Add field groups]** wordt weergegeven. Selecteer **[!UICONTROL IAB TCF 2.0 Consent Details]** in de lijst. U kunt de zoekbalk desgewenst gebruiken om de resultaten te beperken en zo de veldgroep gemakkelijker te vinden.


![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-privacy.png)

Zoek vervolgens de **[!UICONTROL IdentityMap]**-veldgroep in de lijst en selecteer deze ook. Selecteer **[!UICONTROL Add field groups]** als beide veldgroepen in de rechtertrack worden vermeld.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-identitymap.png)

Het canvas verschijnt weer en geeft aan dat de velden `consentStrings` en `identityMap` zijn toegevoegd aan de schemastructuur.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-privacy-structure.png)

Voordat u meer velden aan het schema toevoegt, selecteert u het basisveld dat **[!UICONTROL Schema properties]** in de rechtertrack moet worden weergegeven, waar u een naam en een beschrijving voor het schema kunt opgeven.

![](../../../images/governance-privacy-security/consent/iab/dataset/schema-details-event.png)

Nadat u een naam en een beschrijving hebt verstrekt, kunt u naar keuze meer gebieden aan het schema toevoegen door **[!UICONTROL Add]** onder de **[!UICONTROL Field groups]** sectie op de linkerkant van het canvas te selecteren.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-event.png)

Nadat de gewenste veldgroepen zijn toegevoegd, selecteert u **[!UICONTROL Save]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-all-field-groups.png)

## Gegevenssets maken op basis van uw toestemmingsschema&#39;s {#datasets}

Voor elk van de vereiste hierboven beschreven schema&#39;s, moet u een dataset tot stand brengen die uiteindelijk de gegevens van de klantentoestemming zal opnemen. De dataset die op het verslagschema wordt gebaseerd moet voor [!DNL Real-time Customer Profile] worden toegelaten, terwijl de dataset die op het tijdreeksschema **wordt gebaseerd niet** [!DNL Profile]-toegelaten zou moeten zijn.

Selecteer **[!UICONTROL Datasets]** in de linkernavigatie en selecteer **[!UICONTROL Create dataset]** in de rechterbovenhoek om te beginnen.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create.png)

Selecteer **[!UICONTROL Create dataset from schema]** op de volgende pagina.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create-from-schema.png)

De **[!UICONTROL Create dataset from schema]**-workflow wordt weergegeven, te beginnen bij de stap **[!UICONTROL Select schema]**. Zoek in de opgegeven lijst een van de toestemmingsschema&#39;s die u eerder hebt gemaakt. U kunt de zoekbalk desgewenst gebruiken om de resultaten te beperken en het schema gemakkelijker te vinden. Selecteer het keuzerondje naast het gewenste schema en selecteer **[!UICONTROL Next]** om door te gaan.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-select-schema.png)

De stap **[!UICONTROL Configure dataset]** wordt weergegeven. Geef een unieke, gemakkelijk herkenbare naam en beschrijving voor de gegevensset voordat u **[!UICONTROL Finish]** selecteert.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-configure.png)

De detailspagina voor de pas gecreëerde dataset verschijnt. Als de dataset op uw tijd-reeksen schema gebaseerd is, dan is het proces volledig. Als de dataset op uw verslagschema gebaseerd is, moet de definitieve stap in het proces de dataset voor gebruik in [!DNL Real-time Customer Profile] toelaten.

Selecteer in de rechtertrack de **[!UICONTROL Profile]**-schakeloptie en selecteer **[!UICONTROL Enable]** in de bevestigingspop-up om het schema in te schakelen voor [!DNL Profile].

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-enable-profile.png)

Volg de bovenstaande stappen opnieuw om een op gebeurtenis-gebaseerde dataset tot stand te brengen als u een schema voor het creeerde.

## Volgende stappen

Door deze zelfstudie te volgen, hebt u minstens één dataset gecreeerd die nu kan worden gebruikt om de gegevens van de klantentoestemming te verzamelen:

* Een op verslag-gebaseerde dataset die voor gebruik in het Profiel van de Klant in real time wordt toegelaten. **(Vereist)**
* Een op tijdreeksen gebaseerde dataset die niet voor [!DNL Profile] wordt toegelaten. (Optioneel)

U kunt nu aan [IAB TCF 2.0 overzicht](./overview.md#merge-policies) terugkeren om het proces voort te zetten om Platform voor naleving te vormen TCF 2.0.

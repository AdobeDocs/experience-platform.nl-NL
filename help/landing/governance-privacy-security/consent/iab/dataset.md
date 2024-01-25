---
keywords: Experience Platform;home;IAB;IAB 2.0;toestemming;toestemming
solution: Experience Platform
title: Datasets maken voor het vastleggen van gegevens met IAB TCF 2.0-toestemming
description: Dit document verstrekt stappen voor vestiging de twee vereiste datasets om IAB TCF 2.0 toestemmingsgegevens te verzamelen.
exl-id: 36b2924d-7893-4c55-bc33-2c0234f1120e
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1580'
ht-degree: 0%

---

# Gegevenssets maken voor het vastleggen van gegevens met IAB TCF 2.0-toestemming

Adobe Experience Platform kan gegevens over toestemming van klanten verwerken in overeenstemming met de IAB [!DNL Transparency & Consent Framework] (TCF) 2.0, moeten die gegevens worden verzonden naar datasets de waarvan schema&#39;s TCF 2.0 toestemmingsgebieden bevatten.

Specifiek, worden twee datasets vereist voor het vangen van TCF 2.0 toestemmingsgegevens:

* Een gegevensset gebaseerd op de [!DNL XDM Individual Profile] klasse, ingeschakeld voor gebruik in [!DNL Real-Time Customer Profile].
* Een gegevensset gebaseerd op de [!DNL XDM ExperienceEvent] klasse.

>[!IMPORTANT]
>
>Platform dwingt slechts de koorden TCF die in de Individuele dataset van het Profiel worden verzameld af. Terwijl een dataset ExperienceEvent nog wordt vereist om een gegevensstroom als deel van dit werkschema tot stand te brengen, moet u slechts gegevens in de profieldataset opnemen. De dataset ExperienceEvent kan nog worden gebruikt als u gebeurtenissen van de toestemmingsverandering in tijd wilt volgen, maar deze waarden worden niet gebruikt binnen wanneer het afdwingen op segmentactivering.

Dit document verstrekt stappen voor vestiging deze twee datasets. Voor een overzicht van de volledige werkstroom om uw de gegevensverrichtingen van het Platform voor TCF 2.0 te vormen, verwijs naar [IAB TCF 2.0 nalevingsoverzicht](./overview.md).

## Vereisten

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Experience Data Model (XDM)](../../../../xdm/home.md): Het gestandaardiseerde kader waarbinnen [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
   * [Basisbeginselen van de schemacompositie](../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM.
* [Adobe Experience Platform Identity Service](../../../../identity-service/home.md): Hiermee kunt u de identiteit van klanten overbruggen op basis van verschillende gegevensbronnen op verschillende apparaten en systemen.
   * [Identiteitsnaamruimten](../../../../identity-service/features/namespaces.md): De identiteitsgegevens van de klant moeten worden verstrekt onder een specifieke naamruimte die door de Identiteitsdienst wordt erkend.
* [Klantprofiel in realtime](../../../../profile/home.md): Hefboomwerkingen [!DNL Identity Service] om u gedetailleerde klantenprofielen van uw datasets in real time te laten tot stand brengen. [!DNL Real-Time Customer Profile] trekt gegevens van het meer van Gegevens en handhaaft klantenprofielen in zijn eigen afzonderlijke gegevensopslag.

## TCF 2.0 veldgroepen {#field-groups}

De [!UICONTROL IAB TCF 2.0 Consent Details] de de gebiedsgroep van het schema verstrekt de gebieden van de klantengoedkeuring die voor TCF 2.0 steun worden vereist. Er zijn twee versies van deze veldgroep: een die compatibel is met de [!DNL XDM Individual Profile] en de andere klasse met de [!DNL XDM ExperienceEvent] klasse.

In de volgende secties wordt de structuur van elk van deze veldgroepen uitgelegd, inclusief de gegevens die ze tijdens inname verwachten.

### Profielveldgroep {#profile-field-group}

Voor schema&#39;s gebaseerd op [!DNL XDM Individual Profile]de [!UICONTROL IAB TCF 2.0 Consent Details] veldgroep levert één kaartveld, `identityPrivacyInfo`, waarin de identiteit van de klant wordt toegewezen aan de voorkeuren voor TCF-toestemming. Deze veldgroep moet in een op record gebaseerd schema worden opgenomen dat voor het Profiel van de Klant in real time wordt toegelaten voor automatische handhaving.

Zie de [naslaggids](../../../../xdm/field-groups/profile/iab.md) voor deze veldgroep voor meer informatie over de structuur en het gebruik van hoofdletters en kleine letters.

### Groep Gebeurtenisvelden {#event-field-group}

Als u gebeurtenissen voor het wijzigen van de toestemming wilt bijhouden in de loop van de tijd, kunt u de opdracht [!UICONTROL IAB TCF 2.0 Consent Details] veldgroep naar uw [!UICONTROL XDM ExperienceEvent] schema.

Als u niet van plan bent om gebeurtenissen van de toestemmingsverandering in tijd te volgen, te hoeven u om deze gebiedsgroep niet in uw gebeurtenisschema te omvatten. Bij het automatisch afdwingen van TCF toestemmingswaarden, gebruikt het Experience Platform slechts de recentste toestemmingsinformatie die in [profielveldgroep](#profile-field-group). Goedkeuringswaarden die door gebeurtenissen worden vastgelegd, nemen niet deel aan automatische workflows voor handhaving.

Zie de [naslaggids](../../../../xdm/field-groups/event/iab.md) voor deze veldgroep voor meer informatie over de structuur en het gebruiksgeval.

## Goedkeuringsschema&#39;s voor klanten maken {#create-schemas}

Om datasets tot stand te brengen die toestemmingsgegevens vangen, moet u XDM schema&#39;s eerst creëren om die datasets op te baseren.

Zoals vermeld in de vorige sectie, een schema dat gebruikt [!UICONTROL XDM Individual Profile] -klasse is vereist om toestemming af te dwingen in workflows van het downstream Platform. U kunt ook een afzonderlijk schema maken op basis van [!UICONTROL XDM ExperienceEvent] als u wijzigingen in de toestemming wilt bijhouden. Beide schema&#39;s moeten een `identityMap` en een geschikte TCF 2.0 veldgroep.

Selecteer in de interface Platform de optie **[!UICONTROL Schemas]** in de linkernavigatie om de [!UICONTROL Schemas] werkruimte. Voer van hieruit de stappen in de onderstaande secties uit om elk vereist schema te maken.

>[!NOTE]
>
>Als u bestaande XDM-schema&#39;s hebt die u wilt gebruiken om toestemmingsgegevens in plaats daarvan te vangen, kunt u die schema&#39;s uitgeven in plaats van nieuwe te creëren. Als een bestaand schema echter is ingeschakeld voor gebruik in Real-Time Klantprofiel, kan de primaire identiteit van het schema geen rechtstreeks identificeerbaar veld zijn dat niet mag worden gebruikt in op rente gebaseerde reclame, zoals een e-mailadres. Raadpleeg uw juridische adviseur als u niet zeker weet welke velden beperkt zijn.
>
>Bovendien kunnen bij het bewerken van bestaande schema&#39;s alleen additieve (vaste) wijzigingen worden aangebracht. Zie de sectie over de [beginselen van schemaontwikkeling](../../../../xdm/schema/composition.md#evolution) voor meer informatie .

### Een schema voor profieltoestemming maken {#profile-schema}

Selecteren **[!UICONTROL Create schema]** en kiest u **[!UICONTROL XDM Individual Profile]** in het vervolgkeuzemenu.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-profile.png)

De **[!UICONTROL Add field groups]** wordt weergegeven, zodat u meteen veldgroepen aan het schema kunt toevoegen. Van hier, selecteer **[!UICONTROL IAB TCF 2.0 Consent Details]** in de lijst. U kunt de zoekbalk desgewenst gebruiken om de resultaten te beperken en zo de veldgroep gemakkelijker te vinden.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-privacy.png)

Zoek vervolgens de **[!UICONTROL IdentityMap]** veldgroep in de lijst en selecteer deze ook. Als beide veldgroepen zijn opgenomen in de rechtertrack, selecteert u **[!UICONTROL Add field groups]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-identitymap.png)

Het canvas verschijnt opnieuw, waarbij wordt getoond dat de `identityPrivacyInfo` en `identityMap` er zijn velden toegevoegd aan de schemastructuur.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-privacy-structure.png)

Voordat u meer velden aan het schema toevoegt, selecteert u het basisveld dat moet worden weergegeven **[!UICONTROL Schema properties]** in de juiste rail, waar u een naam en een beschrijving voor het schema kunt verstrekken.

![](../../../images/governance-privacy-security/consent/iab/dataset/schema-details-profile.png)

Nadat u een naam en een beschrijving hebt verstrekt, kunt u naar keuze meer gebieden aan het schema toevoegen door te selecteren **[!UICONTROL Add]** onder de **[!UICONTROL Field groups]** aan de linkerkant van het canvas.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-profile.png)

Als u een bestaand schema bewerkt dat al is ingeschakeld voor gebruik in [!DNL Real-Time Customer Profile], selecteert u **[!UICONTROL Save]** om uw wijzigingen te bevestigen voordat u verdergaat met de sectie op [het creëren van een dataset die op uw toestemmingsschema wordt gebaseerd](#dataset). Als u een nieuw schema maakt, gaat u verder met de stappen in de onderstaande subsectie.

#### Het schema inschakelen voor gebruik in [!DNL Real-Time Customer Profile]

Als Platform de toestemmingsgegevens kan associëren het aan specifieke klantenprofielen ontvangt, moet het toestemmingsschema voor gebruik in worden toegelaten [!DNL Real-Time Customer Profile].

>[!NOTE]
>
>Het voorbeeldschema dat in deze sectie wordt getoond gebruikt zijn `identityMap` veld als primaire identiteit. Als u een ander veld wilt instellen als primaire identiteit, moet u ervoor zorgen dat u een indirecte id gebruikt, zoals een cookie-id, en niet een rechtstreeks identificeerbaar veld dat niet mag worden gebruikt in op rente gebaseerde reclame, zoals een e-mailadres. Raadpleeg uw juridische adviseur als u niet zeker weet welke velden beperkt zijn.
>
>De stappen op hoe te om een primair identiteitsgebied voor een schema te plaatsen kunnen in worden gevonden [[!UICONTROL Schemas] UI-hulplijn](../../../../xdm/ui/fields/identity.md).

Het schema inschakelen voor [!DNL Profile]selecteert u de naam van het schema in de linkerrail om het dialoogvenster **[!UICONTROL Schema properties]** sectie. Selecteer van hieruit de **[!UICONTROL Profile]** schakelknop.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-enable-profile.png)

Er wordt een pop-up weergegeven die aangeeft dat de primaire identiteit ontbreekt. Schakel het selectievakje in voor het gebruik van een andere primaire identiteit, aangezien de primaire identiteit in het dialoogvenster `identityMap` veld.

![](../../../images/governance-privacy-security/consent/iab/dataset/missing-primary-identity.png)

Tot slot selecteert u **[!UICONTROL Save]** om uw wijzigingen te bevestigen.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-save.png)

### Een schema voor gebeurtenismachtigingen maken {#event-schema}

>[!NOTE]
>
>Regelingen voor toestemming voor gebeurtenissen worden alleen gebruikt om gebeurtenissen met betrekking tot wijziging van de toestemming in de loop der tijd te volgen en nemen niet deel aan workflows voor afdwinging stroomafwaarts. Als u wijzigingen in de toestemming niet wilt bijhouden, kunt u de volgende sectie overslaan op [gegevensbestanden voor machtigingen maken](#datasets).

In de **[!UICONTROL Schemas]** werkruimte, selecteert u **[!UICONTROL Create schema]** en kiest u **[!UICONTROL XDM ExperienceEvent]** in de vervolgkeuzelijst.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-event.png)

De **[!UICONTROL Add field groups]** wordt weergegeven. Van hier, selecteer **[!UICONTROL IAB TCF 2.0 Consent Details]** in de lijst. U kunt de zoekbalk desgewenst gebruiken om de resultaten te beperken en zo de veldgroep gemakkelijker te vinden.


![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-privacy.png)

Zoek vervolgens de **[!UICONTROL IdentityMap]** veldgroep in de lijst en selecteer deze ook. Als beide veldgroepen zijn opgenomen in de rechtertrack, selecteert u **[!UICONTROL Add field groups]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-identitymap.png)

Het canvas verschijnt opnieuw, waarbij wordt getoond dat de `consentStrings` en `identityMap` er zijn velden toegevoegd aan de schemastructuur.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-privacy-structure.png)

Voordat u meer velden aan het schema toevoegt, selecteert u het basisveld dat moet worden weergegeven **[!UICONTROL Schema properties]** in de juiste rail, waar u een naam en een beschrijving voor het schema kunt verstrekken.

![](../../../images/governance-privacy-security/consent/iab/dataset/schema-details-event.png)

Nadat u een naam en een beschrijving hebt verstrekt, kunt u naar keuze meer gebieden aan het schema toevoegen door te selecteren **[!UICONTROL Add]** onder de **[!UICONTROL Field groups]** aan de linkerkant van het canvas.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-event.png)

Nadat u de gewenste veldgroepen hebt toegevoegd, selecteert u **[!UICONTROL Save]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-all-field-groups.png)

## Gegevenssets maken op basis van uw toestemmingsschema&#39;s {#datasets}

Voor elk van de vereiste hierboven beschreven schema&#39;s, moet u een dataset tot stand brengen die uiteindelijk de gegevens van de klantentoestemming zal opnemen. De dataset die op het verslagschema wordt gebaseerd moet worden toegelaten voor [!DNL Real-Time Customer Profile], terwijl de dataset die op het tijdreeksschema wordt gebaseerd **mogen niet** zijn [!DNL Profile]-enabled.

Selecteer **[!UICONTROL Datasets]** in de linkernavigatie selecteert u vervolgens **[!UICONTROL Create dataset]** in de rechterbovenhoek.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create.png)

Selecteer op de volgende pagina de optie **[!UICONTROL Create dataset from schema]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create-from-schema.png)

De **[!UICONTROL Create dataset from schema]** wordt weergegeven, vanaf de **[!UICONTROL Select schema]** stap. Zoek in de opgegeven lijst een van de toestemmingsschema&#39;s die u eerder hebt gemaakt. U kunt de zoekbalk desgewenst gebruiken om de resultaten te beperken en het schema gemakkelijker te vinden. Selecteer het keuzerondje naast het gewenste schema en selecteer vervolgens **[!UICONTROL Next]** om door te gaan.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-select-schema.png)

De **[!UICONTROL Configure dataset]** wordt weergegeven. Geef een unieke, gemakkelijk identificeerbare naam en beschrijving voor de gegevensset voordat u **[!UICONTROL Finish]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-configure.png)

De detailspagina voor de pas gecreëerde dataset verschijnt. Als de dataset op uw tijd-reeksen schema gebaseerd is, dan is het proces volledig. Als de dataset op uw verslagschema gebaseerd is, moet de definitieve stap in het proces de dataset voor gebruik toelaten binnen [!DNL Real-Time Customer Profile].

Selecteer in het rechterspoor de optie **[!UICONTROL Profile]** schakelen en vervolgens selecteren **[!UICONTROL Enable]** in de bevestigingspop-up om het schema voor [!DNL Profile].

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-enable-profile.png)

Volg de bovenstaande stappen opnieuw om een op gebeurtenis-gebaseerde dataset tot stand te brengen als u een schema voor het creeerde.

## Volgende stappen

Door deze zelfstudie te volgen, hebt u minstens één dataset gecreeerd die nu kan worden gebruikt om de gegevens van de klantentoestemming te verzamelen:

* Een op verslag-gebaseerde dataset die voor gebruik in het Profiel van de Klant in real time wordt toegelaten. **(Vereist)**
* Een op tijdreeksen gebaseerde dataset die niet wordt toegelaten voor [!DNL Profile]. (Optioneel)

U kunt nu terugkeren naar het dialoogvenster [IAB TCF 2.0 - overzicht](./overview.md#merge-policies) om het proces voort te zetten van het vormen Platform voor naleving TCF 2.0.

---
title: Identiteitsverwerking in de workflow voor doelactivering
description: Leer hoe identiteitsexport wordt verwerkt in de activeringsworkflow, afhankelijk van het doeltype
exl-id: f4894a08-c7a9-4d57-a6d3-660c49206d6a
source-git-commit: 322510055bd8b8803292a2b4af9df9e1dbee7ffb
workflow-type: tm+mt
source-wordcount: '1134'
ht-degree: 0%

---

# Identiteitsverwerking in de workflow voor doelactivering

Op deze pagina worden de bijzonderheden beschreven van de manier waarop identiteiten naar verschillende doeltypen worden geëxporteerd. U ziet dan hoe u kunt zoeken welke identiteiten afhankelijk van de bestemming beschikbaar zijn voor export.

>[!TIP]
>
> Voor uitgebreide informatie over identiteiten, identiteit namespaces, en definities van op identiteit betrekking hebbende termijnen, lees het [&#x200B; overzicht van de identiteitsdienst &#x200B;](/help/identity-service/home.md).

Elke bestemming in de [&#x200B; catalogus &#x200B;](/help/destinations/catalog/overview.md) is lichtjes verschillend, zodat is er geen one-size-past-alle opstelling over alle bestemmingen. Nochtans, zijn er een paar patronen die de opstelling van bestemmingen en hun identiteitsvereisten begeleiden, zoals die in de hieronder secties worden beschreven.

## Bestandsgebaseerde doelen {#file-based}

Voor [&#x200B; op dossier-gebaseerde bestemmingen &#x200B;](/help/destinations/destination-types.md#file-based) (bijvoorbeeld [!DNL Amazon S3], SFTP, de meeste e-mailmarketing bestemmingen zoals [!DNL Adobe Campaign], [!DNL Oracle Eloqua], [!DNL Salesforce Marketing Cloud]), is de identiteitsopstelling in de meeste van deze bestemmingen open, betekenend dat u niet wordt vereist om enige identiteit in de [&#x200B; Uitgezochte attributen &#x200B;](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes) stap van het werkschema van de partijactivering te selecteren.

Als u verkiest om identiteiten aan uw dossieruitvoer toe te voegen, merk op dat slechts één enkele identiteit van [&#x200B; identiteit namespace &#x200B;](/help/identity-service/features/identity-graph-viewer.md#access-identity-graph-viewer) in de uitvoer kan worden geselecteerd. Wanneer u een identiteit voor de uitvoer selecteert, wordt het automatisch geselecteerd als a [&#x200B; verplichte attributen &#x200B;](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes) en [&#x200B; deduplicatietoets &#x200B;](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys).

![&#x200B; een identiteit die als verplicht attribuut en deduplicatiesleutel wordt geselecteerd.](/help/destinations/assets/how-destinations-work/selected-identity.png)

Als tijdelijke oplossing kunt u meer identiteiten aan het exporteren toevoegen als deze als kenmerken in het Experience Platform zijn opgenomen. Zie onder een voorbeeld waarin het e-mailadres van het XDM-kenmerk is geselecteerd voor export, naast de naamruimte voor identiteiten `Phone_E.164` .

![&#x200B; Voorbeeld van e-mailadresattribuut dat voor de uitvoer wordt geselecteerd.](/help/destinations/assets/how-destinations-work/email-selected.png)

## Een identiteit exporteren vanuit een identiteitskaart in plaats van een identiteit te exporteren als een XDM-kenmerk - de verschillen {#identity-map-or-attribute}

Het aantal geëxporteerde records kan verschillen, afhankelijk van de vraag of u voor exportidentiteiten in het identiteitsoverzicht of identiteiten selecteert die als kenmerken in het Experience Platform zijn opgenomen. [&#x200B; beleid van de Fusie &#x200B;](/help/profile/merge-policies/overview.md) speelt ook een belangrijke rol in het aantal verslagen die worden uitgevoerd wanneer u identiteiten van de identiteitskaart selecteert.

Stel dat u uit twee verschillende datasets de volgende profielfragmenten hebt die worden samengevoegd in één klantprofiel:

**fragment van het Profiel één**

| Identiteitskaart | Voornaam | Achternaam | E-mailkenmerk |
|---------|----------|---------|--------|
| email1, Loyalty ID1 | John | Doe | e-mail 1 |


**fragment van het Profiel twee**

| Identiteitskaart | Voornaam | Achternaam | E-mailkenmerk |
|---------|----------|---------|--------|
| email2, Loyalty ID1 | John | Doe | e-mail 2 |

Het samengevoegde profiel ziet er als volgt uit:

| Identiteitskaart | Voornaam | Achternaam | E-mailkenmerk |
|---------|----------|---------|--------|
| e-mail 1, email2, Loyalty ID1 | John | Doe | e-mail 2 |

Het exportgedrag is anders, afhankelijk van de vraag of u `IdentityMap: Email` of `xdm: personalEmail.address` selecteert voor exporteren.

Als een klant `IdentityMap: Email` activeert, bevat het geëxporteerde bestand twee records: een voor e-mail1 en een voor e-mail2.

Als een klant echter `xdm: personalEmail.address` activeert, is alleen email2 aanwezig in de record, aangezien het veld E-mailkenmerk alleen email2 bevat. In deze situaties kunnen verschillende gebruiksgevallen worden opgelost waarbij u mogelijk alle e-mailadressen wilt activeren die in het bestand staan voor een klant, of alleen het meest recente e-mailadres dat in het bestand staat voor de klant.

Het wegnemen is dat het aantal records dat u exporteert, afhankelijk is van het gekozen samenvoegbeleid en of u identiteiten of kenmerken selecteert in het exporteren.

## Op API gebaseerde streamingdoelen {#streaming-destinations}

[&#x200B; op API-Gebaseerde die bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destination) met [&#x200B; Destination SDK &#x200B;](/help/destinations/destination-sdk/overview.md) (bijvoorbeeld [!DNL Facebook], [!DNL Google Customer Match], [!DNL Pinterest], [!DNL Braze], en anderen) wordt gebouwd steunen slechts specifieke IDs voor de uitvoer. Voor gedetailleerde informatie over de specifieke identiteiten die naar elke bestemming kunnen worden uitgevoerd, lees de *gesteunde identiteiten* sectie in elke pagina van de bestemmingsdocumentatie (bijvoorbeeld, zie de [&#x200B; gesteunde identiteitssectie &#x200B;](/help/destinations/catalog/advertising/pinterest.md) in de [!DNL Pinterest] bestemmingspagina).

Nota, echter, dat u de flexibiliteit hebt om gegevens van of [&#x200B; privé grafieken &#x200B;](/help/profile/merge-policies/overview.md#id-stitching) of van attributen als identiteiten te gebruiken. Dit betekent dat u attributen XDM aan het identiteitsgebied kunt in kaart brengen dat door de bestemming wordt vereist. Zie onder een voorbeeld voor het doel [!DNL Pinterest] , waarbij het XDM-kenmerk `personalEmail.address` wordt toegewezen aan de vereiste [!DNL Pinterest] identity `pinterest_audience` .

>[!TIP]
>
>Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om de gegevens automatisch te laten hashen bij activering door het Experience Platform. Lees meer over de **[!UICONTROL Apply transformation]** optie in het [&#x200B; het stromen de activeringsleerprogramma van bestemmingen &#x200B;](/help/destinations/ui/activate-segment-streaming-destinations.md#apply-transformation).

![&#x200B; Voorbeeld van e-mailadresattribuut in kaart gebracht aan identiteitsgebied voor de bestemming van Pinterest.](/help/destinations/assets/how-destinations-work/email-mapped-to-identity.png)

### Advertising-bestemmingen die afhankelijk zijn van integratie met cookies van derden {#third-party-cookie-destinations}

Advertising-doelen die afhankelijk zijn van cookies van derden (bijvoorbeeld: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google DV360], [!DNL Bing], [!DNL The Trade Desk]), vereisen niet dat klanten id&#39;s selecteren in de activeringsworkflow. Voor deze bestemmingen, wanneer vestiging een activeringswerkschema, zoekt het Experience Platform automatisch de lijst van de identiteitsgelijke die door [[!UICONTROL Experience Cloud ID service] wordt geconstrueerd &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=nl-NL) en voert alle identiteiten uit die voor een profiel beschikbaar zijn en door de bestemming worden gesteund.

Voor deze doelen is id-synchronisatie vereist via de [!UICONTROL Experience Cloud ID service] of via [!UICONTROL Experience Platform Web SDK] .

Als u [!UICONTROL Experience Platform Web SDK] gebruikt en erfenis [!UICONTROL Experience Cloud ID service] niet op de pagina wordt uitgevoerd, dan moet u ervoor zorgen dat de gegevensstroom voor de website in kwestie wordt toegelaten om voor de synchronisatie van identiteitskaart van de Derde toe te staan, zoals die in [&#x200B; wordt geschetst vormt datastream documentatie &#x200B;](/help/datastreams/configure.md#create).

Wanneer u een gegevensstroom configureert zoals wordt beschreven in de bovenstaande documentatie, moet u ervoor zorgen dat de schuifregelaar **[!UICONTROL Third Party ID Sync]** is ingeschakeld. De meeste klanten zouden het veld `container_id` leeg laten (standaard ingesteld op 0). U hoeft deze waarde alleen te wijzigen als uw implementatie van een oudere Audience Manager een specifieke container-id gebruikt (dit zou echter de grote minderheid van klanten zijn).

>[!NOTE]
>
>De meeste van deze advertentiebestemmingen worden gesteund in Audience Manager (deze bestemmingstypes zijn gekend in Audience Manager als op apparaat-gebaseerde bestemmingen. Zie a [&#x200B; lijst van alle gesteunde op apparaat-gebaseerde bestemmingen in Audience Manager &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/device-based/device-based-destinations-list.html?lang=nl-NL)). Er worden slechts enkele in Experience Platform vermeld. Voor informatie over het delen van gegevens tussen Experience Platform en Audience Manager, lees de sectie over [&#x200B; toelatend gegevens die van Experience Platform aan Audience Manager &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=nl-NL#enable-aep-to-aam-data) delen. Momenteel is er geen plan om meer cookie-doelen van derden te ondersteunen.

## Enterprise-bestemmingen {#enterprise-destinations}

[&#x200B; de bestemmingen van de Onderneming &#x200B;](/help/destinations/destination-types.md#advanced-enterprise-destinations) ([!DNL Amazon Kinesis], [!DNL Azure Event Hubs], HTTP API) vereisen geen specifieke IDs in de gegevensuitvoer, aangezien deze voor de gebruiksgevallen van de ondernemingsintegratie worden ontworpen. Nochtans, kunt u identiteiten als attributen XDM of van de identiteitskaart uitvoeren, als u wenst. Bekijk een [&#x200B; voorbeeld van uitgevoerde gegevens aan de bestemming van HTTP &#x200B;](/help/destinations/catalog/streaming/http-destination.md#exported-data), die zowel het `personalEmail.address` attribuut XDM, als de identiteiten `ECID` en `email_lc_sha256` (gehakt e-mailadres) van de identiteitskaart omvat.

## Personalization-bestemmingen {#personalization-destinations}

[&#x200B; Personalization (of rand) bestemmingen &#x200B;](/help/destinations/destination-types.md#edge-personalization-destinations) (bijvoorbeeld: Adobe Target, [!DNL Custom Personalization]) vereisen geen identiteitsselectie in het activeringswerkschema, aangezien de integratie een profielraadpleging is. De client ([!DNL Target], [!DNL Web SDK] of anderen) vraagt naar de [[!UICONTROL Edge]](/help/collection/home.md#edge) en haalt de profielgegevens op die de client nodig heeft voor on-site personalisatie.

<!--
![Table with all supported identities](/help/destinations/assets/how-destinations-work/identities-table.png)

-->

## Volgende stappen {#next-steps}

Nadat u dit document hebt gelezen, weet u nu hoe u kunt achterhalen welke identiteiten worden ondersteund of vereist voor afzonderlijke doelen. U weet nu ook hoe identiteitsselectie voor elk bestemmingstype werkt.

Daarna, kunt u lezen over welke [&#x200B; de uitvoermontages &#x200B;](/help/destinations/how-destinations-work/destinations-configurations.md) voor bestemmingen over bestemmingstypes gemeenschappelijk zijn, die op een individueel bestemmingsniveau door ontwikkelaars kunnen worden gevormd, en welke montages door gebruikers in het activeringswerkschema kunnen worden uitgegeven.

U kunt alle beschikbare bestemmingen in de [&#x200B; catalogus &#x200B;](/help/destinations/catalog/overview.md) ook controleren.

---
title: Identiteitsverwerking in de workflow voor doelactivering
description: Leer hoe identiteitsexport wordt verwerkt in de activeringsworkflow, afhankelijk van het doeltype
exl-id: f4894a08-c7a9-4d57-a6d3-660c49206d6a
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1151'
ht-degree: 0%

---

# Identiteitsverwerking in de workflow voor doelactivering

Op deze pagina worden de bijzonderheden beschreven van de manier waarop identiteiten naar verschillende doeltypen worden geëxporteerd. U ziet dan hoe u kunt zoeken welke identiteiten afhankelijk van de bestemming beschikbaar zijn voor export.

>[!TIP]
>
> Voor uitgebreide informatie over identiteiten, naamruimten, en definities van aan identiteit verwante termijnen, lees [Overzicht van identiteitsservice](/help/identity-service/home.md).

Elke bestemming in de [catalogus](/help/destinations/catalog/overview.md) is lichtjes verschillend, zodat is er geen één-grootte-pasvorm-al opstelling over alle bestemmingen. Nochtans, zijn er een paar patronen die de opstelling van bestemmingen en hun identiteitsvereisten begeleiden, zoals die in de hieronder secties worden beschreven.

## Bestandsgebaseerde doelen {#file-based}

Voor [bestandsgebaseerde doelen](/help/destinations/destination-types.md#file-based) (bijvoorbeeld [!DNL Amazon S3], SFTP, de meeste e-mailmarketing bestemmingen zoals [!DNL Adobe Campaign], [!DNL Oracle Eloqua], [!DNL Salesforce Marketing Cloud]), is de identiteitsopstelling in de meeste van deze bestemmingen open, betekenend dat u om het even welke identiteit in niet moet selecteren [Kenmerken selecteren](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes) stap van de batchactiveringsworkflow.

Als u ervoor kiest id&#39;s toe te voegen aan uw geëxporteerde bestanden, moet u niet vergeten dat er slechts één identiteit uit het menu [naamruimte identity](/help/identity-service/ui/identity-graph-viewer.md#access-identity-graph-viewer) kan worden geselecteerd in een exportbewerking. Wanneer u een identiteit selecteert om te exporteren, wordt deze automatisch geselecteerd als een [mandatory, kenmerk](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes) en [deduplicatie-sleutel](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys).

![Een identiteit die is geselecteerd als verplicht kenmerk en een deduplicatietoets.](/help/destinations/assets/how-destinations-work/selected-identity.png)

Als tijdelijke oplossing kunt u meer identiteiten aan het exporteren toevoegen als deze als kenmerken in het Experience Platform zijn opgenomen. Zie onder een voorbeeld waarin het e-mailadres van het XDM-kenmerk is geselecteerd voor export, in aanvulling op de naamruimte identity `Phone_E.164`.

![Voorbeeld van het kenmerk E-mailadres dat is geselecteerd voor exporteren.](/help/destinations/assets/how-destinations-work/email-selected.png)

## Een identiteit exporteren vanuit een identiteitskaart in plaats van een identiteit te exporteren als een XDM-kenmerk - de verschillen {#identity-map-or-attribute}

Het aantal geëxporteerde records kan verschillen, afhankelijk van de vraag of u voor exportidentiteiten in het identiteitsoverzicht of identiteiten selecteert die als kenmerken in het Experience Platform zijn opgenomen. [Beleid samenvoegen](/help/profile/merge-policies/overview.md) speelt ook een belangrijke rol in het aantal verslagen die worden uitgevoerd wanneer u identiteiten van de identiteitskaart selecteert.

Stel dat u uit twee verschillende datasets de volgende profielfragmenten hebt die worden samengevoegd in één klantprofiel:

**Profielfragment één**

| Identiteitskaart | Voornaam | Achternaam | E-mailkenmerk |
|---------|----------|---------|--------|
| email1, Loyalty ID1 | John | Doe | e-mail 1 |


**Profielfragment twee**

| Identiteitskaart | Voornaam | Achternaam | E-mailkenmerk |
|---------|----------|---------|--------|
| email2, Loyalty ID1 | John | Doe | e-mail 2 |

Het samengevoegde profiel ziet er als volgt uit:

| Identiteitskaart | Voornaam | Achternaam | E-mailkenmerk |
|---------|----------|---------|--------|
| e-mail 1, email2, Loyalty ID1 | John | Doe | e-mail 2 |

Het exportgedrag is afhankelijk van de vraag of u `IdentityMap: Email` of `xdm: personalEmail.address` voor uitvoer.

Als een klant activeert `IdentityMap: Email`Er staan twee records in het geëxporteerde bestand: een voor e-mail1 en een voor e-mail2.

Als een klant echter `xdm: personalEmail.address`, bevat de record alleen e-mail2, omdat het veld E-mailkenmerk alleen e-mail2 bevat. In deze situaties kunnen verschillende gebruiksgevallen worden opgelost waarbij u mogelijk alle e-mailadressen wilt activeren die in het bestand staan voor een klant, of alleen het meest recente e-mailadres dat in het bestand staat voor de klant.

Het wegnemen is dat het aantal records dat u exporteert, afhankelijk is van het gekozen samenvoegbeleid en of u identiteiten of kenmerken selecteert in het exporteren.

## Op API gebaseerde streamingdoelen {#streaming-destinations}

[Op API gebaseerde streamingdoelen](/help/destinations/destination-types.md#streaming-destination) gebouwd met [Destination SDK](/help/destinations/destination-sdk/overview.md) (bijvoorbeeld [!DNL Facebook], [!DNL Google Customer Match], [!DNL Pinterest], [!DNL Braze]en andere) ondersteunen alleen specifieke id&#39;s voor exporteren. Voor gedetailleerde informatie over de specifieke identiteiten die naar elke bestemming kunnen worden uitgevoerd, lees *ondersteunde identiteiten* in elke pagina van de bestemmingsdocumentatie (bijvoorbeeld, zie [sectie met ondersteunde identiteiten](/help/destinations/catalog/advertising/pinterest.md) in de [!DNL Pinterest] doelpagina).

Houd er echter rekening mee dat u over de flexibiliteit beschikt om gegevens uit een van beide [privégrafieken](/help/profile/merge-policies/overview.md#id-stitching) of van kenmerken als identiteiten. Dit betekent dat u attributen XDM aan het identiteitsgebied kunt in kaart brengen dat door de bestemming wordt vereist. Zie hieronder een voorbeeld voor de [!DNL Pinterest] doel, waarbij het XDM-kenmerk `personalEmail.address` is toegewezen aan de vereiste [!DNL Pinterest] identiteit `pinterest_audience`.

>[!TIP]
>
>Wanneer het bronveld hashkenmerken bevat, controleert u de **[!UICONTROL Apply transformation]** als u wilt dat Experience Platform de gegevens automatisch verbergt bij activering. Meer informatie over de **[!UICONTROL Apply transformation]** in de [activeringszelfstudie voor streaming doelen](/help/destinations/ui/activate-segment-streaming-destinations.md#apply-transformation).

![Voorbeeld van e-mailadreskenmerk toegewezen aan identiteitsveld voor Pinterest-bestemming.](/help/destinations/assets/how-destinations-work/email-mapped-to-identity.png)

### Reclamebestemmingen die afhankelijk zijn van cookie-integratie van derden {#third-party-cookie-destinations}

Reclamebestemmingen die afhankelijk zijn van cookies van derden (bijvoorbeeld: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google DV360], [!DNL Bing], [!DNL The Trade Desk]) vereist niet dat klanten id&#39;s selecteren in de activeringsworkflow. Voor deze bestemmingen, wanneer vestiging een activeringswerkschema, kijkt het Experience Platform automatisch omhoog de lijst van de identiteitsgelijke die door wordt geconstrueerd [[!UICONTROL Experience Cloud ID service]](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) en exporteert u alle identiteiten die beschikbaar zijn voor een profiel en die door de bestemming worden ondersteund.

Voor deze doelen is een id-sync vereist via een van de [!UICONTROL Experience Cloud ID service] of via [!UICONTROL Experience Platform Web SDK].

Als u [!UICONTROL Experience Platform Web SDK] en de erfenis [!UICONTROL Experience Cloud ID service] niet op de pagina wordt geïmplementeerd, dan moet u ervoor zorgen dat de gegevensstroom voor de website in kwestie is ingeschakeld zodat ID-synchronisatie van derden mogelijk is, zoals beschreven in het [configureren, gegevensstroomdocumentatie](/help/datastreams/configure.md#create).

Wanneer u een gegevensstroom configureert zoals wordt beschreven in de bovenstaande documentatie, moet u ervoor zorgen dat de **[!UICONTROL Third Party ID Sync]** is ingeschakeld. De meeste klanten zouden de `container_id` veld leeg (standaard 0). U hoeft deze waarde alleen te wijzigen als uw implementatie van een oudere Audience Manager een specifieke container-id gebruikt (dit zou echter de grote minderheid van klanten zijn).

>[!NOTE]
>
>De meeste van deze advertentiebestemmingen worden gesteund in Audience Manager (deze bestemmingstypes zijn gekend in Audience Manager als op apparaat-gebaseerde bestemmingen. Zie een [lijst van alle gesteunde op apparaat-gebaseerde bestemmingen in Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/device-based/device-based-destinations-list.html)). Er worden slechts enkele in Experience Platform vermeld. Voor informatie over het delen van gegevens tussen Experience Platform en Audience Manager, lees de sectie over [gegevens delen van Experience Platform naar Audience Manager inschakelen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#enable-aep-to-aam-data). Momenteel is er geen plan om meer cookie-doelen van derden te ondersteunen.

## Enterprise-bestemmingen {#enterprise-destinations}

[Enterprise-bestemmingen](/help/destinations/destination-types.md#streaming-profile-export) ([!DNL Amazon Kinesis], [!DNL Azure Event Hubs], (HTTP API) vereisen geen specifieke id&#39;s in de gegevensexport, aangezien deze ontworpen zijn voor gebruik bij de integratie van bedrijven. Nochtans, kunt u identiteiten als attributen XDM of van de identiteitskaart uitvoeren, als u wenst. Een [voorbeeld van geëxporteerde gegevens naar de HTTP-bestemming](/help/destinations/catalog/streaming/http-destination.md#exported-data), waarin zowel de `personalEmail.address` XDM-kenmerk en de identiteiten `ECID` en `email_lc_sha256` (gehasht e-mailadres) van het identiteitsoverzicht.

## Aanpassingsdoelen {#personalization-destinations}

[Aanpassingsdoelen (of randdoelen)](/help/destinations/destination-types.md#edge-personalization-destinations) (bijvoorbeeld Adobe Target, [!DNL Custom Personalization]) hoeft u geen identiteit te selecteren in de activeringsworkflow, omdat de integratie een opgezocht profiel is. De client ([!DNL Target], [!DNL Web SDK], of anderen) vraagt de [[!UICONTROL Edge]](/help/collection/home.md#edge) en haalt de profielinformatie die het voor onsite verpersoonlijking nodig heeft.

<!--
![Table with all supported identities](/help/destinations/assets/how-destinations-work/identities-table.png)

-->

## Volgende stappen {#next-steps}

Nadat u dit document hebt gelezen, weet u nu hoe u kunt achterhalen welke identiteiten worden ondersteund of vereist voor afzonderlijke doelen. U weet nu ook hoe identiteitsselectie voor elk bestemmingstype werkt.

Vervolgens kunt u lezen over welke [exportinstellingen](/help/destinations/how-destinations-work/destinations-configurations.md) voor bestemmingen zijn gemeenschappelijk over bestemmingstypes, die op een individueel bestemmingsniveau door ontwikkelaars kunnen worden gevormd, en welke montages door gebruikers in het activeringswerkschema kunnen worden uitgegeven.

U kunt ook alle beschikbare doelen uitchecken in de [catalogus](/help/destinations/catalog/overview.md).

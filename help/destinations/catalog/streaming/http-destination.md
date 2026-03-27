---
keywords: streaming; HTTP-bestemming
title: HTTP API-verbinding
description: Gebruik de HTTP API-bestemming in Adobe Experience Platform om profielgegevens naar een extern HTTP-eindpunt te verzenden om uw eigen analyses uit te voeren of andere bewerkingen uit te voeren die u nodig hebt voor profielgegevens die uit Experience Platform zijn geëxporteerd.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 0fc433689ac351bff3fc6930f5e4781f9cde5ade
workflow-type: tm+mt
source-wordcount: '2898'
ht-degree: 0%

---

# HTTP API-verbinding

## Overzicht {#overview}

>[!IMPORTANT]
>
> Deze bestemming is beschikbaar slechts aan [&#x200B; Adobe Real-Time Customer Data Platform Ultimate &#x200B;](https://helpx.adobe.com/nl/legal/product-descriptions/real-time-customer-data-platform.html) klanten.

De HTTP API-bestemming is een Experience Platform-streamingbestemming waarmee u profielgegevens naar HTTP-eindpunten van derden kunt verzenden.

Om profielgegevens naar eindpunten van HTTP te verzenden, moet u eerst [&#x200B; met de bestemming &#x200B;](#connect-destination) in Experience Platform verbinden.

## Gebruiksscenario&#39;s {#use-cases}

Gebruik de HTTP API-bestemming om XDM-profielgegevens en -publiek te exporteren naar algemene HTTP-eindpunten. Daar kunt u uw eigen analyses uitvoeren of andere bewerkingen uitvoeren die u nodig hebt voor profielgegevens die uit Experience Platform zijn geëxporteerd.

De eindpunten van HTTP kunnen of de systemen van klanten of derdeoplossingen zijn.

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#x200B; &#x200B;](../../../segmentation/home.md). |
| Alle andere doelgroepen | Ja | Deze categorie omvat alle oorsprong van het publiek buiten het publiek dat via [!DNL Segmentation Service] wordt gegenereerd. Lees over de [&#x200B; diverse publieksoorsprong &#x200B;](/help/segmentation/ui/audience-portal.md#customize). Voorbeelden zijn: <ul><li> de douane uploadt publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers,</li><li> gelijksoortige doelgroepen, </li><li> federaal publiek, </li><li> publiek dat wordt gegenereerd in andere Experience Platform-toepassingen, zoals [!DNL Adobe Journey Optimizer] , </li><li> en meer. </li></ul> |

{style="table-layout:auto"}

Ondersteund publiek per type publieksgegevens:

| Gegevenstype Publiek | Ondersteund | Beschrijving | Gebruiksscenario&#39;s |
|--------------------|-----------|-------------|-----------|
| [&#x200B; het publiek van Mensen &#x200B;](/help/segmentation/types/people-audiences.md) | Ja | Gebaseerd op klantprofielen. Gebruik deze om specifieke groepen mensen te kiezen voor marketingcampagnes. | Frequente kopers, winkeliers |
| [&#x200B; publiek van de Rekening &#x200B;](/help/segmentation/types/account-audiences.md) | Nee | Doelpersonen binnen specifieke organisaties voor marketingstrategieën op basis van account. | B2B-marketing |
| [&#x200B; Het publiek van het Vooruitzicht &#x200B;](/help/segmentation/types/prospect-audiences.md) | Nee | De individuen van het doel die nog geen klanten zijn maar eigenschappen met uw doelpubliek delen. | Waarschuwing met gegevens van derden |
| [&#x200B; de uitvoer van de Dataset &#x200B;](/help/catalog/datasets/overview.md) | Nee | Verzamelingen gestructureerde gegevens die zijn opgeslagen in het [!DNL Adobe Experience Platform] Data Lake. | Rapportage, workflows voor gegevenswetenschap |

{style="table-layout:auto"}


## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
| ---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een publiek, samen met de gewenste schemagebieden (bijvoorbeeld: e-mailadres, telefoonaantal, achternaam), zoals gekozen in het kaartscherm van het [&#x200B; werkschema van de bestemmingsactivering &#x200B;](../../ui/activate-segment-streaming-destinations.md#mapping). |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [&#x200B; het stromen bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Vereisten {#prerequisites}

Als u de HTTP API-bestemming wilt gebruiken om gegevens uit Experience Platform te exporteren, moet u aan de volgende voorwaarden voldoen:

* U moet een eindpunt van HTTP hebben dat REST API steunt.
* Het HTTP-eindpunt moet het Experience Platform-profielschema ondersteunen. Transformatie naar een extern payload-schema wordt niet ondersteund in de HTTP API-bestemming. Verwijs naar de [&#x200B; uitgevoerde gegevens &#x200B;](#exported-data) sectie voor een voorbeeld van het de outputschema van Experience Platform.
* Uw eindpunt van HTTP moet kopballen steunen.
* Uw eindpunt van HTTP moet binnen 2 seconden antwoorden om juiste gegevensverwerking te verzekeren en onderbrekingsfouten te vermijden.
* Als u mTLS wilt gebruiken: voor uw gegevens die eindpunt ontvangen, moet TLS zijn uitgeschakeld en alleen mTLS zijn ingeschakeld.

>[!TIP]
>
> U kunt [&#x200B; Adobe Experience Platform Destination SDK &#x200B;](/help/destinations/destination-sdk/overview.md) aan opstelling ook gebruiken en Experience Platform profielgegevens verzenden naar een eindpunt van HTTP.

## mTLS-protocolondersteuning en -certificaat {#mtls-protocol-support}

U kunt [!DNL Mutual Transport Layer Security] (mTLS) gebruiken om verbeterde beveiliging te garanderen in uitgaande verbindingen met uw HTTP API-doelverbindingen.

mTLS is een wederzijds authentificatieprotocol dat ervoor zorgt dat beide partijen die informatie delen wie zij beweren te zijn alvorens de gegevens worden gedeeld. mTLS bevat een extra stap in vergelijking met standaard-TLS, waarin de server ook om het clientcertificaat vraagt en dit verifieert, terwijl de client het servercertificaat verifieert.

### mTLS-overwegingen {#mtls-considerations}

De steun mTLS voor HTTP API bestemmingen past **slechts op de gegevens toe die eindpunt** ontvangen waar de profieluitvoer wordt verzonden (het **[!UICONTROL HTTP Endpoint]** gebied in [&#x200B; bestemmingsdetails &#x200B;](#destination-details)).

### mTLS configureren voor gegevensexport {#configuring-mtls}

Om mTLS met HTTP API bestemmingen te gebruiken, **[!UICONTROL HTTP Endpoint]** (gegevens die eindpunt ontvangen) u in de [&#x200B; bestemmingdetails &#x200B;](#destination-details) pagina vormt moet de protocollen van TLS gehandicapt hebben en slechts mTLS toegelaten. Als het TLS 1.2 protocol nog op het eindpunt wordt toegelaten, wordt geen certificaat verzonden voor de cliëntauthentificatie. Dit betekent dat om mTLS met uw bestemming van HTTP API te gebruiken, uw gegevens die servereindpunt ontvangen een mTLS-slechts toegelaten verbindingspunt moeten zijn.

### Certificaatdetails ophalen en inspecteren {#certificate}

Als u certificaatdetails zoals de Gemeenschappelijke Naam (CN) en de Alternatieve Namen van het Onderwerp (San) voor extra derdebevestiging wilt inspecteren, gebruik API om het certificaat terug te winnen en die gebieden uit de reactie te halen.

Zie de [&#x200B; openbare documentatie van het certificaateindpunt &#x200B;](../../../data-governance/mtls-api/public-certificate-endpoint.md) voor meer informatie.

## IP adres lijst van gewenste personen {#ip-address-allowlist}

Experience Platform biedt een lijst met statische IP&#39;s die u voor de HTTP API-bestemming kunt lijsten van gewenste personen om aan de beveiligings- en compatibiliteitseisen van klanten te voldoen. Zie {de lijst van gewenste personen van het 0} IP adres voor het stromen bestemmingen [&#x200B; voor de volledige lijst van IPs aan lijst van gewenste personen.](/help/destinations/catalog/streaming/ip-address-allow-list.md)

## Ondersteunde verificatietypen {#supported-authentication-types}

De HTTP API bestemming steunt verscheidene authentificatietypen aan uw eindpunt van HTTP:

* HTTP-eindpunt zonder verificatie;
* Toekenning aan toonder;
* [&#x200B; OAuth 2.0 cliëntgeloofsbrieven &#x200B;](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) authentificatie met de lichaamvorm, met [!DNL client ID], [!DNL client secret], en [!DNL grant type] in het lichaam van het HTTP- verzoek, zoals aangetoond in het voorbeeld hieronder.

```shell
curl --location --request POST '<YOUR_API_ENDPOINT>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>'
```

* [&#x200B; OAuth 2.0 cliëntgeloofsbrieven &#x200B;](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) met basisvergunning, met een vergunningskopbal die URL-Gecodeerde [!DNL client ID] en [!DNL client secret] bevat.

```shell
curl --location --request POST 'https://some-api.com/token' \
--header 'Authorization: Basic base64(clientId:clientSecret)' \
--header 'Content-type: application/x-www-form-urlencoded; charset=UTF-8' \
--data-urlencode 'grant_type=client_credentials'
```

* [&#x200B; OAuth 2.0 wachtwoordsubsidie &#x200B;](https://www.oauth.com/oauth2-servers/access-tokens/password-grant/).

## Verbinden met de bestemming {#connect-destination}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven. Wanneer u verbinding maakt met dit doel, moet u de volgende informatie opgeven:

### Verificatiegegevens {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_clientcredentialstype"
>title="Type clientgegevens"
>abstract="Selecteer **Gecodeerde Vorm van het Lichaam** om cliëntidentiteitskaart en cliëntgeheim in het lichaam van het verzoek te omvatten of **Basisvergunning** om cliëntidentiteitskaart en cliëntgeheim in een vergunningskopbal te omvatten. Voorbeelden weergeven in de documentatie."

#### Toekennerverificatie {#bearer-token-authentication}

Als u het verificatietype **[!UICONTROL Bearer token]** selecteert om verbinding te maken met het HTTP-eindpunt, voert u hieronder de informatie in en selecteert u **[!UICONTROL Connect to destination]** :

![&#x200B; het de authentificatiescherm van HTTP API met het [!UICONTROL Bearer token] gebied.](../../assets/catalog/http/http-api-authentication-bearer.png)

* **[!UICONTROL Bearer token]**: voer het token voor toonder in om op uw HTTP-locatie te verifiëren.

#### Geen verificatie {#no-authentication}

Als u het verificatietype **[!UICONTROL None]** selecteert om verbinding te maken met het HTTP-eindpunt:

![&#x200B; het de authentificatiescherm van HTTP API met het [!UICONTROL None] geselecteerde authentificatietype.](../../assets/catalog/http/http-api-authentication-none.png)

Wanneer u deze verificatieoptie selecteert, hoeft u alleen **[!UICONTROL Connect to destination]** te selecteren en de verbinding met het eindpunt tot stand te brengen.

#### OAuth 2 Password authentication {#oauth-2-password-authentication}

Als u het verificatietype **[!UICONTROL OAuth 2 Password]** selecteert om verbinding te maken met het HTTP-eindpunt, voert u hieronder de informatie in en selecteert u **[!UICONTROL Connect to destination]** :

![&#x200B; het de authentificatiescherm van HTTP API met [!UICONTROL OAuth 2 Password] gebieden.](../../assets/catalog/http/http-api-authentication-oauth2-password.png)

* **[!UICONTROL Access Token URL]**: De URL aan uw zijde die toegangstokens uitgeeft en, naar keuze, tokens vernieuwt.
* **[!UICONTROL Client ID]**: De `client ID` die uw systeem toewijst aan Adobe Experience Platform.
* **[!UICONTROL Client Secret]**: De `client secret` die uw systeem toewijst aan Adobe Experience Platform.
* **[!UICONTROL Username]**: De gebruikersnaam die toegang geeft tot het HTTP-eindpunt.
* **[!UICONTROL Password]**: Het wachtwoord om tot uw eindpunt van HTTP toegang te hebben.

#### OAuth 2 Client Credentials-verificatie {#oauth-2-client-credentials-authentication}

Als u het verificatietype **[!UICONTROL OAuth 2 Client Credentials]** selecteert om verbinding te maken met het HTTP-eindpunt, voert u hieronder de informatie in en selecteert u **[!UICONTROL Connect to destination]** :

![&#x200B; het de authentificatiescherm van HTTP API met [!UICONTROL OAuth 2 Client Credentials] gebieden.](../../assets/catalog/http/http-api-authentication-oauth2-client-credentials.png)

>[!WARNING]
>
>Als u [!UICONTROL OAuth 2 Client Credentials] -verificatie gebruikt, kan [!UICONTROL Access Token URL] maximaal één queryparameter hebben. Het toevoegen van een [!UICONTROL Access Token URL] met meer vraagparameters kan tot problemen leiden wanneer het verbinden met uw eindpunt.

* **[!UICONTROL Access Token URL]**: De URL aan uw zijde die toegangstokens uitgeeft en, naar keuze, tokens vernieuwt.
* **[!UICONTROL Client ID]**: De `client ID` die uw systeem toewijst aan Adobe Experience Platform.
* **[!UICONTROL Client Secret]**: De `client secret` die uw systeem toewijst aan Adobe Experience Platform.
* **[!UICONTROL Client Credentials Type]**: Selecteer het type OAuth 2 Client Credentials gift die door uw eindpunt wordt gesteund:
   * **[!UICONTROL Body Form Encoded]**: In dit geval, zijn `client ID` en `client secret` inbegrepen *in het lichaam van het verzoek* dat naar uw bestemming wordt verzonden. Bij een voorbeeld, zie de [&#x200B; Ondersteunde authentificatietypen &#x200B;](#supported-authentication-types) sectie.
   * **[!UICONTROL Basic Authorization]**: In dit geval, zijn `client ID` en `client secret` inbegrepen *in een `Authorization` kopbal* na het worden base64 gecodeerd en verzonden naar uw bestemming. Bij een voorbeeld, zie de [&#x200B; Ondersteunde authentificatietypen &#x200B;](#supported-authentication-types) sectie.

### Doelgegevens invullen {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_headers"
>title="Kopteksten"
>abstract="Voer aangepaste kopteksten in die u in de doelaanroepen wilt opnemen, in de volgende notatie: `header1:value1,header2:value2,...headerN:valueN`"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_endpoint"
>title="HTTP-eindpunt"
>abstract="De URL van het HTTP-eindpunt waarnaar u de profielgegevens wilt verzenden. Dit zijn uw gegevens die eindpunt ontvangen en steunt mTLS indien gevormd."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmentnames"
>title="Segmentnamen opnemen"
>abstract="Schakel deze optie in als u wilt dat bij het exporteren van de gegevens de namen worden opgenomen van het publiek dat u exporteert. Bekijk de documentatie voor een voorbeeld van de gegevensuitvoer met deze optie geselecteerd."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmenttimestamps"
>title="Tijdstempels segment opnemen"
>abstract="Schakel deze optie in als u wilt dat bij het exporteren van de gegevens de UNIX-tijdstempel wordt opgenomen wanneer het publiek is gemaakt en bijgewerkt, en ook de UNIX-tijdstempel wanneer het publiek voor activering aan de bestemming is toegewezen. Bekijk de documentatie voor een voorbeeld van de gegevensuitvoer met deze optie geselecteerd."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_queryparameters"
>title="Zoekparameters"
>abstract="Naar keuze, kunt u vraagparameters aan het eindpunt URL van HTTP toevoegen. Maak de queryparameters die u op deze manier gebruikt op: `parameter1=value&parameter2=value` ."

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![&#x200B; het scherm van HTTP API bestemmingsdetails met voltooide gebieden.](../../assets/catalog/http/http-api-destination-details.png)

* **[!UICONTROL Name]**: voer een naam in waarmee u dit doel in de toekomst wilt herkennen.
* **[!UICONTROL Description]**: voer een beschrijving in die u helpt deze bestemming in de toekomst te identificeren.
* **[!UICONTROL Headers]**: ga om het even welke douanekopballen in die u in de bestemmingsvraag wilt worden omvat, die dit formaat volgen: `header1:value1,header2:value2,...headerN:valueN`.
* **[!UICONTROL HTTP Endpoint]**: De URL van het HTTP-eindpunt waarnaar u de profielgegevens wilt verzenden. Dit zijn uw gegevens die eindpunt ontvangen. Als u mTLS gebruikt, moet voor dit eindpunt TLS zijn uitgeschakeld en moet alleen mTLS zijn ingeschakeld.
* **[!UICONTROL Query parameters]**: U kunt optioneel queryparameters toevoegen aan de URL van het HTTP-eindpunt. Maak de queryparameters die u op deze manier gebruikt op: `parameter1=value&parameter2=value` .
* **[!UICONTROL Include Segment Names]**: in-/uitschakelen als u wilt dat bij het exporteren van de gegevens de namen worden opgenomen van het publiek dat u exporteert. **Nota**: De namen van het publiek zijn slechts inbegrepen voor publiek dat aan de bestemming in kaart wordt gebracht. Het veld `name` wordt niet opgenomen in toegewezen doelgroepen die worden weergegeven in het exportbestand. Voor een voorbeeld van een gegevens die met deze geselecteerde optie uitvoeren, verwijs naar de [&#x200B; Uitgevoerde gegevens &#x200B;](#exported-data) sectie verder hieronder.
* **[!UICONTROL Include Segment Timestamps]**: Schakel deze optie in als u wilt dat bij het exporteren van de gegevens de UNIX-tijdstempel wordt gebruikt wanneer het publiek is gemaakt en bijgewerkt, en ook de UNIX-tijdstempel wanneer het publiek voor activering is toegewezen aan het doel. Voor een voorbeeld van een gegevens die met deze geselecteerde optie uitvoeren, verwijs naar de [&#x200B; Uitgevoerde gegevens &#x200B;](#exported-data) sectie verder hieronder.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
>
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* [&#x200B; de beleidsevaluatie van de Goedkeuring &#x200B;](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) wordt momenteel niet gesteund in de uitvoer naar de bestemming van HTTP API. [Meer informatie](/help/destinations/ui/activate-streaming-profile-destinations.md#consent-policy-evaluation).

Zie [&#x200B; publieksgegevens aan het stromen van profieluitvoer bestemmingen &#x200B;](../../ui/activate-streaming-profile-destinations.md) voor instructies op het activeren van publiek aan deze bestemming activeren.

### Doelkenmerken {#attributes}

In de [[!UICONTROL Select attributes]](../../ui/activate-streaming-profile-destinations.md#select-attributes) stap, adviseert Adobe dat u een uniek herkenningsteken van uw [&#x200B; verenigingsschema &#x200B;](../../../profile/home.md#profile-fragments-and-union-schemas) selecteert. Selecteer de unieke id en andere XDM-velden die u naar het doel wilt exporteren.

## Exportgedrag profiel {#profile-export-behavior}

Experience Platform optimaliseert het gedrag voor het exporteren van profielen naar uw HTTP API-bestemming, zodat alleen gegevens naar uw API-eindpunt worden geëxporteerd wanneer relevante updates naar een profiel zijn opgetreden na de kwalificatie van het publiek of andere belangrijke gebeurtenissen. In de volgende situaties worden profielen naar uw doel geëxporteerd:

* De profielupdate werd bepaald door een wijziging in het publiekslidmaatschap voor ten minste een van de doelgroepen. Het profiel is bijvoorbeeld gekwalificeerd voor een van de soorten publiek die aan de bestemming zijn toegewezen of heeft een van de soorten publiek afgesloten die aan de bestemming zijn toegewezen.
* De profielupdate werd bepaald door een verandering in de [&#x200B; identiteitskaart &#x200B;](/help/xdm/field-groups/profile/identitymap.md). Een profiel dat bijvoorbeeld al was gekwalificeerd voor een van de soorten publiek dat aan de bestemming is toegewezen, heeft een nieuwe identiteit toegevoegd aan het kenmerk Naamplaatje.
* De profielupdate is bepaald door een wijziging in kenmerken voor ten minste een van de kenmerken die aan de bestemming zijn toegewezen. Een van de kenmerken die in de toewijzingsstap aan het doel is toegewezen, wordt bijvoorbeeld aan een profiel toegevoegd.

In alle hierboven beschreven gevallen worden alleen de profielen waarin relevante updates zijn opgetreden, naar uw bestemming geëxporteerd. Als een publiek dat is toegewezen aan de doelstroom bijvoorbeeld honderd leden heeft en vijf nieuwe profielen in aanmerking komen voor het publiek, wordt het exporteren naar uw bestemming stapsgewijs uitgevoerd en worden alleen de vijf nieuwe profielen opgenomen.

>[!NOTE]
>
>Alle toegewezen kenmerken worden geëxporteerd voor een profiel, ongeacht de locatie van de wijzigingen. In het voorbeeld hierboven worden alle toegewezen kenmerken voor deze vijf nieuwe profielen geëxporteerd, zelfs als de kenmerken zelf niet zijn gewijzigd.

### Wat bepaalt een gegevensexport en wat wordt opgenomen in de export? {#what-determines-export-what-is-included}

Met betrekking tot het gegeven dat voor een bepaald profiel wordt uitgevoerd, is het belangrijk om de twee verschillende concepten *te begrijpen wat een gegevensuitvoer aan uw bestemming van HTTP API* en *bepaalt welke gegevens in de uitvoer* inbegrepen zijn.

| Wat bepaalt de doelexport | Wat is inbegrepen in de doelexport |
|---------|----------|
| <ul><li>Toegewezen kenmerken en doelgroepen fungeren als actiepunt voor het exporteren van een bestemming. Dit betekent dat als de `segmentMembership` -status van een profiel verandert in `realized` of `exiting` of als toegewezen kenmerken worden bijgewerkt, een doelexport wordt uitgeschakeld.</li><li>Omdat identiteiten momenteel niet aan de bestemmingen van HTTP kunnen worden in kaart gebracht API, bepalen de veranderingen in om het even welke identiteit op een bepaald profiel ook bestemmingsuitvoer.</li><li>Een wijziging voor een kenmerk wordt gedefinieerd als een update voor het kenmerk, ongeacht of het dezelfde waarde heeft of niet. Dit houdt in dat een overschrijven van een kenmerk als een wijziging wordt beschouwd, zelfs als de waarde zelf niet is gewijzigd.</li></ul> | <ul><li>Het `segmentMembership` -object bevat het publiek dat is toegewezen in de activeringsgegevensstroom, waarvoor de status van het profiel is gewijzigd na een afsluitgebeurtenis voor kwalificatie of publiek. Merk op dat andere niet in kaart gebrachte publiek waarvoor het profiel gekwalificeerd deel van de bestemmingsuitvoer kan zijn, als deze doelgroepen tot het zelfde [&#x200B; fusiebeleid &#x200B;](/help/profile/merge-policies/overview.md) behoren zoals het publiek in kaart gebracht in activeringsdataflow. <br> **Belangrijk**: Wanneer de **[!UICONTROL Include Segment Names]** optie wordt toegelaten, zijn de segmentnamen slechts inbegrepen voor publiek dat aan de bestemming in kaart wordt gebracht. Niet-toegewezen doelgroepen die worden weergegeven in het exportbestand, bevatten het veld `name` niet, zelfs niet als de optie is ingeschakeld. </li><li>Alle identiteiten in het `identityMap` -object worden ook opgenomen (Experience Platform ondersteunt momenteel geen identiteitstoewijzing in de HTTP API-bestemming).</li><li>Alleen de toegewezen kenmerken worden opgenomen in de doelexport.</li></ul> |

{style="table-layout:fixed"}

Bijvoorbeeld, overweeg dit dataflow aan een bestemming van HTTP waar drie publiek in dataflow wordt geselecteerd, en vier attributen worden in kaart gebracht aan de bestemming.

![&#x200B; een voorbeeld van een HTTP API bestemmingsdataflow.](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Een profieluitvoer naar de bestemming wordt teweeggebracht wanneer een profiel voor kwalificeert of één van *drie in kaart gebrachte publiek* weggaat. In de gegevensuitvoer, kan het `segmentMembership` voorwerp (zie [&#x200B; Geëxporteerde Gegevens &#x200B;](#exported-data) hieronder) ook unmapped publiek omvatten, als dat profiel een lid van hen is en zij het zelfde fusiebeleid delen zoals het publiek dat de uitvoer teweegbracht. Bijvoorbeeld, als een profiel voor de **Klant met het 1&rbrace; publiek van de Auto&#39;s DeLorean kwalificeert &lbrace;maar ook een lid van de** Gecontroleerde &quot;Terug naar de Toekomstige&quot;**film en** de fictiefondsen van de Wetenschap **publiek is, verschijnen die twee publiek ook in** voorwerp-op voorwaarde zij het zelfde fusiebeleid met de `segmentMembership` Klant met de Cars van DeLorean &lbrace;8 delen **publiek.**

Vanuit het oogpunt van profielkenmerken bepalen wijzigingen in de vier bovenstaande kenmerken de doelexport en zijn alle vier toegewezen kenmerken in het profiel aanwezig in de gegevensexport.

## Back-up van historische gegevens {#historical-data-backfill}

Wanneer u een nieuw publiek aan een bestaande bestemming toevoegt, of wanneer u een nieuw doel creeert en een publiek in kaart brengt aan het, exporteert Experience Platform historische publiekskwalificatiegegevens naar de bestemming. Profielen die voor het publiek *kwalificeerden alvorens* het publiek aan de bestemming werd toegevoegd worden uitgevoerd naar de bestemming binnen ongeveer één uur.

## Geëxporteerde gegevens {#exported-data}

Uw geëxporteerde Experience Platform-gegevens worden in JSON-indeling in uw HTTP-bestemming geplaatst. De onderstaande exportbewerking bevat bijvoorbeeld een profiel dat is gekwalificeerd voor een bepaald publiek, lid is van een ander publiek en een ander publiek verlaat. Het exporteren bevat ook de voornaam, achternaam, geboortedatum en het persoonlijke e-mailadres van het profielkenmerk. De identiteiten voor dit profiel zijn ECID en e-mail.

```json
{
  "person": {
    "birthDate": "YYYY-MM-DD",
    "name": {
      "firstName": "John",
      "lastName": "Doe"
    }
  },
  "personalEmail": {
    "address": "john.doe@acme.com"
  },
  "segmentMembership": {
   "ups":{
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93":{
         "lastQualificationTime":"2022-01-11T21:24:39Z",
         "status":"exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae":{
         "lastQualificationTime":"2022-01-02T23:37:33Z",
         "status":"realized"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"realized"
      },
      "5114d758-ce71-43ba-b53e-e2a91d67b67f":{
         "lastQualificationTime":"2022-01-11T23:37:33Z",
         "status":"realized"
      }
   }
},
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

Hieronder vindt u meer voorbeelden van geëxporteerde gegevens, afhankelijk van de UI-instellingen die u hebt geselecteerd in de doelstroom voor verbinden voor de opties **[!UICONTROL Include Segment Names]** en **[!UICONTROL Include Segment Timestamps]** :

+++ In het onderstaande voorbeeld voor het exporteren van gegevens worden publieksnamen opgenomen in de sectie `segmentMembership`

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
            "name": "First name equals John"
          },
          "354e086f-2e11-49a2-9e39-e5d9a76be683": {
            "lastQualificationTime": "2020-04-15T02:41:50+0000",
            "status": "realized"
          }
        }
      }
```

>[!NOTE]
>
>In dit voorbeeld wordt het eerste publiek (`5b998cb9-9488-4ec3-8d95-fa8338ced490`) toegewezen aan het doel en bevat het veld `name` . Het tweede publiek (`354e086f-2e11-49a2-9e39-e5d9a76be683`) wordt niet toegewezen aan het doel en neemt het `name` veld niet op, ook al is de optie **[!UICONTROL Include Segment Names]** ingeschakeld.

+++

+++ Het onderstaande voorbeeld voor het exporteren van gegevens bevat tijdstempels voor het publiek in de sectie `segmentMembership`

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000
          }
        }
      }
```

+++

## Beperkingen en beleid opnieuw proberen {#limits-retry-policy}

95 percent van de tijd, probeert Experience Platform om een productietolatie van minder dan 10 minuten voor met succes verzonden berichten met een tarief van minder dan 10.000 verzoeken per seconde voor elke dataflow aan een bestemming van HTTP aan te bieden.

Wanneer aanvragen naar de HTTP API-bestemming mislukken, worden deze twee keer opgeslagen en opnieuw uitgevoerd.

## Problemen oplossen {#troubleshooting}

Om betrouwbare gegevenslevering te verzekeren en onderbreking kwesties te vermijden, zorg ervoor dat uw eindpunt van HTTP binnen 2 seconden aan Experience Platform verzoeken, zoals gespecificeerd in de [&#x200B; eerste vereisten &#x200B;](#prerequisites) sectie antwoordt. Reacties die langer duren, resulteren in time-outfouten.

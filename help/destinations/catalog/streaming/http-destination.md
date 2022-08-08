---
title: HTTP API-verbinding
keywords: streaming;
description: Gebruik de HTTP API bestemming in Adobe Experience Platform om profielgegevens naar derdeeindpunt van HTTP te verzenden om uw eigen analyses in werking te stellen of andere verrichtingen uit te voeren u op profielgegevens kunt nodig hebben die uit Experience Platform worden uitgevoerd.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 75399d2fbe111a296479f8d3404d43c6ba0d50b5
workflow-type: tm+mt
source-wordcount: '2295'
ht-degree: 0%

---

# HTTP API-verbinding

## Overzicht {#overview}

>[!IMPORTANT]
>
> Deze bestemming is alleen beschikbaar voor [Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) klanten.

De HTTP API-bestemming is een [!DNL Adobe Experience Platform] streamingbestemming waarmee u profielgegevens naar externe HTTP-eindpunten kunt verzenden.

Als u profielgegevens naar HTTP-eindpunten wilt verzenden, moet u eerst [verbinden met de bestemming](#connect-destination) in [!DNL Adobe Experience Platform].

## Gebruiksscenario’s {#use-cases}

Met de HTTP API-bestemming kunt u XDM-profielgegevens en publiekssegmenten exporteren naar algemene HTTP-eindpunten. Daar kunt u uw eigen analyses uitvoeren of andere bewerkingen uitvoeren die u nodig hebt voor profielgegevens die uit het Experience Platform zijn geëxporteerd.

De eindpunten van HTTP kunnen of de systemen van klanten of derdeoplossingen zijn.

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals gekozen in het koppelingsscherm van het dialoogvenster [doelactiveringsworkflow](../../ui/activate-segment-streaming-destinations.md#mapping). |
| Uitvoerfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Vereisten {#prerequisites}

Als u de HTTP API-bestemming wilt gebruiken om gegevens uit Experience Platform te exporteren, moet u aan de volgende voorwaarden voldoen:

* U moet een eindpunt van HTTP hebben dat REST API steunt.
* Uw eindpunt van HTTP moet het het profielschema van het Experience Platform steunen. Transformatie naar een extern payload-schema wordt niet ondersteund in de HTTP API-bestemming. Zie de [geëxporteerde gegevens](#exported-data) voor een voorbeeld van het uitvoerschema van het Experience Platform.
* Uw eindpunt van HTTP moet kopballen steunen.

>[!TIP]
>
> U kunt ook [Adobe Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) aan opstelling een integratie en verzendt de profielgegevens van het Experience Platform naar een eindpunt van HTTP.

## IP adres lijst van gewenste personen {#ip-address-allowlist}

Om klanten&#39; veiligheid en nalevingsvereisten te ontmoeten, verstrekt het Experience Platform een lijst van statische IPs die u voor de bestemming van HTTP kunt lijsten van gewenste personen API. Zie [IP adres lijst van gewenste personen voor het stromen bestemmingen](/help/destinations/catalog/streaming/ip-address-allow-list.md) voor de volledige lijst van IPs aan lijst van gewenste personen.

## Ondersteunde verificatietypen {#supported-authentication-types}

De HTTP API bestemming steunt verscheidene authentificatietypen aan uw eindpunt van HTTP:

* HTTP-eindpunt zonder verificatie;
* Toekenning aan toonder;
* [OAuth 2.0-clientreferenties](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) verificatie met het lichaamsformulier, met [!DNL client ID], [!DNL client secret] en [!DNL grant type] in de hoofdtekst van de HTTP-aanvraag, zoals in het onderstaande voorbeeld wordt getoond.

```shell
curl --location --request POST '<YOUR_API_ENDPOINT>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>'
```

* [OAuth 2.0-clientreferenties](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) met basisautorisatie, met een autorisatiekop die URL-gecodeerd bevat [!DNL client ID] en [!DNL client secret].

```shell
curl --location --request POST 'https://some-api.com/token' \
--header 'Authorization: Basic base64(clientId:clientSecret)' \
--header 'Content-type: application/x-www-form-urlencoded; charset=UTF-8' \
--data-urlencode 'grant_type=client_credentials'
```

* [OAuth 2.0-wachtwoordgift](https://www.oauth.com/oauth2-servers/access-tokens/password-grant/).

## Verbinden met de bestemming {#connect-destination}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). Wanneer u verbinding maakt met dit doel, moet u de volgende informatie opgeven:

### Verificatiegegevens {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_clientcredentialstype"
>title="Type clientgegevens"
>abstract="Selecteren **Bodyformulier gecodeerd** de client-id en het clientgeheim in de hoofdtekst van de aanvraag of **Basisautorisatie** om client-id en clientgeheim op te nemen in een machtigingheader. Voorbeelden weergeven in de documentatie."

#### Tokenverificatie {#bearer-token-authentication}

Als u **[!UICONTROL Bearer token]** autorisatietype voor verbinding met het HTTP-eindpunt, voer de onderstaande velden in en selecteer **[!UICONTROL Connect to destination]**:

![Afbeelding van het UI-scherm waarin u verbinding kunt maken met de HTTP API-bestemming met behulp van toventokenverificatie](../../assets/catalog/http/http-api-authentication-bearer.png)

* **[!UICONTROL Bearer token]**: neem het dragertoken in om op uw HTTP-locatie te verifiëren.

#### Geen verificatie {#no-authentication}

Als u **[!UICONTROL None]** authentificatietype om met uw eindpunt van HTTP te verbinden:

![Afbeelding van het UI-scherm waar u verbinding kunt maken met de HTTP API-bestemming, zonder verificatie](../../assets/catalog/http/http-api-authentication-none.png)

Wanneer u deze verificatie opent, hoeft u alleen **[!UICONTROL Connect to destination]** en de verbinding aan uw eindpunt wordt gevestigd.

#### OAuth 2-wachtwoordverificatie {#oauth-2-password-authentication}

Als u **[!UICONTROL OAuth 2 Password]** autorisatietype voor verbinding met het HTTP-eindpunt, voer de onderstaande velden in en selecteer **[!UICONTROL Connect to destination]**:

![Afbeelding van het UI-scherm waar u verbinding kunt maken met de HTTP API-bestemming met OAuth 2 met wachtwoordverificatie](../../assets/catalog/http/http-api-authentication-oauth2-password.png)

* **[!UICONTROL Access Token URL]**: De URL aan uw zijde die toegangstokens uitgeeft en, naar keuze, tokens vernieuwt.
* **[!UICONTROL Client ID]**: De [!DNL client ID] dat uw systeem aan Adobe Experience Platform toewijst.
* **[!UICONTROL Client Secret]**: De [!DNL client secret] dat uw systeem aan Adobe Experience Platform toewijst.
* **[!UICONTROL Username]**: De gebruikersnaam om tot uw eindpunt van HTTP toegang te hebben.
* **[!UICONTROL Password]**: Het wachtwoord om tot uw eindpunt van HTTP toegang te hebben.

#### OAuth 2 Client Credentials authentication {#oauth-2-client-credentials-authentication}

Als u **[!UICONTROL OAuth 2 Client Credentials]** autorisatietype voor verbinding met het HTTP-eindpunt, voer de onderstaande velden in en selecteer **[!UICONTROL Connect to destination]**:

![Afbeelding van het UI-scherm waar u verbinding kunt maken met de HTTP API-bestemming met OAuth 2 met verificatie van clientreferenties](../../assets/catalog/http/http-api-authentication-oauth2-client-credentials.png)

* **[!UICONTROL Access Token URL]**: De URL aan uw zijde die toegangstokens uitgeeft en, naar keuze, tokens vernieuwt.
* **[!UICONTROL Client ID]**: De [!DNL client ID] dat uw systeem aan Adobe Experience Platform toewijst.
* **[!UICONTROL Client Secret]**: De [!DNL client secret] dat uw systeem aan Adobe Experience Platform toewijst.
* **[!UICONTROL Client Credentials Type]**: Selecteer het type van OAuth2 verlenen van de Verantwoordelijkheid van de Cliënt die door uw eindpunt wordt gesteund:
   * **[!UICONTROL Body Form Encoded]**: In dit geval worden de [!DNL client ID] en [!DNL client secret] worden opgenomen *in de inhoud van het verzoek* verzonden naar uw bestemming. Zie voor een voorbeeld de [Ondersteunde verificatietypen](#supported-authentication-types) sectie.
   * **[!UICONTROL Basic Authorization]**: In dit geval worden de [!DNL client ID] en [!DNL client secret] worden opgenomen *in een `Authorization` header* nadat base64 gecodeerd en verzonden naar uw bestemming is. Zie voor een voorbeeld de [Ondersteunde verificatietypen](#supported-authentication-types) sectie.

### Doelgegevens invullen {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_headers"
>title="Kopteksten"
>abstract="Ga om het even welke douanekopballen in die u in de bestemmingsvraag, volgend dit formaat wilt worden omvat: `header1:value1,header2:value2,...headerN:valueN`"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_endpoint"
>title="HTTP-eindpunt"
>abstract="De URL van het HTTP-eindpunt waarnaar u de profielgegevens wilt verzenden."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmentnames"
>title="Segmentnamen opnemen"
>abstract="Schakel deze optie in als u wilt dat bij het exporteren van de gegevens de namen van de segmenten worden opgenomen die u exporteert. Bekijk de documentatie voor een voorbeeld van de gegevensuitvoer met deze optie geselecteerd."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmenttimestamps"
>title="Tijdstempels segment opnemen"
>abstract="Schakel deze optie in als u wilt dat de gegevensexport de UNIX-tijdstempel bevat wanneer de segmenten zijn gemaakt en bijgewerkt, evenals de UNIX-tijdstempel wanneer de segmenten voor activering aan de bestemming zijn toegewezen. Bekijk de documentatie voor een voorbeeld van de gegevensuitvoer met deze optie geselecteerd."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_queryparameters"
>title="Zoekparameters"
>abstract="Naar keuze, kunt u vraagparameters aan het eindpunt URL van HTTP toevoegen. Maak de vraagparameters op u als volgt gebruikt: `parameter1=value&parameter2=value`."

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![Afbeelding van het UI-scherm met voltooide velden voor de HTTP-doeldetails](../../assets/catalog/http/http-api-destination-details.png)

* **[!UICONTROL Name]**: Voer een naam in waarmee u deze bestemming in de toekomst wilt herkennen.
* **[!UICONTROL Description]**: Voer een beschrijving in die u helpt deze bestemming in de toekomst te identificeren.
* **[!UICONTROL Headers]**: Ga om het even welke douanekopballen in die u in de bestemmingsvraag, volgend dit formaat wilt worden omvat: `header1:value1,header2:value2,...headerN:valueN`.
* **[!UICONTROL HTTP Endpoint]**: De URL van het HTTP-eindpunt waarnaar u de profielgegevens wilt verzenden.
* **[!UICONTROL Query parameters]**: Naar keuze, kunt u vraagparameters aan het eindpunt URL van HTTP toevoegen. Maak de vraagparameters op u als volgt gebruikt: `parameter1=value&parameter2=value`.
* **[!UICONTROL Include Segment Names]**: Schakel deze optie in als u wilt dat bij het exporteren van de gegevens de namen van de segmenten worden opgenomen die u exporteert. Voor een voorbeeld van een gegevensexport waarbij deze optie is geselecteerd, raadpleegt u de [Geëxporteerde gegevens](#exported-data) hieronder.
* **[!UICONTROL Include Segment Timestamps]**: Schakel deze optie in als u wilt dat de gegevensexport de UNIX-tijdstempel bevat wanneer de segmenten zijn gemaakt en bijgewerkt, evenals de UNIX-tijdstempel wanneer de segmenten voor activering aan de bestemming zijn toegewezen. Voor een voorbeeld van een gegevensexport waarbij deze optie is geselecteerd, raadpleegt u de [Geëxporteerde gegevens](#exported-data) hieronder.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over waarschuwingen raadpleegt u de handleiding over [het abonneren aan bestemmingen alarm gebruikend UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Zie [De publieksgegevens van de activering aan het stromen profiel de uitvoerbestemmingen](../../ui/activate-streaming-profile-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

### Doelkenmerken {#attributes}

In de [[!UICONTROL Select attributes]](../../ui/activate-streaming-profile-destinations.md#select-attributes) stap, raadt Adobe u aan een unieke id te selecteren in uw [samenvoegingsschema](../../../profile/home.md#profile-fragments-and-union-schemas). Selecteer de unieke id en andere XDM-velden die u naar het doel wilt exporteren.

## Exportgedrag profiel {#profile-export-behavior}

Experience Platform optimaliseert het gedrag van de profieluitvoer naar uw bestemming van HTTP API, om gegevens naar uw API eindpunt slechts uit te voeren wanneer de relevante updates aan een profiel na segmentkwalificatie of andere significante gebeurtenissen zijn voorgekomen. In de volgende situaties worden profielen naar uw doel geëxporteerd:

* De profielupdate werd bepaald door een verandering in segmentlidmaatschap voor minstens één van de segmenten in kaart gebracht aan de bestemming. Het profiel is bijvoorbeeld gekwalificeerd voor een van de segmenten die aan het doel zijn toegewezen of heeft een van de segmenten afgesloten die aan het doel zijn toegewezen.
* De profielupdate is bepaald door een wijziging in het dialoogvenster [identiteitsbewijs](/help/xdm/field-groups/profile/identitymap.md). Een profiel dat bijvoorbeeld al was gekwalificeerd voor een van de segmenten die aan de bestemming zijn toegewezen, is toegevoegd aan een nieuwe identiteit in het kenmerk Naamplaatje.
* De profielupdate is bepaald door een wijziging in kenmerken voor ten minste een van de kenmerken die aan de bestemming zijn toegewezen. Een van de kenmerken die in de toewijzingsstap aan het doel is toegewezen, wordt bijvoorbeeld aan een profiel toegevoegd.

In alle hierboven beschreven gevallen worden alleen de profielen waarin relevante updates zijn opgetreden, naar uw bestemming geëxporteerd. Bijvoorbeeld, als een segment dat aan de bestemmingsstroom in kaart wordt gebracht honderd leden heeft, en vijf nieuwe profielen voor het segment kwalificeren, is de uitvoer naar uw bestemming incrementeel en omvat slechts de vijf nieuwe profielen.

Alle toegewezen kenmerken worden geëxporteerd voor een profiel, ongeacht de locatie van de wijzigingen. In het voorbeeld hierboven worden alle toegewezen kenmerken voor deze vijf nieuwe profielen geëxporteerd, zelfs als de kenmerken zelf niet zijn gewijzigd.

### Wat bepaalt een gegevensexport en wat wordt opgenomen in de export? {#what-determines-export-what-is-included}

Met betrekking tot de gegevens die voor een bepaald profiel worden geëxporteerd, is het belangrijk dat u de twee verschillende concepten van *wat een gegevensexport naar uw HTTP API-bestemming bepaalt* en *welke gegevens in de uitvoer worden opgenomen*.

| Wat bepaalt de doelexport | Wat is inbegrepen in de doelexport |
|---------|----------|
| <ul><li>Toegewezen kenmerken en segmenten fungeren als actiepunt voor het exporteren van een bestemming. Dit betekent dat als om het even welke in kaart gebrachte segmenten staten (van ongeldig aan gerealiseerd of van gerealiseerde/bestaande aan het weggaan) veranderen of om het even welke in kaart gebrachte attributen worden bijgewerkt, een bestemmingsuitvoer zou worden weggeduwd.</li><li>Omdat identiteiten momenteel niet aan de bestemmingen van HTTP kunnen worden in kaart gebracht API, bepalen de veranderingen in om het even welke identiteit op een bepaald profiel ook bestemmingsuitvoer.</li><li>Een wijziging voor een kenmerk wordt gedefinieerd als een update voor het kenmerk, ongeacht of het dezelfde waarde heeft of niet. Dit houdt in dat een overschrijven van een kenmerk als een wijziging wordt beschouwd, zelfs als de waarde zelf niet is gewijzigd.</li></ul> | <ul><li>Alle segmenten (met de nieuwste lidmaatschapsstatus), ongeacht of ze in de dataflow zijn toegewezen of niet, worden opgenomen in de `segmentMembership` object.</li><li>Alle identiteiten in de `identityMap` -object worden ook opgenomen (Experience Platform ondersteunt momenteel geen identiteitstoewijzing in de HTTP API-bestemming).</li><li>Alleen de toegewezen kenmerken worden opgenomen in de doelexport.</li></ul> |

{style=&quot;table-layout:fixed&quot;}

Bijvoorbeeld, overweeg dit dataflow aan een bestemming van HTTP waar drie segmenten in dataflow worden geselecteerd, en vier attributen worden in kaart gebracht aan de bestemming.

![HTTP API-doeldatabase](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Een profiel dat naar de bestemming wordt geëxporteerd, kan worden bepaald door een profiel dat in aanmerking komt voor of dat een van de *drie toegewezen segmenten*. Bij de gegevensexport moet u `segmentMembership` object (zie [Geëxporteerde gegevens](#exported-data) (zie hieronder), zouden andere niet in kaart gebrachte segmenten kunnen verschijnen, als dat bepaalde profiel een lid van hen is. Als een profiel in aanmerking komt voor de klant met het segment DeLorean Cars, maar ook lid is van de segmenten &quot;Terug naar de toekomst&quot; film en science fiction, dan zullen deze andere twee segmenten ook aanwezig zijn in de `segmentMembership` -object van de gegevensexport, ook al worden deze niet toegewezen in de gegevensstroom.

Vanuit het oogpunt van profielkenmerken bepalen wijzigingen in de vier bovenstaande kenmerken de doelexport en zijn alle vier toegewezen kenmerken in het profiel aanwezig in de gegevensexport.

## Back-up van historische gegevens {#historical-data-backfill}

Wanneer u een nieuw segment aan een bestaande bestemming toevoegt, of wanneer u een nieuwe bestemming en kaartsegmenten aan het creeert, voert het Experience Platform historische segmentkwalificatiegegevens naar de bestemming uit. Profielen die in aanmerking komen voor het segment *voor* het segment werd toegevoegd aan de bestemming wordt uitgevoerd naar de bestemming binnen ongeveer één uur.

## Geëxporteerde gegevens {#exported-data}

Uw geëxporteerde [!DNL Experience Platform] gegevensterreinen in uw [!DNL HTTP] doel in JSON-indeling. Bijvoorbeeld, bevat de hieronder uitvoer een profiel dat voor een bepaald segment heeft gekwalificeerd, een lid van andere twee segmenten is, en een ander segment verliet. Het exporteren bevat ook de voornaam, achternaam, geboortedatum en het persoonlijke e-mailadres van het profielkenmerk. De identiteiten voor dit profiel zijn ECID en e-mail.

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
         "status":"existing"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"existing"
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

Hieronder vindt u meer voorbeelden van geëxporteerde gegevens, afhankelijk van de UI-instellingen die u hebt geselecteerd in de doelstroom voor het verbinden van **[!UICONTROL Include Segment Names]** en **[!UICONTROL Include Segment Timestamps]** opties:

+++ In de onderstaande voorbeeldweergave voor gegevensexport worden segmentnamen opgenomen in `segmentMembership` sectie

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "existing",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
            "name": "First name equals John"
          }
        }
      }
```

+++

+++ In het onderstaande voorbeeld voor gegevensuitvoer zijn tijdstempels voor segmenten opgenomen in de `segmentMembership` sectie

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "existing",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
          }
        }
      }
```

+++

## Beperkingen en beleid opnieuw proberen {#limits-retry-policy}

In 95 percent van de tijd, probeert het Experience Platform om een productietolerantie van minder dan 10 minuten voor met succes verzonden berichten met een tarief van minder dan 10.000 verzoeken per seconde voor elke dataflow aan een bestemming van HTTP aan te bieden.

In het geval van ontbroken verzoeken aan uw bestemming van HTTP API, slaat het Experience Platform de ontbroken verzoeken op en probeert tweemaal om de verzoeken naar uw eindpunt te verzenden.
---
title: Geheimen in de Reactor-API
description: Leer de grondbeginselen van hoe te om geheimen in Reactor API voor gebruik in gebeurtenishet door:sturen te vormen.
exl-id: 0298c0cd-9fba-4b54-86db-5d2d8f9ade54
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1202'
ht-degree: 0%

---

# Geheimen in de Reactor-API

In de Reactor-API is een geheim een bron die een verificatiereferentie vertegenwoordigt. De geheimen worden gebruikt in gebeurtenis door:sturen om aan een ander systeem voor veilige gegevensuitwisseling voor authentiek te verklaren. Daarom kunnen geheimen alleen worden gemaakt binnen eigenschappen voor het doorsturen van gebeurtenissen (eigenschappen waarvan het kenmerk `platform` is ingesteld op `edge` ).

Het attribuut `type_of` bevat momenteel drie ondersteunde geheime typen:

| Geheim type | Beschrijving |
| --- | --- |
| `token` | Een enkele tekenreeks met tekens die een verificatietoken-waarde vertegenwoordigt die door beide systemen bekend en begrepen is. |
| `simple-http` | Bevat respectievelijk twee tekenreekskenmerken voor een gebruikersnaam en wachtwoord. |
| `oauth2-client_credentials` | Bevat verscheidene attributen om [&#x200B; OAuth &#x200B;](https://datatracker.ietf.org/doc/html/rfc6749) authentificatiespecic te steunen. De gebeurtenis die u door:sturen vraagt om de vereiste informatie, dan behandelt de vernieuwing van deze tokens voor u op een gespecificeerd interval. |

{style="table-layout:auto"}

Deze gids verstrekt een overzicht op hoog niveau van hoe te om geheimen voor gebruik in gebeurtenis te vormen die door:sturen. Voor gedetailleerde begeleiding op hoe te om geheimen in Reactor API, met inbegrip van voorbeeld JSON van de structuur van een geheim te beheren, verwijs naar de [&#x200B; geheimen eindpuntgids &#x200B;](../endpoints/secrets.md).

## Credentials

Elk geheim bevat een attribuut `credentials` dat zijn respectieve referentie waarden houdt. Wanneer [&#x200B; creërend een geheim in API &#x200B;](../endpoints/secrets.md#create), heeft elk type van geheim verschillende vereiste attributen zoals aangetoond in de hieronder secties:

* [&quot;token&quot;](#token)
* [` simple-http`](#simple-http)
* [&quot;oauth2-client_credentials&quot;](#oauth2-client_credentials)
* [&quot;oauth2-google&quot;](#oauth2-google)

### `token` {#token}

Bij geheimen met een `type_of` waarde van `token` is onder `credentials` slechts één kenmerk vereist:

| Referentiekenmerk | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `token` | String | Een geheim teken dat door het bestemmingssysteem wordt begrepen. |

{style="table-layout:auto"}

Het token wordt opgeslagen als een statische waarde en daarom worden de eigenschappen `expires_at` en `refresh_at` van het geheim ingesteld op `null` wanneer het geheim wordt gemaakt.

### `simple-http` {#simple-http}

Bij geheimen met een `type_of` waarde van `simple-http` zijn de volgende kenmerken vereist onder `credentials` :

| Referentiekenmerk | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `username` | String | Een gebruikersnaam. |
| `password` | String | Een wachtwoord. Deze waarde wordt niet opgenomen in de API-reactie. |

{style="table-layout:auto"}

Wanneer het geheim wordt gecreeerd, worden de twee attributen geruild met een codering BASE64 van `username:password`. Na de uitwisseling worden de eigenschappen `expires_at` en `refresh_at` van het geheim ingesteld op `null` .

### `oauth2-client_credentials` {#oauth2-client_credentials}

Bij geheimen met een `type_of` waarde van `oauth2-client_credentials` zijn de volgende kenmerken vereist onder `credentials` :

| Referentiekenmerk | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `client_id` | String | De client-id voor de OAuth-integratie. |
| `client_secret` | String | Het clientgeheim voor de OAuth-integratie. Deze waarde wordt niet opgenomen in de API-reactie. |
| `token_url` | String | De autorisatie-URL voor de OAuth-integratie. |
| `refresh_offset` | Geheel | *(Facultatief)* de waarde, in seconden, om te compenseren verfrist verrichting door. Als dit kenmerk wordt weggelaten tijdens het maken van het geheim, wordt de waarde standaard ingesteld op `14400` (vier uur). |
| `options` | Object | *(Facultatief)* specificeert extra opties voor de integratie OAuth:<ul><li>`scope`: Een koord dat [&#x200B; OAuth 2.0 werkingsgebied &#x200B;](https://oauth.net/2/scope/) voor de geloofsbrieven vertegenwoordigt.</li><li>`audience`: Een koord dat een [&#x200B; Auth0 toegangstoken &#x200B;](https://auth0.com/docs/protocols/protocol-oauth2) vertegenwoordigt.</li></ul> |

Wanneer een `oauth2-client_credentials` -geheim wordt gemaakt of bijgewerkt, worden de `client_id` en `client_secret` (en mogelijk `options` ) uitgewisseld in een verzoek van de POST aan de `token_url` , volgens de Client Credentials-stroom van het OAuth-protocol.

>[!NOTE]
>
>Verwacht wordt dat de responsinstantie van de vergunningdienst verenigbaar is met het OAuth-protocol.

Als de machtigingsservice reageert op `200 OK` en een JSON-responstekst, wordt de hoofdtekst geparseerd en wordt de `access_token` naar de randomgeving geduwd en wordt `expires_in` gebruikt om de `expires_at` en `refresh_at` -kenmerken voor het geheim te berekenen. Als er geen milieuvereniging op het geheim is, wordt `access_token` verworpen.

Een uitwisseling van geloofsbrieven wordt als succesvol beschouwd onder de volgende voorwaarden:

* `expires_in` is groter dan `28800` (8 uur).
* `refresh_offset` is kleiner dan de waarde van `expires_in` minus `14400` (vier uur). Als `expires_in` bijvoorbeeld `36000` (10 uur) is en `refresh_offset` `28800` (8 uur) is, wordt de uitwisseling als mislukt beschouwd omdat `28800` groter is dan `36000` - `14400` (`21600`).

Als de uitwisseling slaagt, wordt het statuskenmerk van het geheim ingesteld op `succeeded` en worden de waarden voor `expires_at` en `refresh_at` ingesteld:

* `expires_at` is de huidige UTC-tijd plus de waarde van `expires_in` .
* `refresh_at` is de huidige UTC-tijd plus de waarde van `expires_in` , minus de waarde van `refresh_offset` . Als `expires_in` bijvoorbeeld `43200` (twaalf uur) is en `refresh_offset` `14400` (vier uur), wordt de eigenschap `refresh_at` ingesteld op `28800` (acht uur) na de huidige UTC-tijd.

Als de uitwisseling om welke reden dan ook mislukt, wordt het kenmerk `status_details` in het `meta` -object bijgewerkt met relevante informatie.

#### Een `oauth2-client_credentials` -geheim vernieuwen

Als een `oauth2-client_credentials` -geheim is toegewezen aan een omgeving en de status `succeeded` (de gegevens zijn uitgewisseld) is, wordt automatisch een nieuwe uitwisseling uitgevoerd op `refresh_at` .

Als de uitwisseling is gelukt, wordt het kenmerk `refresh_status` in het object `meta` ingesteld op `succeeded` while `expires_at` , `refresh_at` en `activated_at` .

Als de uitwisseling ontbreekt, wordt de verrichting geprobeerd nog drie keer met de laatste poging niet meer dan twee uur alvorens het toegangstoken verloopt. Als alle pogingen mislukken, wordt het kenmerk `refresh_status_details` van het object `meta` bijgewerkt met relevante details.

### `oauth2-google` {#oauth2-google}

Bij geheimen met een `type_of` value of `oauth2-google` is het volgende kenmerk vereist onder `credentials` :

| Referentiekenmerk | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `scopes` | Array | Hiermee geeft u de Google-productbereiken voor verificatie weer. Het volgende bereik wordt ondersteund:<ul><li>[&#x200B; Advertentie Google &#x200B;](https://developers.google.com/google-ads/api/docs/oauth/overview): `https://www.googleapis.com/auth/adwords`</li><li>[&#x200B; Google Pub/Sub &#x200B;](https://cloud.google.com/pubsub/docs/reference/service_apis_overview): `https://www.googleapis.com/auth/pubsub`</li></ul> |

Nadat u het geheim `oauth2-google` hebt gemaakt, bevat de reactie een eigenschap `meta.authorization_url` . U moet deze URL kopiëren en in browser plakken om de Google-verificatiestroom te voltooien.

#### Een `oauth2-google` -geheim opnieuw autoriseren

De autorisatie-URL voor een `oauth2-google` -geheim verloopt één uur nadat het geheim is gemaakt (zoals aangegeven door `meta.authorization_url_expires_at` ). Na deze tijd, moet het geheim opnieuw worden geautoriseerd om het authentificatieproces te vernieuwen.

Verwijs naar de [&#x200B; geheimen eindpuntgids &#x200B;](../endpoints/secrets.md#reauthorize) voor details op hoe opnieuw goedkeurt een `oauth2-google` geheim door een verzoek van de PATCH aan Reactor API te doen.

## Omgevingsrelatie

Wanneer u een geheim creeert, moet u het [&#x200B; milieu &#x200B;](../endpoints/environments.md) specificeren waarin het zal bestaan. Geheimen worden onmiddellijk ingezet in de omgeving waarin ze zijn gemaakt.

Een geheim kan slechts aan één milieu worden geassocieerd. Zodra het verband tussen een geheim en een milieu wordt gevestigd, kan het geheim niet uit het milieu worden ontruimd, en het geheim kan niet met een verschillend milieu worden geassocieerd.

>[!NOTE]
>
>De enige uitzondering op deze regel is wanneer het milieu in kwestie wordt geschrapt. In dit geval wordt de relatie gewist en kan het geheim worden toegewezen aan een andere omgeving.

Nadat de geloofsbrieven van een geheim met succes zijn geruild, voor een geheim om met een milieu worden geassocieerd, wordt het uitwisselingsartefact (het symbolische koord voor `token`, het Base64 gecodeerde koord voor `simple-http`, of het toegangstoken voor `oauth2-client_credentials`) veilig bewaard op het milieu.

Nadat het uitwisselingsartefact met succes op het milieu wordt bewaard, wordt het `activated_at` attribuut van het geheim geplaatst aan de huidige tijd UTC, en kan nu worden van verwijzingen voorzien gebruikend een gegevenselement. Zie de [&#x200B; volgende sectie &#x200B;](#referencing-secrets) voor meer informatie bij het van verwijzingen voorzien geheimen.

## Verwijzen naar geheimen {#referencing-secrets}

Om naar een geheim te verwijzen, moet u een gegevenselement van type &quot;[!UICONTROL Secret]&quot;tot stand brengen (door de [[!UICONTROL Core] uitbreiding &#x200B;](../../extensions/client/core/overview.md) wordt verstrekt) op een gebeurtenis die bezit door:sturen. Wanneer het vormen van dit gegevenselement, wordt u ertoe aangezet om te wijzen op welk geheim aan gebruik voor elk milieu. U kunt dan regels tot stand brengen die naar een geheim gegevenselement, zoals binnen de kopbal voor een vraag van HTTP verwijzen.

![&#x200B; Geheime gegevenselement &#x200B;](../../images/api/guides/secrets/data-element.png)

>[!NOTE]
>
>Als u een geheim gegevenselement aan een bibliotheek wilt toevoegen, moet u ten minste één `succeeded` geheim hebben dat is gekoppeld aan de omgeving waarop de bibliotheek wordt gemaakt. Als een bibliotheek bijvoorbeeld een geheim gegevenselement heeft waarvoor geen `succeeded` geheim is geconfigureerd voor de [!UICONTROL Staging Secret] -sectie, leidt het maken van die bibliotheek in de testomgeving tot een fout.

Tijdens runtime wordt het element met geheime gegevens vervangen door het corresponderende geheime uitwisselingsartefact dat op de omgeving is opgeslagen.

## Volgende stappen

In deze handleiding werden de basisprincipes van het werken met geheimen in de Reactor-API besproken. Voor details op hoe te om geheimen te beheren gebruikend API vraag, zie de [&#x200B; geheimen eindpuntgids &#x200B;](../endpoints/secrets.md).

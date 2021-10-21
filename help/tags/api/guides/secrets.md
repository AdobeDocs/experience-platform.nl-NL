---
title: Geheimen in de Reactor-API
description: Leer de grondbeginselen van hoe te om geheimen in Reactor API voor gebruik in gebeurtenishet door:sturen te vormen.
source-git-commit: 6822199c3ecf4414893a8b8dfc650e3da40a6470
workflow-type: tm+mt
source-wordcount: '1111'
ht-degree: 1%

---

# Geheimen in de Reactor-API

In de Reactor-API is een geheim een bron die een verificatiereferentie vertegenwoordigt. De geheimen worden gebruikt in gebeurtenis door:sturen om aan een ander systeem voor veilige gegevensuitwisseling voor authentiek te verklaren. Daarom kunnen geheimen alleen worden gemaakt binnen eigenschappen voor het doorsturen van gebeurtenissen (waarvan `platform` kenmerk is ingesteld op `edge`).

Er zijn momenteel drie ondersteunde geheime typen die in het dialoogvenster `type_of` kenmerk:

| Geheim type | Beschrijving |
| --- | --- |
| `token` | Een enkele tekenreeks met tekens die een verificatietoken-waarde vertegenwoordigt die door beide systemen bekend en begrepen is. |
| `simple-http` | Bevat respectievelijk twee tekenreekskenmerken voor een gebruikersnaam en wachtwoord. |
| `oauth2` | Bevat diverse kenmerken die de [OAuth](https://datatracker.ietf.org/doc/html/rfc6749) verificatiespecificatie. De gebeurtenis die u door:sturen vraagt om de vereiste informatie, dan behandelt de vernieuwing van deze tokens voor u op een gespecificeerd interval. |

{style=&quot;table-layout:auto&quot;}

Deze gids verstrekt een overzicht op hoog niveau van hoe te om geheimen voor gebruik in gebeurtenis te vormen die door:sturen. Raadpleeg voor gedetailleerde informatie over het beheren van geheimen in de Reactor-API, zoals bijvoorbeeld JSON van de structuur van een geheim [punthulplijn voor geheimen](../endpoints/secrets.md).

## Credentials

Elk geheim bevat een `credentials` kenmerk dat de respectieve referentie-waarden bevat. Elk type geheim heeft verschillende vereiste attributen, zoals aangetoond in de hieronder secties.

### `token`

Geheimen met een `type_of` waarde van `token` slechts één enkel attribuut onder vereisen `credentials`:

| Referentiekenmerk | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `token` | Tekenreeks | Een geheim teken dat door het bestemmingssysteem wordt begrepen. |

{style=&quot;table-layout:auto&quot;}

Het token wordt opgeslagen als een statische waarde en daarom is het geheim `expires_at` en `refresh_at` eigenschappen zijn ingesteld op `null` wanneer het geheim wordt gecreeerd.

### `simple-http`

Geheimen met een `type_of` waarde van `simple-http` de volgende kenmerken vereisen onder `credentials`:

| Referentiekenmerk | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `username` | Tekenreeks | Een gebruikersnaam. |
| `password` | Tekenreeks | Een wachtwoord. Deze waarde wordt niet opgenomen in de API-reactie. |

{style=&quot;table-layout:auto&quot;}

Wanneer het geheim wordt gecreeerd, worden de twee attributen geruild met een codering BASE64 van `username:password`. Na de uitwisseling is het geheim `expires_at` en `refresh_at` eigenschappen zijn ingesteld op `null`.

### `oauth2`

>[!NOTE]
>
>Alleen de [Subsidietype Client Credentials](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) wordt ondersteund voor OAuth-geheimen.

Geheimen met een `type_of` waarde van `oauth2` de volgende kenmerken vereisen onder `credentials`:

| Referentiekenmerk | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `client_id` | Tekenreeks | De client-id voor de OAuth-integratie. |
| `client_secret` | Tekenreeks | Het clientgeheim voor de OAuth-integratie. Deze waarde wordt niet opgenomen in de API-reactie. |
| `authorization_url` | Tekenreeks | De autorisatie-URL voor de OAuth-integratie. |
| `refresh_offset` | Geheel | *(Optioneel)* De waarde in seconden waarmee de vernieuwingsbewerking moet worden verschoven. Als dit kenmerk wordt weggelaten bij het maken van het geheim, wordt de waarde ingesteld op `14400` (vier uur) standaard. |
| `options` | Object | *(Optioneel)* Geeft aanvullende opties voor de OAuth-integratie op:<ul><li>`scope`: Een tekenreeks die de [OAuth 2.0-bereik](https://oauth.net/2/scope/) voor de referenties.</li><li>`audience`: Een tekenreeks die een [Auth0-toegangstoken](https://auth0.com/docs/protocols/protocol-oauth2).</li></ul> |

Wanneer een `oauth2` geheim wordt gecreeerd of bijgewerkt, `client_id` en `client_secret` (en eventueel `options`) worden uitgewisseld in een verzoek van de POST aan de `authorization_url`, volgens de stroom van de Referenties van de Cliënt van het protocol OAuth.

>[!NOTE]
>
>Verwacht wordt dat de responsinstantie van de vergunningdienst verenigbaar is met het OAuth-protocol.

Als de vergunningsdienst met antwoordt `200 OK` en een JSON-responsorgaan, het lichaam wordt geparseerd en de `access_token` naar de randomgeving wordt geduwd en `expires_in` wordt gebruikt voor de berekening van de `expires_at` en `refresh_at` attributen voor het geheim. Als er geen milieuvereniging voor het geheim is, `access_token` wordt weggegooid.

Een uitwisseling van geloofsbrieven wordt als succesvol beschouwd onder de volgende voorwaarden:

* `expires_in` is groter dan `28800` (8 uur).
* `refresh_offset` is kleiner dan de waarde van `expires_in` minus `14400` (vier uur). Als `expires_in` is `36000` (tien uur) en de `refresh_offset` is `28800` (8 uur), wordt de uitwisseling als mislukt beschouwd omdat `28800` is groter dan `36000` - `14400` (`21600`).

Als de uitwisseling succesvol is, wordt de de statusattributen van het geheim geplaatst aan `succeeded` en waarden voor `expires_at` en `refresh_at` worden ingesteld:

* `expires_at` is de huidige UTC-tijd plus de waarde van `expires_in`.
* `refresh_at` is de huidige UTC-tijd plus de waarde van `expires_in`, minus de waarde van `refresh_offset`. Als `expires_in` is `43200` (twaalf uur) en de `refresh_offset` is `14400` (vier uur), de `refresh_at` eigenschap zou worden ingesteld op `28800` (8 uur) na de huidige UTC-tijd.

Als de uitwisseling om welke reden dan ook mislukt, `status_details` in het dialoogvenster `meta` objectupdates met relevante informatie.

### Een `oauth2` geheim

Als een `oauth2` geheim is toegewezen aan een milieu en zijn status is `succeeded` (de geloofsbrieven werden met succes geruild), een nieuwe uitwisseling wordt automatisch uitgevoerd op `refresh_at`.

Als de uitwisseling succesvol is, `refresh_status` in het dialoogvenster `meta` object is ingesteld op `succeeded` while `expires_at`, `refresh_at`, en `activated_at` dienovereenkomstig worden bijgewerkt.

Als de uitwisseling ontbreekt, wordt de verrichting geprobeerd nog drie keer met de laatste poging niet meer dan twee uur alvorens het toegangstoken verloopt. Als alle pogingen mislukken, `refresh_status_details` kenmerk van de `meta` objectupdates met relevante details.

## Omgevingsrelatie

Wanneer u een geheim maakt, moet u de opdracht [milieu](../endpoints/environments.md) waarin het zal bestaan. Geheimen worden onmiddellijk ingezet in de omgeving waarin ze zijn gemaakt.

Een geheim kan slechts aan één milieu worden geassocieerd. Zodra het verband tussen een geheim en een milieu wordt gevestigd, kan het geheim niet uit het milieu worden ontruimd, en het geheim kan niet met een verschillend milieu worden geassocieerd.

>[!NOTE]
>
>De enige uitzondering op deze regel is wanneer het milieu in kwestie wordt geschrapt. In dit geval wordt de relatie gewist en kan het geheim worden toegewezen aan een andere omgeving.

Nadat de geloofsbrieven van een geheim met succes zijn geruild, voor een geheim om met een milieu worden geassocieerd, het uitwisselingsartefact (het symbolische koord voor `token`, de Base64-gecodeerde tekenreeks voor `simple-http`of de toegangstoken voor `oauth2`) veilig in de omgeving wordt opgeslagen.

Nadat het uitwisselingsartefact met succes op het milieu wordt bewaard, `activated_at` wordt ingesteld op de huidige UTC-tijd en kan nu worden verwezen met behulp van een gegevenselement. Zie de [volgende sectie](#referencing-secrets) voor meer informatie over het verwijzen naar geheimen.

## Verwijzen naar geheimen {#referencing-secrets}

Als u naar een geheim wilt verwijzen, moet u een gegevenselement van het type &quot;[!UICONTROL Secret]&quot; (verstrekt door de [[!UICONTROL Core] extension](../../extensions/web/core/overview.md)) voor een gebeurtenis die bezit door:sturen. Wanneer het vormen van dit gegevenselement, wordt u ertoe aangezet om te wijzen op welk geheim aan gebruik voor elk milieu. U kunt dan regels tot stand brengen die naar een geheim gegevenselement, zoals binnen de kopbal voor een vraag van HTTP verwijzen.

![Geheim gegevenselement](../../images/api/guides/secrets/data-element.png)

>[!NOTE]
>
>Als u een geheim gegevenselement wilt toevoegen aan een bibliotheek, moet u ten minste één element hebben `succeeded` geheim verbonden aan het milieu waarop de bibliotheek wordt gebouwd. Als een bibliotheek bijvoorbeeld een geheim gegevenselement heeft dat geen `succeeded` geheim dat voor wordt gevormd [!UICONTROL Staging Secret] , resulteert het maken van die bibliotheek in de testomgeving in een fout.

Tijdens runtime wordt het element met geheime gegevens vervangen door het corresponderende geheime uitwisselingsartefact dat op de omgeving is opgeslagen.

## Volgende stappen

In deze handleiding werden de basisprincipes van het werken met geheimen in de Reactor-API besproken. Voor details over hoe te om geheimen te beheren gebruikend API vraag, zie [punthulplijn voor geheimen](../endpoints/secrets.md).

---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Entiteiten van beslissingsservice beheren met behulp van API's
topic: tutorial
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# Beslissingsobjecten en -regels beheren met behulp van API&#39;s

Dit document bevat een zelfstudie voor het werken met de bedrijfsentiteiten van de Decisioning Service met behulp van Adobe Experience Platform-API&#39;s.

De zelfstudie bestaat uit twee onderdelen:

- Algemene Repository-API&#39;s voor het beheren van bedrijfsobjecten worden in het [eerste deel](#managing-repository-entities-using-apis)geïntroduceerd. Deze API&#39;s zijn generiek in de zin dat ze mogelijkheden bieden voor het maken, lezen, bijwerken, verwijderen en zoeken van **elk** type bedrijfsobject. Het algemene API-model wordt beschreven en de relatie met de HAL (Hypertext Application Language) wordt uitgelegd.

- Door de kennis over de API&#39;s van de dataopslag toe te passen, richt het [tweede deel](#creating-and-managing-offer-decisioning-entities-using-apis) zich op de zakelijke entiteiten die worden beheerd via de API&#39;s van de dataopslag. Met de zelfde toegepaste APIs is het enige verschil tussen het beheren van twee verschillende entiteiten zoals een activiteit en een bedrijfsregel de verzoek en antwoordlading, plus de noodzakelijke kopbalwaarden die op het type van voorwerp wijzen dat wordt beheerd.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de services van het Experience Platform en de API-conventies. De opslagplaats van het Platform is de dienst die door verscheidene andere diensten van het Platform wordt gebruikt om bedrijfsvoorwerpen en diverse soorten meta-gegevens op te slaan. Het verstrekt een veilige en flexibele manier om die voorwerpen voor gebruik door verscheidene runtime diensten te beheren en te vragen. De beslissingsdienst is er een van. Lees de documentatie voor het volgende voordat u met deze zelfstudie begint:

- [XDM (Experience Data Model)](../../xdm/home.md): Het gestandaardiseerde kader waardoor Platform gegevens van de klantenervaring organiseert.
- [Beslissingsservice](./../home.md): Verklaart de concepten en de componenten die voor het Beslissen van de Ervaring in het algemeen en het besluit van de Aanbieding in het bijzonder worden gebruikt. Toont de strategieën die voor het kiezen van de beste optie worden gebruikt om tijdens de ervaring van een klant voor te stellen.
- [PQL (Profile Query Language)](../../segmentation/pql/overview.md): PQL is een krachtige taal voor het schrijven van expressies over XDM-instanties. PQL wordt gebruikt om besluitvormingsregels te bepalen.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan Platform APIs te maken.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Platform van de Ervaring te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan Platform APIs te maken, moet u de [authentificatieleerprogramma](../../tutorials/authentication.md)eerst voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen van het Experience Platform, zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in het ervaringsplatform zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Raadpleeg de documentatie bij het overzicht van de [sandbox voor meer informatie over sandboxen in Platform](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

## API-conventies voor opslagplaats

De beslissingsdienst wordt gecontroleerd door een aantal bedrijfsvoorwerpen die met elkaar verwant zijn. Alle bedrijfsvoorwerpen worden opgeslagen in de Bewaarplaats Van Bedrijfs Platform van Objecten. Een belangrijk kenmerk van deze opslagplaats is dat de API&#39;s orthogonaal zijn ten opzichte van het type bedrijfsobject. In plaats van POST, GET, PUT, PATCH of DELETE API te gebruiken die op het type van middel in zijn API eindpunt wijst, zijn er slechts 6 generische eindpunten maar zij aanvaarden of keren een parameter terug die op het type van de doorverwijs wijst wanneer dat nodig is. Het schema moet bij de repository worden geregistreerd, maar daarna is de repository bruikbaar voor een set open-end objecttypen.

Naast de bovenstaande koppen hebben de API&#39;s die u wilt maken, lezen, bijwerken, verwijderen en zoeken in opslagplaatsen de volgende conventies:

- De eindpuntwegen voor alle bewaarplaats APIs beginnen met `https://platform.adobe.io/data/core/xcore/`.

API Payload-indelingen worden onderhandeld met een `Accept` of een `Content-Type` header. Berichtenindelingen in de `Accept` of `Content-Type` koptekst worden aangegeven door een waarde `application/vnd.adobe.platform.xcore.{FORMAT}+json` waarbij {FORMAT} afhankelijk is van het specifieke API-verzoek of responsbericht in de opslagplaats, in de volgende tabel.

| FORMAT-variant | Beschrijving van de verzoek- of responsentiteit |
| --- | --- |
| <br>halfollowed by a parameter `schema={schemaId}` | Het bericht bevat een instantie die door een Schema JSON wordt beschreven dat door het schema van de formaatparameter wordt vermeld. De instantie wordt opgenomen in een JSON-eigenschap `_instance`. De andere eigenschappen op het hoogste niveau in de antwoordlading specificeren bewaarplaats informatie die voor alle middelen beschikbaar is.  De berichten die aan het formaat van HAL voldoen hebben een `_links` bezit dat verwijzingen in formaat HAL bevat. |
| `patch.hal` | Het bericht bevat een JSON PATCH-payload met de aanname dat de te patchen instantie HAL-compatibel is. Dat betekent dat niet alleen de eigen instantie-eigenschappen van de instantie maar ook de HAL-koppelingen van de instantie kunnen worden gerepareerd. Er zijn beperkingen waaraan eigenschappen door de client kunnen worden bijgewerkt. |
| `home.hal` | Het bericht bevat een representatie in JSON-indeling van een thuisdocumentbron voor de gegevensopslagruimte. |
| xdm.kwitantie | Het bericht bevat een reactie met JSON-indeling voor het maken, bijwerken (volledig en repareren) of verwijderen van een bewerking. Ontvangstbewijzen bevatten controlegegevens die op de herziening van de instantie in de vorm van een ETag wijzen. |

Het gebruik van elke **indelingsvariant** is afhankelijk van de specifieke API:

| API | Koptekst van inhoudstype | Koptekst accepteren |
| --- | --- | --- |
| Instance <br/>maken | `hal`<br/>met schemaparameter | `xdm.receipt` |
| InstanceUpdate-<br/>container bijwerken | `hal`<br/>met schemaparameter | `xdm.receipt` |
| Reparatie-instantie | `patch.hal` | `xdm.receipt` |
| InstanceDelete-<br/>container verwijderen | N.v.t. | `xdm.receipt` |
| Read<br/>InstanceRead Container | N.v.t. | `hal` met `schema` parameter |
| Containers List<br/>instancesList | N.v.t. | `hal` met speciale `schema` parameter `https://ns.adobe.com/experience/xcore/hal/results` |
| Zoekinstanties | N.v.t. | hal met speciale `schema` parameter `https://ns.adobe.com/experience/xcore/hal/results` |
| Repo-hoofdmap lezen | N.v.t. | `home.hal` |

Voor de container API&#39;s maken, bijwerken en lezen, heeft het indelingsparameterschema de waarde `https://ns.adobe.com/experience/xcore/container`.

`ContainerId` is de eerste padparameter voor de instantie-API&#39;s. Alle bedrijfsentiteiten bevinden zich in wat een container wordt genoemd. Een container is een isolatiemechanisme om verschillende zorgen van elkaar te onderscheiden. Het eerste padelement voor de instantie-API&#39;s van de repository die het algemene eindpunt volgen, is het `containerId`. De id wordt verkregen uit de lijst met containers die toegankelijk zijn voor de aanroeper. De API die bijvoorbeeld wordt gebruikt om een instantie in een container te maken, is `POST https://platform.adobe.io/data/core/xcore/{containerId}/instances`.

De lijst met toegankelijke containers wordt verkregen door het eindpunt &quot;/&quot; van de repository aan te roepen met een HTTP GET aanvraag met de standaardheaders.

## Toegang tot containers beheren

Een beheerder kan gelijkaardige principes, middelen, toegangstoestemmingen in profielen groeperen. Dit verlaagt de beheerlast en wordt ondersteund door de interface [van de](https://adminconsole.adobe.com)Adobe Admin Console. U moet een productbeheerder zijn voor het Adobe Experience Platform en de aanbiedingen in uw organisatie om profielen te maken en gebruikers aan hen toe te wijzen.

Het is voldoende om in één keer productprofielen te maken die overeenkomen met bepaalde machtigingen en vervolgens gebruikers aan die profielen toe te voegen. Profielen fungeren als groepen waaraan machtigingen zijn verleend en elke echte gebruiker of technische gebruiker in die groep neemt deze machtigingen over.

### Containers weergeven die toegankelijk zijn voor gebruikers en integratie

Wanneer de beheerder toegang heeft verleend tot containers voor gewone gebruikers of integratie, worden deze containers weergegeven in de zogenaamde &quot;thuislijst&quot; van de gegevensopslagruimte. De lijst kan voor verschillende gebruikers of integraties verschillend zijn aangezien het een ondergroep van alle containers toegankelijk voor de bezoeker is. De lijst van containers kan worden gefilterd door hun verband met productcontexten. De filterparameter wordt aangeroepen `product` en kan worden herhaald. Als er meer dan één productcontextfilter wordt gegeven, wordt de samenvoeging van de recipiënten die een verband hebben met een van de gegeven productcontextvarianten geretourneerd. Merk op dat één enkele container aan veelvoudige productcontexten kan worden geassocieerd.

De context voor de containers van de Dienst van het Beslissen van het Platform is momenteel `dma_offers`.

>[!NOTE] De context voor Platform beslissende Containers zal binnenkort veranderen in `acp`. Filteren is optioneel, maar filters alleen `dma_offers` vereisen bewerkingen bij toekomstige release. Om voor deze verandering voorbereidingen te treffen zouden de cliënten geen filters moeten gebruiken of beide productcontexten als filter toepassen.

**Verzoek**

```shell
curl -X GET {ENDPOINT_PATH}/?product=dma_offers&product=acp \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.home.hal+json' \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' 
```

**Antwoord**

```json
{ 
    "_embedded": { 
        "https://ns.adobe.com/experience/xcore/container": [ 
            { 
              "instanceId": "82d1f250-85b6-11e9-ac80-99ba4655b277", 
              "schemas": [ 
                "https://ns.adobe.com/experience/xcore/container;version=0.1" 
              ], 
              "productContexts": [ 
                "dma_offers" 
              ], 
              "repo:etag": 1, 
              "repo:createdDate": "2019-06-03T04:17:33.684Z", 
              "repo:lastModifiedDate": "2019-06-03T04:17:33.684Z", 
              "repo:createdBy": "CREATOR_ACCOUNT_ID", 
              "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
              "repo:createdByClientId": "CLIENT_ID_OR_API_KEY", 
              "repo:lastModifiedByClientId": "CLIENT_ID_OR_API_KEY", 
              "_instance": { 
                "repo:name": "My Organization's container", 
                "dataCenter": "VA7" 
              }, 
              "_links": { 
                "self": { 
                  "href": "/containers/82d1f250-85b6-11e9-ac80-99ba4655b277" 
                } 
              } 
            } 
        ] 
    }, 
    "_links": { 
        "self": { 
            "href": "/"  
        } 
    } 
}  
```

Maak een notitie van de `instanceId` items in de resultatenlijst. Deze wordt gebruikt als de `containerId` parameter in de API&#39;s voor het lezen en bewerken van gewone zakelijke objecten.

De lijst wordt reeds gefiltreerd voor de gebruikers per hun toegangsvoorrechten maar kan verder door een bezitsvraag worden gefiltreerd.

## Algemene API&#39;s voor het beheer van entiteiten

### Instanties maken

De API die een nieuwe instantie in de repository maakt, maakt gebruik van een `containerId` padparameter en identificeert het type instantie in de `Content-Type` header met de schemaparameter.

De instantie-eigenschappen worden gegeven in de payload die in de `_instance` eigenschap is opgenomen. De instantie-eigenschappen moeten geldig zijn ten opzichte van het JSON-schema met de opgegeven schema-id.

De eigenschap HAL `_links` moet aanwezig zijn, maar kan leeg zijn. Dit betekent dat er voor deze instantie geen aangepaste koppelingen zijn gedefinieerd.

**Verzoek**

```shell
curl -X POST {ENDPOINT_PATH}/{CONTAINER_ID}/instances \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' \ 
  -d '{ 
    "_instance": { 
        {JSON_PAYLOAD} 
    }, 
    "_links": { 
    } 
}' 
```

**Antwoord**

```json
{ 
  "instanceId": "3684ceb0-8744-11e9-a989-89f60b24f6cc", 
  "@id": "GENERATED_URI", 
  "repo:etag": 1, 
  "repo:createdDate": "2019-06-05T03:44:25.343Z", 
  "repo:lastModifiedDate": "2019-06-05T03:44:25.343Z", 
  "repo:createdBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:lastModifiedBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:createdByClientId": "YOUR_API_KEY", 
  "repo:lastModifiedByClientId": "YOUR_API_KEY" 
}
```

De reactie bevat instanceId van het object dat zojuist is gemaakt. Deze instanceId is onveranderlijk, altijd toegewezen door de bewaarplaats en globaal uniek. De waarde fungeert als een fysieke id.

Daarnaast wordt een universele resource-id (URI) geretourneerd in de `@id` eigenschap van de antwoordpayload als het schema een dergelijke eigenschap heeft. Elke instantie moet een eigenschap hebben die fungeert als de URI en de primaire sleutel van de instantie. Deze id wordt door andere instanties gebruikt om relaties met het nieuwe exemplaar te maken, ook tussen verschillende typen. In de huidige versie worden de URI&#39;s gegenereerd door de opslagplaats en opgenomen in de `@id` eigenschap. Toekomstige versies kunnen deze regel versoepelen en clients toestaan hun eigen URI-waarden te beheren en de eigenschap die deze bevat een naam te geven.

Deze URI&#39;s zijn geen URL&#39;s en bieden geen manier om de bron rechtstreeks op te halen. Om op dat aspect te wijzen, wordt URI vooraf bepaald met een schema van URI dat geen herwinningsprotocol specificeert. De URI&#39;s kunnen echter worden gebruikt om de instantie met een query op te zoeken.

De REST-reactie heeft een locatiekoptekst die een URL-component bevat die kan worden gebruikt om de instantie op te halen die zojuist is gemaakt. Deze component is een relatieve URI-referentie en moet worden toegepast op de basis-URI van de opslagplaats. De basis-URI wordt geretourneerd in de `Content-Base` header.

De `repo:etag` eigenschap geeft de revisie van de instantie aan. Deze waarde kan worden gebruikt in updatebewerkingen om consistentie af te dwingen. De HTTP-header `If-Match` kan worden gebruikt om een voorwaarde toe te voegen aan een PUT- of PATCH API-aanroep die ervoor zorgt dat er geen andere wijziging in de instantie is die per ongeluk kan worden overschreven. De `repo:etag` waarde wordt geretourneerd bij elke aanroep van create, read, update, delete en query. De waarde wordt gebruikt als waarde in de ` If-Match` kopbal, per [RFC7232 Sectie 3.1](https://tools.ietf.org/html/rfc7232#section-3.1).

De resterende eigenschappen geven aan met welke account en API-sleutel de instantie is gemaakt en voor het laatst is gewijzigd. Aangezien de instantie door deze vraag werd gecreeerd zijn de respectieve waarden die van het verzoek.

### Instantie zoeken op ID

Met de URL in de koptekst Locatie die bij de aanroep Maken wordt geretourneerd, kan een toepassing een instantie opzoeken.

**Verzoek**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

>[!NOTE] Hoewel `instanceId` deze parameter als padparameter wordt gegeven, mogen toepassingen het pad niet zelf samenstellen en in plaats daarvan koppelingen naar instanties in lijsten en zoekbewerkingen volgen. Zie de punten ‎ 6.4.4 en ‎ 6.4.6 voor meer informatie.

**Antwoord**

```json
{ 
  "instanceId": "ID_OF_THIS_INSTANCE", 
  "schemas": [ 
    "SCHEMA_ID_OF_INSTANCE" 
  ], 
  "repo:etag": 1, 
  "repo:createdDate": "2019-03-24T15:52:12.725Z", 
  "repo:lastModifiedDate": "2019-03-24T15:52:12.725Z", 
  "repo:createdBy": "CREATOR_ACCOUNT_ID", 
  "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
  "_instance": { 
    JSON_PROPERTIES_OF_THIS_INSTANCE 
  }, 
  "_links": { 
    "self": { 
      "name": "GENERATED_UNIQUE_LINK_NAME", 
      "href": "RELATIVE_URL_TO_INSTANCE" 
    } 
  } 
} 
```

De JSON-eigenschappen van de instantie worden opgenomen in de `_instance` eigenschap en de andere eigenschappen op hoofdniveau bevatten metagegevens over de instantie.

De bron bevat ook een array met JSON-schema-id&#39;s. Deze array geeft de JSON-schema&#39;s aan waarop deze instantie wordt gevalideerd.

Elke instantie bevat een HAL-koppeling van het relatietype zelf die overeenkomt met de geregistreerde IANA-relatie (zoals gedefinieerd door [RFC5988]).

**Testen op nieuwere revisies van een instantie**

De huidige `eTag` waarde van de instantie is teruggekeerd met de reactie, staat het cliënten toe om voorwaardelijke verrichtingen tegen de instantie uit te geven, of om het terugwinnen van de zelfde middelstaat te vermijden opnieuw of om het beschrijven van de waarden van een recentere revisie zonder de kennis van de cliënt te vermijden.

Met de opzoekAPI kan een client een `If-None-Match` headerparameter opgeven. Zie de definitie van deze standaardHTTP-parameter [RFC2616]. De waarde van de entiteitmarkering een cliënt specificeert is de waarde het met de recentste reactie, of van een update, lees, lijst of onderzoek API vraag ontving. De `etag` waarde moet dekkend zijn voor de client en worden gegeven als een tekenreeks, tussen aanhalingstekens.

**Verzoek**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}" \ 
  -H 'If-None-Match: "{LAST_RECEIVED_ETAG}" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

De API van de repository reageert met status 304 Niet gewijzigd wanneer de laatste revisie van de instantie die is met de gegeven tag.

### Instanties weergeven voor een schema - Sorteren en pagineren

Clients kunnen de instanties die ze maken, niet bijhouden en hebben daarom toegang tot deze instanties via hun fysieke instanceId. Het gebruik van de API voor het lezen van instanties vormt de uitzondering. Clients weten ook niet welke instanties andere clients hebben gemaakt.

Een typisch toegangspatroon zal zijn door de reeks van alle instanties te pagineren.

**Verzoek**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances?schema="{SCHEMA_ID}" \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**Antwoord**

De reactie hangt van het `{schemaId}` gespecificeerde af. Bijvoorbeeld voor &quot;https<span></span>://ns.adobe.com/experience/offer-management/offer-activity&amp;id=xcore:offer-activity:fa24f9e8fc15c73&quot; lijkt het antwoord op het volgende:

```json
{
"requestTime": "2019-06-28T06:54:05.606Z",
"_embedded": {
  "results": [],
  "total": 0,
  "count": 0
  },
  "_links": {
  "self": {
  "href": "/653da250-71b8-11e9-a3fe-9b1d0913f3ed/instances?schema=https://ns.adobe.com/experience/offer-management/offer-activity&id=xcore:offer-activity:fa24f9e8fc15c73",
"@type": "https://ns.adobe.com/experience/xcore/hal/results"
  }
  },
  "containerId": "653da250-71b8-11e9-a3fe-9b1d0913f3ed",
  "schemaNs": "https://ns.adobe.com/experience/offer-management/offer-activity;version=0.1"
}
```

>[!NOTE] Het resultaat bevat de instanties voor het opgegeven schema of de eerste pagina van deze lijst. Merk op, dat de instanties aan meer dan één schema kunnen voldoen en daarom in meer dan één lijst kunnen verschijnen.

De paginabronnen zijn van voorbijgaande aard en zijn alleen-lezen; ze kunnen niet worden bijgewerkt of verwijderd. Het het pagineren model verleent willekeurige toegang tot ondergroepen van een grote lijsten over een lange periode zonder enige per-cliëntstaat te handhaven.

Als u op deze manier een lijst met instanties per pagina wilt openen, moet u een stabiele sortering kunnen definiëren op de items die door die lijst met instanties worden opgesomd. Opmerking: &#39;stabiel&#39; betekent niet dat instanties op een vooraf bepaalde pagina worden weergegeven. Wanneer een paginavolgorde wordt gevormd door het sorteren van instanties volgens een eigenschap P en een client deze eigenschap P bijwerkt, kan een andere client deze instantie opnieuw bereiken op een andere pagina terwijl deze door de lijst pagineert. Met andere woorden, het model geeft de voorkeur aan het retourneren van meer actuele resultaten.

Wanneer de sorteervolgorde echter is gebaseerd op een eigenschap die niet kan worden gewijzigd, garandeert een &#39;stabiele&#39; sorteervolgorde dat alle instanties die aan het begin van de pagineringsbewerking bestonden, worden bereikt (tenzij ze zijn verwijderd op het moment dat de pagina wordt bereikt). Wanneer deze sorteervolgorde wordt toegepast op een eigenschap die monotoon toeneemt, worden ook instanties bereikt die worden gemaakt nadat de pagineringsbewerking is gestart.

Een client kan tips geven over de gewenste paginagrootte, maar het is volledig aan de opslagplaats om de pagina die deze retourneert, meer of minder exemplaren te geven. Om de stabiele orde te waarborgen, moet de dienst punten toevoegen of verwijderen uit de pagina zodat de waarde van het soortbezit over paginagrenzen verschillend is. Op deze manier bevat de volgende pagina geen items van de laatste pagina meer of blijven in het slechtste geval dezelfde items op elke pagina staan.

Het pagineren wordt gecontroleerd door de volgende parameters:

- **`orderBy`**: Bevat een door komma&#39;s gescheiden, geordende lijst met eigenschappen waarmee de instantielijst wordt gesorteerd. De eerste eigenschap wordt gebruikt voor primair sorteren, de tweede eigenschap voor het oplossen van bindingen bij primair sorteren, enzovoort. Wanneer een eigenschap is opgegeven met een unieke waarde per instantie, zijn koppelingen niet mogelijk en kan na elk item een pagina-einde optreden. De naam van een eigenschap kan vooraf worden voorzien van een instructie `+` om oplopende volgorde aan te geven of `-` om aflopende volgorde aan te geven door die eigenschap. Als de naam van de eigenschap niet vooraf is ingesteld, wordt het resultaat in oplopende volgorde gesorteerd. Als `orderBy` niet in het verzoek wordt gespecificeerd zal de bewaarplaats het fysieke instanceId bezit in plaats daarvan gebruiken.
- **`start`**: Clients gebruiken de startparameter om de pagina te definiëren die ze willen ophalen. De beginparameter bepaalt het begin van de gewenste pagina. De reactie bevat instanties die beginnen met instanties met een `orderBy` eigenschapswaarde die strikt groter is dan (voor oplopend) of strikt kleiner dan (voor aflopend) de opgegeven waarde. Wanneer de queryparameter niet wordt opgegeven, wordt standaard een instanceId-waarde gebruikt die sorteert vóór de eerste mogelijke instantie-id en daarom wordt deze waarde weggelaten uit de eerste pagina.
- **`limit`**: geeft een positief geheel getal aan als een tip over het maximumaantal items dat voor een bepaalde aanvraag moet worden geretourneerd. De daadwerkelijke reactiegrootte kan kleiner of groter zijn, zoals beperkt door de behoefte om betrouwbare verrichting van de beginparameter te verstrekken

### Filterlijsten

Het filteren van lijstresultaten is mogelijk en gebeurt onafhankelijk van het het pagineren mechanisme. Filters slaan eenvoudig instanties in de volgorde van de lijsten over of vragen expliciet alleen om instanties die aan een bepaalde voorwaarde voldoen, op te nemen. Een client kan verzoeken dat eigenschapsuitdrukking als filter wordt gebruikt of kan een lijst met URI&#39;s opgeven die als de waarden van de primaire sleutel van de instanties moeten worden gebruikt.

- **`property`**: Bevat een pad naar de eigenschapnaam gevolgd door een vergelijkingsoperator, gevolgd door een waarde. <br/>
De lijst met geretourneerde instanties bevat de instanties waarvoor de expressie true oplevert. Bijvoorbeeld, veronderstellend dat de instantie een nuttige laadeigenschap heeft `status` en de mogelijke waarden zijn `draft`, `approved`, `archived` en `deleted` `property=_instance.status==approved` dan keert de vraagparameter slechts instanties terug waarvoor de status wordt goedgekeurd. <br/>
<br/>
De eigenschap die met de opgegeven waarde moet worden vergeleken, wordt aangeduid als een pad. De afzonderlijke padcomponenten worden gescheiden door `.`, zoals: `_instance.xdm:prop1.xdm:prop1_1.xdm:prop1_1_1`<br/>

Voor eigenschappen met tekenreeks, numerieke waarden of datum/tijd-waarden zijn de toegestane operatoren: `==`, `!=`, `<`, `<=`, `>` en `>=`. Voor eigenschappen met een tekenreekswaarde `~` kan bovendien een operator worden gebruikt. De `~` operator komt overeen met de opgegeven eigenschap volgens een reguliere expressie. De tekenreekswaarde van de eigenschap moet overeenkomen met de **gehele** expressie, anders worden de entiteiten in de gefilterde resultaten opgenomen. Wanneer u bijvoorbeeld ergens in de eigenschapswaarde naar de tekenreeks `cars` zoekt, moet de reguliere expressie zijn `.*cars.*`ingesteld. Zonder de regelafstand of nadering komen `.*`alleen entiteiten overeen met een eigenschapswaarde die respectievelijk begint of eindigt met `cars`. Voor de `~` operator is de vergelijking van lettertekens niet hoofdlettergevoelig. Voor alle andere operatoren is de vergelijking hoofdlettergevoelig.<br/><br/>
Niet alleen instantie payload-eigenschappen kunnen in filterexpressies worden gebruikt. Omhulseleigenschappen worden op dezelfde manier vergeleken, bijvoorbeeld `property=repo:lastModifiedDate>=2019-02-23T16:30:00.000Z`. <br/>
<br/>De `property` queryparameter kan worden herhaald, zodat er meerdere filtervoorwaarden worden toegepast, bijvoorbeeld om alle instanties te retourneren die het laatst na een bepaalde datum en voor een bepaalde datum zijn gewijzigd. Waarden in die expressies moeten URL-gecodeerd zijn. Als geen uitdrukking wordt gegeven en de naam van het bezit eenvoudig vermeld is zijn de punten die kwalificeren die een bezit met de bepaalde naam hebben.<br/>
<br/>

- **`id`**: Soms moet een lijst worden gefilterd door URI van de instanties. De `property` vraagparameter kan worden gebruikt om één instantie uit te filteren, maar om meer dan één geval te verkrijgen, kan een lijst van URIs aan het verzoek worden gegeven. De `id` `id={URI_1}&id={URI_2},…` parameter wordt herhaald en elk voorval geeft één URI-waarde op. De URI-waarden moeten URL-gecodeerd zijn.

Gepagineerde resultaten worden geretourneerd als een speciaal mime-type `application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results"`.

**Verzoek**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances?schema="{SCHEMA_ID}"&orderby${ORDER_BY_PROPERTY_PATH}&property={TIMESTAMP_PROPERTY_PATH}>=2019-02-19T03:19:03.627Z&property${TIMESTAMP_PROPERTY_PATH}<=2019-06-19T03:19:03.627Z \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**Antwoord**

```json
{ 
  "requestTime": "2019-06-10T22:12:13.642Z", 
  "_embedded": { 
    "results": [ 
      { 
        "instanceId": "ID_OF_THIS_INSTANCE", 
        "schemas": [ 
          "SCHEMA_ID_OF_INSTANCE" 
        ], 
        "repo:etag": 1, 
        "repo:createdDate": "2019-04-19T03:19:03.627Z", 
        "repo:lastModifiedDate": "2019-04-19T03:19:03.627Z", 
        "repo:createdBy": "CREATOR_ACCOUNT_ID", 
        "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
        "_instance": { 
          JSON_PROPERTIES_OF_THIS_INSTANCE 
        }, 
        "_links": { 
          "self": { 
            "name": "GENERATED_UNIQUE_LINK_NAME", 
            "href": "RELATIVE_URL_TO_INSTANCE" 
          } 
        } 
      }, 
      { 
        "instanceId": "ID_OF_THIS_INSTANCE", 
        "schemas": [ 
          "SCHEMA_ID_OF_INSTANCE" 
        ], 
        "repo:etag": 1, 
        "repo:createdDate": "2019-04-19T20:30:31.361Z", 
        "repo:lastModifiedDate": "2019-04-19T20:30:31.361Z", 
        "repo:createdBy": "CREATOR_ACCOUNT_ID", 
        "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
        "_instance": { 
          JSON_PROPERTIES_OF_THIS_INSTANCE 
        }, 

        "_links": { 
          "self": { 
            "name": "GENERATED_UNIQUE_LINK_NAME", 
            "href": "RELATIVE_URL_TO_INSTANCE" 
          } 
        } 
      } 
    ], 
    "total": 2, 
    "count": 2 
  }, 
  "_links": { 
    "self": { 
      "href": "RELATIVE_URL_TO_THIS_RESULT" 
    } 
  }, 
  "containerId": "CONTAINER_ID_OF_THIS_LIST", 
  "schemaNs": "SCHEMA_ID_OF_INSTANCE_LIST" 
} 
```

De reactie bevat de lijst van resultaatpunten binnen de JSON bezitsresultaten naast twee eigenschappen die op het aantal resultaten op deze pagina en het totale aantal punten in de gefiltreerde lijst wijzen die met de pagina beginnen die enkel is teruggekeerd.

### Volledige tekstonderzoek en gestructureerde vragen

In gevallen waarin clients complexere filtervoorwaarden en zoekinstanties willen bieden op basis van termen in tekenreekseigenschappen, biedt de gegevensopslagruimte een krachtigere API voor zoeken.

**Verzoek**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/queries/core/search?schema="{SCHEMA_ID}"&… \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

<!-- TODO: needs example response -->

Naast het pagineren en het filtreren parameters van lijst APIs staat dit API cliënten toe om volledige tekst en Booleaanse vraagparameters toe te voegen.

Het zoeken naar volledige tekst wordt bepaald door de volgende parameters:

- **`q`**: Bevat een niet-geordende lijst met termen die door spaties worden gescheiden en die worden genormaliseerd voordat ze worden vergeleken met tekenreekseigenschappen van de instanties. Tekenreekseigenschappen worden geanalyseerd op termen en deze termen worden eveneens genormaliseerd. De zoekquery probeert een of meer van de termen aan te passen die in de `q` parameter zijn opgegeven. De tekens +, -, =, &amp;&amp;,||, >, &lt;,!, (,), {, }, [,], ^, &quot;, ~, *, ?, :, / hebben een speciale betekenis voor het bepalen van de woordgrenzen binnen de queryreeks en moeten worden beschermd met een backslash wanneer deze wordt weergegeven in een token dat moet overeenkomen met het teken. De querytekenreeks kan worden omgeven door dubbele aanhalingstekens voor exacte tekenreeksovereenkomst en om speciale tekens te kunnen omzeilen.
- **`field`**: Als de zoektermen alleen moeten overeenkomen met een subset van de eigenschappen, kan de veldparameter het pad naar die eigenschap aangeven. De parameter kan worden herhaald om op meer dan één bezit te wijzen dat zou moeten worden aangepast.
- **`qop`**: Bevat een controleparameter die wordt gebruikt om het passende gedrag van het onderzoek te wijzigen. Wanneer de parameter aan wordt geplaatst en dan moeten alle onderzoekstermijnen aanpassen en wanneer de parameter afwezig is of zijn waarde aan wordt geplaatst of dan om het even welke termijnen voor een gelijke kunnen tellen.

### Bijwerken en patchen

Als u een instantie wilt bijwerken, kan een client de volledige lijst met eigenschappen tegelijk overschrijven of een JSON PATCH-aanvraag gebruiken om afzonderlijke eigenschapswaarden, waaronder lijsten, te manipuleren.

In beide gevallen specificeert URL van het verzoek de weg aan de fysieke instantie en in beide gevallen zal de reactie een JSON ontvangstlading zoals die zijn teruggekeerd van [creeer verrichting](#create-instances)zijn. Een client moet bij voorkeur de `Location` header of een HAL-koppeling gebruiken die deze heeft ontvangen van een eerdere API-aanroep voor dit object als het volledige URL-pad voor deze API. Als dit niet mogelijk is, kan de client de URL van de URL `containerId` en de `instanceId`URL samenstellen.

**Verzoek** (PUT)

```shell
curl -X PUT {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'\ 
  -d '{ 
  "_instance": { 
    {JSON_PROPERTIES_OF_THIS_INSTANCE} 
  }, 
  "_links": { 
    {HAL_LINKS_OF_THIS_INSTANCE} 
  } 
}'  
```

**Verzoek** (PATCH)

```shell
curl -X PATCH {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.patch.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' \ 
  -d '[ 
  { 
    {JSON_PATCH_INSTRUCTIONS_FOR_THIS_INSTANCE} 
  } 
]'
```

Het PATCH-verzoek past de instructies toe en valideert vervolgens de resulterende entiteit op basis van het schema en dezelfde entiteit- en referentiële integriteitsregels als het PUT-verzoek.

**Waardebewerkingen voor eigenschappen beheren**

U kunt met de volgende annotaties voorkomen dat eigenschappen worden ingesteld bij het maken en/of bijwerken van het bestand:

- **`"meta:usereditable"`**: Boolean - Wanneer een verzoek van een gebruikersagent voortkomt die de bezoeker met een gebruiker of een technisch toegangstoken van de rekeningstoegang identificeert dan zouden de eigenschappen die met geannoteerd zijn niet in de nuttige lading `"meta:usereditable": false` moeten aanwezig zijn. Als ze dat wel zijn, mogen ze geen andere waarde hebben dan de waarde die momenteel is ingesteld. Als de waarden verschillen, wordt het update- of patchverzoek afgewezen met de status 422 Niet-verwerkbare entiteit.
- **`"meta:immutable"`**: Boolean - eigenschappen met een annotatie kunnen `"meta:immutable": true` niet worden gewijzigd wanneer ze zijn ingesteld. Dit geldt voor aanvragen die afkomstig zijn van een eindgebruiker, technische accountintegratie of een speciale service.

**Testen op gelijktijdige update**

Er zijn omstandigheden waarin meerdere clients proberen een instantie tegelijk bij te werken. De gegevensopslagruimte wordt beheerd op een cluster van compute nodes zonder centraal transactiebeheer. Om te voorkomen dat een client een instantie schrijft die gelijktijdig door een andere wordt geschreven, kunnen de clients een voorwaardelijk update- of patchverzoek gebruiken. Door de `etag` tekenreeks in de koptekst op te geven zorgt `If-Match` de repository ervoor dat alleen de eerste aanvraag slaagt en de vervolgaanvragen van andere clients die dezelfde `etag` waarde gebruiken, mislukken. De `etag` waarde verandert bij elke wijziging van de instantie. Clients moeten de instantie ophalen om de laatste `etag` waarde op te halen. Van de vele clients die de update proberen, kan slechts één client deze waarde gebruiken. Andere cliënten zullen worden verworpen met een bericht 409 Conflict.

### Instanties verwijderen

Instanties kunnen worden verwijderd met een DELETE-aanroep. Een client moet bij voorkeur de `Location` header of een HAL-koppeling gebruiken die het heeft ontvangen van een eerdere API-aanroep hiervoor als het volledige URL-pad. Als dit niet mogelijk is, kan de client de URL van de URL `containerId` en de fysieke `instanceId`.

**Verzoek**

```shell
curl -X DELETE {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**Antwoord**

```json
{ 
  "instanceId": "3684ceb0-8744-11e9-a989-89f60b24f6cc", 
  "@id": "INSTANCE_URI", 
  "repo:etag": 1, 
  "repo:createdDate": "2019-06-05T03:44:25.343Z", 
  "repo:lastModifiedDate": "2019-06-05T03:44:25.343Z", 
  "repo:createdBy": "CREATOR_ACCOUNT_ID", 
  "repo:lastModifiedBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:createdByClientId": "CREATOR_API_KEY", 
  "repo:lastModifiedByClientId": "YOUR_API_KEY" 
} 
```

Bij het ontvangen van een verwijderingsverzoek controleert de gegevensopslagruimte op andere instanties, van elk schema, nog steeds naar de instantie die moet worden verwijderd. In een gedistribueerd, hoogst beschikbaar systeem, kan de referentiële integriteit niet onmiddellijk worden gecontroleerd. Als er relaties met externe sleutels zijn gedefinieerd, worden controles asynchroon uitgevoerd. Dit leidt tot een enigszins vertraagde reactie op de uitkomst van het verwijderingsverzoek. Wanneer die controles worden uitgevoerd, omvat de directe reactie status 202 Geaccepteerd en een verbinding om het resultaat van de schrappingsverrichting in de `Location` kopbal te controleren. Een klant moet dan controleren of de koppeling tot resultaat heeft geleid.

Als een instantie wordt gevonden die verwijst naar de instantie die wordt verwijderd, is het resultaat een afwijzing van de verwijderingsbewerking. Als er geen andere verwijzingen naar externe sleutels worden gevonden, wordt het verwijderen voltooid. Als het resultaat nog niet is besloten, geeft het antwoord aan dat nog eens 202 geaccepteerde reacties met dezelfde `Location` koptekst zijn ontvangen en wordt de klant gevraagd om te blijven controleren. Wanneer het resultaat wordt bepaald, zal de reactie erop wijzen dat met een 200 Ok status en de lading van de reactie het resultaat van het originele schrappingsverzoek zal bevatten. De 200 Ok-reactie betekent alleen dat het resultaat bekend is en de responsinstantie zal de bevestiging of afwijzing van het verwijderingsverzoek bevatten.

## Aanbiedingen en hun subcomponenten maken

De API&#39;s die in de vorige sectie worden beschreven, gelden uniform voor alle typen zakelijke objecten. Het enige verschil tussen, zeg het creëren van een aanbieding en een activiteit zou de kopbal zijn die op het schema JSON de nuttige lading JSON van het verzoek noteert dat aan het schema voldoet. `content-type` Daarom hoeven de volgende secties zich alleen op die schema&#39;s en de onderlinge relaties te richten.

Wanneer u de API&#39;s met het inhoudstype gebruikt `application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"`, worden de eigen eigenschappen van de instantie ingesloten in de `_instance` eigenschap naast de eigenschap die een `_links` eigenschap bevat. Dit is het algemene formaat waarin alle instanties worden vertegenwoordigd:

```json
{ 
  … ENVELOPE PROPERTIES 
  "_instance": { 
    INSTANCE PROPERTIES 
  }, 
  "_links": {
    HAL PROPERTIES 
  } 
}
```

>[!NOTE] Om beknoptheid te voorkomen worden in alle JSON-fragmenten alleen de instantie-eigenschappen weergegeven en alleen wanneer dit vereist is, wordt de sectie envelopeigenschappen en _links weergegeven.

### Algemene aanbiedingseigenschappen

Aanbiedingen zijn een type beslissingsoptie en het JSON-schema van aanbiedingen neemt de standaardeigenschappen over van opties die elke optieinstantie zal hebben.

- **`@id`** - Een unieke id voor elke optie die de primaire sleutel is en die wordt gebruikt om naar de optie van andere objecten te verwijzen. Deze eigenschap wordt toegewezen wanneer de instantie wordt gemaakt, is onveranderlijk en kan niet worden bewerkt.
- **`xdm:name`** - Elke optie heeft een naam die wordt gebruikt voor zoek- en weergavedoeleinden. De naam is niet onveranderlijk en kan niet worden gebruikt om de instantie uniek te identificeren. De naam kan vrij worden geselecteerd maar zou over aanbiedingsinstanties uniek moeten zijn.

```json
{ 
  "@id": "INSTANCE_URI",                         // meta:immutable=true, meta:usereditable=false 
  "xdm:name": "A name for the Decision Option",  // meta:immutable=false 
  "xdm:characteristics": { 
    properties specific to this instance         // property names can vary per instance 
  } 
}
```

Zie [](#updating-and-patching-instances) Bijwerken en patchen voor de volledige syntaxis cURL. De `schemaId` parameter moet zijn `https://ns.adobe.com/experience/offer-management/personalized-offer` of `https://ns.adobe.com/experience/offer-management/fallback-offer` als de aanbieding een reserveaanbieding is.

Elke aanbiedingsinstantie kan een optionele set eigenschappen hebben die alleen kenmerkend zijn voor die instantie. De verschillende aanbiedingen kunnen verschillende sleutels voor die eigenschappen hebben, moeten de waarden, nochtans koorden zijn. Deze eigenschappen kunnen in besluit en segmenteringsregels worden gebruikt. Ze zijn ook toegankelijk om de gekozen ervaring samen te stellen en de berichten verder aan te passen.

### Levenscyclus van aanbieding

Er is een eenvoudige staat-overgang stroom die alle Opties zal volgen. Zij beginnen in een ontwerpstaat en wanneer zij klaar zijn zal hun staat aan goedkeuring worden geplaatst. Wanneer hun einddatum is verstreken, kunnen ze naar de gearchiveerde staat worden verplaatst. In die staat kunnen ze worden verwijderd of hergebruikt door ze opnieuw in de redactiestatus te plaatsen.

![](../images/entities/offer-lifecycle.png)

- **`xdm:status`** - Deze eigenschap wordt gebruikt voor levenscyclusbeheer van de instantie. De waarde vertegenwoordigt een workflowstatus die wordt gebruikt om aan te geven of de aanbieding nog in opbouw is (waarde = concept), algemeen door de runtime kan worden beschouwd (waarde = goedgekeurd) of dat deze niet langer mag worden gebruikt (waarde = gearchiveerd).

Een eenvoudige PATCH-bewerking op de instantie wordt meestal gebruikt om alleen een `xdm:status` eigenschap te manipuleren:

```json
[
  {
    "op":    "replace",
    "path":  "/_instance/xdm:status",
    "value": "approved" 
  }
]
```

Zie [](#updating-and-patching-instances) Bijwerken en patchen voor de volledige syntaxis cURL. De `schemaId` parameter moet zijn `https://ns.adobe.com/experience/offer-management/personalized-offer` of `https://ns.adobe.com/experience/offer-management/fallback-offer` als de aanbieding een reserveaanbieding is.

### Vertegenwoordigingen en plaatsingen

Aanbiedingen zijn beslissingsopties met weergave van inhoud. Wanneer een beslissing wordt genomen, wordt de optie gekozen en wordt zijn herkenningsteken gebruikt om de inhoud of inhoudsverwijzingen voor de plaatsing te verkrijgen die moet worden geleverd. Een aanbieding kan meer dan één vertegenwoordiging hebben maar elk van die moet een verschillende plaatsingsverwijzing hebben. Dit zorgt ervoor dat bij een bepaalde plaatsing de vertegenwoordiging ondubbelzinnig kan worden bepaald.
Tijdens de beslissingsbewerking wordt de plaatsing bepaald in combinatie met het object activity. Aanbiedingen die geen representatie hebben met die plaatsing als referentie, worden automatisch verwijderd uit de keuzelijst.

Voordat vertegenwoordigingen aan een aanbieding kunnen worden toegevoegd, moeten de plaatsingsinstanties bestaan. Die instanties worden gecreeerd het schema herkenningsteken`https://ns.adobe.com/experience/offer-management/offer-placement`.

```json
{
  "xdm:name": "Kiosk Placement 1",
  "xdm:channel": "https://ns.adobe.com/xdm/channels/web",
  "xdm:componentType": 
     "https://ns.adobe.com/experience/offer-management/content-component-imagelink",
  "xdm:contentTypes": [
    "image/png", "image/png"
  ],
  "xdm:description": "Generic placeholder for offers in the Kiosk application. \nTechnical constraints: max width 530dpi, min width 480 dpi, aspect ratio 12:5. \nStylistic constraints: single background color with text block in complementary colors, \nNo magenta, please!"
} 
```

Zie [](#updating-and-patching-instances) Bijwerken en patchen voor de volledige syntaxis cURL. De `schemaId` parameter moet zijn `https://ns.adobe.com/experience/offer-management/personalized-offer` of `https://ns.adobe.com/experience/offer-management/fallback-offer` als de aanbieding een reserveaanbieding is.

Een **instantie Placement** kan de volgende eigenschappen hebben:

- **`xdm:name`** - Bevat toegewezen naam voor de plaatsing om naar het in menselijke interactie en gebruikersinterfaces te verwijzen.
- **`xdm:description`** - Gebruikt om menselijke leesbare intenties voor te brengen hoe de inhoud in deze plaatsing in de algemene berichtlevering wordt gebruikt. Wanneer de leveringskanalen nieuwe plaatsen bepalen, kunnen zij verdere informatie in dit bezit toevoegen zodat een inhoudsmaker de inhoud kan tot stand brengen of selecteren dienovereenkomstig. Die instructies worden niet formeel geïnterpreteerd of afgedwongen. Dit bezit dient slechts als plaats om de intenties mee te delen.
- **`xdm:channel`** - De URI van een kanaal. Het kanaal geeft aan waar de dynamische inhoud moet worden geleverd. De kanaalbeperking wordt gebruikt om niet alleen over te brengen waar de aanbieding zal worden gebruikt maar ook om de inhoudsredacteur of validator te bepalen die voor de ervaring wordt gebruikt.
- **`xdm:componentType`** - Een model-id, d.w.z. URI, voor de inhoud die kan worden weergegeven op de locatie die door deze plaatsing wordt beschreven. Componenttypen zijn: afbeeldingskoppeling, html of onbewerkte tekst. Elk componenttype kan een specifieke set eigenschappen (een model) impliceren die het content-item kan hebben. De lijst met componenttypen kan worden uitgebreid. Er zijn drie vooraf gedefinieerde componenttypewaarden:
   - `https://ns.adobe.com/experience/offer-management/content-component-imagelink`
   - `https://ns.adobe.com/experience/offer-management/content-component-text`
   - `https://ns.adobe.com/experience/offer-management/content-component-html`
- **`xdm:contentTypes`**, Een beperking voor de mediatypen van de componenten die in deze plaatsing worden verwacht. Er kunnen meerdere mediatypen zijn voor één componenttype, zoals verschillende afbeeldingsindelingen.

**De punten van de vertegenwoordiging** in een aanbieding hebben een objecten structuur in het seriebezit `xdm:representations`. Elk item kan de volgende eigenschappen hebben:

- **`xdm:placement`** - This property contains the reference to the placement instance. De waarde wordt gecontroleerd wanneer de representatie aan de aanbieding wordt toegevoegd. Een plaatsingsinstantie met die URI moet bestaan en mag niet zijn gemarkeerd als verwijderd. Bovendien wordt een controle uitgevoerd om ervoor te zorgen dat een aanbiedingsinstantie geen twee vertegenwoordiging met de zelfde waarde voor hun plaatsingsverwijzing heeft.
- **`xdm:components`** - Inhoudscomponenten zijn de fragmenten die zijn gekoppeld aan de representatie van een bepaalde aanbieding. Deze fragmenten worden later gebruikt om de gebruikerservaring samen te stellen. Merk op dat de Dienst van Beslissing op zich niet de volledige eindgebruikerervaring samenstelt. De volgende eigenschappen maken deel uit van het model van elke component.
   - **`@type`** - this property specifies the component type. Een andere naam voor dit concept is het fragmentmodel van de inhoud. De `@type` component is eenvoudig een URI voor een model dat door de toepassing of de dienst wordt bepaald die de eindgebruikerservaring assembleert.
   - **`repo:id`** - deze eigenschap bevat een globaal unieke, onveranderlijke id voor de hoofdbron van de component in de opslagplaats waar het element is opgeslagen.
   - **`repo:name`** - This property contains a human readable name for the asset in the repository. Deze naam is door de gebruiker gedefinieerd en is niet gegarandeerd uniek.
   - **`repo:resolveURL`** - deze eigenschap bevat een unieke bronlocator voor het lezen van het element in een inhoudsopslagplaats. Hierdoor wordt het eenvoudiger om het middel te verkrijgen zonder dat de klant begrijpt welke API&#39;s moeten worden aangeroepen. De URL retourneert de bytes van de primaire bron van het element.
   - **`dc:format`** - deze eigenschap is afkomstig uit het Dublin Core Metadata Initiative. De indeling kan worden gebruikt om te bepalen welke software, hardware of andere apparatuur nodig is om de bron weer te geven of te gebruiken. De geadviseerde beste praktijken moeten een waarde van een gecontroleerde woordenlijst (bijvoorbeeld, de lijst van de Types van Media van Internet die computermedia formaten bepalen) selecteren.
   - **`dc:language`** - Deze eigenschap bevat de taal of talen van de bron. Talen worden gespecificeerd in taalcode zoals bepaald in IETF RFC 3066.

Er zijn drie vooraf gedefinieerde componenttypen die in de `@type` eigenschap worden uitgedrukt:

- https<span></span>://ns.adobe.com/Experience/aanbieding-management/content-component-imagelink
- https<span></span>://ns.adobe.com/experience/offer-management/content-component-text
- https<span></span>://ns.adobe.com/experience/offer-management/content-component-html

Afhankelijk van de waarde van de `@type` eigenschap, `xdm:components` bevat deze aanvullende eigenschappen:

- **`xdm:linkURL`** - Aanwezig wanneer de component een beeldverbinding is. This property will contain the link that is associated with the image and that the `user-agent` will navigate to when the end user communicate with the content of the aanbieding.
- **`xdm:copyline`** - Wordt gebruikt wanneer de component tekst is. Naast het verwijzen naar een tekstelement, bijvoorbeeld bij lange formuliertekst die er opmaak in kan bevatten, kan een korte tekstreeks rechtstreeks in de eigenschap xdm:copyline worden opgeslagen.

De extra eigenschappen kunnen door cliënten worden gebruikt om context behandelende instructies te plaatsen en te evalueren. De UI-bibliotheekclient van de aanbieding voegt bijvoorbeeld de volgende optionele eigenschappen toe om de weergave eenvoudiger te verwerken:

- Binnen elk punt in de `xdm:components` serie, voegt de cliënt UI van de Bibliotheek van de Aanbieding de volgende eigenschappen toe. Deze eigenschappen mogen niet worden verwijderd of gemanipuleerd zonder dat de gevolgen voor de gebruikersinterface worden begrepen:
   - **`offerui:previewThumbnail`** - Dit is een optionele eigenschap die de aanbiedingsbibliotheek gebruikt om een rendering van het element weer te geven. Deze uitvoering is niet hetzelfde als het element zelf. De inhoud kan bijvoorbeeld HTML zijn en de vertoning is een bitmapafbeelding die alleen een benadering van de afbeelding weergeeft. Deze (lagere kwaliteit) vertoning wordt weergegeven in het weergaveblok van de aanbieding.

Een voorbeeld van de verrichting van de PATCH op een aanbiedingsinstantie toont hoe te om de vertegenwoordiging te manipuleren:

```json
[
  {
    "op":    "add",
    "path":  "/_instance/xdm:representations/-",
    "value": {
      "xdm:placement": "xcore:offer-placement:e51944a87919861",
      "xdm:components": [
        {
          "xdm:copyline": "Get what you want!",
          "@type": "https://ns.adobe.com/experience/offer-management/content-component-text",
          "dc:format": "text/plain"
        }
      ]
    } 
  }
]' 
```

Zie [](#updating-and-patching-instances) Bijwerken en patchen voor de volledige syntaxis cURL. De `schemaId` parameter moet zijn `https://ns.adobe.com/experience/offer-management/personalized-offer` of `https://ns.adobe.com/experience/offer-management/fallback-offer` als de aanbieding een reserveaanbieding is.

De bewerking PATCH kan mislukken als er `xdm:representations` nog geen eigenschap is. In dat geval kan de bovenstaande add-bewerking worden voorafgegaan door een andere add-bewerking die de `xdm:representations` array maakt of de enkele add-bewerking stelt de array rechtstreeks in.
De schema&#39;s en eigenschappen die worden beschreven worden gebruikt voor alle aanbiedingstypes, verpersoonlijkingsaanbiedingen evenals reserveaanbiedingen. De volgende twee secties over beperkingen en besluitvormingsregels verklaren aspecten van verpersoonlijkingsaanbiedingen.

## Aanbiedingsbeperkingen instellen

### Kalenderbeperkingen

Beslissingsopties in het algemeen kunnen een begin- en einddatum en -tijd opleveren die als een kalenderbeperking fungeren. De eigenschappen zijn ingesloten in de eigenschap `xdm:selectionConstraint`:

- **`xdm:startDate`** - Deze eigenschap geeft de begindatum en -tijd aan. De waarde is een tekenreeks die is opgemaakt volgens RFC 339-regels, dus zoals in dit tijdstempel: &quot;2019-06-13T11:21:23.356Z&quot;.
Beslissingsopties die hun begindatum en -tijd nog niet hebben bereikt, worden in de beschikking nog niet als subsidiabel beschouwd.
- **`xdm:endDate`** - Deze eigenschap geeft de einddatum en -tijd aan. De waarde is een tekenreeks die is opgemaakt volgens RFC 339-regels, dus zoals in dit tijdstempel: &quot;2019-07-13T11:00:00.000Z&quot;Beslissingsopties die hun einddatum en -tijd hebben overschreden, worden niet langer als subsidiabel beschouwd in het besluitvormingsproces.

Het veranderen van een kalenderbeperking kan met de volgende vraag van de PATCH worden verwezenlijkt:

```json
[
  {
    "op":   "replace",
    "path": "/_instance/xdm:selectionConstraint",
    "value": {
      "xdm:startDate": "2019-06-13T00:00:00.000Z",
      "xdm:endDate":   "2019-07-13T00:00:00.000Z"
    } 
  }
]' 
```

Zie [](#updating-and-patching-instances) Bijwerken en patchen voor de volledige syntaxis cURL. De `schemaId` parameter moet zijn `https://ns.adobe.com/experience/offer-management/personalized-offer`. Voor alternatieven gelden geen beperkingen.

### Beperkingen voor plafonds

Een begrenzingsbeperking is een component in een beslissingsoptie die de parameters voor aftopping definieert. Afbakening is het proces waarbij wordt beperkt hoe vaak een optie kan worden voorgesteld, zowel voor een afzonderlijk profiel als voor alle profielen. De eigenschappen bevatten een geheel-getalwaarde die groter of gelijk aan 1 moet zijn. De eigenschappen zijn genest in een eigenschap `xdm:cappingConstraint`:

- **`xdm:globalCap`** - Een mondiaal plafond is een beperking van het aantal keren dat een aanbod in zijn geheel kan worden voorgesteld.
- **`xdm:profileCap`** - Een profiellimiet is een beperking van het aantal keren dat een aanbieding aan een bepaald profiel kan worden voorgesteld.

Het plaatsen van of het veranderen van de het maximum beperking op een verpersoonlijkingsaanbieding kan met de volgende vraag van de PATCH worden verwezenlijkt:

```json
[
  {
    "op":   "add",
    "path": "/_instance/xdm:cappingConstraint",
    "value": {
      "xdm:globalCap":  1000000,
      "xdm:profileCap": 5
    } 
  }
]' 
```

Zie [](#updating-and-patching-instances) Bijwerken en patchen voor de volledige syntaxis cURL. De `schemaId` parameter moet zijn `https://ns.adobe.com/experience/offer-management/personalized-offer`. Voor alternatieven gelden geen beperkingen.

Als u de plafondwaarden wilt verwijderen, wordt de bewerking &quot;add&quot; vervangen door de bewerking &quot;remove&quot;. De plafondwaarden bestaan afzonderlijk en kunnen ook afzonderlijk worden ingesteld of verwijderd.

### Subsidiabiliteitsbeperkingen

Aanbiedingen kunnen voorwaardelijk worden geselecteerd in het besluitvormingsproces. Wanneer een verpersoonlijkingsaanbieding een verwijzing naar een toelatingsregel heeft, moet de voorwaarde van de regel aan waar evalueren om het aanbiedingsvoorwerp voor een bepaald profiel te overwegen. De toelatingsregels worden gecreeerd en beheerd onafhankelijk van de beslissingsopties en de zelfde regel kan van veelvoudige verpersoonlijkingsaanbiedingen worden van verwijzingen voorzien.

De verwijzing naar de regel is ingesloten in de eigenschap `xdm:selectionConstraint`:

- **`xdm:eligibilityRule`** - Deze eigenschap bevat een verwijzing naar een subsidiabiliteitsregel. De waarde is de waarde `@id` van een instantie van schemahttps://ns.adobe.com/experience/offer-management/eligibility-rule.

Het toevoegen van en het schrappen van een regel kunnen ook met een verrichting van de PATCH worden verwezenlijkt:

```
[
  {
    "op":   "replace",
    "path": "/_instance/xdm:selectionConstraint/xdm:eligibilityRule",
    "value": "xcore:eligibility-rule:f84c6b33cc63c65" 
  }
]'
```

Zie [](#updating-and-patching-instances) Bijwerken en patchen voor de volledige syntaxis cURL. De `schemaId` parameter moet zijn `https://ns.adobe.com/experience/offer-management/personalized-offer`. Voor alternatieven gelden geen beperkingen.

Merk op dat de toelatingsregel in het `xdm:selectionConstraint` bezit samen met de kalenderbeperkingen wordt ingebed. De verrichtingen van de PATCH zouden niet moeten proberen om het volledige `SelectionConstraint` bezit te verwijderen.

## Vaststelling van de prioriteit van een aanbieding

De kwalificerende beslissingsopties zullen worden gerangschikt om de beste optie voor het bepaalde profiel te bepalen. Om het rangschikken te steunen en een gebrek te verstrekken in het geval dat het rangschikken niet door een ander mechanisme kan worden bepaald kan een basisprioriteit voor elke verpersoonlijkingsaanbieding worden geplaatst.
De basisprioriteit is ingesloten in de eigenschap `xdm:rank`:

- **`xdm:priority`** - Deze eigenschap staat voor de standaardvolgorde waarin een aanbieding boven een andere wordt geselecteerd als er geen profielspecifieke volgorde bekend is. Als na het vergelijken van de prioritaire waarde twee of meer personaliseringsaanbiedingen nog steeds verbonden zijn wordt gekozen willekeurig en gebruikt in het aanbiedingsvoorstel. De waarde voor deze eigenschap moet een geheel getal groter of gelijk aan 0 zijn.

Het aanpassen van de basisprioriteit kan met de volgende vraag van de PATCH worden gedaan:

```shell
curl -X PATCH {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \
  -H 'Content-Type: application/vnd.adobe.platform.xcore.patch.hal+json; schema="{SCHEMA_ID}"' \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}' \
  -d '[
  {
    "op":   "replace",
    "path": "/_instance/xdm:rank/xdm:priority",
    "value": 0 
  }
]'
```

Zie [](#updating-and-patching-instances) Bijwerken en patchen voor de volledige syntaxis cURL. De `schemaId` parameter moet zijn `https://ns.adobe.com/experience/offer-management/personalized-offer`. Voor alternatieven zijn geen ranking-eigenschappen beschikbaar.

## Besluitvormingsregels beheren

De subsidiabiliteitsregels bevatten de voorwaarden die worden beoordeeld om te bepalen of een bepaalde beslissingsoptie in aanmerking komt voor een bepaald profiel. Het vastmaken van een regel aan één of meerdere besluitvormingsopties bepaalt impliciet dat voor deze optie de regel aan waar voor de optie moet evalueren die voor deze gebruiker moet worden overwogen. De regel kan tests op profielattributen bevatten, uitdrukkingen evalueren die ervaringsgebeurtenissen voor dit profiel impliceren, en kan contextgegevens omvatten die tot het besluitverzoek werden overgegaan. Een voorwaarde kan bijvoorbeeld als volgt worden beschreven:

> &quot;Inclusief personen die de status van elite hebben en in de laatste zes maanden driemaal hebben gevlogen op een vlucht met het vluchtnummer van de huidige vlucht.&quot;

De instanties worden gemaakt met schema-idhttps://ns.adobe.com/experience/offer-management/eligibility-rule. De `_instance` eigenschap voor de aanroep van het bestand create of update ziet er als volgt uit:

```json
{
  "xdm:name": "Eligible for a free flight upgrade",
  "xdm:condition": {
    "xdm:value": 
      "membership.status = \"elite\" 
       and (select e from xEvent 
            where e.type = \"flight\" 
              and e.flightnumber = @{{SCHEMA_ID}}.flightnumber
              and (e.timestamp occurs <= 6 months before now).count() > 3
           )",
    "xdm:format": "pql/text",
    "xdm:type": "PQL"
  }
}
```

Zie [](#updating-and-patching-instances) Bijwerken en patchen voor de volledige syntaxis cURL. De `schemaId` parameter moet zijn `https://ns.adobe.com/experience/offer-management/eligibility-rule`.

De waarde in het de voorwaardeigenschap van de regel bevat een uitdrukking PQL. Naar de contextgegevens wordt verwezen via de speciale padexpressie @{schemaID}.

De regels richten zich natuurlijk op segmenten in het Platform van de Ervaring en vaak zal een regel eenvoudig de bedoeling van een segment hergebruiken door het `segmentMembership` bezit van een profiel te testen. De `segmentMembership` eigenschap bevat de resultaten van segmentvoorwaarden die al zijn geëvalueerd. Hierdoor kan een organisatie haar domeinspecifieke doelgroepen eenmaal definiëren, ze een naam geven en de voorwaarden eenmaal evalueren.

## Aanbiedingen beheren

### Tags en coderingsmogelijkheden maken

Aanbiedingen kunnen worden georganiseerd in verzamelingen waarin elke verzameling de filtervoorwaarde definieert die moet worden toegepast. De filterexpressie in een verzameling kan momenteel een van twee vormen hebben:

1. De `@id` parameter van de aanbieding moet één in een lijst van herkenningstekens voor de aanbieding aanpassen om in de inzameling te zijn. Dit filter is eenvoudig een opsomming van de URIs van de aanbiedingen in de inzameling.
2. Een aanbieding kan een lijst van markeringsverwijzingen hebben en het filter van de inzameling bestaat uit een lijst van markeringen. De aanbieding is in de collectie wanneer:\
   a. alle filterlabels komen overeen met een van de aanbiedingstags\
   b. alle tags van het filter komen overeen met een van de tags van de aanbieding

Tags zijn eenvoudige instanties die instanties kunnen bieden. Het zijn op zichzelf staande instanties met een naam om ze weer te geven. De naam moet uniek zijn over instanties om het in gebruikersinterface gemakkelijker te maken om hen te tonen.

De voorwerpen van de markering dienen om een categorisering onder besluitvormingsopties (aanbiedingen) te vestigen. Een tag kan door veel aanbiedingen worden gekoppeld en een aanbieding kan veel tagverwijzingen bevatten. Een categorie aanbiedingen wordt vastgesteld door te verwijzen naar alle aanbiedingen die betrekking hebben op een bepaalde set taginstanties.

De taginstanties worden gemaakt met de schema-idhttps://ns.adobe.com/experience/offer-management/tag. De `_instance` eigenschap voor de aanroep van het bestand create of update ziet er als volgt uit:

```json
{
  "xdm:name": "credit card"
} 
```

Zie [](#updating-and-patching-instances) Bijwerken en patchen voor de volledige syntaxis cURL. De `schemaId` parameter moet zijn `https://ns.adobe.com/experience/offer-management/tag`.


Een aanbiedingsinstantie kan worden gemaakt met de lijst met tagreferenties, zoals:

```json
{
  "xdm:name": "ABC Bank Credit Card",
  "xdm:tags": [
    "xcore:tag:f66f67dbe6d6ee1",
    "xcore:tag:f2df943c428b6f7"
  ]
}
```

Een aanbieding kan ook worden gepatcheerd om de lijst met tags te wijzigen:

```json
[
  {
    "op":    "add",
    "path":  "/_instance/xdm:tags/-",
    "value": "xcore:tag:f66f677ad3c0ba7" 
  }
]' 
```

In beide gevallen raadpleegt u [Bijwerken en patchen voor de volledige cURL-syntaxis](#updating-and-patching-instances) . De `schemaId` parameter moet zijn `https://ns.adobe.com/experience/offer-management/personalized-offer`.

Merk op dat het `xdm:tags` bezit reeds moet bestaan om toe te voegen verrichting te slagen. Als er geen tags bestaan in een instantie, kan de PATCH-bewerking eerst de array-eigenschap toevoegen en vervolgens een tagverwijzing naar die array toevoegen.

### Filters definiëren voor aanbiedingsverzamelingen

De filterinstanties worden gemaakt met schema-idhttps://ns.adobe.com/experience/offer-management/offer-filter. De `_instance` eigenschap voor de aanroep van het maken of bijwerken kan er als volgt uitzien:

```json
{
  "xdm:name": "All Upgrade offers",
  "xdm:filterType": "allTags",
  "ids": [
    "xcore:tag:f66f67dbe6d6ee1",
    "xcore:tag:f66f677ad3c0ba7"
  ]
}
```

Zie [](#updating-and-patching-instances) Bijwerken en patchen voor de volledige syntaxis cURL. De `schemaId` parameter moet zijn `https://ns.adobe.com/experience/offer-management/offer-filter`.

- **`xdm:filterType`** - Deze eigenschap geeft aan of het filter is ingesteld met tags of met verwijzingen die rechtstreeks door de id&#39;s worden aangeboden. Wanneer het filter is ingesteld om tags te gebruiken, kan het filtertype verder aangeven of alle tags moeten overeenkomen met de tags in een bepaalde aanbieding of of dat een van de opgegeven tags voldoende is om voor het filter in aanmerking te komen. De geldige waarden voor deze enum-eigenschap zijn:
   - `offers`
   - `anyTags`
   - `allTags`
- **`ids`** - Een eigenschap bevat een array van URI&#39;s die verwijzingen zijn naar instanties of taginstanties, afhankelijk van de waarde van `xdm:filterType`. .

De volgende vraag illustreert hoe het `_instance` bezit voor creeert of updatevraag als kijkt in het geval de aanbiedingen direct van verwijzingen worden voorzien:

```json
{
  "xdm:name": "All Upgrade offers",
  "xdm:filterType": "offers",
  "ids": [
    "xcore:personalized-offer:f85e8298e53398d",
    "xcore:personalized-offer:f83a85c2bca3f1f",
    "xcore:personalized-offer:f9195bd412180b1",
    "xcore:personalized-offer:f67be37b6ad6ee6",
    "xcore:personalized-offer:f87bcc710ba6e93",
    "xcore:personalized-offer:f8855c30c0b20f8",
    "xcore:personalized-offer:f67bca7032d6ee5",
    "xcore:personalized-offer:f67bab756ed6ee4",
    "xcore:personalized-offer:f65281d506d6edf"
  ] 
} 
```

## Beheersactiviteiten

Een aanbiedingsactiviteit wordt gebruikt om het besluitvormingsproces te controleren. Het specificeert het aanbiedingsfilter dat op de totale inventaris wordt toegepast om aanbiedingen door onderwerp/categorie te versmallen, de plaatsing om de inventaris aan die aanbiedingen te versmallen die in de gereserveerde ruimte passen en specificeert een reserveoptie als de gecombineerde beperkingen alle beschikbare verpersoonlijkingsopties (aanbiedingen) onbruikbaar maken.

De activity-instanties worden gemaakt met schema-id`https://ns.adobe.com/experience/offer-management/offer-activity`. De `_instance` eigenschap voor de aanroep van het bestand create of update ziet er als volgt uit:

```json
{
  "xdm:name": "Call center IVR Personalization",
  "xdm:startDate": "2019-03-01T05:59:59.999Z",
  "xdm:endDate":   "2019-12-27T00:00:00.000Z",
  "xdm:status":    "live",
  "xdm:placement": "xcore:offer-placement:f652486959731ff",
  "xdm:filter":    "xcore:offer-filter:f6998eb62ed6f15",
  "xdm:fallback":  "xcore:fallback-offer:f6529b31b3c0ba6"
}
```

Zie [](#updating-and-patching-instances) Bijwerken en patchen voor de volledige syntaxis cURL. De `schemaId` parameter moet zijn `https://ns.adobe.com/experience/offer-management/offer-activity`.

- **`xdm:name`** - Deze verplichte eigenschap bevat de naam van de activiteit. De naam wordt getoond in diverse gebruikersinterfaces.
- **`xdm:status`** - Deze eigenschap wordt gebruikt voor levenscyclusbeheer van de instantie. De waarde vertegenwoordigt een werkstroomstatus die wordt gebruikt om aan te geven of de activiteit nog in opbouw is (waarde = concept), algemeen door de runtime kan worden beschouwd (waarde = live) of dat deze niet langer mag worden gebruikt (waarde = gearchiveerd).
- **`xdm:placement`** - Een verplicht bezit dat een verwijzing bevat naar een aanbiedingsplaatpositie die op de inventaris wordt toegepast wanneer in het kader van deze activiteit een beslissing wordt genomen. De waarde is URI (`@id`) van de aanbiedingsplaatsing die wordt gebruikt.
- **`xdm:filter`** - Een verplichte eigenschap met een verwijzing naar een aanbiedingsfilter dat wordt toegepast op de inventaris wanneer in het kader van deze activiteit een besluit wordt genomen. De waarde is URI (`@id`) van het aanbiedingsfilter dat wordt gebruikt.
- **`xdm:fallback`** - Een verplichte eigenschap met een verwijzing naar een fallback-aanbieding. Een fallback-aanbieding wordt gebruikt wanneer een beslissing voor deze activiteit geen van de personalisatieaanbiedingen kwalificeert. De waarde is de URI (`@id`) van een fallback-aanbiedingsinstantie.

### Terugvalaanbiedingen beheren

Voordat activiteiteninstanties kunnen worden gemaakt, moet er een fallback-aanbieding bestaan die in aanmerking komt voor de plaatsing van de activiteit. De instanties van de reserveaanbieding worden gecreeerd met schema herkenningsteken`https://ns.adobe.com/experience/offer-management/fallback-offer`. Het `_instance` bezit voor creeer of updatevraag bevat de zelfde algemene eigenschappen die een verpersoonlijkingsaanbieding heeft, maar het kan geen andere beperkingen hebben.

```json
{
  "xdm:name": "Default for Kiosk Placements",
  "xdm:status": "approved",
  "xdm:representations": [
    {
      "xdm:placement": "xcore:offer-placement:e91afcf81bad130"
      "xdm:components": [
        {
          "dc:language": ["en" ],
          "@type": "https://ns.adobe.com/experience/offer-management/content-component-html",
          "dc:format": "text/html"
        }
      ]
    }
  ]
}  
```

Zie [](#updating-and-patching-instances) Bijwerken en patchen voor de volledige syntaxis cURL. De `schemaId` parameter moet zijn `https://ns.adobe.com/experience/offer-management/fallback-offer`.


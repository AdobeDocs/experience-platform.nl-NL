---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Werken met API's voor de beslissingsservice-runtime
topic: tutorial
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# Werken met API&#39;s voor de beslissingsservice-runtime

Dit document bevat een zelfstudie voor het werken met de runtimeservices van Decisioning Service met behulp van Adobe Experience Platform-API&#39;s.

## Aan de slag

Deze zelfstudie vereist een werkend inzicht in de diensten van het Platform van de Ervaring betrokken bij het besluiten van en het bepalen van het volgende beste aanbod om tijdens klantenervaringen voor te stellen. Lees de documentatie voor het volgende voordat u met deze zelfstudie begint:

- [Beslissingsservice](./../home.md): Biedt het framework voor het toevoegen en verwijderen van aanbiedingen en het maken van algoritmen voor het kiezen van de beste optie die tijdens de ervaring van de klant wordt getoond.
- [XDM (Experience Data Model)](../../xdm/home.md): Het gestandaardiseerde kader waardoor Platform gegevens van de klantenervaring organiseert.
- [PQL (Profile Query Language)](../../segmentation/pql/overview.md): PQL wordt gebruikt om regels en filters te bepalen.
- [Beslissingsobjecten en -regels beheren met behulp van API&#39;s](./entities.md): Voordat u de runtime voor beslissingsservices kunt gebruiken, moet u de verwante entiteiten instellen.

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

>[!NOTE] Raadpleeg de documentatie bij het overzicht van de [sandbox voor meer informatie over sandboxen in Platform](../../tutorials/authentication.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

Ook nodig voor runtime-aanvragen:

- x-request-id: `{UUID}`

>[!NOTE] `UUID` is een tekenreeks in UUID-indeling die wereldwijd uniek is en niet opnieuw mag worden gebruikt voor verschillende API-aanroepen

De beslissingsdienst wordt gecontroleerd door een aantal bedrijfsvoorwerpen die met elkaar verwant zijn. Alle zakelijke objecten worden opgeslagen in de zakelijke objectopslagplaats van Platform, XDM Core Object Repository. Een belangrijk kenmerk van deze opslagplaats is dat de API&#39;s orthogonaal zijn ten opzichte van het type bedrijfsobject. In plaats van POST, GET, PUT, PATCH of DELETE API te gebruiken die op het type van middel in zijn API eindpunt wijst, zijn er slechts 6 generische eindpunten maar zij aanvaarden of keren een parameter terug die op het type van de doorverwijs wijst wanneer dat nodig is. Het schema moet bij de repository worden geregistreerd, maar daarna is de repository bruikbaar voor een set open-end objecttypen.

De eindpuntwegen voor alle Repository APIs van de Voorraad van Objecten XDM van de Kern beginnen met `https://platform.adobe.io/data/core/ode/`.

Het eerste wegelement na eindpunt is het `containerId`. Deze id wordt verkregen via het XDM Core Object Repository root-eindpunt `GET https://platform.adobe.io/data/core/xcore/`.

## Samenstelling van besluitvormingsmodellen

De activering van de bedrijfslogische entiteiten gebeurt automatisch en voortdurend. Zodra een nieuwe optie in de bewaarplaats wordt opgeslagen en als &quot;goedgekeurd&quot;wordt gemerkt, zal het een kandidaat voor opneming de reeks beschikbare opties zijn. Zodra een beslissingsregel is bijgewerkt, worden de regels opnieuw samengesteld en voorbereid voor uitvoering tijdens de runtime. Bij deze automatische activeringsstap worden eventuele beperkingen die door de bedrijfslogica worden gedefinieerd en die niet afhankelijk zijn van de runtimecontext, geëvalueerd. De resultaten van deze activeringsstap worden verzonden naar een cache waar ze beschikbaar zijn voor de beslissingsservice-runtime.

### Effecten van plaatsingen, filters en levenscyclustoestanden

Aanbiedingen worden voortdurend gemaakt, wijzigingen worden doorgevoerd in de levenscyclusstatus of er worden mogelijk nieuwe weergaven van de inhoud weergegeven. Het aanbiedingsfilter van een activiteit kan voorstellen veranderen of aanpassen of filteren de van wie de markeringsreeksen werden bijgewerkt. Dit proces kan op eerlijke wijze worden betrokken en toepassingen en diensten moeten weten wat de uiteindelijke kandidaat-activiteit zal zijn. De beslissingsruntime biedt een API die de activiteit aanbiedt en die aanbiedingen uitfiltert die niet zijn goedgekeurd, niet overeenkomen met het aanbiedingsfilter of geen representatie hebben voor de plaatsing waarnaar door de activiteit wordt verwezen.

**Verzoek**

```shell
curl -X GET {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/offers?activityId={ACTIVITY_URI}' \
  -H 'Accept: application/vnd.adobe.xdm+json \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}'
```

**Antwoord**

De parameter `activityId` kan in url worden herhaald en tot 30 verschillende activiteitenverwijzingen kunnen in één verzoek worden gegeven. De reactie zal nuttig zijn om het even welke onverwachte omstandigheden te merken die uit de opstelling voortvloeien en zal als kijken:

```json
{
  "xdm:activityOffers": [
    {
      "xdm:offerActivity": {
        "@id": "{ACTIVITY_URI}",
        "_links": {
          "self": {
            "href": "{repository_endpoint}/{CONTAINER_ID}/instances/{ACTIVITY_INSTANCE_ID}"
          }
        },
        "repo:etag": "1"
      },
      "xdm:offers": [
        {
          "@id": "{OFFER_URI_1}",
          "_links": {
            "self": {
              "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{OFFER_INSTANCE_ID_1}"
            }
          },
          "repo:etag": "15"
        },
        {
          "@id": "{OFFER_URI_2}",
          "_links": {
            "self": {
              "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{OFFER_INSTANCE_ID_2}"
            }
          },
          "repo:etag": "5"
        }
      ],
      "xdm:fallbackOffer": {
        "@id": "{FALLBACK_URI}",
        "_links": {
          "self": {
            "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{FALLBACK_INSTANCE_ID}"
          }
        },
        "repo:etag": "2"
      }
    }
  ]
}
```

Er is een kleine vertraging van enkele seconden tussen het tijdstip waarop de objecten zijn bijgewerkt en het tijdstip waarop de API-reactie de activity-to-aanbiedingen-toewijzing weerspiegelt. De revisie van elk voorwerp wordt gegeven in de reactie zodat de cliënten kunnen controleren of er een update aan de voorwerpen is die niet is weerspiegeld.

### Diagnostics API en probleemoplossing

Activiteiten, aanbiedingen en subsidiabiliteitsregels worden gecompileerd in een intern formaat (runtime aanbiedingencatalogus) dat wordt gebruikt door de runtime van de beslissingsservice. De compilatie kan fouten ontdekken die niet werden gevangen door de controles die werden uitgevoerd toen de voorwerpen werden opgeslagen en de verbindingen in de Bewaarplaats van de Objecten XDM van de Kern werden gevestigd.

Een API voor diagnostiek wordt verstrekt om het even welke compilatiefouten te verkrijgen die in die stap voorkwamen en in het geval dat er geen fouten zijn om informatie te verkrijgen over wanneer de regels en de activiteiten voor het laatst werden opnieuw samengesteld.

**Verzoek**

```shell
curl -X GET {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/diagnostics \
  -H 'Accept: application/vnd.adobe.xdm+json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}'
```

De enige parameter voor deze API-aanroep is `containerId`. De resultaten alle updates van alle cliënten die besluitvormingsregels, aanbiedingen, activiteiten hebben gewijzigd of filters in die container aanbieden. Er is een kleine vertraging van enkele seconden tussen het tijdstip waarop de objecten zijn bijgewerkt en het tijdstip waarop de compilatie is voltooid. De laatste update timestamp en om het even welke fouten zijn teruggekeerd in het antwoord op de diagnostische vraag.

**Antwoord**

```json
{
  "xdm:operations": {
    "xdm:offerCatalogUpdate": {
      "xdm:date": "2019-06-19T23:28:44.855Z",
      "xdm:errors": []
    },
    "xdm:activitiesUpdate": {
      "xdm:date": "2019-06-19T23:28:40.114Z",
      "xdm:errors": []
    }
  }
}
```

## REST API-aanroepen om beslissingen uit te voeren

REST API is één van de routes voor toepassingen die op Platform lopen om de volgende beste ervaring te verkrijgen die op de regels, de modellen en de beperkingen wordt gebaseerd die de organisatie voor hun gebruikers heeft geplaatst. Toepassingen verzenden een van de identiteiten van het profiel (profiel-id en naamruimte van identiteit). De beslissingsservice zoekt het profiel op en de informatie wordt gebruikt om de bedrijfslogica toe te passen. Aanvullende contextgegevens kunnen worden doorgegeven aan het verzoek en indien gespecificeerd in de bedrijfsregels worden opgenomen in de gegevens om de beslissing te nemen.

Toepassingen kunnen betere prestaties bereiken door een beslissing te vragen voor maximaal 30 activiteiten tegelijk. De URI&#39;s van de activiteiten worden doorgegeven in dezelfde aanvraag. De REST API is synchroon en retourneert de voorgestelde opties voor al die activiteiten of de fallback-optie als geen enkele personalisatieoptie aan de beperkingen voldoet.

Het is mogelijk dat twee verschillende activiteiten dezelfde optie krijgen als hun &quot;beste&quot;. Om te vermijden herhalend een samengestelde ervaring, door gebrek, scheidt de Beslissende Dienst tussen de activiteiten die in het zelfde verzoek van verwijzingen worden voorzien. Arbitrage houdt in dat voor elk van de activiteiten hun top-N-opties in overweging worden genomen, maar dat geen enkele optie meer dan één keer voor die activiteiten wordt voorgesteld. Als twee activiteiten dezelfde bovenste optie hebben, wordt een van hen gekozen om de op een na beste keuze of de op twee na beste optie te gebruiken enzovoort. Deze regels voor deduplicatie proberen te voorkomen dat voor een van de activiteiten de mogelijkheid van terugvalsteun moet worden gebruikt.

Het verzoek om een beschikking bevat de argumenten die de inhoud van een POST-verzoek betreffen. De hoofdtekst is opgemaakt als JSON- `Content-Type` koptekstwaarde `application/vnd.adobe.xdm+json; schema="{REQUEST_SCHEMA_AND_VERSION}"`

Het aanvraagschema en de versie die op dit moment worden ondersteund, zijn `https://ns.adobe.com/experience/offer-management/decision-request;version=0.9`. In de toekomst worden aanvullende aanvraagschema&#39;s of -versies aangeboden.

**Verzoek**

```shell
curl -X POST {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/decisions \
  -H 'Accept: application/json, application/problem+json \
  -H '
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}' \
  -d '{
  "xdm:dryRun": {DRY_RUN_TRUE_FALSE},
  "xdm:validateContextData": {VALIDATE_CONTEXT_DATA_TRUE_FALSE},

  "xdm:offerActivities":[
    {
      "xdm:offerActivity": "{ACTIVITY_URI_1}"
    },
  ],
  "xdm:identityMap":{
    "{PROFILE_ID_NAMESPACE_CODE}":[
      {
        "xdm:id":"{PROFILE_ID}"
      }
    ]
  },
  "xdm:profileModel":"{PROFILE_MODEL}",
  "xdm:contextData": [
    {
      "@type": "{CONTEXT_DATASSCHEMA_ID}"
      "xdm:data": { JSON PROPERTIES OF CONTEXT ENTITY }
    }
  ] ,
  "xdm:allowDuplicatePropositions": {
    "xdm:acrossActivities": {DUPLICATE_OFFER_IDS_OF_TRUE_FALSE},
  }
}’
```

- **`xdm:dryRun`** - Wanneer de waarde van dit facultatieve bezit aan waar wordt geplaatst zal het besluitvormingsverzoek aan het maximum beperken beperkingen maar niet die tellers werkelijk zal trekken, is de verwachting dat de bezoeker nooit van plan is om het voorstel aan het profiel voor te stellen. De beslissingsservice zal het voorstel niet opnemen als een officiële XDM-besluitvormingsgebeurtenis en het zal niet worden weergegeven in de rapportage van gegevenssets. De standaardwaarde van deze eigenschap is false en wanneer de eigenschap wordt weggelaten, wordt de beslissing niet als een testrun beschouwd en moet deze daarom aan de eindgebruiker worden gepresenteerd.
- **`xdm:validateContextData`** - Met deze optionele eigenschap wordt de validatie van de contextgegevens in- of uitgeschakeld. Als de bevestiging wordt aangezet, dan voor elk verstrekt punt van contextgegevens, zal het schema (dat op het `@type` gebied wordt gebaseerd) van de registratie XDM worden gehaald, en het `xdm:data` voorwerp zal tegen het worden bevestigd.

De aanvraag per dit schema bevat een array van URI&#39;s die verwijzen naar aanbiedingsactiviteiten, een profielidentiteit en een array van contextgegevensitems:

- **`xdm:offerActivities`** - Deze verplichte eigenschap is een array van objecten waarin elk item gegevens bevat over de aanbiedingsactiviteit. De aanbiedingsactiviteit heeft de volgende eigenschappen:
   - **`xdm:offerActivity`** - De unieke id (URI) van de activiteit. Dit is de waarde van het `@id` eigendom van de aanbiedingsactiviteit.
- **`xdm:identityMap`** - Een verplichte eigenschap met een JSON-object dat voldoet aan het XDM-schema `https://ns.adobe.com/xdm/context/identitymap`. De eigenschap definieert een kaart waar de sleutel een naamruimtecode voor de identiteit is en de waarde bestaat uit een lijst met id&#39;s voor de eindgebruiker in de opgegeven naamruimte. Indien m.
- **`xdm:contextData`** - Een optionele eigenschap die items bevat die worden beschreven door een verwijzing naar hun schema. Elk contextegegevensitem in de array moet de volgende eigenschappen hebben:
   - **`@type`** - Een verplichte eigenschap die verwijst naar het XDM-schema van het object in dit item.
   - **`xdm:data`** - Een verplichte eigenschap die de objecteigenschappen bevat volgens het XDM-schema dat in de `@type` eigenschap is opgegeven.

## Dynamische contextgegevens in beslissingsverzoeken

In de vorige sectie wordt aangegeven hoe XDM-objecten kunnen worden doorgegeven aan een beslissingsverzoek. Hier volgt een voorbeeld van een dergelijke array van contextobjecten:

```json
"xdm:contextData": [
  {
    "@type":" https://ns.adobe.com/{TENANT_ID_OF_ORG}/schemas/{NUMERIC_SCHEMA_ID};version=1",
    "xdm:data":{ 
      "{TENANT_ID_OF_ORG}": {
        "productDetails":{ 
          "xdm:gender":      "unisex",
          "xdm:fabrication": "leather",
          "xdm:category":    "wallets",
        }
      }
    }
  }
]
```

Het schema moet door uw organisatie zijn samengesteld. Raadpleeg de zelfstudie [Schema-editor voor meer informatie over het samenstellen van schema&#39;s](../../xdm/tutorials/create-schema-ui.md). Het schema wordt weergegeven in een naamruimte `https://ns.adobe.com/{TENANT_ID}/schemas`.

De ontwikkelaarsgids [van de Registratie van het](../../xdm/tutorials/create-schema-api.md) Schema API verklaart hoe de schema&#39;s programmatically kunnen worden betreden en hoe een ontwikkelaar huurder identiteitskaart en het numerieke herkenningsteken van uw schema verkrijgt. Het versieaantal wordt vereist en ook verstrekt door de schemaregistratie APIs.

Een schema dat door een organisatie wordt bepaald zal typisch een wortelbezit hebben genoemd `_{TENANT_ID}`, ook genoemd het huurdersnamespace koord.
Merk op dat de eigenschappen die van een globale schemacomponent zoals _`https://ns.adobe.com/xdm/context/product` worden gebruikt een namespaceprefix hebben `xdm:`. In dit geval `productDetails` is de door de organisatie gedefinieerde eigenschap geconstrueerd met dat datatype. Terwijl huurderseigenschappen in een bezit worden genesteld dat na huurdersnamespace wordt genoemd, datatypes die globaal beschikbaar zijn gebruiken de gereserveerde prefix `xdm:` om botsingen van bezitsnamen te verhinderen.

Meerdere gegevensobjecten kunnen in de `xdm:contextData` eigenschap worden vermeld. Elk object moet zijn type identificeren via de `@type` eigenschap.
De waarden van de contextgegevensobjecten zijn beschikbaar voor gebruik in PQL-expressies, bijvoorbeeld in de voorwaarde van een geschiktheidsregel. Het contextgegevensobject moet worden geadresseerd via de speciale padverwijzingsexpressie `@{schemaId}`. De expressies die volgen op deze verwijzingsexpressie zijn reguliere padexpressies die toegang hebben tot de eigenschappen van het gegevensobject:

```json
{
  "xdm:name": "Eligible for a free gender-specific item of interest",
  "xdm:condition": {
    "xdm:value":
      "gender in (\"female\",\"non-specific\")  
       and (
         select p from
           @{https://ns.adobe.com/{TENANT_ID}/schemas/{NUMERIC_SCHEMA_ID}}._{TENANT_ID}
         select e from xEvent 
            where e.type = \"productSearch\" 
              and e.category = p.category 
              and p.gender in (\"female\",\"unisex\")
       )",
    "xdm:format": "pql/text",
    "xdm:type": "PQL"
  }
}
```

In het bovenstaande voorbeeld `p` doorloopt de variabele de array met objecten die zijn gemarkeerd met `@type` = `https://ns.adobe.com/{TENANT_ID}/schemas/{NUMERIC_SCHEMA_ID}}`.

De PQL-syntaxis gebruikt geen voorvoegsels in eigenschapsnamen. Standaard wordt naar algemene eigenschappen verwezen zonder het `xdm:` voorvoegsel. Eigenschappen die uw organisatie definieert, zijn genest binnen een **extra** eigenschap die naar de naamruimte voor huurders wordt genoemd (in het voorbeeld dat door de variabele wordt aangegeven `{TENANT_ID}`). Als u rechtstreeks wilt kunnen verwijzen naar de door aangepaste instellingen gedefinieerde eigenschappen, `p` wordt de variabele gebonden aan het resultaat van het pad dat de aanvullende geneste eigenschap verwijdert.

## Gebruik van profielrecords

Alle records voor profiel- en ervaringsgebeurtenisentiteiten worden al in de profielopslag beheerd. Door een of meer profielidentiteiten aan het verzoek door te geven, wordt het profiel voor die identiteiten geïdentificeerd en opgezocht uit de opslag. De gegevens zijn dan automatisch beschikbaar voor besluitvormingsregels en modellen die door de beslissingsstrategie worden geëvalueerd.

Om het profiel en de ervaringsverslagen terug te winnen wordt het standaardsamenvoegbeleid toegepast.
Opmerking: na het uploaden van profielrecords naar de gegevens van het platform is er een kleine vertraging tot de profielrecords kunnen worden opgezocht. Hetzelfde geldt voor het opnemen van profiel- en ervaringsrecords via de streaming API&#39;s. Alleen na een paar seconden zijn de gegevens beschikbaar voor het evalueren van beslissingsregels die het profiel evalueren en gebeurtenisgegevens ervaren.
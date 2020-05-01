---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Behandeling van een privacyverzoek in het Data Lake
topic: overview
translation-type: tm+mt
source-git-commit: d3584202554baf46aad174d671084751e6557bbc

---


# Behandeling van een privacyverzoek in het Data Lake

De privacyservice van Adobe Experience Platform verwerkt verzoeken van klanten om toegang te krijgen tot hun persoonlijke gegevens, deze niet te verkopen of deze te verwijderen, zoals gedefinieerd in wettelijke en organisatorische privacyregels.

Dit document behandelt essentiële concepten met betrekking tot het verwerken van privacyverzoeken voor klantgegevens die in het Datameer zijn opgeslagen.

## Aan de slag

U wordt aangeraden een goed begrip te hebben van de volgende services van het Experience Platform voordat u deze handleiding leest:

* [Privacy-service](../privacy-service/home.md): Beheert verzoeken van klanten om hun persoonlijke gegevens in Adobe Experience Cloud-toepassingen te openen, niet te verkopen of te verwijderen.
* [Catalogusservice](home.md): Het registratiesysteem voor gegevenslocatie en gegevenskoppeling binnen het ervaringsplatform. Biedt een API die kan worden gebruikt om metagegevens van gegevenssets bij te werken.
* [XDM-systeem](../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Platform van de Ervaring gegevens van de klantenervaring organiseert.
* [Identiteitsservice](../identity-service/home.md): Oplost de fundamentele uitdaging die door de fragmentatie van de gegevens van de klantenervaring wordt gesteld door identiteiten over apparaten en systemen te overbruggen.

## Naamruimten voor identiteiten {#namespaces}

Adobe Experience Platform Identity Service biedt een brug tussen identiteitsgegevens van klanten op verschillende systemen en apparaten. De Dienst van de identiteit gebruikt **identiteitsnaamruimten** om context aan identiteitswaarden te verstrekken door hen met hun systeem van oorsprong te verbinden. Een naamruimte kan een algemeen concept vertegenwoordigen, zoals een e-mailadres (&quot;E-mail&quot;) of de identiteit koppelen aan een specifieke toepassing, zoals een Adobe Advertising Cloud-id (&quot;AdCloud&quot;) of een Adobe Target-id (&quot;TNTID&quot;).

De Dienst van de identiteit handhaaft een opslag van globaal bepaalde (standaard) en user-defined (douane) identiteitsnamespaces. Standaard naamruimten zijn beschikbaar voor alle organisaties (bijvoorbeeld E-mail en ECID), terwijl uw organisatie aangepaste naamruimten kan maken die aan de specifieke behoeften voldoen.

Voor meer informatie over identiteitsnaamruimten in het Platform van de Ervaring, zie het overzicht [van](../identity-service/namespaces.md)identiteitsnamespace.

## Identiteitsgegevens toevoegen aan gegevenssets

Wanneer het creëren van privacyverzoeken voor het meer van Gegevens, moeten de geldige identiteitswaarden (en hun bijbehorende namespaces) voor elke individuele klant worden verstrekt om van hun gegevens de plaats te bepalen en het dienovereenkomstig te verwerken. Daarom moeten alle datasets die aan privacyverzoeken onderworpen zijn een **identiteitsbeschrijver** in hun bijbehorend schema XDM bevatten.

>[!NOTE] Om het even welke datasets die op schema&#39;s worden gebaseerd die geen meta-gegevens van de identiteitsbeschrijver (zoals ad hoc datasets) steunen kunnen momenteel niet in privacyverzoeken worden verwerkt.

Deze sectie doorloopt de stappen om een identiteitsbeschrijver aan het XDM schema van een bestaande dataset toe te voegen. Als u al een dataset met een identiteitsbeschrijver hebt, kunt u vooruit aan de [volgende sectie](#nested-maps)overslaan.

>[!IMPORTANT] Houd bij het bepalen van de schemavelden die u wilt instellen als id&#39;s rekening met de [beperkingen van het gebruik van geneste map-type velden](#nested-maps).

Er zijn twee methodes om een identiteitsbeschrijver aan een datasetschema toe te voegen:

* [De gebruikersinterface gebruiken](#identity-ui)
* [De API gebruiken](#identity-api)

### De gebruikersinterface gebruiken {#identity-ui}

In de gebruikersinterface van het Platform van de Ervaring, staat de _[!UICONTROL Schemas]_werkruimte u toe om uw bestaande XDM schema&#39;s uit te geven. Om een identiteitsbeschrijver aan een schema toe te voegen, selecteer het schema van de lijst en volg de stappen voor het[plaatsen van een schemagebied als identiteitsgebied](../xdm/tutorials/create-schema-ui.md#identity-field)in het leerprogramma van de Redacteur van het Schema.

Als u de juiste velden in het schema hebt ingesteld als identiteitsvelden, kunt u doorgaan naar de volgende sectie over het [verzenden van privacyverzoeken](#submit).

### De API gebruiken {#identity-api}

>[!NOTE] Deze sectie veronderstelt u de unieke waarde van identiteitskaart van URI van het schema XDM van uw dataset kent. Als u deze waarde niet kent, kunt u deze ophalen met de API voor catalogusservice. Na het lezen van de [begonnen](./api/getting-started.md) sectie van de ontwikkelaarsgids, volg de stappen die in voor het [vermelden](./api/list-objects.md) van of het [zoeken van de voorwerpen van de Catalogus worden geschetst om uw dataset te vinden](./api/look-up-object.md) . De schema-id is te vinden onder `schemaRef.id`
>
> Deze sectie omvat vraag aan de Registratie API van het Schema. Voor belangrijke informatie met betrekking tot het gebruiken van API, met inbegrip van het kennen van uw `{TENANT_ID}` en het concept containers, zie de [begonnen](../xdm/api/getting-started.md) sectie van de ontwikkelaarsgids.

U kunt een identiteitsbeschrijver aan het schema van XDM van een dataset toevoegen door een POST- verzoek aan het `/descriptors` eindpunt in de Registratie API van het Schema te doen.

**API-indeling**

```http
POST /descriptors
```

**Verzoek**

In het volgende verzoek wordt een identiteitsdescriptor gedefinieerd in een voorbeeldschema in het veld E-mailadres.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
      {
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/personalEmail/address",
        "xdm:namespace": "Email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `@type` | Het type descriptor dat wordt gemaakt. Voor identiteitsbeschrijvers moet de waarde &quot;xdm:descriptorIdentity&quot; zijn. |
| `xdm:sourceSchema` | De unieke URI-id van het XDM-schema van uw gegevensset. |
| `xdm:sourceVersion` | De versie van het XDM-schema dat is opgegeven in `xdm:sourceSchema`. |
| `xdm:sourceProperty` | Het pad naar het schemaveld waarop de descriptor wordt toegepast. |
| `xdm:namespace` | Een van de [standaardnaamruimten](../privacy-service/api/appendix.md#standard-namespaces) die wordt herkend door de privacyservice of een aangepaste naamruimte die wordt gedefinieerd door uw organisatie. |
| `xdm:property` | &quot;xdm:id&quot; of &quot;xdm:code&quot;, afhankelijk van de naamruimte die onder wordt gebruikt `xdm:namespace`. |
| `xdm:isPrimary` | Een optionele booleaanse waarde. Indien waar (true), geeft dit aan dat het veld een primaire identiteit is. Schema&#39;s mogen slechts één primaire identiteit bevatten. De standaardwaarde is false als dit item niet wordt opgenomen. |

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 201 (Gemaakt) en de details van de nieuwe descriptor.

```json
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## Verzoeken indienen {#submit}

>[!NOTE] Deze sectie behandelt hoe te om privacyverzoeken voor het meer van Gegevens te formatteren. Het wordt sterk geadviseerd dat u de documentatie van de Dienst van de [Privacy of van de Dienst API](../privacy-service/ui/overview.md) van de [](../privacy-service/api/getting-started.md) Privacy voor volledige stappen op het voorleggen van een privacybaan, met inbegrip van hoe te om verzonden gegevens van de gebruikersidentiteit in verzoeklading behoorlijk te formatteren controleert.

In de volgende sectie wordt beschreven hoe u privacyaanvragen voor het gegevensmeer kunt indienen met de interface of API van de privacyservice.

### De gebruikersinterface gebruiken

Wanneer het creëren van baanverzoeken in UI, ben zeker om **AEP Gegevensmeer** en/of **Profiel** onder _Producten_ te selecteren om banen voor gegevens te verwerken die in het meer van Gegevens of in real time het Profiel van de Klant worden opgeslagen.

<img src="images/privacy/product-value.png" width="450"><br>

### De API gebruiken

Bij het maken van taakaanvragen in de API moeten alle beschikbare bestanden een specifieke `userIDs` en `namespace` `type` afhankelijk van de gegevensopslag gebruiken waarop ze van toepassing zijn. Ids voor het meer van Gegevens moet &quot;unregistered&quot;voor hun `type` waarde gebruiken, en een `namespace` waarde die één de [privacyetiketten](#privacy-labels) aanpast die aan toepasselijke datasets zijn toegevoegd.

Bovendien moet de `include` array van de aanvraaglading de productwaarden voor de verschillende gegevensopslag bevatten het verzoek wordt ingediend. Bij het indienen van aanvragen voor het Data Lake moet de array de waarde &quot;aepDataLake&quot; bevatten.

Met de volgende aanvraag wordt een nieuwe privacytaak voor het Data Lake gemaakt, waarbij de naamruimte &quot;email_label&quot; wordt gebruikt die niet is geregistreerd. Het omvat ook de productwaarde voor het meer van Gegevens in de `include` serie:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email_label",
            "value": "ajones@acme.com",
            "type": "unregistered"
          },
          {
            "namespace": "email_label",
            "value": "jdoe@example.com",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["aepDataLake"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "ccpa"
}'
```

## Verzoek om verwerking verwijderen

Wanneer het Platform van de Ervaring een schrappingsverzoek van de Dienst van de Privacy ontvangt, verzendt het Platform bevestiging aan de Dienst van de Privacy dat het verzoek is ontvangen en de beïnvloede gegevens voor schrapping duidelijk zijn gemaakt. De gegevens worden vervolgens binnen zeven dagen uit het Data Lake verwijderd. Tijdens dat venster van zeven dagen, worden de gegevens zachte geschrapt en daarom niet toegankelijk door om het even welke dienst van het Platform.

In toekomstige releases zal Platform een bevestiging sturen naar de Privacy Service nadat de gegevens fysiek zijn verwijderd.

## Volgende stappen

Door dit document te lezen, bent u geïntroduceerd aan de belangrijke concepten betrokken bij de verwerking van privacyverzoeken voor het meer van Gegevens. U wordt aangeraden de documentatie in deze handleiding te blijven lezen om meer inzicht te krijgen in de manier waarop u identiteitsgegevens kunt beheren en privacytaken kunt maken.

Zie het document over de verwerking van [privacyverzoeken voor Real-time klantprofiel](../profile/privacy.md) voor stappen over het verwerken van privacyverzoeken voor het archief van het Profiel.

## Aanhangsel

De volgende sectie bevat aanvullende informatie voor het verwerken van privacyverzoeken in het Datameer.

### Geneste toewijzingsvelden labelen {#nested-maps}

Het is belangrijk om op te merken dat er twee soorten genestelde kaart-type gebieden zijn die privacy het etiketteren niet steunen:

* Een toewijzingsveld binnen een veld van het type array
* Een veld van het type map binnen een ander veld van het type map

De verwerking van de privacytaak voor een van de twee bovenstaande voorbeelden zal uiteindelijk mislukken. Daarom wordt u aangeraden geneste kaartvelden niet te gebruiken om privéklantgegevens op te slaan. De relevante consument IDs zou als niet-kaartdatatype binnen het `identityMap` gebied (zelf een kaart-type gebied) voor op verslag-gebaseerde datasets, of het `endUserID` gebied voor op tijd-reeksen-gebaseerde datasets moeten worden opgeslagen.
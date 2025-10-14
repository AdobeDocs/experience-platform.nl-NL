---
keywords: Experience Platform;home;populaire onderwerpen;privacy in datapeer;naamruimten;privacy;data Lake
solution: Experience Platform
title: De verwerking van het privacy- verzoek in het meer van Gegevens
description: Adobe Experience Platform Privacy Service verwerkt verzoeken van klanten om toegang te krijgen, te weigeren of hun persoonsgegevens te verwijderen, zoals bepaald in wettelijke en organisatorische privacyregels. Dit document behandelt essentiële concepten met betrekking tot het verwerken van privacyverzoeken voor klantgegevens die in het datumpigment zijn opgeslagen.
exl-id: c06b0a44-be1a-4938-9c3e-f5491a3dfc19
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1425'
ht-degree: 0%

---

# Behandeling van het privacyverzoek in het datumpigment

Adobe Experience Platform [!DNL Privacy Service] verwerkt verzoeken van klanten om toegang te krijgen, te weigeren of hun persoonsgegevens te verwijderen, zoals is vastgelegd in wettelijke en organisatorische privacyregels.

Dit document behandelt essentiële concepten met betrekking tot het verwerken van privacyverzoeken voor klantgegevens die in het datumpigment zijn opgeslagen.

>[!NOTE]
>
>In deze handleiding wordt alleen uitgelegd hoe u een verzoek om privacy kunt indienen voor het datumpigment in Experience Platform. Als u ook van plan bent om privacyverzoeken voor de de gegevensopslag van het Profiel van de Klant in real time te maken, verwijs naar de gids op [&#x200B; verwerking van het privacyverzoek voor Profiel &#x200B;](../profile/privacy.md) naast dit leerprogramma.
>
>Voor stappen op hoe te om privacyverzoeken voor andere toepassingen van Adobe Experience Cloud te maken, verwijs naar de [&#x200B; documentatie van Privacy Service &#x200B;](../privacy-service/experience-cloud-apps.md).

## Aan de slag

U wordt aangeraden eerst de volgende [!DNL Experience Platform] -services te leren kennen voordat u deze handleiding leest:

* [[!DNL Privacy Service]](../privacy-service/home.md): Beheert verzoeken van klanten om toegang te krijgen tot, uit de verkoop te stappen of hun persoonlijke gegevens te verwijderen in Adobe Experience Cloud-toepassingen.
* [[!DNL Catalog Service]](home.md): Het recordsysteem voor de gegevenslocatie en -lijn binnen [!DNL Experience Platform] . Biedt een API die kan worden gebruikt om metagegevens van gegevenssets bij te werken.
* [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): Het gestandaardiseerde framework waarmee [!DNL Experience Platform] gegevens voor de klantervaring indeelt.
* [[!DNL Identity Service]](../identity-service/home.md): lost de fundamentele uitdaging op die door de fragmentatie van de gegevens van de klantenervaring wordt gesteld door identiteiten over apparaten en systemen te overbruggen.

## Naamruimten voor identiteiten {#namespaces}

Adobe Experience Platform [!DNL Identity Service] biedt een brug tussen identiteitsgegevens van klanten op systemen en apparaten. [!DNL Identity Service] gebruikt naamruimten om context aan identiteitswaarden te verstrekken door hen op hun systeem van oorsprong met elkaar in verband te brengen. Een naamruimte kan een algemeen concept vertegenwoordigen, zoals een e-mailadres (&quot;E-mail&quot;) of de identiteit koppelen aan een specifieke toepassing, zoals een Adobe Advertising Cloud-id (&quot;AdCloud&quot;) of een Adobe Target-id (&quot;TNTID&quot;).

[!DNL Identity Service] onderhoudt een opslag van algemeen gedefinieerde (standaard) en door de gebruiker gedefinieerde (aangepaste) naamruimten. Standaard naamruimten zijn beschikbaar voor alle organisaties (bijvoorbeeld E-mail en ECID), terwijl uw organisatie aangepaste naamruimten kan maken die aan de specifieke behoeften voldoen.

Voor meer informatie over identiteit namespaces in [!DNL Experience Platform], zie het [&#x200B; overzicht van identiteitskaart namespace &#x200B;](../identity-service/features/namespaces.md).

## Identiteitsgegevens toevoegen aan gegevenssets

Wanneer het creëren van privacyverzoeken voor het gegevens meer, moeten de geldige identiteitswaarden (en hun bijbehorende namespaces) voor elke individuele klant worden verstrekt om van hun gegevens de plaats te bepalen en het dienovereenkomstig te verwerken. Daarom moeten alle datasets die aan privacyverzoeken onderworpen zijn een identiteitsbeschrijver in hun bijbehorend schema XDM bevatten.

>[!NOTE]
>
>Om het even welke datasets die op schema&#39;s worden gebaseerd die geen meta-gegevens van de identiteitsbeschrijver (zoals ad hoc datasets) steunen kunnen momenteel niet in privacyverzoeken worden verwerkt.

Deze sectie doorloopt de stappen om een identiteitsbeschrijver aan het XDM schema van een bestaande dataset toe te voegen. Als u reeds een dataset met een identiteitsbeschrijver hebt, kunt u vooruit aan de [&#x200B; volgende sectie &#x200B;](#nested-maps) overslaan.

>[!IMPORTANT]
>
>Wanneer het beslissen van welke schemagebieden om als identiteiten te plaatsen, houd in mening de [&#x200B; beperkingen om genestelde kaart-type gebieden &#x200B;](#nested-maps) te gebruiken.

Er zijn twee methodes om een identiteitsbeschrijver aan een datasetschema toe te voegen:

* [UI gebruiken](#identity-ui)
* [De API gebruiken](#identity-api)

### UI gebruiken {#identity-ui}

In het [!DNL Experience Platform] gebruikersinterface, staat de **[!UICONTROL Schemas]** werkruimte u toe om uw bestaande schema&#39;s uit te geven XDM. Om een identiteitsbeschrijver aan een schema toe te voegen, selecteer het schema van de lijst en volg de stappen voor [&#x200B; plaatsend een schemagebied als identiteitsgebied &#x200B;](../xdm/tutorials/create-schema-ui.md#identity-field) in het [!DNL Schema Editor] leerprogramma.

Zodra u de aangewezen gebieden binnen het schema als identiteitsgebieden hebt geplaatst, kunt u aan de volgende sectie te werk gaan over [&#x200B; het voorleggen van privacyverzoeken &#x200B;](#submit).

### De API gebruiken {#identity-api}

>[!NOTE]
>
>Deze sectie veronderstelt u de unieke waarde van identiteitskaart van URI van het schema XDM van uw dataset kent. Als u deze waarde niet kent, kunt u deze ophalen met de API [!DNL Catalog Service] . Na het lezen van de [&#x200B; begonnen &#x200B;](./api/getting-started.md) sectie van de ontwikkelaarsgids, volg de stappen die in voor [&#x200B; worden geschetst lijst &#x200B;](./api/list-objects.md) of [&#x200B; het opzoeken &#x200B;](./api/look-up-object.md) [!DNL Catalog] voorwerpen om uw dataset te vinden. De schema-id staat onder `schemaRef.id`
>
>Deze sectie veronderstelt ook dat u weet hoe te om vraag aan de Registratie API van het Schema te maken. Voor belangrijke informatie met betrekking tot het gebruiken van API, met inbegrip van het kennen van uw `{TENANT_ID}` en het concept containers, zie [&#x200B; begonnen worden &#x200B;](../xdm/api/getting-started.md) sectie van de API gids.

U kunt een identiteitsbeschrijver aan het schema van XDM van een dataset toevoegen door een POST- verzoek aan het `/descriptors` eindpunt in [!DNL Schema Registry] API te doen.

**API formaat**

```http
POST /descriptors
```

**Verzoek**

In het volgende verzoek wordt een identiteitsbeschrijving gedefinieerd in een veld &quot;E-mailadres&quot; in een voorbeeldschema.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
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
| `xdm:sourceVersion` | De versie van het XDM-schema die is opgegeven in `xdm:sourceSchema` . |
| `xdm:sourceProperty` | Het pad naar het schemaveld waarop de descriptor wordt toegepast. |
| `xdm:namespace` | Één van [&#x200B; standaardidentiteitsnamespaces &#x200B;](../privacy-service/api/appendix.md#standard-namespaces) erkend door [!DNL Privacy Service], of een douane namespace die door uw organisatie wordt bepaald. |
| `xdm:property` | Ofwel &quot;xdm:id&quot; of &quot;xdm:code&quot;, afhankelijk van de naamruimte die onder `xdm:namespace` wordt gebruikt. |
| `xdm:isPrimary` | Een optionele booleaanse waarde. Indien waar (true), geeft dit aan dat het veld een primaire identiteit is. Schema&#39;s mogen slechts één primaire identiteit bevatten. De standaardwaarde is false als dit item niet wordt opgenomen. |

**Reactie**

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

>[!NOTE]
>
>In deze sectie wordt beschreven hoe u privacyverzoeken voor het datumpigment kunt opmaken. Het wordt sterk geadviseerd dat u de [[!DNL Privacy Service]  UI &#x200B;](../privacy-service/ui/overview.md) of [[!DNL Privacy Service]  API &#x200B;](../privacy-service/api/getting-started.md) documentatie voor volledige stappen op bekijkt hoe te om een privacybaan voor te leggen, met inbegrip van hoe te om voorgelegde gegevens van de gebruikersidentiteit in verzoeklading behoorlijk te formatteren.

In de volgende sectie wordt beschreven hoe u privacyverzoeken voor het gegevenspomeer kunt maken met de [!DNL Privacy Service] UI of API.

>[!IMPORTANT]
>
>De hoeveelheid tijd die een privacyverzoek kan duren om te voltooien, kan niet worden gegarandeerd. Als er zich wijzigingen voordoen in het datumpeer terwijl een aanvraag nog wordt verwerkt, kan ook niet worden gegarandeerd of die records al dan niet worden verwerkt.

### UI gebruiken

Wanneer u taakaanvragen maakt in de gebruikersinterface, moet u **[!UICONTROL AEP Data Lake]** onder **[!UICONTROL Products]** selecteren om taken te verwerken voor gegevens die in het datumpigment zijn opgeslagen.

![&#x200B; Beeld dat het product toont van het gegevensmeer dat in de de aanmaakdialoog van het privacyverzoek wordt geselecteerd &#x200B;](./images/privacy/product-value.png)

### De API gebruiken

Bij het maken van taakaanvragen in de API moeten alle `userIDs` die worden geleverd, een specifieke `namespace` en `type` gebruiken, afhankelijk van de gegevensopslag waarop ze van toepassing zijn. IDs voor het gegevensmeer moet `unregistered` voor hun `type` waarde, en a `namespace` waarde gebruiken die één [&#x200B; privacyetiketten &#x200B;](#privacy-labels) aanpast die aan toepasselijke datasets zijn toegevoegd.

Bovendien moet de `include` -array van de payload van de aanvraag de productwaarden voor de verschillende gegevensopslagruimten bevatten waarnaar de aanvraag wordt verzonden. Wanneer u een aanvraag indient voor het datumpeer, moet de array de waarde `aepDataLake` bevatten.

Met de volgende aanvraag wordt een nieuwe privacytaak gemaakt voor het datumpeer, waarbij de naamruimte `email_label` niet-geregistreerd wordt gebruikt. De methode bevat ook de productwaarde voor het datumpeer in de array `include` :

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{ORG_ID}"
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

>[!IMPORTANT]
>
>Experience Platform verwerkt privacyverzoeken over alle [&#x200B; zandbakken &#x200B;](../sandboxes/home.md) die tot uw organisatie behoren. Als gevolg hiervan wordt elke `x-sandbox-name` -header die in de aanvraag is opgenomen, genegeerd door het systeem.

## Verzoek om verwerking verwijderen

Wanneer [!DNL Experience Platform] een verwijderaanvraag ontvangt van [!DNL Privacy Service] , stuurt [!DNL Experience Platform] een bevestiging naar [!DNL Privacy Service] dat de aanvraag is ontvangen en de desbetreffende gegevens zijn gemarkeerd voor verwijdering. De gegevens worden vervolgens binnen zeven dagen uit het datumpeer verwijderd. Tijdens dat venster van zeven dagen worden de gegevens via de elektronische weg verwijderd en zijn deze daarom niet toegankelijk voor een [!DNL Experience Platform] -service.

Als u ook `ProfileService` of `identity` in de privacyaanvraag hebt opgenomen, worden de bijbehorende gegevens afzonderlijk verwerkt. Zie de sectie over [&#x200B; schrapping verzoekverwerking voor Profiel &#x200B;](../profile/privacy.md#delete) voor meer informatie.

## Volgende stappen

Door dit document te lezen, bent u geïntroduceerd aan de belangrijke concepten betrokken bij de verwerking van privacyverzoeken voor het gegevenspeer. U wordt aangeraden de documentatie in deze handleiding te blijven lezen om meer inzicht te krijgen in de manier waarop u identiteitsgegevens kunt beheren en privacytaken kunt maken.

Zie het document op [&#x200B; verwerking van het privacyverzoek voor het Profiel van de Klant in real time &#x200B;](../profile/privacy.md) voor stappen op de verzoeken van de verwerkingsprivacy voor de [!DNL Profile] opslag.

## Bijlage

De volgende sectie bevat aanvullende informatie voor het verwerken van privacyverzoeken in het datumpigment.

### Geneste toewijzingsvelden labelen {#nested-maps}

Het is belangrijk om op te merken dat er twee soorten genestelde kaart-type gebieden zijn die privacy het etiketteren niet steunen:

* Een toewijzingsveld binnen een veld van het type array
* Een kaartveld binnen een ander kaartveld

De verwerking van de privacytaak voor een van de twee bovenstaande voorbeelden zal uiteindelijk mislukken. Daarom wordt u aangeraden geneste kaartvelden niet te gebruiken om privéklantgegevens op te slaan. Relevante consumenten-id&#39;s moeten worden opgeslagen als een gegevenstype zonder toewijzing binnen het `identityMap` -veld (zelf een toewijzingsveld) voor op records gebaseerde gegevenssets, of het `endUserID` -veld voor op tijdreeksen gebaseerde gegevenssets.

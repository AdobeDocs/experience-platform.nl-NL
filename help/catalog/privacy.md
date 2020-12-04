---
keywords: Experience Platform;home;popular topics;data lake privacy;identity namespaces;privacy;data lake
solution: Experience Platform
title: Behandeling van een privacyverzoek in het Data Lake
topic: overview
description: Adobe Experience Platform Privacy Service verwerkt verzoeken van klanten om toegang te krijgen, te weigeren of hun persoonsgegevens te verwijderen, zoals bepaald in wettelijke en organisatorische privacyregels. Dit document behandelt essentiële concepten met betrekking tot het verwerken van privacyverzoeken voor klantgegevens die in het Datameer zijn opgeslagen.
translation-type: tm+mt
source-git-commit: 066337419431db24bde0a8d0d30b85132d08f43c
workflow-type: tm+mt
source-wordcount: '1272'
ht-degree: 0%

---


# Behandeling van een privacyverzoek in de [!DNL Data Lake]

Adobe Experience Platform [!DNL Privacy Service] verwerkt verzoeken van klanten om toegang te krijgen, te weigeren of hun persoonsgegevens te verwijderen, zoals bepaald in wettelijke en organisatorische privacyregels.

Dit document behandelt essentiële concepten met betrekking tot het verwerken van privacyverzoeken voor klantgegevens die in de [!DNL Data Lake]website zijn opgeslagen.

## Aan de slag

U wordt aangeraden de volgende [!DNL Experience Platform] services goed te begrijpen voordat u deze handleiding leest:

* [[!DNL Privacy Service]](../privacy-service/home.md): Beheert verzoeken van klanten om hun persoonlijke gegevens in Adobe Experience Cloud-toepassingen te openen, uit de handel te nemen of te verwijderen.
* [[!DNL Catalog Service]](home.md): The system of record for data location and lineage within [!DNL Experience Platform]. Biedt een API die kan worden gebruikt om metagegevens van gegevenssets bij te werken.
* [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Experience Platform] georganiseerd.
* [[!DNL Identity Service]](../identity-service/home.md): Oplost de fundamentele uitdaging die door de fragmentatie van de gegevens van de klantenervaring wordt gesteld door identiteiten over apparaten en systemen te overbruggen.

## Naamruimten voor identiteiten {#namespaces}

Adobe Experience Platform [!DNL Identity Service] biedt een brug tussen identiteitsgegevens van klanten op systemen en apparaten. [!DNL Identity Service] gebruikt naamruimten om context aan identiteitswaarden te verstrekken door hen met hun systeem van oorsprong te verbinden. Een naamruimte kan een algemeen concept vertegenwoordigen, zoals een e-mailadres (&quot;e-mail&quot;) of de identiteit koppelen aan een specifieke toepassing, zoals een Adobe Advertising Cloud-id (&quot;AdCloud&quot;) of een Adobe Target-id (&quot;TNTID&quot;).

[!DNL Identity Service] onderhoudt een opslag van algemeen gedefinieerde (standaard) en door de gebruiker gedefinieerde (aangepaste) naamruimten. Standaard naamruimten zijn beschikbaar voor alle organisaties (bijvoorbeeld E-mail en ECID), terwijl uw organisatie aangepaste naamruimten kan maken die aan de specifieke behoeften voldoen.

Zie het overzicht [!DNL Experience Platform]van naamruimte voor [identiteiten in voor meer informatie over naamruimten in naamruimten](../identity-service/namespaces.md).

## Identiteitsgegevens toevoegen aan gegevenssets

Wanneer het creëren van privacyverzoeken voor [!DNL Data Lake], moeten de geldige identiteitswaarden (en hun bijbehorende namespaces) voor elke individuele klant worden verstrekt om van hun gegevens de plaats te bepalen en het dienovereenkomstig te verwerken. Daarom moeten alle datasets die aan privacyverzoeken onderworpen zijn een identiteitsbeschrijver in hun bijbehorend schema XDM bevatten.

>[!NOTE]
>
>Om het even welke datasets die op schema&#39;s worden gebaseerd die geen meta-gegevens van de identiteitsbeschrijver (zoals ad hoc datasets) steunen kunnen momenteel niet in privacyverzoeken worden verwerkt.

Deze sectie doorloopt de stappen om een identiteitsbeschrijver aan het XDM schema van een bestaande dataset toe te voegen. Als u al een dataset met een identiteitsbeschrijver hebt, kunt u vooruit aan de [volgende sectie](#nested-maps)overslaan.

>[!IMPORTANT]
>
>Houd bij het bepalen van de schemavelden die u wilt instellen als id&#39;s rekening met de [beperkingen van het gebruik van geneste map-type velden](#nested-maps).

Er zijn twee methodes om een identiteitsbeschrijver aan een datasetschema toe te voegen:

* [De gebruikersinterface gebruiken](#identity-ui)
* [De API gebruiken](#identity-api)

### De gebruikersinterface gebruiken {#identity-ui}

In de [!DNL Experience Platform ]gebruikersinterface kunt u met de werkruimte **[!UICONTROL Schema]** uw bestaande XDM-schema&#39;s bewerken. Om een identiteitsbeschrijver aan een schema toe te voegen, selecteer het schema van de lijst en volg de stappen voor het [plaatsen van een schemagebied als identiteitsgebied](../xdm/tutorials/create-schema-ui.md#identity-field) in het [!DNL Schema Editor] leerprogramma.

Als u de juiste velden in het schema hebt ingesteld als identiteitsvelden, kunt u doorgaan naar de volgende sectie over het [verzenden van privacyverzoeken](#submit).

### De API gebruiken {#identity-api}

>[!NOTE]
>
>Deze sectie veronderstelt u de unieke waarde van identiteitskaart van URI van het schema XDM van uw dataset kent. Als u deze waarde niet kent, kunt u deze ophalen met de [!DNL Catalog Service] API. Na het lezen van de [aan de slag](./api/getting-started.md) sectie van de ontwikkelaarsgids, volg de stappen die in voor het [vermelden](./api/list-objects.md) van of het [zoeken van omhoog](./api/look-up-object.md) [!DNL Catalog] voorwerpen worden geschetst om uw dataset te vinden. De schema-id is te vinden onder `schemaRef.id`
>
> Deze sectie omvat vraag aan de Registratie API van het Schema. Voor belangrijke informatie met betrekking tot het gebruiken van API, met inbegrip van het kennen van uw `{TENANT_ID}` en het concept containers, zie de [begonnen](../xdm/api/getting-started.md) sectie van de ontwikkelaarsgids.

U kunt een identiteitsbeschrijver aan het schema van XDM van een dataset toevoegen door een verzoek van de POST aan het `/descriptors` eindpunt in [!DNL Schema Registry] API te doen.

**API-indeling**

```http
POST /descriptors
```

**Verzoek**

In het volgende verzoek wordt een identiteitsbeschrijving gedefinieerd in een veld &quot;E-mailadres&quot; in een voorbeeldschema.

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
| `xdm:namespace` | Een van de [standaardnaamruimten](../privacy-service/api/appendix.md#standard-namespaces) die wordt herkend door [!DNL Privacy Service]of een aangepaste naamruimte die wordt gedefinieerd door uw organisatie. |
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

>[!NOTE]
>
>In deze sectie wordt beschreven hoe u privacyverzoeken voor de [!DNL Data Lake]website kunt opmaken. We raden u ten zeerste aan de [[!DNL Privacy Service] UI](../privacy-service/ui/overview.md) - of [[!DNL Privacy Service] API](../privacy-service/api/getting-started.md) -documentatie te raadplegen voor volledige stappen op het gebied van het verzenden van een privacytaak, waaronder het correct indelen van verzonden identiteitsgegevens van gebruikers in aanvragen.

In de volgende sectie wordt beschreven hoe u privacyverzoeken voor het [!DNL Data Lake] gebruik van de [!DNL Privacy Service] gebruikersinterface of API kunt indienen.

>[!IMPORTANT]
>
>De hoeveelheid tijd die een privacyverzoek kan duren om te voltooien, kan niet worden gegarandeerd. Als er zich wijzigingen voordoen in het datameer terwijl een aanvraag nog wordt verwerkt, kan ook niet worden gegarandeerd of die records al dan niet worden verwerkt.

### De gebruikersinterface gebruiken

Wanneer het creëren van baanverzoeken in UI, ben zeker om **[!UICONTROL AEP Gegevensmeer]** en/of **[!UICONTROL Profiel]** onder **[!UICONTROL Producten]** te selecteren om banen voor gegevens te verwerken die in [!DNL Data Lake] of [!DNL Real-time Customer Profile], respectievelijk worden opgeslagen.

<img src="images/privacy/product-value.png" width="450"><br>

### De API gebruiken

Bij het maken van taakaanvragen in de API moeten alle beschikbare bestanden een specifieke `userIDs` en `namespace` `type` afhankelijk van de gegevensopslag gebruiken waarop ze van toepassing zijn. IDs voor de [!DNL Data Lake] moet &quot;unregistered&quot;voor hun `type` waarde, en een `namespace` waarde gebruiken die één de [privacyetiketten](#privacy-labels) aanpast die aan toepasselijke datasets zijn toegevoegd.

Bovendien moet de `include` array van de aanvraaglading de productwaarden voor de verschillende gegevensopslag bevatten het verzoek wordt ingediend. Wanneer u een aanvraag naar de array indient, moet de array de waarde bevatten [!DNL Data Lake]`aepDataLake`.

Met de volgende aanvraag wordt een nieuwe privacytaak voor de [!DNL Data Lake]naamruimte &#39;email_label&#39; gemaakt die niet is geregistreerd. Het omvat ook de productwaarde voor de [!DNL Data Lake] in de `include` serie:

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

Wanneer [!DNL Experience Platform] een verwijderingsverzoek van [!DNL Privacy Service]ontvangt, [!DNL Platform] verzendt bevestiging aan [!DNL Privacy Service] dat het verzoek is ontvangen en de beïnvloede gegevens voor schrapping duidelijk zijn. De records worden vervolgens binnen zeven dagen uit de [!DNL Data Lake] bibliotheek verwijderd. Tijdens dat venster van zeven dagen, worden de gegevens zachte geschrapt en daarom niet toegankelijk door om het even welke [!DNL Platform] dienst.

In toekomstige versies [!DNL Platform] wordt een bevestiging verzonden naar [!DNL Privacy Service] nadat gegevens fysiek zijn verwijderd.

## Volgende stappen

Door dit document te lezen, bent u geïntroduceerd in de belangrijke concepten die betrekking hebben op het verwerken van privacyverzoeken voor het [!DNL Data Lake]. U wordt aangeraden de documentatie in deze handleiding te blijven lezen om meer inzicht te krijgen in de manier waarop u identiteitsgegevens kunt beheren en privacytaken kunt maken.

Zie het document over de verwerking van [privacyverzoeken voor Real-time klantprofiel](../profile/privacy.md) voor stappen over het verwerken van privacyverzoeken voor de [!DNL Profile] winkel.

## Aanhangsel

De volgende sectie bevat aanvullende informatie voor het verwerken van privacyverzoeken in de [!DNL Data Lake]sectie.

### Geneste toewijzingsvelden labelen {#nested-maps}

Het is belangrijk om op te merken dat er twee soorten genestelde kaart-type gebieden zijn die privacy het etiketteren niet steunen:

* Een toewijzingsveld binnen een veld van het type array
* Een veld van het type map binnen een ander veld van het type map

De verwerking van de privacytaak voor een van de twee bovenstaande voorbeelden zal uiteindelijk mislukken. Daarom wordt u aangeraden geneste kaartvelden niet te gebruiken om privéklantgegevens op te slaan. De relevante consument IDs zou als niet-kaartdatatype binnen het `identityMap` gebied (zelf een kaart-type gebied) voor op verslag-gebaseerde datasets, of het `endUserID` gebied voor op tijd-reeksen-gebaseerde datasets moeten worden opgeslagen.
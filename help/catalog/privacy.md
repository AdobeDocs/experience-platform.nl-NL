---
keywords: Experience Platform;thuis;populaire onderwerpen;gegevens meer privacy;identiteit namespaces;privacy;gegevens meer
solution: Experience Platform
title: De verwerking van het privacy- verzoek in het meer van Gegevens
topic: overview
description: Adobe Experience Platform Privacy Service verwerkt verzoeken van klanten om toegang te krijgen, te weigeren of hun persoonsgegevens te verwijderen, zoals bepaald in wettelijke en organisatorische privacyregels. Dit document behandelt essentiële concepten met betrekking tot het verwerken van privacyverzoeken voor klantgegevens die in het Datameer zijn opgeslagen.
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '1285'
ht-degree: 0%

---


# De verzoekverwerking van de privacy in [!DNL Data Lake]

Adobe Experience Platform [!DNL Privacy Service] verwerkt verzoeken van klanten om toegang te krijgen tot, zich uit verkoop te sluiten van, of hun persoonlijke gegevens te schrappen zoals bepaald door wettelijke en organisatorische privacyregels.

Dit document behandelt essentiële concepten met betrekking tot het verwerken van privacyverzoeken voor klantgegevens die zijn opgeslagen in [!DNL Data Lake].

## Aan de slag

U wordt aangeraden de volgende [!DNL Experience Platform]-services goed te begrijpen voordat u deze handleiding leest:

* [[!DNL Privacy Service]](../privacy-service/home.md): Beheert verzoeken van klanten om hun persoonlijke gegevens in Adobe Experience Cloud-toepassingen te openen, uit de handel te nemen of te verwijderen.
* [[!DNL Catalog Service]](home.md): The system of record for data location and lineage within  [!DNL Experience Platform]. Biedt een API die kan worden gebruikt om metagegevens van gegevenssets bij te werken.
* [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Experience Platform] klantenervaring worden georganiseerd.
* [[!DNL Identity Service]](../identity-service/home.md): Oplost de fundamentele uitdaging die door de fragmentatie van de gegevens van de klantenervaring wordt gesteld door identiteiten over apparaten en systemen te overbruggen.

## Naamruimten voor identiteiten {#namespaces}

Adobe Experience Platform [!DNL Identity Service] biedt een brug tussen identiteitsgegevens van klanten op verschillende systemen en apparaten. [!DNL Identity Service] gebruikt naamruimten om context aan identiteitswaarden te verstrekken door hen met hun systeem van oorsprong te verbinden. Een naamruimte kan een algemeen concept vertegenwoordigen, zoals een e-mailadres (&quot;e-mail&quot;) of de identiteit koppelen aan een specifieke toepassing, zoals een Adobe Advertising Cloud-id (&quot;AdCloud&quot;) of een Adobe Target-id (&quot;TNTID&quot;).

[!DNL Identity Service] onderhoudt een opslag van algemeen gedefinieerde (standaard) en door de gebruiker gedefinieerde (aangepaste) naamruimten. Standaard naamruimten zijn beschikbaar voor alle organisaties (bijvoorbeeld E-mail en ECID), terwijl uw organisatie aangepaste naamruimten kan maken die aan de specifieke behoeften voldoen.

Voor meer informatie over identiteitsnaamruimten in [!DNL Experience Platform], zie [identity namespace overzicht](../identity-service/namespaces.md).

## Identiteitsgegevens toevoegen aan gegevenssets

Bij het maken van privacyverzoeken voor de [!DNL Data Lake] moeten geldige identiteitswaarden (en de bijbehorende naamruimten) worden opgegeven voor elke individuele klant om de gegevens te kunnen vinden en deze dienovereenkomstig te kunnen verwerken. Daarom moeten alle datasets die aan privacyverzoeken onderworpen zijn een identiteitsbeschrijver in hun bijbehorend schema XDM bevatten.

>[!NOTE]
>
>Om het even welke datasets die op schema&#39;s worden gebaseerd die geen meta-gegevens van de identiteitsbeschrijver (zoals ad hoc datasets) steunen kunnen momenteel niet in privacyverzoeken worden verwerkt.

Deze sectie doorloopt de stappen om een identiteitsbeschrijver aan het XDM schema van een bestaande dataset toe te voegen. Als u reeds een dataset met een identiteitsbeschrijver hebt, kunt u naar [volgende sectie](#nested-maps) overslaan.

>[!IMPORTANT]
>
>Wanneer het beslissen welke schemagebieden om als identiteiten te plaatsen, houd in mening de [beperkingen om genestelde kaart-type gebieden](#nested-maps) te gebruiken.

Er zijn twee methodes om een identiteitsbeschrijver aan een datasetschema toe te voegen:

* [De gebruikersinterface gebruiken](#identity-ui)
* [De API gebruiken](#identity-api)

### UI {#identity-ui} gebruiken

In de [!DNL Experience Platform ]gebruikersinterface, **[!UICONTROL Schemas]** werkruimte staat u toe om uw bestaande schema&#39;s uit te geven XDM. Om een identiteitsbeschrijver aan een schema toe te voegen, selecteer het schema van de lijst en volg de stappen voor [plaatsend een schemagebied als identiteitsgebied](../xdm/tutorials/create-schema-ui.md#identity-field) in [!DNL Schema Editor] leerprogramma.

Als u de juiste velden in het schema hebt ingesteld als identiteitsvelden, kunt u doorgaan naar de volgende sectie over [het indienen van privacyverzoeken](#submit).

### API {#identity-api} gebruiken

>[!NOTE]
>
>Deze sectie veronderstelt u de unieke waarde van identiteitskaart van URI van het schema XDM van uw dataset kent. Als u deze waarde niet kent, kunt u deze ophalen met de API [!DNL Catalog Service]. Nadat u de sectie [Aan de slag](./api/getting-started.md) van de ontwikkelaarsgids hebt gelezen, volgt u de stappen die worden beschreven in voor [vermelding](./api/list-objects.md) of [opzoeken](./api/look-up-object.md) [!DNL Catalog] objecten om uw dataset te zoeken. De schema-id is te vinden onder `schemaRef.id`
>
> Deze sectie omvat vraag aan de Registratie API van het Schema. Voor belangrijke informatie met betrekking tot het gebruiken van API, met inbegrip van het kennen van uw `{TENANT_ID}` en het concept containers, zie [Aan de slag](../xdm/api/getting-started.md) sectie van de ontwikkelaarsgids.

U kunt een identiteitsbeschrijver aan het schema van XDM van een dataset toevoegen door een POST verzoek aan het `/descriptors` eindpunt in [!DNL Schema Registry] API te doen.

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
| `xdm:namespace` | Een van de [standaard naamruimten](../privacy-service/api/appendix.md#standard-namespaces) die wordt herkend door [!DNL Privacy Service], of een aangepaste naamruimte die is gedefinieerd door uw organisatie. |
| `xdm:property` | Ofwel &quot;xdm:id&quot; of &quot;xdm:code&quot;, afhankelijk van de naamruimte die onder `xdm:namespace` wordt gebruikt. |
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

## Verzoeken {#submit} verzenden

>[!NOTE]
>
>Deze sectie behandelt hoe te om privacyverzoeken voor [!DNL Data Lake] te formatteren. Het wordt sterk geadviseerd dat u [[!DNL Privacy Service] UI](../privacy-service/ui/overview.md) of [[!DNL Privacy Service] API](../privacy-service/api/getting-started.md) documentatie voor volledige stappen over hoe te om een privacybaan te voorleggen, met inbegrip van hoe te om verzonden gegevens van de gebruikersidentiteit in verzoeklading behoorlijk te formatteren.

In de volgende sectie wordt beschreven hoe u privacyverzoeken voor [!DNL Data Lake] kunt maken met de [!DNL Privacy Service]-interface of -API.

>[!IMPORTANT]
>
>De hoeveelheid tijd die een privacyverzoek kan duren om te voltooien, kan niet worden gegarandeerd. Als er zich wijzigingen voordoen in het datameer terwijl een aanvraag nog wordt verwerkt, kan ook niet worden gegarandeerd of die records al dan niet worden verwerkt.

### De gebruikersinterface gebruiken

Als u taakaanvragen maakt in de gebruikersinterface, moet u **[!UICONTROL AEP-gegevensmeer]** en/of **[!UICONTROL Profiel]** selecteren onder **[!UICONTROL Producten]** om taken te verwerken voor gegevens die zijn opgeslagen in respectievelijk [!DNL Data Lake] of [!DNL Real-time Customer Profile].

<img src="images/privacy/product-value.png" width="450"><br>

### De API gebruiken

Bij het maken van taakaanvragen in de API moeten `userIDs` die worden opgegeven, een specifieke `namespace` en `type` gebruiken, afhankelijk van de gegevensopslag waarop ze van toepassing zijn. Id&#39;s voor de [!DNL Data Lake] moeten &quot;niet-geregistreerd&quot; gebruiken voor hun `type`-waarde en een `namespace`-waarde die overeenkomt met een [privacylabel](#privacy-labels) die zijn toegevoegd aan de toepasselijke gegevenssets.

Daarnaast moet de `include`-array van de payload van het verzoek de productwaarden voor de verschillende gegevensopslagruimten bevatten waarop het verzoek wordt uitgevoerd. Bij het indienen van aanvragen bij [!DNL Data Lake] moet de array de waarde `aepDataLake` bevatten.

Met het volgende verzoek wordt een nieuwe privacytaak voor de naamruimte [!DNL Data Lake] gemaakt met behulp van de niet-geregistreerde naamruimte &quot;email_label&quot;. Het omvat ook de productwaarde voor [!DNL Data Lake] in `include` serie:

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

Wanneer [!DNL Experience Platform] een verwijderingsverzoek van [!DNL Privacy Service] ontvangt, verzendt [!DNL Platform] bevestiging aan [!DNL Privacy Service] dat het verzoek is ontvangen en de beïnvloede gegevens voor schrapping zijn duidelijk gemaakt. De records worden vervolgens binnen zeven dagen uit de [!DNL Data Lake] verwijderd. Tijdens dat venster van zeven dagen, worden de gegevens zachte geschrapt en zijn daarom niet toegankelijk door om het even welke [!DNL Platform] dienst.

In toekomstige releases zal [!DNL Platform] een bevestiging sturen naar [!DNL Privacy Service] nadat gegevens fysiek zijn verwijderd.

## Volgende stappen

Door dit document te lezen, bent u geïntroduceerd aan de belangrijke concepten betrokken bij de verwerking van privacyverzoeken voor [!DNL Data Lake]. U wordt aangeraden de documentatie in deze handleiding te blijven lezen om meer inzicht te krijgen in de manier waarop u identiteitsgegevens kunt beheren en privacytaken kunt maken.

Zie het document over [verwerking van privacyverzoeken voor Real-time klantprofiel](../profile/privacy.md) voor stappen over het verwerken van privacyverzoeken voor de [!DNL Profile]-winkel.

## Aanhangsel

De volgende sectie bevat aanvullende informatie voor het verwerken van privacyverzoeken in [!DNL Data Lake].

### Geneste toewijzingsvelden {#nested-maps} labelen

Het is belangrijk om op te merken dat er twee soorten genestelde kaart-type gebieden zijn die privacy het etiketteren niet steunen:

* Een toewijzingsveld binnen een veld van het type array
* Een veld van het type map binnen een ander veld van het type map

De verwerking van de privacytaak voor een van de twee bovenstaande voorbeelden zal uiteindelijk mislukken. Daarom wordt u aangeraden geneste kaartvelden niet te gebruiken om privéklantgegevens op te slaan. Relevante consumenten-id&#39;s moeten worden opgeslagen als een gegevenstype zonder toewijzing binnen het veld `identityMap` (zelf een toewijzingsveld) voor recordgebaseerde datasets, of het veld `endUserID` voor op tijdreeksen gebaseerde datasets.
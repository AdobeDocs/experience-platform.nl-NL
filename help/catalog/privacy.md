---
keywords: Experience Platform;thuis;populaire onderwerpen;gegevens meer privacy;identiteit namespaces;privacy;gegevens meer
solution: Experience Platform
title: De verwerking van het privacy- verzoek in het meer van Gegevens
topic-legacy: overview
description: Adobe Experience Platform Privacy Service verwerkt verzoeken van klanten om toegang te krijgen, te weigeren of hun persoonsgegevens te verwijderen, zoals bepaald in wettelijke en organisatorische privacyregels. Dit document behandelt essentiële concepten met betrekking tot het verwerken van privacyverzoeken voor klantgegevens die in het Datameer zijn opgeslagen.
exl-id: c06b0a44-be1a-4938-9c3e-f5491a3dfc19
source-git-commit: d8665a349c6f453d83b64317982f3544bbcde0f7
workflow-type: tm+mt
source-wordcount: '1374'
ht-degree: 1%

---

# Behandeling van een privacyverzoek in de [!DNL Data Lake]

Adobe Experience Platform [!DNL Privacy Service] verwerkt verzoeken van klanten om toegang, om zich uit verkoop te laten, of hun persoonsgegevens te schrappen zoals bepaald door wettelijke en organisatorische privacyregels.

Dit document behandelt essentiële concepten met betrekking tot de verwerking van privacyverzoeken voor klantgegevens die zijn opgeslagen in het [!DNL Data Lake].

>[!NOTE]
>
>In deze handleiding wordt alleen uitgelegd hoe u een verzoek om privacy kunt indienen voor het Data Lake in Experience Platform. Als u ook privacyverzoeken wilt indienen voor de gegevensopslag van het Profiel van de Klant in real time, raadpleegt u de handleiding op [verwerking van privacyverzoeken voor profiel](../profile/privacy.md) in aanvulling op deze zelfstudie.
>
>Raadpleeg voor meer informatie over het indienen van privacyverzoeken voor andere Adobe Experience Cloud-toepassingen de [Privacy Service](../privacy-service/experience-cloud-apps.md).

## Aan de slag

U wordt aangeraden het volgende goed te begrijpen: [!DNL Experience Platform] services vóór het lezen van deze handleiding:

* [[!DNL Privacy Service]](../privacy-service/home.md): Beheert verzoeken van klanten om hun persoonlijke gegevens in Adobe Experience Cloud-toepassingen te openen, uit de handel te nemen of te verwijderen.
* [[!DNL Catalog Service]](home.md): Het registratiesysteem voor gegevenslocatie en -lijn binnen [!DNL Experience Platform]. Biedt een API die kan worden gebruikt om metagegevens van gegevenssets bij te werken.
* [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
* [[!DNL Identity Service]](../identity-service/home.md): Oplost de fundamentele uitdaging die door de fragmentatie van de gegevens van de klantenervaring wordt gesteld door identiteiten over apparaten en systemen te overbruggen.

## Naamruimten voor identiteiten {#namespaces}

Adobe Experience Platform [!DNL Identity Service] brugt de gegevens van de klantenidentiteit over systemen en apparaten. [!DNL Identity Service] gebruikt naamruimten om context aan identiteitswaarden te verstrekken door hen met hun systeem van oorsprong te verbinden. Een naamruimte kan een algemeen concept vertegenwoordigen, zoals een e-mailadres (&quot;e-mail&quot;) of de identiteit koppelen aan een specifieke toepassing, zoals een Adobe Advertising Cloud-id (&quot;AdCloud&quot;) of een Adobe Target-id (&quot;TNTID&quot;).

[!DNL Identity Service] onderhoudt een opslag van algemeen gedefinieerde (standaard) en door de gebruiker gedefinieerde (aangepaste) naamruimten. Standaard naamruimten zijn beschikbaar voor alle organisaties (bijvoorbeeld E-mail en ECID), terwijl uw organisatie aangepaste naamruimten kan maken die aan de specifieke behoeften voldoen.

Voor meer informatie over naamruimten in [!DNL Experience Platform], zie de [Overzicht van naamruimte in identiteit](../identity-service/namespaces.md).

## Identiteitsgegevens toevoegen aan gegevenssets

Bij het maken van privacyverzoeken voor de [!DNL Data Lake], moeten geldige identiteitswaarden (en de bijbehorende naamruimten) worden verstrekt voor elke individuele klant om van hun gegevens de plaats te bepalen en het dienovereenkomstig te verwerken. Daarom moeten alle datasets die aan privacyverzoeken onderworpen zijn een identiteitsbeschrijver in hun bijbehorend schema XDM bevatten.

>[!NOTE]
>
>Om het even welke datasets die op schema&#39;s worden gebaseerd die geen meta-gegevens van de identiteitsbeschrijver (zoals ad hoc datasets) steunen kunnen momenteel niet in privacyverzoeken worden verwerkt.

Deze sectie doorloopt de stappen om een identiteitsbeschrijver aan het XDM schema van een bestaande dataset toe te voegen. Als u al een dataset met een identiteitsbeschrijver hebt, kunt u vooruit naar overslaan [volgende sectie](#nested-maps).

>[!IMPORTANT]
>
>Houd bij het bepalen van de schemavelden die u wilt instellen als id&#39;s rekening met de instelling [beperkingen van het gebruik van geneste kaarttekstvelden](#nested-maps).

Er zijn twee methodes om een identiteitsbeschrijver aan een datasetschema toe te voegen:

* [De gebruikersinterface gebruiken](#identity-ui)
* [De API gebruiken](#identity-api)

### De gebruikersinterface gebruiken {#identity-ui}

In de [!DNL Experience Platform ]de gebruikersinterface **[!UICONTROL Schemas]** kunt u uw bestaande XDM-schema&#39;s bewerken. Om een identiteitsbeschrijver aan een schema toe te voegen, selecteer het schema van de lijst en volg de stappen voor [een schemaveld instellen als een identiteitsveld](../xdm/tutorials/create-schema-ui.md#identity-field) in de [!DNL Schema Editor] zelfstudie.

Als u de juiste velden in het schema hebt ingesteld als identiteitsvelden, kunt u doorgaan naar de volgende sectie over [indienen van privacyverzoeken](#submit).

### De API gebruiken {#identity-api}

>[!NOTE]
>
>Deze sectie veronderstelt u de unieke waarde van identiteitskaart van URI van het schema XDM van uw dataset kent. Als u deze waarde niet kent, kunt u deze ophalen met de opdracht [!DNL Catalog Service] API. Na het lezen van de [aan de slag](./api/getting-started.md) in de handleiding voor ontwikkelaars de in [aanbieding](./api/list-objects.md) of [opzoeken](./api/look-up-object.md) [!DNL Catalog] objecten om uw gegevensset te zoeken. De schema-id is te vinden onder `schemaRef.id`
>
>Deze sectie veronderstelt ook dat u weet hoe te om vraag aan de Registratie API van het Schema te maken. Voor belangrijke informatie met betrekking tot het gebruik van de API, zoals het kennen van uw `{TENANT_ID}` en het begrip &quot;containers&quot;, zie [aan de slag](../xdm/api/getting-started.md) van de API-handleiding.

U kunt een identiteitsbeschrijver aan het schema van XDM van een dataset toevoegen door een verzoek van de POST aan het `/descriptors` in de [!DNL Schema Registry] API.

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
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `xdm:sourceVersion` | De versie van het XDM-schema die is opgegeven in `xdm:sourceSchema`. |
| `xdm:sourceProperty` | Het pad naar het schemaveld waarop de descriptor wordt toegepast. |
| `xdm:namespace` | Een van de [standaardnaamruimten](../privacy-service/api/appendix.md#standard-namespaces) erkend door [!DNL Privacy Service]of een aangepaste naamruimte die door uw organisatie is gedefinieerd. |
| `xdm:property` | Ofwel &quot;xdm:id&quot; of &quot;xdm:code&quot;, afhankelijk van de naamruimte die wordt gebruikt onder `xdm:namespace`. |
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
>In deze sectie wordt beschreven hoe u privacyverzoeken kunt opmaken voor de [!DNL Data Lake]. U wordt ten zeerste aangeraden de [[!DNL Privacy Service] UI](../privacy-service/ui/overview.md) of [[!DNL Privacy Service] API](../privacy-service/api/getting-started.md) documentatie voor volledige stappen over hoe te om een privacybaan voor te leggen, met inbegrip van hoe te om ingediende gegevens van de gebruikersidentiteit in verzoek te formatteren lading.

In het volgende gedeelte wordt beschreven hoe u privacyverzoeken kunt indienen voor de [!DNL Data Lake] met de [!DNL Privacy Service] UI of API.

>[!IMPORTANT]
>
>De hoeveelheid tijd die een privacyverzoek kan duren om te voltooien, kan niet worden gegarandeerd. Als er zich wijzigingen voordoen in het datameer terwijl een aanvraag nog wordt verwerkt, kan ook niet worden gegarandeerd of die records al dan niet worden verwerkt.

### De gebruikersinterface gebruiken

Zorg ervoor dat u bij het maken van taakaanvragen in de gebruikersinterface **[!UICONTROL AEP Data Lake]** en/of **[!UICONTROL Profile]** krachtens **[!UICONTROL Products]** om taken te verwerken voor gegevens die zijn opgeslagen in de [!DNL Data Lake] of [!DNL Real-time Customer Profile], respectievelijk.

<img src="images/privacy/product-value.png" width="450"><br>

### De API gebruiken

Bij het maken van taakaanvragen in de API worden alle `userIDs` die een specifieke `namespace` en `type` afhankelijk van de gegevensopslag waarop zij van toepassing zijn. Id&#39;s voor de [!DNL Data Lake] moet `unregistered` voor hun `type` en een `namespace` waarde die overeenkomt met een van de [privacylabels](#privacy-labels) die aan de toepasselijke gegevensbestanden zijn toegevoegd.

Bovendien `include` array van de aanvraag payload moet de productwaarden voor de verschillende gegevensopslagruimten bevatten waarnaar de aanvraag wordt verzonden. Bij het indienen van verzoeken aan de [!DNL Data Lake], moet de array de waarde bevatten `aepDataLake`.

Met de volgende aanvraag wordt een nieuwe privacytaak gemaakt voor de [!DNL Data Lake], met de niet-geregistreerde `email_label` naamruimte. Het omvat ook de productwaarde voor de [!DNL Data Lake] in de `include` array:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
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

>[!IMPORTANT]
>
>Platform verwerkt privacyverzoeken voor alle [sandboxen](../sandboxes/home.md) die deel uitmaken van uw organisatie. Dientengevolge, om het even welke `x-sandbox-name` header die in de aanvraag is opgenomen, wordt genegeerd door het systeem.

## Verzoek om verwerking verwijderen

Wanneer [!DNL Experience Platform] ontvangt een verwijderingsverzoek van [!DNL Privacy Service], [!DNL Platform] stuurt bevestiging naar [!DNL Privacy Service] dat het verzoek is ontvangen en de betrokken gegevens zijn gemarkeerd voor verwijdering. De records worden vervolgens verwijderd uit de [!DNL Data Lake] binnen zeven dagen. Tijdens dat venster van zeven dagen worden de gegevens via de elektronische weg verwijderd en zijn ze daarom door niemand toegankelijk [!DNL Platform] service.

In toekomstige versies [!DNL Platform] stuurt bevestiging naar [!DNL Privacy Service] nadat de gegevens fysiek zijn verwijderd.

## Volgende stappen

Door dit document te lezen, bent u geïntroduceerd in de belangrijke concepten die betrekking hebben op het verwerken van privacyverzoeken voor de [!DNL Data Lake]. U wordt aangeraden de documentatie in deze handleiding te blijven lezen om meer inzicht te krijgen in de manier waarop u identiteitsgegevens kunt beheren en privacytaken kunt maken.

Document weergeven op [verwerking van privacyverzoeken voor realtime klantprofiel](../profile/privacy.md) voor stappen in de verwerking van privacyverzoeken voor de [!DNL Profile] opslaan.

## Aanhangsel

De volgende sectie bevat aanvullende informatie voor de verwerking van privacyverzoeken in het dialoogvenster [!DNL Data Lake].

### Geneste toewijzingsvelden labelen {#nested-maps}

Het is belangrijk om op te merken dat er twee soorten genestelde kaart-type gebieden zijn die privacy het etiketteren niet steunen:

* Een toewijzingsveld binnen een veld van het type array
* Een veld van het type map binnen een ander veld van het type map

De verwerking van de privacytaak voor een van de twee bovenstaande voorbeelden zal uiteindelijk mislukken. Daarom wordt u aangeraden geneste kaartvelden niet te gebruiken om privéklantgegevens op te slaan. Relevante consumenten-id&#39;s moeten worden opgeslagen als een niet-kaartgegevenstype binnen de `identityMap` het gebied (zelf een kaart-type gebied) voor op verslag-gebaseerde datasets, of `endUserID` veld voor op tijdreeksen gebaseerde gegevenssets.

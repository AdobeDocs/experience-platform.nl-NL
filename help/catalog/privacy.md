---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Behandeling van een privacyverzoek in het Data Lake
topic: overview
translation-type: tm+mt
source-git-commit: 5f0e0deb4a2fae636ac4d2313a6541c25309c294

---


# Behandeling van een privacyverzoek in het Data Lake

De privacydienst van het Platform van de Privacy van Adobe verwerkt klantenverzoeken om tot toegang te hebben, uit verkoop te kiezen, of hun persoonlijke gegevens te schrappen zoals die door privacyverordeningen zoals de Algemene Verordening van de Bescherming van Gegevens (GDPR) en de Wet van de Consumeprivacydienst van Californië (CCPA) worden afgebakend.

Dit document behandelt essentiële concepten met betrekking tot het verwerken van privacyverzoeken voor klantgegevens die in het Datameer zijn opgeslagen.

## Aan de slag

U wordt aangeraden een goed begrip te hebben van de volgende services van het Experience Platform voordat u deze handleiding leest:

* [Privacy-service](../privacy-service/home.md): Beheert verzoeken van klanten om hun persoonlijke gegevens in Adobe Experience Cloud-toepassingen te openen, niet te verkopen of te verwijderen.
* [Catalogusservice](home.md): Het registratiesysteem voor gegevenslocatie en gegevenskoppeling binnen het ervaringsplatform. Biedt een API die kan worden gebruikt om metagegevens van gegevenssets bij te werken.
* [XDM-systeem](../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Platform van de Ervaring gegevens van de klantenervaring organiseert.

## Privacy-labels toevoegen aan gegevenssets {#privacy-labels}

Om een dataset in een privacyverzoek voor het meer van Gegevens te verwerken, moet de dataset privacyetiketten worden gegeven. De etiketten van de privacy wijzen op welke gebieden binnen het bijbehorende schema van een dataset op namespaces van toepassing zijn u om in privacyverzoeken verwacht te worden verzonden.

Deze sectie toont aan hoe te om privacyetiketten aan een dataset voor gebruik in de privacyverzoeken van het meer van Gegevens toe te voegen. Om te beginnen, overweeg de volgende dataset:

```json
{
    "5d8e9cf5872f18164763f971": {
        "name": "Loyalty Members",
        "description": "Dataset for the Loyalty Members schema",
        "imsOrg": "{IMS_ORG}",
        "tags": {
            "adobe/pqs/table": [
                "loyalty_members"
            ]
        },
        "namespace": "ACP",
        "state": "DRAFT",
        "id": "5d8e9cf5872f18164763f971",
        "dule": {
            "identity": [],
            "contract": [
                "C2",
                "C5"
            ],
            "sensitive": [],
            "contracts": [
                "C2",
                "C5"
            ],
            "identifiability": [],
            "specialTypes": []
        },
        "version": "1.0.2",
        "created": 1569627381749,
        "updated": 1569880723282,
        "createdClient": "acp_ui_platform",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "viewId": "5d8e9cf5872f18164763f972",
        "aspect": "production",
        "status": "enabled",
        "fileDescription": {
            "persisted": true,
            "containerFormat": "parquet",
            "format": "parquet"
        },
        "files": "@/dataSets/5d8e9cf5872f18164763f971/views/5d8e9cf5872f18164763f972/files",
        "schemaMetadata": {
            "primaryKey": [],
            "delta": [],
            "dule": [
                {
                    "path": "/properties/personalEmail/properties/address",
                    "identity": [
                        "I1"
                    ],
                    "contract": [],
                    "sensitive": [],
                    "contracts": [],
                    "identifiability": [
                        "I1"
                    ],
                    "specialTypes": []
                }
            ],
            "gdpr": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    }
}
```

De `schemaMetadata` eigenschap voor de dataset bevat een `gdpr` array, die momenteel leeg is. Om privacyetiketten aan de dataset toe te voegen, moet deze serie worden bijgewerkt gebruikend een verzoek van de PATCH aan de [Dienst API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)van de Catalogus.

>[!NOTE] Hoewel de array een naam heeft `gdpr`, kan door het toevoegen van labels aan de array privacytaakaanvragen worden gedaan voor zowel GDPR- als CCPA-regels.

**API-indeling**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATASET_ID}` | De `id` waarde van de gegevensset die moet worden bijgewerkt. |

**Verzoek**

In dit voorbeeld bevat een gegevensset een e-mailadres in het `personalEmail.address` veld. Om ervoor te zorgen dat dit veld als id fungeert voor privacyverzoeken bij Data Lake, moet een label dat een niet-geregistreerde naamruimte gebruikt, worden toegevoegd aan de `gdpr` array.

Met de volgende aanvraag wordt een privacylabel toegevoegd dat de naamruimte &quot;email_label&quot; toewijst aan het `personalEmail.address` veld.

>[!IMPORTANT] Wanneer het runnen van een verrichting van de PATCH op het `schemaMetadata` bezit van een dataset, ben zeker om het even welke bestaande sub-eigenschappen binnen de verzoeklading te kopiëren. Als u bestaande waarden niet in de payload opneemt, worden deze verwijderd uit de gegevensset.

```shell
curl -X PATCH 'https://platform.adobe.io/data/foundation/catalog/dataSets/5d8e9cf5872f18164763f971' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{ 
    "schemaMetadata": { 
      "primaryKey": [],
      "delta": [],
      "dule": [
        {
          "path": "/properties/personalEmail/properties/address",
          "identity": [
              "I1"
          ],
          "contract": [],
          "sensitive": [],
          "contracts": [],
          "identifiability": [
              "I1"
          ],
          "specialTypes": []
        }
      ],
      "gdpr": [
          {
              "namespace": ["email_label"],
              "path": "/properties/personalEmail/properties/address"
          }
      ]
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `namespace` | Een array met de naamruimte(n) die moet worden gekoppeld aan het veld dat is opgegeven in `path`. Naamruimten worden gebruikt om privacygerelateerde velden te identificeren wanneer toegang wordt [verzonden of aanvragen](#submit) worden verwijderd in de API voor de privacyservice. |
| `path` | De weg aan het gebied binnen het bijbehorende schema van de dataset dat op `namespace`van toepassing is. In het ideale geval mogen privacylabels alleen worden toegepast op bladvelden (velden zonder subvelden). |

**Antwoord**

Een succesvolle reactie keert HTTP status 200 (O.K.) met identiteitskaart van de dataset terug die in de nuttige lading wordt verstrekt. Het gebruiken van identiteitskaart om de dataset opnieuw op te zoeken onthult dat de privacyetiketten zijn toegevoegd.

```json
[
    "@/dataSets/5d8e9cf5872f18164763f971"
]
```

### Geneste toewijzingsvelden labelen

Het is belangrijk om op te merken dat er twee soorten genestelde kaart-type gebieden zijn die privacy het etiketteren niet steunen:

* Een toewijzingsveld binnen een veld van het type array
* Een veld van het type map binnen een ander veld van het type map

De verwerking van de privacytaak voor een van de twee bovenstaande voorbeelden zal uiteindelijk mislukken. Daarom wordt u aangeraden geneste kaartvelden niet te gebruiken om privéklantgegevens op te slaan. De relevante consument IDs zou als niet-kaartdatatype binnen het `identityMap` gebied (zelf een kaart-type gebied) voor op verslag-gebaseerde datasets, of het `endUserID` gebied voor op tijd-reeksen-gebaseerde datasets moeten worden opgeslagen.

## Verzoeken indienen {#submit}

>[!NOTE] Deze sectie behandelt hoe te om privacyverzoeken voor het meer van Gegevens te formatteren. Het wordt ten zeerste aanbevolen dat u de API [-documentatie](../privacy-service/api/getting-started.md) van de [privacyservice of de gebruikersinterface](../privacy-service/ui/overview.md) van deprivacyservice controleert voor volledige stappen over het verzenden van een privacytaak, waaronder het correct indelen van verzonden identiteitsgegevens van gebruikers in aanvragen.

In de volgende sectie wordt beschreven hoe u privacyaanvragen voor het gegevensmeer kunt indienen met de API of UI van de privacyservice.

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

### De gebruikersinterface gebruiken

Wanneer het creëren van baanverzoeken in UI, ben zeker om **AEP Gegevensmeer** en/of **Profiel** onder _Producten_ te selecteren om banen voor gegevens te verwerken die in het meer van Gegevens of in real time het Profiel van de Klant worden opgeslagen.

<img src="images/privacy/product-value.png" width="450"><br>

## Verzoek om verwerking verwijderen

Wanneer het Platform van de Ervaring een schrappingsverzoek van de Dienst van de Privacy ontvangt, verzendt het Platform bevestiging aan de Dienst van de Privacy dat het verzoek is ontvangen en de beïnvloede gegevens voor schrapping duidelijk zijn gemaakt. De gegevens worden vervolgens binnen zeven dagen uit het Data Lake verwijderd. Tijdens dat venster van zeven dagen, worden de gegevens zachte geschrapt en daarom niet toegankelijk door om het even welke dienst van het Platform.

In toekomstige releases zal Platform een bevestiging sturen naar de Privacy Service nadat de gegevens fysiek zijn verwijderd.

## Volgende stappen

Door dit document te lezen, bent u geïntroduceerd aan de belangrijke concepten betrokken bij de verwerking van privacyverzoeken voor het meer van Gegevens. U wordt aangeraden de documentatie in deze handleiding te blijven lezen om meer inzicht te krijgen in de manier waarop u identiteitsgegevens kunt beheren en privacytaken kunt maken.

Zie het document over de verwerking van [privacyverzoeken voor Real-time klantprofiel](../profile/privacy.md) voor stappen over het verwerken van privacyverzoeken voor het archief van het Profiel.
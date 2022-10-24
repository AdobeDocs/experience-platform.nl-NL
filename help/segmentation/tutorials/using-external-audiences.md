---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Extern publiek importeren en gebruiken
description: Volg deze zelfstudie om te leren hoe u externe doelgroepen kunt gebruiken met Adobe Experience Platform.
topic-legacy: tutorial
exl-id: 56fc8bd3-3e62-4a09-bb9c-6caf0523f3fe
source-git-commit: 13fd1e372a63b55c41893f41d1590d9dab9f7903
workflow-type: tm+mt
source-wordcount: '1406'
ht-degree: 0%

---

# Extern publiek importeren en gebruiken

Adobe Experience Platform ondersteunt de mogelijkheid om extern publiek te importeren. Dit kan vervolgens worden gebruikt als componenten voor een nieuwe segmentdefinitie. Dit document bevat een zelfstudie voor het instellen van een Experience Platform voor het importeren en gebruiken van externe doelgroepen.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de verschillende [!DNL Adobe Experience Platform] de diensten betrokken bij het creëren van publiekssegmenten. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [Segmenteringsservice](../home.md): Staat u toe om publiekssegmenten van de gegevens van het Profiel van de Klant in real time te bouwen.
- [Klantprofiel in realtime](../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [Experience Data Model (XDM)](../../xdm/home.md): Het gestandaardiseerde kader waardoor het Platform gegevens van de klantenervaring organiseert. Als u de segmentatie het beste wilt gebruiken, moet u ervoor zorgen dat uw gegevens als profielen en gebeurtenissen worden opgenomen volgens de [best practices voor gegevensmodellering](../../xdm/schema/best-practices.md).
- [Gegevenssets](../../catalog/datasets/overview.md): De opslag- en beheerconstructie voor gegevenspersistentie in Experience Platform.
- [Streaming opname](../../ingestion/streaming-ingestion/overview.md): Hoe Experience Platform gegevens van client- en server-side apparaten in real-time opneemt en opslaat.

### Segmentgegevens vs segmentmetagegevens

Voordat u begint met het importeren en gebruiken van externe doelgroepen, is het belangrijk dat u het verschil begrijpt tussen segmentgegevens en segmentmetagegevens.

Segmentgegevens verwijzen naar de profielen die voldoen aan de kwalificatiecriteria van het segment en daarom deel uitmaken van het publiek.

De meta-gegevens van het segment zijn informatie over het segment zelf, die de naam, de beschrijving, de uitdrukking (indien van toepassing), de aanmaakdatum, de laatste gewijzigde datum, en identiteitskaart omvat. De id koppelt de segmentmetagegevens aan de afzonderlijke profielen die voldoen aan de segmentkwalificatie en die deel uitmaken van het resulterende publiek.

| Segmentgegevens | Metagegevens segment |
| ------------ | ---------------- |
| Profielen die voldoen aan de segmentkwalificatie | Informatie over het segment zelf |

## Een naamruimte voor identiteit maken voor het externe publiek

De eerste stap voor het gebruik van externe doelgroepen is het maken van een naamruimte voor identiteiten. Identiteitsnaamruimten maken het Platform mogelijk te koppelen van waaruit een segment afkomstig is.

Volg de instructies in het dialoogvenster [Naamruimtehulplijn voor identiteit](../../identity-service/namespaces.md#manage-namespaces). Wanneer u uw naamruimte voor identiteit maakt, voegt u de brongegevens toe aan de naamruimte voor identiteit en markeert u de naamruimte [!UICONTROL Type] als **[!UICONTROL Non-people identifier]**.

![](../images/tutorials/external-audiences/identity-namespace-info.png)

## Een schema maken voor de metagegevens van het segment

Nadat u een naamruimte voor identiteiten hebt gemaakt, moet u een nieuw schema maken voor het segment dat u wilt maken.

Als u wilt beginnen met het samenstellen van een schema, selecteert u eerst **[!UICONTROL Schemas]** op de linkernavigatiebalk, gevolgd door de **[!UICONTROL Create schema]** in de rechterbovenhoek van de werkruimte Schemas. Selecteer **[!UICONTROL Browse]** om een volledige selectie van de beschikbare schematypen te zien.

![](../images/tutorials/external-audiences/create-schema-browse.png)

Aangezien u een segmentdefinitie maakt, die een vooraf gedefinieerde klasse is, selecteert u **[!UICONTROL Use existing class]**. Selecteer nu de **[!UICONTROL Segment definition]** klasse, gevolgd door **[!UICONTROL Assign class]**.

![](../images/tutorials/external-audiences/assign-class.png)

Nu uw schema is gecreeerd, zult u moeten specificeren welk gebied segmentidentiteitskaart zal bevatten. Dit veld moet worden gemarkeerd als de primaire identiteit en worden toegewezen aan de naamruimten die u eerder hebt gemaakt.

![](../images/tutorials/external-audiences/mark-primary-identifier.png)

Na het markeren van `_id` veld als primaire identiteit, selecteer de titel van het schema, gevolgd door de schakeloptie met het label **[!UICONTROL Profile]**. Selecteren **[!UICONTROL Enable]** om het schema in te schakelen voor [!DNL Real-time Customer Profile].

![](../images/tutorials/external-audiences/schema-profile.png)

Dit schema is nu ingeschakeld voor Profiel, waarbij de primaire identificatie is toegewezen aan de naamruimte voor niet-persoonlijke identiteit die u hebt gemaakt. Dientengevolge, betekent dit dat de segmentmeta-gegevens die in Platform worden ingevoerd gebruikend dit schema in Profiel zullen worden opgenomen zonder met andere op mensen betrekking hebbende gegevens van het Profiel worden samengevoegd.

## Creeer een dataset voor het schema

Na het vormen van het schema, zult u een dataset voor de segmentmeta-gegevens moeten tot stand brengen.

Om een dataset tot stand te brengen, volg de instructies in [gebruikershandleiding voor gegevenssets](../../catalog/datasets/user-guide.md#create). U moet de **[!UICONTROL Create dataset from schema]** met het eerder gemaakte schema.

![](../images/tutorials/external-audiences/select-schema.png)

Na het creëren van de dataset, volg de instructies in [gebruikershandleiding voor gegevenssets](../../catalog/datasets/user-guide.md#enable-profile) om deze dataset voor het Profiel van de Klant in real time toe te laten.

![](../images/tutorials/external-audiences/dataset-profile.png)

## Gebruikersgegevens instellen en importeren

Met toegelaten dataset, kunnen de gegevens nu naar Platform of door UI of het gebruiken van Experience Platform APIs worden verzonden. U kunt deze gegevens via een batch- of streamingverbinding invoeren.

### Gegevens opnemen met een batchverbinding

Als u een batchverbinding wilt maken, volgt u de instructies in het algemene [UI-gids voor het uploaden van lokale bestanden](../../sources/tutorials/ui/create/local-system/local-file-upload.md). Voor een volledige lijst van beschikbare bronnen die u kunt gebruiken binnenste gegevens met, te lezen gelieve [overzicht van bronnen](../../sources/home.md).

### Gegevens verzamelen met behulp van een streamingverbinding

Als u een streamingverbinding wilt maken, volgt u de instructies in het dialoogvenster [API-zelfstudie](../../sources/tutorials/api/create/streaming/http.md) of de [UI-zelfstudie](../../sources/tutorials/ui/create/streaming/http.md).

Nadat u een streamingverbinding hebt gemaakt, hebt u toegang tot het unieke streamingeindpunt waarnaar u de gegevens kunt verzenden. Als u wilt weten hoe u gegevens naar deze eindpunten verzendt, leest u de [zelfstudie over streaming recordgegevens](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Structuur van metagegevens voor het publiek

Nadat u een verbinding hebt gemaakt, kunt u uw gegevens nu aan het Platform toevoegen.

Hieronder ziet u een voorbeeld van de metagegevens van de externe doelgroep:

```json
{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample External Audience"
        }
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "xdmEntity": {
            "_id": "{SEGMENT_ID}",
            "description": "Sample description",
            "identityMap": {
                "{IDENTITY_NAMESPACE}": [{
                    "id": "{}"
                }]
            },
            "segmentName" : "{SEGMENT_NAME}",
            "segmentStatus": "ACTIVE",
            "version": "1.0"
        }
    }
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `schemaRef` | Het schema **moet** verwijs naar het eerder gecreeerd schema voor de segmentmeta-gegevens. |
| `datasetId` | De gegevensset-id **moet** verwijs naar de eerder gecreeerde dataset voor het schema u enkel creeerde. |
| `xdmEntity._id` | De id **moet** verwijs naar zelfde segment identiteitskaart u als uw extern publiek gebruikt. |
| `xdmEntity.identityMap` | Deze sectie **moet** bevat het identiteitslabel dat wordt gebruikt bij het maken van de eerder gemaakte naamruimte. |
| `{IDENTITY_NAMESPACE}` | Dit is het label van de eerder gemaakte naamruimte voor identiteit. Als u bijvoorbeeld uw naamruimte ExternalAudience hebt aangeroepen, gebruikt u die als de sleutel van de array. |
| `segmentName` | De naam van het segment waarop u het externe publiek wilt segmenteren. |

## Segmenten samenstellen met behulp van geïmporteerde soorten publiek

Zodra het geïmporteerde publiek is ingesteld, kunnen deze worden gebruikt als onderdeel van het segmenteringsproces. Ga naar de Segment Builder en selecteer **[!UICONTROL Audiences]** in de **[!UICONTROL Fields]** sectie.

![](../images/tutorials/external-audiences/external-audiences.png)

## Volgende stappen

Nu u externe doelgroepen in uw segmenten kunt gebruiken, kunt u de Bouwer van het Segment gebruiken om segmenten tot stand te brengen. Als u wilt leren hoe u segmenten maakt, leest u de [zelfstudie over het maken van segmenten](./create-a-segment.md).

## Aanhangsel

Naast het gebruiken van ingevoerde externe publieksmeta-gegevens en het gebruiken van hen voor het creëren van segmenten, kunt u externe segmentlidmaatschap aan Platform ook invoeren.

### Een extern bestemmingsschema voor een segmentlidmaatschap instellen

Als u wilt beginnen met het samenstellen van een schema, selecteert u eerst **[!UICONTROL Schemas]** op de linkernavigatiebalk, gevolgd door de **[!UICONTROL Create schema]** in de rechterbovenhoek van de werkruimte Schemas. Selecteer **[!UICONTROL XDM Individual Profile]**.

![](../images/tutorials/external-audiences/create-schema-profile.png)

Nu het schema is gecreeerd, zult u de het gebiedsgroep van het segmentlidmaatschap als deel van het schema moeten toevoegen. Selecteer [!UICONTROL Segment Membership Details], gevolgd door [!UICONTROL Add field groups].

![](../images/tutorials/external-audiences/segment-membership-details.png)

Zorg er bovendien voor dat het schema is gemarkeerd voor **[!UICONTROL Profile]**. Hiervoor moet u een veld markeren als de primaire identiteit.

![](../images/tutorials/external-audiences/external-segment-profile.png)

### De gegevensset instellen

Na het creëren van uw schema, zult u een dataset moeten creëren.

Om een dataset tot stand te brengen, volg de instructies in [gebruikershandleiding voor gegevenssets](../../catalog/datasets/user-guide.md#create). U moet de **[!UICONTROL Create dataset from schema]** met het eerder gemaakte schema.

![](../images/tutorials/external-audiences/select-schema.png)

Na het creëren van de dataset, volg de instructies in [gebruikershandleiding voor gegevenssets](../../catalog/datasets/user-guide.md#enable-profile) om deze dataset voor het Profiel van de Klant in real time toe te laten.

![](../images/tutorials/external-audiences/dataset-profile.png)

## Externe gegevens voor publieksleden instellen en importeren

Met toegelaten dataset, kunnen de gegevens nu naar Platform of door UI of het gebruiken van Experience Platform APIs worden verzonden. U kunt deze gegevens via een batch- of streamingverbinding invoeren.

### Gegevens opnemen met een batchverbinding

Als u een batchverbinding wilt maken, volgt u de instructies in het algemene [UI-gids voor het uploaden van lokale bestanden](../../sources/tutorials/ui/create/local-system/local-file-upload.md). Voor een volledige lijst van beschikbare bronnen die u kunt gebruiken binnenste gegevens met, te lezen gelieve [overzicht van bronnen](../../sources/home.md).

### Gegevens verzamelen met behulp van een streamingverbinding

Als u een streamingverbinding wilt maken, volgt u de instructies in het dialoogvenster [API-zelfstudie](../../sources/tutorials/api/create/streaming/http.md) of de [UI-zelfstudie](../../sources/tutorials/ui/create/streaming/http.md).

Nadat u een streamingverbinding hebt gemaakt, hebt u toegang tot het unieke streamingeindpunt waarnaar u de gegevens kunt verzenden. Als u wilt weten hoe u gegevens naar deze eindpunten verzendt, leest u de [zelfstudie over streaming recordgegevens](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Segmentlidmaatschapsstructuur

Nadat u een verbinding hebt gemaakt, kunt u uw gegevens nu aan het Platform toevoegen.

Hieronder ziet u een voorbeeld van de downloadbelasting voor het externe publiek:

```json
{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample External Audience Membership"
        }
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "xdmEntity": {
            "_id": "{UNIQUE_ID}",
            "description": "Sample description",
            "{TENANT_NAME}": {
                "identities": {
                    "{SCHEMA_IDENTITY}": "sample-id"
                }
            },
            "personId" : "sample-name",
            "segmentMembership": {
                "{IDENTITY_NAMESPACE}": {
                    "{EXTERNAL_IDENTITY}": {
                        "status": "realized",
                        "lastQualificationTime": "2022-03-14T:00:00:00Z"
                    }
                }
            }
        }
    }
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `schemaRef` | Het schema **moet** verwijs naar het eerder gecreeerd schema voor de gegevens van het segmentlidmaatschap. |
| `datasetId` | De gegevensset-id **moet** verwijs naar de eerder gecreeerde dataset voor het lidmaatschapsschema u enkel creeerde. |
| `xdmEntity._id` | Een geschikte id die wordt gebruikt om de record in de gegevensset op unieke wijze te identificeren. |
| `{TENANT_NAME}.identities` | Deze sectie wordt gebruikt om de het gebiedsgroep van douaneidentiteiten met de gebruikers te verbinden u eerder invoerde. |
| `segmentMembership.{IDENTITY_NAMESPACE}` | Dit is het label van de eerder gemaakte naamruimte voor aangepaste identiteit. Als u bijvoorbeeld uw naamruimte ExternalAudience hebt aangeroepen, gebruikt u die als de sleutel van de array. |
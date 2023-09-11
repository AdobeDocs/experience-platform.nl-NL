---
solution: Experience Platform
title: Extern publiek importeren en gebruiken
description: Volg deze zelfstudie om te leren hoe u externe doelgroepen kunt gebruiken met Adobe Experience Platform.
exl-id: 56fc8bd3-3e62-4a09-bb9c-6caf0523f3fe
hide: true
hidefromtoc: true
source-git-commit: c83070d85177c72b2e4c4ae472b89c08c20ee743
workflow-type: tm+mt
source-wordcount: '1683'
ht-degree: 0%

---

# Extern publiek importeren en gebruiken

>[!IMPORTANT]
>
>Deze documentatie bevat informatie uit een vorige versie van de documentatie van het publiek en is daarom verouderd.

Adobe Experience Platform ondersteunt de mogelijkheid om extern publiek te importeren. Dit kan vervolgens worden gebruikt als componenten voor een nieuw publiek. Dit document bevat een zelfstudie voor het instellen van een Experience Platform voor het importeren en gebruiken van externe doelgroepen.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de verschillende [!DNL Adobe Experience Platform] diensten die betrokken zijn bij het creëren van een publiek. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [Segmenteringsservice](../home.md): Hiermee kunt u een publiek maken op basis van realtime gegevens in het klantprofiel.
- [Klantprofiel in realtime](../../profile/home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.
- [Experience Data Model (XDM)](../../xdm/home.md): Het gestandaardiseerde kader waardoor Platform gegevens van de klantenervaring organiseert. Als u de segmentatie het beste wilt gebruiken, moet u ervoor zorgen dat uw gegevens als profielen en gebeurtenissen worden opgenomen volgens de [best practices voor gegevensmodellering](../../xdm/schema/best-practices.md).
- [Gegevenssets](../../catalog/datasets/overview.md): De opslag- en beheerconstructie voor gegevenspersistentie in Experience Platform.
- [Streaming opname](../../ingestion/streaming-ingestion/overview.md): Hoe Experience Platform gegevens van client- en server-side apparaten in real-time opneemt en opslaat.

### Publiek versus segmentdefinities

Voordat u begint met het importeren en gebruiken van externe doelgroepen, is het belangrijk dat u het verschil begrijpt tussen publiek- en segmentdefinities.

Het publiek verwijst naar de groep profielen waarnaar u probeert te filteren. Wanneer het gebruiken van segmentdefinities, kunt u een publiek tot stand brengen door een segmentdefinitie te creëren die uw profielen aan de ondergroep filtert die aan de criteria van de segmentkwalificatie voldoet.

Segmentdefinities bevatten informatie zoals de naam, beschrijving, expressie (indien van toepassing), de aanmaakdatum, de laatst gewijzigde datum en een id. De id koppelt de segmentmetagegevens aan de afzonderlijke profielen die voldoen aan de segmentkwalificatie en die deel uitmaken van het resulterende publiek.

| Doelgroepen | Segmentdefinitie |
| --------- | ---------------- |
| De groep profielen die u zoekt. Wanneer het gebruiken van segmentdefinities, betekent dit dat het de groep profielen zal zijn die segmentkwalificatie ontmoeten. | De groep regels gebruikte om het publiek te segmenteren u zoekt. |

## Een naamruimte voor identiteit maken voor het externe publiek

De eerste stap voor het gebruik van externe doelgroepen is het maken van een naamruimte voor identiteiten. Met naamruimten kan Platform aangeven waar een publiek vandaan komt.

Volg de instructies in het dialoogvenster [Naamruimtehulplijn voor identiteit](../../identity-service/namespaces.md#manage-namespaces). Wanneer u uw naamruimte voor identiteit maakt, voegt u de brongegevens toe aan de naamruimte voor identiteit en markeert u de naamruimte [!UICONTROL Type] als **[!UICONTROL Non-people identifier]**.

![De id van de niet-persoon wordt gemarkeerd in het modaal van de naamruimte Naam maken.](../images/tutorials/external-audiences/identity-namespace-info.png)

## Een schema maken voor de metagegevens van het segment

Nadat u een naamruimte voor identiteiten hebt gemaakt, moet u een nieuw schema maken voor het segment dat u wilt maken.

Als u een schema wilt samenstellen, selecteert u eerst **[!UICONTROL Schemas]** op de linkernavigatiebalk, gevolgd door de **[!UICONTROL Create schema]** in de rechterbovenhoek van de werkruimte Schemas. Van hier, selecteer **[!UICONTROL Browse]** om een volledige selectie van de beschikbare schematypen te zien.

![Zowel creeer schema als doorbladert worden benadrukt.](../images/tutorials/external-audiences/create-schema-browse.png)

Aangezien u een segmentdefinitie maakt, die een vooraf gedefinieerde klasse is, selecteert u **[!UICONTROL Use existing class]**. Selecteer nu de **[!UICONTROL Segment definition]** klasse, gevolgd door **[!UICONTROL Assign class]**.

![De segmentdefinitieklasse wordt gemarkeerd.](../images/tutorials/external-audiences/assign-class.png)

Nu uw schema is gecreeerd, zult u moeten specificeren welk gebied segmentidentiteitskaart zal bevatten. Dit veld moet worden gemarkeerd als de primaire identiteit en worden toegewezen aan de naamruimten die u eerder hebt gemaakt.

![De selectievakjes om het geselecteerde veld als de primaire identiteit te markeren, worden gemarkeerd in de Schema-editor.](../images/tutorials/external-audiences/mark-primary-identifier.png)

Nadat u het `_id` veld als primaire identiteit, selecteer de titel van het schema, gevolgd door de schakeloptie met het label **[!UICONTROL Profile]**. Selecteren **[!UICONTROL Enable]** om het schema voor [!DNL Real-Time Customer Profile].

![De knevel om het schema voor Profiel toe te laten wordt benadrukt in de Redacteur van het Schema.](../images/tutorials/external-audiences/schema-profile.png)

Dit schema is nu ingeschakeld voor Profiel, waarbij de primaire identificatie is toegewezen aan de naamruimte voor niet-persoonlijke identiteit die u hebt gemaakt. Dientengevolge, betekent dit dat de segmentmeta-gegevens die in Platform worden ingevoerd gebruikend dit schema in Profiel zullen worden opgenomen zonder met andere op mensen betrekking hebbende gegevens van het Profiel worden samengevoegd.

## Creeer een dataset voor het schema

Na het vormen van het schema, zult u een dataset voor de segmentmeta-gegevens moeten tot stand brengen.

Om een dataset tot stand te brengen, volg de instructies in [gebruikershandleiding voor gegevenssets](../../catalog/datasets/user-guide.md#create). U moet de **[!UICONTROL Create dataset from schema]** met het eerder gemaakte schema.

![Het schema dat u uw dataset wilt baseren wordt benadrukt.](../images/tutorials/external-audiences/select-schema.png)

Na het creëren van de dataset, volg de instructies in [gebruikershandleiding voor gegevenssets](../../catalog/datasets/user-guide.md#enable-profile) om deze dataset voor het Profiel van de Klant in real time toe te laten.

![De knevel om het schema voor Profiel toe te laten wordt benadrukt in de de activiteitenpagina van de Dataset.](../images/tutorials/external-audiences/dataset-profile.png)

## Gebruikersgegevens instellen en importeren

Met toegelaten dataset, kunnen de gegevens nu naar Platform of door UI of het gebruiken van Experience Platform APIs worden verzonden. U kunt deze gegevens via een batch- of streamingverbinding invoeren.

### Gegevens opnemen met een batchverbinding

Als u een batchverbinding wilt maken, volgt u de instructies in het algemene [UI-gids voor het uploaden van lokale bestanden](../../sources/tutorials/ui/create/local-system/local-file-upload.md). Voor een volledige lijst van beschikbare bronnen die u kunt gebruiken binnenste gegevens met, te lezen gelieve [overzicht van bronnen](../../sources/home.md).

### Gegevens verzamelen met behulp van een streamingverbinding

Als u een streamingverbinding wilt maken, volgt u de instructies in het dialoogvenster [API-zelfstudie](../../sources/tutorials/api/create/streaming/http.md) of de [UI-zelfstudie](../../sources/tutorials/ui/create/streaming/http.md).

Nadat u een streamingverbinding hebt gemaakt, hebt u toegang tot het unieke streamingeindpunt waarnaar u de gegevens kunt verzenden. Als u wilt weten hoe u gegevens naar deze eindpunten verzendt, leest u de [zelfstudie over streaming recordgegevens](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![Het streamingeindpunt voor de streamingverbinding wordt gemarkeerd op de pagina met brondetails.](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Structuur van metagegevens voor het publiek

Nadat u een verbinding hebt gemaakt, kunt u uw gegevens nu opnemen in Platform.

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

Zodra het geïmporteerde publiek is ingesteld, kunnen deze worden gebruikt als onderdeel van het segmenteringsproces. Ga naar Segment Builder en selecteer om een extern publiek te zoeken **[!UICONTROL Audiences]** in de **[!UICONTROL Fields]** sectie.

![De externe publiekskiezer in de Segment Builder wordt gemarkeerd.](../images/tutorials/external-audiences/external-audiences.png)

## Volgende stappen

Nu u externe doelgroepen in uw segmenten kunt gebruiken, kunt u de Bouwer van het Segment gebruiken om segmenten tot stand te brengen. Als u wilt leren hoe u segmenten maakt, leest u de [zelfstudie over het maken van segmenten](./create-a-segment.md).

## Bijlage

Naast het gebruiken van ingevoerde externe publieksmeta-gegevens en het gebruiken van hen voor het creëren van segmenten, kunt u externe segmentlidmaatschap aan Platform ook invoeren.

### Een extern bestemmingsschema voor een segmentlidmaatschap instellen

Als u een schema wilt samenstellen, selecteert u eerst **[!UICONTROL Schemas]** op de linkernavigatiebalk, gevolgd door de **[!UICONTROL Create schema]** in de rechterbovenhoek van de werkruimte Schemas. Van hier, selecteer **[!UICONTROL XDM Individual Profile]**.

![Het XDM-gebied Individueel profiel wordt gemarkeerd.](../images/tutorials/external-audiences/create-schema-profile.png)

Nu het schema is gecreeerd, zult u de het gebiedsgroep van het segmentlidmaatschap als deel van het schema moeten toevoegen. Selecteer [!UICONTROL Segment Membership Details], gevolgd door [!UICONTROL Add field groups].

![De de gebiedsgroep van de Details van het Lidmaatschap van het Segment wordt benadrukt.](../images/tutorials/external-audiences/segment-membership-details.png)

Zorg er bovendien voor dat het schema is gemarkeerd voor **[!UICONTROL Profile]**. Hiervoor moet u een veld markeren als de primaire identiteit.

![De knevel om het schema voor Profiel toe te laten wordt benadrukt in de Redacteur van het Schema.](../images/tutorials/external-audiences/external-segment-profile.png)

### De gegevensset instellen

Na het creëren van uw schema, zult u een dataset moeten tot stand brengen.

Om een dataset tot stand te brengen, volg de instructies in [gebruikershandleiding voor gegevenssets](../../catalog/datasets/user-guide.md#create). U moet de **[!UICONTROL Create dataset from schema]** met het eerder gemaakte schema.

![Het schema dat u gebruikt om de database te maken, wordt gemarkeerd.](../images/tutorials/external-audiences/select-schema.png)

Na het creëren van de dataset, volg de instructies in [gebruikershandleiding voor gegevenssets](../../catalog/datasets/user-guide.md#enable-profile) om deze dataset voor het Profiel van de Klant in real time toe te laten.

![De knevel om het schema voor Profiel toe te laten wordt benadrukt in creeer datasetwerkschema.](../images/tutorials/external-audiences/dataset-profile.png)

## Externe gegevens voor publieksleden instellen en importeren

Met toegelaten dataset, kunnen de gegevens nu naar Platform of door UI of het gebruiken van Experience Platform APIs worden verzonden. U kunt deze gegevens via een batch- of streamingverbinding invoeren.

### Gegevens opnemen met een batchverbinding

Als u een batchverbinding wilt maken, volgt u de instructies in het algemene [UI-gids voor het uploaden van lokale bestanden](../../sources/tutorials/ui/create/local-system/local-file-upload.md). Voor een volledige lijst van beschikbare bronnen die u kunt gebruiken binnenste gegevens met, te lezen gelieve [overzicht van bronnen](../../sources/home.md).

### Gegevens verzamelen met behulp van een streamingverbinding

Als u een streamingverbinding wilt maken, volgt u de instructies in het dialoogvenster [API-zelfstudie](../../sources/tutorials/api/create/streaming/http.md) of de [UI-zelfstudie](../../sources/tutorials/ui/create/streaming/http.md).

Nadat u een streamingverbinding hebt gemaakt, hebt u toegang tot het unieke streamingeindpunt waarnaar u de gegevens kunt verzenden. Als u wilt weten hoe u gegevens naar deze eindpunten verzendt, leest u de [zelfstudie over streaming recordgegevens](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![Het streamingeindpunt voor de streamingverbinding wordt gemarkeerd op de pagina met brondetails.](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Segmentlidmaatschapsstructuur

Nadat u een verbinding hebt gemaakt, kunt u uw gegevens nu opnemen in Platform.

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

>[!NOTE]
>
>Externe publieksleden worden standaard na 30 dagen verwijderd. Als u wilt voorkomen dat de gegevens worden verwijderd en deze langer dan 30 dagen wilt bewaren, gebruikt u de `validUntil` veld tijdens het opnemen van uw publieksgegevens. Lees voor meer informatie over dit veld de handleiding op [Segment Membership Details schema veldgroepen](../../xdm/field-groups/profile/segmentation.md).

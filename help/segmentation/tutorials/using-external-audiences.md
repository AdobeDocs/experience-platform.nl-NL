---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Extern publiek importeren en gebruiken
description: Volg deze zelfstudie om te leren hoe u externe doelgroepen kunt gebruiken met Adobe Experience Platform.
topic-legacy: tutorial
exl-id: 56fc8bd3-3e62-4a09-bb9c-6caf0523f3fe
source-git-commit: 8325ae6fd7d0013979e80d56eccd05b6ed6f5108
workflow-type: tm+mt
source-wordcount: '787'
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

Om een dataset tot stand te brengen, volg de instructies in [gebruikershandleiding voor gegevenssets](../../catalog/datasets/user-guide.md#create). U zult willen volgen **[!UICONTROL Create dataset from schema]** met het eerder gemaakte schema.

![](../images/tutorials/external-audiences/select-schema.png)

Na het creëren van de dataset, volg de instructies in [gebruikershandleiding voor gegevenssets](../../catalog/datasets/user-guide.md#enable-profile) om deze dataset voor het Profiel van de Klant in real time toe te laten.

![](../images/tutorials/external-audiences/dataset-profile.png)

## Gebruikersgegevens instellen en importeren

Met toegelaten dataset, kunnen de gegevens nu naar Platform of door UI of het gebruiken van Experience Platform APIs worden verzonden. Als u deze gegevens in het Platform wilt invoeren, moet u een streamingverbinding maken.

Als u een streamingverbinding wilt maken, volgt u de instructies in het dialoogvenster [API-zelfstudie](../../sources/tutorials/api/create/streaming/http.md) of de [UI-zelfstudie](../../sources/tutorials/ui/create/streaming/http.md).

Nadat u een streamingverbinding hebt gemaakt, hebt u toegang tot het unieke streamingeindpunt waarnaar u de gegevens kunt verzenden. Als u wilt weten hoe u gegevens naar deze eindpunten verzendt, leest u de [zelfstudie over streaming recordgegevens](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Segmenten samenstellen met behulp van geïmporteerde soorten publiek

Zodra het geïmporteerde publiek is ingesteld, kunnen deze worden gebruikt als onderdeel van het segmenteringsproces. Ga naar de Segment Builder en selecteer **[!UICONTROL Audiences]** in de **[!UICONTROL Fields]** sectie.

![](../images/tutorials/external-audiences/external-audiences.png)

## Volgende stappen

Nu u externe doelgroepen in uw segmenten kunt gebruiken, kunt u de Bouwer van het Segment gebruiken om segmenten tot stand te brengen. Als u wilt leren hoe u segmenten maakt, leest u de [zelfstudie over het maken van segmenten](./create-a-segment.md).

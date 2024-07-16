---
keywords: Experience Platform;thuis;populaire onderwerpen;bronnen;connectors;bronconnectors;bronnen sdk;sdk;SDK
title: Je Source verzenden
description: Het volgende document verstrekt stappen op hoe te om een nieuwe bron te testen en te verifiëren gebruikend de Dienst API van de Stroom en een nieuwe bron door Zelfbediening Bronnen (de Band SDK) te integreren.
exl-id: 9e945ba1-51b6-40a9-b92f-e0a52b3f92fa
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 0%

---

# Uw bron verzenden

De laatste stap voor het integreren van uw nieuwe bron in Adobe Experience Platform met behulp van Self-Serve Sources (Batch SDK) is het testen van uw bron voor verificatie. Als dit lukt, kunt u de nieuwe bron verzenden door contact op te nemen met uw Adobe.

Het volgende document verstrekt stappen op hoe te om uw bron te testen en te zuiveren gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

* Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Platform APIs ](../../../landing/api-guide.md).
* Voor informatie over hoe te om uw geloofsbrieven voor Platform APIs te produceren, zie het leerprogramma op [ voor authentiek verklaren en tot Experience Platform APIs toegang heeft ](../../../landing/api-authentication.md).
* Voor informatie over hoe te opstelling [!DNL Postman] voor Platform APIs, zie het leerprogramma op [ vestiging de console van de ontwikkelaar en  [!DNL Postman]](../../../landing/postman.md).
* Om uw het testen en het zuiveren proces te helpen, download de [ Zelfbediening inzameling en het milieu van de Broncontrole hier ](../assets/sdk-verification.zip) en volg de hieronder geschetste stappen.

## De bron testen

Om uw bron te testen, moet u de [ Zelf-Serve inzameling van de Broncontrole en het milieu ](../assets/sdk-verification.zip) op [!DNL Postman] in werking stellen terwijl het verstrekken van de aangewezen milieuvariabelen die tot uw bron behoren.

Als u wilt beginnen met testen, moet u eerst de verzameling en de omgeving instellen op [!DNL Postman] . Geef vervolgens de id van de verbindingsspecificatie op die u wilt testen.

### Opgeven `authSpecName`

Nadat u de verbindingsspecificatie-id hebt ingevoerd, moet u vervolgens de `authSpecName` opgeven die u gebruikt voor de basisverbinding. Afhankelijk van uw keuze kan dit `OAuth 2 Refresh Code` of `Basic Authentication` zijn. Nadat u de `authSpecName` -gegevens hebt opgegeven, moet u de vereiste gegevens in de omgeving opnemen. Als u bijvoorbeeld `authSpecName` opgeeft als `OAuth 2 Refresh Code` , moet u de vereiste referenties opgeven voor OAuth 2, die `host` en `accessToken` zijn.

### Opgeven `sourceSpec`

Als de parameters van de verificatiespecificatie zijn toegevoegd, moet u de vereiste eigenschappen vervolgens toevoegen vanuit de bronspecificatie. U kunt de vereiste eigenschappen vinden in `sourceSpec.spec.properties` . In het geval van het onderstaande [!DNL MailChimp Members] voorbeeld is de enige vereiste eigenschap `listId` , wat betekent `listId` en het is de overeenkomstige ID-waarde voor uw [!DNL Postman] -omgeving.

```json
"spec": {
  "$schema": "http://json-schema.org/draft-07/schema#",
  "type": "object",
  "description": "Define user input parameters to fetch resource values.",
  "properties": {
    "listId": {
      "type": "string",
      "description": "listId for which members need to fetch."
    }
  }
}
```

Zodra uw authentificatie en bronspecificatieparameters worden verstrekt, kunt u beginnen de rest milieuvariabelen te bevolken, zie de lijst hieronder ter verwijzing:

>[!NOTE]
>
>Alle onderstaande voorbeeldvariabelen zijn plaatsaanduidingswaarden die u moet bijwerken, behalve `flowSpecificationId` en `targetConnectionSpecId` , die vaste waarden zijn.

| Parameter | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `x-api-key` | Een unieke id die wordt gebruikt om aanroepen van Experience Platform-API&#39;s te verifiëren. Zie het leerprogramma op [ voor authentiek verklaren en tot Experience Platform APIs toegang heeft ](../../../landing/api-authentication.md) voor informatie over hoe te om uw `x-api-key` terug te winnen. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | Een onderneming die producten en diensten kan bezitten of in licentie kan geven en toegang kan verlenen tot haar leden. Zie het leerprogramma op [ vestiging de console van de ontwikkelaar en  [!DNL Postman]](../../../landing/postman.md) voor instructies op hoe te om uw `x-gw-ims-org-id` informatie terug te winnen. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | Het toestemmingstoken dat wordt vereist om vraag aan Experience Platform APIs te voltooien. Zie het leerprogramma op [ voor authentiek verklaren en tot Experience Platform APIs toegang heeft ](../../../landing/api-authentication.md) voor informatie over hoe te om uw `authorizationToken` terug te winnen. | `Bearer authorizationToken` |
| `schemaId` | Om de brongegevens in Platform te gebruiken, moet een doelschema worden gecreeerd om de brongegevens volgens uw behoeften te structureren. Voor gedetailleerde stappen op hoe te om een doelXDM schema tot stand te brengen, zie het leerprogramma op [ creërend een schema gebruikend API ](../../../xdm/api/schemas.md). | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | De unieke versie die overeenkomt met uw schema. | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | De `meta:altId` die wordt geretourneerd naast de `schemaId` bij het maken van een nieuw schema. | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | Voor gedetailleerde stappen op hoe te om een doeldataset tot stand te brengen, zie het leerprogramma op [ het creëren van een dataset gebruikend API ](../../../catalog/api/create-dataset.md). | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | Toewijzingssets kunnen worden gebruikt om te definiëren hoe gegevens in een bronschema worden toegewezen aan dat van een doelschema. Voor gedetailleerde stappen op hoe te om een afbeelding tot stand te brengen, zie het leerprogramma bij [ het creëren van een mappingsreeks gebruikend API ](../../../data-prep/api/mapping-set.md). | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | De unieke id die overeenkomt met uw toewijzingsset. | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | De verbindingsspecificatie-id die overeenkomt met uw bron. Dit is identiteitskaart die u na [ creeerde het creëren van een nieuwe verbindingsspecificatie ](./create.md) produceerde. | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | De flow specification-id van `RestStorageToAEP`. **dit is een vaste waarde**. | `6499120c-0b15-42dc-936e-847ea3c24d72` |
| `targetConnectionSpecId` | De doel verbindingsID van het gegevens meer waar ingeslikte gegevens in landen. **dit is een vaste waarde**. | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | Het opgegeven tijdsinterval dat moet worden gevolgd wanneer wordt gecontroleerd of een flow is voltooid. | `40` |
| `startTime` | De aangewezen begintijd voor uw gegevensstroom. De begintijd moet worden opgemaakt in unieke tijd. | `1597784298` |

Nadat u alle omgevingsvariabelen hebt opgegeven, kunt u de verzameling starten met de interface van [!DNL Postman] . In de [!DNL Postman] interface, selecteer de ellipsen (**...**) naast [!DNL Sources SSSs Verification Collection] en selecteer dan **inzameling van de Looppas**.

![ runner ](../assets/runner.png)

De interface [!DNL Runner] wordt weergegeven, zodat u de uitvoervolgorde van de gegevensstroom kunt configureren. Selecteer **de Verzameling van de Verificatie van SSS van de Looppas om de inzameling in werking te stellen.**

>[!NOTE]
>
>U kunt **Stroom van de Schrapping** van checklist van de looppasorde onbruikbaar maken als u verkiest om bronnen controledashboard in Platform UI te gebruiken. Als u echter klaar bent met testen, moet u ervoor zorgen dat de teststromen worden verwijderd.

![ looppas-inzameling ](../assets/run-collection.png)

## Uw bron verzenden

Zodra uw bron de volledige werkstroom kan voltooien kunt u te werk gaan om uw vertegenwoordiger van de Adobe te contacteren en uw bron voor integratie voor te leggen.

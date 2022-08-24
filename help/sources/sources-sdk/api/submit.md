---
keywords: Experience Platform;thuis;populaire onderwerpen;bronnen;connectors;bronconnectors;bronnen sdk;sdk;SDK
title: Uw bron verzenden
topic-legacy: overview
description: Het volgende document verstrekt stappen op hoe te om een nieuwe bron te testen en te verifiëren gebruikend de Dienst API van de Stroom en een nieuwe bron door Zelfbediening Bronnen (de Band SDK) te integreren.
exl-id: 9e945ba1-51b6-40a9-b92f-e0a52b3f92fa
source-git-commit: 4d7799b01c34f4b9e4a33c130583eadcfdc3af69
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 0%

---

# Uw bron verzenden

De laatste stap voor het integreren van uw nieuwe bron in Adobe Experience Platform met behulp van Self-Serve Sources (Batch SDK) is het testen van uw bron voor verificatie. Als dit lukt, kunt u de nieuwe bron verzenden door contact op te nemen met uw Adobe-vertegenwoordiger.

In het volgende document worden stappen beschreven voor het testen van en het opsporen van fouten in uw bron met behulp van de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

* Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../landing/api-guide.md).
* Raadpleeg de zelfstudie voor informatie over het genereren van referenties voor Platform-API&#39;s [Experience Platform-API&#39;s verifiëren en openen](../../../landing/api-authentication.md).
* Voor informatie over het instellen [!DNL Postman] voor Platform-API&#39;s raadpleegt u de zelfstudie [ontwikkelaarsconsole instellen en [!DNL Postman]](../../../landing/postman.md).
* Download de [Verzameling en omgeving van zelfbedieningsbronnen hier](../assets/sdk-verification.zip) en volgt u de hieronder beschreven stappen.

## De bron testen

Als u de bron wilt testen, moet u de opdracht [Verzameling en omgeving van zelfbedieningsbronnen](../assets/sdk-verification.zip) op [!DNL Postman] terwijl u de juiste omgevingsvariabelen voor uw bron aanbiedt.

Als u wilt beginnen met testen, moet u eerst de verzameling en omgeving instellen op [!DNL Postman]. Geef vervolgens de id van de verbindingsspecificatie op die u wilt testen.

### Geef het volgende op `authSpecName`

Nadat u de verbindingsspecificatie-id hebt ingevoerd, moet u vervolgens de `authSpecName` die u gebruikt voor uw basisverbinding. Afhankelijk van uw keuze kan dit `OAuth 2 Refresh Code` of  `Basic Authentication`. Zodra u uw `authSpecName`, moet u dan zijn vereiste geloofsbrieven in uw milieu omvatten. Als u bijvoorbeeld `authSpecName` als `OAuth 2 Refresh Code`, dan moet u de vereiste geloofsbrieven voor OAuth 2 verstrekken, die zijn `host` en `accessToken`.

### Geef het volgende op `sourceSpec`

Als de parameters van de verificatiespecificatie zijn toegevoegd, moet u de vereiste eigenschappen vervolgens toevoegen vanuit de bronspecificatie. U kunt de vereiste eigenschappen vinden in `sourceSpec.spec.properties`. In het geval van de [!DNL MailChimp Members] voorbeeld hieronder: de enige vereiste eigenschap is `listId`die `listId` en het komt overeen met de ID-waarde van je [!DNL Postman] milieu.

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
>Alle onderstaande voorbeeldvariabelen zijn plaatsaanduidingswaarden die u moet bijwerken, behalve `flowSpecificationId` en `targetConnectionSpecId`, die vaste waarden zijn.

| Parameter | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `x-api-key` | Een unieke id die wordt gebruikt om aanroepen van Experience Platform-API&#39;s te verifiëren. Zie de zelfstudie aan [Experience Platform-API&#39;s verifiëren en openen](../../../landing/api-authentication.md) voor informatie over hoe u uw `x-api-key`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | Een onderneming die producten en diensten kan bezitten of in licentie kan geven en toegang kan verlenen tot haar leden. Zie de zelfstudie aan [ontwikkelaarsconsole instellen en [!DNL Postman]](../../../landing/postman.md) voor instructies over hoe u uw `x-gw-ims-org-id` informatie. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | Het toestemmingstoken dat wordt vereist om vraag aan Experience Platform APIs te voltooien. Zie de zelfstudie aan [Experience Platform-API&#39;s verifiëren en openen](../../../landing/api-authentication.md) voor informatie over hoe u uw `authorizationToken`. | `Bearer authorizationToken` |
| `schemaId` | Om de brongegevens in Platform te gebruiken, moet een doelschema worden gecreeerd om de brongegevens volgens uw behoeften te structureren. Voor gedetailleerde stappen op hoe te om een doelXDM schema tot stand te brengen, zie de zelfstudie op [een schema maken met de API](../../../xdm/api/schemas.md). | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | De unieke versie die overeenkomt met uw schema. | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | De `meta:altId` dat wordt teruggegeven naast de  `schemaId` wanneer u een nieuw schema maakt. | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | Voor gedetailleerde stappen op hoe te om een doeldataset tot stand te brengen, zie het leerprogramma op [een gegevensset maken met behulp van de API](../../../catalog/api/create-dataset.md). | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | Toewijzingssets kunnen worden gebruikt om te definiëren hoe gegevens in een bronschema worden toegewezen aan dat van een doelschema. Raadpleeg de zelfstudie voor gedetailleerde stappen over het maken van een toewijzing [een toewijzingsset maken met de API](../../../data-prep/api/mapping-set.md). | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | De unieke id die overeenkomt met uw toewijzingsset. | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | De verbindingsspecificatie-id die overeenkomt met uw bron. Dit is de id die u hebt gegenereerd na [een nieuwe verbindingsspecificatie maken](./create.md). | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | De stroomspecificatie-id van `RestStorageToAEP`. **Dit is een vaste waarde**. | `6499120c-0b15-42dc-936e-847ea3c24d72` |
| `targetConnectionSpecId` | De doel verbindingsID van het gegevens meer waar ingeslikte gegevens in landen. **Dit is een vaste waarde**. | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | Het opgegeven tijdsinterval dat moet volgen wanneer wordt gecontroleerd of een flow is voltooid. | `40` |
| `startTime` | De aangewezen begintijd voor uw gegevensstroom. De begintijd moet worden opgemaakt in unieke tijd. | `1597784298` |

Als u alle omgevingsvariabelen hebt opgegeven, kunt u de verzameling starten met de [!DNL Postman] interface. In de [!DNL Postman] interface, selecteer de ellipsen (**...**) naast [!DNL Sources SSSs Verification Collection] en selecteer vervolgens **Verzameling uitvoeren**.

![runner](../assets/runner.png)

De [!DNL Runner] interface verschijnt, toestaand u om de looppasorde van uw dataflow te vormen. Selecteren **Verzameling voor SSS-verificatie uitvoeren** om de verzameling uit te voeren.

>[!NOTE]
>
>U kunt **Stroom verwijderen** in de checklist van de uitvoeringsorde als u verkiest om bronnen te gebruiken die dashboard in Platform UI controleren. Als u echter klaar bent met testen, moet u ervoor zorgen dat de teststromen worden verwijderd.

![uitvoeringsverzameling](../assets/run-collection.png)

## Uw bron verzenden

Zodra uw bron de volledige werkstroom kan voltooien kunt u te werk gaan om uw vertegenwoordiger van de Adobe te contacteren en uw bron voor integratie te voorleggen.

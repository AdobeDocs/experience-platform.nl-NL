---
title: De bron testen en verzenden
description: Het volgende document bevat stappen voor het testen en verifiëren van een nieuwe bron met behulp van de Flow Service API en het integreren van een nieuwe bron via Self-Serve Sources (Streaming SDK).
hide: true
hidefromtoc: true
source-git-commit: 7744fef9751212a40f8f20df52812d38130c42fc
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 0%

---

# De bron testen en verzenden

De laatste stappen voor het integreren van uw nieuwe bron in Adobe Experience Platform met behulp van Self-Serve Sources (Streaming SDK) zijn het testen en verzenden van uw nieuwe bron. Nadat u de verbindingsspecificatie hebt voltooid en de streamingstroomspecificatie hebt bijgewerkt, kunt u de functionaliteit van uw bron testen via de API of de gebruikersinterface. Als dit lukt, kunt u de nieuwe bron verzenden door contact op te nemen met uw Adobe-vertegenwoordiger.

In het volgende document worden stappen beschreven voor het testen van en het opsporen van fouten in uw bron met behulp van de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

* Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../landing/api-guide.md).
* Raadpleeg de zelfstudie voor informatie over het genereren van referenties voor Platform-API&#39;s [Experience Platform-API&#39;s verifiëren en openen](../../../landing/api-authentication.md).
* Voor informatie over het instellen [!DNL Postman] voor Platform-API&#39;s raadpleegt u de zelfstudie [ontwikkelaarsconsole instellen en [!DNL Postman]](../../../landing/postman.md).
* Download de [Verzameling en omgeving van zelfbedieningsbronnen hier](../assets/sdk-verification.zip) en volgt u de hieronder beschreven stappen.

## De bron testen met de API

Als u de bron wilt testen met de API, moet u de [Verzameling en omgeving van zelfbedieningsbronnen](../assets/sdk-verification.zip) op [!DNL Postman] terwijl u de juiste omgevingsvariabelen voor uw bron aanbiedt.

Als u wilt beginnen met testen, moet u eerst de verzameling en omgeving instellen op [!DNL Postman]. Geef vervolgens de id van de verbindingsspecificatie op die u wilt testen.

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
| `flowSpecificationId` | De stroomspecificatie-id van `GenericStreamingAEP`. **Dit is een vaste waarde**. | `e77fde5a-22a8-11ed-861d-0242ac120002` |
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

## De bron testen met de gebruikersinterface

Als u de bron in de gebruikersinterface wilt testen, gaat u naar de broncatalogus van de sandbox van uw organisatie in de gebruikersinterface van het Platform. Vanaf hier ziet u de nieuwe bron onder de *Streaming* categorie.

Nu uw nieuwe bron nu beschikbaar is in uw sandbox, moet u de workflow voor bronnen volgen om de functionaliteit te testen. Selecteer **[!UICONTROL Set up]**.

![De broncatalogus met de nieuwe streamingbron.](../assets/testing/catalog-test.png)

De [!UICONTROL Add data] wordt weergegeven. Om te testen dat uw bron gegevens kan stromen, gebruik de linkerkant van de interface om te uploaden [een voorbeeld van JSON-gegevens](../assets/testing/raw.json.zip). Zodra uw gegevens zijn geüpload, wordt de rechterkant van de interface bijgewerkt in een voorvertoning van de bestandshiërarchie van uw gegevens. Selecteren **[!UICONTROL Next]** om verder te gaan.

![De stap Gegevens toevoegen in de bronwerkstroom waar u uw gegevens kunt uploaden en voorvertonen voordat u ze opneemt.](../assets/testing/add-data-test.png)

De [!UICONTROL Dataflow detail] De pagina staat u toe om te selecteren of u een bestaande dataset of een nieuwe dataset wilt gebruiken. Tijdens dit proces kunt u ook uw gegevens configureren om in te voegen in profiel en instellingen inschakelen zoals [!UICONTROL Error diagnostics] en [!UICONTROL Partial ingestion].

Selecteer **[!UICONTROL New dataset]** en geef een naam op voor de uitvoergegevensset. Tijdens deze stap, kunt u een facultatieve beschrijving ook verstrekken om verdere informatie aan uw dataset toe te voegen. Selecteer vervolgens het schema waaraan u wilt toewijzen [!UICONTROL Advanced search] of door door de lijst van bestaande schema&#39;s in het dropdown menu te scrollen. Nadat u een schema hebt geselecteerd, geeft u een naam en een beschrijving voor de gegevensstroom op.

Als u klaar bent, selecteert u **[!UICONTROL Next]**.

![De stap met details voor gegevensstroom in de bronworkflow.](../assets/testing/dataflow-details-test.png)

De [!UICONTROL Mapping] de stap verschijnt, die u van een interface voorziet om de brongebieden van uw bronschema aan hun aangewezen doelXDM gebieden in het doelschema in kaart te brengen.

Platform biedt intelligente aanbevelingen voor automatisch toegewezen velden op basis van het doelschema of de gegevensset die u hebt geselecteerd. U kunt toewijzingsregels handmatig aanpassen aan uw gebruiksgevallen. Op basis van uw behoeften kunt u ervoor kiezen om velden rechtstreeks toe te wijzen of gegevens prep-functies te gebruiken om brongegevens om berekende of berekende waarden af te leiden. Voor uitvoerige stappen bij het gebruiken van de kaartperinterface en berekende gebieden, zie [UI-hulplijn voor gegevensvoorinstelling](../../../data-prep/ui/mapping.md)

Als de brongegevens eenmaal zijn toegewezen, selecteert u **[!UICONTROL Next]**.

![De toewijzingsstap van de workflow voor bronnen.](../assets/testing/mapping-test.png)

De **[!UICONTROL Review]** wordt weergegeven, zodat u de nieuwe gegevensstroom kunt controleren voordat deze wordt gemaakt. De details worden gegroepeerd in de volgende categorieën:

* **[!UICONTROL Connection]**: Hiermee geeft u de naam van uw account, het type bron en andere informatie weer die specifiek is voor de streamingbron voor cloudopslag die u gebruikt.
* **[!UICONTROL Assign dataset and map fields]**: Toont de doeldataset en het schema u voor uw gegevensstroom gebruikt.

Nadat u de gegevensstroom hebt gecontroleerd, selecteert u **[!UICONTROL Finish]** en laat enige tijd voor de gegevensstroom worden gecreeerd.

![De revisiestap van de workflow voor bronnen.](../assets/testing/review-test.png)

Tot slot moet u het het stromen eindpunt van uw gegevensstroom terugwinnen. Dit eindpunt zal worden gebruikt om aan uw webhaak in te tekenen, toestaand uw het stromen bron om met Experience Platform te communiceren. Ga naar het tabblad [!UICONTROL Dataflow activity] pagina van de gegevensstroom die u enkel creeerde en het eindpunt van de bodem kopieert [!UICONTROL Properties] deelvenster.

![Het het stromen eindpunt in dataflow activiteit.](../assets/testing/endpoint-test.png)

## Uw bron verzenden

Zodra uw bron het volledige werkschema kan voltooien kunt u te werk gaan om uw vertegenwoordiger van de Adobe te contacteren en uw bron voor integratie over andere organisaties van de Experience Platform voor te leggen.

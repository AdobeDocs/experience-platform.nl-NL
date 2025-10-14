---
title: Een Pendo Source Connection maken in de gebruikersinterface
description: Leer hoe u een Pendo-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
badge: Beta
exl-id: defdec30-42af-43c8-b2eb-7ce98f7871e3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 0%

---

# Een [!DNL Pendo] bronverbindingsgegevensstroom en in de gebruikersinterface maken

>[!NOTE]
>
>De bron [!DNL Pendo] is in bèta. Gelieve te lezen het [&#x200B; overzicht van bronnen &#x200B;](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

Deze zelfstudie bevat stappen voor het maken van een [!DNL Pendo] bronverbinding en gegevensstroom via de Adobe Experience Platform-gebruikersinterface.

## Aan de slag {#getting-started}

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem &#x200B;](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   * [&#x200B; Grondbeginselen van schemacompositie &#x200B;](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [&#x200B; het leerprogramma van de Redacteur van het Schema &#x200B;](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

## Vereisten {#prerequisites}

In de volgende sectie vindt u informatie over voorwaarden die moeten worden voltooid voordat u een [!DNL Pendo] bronverbinding kunt maken.

### Voorbeeld-JSON om het bronschema voor [!DNL Pendo] te definiëren {#prerequisites-json-schema}

Voordat u een [!DNL Pendo] -bronverbinding maakt, moet u een bronschema opgeven. U kunt de JSON hieronder gebruiken.

```
{
  "accountId": "58f79ee324d3f",
  "timestamp": 1673372516,
  "visitorId": "test@test.com",
  "uniqueId": "166e50cdf40930fe1367e4d44795c9c74d88b83a",
  "properties": {
    "guideProperties": {
  "name": "Guide Conversion Test"
  }
}
}
```

Voor meer informatie, lees de [[!DNL Pendo]  gids op webhooks &#x200B;](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks).

### Experience Platform-schema maken voor [!DNL Pendo] {#create-platform-schema}

U moet er ook voor zorgen dat u eerst een Experience Platform-schema voor uw bron maakt. Zie het leerprogramma op [&#x200B; creërend een schema van Experience Platform &#x200B;](../../../../../xdm/schema/composition.md) voor uitvoerige stappen op hoe te om een schema tot stand te brengen.

![&#x200B; UI die van Experience Platform een voorbeeldschema voor Pendo toont.](../../../../images/tutorials/create/analytics-pendo-webhook/schema.png)

## Sluit uw [!DNL Pendo] -account aan {#connect-account}

Selecteer in de gebruikersinterface van Experience Platform **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van [!UICONTROL Sources] en bekijk een catalogus met bronnen die beschikbaar zijn in Experience Platform.

Gebruik het menu *[!UICONTROL Categories]* om bronnen op categorie te filteren. U kunt ook een bronnaam invoeren in de zoekbalk om een specifieke bron uit de catalogus te zoeken.

Ga naar de categorie [!UICONTROL Analytics] om de [!DNL Pendo] bronkaart te zien. Selecteer eerst **[!UICONTROL Add data]** .

![&#x200B; de bron van Experience Platform UI catalogus met de kaart van de Buigmachine.](../../../../images/tutorials/create/analytics-pendo-webhook/catalog.png)

## Gegevens selecteren {#select-data}

De stap **[!UICONTROL Select data]** wordt weergegeven en biedt een interface waarmee u de gegevens kunt selecteren die u naar Experience Platform wilt verzenden.

* Het linkergedeelte van de interface is een browser waarmee u de beschikbare gegevensstromen binnen uw account kunt bekijken.
* In het rechtergedeelte van de interface kunt u maximaal 100 rijen gegevens uit een JSON-bestand voorvertonen.

Selecteer **[!UICONTROL Upload files]** om een JSON-bestand van uw lokale systeem te uploaden. U kunt ook het JSON-bestand dat u wilt uploaden naar het deelvenster [!UICONTROL Drag and drop files] slepen.

![&#x200B; voegt gegevensstap van het bronwerkschema toe.](../../../../images/tutorials/create/analytics-pendo-webhook/add-data.png)

Nadat het bestand is geüpload, wordt de voorbeeldinterface bijgewerkt en wordt een voorvertoning weergegeven van het schema dat u hebt geüpload. Met de voorvertoningsinterface kunt u de inhoud en structuur van een bestand controleren. U kunt het hulpprogramma [!UICONTROL Search field] ook gebruiken om toegang te krijgen tot specifieke items binnen uw schema.

Selecteer **[!UICONTROL Next]** als u klaar bent.

![&#x200B; de voorproefstap van het bronwerkschema.](../../../../images/tutorials/create/analytics-pendo-webhook/preview.png)

## Gegevens {#dataflow-detail}

De **Dataflow detailstap** verschijnt, die u van opties voorzien om een bestaande dataset te gebruiken of een nieuwe dataset voor uw dataflow te vestigen, evenals een kans om een naam en een beschrijving voor uw dataflow te verstrekken. Tijdens deze stap kunt u ook instellingen configureren voor het opnemen van profielen, foutdiagnose, gedeeltelijke inname en waarschuwingen.

Selecteer **[!UICONTROL Next]** als u klaar bent.

![&#x200B; dataflow-detail stap van het bronwerkschema.](../../../../images/tutorials/create/analytics-pendo-webhook/dataflow-detail.png)

## Toewijzing {#mapping}

De stap [!UICONTROL Mapping] verschijnt, die u van een interface voorziet om de brongebieden van uw bronschema aan hun aangewezen doelXDM gebieden in het doelschema in kaart te brengen.

Experience Platform biedt intelligente aanbevelingen voor automatisch toegewezen velden op basis van het doelschema of de gegevensset die u hebt geselecteerd. U kunt toewijzingsregels handmatig aanpassen aan uw gebruiksgevallen. Op basis van uw behoeften kunt u ervoor kiezen om velden rechtstreeks toe te wijzen of gegevens prep-functies te gebruiken om brongegevens om berekende of berekende waarden af te leiden. Voor uitvoerige stappen bij het gebruiken van de kaartperinterface en berekende gebieden, zie de [&#x200B; gids UI van de Prep van Gegevens &#x200B;](../../../../../data-prep/ui/mapping.md).

De onderstaande toewijzingen zijn verplicht en moeten worden ingesteld voordat u naar het [!UICONTROL Review] -werkgebied gaat.

| Doelveld | Beschrijving |
| --- | --- |
| `uniqueId` | De [!DNL Pendo] -id voor de gebeurtenis. |

Selecteer **[!UICONTROL Next]** wanneer de brongegevens correct zijn toegewezen.

![&#x200B; de afbeeldingsstap van het bronwerkschema.](../../../../images/tutorials/create/analytics-pendo-webhook/mapping.png)

## Controleren {#review}

De stap **[!UICONTROL Review]** wordt weergegeven, zodat u de nieuwe gegevensstroom kunt bekijken voordat deze wordt gemaakt. De details worden gegroepeerd in de volgende categorieën:

* **[!UICONTROL Connection]**: geeft het brontype, het relevante pad van het gekozen bronbestand en de hoeveelheid kolommen in dat bronbestand weer.
* **[!UICONTROL Assign dataset & map fields]**: Toont welke dataset de brongegevens worden opgenomen in, met inbegrip van het schema dat de dataset volgt aan.

Nadat u de gegevensstroom hebt gereviseerd, selecteert u **[!UICONTROL Finish]** en laat u enige tijd over om de gegevensstroom te maken.

![&#x200B; de overzichtsstap van het bronwerkschema.](../../../../images/tutorials/create/analytics-pendo-webhook/review.png)

## Uw URL voor het streamingeindpunt ophalen {#get-streaming-endpoint-url}

Wanneer uw streaminggegevens zijn gemaakt, kunt u nu de URL van het streamingeindpunt ophalen. Dit eindpunt wordt gebruikt om een abonnement te nemen op uw webhaak, zodat uw streamingbron kan communiceren met Experience Platform.

Als u de URL wilt maken die wordt gebruikt om de webhaak op [!DNL Pendo] te configureren, moet u het volgende ophalen:

* **[!UICONTROL Dataflow ID]**
* **[!UICONTROL Streaming endpoint]**

Als u de gegevens **[!UICONTROL Dataflow ID]** en **[!UICONTROL Streaming endpoint]** wilt ophalen, gaat u naar de [!UICONTROL Dataflow activity] pagina van de gegevensstroom die u net hebt gemaakt en kopieert u de gegevens onder aan het deelvenster [!UICONTROL Properties] .

![&#x200B; het stromen eindpunt in dataflow activiteit.](../../../../images/tutorials/create/analytics-pendo-webhook/endpoint-test.png)

Wanneer u het streamingeindpunt en de dataflow-id hebt opgehaald, maakt u een URL op basis van het volgende patroon: ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}``` . Een geconstrueerde URL voor een webhaak ziet er bijvoorbeeld als volgt uit: ```https://dcs.adobedc.net/collection/0c61859cc71939a0caf01123f91b2fc52589018800ad46b6c76c2dff3595ee95```

## Webhaak instellen in [!DNL Pendo] {#set-up-webhook}

Meld u vervolgens aan bij uw account op [[!DNL Pendo] &#x200B;](https://pendo.io/) en maak een webhaak. Voor stappen op hoe te om een webhaak tot stand te brengen die het [!DNL Pendo] gebruikersinterface gebruiken, gelieve te verwijzen naar de [[!DNL Pendo]  gids bij het creëren van webhaak &#x200B;](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks#create-a-webhook-0-4).

Nadat u de webhaak hebt gemaakt, navigeert u naar de instellingenpagina van de [!DNL Pendo] webhaak en voert u de URL van de webhaak in het veld [!DNL URL] in.

![&#x200B; het het schermschot van de Buigmachine UI die het gebied van het webhaakeindpunt toont &#x200B;](../../../../images/tutorials/create/analytics-pendo-webhook/webhook.png)

>[!TIP]
>
>U kunt zich abonneren op verschillende categorieën gebeurtenissen om het type gebeurtenissen te bepalen dat u van uw [!DNL Pendo] -instantie naar Experience Platform wilt verzenden. Voor meer informatie over de verschillende gebeurtenissen, gelieve te verwijzen naar de [[!DNL Pendo]  documentatie &#x200B;](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks#create-a-webhook-0-4).

## Volgende stappen {#next-steps}

Aan de hand van deze zelfstudie hebt u een streaminggegevensstroom geconfigureerd om uw [!DNL Pendo] -gegevens over te brengen naar Experience Platform. Om de gegevens te controleren die worden opgenomen, verwijs naar de gids bij [&#x200B; controle die dataflows gebruikend Experience Platform UI &#x200B;](../../monitor-streaming.md) stromen.

## Aanvullende bronnen {#additional-resources}

De onderstaande secties bevatten aanvullende bronnen waarnaar u kunt verwijzen wanneer u de [!DNL Pendo] -bron gebruikt.

### Validatie {#validation}

Voer de onderstaande stappen uit om te controleren of u de bron juist hebt ingesteld en of [!DNL Pendo] -berichten worden ingevoerd:

* U kunt de pagina [!DNL Pendo] **[!UICONTROL Reports]** > **[!UICONTROL Chat History]** controleren om de gebeurtenissen te identificeren die door [!DNL Pendo] worden vastgelegd.

{het schermschot van 0} van de Buigmachine UI die praatjegeschiedenis toont ![&#128279;](../../../../images/tutorials/create/analytics-pendo-webhook/pendo-events.png)

* Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL View Dataflows]** naast het kaartmenu [!DNL Pendo] in de catalogus met bronnen. Selecteer vervolgens **[!UICONTROL Preview dataset]** om de gegevens te verifiëren die zijn ingevoerd voor de webhooks die u hebt geconfigureerd in [!DNL Pendo] .

{het schermschot van 0} Experience Platform UI die ingebedde gebeurtenissen ![&#128279;](../../../../images/tutorials/create/analytics-pendo-webhook/platform-dataset.png) toont

### Fouten en problemen oplossen {#errors-and-troubleshooting}

Bij het controleren van een gegevensstroomuitvoering kan het volgende foutbericht optreden: `The message can't be validated ... uniqueID:expected minLength:1, actual 0].`

{het schermschot van 0} Experience Platform UI die fout toont.![&#128279;](../../../../images/tutorials/create/analytics-pendo-webhook/error.png)

Om deze fout te bevestigen, moet u verifiëren dat de ** afbeelding uniqueID opstelling is geweest. Voor extra begeleiding, verwijs naar de [&#x200B; Mpping &#x200B;](#mapping) sectie.

Voor meer informatie bezoek het [[!DNL Pendo]  Centrum van de Hulp &#x200B;](https://www.pendo.io/help-center/).

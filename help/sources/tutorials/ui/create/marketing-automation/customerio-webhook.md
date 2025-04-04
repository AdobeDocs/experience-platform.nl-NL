---
title: Een Customer.io Source Connection en Dataflow maken in de gebruikersinterface
description: Leer hoe u een Customer.io-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
badge: Beta
exl-id: 7655a34c-808a-46e3-94e3-022a433755a4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 0%

---

# Een [!DNL Customer.io] bronverbinding en gegevensstroom maken in de gebruikersinterface

>[!NOTE]
>
>De bron [!DNL Customer.io] is in bèta. Gelieve te lezen het [ overzicht van bronnen ](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

Deze zelfstudie bevat stappen voor het maken van een [!DNL Customer.io] bronverbinding en gegevensstroom via de Adobe Experience Platform-gebruikersinterface.

## Aan de slag {#getting-started}

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

## Vereisten {#prerequisites}

In de volgende sectie vindt u informatie over voorwaarden die moeten worden voltooid voordat u een [!DNL Customer.io] bronverbinding kunt maken.

### Voorbeeld-JSON om het bronschema voor [!DNL Customer.io] te definiëren {#prerequisites-json-schema}

Voordat u een [!DNL Customer.io] -bronverbinding maakt, moet u een bronschema opgeven. U kunt de onderstaande JSON gebruiken.

```
{
  "event_id": "01E4C4CT6YDC7Y5M7FE1GWWPQJ",
  "object_type": "customer",
  "metric": "subscribed",
  "timestamp": 1613063089,
  "data": {
    "customer_id": "42",
    "email_address": "test@example.com",
    "identifiers": {
      "id": "42",
      "email": "test@example.com",
      "cio_id": "d9c106000001"
    }
  }
}
```

### Experience Platform-schema maken voor [!DNL Customer.io] {#create-platform-schema}

U moet er ook voor zorgen dat u een Experience Platform-schema maakt dat u voor uw bron kunt gebruiken. Zie het leerprogramma op [ creërend een schema van Experience Platform ](../../../../../xdm/schema/composition.md) voor uitvoerige stappen op hoe te om een schema tot stand te brengen.

{het schermschot van 0} Experience Platform UI die een voorbeeldschema voor Customer.io toont ](../../../../images/tutorials/create/marketing-automation/customerio-webhook/schema.png)![

## Sluit uw [!DNL Customer.io] -account aan {#connect-account}

Selecteer in de gebruikersinterface van Experience Platform **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van [!UICONTROL Sources] en bekijk een catalogus met bronnen die beschikbaar zijn in Experience Platform.

Gebruik het menu *[!UICONTROL Categories]* om bronnen op categorie te filteren. U kunt ook een bronnaam invoeren in de zoekbalk om een specifieke bron uit de catalogus te zoeken.

Ga naar de categorie [!UICONTROL Marketing automation] om de [!DNL Customer.io] bronkaart te zien. Selecteer eerst **[!UICONTROL Add data]** .

{het schermschot van 0} Experience Platform UI voor catalogus met Customer.io kaart ](../../../../images/tutorials/create/marketing-automation/customerio-webhook/catalog.png)![

## Gegevens selecteren {#select-data}

De stap **[!UICONTROL Select data]** wordt weergegeven en biedt een interface waarmee u de gegevens kunt selecteren die u naar Experience Platform wilt verzenden.

* Het linkergedeelte van de interface is een browser waarmee u de beschikbare gegevensstromen binnen uw account kunt bekijken.
* In het rechtergedeelte van de interface kunt u maximaal 100 rijen gegevens uit een JSON-bestand voorvertonen.

Selecteer **[!UICONTROL Upload files]** om een JSON-bestand van uw lokale systeem te uploaden. U kunt ook het JSON-bestand dat u wilt uploaden naar het deelvenster [!UICONTROL Drag and drop files] slepen.

![ voegt gegevensstap van het bronwerkschema toe.](../../../../images/tutorials/create/marketing-automation/customerio-webhook//add-data.png)

Nadat het bestand is geüpload, wordt de voorbeeldinterface bijgewerkt en wordt een voorvertoning weergegeven van het schema dat u hebt geüpload. Met de voorvertoningsinterface kunt u de inhoud en structuur van een bestand controleren. U kunt het hulpprogramma [!UICONTROL Search field] ook gebruiken om toegang te krijgen tot specifieke items binnen uw schema.

Selecteer **[!UICONTROL Next]** als u klaar bent.

![ de voorproefstap van het bronwerkschema.](../../../../images/tutorials/create/marketing-automation/customerio-webhook//preview.png)

## Gegevens {#dataflow-detail}

De **Dataflow detailstap** verschijnt, die u van opties voorzien om een bestaande dataset te gebruiken of een nieuwe dataset voor uw dataflow te vestigen, evenals een kans om een naam en een beschrijving voor uw dataflow te verstrekken. Tijdens deze stap kunt u ook instellingen configureren voor het opnemen van profielen, foutdiagnose, gedeeltelijke inname en waarschuwingen.

Selecteer **[!UICONTROL Next]** als u klaar bent.

![ dataflow-detail stap van het bronwerkschema.](../../../../images/tutorials/create/marketing-automation/customerio-webhook//dataflow-detail.png)

## Toewijzing {#mapping}

De stap [!UICONTROL Mapping] verschijnt, die u van een interface voorziet om de brongebieden van uw bronschema aan hun aangewezen doelXDM gebieden in het doelschema in kaart te brengen.

Experience Platform biedt intelligente aanbevelingen voor automatisch toegewezen velden op basis van het doelschema of de gegevensset die u hebt geselecteerd. U kunt toewijzingsregels handmatig aanpassen aan uw gebruiksgevallen. Op basis van uw behoeften kunt u ervoor kiezen om velden rechtstreeks toe te wijzen of gegevens prep-functies te gebruiken om brongegevens om berekende of berekende waarden af te leiden. Voor uitvoerige stappen bij het gebruiken van de kaartperinterface en berekende gebieden, zie de [ gids UI van de Prep van Gegevens ](../../../../../data-prep/ui/mapping.md).

Alle onderstaande toewijzingen zijn verplicht en moeten worden ingesteld voordat u naar het [!UICONTROL Review] -werkgebied gaat.

| Doelveld | Beschrijving |
| --- | --- |
| `object_type` | Het objecten type, verwijs naar de [!DNL Customer.io] [ gebeurtenissen ](https://customer.io/docs/webhooks/#events) documentatie voor de gesteunde types. |
| `id` | De id van het object. |
| `email` | Het e-mailadres dat aan het object is gekoppeld. |
| `event_id` | De unieke id van de gebeurtenis. |
| `cio_id` | De [!DNL Customer.io] -id voor de gebeurtenis. |
| `metric` | Het gebeurtenistype. Voor meer informatie, verwijs naar de [!DNL Customer.io] [ gebeurtenissen ](https://customer.io/docs/webhooks/#events) documentatie voor gesteunde types. |
| `timestamp` | De tijdstempel wanneer de gebeurtenis heeft plaatsgevonden. |

>[!IMPORTANT]
>
>Wijs `cio_id` niet toe bij het uitvoeren van [!DNL Customer.io] webhaak in de `test mode` omdat er geen gekoppelde velden worden verzonden vanuit [!DNL Customer.io] .

Selecteer **[!UICONTROL Next]** wanneer de brongegevens correct zijn toegewezen.

![ de afbeeldingsstap van het bronwerkschema.](../../../../images/tutorials/create/marketing-automation/customerio-webhook/mapping.png)

## Controleren {#review}

De stap **[!UICONTROL Review]** wordt weergegeven, zodat u de nieuwe gegevensstroom kunt bekijken voordat deze wordt gemaakt. De details worden gegroepeerd in de volgende categorieën:

* **[!UICONTROL Connection]**: geeft het brontype, het relevante pad van het gekozen bronbestand en de hoeveelheid kolommen in dat bronbestand weer.
* **[!UICONTROL Assign dataset & map fields]**: Toont welke dataset de brongegevens worden opgenomen in, met inbegrip van het schema dat de dataset volgt aan.

Nadat u de gegevensstroom hebt gereviseerd, selecteert u **[!UICONTROL Finish]** en laat u enige tijd over om de gegevensstroom te maken.

![ de overzichtsstap van het bronwerkschema.](../../../../images/tutorials/create/marketing-automation/customerio-webhook/review.png)

## Uw URL voor het streamingeindpunt ophalen {#get-streaming-endpoint}

Wanneer uw streaminggegevens zijn gemaakt, kunt u nu de URL van het streamingeindpunt ophalen. Dit eindpunt wordt gebruikt om een abonnement te nemen op uw webhaak, zodat uw streamingbron kan communiceren met Experience Platform.

Als u de URL wilt maken die wordt gebruikt om de webhaak op [!DNL Customer.io] te configureren, moet u het volgende ophalen:

* **[!UICONTROL Dataflow ID]**
* **[!UICONTROL Streaming endpoint]**

Als u de gegevens **[!UICONTROL Dataflow ID]** en **[!UICONTROL Streaming endpoint]** wilt ophalen, gaat u naar de [!UICONTROL Dataflow activity] pagina van de gegevensstroom die u net hebt gemaakt en kopieert u de gegevens onder aan het deelvenster [!UICONTROL Properties] .

![ het stromen eindpunt in dataflow activiteit.](../../../../images/tutorials/create/marketing-automation/customerio-webhook/endpoint-test.png)

Wanneer u het streamingeindpunt en de dataflow-id hebt opgehaald, maakt u een URL op basis van het volgende patroon: ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}``` . Een geconstrueerde URL voor een webhaak ziet er bijvoorbeeld als volgt uit: ``https://dcs.adobedc.net/collection/febc116d22ba0ea2868e9c93b199375302afb8a589617700991bb8f3f0341ad7?x-adobe-flow-id=439b3fc4-3042-4a3a-b5e0-a494898d3fb0``

## Rapportwebhaak instellen in [!DNL Customer.io] {#set-up-webhook}

Als de URL van uw webhaak is gemaakt, kunt u nu de rapportwebhaak instellen via de gebruikersinterface van [!DNL Customer.io] . Voor stappen bij vestiging die webhooks melden, te lezen gelieve de [[!DNL Customer.io]  gids ](https://customer.io/docs/webhooks/#setup) bij vestiging webhooks.

In het [!DNL Customer.io] gebruikersinterface, input uw [ webhaak URL ](#get-streaming-endpoint-url) op het [!DNL WEBHOOK ENDPOINT] gebied.

![ Het gebruikersinterface Customer.io die het WebHaak eindpuntgebied ](../../../../images/tutorials/create/marketing-automation/customerio-webhook/webhook.png) toont

>[!TIP]
>
>U kunt zich abonneren op verschillende gebeurtenissen voor uw rapporterende webhaak. Het bericht van elke gebeurtenis wordt naar Experience Platform verzonden wanneer aan de triggercriteria voor een gebeurtenis met [!DNL Customer.io] -actie wordt voldaan. Voor meer informatie over de verschillende gebeurtenissen, gelieve te verwijzen naar de [[!DNL Customer.io]  gebeurtenisdocumentatie ](https://customer.io/docs/webhooks/#events).

## Volgende stappen {#next-steps}

Aan de hand van deze zelfstudie hebt u een streaminggegevensstroom geconfigureerd om uw [!DNL Customer.io] -gegevens over te brengen naar Experience Platform. Om de gegevens te controleren die worden opgenomen, verwijs naar de gids bij [ controle die dataflows gebruikend Experience Platform UI ](../../monitor-streaming.md) stromen.

## Aanvullende bronnen {#additional-resources}

De onderstaande secties bevatten aanvullende bronnen waarnaar u kunt verwijzen wanneer u de [!DNL Customer.io] -bron gebruikt.

### Guardrails {#guardrails}

Voor informatie over gidsen, gelieve te verwijzen naar de [[!DNL Customer.io]  onderbrekingen en mislukkingspagina ](https://customer.io/docs/webhooks/#timeouts-and-failures).

### Validatie {#validation}

Voer de onderstaande stappen uit om te controleren of u de bron juist hebt ingesteld en of [!DNL Customer.io] -berichten worden ingevoerd:

* U kunt de pagina [!DNL Customer.io] **[!UICONTROL Activity Logs]** controleren om de gebeurtenissen te identificeren die door [!DNL Customer.io] worden vastgelegd.

{het schermschot van 0} Customer.io die activiteitenlogboeken tonen ](../../../../images/tutorials/create/marketing-automation/customerio-webhook/activity-logs.png)![

* Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL View Dataflows]** naast het kaartmenu [!DNL Customer.io] in de catalogus met bronnen. Selecteer vervolgens **[!UICONTROL Preview dataset]** om de gegevens te verifiëren die zijn ingevoerd voor de gebeurtenissen die u in [!DNL Customer.io] hebt geselecteerd.

{het schermschot van 0} Experience Platform UI die ingebedde gebeurtenissen ](../../../../images/tutorials/create/marketing-automation/customerio-webhook/platform-dataset.png) toont![

---
title: Een Chatlio Source Connection maken in de gebruikersinterface
description: Leer hoe u een Chatlio-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
badge: Beta
exl-id: 55c10bcb-0332-45ff-970b-272d375b591d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1120'
ht-degree: 0%

---

# Een [!DNL Chatlio] bronverbinding maken in de gebruikersinterface

>[!NOTE]
>
>De bron [!DNL Chatlio] is in bèta. Gelieve te lezen het [&#x200B; overzicht van bronnen &#x200B;](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

Deze zelfstudie bevat stappen voor het maken van een [!DNL Chatlio] -bronverbinding met de Adobe Experience Platform-gebruikersinterface.

## Aan de slag {#getting-started}

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem &#x200B;](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   * [&#x200B; Grondbeginselen van schemacompositie &#x200B;](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [&#x200B; het leerprogramma van de Redacteur van het Schema &#x200B;](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

## Vereisten {#prerequisites}

In de volgende sectie vindt u informatie over voorwaarden die moeten worden voltooid voordat u een [!DNL Chatlio] bronverbinding kunt maken.

### Voorbeeld-JSON om het bronschema voor [!DNL Chatlio] te definiëren {#prerequisites-json-schema}

Voordat u een [!DNL Chatlio] -bronverbinding maakt, moet u een bronschema opgeven. U kunt de JSON hieronder gebruiken.

```
{
  "visitor": {
    "email": "test@example.com",
    "UUID": "2d3f4260-2235-903b-0a82-a23d326cc257"
  },
   "message": "Hi",
  "channelId": "C04J7M7LCMQ",
  "slackChannelName": "aep",
  "slackChannelId": "C04JVR71WKS"
}
```

### Experience Platform-schema maken voor [!DNL Chatlio] {#create-platform-schema}

U moet er ook voor zorgen dat u een Experience Platform-schema maakt dat u voor uw bron kunt gebruiken. Lees het leerprogramma op [&#x200B; creërend een schema van Experience Platform &#x200B;](../../../../../xdm/schema/composition.md) voor uitvoerige stappen op hoe te om een schema tot stand te brengen.

![&#x200B; UI die van Experience Platform een voorbeeldschema voor Chatlio toont &#x200B;](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/schema.png)

## Sluit uw [!DNL Chatlio] -account aan {#connect-account}

Selecteer in de gebruikersinterface van Experience Platform **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van [!UICONTROL Sources] en bekijk een catalogus met bronnen die beschikbaar zijn in Experience Platform.

Gebruik het menu *[!UICONTROL Categories]* om bronnen op categorie te filteren. U kunt ook een bronnaam invoeren in de zoekbalk om een specifieke bron uit de catalogus te zoeken.

Ga naar de categorie [!UICONTROL Marketing automation] om de [!DNL Chatlio] bronkaart te zien. Selecteer eerst **[!UICONTROL Add data]** .

![&#x200B; de catalogus UI van Experience Platform met Chatlio kaart &#x200B;](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/catalog.png)

## Gegevens selecteren {#select-data}

De stap **[!UICONTROL Select data]** wordt weergegeven en biedt een interface waarmee u de gegevens kunt selecteren die u naar Experience Platform wilt verzenden.

* Het linkergedeelte van de interface is een browser waarmee u de beschikbare gegevensstromen binnen uw account kunt bekijken.
* In het rechtergedeelte van de interface kunt u maximaal 100 rijen gegevens uit een JSON-bestand voorvertonen.

Selecteer **[!UICONTROL Upload files]** om een JSON-bestand van uw lokale systeem te uploaden. U kunt ook het JSON-bestand dat u wilt uploaden naar het deelvenster [!UICONTROL Drag and drop files] slepen.

![&#x200B; voegt gegevensstap van het bronwerkschema toe.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/add-data.png)

Nadat het bestand is geüpload, wordt de voorbeeldinterface bijgewerkt en wordt een voorvertoning weergegeven van het schema dat u hebt geüpload. Met de voorvertoningsinterface kunt u de inhoud en structuur van een bestand controleren. U kunt het hulpprogramma [!UICONTROL Search field] ook gebruiken om toegang te krijgen tot specifieke items binnen uw schema.

Selecteer **[!UICONTROL Next]** als u klaar bent.

![&#x200B; de voorproefstap van het bronwerkschema.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/preview.png)

## Gegevens {#dataflow-detail}

De **Dataflow detailstap** verschijnt, die u van opties voorzien om een bestaande dataset te gebruiken of een nieuwe dataset voor uw dataflow te vestigen, evenals een kans om een naam en een beschrijving voor uw dataflow te verstrekken. Tijdens deze stap kunt u ook instellingen configureren voor het opnemen van profielen, foutdiagnose, gedeeltelijke inname en waarschuwingen.

Selecteer **[!UICONTROL Next]** als u klaar bent.

![&#x200B; dataflow-detail stap van het bronwerkschema.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/dataflow-detail.png)

## Toewijzing {#mapping}

De stap [!UICONTROL Mapping] verschijnt, die u van een interface voorziet om de brongebieden van uw bronschema aan hun aangewezen doelXDM gebieden in het doelschema in kaart te brengen.

Experience Platform biedt intelligente aanbevelingen voor automatisch toegewezen velden op basis van het doelschema of de gegevensset die u hebt geselecteerd. U kunt toewijzingsregels handmatig aanpassen aan uw gebruiksgevallen. Op basis van uw behoeften kunt u ervoor kiezen om velden rechtstreeks toe te wijzen of gegevens prep-functies te gebruiken om brongegevens om berekende of berekende waarden af te leiden. Voor uitvoerige stappen bij het gebruiken van de kaartperinterface en berekende gebieden, zie de [&#x200B; gids UI van de Prep van Gegevens &#x200B;](../../../../../data-prep/ui/mapping.md).

De onderstaande toewijzingen zijn verplicht en moeten worden ingesteld voordat u naar het [!UICONTROL Review] -werkgebied gaat.

| Doelveld | Beschrijving |
| --- | --- |
| `UUID` | De [!DNL Chatlio] -id voor de gebeurtenis. |

Selecteer **[!UICONTROL Next]** wanneer de brongegevens correct zijn toegewezen.

![&#x200B; de afbeeldingsstap van het bronwerkschema.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/mapping.png)

## Controleren {#review}

De stap **[!UICONTROL Review]** wordt weergegeven, zodat u de nieuwe gegevensstroom kunt bekijken voordat deze wordt gemaakt. De details worden gegroepeerd in de volgende categorieën:

* **[!UICONTROL Connection]**: geeft het brontype, het relevante pad van het gekozen bronbestand en de hoeveelheid kolommen in dat bronbestand weer.
* **[!UICONTROL Assign dataset & map fields]**: Toont welke dataset de brongegevens worden opgenomen in, met inbegrip van het schema dat de dataset volgt aan.

Nadat u de gegevensstroom hebt gereviseerd, selecteert u **[!UICONTROL Finish]** en laat u enige tijd over om de gegevensstroom te maken.

![&#x200B; de overzichtsstap van het bronwerkschema.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/review.png)

## Uw URL voor het streamingeindpunt ophalen {#get-streaming-endpoint-url}

Wanneer uw streaminggegevens zijn gemaakt, kunt u nu de URL van het streamingeindpunt ophalen. Dit eindpunt wordt gebruikt om een abonnement te nemen op uw webhaak, zodat uw streamingbron kan communiceren met Experience Platform.

Als u de URL wilt maken die wordt gebruikt om de webhaak op [!DNL Chatlio] te configureren, moet u het volgende ophalen:

* **[!UICONTROL Dataflow ID]**
* **[!UICONTROL Streaming endpoint]**

Als u de gegevens **[!UICONTROL Dataflow ID]** en **[!UICONTROL Streaming endpoint]** wilt ophalen, gaat u naar de [!UICONTROL Dataflow activity] pagina van de gegevensstroom die u net hebt gemaakt en kopieert u de gegevens onder aan het deelvenster [!UICONTROL Properties] .

![&#x200B; het stromen eindpunt in dataflow activiteit.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/endpoint-test.png)

Wanneer u het streamingeindpunt en de dataflow-id hebt opgehaald, maakt u een URL op basis van het volgende patroon: ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}``` . Een geconstrueerde URL voor een webhaak ziet er bijvoorbeeld als volgt uit: ``https://dcs.adobedc.net/collection/d56b47ee3985104beaf724efcd78a3e1a863d720471a482bebac0acc1ab95983``

## Webhaak instellen in [!DNL Chatlio] {#set-up-webhook}

Wanneer de URL van uw webhaak is gemaakt, kunt u de webhaak nu instellen via de gebruikersinterface van [!DNL Chatlio] .

Login aan uw [[!DNL Chatlio] &#x200B;](https://chatlio.com/) rekening en volg [&#x200B; de gids op opstelling en installatie &#x200B;](https://chatlio.com/docs/setup/) om een widget tot stand te brengen.

Wanneer een widget is gemaakt, navigeert u naar de instellingenpagina van de widget om uw webhaak-URL aan die widget toe te voegen.

![&#x200B; de WebHaak montagespagina op Chatlio.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/widget-settings.png)

Selecteer vervolgens het tabblad **[!DNL Behavior]** en voeg de URL van de webhaak toe aan het veld *[!DNL Webhook when a new conversation starts]* en aan alle andere webhaakgebeurtenissen waarop u zich wilt abonneren.

![&#x200B; Chatlio UI die het gebied van het webhaakeindpunt toont.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/webhook.png)

>[!TIP]
>
>U kunt zich abonneren op een aantal verschillende gebeurtenissen voor uw [!DNL Chatlio] -webhaak. Voor meer informatie over de verschillende gebeurtenissen, gelieve te verwijzen naar de [[!DNL Chatlio]  gebeurtenisdocumentatie &#x200B;](https://chatlio.com/docs/webhooks/).

## Volgende stappen {#next-steps}

Aan de hand van deze zelfstudie hebt u een streaminggegevensstroom geconfigureerd om uw [!DNL Chatlio] -gegevens over te brengen naar Experience Platform. Om de gegevens te controleren die worden opgenomen, verwijs naar de gids bij [&#x200B; controle die dataflows gebruikend Experience Platform UI &#x200B;](../../monitor-streaming.md) stromen.

## Aanvullende bronnen {#additional-resources}

De onderstaande secties bevatten aanvullende bronnen waarnaar u kunt verwijzen wanneer u de [!DNL Chatlio] -bron gebruikt.

### Validatie {#validation}

Voer de onderstaande stappen uit om te controleren of u de bron juist hebt ingesteld en of [!DNL Chatlio] -berichten worden ingevoerd:

* U kunt de pagina [!DNL Chatlio] **[!UICONTROL Reports]** > **[!UICONTROL Chat History]** controleren om de gebeurtenissen te identificeren die door [!DNL Chatlio] worden vastgelegd.

{het schermschot van 0} Chatlio UI die praatjegeschiedenis ![&#128279;](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/chatlio-chat-history.png) tonen

* Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL View Dataflows]** naast het kaartmenu [!DNL Chatlio] in de catalogus met bronnen. Selecteer vervolgens **[!UICONTROL Preview dataset]** om de gegevens te verifiëren die zijn ingevoerd voor de webhooks die u hebt geconfigureerd in [!DNL Chatlio] .

{het schermschot van 0} Experience Platform UI die ingebedde gebeurtenissen ![&#128279;](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/platform-dataset.png) toont

Voor extra informatie over [!DNL Chatlio], bezoek de [[!DNL Chatlio]  documentatie &#x200B;](https://chatlio.com/docs/) en [&#x200B; Veelgestelde vragen &#x200B;](https://chatlio.com/pricing/#FAQ).

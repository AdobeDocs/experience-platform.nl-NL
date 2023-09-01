---
title: Een Chatlio Source Connection maken in de gebruikersinterface
description: Leer hoe u een Chatlio-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
badge: Beta
exl-id: 55c10bcb-0332-45ff-970b-272d375b591d
source-git-commit: 8de45a54607bed17fd79bbed693666beb09c0502
workflow-type: tm+mt
source-wordcount: '1120'
ht-degree: 0%

---

# Een [!DNL Chatlio] bronverbinding in de gebruikersinterface

>[!NOTE]
>
>De [!DNL Chatlio] De bron is in bèta. Lees de [overzicht van bronnen](../../../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bronnen met een bètalabel.

Deze zelfstudie bevat stappen voor het maken van een [!DNL Chatlio] bronverbinding via de Adobe Experience Platform-gebruikersinterface.

## Aan de slag {#getting-started}

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waarbinnen [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema-editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe u aangepaste schema&#39;s maakt met de gebruikersinterface van de Schema-editor.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

## Vereisten {#prerequisites}

De volgende sectie bevat informatie over voorwaarden die moeten worden voltooid voordat u een [!DNL Chatlio] bronverbinding.

### Voorbeeld-JSON om het bronschema te definiëren voor [!DNL Chatlio] {#prerequisites-json-schema}

Voordat u een [!DNL Chatlio] bronverbinding, zult u een bronschema vereisen om worden verstrekt. U kunt de JSON hieronder gebruiken.

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

### Een platformschema maken voor [!DNL Chatlio] {#create-platform-schema}

U moet ook ervoor zorgen dat u een schema van het Platform voor uw bron creeert te gebruiken. Lees de zelfstudie aan [een platformschema maken](../../../../../xdm/schema/composition.md) voor uitvoerige stappen op hoe te om een schema tot stand te brengen.

![De interface van het Platform die een voorbeeldschema voor Chatlio toont](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/schema.png)

## Verbind uw [!DNL Chatlio] account {#connect-account}

Selecteer in de interface Platform de optie **[!UICONTROL Sources]** van de linkernavigatie om tot [!UICONTROL Sources] en bekijk een catalogus met bronnen die beschikbaar zijn in het Experience Platform.

Gebruik de *[!UICONTROL Categories]* om bronnen op categorie te filteren. U kunt ook een bronnaam invoeren in de zoekbalk om een specifieke bron uit de catalogus te zoeken.

Ga naar de [!UICONTROL Marketing automation] categorie om de [!DNL Chatlio] bronkaart. Selecteer **[!UICONTROL Add data]**.

![De Platform UI-catalogus met Chatlio-kaart](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/catalog.png)

## Gegevens selecteren {#select-data}

De **[!UICONTROL Select data]** wordt weergegeven, zodat u een interface hebt waarmee u de gegevens kunt selecteren die u naar het platform wilt verzenden.

* Het linkergedeelte van de interface is een browser waarmee u de beschikbare gegevensstromen binnen uw account kunt bekijken.
* In het rechtergedeelte van de interface kunt u maximaal 100 rijen gegevens uit een JSON-bestand voorvertonen.

Selecteren **[!UICONTROL Upload files]** om een JSON-bestand vanaf uw lokale systeem te uploaden. U kunt ook het JSON-bestand dat u wilt uploaden, slepen naar het [!UICONTROL Drag and drop files] deelvenster.

![De stap Gegevens toevoegen van de bronwerkstroom.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/add-data.png)

Nadat het bestand is geüpload, wordt de voorbeeldinterface bijgewerkt en wordt een voorvertoning weergegeven van het schema dat u hebt geüpload. Met de voorvertoningsinterface kunt u de inhoud en structuur van een bestand controleren. U kunt ook de opdracht [!UICONTROL Search field] nut om tot specifieke punten van binnen uw schema toegang te hebben.

Selecteer **[!UICONTROL Next]**.

![De voorbeeldstap van de bronworkflow.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/preview.png)

## Gegevens {#dataflow-detail}

De **Gegevens** de stap verschijnt, die u van opties voorzien om een bestaande dataset te gebruiken of een nieuwe dataset voor uw gegevensstroom te vestigen, evenals een kans om een naam en een beschrijving voor uw gegevensstroom te verstrekken. Tijdens deze stap kunt u ook instellingen configureren voor het opnemen van profielen, foutdiagnose, gedeeltelijke inname en waarschuwingen.

Selecteer **[!UICONTROL Next]**.

![De gegevensstroom-detailstap van het bronwerkschema.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/dataflow-detail.png)

## Toewijzing {#mapping}

De [!UICONTROL Mapping] de stap verschijnt, die u van een interface voorziet om de brongebieden van uw bronschema aan hun aangewezen doelXDM gebieden in het doelschema in kaart te brengen.

Platform biedt intelligente aanbevelingen voor automatisch toegewezen velden op basis van het doelschema of de gegevensset die u hebt geselecteerd. U kunt toewijzingsregels handmatig aanpassen aan uw gebruiksgevallen. Op basis van uw behoeften kunt u ervoor kiezen om velden rechtstreeks toe te wijzen of gegevens prep-functies te gebruiken om brongegevens om berekende of berekende waarden af te leiden. Voor uitvoerige stappen bij het gebruiken van de kaartperinterface en berekende gebieden, zie [UI-hulplijn voor gegevensvoorinstelling](../../../../../data-prep/ui/mapping.md).

De onderstaande toewijzingen zijn verplicht en moeten worden ingesteld voordat u verdergaat met de [!UICONTROL Review] in het werkgebied.

| Doelveld | Beschrijving |
| --- | --- |
| `UUID` | De [!DNL Chatlio] id voor de gebeurtenis. |

Als de brongegevens zijn toegewezen, selecteert u **[!UICONTROL Next]**.

![De toewijzingsstap van de workflow voor bronnen.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/mapping.png)

## Controleren {#review}

De **[!UICONTROL Review]** wordt weergegeven, zodat u de nieuwe gegevensstroom kunt controleren voordat deze wordt gemaakt. De details worden gegroepeerd in de volgende categorieën:

* **[!UICONTROL Connection]**: Hiermee geeft u het brontype, het relevante pad van het gekozen bronbestand en de hoeveelheid kolommen in dat bronbestand weer.
* **[!UICONTROL Assign dataset & map fields]**: Toont welke dataset de brongegevens worden opgenomen in, met inbegrip van het schema dat de dataset volgt.

Nadat u de gegevensstroom hebt gecontroleerd, selecteert u **[!UICONTROL Finish]** en laat enige tijd voor de gegevensstroom worden gecreeerd.

![De revisiestap van de workflow voor bronnen.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/review.png)

## Uw URL voor het streamingeindpunt ophalen {#get-streaming-endpoint-url}

Wanneer uw streaminggegevens zijn gemaakt, kunt u nu de URL van het streamingeindpunt ophalen. Dit eindpunt zal worden gebruikt om aan uw webhaak in te tekenen, toestaand uw het stromen bron om met Experience Platform te communiceren.

Om URL te construeren die wordt gebruikt om webhaak te vormen op [!DNL Chatlio] u moet het volgende terugwinnen:

* **[!UICONTROL Dataflow ID]**
* **[!UICONTROL Streaming endpoint]**

Om uw **[!UICONTROL Dataflow ID]** en **[!UICONTROL Streaming endpoint]**, ga naar de [!UICONTROL Dataflow activity] pagina van de gegevensstroom die u net creeerde en kopieer de details van de bodem van [!UICONTROL Properties] deelvenster.

![Het het stromen eindpunt in dataflow activiteit.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/endpoint-test.png)

Zodra u uw het stromen eindpunt en dataflow identiteitskaart hebt teruggewonnen, bouw een URL die op het volgende patroon wordt gebaseerd: ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```. Een geconstrueerde URL voor een webhaak ziet er bijvoorbeeld als volgt uit: ``https://dcs.adobedc.net/collection/d56b47ee3985104beaf724efcd78a3e1a863d720471a482bebac0acc1ab95983``

## Webhaak instellen in [!DNL Chatlio] {#set-up-webhook}

Als u de URL van uw webhaak hebt gemaakt, kunt u nu de webhaak instellen met de [!DNL Chatlio] gebruikersinterface.

Aanmelden bij uw [[!DNL Chatlio]](https://chatlio.com/) account en volgen [de gids over installatie en installatie](https://chatlio.com/docs/setup/) om een widget te maken.

Wanneer een widget is gemaakt, navigeert u naar de instellingenpagina van de widget om uw webhaak-URL aan die widget toe te voegen.

![De pagina met instellingen voor de webhaak in Chatlio.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/widget-settings.png)

Selecteer vervolgens de **[!DNL Behavior]** en voeg uw webhaak-URL toe aan de *[!DNL Webhook when a new conversation starts]* veld en andere webhaakgebeurtenisvelden waarop u zich wilt abonneren.

![De Chatlio UI die het WebHaak eindpuntgebied toont.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/webhook.png)

>[!TIP]
>
>U kunt zich abonneren op verschillende gebeurtenissen voor uw [!DNL Chatlio] webhaak. Voor meer informatie over de verschillende gebeurtenissen raadpleegt u de [[!DNL Chatlio] documentatie bij gebeurtenissen](https://chatlio.com/docs/webhooks/).

## Volgende stappen {#next-steps}

Aan de hand van deze zelfstudie hebt u een streaminggegevensstroom geconfigureerd om uw [!DNL Chatlio] gegevens naar Experience Platform. Als u de gegevens wilt controleren die worden ingevoerd, raadpleegt u de handleiding op [streaming gegevens controleren met behulp van platforminterface](../../monitor-streaming.md).

## Aanvullende bronnen {#additional-resources}

In de volgende secties vindt u aanvullende bronnen die u kunt raadplegen wanneer u de [!DNL Chatlio] bron.

### Validatie {#validation}

Om te controleren of u de bron correct hebt ingesteld en [!DNL Chatlio] de berichten worden opgenomen, volg de stappen hieronder:

* U kunt de [!DNL Chatlio] **[!UICONTROL Reports]** > **[!UICONTROL Chat History]** pagina om de gebeurtenissen te identificeren waarop [!DNL Chatlio].

![Chatlio UI-screenshot met chatgeschiedenis](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/chatlio-chat-history.png)

* Selecteer in de interface Platform de optie **[!UICONTROL View Dataflows]** naast de [!DNL Chatlio] kaartmenu in de broncatalogus. Selecteer vervolgens **[!UICONTROL Preview dataset]** om de gegevens te verifiëren die voor de webhaken werden opgenomen die u binnen hebt gevormd [!DNL Chatlio].

![Platform UI-screenshot met ingesloten gebeurtenissen](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/platform-dataset.png)

Voor aanvullende informatie over [!DNL Chatlio], bezoek de [[!DNL Chatlio] documentatie](https://chatlio.com/docs/) en [Veelgestelde vragen](https://chatlio.com/pricing/#FAQ).

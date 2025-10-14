---
title: Connect Relay to Experience Platform in de gebruikersinterface
description: Leer hoe te om een verbinding van de Verbinding van de Verbinding van de Relais douanebron tot stand te brengen gebruikend de UI van Adobe Experience Platform.
exl-id: f80855f5-0769-4253-b737-28c46e4dea6e
source-git-commit: bd5611b23740f16e41048f3bc65f62312593a075
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---

# Connect Relay to Experience Platform in de gebruikersinterface

>[!NOTE]
>
>De bron [!DNL Relay Connector] is in bèta. Gelieve te lezen het [&#x200B; overzicht van bronnen &#x200B;](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

Met [!DNL Relay Connector] kunt u uw klanten op de meest betekenisvolle momenten in hun reis persoonlijke ervaringen bieden, zodat u sterkere relaties kunt opbouwen en meer loyaliteit en waarde kunt creëren door een binnenkomende verbinding te maken met streaming gebeurtenissen vanaf de [!DNL Relay Network] -integratie in Adobe Experience Platform.

Lees deze handleiding voor meer informatie over het gebruik van de [!DNL Relay Connector] in de werkruimte Bronnen van de gebruikersinterface van Experience Platform.

>[!IMPORTANT]
>
>Deze documentatiepagina wordt bijgehouden door het team van *[!DNL Relay Network]* . Voor om het even welke vragen of updateverzoeken, gelieve hen direct in *[[!DNL Relay Network]te contacteren &#x200B;](https://www.relaynetwork.com/) of e-mail [&#x200B; info@relaynetwork.com](mailto:info@relaynetwork.com)*.

## Sluit de [!DNL Relay Connector] -bron aan

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatiebalk voor toegang tot de werkruimte van [!UICONTROL Sources] . In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken. U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm of de zoekoptie gebruiken om een specifieke bron te zoeken.

Selecteer onder de categorie *[!UICONTROL Marketing automation]* de [!DNL Relay Connector] bronkaart en selecteer **[!UICONTROL Add data]** .

>[!TIP]
>
>Bronnen in de catalogus met bronnen geven de optie **[!UICONTROL Set up]** weer wanneer er geen geverifieerde account bestaat. Als een account eenmaal is geverifieerd, verandert deze optie in **[!UICONTROL Add data]** .

![&#x200B; de cataloguspagina van de bronwerkruimte.](../../../../images/tutorials/create/relay-connector/relay-source.jpg)

### Gegevens selecteren

De interface **[!UICONTROL Connect Relay Connector source]** wordt weergegeven. Gebruik de interface van *[!UICONTROL Select data]* om het schema van brongegevens te doorbladeren of te specificeren. U kunt ook een JSON-voorbeeldbestand uploaden om het bronschema te definiëren.

>[!NOTE]
>
>De aanvaardbare bestandsgrootte is maximaal 1 GB.

![&#x200B; de uitgezochte gegevensinterface &#x200B;](../../../../images/tutorials/create/relay-connector/upload-data.jpg)

Nadat de gegevens zijn geüpload, kunt u de sectie [!UICONTROL Preview sample data] gebruiken om een voorvertoning van de gegevens weer te geven.

![&#x200B; de geüploade gegevens.](../../../../images/tutorials/create/relay-connector/uploaded-data.jpg)

### Gegevens gegevensstroom

Daarna, gebruik de *[!UICONTROL Dataflow details]* interface om a **naam** en een **facultatieve beschrijving** voor uw dataflow te verstrekken. Selecteer bovendien de **[!UICONTROL Target dataset]** die u wilt gebruiken. U kunt of een nieuwe dataset tot stand brengen of een bestaande dataset gebruiken.

![&#x200B; de dataflow detailinterface. &#x200B;](../../../../images/tutorials/create/relay-connector/dataflow.jpg)

### Toewijzing

U kunt uw brongebieden aan XDM schemagebieden in kaart brengen gebruikend de auto-kaartfunctionaliteit, die gebieden aanpast die op hun namen worden gebaseerd, of douaneafbeeldingen voor nauwkeurigere controle tot stand brengen. Indien nodig, kunt u transformaties zoals aaneenschakeling, het formatteren, of het anders noemen ook toepassen om uw gegevens te verzekeren past perfect in het doelschema. Voor meer informatie bij afbeelding, lees de [&#x200B; gids UI van de Prep van Gegevens &#x200B;](../../../../../data-prep/ui/mapping.md).

![&#x200B; de toewijzingsinterface in het bronwerkschema.](../../../../images/tutorials/create/relay-connector/mapping.jpg)

>[!TIP]
>
>Voor details op de types van gebeurtenissen en gegevenswaarden die het Relais naar uw bron zal verzenden, lees de [[!DNL Relay Network]  Push Events &#x200B;](https://docs.relaynetwork.com/docs/push-events) documentatie. Deze informatie zal u helpen uw **Schema van de Gebeurtenissen van de Ervaring** geschikt ontwerpen.

### Controleren

Tot slot herzie alle configuraties met inbegrip van uw **bron, dataset, en afbeeldingen**. Wanneer gebeëindigd, uitgezochte **Afwerking** om dataflow tot stand te brengen.

![&#x200B; de overzichtsstap van het bronwerkschema.](../../../../images/tutorials/create/relay-connector/review.jpg)

### Win uw het stromen eindpunt URL terug

Zodra u dataflow hebt gecreeerd, zult u het *stromen eindpunt URL* en andere verwante details in de **sectie van Eigenschappen** op de rechterkant van de dataflow pagina vinden.

![&#x200B; de dataflow eigenschappen &#x200B;](../../../../images/tutorials/create/relay-connector/streaming-endpoint.jpg)

Gebruik deze waarden aan opstelling webhaak in de **console van het Relais**. Voor gedetailleerde instructies bij het vormen van de duw, zie de documentatie van het Relais: [&#x200B; Vormend de Duw API &#x200B;](https://docs.relaynetwork.com/docs/configuring-the-push-api).

## Aanvullende bronnen

* [&#x200B; creeer een nieuwe verbindingsspecificatie gebruikend de Dienst API van de Stroom &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-platform/sources/sdk/streaming-sdk/create)
* [&#x200B; verbind met uw bron gebruikend UI &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-platform/sources/sdk/streaming-sdk/submit#test-your-source-using-the-ui)

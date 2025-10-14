---
title: Een slimme streamingverbinding en gegevensstroom maken in de gebruikersinterface
description: Leer hoe u via de Experience Platform-gebruikersinterface een Shopify Streaming-bronverbinding en -gegevensstroom maakt
badge: Beta
exl-id: d53f4ab5-8bdc-4647-83d5-ee898abda0f2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 0%

---

# Een bronverbinding en gegevensstroom maken voor [!DNL Shopify Streaming] -gegevens met behulp van de interface

Deze zelfstudie bevat stappen voor het maken van een [!DNL Shopify Streaming] bronverbinding en gegevensstroom via de Experience Platform-gebruikersinterface.

## Aan de slag {#getting-started}

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem &#x200B;](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   * [&#x200B; Grondbeginselen van schemacompositie &#x200B;](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [&#x200B; het leerprogramma van de Redacteur van het Schema &#x200B;](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

>[!IMPORTANT]
>
>Deze zelfstudie vereist dat u de vereiste instellingen voor uw [!DNL Shopify Streaming] -account hebt voltooid. Voor stappen bij vestiging uw rekening, lees het [[!DNL Shopify Streaming]  overzicht &#x200B;](../../../../connectors/ecommerce/shopify-streaming.md).

## Sluit uw [!DNL Shopify Streaming] -account aan

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatiebalk voor toegang tot de werkruimte van [!UICONTROL Sources] . In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de **eCommerce** categorie, selecteer [!DNL Shopify Streaming], en selecteer dan **[!UICONTROL Add data]**.

![&#x200B; de Experience Platform broncatalogus &#x200B;](../../../../images/tutorials/create/shopify-streaming/catalog.png)

## Gegevens selecteren

De stap **[!UICONTROL Select data]** wordt weergegeven en biedt een interface waarmee u de gegevens kunt selecteren die u naar Experience Platform verzendt.

* Het linkergedeelte van de interface is een browser waarmee u de beschikbare gegevensstromen binnen uw account kunt bekijken.
* In het rechtergedeelte van de interface kunt u maximaal 100 rijen gegevens uit een JSON-bestand voorvertonen.

Selecteer **[!UICONTROL Upload files]** om een JSON-bestand van uw lokale systeem te uploaden. U kunt ook het JSON-bestand dat u wilt uploaden naar het deelvenster [!UICONTROL Drag and drop files] slepen.

![&#x200B; voegt gegevensstap van het bronwerkschema toe.](../../../../images/tutorials/create/shopify-streaming/select-data.png)

Nadat het bestand is geüpload, wordt de voorbeeldinterface bijgewerkt en wordt een voorvertoning weergegeven van het schema dat u hebt geüpload. Met de voorvertoningsinterface kunt u de inhoud en structuur van een bestand controleren. U kunt het hulpprogramma [!UICONTROL Search field] ook gebruiken om toegang te krijgen tot specifieke items binnen uw schema.

Selecteer **[!UICONTROL Next]** als u klaar bent.

![&#x200B; de voorproefstap van het bronwerkschema.](../../../../images/tutorials/create/shopify-streaming/preview.png)

## Gegevens

De **Dataflow detailstap** verschijnt, die u van opties voorzien om een bestaande dataset te gebruiken of een nieuwe dataset voor uw dataflow te vestigen, evenals een kans om een naam en een beschrijving voor uw dataflow te verstrekken. Tijdens deze stap kunt u ook instellingen configureren voor het opnemen van profielen, foutdiagnose, gedeeltelijke inname en waarschuwingen.

Selecteer **[!UICONTROL Next]** als u klaar bent.

![&#x200B; dataflow-detail stap van het bronwerkschema.](../../../../images/tutorials/create/shopify-streaming/dataflow-detail.png)

## Toewijzing

De stap [!UICONTROL Mapping] verschijnt, die u van een interface voorziet om de brongebieden van uw bronschema aan hun aangewezen doelXDM gebieden in het doelschema in kaart te brengen.

Experience Platform biedt intelligente aanbevelingen voor automatisch toegewezen velden op basis van het doelschema of de gegevensset die u selecteert. U kunt toewijzingsregels handmatig aanpassen aan uw gebruiksgevallen. Op basis van uw behoeften kunt u ervoor kiezen om velden rechtstreeks toe te wijzen of gegevens prep-functies te gebruiken om brongegevens om berekende of berekende waarden af te leiden. Voor uitvoerige stappen bij het gebruiken van de kaartperinterface en berekende gebieden, zie de [&#x200B; gids UI van de Prep van Gegevens &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/data-prep/ui/mapping.html?lang=nl-NL).

Selecteer **[!UICONTROL Next]** wanneer de brongegevens correct zijn toegewezen.

![&#x200B; de afbeeldingsstap van het bronwerkschema.](../../../../images/tutorials/create/shopify-streaming/mapping.png)

## Controleren

De stap **[!UICONTROL Review]** wordt weergegeven, zodat u de nieuwe gegevensstroom kunt bekijken voordat deze wordt gemaakt. De details worden gegroepeerd in de volgende categorieën:

* **[!UICONTROL Connection]**: geeft het brontype, het relevante pad van het gekozen bronbestand en het aantal kolommen in dat bronbestand weer.
* **[!UICONTROL Assign dataset & map fields]**: Toont welke dataset de brongegevens worden opgenomen in, met inbegrip van het schema dat de dataset volgt aan.

Nadat u de gegevensstroom hebt gereviseerd, selecteert u **[!UICONTROL Finish]** en laat u enige tijd over om de gegevensstroom te maken.

![&#x200B; de overzichtsstap van het bronwerkschema.](../../../../images/tutorials/create/shopify-streaming/review.png)

## Uw URL voor het streamingeindpunt ophalen

Wanneer uw streaminggegevens zijn gemaakt, kunt u nu de URL van het streamingeindpunt ophalen. Dit eindpunt wordt gebruikt om een abonnement te nemen op uw webhaak, zodat uw streamingbron kan communiceren met Experience Platform.

Als u het streamingeindpunt wilt ophalen, gaat u naar de [!UICONTROL Dataflow activity] -pagina van de gegevensstroom die u net hebt gemaakt en kopieert u het eindpunt van de onderkant van het deelvenster [!UICONTROL Properties] .

![&#x200B; het stromen eindpunt in dataflow activiteit.](../../../../images/tutorials/create/shopify-streaming/endpoint.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een bronverbinding en gegevensstroom tot stand gebracht voor uw [!DNL Shopify Streaming] -account. Voor instructies op hoe te om uw [!DNL Shopify Streaming] rekening te verbinden gebruikend API, te lezen gelieve het leerprogramma op [&#x200B; creërend een bronverbinding en dataflow aan stroom  [!DNL Shopify]  gegevens gebruikend de Dienst API van de Stroom &#x200B;](../../../api/create/ecommerce/shopify-streaming.md).

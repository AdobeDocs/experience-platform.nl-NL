---
title: Een slimme streamingverbinding en gegevensstroom maken in de gebruikersinterface
description: Leer hoe u via de gebruikersinterface van het Platform een Shopify Streaming-bronverbinding en -gegevensstroom maakt
badge: Beta
exl-id: 3368ecf6-0c61-49ce-bc9c-29ee50b3f037
source-git-commit: feb05d5bddc4135c5fe14d3ec5d8fad62c5e2236
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 0%

---

# Een bronverbinding en gegevensstroom maken voor [!DNL Shopify Streaming] gegevens die de UI gebruiken

Deze zelfstudie bevat stappen voor het maken van een [!DNL Shopify Streaming] bronverbinding en gegevensstroom via de gebruikersinterface van het Platform.

## Aan de slag {#getting-started}

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema Editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

>[!IMPORTANT]
>
>Voor deze zelfstudie moet u de vereiste installatie voor uw [!DNL Shopify Streaming] account. Voor stappen voor het instellen van uw account, leest u de [[!DNL Shopify Streaming] overzicht](../../../../connectors/ecommerce/shopify-streaming.md).

## Verbind uw [!DNL Shopify Streaming] account

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Sources]** van de linkernavigatiebalk voor toegang tot de [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de **eCommerce** categorie, selecteert u [!DNL Shopify Streaming]en selecteer vervolgens **[!UICONTROL Add data]**.

![De catalogus met bronnen voor Experience Platforms](../../../../images/tutorials/create/shopify-streaming/catalog.png)

## Gegevens selecteren

De **[!UICONTROL Select data]** wordt weergegeven, zodat u de gegevens kunt selecteren die u naar het Platform verzendt.

* Het linkergedeelte van de interface is een browser waarmee u de beschikbare gegevensstromen binnen uw account kunt bekijken.
* In het rechtergedeelte van de interface kunt u maximaal 100 rijen gegevens uit een JSON-bestand voorvertonen.

Selecteren **[!UICONTROL Upload files]** om een JSON-bestand vanaf uw lokale systeem te uploaden. U kunt ook het JSON-bestand dat u wilt uploaden, slepen naar het [!UICONTROL Drag and drop files] deelvenster.

![De stap Gegevens toevoegen van de bronwerkstroom.](../../../../images/tutorials/create/shopify-streaming/select-data.png)

Nadat het bestand is geüpload, wordt de voorbeeldinterface bijgewerkt en wordt een voorvertoning weergegeven van het schema dat u hebt geüpload. Met de voorvertoningsinterface kunt u de inhoud en structuur van een bestand controleren. U kunt ook de opdracht [!UICONTROL Search field] nut om tot specifieke punten van binnen uw schema toegang te hebben.

Als u klaar bent, selecteert u **[!UICONTROL Next]**.

![De voorvertoningsstap van de workflow voor bronnen.](../../../../images/tutorials/create/shopify-streaming/preview.png)

## Gegevens

De **Gegevens** de stap verschijnt, die u van opties voorzien om een bestaande dataset te gebruiken of een nieuwe dataset voor uw gegevensstroom te vestigen, evenals een kans om een naam en een beschrijving voor uw gegevensstroom te verstrekken. Tijdens deze stap kunt u ook instellingen configureren voor het opnemen van profielen, foutdiagnose, gedeeltelijke inname en waarschuwingen.

Als u klaar bent, selecteert u **[!UICONTROL Next]**.

![De gegevensstroom-detailstap van het bronwerkschema.](../../../../images/tutorials/create/shopify-streaming/dataflow-detail.png)

## Toewijzing

De [!UICONTROL Mapping] de stap verschijnt, die u van een interface voorziet om de brongebieden van uw bronschema aan hun aangewezen doelXDM gebieden in het doelschema in kaart te brengen.

Platform biedt intelligente aanbevelingen voor automatisch toegewezen velden op basis van het doelschema of de gegevensset die u selecteert. U kunt toewijzingsregels handmatig aanpassen aan uw gebruiksgevallen. Op basis van uw behoeften kunt u ervoor kiezen om velden rechtstreeks toe te wijzen of gegevens prep-functies te gebruiken om brongegevens om berekende of berekende waarden af te leiden. Voor uitvoerige stappen bij het gebruiken van de kaartperinterface en berekende gebieden, zie [UI-hulplijn voor gegevensvoorinstelling](https://experienceleague.adobe.com/docs/experience-platform/data-prep/ui/mapping.html).

Als de brongegevens eenmaal zijn toegewezen, selecteert u **[!UICONTROL Next]**.

![De toewijzingsstap van de workflow voor bronnen.](../../../../images/tutorials/create/shopify-streaming/mapping.png)

## Controleren

De **[!UICONTROL Review]** wordt weergegeven, zodat u de nieuwe gegevensstroom kunt controleren voordat deze wordt gemaakt. De details worden gegroepeerd in de volgende categorieën:

* **[!UICONTROL Connection]**: Toont het brontype, de relevante weg van het gekozen brondossier, en het aantal kolommen binnen dat brondossier.
* **[!UICONTROL Assign dataset & map fields]**: Toont welke dataset de brongegevens worden opgenomen in, met inbegrip van het schema dat de dataset zich aan houdt.

Nadat u de gegevensstroom hebt gecontroleerd, selecteert u **[!UICONTROL Finish]** en laat enige tijd voor de gegevensstroom worden gecreeerd.

![De revisiestap van de workflow voor bronnen.](../../../../images/tutorials/create/shopify-streaming/review.png)

## Uw URL voor het streamingeindpunt ophalen

Wanneer uw streaminggegevens zijn gemaakt, kunt u nu de URL van het streamingeindpunt ophalen. Dit eindpunt zal worden gebruikt om aan uw webhaak in te tekenen, toestaand uw het stromen bron om met Experience Platform te communiceren.

Ga naar het tabblad [!UICONTROL Dataflow activity] pagina van de gegevensstroom die u enkel creeerde en het eindpunt van de bodem kopieert [!UICONTROL Properties] deelvenster.

![Het het stromen eindpunt in dataflow activiteit.](../../../../images/tutorials/create/shopify-streaming/endpoint.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een bronverbinding en gegevensstroom tot stand gebracht [!DNL Shopify Streaming] account. Voor instructies over hoe te om uw te verbinden [!DNL Shopify Streaming] account met de API, lees de zelfstudie op [een bronverbinding en gegevensstroom maken [!DNL Shopify] gegevens die de Flow Service API gebruiken](../../../api/create/ecommerce/shopify-streaming.md).

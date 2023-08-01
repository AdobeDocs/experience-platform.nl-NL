---
title: Sluit uw RainFocus-account aan op het Experience Platform via de gebruikersinterface
description: Leer hoe u uw RainFocus-account met Experience Platform kunt verbinden via de gebruikersinterface.
badge: Beta
source-git-commit: 1ed82798125f32fe392f2a06a12280ac61f225c6
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---

# Verbind uw [!DNL RainFocus] account aan Experience Platform met behulp van de gebruikersinterface

>[!NOTE]
>
>De [!DNL RainFocus] De bron is in bèta. Zie de [overzicht van bronnen](../../../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bronnen met een bètalabel.

Deze zelfstudie bevat stappen voor het tot stand brengen van een verbinding met uw [!DNL RainFocus] account- en stream-gebeurtenisbeheer en analysegegevens naar Adobe Experience Platform.

>[!IMPORTANT]
>
>Deze bronschakelaar en documentatiepagina worden gecreeerd en gehandhaafd door [!DNL RainFocus] team. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen met de klant<span>@rainfocus.com of ga naar de [[!DNL RainFocus] Help Center](https://help.rainfocus.com/hc/en-us)

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema-editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe u aangepaste schema&#39;s maakt met de gebruikersinterface van de Schema-editor.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

### Vereisten

Voordat u verbinding kunt maken met uw [!DNL RainFocus] account aan Experience Platform, moet u eerst de volgende vereiste taken uitvoeren:

* [Vereiste referenties verzamelen](../../../../connectors/analytics/rainfocus.md#gather-required-credentials)
* [Een XDM-schema maken en het identiteitsveld definiëren](../../../../connectors/analytics/rainfocus.md#create-an-xdm-schema-and-define-the-identity-field)
* [Een integratieprofiel maken in RainFocus](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus)

Nadat u de vereiste instellingen hebt voltooid, kunt u de onderstaande stappen uitvoeren.

## Sluit uw RainFocus-account aan op Experience Platform

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Sources]** in de linkernavigatiebalk om de werkruimte Bronnen te openen. De *[!UICONTROL Catalog]* in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de *[!UICONTROL Analytics]* categorie, selecteert u **[!UICONTROL RainFocus Experience]** en selecteer vervolgens **[!UICONTROL Add data]**.

![De broncatalogus op Experience Platform UI met de bron RainFocus geselecteerd.](/help/sources/images/tutorials/create/rainfocus/rainfocus_sources-rf.png)

## Gegevens selecteren

De stap Gegevens selecteren wordt weergegeven en biedt een interface waarmee u de gegevens kunt selecteren die u naar het Experience Platform verzendt.

* Het linkergedeelte van de interface is een browser waarmee u de beschikbare gegevensstromen binnen uw account kunt bekijken.
* In het rechtergedeelte van de interface kunt u maximaal 100 rijen gegevens uit een JSON-bestand voorvertonen.

Selecteren **[!UICONTROL Upload files]** om een JSON-bestand vanaf uw lokale systeem te uploaden. U kunt ook het JSON-bestand dat u wilt uploaden, slepen naar het deelvenster Bestanden slepen en neerzetten.

Upload de Sample JSON Payload die u hebt gedownload van **RainFocus**.

![De geselecteerde gegevensstap in de bronwerkstroom.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-upload.png)

Nadat het bestand is geüpload, wordt de voorbeeldinterface bijgewerkt en wordt een voorvertoning weergegeven van het schema dat u hebt geüpload. Met de voorvertoningsinterface kunt u de inhoud en structuur van een bestand controleren. U kunt het het gebiedsnut van het Onderzoek ook gebruiken om tot specifieke punten van binnen uw schema toegang te hebben.

Selecteer **[!UICONTROL Next]**.

![De stap voor gegevensvoorvertoning van de workflow voor bronnen.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-preview.png)

## Gegevens

De **Gegevens** de stap verschijnt, die u van opties voorzien om een bestaande dataset te gebruiken of een nieuwe dataset voor uw gegevensstroom te vestigen, evenals een kans om een naam en een beschrijving voor uw gegevensstroom te verstrekken. Tijdens deze stap kunt u ook instellingen configureren voor het opnemen van profielen, foutdiagnose, gedeeltelijke inname en waarschuwingen.

Selecteer **[!UICONTROL Next]**.

![De stap met details van de gegevensstroom van de bronworkflow.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-setup.png)

## Toewijzing {#mapping}

De stap van de Afbeelding verschijnt, die u van een interface voorziet om de brongebieden van uw bronschema aan hun aangewezen doelXDM gebieden in het doelschema in kaart te brengen.

Experience Platform biedt intelligente aanbevelingen voor automatisch toegewezen velden op basis van het doelschema of de gegevensset die u hebt geselecteerd. U kunt toewijzingsregels handmatig aanpassen aan uw gebruiksgevallen. Op basis van uw behoeften kunt u ervoor kiezen om velden rechtstreeks toe te wijzen of gegevens prep-functies te gebruiken om brongegevens om berekende of berekende waarden af te leiden. Voor uitvoerige stappen bij het gebruiken van de kaartperinterface en berekende gebieden, zie [UI-hulplijn voor gegevensvoorinstelling](../../../../../data-prep/ui/mapping.md).

Als de brongegevens zijn toegewezen, selecteert u **[!UICONTROL Next]**.

![De toewijzingsstap van de workflow voor bronnen.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-mappings.png)

## Controleren

De **Controleren** wordt weergegeven, zodat u de nieuwe gegevensstroom kunt controleren voordat deze wordt gemaakt. De details worden gegroepeerd in de volgende categorieën:

* **Verbinding**: Hiermee geeft u het brontype, het relevante pad van het gekozen bronbestand en de hoeveelheid kolommen in dat bronbestand weer.
* **Gegevensset- en kaartvelden toewijzen**: Toont welke dataset de brongegevens worden opgenomen in, met inbegrip van het schema dat de dataset volgt.

Nadat u de gegevensstroom hebt gecontroleerd, selecteert u **Voltooien** en laat enige tijd voor de gegevensstroom worden gecreeerd.

![De revisiestap van de workflow voor bronnen.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-compelete.png)

## Uw URL voor het streamingeindpunt ophalen {#get-your-streaming-endpoint-url}

Wanneer uw streaminggegevens zijn gemaakt, kunt u nu de URL van het streamingeindpunt ophalen. Dit eindpunt zal worden gebruikt om aan uw webhaak in te tekenen, toestaand uw het stromen bron om met Experience Platform te communiceren.

Ga naar het tabblad *[!UICONTROL Dataflow activity]* pagina van de gegevensstroom die u enkel creeerde en het eindpunt van de bodem kopieert *[!UICONTROL Properties]* deelvenster.

![De pagina met gegevensstroomactiviteit in de bronwerkruimte, met het stromen eindpunt URL benadrukt.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-api.png)

## Uw integratieprofiel activeren in RainFocus

Zodra uw gegevensstroom volledig is en u uw het stromen eindpunt URL hebt teruggewonnen, kunt u nu activeren [!DNL Integration Profile] in [!DNL RainFocus].

* Aanmelden bij [[!DNL RainFocus] platform](https://app.rainfocus.com). Selecteer in de primaire navigatie de optie **[!DNL Libraries]** en **[!DNL Integration Profiles]**
* Open de [!DNL Integration Profile] die u eerder hebt gemaakt als onderdeel van het dialoogvenster [voorwaarden](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus).
* Plak de **Dataflow-id** en **Streaming eindpunt** gekopieerd uit de Dataflow in Experience Platform en selecteer **Opslaan**

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht voor uw [!DNL RainFocus] bron, zodat u uw gebeurtenisbeheer- en analysegegevens naar het Experience Platform kunt streamen.

## Aanvullende bronnen

De volgende documenten bieden aanvullende richtsnoeren voor nuances rond de [!DNL RainFocus] bron.

* [RainFocus Help Center](https://help.rainfocus.com/hc/en-us)
* [Een Adobe Service-account (JWT) maken in de Adobe Developer Portal](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)
* [Een schema maken in de API](../../../../../xdm/tutorials/create-schema-api.md)
* [Een schema maken in de gebruikersinterface](../../../../../xdm/tutorials/create-schema-ui.md)
* [Identiteitsvelden definiëren in de gebruikersinterface](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html)
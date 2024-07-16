---
title: Sluit uw RainFocus-account aan op het Experience Platform via de gebruikersinterface
description: Leer hoe u uw RainFocus-account met Experience Platform kunt verbinden via de gebruikersinterface.
badge: Beta
exl-id: a349e37e-9f2c-47ff-8360-ccbe578dce27
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 0%

---

# Sluit uw [!DNL RainFocus] -account aan op het Experience Platform via de gebruikersinterface

>[!NOTE]
>
>De bron [!DNL RainFocus] is in bèta. Zie het [ overzicht van bronnen ](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

Deze zelfstudie bevat stappen voor het verbinden van uw [!DNL RainFocus] -account en het streamen van gebeurtenisbeheer- en analysegegevens met Adobe Experience Platform.

>[!IMPORTANT]
>
>Deze bronaansluiting en documentatiepagina worden gemaakt en onderhouden door het team van [!DNL RainFocus] . Voor om het even welke onderzoeken of updateverzoeken, gelieve hen direct bij cliëntcare <span> te contacteren@rainfocus.com of het [[!DNL RainFocus]  Centrum van de Hulp ](https://help.rainfocus.com/hc/en-us) te bezoeken

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

### Vereisten

Voordat u een verbinding tot stand kunt brengen tussen uw [!DNL RainFocus] -account en het Experience Platform, moet u eerst de volgende taken uitvoeren:

* [Vereiste referenties verzamelen](../../../../connectors/analytics/rainfocus.md#gather-required-credentials)
* [Een XDM-schema maken en het identiteitsveld definiëren](../../../../connectors/analytics/rainfocus.md#create-an-xdm-schema-and-define-the-identity-field)
* [Een integratieprofiel maken in RainFocus](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus)

Nadat u de vereiste instellingen hebt voltooid, kunt u de onderstaande stappen uitvoeren.

## Sluit uw RainFocus-account aan op Experience Platform

Selecteer in de gebruikersinterface van het platform de optie **[!UICONTROL Sources]** in de linkernavigatiebalk voor toegang tot de werkruimte Bronnen. In het scherm *[!UICONTROL Catalog]* worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie *[!UICONTROL Analytics]* de optie **[!UICONTROL RainFocus Experience]** en selecteer vervolgens **[!UICONTROL Add data]** .

![ de broncatalogus op Experience Platform UI met geselecteerde bron RainFocus.](/help/sources/images/tutorials/create/rainfocus/rainfocus_sources-rf.png)

## Gegevens selecteren

De stap Gegevens selecteren wordt weergegeven en biedt een interface waarmee u de gegevens kunt selecteren die u naar het Experience Platform verzendt.

* Het linkergedeelte van de interface is een browser waarmee u de beschikbare gegevensstromen binnen uw account kunt bekijken.
* In het rechtergedeelte van de interface kunt u maximaal 100 rijen gegevens uit een JSON-bestand voorvertonen.

Selecteer **[!UICONTROL Upload files]** om een JSON-bestand van uw lokale systeem te uploaden. U kunt ook het JSON-bestand dat u wilt uploaden, slepen naar het deelvenster Bestanden slepen en neerzetten.

Upload Steekproef JSON die nuttige lading van **RainFocus** wordt gedownload.

![ de uitgezochte gegevensstap in het bronwerkschema.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-upload.png)

Nadat het bestand is geüpload, wordt de voorbeeldinterface bijgewerkt en wordt een voorvertoning weergegeven van het schema dat u hebt geüpload. Met de voorvertoningsinterface kunt u de inhoud en structuur van een bestand controleren. U kunt het het gebiedsnut van het Onderzoek ook gebruiken om tot specifieke punten van binnen uw schema toegang te hebben.

Selecteer **[!UICONTROL Next]** als u klaar bent.

![ de stap van de gegevensvoorproef van het bronwerkschema.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-preview.png)

## Gegevens

De **Dataflow detailstap** verschijnt, die u van opties voorzien om een bestaande dataset te gebruiken of een nieuwe dataset voor uw dataflow te vestigen, evenals een kans om een naam en een beschrijving voor uw dataflow te verstrekken. Tijdens deze stap kunt u ook instellingen configureren voor het opnemen van profielen, foutdiagnose, gedeeltelijke inname en waarschuwingen.

Selecteer **[!UICONTROL Next]** als u klaar bent.

![ de dataflow detailstap van het bronwerkschema.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-setup.png)

## Toewijzing {#mapping}

De stap van de Afbeelding verschijnt, die u van een interface voorziet om de brongebieden van uw bronschema aan hun aangewezen doelXDM gebieden in het doelschema in kaart te brengen.

Experience Platform biedt intelligente aanbevelingen voor automatisch toegewezen velden op basis van het doelschema of de gegevensset die u hebt geselecteerd. U kunt toewijzingsregels handmatig aanpassen aan uw gebruiksgevallen. Op basis van uw behoeften kunt u ervoor kiezen om velden rechtstreeks toe te wijzen of gegevens prep-functies te gebruiken om brongegevens om berekende of berekende waarden af te leiden. Voor uitvoerige stappen bij het gebruiken van de kaartperinterface en berekende gebieden, zie de [ gids UI van de Prep van Gegevens ](../../../../../data-prep/ui/mapping.md).

Selecteer **[!UICONTROL Next]** wanneer de brongegevens correct zijn toegewezen.

![ de afbeeldingsstap van het bronwerkschema.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-mappings.png)

## Controleren

De **stap van het Overzicht** verschijnt, toestaand u om uw nieuwe dataflow te herzien alvorens het wordt gecreeerd. De details worden gegroepeerd in de volgende categorieën:

* **Verbinding**: Toont het brontype, de relevante weg van het gekozen brondossier, en de hoeveelheid kolommen binnen dat brondossier.
* **wijst dataset &amp; kaartgebieden** toe: Toont welke dataset de brongegevens in, met inbegrip van het schema worden opgenomen dat de dataset aan vasthoudt.

Zodra u uw dataflow hebt herzien, uitgezochte **Afwerking** en laat wat tijd voor dataflow toe om worden gecreeerd.

![ de overzichtsstap van het bronwerkschema.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-compelete.png)

## Uw URL voor het streamingeindpunt ophalen {#get-your-streaming-endpoint-url}

Wanneer uw streaminggegevens zijn gemaakt, kunt u nu de URL van het streamingeindpunt ophalen. Dit eindpunt zal worden gebruikt om aan uw webhaak in te tekenen, toestaand uw het stromen bron om met Experience Platform te communiceren.

Als u het streamingeindpunt wilt ophalen, gaat u naar de *[!UICONTROL Dataflow activity]* -pagina van de gegevensstroom die u net hebt gemaakt en kopieert u het eindpunt van de onderkant van het deelvenster *[!UICONTROL Properties]* .

![ de dataflow activiteitenpagina in de bronwerkruimte, met het stromen eindpunt URL benadrukte.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-api.png)

## Uw integratieprofiel activeren in RainFocus

Nadat de gegevensstroom is voltooid en u de URL van het streamingeindpunt hebt opgehaald, kunt u de URL [!DNL Integration Profile] in [!DNL RainFocus] nu activeren.

* Logboek in het [[!DNL RainFocus]  platform ](https://app.rainfocus.com). Selecteer **[!DNL Libraries]** en **[!DNL Integration Profiles]** in de primaire navigatie
* Open [!DNL Integration Profile] dat u vroeger als deel van de [ eerste vereisten ](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus) creeerde.
* Plak **identiteitskaart Dataflow** en **Streaming Eindpunt** gekopieerd van Dataflow in Experience Platform en selecteer **sparen**

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht voor uw [!DNL RainFocus] -bron, waarmee u gegevens voor gebeurtenisbeheer en analyses kunt streamen naar het Experience Platform.

## Aanvullende bronnen

De volgende documenten bieden aanvullende informatie over nuances rond de [!DNL RainFocus] -bron.

* [ RainFocus Help Center ](https://help.rainfocus.com/hc/en-us)
* [ creeer een Rekening van de Dienst van Adobe (JWT) in het Portaal van Adobe Developer ](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)
* [Een schema maken in de API](../../../../../xdm/tutorials/create-schema-api.md)
* [Een schema maken in de gebruikersinterface](../../../../../xdm/tutorials/create-schema-ui.md)
* [ bepaalt de Gebieden van de Identiteit in UI ](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html)

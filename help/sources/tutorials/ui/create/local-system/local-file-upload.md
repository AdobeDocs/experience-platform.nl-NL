---
keywords: Experience Platform;home;populaire onderwerpen;lokaal systeem;bestandsupload;map csv;map csv-bestand;map csv-bestand toewijzen aan xdm;map csv aan xdm;ui-gids;
solution: Experience Platform
title: Creeer een Lokaal Dossier uploadt Bronschakelaar in UI
topic-legacy: overview
type: Tutorial
description: Leer hoe u een bronverbinding maakt voor uw lokale systeem om lokale bestanden naar het Platform te brengen
exl-id: 9ce15362-c30d-40cc-9d9c-caa650579390
source-git-commit: 08805ed0d89d3d6908ddccdafda55d2f862e727e
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 0%

---

# Een lokale bronconnector voor het uploaden van bestanden maken in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een lokale bronaansluiting voor het uploaden van bestanden om lokale bestanden via de gebruikersinterface in te voeren in het Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema Editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

## Lokale bestanden uploaden naar Platform

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Sources]** van de linkernavigatiebalk voor toegang tot de [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarvoor u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de [!UICONTROL Local system] categorie, selecteert u **[!UICONTROL Local file upload]** en selecteer vervolgens **[!UICONTROL Add data]**.

![catalogus](../../../../images/tutorials/create/local/catalog.png)

### Een bestaande gegevensset gebruiken

De [!UICONTROL Dataflow detail] De pagina staat u toe om te selecteren of u uw gegevens CSV in een bestaande dataset of een nieuwe dataset wilt opnemen.

Om uw CSV- gegevens in een bestaande dataset in te voeren, selecteer **[!UICONTROL Existing dataset]**. U kunt of een bestaande dataset terugwinnen gebruikend [!UICONTROL Advanced search] of door door de lijst van bestaande datasets in het dropdown menu te scrollen.

Selecteer een gegevensset en geef een naam op voor de gegevensstroom en een optionele beschrijving.

Tijdens dit proces kunt u ook [!UICONTROL Error diagnostics] en [!UICONTROL Partial ingestion]. [!UICONTROL Error diagnostics] laat gedetailleerde foutenmelding generatie voor om het even welke onjuiste verslagen toe die in uw dataflow voorkomen, terwijl [!UICONTROL Partial ingestion] kunt u gegevens met fouten opnemen tot een bepaalde drempel die u handmatig definieert. Zie de [gedeeltelijke batch-opname, overzicht](../../../../../ingestion/batch-ingestion/partial.md) voor meer informatie .

![bestaande gegevensset](../../../../images/tutorials/create/local/existing-dataset.png)

### Een nieuwe gegevensset gebruiken

Om uw CSV- gegevens in een nieuwe dataset in te voeren, selecteer **[!UICONTROL New dataset]** en geef vervolgens een naam voor de uitvoergegevensset en een optionele beschrijving op. Selecteer vervolgens het schema waaraan u wilt toewijzen [!UICONTROL Advanced search] of door door de lijst van bestaande schema&#39;s in het dropdown menu te scrollen.

Selecteer een schema, geef een naam voor de gegevensstroom en een optionele beschrijving op en pas vervolgens het [!UICONTROL Error diagnostics] en [!UICONTROL Partial ingestion] de gewenste instellingen voor de gegevensstroom. Als u klaar bent, selecteert u **[!UICONTROL Next]**.

![new-dataset](../../../../images/tutorials/create/local/new-dataset.png)

### Gegevens selecteren

De [!UICONTROL Select data] wordt weergegeven, zodat u een interface hebt om uw lokale bestanden te uploaden en een voorvertoning van de structuur en inhoud ervan te bekijken. Selecteren **[!UICONTROL Choose files]** om een CSV-bestand vanaf uw lokale systeem te uploaden. U kunt ook het CSV-bestand dat u wilt uploaden, naar de [!UICONTROL Drag and drop files] deelvenster.

>[!TIP]
>
>Momenteel worden alleen CSV-bestanden ondersteund door lokale bestanden te uploaden. De maximale bestandsgrootte voor elk bestand is 1 GB.

![bestanden kiezen](../../../../images/tutorials/create/local/choose-files.png)

Nadat het bestand is geüpload, wordt de voorbeeldinterface bijgewerkt en worden de inhoud en de structuur van het bestand weergegeven.

![preview-sample-data](../../../../images/tutorials/create/local/preview-sample-data.png)

Afhankelijk van het bestand kunt u een kolomscheidingsteken selecteren, zoals tabs, komma&#39;s, pijpen of een aangepast kolomscheidingsteken voor de brongegevens. Selecteer **[!UICONTROL Delimiter]** vervolgkeuzepijl en selecteer vervolgens het juiste scheidingsteken in het menu.

Als u klaar bent, selecteert u **[!UICONTROL Next]**.

![scheidingsteken](../../../../images/tutorials/create/local/delimiter.png)

## Toewijzing

De [!UICONTROL Mapping] de stap verschijnt, die u van een interface voorziet om de brongebieden van uw bronschema aan hun aangewezen doelXDM gebieden in het doelschema in kaart te brengen.

Op basis van uw behoeften kunt u ervoor kiezen om velden rechtstreeks toe te wijzen of gegevens prep-functies te gebruiken om brongegevens om berekende of berekende waarden af te leiden. Voor uitvoerige stappen bij het gebruiken van de kaartinterface, zie [UI-hulplijn voor gegevensvoorinstelling](../../../../../data-prep/ui/mapping.md).

Als uw toewijzingssets gereed zijn, selecteert u **[!UICONTROL Finish]** en kan de nieuwe gegevensstroom even worden gemaakt.

![toewijzing](../../../../images/tutorials/create/local/mapping.png)

## Gegevens bijhouden

Nadat het CSV-bestand is toegewezen en gemaakt, kunt u de gegevens die ermee worden ingevoerd, controleren met het dashboard voor bewaking. Raadpleeg de zelfstudie voor meer informatie [gegevens van bronnen controleren in de UI](../../../../../dataflows/ui/monitor-sources.md).

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een standaard CSV-bestand toegewezen aan een XDM-schema en het in Platform opgenomen. Deze gegevens kunnen nu door downstreamgebruikers worden gebruikt [!DNL Platform] diensten zoals [!DNL Real-time Customer Profile]. Zie het overzicht voor [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) voor meer informatie .

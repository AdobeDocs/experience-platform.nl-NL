---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;
solution: Experience Platform
title: Een CSV-bestand toewijzen aan een XDM-schema
topic: tutorial
type: Tutorial
description: In deze zelfstudie wordt uitgelegd hoe u een CSV-bestand via de Adobe Experience Platform-gebruikersinterface toewijst aan een XDM-schema.
translation-type: tm+mt
source-git-commit: c19360450d7b1f11063683b796774a04f3dbe16c
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 1%

---


# Een CSV-bestand toewijzen aan een XDM-schema

Om CSV-gegevens in te voeren [!DNL Adobe Experience Platform], moeten de gegevens worden toegewezen aan een [!DNL Experience Data Model] (XDM)-schema. In deze zelfstudie wordt uitgelegd hoe u een CSV-bestand via de [!DNL Platform] gebruikersinterface kunt toewijzen aan een XDM-schema.

Daarnaast bevat het aanhangsel bij deze zelfstudie nadere informatie over het gebruik van [toewijzingsfuncties](#mapping-functions).

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van [!DNL Platform]:

- [[!DNL Experience Data Model (XDM System)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Platform] georganiseerd.
- [[!DNL Batch ingestion]](../batch-ingestion/overview.md): De methode waarmee gegevens uit door de gebruiker opgegeven gegevensbestanden worden [!DNL Platform] ingesloten.

Deze zelfstudie vereist ook dat u al een dataset hebt gemaakt om uw CSV-gegevens in te voeren. Voor stappen bij het creëren van een dataset in UI, zie de [gegevens ingest leerprogramma](./ingest-batch-data.md).

## Kies een bestemming

Meld u aan bij [[!DNL Adobe Experience Platform]](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Workflows]** in de linkernavigatiebalk voor toegang tot de **[!UICONTROL werkruimte Workflows]** .

Selecteer in het scherm **[!UICONTROL Workflows]** de optie CSV **[!UICONTROL toewijzen aan XDM-schema]** onder de sectie **[!UICONTROL Gegevensinvoer]** en selecteer vervolgens **[!UICONTROL Starten]**.

![](../images/tutorials/map-a-csv-file/workflows.png)

De werkstroom CSV **[!UICONTROL toewijzen aan XDM-schema]** wordt weergegeven, te beginnen bij de stap **[!UICONTROL Doel]** . Kies een dataset voor binnenkomende gegevens waarin moeten worden opgenomen. U kunt of een bestaande dataset gebruiken of nieuwe creëren.

**Een bestaande gegevensset gebruiken**

Om uw CSV- gegevens in een bestaande dataset in te voeren, selecteer **[!UICONTROL Gebruik bestaande dataset]**. U kunt of een bestaande dataset terugwinnen gebruikend de onderzoeksfunctie of door door de lijst van bestaande datasets in het paneel te scrollen.

![](../images/tutorials/map-a-csv-file/use-existing-dataset.png)

Als u uw CSV-gegevens wilt opnemen in een nieuwe gegevensset, selecteert u **[!UICONTROL Nieuwe gegevensset]** maken en voert u een naam en een beschrijving in voor de gegevensset in de velden die u opgeeft. Selecteer een schema door of de onderzoeksfunctie te gebruiken of door door de lijst van schema&#39;s te scrollen verstrekt. Selecteer **[!UICONTROL Volgende]** om door te gaan.

![](../images/tutorials/map-a-csv-file/create-new-dataset.png)

## Gegevens toevoegen

De stap Gegevens **** toevoegen wordt weergegeven. Sleep het CSV-bestand naar de beschikbare ruimte en zet het neer of selecteer Bestanden **** kiezen om het CSV-bestand handmatig in te voeren.

![](../images/tutorials/map-a-csv-file/add-data.png)

De sectie **[!UICONTROL Voorbeeldgegevens]** wordt weergegeven wanneer het bestand is geüpload. De eerste tien rijen met gegevens worden weergegeven. Nadat u hebt bevestigd dat de gegevens naar behoren zijn geüpload, selecteert u **[!UICONTROL Volgende]**.

![](../images/tutorials/map-a-csv-file/sample-data.png)

## CSV-velden toewijzen aan XDM-schemavelden

De stap **[!UICONTROL Toewijzing]** wordt weergegeven. De kolommen van het CSV-bestand worden weergegeven onder **[!UICONTROL Bronveld]**, met de bijbehorende XDM-schemavelden onder **[!UICONTROL Doelveld]**.

[!DNL Platform] verstrekt automatisch intelligente aanbevelingen voor auto-in kaart gebrachte gebieden die op het doelschema of de dataset worden gebaseerd dat u selecteerde. U kunt toewijzingsregels handmatig aanpassen aan uw gebruiksgevallen.

![](../images/tutorials/map-a-csv-file/mapping-with-suggestions.png)

Als u alle automatisch gegenereerde toewijzingswaarden wilt accepteren, schakelt u het selectievakje &quot;[!UICONTROL Alle doelvelden]accepteren&quot; in.

![](../images/tutorials/map-a-csv-file/filled-mapping-with-suggestions.png)

Soms is er meer dan één aanbeveling beschikbaar voor het bronschema. Als dit gebeurt, wordt op de kaart de meest prominente aanbeveling weergegeven, gevolgd door een blauwe cirkel die het aantal aanvullende aanbevelingen bevat dat beschikbaar is. Als u het gloeilamppictogram selecteert, wordt een lijst met aanvullende aanbevelingen weergegeven. U kunt één van de afwisselende aanbevelingen kiezen door checkbox naast de aanbeveling te selecteren u aan in plaats daarvan wilt in kaart brengen.

![](../images/tutorials/map-a-csv-file/multiple-recommendations.png)

Alternatief, kunt u verkiezen om uw bronschema aan uw doelschema manueel in kaart te brengen. Houd de muisaanwijzer boven het bronschema dat u wilt toewijzen en selecteer vervolgens het plusteken.

![](../images/tutorials/map-a-csv-file/mapping-with-suggestions-and-buttons.png)

De pop-up Bron **[!UICONTROL toewijzen aan doelveld]** wordt weergegeven. Van hieruit kunt u selecteren welk veld u wilt toewijzen, gevolgd door **[!UICONTROL Opslaan]** om de nieuwe toewijzing toe te voegen.

![](../images/tutorials/map-a-csv-file/manual-mapping.png)

Als u een van de toewijzingen wilt verwijderen, plaatst u de muisaanwijzer boven de toewijzing en selecteert u het minteken.

### Berekend veld toevoegen

Met berekende velden kunnen waarden worden gemaakt op basis van de kenmerken in het invoerschema. Deze waarden kunnen vervolgens aan kenmerken in het doelschema worden toegewezen en een naam en beschrijving worden gegeven om de referentie eenvoudiger te maken.

Selecteer de knop Berekend veld **** toevoegen om door te gaan.

![](../images/tutorials/map-a-csv-file/add-calculated-field.png)

Het **[!UICONTROL deelvenster Berekend veld]** maken wordt weergegeven. Het linkerdialoogvenster bevat de velden, functies en operatoren die in berekende velden worden ondersteund. Selecteer een van de tabbladen om functies, velden of operatoren toe te voegen aan de expressie-editor.

![](../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| Tab | Beschrijving |
| --------- | ----------- |
| Velden | Het tabblad Veld bevat velden en kenmerken die beschikbaar zijn in het bronschema. |
| Functies | Op het tabblad Functies staan de functies die beschikbaar zijn voor het transformeren van de gegevens. Voor meer informatie over de functies die u kunt gebruiken binnen berekende velden, leest u de handleiding over het [gebruik van de functies](../../data-prep/functions.md)Data Prep (Mapper). |
| Operatoren | Het tabblad Operatoren bevat een lijst met operatoren die beschikbaar zijn om de gegevens te transformeren. |

U kunt handmatig velden, functies en operatoren toevoegen met de expressieeditor in het midden. Selecteer de editor om een expressie te maken.

![](../images/tutorials/map-a-csv-file/create-calculated-field.png)

Selecteer **[!UICONTROL Opslaan]** om door te gaan.

Het kaartscherm verschijnt weer met het nieuwe bronveld. Pas het desbetreffende doelveld toe en selecteer **[!UICONTROL Voltooien]** om de toewijzing te voltooien.

![](../images/tutorials/map-a-csv-file/new-calculated-field.png)

## Gegevens bijhouden

Nadat het CSV-bestand is toegewezen en gemaakt, kunt u de gegevens controleren die er doorheen worden ingevoerd. Zie de zelfstudie over het [controleren van gegevensinvoer](../../ingestion/quality/monitor-data-ingestion.md)voor meer informatie over het controleren van gegevensinvoer.

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een vlak CSV-bestand toegewezen aan een XDM-schema en het ingepakt in [!DNL Platform]. Deze gegevens kunnen nu worden gebruikt door downstreamdiensten [!DNL Platform] zoals [!DNL Real-time Customer Profile]. Zie het overzicht voor [[!DNL Real-time Customer Profile]](../../profile/home.md) meer informatie.

---
keywords: Experience Platform;home;populaire onderwerpen;map csv;map csv-bestand;map csv-bestand toewijzen aan xdm;map csv aan xdm;ui-gids;
solution: Experience Platform
title: Een CSV-bestand toewijzen aan een bestaand XDM-schema
topic-legacy: tutorial
type: Tutorial
description: In deze zelfstudie wordt uitgelegd hoe u een CSV-bestand via de Adobe Experience Platform-gebruikersinterface toewijst aan een bestaand XDM-schema.
exl-id: 15f55562-269d-421d-ad3a-5c10fb8f109c
source-git-commit: 160a75a1811afa002717e167887550715eee5471
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 1%

---

# Een CSV-bestand toewijzen aan een bestaand XDM-schema

>[!NOTE]
>
>In dit document wordt beschreven hoe u een CSV-bestand toewijst aan een bestaand XDM-schema. Voor informatie over hoe te om het AI-Gegenereerde hulpmiddel van de schemaaanbeveling (momenteel in bèta) te gebruiken, zie het document op [toewijzen van een CSV-bestand aan de hand van aanbevelingen voor machinaal leren](./recommendations.md).

Om CSV-gegevens in te nemen [!DNL Adobe Experience Platform], moeten de gegevens worden toegewezen aan een [!DNL Experience Data Model] (XDM) schema. In deze zelfstudie wordt uitgelegd hoe u een CSV-bestand met het [!DNL Platform] gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van [!DNL Platform]:

- [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Platform] organiseert de gegevens van de klantenervaring.
- [Inname in batch](../../batch-ingestion/overview.md): De methode waarbij [!DNL Platform] Hiermee worden gegevens uit door de gebruiker opgegeven gegevensbestanden opgenomen.
- [Adobe Experience Platform Data Prep](../../batch-ingestion/overview.md): Een reeks mogelijkheden die u toestaan om opgenomen gegevens in kaart te brengen en om te zetten om aan schema&#39;s in overeenstemming te zijn XDM. De documentatie over [Functies Data Prep](../../../data-prep/functions.md) is met name van belang voor schema-toewijzing.

Deze zelfstudie vereist ook dat u al een dataset hebt gemaakt om uw CSV-gegevens in te voeren. Voor stappen bij het creëren van een dataset in UI, zie [zelfstudie over gegevensinvoer](../ingest-batch-data.md).

## Kies een bestemming

Aanmelden bij [[!DNL Adobe Experience Platform]](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Workflows]** van de linkernavigatiebalk voor toegang tot de **[!UICONTROL Workflows]** werkruimte.

Van de **[!UICONTROL Workflows]** scherm, selecteren **[!UICONTROL Map CSV to XDM schema]** onder de **[!UICONTROL Data ingestion]** en selecteer vervolgens **[!UICONTROL Launch]**.

![](../../images/tutorials/map-a-csv-file/workflows.png)

De **[!UICONTROL Map CSV to XDM schema]** wordt weergegeven, vanaf de **[!UICONTROL Destination]** stap. Kies een dataset voor binnenkomende gegevens waarin moeten worden opgenomen. U kunt of een bestaande dataset gebruiken of nieuwe creëren.

**Een bestaande gegevensset gebruiken**

Om uw CSV- gegevens in een bestaande dataset in te voeren, selecteer **[!UICONTROL Use existing dataset]**. U kunt of een bestaande dataset terugwinnen gebruikend de onderzoeksfunctie of door door de lijst van bestaande datasets in het paneel te scrollen.

![](../../images/tutorials/map-a-csv-file/use-existing-dataset.png)

Om uw CSV- gegevens in een nieuwe dataset in te voeren, selecteer **[!UICONTROL Create new dataset]** en voert een naam en een beschrijving voor de gegevensset in de opgegeven velden in. Selecteer een schema door of de onderzoeksfunctie te gebruiken of door door de lijst van schema&#39;s te scrollen verstrekt. Selecteren **[!UICONTROL Next]** om verder te gaan.

![](../../images/tutorials/map-a-csv-file/create-new-dataset.png)

## Gegevens toevoegen

De **[!UICONTROL Add data]** wordt weergegeven. Sleep het CSV-bestand naar de beschikbare ruimte of selecteer **[!UICONTROL Choose files]** om uw CSV-bestand handmatig in te voeren.

![](../../images/tutorials/map-a-csv-file/add-data.png)

De **[!UICONTROL Sample data]** wordt weergegeven zodra het bestand is geüpload, met daarin de eerste tien rijen met gegevens. Nadat u hebt bevestigd dat de gegevens naar behoren zijn geüpload, selecteert u **[!UICONTROL Next]**.

![](../../images/tutorials/map-a-csv-file/sample-data.png)

## CSV-velden toewijzen aan XDM-schemavelden

De **[!UICONTROL Mapping]** wordt weergegeven. De kolommen van het CSV-bestand staan onder **[!UICONTROL Source Field]**, met de bijbehorende XDM-schemavelden vermeld onder **[!UICONTROL Target Field]**.

[!DNL Platform] verstrekt automatisch intelligente aanbevelingen voor auto-in kaart gebrachte gebieden die op het doelschema of de dataset worden gebaseerd dat u selecteerde. U kunt toewijzingsregels handmatig aanpassen aan uw gebruiksgevallen.

![](../../images/tutorials/map-a-csv-file/mapping-with-suggestions.png)

Als u alle automatisch gegenereerde toewijzingswaarden wilt accepteren, schakelt u het selectievakje &quot;[!UICONTROL Accept all target fields]&quot;.

![](../../images/tutorials/map-a-csv-file/filled-mapping-with-suggestions.png)

Soms is er meer dan één aanbeveling beschikbaar voor het bronschema. Als dit gebeurt, wordt op de kaart de meest prominente aanbeveling weergegeven, gevolgd door een blauwe cirkel die het aantal aanvullende aanbevelingen bevat dat beschikbaar is. Als u het gloeilamppictogram selecteert, wordt een lijst met aanvullende aanbevelingen weergegeven. U kunt één van de afwisselende aanbevelingen kiezen door checkbox naast de aanbeveling te selecteren u aan in plaats daarvan wilt in kaart brengen.

![](../../images/tutorials/map-a-csv-file/multiple-recommendations.png)

Alternatief, kunt u verkiezen om uw bronschema aan uw doelschema manueel in kaart te brengen. Houd de muisaanwijzer boven het bronschema dat u wilt toewijzen en selecteer vervolgens het plusteken.

![](../../images/tutorials/map-a-csv-file/mapping-with-suggestions-and-buttons.png)

De **[!UICONTROL Map source to target field]** wordt weergegeven. Hier kunt u selecteren welk veld u wilt toewijzen, gevolgd door **[!UICONTROL Save]** om uw nieuwe toewijzing toe te voegen.

![](../../images/tutorials/map-a-csv-file/manual-mapping.png)

Als u een van de toewijzingen wilt verwijderen, plaatst u de muis boven de toewijzing en selecteert u het min-pictogram.

### Berekend veld toevoegen {#add-calculated-field}

Met berekende velden kunnen waarden worden gemaakt op basis van de kenmerken in het invoerschema. Deze waarden kunnen vervolgens aan kenmerken in het doelschema worden toegewezen en een naam en beschrijving worden gegeven om de referentie eenvoudiger te maken.

Selecteer **[!UICONTROL Add calculated field]** om verder te gaan.

![](../../images/tutorials/map-a-csv-file/add-calculated-field.png)

De **[!UICONTROL Create calculated field]** wordt weergegeven. Het linkerdialoogvenster bevat de velden, functies en operatoren die in berekende velden worden ondersteund. Selecteer een van de tabbladen om functies, velden of operatoren toe te voegen aan de expressie-editor.

![](../../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| Tabtoets | Beschrijving |
| --------- | ----------- |
| Velden | Het tabblad Veld bevat velden en kenmerken die beschikbaar zijn in het bronschema. |
| Functies | Op het tabblad Functies staan de functies die beschikbaar zijn voor het transformeren van de gegevens. Lees de handleiding voor meer informatie over de functies die u binnen berekende velden kunt gebruiken [functies Data Prep (Mapper) gebruiken](../../../data-prep/functions.md). |
| Operatoren | Het tabblad Operatoren bevat een lijst met operatoren die beschikbaar zijn om de gegevens te transformeren. |

U kunt handmatig velden, functies en operatoren toevoegen met de expressieeditor in het midden. Selecteer de editor om een expressie te maken.

![](../../images/tutorials/map-a-csv-file/create-calculated-field.png)

Selecteren **[!UICONTROL Save]** om verder te gaan.

Het kaartscherm verschijnt weer met het nieuwe bronveld. Pas het desbetreffende doelveld toe en selecteer **[!UICONTROL Finish]** om de toewijzing te voltooien.

![](../../images/tutorials/map-a-csv-file/new-calculated-field.png)

## Gegevens bijhouden

Nadat het CSV-bestand is toegewezen en gemaakt, kunt u de gegevens controleren die er doorheen worden ingevoerd. Raadpleeg de zelfstudie voor meer informatie over het controleren van gegevensinvoer. [controle gegevensinvoer](../../../ingestion/quality/monitor-data-ingestion.md).

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een standaard CSV-bestand toegewezen aan een XDM-schema en het ingepakt in [!DNL Platform]. Deze gegevens kunnen nu door downstreamgebruikers worden gebruikt [!DNL Platform] diensten zoals [!DNL Real-time Customer Profile]. Zie het overzicht voor [[!DNL Real-time Customer Profile]](../../../profile/home.md) voor meer informatie .

---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;
solution: Experience Platform
title: Een CSV-bestand toewijzen aan een XDM-schema
topic: tutorial
type: Tutorial
description: In deze zelfstudie wordt uitgelegd hoe u een CSV-bestand via de Adobe Experience Platform-gebruikersinterface toewijst aan een XDM-schema.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---


# Een CSV-bestand toewijzen aan een XDM-schema

Om CSV-gegevens in te voeren [!DNL Adobe Experience Platform], moeten de gegevens worden toegewezen aan een [!DNL Experience Data Model] (XDM)-schema. In deze zelfstudie wordt uitgelegd hoe u een CSV-bestand via de [!DNL Platform] gebruikersinterface kunt toewijzen aan een XDM-schema.

Daarnaast bevat het aanhangsel bij deze zelfstudie nadere informatie over het gebruik van [toewijzingsfuncties](#mapping-functions).

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van [!DNL Platform]:

- [[!DNL-ervaringsgegevensmodel (XDM-systeem)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Platform] georganiseerd.
- [[!DNL Batch-inname]](../batch-ingestion/overview.md): De methode waarmee gegevens uit door de gebruiker opgegeven gegevensbestanden worden [!DNL Platform] ingesloten.

Deze zelfstudie vereist ook dat u al een dataset hebt gemaakt om uw CSV-gegevens in te voeren. Voor stappen bij het creëren van een dataset in UI, zie de [gegevens ingest leerprogramma](./ingest-batch-data.md).

## Kies een bestemming

Meld u aan bij [[!DNL Adobe Experience Platform]](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Workflows]** in de linkernavigatiebalk voor toegang tot de werkruimte **[!UICONTROL Workflows]** .

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

De stap **[!UICONTROL Toewijzing]** wordt weergegeven. De kolommen van het CSV-bestand worden weergegeven onder **[!UICONTROL Bronveld]**, met de bijbehorende XDM-schemavelden onder **[!UICONTROL Doelveld]**. Niet-geselecteerde doelvelden krijgen een rode omtrek. Met de optie Filtervelden kunt u de lijst met beschikbare bronvelden verkleinen.

>[!TIP]
>
>[!DNL Platform] verstrekt intelligente aanbevelingen voor auto-in kaart gebrachte gebieden die op het doelschema of de dataset worden gebaseerd dat u selecteerde. U kunt toewijzingsregels handmatig aanpassen aan uw gebruiksgevallen.

Als u een CSV-kolom wilt toewijzen aan een XDM-veld, selecteert u het schemapictogram naast het bijbehorende doelveld van de kolom.

![](../images/tutorials/map-a-csv-file/mapping.png)

Het venster **[!UICONTROL Selectieschemaveld]** wordt weergegeven. Hier kunt u de structuur van het XDM-schema navigeren en van het gebied de plaats bepalen u wenst om de kolom in kaart te brengen CSV aan. Klik op een XDM-veld om dit te selecteren en klik vervolgens op **[!UICONTROL Selecteren]**.

![](../images/tutorials/map-a-csv-file/select-schema-field.png)

Nadat u de stappen voor de resterende niet-toegewezen bronvelden hebt uitgevoerd, wordt het scherm **[!UICONTROL Toewijzing]** opnieuw weergegeven met het geselecteerde XDM-veld dat nu onder **[!UICONTROL Doelveld]** wordt weergegeven.

![](../images/tutorials/map-a-csv-file/field-mapped.png)

Bij het toewijzen van velden kunt u ook functies opnemen om waarden te berekenen op basis van invoerbronvelden. Zie de sectie [toewijzingsfuncties](#mapping-functions) in de bijlage voor meer informatie.

### Berekend veld toevoegen

Met berekende velden kunnen waarden worden gemaakt op basis van de kenmerken in het invoerschema. Deze waarden kunnen vervolgens aan kenmerken in het doelschema worden toegewezen en een naam en beschrijving worden gegeven om de referentie eenvoudiger te maken.

Selecteer de knop Berekend veld **** toevoegen om door te gaan.

![](../images/tutorials/map-a-csv-file/add-calculate-field.png)

Het **[!UICONTROL deelvenster Berekend veld]** maken wordt weergegeven. Het linkerdialoogvenster bevat de velden, functies en operatoren die in berekende velden worden ondersteund. Selecteer een van de tabbladen om functies, velden of operatoren toe te voegen aan de expressie-editor.

![](../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| Tab | Beschrijving |
| --------- | ----------- |
| Velden | Het tabblad Veld bevat velden en kenmerken die beschikbaar zijn in het bronschema. |
| Functies | Op het tabblad Functies staan de functies die beschikbaar zijn voor het transformeren van de gegevens. |
| Operatoren | Het tabblad Operatoren bevat een lijst met operatoren die beschikbaar zijn om de gegevens te transformeren. |

U kunt handmatig velden, functies en operatoren toevoegen met de expressieeditor in het midden. Selecteer de editor om een expressie te maken.

![](../images/tutorials/map-a-csv-file/expression-editor.png)

Selecteer **[!UICONTROL Opslaan]** om door te gaan.

Het kaartscherm verschijnt weer met het nieuwe bronveld. Pas het desbetreffende doelveld toe en selecteer **[!UICONTROL Voltooien]** om de toewijzing te voltooien.

![](../images/tutorials/map-a-csv-file/new-field.png)

## Uw gegevensstroom controleren

Nadat het CSV-bestand is toegewezen en gemaakt, kunt u de gegevens controleren die er doorheen worden ingevoerd. Raadpleeg de zelfstudie over het [controleren van streaming dataflows voor meer informatie over het controleren van gegevensstromen](../../ingestion/quality/monitor-data-flows.md).

## Toewijzingsfuncties gebruiken

Als u een functie wilt gebruiken, typt u deze onder **[!UICONTROL Bronveld]** met de juiste syntaxis en invoer.

Als u bijvoorbeeld CSV-velden voor stad en land wilt samenvoegen en deze aan het XDM-veld voor stad wilt toewijzen, stelt u het bronveld in als `concat(city, ", ", county)`.

![](../images/tutorials/map-a-csv-file/mapping-function.png)

Meer over het in kaart brengen van kolommen aan gebieden XDM, lees de gids bij het [gebruiken van de functies](../../data-prep/functions.md)van de Prep van Gegevens (Mapper).

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een vlak CSV-bestand toegewezen aan een XDM-schema en het ingepakt in [!DNL Platform]. Deze gegevens kunnen nu worden gebruikt door downstreamdiensten [!DNL Platform] zoals [!DNL Real-time Customer Profile]. Zie het overzicht voor [[!DNL Real-time klantprofiel]](../../profile/home.md) voor meer informatie.

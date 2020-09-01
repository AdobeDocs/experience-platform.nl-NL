---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een CSV-bestand toewijzen aan een XDM-schema
topic: tutorial
translation-type: tm+mt
source-git-commit: c6c5ada52321b11543254f80399c38365f0fb9d7
workflow-type: tm+mt
source-wordcount: '1371'
ht-degree: 1%

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

Als u een CSV-kolom wilt toewijzen aan een XDM-veld, selecteert u het schemapictogram naast het bijbehorende doelveld van de kolom.

![](../images/tutorials/map-a-csv-file/mapping.png)

Het venster **[!UICONTROL Selectieschemaveld]** wordt weergegeven. Hier kunt u de structuur van het XDM-schema navigeren en van het gebied de plaats bepalen u wenst om de kolom in kaart te brengen CSV aan. Klik op een XDM-veld om dit te selecteren en klik vervolgens op **[!UICONTROL Selecteren]**.

![](../images/tutorials/map-a-csv-file/select-schema-field.png)

Het scherm **[!UICONTROL Toewijzing]** wordt opnieuw weergegeven, waarbij het geselecteerde XDM-veld nu wordt weergegeven onder **[!UICONTROL Doelveld]**.

![](../images/tutorials/map-a-csv-file/field-mapped.png)

Als u geen bepaalde CSV-kolom wilt toewijzen, kunt u de toewijzing verwijderen door op het pictogram **** Verwijderen naast het doelveld te klikken. U kunt ook alle toewijzingen verwijderen door de knop **[!UICONTROL Alle toewijzingen]** wissen te selecteren.

![](../images/tutorials/map-a-csv-file/remove-mapping.png)

Als u een nieuwe afbeelding wilt toevoegen, selecteert u Nieuwe toewijzing **** toevoegen boven aan de lijst **[!UICONTROL Bronveld]** .

![](../images/tutorials/map-a-csv-file/add-mapping.png)

Bij het toewijzen van velden kunt u ook functies opnemen om waarden te berekenen op basis van invoerbronvelden. Zie de sectie [toewijzingsfuncties](#mapping-functions) in de bijlage voor meer informatie.

### Berekend veld toevoegen

Met berekende velden kunnen waarden worden gemaakt op basis van de kenmerken in het invoerschema. Deze waarden kunnen vervolgens aan kenmerken in het doelschema worden toegewezen en een naam en beschrijving worden gegeven om de referentie eenvoudiger te maken.

Selecteer de knop Berekend veld **** toevoegen om door te gaan.

![](../images/tutorials/map-a-csv-file/add-calculated-field.png)

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

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een vlak CSV-bestand toegewezen aan een XDM-schema en het ingepakt in [!DNL Platform]. Deze gegevens kunnen nu worden gebruikt door downstreamdiensten [!DNL Platform] zoals [!DNL Real-time Customer Profile]. Zie het overzicht voor [[!DNL Real-time klantprofiel]](../../profile/home.md) voor meer informatie.

## Aanhangsel

De volgende sectie verstrekt extra informatie voor het in kaart brengen CSV kolommen aan XDM gebieden.

### Toewijzingsfuncties

Bepaalde toewijzingsfuncties kunnen worden gebruikt om waarden te berekenen en te berekenen op basis van wat is ingevoerd in bronvelden. Als u een functie wilt gebruiken, typt u deze onder **[!UICONTROL Bronveld]** met de juiste syntaxis en invoer.

Als u bijvoorbeeld CSV-velden voor **steden** en **landen** wilt samenvoegen en deze aan het XDM-veld **Plaats** wilt toewijzen, stelt u het bronveld in als `concat(city, ", ", county)`.

![](../images/tutorials/map-a-csv-file/mapping-function.png)

De volgende tabel bevat een lijst met alle ondersteunde toewijzingsfuncties, inclusief voorbeeldexpressies en de resulterende uitvoer.

| -functie | Beschrijving | Voorbeeldexpressie | Voorbeelduitvoer |
| -------- | ----------- | ----------------- | ------------- |
| concat | Voegt bepaalde tekenreeksen samen. | concat(&quot;Hi, &quot;, &quot;there&quot;, &quot;!&quot;) | `"Hi, there!"` |
| ontploffen | Splitst de tekenreeks op basis van een regex en retourneert een array met onderdelen. | explode(&quot;Hallo, daar!&quot;, &quot; &quot;) | `["Hi,", "there"]` |
| instr | Retourneert de locatie/index van een subtekenreeks. | instr(&quot;adobe<span>.com&quot;, &quot;com&quot;) | 6 |
| vervanger | Vervangt de zoektekenreeks indien aanwezig in de oorspronkelijke tekenreeks. | replacestr(&quot;This is a string re test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;Dit is een test ter vervanging van een tekenreeks |
| substr | Retourneert een subtekenreeks van een bepaalde lengte. | substr(&quot;This is a substring test&quot;, 7, 8) | &quot; a subst&quot; |
| lower /<br>lcase | Zet een tekenreeks om in kleine letters. | lower(&quot;HeLLo&quot;)<br>lcase(&quot;HeLLo&quot;) | &quot;hallo&quot; |
| upper/<br>ucase | Zet een tekenreeks om in hoofdletters. | upper(&quot;HeLLo&quot;)<br>ucase(&quot;HeLLo&quot;) | &quot;HELLO&quot; |
| splitsen | Splitst een invoertekenreeks op een scheidingsteken. | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| join | Hiermee wordt een lijst met objecten samengevoegd met het scheidingsteken. | `join(" ", ["Hello", "world"]`) | &quot;Hello world&quot; |
| samenvoegen | Retourneert het eerste object in een bepaalde lijst dat niet null is. | coalesce(null, null, null, &quot;first&quot;, null, &quot;second&quot;) | &quot;first&quot; |
| decoderen | Op basis van een sleutel en een lijst met sleutelwaardeparen die als een array zijn samengevoegd, retourneert de functie de waarde als een sleutel wordt gevonden of retourneert deze een standaardwaarde als deze aanwezig is in de array. | decode(&quot;k2&quot;, &quot;k1&quot;, &quot;v1&quot;, &quot;k2&quot;, &quot;v2&quot;, &quot;default&quot;) | &quot;v2&quot; |
| iif | Evalueert een bepaalde booleaanse expressie en retourneert de opgegeven waarde op basis van het resultaat. | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;Waar&quot; |
| min | Geeft als resultaat het minimum van de opgegeven argumenten. Gebruikt natuurlijke volgorde. | min(3, 1, 4) | 1 |
| max | Geeft als resultaat het maximum van de opgegeven argumenten. Gebruikt natuurlijke volgorde. | max(3, 1, 4) | 4 |
| first | Haalt het eerste opgegeven argument op. | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| last | Haalt het laatst opgegeven argument op. | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| uuid /<br>guid | Hiermee genereert u een pseudo-willekeurige id. | uuid()<br>guid() | {UNIQUE_ID} |
| now | Hiermee wordt de huidige tijd opgehaald. | now() | `2019-10-23T10:10:24.556-07:00[America/Los_Angeles]` |
| timestamp | Hiermee wordt de huidige Unix-tijd opgehaald. | timestamp() | 1571850624571 |
| format | Hiermee wordt de invoerdatum opgemaakt volgens een opgegeven notatie. | format({DATE}, &quot;yyyy-MM-dd HH:mm:ss&quot;) | &quot;2019-10-23 11:24:35&quot; |
| dformat | Converteert een tijdstempel naar een datumtekenreeks volgens een opgegeven notatie. | dformat(1571829875, &quot;dd-MMM-yyyy hh:mm&quot;) | &quot;23-okt-2019 11:24&quot; |
| date | Converteert een datumtekenreeks naar een ZonedDateTime-object (ISO 8601-indeling). | date(&quot;23-okt-2019 11:24&quot;) | &quot;2019-10-23T11:24:00+00:00&quot; |
| date_part | Hiermee worden de delen van de datum opgehaald. De volgende componentwaarden worden ondersteund: <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;quarters&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;month&quot;<br>&quot;m&quot;m&quot;<br>&quot;m&quot;m&quot;of&quot;dy&quot;y&quot;dag&quot;y&quot;dag&quot;<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>&quot;dag&quot;dd&quot;d&quot;d&quot;d&quot;week&quot;week&quot;week&quot;ww&quot;&quot;w&quot;week&quot;dag&quot;dag&quot;&quot;uur&quot;uur&quot;&quot;h&quot;&quot;hh24&quot;&quot;hh12&quot;&quot;minute&quot;&quot;mi&quot;&quot;tweede&quot;&quot;ss&quot;&quot;&quot;s&quot;&quot;millisecond&quot;&quot;ms&quot; | date_part(date(&quot;2019-10-17 11:55:12&quot;), &quot;MM&quot;) | 10 |
| set_date_part | Hiermee vervangt u een component in een bepaalde datum. De volgende onderdelen worden geaccepteerd: <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;hh&quot;&quot;minute&quot;&quot;mi&quot;&quot;n&quot;tweede&quot;&quot;ss&quot;ss&quot;&quot;s&quot;<br><br><br><br><br><br><br><br><br>&quot;s&quot; | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44.797&quot; |
| make_date_time /<br>make_timestamp | Hiermee maakt u een datum op basis van onderdelen. | make_date_time(2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12.0&#x200B;00000999-07:00[America/Los_Angeles]` |
| current_timestamp | Retourneert de huidige tijdstempel. | current_timestamp() | 1571850624571 |
| current_date | Retourneert de huidige datum zonder een tijdcomponent. | current_date() | &quot;18-nov-2019&quot; |
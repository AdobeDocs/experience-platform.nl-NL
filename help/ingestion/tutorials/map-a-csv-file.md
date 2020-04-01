---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een CSV-bestand toewijzen aan een XDM-schema
topic: tutorial
translation-type: tm+mt
source-git-commit: 33282b1c8ab1129344bd4d7054e86fed75e7b899

---


# Een CSV-bestand toewijzen aan een XDM-schema

Als u CSV-gegevens wilt opnemen in het Adobe Experience Platform, moeten de gegevens worden toegewezen aan een XDM-schema (Experience Data Model). In deze zelfstudie wordt uitgelegd hoe u een CSV-bestand met behulp van de gebruikersinterface van het Experience Platform toewijst aan een XDM-schema.

Daarnaast bevat het aanhangsel bij deze zelfstudie nadere informatie over het gebruik van [toewijzingsfuncties](#mapping-functions).

## Aan de slag

Voor deze zelfstudie is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

- [Experience Data Model (XDM-systeem)](../../xdm/home.md): Het gestandaardiseerde kader waardoor het Platform van de Ervaring gegevens van de klantenervaring organiseert.
- [Inname](../batch-ingestion/overview.md)in batch: De methode waarmee Platform gegevens uit door de gebruiker opgegeven gegevensbestanden opneemt.

Deze zelfstudie vereist ook dat u al een dataset hebt gemaakt om uw CSV-gegevens in te voeren. Voor stappen bij het creëren van een dataset in UI, zie de [gegevens ingest leerprogramma](./ingest-batch-data.md).

## Gegevens toevoegen

Klik in de gebruikersinterface van het ervaringsplatform op **Workflows** in de linkernavigatie en klik vervolgens op CSV **toewijzen aan XDM-schema**. Klik in het rechterspoor dat wordt weergegeven op **Starten**.

![](../images/tutorials/map-a-csv-file/workflow-tab.png)

De werkstroom CSV _toewijzen aan XDM-schema_ wordt weergegeven, te beginnen bij de stap Gegevens __ toevoegen.

![](../images/tutorials/map-a-csv-file/add-data.png)

Sleep het CSV-bestand naar de beschikbare ruimte en zet het neer, of klik op **Bladeren** om een bestand rechtstreeks te selecteren. Nadat het bestand is geüpload, wordt een _sectie met voorbeeldgegevens_ weergegeven met daarin de eerste tien rijen met gegevens. Als u hebt bevestigd dat de gegevens naar behoren zijn geüpload, klikt u op **Volgende**.

![](../images/tutorials/map-a-csv-file/csv-added.png)

## Kies een bestemming

De stap _Doel_ wordt weergegeven. Van de verstrekte lijst, selecteer de dataset dat de gegevens CSV in zullen worden opgenomen, dan klik **daarna**.

![](../images/tutorials/map-a-csv-file/select-destination.png)

## CSV-velden toewijzen aan XDM-schemavelden

De stap _Toewijzing_ wordt weergegeven. De kolommen van het CSV-bestand worden weergegeven onder _Bronveld_, met de bijbehorende XDM-schemavelden onder _Doelveld_. Niet-geselecteerde doelvelden krijgen een rode omtrek.

Als u een CSV-kolom wilt toewijzen aan een XDM-veld, klikt u op het schemapictogram naast het bijbehorende doelveld van de kolom.

![](../images/tutorials/map-a-csv-file/target-field-mapping.png)

Het venster _Selectieschemaveld_ wordt weergegeven. Hier kunt u de structuur van het XDM-schema navigeren en van het gebied de plaats bepalen u wenst om de kolom in kaart te brengen CSV aan. Klik op een XDM-veld om dit te selecteren en klik vervolgens op **Selecteren**.

![](../images/tutorials/map-a-csv-file/xdm-field-selection.png)

Het scherm _Toewijzing_ wordt opnieuw weergegeven, waarbij het geselecteerde XDM-veld nu wordt weergegeven onder _Doelveld_.

![](../images/tutorials/map-a-csv-file/xdm-field-mapped.png)

Als u geen bepaalde CSV-kolom wilt toewijzen, kunt u de toewijzing verwijderen door op het pictogram **** Verwijderen naast het doelveld te klikken. Als u een nieuwe afbeelding wilt toevoegen, klikt u op Nieuwe toewijzing **** toevoegen onder aan de lijst.

![](../images/tutorials/map-a-csv-file/remove-or-add-mapping.png)

Bij het toewijzen van velden kunt u ook functies opnemen om waarden te berekenen op basis van invoerbronvelden. Zie de sectie [toewijzingsfuncties](#mapping-functions) in de bijlage voor meer informatie.

Herhaal bovenstaande stappen om CSV-kolommen verder toe te wijzen aan XDM-velden. Als u klaar bent, klikt u op **Volgende**.

![](../images/tutorials/map-a-csv-file/mapping-finish.png)

## Gegevens samenvoegen

De stap _Samenvatting_ verschijnt, toestaand u om de details van uw brondossier en doeldataset te herzien. Klik op **Samenvatting** om de CSV-gegevens in te voeren. Afhankelijk van de grootte van het CSV-bestand kan dit proces enkele minuten duren. Het scherm wordt bijgewerkt zodra de inname is voltooid, wat aangeeft of de opname is gelukt of mislukt. Klik op **Voltooien** om de workflow te voltooien.

![](../images/tutorials/map-a-csv-file/ingest-data.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een vlak CSV-bestand toegewezen aan een XDM-schema en het ingepakt in Platform. Deze gegevens kunnen nu worden gebruikt door downstreamplatformservices, zoals Real-time klantprofiel. Zie het overzicht [van het profiel van de Klant in](../../profile/home.md) real time voor meer informatie.

## Aanhangsel

De volgende sectie verstrekt extra informatie voor het in kaart brengen CSV kolommen aan XDM gebieden.

### Toewijzingsfuncties

Bepaalde toewijzingsfuncties kunnen worden gebruikt om waarden te berekenen en te berekenen op basis van wat is ingevoerd in bronvelden. Als u een functie wilt gebruiken, typt u deze onder _Bronveld_ met de juiste syntaxis en invoer.

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
| tijdstempel | Hiermee wordt de huidige Unix-tijd opgehaald. | timestamp() | 1571850624571 |
| format | Hiermee wordt de invoerdatum opgemaakt volgens een opgegeven notatie. | format({DATE}, &quot;yyyy-MM-dd HH:mm:ss&quot;) | &quot;2019-10-23 11:24:35&quot; |
| dformat | Converteert een tijdstempel naar een datumtekenreeks volgens een opgegeven notatie. | dformat(1571829875, &quot;dd-MMM-yyyy hh:mm&quot;) | &quot;23-okt-2019 11:24&quot; |
| date | Converteert een datumtekenreeks naar een ZonedDateTime-object (ISO 8601-indeling). | date(&quot;23-okt-2019 11:24&quot;) | &quot;2019-10-23T11:24:00+00:00&quot; |
| date_part | Hiermee worden de delen van de datum opgehaald. De volgende componentwaarden worden ondersteund: <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;quarters&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;month&quot;<br>&quot;m&quot;<br>&quot;m&quot;m&quot;<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>&quot;ofJaar&quot;&quot;y&quot;dag&quot;dag&quot;dag&quot;dd&quot;&quot;d&quot;d&quot;week&quot;week&quot;week&quot;&quot;w&quot;&quot;w&quot;weekdag&quot;&quot;&quot;uur&quot;&quot;&quot;&quot;&quot;hh&quot;&quot;hh24&quot;&quot;hh12&quot;&quot;minute&quot;&quot;mi&quot;&quot;n&quot;&quot;second&quot;&quot;ss&quot;&quot;millisecond&quot;&quot;ms&quot; | date_part(date(&quot;2019-10-17 11:55:12&quot;), &quot;MM&quot;) | 10 |
| set_date_part | Hiermee vervangt u een component in een bepaalde datum. De volgende onderdelen worden geaccepteerd: <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br><br><br><br><br><br><br><br><br><br>&quot;hour&quot;hh&quot;&quot;minute&quot;&quot;mi&quot;mi&quot;&quot;n&quot;tweede&quot;&quot;ss&quot;ss&quot;&quot;s&quot; | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44.797&quot; |
| make_date_time /<br>make_timestamp | Hiermee maakt u een datum op basis van onderdelen. | make_date_time(2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12.0&#x200B;00000999-07:00[America/Los_Angeles]` |
| current_timestamp | Retourneert de huidige tijdstempel. | current_timestamp() | 1571850624571 |
| current_date | Retourneert de huidige datum zonder een tijdcomponent. | current_date() | &quot;18-nov-2019&quot; |
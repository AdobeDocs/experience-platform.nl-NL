---
title: Importeren van Acrobat-perspectiefgegevens
description: Leer hoe u via de gebruikersinterface verbinding maakt met Acrobat Prospecting Data naar Adobe Experience Platform en Adobe Real-Time Customer Data Platform.
last-substantial-update: 2024-02-21T00:00:00Z
badge: Beta
exl-id: cde0bfe9-0604-41d3-8422-114f58a74d04
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1819'
ht-degree: 0%

---

# Een [!DNL Acxiom Prospecting Data Import] bronverbinding en gegevensstroom maken in de gebruikersinterface

>[!NOTE]
>
>De bron [!DNL Acxiom Prospecting Data Import] is in bèta. Gelieve te lezen het [ overzicht van bronnen ](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

De [!DNL Acxiom] -programma voor het doorvoeren van gegevens voor Adobe Real-Time Customer Data Platform is een proces voor het bieden van het meest productieve mogelijke publiek. [!DNL Acxiom] gebruikt Real-Time CDP-gegevens van de eerste partij via een beveiligde exportbewerking en voert deze gegevens uit via een bekroond systeem voor het oplossen van hygiëne en identiteit. Dit veroorzaakt een gegevensdossier dat als onderdrukkingslijst moet worden gebruikt. Dit gegevensdossier wordt dan aangepast tegen het Globale gegevensbestand van Acxiom, dat toelaat dat de perspectieflijsten worden gemaakt voor de invoer.

U kunt de [!DNL Acxiom] bron gebruiken om reacties van de dienst van het Vooruitzicht van Acxiom terug te winnen en in kaart te brengen gebruikend Amazon S3 als dalingspunt.

Lees deze zelfstudie om te leren hoe u een [!DNL Acxiom Prospecting Data Import] bronverbinding en gegevensstroom maakt via de Adobe Experience Platform-gebruikersinterface.

## Vereisten {#prerequisites}

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.
* [[!DNL Prospect Profile]](../../../../../profile/ui/prospect-profile.md): Leer hoe u een perspectiefprofiel maakt en gebruikt om informatie over onbekende klanten te verzamelen met behulp van informatie van derden.

### Vereiste referenties verzamelen

Als u toegang wilt tot uw emmertje op Experience Platform, moet u geldige waarden opgeven voor de volgende referenties:

| Credentials | Beschrijving |
| --- | --- |
| [!DNL Acxiom] verificatiesleutel | De verificatiesleutel. U kunt deze waarde ophalen van het team van [!DNL Acxiom] . |
| [!DNL Amazon S3] toegangstoets | De toegangs belangrijkste identiteitskaart voor uw emmer. U kunt deze waarde ophalen van het team van [!DNL Acxiom] . |
| [!DNL Amazon S3] geheime sleutel | De geheime sleutel-id voor uw emmer. U kunt deze waarde ophalen van het team van [!DNL Acxiom] . |
| Naam van emmertje | Dit is uw emmertje waar de dossiers zullen worden gedeeld. U kunt deze waarde ophalen van het team van [!DNL Acxiom] . |

>[!IMPORTANT]
>
>U moet zowel **[!UICONTROL View Sources]** - als **[!UICONTROL Manage Sources]** -machtigingen hebben ingeschakeld voor uw account om uw [!DNL Acxiom] -account te kunnen verbinden met Experience Platform. Neem contact op met de productbeheerder om de benodigde machtigingen te verkrijgen. Voor meer informatie, lees de [ gids UI van de toegangscontrole ](../../../../../access-control/ui/overview.md).

## Sluit uw [!DNL Acxiom] -account aan

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatiebalk voor toegang tot de werkruimte van [!UICONTROL Sources] . In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie **[!UICONTROL Data & Identity Partners]** de optie **[!UICONTROL Acxiom Prospecting Data Import]** en selecteer vervolgens **[!UICONTROL Set up]** .

>[!TIP]
>
>Een bronkaart die **[!UICONTROL Add data]** weergeeft, houdt in dat de bron al een geverifieerd account heeft. Een bronkaart die **[!UICONTROL Set up]** weergeeft, betekent daarentegen dat u aanmeldingsgegevens moet opgeven en een nieuwe account moet maken om die bron te kunnen gebruiken.

![ de broncatalogus met geselecteerde bron van Acxiom.](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-catalog.png)

### Een nieuwe account maken

Selecteer **[!UICONTROL New account]** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL Acxiom] -gegevens op. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![ de nieuwe rekeningsinterface van het bronwerkschema.](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-new-account.png)

| Credentials | Beschrijving |
| --- | --- |
| Accountnaam | De naam van de account. |
| Beschrijving | (Optioneel) Een korte toelichting van het doel van de rekening. |
| [!DNL Acxiom] verificatiesleutel | De door [!DNL Acxiom] opgegeven sleutel die is vereist voor accountgoedkeuring. Dit moet overeenkomen met de juiste waarde voordat een verbinding met de database tot stand kan worden gebracht.  Deze sleutel moet 24 tekens lang zijn en mag alleen bestaan uit: A-Z, a-z en 0-9. |
| S3-toegangstoets | De S3 toegangstoets verwijst naar de Amazon S3 locatie. Dit wordt verstrekt door uw beheerder wanneer de S3 roltoestemmingen worden bepaald. |
| S3, geheime sleutel | De geheime sleutel S3 verwijst naar de plaats van Amazon S3. Dit wordt verstrekt door uw beheerder wanneer de S3 roltoestemmingen worden bepaald. |
| s3SessionToken | (Optioneel) De waarde van het verificatietoken bij verbinding met S3. |
| serviceUrl | (Optioneel) De URL-locatie die moet worden gebruikt wanneer verbinding wordt gemaakt met S3 op een niet-standaardlocatie. |
| Naam van emmertje | (Optioneel) De naam van het S3-emmertje dat is ingesteld op S3 en dat fungeert als beginpad voor gegevensselectie. |
| Mappad | Als submappen in een emmertje worden gebruikt, kunt u ook een pad opgeven als beginpad in de gegevensselectie. |

### Een bestaande account gebruiken

Selecteer **[!UICONTROL Existing account]** als u een bestaande account wilt gebruiken.

Selecteer een account in de lijst om details over dat account weer te geven. Nadat u een account hebt geselecteerd, selecteert u **[!UICONTROL Next]** om door te gaan.

![ de bestaande rekeningsinterface van het bronwerkschema.](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-existing-account.png)

## Gegevens selecteren

Selecteer het bestand dat u wilt opnemen in het gewenste emmertje en de gewenste submap. U kunt een voorbeeld van de gegevens weergeven wanneer het scheidingsteken en het compressietype zijn gedefinieerd. Nadat u het bestand hebt geselecteerd, selecteert u **[!UICONTROL Next]** om door te gaan.

![ de uitgezochte gegevens en interface van de dossiervoorproef van het bronwerkschema.](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-preview.png)

>[!NOTE]
>
>Hoewel de bestandstypen JSON en Parquet worden vermeld, is het niet vereist of verwacht dat u deze zult gebruiken tijdens de [!DNL Acxiom] -bronworkflow.

## Gegevensset en gegevens over gegevensstroom opgeven

Daarna, moet u informatie betreffende uw dataset en uw gegevensstroom verstrekken.

### Gegevens over gegevensset

>[!BEGINTABS]

>[!TAB  Gebruik een nieuwe dataset ]

Een dataset is een opslag en beheersconstructie voor een inzameling van gegevens, typisch een lijst, die een schema (kolommen) en gebieden (rijen) bevat. De gegevens die met succes in Experience Platform worden opgenomen worden voortgeduurd binnen het gegevensmeer als datasets. Selecteer **[!UICONTROL New dataset]** als u een nieuwe gegevensset wilt gebruiken.

![ de nieuwe datasetinterface.](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-new-dataset.png)

| Nieuwe gegevens gegevensset | Beschrijving |
| --- | --- |
| Naam uitvoergegevensset | De naam van de nieuwe dataset. |
| Beschrijving | (Optioneel) Een korte toelichting van het doel van de gegevensset. |
| Schema | Een vervolgkeuzelijst met schema&#39;s die in uw organisatie bestaan. U kunt ook uw eigen schema vóór het proces van de bronconfiguratie maken. Voor meer informatie, lees de gids op [ creërend schema in UI ](../../../../../xdm/tutorials/create-schema-ui.md). |

>[!TAB  Gebruik een bestaande dataset ]

Selecteer **[!UICONTROL Existing dataset]** als u een bestaande gegevensset wilt gebruiken.

U kunt **[!UICONTROL Advanced search]** selecteren om een venster van alle datasets te bekijken uw organisatie, met inbegrip van hun respectieve details zoals of zij voor opname aan het Profiel van de Klant in real time worden toegelaten.

![ de bestaande datasetinterface.](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-dataset.png)

>[!ENDTABS]

### Gegevens gegevensstroom

Als tijdens deze stap uw gegevensset is ingeschakeld voor Profiel, kunt u de schakeloptie **[!UICONTROL Profile dataset]** selecteren om uw gegevens in te schakelen voor opnemen van profiel. U kunt ook [!UICONTROL Error diagnostics] en [!UICONTROL Partial ingestion] inschakelen.

* **Diagnose van de Fout** - Uitgezochte **Diagnose van de Fout** om de bron op te dragen om foutendiagnostiek te veroorzaken die u kunt later van verwijzingen voorzien gebruikend APIs. Voor meer informatie, lees het [ overzicht van foutendiagnostiek ](../../../../../ingestion/quality/error-diagnostics.md)
* **laat Gedeeltelijke Opname** toe - Gedeeltelijke partijingestie is de capaciteit om gegevens in te voeren die fouten bevatten, tot een bepaalde drempel. Met deze functie kunnen gebruikers al hun juiste gegevens in Adobe Experience Platform opnemen terwijl al hun onjuiste gegevens afzonderlijk worden opgeslagen, samen met informatie over waarom de gegevens ongeldig zijn.  Voor meer informatie, leest het [ Gedeeltelijke ingestitieoverzicht ](../../../../../ingestion/batch-ingestion/partial.md)

![ de interface van de dataflow detailsconfiguraties.](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-dataset-details.png)

| Dataflow-configuraties | Beschrijving |
| --- | --- |
| Naam gegevensstroom | De naam van de gegevensstroom.  Standaard wordt hiervoor de naam gebruikt van het bestand dat wordt geïmporteerd. |
| Beschrijving | (Optioneel) Een korte beschrijving van uw gegevensstroom. |
| Waarschuwingen | Experience Platform kan op gebeurtenissen gebaseerde waarschuwingen produceren waarop gebruikers zich kunnen abonneren. Deze opties zijn allemaal een doorlopende gegevensstroom om deze waarschuwingen te activeren.  Voor meer informatie, lees het [ alarm overzicht ](../../alerts.md) <ul><li>**het Begin van de Looppas van Bronnen Dataflow**: Selecteer dit alarm om een bericht te ontvangen wanneer uw dataflow looppas begint.</li><li>**Bronnen Dataflow de Succes van de Looppas**: Selecteer dit alarm om een bericht te ontvangen als uw dataflow zonder enige fouten beëindigt.</li><li>**de Uitval van de Looppas van Gegevensstroom van Bronnen**: Selecteer dit alarm om een bericht te ontvangen als uw dataflow looppas met om het even welke fouten beëindigt.</li></ul> |

## Toewijzing

Gebruik de toewijzingsinterface om uw brongegevens toe te wijzen aan de aangewezen schemagebieden alvorens gegevens aan Experience Platform in te voeren.  Voor meer informatie, lees de [ kaartgids in UI ](../../../../../data-prep/ui/mapping.md)

![ de afbeeldingsinterface.](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-mapping.png)

## Plaats uw gegevensstroomopname

Gebruik de het plannen interface om het innameprogramma van uw dataflow te bepalen.

| Configuratie plannen | Beschrijving |
| --- | --- |
| Frequentie | Vorm frequentie om erop te wijzen hoe vaak dataflow zou moeten lopen. U kunt de frequentie instellen op: <ul><li>**Eenmaal**: Plaats uw frequentie aan `once` om eenmalig te creëren. Configuraties voor interval en backfill zijn niet beschikbaar wanneer u een eenmalige gegevensstroom maakt. Standaard wordt de planningsfrequentie ingesteld op één keer.</li><li>**Minuut**: Plaats uw frequentie aan `minute` om uw gegevensstroom te plannen om gegevens op een per-minieme basis in te voeren.</li><li>**Uur**: Plaats uw frequentie aan `hour` om uw gegevensstroom te plannen om gegevens op een per-uurbasis in te voeren.</li><li>**Dag**: Plaats uw frequentie aan `day` om uw gegevensstroom te plannen om gegevens op een per-dagbasis in te voeren.</li><li>**Week**: Plaats uw frequentie aan `week` om uw gegevensstroom te plannen om gegevens op een per-weekbasis in te voeren.</li></ul> |
| Interval | Zodra u een frequentie selecteert, kunt u het interval dat dan vormen om het tijdkader tussen elke opname te vestigen. Bijvoorbeeld, als u uw frequentie aan dag plaatst en het interval aan 15 vormt, dan zal uw dataflow om de 15 dagen lopen. U kunt het interval niet instellen op nul. De minimaal toegestane intervalwaarde voor elke frequentie is als volgt:<ul><li>**Eenmaal**: n/a</li><li>**Minuut**: 15</li><li>**Uur**: 1</li><li>**Dag**: 1</li><li>**Week**: 1</li></ul> |
| Begintijd | Het tijdstempel voor de geprojecteerde run, weergegeven in UTC-tijdzone. |
| Achtergrond | Met Backfill wordt bepaald welke gegevens in eerste instantie worden ingevoerd. Als backfill is ingeschakeld, worden alle huidige bestanden in het opgegeven pad tijdens de eerste geplande inname opgenomen. Als terugvullen is uitgeschakeld, worden alleen de bestanden opgenomen die tussen de eerste opname en de begintijd worden geladen. Bestanden die vóór de begintijd zijn geladen, worden niet opgenomen. |

![ de het plannen configuratieinterface.](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-scheduling.png)

## Controleer uw gegevensstroom

Gebruik de overzichtspagina voor een samenvatting van uw gegevensstroom voorafgaand aan opname. De details worden gegroepeerd in de volgende categorieën:

* **Verbinding** - toont het brontype, de relevante weg van het gekozen brondossier, en de hoeveelheid kolommen binnen dat brondossier.
* **wijst dataset en kaartgebieden** toe - toont welke dataset de brongegevens in, met inbegrip van het schema worden opgenomen dat de dataset aan voldoet.
* **Plannend** - toont die actieve periode, frequentie, en interval van het innameprogramma.
Nadat u de gegevensstroom hebt gereviseerd, klikt u op Voltooien en wacht u enige tijd tot de gegevensstroom is gemaakt.

![ De overzichtspagina.](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-review.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een gegevensstroom gemaakt om batchgegevens van uw [!DNL Acxiom] -bron naar Experience Platform te verzenden. Voor extra bronnen raadpleegt u de documentatie die hieronder wordt beschreven.

### Uw gegevensstroom controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over innamesnelheden, succes, en fouten te bekijken. Voor meer informatie over hoe te om dataflow te controleren, bezoek het leerprogramma op [ controlerekeningen en dataflows in UI ](../../monitor.md).

### Uw gegevensstroom bijwerken

Om configuraties voor uw dataflows bij te werken die, afbeelding, en algemene informatie plannen, bezoek het leerprogramma op [ bijwerken brondataflows in UI ](../../update-dataflows.md).

### Uw gegevensstroom verwijderen

U kunt gegevensstromen verwijderen die niet meer nodig zijn of die onjuist zijn gemaakt met de functie **[!UICONTROL Delete]** die beschikbaar is in de **[!UICONTROL Dataflows]** -werkruimte. Voor meer informatie over hoe te om dataflows te schrappen, bezoek het leerprogramma bij [ het schrappen van dataflows in UI ](../../delete.md).

## Aanvullende bronnen {#additional-resources}

[!DNL Acxiom] Poortgegevens en -verspreiding: https://www.acxiom.com/customer-data/audience-data-distribution/

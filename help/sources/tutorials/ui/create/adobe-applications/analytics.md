---
keywords: Experience Platform;home;populaire onderwerpen;Bronaansluiting voor analyse;Analytische aansluiting;Analytische bron;Analytics
solution: Experience Platform
title: Een Adobe Analytics-bronverbinding maken in de gebruikersinterface
topic-legacy: overview
type: Tutorial
description: Leer hoe u een Adobe Analytics-bronverbinding maakt in de gebruikersinterface om consumentengegevens over te brengen naar Adobe Experience Platform.
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: 04a8ca33e712c00d687432ddf9ad82f5d1644db2
workflow-type: tm+mt
source-wordcount: '2167'
ht-degree: 0%

---

# Een Adobe Analytics-bronverbinding maken in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een Adobe Analytics-bronverbinding in de gebruikersinterface om Adobe Analytics-rapportsuite met gegevens naar Adobe Experience Platform te brengen.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Experience Platform:

* [XDM-systeem (Experience Data Model)](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
* [Klantprofiel in realtime](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Belangrijke terminologie

Het is belangrijk dat u de volgende belangrijke termen kent die in dit document worden gebruikt:

* **Standaardkenmerk**: Standaardkenmerken zijn alle kenmerken die vooraf door Adobe zijn gedefinieerd. Zij bevatten dezelfde betekenis voor alle klanten en zijn beschikbaar in de [!DNL Analytics] brongegevens en [!DNL Analytics] schemaveldgroepen.
* **Aangepast kenmerk**: Aangepaste kenmerken zijn alle kenmerken in de aangepaste variabelenhiërarchie in [!DNL Analytics]. De attributen van de douane worden gebruikt binnen een implementatie van Adobe Analytics om specifieke informatie in een rapportreeks te vangen, en zij kunnen in hun gebruik van rapportreeks aan rapportreeks verschillen. Aangepaste kenmerken zijn eVars, props en lijsten. Zie het volgende [[!DNL Analytics] documentatie over conversievariabelen](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) voor meer informatie over eVars.
* **Willekeurig kenmerk in veldgroepen Aangepast**: Kenmerken die afkomstig zijn van veldgroepen die door klanten zijn gemaakt, zijn allemaal door de gebruiker gedefinieerd en worden beschouwd als standaard- of aangepaste kenmerken.
* **Vriendelijke namen**: Vriendelijke namen zijn door mensen verschafte labels voor aangepaste variabelen in een [!DNL Analytics] uitvoering. Zie het volgende [[!DNL Analytics] documentatie over conversievariabelen](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) voor meer informatie over vriendelijke namen .

## Een bronverbinding maken met Adobe Analytics

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Sources]** van de linkernavigatie om tot [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt de zoekbalk ook gebruiken om de weergegeven bronnen te beperken.

Onder de **[!UICONTROL Adobe applications]** categorie, selecteert u **[!UICONTROL Adobe Analytics]** en selecteer vervolgens **[!UICONTROL Add data]**.

![catalogus](../../../../images/tutorials/create/analytics/catalog.png)

### Gegevens selecteren

De **[!UICONTROL Analytics source add data]** deze stap bevat een lijst met [!DNL Analytics] rapporteert reeksgegevens om een bronverbinding met te maken.

Een rapportsuite is een container met gegevens die de basis vormt van [!DNL Analytics] rapportage. Een organisatie kan vele rapportreeksen hebben, elk die verschillende datasets bevatten.

U kunt rapportsuites van om het even welk gebied (Verenigde Staten, Verenigd Koninkrijk, of Singapore) opnemen zolang zij aan de zelfde organisatie zoals de zandbakinstantie van het Experience Platform worden in kaart gebracht waarin de bronverbinding wordt gecreeerd. Een rapportreeks kan worden opgenomen gebruikend slechts één enkele actieve dataflow. Er is al een rapportsuite die niet selecteerbaar is, opgenomen in de sandbox die u gebruikt of in een andere sandbox.

Er kunnen meerdere interne verbindingen worden gemaakt om meerdere rapportsuites over te brengen naar dezelfde sandbox. Als de rapportsuites verschillende schema&#39;s voor variabelen (zoals eVars of gebeurtenissen) hebben, zouden zij aan specifieke gebieden in de groepen van het douanegebied moeten worden in kaart gebracht en gegevensconflicten vermijden gebruikend [Gegevensprep](../../../../../data-prep/ui/mapping.md). Rapportsuites kunnen alleen aan één sandbox worden toegevoegd.

![](../../../../images/tutorials/create/analytics/report-suite.png)

>[!NOTE]
>
>Gegevens uit meerdere rapportsuites kunnen alleen voor realtime klantgegevensprofiel worden ingeschakeld als er geen gegevensconflicten zijn, zoals twee aangepaste eigenschappen (eVars, lijsten en props) die een andere betekenis hebben.

Om een [!DNL Analytics] bronverbinding, selecteer een rapportreeks en selecteer dan **[!UICONTROL Next]** om verder te gaan.

![](../../../../images/tutorials/create/analytics/add-data.png)

<!---Analytics Report Suites can be configured for one sandbox at a time. To import the same Report Suite into a different sandbox, the dataset flow will have to be deleted and instantiated again via configuration for a different sandbox.--->

### Toewijzing

>[!IMPORTANT]
>
>Transformaties van de Prep van gegevens kunnen latentie aan algemene dataflow toevoegen. De extra toegevoegde latentie is afhankelijk van de complexiteit van de transformatielogica.

Voordat u uw [!DNL Analytics] gegevens aan doelXDM schema, moet u eerst selecteren of u een standaardschema of een douaneschema gebruikt.

Een standaardschema leidt tot een nieuw schema namens u, die het [!DNL Adobe Analytics ExperienceEvent Template] veldgroep. Als u een standaardschema wilt gebruiken, selecteert u **[!UICONTROL Default schema]**.

![standaardschema](../../../../images/tutorials/create/analytics/default-schema.png)

Met een aangepast schema kunt u elk beschikbaar schema voor uw [!DNL Analytics] gegevens, zolang dat schema de [!DNL Adobe Analytics ExperienceEvent Template] veldgroep. Als u een aangepast schema wilt gebruiken, selecteert u **[!UICONTROL Custom schema]**.

![aangepast schema](../../../../images/tutorials/create/analytics/custom-schema.png)

De [!UICONTROL Mapping] pagina verstrekt een interface om brongebieden aan hun aangewezen gebieden van het doelschema in kaart te brengen. Van hier, kunt u douanevariabelen aan nieuwe groepen van het schemagebied in kaart brengen en berekeningen toepassen zoals die door de Prep van Gegevens worden gesteund. Selecteer een doelschema om het toewijzingsproces te starten.

>[!TIP]
>
>Alleen schema&#39;s met de [!DNL Adobe Analytics ExperienceEvent Template] de gebiedsgroep wordt getoond in het menu van de schemaselectie. Andere schema&#39;s worden weggelaten. Als er geen aangewezen schema&#39;s beschikbaar voor uw gegevens van de Reeks van het Rapport zijn, dan moet u een nieuw schema tot stand brengen. Voor gedetailleerde stappen bij het creëren van schema&#39;s, zie de gids op [schema&#39;s maken en bewerken in de gebruikersinterface](../../../../../xdm/ui/resources/schemas.md).

![selectieschema](../../../../images/tutorials/create/analytics/select-schema.png)

De [!UICONTROL Map standard fields] sectie geeft deelvensters weer voor [!UICONTROL Standard mappings applied], [!UICONTROL Non matching standard mappings] en [!UICONTROL Custom mappings]. Zie de volgende tabel voor specifieke informatie over elke categorie:

| Standaardvelden toewijzen | Beschrijving |
| --- | --- |
| [!UICONTROL Standard mappings applied] | De [!UICONTROL Standard mappings applied] geeft het totale aantal toegewezen kenmerken weer. Standaardtoewijzingen hebben betrekking op toewijzingsets tussen alle kenmerken in de bron [!DNL Analytics] gegevens en bijbehorende kenmerken in [!DNL Analytics] veldgroep. Deze zijn vooraf toegewezen en kunnen niet worden bewerkt. |
| [!UICONTROL Non matching standard mappings] | De [!UICONTROL Non matching standard mappings] verwijst naar het aantal toegewezen kenmerken die conflicten met vriendschappelijke namen bevatten. Deze conflicten verschijnen wanneer u een schema opnieuw gebruikt dat reeds een bevolkte reeks gebiedsbeschrijvers van een verschillende Reeks van het Rapport heeft. U kunt doorgaan met uw [!DNL Analytics] gegevensstroom zelfs met vriendschappelijke naamconflicten. |
| [!UICONTROL Custom mappings] | De [!UICONTROL Custom mappings] geeft het aantal toegewezen aangepaste kenmerken weer, waaronder eVars, props en lijsten. Aangepaste toewijzingen verwijzen naar toewijzingssets tussen aangepaste kenmerken in de bron [!DNL Analytics] gegevens en kenmerken in aangepaste veldgroepen die zijn opgenomen in het geselecteerde schema. |

![kaartstandaardvelden](../../../../images/tutorials/create/analytics/map-standard-fields.png)

Als u een voorvertoning wilt weergeven van de [!DNL Analytics] ExperienceEvent-sjabloonschemaveldgroep, selecteer **[!UICONTROL View]** in de [!UICONTROL Standard mappings applied] deelvenster.

![weergave](../../../../images/tutorials/create/analytics/view.png)

De [!UICONTROL Adobe Analytics ExperienceEvent Template Schema Field Group] biedt u een interface voor het inspecteren van de structuur van uw schema. Als u klaar bent, selecteert u **[!UICONTROL Close]**.

![field-group-preview](../../../../images/tutorials/create/analytics/field-group-preview.png)

Platform detecteert automatisch uw toewijzingssets voor eventuele conflicten met vriendschappelijke namen. Als er geen conflicten zijn met uw sets toewijzingen, selecteert u **[!UICONTROL Next]** om verder te gaan.

![toewijzing](../../../../images/tutorials/create/analytics/mapping.png)

Als er vriendschappelijke naamconflicten zijn tussen uw bronrapportsuite en uw geselecteerde schema, kunt u toch doorgaan met uw [!DNL Analytics] gegevensstroom, waarbij wordt erkend dat de velddescriptors niet worden gewijzigd. U kunt er ook voor kiezen om een nieuw schema te maken met een lege set beschrijvingen.

Selecteren **[!UICONTROL Next]** om verder te gaan.

![voorzichtigheid](../../../../images/tutorials/create/analytics/caution.png)

#### Aangepaste toewijzingen

Selecteer **[!UICONTROL View custom mappings]**.

![view-custom-mapping](../../../../images/tutorials/create/analytics/view-custom-mapping.png)

Selecteer vervolgens **[!UICONTROL Add new mapping]**.

Afhankelijk van uw behoeften kunt u kiezen uit **[!UICONTROL Add new mapping]** of **[!UICONTROL Add calculated field]** in de weergegeven opties.

![add-new-mapping](../../../../images/tutorials/create/analytics/add-new-mapping.png)

Er wordt een lege toewijzingsset weergegeven. Selecteer het toewijzingspictogram om een bronveld toe te voegen.

![select-source-field](../../../../images/tutorials/create/analytics/select-source-field.png)

U kunt de interface gebruiken om door de bronschemastructuur te navigeren en het nieuwe brongebied te identificeren dat u wilt gebruiken. Als u het bronveld hebt geselecteerd dat u wilt toewijzen, selecteert u **[!UICONTROL Select]**.

![select-mapping](../../../../images/tutorials/create/analytics/select-mapping.png)

Selecteer vervolgens het toewijzingspictogram onder [!UICONTROL Target Field] om het geselecteerde bronveld toe te wijzen aan het desbetreffende doelveld.

![select-target-field](../../../../images/tutorials/create/analytics/select-target-field.png)

Net als het bronschema kunt u met de interface door de doelschemastructuur navigeren en het doelveld selecteren waarnaar u wilt toewijzen. Als u het gewenste doelveld hebt geselecteerd, selecteert u **[!UICONTROL Select]**.

![select-target-mapping](../../../../images/tutorials/create/analytics/select-target-mapping.png)

Selecteer **[!UICONTROL Next]** om verder te gaan.

![volledig-douaneafbeelding](../../../../images/tutorials/create/analytics/complete-custom-mapping.png)

De volgende documentatie verstrekt verdere middelen bij het begrip Prep van Gegevens, berekende gebieden, en kaartfuncties:

* [Overzicht van Data Prep](../../../../../data-prep/home.md)
* [Toewijzingsfuncties van Data Prep](../../../../../data-prep/functions.md)
* [Berekende velden toevoegen](../../../../../data-prep/ui/mapping.md#calculated-fields)

### Filteren voor [!DNL Profile Service] (bèta) {#filtering-for-profile}

>[!CONTEXTUALHELP]
>id="platform_data_prep_analytics_filtering"
>title="Filterregels maken"
>abstract="Bepaal rij en kolom-vlakke het filtreren regels wanneer het verzenden van gegevens naar het Profiel van de Klant in real time. Filteren op rijniveau gebruiken om voorwaarden toe te passen en te bepalen op welke gegevens **include for Profile ingestion**. Het kolom-vlakke filtreren gebruiken om de kolommen van gegevens te selecteren die u wilt **uitsluiten voor opnemen van profiel**. Filterregels zijn niet van toepassing op gegevens die naar een datumpeer worden verzonden."

>[!IMPORTANT]
>
>Ondersteuning voor filteren [!DNL Analytics] gegevens worden momenteel in bèta weergegeven en zijn niet voor alle gebruikers beschikbaar. De documentatie en de functionaliteit kunnen worden gewijzigd.

Nadat u de toewijzingen voor uw [!DNL Analytics] de gegevens van de rapportreeks, kunt u het filtreren regels en voorwaarden toepassen om gegevens te omvatten of uit te sluiten van opname aan [!DNL Profile Service]. Ondersteuning voor filteren is alleen beschikbaar voor [!DNL Analytics] gegevens en gegevens worden alleen gefilterd voordat ze worden ingevoerd [!DNL Profile.] Alle gegevens worden opgenomen in het data Lake.

#### Filteren op rijniveau

>[!IMPORTANT]
>
>Filteren op rijniveau gebruiken om voorwaarden toe te passen en te bepalen op welke gegevens **include for Profile ingestion**. Het kolom-vlakke filtreren gebruiken om de kolommen van gegevens te selecteren die u wilt **uitsluiten voor opnemen van profiel**.

U kunt gegevens filteren voor [!DNL Profile] opname op rij- en kolomniveau. Door het filteren op rijniveau kunt u criteria definiëren, zoals tekenreeksen bevatten, gelijk zijn aan, beginnen of eindigen met. U kunt het rijen-niveau filtreren ook gebruiken om voorwaarden te verbinden gebruikend `AND` alsmede `OR`en de omstandigheden negeren bij `NOT`.

Als u uw [!DNL Analytics] gegevens op rijniveau, selecteer **[!UICONTROL Row filter]**.

![rijfilter](../../../../images/tutorials/create/analytics/row-filter.png)

Gebruik het linkerspoor om door de schemahiërarchie te navigeren en de schemaattributen van uw keus te selecteren om een bepaald schema verder te boren.

![links](../../../../images/tutorials/create/analytics/left-rail.png)

Nadat u het kenmerk hebt geïdentificeerd dat u wilt configureren, selecteert u het kenmerk en sleept u het van de linkerspoorstaaf naar het filterdeelvenster.

![filteren, deelvenster](../../../../images/tutorials/create/analytics/filtering-panel.png)

Selecteer **[!UICONTROL equals]** en selecteer vervolgens een voorwaarde in het vervolgkeuzevenster dat wordt weergegeven.

De lijst configureerbare voorwaarden omvat:

* [!UICONTROL equals]
* [!UICONTROL does not equal]
* [!UICONTROL starts with]
* [!UICONTROL ends with]
* [!UICONTROL does not end with]
* [!UICONTROL contains]
* [!UICONTROL does not contain]
* [!UICONTROL exists]
* [!UICONTROL does not exist]

![voorwaarden](../../../../images/tutorials/create/analytics/conditions.png)

Voer vervolgens de waarden in die u wilt opnemen op basis van het kenmerk dat u hebt geselecteerd. In het onderstaande voorbeeld: [!DNL Apple] en [!DNL Google] worden geselecteerd voor inname als onderdeel van de **[!UICONTROL Manufacturer]** kenmerk.

![include-fabrikant](../../../../images/tutorials/create/analytics/include-manufacturer.png)

Om uw het filtreren voorwaarden verder te specificeren, voeg een ander attribuut van het schema toe en voeg dan waarden toe die op dat attribuut worden gebaseerd. In het onderstaande voorbeeld wordt **[!UICONTROL Model]** kenmerk is toegevoegd en modellen zoals [!DNL iPhone 13] en [!DNL Google Pixel 6] gefilterd voor inname.

![include-model](../../../../images/tutorials/create/analytics/include-model.png)

Als u een nieuwe container wilt toevoegen, selecteert u de ovalen (`...`) rechtsboven in de filterinterface en selecteer vervolgens **[!UICONTROL Add container]**.

![add-container](../../../../images/tutorials/create/analytics/add-container.png)

Als een nieuwe container is toegevoegd, selecteert u **[!UICONTROL Include]** en selecteer vervolgens **[!UICONTROL Exclude]** in het vervolgkeuzevenster dat wordt weergegeven.

![uitsluiten](../../../../images/tutorials/create/analytics/exclude.png)

Voltooi vervolgens hetzelfde proces door de schemakenmerken te slepen en de bijbehorende waarden toe te voegen die u niet wilt filteren. In het onderstaande voorbeeld wordt [!DNL iPhone 12], [!DNL iPhone 12 mini], en [!DNL Google Pixel 5] alle gefilterd zijn van uitsluiting van **[!UICONTROL Model]** kenmerk, liggend is uitgesloten van de **[!UICONTROL Screen orientation]** en modelnummer [!DNL A1633] is uitgesloten van **[!UICONTROL Model number]**.

Als u klaar bent, selecteert u **[!UICONTROL Next]**.

![exclude-examples](../../../../images/tutorials/create/analytics/exclude-examples.png)

#### Filteren op kolomniveau

Selecteren **[!UICONTROL Column filter]** in de koptekst om filteren op kolomniveau toe te passen.

![column-filter](../../../../images/tutorials/create/analytics/column-filter.png)

De pagina wordt bijgewerkt in een interactieve schemastructuur, die uw schemakenattributen op kolom-niveau toont. Van hier, kunt u de kolommen van gegevens selecteren u van zou willen uitsluiten [!DNL Profile] ingestie. U kunt ook een kolom uitvouwen en specifieke kenmerken voor uitsluiting selecteren.

Standaard, alles [!DNL Analytics] ga naar [!DNL Profile] en dit proces maakt het mogelijk vertakkingen van XDM-gegevens uit te sluiten [!DNL Profile] ingestie.

Als u klaar bent, selecteert u **[!UICONTROL Next]**.

![kolommen geselecteerd](../../../../images/tutorials/create/analytics/columns-selected.png)

### Gegevens over gegevensstroom opgeven

De **[!UICONTROL Dataflow detail]** wordt weergegeven, waarin u een naam en een optionele beschrijving voor de gegevensstroom moet opgeven. Selecteren **[!UICONTROL Next]** wanneer gereed.

![dataFlow-detail](../../../../images/tutorials/create/analytics/dataflow-detail.png)

### Controleren

De [!UICONTROL Review] wordt weergegeven, zodat u de nieuwe gegevens voor Analytics kunt bekijken voordat deze worden gemaakt. De details van de verbinding worden gegroepeerd per categorieën, die omvatten:

* [!UICONTROL Connection]: Toont het bronplatform van de verbinding.
* [!UICONTROL Data type]: Hiermee geeft u de geselecteerde rapportsuite en de bijbehorende rapportsuite-id weer.

![revisie](../../../../images/tutorials/create/analytics/review.png)

### Uw gegevensstroom controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen. Van de [!UICONTROL Catalog] scherm, selecteren **[!UICONTROL Dataflows]** om een lijst weer te geven met vastgestelde stromen die zijn gekoppeld aan uw account Analytics.

![select-dataflows](../../../../images/tutorials/create/analytics/select-dataflows.png)

De **Gegevensstromen** wordt weergegeven. Op deze pagina is een paar gegevenssetstromen, met inbegrip van informatie over hun naam, brongegevens, aanmaaktijd, en status.

De schakelaar concretiseert twee datasetstromen. De ene flow vertegenwoordigt de backfill-gegevens en de andere stroom is bedoeld voor live-gegevens. De gegevens van de backfill worden niet gevormd voor Profiel maar wordt verzonden naar het gegevensmeer voor analytische en gegeven-wetenschapsgebruik-gevallen.

Zie voor meer informatie over back-up, live gegevens en de bijbehorende latentie de [Overzicht van de gegevensconnector Analytics](../../../../connectors/adobe-applications/analytics.md).

Selecteer de datasetstroom u wenst om van de lijst te bekijken.

![select-target-dataset](../../../../images/tutorials/create/analytics/select-target-dataset.png)

De **[!UICONTROL Dataset activity]** wordt weergegeven. Op deze pagina wordt de snelheid van berichten weergegeven die in de vorm van een grafiek worden gebruikt. Selecteren **[!UICONTROL Data governance]** in de bovenste koptekst om de etiketteringsvelden te openen.

![datasetactiviteit](../../../../images/tutorials/create/analytics/dataset-activity.png)

U kunt de geërfte etiketten van een datasetstroom van bekijken [!UICONTROL Data governance] scherm. Ga voor meer informatie over het labelen van gegevens afkomstig van Analytics naar de [handleiding met gegevensgebruikslabels](../../../../../data-governance/labels/user-guide.md).

![data-gov](../../../../images/tutorials/create/analytics/data-gov.png)

Als u een gegevensstroom wilt verwijderen, gaat u naar de [!UICONTROL Dataflows] pagina en selecteer vervolgens de ovalen (`...`) naast de naam van de gegevensstroom en selecteer vervolgens [!UICONTROL Delete].

![delete](../../../../images/tutorials/create/analytics/delete.png)

## Volgende stappen en extra bronnen

Zodra de verbinding wordt gecreeerd, wordt de dataflow automatisch gecreeerd om de inkomende gegevens te bevatten en een dataset met uw geselecteerd schema te bevolken. Bovendien vindt de terugvulling van gegevens plaats en neemt deze tot 13 maanden aan historische gegevens in. Wanneer de eerste inname is voltooid, [!DNL Analytics] gegevens en worden gebruikt door downstreamdiensten van Platforms, zoals [!DNL Real-time Customer Profile] en Segmenteringsservice. Raadpleeg de volgende documenten voor meer informatie:

* [[!DNL Real-time Customer Profile] - overzicht](../../../../../profile/home.md)
* [[!DNL Segmentation Service] - overzicht](../../../../../segmentation/home.md)
* [[!DNL Data Science Workspace] - overzicht](../../../../../data-science-workspace/home.md)
* [[!DNL Query Service] - overzicht](../../../../../query-service/home.md)

De volgende video is bedoeld ter ondersteuning van uw inzicht in het opnemen van gegevens via de Adobe Analytics Source-connector:

>[!WARNING]
>
> De [!DNL Platform] De interface die in de volgende video wordt weergegeven, is verouderd. Raadpleeg de bovenstaande documentatie voor de meest recente schermafbeeldingen en functionaliteit van de gebruikersinterface.

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)

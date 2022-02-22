---
keywords: Experience Platform;home;populaire onderwerpen;Bronaansluiting voor analyse;Analytische aansluiting;Analytische bron;Analytics
solution: Experience Platform
title: Een Adobe Analytics-bronverbinding maken in de gebruikersinterface
topic-legacy: overview
type: Tutorial
description: Leer hoe u een Adobe Analytics-bronverbinding maakt in de gebruikersinterface om consumentengegevens over te brengen naar Adobe Experience Platform.
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: 96791e24c59734f82113972a8db9191ea1c0c557
workflow-type: tm+mt
source-wordcount: '1461'
ht-degree: 0%

---

# Een Adobe Analytics-bronverbinding maken in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een Adobe Analytics-bronverbinding in de gebruikersinterface [!DNL Analytics] Rapporteer Suite-gegevens naar Adobe Experience Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [XDM-systeem (Experience Data Model)](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
* [Klantprofiel in realtime](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Belangrijke terminologie

Het is belangrijk dat u de volgende belangrijke termen kent die in dit document worden gebruikt:

* **Standaardkenmerk**: Standaardkenmerken zijn alle kenmerken die vooraf door Adobe zijn gedefinieerd. Zij bevatten dezelfde betekenis voor alle klanten en zijn beschikbaar in de [!DNL Analytics] brongegevens en [!DNL Analytics] schemaveldgroepen.
* **Aangepast kenmerk**: Aangepaste kenmerken zijn alle kenmerken in de aangepaste variabelenhiërarchie in [!DNL Analytics]. De attributen van de douane worden gebruikt binnen een implementatie van Adobe Analytics om specifieke informatie in een Reeks van het Rapport te vangen, en zij kunnen in hun gebruik van de Reeks van het Rapport aan de Reeks van het Rapport verschillen. Aangepaste kenmerken zijn eVars, props en lijsten. Zie het volgende [[!DNL Analytics] documentatie over conversievariabelen](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) voor meer informatie over eVars.
* **Willekeurig kenmerk in veldgroepen Aangepast**: Kenmerken die afkomstig zijn van veldgroepen die door klanten zijn gemaakt, zijn allemaal door de gebruiker gedefinieerd en worden beschouwd als standaard- of aangepaste kenmerken.
* **Vriendelijke namen**: Vriendelijke namen zijn door mensen verschafte labels voor aangepaste variabelen in een [!DNL Analytics] uitvoering. Zie het volgende [[!DNL Analytics] documentatie over conversievariabelen](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) voor meer informatie over vriendelijke namen .

## Een bronverbinding maken met Adobe Analytics

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Sources]** van de linkernavigatie om tot [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt de zoekbalk ook gebruiken om de weergegeven bronnen te beperken.

Onder de **[!UICONTROL Adobe applications]** categorie, selecteert u **[!UICONTROL Adobe Analytics]** en selecteer vervolgens **[!UICONTROL Add data]**.

![catalogus](../../../../images/tutorials/create/analytics/catalog.png)

### Gegevens selecteren

De **[!UICONTROL Analytics source add data]** wordt weergegeven. Selecteren **[!UICONTROL Report Suite]** om een bronverbinding voor de gegevens van de Reeks van het Rapport van Analytics te beginnen, en dan de Reeks van het Rapport te selecteren u zou willen opnemen. Rapportsets die niet kunnen worden geselecteerd, zijn al opgenomen in deze sandbox of in een andere sandbox. Selecteren **[!UICONTROL Next]** om verder te gaan.

>[!NOTE]
>
>Er kunnen meerdere ingebouwde verbindingen worden gemaakt om meerdere rapportsuite in te voeren, maar slechts één rapportsuite kan tegelijk met Real-time Customer Data Platform worden gebruikt.

![](../../../../images/tutorials/create/analytics/add-data.png)

<!---Analytics Report Suites can be configured for one sandbox at a time. To import the same Report Suite into a different sandbox, the dataset flow will have to be deleted and instantiated again via configuration for a different sandbox.--->

### Toewijzing

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

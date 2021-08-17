---
keywords: Experience Platform;home;populaire onderwerpen;Bronaansluiting voor analyse;Analytische aansluiting;Analytische bron;Analytics
solution: Experience Platform
title: Een Adobe Analytics-bronverbinding maken in de gebruikersinterface
topic-legacy: overview
type: Tutorial
description: Leer hoe u een Adobe Analytics-bronverbinding maakt in de gebruikersinterface om consumentengegevens over te brengen naar Adobe Experience Platform.
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: 0af9290a3143b85311fbbd8d194f4799b0c9a873
workflow-type: tm+mt
source-wordcount: '1346'
ht-degree: 0%

---

# Een Adobe Analytics-bronverbinding maken in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een Adobe Analytics-bronverbinding in de gebruikersinterface om gegevens van de [!DNL Analytics]-rapportsuite over te brengen naar Adobe Experience Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [XDM-systeem](../../../../../xdm/home.md) (Experience Data Model): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
* [Klantprofiel](../../../../../profile/home.md) in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Belangrijke terminologie

Het is belangrijk dat u de volgende belangrijke termen kent die in dit document worden gebruikt:

* **Standaardkenmerk**: Standaardkenmerken zijn alle kenmerken die vooraf door Adobe zijn gedefinieerd. Ze bevatten dezelfde betekenis voor alle klanten en zijn beschikbaar in de [!DNL Analytics] brongegevens en [!DNL Analytics] schemaveldgroepen.
* **Aangepast kenmerk**: Aangepaste kenmerken zijn alle kenmerken in de aangepaste dimensie-hiërarchie in  [!DNL Analytics]. Zij zijn ook onder de Adobe-bepaalde schema&#39;s, maar kunnen verschillend door verschillende klanten worden geïnterpreteerd. Aangepaste kenmerken zijn eVars, props en lijsten. Raadpleeg de volgende [[!DNL Analytics] documentatie over conversievariabelen](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) voor meer informatie over Vars.
* **Willekeurig kenmerk in veldgroepen** Aangepast: Kenmerken die afkomstig zijn van veldgroepen die door klanten zijn gemaakt, zijn allemaal door de gebruiker gedefinieerd en worden beschouwd als standaard- of aangepaste kenmerken.
* **Vriendelijke namen**: Vriendelijke namen zijn door mensen verschafte labels voor aangepaste variabelen in een  [!DNL Analytics] implementatie. Zie de volgende [[!DNL Analytics] documentatie over conversievariabelen](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) voor meer informatie over vriendschappelijke namen.

## Een bronverbinding maken met Adobe Analytics

Selecteer **[!UICONTROL Sources]** in de gebruikersinterface van het Platform in de linkernavigatie om de werkruimte [!UICONTROL Sources] te openen. In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt de zoekbalk ook gebruiken om de weergegeven bronnen te beperken.

Selecteer **[!UICONTROL Adobe applications]** onder de categorie **[!UICONTROL Adobe Analytics]** en selecteer **[!UICONTROL Add data]**.

![catalogus](../../../../images/tutorials/create/analytics/catalog.png)

### Gegevens selecteren

De stap **[!UICONTROL Analytics source add data]** wordt weergegeven. Selecteer **[!UICONTROL Report suite]** beginnen een bronverbinding voor de gegevens van de het rapportreeks van Analytics te creëren, en dan de rapportreeks te selecteren u zou willen opnemen. Selecteer **[!UICONTROL Next]** om door te gaan.

>[!NOTE]
>
>Er kunnen meerdere interne verbindingen met een bron worden gemaakt om verschillende gegevens in te voeren.

![](../../../../images/tutorials/create/analytics/add-data.png)

<!---Analytics report suites can be configured for one sandbox at a time. To import the same report suite into a different sandbox, the dataset flow will have to be deleted and instantiated again via configuration for a different sandbox.--->

### Toewijzing

>[!IMPORTANT]
>
>De eigenschap van de Prepsteun van Gegevens voor de [!DNL Analytics] bron is in bèta.

De [!UICONTROL Mapping] pagina verstrekt een interface om brongebieden aan hun aangewezen gebieden van het doelschema in kaart te brengen. Van hier, kunt u douanevariabelen aan nieuwe groepen van het schemagebied in kaart brengen en berekeningen toepassen zoals die door de Prep van Gegevens worden gesteund. Selecteer een doelschema om het toewijzingsproces te starten.

>[!TIP]
>
>Alleen schema&#39;s met de sjabloonveldgroep [!DNL Analytics] worden weergegeven in het menu Schema selecteren. Andere schema&#39;s worden weggelaten. Als er geen aangewezen schema&#39;s beschikbaar voor uw gegevens van de rapportreeks zijn, dan moet u een nieuw schema tot stand brengen. Voor gedetailleerde stappen bij het creëren van schema&#39;s, zie de gids op [het creëren van en het uitgeven van schema&#39;s in UI](../../../../../xdm/ui/resources/schemas.md).

![selectieschema](../../../../images/tutorials/create/analytics/select-schema.png)

In de sectie [!UICONTROL Map standard fields] worden deelvensters voor [!UICONTROL Standard mappings applied], [!UICONTROL Non matching standard mappings] en [!UICONTROL Custom mappings] weergegeven. Zie de volgende tabel voor specifieke informatie over elke categorie:

| Standaardvelden toewijzen | Beschrijving |
| --- | --- |
| [!UICONTROL Standard mappings applied] | In het deelvenster [!UICONTROL Standard mappings applied] wordt het totale aantal toegewezen standaardkenmerken weergegeven. Standaardtoewijzingen hebben betrekking op sets van toewijzingen tussen standaardkenmerken in de [!DNL Analytics]-gegevens van de bron en standaardkenmerken in [!DNL Analytics]-veldgroep. Deze zijn vooraf toegewezen en kunnen niet worden bewerkt. |
| [!UICONTROL Non matching standard mappings] | Het [!UICONTROL Non matching standard mappings] paneel verwijst naar het aantal in kaart gebrachte standaardattributen die vriendschappelijke naamconflicten bevatten. Deze conflicten verschijnen wanneer u een schema opnieuw gebruikt dat reeds een bevolkte reeks gebiedsbeschrijvers heeft. U kunt doorgaan met uw [!DNL Analytics]-gegevensstroom, zelfs met conflicten met vriendelijke namen. |
| [!UICONTROL Custom mappings] | In het [!UICONTROL Custom mappings]-deelvenster wordt het aantal toegewezen aangepaste kenmerken weergegeven, waaronder eVars, props en lijsten. Aangepaste toewijzingen hebben betrekking op toewijzingssets tussen aangepaste kenmerken in de brongegevens [!DNL Analytics] en aangepaste kenmerken in [!DNL Analytics]-veldgroep. Aangepaste kenmerken kunnen worden toegewezen aan andere aangepaste kenmerken en aan standaardkenmerken. |

![kaartstandaardvelden](../../../../images/tutorials/create/analytics/map-standard-fields.png)

Selecteer **[!UICONTROL View]** in het [!UICONTROL Standard mappings applied] deelvenster om een voorvertoning van de [!DNL Analytics] ExperienceEvent-sjabloonschemaveldgroep weer te geven.

![weergave](../../../../images/tutorials/create/analytics/view.png)

De [!UICONTROL Adobe Analytics ExperienceEvent Template Schema Field Group] pagina voorziet u van een interface voor het inspecteren van de structuur van uw schema te gebruiken. Selecteer **[!UICONTROL Close]** als u klaar bent.

![field-group-preview](../../../../images/tutorials/create/analytics/field-group-preview.png)

Platform detecteert automatisch uw toewijzingssets voor eventuele conflicten met vriendschappelijke namen. Als er geen conflicten zijn met uw toewijzingssets, selecteert u **[!UICONTROL Next]** om door te gaan.

![toewijzing](../../../../images/tutorials/create/analytics/mapping.png)

Als er vriendschappelijke naamconflicten in uw kaartreeksen zijn, kunt u nog met uw [!DNL Analytics] dataflow verdergaan, erkennend dat de gebiedsbeschrijvers het zelfde zullen zijn. U kunt er ook voor kiezen om een nieuw schema te maken met een lege set beschrijvingen.

Selecteer **[!UICONTROL Next]** om door te gaan.

![voorzichtigheid](../../../../images/tutorials/create/analytics/caution.png)

#### Aangepaste toewijzingen

Selecteer **[!UICONTROL View custom mappings]** als u Data Prep-functies wilt gebruiken en nieuwe toewijzingen of berekende velden voor aangepaste kenmerken wilt toevoegen.

![view-custom-mapping](../../../../images/tutorials/create/analytics/view-custom-mapping.png)

Selecteer vervolgens **[!UICONTROL Add new mapping]**.

Afhankelijk van uw behoeften, kunt u of **[!UICONTROL Add new mapping]** of **[!UICONTROL Add calculated field]** van de opties selecteren die verschijnen.

![add-new-mapping](../../../../images/tutorials/create/analytics/add-new-mapping.png)

Er wordt een lege toewijzingsset weergegeven. Selecteer het toewijzingspictogram om een bronveld toe te voegen.

![select-source-field](../../../../images/tutorials/create/analytics/select-source-field.png)

U kunt de interface gebruiken om door de bronschemastructuur te navigeren en het nieuwe brongebied te identificeren dat u wilt gebruiken. Wanneer u het bronveld hebt geselecteerd dat u wilt toewijzen, selecteert u **[!UICONTROL Select]**.

![select-mapping](../../../../images/tutorials/create/analytics/select-mapping.png)

Selecteer vervolgens het toewijzingspictogram onder [!UICONTROL Target Field] om het geselecteerde bronveld toe te wijzen aan het desbetreffende doelveld.

![select-target-field](../../../../images/tutorials/create/analytics/select-target-field.png)

Net als het bronschema kunt u met de interface door de doelschemastructuur navigeren en het doelveld selecteren waarnaar u wilt toewijzen. Als u het juiste doelveld hebt geselecteerd, selecteert u **[!UICONTROL Select]**.

![select-target-mapping](../../../../images/tutorials/create/analytics/select-target-mapping.png)

Selecteer **[!UICONTROL Next]** om door te gaan terwijl de aangepaste toewijzingenset is voltooid.

![volledig-douaneafbeelding](../../../../images/tutorials/create/analytics/complete-custom-mapping.png)

De volgende documentatie verstrekt verdere middelen bij het begrip Prep van Gegevens, berekende gebieden, en kaartfuncties:

* [Overzicht van Data Prep](../../../../../data-prep/home.md)
* [Toewijzingsfuncties van Data Prep](../../../../../data-prep/functions.md)
* [Berekende velden toevoegen](../../../../../data-prep/calculated-fields.md)

### Gegevens over gegevensstroom opgeven

De stap **[!UICONTROL Dataflow detail]** verschijnt, waar u een naam en een facultatieve beschrijving voor dataflow moet verstrekken. Selecteer **[!UICONTROL Next]** wanneer gebeëindigd.

![dataFlow-detail](../../../../images/tutorials/create/analytics/dataflow-detail.png)

### Controleren

De stap [!UICONTROL Review] wordt weergegeven, zodat u de nieuwe gegevensstroom Analytics kunt bekijken voordat deze wordt gemaakt. De details van de verbinding worden gegroepeerd per categorieën, die omvatten:

* [!UICONTROL Connection]: Toont het bronplatform van de verbinding.
* [!UICONTROL Data type]: Toont de geselecteerde rapportreeks en zijn overeenkomstige identiteitskaart van de rapportreeks.

![revisie](../../../../images/tutorials/create/analytics/review.png)

### Uw gegevensstroom controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen. Selecteer [!UICONTROL Catalog] in het scherm **[!UICONTROL Dataflows]** om een lijst weer te geven met bestaande stromen die zijn gekoppeld aan uw account Analytics.

![select-dataflows](../../../../images/tutorials/create/analytics/select-dataflows.png)

Het scherm **Dataflows** wordt weergegeven. Op deze pagina is een paar gegevenssetstromen, met inbegrip van informatie over hun naam, brongegevens, aanmaaktijd, en status.

De schakelaar concretiseert twee datasetstromen. De ene flow vertegenwoordigt de backfill-gegevens en de andere stroom is bedoeld voor live-gegevens. De gegevens van de backfill worden niet gevormd voor Profiel maar wordt verzonden naar het gegevensmeer voor analytische en gegeven-wetenschapsgebruik-gevallen.

Zie [Overzicht van de gegevensconnector Analytics](../../../../connectors/adobe-applications/analytics.md) voor meer informatie over backfill, live gegevens en de bijbehorende latentie.

Selecteer de datasetstroom u wenst om van de lijst te bekijken.

![select-target-dataset](../../../../images/tutorials/create/analytics/select-target-dataset.png)

De pagina **[!UICONTROL Dataset activity]** wordt weergegeven. Op deze pagina wordt de snelheid van berichten weergegeven die in de vorm van een grafiek worden gebruikt. Selecteer **[!UICONTROL Data governance]** in de bovenste koptekst om de labelvelden te openen.

![datasetactiviteit](../../../../images/tutorials/create/analytics/dataset-activity.png)

U kunt de geërfte etiketten van een datasetstroom van het [!UICONTROL Data governance] scherm bekijken. Voor meer informatie over hoe te om gegevens te etiketteren die uit Analytics komen, bezoek [de gids van de etiketten van het gegevensgebruik](../../../../../data-governance/labels/user-guide.md).

![data-gov](../../../../images/tutorials/create/analytics/data-gov.png)

Als u een gegevensstroom wilt verwijderen, gaat u naar de [!UICONTROL Dataflows]-pagina en selecteert u vervolgens de ovalen (`...`) naast de naam van de gegevensstroom en selecteert u [!UICONTROL Delete].

![delete](../../../../images/tutorials/create/analytics/delete.png)

## Volgende stappen en extra bronnen

Zodra de verbinding wordt gecreeerd, worden een doelschema en een gegevensstroom automatisch gecreeerd om de inkomende gegevens te bevatten. Bovendien vindt de terugvulling van gegevens plaats en neemt deze tot 13 maanden aan historische gegevens in. Wanneer de eerste opname is voltooid, worden [!DNL Analytics] gegevens gebruikt en worden deze gebruikt door downstreamservices voor Platforms zoals [!DNL Real-time Customer Profile] en Segmentatieservice. Raadpleeg de volgende documenten voor meer informatie:

* [[!DNL Real-time Customer Profile] - overzicht](../../../../../profile/home.md)
* [[!DNL Segmentation Service] - overzicht](../../../../../segmentation/home.md)
* [[!DNL Data Science Workspace] - overzicht](../../../../../data-science-workspace/home.md)
* [[!DNL Query Service] - overzicht](../../../../../query-service/home.md)

De volgende video is bedoeld ter ondersteuning van uw inzicht in het opnemen van gegevens via de Adobe Analytics Source-connector:

>[!WARNING]
>
> De interface [!DNL Platform] die in de volgende video wordt getoond is verouderd. Raadpleeg de bovenstaande documentatie voor de meest recente schermafbeeldingen en functionaliteit van de gebruikersinterface.

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)

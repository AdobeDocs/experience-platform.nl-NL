---
description: Leer hoe u sjablonen in de gebruikersinterface van Adobe Experience Platform kunt gebruiken om uw gegevensverwerking voor B2B-gegevens te versnellen.
title: Een gegevensstroom voor bronnen maken met behulp van sjablonen in de gebruikersinterface
badge1: "Beta"
exl-id: 48aa36ca-656d-4b9d-954c-48c8da9df1e9
source-git-commit: deca8300ebbada548a409de9c6a7b7178d0032e0
workflow-type: tm+mt
source-wordcount: '2215'
ht-degree: 0%

---

# Een gegevensstroom voor bronnen maken met behulp van sjablonen in de gebruikersinterface {#create-a-sources-dataflow-using-templates-in-the-ui}

>[!CONTEXTUALHELP]
>id="platform_sources_marketo_mapping"
>title="Sjablonen voor bronnen in interface van Platform"
>abstract="De malplaatjes omvatten auto-geproduceerde activa zoals schema&#39;s, datasets, identiteiten, toewijzingsregels, identiteitsnamespaces, en dataflows die u kunt gebruiken wanneer het brengen van gegevens van een bron aan Experience Platform. U kunt automatisch gegenereerde elementen bijwerken en deze aan uw wensen aanpassen."

>[!IMPORTANT]
>
>De malplaatjes zijn in bèta en door de volgende bronnen gesteund:
>
>* [[!DNL Marketo Engage]](../../connectors/adobe-applications/marketo/marketo.md)
>* [[!DNL Microsoft Dynamics]](../../connectors/crm/ms-dynamics.md)
>* [[!DNL Salesforce]](../../connectors/crm/salesforce.md)
>
>De documentatie en functies kunnen worden gewijzigd.

Adobe Experience Platform biedt vooraf geconfigureerde sjablonen die u kunt gebruiken om uw gegevensinvoer te versnellen. De malplaatjes omvatten auto-geproduceerde activa zoals schema&#39;s, datasets, identiteiten, toewijzingsregels, identiteitsnamespaces, en dataflows die u kunt gebruiken wanneer het brengen van gegevens van een bron aan Experience Platform.

Met sjablonen kunt u:

* Verminder tijd-aan-waarde van opname door versnelling van templatized activa verwezenlijking.
* Minimaliseer fouten die tijdens het proces van handmatige gegevensinvoer kunnen voorkomen.
* Werk automatisch gegenereerde elementen op elk gewenst moment bij om deze aan te passen aan uw gebruiksscenario&#39;s.

De volgende zelfstudie biedt stappen voor het gebruik van sjablonen in de gebruikersinterface van het Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Experience Platform:

* [Bronnen](../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
* [[!DNL Experience Data Model (XDM)] Systeem](../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
* [Sandboxen](../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

## Sjablonen gebruiken in de gebruikersinterface van het Platform {#use-templates-in-the-platform-ui}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_accounttype"
>title="Bedrijfstype selecteren"
>abstract="Selecteer het juiste bedrijfstype voor uw gebruiksscenario. De toegang hangt af van uw Real-time Customer Data Platform-abonnementaccount."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=nl" text="Real-Time CDP-overzicht"

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Sources]** van de linkernavigatie om tot [!UICONTROL Sources] en bekijk een catalogus met bronnen die beschikbaar zijn in het Experience Platform.

Gebruik de *[!UICONTROL Categories]* om bronnen op categorie te filteren. U kunt ook een bronnaam invoeren in de zoekbalk om een specifieke bron uit de catalogus te zoeken.

Ga naar de [!UICONTROL Adobe applications] categorie om de [!DNL Marketo Engage] bronkaart en selecteer vervolgens [!UICONTROL Add data] om te beginnen.

![Een catalogus van de werkruimte Bronnen met de Marketo Engage-bron gemarkeerd.](../../images/tutorials/templates/catalog.png)

Er verschijnt een pop-upvenster met de optie om sjablonen te doorbladeren of bestaande schema&#39;s en gegevenssets te gebruiken.

* **Door sjablonen bladeren**: Bronsjablonen maken automatisch schema&#39;s, identiteiten, gegevenssets en gegevensstromen met toewijzingsregels voor u. U kunt deze elementen naar wens aanpassen.
* **Mijn bestaande middelen gebruiken**: Maak een overzicht van uw gegevens met behulp van bestaande gegevenssets en schema&#39;s die u hebt gemaakt. U kunt nieuwe datasets en schema&#39;s ook tot stand brengen indien nodig.

Als u automatisch gegenereerde elementen wilt gebruiken, selecteert u **[!UICONTROL Browse templates]** en selecteer vervolgens **[!UICONTROL Select]**.

![Een pop-upvenster met opties voor het bladeren door sjablonen of het gebruik van bestaande elementen.](../../images/tutorials/templates/browse-templates.png)

### Verificatie

De verificatiestap wordt weergegeven en u wordt gevraagd een nieuw account te maken of een bestaand account te gebruiken.

>[!BEGINTABS]

>[!TAB Een bestaande account gebruiken]

Als u een bestaande account wilt gebruiken, selecteert u [!UICONTROL Existing account] en selecteer vervolgens de account die u wilt gebruiken in de lijst die wordt weergegeven.

![De selectiepagina voor een bestaande account met een lijst met bestaande accounts waartoe u toegang hebt.](../../images/tutorials/templates/existing-account.png)

>[!TAB Een nieuwe account maken]

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geef vervolgens uw bronverbindingsgegevens en accountverificatiegegevens op. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat de nieuwe verbinding enige tijd tot stand brengen.

![De verificatiepagina voor een nieuwe account met gegevens over de bronverbinding en verificatiegegevens van de account.](../../images/tutorials/templates/new-account.png)

>[!ENDTABS]

### Sjablonen selecteren

Als uw account is geverifieerd, kunt u nu de sjabloon selecteren die u voor uw gegevensstroom wilt gebruiken.

+++[!DNL Marketo Engage] sjablonen In de volgende tabel worden de sjablonen weergegeven die beschikbaar zijn voor de [!DNL Marketo Engage] bron.

| [!DNL Marketo Engage] sjablonen | Beschrijving |
| --- | --- |
| Activiteiten | In de sjabloon Activiteiten worden op gebeurtenissen gebaseerde momentopnamen van activiteiten vastgelegd, zoals e-mailinteracties, websiteinteracties en verkoopaanroepen. |
| Bedrijven | Het malplaatje van Bedrijven vangt bedrijfsrekeningsdetails zoals bedrijf firmographic informatie, plaats, en het factureren informatie. |
| Benoemde accounts | In de sjabloon Benoemde rekeningen worden details vastgelegd voor rekeningen die zijn vastgesteld als te voeren doelrekeningen. |
| Kansen | In de sjabloon Opportunity worden zakelijke opportuniteitsgegevens vastgelegd, zoals type, verkoopstadium en verwante accounts. |
| Functies contactpersoon opportunity | Het malplaatje van de Rollen van het Contact van de Kans vangt details over de rollen voor lood verbonden aan een bepaalde kans. |
| Personen | In de sjabloon Personen worden kenmerken voor individuele personen vastgelegd, zoals demografische gegevens, contactgegevens en voorkeuren voor machtigingen. |
| Programmalidmaatschappen | Het malplaatje van de Lidmaatschappen van het Programma vangt details voor contacten verbonden aan een bedrijfscampagne, omvat de kakken van de verpleegkunde en contactreacties. |
| Programma&#39;s | In de sjabloon Programma&#39;s worden de details van de zakelijke campagne vastgelegd, zoals status, kanalen, tijdlijnen en kosten. |
| Statische lijstlidmaatschappen | Het Statische malplaatje van Lidmaatschappen van de Lijst vangt de verhoudingen tussen mensen en hun lidmaatschap in statische lijsten. |
| Statische lijsten | Het Statische malplaatje van de Lijst vangt geconcretiseerde lijsten van mensen voor specifieke gebruiksgevallen. |

{style="table-layout:auto"}

+++

+++[!DNL Salesforce] B2B-sjablonen De volgende tabel geeft een overzicht van de B2B-sjablonen die beschikbaar zijn voor de [!DNL Salesforce] bron.

| [!DNL Salesforce] B2B-sjablonen | Beschrijving |
| --- | --- |
| Contact opnemen met account | De sjabloon Relatie contactpersoon account legt de relatie vast tussen een contactpersoon en een of meer accounts. |
| Accounts | In de accountsjabloon worden gegevens van zakelijke accounts vastgelegd, zoals bedrijfsinformatie, locatie en factureringsgegevens. |
| Campagneleden | In de sjabloon Campagneleden wordt de relatie vastgelegd tussen een afzonderlijke lead of contactpersoon en een specifieke [!DNL Salesforce] campagne. |
| Campagnes | Het malplaatje van Campagnes vangt bedrijfsrekeningsdetails zoals bedrijf firmographic informatie, plaats, en het factureren informatie. |
| Contactpersonen | Het malplaatje van het Contact vangt attributen voor contacten zoals demografische details, contactinformatie, en verwante bedrijfsentiteiten. |
| Leads | In de Leads-sjabloon worden kenmerken voor leads vastgelegd, zoals demografische gegevens, contactgegevens en gerelateerde bedrijfsentiteiten. |
| Kansen | De sjabloon Opportunity legt zakelijke opportuniteitsdetails vast, zoals type, verkoopstadium en verwante account. |
| Functies contactpersoon opportunity | Het malplaatje van de Rollen van het Contact van de Kans vangt details over de rollen voor lood verbonden aan een bepaalde kans. |

{style="table-layout:auto"}

+++

+++[!DNL Salesforce] B2C-sjablonen De volgende tabel geeft een overzicht van de B2C-sjablonen die beschikbaar zijn voor de [!DNL Salesforce] bron.

| [!DNL Salesforce] B2C-sjablonen | Beschrijving |
| --- | --- |
| Contact | Het malplaatje van het Contact vangt attributen voor contacten zoals demografische details, contactinformatie, en verwante bedrijfsentiteiten. |
| Lood | In de Lead-sjabloon worden kenmerken voor leads vastgelegd, zoals demografische gegevens, contactgegevens en gerelateerde bedrijfsentiteiten. |

{style="table-layout:auto"}

+++

+++[!DNL Microsoft Dynamics] B2B-sjablonen De volgende tabel geeft een overzicht van de B2B-sjablonen die beschikbaar zijn voor de [!DNL Microsoft Dynamics] bron.

| [!DNL Microsoft Dynamics] B2B-sjablonen | Beschrijving |
| --- | --- |
| Accounts | In de accountsjabloon worden gegevens van zakelijke accounts vastgelegd, zoals bedrijfsinformatie, locatie en factureringsgegevens. |
| Campagnes | Het malplaatje van Campagnes vangt bedrijfsrekeningsdetails zoals bedrijf firmographic informatie, plaats, en het factureren informatie. |
| Contactpersonen | Het malplaatje van het Contact vangt attributen voor contacten zoals demografische details, contactinformatie, en verwante bedrijfsentiteiten. |
| Leads | In de Leads-sjabloon worden kenmerken voor leads vastgelegd, zoals demografische gegevens, contactgegevens en gerelateerde bedrijfsentiteiten. |
| Marketinglijst | Het malplaatje van de Lijst van de Marketing vangt een groep bestaande of potentiële klanten die voor een marketing campagne of andere verkoopdoeleinden worden gecreeerd. |
| Leden van de marketinglijst | De leden van de Lijst van de Marketing vangen de details van om het even welk één type van klantenverslag, zoals lood, rekeningen, of contacten, in een marketing lijst. |
| Kansen | De sjabloon Opportunity legt zakelijke opportuniteitsdetails vast, zoals type, verkoopstadium en verwante account. |
| Functies contactpersoon opportunity | Het malplaatje van de Rollen van het Contact van de Kans vangt details over de rollen voor lood verbonden aan een bepaalde kans. |

{style="table-layout:auto"}

+++

+++[!DNL Microsoft Dynamics] B2C-sjablonen De volgende tabel geeft een overzicht van de B2C-sjablonen die beschikbaar zijn voor de [!DNL Microsoft Dynamics] bron.

| [!DNL Microsoft Dynamics] B2C-sjablonen | Beschrijving |
| --- | --- |
| Contact | Het malplaatje van het Contact vangt attributen voor contacten zoals demografische details, contactinformatie, en verwante bedrijfsentiteiten. |
| Lood | In de Lead-sjabloon worden kenmerken voor leads vastgelegd, zoals demografische gegevens, contactgegevens en gerelateerde bedrijfsentiteiten. |

{style="table-layout:auto"}

+++

Afhankelijk van het geselecteerde bedrijfstype, verschijnt een lijst van malplaatjes. Het voorvertoningspictogram selecteren ![voorvertoningspictogram](../../images/tutorials/templates/preview-icon.png) naast een sjabloonnaam om voorbeeldgegevens van de sjabloon voor te vertonen.

![Een lijst met sjablonen waarop het voorvertoningspictogram is gemarkeerd.](../../images/tutorials/templates/templates.png)

Het voorvertoningsvenster wordt weergegeven, zodat u de voorbeeldgegevens van uw sjabloon kunt bekijken en inspecteren. Als u klaar bent, selecteert u **[!UICONTROL Got it]**.

![Het voorbeeldvenster met voorbeeldgegevens.](../../images/tutorials/templates/preview-sample-data.png)

Selecteer vervolgens in de lijst de sjabloon die u wilt gebruiken. U kunt meerdere sjablonen selecteren en meerdere gegevensstromen tegelijk maken. Een sjabloon kan echter slechts eenmaal per account worden gebruikt. Als u de sjablonen hebt geselecteerd, selecteert u **[!UICONTROL Finish]** en laat u even de elementen genereren.

Als u één of gedeeltelijke punten van de lijst van beschikbare malplaatjes selecteert, zullen alle schema&#39;s B2B en identiteitsnamespaces nog worden geproduceerd om ervoor te zorgen dat de verhoudingen B2B over schema&#39;s correct worden gevormd.

>[!NOTE]
>
>Sjablonen die al zijn gebruikt, worden uitgeschakeld in de selectie.

![De lijst van malplaatjes met het malplaatje van de Rol van het Contact van de Kans geselecteerd.](../../images/tutorials/templates/select-template.png)

### Een schema instellen

De [!DNL Microsoft Dynamics] en de [!DNL Salesforce] bronnen beide ondersteuning bij het plannen van gegevensstromen.

Gebruik de het plannen interface om een innameprogramma voor uw gegevensstromen te vormen. Invoerfrequentie instellen op **Eenmaal** om een eenmalige opname te maken.

![De het plannen interface voor de malplaatjes van de Dynamiek en van Salesforce.](../../images/tutorials/templates/schedule.png)

U kunt ook de innamefrequentie instellen op **Minuut**, **Uur**, **Dag**, of **Week**. Als u uw gegevensstroom voor veelvoudige ingesties plant, dan moet u een interval plaatsen om een tijdkader tussen elke opname te vestigen. Bijvoorbeeld een innamefrequentie ingesteld op **Uur** en een interval instellen op **15** betekent dat uw gegevensstroom gepland is om gegevens elke **15 uur**.

Tijdens deze stap kunt u ook **backfill** en definieert u een kolom voor de incrementele opname van gegevens. Backfill wordt gebruikt om historische gegevens in te voeren, terwijl in de kolom die u voor incrementele inname definieert, nieuwe gegevens kunnen worden onderscheiden van bestaande gegevens.

Nadat u het configureren van uw innameschema hebt voltooid, selecteert u **[!UICONTROL Finish]**.

![De het plannen interface voor Dynamica en malplaatjes Salesforce met toegelaten backfill.](../../images/tutorials/templates/backfill.png)

### Elementen bekijken {#review-assets}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_review"
>title="De automatisch gegenereerde elementen bekijken"
>abstract="Het kan tot vijf minuten duren om alle activa te produceren. Als u ervoor kiest om de pagina te verlaten, ontvangt u een melding om terug te keren zodra de elementen zijn voltooid. U kunt de elementen bekijken zodra ze zijn gegenereerd en op elk gewenst moment aanvullende configuraties aan de gegevensstroom toevoegen."

De [!UICONTROL Review template assets] op de pagina worden de elementen weergegeven die automatisch zijn gegenereerd als onderdeel van de sjabloon. In deze pagina, kunt u de auto-geproduceerde schema&#39;s, datasets, identiteitsnamespaces, en dataflows bekijken verbonden aan uw bronverbinding. Het kan tot vijf minuten duren om alle activa te produceren. Als u ervoor kiest om de pagina te verlaten, ontvangt u een melding om terug te keren zodra de elementen zijn voltooid. U kunt de elementen bekijken zodra ze zijn gegenereerd en op elk gewenst moment aanvullende configuraties aan de gegevensstroom toevoegen.

Door gebrek, worden de auto-geproduceerde dataflows geplaatst aan een ontwerpstaat om verdere aanpassing op configuraties, zoals toewijzingsregels of geplande frequenties toe te staan. De ovalen selecteren (`...`) naast de naam van de gegevensstroom en selecteer vervolgens **[!UICONTROL Preview mappings]** om de toewijzingssets te zien die voor uw conceptgegevensstroom zijn gemaakt.

![Een vervolgkeuzevenster met de optie voor voorvertoningstoewijzingen geselecteerd.](../../images/tutorials/templates/preview.png)

Er wordt een voorvertoningspagina weergegeven waarmee u de toewijzingsrelatie tussen de brongegevensvelden en de doelschemavelden kunt controleren. Zodra u de afbeeldingen van uw gegevensstroom hebt bekeken. Selecteer **[!UICONTROL Got it.]**

![Het voorvertoningsvenster voor toewijzingen.](../../images/tutorials/templates/preview-mappings.png)

U kunt uw gegevensstromen op elk ogenblik na uitvoering bijwerken. De ovalen selecteren (`...`) naast de naam van de gegevensstroom en selecteer vervolgens **[!UICONTROL Update dataflow]**. U wordt genomen aan de pagina van het bronwerkschema waar u uw gegevens kunt bijwerken, met inbegrip van montages voor gedeeltelijke opname, foutendiagnostiek, en waakzame berichten, evenals de afbeelding van uw gegevensstroom.

U kunt de mening van de schemaredacteur gebruiken om updates aan uw auto-geproduceerd schema te maken. Bezoek de handleiding op [het gebruiken van de schemaredacteur](../../../xdm/tutorials/create-schema-ui.md) voor meer informatie .

![Een vervolgkeuzevenster met de optie voor het bijwerken van gegevens geselecteerd.](../../images/tutorials/templates/update.png)

>[!TIP]
>
>U hebt toegang tot uw conceptgegevensstroom via de [!UICONTROL Dataflows] cataloguspagina in de werkruimte Bronnen. Selecteren **[!UICONTROL Dataflows]** in de bovenste koptekst en selecteer vervolgens de gegevensstroom die u wilt bijwerken in de lijst.
>
>![Een lijst van bestaande gegevens in de dataflow catalogus van de bronwerkruimte.](../../images/tutorials/templates/dataflows.png)

### Uw gegevensstroom publiceren

Begin met het publicatieproces door de bronworkflow te doorlopen. Nadat u [!UICONTROL Update dataflow], wordt u doorgestuurd naar de *[!UICONTROL Add data]* stap van de workflow. Selecteren **[!UICONTROL Next]** om verder te gaan.

![De add gegevensstap voor een ontwerp dataflow](../../images/tutorials/templates/continue-draft.png)

Bevestig vervolgens de gegevens in de gegevensstroom en configureer instellingen voor foutdiagnose, gedeeltelijke inname en waarschuwingsmeldingen. Als u klaar bent, selecteert u **[!UICONTROL Next]**.

![De stap met de details van de gegevensstroom voor een conceptgegevensstroom.](../../images/tutorials/templates/dataflow-detail.png)

>[!NOTE]
>
>U kunt **[!UICONTROL Save as draft]** op om het even welk punt om de veranderingen te stoppen en te bewaren u aan uw gegevensstroom hebt aangebracht.

De toewijzingsstap wordt weergegeven. Tijdens deze stap, kunt u de kaartconfiguraties van uw dataflow aanpassen. Voor een uitgebreide gids over de gegevens prep functies die voor afbeelding worden gebruikt, bezoek [UI-hulplijn voor gegevenprep](../../../data-prep/ui/mapping.md).

![De toewijzingsstap voor een conceptgegevensstroom.](../../images/tutorials/templates/mapping.png)

Tot slot herzie de details van uw gegevensstroom en selecteer dan **[!UICONTROL Save & ingest]** om uw concept te publiceren.

![De overzichtsstap voor een ontwerp dataflow.](../../images/tutorials/templates/review.png)

## Volgende stappen

Door dit leerprogramma te volgen, hebt u nu dataflows, evenals activa zoals schema&#39;s, datasets, en identiteitsnamespaces gebruikend malplaatjes gecreeerd. Voor algemene informatie over bronnen gaat u naar de [overzicht van bronnen](../../home.md).

## Waarschuwingen en meldingen {#alerts-and-notifications}

Sjablonen worden ondersteund door Adobe Experience Platform Alerts en u kunt het deelvenster Meldingen gebruiken om updates over de status van uw middelen te ontvangen en ook om terug te gaan naar de overzichtspagina.

Selecteer het berichtpictogram de hoogste kopbal van Platform UI en selecteer dan de statusalarm om de activa te zien die u wilt herzien.

![Het deelvenster Meldingen in de gebruikersinterface van het Platform met een melding die een mislukte gegevensstroom waarschuwt.](../../images/tutorials/templates/notifications.png)

U kunt de waakzame montages van uw malplaatjes bijwerken om zowel e-mail als in-Platform berichten over de status van uw gegevensstroom te ontvangen. Voor meer informatie bij het vormen van alarm, lees de gids op [hoe u zich op waarschuwingen voor gegevensstromen van bronnen kunt abonneren](../ui/alerts.md).
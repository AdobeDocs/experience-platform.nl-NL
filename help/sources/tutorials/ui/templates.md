---
description: Leer hoe u sjablonen in de gebruikersinterface van Adobe Experience Platform kunt gebruiken om uw gegevensverwerking voor B2B-gegevens te versnellen.
title: Een gegevensstroom voor bronnen maken met sjablonen in de gebruikersinterface
badge1: Beta
exl-id: 48aa36ca-656d-4b9d-954c-48c8da9df1e9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2207'
ht-degree: 0%

---

# Een gegevensstroom voor bronnen maken met sjablonen in de gebruikersinterface {#create-a-sources-dataflow-using-templates-in-the-ui}

>[!CONTEXTUALHELP]
>id="platform_sources_marketo_mapping"
>title="Sjablonen voor bronnen in gebruikersinterface van Experience Platform"
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
* Werk automatisch gegenereerde elementen op elk gewenst moment bij om deze aan te passen aan uw gebruiksgevallen.

De volgende zelfstudie biedt stappen voor het gebruik van sjablonen in de gebruikersinterface van Experience Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [ Bronnen ](../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
* [ Sandboxes ](../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

## Sjablonen gebruiken in de gebruikersinterface van Experience Platform {#use-templates-in-the-platform-ui}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_accounttype"
>title="Bedrijfstype selecteren"
>abstract="Selecteer het juiste bedrijfstype voor uw gebruiksscenario. De toegang hangt af van uw Real-Time Customer Data Platform-abonnementaccount."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html" text="Real-Time CDP-overzicht"

Selecteer in de gebruikersinterface van Experience Platform **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van [!UICONTROL Sources] en bekijk een catalogus met bronnen die beschikbaar zijn in Experience Platform.

Gebruik het menu *[!UICONTROL Categories]* om bronnen op categorie te filteren. U kunt ook een bronnaam invoeren in de zoekbalk om een specifieke bron uit de catalogus te zoeken.

Ga naar de categorie [!UICONTROL Adobe applications] om de [!DNL Marketo Engage] bronkaart te zien en selecteer vervolgens [!UICONTROL Add data] om te beginnen.

![ een catalogus van de bronwerkruimte met de benadrukte bron van Marketo Engage.](../../images/tutorials/templates/catalog.png)

Er verschijnt een pop-upvenster met de optie om sjablonen te doorbladeren of bestaande schema&#39;s en gegevenssets te gebruiken.

* **doorbladert malplaatjes**: De bronmalplaatjes leiden automatisch schema&#39;s, identiteiten, datasets, en dataflows met toewijzingsregels voor u. U kunt deze elementen naar wens aanpassen.
* **Gebruik mijn bestaande activa**: Maak uw gegevens gebruikend bestaande datasets en schema&#39;s bekend die u creeerde. U kunt nieuwe datasets en schema&#39;s ook tot stand brengen indien nodig.

Als u automatisch gegenereerde elementen wilt gebruiken, selecteert u **[!UICONTROL Browse templates]** en selecteert u **[!UICONTROL Select]** .

![ pop-up venster van A met opties om malplaatjes te doorbladeren of bestaande activa te gebruiken.](../../images/tutorials/templates/browse-templates.png)

### Verificatie

De verificatiestap wordt weergegeven en u wordt gevraagd een nieuw account te maken of een bestaand account te gebruiken.

>[!BEGINTABS]

>[!TAB  Gebruik een bestaande rekening ]

Als u een bestaande account wilt gebruiken, selecteert u [!UICONTROL Existing account] en selecteert u vervolgens de account die u wilt gebruiken in de lijst die wordt weergegeven.

![ de selectiepagina voor een bestaande rekening met een lijst van bestaande rekeningen u kunt toegang hebben.](../../images/tutorials/templates/existing-account.png)

>[!TAB  creeer een nieuwe rekening ]

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geeft u vervolgens de gegevens van de bronverbinding en de verificatiegegevens van de account op. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![ de authentificatiepagina voor een nieuwe rekening met bronverbindingsdetails en geloofsbrieven van de rekeningsauthentificatie.](../../images/tutorials/templates/new-account.png)

>[!ENDTABS]

### Sjablonen selecteren

Als uw account is geverifieerd, kunt u nu de sjabloon selecteren die u voor uw gegevensstroom wilt gebruiken.

+++[!DNL Marketo Engage] sjablonen
In de volgende tabel worden de sjablonen weergegeven die beschikbaar zijn voor de [!DNL Marketo Engage] -bron.

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

+++[!DNL Salesforce] B2B-sjablonen
In de volgende tabel worden de B2B-sjablonen weergegeven die beschikbaar zijn voor de [!DNL Salesforce] -bron.

| [!DNL Salesforce] B2B-sjablonen | Beschrijving |
| --- | --- |
| Contact opnemen met account | De sjabloon Relatie contactpersoon account legt de relatie vast tussen een contactpersoon en een of meer accounts. |
| Accounts | In de accountsjabloon worden gegevens van zakelijke accounts vastgelegd, zoals bedrijfsinformatie, locatie en factureringsgegevens. |
| Campagneleden | In de sjabloon Campagneleden wordt de relatie vastgelegd tussen een afzonderlijke lead of contactpersoon en een specifieke [!DNL Salesforce] -campagne. |
| Campagnes | Het malplaatje van Campagnes vangt bedrijfsrekeningsdetails zoals bedrijf firmographic informatie, plaats, en het factureren informatie. |
| Contactpersonen | Het malplaatje van het Contact vangt attributen voor contacten zoals demografische details, contactinformatie, en verwante bedrijfsentiteiten. |
| Leads | In de Leads-sjabloon worden kenmerken voor leads vastgelegd, zoals demografische gegevens, contactgegevens en gerelateerde bedrijfsentiteiten. |
| Kansen | De sjabloon Opportunity legt zakelijke opportuniteitsdetails vast, zoals type, verkoopstadium en verwante account. |
| Functies contactpersoon opportunity | Het malplaatje van de Rollen van het Contact van de Kans vangt details over de rollen voor lood verbonden aan een bepaalde kans. |

{style="table-layout:auto"}

+++

+++[!DNL Salesforce] B2C-sjablonen
In de volgende tabel worden de B2C-sjablonen weergegeven die beschikbaar zijn voor de [!DNL Salesforce] -bron.

| [!DNL Salesforce] B2C-sjablonen | Beschrijving |
| --- | --- |
| Contact | Het malplaatje van het Contact vangt attributen voor contacten zoals demografische details, contactinformatie, en verwante bedrijfsentiteiten. |
| Lood | In de Lead-sjabloon worden kenmerken voor leads vastgelegd, zoals demografische gegevens, contactgegevens en gerelateerde bedrijfsentiteiten. |

{style="table-layout:auto"}

+++

+++[!DNL Microsoft Dynamics] B2B-sjablonen
In de volgende tabel worden de B2B-sjablonen weergegeven die beschikbaar zijn voor de [!DNL Microsoft Dynamics] -bron.

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

+++[!DNL Microsoft Dynamics] B2C-sjablonen
In de volgende tabel worden de B2C-sjablonen weergegeven die beschikbaar zijn voor de [!DNL Microsoft Dynamics] -bron.

| [!DNL Microsoft Dynamics] B2C-sjablonen | Beschrijving |
| --- | --- |
| Contact | Het malplaatje van het Contact vangt attributen voor contacten zoals demografische details, contactinformatie, en verwante bedrijfsentiteiten. |
| Lood | In de Lead-sjabloon worden kenmerken voor leads vastgelegd, zoals demografische gegevens, contactgegevens en gerelateerde bedrijfsentiteiten. |

{style="table-layout:auto"}

+++

Afhankelijk van het geselecteerde bedrijfstype, verschijnt een lijst van malplaatjes. Selecteer het voorproefpictogram ![ voorproefpictogram ](/help/images/icons/preview.png) naast een malplaatjenaam aan voorproefgegevens van het malplaatje.

![ een lijst van malplaatjes met het voorproefpictogram benadrukte.](../../images/tutorials/templates/templates.png)

Het voorvertoningsvenster wordt weergegeven, zodat u de voorbeeldgegevens van uw sjabloon kunt bekijken en inspecteren. Selecteer **[!UICONTROL Got it]** als u klaar bent.

![ het venster van voorproefsteekproefgegevens.](../../images/tutorials/templates/preview-sample-data.png)

Selecteer vervolgens in de lijst de sjabloon die u wilt gebruiken. U kunt meerdere sjablonen selecteren en meerdere gegevensstromen tegelijk maken. Een sjabloon kan echter slechts eenmaal per account worden gebruikt. Nadat u de sjablonen hebt geselecteerd, selecteert u **[!UICONTROL Finish]** en laat u de elementen enkele ogenblikken genereren.

Als u één of gedeeltelijke punten van de lijst van beschikbare malplaatjes selecteert, zullen alle schema&#39;s B2B en identiteitsnamespaces nog worden geproduceerd om ervoor te zorgen dat de verhoudingen B2B over schema&#39;s correct worden gevormd.

>[!NOTE]
>
>Sjablonen die al zijn gebruikt, worden uitgeschakeld in de selectie.

![ de lijst van malplaatjes met het malplaatje van de Rol van het Contact van de Kans selecteerde.](../../images/tutorials/templates/select-template.png)

### Een schema instellen

De [!DNL Microsoft Dynamics] en de [!DNL Salesforce] -bronnen ondersteunen beide het plannen van gegevensstromen.

Gebruik de het plannen interface om een innameprogramma voor uw gegevensstromen te vormen. Plaats uw innamefrequentie aan **eens** om eenmalig inname tot stand te brengen.

![ de het plannen interface voor de malplaatjes van de Dynamiek en van Salesforce.](../../images/tutorials/templates/schedule.png)

Alternatief, kunt u uw ingangsfrequentie plaatsen aan **Minuut**, **Uur**, **Dag**, of **Week**. Als u uw gegevensstroom voor veelvoudige ingesties plant, dan moet u een interval plaatsen om een tijdkader tussen elke opname te vestigen. Bijvoorbeeld, een innamefrequentie die aan **wordt geplaatst Uren** en een interval dat aan **wordt geplaatst 15** betekent dat uw dataflow om gegevens in te voeren elk **15 uren**.

Tijdens deze stap, kunt u **backfill** ook toelaten en een kolom voor de stijgende opname van gegevens bepalen. Backfill wordt gebruikt om historische gegevens in te voeren, terwijl in de kolom die u voor incrementele inname definieert, nieuwe gegevens kunnen worden onderscheiden van bestaande gegevens.

Selecteer **[!UICONTROL Finish]** nadat u het configureren van het innameschema hebt voltooid.

![ de het plannen interface voor Dynamica en de malplaatjes van Salesforce met toegelaten backfill.](../../images/tutorials/templates/backfill.png)

### Elementen bekijken {#review-assets}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_review"
>title="De automatisch gegenereerde elementen bekijken"
>abstract="Het kan tot vijf minuten duren om alle activa te produceren. Als u ervoor kiest om de pagina te verlaten, ontvangt u een melding om terug te keren zodra de elementen zijn voltooid. U kunt de elementen bekijken zodra ze zijn gegenereerd en op elk gewenst moment aanvullende configuraties aan de gegevensstroom toevoegen."

Op de pagina [!UICONTROL Review template assets] worden de elementen weergegeven die automatisch zijn gegenereerd als onderdeel van de sjabloon. In deze pagina, kunt u de auto-geproduceerde schema&#39;s, datasets, identiteitsnamespaces, en dataflows bekijken verbonden aan uw bronverbinding. Het kan tot vijf minuten duren om alle activa te produceren. Als u ervoor kiest om de pagina te verlaten, ontvangt u een melding om terug te keren zodra de elementen zijn voltooid. U kunt de elementen bekijken zodra ze zijn gegenereerd en op elk gewenst moment aanvullende configuraties aan de gegevensstroom toevoegen.

Door gebrek, worden de auto-geproduceerde dataflows geplaatst aan een ontwerpstaat om verdere aanpassing op configuraties, zoals toewijzingsregels of geplande frequenties toe te staan. Selecteer de ovalen (`...`) naast de naam van de gegevensstroom en selecteer vervolgens **[!UICONTROL Preview mappings]** om de toewijzingssets weer te geven die voor uw conceptgegevensstroom zijn gemaakt.

![ dropdown venster van A met de geselecteerde voorproefmappings optie.](../../images/tutorials/templates/preview.png)

Er wordt een voorvertoningspagina weergegeven waarmee u de toewijzingsrelatie tussen de brongegevensvelden en de doelschemavelden kunt controleren. Zodra u de afbeeldingen van uw gegevensstroom hebt bekeken. Selecteren **[!UICONTROL Got it.]**

![ het venster van de afbeeldingsvoorproef.](../../images/tutorials/templates/preview-mappings.png)

U kunt uw gegevensstromen op elk ogenblik na uitvoering bijwerken. Selecteer de ovalen (`...`) naast de naam van de gegevensstroom en selecteer vervolgens **[!UICONTROL Update dataflow]** . U wordt genomen aan de pagina van het bronwerkschema waar u uw gegevens kunt bijwerken, met inbegrip van montages voor gedeeltelijke opname, foutendiagnostiek, en waakzame berichten, evenals de afbeelding van uw gegevensstroom.

U kunt de mening van de schemaredacteur gebruiken om updates aan uw auto-geproduceerd schema te maken. Bezoek de gids op [ gebruikend de schemaredacteur ](../../../xdm/tutorials/create-schema-ui.md) voor meer informatie.

![ dropdown venster van A met de geselecteerde update dataflows optie.](../../images/tutorials/templates/update.png)

>[!TIP]
>
>U hebt toegang tot uw conceptgegevensstroom via de cataloguspagina [!UICONTROL Dataflows] in de werkruimte Bronnen. Selecteer **[!UICONTROL Dataflows]** in de bovenste koptekst en selecteer vervolgens in de lijst de gegevensstroom die u wilt bijwerken.
>
>![ een lijst van bestaande dataflows in de dataflows catalogus van de bronwerkruimte.](../../images/tutorials/templates/dataflows.png)

### Uw gegevensstroom publiceren

Begin met het publicatieproces door de bronworkflow te doorlopen. Nadat u [!UICONTROL Update dataflow] hebt geselecteerd, gaat u naar de *[!UICONTROL Add data]* -stap van de workflow. Selecteer **[!UICONTROL Next]** om door te gaan.

![ voegt gegevensstap voor een ontwerp dataflow ](../../images/tutorials/templates/continue-draft.png) toe

Bevestig vervolgens de gegevens in de gegevensstroom en configureer instellingen voor foutdiagnose, gedeeltelijke inname en waarschuwingsmeldingen. Selecteer **[!UICONTROL Next]** als u klaar bent.

![ de dataflow detailstap voor een ontwerp dataflow.](../../images/tutorials/templates/dataflow-detail.png)

>[!NOTE]
>
>U kunt op elk gewenst moment **[!UICONTROL Save as draft]** selecteren om de wijzigingen die u in de gegevensstroom hebt aangebracht, te stoppen en op te slaan.

De toewijzingsstap wordt weergegeven. Tijdens deze stap, kunt u de kaartconfiguraties van uw dataflow aanpassen. Voor een uitvoerige gids over de gegevens prep functies die voor afbeelding worden gebruikt, bezoek de [ gegevens prep UI gids ](../../../data-prep/ui/mapping.md).

![ de afbeeldingsstap voor een ontwerp dataflow.](../../images/tutorials/templates/mapping.png)

Controleer ten slotte de details van uw gegevensstroom en selecteer **[!UICONTROL Save & ingest]** om uw concept te publiceren.

![ de overzichtsstap voor een ontwerp dataflow.](../../images/tutorials/templates/review.png)

## Volgende stappen

Door dit leerprogramma te volgen, hebt u nu dataflows, evenals activa zoals schema&#39;s, datasets, en identiteitsnamespaces gebruikend malplaatjes gecreeerd. Voor algemene informatie over bronnen, bezoek het [ overzicht van bronnen ](../../home.md).

## Waarschuwingen en meldingen {#alerts-and-notifications}

Sjablonen worden ondersteund door Adobe Experience Platform Alerts en u kunt het deelvenster Meldingen gebruiken om updates over de status van uw middelen te ontvangen en ook om terug te gaan naar de overzichtspagina.

Selecteer het berichtpictogram in de bovenste koptekst van de gebruikersinterface van Experience Platform en selecteer vervolgens de statuswaarschuwing om de elementen weer te geven die u wilt controleren.

![ het berichtenpaneel in Experience Platform UI met een bericht alarmerend een ontbroken benadrukt gegevensstroom.](../../images/tutorials/templates/notifications.png)

U kunt de waarschuwingsinstellingen van uw sjablonen bijwerken om zowel e-mailberichten als meldingen in Experience Platform over de status van uw gegevensstromen te ontvangen. Voor meer informatie bij het vormen van alarm, lees de gids op [ hoe te aan alarm voor brondataflows in te schrijven ](../ui/alerts.md).
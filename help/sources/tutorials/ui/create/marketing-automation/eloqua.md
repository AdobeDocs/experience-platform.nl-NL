---
title: Oracle Eloqua (V2) verbinden met Experience Platform in de gebruikersinterface
description: Leer hoe u uw Oracle Eloqua-account in de gebruikersinterface koppelt aan Experience Platform.
source-git-commit: 180754969d4ae8dbd1308dfc85dae73baf64f759
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 0%

---

# Verbind [!DNL Oracle Eloqua] (V2) met Experience Platform in UI

Met de [!DNL Oracle Eloqua (V2)] -bronaansluiting kunt u uw Oracle Eloqua-account aansluiten op Adobe Experience Platform, zodat u belangrijke B2B-marketinggegevens automatisch en schaalbaar kunt invoeren, zoals contactpersonen, accounts, campagnes en betrokkenheidsactiviteiten.

Gebruik deze bronschakelaar om veilige authentificatie te vormen, de nauwkeurige Eloqua gegevensentiteiten te selecteren u wenst, en hen in kaart te brengen aan gestandaardiseerde schema&#39;s van de Gegevens van de Ervaring van het Model (XDM). Met de flexibele planningsopties kunt u zowel initiële gegevensladingen als terugkerende, incrementele syncs instellen, zodat uw marketinggegevens actueel en activeerbaar blijven.

De [!DNL Oracle Eloqua (V2)] -bronaansluiting is gebaseerd op het Adobe Enterprise-innameframework en biedt een betrouwbare, uitbreidbare basis voor het optimaliseren van campagnes, het meten van prestaties en het aanpassen van meerdere kanalen.

Lees deze handleiding voor informatie over hoe u uw [!DNL Oracle Eloqua] -account kunt verbinden met Adobe Experience Platform via de werkruimte Bronnen in de Experience Platform-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

### Vereiste referenties verzamelen {#credentials}

Lees het [[!DNL Eloqua]  overzicht ](../../../../connectors/marketing-automation/eloqua.md) voor informatie over authentificatie.

## Navigeren door de catalogus met bronnen {#catalog}

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van *[!UICONTROL Sources]* . Kies een categorie of gebruik de zoekbalk om de bron te zoeken.

Als u verbinding wilt maken met [!DNL Eloqua] , gaat u naar de categorie *[!UICONTROL Marketing Automation]* , selecteert u de **[!UICONTROL (V2) Oracle Eloqua]** bronkaart en selecteert u vervolgens **[!UICONTROL Set up]** .

>[!TIP]
>
>Bronnen in de catalogus met bronnen geven de optie **[!UICONTROL Set up]** weer wanneer een bepaalde bron nog geen geverifieerde account heeft. Zodra een geverifieerd account is gemaakt, verandert deze optie in **[!UICONTROL Add data]** .

![ Eloqua bronkaart in de broncatalogus met de benadrukte knoop van de Opstelling.](../../../../images/tutorials/create/eloqua/catalog.png)

## Een bestaande account gebruiken {#existing}

Als u een bestaande account wilt gebruiken, selecteert u **[!UICONTROL Existing account]** en vervolgens de [!DNL Eloqua] -account die u wilt gebruiken.

![ de Bestaande die rekeningsoptie in de interface van de rekeningsverwezenlijking wordt geselecteerd.](../../../../images/tutorials/create/eloqua/existing.png)

## Een nieuwe account maken {#new}

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geeft u een naam en beschrijving op onder [!UICONTROL Source connection details] . Daarna, onder [!UICONTROL Account authentication], verstrek waarden voor uw **identiteitskaart van de Cliënt**, **geheim van de Cliënt**, **Gebruikersnaam**, **Wachtwoord**, en **het eindpunt van de Basis**. U kunt de [ authentificatiegids ](../../../../connectors/marketing-automation/eloqua.md) voor meer informatie over deze geloofsbrieven lezen. Selecteer **[!UICONTROL Connect to source]** als u klaar bent en wacht een paar seconden totdat de verbinding tot stand is gebracht.

![ de Nieuwe rekeningsinterface met gebieden voor bronverbindingsdetails en authentificatiegeloofsbrieven.](../../../../images/tutorials/create/eloqua/new.png)

## Gegevens selecteren

Gebruik de interface select data om de entiteit [!DNL Eloqua] te selecteren die u aan Experience Platform wilt toevoegen.

>[!TIP]
>
>Wanneer u gegevens selecteert, ziet u dat de andere entiteiten behalve campagnes representatieve voorbeeldgegevens weergeven. Deze aanpak zorgt ervoor dat u een voorvertoning kunt weergeven van de beschikbare velden en structuur, aangezien [!DNL Eloqua] openbare API&#39;s momenteel alleen echte gegevens voor campagnes ophalen. Voor de overige entiteiten worden voorbeeldgegevens verschaft ter ondersteuning van uw configuratieworkflow.

![ de interface die van de gegevensselectie beschikbare Eloqua gegevensentiteiten toont.](../../../../images/tutorials/create/eloqua/select-data.png)

## Gegevens over gegevensset en gegevensstroom {#details}

Daarna, moet u informatie over uw dataset en dataflow verstrekken. Tijdens deze stap, kunt u of een bestaande dataset gebruiken of een nieuwe dataset creëren. Bovendien, kunt u naar keuze uw dataset voor opname aan het Profiel van de Klant in real time tijdens deze stap toelaten.

![ de dataset en dataflow detailinterface met opties om dataseteigenschappen te vormen.](../../../../images/tutorials/create/eloqua/details.png)

## Toewijzing {#mapping}

Toewijzingen voor [!DNL Eloqua] worden ingedeeld in vier typen hoofdentiteiten:

* **Rekeningen** - Bedrijf/organisatieverslagen van [!DNL Eloqua].
* **Activiteiten** - de activiteit van de marketing en betrokkenheidsgebeurtenissen van [!DNL Eloqua].
* **Campagnes** - de campagneverslagen van de Marketing van [!DNL Eloqua].
* **Contacten** - Individuele persoonverslagen van [!DNL Eloqua].

Als u toegang tot extra gebieden naast die nodig hebt die door gebrek worden verstrekt, kunt u deze gebieden toevoegen gebruikend het proces van de Toewijzing van de Prep van Gegevens in Experience Platform. Als het standaardschema (standaard)geen ondersteuning biedt voor een aantal van uw vereiste velden, kunt u een aangepast schema definiëren in Experience Platform. Met deze functie kunt u de benodigde velden maken en toewijzen, zodat u alle relevante gegevens van [!DNL Eloqua] naadloos kunt opnemen in Experience Platform.

Overzicht van de volgende stappen:

* Controleer de standaard toegewezen gebieden beschikbaar met de integratie.
* Neem tijdens de toewijzingsstap alle aanvullende velden op die nodig zijn vanuit [!DNL Eloqua] .
* Als het standaardschema geen nieuwe velden bevat, breidt u een aangepast schema uit of maakt u een aangepast schema in Experience Platform dat deze velden bevat.
* Voltooi de toewijzing om ervoor te zorgen dat alle gewenste gegevens worden opgenomen.

Om ervoor te zorgen dat uw externe CRM-informatie correct wordt weergegeven, gebruikt u de berekende veldfunctie in Data Prep om de tijdelijke aanduiding van `{CRM_INSTANCE_ID}` bij te werken met uw specifieke CRM-instantie-id in het brongegevensveld. Dit geeft u de flexibiliteit om de integratie aan de unieke opstelling van uw organisatie aan te passen.

Als u de berekende veldeditor wilt gebruiken, selecteert u het bronveld dat u wilt bijwerken.

![ het Eloqua brongebied met berekende gebieden.](../../../../images/tutorials/create/eloqua/select-calculated-field.png)

>[!BEGINTABS]

>[!TAB  Salesforce ]

Voor [!DNL Salesforce] -gebruikers gebruikt u de berekende veldeditor en werkt u de `{CRM_INSTANCE_ID}` bij met de juiste instantie-id.

![ het berekende gebied voor Salesforce.](../../../../images/tutorials/create/eloqua/sf-field.png)

>[!TAB  Microsoft Dynamics ]

Voor [!DNL Microsoft] -gebruikers gebruikt u de berekende veldeditor en werkt u de `{CRM_INSTANCE_ID}` bij met de juiste instantie-id.

![ het berekende gebied voor Dynamica.](../../../../images/tutorials/create/eloqua/dynamics-field.png)

>[!ENDTABS]

Als u de berekende velden hebt bijgewerkt, selecteert u **[!UICONTROL Next]** om door te gaan.

![ de toewijzingsinterface die gebiedsafbeeldingen voor Eloqua gegevensentiteiten toont.](../../../../images/tutorials/create/eloqua/mapping.png)

## Planning

>[!NOTE]
>
>Hieronder vindt u de deltavelden die intern worden gebruikt voor het laden van incrementele gegevens:
>
>* **Contacten:** `C_DateModified`
>* **Rekeningen:** `M_DateModified`
>* **Activiteit:** `CreatedAt`
>* **de Voorwerpen van de Douane:** `UpdatedAt`
>* **Campagne:** `updatedAt`

Met uw afbeelding volledig, kunt u een innameprogramma voor uw gegevensstroom nu vormen. Stel de [!UICONTROL Frequency] in op `Once` om een eenmalige invoeruitvoering te configureren. Voor incrementele invoer kunt u de [!UICONTROL Frequency] instellen op `Hour` , `Day` of `Week` . Wanneer u incrementele inname gebruikt, moet u de [!UICONTROL Interval] ook zodanig configureren dat deze de hoeveelheid tijd definieert die tussen inname-bewerkingen plaatsvindt. Als de innamefrequentie bijvoorbeeld is ingesteld op `Day` en als het interval is ingesteld op `15` , worden gegevens elke 15 dagen opgenomen.

De innamefrequentie per minuut is niet beschikbaar voor de [!DNL Eloqua] bron. Het meest voorkomende schema dat u kunt kiezen, is per uur. Selecteer een schema dat aansluit bij uw behoeften aan gegevensversheid. Houd er rekening mee dat als u een frequentere planning kiest, de kosten van uw computer stijgen.

![ de het plannen interface met opties om innamefrequentie en interval te vormen.](../../../../images/tutorials/create/eloqua/scheduling.png)

## Controleren

Met het gevormde ingenschema, gebruik de [!UICONTROL Review] interface om de details van uw gegevensstroom te bevestigen. Selecteer **[!UICONTROL Finish]** om de installatie te voltooien en de gegevensstroom enkele ogenblikken te laten starten.

![ de overzichtsinterface die een samenvatting van de dataflow configuratie vóór voltooiing toont.](../../../../images/tutorials/create/eloqua/review.png)

## Monitor

Als de gegevensstroom is geselecteerd, worden de gegevens eenmalig teruggevuld en wordt de gegevens vervolgens stapsgewijs gesynchroniseerd volgens het opgegeven schema. De status van synchronisatie kan worden gecontroleerd door aan dataflow te navigeren. Voor meer informatie, leest de gids op [ controlemodellen dataflows in UI ](../../../../../dataflows/ui/monitor-sources.md).

## Volgende stappen

U hebt de installatie en configuratie van uw [!DNL Eloqua] -bron nu voltooid in Experience Platform. Wanneer uw gegevensstroom is ingesteld, worden uw [!DNL Eloqua] -gegevens opgenomen volgens uw gekozen schema en toegewezen aan XDM-schema&#39;s (Standard Experience Data Model). Ga door met het bewaken van uw gegevensstromen en ontdek uw ingesloten gegevens binnen Platform om inzichten te creëren en uw gevallen van marketinggebruik te activeren. Raadpleeg de desbetreffende documentatie voor meer geavanceerde configuraties en probleemoplossing of neem contact op met de Adobe-ondersteuningsbronnen.

Raadpleeg de volgende documentatie voor aanvullende informatie:

* [Overzicht van bronnen](../../../../home.md)
* [Real-Time CDP B2B Edition](../../../../../rtcdp/b2b-overview.md)

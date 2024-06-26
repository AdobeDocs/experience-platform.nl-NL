---
keywords: Experience Platform;thuis;populaire onderwerpen;ui;UI;XDM;XDM systeem;ervaringsgegevensmodel;Ervaring gegevensmodel;Gegevensmodel;Gegevensmodel;Gegevensmodel;Schema redacteur;Schema;Schema;Schema;schema's;Schema's;Schema's;creeer
solution: Experience Platform
title: Een schema maken met de Schema-editor
type: Tutorial
description: Deze zelfstudie behandelt de stappen voor het maken van een schema met behulp van de Schema-editor in het Experience Platform.
exl-id: 3edeb879-3ce4-4adb-a0bd-8d7ad2ec6102
source-git-commit: df0912bcb7122152da127c4e6b625cff73f7fa72
workflow-type: tm+mt
source-wordcount: '4567'
ht-degree: 0%

---

# Een schema maken met de opdracht [!DNL Schema Editor]

Met de Adobe Experience Platform-gebruikersinterface kunt u [!DNL Experience Data Model] (XDM) schema&#39;s in een interactief visueel canvas genoemd [!DNL Schema Editor]. In deze zelfstudie wordt uitgelegd hoe u een schema kunt maken met de [!DNL Schema Editor].

Voor demonstratiedoeleinden, impliceren de stappen in dit leerprogramma het creëren van een voorbeeldschema dat leden van een programma van de klantenloyaliteit beschrijft. Terwijl u deze stappen kunt gebruiken om een verschillend schema voor uw eigen doeleinden tot stand te brengen, adviseert men dat u eerst samen met het creëren van het voorbeeldschema volgt om de mogelijkheden van te leren [!DNL Schema Editor].

>[!NOTE]
>
>Als u CSV-gegevens opneemt in Platform, kunt u [kaart die gegevens aan een schema XDM dat door AI-Gegenereerde aanbevelingen wordt gecreeerd](../../ingestion/tutorials/map-csv/recommendations.md) (momenteel in bèta) zonder het schema zelf manueel te moeten creëren.
>
>Als u liever een schema samenstelt met de opdracht [!DNL Schema Registry] API, begin door te lezen [[!DNL Schema Registry] ontwikkelaarsgids](../api/getting-started.md) voordat u de zelfstudie hebt ingeschakeld [een schema maken met de API](create-schema-api.md).

## Aan de slag

Deze zelfstudie vereist een goed begrip van de verschillende aspecten van Adobe Experience Platform die bij het maken van schema&#39;s betrokken zijn. Lees vóór het starten van deze zelfstudie de documentatie voor de volgende concepten:

* [[!DNL Experience Data Model (XDM)]](../home.md): Het gestandaardiseerde kader waarbinnen [!DNL Platform] organiseert de gegevens van de klantenervaring.
   * [Basisbeginselen van de schemacompositie](../schema/composition.md): Een overzicht van XDM-schema&#39;s en de bijbehorende bouwstenen, waaronder klassen, groepen van schemavelden, gegevenstypen en afzonderlijke velden.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

## Open de [!UICONTROL Schemas] werkruimte {#browse}

De [!UICONTROL Schemas] werkruimte in de [!DNL Platform] UI verstrekt een visualisatie van [!DNL Schema Library], zodat u de schema&#39;s die beschikbaar zijn voor uw organisatie kunt weergeven. De werkruimte bevat ook de [!DNL Schema Editor], het canvas waarop u een schema kunt samenstellen tijdens deze zelfstudie.

Na aanmelden [!DNL Experience Platform], selecteert u **[!UICONTROL Schemas]** in de linkernavigatie om de **[!UICONTROL Schemas]** werkruimte. De **[!UICONTROL Browse]** tabblad geeft een lijst met schema&#39;s weer (een weergave van de [!DNL Schema Library]) kunt weergeven en aanpassen. De lijst bevat de naam, het type, de klasse en het gedrag (record of tijdreeks) waarop het schema is gebaseerd, evenals de datum en tijd waarop het schema voor het laatst is gewijzigd.

Zie de handleiding op [bestaande XDM-bronnen in de gebruikersinterface verkennen](../ui/explore.md) voor meer informatie .

## Een schema maken en een naam geven {#create}

Selecteer **[!UICONTROL Create schema]** in de rechterbovenhoek van het **[!UICONTROL Schemas]** werkruimte.

![De [!UICONTROL Schemas] werkruimte [!UICONTROL Browse] tab met [!UICONTROL Create schema] gemarkeerd.](../images/tutorials/create-schema/create-schema-button.png)

De [!UICONTROL Create schema] wordt weergegeven. Kies vervolgens een basisklasse voor het schema. U kunt kiezen uit de kernklassen van [!UICONTROL XDM Individual Profile] en [!UICONTROL XDM ExperienceEvent], of [!UICONTROL Other] als deze klassen niet geschikt zijn voor uw doeleinden. De [!UICONTROL Other] Met de optie voor klassen kunt u [een nieuwe klasse maken](#create-new-class) of kies uit andere reeds bestaande klassen.

Zie de [Afzonderlijk XDM-profiel](../classes/individual-profile.md) en [XDM ExperienceEvent](../classes/experienceevent.md) documentatie voor meer informatie over deze klassen. In deze zelfstudie selecteert u **[!UICONTROL XDM Individual Profile]** gevolgd door **[!UICONTROL Next]**.

<!-- You can  by selecting either **[!UICONTROL Individual Profile]**, **[!UICONTROL Experience Event]**, or **[!UICONTROL Other]**, followed by **[!UICONTROL Next]** to confirm your choice.  -->


![De [!UICONTROL Create schema] met de [!UICONTROL XDM individual profile] opties en [!UICONTROL Next] gemarkeerd.](../images/tutorials/create-schema/individual-profile-base-class.png)

Nadat u een klasse hebt geselecteerd, [!UICONTROL Name and review] wordt weergegeven. In deze sectie geeft u een naam en beschrijving op om uw schema te identificeren. Er zijn verscheidene belangrijke overwegingen om te maken wanneer het beslissen over een naam voor uw schema:

* De namen van het schema zouden kort en beschrijvend moeten zijn zodat het schema later gemakkelijk kan worden gevonden.
* Schemenamen moeten uniek zijn, wat betekent dat ze ook specifiek genoeg moeten zijn om in de toekomst niet opnieuw te worden gebruikt. Bijvoorbeeld, als uw organisatie afzonderlijke loyaliteitsprogramma&#39;s voor verschillende merken had, zou het verstandig zijn om uw schema &quot;Merk A Loyalty Leden&quot;te noemen om het gemakkelijk te maken om van andere loyaliteits-verwante regelingen onderscheid te maken u zou kunnen later bepalen.
* U kunt de schemabeschrijving ook gebruiken om het even welke extra contextafhankelijke informatie betreffende het schema te verstrekken.

Deze zelfstudie stelt een schema samen om gegevens met betrekking tot de leden van een loyaliteitsprogramma in te voeren, en daarom wordt het schema genoemd &quot;[!DNL Loyalty Members]&quot;.

&#x200B; De basisstructuur van het schema (verstrekt door de klasse) wordt getoond in het canvas voor u om uw geselecteerde klasse en schemastructuur te herzien en te verifiëren.

Ga een mensvriendelijk [!UICONTROL Schema display name] in het tekstveld. Voer vervolgens een geschikte beschrijving in om uw schema te identificeren. Wanneer u de schemastructuur hebt herzien en met uw montages gelukkig bent **[!UICONTROL Finish]** om uw schema te maken.

![De [!UICONTROL Name and review] van de [!UICONTROL Create schema] met de [!UICONTROL Schema display name], [!UICONTROL Description], en [!UICONTROL Finish] gemarkeerd.](../images/ui/resources/schemas/name-and-review.png)

De [!DNL Schema Editor] wordt weergegeven. Dit is het canvas waarop u het schema wilt samenstellen. Het zelfbenoemde schema wordt automatisch gemaakt in het dialoogvenster **[!UICONTROL Structure]** van het canvas wanneer u in de editor aankomt, samen met de standaardvelden in de basisklasse die u hebt geselecteerd. De toegewezen klasse voor het schema wordt ook onder **[!UICONTROL Class]** in **[!UICONTROL Composition]** sectie.

>[!NOTE]
>
>U kunt de weergavenaam en de optionele beschrijving voor het schema bijwerken via het menu  **[!UICONTROL Schema properties]** zijbalk. Zodra een nieuwe naam is ingegaan, werkt het canvas automatisch bij om op de nieuwe naam van het schema te wijzen.

![De Redacteur van het Schema met de benadrukte basisklasse en schemadiagram.](../images/tutorials/create-schema/loyalty-members-schema-editor.png)

>[!NOTE]
>
>U kunt [de klasse van een schema wijzigen](#change-class) op om het even welk punt tijdens het aanvankelijke samenstellingsproces alvorens het schema is bewaard, maar dit zou met uiterste voorzichtigheid moeten worden gedaan. Veldgroepen zijn alleen compatibel met bepaalde klassen. Als u de klasse wijzigt, worden het canvas en alle velden die u hebt toegevoegd opnieuw ingesteld.

## Een veldgroep toevoegen {#field-group}

U kunt nu velden toevoegen aan uw schema door veldgroepen toe te voegen. Een veldgroep is een groep van een of meer velden die vaak samen worden gebruikt om een bepaald concept te beschrijven. Deze zelfstudie gebruikt veldgroepen om de leden van het loyaliteitsprogramma te beschrijven en belangrijke informatie zoals naam, verjaardag, telefoonaantal, adres, en meer te vangen.

Als u een veldgroep wilt toevoegen, selecteert u **[!UICONTROL Add]** in de **[!UICONTROL Field groups]** onderafdeling.

![De Schema-editor met de knop Veldgroepen toevoegen gemarkeerd.](../images/tutorials/create-schema/add-field-group-button.png)

Er wordt een nieuw dialoogvenster weergegeven met een lijst met beschikbare veldgroepen. Elke veldgroep is alleen bedoeld voor gebruik met een specifieke klasse. Daarom worden in het dialoogvenster alleen veldgroepen weergegeven die compatibel zijn met de geselecteerde klasse (in dit geval de klasse [!DNL XDM Individual Profile] klasse). Als u een standaard XDM-klasse gebruikt, wordt de lijst met veldgroepen op intelligente wijze gesorteerd op basis van de populariteit van het gebruik.

![De [!UICONTROL Add field groups] in.](../images/tutorials/create-schema/field-group-popularity.png)

U kunt een van de filters in de linkerraster selecteren om de lijst met standaardveldgroepen te beperken tot specifieke [industrieën](../schema/industries/overview.md) zoals detailhandel, financiële diensten, en gezondheidszorg.

![De [!UICONTROL Add field groups] de dialoog met de industriegerichte groepen .](../images/tutorials/create-schema/industry-field-groups.png)

Als u een veldgroep in de lijst selecteert, wordt deze weergegeven in de rechtertrack. U kunt desgewenst meerdere veldgroepen selecteren en deze aan de lijst in de rechtertrack toevoegen voordat u de groep bevestigt. Bovendien wordt aan de rechterkant van de momenteel geselecteerde veldgroep een pictogram weergegeven waarmee u een voorvertoning kunt weergeven van de structuur van de velden die worden weergegeven.

![De [!UICONTROL Add field groups] wordt weergegeven. Het voorvertoningspictogram van de geselecteerde veldgroep is gemarkeerd.](../images/tutorials/create-schema/preview-field-group-button.png)

Als u een voorbeeld van een veldgroep bekijkt, wordt een gedetailleerde beschrijving van het schema van de veldgroep weergegeven in de rechtertrack. U kunt ook door de velden van de veldgroep navigeren op het beschikbare canvas. Als u verschillende velden selecteert, wordt het rechterspoor bijgewerkt om details over het betreffende veld weer te geven. Selecteren **[!UICONTROL Back]** als u klaar bent met de voorvertoning om terug te keren naar het dialoogvenster voor het selecteren van veldgroepen.

![De [!UICONTROL Preview field group] met de voorbeeldveldgroep Demografische details.](../images/tutorials/create-schema/preview-field-group.png)

Selecteer voor deze zelfstudie de optie **[!UICONTROL Demographic Details]** veldgroep en selecteer vervolgens **[!UICONTROL Add field group]**.

![De [!UICONTROL Add field groups] dialoog met de geselecteerde groep van het veld Demografische details en [!UICONTROL Add field groups] gemarkeerd.](../images/tutorials/create-schema/demographic-details.png)

Het schemacanvas verschijnt opnieuw. De **[!UICONTROL Field groups]** sectie nu lijsten &quot;[!UICONTROL Demographic Details]&quot; en de **[!UICONTROL Structure]** bevat de velden die worden toegevoegd door de veldgroep. U kunt de naam van de veldgroep selecteren onder de naam **[!UICONTROL Field groups]** om de specifieke velden te markeren die worden weergegeven op het canvas.

![De Schema-editor met de groepen in het veld Demografische details gemarkeerd.](../images/tutorials/create-schema/demographic-details-structure.png)

>[!NOTE]
>
>In de Schema-editor worden standaard (door Adobe gegenereerde) klassen en veldgroepen aangeduid met het hangslotpictogram (![Een hangslotpictogram.](../images/ui/explore/padlock-icon.png). Het hangslot verschijnt in de linkerspoorstaaf naast de klasse of de naam van de gebiedsgroep, evenals naast om het even welk gebied in het schemadiagram dat een deel van een systeem-geproduceerde middel is.
>
>![De Schema-editor met het hangslotpictogram gemarkeerd](../images/ui/explore/padlock-icon-highlight.png)

Deze veldgroep levert verschillende velden onder de naam van het hoogste niveau op `person` met het gegevenstype &quot;[!UICONTROL Person]&quot;. In deze groep velden wordt informatie over een individu beschreven, zoals naam, geboortedatum en geslacht.

>[!NOTE]
>
>Houd er rekening mee dat in velden scalaire typen (zoals een tekenreeks, geheel getal, array of datum) kunnen worden gebruikt, evenals elk gegevenstype (een groep velden die een algemeen concept vertegenwoordigen) dat is gedefinieerd in het dialoogvenster [!DNL Schema Registry].

Let erop dat de `name` veld heeft gegevenstype &quot;[!UICONTROL Full name]&quot;, wat betekent dat het ook een algemeen concept beschrijft en naamgerelateerde subvelden bevat, zoals voornaam, achternaam, hoffelijkheidstitel en achtervoegsel.

Selecteer de verschillende velden op het canvas om extra velden weer te geven die worden toegevoegd aan de schemastructuur.

## Meer veldgroepen toevoegen {#field-group-2}

U kunt nu dezelfde stappen herhalen om een andere veldgroep toe te voegen. Wanneer u de **[!UICONTROL Add field group]** deze keer wordt weergegeven, merkt u op dat &quot;[!UICONTROL Demographic Details]&quot; de veldgroep is grijs weergegeven en het selectievakje naast de veldgroep kan niet worden geselecteerd. Zo voorkomt u dat u per ongeluk veldgroepen dupliceert die u al in het huidige schema hebt opgenomen.

Selecteer voor deze zelfstudie de standaardveldgroepen **[!UICONTROL Personal Contact Details]** en **[!UICONTROL Loyalty Details]** in de lijst selecteert u vervolgens **[!UICONTROL Add field groups]** om deze aan het schema toe te voegen.

![De [!UICONTROL Add field groups] dialoog met twee nieuwe geselecteerde veldgroepen en [!UICONTROL Add field groups] gemarkeerd.](../images/tutorials/create-schema/more-field-groups.png)

Het canvas verschijnt weer met toegevoegde veldgroepen die onder **[!UICONTROL Field groups]** in de **[!UICONTROL Composition]** en de bijbehorende samengestelde velden worden toegevoegd aan de schemastructuur.

![De Schema-editor met de nieuwe samengestelde schemastructuur gemarkeerd.](../images/tutorials/create-schema/updated-structure.png)

## Een aangepaste veldgroep definiëren {#define-field-group}

De [!UICONTROL Loyalty Members] schema is bedoeld om gegevens te vangen met betrekking tot de leden van een loyaliteitsprogramma, en de norm [!UICONTROL Loyalty Details] de gebiedsgroep die u aan het schema toevoegde verstrekt het grootste deel van deze, met inbegrip van het programmatype, punten, bij datum aansluiten, en meer.

Er kan echter een scenario zijn waarin u extra aangepaste velden wilt opnemen die niet door standaardveldgroepen worden gedekt om uw gebruiksgevallen te bereiken. Als u velden voor aangepaste loyaliteit toevoegt, hebt u twee opties:

1. Maak een nieuwe aangepaste veldgroep om deze velden vast te leggen. Dit is de methode die in deze zelfstudie wordt behandeld.
1. De standaard uitbreiden [!UICONTROL Loyalty Details] veldgroep met aangepaste velden. Dit veroorzaakt [!UICONTROL Loyalty Details] om te zetten in een aangepaste veldgroep en de oorspronkelijke standaardveldgroep is niet meer beschikbaar. Zie de [!UICONTROL Schemas] UI-gids voor meer informatie over [aangepaste velden toevoegen aan de structuur van standaardveldgroepen](../ui/resources/schemas.md#custom-fields-for-standard-groups).

Als u een nieuwe veldgroep wilt maken, selecteert u **[!UICONTROL Add]** in de **[!UICONTROL Field groups]** subsectie zoals voorheen, maar selecteer deze keer **[!UICONTROL Create New Field group]** boven aan het dialoogvenster dat wordt weergegeven. Vervolgens wordt u gevraagd een weergavenaam en beschrijving op te geven voor de nieuwe veldgroep. In deze zelfstudie geeft u de nieuwe veldgroep de naam &quot;[!DNL Custom Loyalty Details]&quot;, selecteert u vervolgens **[!UICONTROL Add field groups]**.

![De [!UICONTROL Add field groups] dialoog met [!UICONTROL Create new field group], [!UICONTROL Display name] en [!UICONTROL Description] gemarkeerd.](../images/tutorials/create-schema/create-new-field-group.png)

>[!NOTE]
>
>Net als bij klassennamen moet de naam van de veldgroep kort en eenvoudig zijn en beschrijven wat de veldgroep aan het schema zal bijdragen. Ook deze zijn uniek, dus u kunt de naam niet opnieuw gebruiken en moet er dus voor zorgen dat deze voldoende specifiek is.

&quot;[!DNL Custom Loyalty Details]&quot; nu onder **[!UICONTROL Field groups]** aan de linkerkant van het canvas, maar er zijn nog geen gebieden verbonden aan het en daarom verschijnen geen nieuwe gebieden onder **[!UICONTROL Structure]**.

## Velden toevoegen aan de veldgroep {#field-group-fields}

Nu hebt u &quot;[!DNL Custom Loyalty Details]&quot; veldgroep, is het tijd om de gebieden te bepalen die de gebiedsgroep aan het schema zal bijdragen.

Selecteer eerst de **plus (+)** naast de naam van het schema in het canvas.

![De Schema-editor met het plusteken gemarkeerd.](../images/tutorials/create-schema/add-field.png)

Een &quot;[!UICONTROL Untitled Field]&quot; weergegeven op het canvas en de rechterrails worden bijgewerkt om configuratieopties voor het veld weer te geven.

![De Schema-editor met een [!UICONTROL Untitled Field] en het schema [!UICONTROL Field properties] gemarkeerd.](../images/tutorials/create-schema/untitled-field.png)

In dit scenario, moet het schema een voorwerp-type gebied hebben dat de huidige loyaliteitsrij van de persoon in detail beschrijft. Begin met het gebruik van de besturingselementen in het rechterspoor een `loyaltyTier` veld met type &quot;[!UICONTROL Object]&quot; die wordt gebruikt voor de bijbehorende velden.

Onder **[!UICONTROL Assign to]** selecteert u een veldgroep waaraan u het veld wilt toewijzen. Houd er rekening mee dat alle schemavelden tot een klasse of een veldgroep behoren. Aangezien in dit schema een standaardklasse wordt gebruikt, kunt u alleen een veldgroep selecteren. Typ de naam &quot;[!DNL Custom Loyalty Details]&quot;, selecteert u vervolgens de veldgroep in de lijst.

Selecteer **[!UICONTROL Apply]**.

![De Schema-editor met het object Loyalty Tier toegevoegd aan het schema [!UICONTROL Field properties] gemarkeerd.](../images/tutorials/create-schema/loyalty-tier-object.png)

De wijzigingen worden toegepast en de nieuwe `loyaltyTier` wordt weergegeven. Aangezien dit een douanegebied is, wordt het automatisch genesteld binnen een voorwerp genoemd aan huurder ID van uw organisatie, voorafgegaan door een onderstrepingsteken (`_tenantId` in dit voorbeeld).

![De Redacteur van het Schema met huurdersidentiteitskaart en Rij Loyalty die in het schemadiagram wordt benadrukt.](../images/tutorials/create-schema/tenant-id.png)

>[!NOTE]
>
>De aanwezigheid van het voorwerp van huurderidentiteitskaart wijst erop dat de gebieden u toevoegt in namespace van uw organisatie bevat zijn.
>
>Met andere woorden, de velden die u toevoegt, zijn uniek voor uw organisatie en worden opgeslagen in het dialoogvenster [!DNL Schema Registry] in een specifiek gebied dat alleen voor uw organisatie toegankelijk is. De gebieden u bepaalt moeten altijd aan uw huurdersnamespace worden toegevoegd om botsingen met namen van andere standaardklassen, gebiedsgroepen, gegevenstypes, en gebieden te verhinderen.

Selecteer de **plus (+)** pictogram naast `loyaltyTier` -object om subvelden toe te voegen. Er verschijnt een nieuwe plaatsaanduiding voor velden en de **[!UICONTROL Field properties]** is zichtbaar aan de rechterkant van het canvas.

![De Redacteur van het Schema met huurdersidentiteitskaart en nieuw subgebied dat aan de Rij van de Loyalty in het schemadiagram wordt toegevoegd.](../images/tutorials/create-schema/new-field-in-loyalty-tier-object.png)

Voor elk veld is de volgende informatie vereist:

* **[!UICONTROL Field Name]:** De naam van het veld, bij voorkeur geschreven in camelCase. Spaties zijn niet toegestaan. Dit is de naam die wordt gebruikt om in code en in andere downstreamtoepassingen naar het veld te verwijzen.
   * Voorbeeld: loyaltyLevel
* **[!UICONTROL Display Name]:** De naam van het veld, geschreven in hoofdletters/kleine letters. Dit is de naam die op het canvas wordt weergegeven wanneer u het schema weergeeft of bewerkt.
   * Voorbeeld: Loyaliteitsniveau
* **[!UICONTROL Type]:** Het gegevenstype van het veld. Dit omvat fundamentele scalaire types en om het even welke gegevenstypes die in [!DNL Schema Registry]. Voorbeelden: [!UICONTROL String], [!UICONTROL Integer], [!UICONTROL Boolean], [!UICONTROL Person], [!UICONTROL Address], [!UICONTROL Phone number], enz.
* **[!UICONTROL Description]:** Een optionele beschrijving van het veld moet maximaal 200 tekens bevatten.

Het eerste veld voor de `loyaltyTier` object wordt een tekenreeks genoemd `id`, die de id van de huidige laag van het loyaliteitslid vertegenwoordigt. Identiteitskaart van de rij zal uniek voor elk loyaliteitlid zijn, aangezien dit bedrijf verschillende die puntdrempels van de loyaliteitsrij voor elke klant plaatst op verschillende factoren wordt gebaseerd. Het nieuwe veldtype instellen op &quot;[!UICONTROL String]&quot;, en de **[!UICONTROL Field properties]** wordt gevuld met verschillende opties voor het toepassen van beperkingen, zoals standaardwaarde, opmaak en maximumlengte. Zie de documentatie op [aanbevolen procedures voor velden voor gegevensvalidatie](../schema/best-practices.md#data-validation-fields) voor meer informatie.

![De Schema-editor met de waarden van de veldeigenschappen voor het nieuwe id-veld gemarkeerd.](../images/tutorials/create-schema/string-constraints.png)

Sinds `id` een willekeurig gegenereerde vrije-vormtekenreeks, zijn geen verdere beperkingen meer nodig. Selecteren **[!UICONTROL Apply]** om uw wijzigingen toe te passen.

![De Schema-editor met het veld Id toegevoegd en gemarkeerd.](../images/tutorials/create-schema/id-field-added.png)

## Meer velden toevoegen aan de veldgroep {#field-group-fields-2}

Nu hebt u de `id` veld, kunt u extra velden toevoegen om informatie over de loyaliteitslaag vast te leggen, zoals:

* Huidige puntdrempel (geheel getal): het minimale aantal loyaliteitspunten dat het lid moet behouden om in de huidige laag te blijven.
* Drempel van volgende tier (geheel getal): het aantal loyaliteitspunten dat het lid moet krijgen om te kunnen afstuderen aan de volgende laag.
* Ingangsdatum (datum-tijd): de datum waarop het loyaliteitslid zich bij deze lijst heeft aangesloten.

Om elk gebied aan het schema toe te voegen, selecteer **plus (+)** pictogram naast `loyalty` -object en vul de vereiste gegevens in.

Wanneer voltooid, `loyaltyTier` object bevat velden voor `id`, `currentThreshold`, `nextThreshold`, en `effectiveDate`.

![De Schema-editor met het object Loyalty Tier gemarkeerd.](../images/tutorials/create-schema/loyalty-tier-object-fields.png)

## Een opsommingsveld toevoegen aan de veldgroep {#enum}

Wanneer u velden definieert in het dialoogvenster [!DNL Schema Editor]Er zijn enkele aanvullende opties die u kunt toepassen op standaardveldtypen om extra beperkingen op te leggen aan de gegevens die het veld kan bevatten. De gebruiksgevallen voor deze beperkingen worden in de volgende tabel uitgelegd:

| Restrictie | Beschrijving |
| --- | --- |
| [!UICONTROL Required] | Geeft aan dat het veld verplicht is voor gegevensinvoer. Om het even welke gegevens die aan een dataset worden geupload die op dit schema wordt gebaseerd dat dit gebied niet bevat zullen op opname ontbreken. |
| [!UICONTROL Array] | Geeft aan dat het veld een array van waarden bevat, elk met het opgegeven gegevenstype. Als u deze beperking bijvoorbeeld gebruikt voor een veld met het gegevenstype &quot;[!UICONTROL String]&quot; specificeert dat het gebied een serie van koorden zal bevatten. |
| [!UICONTROL Enum & Suggested Values] | Een opsomming geeft aan dat dit veld een van de waarden uit een opsommingslijst met mogelijke waarden moet bevatten. U kunt deze optie ook gebruiken om alleen een lijst met voorgestelde waarden voor een tekenreeksveld op te geven zonder het veld tot die waarden te beperken. |
| [!UICONTROL Identity] | Geeft aan dat dit veld een identiteitsveld is. Meer informatie over identiteitsvelden is beschikbaar [later in deze zelfstudie](#identity-field). |
| [!UICONTROL Relationship] | Hoewel schemarelaties kunnen worden afgeleid door het gebruik van het union-schema en [!DNL Real-Time Customer Profile], is dit alleen van toepassing op schema&#39;s die dezelfde klasse delen. De [!UICONTROL Relationship] beperking geeft aan dat dit veld verwijst naar de primaire identiteit van een schema op basis van een andere klasse, wat een relatie tussen de twee schema&#39;s impliceert. Zie de zelfstudie aan [definiëren van een relatie](./relationship-ui.md) voor meer informatie . |

{style="table-layout:auto"}

>[!NOTE]
>
>Alle vereiste, identiteits- of relatievelden worden vermeld in hun respectieve secties in de linkertrack, zodat u deze velden gemakkelijk kunt vinden, ongeacht de complexiteit van het schema.

Voor deze zelfstudie `loyaltyTier` -object in het schema vereist een nieuw opsommingsveld dat de klasse tier beschrijft, waarbij de waarde slechts een van de vier mogelijke opties kan zijn. Als u dit veld aan het schema wilt toevoegen, selecteert u de **plus (+)** pictogram naast `loyaltyTier` object en vul de vereiste velden in voor **[!UICONTROL Field name]** en **[!UICONTROL Display name]**. Voor **[!UICONTROL Type]** selecteert u &quot;[!UICONTROL String]&quot;.

![De Schema-editor met het object Tier-klasse toegevoegd en gemarkeerd in het dialoogvenster [!UICONTROL Field properties].](../images/tutorials/create-schema/tier-class-type.png)

Er verschijnen extra selectievakjes voor het veld nadat het type is geselecteerd, waaronder selectievakjes voor **[!UICONTROL Array]**, **[!UICONTROL Enum & Suggested Values]**, **[!UICONTROL Identity]**, en **[!UICONTROL Relationship]**.

Selecteer de **[!UICONTROL Enum & Suggested Values]** selectievakje en selecteer vervolgens **[!UICONTROL Enum]**. Hier kunt u de **[!UICONTROL Value]** (in camelCase) en **[!UICONTROL Display Name]** (een optionele, leesvriendelijke naam in het geval van Titel) voor elke acceptabele klasse van de loyaliteitslaag.

Als u alle veldeigenschappen hebt voltooid, selecteert u **[!UICONTROL Apply]** om de `tierClass` aan de `loyaltyTier` object.

![De opsomming en suggesties voor veldeigenschappen van waarden die zijn voltooid met [!UICONTROL Apply] gemarkeerd.](../images/tutorials/create-schema/tier-class-enum.png)

## Een object met meerdere velden omzetten in een gegevenstype {#datatype}

De `loyaltyTier` Het object bevat nu verschillende velden en vertegenwoordigt een algemene gegevensstructuur die nuttig kan zijn in andere schema&#39;s. De [!DNL Schema Editor] Hiermee kunt u gemakkelijk herbruikbare objecten met meerdere velden toepassen door de structuur van die objecten om te zetten in gegevenstypen.

De types van gegevens staan voor het verenigbare gebruik van multi-gebiedsstructuren toe en verstrekken meer flexibiliteit dan een gebiedsgroep omdat zij overal binnen een schema kunnen worden gebruikt. Dit wordt gedaan door het gebied te plaatsen **[!UICONTROL Type]** de waarde van elk gegevenstype dat in de [!DNL Schema Registry].

Als u het dialoogvenster `loyaltyTier` -object naar een gegevenstype, selecteert u de optie `loyaltyTier` op het canvas en selecteert u vervolgens **[!UICONTROL Convert to new data type]** aan de rechterkant van de editor **[!UICONTROL Field properties]**.

![De Schema-editor met het object loyaltyTier en [!UICONTROL Convert to new data type] gemarkeerd.](../images/tutorials/create-schema/convert-data-type.png)

Er wordt een melding weergegeven waarin wordt bevestigd dat het object is geconverteerd. Op het canvas kunt u nu zien dat de `loyaltyTier` field has now a link icon and the right rail indicates it has a data type of &quot;[!DNL Loyalty Tier]&quot;.

![De Redacteur van het Schema met het voorwerp loyaltyTier en de nieuwe benadrukte vertoningsnaam.](../images/tutorials/create-schema/loyalty-tier-data-type.png)

In een toekomstig schema kunt u nu een veld toewijzen als &quot;[!DNL Loyalty Tier]&quot; type en omvat automatisch velden voor ID, klasse op laag, puntdrempels en effectieve datum.

>[!NOTE]
>
>U kunt ook aangepaste gegevenstypen maken en bewerken, onafhankelijk van het bewerken van schema&#39;s. Zie de handleiding op [gegevenstypen maken en bewerken](../ui/resources/data-types.md) voor meer informatie .

## Schema-velden zoeken en filteren

Het schema bevat nu diverse veldgroepen naast de velden die door de basisklasse worden verschaft. Wanneer u met grotere schema&#39;s werkt, kunt u de selectievakjes naast veldgroepnamen in de linkerrail selecteren om de weergegeven velden te filteren op de velden die alleen worden weergegeven door de veldgroepen waarin u geïnteresseerd bent.

![Sommige selectievakjes die zijn geselecteerd in de sectie Veldgroepen van de Schema-editor om de grootte van het schemadiagram te verkleinen.](../images/tutorials/create-schema/filter-by-field-group.png)

Als u een specifiek veld in uw schema zoekt, kunt u ook de zoekbalk gebruiken om weergegeven velden op naam te filteren, ongeacht de veldgroep waarin ze staan.

![Het zoekveld van de Schema-editor met de relevante resultaten gemarkeerd op het canvas.](../images/tutorials/create-schema/search.png)

>[!IMPORTANT]
>
>De zoekfunctie houdt bij het weergeven van overeenkomende velden rekening met alle geselecteerde veldgroepfilters. Als een zoekquery de resultaten die u verwacht niet weergeeft, moet u mogelijk twee keer controleren of er geen relevante veldgroepen worden uitgefilterd.

## Een schemaveld instellen als een identiteitsveld {#identity-field}

De standaard gegevensstructuur die schema&#39;s verstrekken kan worden gebruikt om gegevens te identificeren die tot het zelfde individu over veelvoudige bronnen behoren, die voor diverse stroomafwaartse gebruiksgevallen zoals segmentatie, rapportering, gegevenswetenschapsanalyse, en meer toestaan. Om gegevens op basis van individuele identiteiten te koppelen, moeten de sleutelvelden worden gemarkeerd als [!UICONTROL Identity] velden binnen toepasselijke schema&#39;s.

[!DNL Experience Platform] maakt het gemakkelijk om een identiteitsgebied door het gebruiken van **[!UICONTROL Identity]** Selectievakje in het dialoogvenster [!DNL Schema Editor]. U moet echter bepalen welk veld de beste kandidaat is om als identiteit te gebruiken, op basis van de aard van uw gegevens.

Bijvoorbeeld, kunnen er duizenden leden van het loyaliteitsprogramma tot het zelfde loyaliteitsniveau behoren, en verscheidene die het zelfde fysieke adres kunnen delen. In dit scenario, echter, bij inschrijving verstrekt elk lid van het loyaliteitsprogramma zijn persoonlijk e-mailadres. Aangezien persoonlijke e-mailadressen meestal door één persoon worden beheerd, wordt het veld `personalEmail.address` (verstrekt door de [!UICONTROL Personal Contact Details] veldgroep) is een goede kandidaat voor een identiteitsveld.

>[!IMPORTANT]
>
>De stappen hieronder beschrijven hoe te om een identiteitsbeschrijver aan een bestaand schemagebied toe te voegen. Als alternatief voor het definiëren van identiteitsvelden binnen de structuur van het schema zelf, kunt u ook een `identityMap` in plaats daarvan identiteitsgegevens te bevatten.
>
>Als u van plan bent te gebruiken `identityMap`, houd in mening dat het om het even welke primaire identiteit zal met voeten treden u direct aan het schema toevoegt. Zie de sectie over `identityMap` in de [grondbeginselen van de schemacompositie](../schema/composition.md#identityMap) voor meer informatie .

Selecteer de `personalEmail.address` op het canvas en de **[!UICONTROL Identity]** selectievakje wordt weergegeven onder **[!UICONTROL Field properties]**. Schakel het selectievakje in en stel dit in als de optie **[!UICONTROL Primary identity]** wordt weergegeven. Selecteer dit vak ook.

>[!NOTE]
>
>Elk schema mag slechts één primair identiteitsveld bevatten. Zodra een schemagebied als primaire identiteit is geplaatst, zult u een foutenmelding ontvangen als u later probeert om een ander identiteitsgebied in het schema als primaire identiteit te plaatsen.

Vervolgens moet u een **[!UICONTROL Identity namespace]** in de lijst met vooraf gedefinieerde naamruimten in de vervolgkeuzelijst. Aangezien dit veld het e-mailadres van de klant is, selecteert u &quot;[!UICONTROL Email]&quot; uit het vervolgkeuzemenu. Selecteren **[!UICONTROL Apply]** ter bevestiging van de bijwerkingen van de `personalEmail.address` veld.

![De Schema-editor met het e-mailadres gemarkeerd en het selectievakje Primaire identiteit ingeschakeld.](../images/tutorials/create-schema/primary-identity.png)

>[!NOTE]
>
>Voor een lijst van standaardnamespaces en hun definities, zie [[!DNL Identity Service] documentatie](../../identity-service/troubleshooting-guide.md#standard-namespaces).

Nadat u de wijziging hebt toegepast, wordt het pictogram voor `personalEmail.address` geeft een vingerafdruksymbool weer dat aangeeft dat het nu een identiteitsveld is. Het veld wordt ook vermeld in het linkerspoor onder **[!UICONTROL Identities]**.

![De Redacteur van het Schema met het e-mailadres benadrukt en het identiteitsgebied dat in de schemacompositie wordt benadrukt sidebar.](../images/tutorials/create-schema/identity-applied.png)

Nu alle gegevens die in de `personalEmail.address` wordt gebruikt om te helpen die persoon identificeren en één enkele mening van die klant verbinden. Meer informatie over het werken met identiteiten in [!DNL Experience Platform], bekijk de [[!DNL Identity Service]](../../identity-service/home.md) documentatie.

## Het schema inschakelen voor gebruik in [!DNL Real-Time Customer Profile] {#profile}

[[!DNL Real-Time Customer Profile]](../../profile/home.md) gebruikt identiteitsgegevens in [!DNL Experience Platform] een holistische visie op elke individuele klant te geven. De dienst bouwt robuuste, 360° profielen van klantenattributen evenals timestamped rekeningen van elke interactie die klanten over om het even welk systeem hebben geïntegreerd met [!DNL Experience Platform].

Een schema kan alleen worden ingeschakeld voor gebruik met [!DNL Real-Time Customer Profile], moet er een primaire identiteit worden gedefinieerd. Er wordt een foutbericht weergegeven als u een schema wilt inschakelen zonder eerst een primaire identiteit te definiëren.

![Het dialoogvenster Ontbrekende primaire identiteit.](../images/tutorials/create-schema/missing-primary-identity.png)

Het schema &quot;Loyalty-leden&quot; inschakelen voor gebruik in [!DNL Profile]selecteert u eerst de titel van het schema in het canvas.

Rechts in de editor wordt informatie over het schema weergegeven, inclusief de weergavenaam, beschrijving en type. Naast deze informatie is er een **[!UICONTROL Profile]** schakelknop.

![De Schema-editor met de hoofdmap van het schema en de schakeloptie Inschakelen voor profiel gemarkeerd.](../images/tutorials/create-schema/profile-toggle.png)

Selecteren **[!UICONTROL Profile]** en wordt een pop-up weergegeven met de vraag of u het schema wilt inschakelen voor [!DNL Profile].

![Het bevestigingsvenster Inschakelen voor profiel.](../images/tutorials/create-schema/enable-profile.png)

>[!WARNING]
>
>Zodra een schema is toegelaten voor [!DNL Real-Time Customer Profile] en opgeslagen, kan deze niet worden uitgeschakeld.

Selecteren **[!UICONTROL Enable]** om uw keuze te bevestigen. U kunt de **[!UICONTROL Profile]** schakelen opnieuw om het schema uit te schakelen als u dit wenst, maar als het schema is opgeslagen terwijl [!DNL Profile] is ingeschakeld, kan deze niet meer worden uitgeschakeld.

## Meer handelingen {#more}

In de Schema-editor kunt u ook snel handelingen uitvoeren om de JSON-structuur van het schema te kopiëren of het schema te verwijderen. Selecteren [!UICONTROL More] boven aan de weergave om een vervolgkeuzelijst met snelle acties weer te geven.

![De Schema-editor met de knop Meer gemarkeerd en de vervolgkeuzemogelijkheden weergegeven.](../images/tutorials/create-schema/more-actions.png)

### Schema verwijderen {#delete-a-schema}

>[!CONTEXTUALHELP]
>id="platform_schemas_delete_profileenabledwithdatasets"
>title="Kan schema niet verwijderen"
>abstract="Het schema kan niet worden geschrapt omdat het voor Profiel is toegelaten en bijbehorende datasets heeft."

>[!CONTEXTUALHELP]
>id="platform_schemas_delete_profileenablednodatasets"
>title="Kan schema niet verwijderen"
>abstract="Het schema kan niet worden verwijderd omdat het is ingeschakeld voor Profiel."

>[!CONTEXTUALHELP]
>id="platform_schemas_delete_withdatasetsnotprofileenabled"
>title="Kan schema niet verwijderen"
>abstract="Het schema kan niet worden geschrapt omdat het bijbehorende datasets heeft."

Een schema kan binnen UI van de Redacteur van het Schema worden geschrapt gebruikend [!UICONTROL More] acties en ook van de schemadetails in [!UICONTROL Browse] tab. Er zijn bepaalde voorwaarden die voorkomen dat een schema wordt verwijderd. Een schema kan niet worden verwijderd als:

* Het schema is ingeschakeld voor Profiel.
* Het schema wordt toegelaten voor Profiel en heeft bijbehorende datasets.
* Het schema heeft bijbehorende datasets maar is niet toegelaten voor Profiel.

### JSON-structuur kopiëren {#copy-json-structure}

Selecteren **[!UICONTROL Copy JSON structure]** om een uitvoerlading voor om het even welk schema in de Bibliotheek van het Schema te produceren. Met deze handeling wordt de JSON-structuur naar het klembord gekopieerd. Uw geëxporteerde JSON kan vervolgens worden gebruikt om het schema en eventuele gerelateerde bronnen te importeren in een andere sandbox of organisatie. Dit maakt het delen en hergebruiken van schema&#39;s tussen verschillende milieu&#39;s eenvoudig en efficiënt.

## Volgende stappen en extra bronnen

Nu u klaar bent met het samenstellen van het schema, kunt u het volledige schema in het canvas zien. Selecteren **[!UICONTROL Save]** en het schema wordt opgeslagen in het [!DNL Schema Library], die toegankelijk worden gemaakt door de [!DNL Schema Registry].

Het nieuwe schema kan nu worden gebruikt om gegevens in te voeren in [!DNL Platform]. Herinner dat zodra het schema is gebruikt om gegevens in te voeren, slechts de additieve veranderingen kunnen worden aangebracht. Zie de [grondbeginselen van de schemacompositie](../schema/composition.md) voor meer informatie over schemaversie.

U kunt nu de zelfstudie volgen op [het bepalen van een schemaverhouding in UI](./relationship-ui.md) om een nieuw relatieveld aan het schema van &quot;Loyalty Leden&quot;toe te voegen.

Het schema &quot;Leden van de Loyalty&quot;is ook beschikbaar om te bekijken en te leiden gebruikend [!DNL Schema Registry] API. Als u met de API wilt gaan werken, begint u met het lezen van de [[!DNL Schema Registry API] ontwikkelaarsgids](../api/getting-started.md).

### Videobronnen

>[!WARNING]
>
>De [!DNL Platform] De interface die in de volgende video&#39;s wordt weergegeven, is verouderd. Raadpleeg de bovenstaande documentatie voor de meest recente schermafbeeldingen en functionaliteit van de gebruikersinterface.

In de volgende video ziet u hoe u een eenvoudig schema kunt maken in het dialoogvenster [!DNL Platform] UI.

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

De volgende video is bedoeld om u meer inzicht te geven in het werken met veldgroepen en klassen.

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## Bijlage

De volgende secties bevatten aanvullende informatie over het gebruik van de [!DNL Schema Editor].

### Een nieuwe klasse maken {#create-new-class}

[!DNL Experience Platform] biedt de flexibiliteit om een schema te definiëren dat is gebaseerd op een klasse die uniek is voor uw organisatie. Zie de handleiding voor meer informatie over het maken van een nieuwe klasse [klassen maken en bewerken in de gebruikersinterface](../ui/resources/classes.md#create).

### De klasse van een schema wijzigen {#change-class}

U kunt de klasse van een schema op om het even welk punt tijdens het aanvankelijke samenstellingsproces veranderen alvorens het schema is bewaard.

>[!WARNING]
>
>Het opnieuw toewijzen van de klasse voor een schema zou met uiterste voorzichtigheid moeten worden gedaan. Veldgroepen zijn alleen compatibel met bepaalde klassen. Als u de klasse wijzigt, worden het canvas en alle velden die u hebt toegevoegd opnieuw ingesteld.

Zie de handleiding voor informatie over het wijzigen van de klasse van een schema [het beheren van schema&#39;s in UI](../ui/resources/schemas.md#change-class).

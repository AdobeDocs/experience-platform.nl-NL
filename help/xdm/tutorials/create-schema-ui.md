---
keywords: Experience Platform;home;popular topics;ui;UI;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema editor;Schema Editor;schema;Schema;schemas;Schemas;create
solution: Experience Platform
title: Een schema maken met de Schema-editor
topic: tutorial
type: Tutorial
description: Deze zelfstudie behandelt de stappen voor het maken van een schema met de Schema-editor in het Experience Platform.
translation-type: tm+mt
source-git-commit: 26c3aa3b21c2d9850f29816d57ddf2da953d6b10
workflow-type: tm+mt
source-wordcount: '3779'
ht-degree: 0%

---


# Een schema maken met de opdracht [!DNL Schema Editor]

Met de Adobe Experience Platform-gebruikersinterface kunt u [!DNL Experience Data Model] (XDM)-schema&#39;s maken en beheren in een interactief visueel canvas dat de [!DNL Schema Editor]naam draagt. In deze zelfstudie wordt uitgelegd hoe u een schema maakt met behulp van het [!DNL Schema Editor]deelvenster.

>[!NOTE]
>
>Voor demonstratiedoeleinden, impliceren de stappen in dit leerprogramma het creëren van een voorbeeldschema dat leden van een programma van de klantenloyaliteit beschrijft. Terwijl u deze stappen kunt gebruiken om een verschillend schema voor uw eigen doeleinden tot stand te brengen, adviseert men dat u eerst samen met het creëren van het voorbeeldschema volgt om de mogelijkheden van [!DNL Schema Editor]te leren.

Als u liever een schema samenstelt met de [!DNL Schema Registry] API, begint u met het lezen van de [[!DNL Schema Registry] ontwikkelaarsgids](../api/getting-started.md) voordat u de zelfstudie over het [maken van een schema met de API](create-schema-api.md)gebruikt.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de verschillende aspecten van Adobe Experience Platform die bij het maken van schema&#39;s betrokken zijn. Lees vóór het starten van deze zelfstudie de documentatie voor de volgende concepten:

* [[!DNL Experience Data Model (XDM)]](../home.md): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Platform] georganiseerd.
   * [Basisbeginselen van de schemacompositie](../schema/composition.md): Een overzicht van schema&#39;s XDM en hun bouwstenen, met inbegrip van klassen, mengen, gegevenstypes, en gebieden.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

## De werkruimte [!UICONTROL Schema] openen {#browse}

De [!UICONTROL werkruimte van Schema] in [!DNL Platform] UI verstrekt een visualisatie van [!DNL Schema Library], toestaand u om de schema&#39;s te bekijken beschikbaar voor uw organisatie. De werkruimte bevat ook het [!DNL Schema Editor]canvas waarop u in deze zelfstudie een schema kunt samenstellen.

Nadat u zich hebt aangemeld [!DNL Experience Platform], selecteert u **[!UICONTROL Schema]** in de linkernavigatie om de werkruimte **[!UICONTROL Schema]** te openen. Op het tabblad **[!UICONTROL Bladeren]** wordt een lijst weergegeven met schema&#39;s (een weergave van de schema&#39;s [!DNL Schema Library]) die u kunt weergeven en aanpassen. De lijst bevat de naam, het type, de klasse en het gedrag (record of tijdreeks) waarop het schema is gebaseerd, evenals de datum en tijd waarop het schema voor het laatst is gewijzigd.

Zie de handleiding over het [verkennen van bestaande XDM-bronnen in de gebruikersinterface](./explore.md) voor meer informatie.

## Een schema maken en een naam geven {#create}

Als u wilt beginnen met het samenstellen van een schema, selecteert u Schema **[!UICONTROL maken in de rechterbovenhoek van de]** werkruimte Schema **** . Er wordt een vervolgkeuzemenu weergegeven met de optie die u kunt kiezen tussen de kernklassen [!UICONTROL XDM Individual Profile] en [!UICONTROL XDM ExperienceEvent]. Als deze klassen niet geschikt zijn voor uw doeleinden, kunt u ook **[!UICONTROL Bladeren]** selecteren om te kiezen uit andere beschikbare klassen of een nieuwe klasse [](#create-new-class)maken.

Voor deze zelfstudie selecteert u Afzonderlijk **[!UICONTROL XDM-profiel]**.

![](../images/tutorials/create-schema/create_schema_button.png)

De [!DNL Schema Editor] knop verschijnt. Dit is het canvas waarop u het schema wilt samenstellen. Aangezien u een standaardXDM klasse koos om het schema te baseren op, wordt een naamloos schema automatisch gecreeerd in de sectie van de **[!UICONTROL Structuur]** van het canvas wanneer u in de redacteur aankomt, samen met de standaardgebieden inbegrepen in alle schema&#39;s die op die klasse worden gebaseerd. De toegewezen klasse voor het schema wordt ook vermeld onder **[!UICONTROL Klasse]** in de sectie van de **[!UICONTROL Samenstelling]** .

![](../images/tutorials/create-schema/schema_editor.png)

>[!NOTE]
>
>U kunt de klasse van een schema [op om het even welk punt tijdens het aanvankelijke samenstellingsproces](#change-class) veranderen alvorens het schema is bewaard, maar dit zou met uiterste voorzichtigheid moeten worden gedaan. Mixins zijn alleen compatibel met bepaalde klassen en als u de klasse wijzigt, worden het canvas en alle toegevoegde velden opnieuw ingesteld.

Gebruik de velden aan de rechterkant van de editor om een weergavenaam en een optionele beschrijving voor het schema op te geven. Nadat u een naam hebt ingevoerd, wordt het canvas bijgewerkt met de nieuwe naam van het schema.

![](../images/tutorials/create-schema/name_schema.png)

Er zijn verscheidene belangrijke overwegingen om te maken wanneer het beslissen over een naam voor uw schema:

* De namen van het schema zouden kort en beschrijvend moeten zijn zodat het schema later gemakkelijk kan worden gevonden.
* Schemenamen moeten uniek zijn, wat betekent dat ze ook specifiek genoeg moeten zijn om in de toekomst niet opnieuw te worden gebruikt. Bijvoorbeeld, als uw organisatie afzonderlijke loyaliteitsprogramma&#39;s voor verschillende merken had, zou het verstandig zijn om uw schema &quot;Merk A Loyalty Leden&quot;te noemen om het gemakkelijk te maken om van andere loyaliteits-verwante regelingen onderscheid te maken u zou kunnen later bepalen.
* U kunt de schemabeschrijving ook gebruiken om het even welke extra contextafhankelijke informatie betreffende het schema te verstrekken.

Deze zelfstudie stelt een schema samen om gegevens met betrekking tot de leden van een loyaliteitsprogramma in te voeren, en daarom wordt het schema genoemd &quot;Loyalty Leden&quot;.

## Een mix toevoegen {#mixin}

U kunt nu velden toevoegen aan uw schema door mixen toe te voegen. Een mix is een groep van één of meerdere gebieden die vaak samen worden gebruikt om een bepaald concept te beschrijven. Deze zelfstudie gebruikt mixins om de leden van het loyaliteitsprogramma te beschrijven en zeer belangrijke informatie zoals naam, verjaardag, telefoonaantal, adres, en meer te vangen.

Als u een mix wilt toevoegen, selecteert u **[!UICONTROL Toevoegen]** in de subsectie **[!UICONTROL Mixins]** .

![](../images/tutorials/create-schema/add_mixin_button.png)

Er wordt een nieuw dialoogvenster weergegeven met een lijst met beschikbare mixen. Elke mix is alleen bedoeld voor gebruik met een specifieke klasse. Daarom worden in het dialoogvenster alleen mengen weergegeven die compatibel zijn met de geselecteerde klasse (in dit geval de [!DNL XDM Individual Profile] klasse). Als u een standaard XDM-klasse gebruikt, wordt de lijst met mixen op intelligente wijze gesorteerd op basis van de populariteit van het gebruik.

![](../images/tutorials/create-schema/mixin-popularity.png)

Als u een mix in de lijst selecteert, wordt deze weergegeven in de rechterspoorstaaf. U kunt desgewenst meerdere mixen selecteren en vervolgens de mixen toevoegen aan de lijst in de rechterrail voordat u de mixer bevestigt. Bovendien verschijnt er een pictogram aan de rechterkant van de geselecteerde mix, zodat u een voorbeeld kunt bekijken van de structuur van de velden die worden weergegeven.

![](../images/tutorials/create-schema/preview-mixin-button.png)

Als u een voorbeeld van een mix bekijkt, wordt een gedetailleerde beschrijving van het schema van de mix gegeven in de rechterspoorstaaf. U kunt ook door de velden van de mix navigeren op het beschikbare canvas. Als u verschillende velden selecteert, wordt het rechterspoor bijgewerkt om details over het betreffende veld weer te geven. Selecteer **[!UICONTROL Terug]** wanneer u klaar bent met de voorvertoning om terug te keren naar het dialoogvenster voor gemengde selectie.

![](../images/tutorials/create-schema/preview-mixin.png)

Voor deze zelfstudie selecteert u de **[!UICONTROL mix Demografische details]** en selecteert u vervolgens **[!UICONTROL Mengsel]** toevoegen.

![](../images/tutorials/create-schema/add_mixin_person_details.png)

Het schemacanvas verschijnt opnieuw. De sectie **[!UICONTROL Mixins]** bevat nu de sectie[!UICONTROL Demografische details]en de sectie **[!UICONTROL Structuur]** bevat de velden die door de mix worden toegevoegd. U kunt de naam van de mix selecteren onder de sectie **[!UICONTROL Mixins]** om de specifieke velden te markeren die worden weergegeven op het canvas.

![](../images/tutorials/create-schema/person_details_structure.png)

Deze mix levert verschillende velden onder de naam op hoofdniveau bij `person` het gegevenstype &quot;[!UICONTROL Persoon]&quot;. In deze groep velden wordt informatie over een individu beschreven, zoals naam, geboortedatum en geslacht.

>[!NOTE]
>
>Onthoud dat in velden scalaire typen kunnen worden gebruikt (zoals een tekenreeks, geheel getal, array of datum) en ook elk gegevenstype (een groep velden die een algemeen concept vertegenwoordigen) dat in de [!DNL Schema Registry]code is gedefinieerd.

Het `name` veld heeft een gegevenstype &quot;[!UICONTROL Persoon name]&quot;, wat betekent dat het ook een algemeen concept beschrijft en naamgerelateerde subvelden bevat, zoals voornaam, achternaam, hoffelijkheidstitel en achtervoegsel.

Selecteer de verschillende velden op het canvas om extra velden weer te geven die worden toegevoegd aan de schemastructuur.

## Een andere mix toevoegen {#mixin-2}

U kunt nu dezelfde stappen herhalen om een andere mix toe te voegen. Wanneer u dit keer het dialoogvenster **[!UICONTROL Toevoegen]** bekijkt, ziet u dat de mix &quot;[!UICONTROL Demografische details]&quot; grijs is weergegeven en dat het selectievakje ernaast niet kan worden ingeschakeld. Zo voorkomt u dat u per ongeluk combinaties dupliceert die u al in het huidige schema hebt opgenomen.

Voor deze zelfstudie selecteert u de &#39;[!DNL Personal Contact Details]&#39; mix in het dialoogvenster en selecteert u vervolgens **[!UICONTROL Toevoegen, mixen]** om deze aan het schema toe te voegen.

![](../images/tutorials/create-schema/add_mixin_personal_details.png)

Nadat u het canvas hebt toegevoegd, verschijnt het weer. De &quot;[!UICONTROL Persoonlijke Details]van het Contact&quot;is nu vermeld onder **[!UICONTROL Mixins]** in de sectie van de **[!UICONTROL Samenstelling]** , en gebieden voor huisadres, mobiele telefoon, en meer zijn toegevoegd onder **[!UICONTROL Structuur]**.

Net als in het `name` veld vertegenwoordigen de velden die u zojuist hebt toegevoegd concepten met meerdere velden. Bijvoorbeeld, heeft `homeAddress` een gegevenstype van &quot;[!UICONTROL Postadres]&quot;en `mobilePhone` heeft een gegevenstype van &quot;[!UICONTROL telefoonaantal]&quot;. U kunt elk van deze velden selecteren om deze uit te vouwen en de extra velden in het gegevenstype bekijken.

![](../images/tutorials/create-schema/personal_details_structure.png)

## Een nieuwe mix definiëren {#define-mixin}

Het schema &quot;[!UICONTROL Loyalty-leden]&quot; is bedoeld voor het vastleggen van gegevens die betrekking hebben op de leden van een loyaliteitsprogramma, zodat het een aantal specifieke velden met betrekking tot loyaliteit vereist. Er zijn geen standaardmengingen beschikbaar die de noodzakelijke gebieden bevatten, daarom zult u een nieuwe mix moeten bepalen.

Wanneer u dit keer het dialoogvenster **[!UICONTROL Mixin]** toevoegen opent, selecteert u Nieuwe **[!UICONTROL mixer]** maken. Vervolgens wordt u gevraagd een weergavenaam en een beschrijving voor de mix op te geven.

![](../images/tutorials/create-schema/mixin_create_new.png)

Net als bij klassennamen moet de mixinnaam kort en eenvoudig zijn en beschrijven wat de mix aan het schema zal bijdragen. Ook deze zijn uniek, dus u kunt de naam niet opnieuw gebruiken en moet er dus voor zorgen dat deze voldoende specifiek is.

Geef voor deze zelfstudie de nieuwe mix de naam &quot;Loyalty Details&quot;.

Selecteer Mengsel **[!UICONTROL toevoegen]** om terug te keren naar de [!DNL Schema Editor]. &quot;[!UICONTROL Loyalty Details]&quot; moeten nu worden weergegeven onder **[!UICONTROL Mixins]** aan de linkerkant van het canvas, maar er zijn nog geen velden aan gekoppeld en daarom verschijnen er geen nieuwe velden onder **[!UICONTROL Structuur]**.

## Velden toevoegen aan de mix {#mixin-fields}

Nu u de mix &quot;Loyalty Details&quot;hebt gecreeerd, is het tijd om de gebieden te bepalen die de mixin aan het schema zal bijdragen.

Selecteer eerst de naam van de mix in de sectie **[!UICONTROL Mixins]** . Zodra u dit doet, verschijnen de eigenschappen van de mixin op de rechterkant van de redacteur en een **plusteken (+)** verschijnt naast de naam van het schema onder **[!UICONTROL Structuur]**.

![](../images/tutorials/create-schema/loyalty_details_structure.png)

Selecteer de **plusknop (+)** naast &quot;[!DNL Loyalty Members]&quot; om een nieuw knooppunt in de structuur te maken. Dit knooppunt (in dit voorbeeld aangeroepen) vertegenwoordigt de huurder-id van uw IMS-organisatie, voorafgegaan door een onderstrepingsteken. `_tenantId` De aanwezigheid van huurder identiteitskaart wijst erop dat de gebieden u toevoegt in namespace van uw organisatie bevat zijn.

Met andere woorden, de velden die u toevoegt, zijn uniek voor uw organisatie en worden opgeslagen in een specifiek gebied dat alleen voor uw organisatie toegankelijk is. [!DNL Schema Registry] De gebieden u bepaalt moeten altijd aan uw huurdersnamespace worden toegevoegd om botsingen met namen van andere standaardklassen, mixins, gegevenstypes, en gebieden te verhinderen.

In dat knooppunt met naamruimte bevindt zich een &quot;[!UICONTROL Nieuw veld]&quot;. Dit is het begin van de mix &quot;[!UICONTROL Loyalty Details]&quot;.

![](../images/tutorials/create-schema/new_field_loyalty.png)

Gebruikend de controles op de rechterkant van de redacteur, begin door een `loyalty` gebied met type &quot;[!UICONTROL Voorwerp]&quot;te creëren dat zal worden gebruikt om uw loyaliteits-verwante gebieden te houden. Als u klaar bent, selecteert u **[!UICONTROL Toepassen]**.

![](../images/tutorials/create-schema/loyalty_object.png)

De wijzigingen worden toegepast en het nieuwe `loyalty` object wordt weergegeven. Selecteer de **plusknop (+)** naast het object om extra velden toe te voegen die betrekking hebben op loyaliteit. Er wordt een &#39;&#39;[!UICONTROL Nieuw veld]&#39;&#39; weergegeven en de sectie met **[!UICONTROL veldeigenschappen]** is zichtbaar aan de rechterkant van het canvas.

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

Voor elk veld is de volgende informatie vereist:

* **[!UICONTROL Veldnaam]:** De naam van het veld, geschreven in camelcase. Voorbeeld: loyaltyLevel
* **[!UICONTROL Weergavenaam]:** De naam van het veld, geschreven in hoofdletters/kleine letters. Voorbeeld: Loyaliteitsniveau
* **[!UICONTROL Type]:** Het gegevenstype van het veld. Dit omvat fundamentele scalaire types en om het even welke die gegevenstypes in [!DNL Schema Registry]worden bepaald. Voorbeelden: [!UICONTROL Tekenreeks], [!UICONTROL Geheel getal], [!UICONTROL Boolean], [!UICONTROL Persoon], [!UICONTROL Adres], Telefoonnummer, enz.
* **[!UICONTROL Omschrijving]:** Er moet een optionele beschrijving van het veld worden opgenomen, geschreven in een zin met maximaal 200 tekens.

Het eerste veld voor het `Loyalty` object is een tekenreeks met de naam `loyaltyId`. Wanneer u het type van het nieuwe veld instelt op &quot;[!UICONTROL String]&quot;, wordt de sectie met **[!UICONTROL veldeigenschappen]** gevuld met verschillende opties voor het toepassen van beperkingen, zoals standaardwaarde, opmaak en maximumlengte.

![](../images/tutorials/create-schema/string_constraints.png)

Welke beperkingsopties beschikbaar zijn, is afhankelijk van het geselecteerde gegevenstype. Aangezien dit een e-mailadres `loyaltyId` wordt, selecteert u &quot;[!UICONTROL e-mail]&quot; in het vervolgkeuzemenu **[!UICONTROL Indeling]** . Selecteer **[!UICONTROL Toepassen]** om uw wijzigingen toe te passen.

![](../images/tutorials/create-schema/loyaltyId_field.png)

## Meer velden toevoegen aan de mix {#mixin-fields-2}

Nu u het `loyaltyId` veld hebt toegevoegd, kunt u aanvullende velden toevoegen om informatie over loyaliteit vast te leggen, zoals:

* Punten (geheel getal)
* Sinds lid (datum)

Als u elk veld aan het schema wilt toevoegen, selecteert u de **plusknop (+)** naast het `loyalty` object en vult u de vereiste gegevens in.

Wanneer voltooid, zal het voorwerp van de Loyalty gebieden voor loyauiteits identiteitskaart, punten, en lid-sinds bevatten.

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## Een opsommingsveld toevoegen aan de mix {#enum}

Wanneer u velden in het veld definieert, [!DNL Schema Editor]zijn er enkele aanvullende opties die u kunt toepassen op standaardveldtypen om de gegevens in het veld verder te beperken. De gebruiksgevallen voor deze beperkingen worden in de volgende tabel uitgelegd:

| Restrictie | Beschrijving |
| --- | --- |
| [!UICONTROL Vereist] | Geeft aan dat het veld verplicht is voor gegevensinvoer. Om het even welke gegevens die aan een dataset worden geupload die op dit schema wordt gebaseerd dat dit gebied niet bevat zullen op opname ontbreken. |
| [!UICONTROL Array] | Geeft aan dat het veld een array van waarden bevat, elk met het opgegeven gegevenstype. Als u deze beperking bijvoorbeeld gebruikt voor een veld met het gegevenstype &quot;[!UICONTROL String]&quot;, geeft u op dat het veld een array van tekenreeksen zal bevatten. |
| [!UICONTROL Enum] | Geeft aan dat dit veld een van de waarden uit een opsommingslijst met mogelijke waarden moet bevatten. |
| [!UICONTROL Identiteit] | Geeft aan dat dit veld een identiteitsveld is. Meer informatie over identiteitsvelden vindt u [later in deze zelfstudie](#identity-field). |
| [!UICONTROL Relatie] | Terwijl de schemaverhoudingen door het gebruik van het unieschema kunnen worden afgeleid en [!DNL Real-time Customer Profile], is dit slechts op schema&#39;s van toepassing die de zelfde klasse delen. De beperking [!UICONTROL Relatie] geeft aan dat dit veld verwijst naar de primaire identiteit van een schema op basis van een andere klasse, wat een relatie tussen de twee schema&#39;s impliceert. Zie de zelfstudie over het [definiëren van een relatie](./relationship-ui.md) voor meer informatie. |

Voor dit leerprogramma, vereist het [!DNL "loyalty"] voorwerp in het schema een nieuw enum gebied dat het &quot;loyaliteitsniveau&quot;van een klant beschrijft, waar de waarde slechts één van vier mogelijke opties kan zijn. Als u dit veld aan het schema wilt toevoegen, selecteert u de **plusknop (+)** naast het `loyalty` object en vult u de vereiste velden in voor **[!UICONTROL veldnaam]** en **[!UICONTROL weergavenaam]**. Selecteer bij **[!UICONTROL Type]**&quot;[!UICONTROL String]&quot;.

![](../images/tutorials/create-schema/loyalty-level-type.png)

Er verschijnen extra selectievakjes voor het veld nadat het type is geselecteerd, waaronder selectievakjes voor **[!UICONTROL Array]**, **[!UICONTROL Enum]** en **[!UICONTROL Identity]**.

Schakel het selectievakje **[!UICONTROL Enum]** in om de sectie **[!UICONTROL Enum values]** hieronder te openen. Hier kunt u de **[!UICONTROL Waarde]** (in camelCase) en het **[!UICONTROL Etiket]** (een facultatieve, reader-vriendelijke naam in het Geval van de Titel) voor elk aanvaardbaar loyaliteitsniveau invoeren.

Als u alle veldeigenschappen hebt voltooid, selecteert u **[!UICONTROL Toepassen]** om het veld &quot;[!DNL loyaltyLevel]&quot; aan het `loyalty` object toe te voegen.

![](../images/tutorials/create-schema/loyalty_level_enum.png)

## Een object met meerdere velden omzetten in een gegevenstype {#datatype}

Het `loyalty` object bevat nu verschillende loyaliteitsspecifieke velden en vertegenwoordigt een algemene gegevensstructuur die nuttig kan zijn in andere schema&#39;s. Met de optie [!DNL Schema Editor] kunt u gemakkelijk herbruikbare objecten met meerdere velden toepassen door de structuur van die objecten om te zetten in gegevenstypen.

De types van gegevens staan voor het verenigbare gebruik van multi-gebiedsstructuren toe en verstrekken meer flexibiliteit dan een mengeling omdat zij overal binnen een schema kunnen worden gebruikt. Dit wordt gedaan door de waarde van het **[!UICONTROL Type]** van het gebied aan dat van om het even welk die gegevenstype te plaatsen in [!DNL Schema Registry].

Als u het `loyalty` object wilt omzetten in een gegevenstype, selecteert u het `loyalty` veld onder **[!UICONTROL Structuur]** en selecteert u vervolgens **[!UICONTROL Omzetten in nieuw gegevenstype]** aan de rechterkant van de editor onder **[!UICONTROL Veldeigenschappen]**. Er verschijnt een groene popover om te bevestigen dat het object is geconverteerd.

![](../images/tutorials/create-schema/convert-data-type.png)

Als u nu onder **[!UICONTROL Structuur]** kijkt, ziet u dat het `loyalty` veld een gegevenstype &quot;[!DNL Loyalty]&quot; heeft en dat de velden kleine vergrendelingspictogrammen ernaast hebben, wat aangeeft dat het niet langer afzonderlijke velden zijn, maar deel uitmaken van een gegevenstype met meerdere velden.

![](../images/tutorials/create-schema/loyalty_data_type.png)

In een toekomstig schema, kon u een gebied nu toewijzen als &quot;[!DNL Loyalty]&quot;type en het zou automatisch gebieden voor identiteitskaart, loyaliteitsniveau, lid sinds, en punten omvatten.

>[!NOTE]
>
>U kunt ook aangepaste gegevenstypen maken en bewerken, onafhankelijk van het bewerken van schema&#39;s. Zie de zelfstudie over het [maken en bewerken van gegevenstypen](./create-data-type.md) voor meer informatie.

## Schema-velden zoeken en filteren

Het schema bevat nu verschillende combinaties naast de velden die door de basisklasse worden verschaft. Wanneer u met grotere schema&#39;s werkt, kunt u de selectievakjes naast mixinnamen in de linkerrails selecteren om de weergegeven velden te filteren op de velden die alleen worden weergegeven door de mixins waarin u geïnteresseerd bent.

![](../images/tutorials/create-schema/filter-by-mixin.png)

Als u naar een specifiek veld in uw schema zoekt, kunt u ook de zoekbalk gebruiken om weergegeven velden op naam te filteren, ongeacht onder welke combinatie deze velden staan.

![](../images/tutorials/create-schema/search.png)

>[!IMPORTANT]
>
>Bij de weergave van overeenkomende velden houdt de zoekfunctie rekening met eventuele geselecteerde mixfilters. Als een onderzoeksvraag niet de resultaten toont u verwacht, kunt u moeten tweemaal controleren dat u geen relevante mengen filtreert.

## Een schemaveld instellen als een identiteitsveld {#identity-field}

De standaard gegevensstructuur die schema&#39;s verstrekken kan worden gebruikt om gegevens te identificeren die tot het zelfde individu over veelvoudige bronnen behoren, die voor diverse stroomafwaartse gebruiksgevallen zoals segmentatie, rapportering, gegevenswetenschapsanalyse, en meer toestaan. Om gegevens op basis van individuele identiteiten te koppelen, moeten de sleutelvelden worden gemarkeerd als [!UICONTROL identiteitsvelden] binnen de toepasselijke schema&#39;s.

[!DNL Experience Platform] maakt het gemakkelijk om een identiteitsgebied door het gebruik van een checkbox van de **[!UICONTROL Identiteit]** in te duiden [!DNL Schema Editor]. U moet echter bepalen welk veld de beste kandidaat is om als identiteit te gebruiken, op basis van de aard van uw gegevens.

Er kunnen bijvoorbeeld duizenden leden van het loyaliteitsprogramma zijn die tot hetzelfde &quot;loyaliteitsniveau&quot; behoren, maar elk lid van het loyaliteitsprogramma heeft een unieke naam `loyaltyId` (wat in dit geval het e-mailadres van het individuele lid is). Het feit dat dit voor elk lid een unieke identificatiecode `loyaltyId` is, maakt het een goede kandidaat voor een identiteitsveld, terwijl dat `loyaltyLevel` niet zo is.

>[!IMPORTANT]
>
>De stappen hieronder beschrijven hoe te om een identiteitsbeschrijver aan een bestaand schemagebied toe te voegen. Als alternatief voor het definiëren van identiteitsvelden binnen de structuur van het schema zelf, kunt u in plaats daarvan ook een `identityMap` veld gebruiken voor het bevatten van identiteitsgegevens.
>
>Als u van plan bent om te gebruiken `identityMap`, houd in mening dat het om het even welke primaire identiteit zal met voeten treden u direct aan het schema toevoegt. Zie de sectie op `identityMap` in de [grondbeginselen van de gids](../schema/composition.md#identityMap) van de schemacompositie voor meer informatie.

Selecteer in het gedeelte **[!UICONTROL Structuur]** van de editor het `loyaltyId` veld en schakel het selectievakje **[!UICONTROL Identiteit]** in onder **[!UICONTROL Veldeigenschappen]**. Schakel het selectievakje in en kies de optie om dit in te stellen als de **[!UICONTROL primaire identiteit]** wordt weergegeven. Selecteer dit vak ook.

>[!NOTE]
>
>Elk schema mag slechts één primair identiteitsveld bevatten. Zodra een schemagebied als primaire identiteit is geplaatst, zult u een foutenmelding ontvangen als u later probeert om een ander identiteitsgebied in het schema als primaire identiteit te plaatsen.

Vervolgens moet u een naamruimte **** Identiteit opgeven in de lijst met vooraf gedefinieerde naamruimten in het vervolgkeuzemenu. Aangezien dit het e-mailadres van de klant `loyaltyId` is, selecteert u &quot;[!UICONTROL E-mail]&quot; in het vervolgkeuzemenu. Selecteer **[!UICONTROL Toepassen]** om de updates voor het `loyaltyId` veld te bevestigen.

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>Raadpleeg de [[!DNL Identity Service] documentatie](../../identity-service/troubleshooting-guide.md#standard-namespaces)voor een lijst met standaardnaamruimten en de bijbehorende definities.

Nadat u de wijziging hebt toegepast, wordt op het pictogram voor `loyaltyId` een vingerafdruksymbool een identiteitsveld weergegeven.

![](../images/tutorials/create-schema/identity-applied.png)

Alle gegevens die in het `loyaltyId` veld worden ingevoerd, worden nu gebruikt om die persoon te identificeren en één weergave van die klant samen te voegen. Raadpleeg de [!DNL Experience Platform]documentatie voor meer informatie over het werken met identiteiten in [[!DNL Identity Service]](../../identity-service/home.md) .

## Het schema inschakelen voor gebruik in [!DNL Real-time Customer Profile] {#profile}

[[!DNL Real-time Customer Profile]](../../profile/home.md) Gebruikt identiteitsgegevens in [!DNL Experience Platform] om een holistische mening van elke individuele klant te verstrekken. De service bouwt robuuste, 360°-profielen van klantkenmerken en accounts met tijdstempels van elke interactie die klanten hebben gehad in elk systeem dat is geïntegreerd met [!DNL Experience Platform].

Als u wilt dat een schema kan worden gebruikt met, moet er een primaire identiteit zijn gedefinieerd. [!DNL Real-time Customer Profile] Er wordt een foutbericht weergegeven als u een schema wilt inschakelen zonder eerst een primaire identiteit te definiëren.

<img src="../images/tutorials/create-schema/missing_primary_identity.png" width="600" /><br>

Als u het schema &quot;Loyalty-leden&quot; wilt inschakelen voor gebruik in [!DNL Profile], selecteert u eerst &quot;[!DNL Loyalty Members]&quot; in het gedeelte **[!UICONTROL Structuur]** van de editor.

Aan de rechterkant van de editor wordt informatie over het schema weergegeven, inclusief de weergavenaam, beschrijving en type. Naast deze informatie is er een schakelknop **[!UICONTROL Profiel]** .

![](../images/tutorials/create-schema/profile-toggle.png)

Selecteer **[!UICONTROL Profiel]** en er verschijnt een pop-up met de vraag of u het schema wilt inschakelen voor [!DNL Profile].

<img src="../images/tutorials/create-schema/enable-profile.png" width="700" /><br>

>[!WARNING]
>
>Als een schema is ingeschakeld voor [!DNL Real-time Customer Profile] en opgeslagen, kan het niet worden uitgeschakeld.

Selecteer **[!UICONTROL Inschakelen]** om uw keuze te bevestigen. U kunt desgewenst de **[!UICONTROL profielschakelaar]** opnieuw selecteren om het schema uit te schakelen, maar als het schema is opgeslagen terwijl [!DNL Profile] is ingeschakeld, kan het niet meer worden uitgeschakeld.

## Volgende stappen en extra bronnen

Nu u klaar bent met het samenstellen van het schema, kunt u het volledige schema in het canvas zien. Selecteer **[!UICONTROL Opslaan]** en het schema wordt opgeslagen in de [!DNL Schema Library]toepassing, zodat deze toegankelijk is voor de [!DNL Schema Registry]gebruiker.

Het nieuwe schema kan nu worden gebruikt om gegevens in te voeren [!DNL Platform]. Herinner dat zodra het schema is gebruikt om gegevens in te voeren, slechts de additieve veranderingen kunnen worden aangebracht. Zie de [grondbeginselen van schemacompositie](../schema/composition.md) voor meer informatie over schema versioning.

U kunt nu de zelfstudie volgen over het [definiëren van een schemarelatie in de gebruikersinterface](./relationship-ui.md) om een nieuw relatieveld toe te voegen aan het schema &quot;Loyalty-leden&quot;.

Het schema &quot;Loyalty Member&quot; is ook beschikbaar voor weergave en beheer met behulp van de [!DNL Schema Registry] API. Als u met de API wilt gaan werken, leest u eerst de [[!DNL Schema Registry API] ontwikkelaarsgids](../api/getting-started.md).

### Videobronnen

>[!WARNING]
>
>De [!DNL Platform] UI die in de volgende video&#39;s wordt getoond is verouderd. Raadpleeg de bovenstaande documentatie voor de meest recente schermafbeeldingen en functionaliteit van de gebruikersinterface.

De volgende video laat zien hoe u een eenvoudig schema maakt in de [!DNL Platform] gebruikersinterface.

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

De volgende video is bedoeld om uw inzicht in het werken met mixins en klassen te versterken.

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## Aanhangsel

In de volgende secties vindt u aanvullende informatie over het gebruik van de [!DNL Schema Editor]code.

### Een nieuwe klasse maken {#create-new-class}

[!DNL Experience Platform] biedt de flexibiliteit om een schema te definiëren dat is gebaseerd op een klasse die uniek is voor uw organisatie.

Selecteer in de **[!UICONTROL werkruimte Schema]** de optie **[!UICONTROL Schema]** maken en selecteer vervolgens **[!UICONTROL Bladeren]** in het vervolgkeuzemenu.

![](../images/tutorials/create-schema/browse-classes.png)

Er wordt een dialoogvenster weergegeven waarin u een keuze kunt maken uit een lijst met beschikbare klassen. Selecteer boven aan het dialoogvenster de optie **[!UICONTROL Nieuwe klasse]** maken. U kunt uw nieuwe klasse dan een vertoningsnaam (een korte, beschrijvende, unieke, en gebruikersvriendelijke naam voor de klasse), een beschrijving, en een gedrag (&quot;[!UICONTROL Verslag]&quot;of &quot;Reeks[!UICONTROL van de]Tijd&quot;) voor de gegevens geven het schema zal bepalen.

![](../images/tutorials/create-schema/create_new_class.png)

>[!IMPORTANT]
>
>Wanneer het bouwen van een schema dat een klasse uitvoert die door uw organisatie wordt bepaald, herinner dat de mengen voor gebruik slechts met compatibele klassen beschikbaar zijn. Aangezien de klasse die u hebt gedefinieerd nieuw is, worden er geen compatibele combinaties weergegeven in het dialoogvenster **[!UICONTROL Toevoegen]** . In plaats daarvan moet u Nieuwe mix **** maken selecteren en een mix definiëren voor gebruik met die klasse. De volgende keer dat u een schema samenstelt dat de nieuwe klasse implementeert, wordt de mix die u hebt gedefinieerd vermeld en beschikbaar voor gebruik.

### De klasse van een schema wijzigen {#change-class}

U kunt de klasse van een schema op om het even welk punt tijdens het aanvankelijke samenstellingsproces veranderen alvorens het schema is bewaard.

>[!WARNING]
>
>Het opnieuw toewijzen van de klasse voor een schema zou met uiterste voorzichtigheid moeten worden gedaan. Mixins zijn alleen compatibel met bepaalde klassen en als u de klasse wijzigt, worden het canvas en alle toegevoegde velden opnieuw ingesteld.

Als u een klasse opnieuw wilt toewijzen, selecteert u **[!UICONTROL Toewijzen]** aan de linkerkant van het canvas.

![](../images/tutorials/create-schema/assign_class_button.png)

Er wordt een dialoogvenster weergegeven met een lijst met alle beschikbare klassen, inclusief alle klassen die door uw organisatie zijn gedefinieerd (de eigenaar is &quot;[!UICONTROL Klant]&quot;) en standaardklassen die door Adobe zijn gedefinieerd.

Selecteer een klasse in de lijst om de beschrijving ervan aan de rechterkant van het dialoogvenster weer te geven. U kunt ook de klassenstructuur **** Voorvertoning selecteren om de velden en metagegevens weer te geven die aan de klasse zijn gekoppeld. Selecteer **[!UICONTROL Klasse]** toewijzen om door te gaan.

![](../images/tutorials/create-schema/assign_class.png)

Er wordt een nieuw dialoogvenster geopend waarin u wordt gevraagd te bevestigen dat u een nieuwe klasse wilt toewijzen. Selecteer **[!UICONTROL Toewijzen]** om te bevestigen.

![](../images/tutorials/create-schema/assign-confirm.png)

Nadat de klassewijziging is bevestigd, wordt het canvas opnieuw ingesteld en gaat alle compositievoortgang verloren.
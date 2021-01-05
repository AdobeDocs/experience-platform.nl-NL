---
keywords: Experience Platform;home;popular topics;ui;UI;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema editor;Schema Editor;schema;Schema;schemas;Schemas;create
solution: Experience Platform
title: Een schema maken met de Schema-editor
topic: tutorial
type: Tutorial
description: Deze zelfstudie behandelt de stappen voor het maken van een schema met de Schema-editor in het Experience Platform.
translation-type: tm+mt
source-git-commit: e5c5fea783aa4088d225f771905fa8b2098613cf
workflow-type: tm+mt
source-wordcount: '3568'
ht-degree: 0%

---


# Een schema maken met de [!DNL Schema Editor]

Met de Adobe Experience Platform-gebruikersinterface kunt u [!DNL Experience Data Model] (XDM)-schema&#39;s maken en beheren in een interactief visueel canvas met de naam [!DNL Schema Editor]. In deze zelfstudie wordt uitgelegd hoe u een schema maakt met de [!DNL Schema Editor].

>[!NOTE]
>
>Voor demonstratiedoeleinden, impliceren de stappen in dit leerprogramma het creëren van een voorbeeldschema dat leden van een programma van de klantenloyaliteit beschrijft. Terwijl u deze stappen kunt gebruiken om een verschillend schema voor uw eigen doeleinden tot stand te brengen, adviseert men dat u eerst samen met het creëren van het voorbeeldschema volgt om de mogelijkheden van [!DNL Schema Editor] te leren.

Als u verkiest om een schema samen te stellen gebruikend [!DNL Schema Registry] API in plaats daarvan, begin door [[!DNL Schema Registry] ontwikkelaarsgids](../api/getting-started.md) te lezen alvorens de leerprogramma [het creëren van een schema te proberen gebruikend API](create-schema-api.md).

## Aan de slag

Deze zelfstudie vereist een goed begrip van de verschillende aspecten van Adobe Experience Platform die bij het maken van schema&#39;s betrokken zijn. Lees vóór het starten van deze zelfstudie de documentatie voor de volgende concepten:

* [[!DNL Experience Data Model (XDM)]](../home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Platform] klantenervaring worden georganiseerd.
   * [Basisbeginselen van de schemacompositie](../schema/composition.md): Een overzicht van schema&#39;s XDM en hun bouwstenen, met inbegrip van klassen, mengen, gegevenstypes, en gebieden.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

## De [!UICONTROL Schemas]-werkruimte {#browse} openen

De [!UICONTROL Schemas] werkruimte in [!DNL Platform] UI verstrekt een visualisatie van [!DNL Schema Library], die u toestaat om de schema&#39;s te bekijken beschikbaar voor uw organisatie. De werkruimte omvat ook [!DNL Schema Editor], het canvas waarop u een schema door dit leerprogramma kunt samenstellen.

Nadat u zich hebt aangemeld bij [!DNL Experience Platform], selecteert u **[!UICONTROL Schemas]** in de linkernavigatie om de werkruimte **[!UICONTROL Schemas]** te openen. Het **[!UICONTROL Browse]** lusje toont een lijst van schema&#39;s (een vertegenwoordiging van [!DNL Schema Library]) die u kunt bekijken en aanpassen. De lijst bevat de naam, het type, de klasse en het gedrag (record of tijdreeks) waarop het schema is gebaseerd, evenals de datum en tijd waarop het schema voor het laatst is gewijzigd.

Zie de gids op [het onderzoeken van bestaande middelen XDM in UI](../ui/explore.md) voor meer informatie.

## Een schema maken en een naam geven {#create}

Als u wilt beginnen met het samenstellen van een schema, selecteert u **[!UICONTROL Schema maken]** in de rechterbovenhoek van de werkruimte **[!UICONTROL Schema&#39;s]**. Er wordt een vervolgkeuzemenu weergegeven met de optie om te kiezen tussen de kernklassen [!UICONTROL XDM Individual Profile] en [!UICONTROL XDM ExperienceEvent]. Als deze klassen niet uw doelstellingen aanpassen, kunt u **[!UICONTROL Browse]** ook selecteren om van andere beschikbare klassen te kiezen of [een nieuwe klasse tot stand te brengen](#create-new-class).

Voor deze zelfstudie selecteert u **[!UICONTROL Afzonderlijk XDM-profiel]**.

![](../images/tutorials/create-schema/create_schema_button.png)

De [!DNL Schema Editor] verschijnt. Dit is het canvas waarop u het schema wilt samenstellen. Aangezien u een standaardXDM klasse koos om het schema te baseren op, wordt een naamloos schema automatisch gecreeerd in de **[!UICONTROL sectie van de Structuur]** van het canvas wanneer u in de redacteur, samen met de standaardgebieden inbegrepen in alle schema&#39;s die op die klasse worden gebaseerd. De toegewezen klasse voor het schema wordt ook vermeld onder **[!UICONTROL Klasse]** in **[!UICONTROL Compositie]** sectie.

![](../images/tutorials/create-schema/schema_editor.png)

>[!NOTE]
>
>U kunt [de klasse van een schema ](#change-class) op om het even welk punt tijdens het aanvankelijke samenstellingsproces veranderen alvorens het schema is bewaard, maar dit zou met uiterste voorzichtigheid moeten worden gedaan. Mixins zijn alleen compatibel met bepaalde klassen en als u de klasse wijzigt, worden het canvas en alle toegevoegde velden opnieuw ingesteld.

Gebruik de velden aan de rechterkant van de editor om een weergavenaam en een optionele beschrijving voor het schema op te geven. Nadat u een naam hebt ingevoerd, wordt het canvas bijgewerkt met de nieuwe naam van het schema.

![](../images/tutorials/create-schema/name_schema.png)

Er zijn verscheidene belangrijke overwegingen om te maken wanneer het beslissen over een naam voor uw schema:

* De namen van het schema zouden kort en beschrijvend moeten zijn zodat het schema later gemakkelijk kan worden gevonden.
* Schemenamen moeten uniek zijn, wat betekent dat ze ook specifiek genoeg moeten zijn om in de toekomst niet opnieuw te worden gebruikt. Bijvoorbeeld, als uw organisatie afzonderlijke loyaliteitsprogramma&#39;s voor verschillende merken had, zou het verstandig zijn om uw schema &quot;Merk A Loyalty Leden&quot;te noemen om het gemakkelijk te maken om van andere loyaliteits-verwante regelingen onderscheid te maken u zou kunnen later bepalen.
* U kunt de schemabeschrijving ook gebruiken om het even welke extra contextafhankelijke informatie betreffende het schema te verstrekken.

Deze zelfstudie stelt een schema samen om gegevens met betrekking tot de leden van een loyaliteitsprogramma in te voeren, en daarom wordt het schema genoemd &quot;Loyalty Leden&quot;.

## Een mix toevoegen {#mixin}

U kunt nu velden toevoegen aan uw schema door mixen toe te voegen. Een mix is een groep van één of meerdere gebieden die vaak samen worden gebruikt om een bepaald concept te beschrijven. Deze zelfstudie gebruikt mixins om de leden van het loyaliteitsprogramma te beschrijven en zeer belangrijke informatie zoals naam, verjaardag, telefoonaantal, adres, en meer te vangen.

Als u een mix wilt toevoegen, selecteert u **[!UICONTROL Add]** in de **[!UICONTROL Mixins]**-subsectie.

![](../images/tutorials/create-schema/add_mixin_button.png)

Er wordt een nieuw dialoogvenster weergegeven met een lijst met beschikbare mixen. Elke mix is alleen bedoeld voor gebruik met een specifieke klasse. Daarom worden in het dialoogvenster alleen mengen weergegeven die compatibel zijn met de klasse die u hebt geselecteerd (in dit geval de klasse [!DNL XDM Individual Profile]). Als u een standaard XDM-klasse gebruikt, wordt de lijst met mixen op intelligente wijze gesorteerd op basis van de populariteit van het gebruik.

![](../images/tutorials/create-schema/mixin-popularity.png)

Als u een mix in de lijst selecteert, wordt deze weergegeven in de rechterspoorstaaf. U kunt desgewenst meerdere mixen selecteren en vervolgens de mixen toevoegen aan de lijst in de rechterrail voordat u de mixer bevestigt. Bovendien verschijnt er een pictogram aan de rechterkant van de geselecteerde mix, zodat u een voorbeeld kunt bekijken van de structuur van de velden die worden weergegeven.

![](../images/tutorials/create-schema/preview-mixin-button.png)

Als u een voorbeeld van een mix bekijkt, wordt een gedetailleerde beschrijving van het schema van de mix gegeven in de rechterspoorstaaf. U kunt ook door de velden van de mix navigeren op het beschikbare canvas. Als u verschillende velden selecteert, wordt het rechterspoor bijgewerkt om details over het betreffende veld weer te geven. Selecteer **[!UICONTROL Vorige]** wanneer u klaar bent met voorvertonen om terug te keren naar het dialoogvenster voor gemengde selectie.

![](../images/tutorials/create-schema/preview-mixin.png)

Voor deze zelfstudie selecteert u de **[!UICONTROL Demografische details]** mix en selecteert u **[!UICONTROL Mixin toevoegen]**.

![](../images/tutorials/create-schema/add_mixin_person_details.png)

Het schemacanvas verschijnt opnieuw. De sectie **[!UICONTROL Mixins]** bevat nu &quot;[!UICONTROL Demografische details]&quot; en de sectie **[!UICONTROL Structuur]** bevat de velden die worden toegevoegd door de mix. U kunt de naam van de mix selecteren onder de sectie **[!UICONTROL Mixins]** om de specifieke velden te markeren die worden weergegeven in het canvas.

![](../images/tutorials/create-schema/person_details_structure.png)

Deze mix levert verschillende velden onder de naam `person` op hoofdniveau bij met het gegevenstype &quot;[!UICONTROL Person]&quot;. In deze groep velden wordt informatie over een individu beschreven, zoals naam, geboortedatum en geslacht.

>[!NOTE]
>
>Onthoud dat velden scalaire typen kunnen gebruiken (zoals een tekenreeks, geheel getal, array of datum), evenals elk gegevenstype (een groep velden die een algemeen concept vertegenwoordigen) dat is gedefinieerd in [!DNL Schema Registry].

Het veld `name` heeft het gegevenstype &quot;[!UICONTROL Perdennaam]&quot;, wat betekent dat het ook een algemeen concept beschrijft en aan naam gerelateerde subvelden bevat zoals voornaam, achternaam, hoffelijkheidstitel en achtervoegsel.

Selecteer de verschillende velden op het canvas om extra velden weer te geven die worden toegevoegd aan de schemastructuur.

## Een andere mix toevoegen {#mixin-2}

U kunt nu dezelfde stappen herhalen om een andere mix toe te voegen. Wanneer u het **[!UICONTROL Add mixin]** dialoogvenster dit keer bekijkt, ziet u dat de &quot;[!UICONTROL Demographic Details]&quot;-mix grijs is weergegeven en dat het selectievakje naast deze mix niet kan worden geselecteerd. Zo voorkomt u dat u per ongeluk combinaties dupliceert die u al in het huidige schema hebt opgenomen.

Voor deze zelfstudie selecteert u de &quot;[!DNL Personal Contact Details]&quot; mix in het dialoogvenster en selecteert u **[!UICONTROL mixin]** toevoegen om deze aan het schema toe te voegen.

![](../images/tutorials/create-schema/add_mixin_personal_details.png)

Nadat u het canvas hebt toegevoegd, verschijnt het weer. &quot;[!UICONTROL Persoonlijke contactgegevens]&quot; wordt nu vermeld onder **[!UICONTROL Mixins]** in de sectie **[!UICONTROL Compositie]** en velden voor thuisadres, mobiele telefoon en meer zijn toegevoegd onder **[!UICONTROL Structuur]**.

Net als in het veld `name` vertegenwoordigen de velden die u zojuist hebt toegevoegd concepten met meerdere velden. `homeAddress` heeft bijvoorbeeld een gegevenstype &quot;[!UICONTROL Postal address]&quot; en `mobilePhone` heeft een gegevenstype &quot;[!UICONTROL Telefoonnummer]&quot;. U kunt elk van deze velden selecteren om deze uit te vouwen en de extra velden in het gegevenstype bekijken.

![](../images/tutorials/create-schema/personal_details_structure.png)

## Een nieuwe mix definiëren {#define-mixin}

Het schema &quot;[!UICONTROL Loyalty Leden]&quot;is bedoeld om gegevens met betrekking tot de leden van een loyaliteitsprogramma te vangen, zodat zal het sommige specifieke op loyaliteit betrekking hebbende gebieden vereisen. Er zijn geen standaardmengingen beschikbaar die de noodzakelijke gebieden bevatten, daarom zult u een nieuwe mix moeten bepalen.

Dit keer, wanneer u **[!UICONTROL Add Mixin]** dialoog opent, selecteer **[!UICONTROL Create Nieuwe Mixin]**. Vervolgens wordt u gevraagd een weergavenaam en een beschrijving voor de mix op te geven.

![](../images/tutorials/create-schema/mixin_create_new.png)

Net als bij klassennamen moet de mixinnaam kort en eenvoudig zijn en beschrijven wat de mix aan het schema zal bijdragen. Ook deze zijn uniek, dus u kunt de naam niet opnieuw gebruiken en moet er dus voor zorgen dat deze voldoende specifiek is.

Geef voor deze zelfstudie de nieuwe mix de naam &quot;Loyalty Details&quot;.

Selecteer **[!UICONTROL Add mixin]** om aan [!DNL Schema Editor] terug te keren. &quot;[!UICONTROL Loyalty Details]&quot; moeten nu onder **[!UICONTROL Mixins]** aan de linkerkant van het canvas worden weergegeven, maar er zijn nog geen velden aan gekoppeld en er worden daarom geen nieuwe velden onder **[!UICONTROL Structuur]** weergegeven.

## Velden toevoegen aan de mix {#mixin-fields}

Nu u de mix &quot;Loyalty Details&quot;hebt gecreeerd, is het tijd om de gebieden te bepalen die de mixin aan het schema zal bijdragen.

Selecteer eerst de mixnaam in de sectie **[!UICONTROL Mixins]**. Zodra u dit doet, verschijnen de eigenschappen van de mixin op de rechterkant van de redacteur en **plus (+)** verschijnt naast de naam van het schema onder **[!UICONTROL Structuur]**.

![](../images/tutorials/create-schema/loyalty_details_structure.png)

Selecteer **plus (+)** pictogram naast &quot;[!DNL Loyalty Members]&quot;om een nieuwe knoop in de structuur tot stand te brengen. Dit knooppunt (in dit voorbeeld `_tenantId` genoemd) vertegenwoordigt de huurder-id van uw IMS-organisatie, voorafgegaan door een onderstrepingsteken. De aanwezigheid van huurder identiteitskaart wijst erop dat de gebieden u toevoegt in namespace van uw organisatie bevat zijn.

Met andere woorden, de velden die u toevoegt, zijn uniek voor uw organisatie en worden in het [!DNL Schema Registry] opgeslagen in een specifiek gebied dat alleen voor uw organisatie toegankelijk is. De gebieden u bepaalt moeten altijd aan uw huurdersnamespace worden toegevoegd om botsingen met namen van andere standaardklassen, mixins, gegevenstypes, en gebieden te verhinderen.

In dat knooppunt met naamruimte bevindt zich een &quot;[!UICONTROL Nieuw veld]&quot;. Dit is het begin van &quot;[!UICONTROL Loyalty Details]&quot;mengen.

![](../images/tutorials/create-schema/new_field_loyalty.png)

Gebruikend de controles op de rechterkant van de redacteur, begin door een `loyalty` gebied met type &quot;[!UICONTROL Object]&quot;te creëren dat zal worden gebruikt om uw loyaliteits-verwante gebieden te houden. Selecteer **[!UICONTROL Toepassen]** als u klaar bent.

![](../images/tutorials/create-schema/loyalty_object.png)

De wijzigingen worden toegepast en het nieuwe object `loyalty` wordt weergegeven. Selecteer het **plus (+)** pictogram naast het voorwerp om extra loyaliteitsgerelateerde gebieden toe te voegen. Er verschijnt een &quot;[!UICONTROL Nieuw veld]&quot; en de sectie **[!UICONTROL Veldeigenschappen]** is zichtbaar aan de rechterkant van het canvas.

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

Voor elk veld is de volgende informatie vereist:

* **[!UICONTROL Veldnaam]:** de naam van het veld, geschreven in hoofdletters en kleine letters. Voorbeeld: loyaltyLevel
* **[!UICONTROL Weergavenaam]:** de naam van het veld, geschreven in hoofdletters/kleine letters. Voorbeeld: Loyaliteitsniveau
* **[!UICONTROL Type]:** het gegevenstype van het veld. Dit omvat fundamentele scalaire types en om het even welke gegevenstypes die in [!DNL Schema Registry] worden bepaald. Voorbeelden: [!UICONTROL String], [!UICONTROL Integer], [!UICONTROL Boolean], [!UICONTROL Person], [!UICONTROL Adres], [!UICONTROL Telefoonnummer], enz.
* **[!UICONTROL Beschrijving]:** Een optionele beschrijving van het veld moet worden opgenomen, geschreven in een zin met maximaal 200 tekens.

Het eerste veld voor het object `Loyalty` is een tekenreeks met de naam `loyaltyId`. Wanneer u het type van het nieuwe veld instelt op &quot;[!UICONTROL String]&quot;, wordt de sectie **[!UICONTROL Veldeigenschappen]** gevuld met verschillende opties voor het toepassen van beperkingen, waaronder standaardwaarde, opmaak en maximumlengte.

![](../images/tutorials/create-schema/string_constraints.png)

Welke beperkingsopties beschikbaar zijn, is afhankelijk van het geselecteerde gegevenstype. Aangezien `loyaltyId` een e-mailadres zal zijn, selecteert u &quot;[!UICONTROL email]&quot; in het vervolgkeuzemenu **[!UICONTROL Indeling]**. Selecteer **[!UICONTROL Toepassen]** om uw wijzigingen toe te passen.

![](../images/tutorials/create-schema/loyaltyId_field.png)

## Meer velden toevoegen aan de mix {#mixin-fields-2}

Nu u het `loyaltyId` gebied hebt toegevoegd, kunt u extra gebieden toevoegen om loyaliteitsgerelateerde informatie zoals te vangen:

* Punten (geheel getal)
* Sinds lid (datum)

Als u elk veld aan het schema wilt toevoegen, selecteert u het **plus-pictogram (+)** naast het object `loyalty` en vult u de vereiste informatie in.

Wanneer voltooid, zal het voorwerp van de Loyalty gebieden voor loyauiteits identiteitskaart, punten, en lid-sinds bevatten.

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## Een opsommingsveld toevoegen aan de mix {#enum}

Bij het definiëren van velden in de [!DNL Schema Editor] zijn er enkele extra opties die u kunt toepassen op standaardveldtypen om verdere beperkingen te bieden aan de gegevens die het veld kan bevatten. De gebruiksgevallen voor deze beperkingen worden in de volgende tabel uitgelegd:

| Restrictie | Beschrijving |
| --- | --- |
| [!UICONTROL Vereist] | Geeft aan dat het veld verplicht is voor gegevensinvoer. Om het even welke gegevens die aan een dataset worden geupload die op dit schema wordt gebaseerd dat dit gebied niet bevat zullen op opname ontbreken. |
| [!UICONTROL Array] | Geeft aan dat het veld een array van waarden bevat, elk met het opgegeven gegevenstype. Als u deze beperking bijvoorbeeld gebruikt voor een veld met het gegevenstype &quot;[!UICONTROL String]&quot;, geeft u op dat het veld een array van tekenreeksen zal bevatten. |
| [!UICONTROL Enum] | Geeft aan dat dit veld een van de waarden uit een opsommingslijst met mogelijke waarden moet bevatten. |
| [!UICONTROL Identiteit] | Geeft aan dat dit veld een identiteitsveld is. Meer informatie over identiteitsgebieden wordt verstrekt [later in dit leerprogramma](#identity-field). |
| [!UICONTROL Relatie] | Hoewel schemarelaties kunnen worden afgeleid door het gebruik van het samenvoegingsschema en [!DNL Real-time Customer Profile], is dit alleen van toepassing op schema&#39;s die dezelfde klasse delen. De [!UICONTROL beperking Relationship] wijst erop dat dit gebied verwijzingen de primaire identiteit van een schema dat op een verschillende klasse wordt gebaseerd, die een verhouding tussen de twee schema&#39;s impliceert. Zie de zelfstudie over [het definiëren van een relatie](./relationship-ui.md) voor meer informatie. |

>[!NOTE]
>
>Alle vereiste, identiteits- of relatievelden worden weergegeven in het linkerspoor, zodat u deze velden gemakkelijk kunt vinden, ongeacht de complexiteit van het schema.
>
>![](../images/tutorials/create-schema/left-rail-special.png)

Voor deze zelfstudie vereist het [!DNL "loyalty"]-object in het schema een nieuw enum-veld dat het &quot;loyaliteitsniveau&quot; van een klant beschrijft, waarbij de waarde slechts een van de vier mogelijke opties kan zijn. Als u dit veld aan het schema wilt toevoegen, selecteert u het pictogram **plus (+)** naast het object `loyalty` en vult u de vereiste velden in voor **[!UICONTROL Veldnaam]** en **[!UICONTROL Weergavenaam]**. Voor **[!UICONTROL Type]**, selecteer &quot;[!UICONTROL String]&quot;.

![](../images/tutorials/create-schema/loyalty-level-type.png)

Er verschijnen extra selectievakjes voor het veld nadat het type is geselecteerd, waaronder selectievakjes voor **[!UICONTROL Array]**, **[!UICONTROL Enum]** en **[!UICONTROL Identity]**.

Schakel het selectievakje **[!UICONTROL Enum]** in om de sectie **[!UICONTROL Enum values]** hieronder te openen. Hier kunt u **[!UICONTROL Waarde]** (in camelCase) en **[!UICONTROL Label]** (een facultatieve, lezer-vriendelijke naam in het Geval van de Titel) voor elk aanvaardbaar loyaliteitsniveau invoeren.

Wanneer u alle veldeigenschappen hebt voltooid, uitgezocht **[!UICONTROL Apply]** om &quot;[!DNL loyaltyLevel]&quot;gebied aan het `loyalty` voorwerp toe te voegen.

![](../images/tutorials/create-schema/loyalty_level_enum.png)

## Een object met meerdere velden omzetten in een gegevenstype {#datatype}

Het `loyalty` voorwerp bevat nu verscheidene loyaliteitspecifieke gebieden, en vertegenwoordigt een gemeenschappelijke gegevensstructuur die in andere schema&#39;s nuttig zou kunnen zijn. Met [!DNL Schema Editor] kunt u gemakkelijk herbruikbare objecten met meerdere velden toepassen door de structuur van die objecten om te zetten in gegevenstypen.

De types van gegevens staan voor het verenigbare gebruik van multi-gebiedsstructuren toe en verstrekken meer flexibiliteit dan een mengeling omdat zij overal binnen een schema kunnen worden gebruikt. Dit wordt gedaan door de waarde **[!UICONTROL Type]** van het gebied aan dat van om het even welk gegevenstype te plaatsen die in [!DNL Schema Registry] wordt bepaald.

Als u het object `loyalty` wilt omzetten in een gegevenstype, selecteert u het veld `loyalty` onder **[!UICONTROL Structuur]** en selecteert u **[!UICONTROL Omzetten in nieuw gegevenstype]** aan de rechterkant van de editor onder **[!UICONTROL Veldeigenschappen]**. Er verschijnt een groene popover om te bevestigen dat het object is geconverteerd.

![](../images/tutorials/create-schema/convert-data-type.png)

Als u nu onder **[!UICONTROL Structuur]** kijkt, ziet u dat het veld `loyalty` een gegevenstype heeft van &quot;[!DNL Loyalty]&quot; en dat de velden kleine vergrendelingspictogrammen bevatten naast de velden. Dit geeft aan dat het niet langer om afzonderlijke velden gaat, maar om een onderdeel van een gegevenstype met meerdere velden.

![](../images/tutorials/create-schema/loyalty_data_type.png)

In een toekomstig schema, kon u een gebied nu toewijzen als &quot;[!DNL Loyalty]&quot;type en het zou automatisch gebieden voor identiteitskaart, loyaliteitsniveau, lid sinds, en punten omvatten.

>[!NOTE]
>
>U kunt ook aangepaste gegevenstypen maken en bewerken, onafhankelijk van het bewerken van schema&#39;s. Zie de handleiding bij [het maken en bewerken van gegevenstypen](../ui/resources/data-types.md) voor meer informatie.

## Schema-velden zoeken en filteren

Het schema bevat nu verschillende combinaties naast de velden die door de basisklasse worden verschaft. Wanneer u met grotere schema&#39;s werkt, kunt u de selectievakjes naast mixinnamen in de linkerrails selecteren om de weergegeven velden te filteren op de velden die alleen worden weergegeven door de mixins waarin u geïnteresseerd bent.

![](../images/tutorials/create-schema/filter-by-mixin.png)

Als u naar een specifiek veld in uw schema zoekt, kunt u ook de zoekbalk gebruiken om weergegeven velden op naam te filteren, ongeacht onder welke combinatie deze velden staan.

![](../images/tutorials/create-schema/search.png)

>[!IMPORTANT]
>
>Bij de weergave van overeenkomende velden houdt de zoekfunctie rekening met eventuele geselecteerde mixfilters. Als een onderzoeksvraag niet de resultaten toont u verwacht, kunt u moeten tweemaal controleren dat u geen relevante mengen filtreert.

## Een schemaveld instellen als een identiteitsveld {#identity-field}

De standaard gegevensstructuur die schema&#39;s verstrekken kan worden gebruikt om gegevens te identificeren die tot het zelfde individu over veelvoudige bronnen behoren, die voor diverse stroomafwaartse gebruiksgevallen zoals segmentatie, rapportering, gegevenswetenschapsanalyse, en meer toestaan. Als u gegevens op basis van individuele identiteiten wilt koppelen, moeten de sleutelvelden worden gemarkeerd als [!UICONTROL Identiteitsvelden] binnen de toepasselijke schema&#39;s.

[!DNL Experience Platform] maakt het gemakkelijk om een identiteitsgebied door het gebruik van een  **** Identitycheckbox in  [!DNL Schema Editor]te wijzen. U moet echter bepalen welk veld de beste kandidaat is om als identiteit te gebruiken, op basis van de aard van uw gegevens.

Er kunnen bijvoorbeeld duizenden leden van het loyaliteitsprogramma zijn die tot hetzelfde &quot;loyaliteitsniveau&quot; behoren, maar elk lid van het loyaliteitsprogramma heeft een unieke `loyaltyId` (wat in dit geval het e-mailadres van het individuele lid is). Het feit dat `loyaltyId` een uniek herkenningsteken voor elk lid is maakt het een goede kandidaat voor een identiteitsgebied, terwijl `loyaltyLevel` niet is.

>[!IMPORTANT]
>
>De stappen hieronder beschrijven hoe te om een identiteitsbeschrijver aan een bestaand schemagebied toe te voegen. Als alternatief voor het definiëren van identiteitsvelden binnen de structuur van het schema zelf, kunt u ook een veld `identityMap` gebruiken om identiteitsgegevens te bevatten.
>
>Als u van plan bent om `identityMap` te gebruiken, houd in mening dat het om het even welke primaire identiteit zal met voeten treden u direct aan het schema toevoegt. Zie de sectie over `identityMap` in [grondbeginselen van schemacompositie gids](../schema/composition.md#identityMap) voor meer informatie.

Selecteer in de sectie **[!UICONTROL Structuur]** van de editor het veld `loyaltyId` en schakel het selectievakje **[!UICONTROL Identiteit]** onder **[!UICONTROL Veldeigenschappen]** in. Schakel het selectievakje en de optie in om dit in te stellen als de **[!UICONTROL primaire identiteit]** wordt weergegeven. Selecteer dit vak ook.

>[!NOTE]
>
>Elk schema mag slechts één primair identiteitsveld bevatten. Zodra een schemagebied als primaire identiteit is geplaatst, zult u een foutenmelding ontvangen als u later probeert om een ander identiteitsgebied in het schema als primaire identiteit te plaatsen.

Daarna, moet u **[!UICONTROL Identiteitsnamespace]** van de lijst van vooraf bepaalde namespaces in dropdown verstrekken. Aangezien `loyaltyId` het e-mailadres van de klant is, selecteert u &quot;[!UICONTROL Email]&quot; in het vervolgkeuzemenu. Selecteer **[!UICONTROL Toepassen]** om de updates aan het `loyaltyId` gebied te bevestigen.

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>Zie de [[!DNL Identity Service] documentatie](../../identity-service/troubleshooting-guide.md#standard-namespaces) voor een lijst met standaardnaamruimten en de bijbehorende definities.

Nadat de wijziging is toegepast, wordt op het pictogram voor `loyaltyId` een vingerafdruksymbool weergegeven om aan te geven dat het nu een identiteitsveld is.

![](../images/tutorials/create-schema/identity-applied.png)

Alle gegevens die in het veld `loyaltyId` worden ingevoerd, worden nu gebruikt om die persoon te identificeren en één weergave van die klant samen te voegen. Raadpleeg de [[!DNL Identity Service]](../../identity-service/home.md) documentatie voor meer informatie over het werken met identiteiten in [!DNL Experience Platform].

## Het schema inschakelen voor gebruik in [!DNL Real-time Customer Profile] {#profile}

[[!DNL Real-time Customer Profile]](../../profile/home.md) Gebruikt identiteitsgegevens in  [!DNL Experience Platform] om een holistische mening van elke individuele klant te verstrekken. De service bouwt robuuste, 360°-profielen van klantkenmerken en tijdstempelde accounts van elke interactie die klanten hebben gehad in elk systeem dat is geïntegreerd met [!DNL Experience Platform].

Een schema kan alleen worden ingeschakeld voor gebruik met [!DNL Real-time Customer Profile] als er een primaire identiteit is gedefinieerd. Er wordt een foutbericht weergegeven als u een schema wilt inschakelen zonder eerst een primaire identiteit te definiëren.

<img src="../images/tutorials/create-schema/missing_primary_identity.png" width="600" /><br>

Als u het schema &quot;Loyalty-leden&quot; wilt inschakelen voor gebruik in [!DNL Profile], selecteert u eerst &quot;[!DNL Loyalty Members]&quot; in de sectie **[!UICONTROL Structuur]** van de editor.

Aan de rechterkant van de editor wordt informatie over het schema weergegeven, inclusief de weergavenaam, beschrijving en type. Naast deze informatie is er een schakelknop **[!UICONTROL Profiel]**.

![](../images/tutorials/create-schema/profile-toggle.png)

Selecteer **[!UICONTROL Profiel]** en een popover verschijnt, vragend u om te bevestigen dat u wenst om het schema voor [!DNL Profile] toe te laten.

<img src="../images/tutorials/create-schema/enable-profile.png" width="700" /><br>

>[!WARNING]
>
>Als een schema eenmaal is ingeschakeld voor [!DNL Real-time Customer Profile] en is opgeslagen, kan het niet worden uitgeschakeld.

Selecteer **[!UICONTROL Inschakelen]** om uw keuze te bevestigen. U kunt **[!UICONTROL Profiel]** opnieuw selecteren om het schema onbruikbaar te maken als u wenst, maar zodra het schema is bewaard terwijl [!DNL Profile] wordt toegelaten, kan het niet meer worden onbruikbaar gemaakt.

## Volgende stappen en extra bronnen

Nu u klaar bent met het samenstellen van het schema, kunt u het volledige schema in het canvas zien. Selecteer **[!UICONTROL Opslaan]** en het schema wordt opgeslagen naar [!DNL Schema Library], waardoor het toegankelijk wordt gemaakt via [!DNL Schema Registry].

Uw nieuwe schema kan nu worden gebruikt om gegevens in [!DNL Platform] in te voeren. Herinner dat zodra het schema is gebruikt om gegevens in te voeren, slechts de additieve veranderingen kunnen worden aangebracht. Zie [grondbeginselen van schemacompositie](../schema/composition.md) voor meer informatie over schema versioning.

U kunt nu de zelfstudie op [het bepalen van een schemaverhouding in UI](./relationship-ui.md) volgen om een nieuw relatieveld aan het schema van de &quot;Leden van de Waardigheid&quot;toe te voegen.

Het schema &quot;Loyalty members&quot; is ook beschikbaar voor weergave en beheer met de API [!DNL Schema Registry]. Als u met de API wilt gaan werken, begint u met het lezen van de [[!DNL Schema Registry API] ontwikkelaarshandleiding](../api/getting-started.md).

### Videobronnen

>[!WARNING]
>
>De interface [!DNL Platform] die in de volgende video&#39;s wordt getoond is verouderd. Raadpleeg de bovenstaande documentatie voor de meest recente schermafbeeldingen en functionaliteit van de gebruikersinterface.

De volgende video toont hoe te om een eenvoudig schema in [!DNL Platform] UI tot stand te brengen.

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

De volgende video is bedoeld om uw inzicht in het werken met mixins en klassen te versterken.

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## Aanhangsel

De volgende secties verstrekken extra informatie betreffende het gebruik van [!DNL Schema Editor].

### Een nieuwe klasse maken {#create-new-class}

[!DNL Experience Platform] biedt de flexibiliteit om een schema te definiëren dat is gebaseerd op een klasse die uniek is voor uw organisatie. Leer hoe te om een nieuwe klasse tot stand te brengen, zie de gids op [creërend en het uitgeven klassen in UI](../ui/resources/classes.md#create).

### De klasse van een schema wijzigen {#change-class}

U kunt de klasse van een schema op om het even welk punt tijdens het aanvankelijke samenstellingsproces veranderen alvorens het schema is bewaard.

>[!WARNING]
>
>Het opnieuw toewijzen van de klasse voor een schema zou met uiterste voorzichtigheid moeten worden gedaan. Mixins zijn alleen compatibel met bepaalde klassen en als u de klasse wijzigt, worden het canvas en alle toegevoegde velden opnieuw ingesteld.

Leer hoe te om de klasse van een schema te veranderen, zie de gids op [het beheren van schema&#39;s in UI](../ui/resources/schemas.md).
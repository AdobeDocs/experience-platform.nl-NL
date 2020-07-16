---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een schema maken met de Schema-editor
topic: tutorials
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '3376'
ht-degree: 0%

---


# Een schema maken met de opdracht [!DNL Schema Editor]

Het [!DNL Schema Registry] biedt een gebruikersinterface en RESTful-API waarmee u alle bronnen in het Adobe Experience Platform kunt weergeven en beheren [!DNL Schema Library]. Het [!DNL Schema Library] bevat bronnen die beschikbaar zijn gesteld door Adobe, partners van Experience Platforms en leveranciers van wie u de toepassingen gebruikt, en bronnen die u definieert en opslaat naar de [!DNL Schema Registry]server.

Deze zelfstudie behandelt de stappen voor het maken van een schema met behulp van de Schema-editor in [!DNL Experience Platform]. Als u liever een schema samenstelt met de API voor de registratie van het schema, moet u eerst de handleiding voor [de ontwikkelaar van het](../api/getting-started.md) schemaregister lezen voordat u de zelfstudie [maakt met behulp van de API](create-schema-api.md).

Deze zelfstudie bevat ook stappen om een nieuwe klasse [te](#create-new-class) definiëren waarmee u een schema kunt samenstellen.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de verschillende aspecten van Adobe Experience Platform die betrokken zijn bij het gebruik van de Schema-editor. Lees vóór het starten van deze zelfstudie de documentatie voor de volgende concepten:

* [!DNL Experience Data Model (XDM)](../home.md): Het gestandaardiseerde kader waardoor het Platform gegevens van de klantenervaring organiseert.
* [Basisbeginselen van de schemacompositie](../schema/composition.md): Een overzicht van schema&#39;s XDM en hun bouwstenen, met inbegrip van klassen, mengen, gegevenstypes, en gebieden.
* [!DNL Real-time Customer Profile](../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Deze zelfstudie vereist dat u toegang hebt tot [!DNL Experience Platform]. Als u geen toegang hebt tot een IMS-organisatie in [!DNL Experience Platform], neemt u contact op met uw systeembeheerder voordat u verdergaat.

## Door bestaande schema&#39;s in de werkruimte Schema&#39;s bladeren {#browse}

De werkruimte van Schema&#39;s binnen [!DNL Experience Platform] verstrekt een visualisatie van [!DNL Schema Library], die u toestaat om alle schema&#39;s te bekijken en te beheren beschikbaar aan u, evenals nieuwe degenen samen te stellen. De werkruimte omvat ook de Redacteur van het Schema, het canvas waarop u een schema door dit leerprogramma zult samenstellen.

Nadat u zich hebt aangemeld [!DNL Experience Platform], klikt u op **[!UICONTROL Schema]** in de linkernavigatie en gaat u naar de werkruimte Schemas. U zult een lijst van schema&#39;s (een vertegenwoordiging van [!DNL Schema Library]) zien waar u, alle schema&#39;s kunt bekijken beheren en aanpassen beschikbaar aan u. De lijst bevat de naam, het type, de klasse en het gedrag (record of tijdreeks) waarop het schema is gebaseerd, evenals de datum en tijd waarop het schema voor het laatst is gewijzigd.

Klik het filterpictogram naast de bar van het Onderzoek om het filtreren mogelijkheden voor alle middelen in de registratie, met inbegrip van klassen, mengen, en gegevenstypes te gebruiken.

![De schemabibliotheek weergeven](../images/tutorials/create-schema/schemas_filter.png)

## Een schema maken en een naam geven {#create}

Als u wilt beginnen met het samenstellen van een schema, klikt u op Schema **** maken in de rechterbovenhoek van de werkruimte Schema.

![Schema maken, knop](../images/tutorials/create-schema/create_schema_button.png)

De *Schema-editor* wordt weergegeven. Dit is het canvas waarop u het schema wilt samenstellen. Wanneer u bij de redacteur aankomt, wordt een &quot;Naamloos Schema&quot;in de sectie van de *Structuur* van het canvas automatisch gecreeerd voor u beginnen aanpassend.

![Schema-editor](../images/tutorials/create-schema/schema_editor.png)

Aan de rechterkant van de editor staan de *schemaeigenschappen* , waar u een naam voor het schema kunt opgeven (met behulp van het veld **[!UICONTROL Weergavenaam]** ). Nadat u een naam hebt ingevoerd, wordt het canvas bijgewerkt met de nieuwe naam van het schema.

![Schema Canvas](../images/tutorials/create-schema/name_schema.png)

Er zijn verscheidene belangrijke overwegingen om te maken wanneer het beslissen over een naam voor uw schema:

* De namen van het schema zouden kort en beschrijvend moeten zijn zodat het schema in de bibliotheek later gemakkelijk kan worden gevonden.
* Schemenamen moeten uniek zijn, wat betekent dat ze ook specifiek genoeg moeten zijn om in de toekomst niet opnieuw te worden gebruikt. Bijvoorbeeld, als uw organisatie afzonderlijke loyaliteitsprogramma&#39;s voor verschillende merken had, zou het verstandig zijn om uw schema &quot;Merk A Loyalty Leden&quot;te noemen om het gemakkelijk te maken om van andere loyaliteits-verwante regelingen onderscheid te maken u zou kunnen later bepalen.
* U kunt desgewenst aanvullende informatie over het schema opgeven in het veld **[!UICONTROL Beschrijving]** .

Deze zelfstudie stelt een schema samen om gegevens met betrekking tot de leden van een loyaliteitsprogramma in te voeren, daarom wordt het schema genoemd &quot;Loyalty Leden&quot;.

## Een klasse toewijzen {#class}

Links in de editor bevindt zich de sectie *Compositie* . Het bevat momenteel twee subsecties: *[!UICONTROL Schema]* en *[!UICONTROL Klasse]*.

Nu het schema een naam heeft, is het tijd om de klasse toe te wijzen die het schema zal uitvoeren. Klik op **[!UICONTROL Toewijzen]** naast *[!UICONTROL Klasse]*.

![](../images/tutorials/create-schema/assign_class_button.png)

Het dialoogvenster *[!UICONTROL Klasse]* toewijzen wordt weergegeven. In dit venster wordt een lijst weergegeven met alle beschikbare klassen, inclusief alle klassen die door uw organisatie zijn gedefinieerd (de eigenaar is &quot;Klant&quot;) en standaardklassen die door Adobe zijn gedefinieerd.

Klik op de klassenaam om de beschrijving van de klasse weer te geven. U kunt ook een **[!UICONTROL voorbeeld van de klassenstructuur]** weergeven om de velden en metagegevens weer te geven die aan de klasse zijn gekoppeld.

Deze zelfstudie gebruikt de [!DNL XDM Individual Profile] klasse. Klik op het keuzerondje naast de klasse om deze te selecteren en klik vervolgens op **[!UICONTROL Klasse]** toewijzen.

![Dialoogvenster Klasse toewijzen](../images/tutorials/create-schema/assign_class.png)

Het canvas verschijnt weer. De sectie *[!UICONTROL Klasse]* bevat nu de klasse die u hebt geselecteerd ([!DNL XDM Individual Profile]) en de velden die door de [!DNL XDM Individual Profile] klasse worden bijgedragen, zijn nu zichtbaar in de sectie *[!UICONTROL Structuur]* .

![Afzonderlijke XDM-profielklasse toegewezen](../images/tutorials/create-schema/class_assigned_structure.png)

De velden worden weergegeven in de notatie &quot;fieldName | Gegevenstype&quot;. De stappen voor het bepalen van schemagebieden in UI worden verstrekt later in dit leerprogramma.

>[!NOTE]
>
>U kunt de klasse van een schema [op om het even welk punt tijdens het aanvankelijke samenstellingsproces](#change-class) veranderen alvorens het schema is bewaard, maar dit zou met uiterste voorzichtigheid moeten worden gedaan. Mixins zijn alleen compatibel met bepaalde klassen. Als u de klasse wijzigt, worden het canvas en alle toegevoegde velden opnieuw ingesteld.

## Een mix toevoegen {#mixin}

Nu een klasse is toegewezen, bevat de sectie *Compositie* een derde subsectie: *[!UICONTROL Mengsels]*.

U kunt nu velden toevoegen aan uw schema door mixen toe te voegen. Een mix is een groep van één of meerdere gebieden die een bepaald concept beschrijven. Deze zelfstudie gebruikt mixins om de leden van het loyaliteitsprogramma te beschrijven en zeer belangrijke informatie zoals naam, verjaardag, telefoonaantal, adres, en meer te vangen.

Als u een mix wilt toevoegen, klikt u op **Toevoegen** in de subsectie *Mixins* .

![](../images/tutorials/create-schema/add_mixin_button.png)

Het dialoogvenster *[!UICONTROL Mixin]* toevoegen wordt weergegeven. Mixinen zijn alleen bedoeld voor gebruik met specifieke klassen. Daarom bevat de lijst met mengsels alleen die welke compatibel zijn met de geselecteerde klasse (in dit geval de [!DNL XDM Individual Profile] klasse).

Als u het keuzerondje naast een mix selecteert, kunt u de **[!UICONTROL mixinstructuur]** voorvertonen. Selecteer de mix Details van de Persoon van het Profiel, dan klik **[!UICONTROL Add Mixin]**.

![](../images/tutorials/create-schema/add_mixin_person_details.png)

Het schemacanvas verschijnt opnieuw. De sectie *[!UICONTROL Mixins]* bevat nu de mix &quot;Details[!UICONTROL van]profielpersoon&quot; en de sectie *[!UICONTROL Structuur]* bevat de velden die worden ingebracht door de mix.

![](../images/tutorials/create-schema/person_details_structure.png)

Deze mix levert verschillende velden onder de naam &quot;person&quot; op het hoogste niveau bij met het gegevenstype &quot;Person&quot;. In deze groep velden wordt informatie over een individu beschreven, zoals naam, geboortedatum en geslacht.

>[!NOTE]
>
>Vergeet niet dat in velden scalaire typen (zoals een tekenreeks, geheel getal, array of datum) kunnen worden gebruikt als gegevenstype, en ook elk gegevenstype (een groep velden die een algemeen concept vertegenwoordigen) in de [!DNL Schema Registry]velden.

Het veld &quot;[!UICONTROL name]&quot; heeft een gegevenstype van het type &quot;[!UICONTROL Persoon Name]&quot;, wat betekent dat het ook een algemeen concept beschrijft en naamgerelateerde subvelden bevat zoals voornaam, achternaam en volledige naam.

Klik op verschillende velden op het canvas om extra velden weer te geven die worden toegevoegd aan de schemastructuur.

## Een andere mix toevoegen {#mixin-2}

U kunt nu dezelfde stappen herhalen om een andere mix toe te voegen. Wanneer u dit keer het dialoogvenster *[!UICONTROL Mixin]* toevoegen weergeeft, ziet u dat de mix &quot;Details[!UICONTROL van]profielpersoon&quot; grijs is weergegeven en dat het keuzerondje ernaast niet kan worden geselecteerd. Zo voorkomt u dat u per ongeluk combinaties dupliceert die u al in het huidige schema hebt opgenomen.

U kunt nu de optie &quot;[!DNL Profile Personal Details" mixin] toevoegen via het dialoogvenster *[!UICONTROL Mengsel]* toevoegen.

![](../images/tutorials/create-schema/add_mixin_personal_details.png)

Nadat u het canvas hebt toegevoegd, verschijnt het weer. De &quot;Persoonlijke Details[!UICONTROL van het]Profiel&quot;is nu vermeld onder *[!UICONTROL Mixins]* in de sectie van de *[!UICONTROL Samenstelling]* , en gebieden voor huisadres, mobiele telefoon, en meer zijn toegevoegd onder *[!UICONTROL Structuur]*.

Net als in het veld &quot;[!UICONTROL naam]&quot; vertegenwoordigen de velden die u zojuist hebt toegevoegd concepten met meerdere velden. &quot;[!UICONTROL homeAddress]&quot; heeft bijvoorbeeld een gegevenstype &quot;[!UICONTROL Address]&quot; en &quot;[!UICONTROL mobilePhone]&quot; heeft een gegevenstype &quot;[!UICONTROL Phone Number]&quot;. U kunt op elk van deze gebieden klikken om hen uit te breiden en de extra gebieden te zien inbegrepen in het gegevenstype.

![](../images/tutorials/create-schema/personal_details_structure.png)

## Een nieuwe mix definiëren {#define-mixin}

Het schema &quot;[!UICONTROL Loyalty-leden]&quot; is bedoeld voor het vastleggen van gegevens die betrekking hebben op de leden van een loyaliteitsprogramma, zodat het een aantal specifieke velden met betrekking tot loyaliteit vereist. Er zijn geen standaardmengingen beschikbaar die de noodzakelijke gebieden bevatten, daarom zult u een nieuwe mix moeten bepalen.

Wanneer u dit keer het dialoogvenster *[!UICONTROL Mixin]* toevoegen opent, selecteert u Nieuwe **[!UICONTROL mixer]** maken. Vervolgens wordt u gevraagd een **[!UICONTROL weergavenaam]** en een **[!UICONTROL beschrijving]** voor de mix op te geven.

![](../images/tutorials/create-schema/mixin_create_new.png)

Net als bij klassennamen moet de mixinnaam kort en eenvoudig zijn en beschrijven wat de mix aan het schema zal bijdragen. Ook deze zijn uniek, dus u kunt de naam niet opnieuw gebruiken en moet er dus voor zorgen dat deze voldoende specifiek is.

Geef voor deze zelfstudie de naam van de nieuwe mix &quot;[!UICONTROL Loyalty Details]&quot;.

Klik op Mixin **[!UICONTROL toevoegen]** om terug te keren naar de schema-editor. &quot;[!UICONTROL Loyalty Details]&quot; moeten nu worden weergegeven onder *[!UICONTROL Mixins]* aan de linkerkant van het canvas, maar er zijn nog geen velden aan gekoppeld en daarom verschijnen er geen nieuwe velden onder *[!UICONTROL Structuur]*.

## Velden toevoegen aan de mix {#mixin-fields}

Nu u de mix &quot;[!UICONTROL Loyalty Details]&quot;hebt gecreeerd, is het tijd om de gebieden te bepalen die de mixin aan het schema zal bijdragen.

Klik om te beginnen op de naam van de mix in de sectie *[!UICONTROL Mixins]* . Zodra u dit doet, zullen de Eigenschappen *[!UICONTROL van de]* Mixin op de rechterkant van de redacteur verschijnen en zal een **[!UICONTROL Add knoop van het Gebied]** naast de naam van het schema onder *[!UICONTROL Structuur]* verschijnen.

![](../images/tutorials/create-schema/loyalty_details_structure.png)

Klik op Veld **** toevoegen naast &quot;[!UICONTROL Loyalty-leden]&quot; om een nieuw knooppunt in de structuur te maken. Dit knooppunt (in dit voorbeeld &#39;_huurderId&#39; genoemd) vertegenwoordigt de huurder-id van uw IMS-organisatie, voorafgegaan door een onderstrepingsteken. De aanwezigheid van huurder identiteitskaart wijst erop dat de gebieden u toevoegt in namespace van uw organisatie bevat zijn.

Met andere woorden, de velden die u toevoegt, zijn uniek voor uw organisatie en worden opgeslagen in een specifiek gebied dat alleen voor uw IMS-organisatie toegankelijk is. [!DNL Schema Registry] Velden die u definieert, moeten altijd aan de naamruimte worden toegevoegd om conflicten te voorkomen met namen van andere standaardklassen, mixins, gegevenstypen en velden.

In dat knooppunt met naamruimte bevindt zich een &quot;[!UICONTROL Nieuw veld]&quot;. Dit is het begin van de mix &quot;[!UICONTROL Loyalty Details]&quot;.

![](../images/tutorials/create-schema/new_field_loyalty.png)

Gebruikend de Eigenschappen *[!UICONTROL van het]* Gebied op de rechterkant van de redacteur, begin door een gebied van de &quot;[!UICONTROL loyaliteit]&quot;met type &quot;[!UICONTROL Voorwerp]&quot;te creëren dat zal worden gebruikt om uw op loyaliteit betrekking hebbende gebieden te houden. Klik op **[!UICONTROL Toepassen]** als u klaar bent.

![](../images/tutorials/create-schema/loyalty_object.png)

De wijzigingen worden toegepast en het nieuwe &quot;[!UICONTROL loyalty]&quot;-object wordt weergegeven. Klik naast het object op Veld **** toevoegen om aanvullende aan loyaliteit gerelateerde velden toe te voegen. Er wordt een &#39;&#39;Nieuw veld&#39;&#39; weergegeven en de sectie *[!UICONTROL Veldeigenschappen]* is aan de rechterkant van het canvas zichtbaar.

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

Voor elk veld is de volgende informatie vereist:

* **[!UICONTROL Veldnaam]:**De naam van het veld, geschreven in camelcase. Voorbeeld: loyaltyLevel
* **[!UICONTROL Weergavenaam]:**De naam van het veld, geschreven in hoofdletters/kleine letters. Voorbeeld: Loyaliteitsniveau
* **[!UICONTROL Type]:**Het gegevenstype van het veld. Dit omvat fundamentele scalaire types en om het even welke die gegevenstypes in[!DNL Schema Registry]worden bepaald. Voorbeelden: tekenreeks, geheel getal, Booleaans, Persoon, Adres, Telefoonnummer, enz.
* **[!UICONTROL Omschrijving]:**Er moet een facultatieve beschrijving van het veld worden opgenomen, geschreven in geval van een zin. (max. 200 tekens)

Het eerste veld voor het object Loyalty is een tekenreeks met de naam &quot;[!UICONTROL loyaltyId]&quot;. Wanneer u het type van het nieuwe veld instelt op &quot;[!UICONTROL String]&quot;, wordt het venster *[!UICONTROL Veldeigenschappen]* gevuld met verschillende opties voor het toepassen van beperkingen, waaronder **[!UICONTROL Standaardwaarde]**, **[!UICONTROL Indeling]** en **[!UICONTROL Maximale lengte]**.

![](../images/tutorials/create-schema/string_constraints.png)

Welke beperkingsopties beschikbaar zijn, is afhankelijk van het geselecteerde gegevenstype. Aangezien &#39;[!UICONTROL loyaltyId]&#39; een e-mailadres is, selecteert u &#39;[!UICONTROL email]&#39; in het vervolgkeuzemenu **[!UICONTROL Indeling]** . Selecteer **[!UICONTROL Toepassen]** om uw wijzigingen toe te passen.

![](../images/tutorials/create-schema/loyaltyId_field.png)

## Meer velden toevoegen om te mengen {#mixin-fields-2}

Nu u het gebied &quot;[!UICONTROL loyaltyId]&quot;hebt toegevoegd, kunt u extra gebieden toevoegen om loyaliteitsgerelateerde informatie zoals te vangen:

* Punten (geheel getal)
* Lid sinds (datum)

Elk veld wordt toegevoegd door op Veld **** toevoegen op het loyaliteitsobject te klikken en de vereiste informatie in te vullen.

Wanneer dit is voltooid, bevat het object Loyalty velden voor: Loyalty ID, Punten, en Lid sinds.

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## Veld &#39;enum&#39; toevoegen om te mengen {#enum}

Wanneer u velden in de Schema-editor definieert, zijn er enkele aanvullende opties die u kunt toepassen op elementaire veldtypen om de gegevens in het veld verder te beperken.

Een voorbeeld hiervan is een veld met het[!UICONTROL kwaliteitsniveau], waarbij de waarde slechts een van de vier mogelijke opties kan zijn. Als u dit veld aan het schema wilt toevoegen, klikt u op Veld **** toevoegen naast het object &quot;[!UICONTROL loyaliteit]&quot; en vult u de vereiste velden in onder *[!UICONTROL Veldeigenschappen]*.

Voor **[!UICONTROL Type]** selecteert u &quot;String&quot; en ziet u extra selectievakjes voor **[!UICONTROL Array]**, **[!UICONTROL Enum]** en **[!UICONTROL Identity]**.

Schakel het selectievakje **[!UICONTROL Enum]** in om de sectie *[!UICONTROL Enum Values]* hieronder te openen. Hier kunt u de **[!UICONTROL Waarde]** (in camelCase) en het **[!UICONTROL Etiket]** (een facultatieve, reader-vriendelijke naam in het Geval van de Titel) voor elk aanvaardbaar loyaliteitsniveau invoeren.

Als u alle veldeigenschappen hebt voltooid, klikt u op **[!UICONTROL Toepassen]** en wordt het veld &quot;[!UICONTROL loyaltyLevel]&quot; toegevoegd aan het object &quot;loyalty&quot;.

![](../images/tutorials/create-schema/loyalty_level_enum.png)

Meer informatie over beschikbare extra beperkingen:

* **[!UICONTROL Vereist]:**Geeft aan dat het veld verplicht is voor gegevensinvoer. Om het even welke gegevens die aan een dataset worden geupload die op dit schema wordt gebaseerd dat dit gebied niet bevat zullen op opname ontbreken.
* **[!UICONTROL Array]:**Geeft aan dat het veld een array van waarden bevat, elk met het opgegeven gegevenstype. Als u bijvoorbeeld een gegevenstype &quot;String&quot; selecteert en het selectievakje &quot;Array&quot; inschakelt, bevat het veld een array van tekenreeksen.
* **[!UICONTROL Enum]:**Geeft aan dat dit veld een van de waarden uit een opsommingslijst met mogelijke waarden moet bevatten.
* **[!UICONTROL Identiteit]:**Geeft aan dat dit veld een identiteitsveld is. Meer informatie over identiteitsvelden vindt u[later in deze zelfstudie](#identity-field).

## Een object met meerdere velden omzetten in een gegevenstype {#datatype}

Na het toevoegen van verscheidene loyaliteits-specifieke gebieden, bevat het &quot;[!UICONTROL loyalty]&quot;voorwerp nu een gemeenschappelijke gegevensstructuur die in andere schema&#39;s nuttig zou kunnen zijn.

Wanneer u vindt dat een structuur met meerdere velden opnieuw kan worden gebruikt en u de flexibiliteit wilt hebben om die zelfde gegevensstructuur elders te gebruiken, maakt de Redacteur van het Schema het mogelijk om die structuur in een gegevenstype om te zetten.

De types van gegevens staan voor het verenigbare gebruik van multi-gebiedsstructuren toe en verstrekken meer flexibiliteit dan een mengeling omdat zij overal binnen een schema kunnen worden gebruikt. Dit wordt gedaan door het **[!UICONTROL Type]** van een gebied in een mengeling aan dat van om het even welk die gegevenstype te plaatsen in de registratie wordt bepaald.

Als u het object &quot;[!UICONTROL loyalty]&quot; wilt omzetten in een gegevenstype, klikt u op het veld &quot;loyalty&quot; onder *[!UICONTROL Structuur]* en selecteert u **[!UICONTROL Converteren naar nieuw gegevenstype]** aan de rechterkant van de editor onder *[!UICONTROL Veldeigenschappen]*. Er verschijnt een kleine groene pop-up met de bevestiging &quot;[!UICONTROL Object omgezet in gegevenstype]&quot;.

Als je nu onder *[!UICONTROL Structuur]* kijkt, zie je dat het veld &quot;[!UICONTROL loyaliteit]&quot; een gegevenstype heeft van &quot;[!UICONTROL Loyalty]&quot; en dat de velden kleine slotpictogrammen naast ze hebben die aangeven dat ze geen afzonderlijke velden meer zijn, maar onderdeel van een structuur met meerdere velden.

In een toekomstig schema, kon u een gebied nu toewijzen het **[!UICONTROL Type]** van &quot;[!UICONTROL Loyalty]&quot;en het zou automatisch het Niveau van de Loyalty, Punten, Lid sinds, en de gebieden van identiteitskaart van de Loyalty omvatten.

![](../images/tutorials/create-schema/loyalty_data_type.png)

## Een schemaveld instellen als een identiteitsveld {#identity-field}

Schema&#39;s worden gebruikt voor het opnemen van gegevens in [!DNL Experience Platform], en die gegevens worden uiteindelijk gebruikt om individuen te identificeren en informatie die uit meerdere bronnen afkomstig is aan elkaar te koppelen. Om dit proces te helpen, kunnen de zeer belangrijke gebieden als gebieden van de &quot;[!UICONTROL Identiteit]&quot;worden gemerkt.

[!DNL Experience Platform] maakt het gemakkelijk om een identiteitsgebied door het gebruik van een checkbox van de **[!UICONTROL Identiteit]** in te duiden [!DNL Schema Editor].

Er kunnen bijvoorbeeld duizenden leden van het loyaliteitsprogramma zijn die tot hetzelfde &quot;niveau&quot; behoren, maar elk lid van het loyaliteitsprogramma heeft een unieke &quot;loyaltyId&quot; (wat in dit geval het e-mailadres van het individuele lid is). Het feit dat &quot;loyaltyId&quot;een uniek herkenningsteken voor elk lid is maakt het een goede kandidaat voor een identiteitsgebied, terwijl &quot;niveau&quot;niet is.

In de sectie van de *[!UICONTROL Structuur]* van de redacteur, klik op het &quot;[!UICONTROL loyaltyId]&quot;gebied dat u creeerde en u zult het **[!UICONTROL vakje van de Identiteit]** onder de Eigenschappen *[!UICONTROL van het]* Gebied zien. Schakel het selectievakje in en u kunt dit instellen als de **[!UICONTROL primaire identiteit]**. Controleer ook die doos.

Vervolgens moet u een **[!UICONTROL identiteitsnaamruimte opgeven]**. Er zijn verschillende vooraf gedefinieerde naamruimten, maar aangezien &quot;[!UICONTROL loyaltyId]&quot; het e-mailadres van het lid is, selecteert u &quot;E-mail&quot; in de vervolgkeuzelijst. U kunt nu op **[!UICONTROL Toepassen]** klikken om de updates van het veld &quot;[!UICONTROL loyaltyId]&quot; te bevestigen.

Nu zullen alle gegevens die in het &quot;[!UICONTROL loyaltyId]&quot;gebied worden opgenomen worden gebruikt helpen die individu identificeren en één enkele mening van die klant verbinden.

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>Als een schemaveld eenmaal is ingesteld als primaire identiteit, ontvangt u een foutbericht als u later probeert een ander veld in het schema in te stellen als primaire identiteit. Elk schema mag slechts één primair identiteitsveld bevatten.

Raadpleeg de [!DNL Identity Service](../../identity-service/home.md) documentatie voor meer informatie over het werken met identiteiten.

<!-- ## Relationship

Schemas define a static view of a concept, but do not provide specific details on how data based on these schemas (datasets, etc) may relate to one another. Adobe Experience Platform allows you to describe these relationships through the **Relationship** checkbox in the schema editor. 

In order to define a relationship, click on the field and check the **Relationship** checkbox on the right-side of the canvas. 

![](../images/tutorials/create-schema/relationship.png)

More information about relationships and other schema metadata can be found in the [Schema Registry API Developer Guide](../schema_registry_developer_guide.md). -->

## Het schema inschakelen voor gebruik in [!DNL Real-time Customer Profile] {#profile}

De Redacteur van het Schema verstrekt de capaciteit om een schema voor gebruik toe te laten met [!DNL Real-time Customer Profile](../../profile/home.md). [!DNL Profile] biedt een holistische weergave van elke individuele klant door een robuust, 360°-profiel van klantkenmerken op te bouwen en een tijdstempelaccount van elke interactie die de klant heeft gehad in elk systeem dat met [!DNL Experience Platform]is geïntegreerd.

Als u wilt dat een schema kan worden gebruikt met, moet er een primaire identiteit zijn gedefinieerd. [!DNL Real-time Customer Profile] Als u een schema wilt inschakelen zonder eerst een primaire identiteit te definiëren, ontvangt u het foutbericht &quot;Ontbrekende primaire identiteit&quot;.

![](../images/tutorials/create-schema/missing_primary_identity.png)

Als u het schema &quot;Loyalty-leden&quot; wilt gebruiken in [!DNL Profile], klikt u eerst op &quot;Loyalty-leden&quot; in het gedeelte *Structuur* van de editor.

Aan de rechterkant van de editor, onder *Schema-eigenschappen*, wordt informatie over het schema weergegeven, inclusief de weergavenaam, beschrijving en type. Naast deze informatie is er een schakelknop met de naam **[!UICONTROL Profiel]**.

![](../images/tutorials/create-schema/unified_profile_toggle.png)

Klik op **[!UICONTROL Profiel]** en er verschijnt een pop-up met de vraag of u het schema wilt inschakelen voor [!DNL Profile].

![](../images/tutorials/create-schema/enable_unified_profile.png)

>[!NOTE]
>
>Als een schema is ingeschakeld voor [!DNL Real-time Customer Profile] en opgeslagen, kan het niet worden uitgeschakeld.

## Volgende stappen en extra bronnen

Nu u klaar bent met het samenstellen van een schema &quot;[!UICONTROL Loyalty Leden]&quot;, kunt u het volledige schema in de sectie van de *Structuur* van de redacteur zien. Klik op **[!UICONTROL Opslaan]** en het schema wordt opgeslagen in de [!DNL Schema Library]toepassing, zodat deze toegankelijk is voor de [!DNL Schema Registry]gebruiker.

Het nieuwe schema kan nu worden gebruikt om gegevens in te voeren [!DNL Platform]. Herinner dat zodra het schema is gebruikt om gegevens in te voeren, slechts de additieve veranderingen kunnen worden aangebracht. Zie de [grondbeginselen van schemacompositie](../schema/composition.md) voor meer informatie over schema versioning.

Het schema &quot;[!UICONTROL Loyalty-leden]&quot; is ook beschikbaar voor weergave en beheer met behulp van de [!DNL Schema Registry] API. Om met API te beginnen te werken, begin door de de ontwikkelaarsgids [van de Registratie van het](../api/getting-started.md)Schema te lezen.

>[!WARNING]
>
>De [!DNL Platform] UI die in de volgende video&#39;s wordt getoond is verouderd. Raadpleeg de bovenstaande documentatie voor de meest recente schermafbeeldingen en functionaliteit van de gebruikersinterface.

De volgende video laat zien hoe u een eenvoudig schema maakt in de [!DNL Platform] gebruikersinterface.

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

De volgende video is bedoeld om uw inzicht in het werken met mixins en klassen te versterken.

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## Aanhangsel

De volgende informatie is een aanvulling op de zelfstudie voor de Schema-editor.

### Een nieuwe klasse maken {#create-new-class}

[!DNL Experience Platform] biedt de flexibiliteit om een schema te definiëren dat is gebaseerd op een klasse die uniek is voor uw organisatie.

Open het dialoogvenster Klasse ** toewijzen door te klikken op **[!UICONTROL Toewijzen]** in de sectie *[!UICONTROL Klasse]* van de Schema-editor. Selecteer Nieuwe klasse ****maken in het dialoogvenster.

U kunt uw nieuwe klasse dan een Naam **[!UICONTROL van de]** Vertoning (een korte, beschrijvende, unieke, en gebruikersvriendelijke naam voor de klasse), een **[!UICONTROL Beschrijving]**, en een **[!UICONTROL Gedrag]** (&quot;[!UICONTROL Verslag]&quot; of &quot;de Reeks[!UICONTROL van de]Tijd&quot;) voor de gegevens geven het schema zal bepalen.

![Nieuwe klassedetails](../images/tutorials/create-schema/create_new_class.png)

>[!NOTE]
>
>Wanneer het bouwen van een schema dat een klasse uitvoert die door uw organisatie wordt bepaald, herinner dat de mengen voor gebruik slechts met compatibele klassen beschikbaar zijn. Aangezien de klasse die u hebt gedefinieerd nieuw is, worden er geen compatibele combinaties weergegeven in het dialoogvenster *Mixin* toevoegen. In plaats daarvan moet u Nieuwe mix **** maken selecteren en een mix definiëren voor gebruik met die klasse. De volgende keer dat u een schema samenstelt dat de nieuwe klasse implementeert, wordt de mix die u hebt gedefinieerd vermeld en beschikbaar voor gebruik.

### De klasse van een schema wijzigen {#change-class}

Op elk ogenblik tijdens het aanvankelijke proces van de schemacompositie, alvorens het schema wordt bewaard, kunt u de klasse veranderen waarop het schema wordt gebaseerd.

>[!WARNING]
>
>Wees voorzichtig voordat u de klasse wijzigt. Mixins zijn alleen compatibel met bepaalde klassen. Als u de klasse wijzigt, wordt het canvas opnieuw ingesteld en worden alle velden verwijderd die u aan dat punt hebt toegevoegd.

Als u de klasse wilt wijzigen, klikt u op **[!UICONTROL Toewijzen]** naast *[!UICONTROL Klasse]* in het gedeelte *[!UICONTROL Compositie]* van de editor.

Wanneer het dialoogvenster Klasse ** toewijzen wordt geopend, kunt u een nieuwe klasse kiezen in de beschikbare lijst. Klik op Klasse **** toewijzen en er wordt een nieuw dialoogvenster geopend waarin u wordt gevraagd te bevestigen dat u een nieuwe klasse wilt toewijzen.

![Klasse wijzigen](../images/tutorials/create-schema/assign_new_class_warning.png)

Als u de klassenwijziging bevestigt, wordt het canvas opnieuw ingesteld en gaat alle voortgang van de compositie verloren.
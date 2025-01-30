---
title: Back-ups maken van objectconfiguraties met behulp van sandboxgereedschappen
description: Als u sandboxen veilig wilt herstellen en ondersteuning voor versiebeheer wilt toevoegen, maakt u een back-up van objectconfiguraties (of metagegevens) met behulp van gereedschapspakketten van de sandbox. De reserve pakketten verhinderen het verlies van kritieke configuraties zoals schema's, datasets, en publiek, vooral tijdens ontwikkeliteraties.
exl-id: cccbaaf1-ee68-4a00-9a44-aa5db4a83a14
source-git-commit: d4df5606228347b5fb69fdaa24c637c329099895
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 0%

---

# Back-ups maken van objectconfiguraties met behulp van sandboxgereedschappen

Als u sandboxen veilig wilt herstellen en ondersteuning voor versiebeheer wilt toevoegen, maakt u een back-up van objectconfiguraties (of metagegevens) met behulp van gereedschapspakketten van de sandbox. De reserve pakketten verhinderen het verlies van kritieke configuraties zoals schema&#39;s, datasets, en publiek, vooral tijdens ontwikkeliteraties.

![ Overzicht die de voordelen van zandbak toont tooling ](../images/use-cases/tooling-overview.png){zoomable="yes"}

## Waarom dit gebruiksgeval overwegen {#why-this-use-case}

Als u een back-uppakket maakt met behulp van sandboxgereedschappen, worden de objectconfiguraties opgeslagen en beveiligd. Ontwikkelingssandboxen kunnen snel worden gevuld tijdens het experimenteren en bouwen, terwijl het maken van een volledig nieuwe sandbox na het opnieuw instellen van de sandbox tijdrovend kan zijn en ruimte voor fouten kan vrijmaken. Met de kracht van sandboxgereedschappen kunt u een back-uppakket importeren in een sandbox met nieuwe instellingen, zodat u de ideale configuraties direct kunt retourneren, zodat u verder kunt ontwikkelen.

Met back-uppakketten kunt u ook versiebeheer tijdens het gehele ontwikkelingsproces ondersteunen. Wanneer de sandbox verandert, maakt u aanvullende back-uppakketten naast de vorige pakketten, zodat u de sandbox eenvoudig kunt terugzetten naar een van uw configuraties.

## Vereisten en planning {#prerequisites-and-planning}

Wanneer u uw eigen back-uppakket binnen uw organisatie wilt maken, moet u rekening houden met de volgende voorwaarden in uw planningsproces:

- Evalueer het huidige gebruik van de sandboxen binnen uw organisatie. Zijn er niet-productiesandboxen die hun licentierechten naderen of overschrijden?
- Wat is het bereik van de metagegevens waarvan u een back-up wilt maken? Afhankelijk van uw gebruiksgeval kunt u een back-up van een volledige of gedeeltelijke sandbox maken.
- Afhankelijk van de werkingsgebiedmeta-gegevens u aan file wenst, zorg ervoor u begrijpt hoe te [ voorwerpen aan een pakket ](../ui/sandbox-tooling.md#add-object-to-a-new-package) toevoegen of hoe te [ een volledige zandbak ](../ui/sandbox-tooling.md#export-an-entire-sandbox) uitvoeren.
- Zorg ervoor dat u toegang hebt tot de sandboxgereedschappen in uw organisatie met de juiste machtigingen.

### UI-functionaliteit, platformcomponenten en Experiencen Cloud die u wilt gebruiken {#ui-functionality-and-elements}

Als u dit geval wilt gebruiken, moet u meerdere gebieden van Adobe Experience Platform gebruiken. Verzeker u de noodzakelijke [ op attributen-gebaseerde toegangsbeheertoestemmingen ](../../access-control/abac/overview.md) voor al deze gebieden hebt, of uw systeembeheerder vragen om u de noodzakelijke toestemmingen te verlenen.

- [Sandbox-tools](../ui/sandbox-tooling.md)
- [Sandboxbeheer](../ui/user-guide.md)
- [Het gebruiksdashboard voor licenties](../../landing/license-usage-and-guardrails/license-usage-dashboard.md)
- [Gegevenssets](../../catalog/datasets/overview.md)
- [Schema&#39;s](../../xdm//home.md)
- [Doelgroepen](../../segmentation/home.md)
- [ reizen van Adobe Journey Optimizer ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)

## Hoe het gebruiksgeval te bereiken: overzicht op hoog niveau {#achieve-the-use-case-high-level}

1. Bepaal het werkingsgebied van de meta-gegevens u aan steun wenst.
2. Met de sandbox-toolinggebruikersinterface kunt u de gewenste objecten exporteren naar een back-uppakket.
3. Maak regelmatig nieuwe versies van het back-uppakket om ervoor te zorgen dat de sandboxen op de huidige configuraties worden afgestemd.
4. Controleer uw huidige gebruik in het dashboard van het vergunningsgebruik tegen uw rechten voor niet productiesanddozen.
5. Niet-productie sandboxen opnieuw instellen om aan rechten te voldoen of om onnodige bronnen en gegevensopslag vrij te maken.
6. Importeer het back-uppakket in uw sandbox nadat u het opnieuw hebt ingesteld om objectconfiguraties te herstellen.

## Hoe het gebruiksgeval te bereiken: Step-by-step instructies {#step-by-step-instructions}

Lees de onderstaande secties door, die koppelingen naar verdere documentatie bevatten, om alle stappen in het bovenstaande overzicht op hoog niveau te voltooien.

### Het bereik van metagegevens definiëren

Voordat u begint met het maken van uw back-uppakket, moet u rekening houden met het gebruiksgeval van het pakket. Afhankelijk van uw behoeften, kunt u aan file een volledige zandbak willen of specifieke voorwerpen selecteren om aan uw pakket toe te voegen, zoals vermeld in [ vereisten ](#prerequisites-and-planning).

>[!NOTE]
>
> Als u overweegt het steunen van uw zandbak om het terug te stellen, ben zich bewust van de [ beperkingen ](../ui/user-guide.md#reset-a-sandbox) omringend het terugstellen zandbakken.

### De gekozen metagegevens exporteren naar een pakket

U kunt nu een back-up van uw sandbox maken via de gebruikersinterface van de sandbox met gereedschappen. In deze stap wordt zowel het maken van een back-up van een volledige sandbox als het maken van een back-up van specifieke objecten behandeld.

>[!NOTE]
>
> Niet alle objecten worden ondersteund voor gereedschappen in de sandbox. Verwijs naar de [ voorwerpen die voor zandbak tooling ](../ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling) gids voor een uitvoerige lijst van toegestane voorwerpen worden gesteund.

#### Een volledige sandbox exporteren

Aan file uw zandbak volledig, volg de [ zandbak het gebruiken gids ](../ui/sandbox-tooling.md#export-an-entire-sandbox) om een nieuw pakket tot stand te brengen en te publiceren dat de configuraties van uw volledige zandbak bevat.

#### Afzonderlijke objecten exporteren

U kunt op de volgende manieren een back-up maken van afzonderlijke objecten in een pakket. Hoewel deze hulplijnen zich richten op het toevoegen van een schema in het pakket, zijn dezelfde stappen van toepassing op andere objecten, zoals gegevenssets, doelgroepen of ritten.

- Voeg een individueel voorwerp aan een nieuw pakket toe, na zandbak tooling [ toevoegend de gids van voorwerpen ](../ui/sandbox-tooling.md#add-object-to-a-new-package).
- Voeg een individueel voorwerp aan een bestaand reservepakket toe, na de [ zandbak tooling gids ](../ui/sandbox-tooling.md#add-an-object-to-an-existing-package-and-publish), die ervoor zorgen u uw veranderingen publiceert.
- Maak een leeg pakket met meerdere objecten waaraan u objecten wilt toevoegen, volgens de onderstaande handleiding.

##### Een pakket met meerdere objecten maken

Selecteer in Experience Platform **[!UICONTROL Sandboxes]** in de linkernavigatie en selecteer vervolgens **[!UICONTROL Packages]** . Als u een nieuw pakket wilt maken, selecteert u **[!UICONTROL Create package]** in de rechterbovenhoek.

![ het pakketlusje in het zandbakendashboard met Create benadrukt pakket.](../images/use-cases/create-package.png)

Het dialoogvenster **[!UICONTROL Create package]** wordt weergegeven. Kies **[!UICONTROL Select objects]** en selecteer vervolgens **[!UICONTROL Select]** .

![ Create het vakje van de pakketdialoog met Uitgezochte voorwerpen en de Uitgezochte benadrukte optie.](../images/use-cases/create-package-select-objects.png)

Selecteer de optie **[!UICONTROL Multi-object]** . Nu moet u een naam opgeven voor het nieuwe pakket. Voer de gewenste naam in het tekstveld **[!UICONTROL Package name]** in. Selecteer **[!UICONTROL Create]** wanneer u klaar bent.

![ Create de doos van de pakketdialoog met Geselecteerd Multi-voorwerp en de pakketnaam &quot;Steun&quot;wordt ingevuld.](../images/use-cases/name-multi-object.png)

Het nieuwe pakket met meerdere objecten wordt gemaakt en is beschikbaar op het dashboard van [!UICONTROL Packages] . Selecteer het pakket in de lijst.

![ het dashboard van Pakketten met het pakket genoemd benadrukte Steun.](../images/use-cases/package-created.png)

De informatie en inhoud van het pakket worden weergegeven. Er zijn momenteel geen objecten in ons nieuwe pakket. Beginnen voorwerpen toe te voegen, volg de gids op [ toevoegend voorwerpen aan een bestaand pakket ](../ui/sandbox-tooling.md#add-object-to-a-new-package).

### Maak zo nodig nieuwe versies van het back-uppakket

Nu u het eerste back-uppakket voor uw sandbox hebt gemaakt, wilt u nieuwe versies van uw back-uppakket maken terwijl de configuratie van de sandbox wordt gewijzigd.

Hoewel het mogelijk is om nieuwe objecten toe te voegen aan uw bestaande back-uppakket, wordt u aangeraden nieuwe pakketten te maken ter ondersteuning van versioning in uw sandbox. Zo kunt u elke vorige versie van uw sandboxen eenvoudig herstellen en importeren terwijl u doorgaat met ontwikkelen.

### Je huidige gebruik controleren op basis van je licentierechten

Nu het back-uppakket gereed is, kunt u de sandbox opnieuw instellen en uw gebruik opnieuw instellen. U moet regelmatig uw gebruik controleren zodat u uw licentierechten kunt aanpassen of uw sandbox naar wens kunt herstellen. U kunt naar de [ gids van het vergunningsgebruik ](../../dashboards/guides/license-usage.md) verwijzen om meer over het dashboard van het vergunningsgebruik te leren.

### De sandbox opnieuw instellen

Op dit punt kunt u de sandbox veilig opnieuw instellen, ervan uitgaande dat de sandbox aan de vereiste parameters voldoet. Volg [ terugstellen een zandbakgids ](../ui/user-guide.md#reset-a-sandbox) beginnen opnieuw in te stellen uw zandbak, die zeker zijn om de waarschuwingslijstgevallen te lezen die u kunnen verhinderen uw zandbak opnieuw in te stellen.

### Het nieuwe back-uppakket importeren in de herstelsandbox

Nu u uw zandbak opnieuw hebt ingesteld, kunt u gebruik maken van het reservepakket u creeerde. Volg de [ zandbak tooling gids ](../ui/sandbox-tooling.md#import-a-package-to-a-target-sandbox) voor een geleidelijke proces bij het invoeren van een pakket in uw doelzandbak.

## Andere gebruiksgevallen die zijn bereikt met gereedschappen voor sandboxen: {#other-use-cases}

Verken meer gebruiksgevallen die zijn gegenereerd via gereedschappen voor sandboxen:

- [Een expertisecentrum inschakelen met behulp van sandboxgereedschappen](./center-of-excellence.md)

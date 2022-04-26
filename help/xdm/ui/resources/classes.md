---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;gegevensmodel;ui;werkruimte;klasse;klassen;
solution: Experience Platform
title: Klassen maken en bewerken in de gebruikersinterface
description: Leer hoe u klassen maakt en bewerkt in de gebruikersinterface van het Experience Platform.
topic-legacy: user guide
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: c83b5616f46f6f7d752979fa66a66fad16f16102
workflow-type: tm+mt
source-wordcount: '977'
ht-degree: 0%

---

# Klassen maken en bewerken in de gebruikersinterface

In het Model van Gegevens van de Ervaring (XDM), bepalen de klassen de gedragsaspecten van de gegevens die een schema (verslag of tijdreeks) zal bevatten. Bovendien beschrijven de klassen het kleinste aantal gemeenschappelijke eigenschappen die alle die schema&#39;s op die klasse worden gebaseerd zouden moeten omvatten en een manier verstrekken om veelvoudige compatibele datasets worden samengevoegd.

Adobe biedt verschillende standaard (&quot;core&quot;) XDM-klassen, waaronder [!DNL XDM Individual Profile] en [!DNL XDM ExperienceEvent]. Naast deze kernklassen kunt u ook uw eigen aangepaste klassen maken om specifieke gebruiksgevallen voor uw organisatie te beschrijven.

Dit document biedt een overzicht van het maken, bewerken en beheren van aangepaste klassen in de gebruikersinterface van Adobe Experience Platform.

## Vereisten

Deze handleiding vereist een goed begrip van XDM System. Zie de [XDM-overzicht](../../home.md) voor een inleiding op de rol van XDM binnen het ecosysteem van het Experience Platform, en [grondbeginselen van de schemacompositie](../../schema/composition.md) om te leren hoe de klassen tot schema&#39;s XDM bijdragen.

Hoewel dit niet nodig is voor deze handleiding, wordt u aangeraden de zelfstudie ook op te volgen [samenstellen van een schema in UI](../../tutorials/create-schema-ui.md) om de verschillende mogelijkheden van de [!DNL Schema Editor].

## Een nieuwe klasse maken {#create}

In de **[!UICONTROL Schemas]** werkruimte, selecteert u **[!UICONTROL Create schema]** selecteert u vervolgens **[!UICONTROL Browse]** in de vervolgkeuzelijst.

![](../../images/ui/resources/classes/browse-classes.png)

Er wordt een dialoogvenster weergegeven waarin u een keuze kunt maken uit een lijst met beschikbare klassen. Selecteer boven aan het dialoogvenster de optie **[!UICONTROL Create new class]**. U kunt uw nieuwe klasse dan een vertoningsnaam (een korte, beschrijvende, unieke, en gebruikersvriendelijke naam voor de klasse), een beschrijving, en een gedrag voor de gegevens geven die het schema zal bepalen (&quot;[!UICONTROL Record]&quot; of &quot;[!UICONTROL Time-series]&quot;).

Als u klaar bent, selecteert u **[!UICONTROL Assign class]**.

![](../../images/ui/resources/classes/class-details.png)

De [!DNL Schema Editor] wordt weergegeven en ziet u een nieuw schema in het canvas dat is gebaseerd op de aangepaste klasse die u zojuist hebt gemaakt. Aangezien er nog geen velden aan de klasse zijn toegevoegd, bevat het schema alleen een `_id` veld, dat de door het systeem gegenereerde unieke id vertegenwoordigt die automatisch wordt toegepast op alle bronnen in het [!DNL Schema Registry].

![](../../images/ui/resources/classes/schema.png)

>[!IMPORTANT]
>
>Wanneer het bouwen van een schema dat een klasse uitvoert die door uw organisatie wordt bepaald, herinner dat de groepen van het schemagebied voor gebruik slechts met compatibele klassen beschikbaar zijn. Aangezien de klasse die u hebt gedefinieerd nieuw is, worden er geen compatibele veldgroepen weergegeven in het dialoogvenster **[!UICONTROL Add field group]** . In plaats daarvan moet u [nieuwe veldgroepen maken](./field-groups.md#create) voor gebruik met die klasse. De volgende keer dat u een schema samenstelt dat de nieuwe klasse implementeert, worden de gedefinieerde veldgroepen weergegeven en beschikbaar voor gebruik.

U kunt nu beginnen [toevoegen van velden aan de klasse](#add-fields), die door alle schema&#39;s worden gedeeld die de klasse in dienst nemen.

## Een bestaande klasse bewerken {#edit}

>[!IMPORTANT]
>
>Aangepaste klassen die na 30 april 2022 zijn gemaakt, kunnen niet rechtstreeks worden bewerkt en er wordt momenteel een oplossing ontwikkeld. Als oplossing kunt u [een aangepaste veldgroep maken](./field-groups.md) en gebruikt deze opnieuw voor elk schema dat de aangepaste klasse gebruikt die u wilt uitbreiden. Deze beperking geldt niet voor aangepaste klassen die vóór 30 april 2022 zijn gemaakt.

>[!NOTE]
>
>Alleen aangepaste klassen die door uw organisatie zijn gedefinieerd, kunnen volledig worden bewerkt en aangepast. Voor kernklassen die door Adobe worden gedefinieerd, kunnen alleen de weergavenamen voor hun velden worden bewerkt binnen de context van afzonderlijke schema&#39;s. Zie de sectie over [weergavenamen voor schemavelden bewerken](./schemas.md#display-names) voor meer informatie.
>
>Als een aangepaste klasse eenmaal is opgeslagen en in gegevensinvoer is gebruikt, kunnen er daarna alleen aanvullende wijzigingen in worden aangebracht. Zie de [regels voor schemaontwikkeling](../../schema/composition.md#evolution) voor meer informatie .

Als u een bestaande klasse wilt bewerken, selecteert u de optie **[!UICONTROL Browse]** en selecteert u vervolgens de naam van een schema dat gebruikmaakt van de klasse die u wilt bewerken.

![](../../images/ui/resources/classes/select-for-edit.png)

>[!TIP]
>
>Met de zoek- en filtermogelijkheden van de werkruimte kunt u het schema gemakkelijker vinden. Zie de handleiding op [XDM-bronnen verkennen](../explore.md) voor meer informatie .

De [!DNL Schema Editor] verschijnt, terwijl de structuur van het schema op het canvas wordt weergegeven. U kunt nu beginnen [toevoegen van velden aan de klasse](#add-fields).

![](../../images/ui/resources/classes/edit.png)

## Velden aan een klasse toevoegen {#add-fields}

>[!IMPORTANT]
>
>Aangepaste klassen die na 30 april 2022 zijn gemaakt, kunnen niet rechtstreeks worden bewerkt en er wordt momenteel een oplossing ontwikkeld. Als oplossing kunt u [een aangepaste veldgroep maken](./field-groups.md) en gebruikt deze opnieuw voor elk schema dat de aangepaste klasse gebruikt die u wilt uitbreiden. Deze beperking geldt niet voor aangepaste klassen die vóór 30 april 2022 zijn gemaakt.

Als u een schema hebt waarin een aangepaste klasse wordt gebruikt die is geopend in het dialoogvenster [!UICONTROL Schema Editor], kunt u beginnen gebieden aan de klasse toe te voegen. Als u een nieuw veld wilt toevoegen, selecteert u de optie **plus (+)** naast de naam van het schema.

![](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>Onthoud dat alle velden die u aan een klasse toevoegt, worden gebruikt in alle schema&#39;s waarin die klasse wordt gebruikt. Daarom moet u zorgvuldig overwegen welke velden handig zijn in alle gevallen waarin het schema wordt gebruikt. Als u van plan bent een gebied toe te voegen dat slechts gebruik in sommige schema&#39;s onder deze klasse kan zien, kunt u het aan die schema&#39;s willen toevoegen door [een veldgroep maken](./field-groups.md#create) in plaats daarvan.

A **[!UICONTROL New field]** verschijnt in het canvas, en de juiste spoorupdates om controles te tonen om de eigenschappen van het gebied te vormen. Zie de handleiding op [velden definiëren in de gebruikersinterface](../fields/overview.md#define) voor specifieke stappen op om het gebied aan de klasse te vormen en toe te voegen.

Ga door met het toevoegen van zoveel velden als nodig zijn voor de klasse. Als u klaar bent, selecteert u **[!UICONTROL Save]** om zowel het schema als de klasse op te slaan.

![](../../images/ui/resources/classes/save.png)

Als u eerder schema&#39;s hebt gecreeerd die deze klasse gebruiken, zullen de onlangs toegevoegde gebieden automatisch in die schema&#39;s verschijnen.

## De klasse van een schema wijzigen {#schema}

U kunt de klasse van het schema op elk gewenst moment tijdens het eerste ontwerpproces wijzigen voordat het is opgeslagen. Zie de handleiding op [schema&#39;s maken en bewerken](./schemas.md#change-class) voor meer informatie .

## Volgende stappen

In dit document wordt beschreven hoe u klassen kunt maken en bewerken met de gebruikersinterface van het Platform. Voor meer informatie over de mogelijkheden van de [!UICONTROL Schemas] werkruimte, zie [[!UICONTROL Schemas] werkruimte - overzicht](../overview.md).

Leren hoe u klassen kunt beheren met de opdracht [!DNL Schema Registry] API, zie [hulplijn voor klassen eindpunt](../../api/classes.md).

---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;gegevensmodel;ui;werkruimte;klasse;klassen;
solution: Experience Platform
title: Klassen maken en bewerken in de gebruikersinterface
description: Leer hoe u klassen maakt en bewerkt in de gebruikersinterface van het Experience Platform.
topic: user guide
translation-type: tm+mt
source-git-commit: aa2088d30716f56ac2909214badbb39c0ae97855
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---


# Klassen maken en bewerken in de gebruikersinterface

In het Model van Gegevens van de Ervaring (XDM), bepalen de klassen de gedragsaspecten van de gegevens die een schema (verslag of tijdreeks) zal bevatten. Bovendien beschrijven de klassen het kleinste aantal gemeenschappelijke eigenschappen die alle die schema&#39;s op die klasse worden gebaseerd zouden moeten omvatten en een manier verstrekken om veelvoudige compatibele datasets worden samengevoegd.

Adobe biedt verschillende standaard (&quot;core&quot;) XDM-klassen, waaronder [!DNL XDM Individual Profile] en [!DNL XDM ExperienceEvent]. Naast deze kernklassen kunt u ook uw eigen aangepaste klassen maken om specifieke gebruiksgevallen voor uw organisatie te beschrijven.

Dit document biedt een overzicht van het maken, bewerken en beheren van aangepaste klassen in de gebruikersinterface van Adobe Experience Platform.

## Vereisten

Deze handleiding vereist een goed begrip van XDM System. Verwijs naar [XDM overzicht](../../home.md) voor een inleiding aan de rol van XDM binnen het ecosysteem van het Experience Platform, en [grondbeginselen van schemacompositie](../../schema/composition.md) om te leren hoe de klassen aan schema&#39;s bijdragen XDM.

Hoewel niet vereist voor deze gids, wordt het geadviseerd dat u het leerprogramma ook [het samenstellen van een schema in UI](../../tutorials/create-schema-ui.md) volgt om zich met de diverse mogelijkheden van [!DNL Schema Editor] vertrouwd te maken.

## Een nieuwe klasse maken {#create}

Selecteer **[!UICONTROL Schema**[!UICONTROL  Schema&#39;s ]**maken in de werkruimte en selecteer**[!UICONTROL  Bladeren ]**in het vervolgkeuzemenu.]**

![](../../images/ui/resources/classes/browse-classes.png)

Er wordt een dialoogvenster weergegeven waarin u een keuze kunt maken uit een lijst met beschikbare klassen. Selecteer **[!UICONTROL Nieuwe klasse maken]** boven in het dialoogvenster. U kunt uw nieuwe klasse dan een vertoningsnaam (een korte, beschrijvende, unieke, en gebruikersvriendelijke naam voor de klasse), een beschrijving, en een gedrag voor de gegevens geven die het schema (&quot;[!UICONTROL Verslag]&quot;of &quot;[!UICONTROL Time-series]&quot;zal bepalen).

Selecteer **[!UICONTROL Klasse toewijzen]** als u klaar bent.

![](../../images/ui/resources/classes/class-details.png)

De [!DNL Schema Editor] verschijnt, die een nieuw schema in het canvas tonen dat op de douaneklasse gebaseerd is u enkel creeerde. Aangezien er nog geen velden aan de klasse zijn toegevoegd, bevat het schema alleen een veld `_id`, dat de door het systeem gegenereerde unieke id vertegenwoordigt die automatisch wordt toegepast op alle bronnen in [!DNL Schema Registry].

![](../../images/ui/resources/classes/schema.png)

>[!IMPORTANT]
>
>Wanneer het bouwen van een schema dat een klasse uitvoert die door uw organisatie wordt bepaald, herinner dat de mengen voor gebruik slechts met compatibele klassen beschikbaar zijn. Aangezien de klasse u bepaalde nieuw is, zijn er geen compatibele mengen die in **[!UICONTROL Add worden vermeld mixin]** dialoog. In plaats daarvan moet u [nieuwe mixins](./mixins.md#create) maken voor gebruik met die klasse. De volgende keer dat u een schema samenstelt dat de nieuwe klasse uitvoert, worden de mixins die u hebt bepaald vermeld en beschikbaar voor gebruik.

U kunt nu [velden toevoegen aan de klasse](#add-fields), die wordt gedeeld door alle schema&#39;s waarin de klasse wordt gebruikt.

## Een bestaande klasse bewerken {#edit}

>[!NOTE]
>
>Alleen aangepaste klassen die door uw organisatie zijn gedefinieerd, kunnen volledig worden bewerkt en aangepast. Voor kernklassen die door Adobe worden gedefinieerd, kunnen alleen de weergavenamen voor hun velden worden bewerkt binnen de context van afzonderlijke schema&#39;s. Zie de sectie op [het uitgeven vertoningsnamen voor schemagebieden](./schemas.md#display-names) voor details.
>
>Als een aangepaste klasse eenmaal is opgeslagen en in gegevensinvoer is gebruikt, kunnen er daarna alleen aanvullende wijzigingen in worden aangebracht. Zie [regels van schemaevolutie](../../schema/composition.md#evolution) voor meer informatie.

Als u een bestaande klasse wilt bewerken, selecteert u het tabblad **[!UICONTROL Bladeren]** en selecteert u vervolgens de naam van een schema met de klasse die u wilt bewerken.

![](../../images/ui/resources/classes/select-for-edit.png)

>[!TIP]
>
>Met de zoek- en filtermogelijkheden van de werkruimte kunt u het schema gemakkelijker vinden. Zie de handleiding bij [het verkennen van XDM-bronnen](../explore.md) voor meer informatie.

De [!DNL Schema Editor] verschijnt, met de structuur van het schema die in het canvas wordt getoond. U kunt nu [velden toevoegen aan de klasse](#add-fields).

![](../../images/ui/resources/classes/edit.png)

## Velden toevoegen aan een klasse {#add-fields}

Als u een schema hebt waarin een aangepaste klasse wordt gebruikt die is geopend in de [!UICONTROL Schema-editor], kunt u beginnen met het toevoegen van velden aan de klasse. Als u een nieuw veld wilt toevoegen, selecteert u het **plus-pictogram (+)** naast de naam van het schema.

![](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>Onthoud dat alle velden die u aan een klasse toevoegt, worden gebruikt in alle schema&#39;s waarin die klasse wordt gebruikt. Daarom moet u zorgvuldig overwegen welke velden handig zijn in alle gevallen waarin het schema wordt gebruikt. Als u overweegt om een gebied toe te voegen dat slechts gebruik in sommige schema&#39;s onder deze klasse kan zien, kunt u het aan die schema&#39;s door [in plaats daarvan tot een mixin](./mixins.md#create) kunnen willen toevoegen.

Er verschijnt een **[!UICONTROL Nieuw veld]** op het canvas en de juiste updates per spoor om besturingselementen weer te geven waarmee de eigenschappen van het veld worden geconfigureerd. Zie de gids op [het bepalen van gebieden in UI](../fields/overview.md#define) voor specifieke stappen op om het gebied aan de klasse te vormen en toe te voegen.

Ga door met het toevoegen van zoveel velden als nodig zijn voor de klasse. Als u klaar bent, selecteert u **[!UICONTROL Opslaan]** om zowel het schema als de klasse op te slaan.

![](../../images/ui/resources/classes/save.png)

Als u eerder schema&#39;s hebt gecreeerd die deze klasse gebruiken, zullen de onlangs toegevoegde gebieden automatisch in die schema&#39;s verschijnen.

## De klasse van een schema wijzigen {#schema}

U kunt de klasse van het schema op elk gewenst moment tijdens het eerste ontwerpproces wijzigen voordat het is opgeslagen. Zie de handleiding bij [Schema&#39;s maken en bewerken](./schemas.md#change-class) voor meer informatie.

## Volgende stappen

In dit document wordt beschreven hoe u klassen kunt maken en bewerken met de gebruikersinterface van het Platform. Voor meer informatie over de mogelijkheden van de [!UICONTROL Schemas] werkruimte, zie [[!UICONTROL Schemas] werkruimteoverzicht](../overview.md).

Meer informatie over het beheren van klassen met de [!DNL Schema Registry] API vindt u in de [gids voor het eindpunt van klassen](../../api/classes.md).
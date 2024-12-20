---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;gegevensmodel;ui;werkruimte;identity;field;
solution: Experience Platform
title: Identiteitsvelden definiëren in de gebruikersinterface
description: Leer hoe u een identiteitsveld definieert in de gebruikersinterface van het Experience Platform.
exl-id: 11a53345-4c3f-4537-b3eb-ee7a5952df2a
source-git-commit: 6020f1c294f123cbf57629405128580efc5642ec
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 0%

---

# Identiteitsvelden definiëren in de gebruikersinterface

In het Model van Gegevens van de Ervaring (XDM), vertegenwoordigt een identiteitsgebied een gebied dat kan worden gebruikt om een individuele persoon te identificeren met betrekking tot een verslag of een tijd-reeksgebeurtenis. In dit document wordt beschreven hoe u een identiteitsveld definieert in de gebruikersinterface van Adobe Experience Platform.

## Vereisten

Identiteitsvelden zijn een cruciale component in de manier waarop identiteitsgrafieken van klanten worden samengesteld in Platform. Dit beïnvloedt uiteindelijk de manier waarop in realtime-klantprofiel afzonderlijke gegevensfragmenten worden samengevoegd om een volledig beeld van de klant te krijgen. Voordat u identiteitsvelden in uw schema&#39;s definieert, raadpleegt u de volgende documentatie voor meer informatie over de belangrijkste services en concepten met betrekking tot identiteitsvelden:

* [ Dienst van de Identiteit van Adobe Experience Platform ](../../../identity-service/home.md): Brugshanden identiteiten over apparaten en systemen, die datasets verbinden samen op de identiteitsgebieden worden gebaseerd die door de schema&#39;s XDM worden bepaald zij met in overeenstemming zijn.
   * [ Identiteit namespaces ](../../../identity-service/features/namespaces.md): Identiteitsnaamruimten bepalen de verschillende soorten identiteitsinformatie die op één enkele persoon kunnen betrekking hebben, en een vereiste component voor elk identiteitsgebied zijn.
* [ Real-Time Profiel van de Klant ](../../../profile/home.md): De grafieken van de klantenidentiteit van hefboomwerkingen om een verenigd consumentenprofiel te verstrekken dat op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd, die in dichtbij-real-time wordt bijgewerkt.

## Een identiteitsveld definiëren {#define-a-identity-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_identityField_primaryIdentityRestriction"
>title="Beperkingen van de primaire identiteit"
>abstract="In dit schema wordt een veldgroep gebruikt die is bedoeld voor gebruik in een specifieke bronverbinding. Voor de verbinding moet identityMap worden gebruikt als primaire identiteit en automatisch worden ingesteld."

Wanneer [ het bepalen van een nieuw gebied ](./overview.md#define) in UI, kunt u het als identiteitsgebied plaatsen door **[!UICONTROL Identity]** checkbox in het juiste spoor te selecteren.

![](../../images/ui/fields/special/identity.png)

Aanvullende besturingselementen worden weergegeven nadat u het selectievakje hebt ingeschakeld. Als u wilt dat dit veld de primaire identiteit voor het schema is, schakelt u het selectievakje **[!UICONTROL Primary identity]** in.

>[!NOTE]
>
>Voor één schema kunnen veel identiteitsvelden zijn gedefinieerd, maar dit schema kan slechts één primaire identiteit hebben. Alle identiteitsgebieden (primair of anders) dragen aan de identiteitsgrafiek voor een individuele klant bij, maar het Profiel van de Klant in real time gebruikt slechts de primaire identiteit als bron van waarheid wanneer het samenvoegen van gegevensfragmenten samen. Als u een schema voor gebruik in Profiel wilt toelaten, moet het schema een primaire bepaalde identiteit hebben.

Gebruik onder **[!UICONTROL Identity namespace]** het vervolgkeuzemenu om de juiste naamruimte voor het naamveld te selecteren. De standaardnaamruimten die door de Adobe worden verschaft, worden samen met aangepaste naamruimten weergegeven die door uw organisatie zijn gedefinieerd.

Als u klaar bent, selecteert u **[!UICONTROL Apply]** om de wijziging toe te passen op het schema.

![](../../images/ui/fields/special/identity-config.png)

Het canvas wordt bijgewerkt met de wijzigingen, waarbij het geselecteerde veld een vingerafdruksymbool (![](/help/images/icons/identity-service.png)) krijgt om het aan te duiden als een identiteit. In het linkerspoor, is het identiteitsgebied nu vermeld onder de naam van de klasse of de groep van het schemagebied die het gebied aan het schema verstrekt.

Als het veld ook als primaire identiteit is ingesteld, wordt het veld ook in de linkertrack onder **[!UICONTROL Required fields]** vermeld. Als het identiteitsveld is genest binnen de schemastructuur, worden alle bovenliggende velden ook vermeld zoals vereist.

![](../../images/ui/fields/special/identity-applied.png)

Als u een primaire identiteit voor het schema bepaalde, kunt u nu te werk gaan [ het schema voor gebruik in het Profiel van de Klant in real time ](../resources/schemas.md#profile) toelaten.

## Volgende stappen

Deze gids besprak hoe te om een identiteitsgebied in UI te bepalen. Aangezien het gegeven gebruikend dit schema wordt opgenomen, zullen de grafieken van uw klantenidentiteit worden bijgewerkt om op de de identiteitsgebieden van het schema te wijzen. Zie de gids op de [ kijker van de identiteitsgrafiek ](../../../identity-service/features/identity-graph-viewer.md) leren hoe te om de privé grafiek van uw organisatie in UI te onderzoeken.

Zie het overzicht op [ bepalende gebieden in UI ](./overview.md#special) leren hoe te om andere XDM gebiedstypes in [!DNL Schema Editor] te bepalen.


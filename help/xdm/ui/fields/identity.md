---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;gegevensmodel;ui;werkruimte;identity;field;
solution: Experience Platform
title: Identiteitsvelden definiëren in de gebruikersinterface
description: Leer hoe u een identiteitsveld definieert in de gebruikersinterface van het Experience Platform.
exl-id: 11a53345-4c3f-4537-b3eb-ee7a5952df2a
source-git-commit: 857c1d4f74b6352e90f9c97ef22d686a883e3563
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---

# Identiteitsvelden definiëren in de gebruikersinterface

In het Model van Gegevens van de Ervaring (XDM), vertegenwoordigt een identiteitsgebied een gebied dat kan worden gebruikt om een individuele persoon te identificeren met betrekking tot een verslag of een tijd-reeksgebeurtenis. In dit document wordt beschreven hoe u een identiteitsveld definieert in de gebruikersinterface van Adobe Experience Platform.

## Vereisten

Identiteitsvelden vormen een cruciaal onderdeel van de manier waarop identiteitsgrafieken van klanten in Platform worden samengesteld. Dit beïnvloedt uiteindelijk de manier waarop in Real-Time Customer Profile verschillende gegevensfragmenten worden samengevoegd om een volledig beeld van de klant te krijgen. Voordat u identiteitsvelden in uw schema&#39;s definieert, raadpleegt u de volgende documentatie voor informatie over de belangrijkste services en concepten met betrekking tot identiteitsvelden:

* [Adobe Experience Platform Identity Service](../../../identity-service/home.md): Bruggen identiteiten over apparaten en systemen, die datasets verbinden samen op de identiteitsgebieden worden bepaald die door de schema&#39;s XDM worden bepaald zij met in overeenstemming zijn.
   * [Identiteitsnaamruimten](../../../identity-service/namespaces.md): Naamruimten definiëren de verschillende typen identiteitsgegevens die betrekking kunnen hebben op één persoon en die een vereiste component zijn voor elk identiteitsveld.
* [Klantprofiel in realtime](../../../profile/home.md): Gebruikt de grafieken van de klantenidentiteit van hefboomwerkingen om een verenigd consumentenprofiel te verstrekken dat op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd, die in bijna-real-time wordt bijgewerkt.

## Een identiteitsveld definiëren {#define-a-identity-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_identityField_primaryIdentityRestriction"
>title="Beperkingen van de primaire identiteit"
>abstract="In dit schema wordt een veldgroep gebruikt die is bedoeld voor gebruik in een specifieke bronverbinding. Voor de verbinding moet identityMap worden gebruikt als primaire identiteit en automatisch worden ingesteld."

Wanneer [een nieuw veld definiëren](./overview.md#define) in UI, kunt u het als identiteitsgebied plaatsen door te selecteren **[!UICONTROL Identity]** selectievakje in de rechterspoorstaaf.

![](../../images/ui/fields/special/identity.png)

Aanvullende besturingselementen worden weergegeven nadat u het selectievakje hebt ingeschakeld. Als u wilt dat dit veld de primaire identiteit voor het schema is, selecteert u de optie **[!UICONTROL Primary identity]** selectievakje.

>[!NOTE]
>
>Voor één schema kunnen veel identiteitsvelden zijn gedefinieerd, maar dit schema kan slechts één primaire identiteit hebben. Alle identiteitsgebieden (primair of anders) dragen aan de identiteitsgrafiek voor een individuele klant bij, maar het Profiel van de Klant in real time gebruikt slechts de primaire identiteit als bron van waarheid wanneer het samenvoegen van gegevensfragmenten samen. Als u een schema voor gebruik in Profiel wilt toelaten, moet het schema een primaire bepaalde identiteit hebben.

Onder **[!UICONTROL Identity namespace]** gebruikt u het vervolgkeuzemenu om de juiste naamruimte voor het naamveld te selecteren. De standaardnaamruimten die door Adobe worden verschaft, worden weergegeven samen met aangepaste naamruimten die door uw organisatie zijn gedefinieerd.

Als u klaar bent, selecteert u **[!UICONTROL Apply]** om de wijziging op het schema toe te passen.

![](../../images/ui/fields/special/identity-config.png)

Het canvas wordt bijgewerkt met de wijzigingen, waarbij het geselecteerde veld een vingerafdruksymbool krijgt (![](../../images/ui/fields/special/identity-symbol.png)) om het als een identiteit aan te wijzen. In het linkerspoor, is het identiteitsgebied nu vermeld onder de naam van de klasse of de groep van het schemagebied die het gebied aan het schema verstrekt.

Als het veld ook is ingesteld als primaire identiteit, wordt het ook onder **[!UICONTROL Required fields]** in het linkerspoor. Als het identiteitsveld is genest binnen de schemastructuur, worden alle bovenliggende velden ook vermeld zoals vereist.

![](../../images/ui/fields/special/identity-applied.png)

Als u een primaire identiteit voor het schema hebt gedefinieerd, kunt u nu doorgaan naar [laat het schema voor gebruik in het Profiel van de Klant in real time toe](../resources/schemas.md#profile).

## Volgende stappen

Deze gids besprak hoe te om een identiteitsgebied in UI te bepalen. Aangezien het gegeven gebruikend dit schema wordt opgenomen, zullen de grafieken van uw klantenidentiteit worden bijgewerkt om op de de identiteitsgebieden van het schema te wijzen. Zie de handleiding op de [identiteitsgrafiekviewer](../../../identity-service/ui/identity-graph-viewer.md) om te leren hoe u de persoonlijke grafiek van uw organisatie kunt verkennen in de gebruikersinterface.

Zie het overzicht op [velden definiëren in de gebruikersinterface](./overview.md#special) leren hoe u andere XDM-veldtypen definieert in het dialoogvenster [!DNL Schema Editor].

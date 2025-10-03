---
title: Kaartvelden definiëren in de gebruikersinterface
description: Leer hoe u een kaartveld definieert in de Experience Platform-gebruikersinterface.
exl-id: 657428a2-f184-4d7c-b657-4fc60d77d5c6
source-git-commit: c0421974493884488e4d639278106835ad1d8b1b
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# Kaartvelden definiëren in de gebruikersinterface

Adobe Experience Platform staat u toe om de structuur van uw klassen van het Model van de Gegevens van de Ervaring (XDM), schema gebiedsgroepen, en gegevenstypes volledig aan te passen.

U kunt kaartgebieden in de Redacteur van het Schema ook bepalen om een inzameling van zeer belangrijk-waardeparen met flexibele, dynamische sleutels op te slaan.

Wanneer u een nieuw veld in de gebruikersinterface van Experience Platform (UI) definieert, gebruikt u het vervolgkeuzemenu **[!UICONTROL Type]** en selecteert u &quot;**[!UICONTROL Map]**&quot; in de lijst.

![ de Redacteur van Schema&#39;s met het Type dropdown en benadrukte waarde van de Kaart.](../../images/ui/fields/special/map.png)

Er wordt een eigenschap [!UICONTROL Map value type] weergegeven. Deze waarde is vereist voor [!UICONTROL Map] -gegevenstypen. Beschikbare waarden voor de kaart zijn [!UICONTROL String] en [!UICONTROL Integer] . Selecteer een waarde in de vervolgkeuzelijst met beschikbare opties.

![ de Redacteur van Schema met [!UICONTROL Map value type] benadrukt dropdown.](../../images/ui/fields/special/map-value-type.png)

Nadat u het subveld hebt geconfigureerd, moet u het aan een veldgroep toewijzen. Gebruik de vervolgkeuzelijst **[!UICONTROL Field Group]** of het zoekveld en selecteer **[!UICONTROL Apply]** . U kunt velden aan het object blijven toevoegen met hetzelfde proces of u kunt **[!UICONTROL Save]** selecteren om uw instellingen te bevestigen.

![ een opname van de selectie van de gebiedsgroep en montages die worden toegepast.](../../images/ui/fields/special/assign-to-field-group.gif)

## Gebruiksbeperkingen {#restrictions}

XDM plaatst de volgende beperkingen op het gebruik van dit gegevenstype:

* Kaarttypen MOETEN van het type `object` zijn.
* Voor typen toewijzingen MOET GEEN eigenschap zijn gedefinieerd (met andere woorden, ze definiëren &quot;lege&quot; objecten).
* Kaarttypen MOETEN een `additionalProperties.type` -veld bevatten dat de waarden beschrijft die binnen de kaart kunnen worden geplaatst, `string` of `integer` .
* Segmentatie tussen meerdere entiteiten kan alleen worden gedefinieerd op basis van de kaarttoetsen en niet op basis van de waarden.
* Kaarten worden niet ondersteund voor accountpubliek.
* Kaarten die zijn gedefinieerd in aangepaste XDM-objecten, zijn beperkt tot één niveau. Geneste kaarten kunnen niet worden gemaakt. Deze beperking geldt niet voor kaarten die zijn gedefinieerd in standaard XDM-objecten.
* Arrays met kaarten worden niet ondersteund.

Zorg ervoor dat u kaart-type gebieden wanneer absoluut noodzakelijk slechts gebruikt, aangezien zij de volgende prestatiesnadelen dragen:

* De tijd van de reactie van [ de Dienst van de Vraag van Adobe Experience Platform ](../../../query-service/home.md) degradeert van drie seconden aan tien seconden voor 100 miljoen verslagen.
* Kaarten moeten minder dan 16 sleutels hebben of anders risico op verdere afbraak.

>[!NOTE]
>
>De gebruikersinterface van Experience Platform kent beperkingen in de manier waarop de sleutels van kaartvelden kunnen worden geëxtraheerd. Terwijl objecttekstvelden kunnen worden uitgebreid, worden kaarten als één veld weergegeven. De gebieden van de kaart die door de Registratie API van het Schema worden gecreeerd die geen koord of geheel gegevenstypes zijn worden getoond als &quot;[!UICONTROL Complex]&quot;gegevenstypes die.

## Volgende stappen

Nadat u dit document hebt gelezen, kunt u nu kaartvelden definiëren in de gebruikersinterface van Experience Platform. U kunt alleen klassen en veldgroepen gebruiken om velden aan schema&#39;s toe te voegen. Meer over leren hoe te om deze middelen in UI te beheren, zie de gidsen bij het creëren van en het uitgeven van [ klassen ](../resources/classes.md) en [ gebiedsgroepen ](../resources/field-groups.md).

Voor meer informatie over de mogelijkheden van de [!UICONTROL Schemas] werkruimte, zie het [[!UICONTROL Schemas] overzicht van de werkruimte ](../overview.md).

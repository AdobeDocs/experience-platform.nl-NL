---
title: Kaartvelden definiëren in de gebruikersinterface
description: Leer hoe u een kaartveld definieert in de gebruikersinterface van het Experience Platform.
exl-id: 657428a2-f184-4d7c-b657-4fc60d77d5c6
source-git-commit: ee27fc42a1ee23ef650d320df64e5970a84d0d38
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# Kaartvelden definiëren in de gebruikersinterface

Adobe Experience Platform staat u toe om de structuur van uw klassen van het Model van de Gegevens van de Ervaring (XDM), schema gebiedsgroepen, en gegevenstypes volledig aan te passen.

U kunt kaartgebieden in de Redacteur van het Schema ook bepalen om flexibele en dynamische gegevensstructuren te modelleren of een inzameling van sleutel-waardeparen op te slaan.

Wanneer u een nieuw veld in de gebruikersinterface van het platform (UI) definieert, gebruikt u de **[!UICONTROL Type]** vervolgkeuzelijst en selecteer &quot;**[!UICONTROL Map]**&quot; in de lijst.

![De Schema-editor met het vervolgkeuzemenu Type en de waarde Kaart gemarkeerd.](../../images/ui/fields/special/map.png)

A [!UICONTROL Map value type] wordt weergegeven. Deze waarde is vereist voor [!UICONTROL Map] gegevenstypen. Beschikbare waarden voor de kaart zijn: [!UICONTROL String] en [!UICONTROL Integer]. Selecteer een waarde in de vervolgkeuzelijst met beschikbare opties.

![De Schemas Editor met de [!UICONTROL Map value type] vervolgkeuzelijst gemarkeerd.](../../images/ui/fields/special/map-value-type.png)

Nadat u het subveld hebt geconfigureerd, moet u het aan een veldgroep toewijzen. Gebruik de **[!UICONTROL Field Group]** vervolgkeuzemenu, of zoekveld, en selecteer **[!UICONTROL Apply]**. U kunt velden aan het object blijven toevoegen met hetzelfde proces of **[!UICONTROL Save]** om uw instellingen te bevestigen.

![Een opname van de selectie van de veldgroep en de instellingen die worden toegepast.](../../images/ui/fields/special/assign-to-field-group.gif)

## Gebruiksbeperkingen {#restrictions}

XDM plaatst de volgende beperkingen op het gebruik van dit gegevenstype:

* Type kaart MOET van het type zijn `object`.
* Voor typen toewijzingen MOET GEEN eigenschap zijn gedefinieerd (met andere woorden, ze definiëren &quot;lege&quot; objecten).
* Kaarttypen MOETEN een `additionalProperties.type` veld dat de waarden beschrijft die binnen de kaart kunnen worden geplaatst, of `string` of `integer`.
* Segmentatie tussen meerdere entiteiten kan alleen worden gedefinieerd op basis van de kaarttoetsen en niet op basis van de waarden.
* Kaarten worden niet ondersteund voor accountpubliek.

Zorg ervoor dat u kaart-type gebieden wanneer absoluut noodzakelijk slechts gebruikt, aangezien zij de volgende prestatiesnadelen dragen:

* Responstijd van [Adobe Experience Platform Query Service](../../../query-service/home.md) degradeert van drie seconden tot tien seconden voor 100 miljoen verslagen.
* Kaarten moeten minder dan 16 sleutels hebben of anders risico op verdere afbraak.

>[!NOTE]
>
>De interface van het platform heeft beperkingen in hoe het de sleutels van kaart-type gebieden kan halen. Terwijl objecttekstvelden kunnen worden uitgebreid, worden kaarten als één veld weergegeven. De gebieden van de kaart die door de Registratie API van het Schema worden gecreeerd die geen koord of geheel gegevenstypes zijn worden getoond zoals &quot;[!UICONTROL Complex]&quot;gegevenstypen.

## Volgende stappen

Nadat u dit document hebt gelezen, kunt u nu kaartvelden definiëren in de interface van het platform. U kunt alleen klassen en veldgroepen gebruiken om velden aan schema&#39;s toe te voegen. Raadpleeg de handleidingen bij het maken en bewerken van deze bronnen voor meer informatie over het beheren van deze bronnen in de gebruikersinterface [klassen](../resources/classes.md) en [veldgroepen](../resources/field-groups.md).

Voor meer informatie over de mogelijkheden van de [!UICONTROL Schemas] werkruimte, zie de [[!UICONTROL Schemas] werkruimte - overzicht](../overview.md).

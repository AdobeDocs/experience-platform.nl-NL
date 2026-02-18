---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;gegevensmodel;ui;werkruimte;enum;field;
solution: Experience Platform
title: Enum Fields en voorgestelde waarden in UI bepalen
description: Leer hoe u opsommingen en voorgestelde waarden voor tekenreeksvelden definieert in de Experience Platform-gebruikersinterface.
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1222'
ht-degree: 0%

---

# Opsommingen en voorgestelde waarden definiëren in de gebruikersinterface {#enums-and-suggested-values}

>[!CONTEXTUALHELP]
>id="platform_xdm_enum_suggestedvalue"
>title="Opsommingen en voorgestelde waarden"
>abstract="An **Enum** beperkt een koordgebied om slechts gegevens toe te staan die een vooraf bepaalde reeks te nemen waarden aanpassen. Elke enumbeperking kan a **naam van de Vertoning** worden toegewezen die kenmerkdropdowns in de Segmentatie UI bevolkt. **voorgestelde waarden** voor een gebied beperken geen opname en bepalen slechts de vertoningsnamen die in Segmentatie worden getoond. Als u veelvoudige schema&#39;s hebt die een gebied delen dat tot een gemeenschappelijke klasse of een gebiedsgroep behoort, en u verschillende aantallen of voorgestelde waarden voor dat gebied tussen elk schema bepaalt, worden die waarden samengevoegd en toegevoegd in het unieschema."

In het Model van Gegevens van de Ervaring (XDM), kan een koordgebied een vooraf bepaalde reeks toegelaten of voorgestelde waarden worden gegeven om beter te controleren welke waarden in dat gebied worden opgenomen of hoe het in segmentatie zal gedragen.

**[!UICONTROL Enums]** beperkt de waarden die voor een tekenreeksveld kunnen worden ingevoerd tot een vooraf gedefinieerde set. Als u probeert gegevens in te voeren in een opsommingsveld en de waarde niet overeenkomt met een van de gedefinieerde waarden in de configuratie, wordt invoer geweigerd.

In tegenstelling tot opsommingen, staat de **[!UICONTROL Suggested values]** optie toe om een reeks geadviseerde waarden voor een koordgebied te wijzen dat niet de waarden beperkt die het kan opnemen. In plaats daarvan, beïnvloeden de voorgestelde waarden welke vooraf bepaalde waarden in [&#x200B; Segmentatie UI &#x200B;](../../../segmentation/ui/overview.md) beschikbaar zijn wanneer het omvatten van het koordgebied als attribuut.

Wanneer [&#x200B; het bepalen van een nieuw gebied &#x200B;](./overview.md#define) in het gebruikersinterface van Adobe Experience Platform en het plaatsen van het type aan [!UICONTROL String], wordt u gegeven de optie om een [&#x200B; enum &#x200B;](#enum) of [&#x200B; gesuggereerde waarden &#x200B;](#suggested-values) voor dat gebied te bepalen.

![&#x200B; Beeld dat Enum &amp; de Voorgestelde optie van Waarden toont die voor een koordgebied in UI wordt toegelaten &#x200B;](../../images/ui/fields/enum/enum-options-selected.png)

In dit document wordt beschreven hoe u opsommingen en voorgestelde waarden definieert in de gebruikersinterface van [!UICONTROL Schemas] . Bekijk de volgende video voor een snel overzicht van opsommingen en voorgestelde waarden, inclusief hoe u deze kunt configureren in de gebruikersinterface en de bijbehorende downstreameffecten:

>[!VIDEO](https://video.tv.adobe.com/v/3409501/?quality=12&learn=on)

## Een opsomming definiëren {#enum}

Selecteer **[!UICONTROL Enums and Suggested Values]** en selecteer vervolgens **[!UICONTROL Enums]** . Er worden extra besturingselementen weergegeven, zodat u de waardebeperkingen voor de opsomming kunt opgeven. Selecteer **[!UICONTROL Add row]** als u een restrictie wilt toevoegen.

![&#x200B; Beeld dat de optie van Enums toont die in UI wordt geselecteerd &#x200B;](../../images/ui/fields/enum/enum-add-row.png)

Onder de kolom **[!UICONTROL Value]** moet u de exacte waarde opgeven waarnaar u het veld wilt beperken. U kunt optioneel ook een gebruiksvriendelijke **[!UICONTROL Display Name]** versie van de beperking opgeven, die bepaalt hoe de waarde in de segmentatie wordt weergegeven.

Ga verder om **[!UICONTROL Add row]** te gebruiken om de gewenste beperkingen en facultatieve etiketten aan de opsomming toe te voegen, of het schrappingspictogram (![&#x200B; Beeld van het schrappingspictogram &#x200B;](/help/images/icons/remove-circle.png)) naast een eerder toegevoegde rij te selecteren om het te verwijderen. Als u klaar bent, selecteert u **[!UICONTROL Apply]** om de wijzigingen toe te passen op het schema.

![&#x200B; Beeld dat de opsommingswaarden en vertoningsnamen toont die voor het koordgebied in UI worden gevuld &#x200B;](../../images/ui/fields/enum/enum-confirm.png)

Het canvas wordt bijgewerkt met de wijzigingen. Wanneer u dit schema in de toekomst verkent, kunt u de beperkingen voor het enum gebied binnen het juiste spoor bekijken en uitgeven.

## Voorgestelde waarden definiëren {#suggested-values}

Selecteer **[!UICONTROL Enums and Suggested Values]** en selecteer vervolgens **[!UICONTROL Suggested Values]** om extra besturingselementen weer te geven. Selecteer van hieruit **[!UICONTROL Add row]** om voorgestelde waarden toe te voegen.

![&#x200B; Beeld dat de Voorgestelde optie van Waarden toont die in UI wordt geselecteerd &#x200B;](../../images/ui/fields/enum/suggested-add-row.png)

Geef onder de kolom **[!UICONTROL Display Name]** een mensvriendelijke naam voor de waarde op zoals u deze wilt weergeven in de segmenteringsinterface. Als u meer gesuggereerde waarden wilt toevoegen, selecteert u **[!UICONTROL Add row]** nogmaals en herhaalt u zo nodig het proces. Om een eerder toegevoegde rij te verwijderen, selecteer ![&#x200B; het schrappingspictogram &#x200B;](/help/images/icons/remove-circle.png) naast de rij in kwestie.

Als u klaar bent, selecteert u **[!UICONTROL Apply]** om de wijzigingen toe te passen op het schema.

![&#x200B; Beeld dat de opsommingswaarden en vertoningsnamen toont die voor het koordgebied in UI worden gevuld &#x200B;](../../images/ui/fields/enum/suggested-confirm.png)

>[!NOTE]
>
>Er is een ongeveer vijf-minieme vertraging voor de bijgewerkte voorgestelde waarden van een gebied om in de Segmentatie UI worden weerspiegeld.

### Voorgestelde waarden voor standaardvelden beheren

Sommige gebieden van standaardXDM componenten bevatten hun eigen gesuggereerde waarden, zoals `eventType` van de [[!UICONTROL XDM ExperienceEvent] klasse &#x200B;](../../classes/experienceevent.md). Hoewel u aanvullende voorgestelde waarden voor een standaardveld kunt maken, kunt u voorgestelde waarden die niet door uw organisatie zijn gedefinieerd, niet wijzigen of verwijderen. Als u een standaardveld in de gebruikersinterface weergeeft, worden de voorgestelde waarden weergegeven, maar alleen-lezen.

![&#x200B; Beeld dat de opsommingswaarden en vertoningsnamen toont die voor het koordgebied in UI worden gevuld &#x200B;](../../images/ui/fields/enum/suggested-standard.png)

Selecteer **[!UICONTROL Add row]** als u nieuwe voorgestelde waarden voor een standaardveld wilt toevoegen. Om een gesuggereerde waarde te verwijderen die eerder door uw organisatie werd toegevoegd, selecteer ![&#x200B; het schrappingspictogram &#x200B;](/help/images/icons/remove-circle.png) naast de rij in kwestie.

![&#x200B; Beeld dat de opsommingswaarden en vertoningsnamen toont die voor het koordgebied in UI worden gevuld &#x200B;](../../images/ui/fields/enum/suggested-standard-add.png)

<!-- ### Removing suggested values for standard fields

Only suggested values that you define can be removed from a standard field. Existing suggested values can be disabled so that they no longer appear in the segmentation dropdown, but they cannot be removed outright.

For example, consider a profile schema where the a suggested value for the standard `person.gender` field is disabled:

![Image showing the enum values and display names filled out for the string field in the UI](../../images/ui/fields/enum/standard-enum-disabled.png)

In this example, the display name "[!UICONTROL Non-specific]" is now disabled from being shown in the segmentation dropdown list. However, the value `non_specific` is still part of the list of enumerated fields and is therefore still allowed on ingestion. In other words, you cannot disable the actual enum value for the standard field as it would go against the principle of only allowing changes that make a field less restrictive.

See the [section below](#evolution) for more information on the rules for updating enums and suggested values for existing schema fields. -->

## Evolutieregels voor opsommingen en voorgestelde waarden {#evolution}

Nadat een schema met een enum gebied is gebruikt om gegevens in Experience Platform in te voeren, moeten om het even welke verdere veranderingen die in de schemadefinitie worden aangebracht aan de gegevens voldoen reeds in het systeem. In het algemeen, kunnen de veranderingen die aan een bestaand gebied worden aangebracht slechts dat gebied **minder** restrictief maken. Een veld kan niet restrictiever worden gemaakt dan het al is.

Wanneer het over aantallen en voorgestelde waarden aankomt, zijn de volgende regels post-ingesetion van toepassing:

* U **KUNT** voorgestelde waarden voor standaard en douanevelden met bestaande voorgestelde waarden toevoegen.
* U **KUNT** voorgestelde waarden uit douanegebieden met bestaande voorgestelde waarden verwijderen.
* U **KUNT** nieuwe opsommingswaarden voor een bestaand gebied van het douanenum toevoegen.
* U **KUNT** schakelaar de enum waarden van een douanegebied aan gesuggereerde waarden slechts, of het in een koord zonder opsomming of voorgestelde waarden omzetten. **deze schakelaar kan niet worden ongedaan gemaakt zodra toegepast.**
* U **KAN** lijsten of gesuggereerde waarden van standaardgebieden NIET verwijderen.
* U **KAN** enumwaarden aan een gebied zonder bestaand enum NIET toevoegen.
* U **KAN** minder dan alle bestaande enumwaarden voor een douanegebied NIET verwijderen.
* U **KAN** schakelaar van voorgestelde waarden aan een opsomming NIET.

## Regels samenvoegen voor opsommingen en voorgestelde waarden {#merging}

Als de veelvoudige schema&#39;s het zelfde enum gebied met verschillende configuraties gebruiken, en die schema&#39;s inbegrepen in een unie zijn, zijn bepaalde regels van toepassing wanneer het over hoe de enum verschillen met elkaar in overeenstemming worden gebracht. De exacte regels zijn afhankelijk van het feit of de schema&#39;s verwijzen naar hetzelfde standaardveld (zoals `eventType` ) of dat er wordt verwezen naar hetzelfde aangepaste veldpad in verschillende veldgroepen.

Bij verwijzing naar hetzelfde standaardveld:

* Om het even welke extra voorgestelde waarden worden **TOEGEVOEGD** in de unie.
* De updates die aan de voorgestelde waarden voor de zelfde enum sleutel worden gemaakt zijn **BIJGEWERKT** in de unie.

Als in verschillende veldgroepen wordt verwezen naar hetzelfde aangepaste veldpad:

* Om het even welke extra voorgestelde waarden worden **TOEGEVOEGD** in de unie.
* Als de zelfde extra gesuggereerde waarde in meer dan één schema wordt bepaald, zijn die waarden **GEMERGED** in de unie. Met andere woorden, dezelfde voorgestelde waarde wordt niet twee keer na het samenvoegen weergegeven.

## Beperkingen voor validatie

Vanwege de huidige systeembeperkingen zijn er twee gevallen waarin een enum niet door het systeem wordt gevalideerd tijdens inname:

1. Het enum wordt bepaald op een [&#x200B; seriegebied &#x200B;](./array.md).
1. De opsomming wordt meer dan één niveau diep gedefinieerd in de schemahiërarchie.

## Volgende stappen

In deze handleiding wordt beschreven hoe u opsommingen en voorgestelde waarden voor tekenreeksvelden in de gebruikersinterface definieert. Voor informatie over hoe te om lijsten en voorgestelde waarden te beheren gebruikend de Registratie API van het Schema, verwijs naar het volgende [&#x200B; leerprogramma &#x200B;](../../tutorials/suggested-values.md).

Leren hoe te om andere XDM gebiedstypes in [!DNL Schema Editor] te bepalen, zie het overzicht op [&#x200B; bepalend gebieden in UI &#x200B;](./overview.md#special).

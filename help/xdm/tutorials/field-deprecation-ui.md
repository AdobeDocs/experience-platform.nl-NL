---
title: Een XDM-veld in de gebruikersinterface verwijderen
description: Leer hoe te om de gebieden van de Gegevens van de Ervaring van het Model (XDM) te verwerpen gebruikend de Redacteur van het Schema binnen Experience Platform.
exl-id: f4c5f58a-5190-47d7-8bfc-b33ed238bf25
source-git-commit: 4fa98df9dcc296ba7cb141cb22df116524a0eb0c
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# Een XDM-veld in de gebruikersinterface verwijderen

Het Model van Gegevens van de ervaring (XDM) biedt u de flexibiliteit om uw gegevensmodel te beheren aangezien uw bedrijfsbehoeften veranderen door schemagebieden af te schilderen nadat de gegevens zijn opgenomen. De ongewenste gebieden kunnen worden verouderd om hen uit de mening te verwijderen UI en hen ook te verbergen van stroomafwaartse UIs. Met een selectievakje in de Schema-editor kunt u verouderde velden weergeven en, indien nodig, kunt u deze ook ontwaarderen.

Aangezien de vervangen gebieden van UI door gebrek worden verborgen, stroomlijnt dit uw schema in de Redacteur van het Schema en verhindert ongewenste gebieden aan stroomafwaartse gebiedsdelen zoals de Bouwer van het Segment, reisontwerper, etc. worden toegevoegd. Veldveroudering is ook compatibel met oudere versies. Andere systemen die afgekeurde velden gebruiken, zoals publiek en query&#39;s, zullen deze blijven evalueren zoals bedoeld. Als een afgekeurd gebied in een bestaand publiek wordt gebruikt wordt het normaal behandeld, betekenend dat het gebied zoals verwacht op het canvas van de Bouwer van het Segment verschijnt of op om het even welke gegevens wordt geëvalueerd beschikbaar op de afgekeurde gebieden. Dit is een vaste wijziging die geen negatieve invloed heeft op bestaande gegevensstromen.

>[!NOTE]
>
>Voordat gegevens in een schema worden opgenomen, kunt u overbodige veldgroepen verwijderen. Zie de documentatie op [&#x200B; hoe te om een gebiedsgroep uit een schema &#x200B;](../ui/resources/schemas.md#remove-fields) voor meer informatie te verwijderen.

Nadat gegevens in uw schema zijn opgenomen, kunt u geen velden meer uit het schema verwijderen zonder verbreken van wijzigingen aan te brengen. In dit geval, kunt u een ongewenst gebied binnen een schema of een douanemiddel verwerpen door de [&#x200B; Redacteur van het Schema &#x200B;](./create-schema-ui.md) of [&#x200B; Registratie API van het Schema &#x200B;](https://developer.adobe.com/experience-platform-apis/references/schema-registry/) te gebruiken.

In dit document wordt beschreven hoe u velden voor verschillende XDM-bronnen kunt vervangen met de Schema-editor in de gebruikersinterface van het Experience Platform. Voor stappen bij het afschilderen van een XDM gebied gebruikend API, zie het leerprogramma op [&#x200B; afgekeurd een gebied XDM gebruikend de Registratie API van het Schema &#x200B;](./field-deprecation-api.md).

## Een veld verwijderen {#deprecate}

Als u een aangepast veld wilt vervangen, navigeert u naar de Schema-editor voor het schema dat u wilt bewerken. Selecteer het veld dat u wilt vervangen in het gedeelte [!UICONTROL Structure] van het canvas, gevolgd door **[!UICONTROL Deprecate]** in het [!UICONTROL Field Properties] .

![&#x200B; de redacteur van het Schema met een geselecteerd gebied en benadrukt afgekeurd.](../images/tutorials/field-deprecation/deprecate-single-field.png)

Er wordt een dialoogvenster weergegeven waarin u uw keuzes kunt bevestigen en waarin u wordt gemeld dat het veld wordt verwijderd uit de UI-weergave van het samenvoegingsschema en verborgen wordt voor downstreamgebruikersinterface. Selecteer **[!UICONTROL Confirm]** om de handeling te voltooien.

![&#x200B; de Deprecate gebiedsdialoog met Bevestig benadrukte.](../images/tutorials/field-deprecation/deprecate-field-dialog.png)

Het veld wordt nu verwijderd uit de UI-weergave.

>[!NOTE]
>
>Zodra vervangen, stroomafwaartse UIs zoals de dashboards van de Segmentatie, Customer Journey Analytics, en Adobe Journey Optimizer niet meer tonen verouderde gebieden als deel van hun werkschema. Downstreamgebruikersinterface&#39;s hebben echter de optie om vervangen velden weer te geven als dat nodig is en het vervangen veld verder als normaal te behandelen. Raadpleeg de documentatie bij deze groep voor meer informatie. De vragen en het publiek die het vervangen gebied gebruiken zullen blijven zoals verwacht lopen.

## Vervangen velden tonen {#show-deprecated}

Als u eerder vervangen velden wilt weergeven, navigeert u naar het desbetreffende schema in de Schema-editor. Schakel het selectievakje **[!UICONTROL Show deprecated fields]** in het gedeelte [!UICONTROL Composition] van het canvas in.

Het vervangen veld wordt nu weergegeven in de UI-weergave. Selecteer **[!UICONTROL Save]** om uw instellingen te bevestigen.

![&#x200B; de Redacteur van het Schema met een geselecteerd gebied, toon verouderde gebieden en sparen benadrukte.](../images/tutorials/field-deprecation/show-deprecated-fields.png)

## Onbewerkte velden {#undeprecate-fields}

Om een afgekeurd gebied ongedaan te maken, eerst [&#x200B; tonen het afgekeurde gebied &#x200B;](#show-deprecated) zoals hierboven beschreven, dan selecteren het afgekeurde gebied van de redacteur [!UICONTROL Structure] sectie. Selecteer vervolgens **[!UICONTROL Undeprecate]** in de [!UICONTROL Field properties] zijbalk gevolgd door **[!UICONTROL Save]** .

![&#x200B; de Redacteur van het Schema met het afgekeurde gebied, Onafgekeurd, en sparen benadrukte.](../images/tutorials/field-deprecation/undeprecate-single-field.png)

Het dialoogvenster [!UICONTROL Undeprecate field] wordt weergegeven. Selecteer **[!UICONTROL Confirm]** om uw wijzigingen te bevestigen.

![&#x200B; de [!UICONTROL Undeprecate field] dialoog met Bevestig benadrukte.](../images/tutorials/field-deprecation/undeprecate-field-dialog.png)

Het veld wordt nu als standaard weergegeven in de UI-weergave en ook in downstreamgebruikersinterface. U kunt het veld nu vervangen.

## Volgende stappen

In dit document wordt beschreven hoe u XDM-velden kunt vervangen met de interface van de Schema-editor. Voor meer informatie bij het vormen van gebieden voor douanemiddelen, zie de gids bij [&#x200B; het bepalen van gebieden XDM in API &#x200B;](./custom-fields-api.md). Voor meer informatie bij het beheren van beschrijvers, zie de [&#x200B; gids van het beschrijvingseindpunt &#x200B;](../api/descriptors.md).

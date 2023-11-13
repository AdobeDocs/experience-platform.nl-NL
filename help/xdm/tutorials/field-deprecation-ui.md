---
title: Een XDM-veld in de gebruikersinterface verwijderen
description: Leer hoe te om de gebieden van de Gegevens van de Ervaring van het Model (XDM) te verwerpen gebruikend de Redacteur van het Schema binnen Experience Platform.
exl-id: f4c5f58a-5190-47d7-8bfc-b33ed238bf25
source-git-commit: 4fa98df9dcc296ba7cb141cb22df116524a0eb0c
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 0%

---

# Een XDM-veld in de gebruikersinterface verwijderen

Het Model van Gegevens van de ervaring (XDM) biedt u de flexibiliteit om uw gegevensmodel te beheren aangezien uw bedrijfsbehoeften veranderen door schemagebieden af te schilderen nadat de gegevens zijn opgenomen. De ongewenste gebieden kunnen worden verouderd om hen uit de mening te verwijderen UI en hen ook te verbergen van stroomafwaartse UIs. Met een selectievakje in de Schema-editor kunt u verouderde velden weergeven en, indien nodig, kunt u deze ook ontwaarderen.

Aangezien de vervangen gebieden van UI door gebrek worden verborgen, stroomlijnt dit uw schema in de Redacteur van het Schema en verhindert ongewenste gebieden aan stroomafwaartse gebiedsdelen zoals de Bouwer van het Segment, reisontwerper, etc. worden toegevoegd. Veldveroudering is ook compatibel met oudere versies. Andere systemen die afgekeurde velden gebruiken, zoals publiek en query&#39;s, zullen deze blijven evalueren zoals bedoeld. Als een afgekeurd gebied in een bestaand publiek wordt gebruikt wordt het normaal behandeld, betekenend dat het gebied zoals verwacht op het canvas van de Bouwer van het Segment verschijnt of op om het even welke gegevens wordt geëvalueerd beschikbaar op de afgekeurde gebieden. Dit is een vaste wijziging die geen negatieve invloed heeft op bestaande gegevensstromen.

>[!NOTE]
>
>Voordat gegevens in een schema worden opgenomen, kunt u overbodige veldgroepen verwijderen. Zie de documentatie op [hoe te om een gebiedsgroep uit een schema te verwijderen](../ui/resources/schemas.md#remove-fields) voor meer informatie .

Nadat gegevens in uw schema zijn opgenomen, kunt u geen velden meer uit het schema verwijderen zonder verbreken van wijzigingen aan te brengen. In dit geval kunt u een ongewenst veld binnen een schema of aangepaste bron vervangen door de opdracht [Schema-editor](./create-schema-ui.md) of de [Schema-register-API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

In dit document wordt beschreven hoe u velden voor verschillende XDM-bronnen kunt vervangen met de Schema-editor in de gebruikersinterface van het Experience Platform. Raadpleeg de zelfstudie voor stappen over het vervangen van een XDM-veld met de API [een XDM-veld vervangen met de API voor het schemaregister](./field-deprecation-api.md).

## Een veld verwijderen {#deprecate}

Als u een aangepast veld wilt vervangen, navigeert u naar de Schema-editor voor het schema dat u wilt bewerken. Selecteer het veld dat u wilt vervangen in het dialoogvenster [!UICONTROL Structure] het canvas, gevolgd door **[!UICONTROL Deprecate]** van de [!UICONTROL Field Properties].

![De Schema-editor met een geselecteerd veld en de optie Vervangen gemarkeerd.](../images/tutorials/field-deprecation/deprecate-single-field.png)

Er wordt een dialoogvenster weergegeven waarin u uw keuzes kunt bevestigen en waarin u wordt gemeld dat het veld wordt verwijderd uit de UI-weergave van het samenvoegingsschema en verborgen wordt voor downstreamgebruikersinterface. Selecteer **[!UICONTROL Confirm]**.

![Het dialoogvenster Afgekeurd veld met Bevestigen gemarkeerd.](../images/tutorials/field-deprecation/deprecate-field-dialog.png)

Het veld wordt nu verwijderd uit de UI-weergave.

>[!NOTE]
>
>Zodra vervangen, stroomafwaartse UIs zoals de dashboards van de Segmentatie, Customer Journey Analytics, en Adobe Journey Optimizer niet meer tonen verouderde gebieden als deel van hun werkschema. Downstreamgebruikersinterface&#39;s hebben echter de optie om vervangen velden weer te geven als dat nodig is en het vervangen veld verder als normaal te behandelen. Raadpleeg de documentatie bij deze groep voor meer informatie. De vragen en het publiek die het vervangen gebied gebruiken zullen blijven zoals verwacht lopen.

## Vervangen velden tonen {#show-deprecated}

Als u eerder vervangen velden wilt weergeven, navigeert u naar het desbetreffende schema in de Schema-editor. Selecteer de **[!UICONTROL Show deprecated fields]** Selectievakje in het dialoogvenster [!UICONTROL Composition] van het canvas.

Het vervangen veld wordt nu weergegeven in de UI-weergave. Selecteren **[!UICONTROL Save]** om uw instellingen te bevestigen.

![De Schema-editor waarin een veld is geselecteerd, Afgekeurde velden tonen en Geselecteerde velden opslaan.](../images/tutorials/field-deprecation/show-deprecated-fields.png)

## Onbewerkte velden {#undeprecate-fields}

Als u een vervangen veld ongedaan wilt maken, moet u eerst [het vervangen veld weergeven](#show-deprecated) zoals hierboven beschreven, selecteert u vervolgens het vervangen veld in de [!UICONTROL Structure] sectie. Selecteer vervolgens **[!UICONTROL Undeprecate]** van de [!UICONTROL Field properties] zijbalk, gevolgd door **[!UICONTROL Save]**.

![De Schema-editor met het vervangen veld, Onafgekeurd en Opslaan gemarkeerd.](../images/tutorials/field-deprecation/undeprecate-single-field.png)

De [!UICONTROL Undeprecate field] wordt weergegeven. Selecteer **[!UICONTROL Confirm]**.

![De [!UICONTROL Undeprecate field] dialoog met Bevestigen gemarkeerd.](../images/tutorials/field-deprecation/undeprecate-field-dialog.png)

Het veld wordt nu als standaard weergegeven in de UI-weergave en ook in downstreamgebruikersinterface. U kunt het veld nu vervangen.

## Volgende stappen

In dit document wordt beschreven hoe u XDM-velden kunt vervangen met de interface van de Schema-editor. Voor meer informatie bij het vormen van gebieden voor douanemiddelen, zie de gids op [XDM-velden definiëren in de API](./custom-fields-api.md). Zie voor meer informatie over het beheren van descriptoren de [eindhulplijn descriptorpunt](../api/descriptors.md).

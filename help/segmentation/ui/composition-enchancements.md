---
title: Verbeteringen in compositie publiek
description: Meer informatie over de verbeteringen die zijn aangebracht in Audience Composition met de verrijking van het publiek en snellere activering.
hide: true
hidefromtoc: true
source-git-commit: 065990790307124e0992731139abe9641a742a1b
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---


# Verbeteringen voor compositie publiek

U hebt nu toegang tot **twee** verhogingen voor de Samenstelling van het Publiek:

- [Publiek verrijking](#audience-enrichment)
- [Snellere activering](#faster-activation)

## Publiek verrijking {#audience-enrichment}

Met de verrijking van het publiek kunt u de reeks waarden uitvoeren waarmee uw profielen in aanmerking komen voor het publiek dat u hebt gemaakt.

Als u publieksverbeteringen aan uw compositie wilt toevoegen, selecteert u het bovenste **[!UICONTROL Audience]** -blok binnen het canvas. Nadat u het publiek een naam hebt gegeven, selecteert u **[!UICONTROL Build rule]** om het canvas voor regelbuilders te openen.

![&#x200B; het blok van het Publiek wordt benadrukt, evenals de de regelknoop van de Bouwstijl.](/help/segmentation/images/ui/composition-enhancements/select-build-rule.png)

Het canvas voor het opbouwen van regels wordt weergegeven. U kunt nu filtercriteria voor de verrijking van uw publiek maken. Deze filtercriteria **moeten** een attribuut omvatten dat binnen een serie is. Het kenmerk dat een array is, is afhankelijk van de schemastructuur van uw organisatie. Nadat u de filtercriteria hebt gemaakt, selecteert u **[!UICONTROL Delivery]** in het rechterdeelvenster.

![&#x200B; het canvas van de regelbouwer toont een voorbeeld van een publiek dat verbeteringen kan hebben. De knoop van de Levering wordt ook benadrukt.](/help/segmentation/images/ui/composition-enhancements/view-delivery.png)

Kies in de lijst in het linkerdeelvenster de objectarray die u wilt gebruiken voor verrijking. Als het profiel slechts één array bevat, wordt de array automatisch voor u geselecteerd. Selecteer **[!UICONTROL Save]** om terug te keren naar de publiekscompositie.

<!-- , as well as the fields you want to be used in the enrichment. -->

![&#x200B; de schemaboom voor de verrijkingsboom wordt getoond.](/help/segmentation/images/ui/composition-enhancements/view-schema-tree.png)

Binnen publiekscompositie, is uw [!UICONTROL Audience] blok nu een &quot;[!UICONTROL Rule builder with enhancement]&quot;type. Selecteer **[!UICONTROL Publish]** om uw publiek te activeren met de volgende batch per dag.

![&#x200B; het blok van het Publiek wordt benadrukt, tonend dat een publiek met verrijking wordt toegevoegd.](/help/segmentation/images/ui/composition-enhancements/rule-builder-with-enrichment.png)

### Gedragdetails en -instructies

Houd rekening met de volgende details en instructies wanneer u de verrijking van het publiek gebruikt:

- U kunt publieksverrijking binnen publiek slechts gebruiken die binnen de Samenstelling van het Publiek wordt gecreeerd
- Het eerste die blok binnen de samenstelling **wordt gebruikt moet** een op regel-gebaseerd publiek zijn.
- U **kunt** geen andere verrichtingen binnen de samenstelling gebruiken.
- Zodra gepubliceerd, kunt u **niet** de samenstelling op het op regel-gebaseerde publiek uitgeven.

   - U *kunt* de samenstelling in een ontwerp kopiëren en het ontwerp uitgeven als u wenst om veranderingen in de basissamenstelling of op regel-gebaseerd publiek aan te brengen.

- Slechts **één** objecten serie kan worden gebruikt om de verrijkingslading binnen één enkel publiek te produceren

   - De nuttige ladingsserie kan binnen een voorwerp (tot zeven lagen binnen het profielschema) worden genesteld, maar **kan niet** in een andere serie worden bevat.
   - De nuttige ladingsserie **moet** 50 of minder rijen hebben.
   - Alle kolomoutput binnen de nuttige lading **moet** een primitief type zijn.
   - Slechts worden de eerste **twintig** kolommen van de serie uitgevoerd.

- Slechts **tien** publiekssamenstellingen zijn beschikbaar voor gebruik op dit ogenblik

## Snellere activering {#faster-activation}

Met snellere activering kunt u uw publiek direct na de evaluatie van de compositie naar een lagere bestemming activeren. Dientengevolge, als uw bestemming wordt geplaatst om na segmentevaluatie te activeren, te hoeven u niet meer op 24 uren op de evaluatietaak te wachten om te beëindigen.

Voor meer informatie, leest [&#x200B; publiek aan de gids van de partijprofielbestemmingen &#x200B;](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) activeren.

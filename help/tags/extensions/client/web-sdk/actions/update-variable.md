---
title: Variabele bijwerken
description: Wijzigt de inhoud van een veranderlijk gegevenselement.
exl-id: 6c558d1e-85b4-45f9-ba4d-5fed1ec6e308
source-git-commit: 50881ef9498196f2de5519f050800334019a2586
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Variabele bijwerken

De **[!UICONTROL Update variable]** actie staat u toe om gedeeltelijke of stijgende veranderingen in a [&#x200B; veranderlijk gegevenselement &#x200B;](../data-element-types.md#variable) aan te brengen. Met deze handeling kunt u een object maken waarnaar later in een [[!UICONTROL Send event]](send-event.md) -handeling kan worden verwezen. Het bevolken van gegevenselementen en het toewijzen van hen aan eigenschappen binnen een voorwerp XDM past de meeste gebruiksgevallen; deze actie verstrekt meer flexibiliteit om u toe te staan om eigenschappen aan verschillende gegevenselementen voorwaardelijk te plaatsen die op regelvoorwaarden worden gebaseerd.

Voordat u deze handeling kunt gebruiken, moet u al een element met variabele gegevens hebben gemaakt. Nadat u een variabele-gegevenselement hebt geselecteerd dat u wilt wijzigen, wordt een editor weergegeven waarmee u de gewenste velden voor deze actie kunt instellen.

![&#x200B; Screenshot van de update veranderlijke actie binnen de interface van de actieconfiguratie &#x200B;](../assets/update-variable.png)

Het XDM-schema dat in de editor wordt gebruikt, komt overeen met het schema dat in het variabele gegevenselement is geselecteerd. U kunt een of meer eigenschappen van het object instellen door objecten uit te breiden en de gewenste eigenschappen te selecteren. In de onderstaande schermafbeelding wordt de eigenschap `producedBy` bijvoorbeeld ingesteld op het gegevenselement `%Produced by data element%` .

![&#x200B; Screenshot van de interface die van de actieconfiguratie een bijgewerkt bezit toont &#x200B;](../assets/update-variable-set-property.png)

Als u een veranderlijk gegevenselement selecteert dat een gegevensvoorwerp in plaats van een voorwerp XDM gebruikt, hangen de beschikbare gebieden van de producten af die wanneer het vormen van het gegevenselement worden geselecteerd. Als u bijvoorbeeld een gegevensobject maakt dat Adobe Analytics bevat, velden, en u het element met variabele gegevens in deze interface selecteert, worden velden weergegeven die u specifiek voor Adobe Analytics kunt invullen.

![&#x200B; Screenshot van de interface die van de actieconfiguratie een veranderlijk gegevenselement toont op een gegevensvoorwerp wordt gebaseerd &#x200B;](../assets/variable-data-element-data.png)

---
title: Overzicht van Pixel magnetisch
description: Leer hoe u de tagextensie Pixel magnetisch kunt gebruiken om geldige gebruikersinteracties in Adobe Experience Platform vast te leggen.
last-substantial-update: 2025-09-17T00:00:00Z
source-git-commit: d846bd5dee5ce0ee8836dc25e20d9fd070714114
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---

# [!DNL Snap Pixel] overzicht van extensies

[[!DNL Snap Pixel] ](https://businesshelp.snapchat.com/s/article/snap-pixel-about) is een op JavaScript gebaseerd analysehulpmiddel dat u machtigt om waardevolle gebruikersinteractie op uw website te vangen. De belangrijke bezoekersacties, zoals aankopen, sign-ups, of andere omzettingen, worden automatisch verzonden naar uw [ Manager van Advertenties ](http://ads.snapchat.com/), toelatend u om de prestaties van uw advertenties, campagnes, omzettingswegen, en meer te meten en te optimaliseren.

Met de tagextensie [!DNL Snap Pixel] kunt u de functionaliteit van [!DNL Snap Pixel] rechtstreeks integreren in uw tagbibliotheken aan de clientzijde. In deze documentatie wordt beschreven hoe u de extensie installeert en de functies ervan implementeert binnen de regels voor tagbeheer.

Met de tagextensie [!DNL Snap Pixel] stroomlijnt u de integratie van [!DNL Snap Pixel] -functionaliteit in uw bestaande tagbibliotheken aan de clientzijde. Deze documentatie schetst hoe te om de uitbreiding te installeren en zijn eigenschappen binnen uw markeringsbeheer [ te vormen regels ](../../../ui/managing-resources/rules.md).

## Vereisten {#prerequisites}

Als u de extensie wilt gebruiken, hebt u een geldig [!DNL Snap] -account nodig met toegang tot [!DNL Ads Manager] . U moet [ een nieuw  [!DNL Snap Pixel] ](https://forbusiness.snapchat.com/advertising/snap-pixel#about) creëren en zijn identiteitskaart van het Pixel kopiëren om de uitbreiding voor uw rekening te vormen. Als u een bestaande [!DNL Snap Pixel] hebt, kunt u gewoon de id ervan gebruiken.

U wordt aangeraden [!DNL Snap Pixel] naast [!DNL Snap Conversions API] te gebruiken om dezelfde gebeurtenissen vanaf de client en de server te verzenden. Deze aanpak kan helpen gebeurtenissen te herstellen die mogelijk niet alleen door [!DNL Snap Pixel] worden vastgelegd. Verwijs naar de [[!DNL Snap]  Conversies API uitbreiding voor gebeurtenis door:sturen ](../../server/snap/overview.md) voor stappen op hoe te om het in uw server-zijimplementaties te integreren. Gelieve te merken op dat uw organisatie toegang tot [ gebeurtenis moet hebben door:sturen ](../../../ui/event-forwarding/overview.md) om de server-zijuitbreiding te gebruiken.

## De extensie installeren {#install}

Als u de extensie [!DNL Snap Pixel] wilt installeren, navigeert u naar de gebruikersinterface van de gegevensverzameling of de gebruikersinterface van Experience Platform en selecteert u **[!UICONTROL Tags]** in de linkernavigatie. Selecteer van hieruit een eigenschap waaraan u de extensie wilt toevoegen of maak een nieuwe eigenschap.

Wanneer u de gewenste eigenschap hebt geselecteerd of gemaakt, selecteert u **[!UICONTROL Extensions]** in de linkernavigatie en selecteert u vervolgens de tab **[!UICONTROL Catalog]** . Zoek de [!UICONTROL Snap Pixel] -kaart en selecteer vervolgens **[!UICONTROL Install]** .

![ de [!UICONTROL Install] knoop die voor de [!UICONTROL Snap Pixel] uitbreiding in de Inzameling UI van Gegevens wordt geselecteerd.](./images/install.png)

In de configuratieweergave die wordt weergegeven, moet u de pixel-id opgeven die u eerder hebt gekopieerd om de extensie te koppelen aan uw account. U kunt de id rechtstreeks in de invoer plakken, maar u kunt ook een bestaand gegevenselement selecteren.

Selecteer **[!UICONTROL Save]** als u klaar bent.

![ identiteitskaart [!DNL Pixel] als gegevenselement in de mening van de uitbreidingsconfiguratie wordt verstrekt die.](./images/configure.png)

De extensie is geïnstalleerd en u kunt nu de verschillende handelingen in de labelregels uitvoeren.

## Een labelregel configureren {#rule}

[!DNL Snap Pixel] ondersteunt een set vooraf gedefinieerde standaardgebeurtenissen, elk met een specifieke context en geaccepteerde parameters. De regelhandelingen die beschikbaar zijn in de extensie [!DNL Snap Pixel], worden uitgelijnd met deze gebeurtenistypen, waardoor het eenvoudig is om gebeurtenissen die naar [!DNL Snap] worden verzonden, te categoriseren en te configureren op basis van het type.

Voor demonstratiedoeleinden toont deze sectie hoe u een regel bouwt die een aankoopgebeurtenis naar [!DNL Snap] verzendt.

Maak eerst een nieuwe labelregel en definieer de voorwaarden. Wanneer u de handelingen van de regel instelt, kiest u [!DNL Snap Pixel] als extensie en selecteert u **[!UICONTROL Send Purchase Event]** als actietype.

Nadat u de handeling [!UICONTROL Send Purchase Event] hebt geconfigureerd, selecteert u **[!UICONTROL Keep Changes]** om deze aan de regelinstelling toe te voegen.

![ het [!UICONTROL Send Purchase Event] actietype dat voor een regel in de Inzameling UI van Gegevens wordt geselecteerd.](./images/action-type.png)

Wanneer u met de algemene regelconfiguratie tevreden bent, uitgezochte **[!UICONTROL Save to Library]**.

Om uw updates toe te passen, publiceer een nieuwe markering [ bouwstijl ](../../../ui/publishing/builds.md) om de veranderingen in de bibliotheek toe te laten.

## Bevestig dat [!DNL Snap] gegevens ontvangt {#confirm}

Zodra uw bijgewerkte build is geïmplementeerd op uw website, kunt u controleren of de gegevens naar behoren worden verzonden door conversiegebeurtenissen in uw browser te activeren en te controleren of deze gebeurtenissen worden weergegeven in [[!DNL Snap Events Manager] ](https://businesshelp.snapchat.com/s/article/events-manager) .

## Volgende stappen {#next-steps}

In deze handleiding wordt uitgelegd hoe u gegevens naar [!DNL Snap] kunt verzenden met de tagextensie [!DNL Snap Pixel] . Als u ook servergebeurtenissen naar [!DNL Snap] wilt verzenden, kunt u doorgaan met het installeren en configureren van [[!DNL Snap Conversions API event forwarding extension]](../../server/snap/overview.md) .

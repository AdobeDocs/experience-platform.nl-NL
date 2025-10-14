---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;gegevensmodel;ui;werkruimte;object;field;
solution: Experience Platform
title: Objectvelden definiëren in de gebruikersinterface
description: Leer hoe u een objecttype-veld definieert in de gebruikersinterface van het Experience Platform.
exl-id: 5b7b3cf0-7f11-4e15-af87-09127f4423a5
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# Objectvelden definiëren in de gebruikersinterface

Adobe Experience Platform staat u toe om de structuur van uw klassen van het Model van de Gegevens van de Ervaring (XDM), schema gebiedsgroepen, en gegevenstypes volledig aan te passen. Als u gerelateerde velden wilt ordenen en nesten in aangepaste XDM-bronnen, kunt u objecttype-velden definiëren die aanvullende subvelden kunnen bevatten.

Wanneer [&#x200B; het bepalen van een nieuw gebied &#x200B;](./overview.md#define) in het gebruikersinterface van Adobe Experience Platform, gebruik **[!UICONTROL Type]** dropdown en selecteer &quot;[!UICONTROL Object]&quot;van de lijst.

![](../../images/ui/fields/special/object.png)

Selecteer **[!UICONTROL Apply]** om het object aan het schema toe te voegen. Het canvas wordt bijgewerkt om het nieuwe veld weer te geven met het gegevenstype [!UICONTROL Object] toegepast, inclusief besturingselementen voor het bewerken en toevoegen van subvelden aan het object.

![](../../images/ui/fields/special/object-applied.png)

Om een sub-gebied toe te voegen, selecteer **plus (+)** pictogram naast het objecten gebied op het canvas. Onder het object wordt een nieuw veld weergegeven met besturingselementen voor het configureren van het subveld in het rechterspoor.

![](../../images/ui/fields/special/object-add-field.png)

Nadat u het subveld hebt geconfigureerd en **[!UICONTROL Apply]** hebt geselecteerd, kunt u via hetzelfde proces velden aan het object blijven toevoegen. U kunt ook subvelden toevoegen die zelf objecten zijn, zodat u velden zo diep kunt nesten als u wilt.

Wanneer u klaar bent met het samenstellen van het object, zult u merken dat u de structuur ervan opnieuw wilt gebruiken in verschillende klassen en veldgroepen. In dit geval kunt u ervoor kiezen het object om te zetten in een gegevenstype. Zie de sectie over [&#x200B; het omzetten van voorwerpen in gegevenstypes &#x200B;](../resources/data-types.md#convert) in de gids van gegevenstypes UI voor meer informatie.

## Volgende stappen

In deze handleiding wordt beschreven hoe u een objectveld in de gebruikersinterface definieert. Zie het overzicht op [&#x200B; bepalende gebieden in UI &#x200B;](./overview.md#special) leren hoe te om andere XDM gebiedstypes in [!DNL Schema Editor] te bepalen.

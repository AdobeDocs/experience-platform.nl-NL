---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;gegevensmodel;ui;werkruimte;object;field;
solution: Experience Platform
title: Objectvelden definiëren in de gebruikersinterface
description: Leer hoe u een objecttype-veld definieert in de gebruikersinterface van het Experience Platform.
topic-legacy: user guide
exl-id: 5b7b3cf0-7f11-4e15-af87-09127f4423a5
source-git-commit: fe3d9a3fc473e7ca13f0e0c2f222bcc1b1a991c4
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# Objectvelden definiëren in de gebruikersinterface

Adobe Experience Platform staat u toe om de structuur van uw klassen van het Model van de Gegevens van de Ervaring (XDM), schema gebiedsgroepen, en gegevenstypes volledig aan te passen. Als u gerelateerde velden wilt ordenen en nesten in aangepaste XDM-bronnen, kunt u objecttype-velden definiëren die aanvullende subvelden kunnen bevatten.

Wanneer [een nieuw veld definiëren](./overview.md#define) in de Adobe Experience Platform-gebruikersinterface **[!UICONTROL Type]** vervolgkeuzelijst en selecteer &quot;[!UICONTROL Object]&quot; in de lijst.

![](../../images/ui/fields/special/object.png)

Selecteren **[!UICONTROL Apply]** om het object aan het schema toe te voegen. Het canvas wordt bijgewerkt om het nieuwe veld weer te geven met het [!UICONTROL Object] toegepast gegevenstype, inclusief besturingselementen voor het bewerken en toevoegen van subvelden aan het object.

![](../../images/ui/fields/special/object-applied.png)

Als u een subveld wilt toevoegen, selecteert u de optie **plus (+)** pictogram naast het objectveld op het canvas. Onder het object wordt een nieuw veld weergegeven met besturingselementen voor het configureren van het subveld in het rechterspoor.

![](../../images/ui/fields/special/object-add-field.png)

Nadat u het subveld hebt geconfigureerd en geselecteerd **[!UICONTROL Apply]** kunt u doorgaan met het toevoegen van velden aan het object met hetzelfde proces. U kunt ook subvelden toevoegen die zelf objecten zijn, zodat u velden zo diep kunt nesten als u wilt.

Wanneer u klaar bent met het samenstellen van het object, zult u merken dat u de structuur ervan opnieuw wilt gebruiken in verschillende klassen en veldgroepen. In dat geval kunt u het object omzetten in een gegevenstype. Zie de sectie over [objecten omzetten in gegevenstypen](../resources/data-types.md#convert) in de UI-gids voor gegevenstypen voor meer informatie.

## Volgende stappen

In deze handleiding wordt beschreven hoe u een objectveld in de gebruikersinterface definieert. Zie het overzicht op [velden definiëren in de gebruikersinterface](./overview.md#special) leren hoe u andere XDM-veldtypen definieert in het dialoogvenster [!DNL Schema Editor].

---
title: Opmerkingen bij de release van Adobe Experience Platform
description: Opmerkingen bij de release Experience Platform november 2020
doc-type: release notes
last-update: November, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 39668013723dcda332558b74cf72b5f93db04461
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 3%

---


# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: november 2020**

Nieuwe functies in Adobe Experience Platform:

- [[!DNL Access control]](#access-control)
- [[!DNL-sandboxen]](#sandboxes)

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] Gebruikt [Adobe Admin Console](https://adminconsole.adobe.com) -productprofielen om gebruikers te koppelen aan machtigingen en sandboxen. Machtigingen beheren de toegang tot verschillende mogelijkheden van Platforms, waaronder gegevensmodellering, profielbeheer en sandboxbeheer.

**Belangrijkste kenmerken**

| Functie | Beschrijving |
|--- | ---|
| Toestemmingen | Op de [!DNL Admin Console]tab in een [!DNL Platform] productprofiel kunt u aanpassen welke [!DNL Platform] mogelijkheden beschikbaar zijn voor de gebruikers die aan dat profiel zijn gekoppeld. Beschikbare machtigingscategorieën zijn: [!UICONTROL Gegevensmodellering], [!UICONTROL gegevensbeheer], [!UICONTROL profielbeheer], [!UICONTROL identiteiten], [!UICONTROL gegevenscontrole], Sandbox-beheer, Destination, Sources. |
| Toegang tot sandboxen | Met het tabblad **[!UICONTROL Machtigingen]** in een [!DNL Platform] productprofiel kunnen gebruikers toegang krijgen tot specifieke sandboxen. Zie de sectie over [sandboxen](#sandboxes) hieronder voor meer informatie. |

Zie het overzicht [van](../../access-control/home.md)toegangsbeheer voor meer informatie.

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] is ontworpen om toepassingen voor digitale ervaring wereldwijd te verrijken. Bedrijven voeren vaak meerdere digitale-ervaringstoepassingen parallel uit en moeten rekening houden met de ontwikkeling, het testen en de implementatie van deze toepassingen en tegelijk de operationele compatibiliteit garanderen. Om aan deze behoefte tegemoet te komen, [!DNL Experience Platform] verstrekt zandbakken die één enkele [!DNL Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

**Belangrijkste kenmerken**

| Functie | Beschrijving |
|--- | ---|
| Productiesandbox | [!DNL Experience Platform] biedt één productiesandbox die niet kan worden verwijderd of opnieuw ingesteld. |
| Niet-productie sandboxen | Er kunnen meerdere niet-productiesandboxen voor één [!DNL Platform] instantie worden gemaakt, zodat u functies kunt testen, experimenten kunt uitvoeren en aangepaste configuraties kunt maken zonder dat dit invloed heeft op de productiesandbox. |
| Sandboxschakelaar | In de [!DNL Experience Platform] gebruikersinterface kunt u met de sandboxschakelaar in de linkerbovenhoek van het scherm schakelen tussen beschikbare sandboxen via een vervolgkeuzemenu. |
| `x-sandbox-name` header | Alle aanroepen van [!DNL Experience Platform] API&#39;s moeten nu de nieuwe `x-sandbox-name` header bevatten, waarvan de waarde verwijst naar het `name` kenmerk van de sandbox waarin de bewerking plaatsvindt. |

Zie het [sandboxoverzicht](../../sandboxes/home.md)voor meer informatie.
---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;gegevensmodel;ui;werkruimte;enum;field;
solution: Experience Platform
title: Enum Fields definiëren in de UI
description: Leer hoe u een opsommingsveld definieert in de gebruikersinterface van het Experience Platform.
topic-legacy: user guide
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
source-git-commit: f6fefda974d2ae6fd4b035ef3b5fe633311c9772
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# Enumvelden definiëren in de gebruikersinterface {#enum}

>[!CONTEXTUALHELP]
>id="platform_xdm_enumsuggestedvalue"
>title="Opsommingen en voorgestelde waarden"
>abstract="Een opsomming beperkt een tekenreeksveld om alleen gegevens toe te staan die overeenkomen met een vooraf gedefinieerde set waarden die moeten worden ingevoerd. U kunt ook een set voorgestelde waarden voor het veld definiëren die de opname niet beperken, maar in plaats daarvan de kenmerken definiëren waaruit u in de segmentatie kunt kiezen. Raadpleeg de documentatie voor meer informatie."

In het Model van Gegevens van de Ervaring (XDM), vertegenwoordigt een enumgebied een gebied dat tot een vooraf bepaalde lijst van aanvaardbare waarden wordt beperkt.

Wanneer [een nieuw veld definiëren](./overview.md#define) in de Adobe Experience Platform-gebruikersinterface kunt u deze als een opsommingsveld instellen door de optie **[!UICONTROL Enum]** selectievakje in de rechterspoorstaaf.

![](../../images/ui/fields/special/enum.png)

Aanvullende besturingselementen worden weergegeven nadat u het selectievakje hebt ingeschakeld, zodat u de waardebeperkingen voor de opsomming kunt opgeven. Onder de **[!UICONTROL Value]** moet u de exacte waarde opgeven waarmee u het veld wilt beperken. Deze waarde moet voldoen aan de [!UICONTROL Type] u hebt voor het opsommingsveld geselecteerd. U kunt desgewenst een mensvriendelijk **[!UICONTROL Label]** ook voor de beperking.

Als u aanvullende beperkingen aan de opsomming wilt toevoegen, selecteert u **[!UICONTROL Add row]**.

![](../../images/ui/fields/special/enum-add-row.png)

Ga verder met het toevoegen van de gewenste restricties en optionele labels aan de opsomming. Als u klaar bent, selecteert u **[!UICONTROL Apply]** om de wijzigingen toe te passen op het schema.

![](../../images/ui/fields/special/enum-configured.png)

Het canvas wordt bijgewerkt met de wijzigingen. Wanneer u dit schema in de toekomst verkent, kunt u de beperkingen voor het enum gebied binnen het juiste spoor bekijken en uitgeven.

![](../../images/ui/fields/special/enum-applied.png)

## Volgende stappen

Deze handleiding besprak hoe u een opsommingsveld kunt definiëren in de gebruikersinterface. Zie het overzicht op [velden definiëren in de gebruikersinterface](./overview.md#special) leren hoe u andere XDM-veldtypen definieert in het dialoogvenster [!DNL Schema Editor].

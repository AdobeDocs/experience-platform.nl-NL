---
title: Overzicht van Meta-pixelextensie
description: Meer informatie over de extensie Meta Pixel in Adobe Experience Platform.
source-git-commit: 87376172f89858bfa883084461544a2c50ba5009
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---

# [!DNL Meta Pixel] extensieoverzicht

[[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) is een op JavaScript gebaseerd analyseprogramma waarmee u de bezoekersactiviteit op uw website kunt volgen. Bezoekersacties die u bijhoudt (conversies genoemd) worden verzonden naar [[!DNL Ads Manager]](https://www.facebook.com/business/tools/ads-manager) waar ze kunnen worden gebruikt om de effectiviteit van advertenties, campagnes, conversietrechter en nog veel meer te meten.

De [!DNL Meta Pixel] met de extensie van tags kunt u gebruikmaken van [!DNL Pixel] functies in de tagbibliotheken aan de clientzijde. In dit document wordt beschreven hoe u de extensie installeert en de mogelijkheden ervan kunt gebruiken in een [regel](../../../ui/managing-resources/rules.md).

<!-- (To include when Conversions API extension doc is published)
>[!NOTE]
>
>If you are trying to send server-side events to [!DNL Meta] rather than from the client side, use the [[!DNL Meta Conversions API] extension](../../server/meta/overview.md) instead.
-->

## Vereisten

Als u de extensie wilt gebruiken, moet u een geldige [!DNL Meta] account met toegang tot [!DNL Ads Manager]. Specifiek, moet u [een nieuwe [!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755) en kopieert [!DNL Pixel ID] kan de extensie dus worden geconfigureerd voor uw account. Als u al een bestaande [!DNL Meta Pixel], kunt u in plaats daarvan de id gebruiken.

## De extensie installeren

Als u het dialoogvenster [!DNL Meta Pixel] de extensie, navigeert u naar de gebruikersinterface van de gegevensverzameling of het Experience Platform en selecteert u **[!UICONTROL Tags]** in de linkernavigatie. Van hier, selecteer een bezit om de uitbreiding aan toe te voegen, of een nieuw bezit in plaats daarvan tot stand te brengen.

Als u de gewenste eigenschap hebt geselecteerd of gemaakt, selecteert u **[!UICONTROL Extensions]** in de linkernavigatie, dan selecteer **[!UICONTROL Catalog]** tab. Zoeken naar [!UICONTROL Meta Pixel] kaart, dan selecteren **[!UICONTROL Install]**.

![De [!UICONTROL Install] knop die wordt geselecteerd voor de [!UICONTROL Meta Pixel] in de UI voor gegevensverzameling.](../../../images/extensions/client/meta/install.png)

In de configuratieweergave die wordt weergegeven, moet u de opdracht [!DNL Pixel] ID die u eerder hebt gekopieerd om de extensie te koppelen aan uw account. U kunt de id rechtstreeks in de invoer plakken, maar u kunt ook een bestaand gegevenselement selecteren.

>[!TIP]
>
>Als u een gegevenselement gebruikt, kunt u de optie [!DNL Pixel] ID wordt gebruikt afhankelijk van andere factoren zoals de bouwstijlomgeving. Zie het aanhangsel over [verschillend gebruiken [!DNL Pixel] ID&#39;s voor verschillende omgevingen](#id-data-element) voor meer informatie .

U kunt ook een gebeurtenis-id opgeven die u aan de extensie wilt koppelen. Dit wordt gebruikt om identieke gebeurtenissen tussen [!DNL Meta Pixel] en de [!DNL Meta Conversions API]. Zie de [!DNL Meta] documentatie over [dupliceren [!DNL Pixel] en [!DNL Conversions API] gebeurtenissen](https://developers.facebook.com/docs/marketing-api/conversions-api/deduplicate-pixel-and-server-events/) voor meer informatie.

Als u klaar bent, selecteert u **[!UICONTROL Save]**

![De [!DNL Pixel] ID verstrekt als gegevenselement in de mening van de uitbreidingsconfiguratie.](../../../images/extensions/client/meta/configure.png)

De extensie is geïnstalleerd en u kunt nu de verschillende handelingen in de labelregels uitvoeren.

## Een labelregel configureren {#rule}

[!DNL Meta Pixel] accepteert een set vooraf gedefinieerde [standaardgebeurtenissen](https://www.facebook.com/business/help/402791146561655), elk met hun eigen context en aanvaarde eigenschappen. De door de [!DNL Pixel] de extensie correleert met deze gebeurtenistypen, zodat u de gebeurtenis die wordt verzonden naar gemakkelijk kunt categoriseren en configureren [!DNL Meta] afhankelijk van het type.

Voor demonstratiedoeleinden toont deze sectie hoe te om een regel te bouwen die een gebeurtenis van de paginamening verzendt naar [!DNL Meta].

Begin het creëren van een nieuwe markeringsregel en vorm zijn voorwaarden zoals gewenst. Selecteer bij het selecteren van de handelingen voor de regel de optie **[!UICONTROL Meta Pixel]** voor de extensie selecteert u vervolgens **[!UICONTROL Send Page View]** voor het actietype.

![De [!UICONTROL Send Page View] actietype dat voor een regel in de Inzameling UI van Gegevens wordt geselecteerd.](../../../images/extensions/client/meta/select-action.png)

Er is geen verdere configuratie vereist voor de [!UICONTROL Send Page View] handeling. Selecteren **[!UICONTROL Keep Changes]** om de actie aan de regelconfiguratie toe te voegen. Als u tevreden bent met de regel, selecteert u **[!UICONTROL Save to Library]**.

Ten slotte publiceert u een nieuwe tag [build](../../../ui/publishing/builds.md) om de wijzigingen in de bibliotheek in te schakelen.

## Bevestig dat [!DNL Meta] ontvangt gegevens

Nadat uw bijgewerkte build op uw website is geïmplementeerd, kunt u bevestigen of gegevens naar behoren worden verzonden door conversiegebeurtenissen te genereren in uw browser en te controleren of deze gebeurtenissen worden weergegeven in [[!DNL Meta Events Manager]](https://www.facebook.com/business/help/898185560232180).

## Volgende stappen

In deze handleiding wordt beschreven hoe gegevens worden verzonden naar [!DNL Meta] met de [!DNL Meta Pixel] tagextensie. Raadpleeg voor meer informatie over tags in Experience Platform de [overzicht van tags](../../../home.md).

## Aanhangsel: Verschil gebruiken [!DNL Pixel] ID&#39;s voor verschillende omgevingen {#id-data-element}

Als u uw implementatie wilt testen in ontwikkelings- of staging-omgevingen terwijl uw productie behouden blijft [!DNL Meta Pixel] intacte analysemogelijkheden, kunt u een gegevenselement gebruiken om dynamisch een aangewezen [!DNL Pixel] ID afhankelijk van de omgeving die wordt gebruikt.

U kunt dit bereiken door een [!UICONTROL Custom Code] gegevenselement (verstrekt door de [[!UICONTROL Core] extension](../core/overview.md)) in combinatie met de [`turbine` vrije variabele](../../../extension-dev/turbine.md). In de JavaScript-code van het gegevenselement gebruikt u de opdracht `turbine` -object om het huidige milieustadium te vinden, en retourneert vervolgens een geschikt [!DNL Pixel] ID gebaseerd op het resultaat.

In het volgende voorbeeld wordt een onechte productie-id geretourneerd `exampleProductionKey` bij gebruik in de productieomgeving en een andere id `exampleTestKey` wanneer een andere omgeving wordt gebruikt. Vervang bij het implementeren van deze code elke waarde door de werkelijke productie en test [!DNL Pixel] ID&#39;s.

```js
return (turbine.environment.stage === "production" ? 'exampleProductionKey' : 'exampleTestKey');
```


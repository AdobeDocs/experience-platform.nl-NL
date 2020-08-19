---
keywords: launch web tags;web tags launch;website tags;web tags;launch;Launch
title: Zelfstudie Websitetags implementeren met Adobe Launch
seo-title: Websitetags implementeren met Adobe Launch
description: Adobe starten gebruiken om websitetags te implementeren in Adobe Experience Platform
seo-description: Adobe starten gebruiken om websitetags te implementeren in Adobe Experience Platform
translation-type: tm+mt
source-git-commit: 54df4778a025811504801306120bda78e04281c1
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 3%

---


# Zelfstudie: Websitetags implementeren met Adobe Launch

In deze zelfstudie wordt uitgelegd hoe u uw websitetags kunt implementeren om gegevens naar Adobe Experience Platform te verzenden met behulp van Adobe Launch.

## Vereisten

* Het vereiste schema en de dataset worden gecreeerd in [!DNL Platform].
* De noodzakelijke configuratie is opgesteld in de Rand van de Ervaring en heeft de passende identiteitskaart van de Configuratie en het domein van de Rand.
* Het bedrijf CMS is al geconfigureerd om een JavaScript-object op elke pagina te leveren met de gegevens die u naar het Platform moet verzenden.

## Stappen

Deze zelfstudie bevat de volgende stappen:

1. Installeer de Adobe Experience Platform- [!DNL Web SDK] extensie.
1. Maak een regel om te bepalen [!DNL Launch] welke gegevens moeten worden verzonden.
1. Bundel de extensie en regel in een bibliotheek.

## De Adobe Experience Platform- [!DNL Web SDK] extensie installeren

Installeer eerst de Adobe Experience Platform- [!DNL Web SDK] extensie.

1. Open [!DNL Launch]het tabblad **[!UICONTROL Extensies]** in.

   ![afbeelding](assets/launch-overview.png)

1. Selecteer de extensie Adobe Experience Platform Web SDK in de catalogus Extensie starten. Het configuratiescherm wordt geopend.

   ![afbeelding](assets/launch-extension-install.png)

   Zie [Extensies](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html) in de [!DNL Launch] documentatie voor meer informatie.

1. Configureer de extensie.

   U hebt nu alleen de volgende instellingen nodig:

   * **Configuratie-id:** Geef de configuratie-id op die u van uw Adobe-vertegenwoordiger hebt gekregen.
   * **Randdomein:** Geef het randdomein op dat u van uw Adobe-vertegenwoordiger hebt gekregen.

1. Klik op **[!UICONTROL Opslaan]** en ga verder met de volgende stap.

## Een regel maken om te bepalen [!DNL Launch] welke gegevens moeten worden verzonden

Maak vervolgens een regel om te laten [!DNL Launch] weten welke gegevens u naar Adobe Experience Platform wilt verzenden en wanneer u deze wilt verzenden.

1. Configureer op het tabblad **[!UICONTROL Regels]** een gebeurtenis die op elke nieuwe pagina van de website wordt geactiveerd wanneer de [!DNL Launch] bibliotheek wordt geladen.

   ![afbeelding](assets/launch-make-a-rule.png)

1. Voeg een handeling toe.

   Om de actie te vormen, vertel [!DNL Launch] waar om uw gegevenslaag te vinden. De gegevenslaag is een JavaScript-object dat op de pagina aanwezig is en wordt geleverd vanuit hetzelfde CMS dat de webpagina rendert. Geef het JavaScript-pad naar het gegevensobject op.

   ![afbeelding](assets/launch-add-aep-action.png)

   Het gegevensvoorwerp u verzendt moet geldige XDM zijn die bevestiging tegen het schema zal overgaan dat door de dataset wordt gebruikt die met uw identiteitskaart van de Configuratie wordt verbonden.

1. Klik op Wijzigingen **[!UICONTROL behouden]**.

Zie [Regels](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/rules.html) in de [!DNL Launch] documentatie voor meer informatie.

## De extensie en regel bundelen in een bibliotheek

Daarna, [bundel de uitbreiding](https://docs.adobe.com/content/help/en/launch/using/reference/publish/overview.html) en uw nieuwe regel samen in een bibliotheek en test die veranderingen in een ontwikkelomgeving.

![afbeelding](assets/launch-add-changes-to-library.png)

Nadat u uw tests hebt voltooid, promoot u de bibliotheek via de workflow zodat deze op de productiesite kan worden geïmplementeerd. Er stromen nu gegevens van elke individuele gebruiker naar Adobe Experience Platform.

![afbeelding](assets/launch-promote-library.png)

Zie [Bibliotheken](https://docs.adobe.com/content/help/en/launch/using/reference/publish/libraries.html) in de [!DNL Launch] documentatie voor meer informatie.
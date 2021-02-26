---
title: Overzicht van Adobe Experience Platform Web SDK-extensie
description: Meer informatie over de Adobe Experience Platform Web SDK Extension voor Adobe Experience Platform Launch
translation-type: tm+mt
source-git-commit: 18e511337eaa8b6eb7785b1ee5f1ce2366ddd7c7
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---


# Overzicht van Adobe Experience Platform Web SDK-extensie

De Adobe Experience Platform Web SDK-extensie verzendt gegevens van wegeigenschappen naar Adobe Experience Cloud via het Adobe Experience Platform Edge Network. Met de extensie kunt u gegevens streamen naar een Platform, identiteiten synchroniseren, de toestemmingssignalen van de klant verwerken en automatisch contextgegevens verzamelen.

In dit document wordt beschreven hoe u de extensie configureert in de gebruikersinterface van Adobe Experience Platform Launch.

## De extensie configureren

Als de uitbreiding van SDK van het Web van het Platform reeds voor een bezit is geïnstalleerd, open het bezit in Platform launch UI en selecteer **[!UICONTROL Extensions]** tabel. Selecteer **[!UICONTROL Configure]** onder de SDK van het Web Platform.

![](../images/extension/overview/configure.png)

Als u de extensie nog niet hebt geïnstalleerd, selecteert u het tabblad **[!UICONTROL Catalog]**. Van de lijst van beschikbare uitbreidingen, vind de uitbreiding van SDK van het Web van het Platform en selecteer **[!UICONTROL Install]**.

![](../images/extension/overview/install.png)

In beide gevallen, komt u bij de configuratiepagina voor het Web SDK van het Platform aan. In de volgende secties worden de configuratieopties van de extensie uitgelegd.

![](../images/extension/overview/config-screen.png)

## Algemene configuratieopties

De configuratieopties boven aan de pagina vertellen Adobe Experience Platform waar te om de gegevens te leiden en welke configuraties op de server zouden moeten worden gebruikt.

### [!UICONTROL Naam]

De extensie Adobe Experience Platform Web SDK ondersteunt meerdere exemplaren op de pagina. Dit wordt gebruikt om gegevens naar veelvoudige organisaties met één enkele configuratie van de Platform launch te verzenden.

De naam van de extensie is standaard &quot;[!DNL alloy]&quot;. U kunt de instantienaam echter wijzigen in elke geldige naam voor een JavaScript-object.

### **[!UICONTROL IMS-organisatie-id]**

De [!UICONTROL IMS Organisatie-id] is de organisatie waarnaar u de gegevens op Adobe wilt verzenden. Meestal moet u de standaardwaarde gebruiken die automatisch wordt ingevuld. Wanneer u meerdere exemplaren op de pagina hebt, vult u dit veld met de waarde van de tweede organisatie waarnaar u gegevens wilt verzenden.

### **[!UICONTROL Edge-domein]**

Het [!UICONTROL Edge-domein] is het domein waarvan de Adobe Experience Platform-extensie gegevens verzendt en ontvangt. De uitbreiding vereist dat u 1st-partij CNAME voor productieverkeer gebruikt. Het standaard domein van derden werkt voor ontwikkelomgevingen, maar is niet geschikt voor productieomgevingen. Instructies over hoe te opstelling een eerste-partij CNAME zijn vermeld [hier](https://docs.adobe.com/content/help/en/core-services/interface/ec-cookies/cookies-first-party.html).

## [!UICONTROL Edge-configuraties]

Wanneer een aanvraag naar het Adobe Experience Platform Edge-netwerk wordt verzonden, wordt een Edge-configuratie-id gebruikt om naar de serverconfiguratie te verwijzen. Hierdoor kunt u de configuratie bijwerken zonder dat u codewijzigingen hoeft aan te brengen op uw website.

Zie de handleiding op [randconfiguraties](../fundamentals/edge-configuration.md) voor meer informatie.

## [!UICONTROL Privacy]

In de sectie [!UICONTROL Privacy] kunt u configureren hoe de SDK de toestemmingssignalen van de klant van uw website afhandelt. Specifiek, staat het u toe om het standaardniveau van toestemming te selecteren dat van een klant wordt verondersteld als geen andere expliciete toestemmingsvoorkeur is verstrekt. In de volgende tabel wordt aangegeven wat elke optie inhoudt:

| [!UICONTROL Standaardniveau van toestemming] | Beschrijving |
| --- | --- |
| [!UICONTROL In] | Inschakelen. Gebruik deze optie als u de instemming van de klant standaard aanneemt en alleen de signalen van de opt-out respecteert. |
| [!UICONTROL In behandeling] | Klanten met &quot;hangende&quot; toestemming worden verondersteld te worden uitgesloten tot een opt-in signaal wordt verzonden. Gebruik deze optie als u expliciete klantentoestemming voor uw bedrijfsverrichtingen vereist. |
| [!UICONTROL Verstrekt door gegevenselement] | Het standaard toestemmingsniveau wordt bepaald door een afzonderlijk gegevenselement dat u bepaalt. Wanneer u deze optie gebruikt, moet u het gegevenselement opgeven met behulp van het opgegeven vervolgkeuzemenu. |
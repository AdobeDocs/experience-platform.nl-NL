---
title: Opmerkingen bij de release van Adobe Experience Platform
description: De meest recente releaseopmerkingen voor Adobe Experience Platform.
source-git-commit: 641fcab89b849d91a075fa5058421950bc7fecd7
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 2%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 26 januari 2021**

Updates voor bestaande functies in Adobe Experience Platform:

- [Waarschuwingen](#alerts)
- [Gegevensprep](#data-prep)
- [Sandboxen](#sandboxes)
- [Segmenteringsservice](#segmentation)

## Waarschuwingen {#alerts}

Met Experience Platform kunt u zich abonneren op waarschuwingen op basis van gebeurtenissen voor verschillende activiteiten van Platforms. U kunt zich abonneren op verschillende waarschuwingsregels via de [!UICONTROL Alerts] in de gebruikersinterface van het Platform en kan ervoor kiezen waarschuwingsberichten te ontvangen binnen de gebruikersinterface zelf of via e-mailberichten.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe waarschuwingsregels | Er zijn nu verschillende nieuwe waarschuwingsregels beschikbaar voor workflows die betrekking hebben op gegevensinvoer, identiteiten, profielen, segmentering en activering. Zie het overzicht op [waarschuwingsregels](../../observability/alerts/rules.md) voor de bijgewerkte lijst met waarschuwingstypen. |

Raadpleeg voor meer informatie over waarschuwingen in Platform de [waarschuwingsoverzicht](../../observability/alerts/overview.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om, gegevens aan en van het Model van Gegevens van de Ervaring in kaart te brengen om te zetten en te bevestigen (XDM).

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Geconsolideerde toewijzingservaring | De nieuwe toewijzingsinterface in het Platform UI voorziet u van een verenigbare afbeeldingservaring om uit intelligente kaartaanbevelingen voordeel te halen, manueel toewijzingsregels te vormen, en om het even welke fouten te zuiveren die aan uw kaartreeksen voorkomen. Zie voor meer informatie de [[!DNL Data Prep] UI-hulplijn](../../data-prep/home.md). |

Voor meer informatie over [!DNL Data Prep], zie de [[!DNL Data Prep] overzicht](../../data-prep/home.md).

## Sandboxen {#sandboxes}

Adobe Experience Platform is ontworpen om toepassingen voor digitale beleving wereldwijd te verrijken. Bedrijven voeren vaak meerdere digitale-ervaringstoepassingen parallel uit en moeten rekening houden met de ontwikkeling, het testen en de implementatie van deze toepassingen en tegelijk de operationele compatibiliteit garanderen. Om aan deze behoefte tegemoet te komen, biedt Experience Platform sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Verbeteringen in de gebruikersinterface van sandboxen | De sandboxindicator is nu geïntegreerd in de header voor alle Platform-UI-toepassingen. De sandboxindicator geeft de naam, het gebied en het type van de sandbox weer en geeft u ook toegang tot een vervolgkeuzemenu om tussen de sandboxen te schakelen. Zie voor meer informatie de [UI-hulplijn sandbox](../../sandboxes/ui/user-guide.md). |

Voor meer informatie over sandboxen raadpleegt u de [sandboxen, overzicht](../../sandboxes/home.md).

## Segmenteringsservice {#segmentation}

[!DNL Segmentation Service] definieert een bepaalde subset van profielen door de criteria te beschrijven die een verhandelbare groep personen binnen uw klantenbasis onderscheiden. De segmenten kunnen op verslaggegevens (zoals demografische informatie) of tijdreeksgebeurtenissen worden gebaseerd die klanteninteractie met uw merk vertegenwoordigen.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Segmentovereenkomst | Segmentovereenkomst is een service voor gegevenssamenwerking waarmee twee of meer gebruikers in het Platform gegevens kunnen uitwisselen op basis van gemeenschappelijke id&#39;s op een veilige, beheerde en privacyvriendelijke manier. Zie voor meer informatie de [Overzicht van afstemming van segment](../../segmentation/ui/segment-match/overview.md). |

Voor meer informatie over [!DNL Segmentation Service], zie de [Overzicht van segmentatie](../../segmentation/home.md).

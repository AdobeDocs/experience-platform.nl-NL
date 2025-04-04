---
title: IAB TCF 2.0 Steun in de Adobe Experience Platform Web SDK
description: Leer hoe u IAB TCF 2.0-voorkeuren voor toestemming ondersteunt met de Adobe Experience Platform Web SDK
keywords: toestemming;setConsent;Profile Privacy Field group;Experience Event Privacy Field group;Privacy Field group;IAB TCF 2.0;Real-Time CDP;
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 0%

---

# IAB TCF 2.0 steun in de Adobe Experience Platform Web SDK

De Adobe Experience Platform Web SDK ondersteunt het Interactive Advertising Bureau Transparency &amp; Consent Framework, versie 2.0 (IAB TCF 2.0). Deze gids toont de vereisten voor het steunen van IAB TCF 2.0 door het Web SDK van Adobe Experience Platform integreren met Adobe Real-Time Customer Data Platform, Audience Manager, de Gebeurtenissen van de Ervaring, Adobe Analytics, en Edge Network.

Bovendien zijn de volgende gidsen beschikbaar om in het leren te helpen hoe te om IAB TCF 2.0 met en zonder markeringen te integreren.

- [Met tags](./with-tags.md)
- [Zonder tags](./without-tags.md)

## Aan de slag

Om het Web SDK met IAB TCF 2.0 uit te voeren, moet u een werkend inzicht in het Model van de Gegevens van de Ervaring (XDM) en de Gebeurtenissen van de Ervaring hebben. Lees het volgende document voordat u begint:

- [ het overzicht van het Systeem van Gegevens van de Ervaring Model (XDM) ](../../../xdm/home.md): De normalisering en de interoperabiliteit zijn zeer belangrijke concepten achter Adobe Experience Platform. [!DNL Experience Data Model (XDM)] wordt aangestuurd door Adobe en is een poging om gegevens over de klantervaring te standaardiseren en schema&#39;s voor het beheer van de klantervaring te definiëren.

## Experience Platform-integratie

Als u toestemmingsgegevens naar Adobe Experience Platform wilt verzenden via de SDK, is het volgende vereist:

- Een dataset waarvan het schema is gebaseerd op de [!DNL XDM Individual Profile] -klasse en TCF 2.0-toestemmingsvelden bevat, die zijn ingeschakeld voor gebruik in [!DNL Real-Time Customer Profile] .
- Een gegevensstroom die opstelling met Experience Platform en de profiel-Toegelaten dataset hierboven wordt vermeld.

Gelieve te verwijzen naar de gids op [ TCF 2.0 naleving ](../../../landing/governance-privacy-security/consent/iab/overview.md) voor instructies bij het creëren van de vereiste datasets en datastream.

## Audience Manager-integratie

Adobe Audience Manager (AAM) omvat steun voor IAB TCF 2.0, die u toelaat om, klant privacykeuzen aan stroomafwaartse partners te evalueren te respecteren en door:sturen. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Als u wilt integreren met Audience Manager via Adobe Experience Platform Web SDK, dient u een gegevensstroom in te stellen die u naar Adobe Audience Manager kunt doorsturen.

## Experience Events en Adobe Analytics-integratie

Terwijl het Real-Time CDP- en Audience Manager-publiek de huidige voorkeuren voor toestemming van een klant bijhoudt, kunnen Experience Events voorkeuren voor toestemming van een klant aanhouden die actief waren toen de gebeurtenis werd verzameld.

Om toestemmingsinformatie over gebeurtenissen te verzamelen, wordt het volgende vereist:

- Een gegevensset die is gebaseerd op de klasse [!DNL XDM Experience Event] , met de veldgroep met het [!DNL Experience Event] privacyschema.
- Een gegevensstroom die is ingesteld met de [!DNL XDM Experience Event] dataset hierboven.

Voor meer informatie over hoe te om een Gebeurtenis van de Ervaring XDM in een hit van Analytics om te zetten, zie [ Verzendende gegevens naar Adobe Analytics gebruikend het Web SDK ](/help/web-sdk/use-cases/adobe-analytics.md).

## Integratie van Adobe Experience Platform Web SDK

In de onderstaande secties worden de belangrijkste integratiepunten tussen IAB TCF 2.0 en Adobe Experience Platform Web SDK beschreven.

>[!NOTE]
>
>Zelfs zonder Real-Time CDP of Audience Manager opstelling, kunt u IAB TCF 2.0 met het Web SDK nog integreren. De toestemmingsvoorkeur kan worden gebruikt om de inzameling van de Gebeurtenissen van de Ervaring te controleren en een identiteitskoekje te plaatsen.

### Standaardtoestemming

De standaardtoestemming wordt gebruikt wanneer er geen toestemmingsvoorkeur reeds voor een klant wordt bewaard. Dit betekent dat de standaardopties voor toestemming het gedrag van Adobe Experience Platform Web SDK kunnen bepalen en kunnen veranderen op basis van het gebied van een klant.

Als u bijvoorbeeld een klant hebt die niet onder de algemene gegevensbeschermingsverordening (GDPR) valt, kan de standaardtoestemming worden ingesteld op `in`, maar binnen de jurisdictie van GDPR, kan de standaardtoestemming worden ingesteld op `pending` . Uw platform van het Beheer van de Toestemming (CMP) zou het gebied van de klant kunnen ontdekken en de vlag `gdprApplies` verstrekken aan IAB TCF 2.0. Deze markering kan worden gebruikt om de standaardtoestemming te plaatsen. Zie [`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md) voor meer informatie.

### Toestemming instellen wanneer deze wordt gewijzigd

Adobe Experience Platform Web SDK heeft een `setConsent` -opdracht waarmee de voorkeuren van uw klant voor toestemming aan alle Adobe-services worden doorgegeven met IAB TCF 2.0. Als u integreert met Real-Time CDP, wordt hiermee het profiel van uw klant bijgewerkt. Als u met Audience Manager integreert, worden hiermee de gegevens van uw klant bijgewerkt. Als u dit aanroept, wordt ook een cookie ingesteld met de voorkeur voor &#39;alles of niets&#39;-toestemming die bepaalt of toekomstige ervaringsgebeurtenissen mogen worden verzonden. Het is de bedoeling dat deze actie wordt opgeroepen wanneer de toestemming verandert. Bij het laden van toekomstige pagina&#39;s wordt het Edge Network toestemmingscookie gelezen om te bepalen of Experience Events kan worden verzonden en of een identiteitscookie kan worden ingesteld.

Net als bij de Audience Manager IAB TCF 2.0-integratie geeft de Edge Network toestemming wanneer een klant uitdrukkelijk zijn toestemming heeft gegeven voor de volgende doeleinden:

- **Doel 1:** opslag en/of toegangsinformatie over een apparaat
- **Doel 10:** ontwikkelt en verbetert producten
- **Speciaal Doel 1:** verzekert veiligheid, verhindert fraude, en zuivert. (Per IAB TCF verordeningen, wordt dit altijd goedgekeurd aan)
- **Vergunning van de Leverancier van Adobe:** Toestemming voor Adobe (Leverancier 565)

Voor meer informatie over het `setConsent` bevel, lees de specifieke documentatie van SDK van het Web over [ setConsent ](../../../web-sdk/commands/setconsent.md).

### Toestemming toevoegen aan Experience Events

Adobe Experience Platform Web SDK heeft een [`sendEvent`](/help/web-sdk/commands/sendevent/overview.md) -opdracht waarmee een Experience Event wordt verzameld. Als u integreert met Experience Events of Adobe Analytics en u de voorkeuren voor toestemming bij elke Experience Event wilt gebruiken, voegt u informatie over toestemming toe aan elke `sendEvent` -opdracht.

## Volgende stappen

Nu u een basisbegrip van de Transparantie IAB &amp; het Toegelaten Kader 2.0 hebt, gelieve te verwijzen naar één van beide gidsen bij het gebruiken van IAB TCF 2.0 [ met markeringen ](./with-tags.md) of [ zonder markeringen ](./without-tags.md).

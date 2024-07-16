---
title: IAB TCF 2.0 Steun in de SDK van het Web van Adobe Experience Platform
description: Leer hoe u IAB TCF 2.0-voorkeuren voor toestemming ondersteunt met de Adobe Experience Platform Web SDK
keywords: toestemming;setConsent;Profile Privacy Field group;Experience Event Privacy Field group;Privacy Field group;IAB TCF 2.0;Real-Time CDP;
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
source-git-commit: b08c6cf12a38f79e019544dea91913a77bd6490a
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 0%

---

# IAB TCF 2.0 steun in de SDK van het Web van Adobe Experience Platform

De Adobe Experience Platform Web SDK biedt ondersteuning voor het Interactive Advertising Bureau Transparency &amp; Consent Framework, versie 2.0 (IAB TCF 2.0). Deze gids toont de vereisten voor het steunen van IAB TCF 2.0 door het Web SDK van Adobe Experience Platform integreren met Adobe Real-time Customer Data Platform, Audience Manager, de Gebeurtenissen van de Ervaring, Adobe Analytics, en Edge Network.

Bovendien zijn de volgende gidsen beschikbaar om in het leren te helpen hoe te om IAB TCF 2.0 met en zonder markeringen te integreren.

- [Met tags](./with-tags.md)
- [Zonder tags](./without-tags.md)

## Aan de slag

Om het Web SDK met IAB TCF 2.0 uit te voeren, moet u een werkend inzicht in het Model van de Gegevens van de Ervaring (XDM) en de Gebeurtenissen van de Ervaring hebben. Lees het volgende document voordat u begint:

- [ het overzicht van het Systeem van Gegevens van de Ervaring Model (XDM) ](../../../xdm/home.md): De normalisering en de interoperabiliteit zijn zeer belangrijke concepten achter Adobe Experience Platform. [!DNL Experience Data Model (XDM)], aangedreven door Adobe, is een inspanning om de gegevens van de klantenervaring te standaardiseren en schema&#39;s voor het beheer van de klantenervaring te bepalen.

## Integratie van Experience Platform

Als u toestemmingsgegevens naar Adobe Experience Platform wilt verzenden met behulp van de SDK, is het volgende vereist:

- Een dataset waarvan het schema is gebaseerd op de [!DNL XDM Individual Profile] -klasse en TCF 2.0-toestemmingsvelden bevat, die zijn ingeschakeld voor gebruik in [!DNL Real-Time Customer Profile] .
- Een gegevensstroomopstelling met Platform en de profiel-Toegelaten dataset hierboven vermeld.

Gelieve te verwijzen naar de gids op [ TCF 2.0 naleving ](../../../landing/governance-privacy-security/consent/iab/overview.md) voor instructies bij het creëren van de vereiste datasets en datastream.

## Integratie van Audience Managers

Adobe Audience Manager (AAM) omvat steun voor IAB TCF 2.0, die u toelaat om, klant privacykeuzen aan stroomafwaartse partners te evalueren te respecteren en door:sturen. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Om met Audience Manager door het Web SDK van Adobe Experience Platform te integreren, zorg ervoor u een gegevensstroom hebt die opstelling aan Adobe Audience Manager door:sturen.

## Experience Events en Adobe Analytics-integratie

Terwijl het publiek van Real-Time CDP en de Audience Manager de huidige voorkeuren voor toestemming van een klant bijhoudt, kunnen de Experience Events voorkeuren voor toestemming van een klant aanhouden die actief waren toen de gebeurtenis werd verzameld.

Om toestemmingsinformatie over gebeurtenissen te verzamelen, wordt het volgende vereist:

- Een gegevensset die is gebaseerd op de klasse [!DNL XDM Experience Event] , met de veldgroep met het [!DNL Experience Event] privacyschema.
- Een gegevensstroom die is ingesteld met de [!DNL XDM Experience Event] dataset hierboven.

Voor meer informatie over hoe te om een Gebeurtenis van de Ervaring XDM in een hit van Analytics om te zetten, zie [ Verzendende gegevens aan Adobe Analytics gebruikend het Web SDK ](/help/web-sdk/use-cases/adobe-analytics.md).

## Integratie van Adobe Experience Platform Web SDK

In de onderstaande secties worden de belangrijkste integratiepunten tussen IAB TCF 2.0 en Adobe Experience Platform Web SDK beschreven.

>[!NOTE]
>
>Zelfs zonder Real-Time CDP of Audience Manager opstelling, kunt u IAB TCF 2.0 met het Web SDK nog integreren. De toestemmingsvoorkeur kan worden gebruikt om de inzameling van de Gebeurtenissen van de Ervaring te controleren en een identiteitskoekje te plaatsen.

### Standaardtoestemming

De standaardtoestemming wordt gebruikt wanneer er geen toestemmingsvoorkeur reeds voor een klant wordt bewaard. Dit betekent dat de opties voor standaardtoestemming het gedrag van Adobe Experience Platform Web SDK kunnen bepalen en kunnen wijzigen op basis van het gebied van een klant.

Als u bijvoorbeeld een klant hebt die niet onder de algemene gegevensbeschermingsverordening (GDPR) valt, kan de standaardtoestemming worden ingesteld op `in`, maar binnen de jurisdictie van GDPR, kan de standaardtoestemming worden ingesteld op `pending` . Uw platform van het Beheer van de Toestemming (CMP) zou het gebied van de klant kunnen ontdekken en de vlag `gdprApplies` verstrekken aan IAB TCF 2.0. Deze markering kan worden gebruikt om de standaardtoestemming te plaatsen. Zie [`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md) voor meer informatie.

### Toestemming instellen wanneer deze wordt gewijzigd

Adobe Experience Platform Web SDK heeft een opdracht `setConsent` , die de voorkeuren van uw klant voor toestemming aan alle Adobe-services doorgeeft met IAB TCF 2.0. Als u integreert met Real-Time CDP, wordt hiermee het profiel van uw klant bijgewerkt. Als u met Audience Manager integreert, werkt dit de informatie van uw klant bij. Als u dit aanroept, wordt ook een cookie ingesteld met de voorkeur voor &#39;alles of niets&#39;-toestemming die bepaalt of toekomstige ervaringsgebeurtenissen mogen worden verzonden. Het is de bedoeling dat deze actie wordt opgeroepen wanneer de toestemming verandert. Wanneer de pagina later wordt geladen, wordt het instemmingscookie van de Edge Network gelezen om te bepalen of Experience Events kan worden verzonden en of een identiteitscookie kan worden ingesteld.

Net als bij de IAB TCF 2.0-integratie van Audience Managers geeft de Edge Network toestemming wanneer een klant uitdrukkelijk zijn toestemming heeft gegeven voor de volgende doeleinden:

- **Doel 1:** opslag en/of toegangsinformatie over een apparaat
- **Doel 10:** ontwikkelt en verbetert producten
- **Speciaal Doel 1:** verzekert veiligheid, verhindert fraude, en zuivert. (Per IAB TCF verordeningen, wordt dit altijd goedgekeurd aan)
- **de Toestemming van de Leverancier van de Adobe:** Toestemming voor Adobe (Leverancier 565)

Voor meer informatie over het `setConsent` bevel, lees de specifieke documentatie van SDK van het Web over [ setConsent ](../../../web-sdk/commands/setconsent.md).

### Toestemming toevoegen aan Experience Events

Adobe Experience Platform Web SDK heeft een [`sendEvent`](/help/web-sdk/commands/sendevent/overview.md) -opdracht waarmee een Experience Event wordt verzameld. Als u integreert met Experience Events of Adobe Analytics en u de voorkeuren voor toestemming bij elke Experience Event wilt gebruiken, voegt u informatie over toestemming toe aan elke `sendEvent` -opdracht.

## Volgende stappen

Nu u een basisbegrip van de Transparantie IAB &amp; het Toegelaten Kader 2.0 hebt, gelieve te verwijzen naar één van beide gidsen bij het gebruiken van IAB TCF 2.0 [ met markeringen ](./with-tags.md) of [ zonder markeringen ](./without-tags.md).

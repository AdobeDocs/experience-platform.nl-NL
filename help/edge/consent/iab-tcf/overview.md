---
title: IAB TCF 2.0 Steun in de SDK van het Web van Adobe Experience Platform
description: Leer hoe u IAB TCF 2.0-voorkeuren voor toestemming ondersteunt met de Adobe Experience Platform Web SDK
keywords: toestemming;setConsent;Profile Privacy Field group;Experience Event Privacy Field group;Privacy Field group;IAB TCF 2.0;Real-Time CDP;
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 0%

---

# IAB TCF 2.0 steun in de SDK van het Web van Adobe Experience Platform

De Adobe Experience Platform Web SDK ondersteunt het Interactive Advertising Bureau Transparency &amp; Consent Framework, versie 2.0 (IAB TCF 2.0). Deze gids toont de vereisten voor het steunen van IAB TCF 2.0 door het Web SDK van Adobe Experience Platform integreren met Adobe Real-time Customer Data Platform, Audience Manager, de Gebeurtenissen van de Ervaring, Adobe Analytics, en het Netwerk van de Rand.

Bovendien zijn de volgende gidsen beschikbaar om in het leren te helpen hoe te om IAB TCF 2.0 met en zonder markeringen te integreren.

- [Met tags](./with-launch.md)
- [Zonder tags](./without-launch.md)

## Aan de slag

Om het Web SDK met IAB TCF 2.0 uit te voeren, moet u een werkend inzicht in het Model van de Gegevens van de Ervaring (XDM) en de Gebeurtenissen van de Ervaring hebben. Lees het volgende document voordat u begint:

- [Overzicht van XDM (Experience Data Model)](../../../xdm/home.md): Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter Adobe Experience Platform. [!DNL Experience Data Model (XDM)], aangedreven door Adobe, is een inspanning om de gegevens van de klantenervaring te standaardiseren en schema&#39;s voor het beheer van de klantenervaring te bepalen.

## Integratie van Experience Platform

Als u toestemmingsgegevens naar Adobe Experience Platform wilt verzenden met behulp van de SDK, is het volgende vereist:

- Een dataset het waarvan schema op wordt gebaseerd [!DNL XDM Individual Profile] klasse en bevat TCF 2.0 toestemmingsgebieden, toegelaten voor gebruik in [!DNL Real-Time Customer Profile].
- Een gegevensstroomopstelling met Platform en de profiel-Toegelaten dataset hierboven vermeld.

Raadpleeg de handleiding op [Compatibiliteit met TCF 2.0](../../../landing/governance-privacy-security/consent/iab/overview.md) voor instructies over het creëren van de vereiste datasets en datastream.

## Integratie van Audience Managers

Adobe Audience Manager (AAM) omvat steun voor IAB TCF 2.0, die u toelaat om, klant privacykeuzen aan stroomafwaartse partners te evalueren te respecteren en door:sturen. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Om met Audience Manager door het Web SDK van Adobe Experience Platform te integreren, zorg ervoor u een gegevensstroom hebt die opstelling aan Adobe Audience Manager door:sturen.

## Experience Events en Adobe Analytics-integratie

Terwijl het publiek van Real-Time CDP en de Audience Manager de huidige voorkeuren voor toestemming van een klant bijhoudt, kunnen de Experience Events voorkeuren voor toestemming van een klant aanhouden die actief waren toen de gebeurtenis werd verzameld.

Om toestemmingsinformatie over gebeurtenissen te verzamelen, wordt het volgende vereist:

- Een gegevensset gebaseerd op de [!DNL XDM Experience Event] klasse, met de [!DNL Experience Event] veldgroep privacyschema.
- Een gegevensstroom die met [!DNL XDM Experience Event] dataset hierboven.

Voor meer informatie over het omzetten van een XDM Experience-gebeurtenis naar een Analytics-hit, begint u met het lezen van de [Overzicht van analysemogelijkheden](../../data-collection/adobe-analytics/analytics-overview.md) documentatie.

## Integratie van Adobe Experience Platform Web SDK

In de onderstaande secties worden de belangrijkste integratiepunten tussen IAB TCF 2.0 en Adobe Experience Platform Web SDK beschreven.

>[!NOTE]
>
>Zelfs zonder Real-Time CDP of Audience Manager opstelling, kunt u IAB TCF 2.0 met het Web SDK nog integreren. De toestemmingsvoorkeur kan worden gebruikt om de inzameling van de Gebeurtenissen van de Ervaring te controleren en een identiteitskoekje te plaatsen.

### Standaardtoestemming

De standaardtoestemming wordt gebruikt wanneer er geen toestemmingsvoorkeur reeds voor een klant wordt bewaard. Dit betekent dat de opties voor standaardtoestemming het gedrag van Adobe Experience Platform Web SDK kunnen bepalen en kunnen wijzigen op basis van het gebied van een klant.

Als u bijvoorbeeld een klant hebt die niet onder de algemene gegevensbeschermingsverordening (GDPR) valt, kan de standaardtoestemming worden ingesteld op `in`, maar binnen de jurisdictie van de GDPR kan de toestemming tot wanbetaling worden ingesteld op `pending`. Uw CMP (Consent Management Platform) kan het gebied van de klant detecteren en de vlag voorzien `gdprApplies` naar IAB TCF 2.0. Deze markering kan worden gebruikt om de standaardtoestemming te plaatsen.

Raadpleeg voor meer informatie over de toestemming bij wanbetaling de [sectie voor standaardtoestemming](../../fundamentals/configuring-the-sdk.md#default-consent) in de SDK-configuratiedocumentatie.

### Toestemming instellen wanneer deze wordt gewijzigd

Adobe Experience Platform Web SDK heeft een `setConsent` , waarmee de voorkeuren van uw klant voor toestemming aan alle Adobe-services worden doorgegeven met IAB TCF 2.0. Als u integreert met Real-Time CDP, wordt hiermee het profiel van uw klant bijgewerkt. Als u met Audience Manager integreert, werkt dit de informatie van uw klant bij. Als u dit aanroept, wordt ook een cookie ingesteld met de voorkeur voor &#39;alles of niets&#39;-toestemming die bepaalt of toekomstige ervaringsgebeurtenissen mogen worden verzonden. Het is de bedoeling dat deze actie wordt opgeroepen wanneer de toestemming verandert. Bij toekomstige paginaladingen wordt het Edge Network-toestemmingscookie gelezen om te bepalen of Experience Events kan worden verzonden en of een identiteitscookie kan worden ingesteld.

Net als bij de IAB TCF 2.0-integratie van Audience Manager geeft het Edge Network toestemming wanneer een klant expliciet zijn toestemming heeft gegeven voor de volgende doeleinden:

- **Doel 1:** Informatie opslaan en/of openen op een apparaat
- **Doelstelling 10:** Producten ontwikkelen en verbeteren
- **Speciaal doel 1:** Zorgen voor beveiliging, fraude voorkomen en fouten opsporen. (Per IAB TCF verordeningen, wordt dit altijd goedgekeurd aan)
- **Machtiging leverancier Adobe:** Goedkeuring voor Adobe (leverancier 565)

Voor meer informatie over de `setConsent` de documentatie lezen op [Ondersteunende toestemming](../../consent/supporting-consent.md).

### Toestemming toevoegen aan Experience Events

Adobe Experience Platform Web SDK heeft een `sendEvent` gebruiken die een Experience Event verzamelt. Als u integreert met Experience Events of Adobe Analytics en u de voorkeuren voor toestemming wilt gebruiken voor elke Experience Event, moet u de gegevens voor toestemming toevoegen aan elke `sendEvent` gebruiken.

Voor meer informatie over de `sendEvent` de documentatie lezen op [bijhouden, gebeurtenissen](../../fundamentals/tracking-events.md).

## Volgende stappen

Nu u een basisbegrip van IAB Transparency &amp; Consent Kader 2.0 hebt, gelieve te verwijzen naar één van beide gidsen bij het gebruiken van IAB TCF 2.0 [met tags](./with-launch.md) of [zonder tags](./without-launch.md).

---
title: IAB TCF 2.0 Steun in de SDK van het Web van Adobe Experience Platform
description: Leer hoe u IAB TCF 2.0-voorkeuren voor toestemming ondersteunt met de Adobe Experience Platform Web SDK
keywords: toestemming;setConsent;Profile Privacy Mixin;Experience Event Privacy Mixin;Privacy Mixin;IAB TCF 2.0;Real-time CDP;Real-time Customer Data Profile
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 0%

---


# IAB TCF 2.0 steun in de SDK van het Web van Adobe Experience Platform

De Adobe Experience Platform Web SDK biedt ondersteuning voor het Interactive Advertising Bureau Transparency &amp; Consent Framework, versie 2.0 (IAB TCF 2.0). In deze handleiding worden de vereisten voor ondersteuning van IAB TCF 2.0 via Adobe Experience Platform Web SDK weergegeven, die geïntegreerd zijn met Real-time Customer Data Platform, Audience Manager, Experience Events, Adobe Analytics en Experience Edge.

Bovendien zijn de volgende gidsen beschikbaar om in het leren te helpen hoe te om IAB TCF 2.0 met en zonder Adobe Experience Platform Launch te integreren.

- [Met Adobe Experience Platform Launch](./with-launch.md)
- [Zonder Adobe Experience Platform Launch](./without-launch.md)

## Aan de slag

Om het Web SDK met IAB TCF 2.0 uit te voeren, moet u een werkend inzicht in het Model van de Gegevens van de Ervaring (XDM) en de Gebeurtenissen van de Ervaring hebben. Lees het volgende document voordat u begint:

- [XDM-systeemoverzicht](../../../xdm/home.md) (Experience Data Model): Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter Adobe Experience Platform. [!DNL Experience Data Model (XDM)], gedreven door Adobe, is een inspanning om de gegevens van de klantenervaring te standaardiseren en schema&#39;s voor het beheer van de klantenervaring te bepalen.

## Integratie van Experience Platform

Als u toestemmingsgegevens naar Adobe Experience Platform wilt verzenden met behulp van de SDK, is het volgende vereist:

- Een dataset het waarvan schema gebaseerd is op de [!DNL XDM Individual Profile] klasse en TCF 2.0 toestemmingsgebieden bevat, die voor gebruik in [!DNL Real-time Customer Profile] worden toegelaten.
- Een randconfiguratie opstelling met Platform en de profiel-Toegelaten dataset hierboven vermeld.

Raadpleeg de handleiding bij [TCF 2.0-compatibiliteit](../../../landing/governance-privacy-security/consent/iab/overview.md) voor instructies voor het maken van de vereiste datasets en randconfiguratie.

## Audience Manager-integratie

Adobe Audience Manager (AAM) omvat steun voor IAB TCF 2.0, die u toelaat om, klant privacykeuzen aan stroomafwaartse partners te evalueren te respecteren en door:sturen. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Om met Audience Manager door het Web SDK van Adobe Experience Platform te integreren, zorg ervoor u een randconfiguratie opstelling hebt om aan Adobe Audience Manager door:sturen.

## Experience Events en Adobe Analytics-integratie

Terwijl CDP in real time en het publiek van de Audience Manager spoor van de huidige toestemmingsvoorkeur van een klant houden, kunnen de Gebeurtenissen van de Ervaring de toestemmingsvoorkeur van een klant houden die actief was toen de gebeurtenis werd verzameld.

Om toestemmingsinformatie over gebeurtenissen te verzamelen, wordt het volgende vereist:

- Een dataset die op de [!DNL XDM Experience Event] klasse, met [!DNL Experience Event] privacymengsel wordt gebaseerd.
- Een randconfiguratie opstelling met de [!DNL XDM Experience Event] dataset hierboven.

Voor meer informatie over hoe te om een Gebeurtenis van de Ervaring XDM in een hit van de Analyse om te zetten, begin door [Analytics te lezen overzicht](../../data-collection/adobe-analytics/analytics-overview.md) documentatie.

## Integratie van Adobe Experience Platform Web SDK

In de onderstaande secties worden de belangrijkste integratiepunten tussen IAB TCF 2.0 en Adobe Experience Platform Web SDK beschreven.

>[!NOTE]
>
>Zelfs zonder Echte - tijd CDP of opstelling van de Audience Manager, kunt u IAB TCF 2.0 met het Web SDK nog integreren. De toestemmingsvoorkeur kan worden gebruikt om de inzameling van de Gebeurtenissen van de Ervaring te controleren en een identiteitskoekje te plaatsen.

### Standaardtoestemming

De standaardtoestemming wordt gebruikt wanneer er geen toestemmingsvoorkeur reeds voor een klant wordt bewaard. Dit betekent dat de opties voor standaardtoestemming het gedrag van Adobe Experience Platform Web SDK kunnen bepalen en kunnen wijzigen op basis van het gebied van een klant.

Als u bijvoorbeeld een klant hebt die niet onder de algemene gegevensbeschermingsverordening (GDPR) valt, kan de standaardtoestemming worden ingesteld op `in`, maar binnen de jurisdictie van GDPR, kan de standaardtoestemming worden ingesteld op `pending`. Uw cloudbeheerplatform (CMP) kan het gebied van de klant detecteren en de vlag `gdprApplies` leveren aan IAB TCF 2.0. Deze markering kan worden gebruikt om de standaardtoestemming te plaatsen.

Raadpleeg voor meer informatie over de standaardtoestemming de sectie [standaardtoestemming](../../fundamentals/configuring-the-sdk.md#default-consent) in de SDK-configuratiedocumentatie.

### Toestemming instellen wanneer deze verandert

Adobe Experience Platform Web SDK heeft de opdracht `setConsent`, die de voorkeuren van uw klant voor toestemming doorgeeft aan alle Adobe-services met IAB TCF 2.0. Als u met CDP in real time integreert, werkt dit het profiel van uw klant bij. Als u met Audience Manager integreert, werkt dit de informatie van uw klant bij. Als u dit aanroept, wordt ook een cookie ingesteld met de voorkeur voor &#39;alles of niets&#39;-toestemming die bepaalt of toekomstige ervaringsgebeurtenissen mogen worden verzonden. Het is de bedoeling dat deze actie wordt opgeroepen wanneer de toestemming verandert. Wanneer de pagina later wordt geladen, wordt het Jaap Edge-toestemmingscookie gelezen om te bepalen of Experience Events kan worden verzonden en of een identiteitscookie kan worden ingesteld.

Gelijkaardig aan de integratie van IAB TCF 2.0 van Audience Manager, geeft de Rand van de Ervaring toestemming wanneer een klant hun uitdrukkelijke toestemming voor de volgende doeleinden heeft verstrekt:

- **Doelstelling 1:Informatie** opslaan en/of openen op een apparaat
- **Doelstelling 10:** Producten ontwikkelen en verbeteren
- **Speciaal doel 1:** Zorgen voor beveiliging, fraude voorkomen en fouten opsporen. (Per IAB TCF verordeningen, wordt dit altijd goedgekeurd aan)
- **Adobe-machtiging leverancier:** toestemming voor Adobe (leverancier 565)

Voor meer informatie over `setConsent` bevel, lees de documentatie over [Ondersteunende Toestemming](../../consent/supporting-consent.md).

### Toestemming toevoegen aan Experience Events

Adobe Experience Platform Web SDK heeft een opdracht `sendEvent` die een Experience Event verzamelt. Als u integreert met Experience Events of Adobe Analytics en u de voorkeuren voor toestemming wilt gebruiken voor elke Experience Event, moet u de gegevens voor de toestemming toevoegen aan elke `sendEvent`-opdracht.

Lees de documentatie over [gebeurtenissen bijhouden](../../fundamentals/tracking-events.md) voor meer informatie over de opdracht `sendEvent`.

## Volgende stappen

Nu u een basisbegrip van IAB Transparency &amp; Consent Kader 2.0 hebt, gelieve te verwijzen naar één van beide gidsen bij het gebruiken van IAB TCF 2.0 [met Adobe Experience Platform Launch](./with-launch.md) of [zonder Adobe Experience Platform Launch](./without-launch.md).

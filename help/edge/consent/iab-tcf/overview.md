---
title: IAB-overzicht van transparantie en instemming in framework 2.0
seo-title: Ondersteuning van de Adobe Experience Platform Web SDK-toestemmingsvoorkeuren van het Interactive Advertising Bureau Transparency & Consent Framework 2.0
description: Leer hoe te om IAB TCF 2.0 toestemmingsvoorkeur met het Web SDK van het Experience Platform te steunen
seo-description: Leer hoe te om IAB TCF 2.0 toestemmingsvoorkeur met het Web SDK van het Experience Platform te steunen
keywords: consent;setConsent;Profile Privacy Mixin;Experience Event Privacy Mixin;Privacy Mixin;IAB TCF 2.0;Real-time CDP;Real-time Customer Data Profile
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 0%

---


# IAB-overzicht van transparantie en instemming in framework 2.0

De Adobe Experience Platform Web SDK (AEP Web SDK) biedt ondersteuning voor het Interactive Advertising Bureau Transparency &amp; Consent Framework, versie 2.0 (IAB TCF 2.0). Deze gids toont de vereisten voor het steunen van IAB TCF 2.0 door het Web SDK van AEP die met het Platform van de Gegevens van de Klant in real time, Audience Manager, de Gebeurtenissen van de Ervaring, Adobe Analytics, en de Rand van de Ervaring integreert.

Bovendien zijn de volgende gidsen beschikbaar om in het leren te helpen hoe te om IAB TCF 2.0 met en zonder Adobe Experience Platform Launch te integreren.

- [Met Adobe Experience Platform Launch](./with-launch.md)
- [Zonder Adobe Experience Platform Launch](./without-launch.md)

## Aan de slag

Om AEP Web SDK met IAB TCF 2.0 uit te voeren, wordt het vereist dat u een werkend inzicht in het Model van de Gegevens van de Ervaring (XDM) en de Gebeurtenissen van de Ervaring hebt. Lees het volgende document voordat u begint:

- [XDM-systeemoverzicht](../../../xdm/home.md)(Experience Data Model): Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter Adobe Experience Platform. [!DNL Experience Data Model (XDM)], gedreven door Adobe, is een inspanning om de gegevens van de klantenervaring te standaardiseren en schema&#39;s voor het beheer van de klantenervaring te bepalen.

## Integratie van het Platform voor realtime klantgegevens

Dankzij het Adobe Experience Platform-Platform (Real-time CDP) van Adobe-klantgegevens (Real-time Customer Data ) kunt u bekende en anonieme gegevens uit meerdere bedrijfsbronnen samenbrengen. Dit staat u toe om klantenprofielen tot stand te brengen die kunnen worden gebruikt om gepersonaliseerde klantenervaringen over alle kanalen en apparaten in real time te verstrekken. Om toestemmingsgegevens naar CDP in real time door AEP Web SDK te verzenden, wordt het volgende vereist:

- Een dataset die op de [!DNL XDM Individual Profile] klasse wordt gebaseerd, voor gebruik binnen [!DNL Real-time Customer Profile], met de de privacymengeling van het Profiel wordt toegelaten.
- Een opstelling van de randconfiguratie met CDP in real time, en de profiel dataset hierboven vermeld.

Gelieve te verwijzen naar de zelfstudie over het [creëren van datasets voor het vangen van TCF 2.0 toestemming](../../../rtcdp/privacy/iab/dataset-preparation.md) voor hoe te om de vereiste dataset tot stand te brengen.

Raadpleeg het compatibiliteitsoverzicht [van](../../../rtcdp/privacy/privacy-overview.md) IAB TCF 2.0 voor instructies over het maken van de randconfiguratie.

## Audience Manager-integratie

Adobe Audience Manager (AAM) omvat steun voor IAB TCF 2.0, die u toelaat om, klant privacykeuzen aan stroomafwaartse partners te evalueren te respecteren en door:sturen. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Om met Audience Manager door het Web SDK van AEP te integreren, zorg ervoor u een randconfiguratie opstelling hebt om aan Adobe Audience Manager door:sturen.

## Experience Events en Adobe Analytics-integratie

Terwijl CDP in real time en het publiek van de Audience Manager spoor van de huidige toestemmingsvoorkeur van een klant houden, kunnen de Gebeurtenissen van de Ervaring de toestemmingsvoorkeur van een klant houden die actief was toen de gebeurtenis werd verzameld.

Om toestemmingsinformatie over gebeurtenissen te verzamelen, wordt het volgende vereist:

- Een dataset die op de [!DNL XDM Experience Event] klasse, met de [!DNL Experience Event] privacymixin wordt gebaseerd.
- Een randconfiguratie opstelling met de hierboven [!DNL XDM Experience Event] dataset.

Voor meer informatie over hoe te om een Gebeurtenis van de Ervaring XDM in een hit van de Analyse om te zetten, begin door de documentatie van het [Analytics- overzicht](../../data-collection/adobe-analytics/analytics-overview.md) te lezen.

## Integratie AEP Web SDK

In de volgende secties worden de belangrijkste integratiepunten tussen IAB TCF 2.0 en AEP Web SDK beschreven.

>[!NOTE]
>
>Zelfs zonder Echte - tijd CDP of opstelling van de Audience Manager, kunt u IAB TCF 2.0 met het Web SDK nog integreren. De toestemmingsvoorkeur kan worden gebruikt om de inzameling van de Gebeurtenissen van de Ervaring te controleren en een identiteitskoekje te plaatsen.

### Standaardtoestemming

De standaardtoestemming wordt gebruikt wanneer er geen toestemmingsvoorkeur reeds voor een klant wordt bewaard. Dit betekent de standaardopties van de toestemming het gedrag van AEP Web SDK kunnen controleren en veranderen gebaseerd op het gebied van een klant.

Als u bijvoorbeeld een klant hebt die niet onder de jurisdictie van de algemene gegevensbeschermingsverordening (GDPR) valt, kan de standaardtoestemming worden ingesteld op `in`, maar binnen de jurisdictie van de GDPR, kan de standaardtoestemming worden ingesteld op `pending`. Uw cloudbeheerplatform (CMP) kan het gebied van de klant detecteren en de vlag leveren `gdprApplies` aan IAB TCF 2.0. Deze markering kan worden gebruikt om de standaardtoestemming te plaatsen.

Raadpleeg de sectie [over](../../fundamentals/configuring-the-sdk.md#default-consent) standaardtoestemming in de documentatie bij de SDK-configuratie voor meer informatie over standaardtoestemming.

### Toestemming instellen wanneer deze verandert

De AEP Web SDK heeft een `setConsent` bevel, dat de toestemmingsvoorkeur van uw klant aan alle diensten van de Adobe gebruikend IAB TCF 2.0 meedeelt. Als u met CDP in real time integreert, werkt dit het profiel van uw klant bij. Als u met Audience Manager integreert, werkt dit de informatie van uw klant bij. Als u dit aanroept, wordt ook een cookie ingesteld met de voorkeur voor &#39;alles of niets&#39;-toestemming die bepaalt of toekomstige ervaringsgebeurtenissen mogen worden verzonden. Het is de bedoeling dat deze actie wordt opgeroepen wanneer de toestemming verandert. Wanneer de pagina later wordt geladen, wordt het Jaap Edge-toestemmingscookie gelezen om te bepalen of Experience Events kan worden verzonden en of een identiteitscookie kan worden ingesteld.

Gelijkaardig aan de integratie van IAB TCF 2.0 van Audience Manager, geeft de Rand van de Ervaring toestemming wanneer een klant hun uitdrukkelijke toestemming voor de volgende doeleinden heeft verstrekt:

- **Doel 1:** Informatie opslaan en/of openen op een apparaat
- **Doelstelling 10:** Producten ontwikkelen en verbeteren
- **Speciaal doel 1:** Zorgen voor beveiliging, fraude voorkomen en fouten opsporen. (Per IAB TCF verordeningen, wordt dit altijd goedgekeurd aan)
- **Machtiging Adobe leverancier:** Goedkeuring voor Adobe (leverancier 565)

Voor meer informatie over het `setConsent` bevel, lees de documentatie over de [Ondersteunende Toestemming](../../consent/supporting-consent.md).

### Toestemming toevoegen aan Experience Events

AEP Web SDK heeft een `sendEvent` opdracht waarmee een Experience Event wordt verzameld. Als u integreert met Experience Events of Adobe Analytics en u de voorkeuren voor toestemming wilt gebruiken voor elke Experience Event, moet u de gegevens voor toestemming toevoegen aan elke `sendEvent` opdracht.

Voor meer informatie over het `sendEvent` bevel, lees de documentatie over het [volgen van gebeurtenissen](../../fundamentals/tracking-events.md).

## Volgende stappen

Nu u een basisbegrip van IAB Transparency &amp; Consent Kader 2.0 hebt, gelieve te verwijzen naar één van beiden van de gidsen bij het gebruiken van IAB TCF 2.0 [met Adobe Experience Platform Launch](./with-launch.md) of [zonder Adobe Experience Platform Launch](./without-launch.md).

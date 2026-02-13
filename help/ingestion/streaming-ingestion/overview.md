---
keywords: Experience Platform;home;populaire onderwerpen;gegevensinvoer;ingesloten gegevens;streaming;overzicht;streaming opname;latentie;streaming latentie;
solution: Experience Platform
title: Overzicht van streaming inscriptie
description: Meer informatie over streaming opname in Adobe Experience Platform.
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: 568208c9b2cb774bbbeed74ae2d456c87e99bca9
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# Overzicht van het opnemen van streaming

Streaming opname voor Adobe Experience Platform biedt gebruikers een methode om gegevens van client- en serverapparaten in real-time naar Experience Platform te verzenden.

## Wat kan je doen met streaming opname?

Met Adobe Experience Platform kunt u gecoördineerde, consistente en relevante ervaringen aansturen door een realtime klantprofiel voor elk van uw individuele klanten te genereren. Streaming opname speelt een belangrijke rol bij het samenstellen van deze profielen doordat u de gegevens van het Profiel met zo weinig mogelijk vertraging in het datumpomeer kunt leveren.

De volgende video is ontworpen om u te helpen bij het begrijpen van streaming opname en geeft een overzicht van de bovenstaande concepten.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Stream-profielrecords en [!DNL ExperienceEvents]

Met streaming opname kunnen gebruikers profielrecords streamen en [!DNL ExperienceEvents] in seconden naar Experience Platform om de realtime personalisatie te bevorderen. Alle gegevens die naar streaming opname-API&#39;s worden verzonden, blijven automatisch behouden in het datumpomeer.

Gelieve te lezen [ creeer een het stromen verbindingsgids ](../tutorials/create-streaming-connection.md) voor meer informatie.

### Stream naar gegevenssets

Zodra u zeker bent dat uw gegevens schoon zijn, kunt u uw datasets voor het Profiel van de Klant in real time en [!DNL Identity Service] toelaten.

Voor meer informatie bij het toelaten van een dataset voor Profiel en [!DNL Identity Service], te lezen gelieve [ een datasetgids ](/help/profile/tutorials/dataset-configuration.md) vormen.

## Wat is de verwachte latentie voor het stromen opname op Experience Platform?

>[!IMPORTANT]
>
>Guardrails voor het streamen van inname zijn gebonden aan de totale gebruiksrechten voor licenties die overeenkomen met de volledige organisatie. Daarnaast is het gebruik van gegevens in ontwikkelingssandboxen beperkt tot 10% van uw totale profielen. Voor meer informatie over de gebruiksrechten van de vergunning, lees de [ gids van de beste praktijken van het gegevensbeheer ](/help/landing/license-usage-and-guardrails/data-management-best-practices.md). Leren hoe te om grenzen aan uw het stromen productie te plaatsen, lees het [ overzicht van de Capaciteit ](../../landing/license-usage-and-guardrails/capacity.md).

| Bestemming | Verwachte vertraging |
| --------- | ---------------- |
| Real-Time Customer Profile | <ul><li>&lt; 15 minuten bij het 95e percentiel voor B2C-gegevensinname.</li><li>&lt; 30 minuten bij het 95e percentiel voor B2B-gegevensinname.</li></ul> |
| Gegevensmeer | &lt; 60 minuten |

## Vraag per seconden (RPS) om hulp bij het streamen van opname

In de onderstaande tabel vindt u een overzicht van de aanvraag per seconden voor het streamen van opname.

| RPS-limiet | Notities |
| --- | --- |
| 1000 verzoeken per seconde | Deze kunnen meerdere berichten bevatten wanneer het gebruiken van `/collection/batch` eindpunt. |
| 10000 individuele berichten per seconde | De berichten kunnen in minder daadwerkelijke verzoeken worden gegroepeerd wanneer het gebruiken van het `/collection/` eindpunt. |

>[!IMPORTANT]
>
>De afgedwongen grens wordt **60 verzoeken per minuut** wanneer het gebruiken van synchrone bevestiging aangezien het voor het zuiveren doeleinden bedoeld is.

## Adobe Experience Platform-extensie

Met de Adobe Experience Platform-extensie kunt u een nieuwe streamingverbinding maken. De extensie [!DNL Experience Platform] biedt acties voor het verzenden van bakens die zijn opgemaakt in [!DNL Experience Data Model] (XDM) voor realtime invoer naar [!DNL Experience Platform] . Bezoek de [ documentatie van de Uitbreiding van 0} Experience Platform {voor meer informatie.](/help/tags/extensions/client/web-sdk/overview.md)

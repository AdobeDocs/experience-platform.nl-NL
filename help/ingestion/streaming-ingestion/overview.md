---
keywords: Experience Platform;home;populaire onderwerpen;gegevensinvoer;ingesloten gegevens;streaming;overzicht;streaming opname;latentie;streaming latentie;
solution: Experience Platform
title: Overzicht van streaming inscriptie
topic-legacy: overview
description: Streaming opname voor Adobe Experience Platform biedt gebruikers een methode om gegevens van client- en serverapparaten in real-time naar het Experience Platform te verzenden.
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: 3ec4bfcb185459ec644ce1826e2a970cb6294538
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# Overzicht van het opnemen van streaming

Streaming invoer voor Adobe Experience Platform biedt gebruikers een methode om gegevens van client- en serverapparaten naar [!DNL Experience Platform] in real time.

## Wat kan je doen met streaming opname?

Met Adobe Experience Platform kunt u zorgen voor een gecoördineerde, consistente en relevante ervaring door een [!DNL Real-time Customer Profile] voor elk van uw individuele klanten. Streaming opname speelt een sleutelrol bij het samenstellen van deze profielen doordat u [!DNL Profile] gegevens in de [!DNL Data Lake] met zo weinig mogelijk vertraging.

De volgende video is ontworpen om u te helpen bij het begrijpen van streaming opname en geeft een overzicht van de bovenstaande concepten.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Stroomprofielrecords en [!DNL ExperienceEvents]

Met streaming opname kunnen gebruikers profielrecords streamen en [!DNL ExperienceEvents] tot [!DNL Platform] in seconden om realtime personalisatie te bevorderen. Alle gegevens die naar streaming opname-API&#39;s worden verzonden, blijven automatisch behouden in de [!DNL Data Lake].

Lees de [een verbindingsgids voor streaming maken](../tutorials/create-streaming-connection.md) voor meer informatie .

### Stream naar gegevenssets

Zodra u zeker bent dat uw gegevens schoon zijn, kunt u uw datasets toelaten voor [!DNL Real-time Customer Profile] en [!DNL Identity Service].

Voor meer informatie over het toelaten van een dataset voor [!DNL Profile] en [!DNL Identity Service], lees de [vormen een datasetgids](../../profile/tutorials/dataset-configuration.md).

## Wat is de verwachte latentie voor het stromen van opname op [!DNL Platform]?

| Bestemming | Verwachte vertraging |
| --------- | ---------------- |
| Klantprofiel in realtime | &lt; 1 minuut |
| Data Lake | &lt; 60 minuten |

## Vraag per seconden (RPS) om hulp bij het streamen van opname

In de onderstaande tabel vindt u een overzicht van de aanvraag per seconden voor het streamen van opname.

| RPS-limiet | Notities |
| --- | --- |
| 1000 verzoeken per seconde | Deze kunnen meerdere berichten bevatten wanneer u `/collection/batch` eindpunt. |
| 10000 individuele berichten per seconde | De berichten kunnen in minder daadwerkelijke verzoeken worden gegroepeerd wanneer het gebruiken van `/collection/batch` eindpunt. |

>[!IMPORTANT]
>
>De afgedwongen limiet wordt **60 verzoeken per minuut** bij synchrone validatie zoals bedoeld voor foutopsporingsdoeleinden.

## Adobe Experience Platform-extensie

Met de Adobe Experience Platform-extensie kunt u een nieuwe streamingverbinding maken. De [!DNL Experience Platform] extensie biedt acties voor het verzenden van bakens die zijn opgemaakt in [!DNL Experience Data Model] (XDM) voor real-time invoer naar [!DNL Experience Platform]. Ga naar [Extensie Experience Platform](../../tags/extensions/web/sdk/overview.md) documentatie voor meer informatie.

---
keywords: Experience Platform;home;popular topics;Real-time Customer Profile;Identity Service;
solution: Experience Platform
title: Zelfstudies voor realtime klantprofiel
topic: tutorial
description: In dit document worden de desbetreffende stappen beschreven en worden koppelingen weergegeven naar zelfstudies voor het voltooien van elke afzonderlijke workflow.
translation-type: tm+mt
source-git-commit: d3ece56d10b1940a5992906a65a50ffe2f7e4346
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---


# Configureren [!DNL Real-time Customer Profile] en [!DNL Identity Service]

Voor de configuratie [!DNL Real-time Customer Profile] voor uw organisatie moet u meerdere afzonderlijke workflows voltooien. In dit document worden de desbetreffende stappen beschreven en worden koppelingen weergegeven naar zelfstudies voor het voltooien van elke afzonderlijke workflow. Als u meer wilt weten over [!DNL Real-time Customer Profile]het profiel, leest u eerst het [profieloverzicht](../profile/home.md).

## Schema inschakelen voor [!DNL Profile] en [!DNL Identity]

Voordat gegevens in Adobe Experience Platform kunnen worden ingevoerd en bij het maken van [!DNL Real-time Customer Profiles]het schema kunnen worden gebruikt, moet een schema worden gemaakt dat de structuur bevat voor de gegevens die worden ingevoerd en dat schema moet zijn ingeschakeld voor gebruik in [!DNL Profile] en Adobe Experience Platform [!DNL Identity Service]. Voor geleidelijke instructies bij het creëren van een schema dat voor zowel [!DNL Profile] als [!DNL Identity Service], gelieve te verwijzen naar de leerprogramma&#39;s voor het [creëren van een schema gebruikend de Registratie API](../xdm/tutorials/create-schema-api.md) van het Schema of [het creëren van een schema gebruikend de Bouwer UI](../xdm/tutorials/create-schema-ui.md)van het Schema.

## Een dataset configureren voor [!DNL Profile] en [!DNL Identity]

Beginnen opnemend gegevens in [!DNL Profile], moet u een dataset hebben die behoorlijk voor gebruik met [!DNL Real-time Customer Profile] en [!DNL Identity Service]. is gevormd. Om te beginnen, volg een dataset voor Profiel en de zelfstudie [van de Identiteit](../profile/tutorials/dataset-configuration.md)vormen.

## Samenvoegingsbeleid configureren

Met Adobe Experience Platform kunt u gegevens uit meerdere bronnen samenvoegen en combineren om een volledig beeld van elk van uw individuele klanten te krijgen. Wanneer het brengen van deze gegevens samen, zijn het fusiebeleid de regels die [!DNL Platform] gebruiken om te bepalen hoe de gegevens aan voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om die verenigde mening tot stand te brengen. Gebruikend RESTful APIs of het gebruikersinterface, kunt u nieuw samenvoegbeleid tot stand brengen, bestaand beleid beheren, en een standaardsamenvoegbeleid voor uw organisatie plaatsen. Om met samenvoegbeleid in [!DNL Platform] UI te werken, bezoek de de gebruikersgids [van het](../profile/ui/merge-policies.md)fusiebeleid. Om met samenvoegbeleid te werken gebruikend Real-time API van het Profiel van de Klant, zie de de ontwikkelaarsgids [van het](../profile/api/merge-policies.md)fusiebeleid.

## Edge-projecties configureren

Om gecoördineerde, verenigbare, en gepersonaliseerde ervaringen voor uw klanten over veelvoudige kanalen in real time te drijven, moeten de juiste gegevens gemakkelijk beschikbaar en onophoudelijk bijgewerkt zijn aangezien de veranderingen gebeuren. Adobe maakt deze realtime toegang tot gegevens mogelijk door gebruik te maken van zogenaamde randen. [!DNL Experience Platform] Een rand is een geografisch geplaatste server die gegevens opslaat en deze gemakkelijk toegankelijk maakt voor toepassingen. De gegevens worden verpletterd aan een rand door een projectie, met een projectiebestemming die de rand bepaalt waarnaar de gegevens zullen worden verzonden, en een projectieconfiguratie die de specifieke informatie bepaalt die op de rand beschikbaar zal worden gemaakt. Raadpleeg de [!DNL Real-time Customer Profile] API- [subhandleiding voor randprojecties](../profile/api/edge-projections.md)voor meer informatie en om te gaan werken met randen.

## Volgende stappen

Zodra u [!DNL Real-time Customer Profile] voor uw organisatie hebt gevormd, kunt u beginnen gegevens aan individuele klantenprofielen toe te voegen en publiekssegmenten te creëren die op specifieke klantenattributen worden gebaseerd. Raadpleeg de volgende zelfstudies om aan de slag te gaan:

* [Gegevens toevoegen aan realtime klantprofiel](../profile/tutorials/add-profile-data.md)
* [Een segment maken](../segmentation/tutorials/create-a-segment.md)
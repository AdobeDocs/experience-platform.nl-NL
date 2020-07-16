---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Zelfstudies voor realtime klantprofiel
topic: tutorial
translation-type: tm+mt
source-git-commit: 5c5f6c4868e195aef76bacc0a1e5df3857647bde
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---


# Configureren [!DNL Real-time Customer Profile] en [!DNL Identity Service]

Voor de configuratie [!DNL Real-time Customer Profile] voor uw organisatie moet u meerdere afzonderlijke workflows voltooien. In dit document worden de desbetreffende stappen beschreven en worden koppelingen weergegeven naar zelfstudies voor het voltooien van elke afzonderlijke workflow. Meer informatie over [!DNL Real-time Customer Profile], begin door het overzicht [van het](../profile/home.md)Profiel te lezen.

## Schema inschakelen voor [!DNL Profile] en [!DNL Identity]

Alvorens de gegevens in Adobe Experience Platform kunnen worden opgenomen en in de verwezenlijking van [!DNL Real-time Customer Profiles]worden gebruikt, moet een schema worden gecreeerd om de structuur voor de gegevens te verstrekken die zullen worden opgenomen en dat schema moet voor gebruik in [!DNL Profile] en Adobe Experience Platform worden toegelaten [!DNL Identity Service]. Voor geleidelijke instructies bij het creëren van een schema dat voor zowel [!DNL Profile] als [!DNL Identity Service], gelieve te verwijzen naar de leerprogramma&#39;s voor het [creëren van een schema gebruikend de Registratie API](../xdm/tutorials/create-schema-api.md) van het Schema of [het creëren van een schema gebruikend de Bouwer UI](../xdm/tutorials/create-schema-ui.md)van het Schema.

## Een dataset configureren voor [!DNL Profile] en [!DNL Identity]

Beginnen opnemend gegevens in [!DNL Profile], moet u een dataset hebben die behoorlijk voor gebruik met [!DNL Real-time Customer Profile] en [!DNL Identity Service]. is gevormd. Om te beginnen, volg een dataset voor Profiel en de zelfstudie [van de Identiteit](../profile/tutorials/dataset-configuration.md)vormen.

## Samenvoegingsbeleid configureren

Met Adobe Experience Platform kunt u gegevens uit meerdere bronnen samenbrengen en combineren om een volledige weergave van elk van uw individuele klanten te bekijken. Wanneer het brengen van deze gegevens samen, zijn het fusiebeleid de regels die [!DNL Platform] gebruiken om te bepalen hoe de gegevens aan voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om die verenigde mening tot stand te brengen. Gebruikend RESTful APIs of het gebruikersinterface, kunt u nieuw samenvoegbeleid tot stand brengen, bestaand beleid beheren, en een standaardsamenvoegbeleid voor uw organisatie plaatsen. Om met samenvoegbeleid in [!DNL Platform] UI te werken, bezoek de de gebruikersgids [van het](../profile/ui/merge-policies.md)fusiebeleid. Om met samenvoegbeleid te werken gebruikend Real-time API van het Profiel van de Klant, zie de de ontwikkelaarsgids [van het](../profile/api/merge-policies.md)fusiebeleid.

## Edge-projecties configureren

Om gecoördineerde, verenigbare, en gepersonaliseerde ervaringen voor uw klanten over veelvoudige kanalen in real time te drijven, moeten de juiste gegevens gemakkelijk beschikbaar en onophoudelijk bijgewerkt zijn aangezien de veranderingen gebeuren. Adobe [!DNL Experience Platform] biedt realtime toegang tot gegevens via zogenaamde randen. Een rand is een geografisch geplaatste server die gegevens opslaat en deze gemakkelijk toegankelijk maakt voor toepassingen. De gegevens worden verpletterd aan een rand door een projectie, met een projectiebestemming die de rand bepaalt waarnaar de gegevens zullen worden verzonden, en een projectieconfiguratie die de specifieke informatie bepaalt die op de rand beschikbaar zal worden gemaakt. Raadpleeg de [!DNL Real-time Customer Profile] API- [subhandleiding voor randprojecties](../profile/api/edge-projections.md)voor meer informatie en om te gaan werken met randen.

## Volgende stappen

Zodra u [!DNL Real-time Customer Profile] voor uw organisatie hebt gevormd, kunt u beginnen gegevens aan individuele klantenprofielen toe te voegen en publiekssegmenten te creëren die op specifieke klantenattributen worden gebaseerd. Raadpleeg de volgende zelfstudies om aan de slag te gaan:

* [Gegevens toevoegen aan realtime klantprofiel](../profile/tutorials/add-profile-data.md)
* [Een segment maken](../segmentation/tutorials/create-a-segment.md)
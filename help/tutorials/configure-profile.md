---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Zelfstudies voor realtime klantprofiel
topic: tutorial
translation-type: tm+mt
source-git-commit: ee08f43400fa72abce95ed52aff879f954f4b4d6

---


# Klantprofiel en identiteitsservice in realtime configureren

Om het profiel van de Klant in real time voor uw organisatie te vormen, moet u veelvoudige afzonderlijke werkschema&#39;s voltooien. In dit document worden de desbetreffende stappen beschreven en worden koppelingen weergegeven naar zelfstudies voor het voltooien van elke afzonderlijke workflow. Voor meer informatie over het profiel van de klant in real time, begin door het overzicht [van het](../profile/home.md)Profiel te lezen.

## Schema voor profiel en identiteit inschakelen

Voordat gegevens kunnen worden opgenomen in het Adobe Experience Platform en kunnen worden gebruikt voor het maken van realtime-klantprofielen, moet een schema worden gemaakt dat de structuur biedt voor de gegevens die worden ingevoerd en dat schema moet zijn ingeschakeld voor gebruik in de Identity Service Profiel en Adobe Experience Platform. Voor geleidelijke instructies bij het creëren van een schema dat voor zowel de Dienst van het Profiel als van de Identiteit wordt toegelaten, gelieve te verwijzen naar de leerprogramma&#39;s voor het [creëren van een schema gebruikend de Registratie API](../xdm/tutorials/create-schema-api.md) van het Schema of [het creëren van een schema gebruikend de Bouwer UI](../xdm/tutorials/create-schema-ui.md)van het Schema.

## Een gegevensset configureren voor profiel en identiteit

Als u gegevens in het profiel wilt opnemen, moet u beschikken over een gegevensset die correct is geconfigureerd voor gebruik met het profiel en de identiteitsservice van realtime klanten. Om te beginnen, volg een dataset voor Profiel en de zelfstudie [van de Identiteit](../profile/tutorials/dataset-configuration.md)vormen.

## Samenvoegingsbeleid configureren

Met het Adobe Experience Platform kunt u gegevens uit meerdere bronnen samenvoegen en combineren om een volledig beeld van elk van uw individuele klanten te krijgen. Wanneer het brengen van deze gegevens samen, zijn het fusiebeleid de regels die het Platform gebruikt om te bepalen hoe de gegevens voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om die verenigde mening tot stand te brengen. Gebruikend RESTful APIs of het gebruikersinterface, kunt u nieuw samenvoegbeleid tot stand brengen, bestaand beleid beheren, en een standaardsamenvoegbeleid voor uw organisatie plaatsen. Om met samenvoegbeleid in de UI van het Platform te werken, bezoek de de gebruikersgids [van het](../profile/ui/merge-policies.md)fusiebeleid. Om met samenvoegbeleid te werken gebruikend Real-time API van het Profiel van de Klant, zie de de ontwikkelaarsgids [van het](../profile/api/merge-policies.md)fusiebeleid.

## Edge-projecties configureren

Om gecoördineerde, verenigbare, en gepersonaliseerde ervaringen voor uw klanten over veelvoudige kanalen in real time te drijven, moeten de juiste gegevens gemakkelijk beschikbaar en onophoudelijk bijgewerkt zijn aangezien de veranderingen gebeuren. Met het Adobe Experience Platform hebt u in real-time toegang tot gegevens via zogenaamde randen. Een rand is een geografisch geplaatste server die gegevens opslaat en deze gemakkelijk toegankelijk maakt voor toepassingen. De gegevens worden verpletterd aan een rand door een projectie, met een projectiebestemming die de rand bepaalt waarnaar de gegevens zullen worden verzonden, en een projectieconfiguratie die de specifieke informatie bepaalt die op de rand beschikbaar zal worden gemaakt. Raadpleeg de [subhandleiding Real-time Customer Profile API voor randprojecties](../profile/api/edge-projections.md)voor meer informatie en om met randen te gaan werken.

## Volgende stappen

Zodra u het Profiel van de Klant in real time voor uw organisatie hebt gevormd, kunt u beginnen gegevens aan individuele klantenprofielen toe te voegen en publiekssegmenten tot stand te brengen die op specifieke klantenattributen worden gebaseerd. Raadpleeg de volgende zelfstudies om aan de slag te gaan:

* [Gegevens toevoegen aan realtime klantprofiel](../profile/tutorials/add-profile-data.md)
* [Een segment maken](../segmentation/tutorials/create-a-segment.md)
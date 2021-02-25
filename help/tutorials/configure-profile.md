---
keywords: Experience Platform;thuis;populaire onderwerpen;Real-time profiel van de Klant;De Dienst van de Identiteit;
solution: Experience Platform
title: Zelfstudies voor realtime klantprofiel
topic: zelfstudie
type: Zelfstudie
description: In dit document worden de desbetreffende stappen beschreven en worden koppelingen weergegeven naar zelfstudies voor het voltooien van elke afzonderlijke workflow.
translation-type: tm+mt
source-git-commit: 0aa59a5375757f81d63ac43d778ff2c7179d449b
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 0%

---


# Configureren [!DNL Real-time Customer Profile]

Als u [!DNL Real-time Customer Profile] voor uw organisatie wilt configureren, moet u meerdere afzonderlijke workflows voltooien. In dit document worden de desbetreffende stappen beschreven en worden koppelingen weergegeven naar zelfstudies voor het voltooien van elke afzonderlijke workflow.

Als u meer wilt weten over [!DNL Real-time Customer Profile], leest u eerst het [Profieloverzicht](../profile/home.md).

## Overzicht gebruikersinterface voor realtime gebruikersprofiel

Het profiel van de Klant in real time leidt tot een holistische mening van elk van uw individuele klanten, die gegevens van veelvoudige kanalen met inbegrip van online, off-line, CRM, en derdegegevens combineren.

**Deze handleiding helpt u:**
- Lees de interface [!UICONTROL Profielen] en de beschikbare functies.
- De profielgegevens weergeven en beheren.

Voor meer informatie raadpleegt u de [Gebruikershandleiding voor realtime klantprofiel](../profile/ui/user-guide.md)

## Real-time API voor klantprofiel

De realtime-API voor klantprofiel bevat meerdere eindpunten. Lees het [Real-time overzicht van de API van het Profiel van de Klant](../profile/api/overview.md) voor meer informatie over elk van de beschikbare eindpunten en hun gebruiksgevallen.

Als u meer wilt weten en de vereiste waarden voor het uitvoeren van CRUD-bewerkingen met de Real-time Customer Profile API wilt opvragen, gaat u naar de [gids Aan de slag](../profile/api/getting-started.md).

## Een schema inschakelen voor [!DNL Profile]- en [!DNL Identity]-service

Voordat gegevens in Adobe Experience Platform kunnen worden ingevoerd en kunnen worden gebruikt bij het maken van [!DNL Real-time Customer Profiles], moet een schema worden gemaakt dat de structuur biedt voor de gegevens die worden ingevoerd en dat schema moet zijn ingeschakeld voor gebruik in [!DNL Profile] en Adobe Experience Platform [!DNL Identity Service].

**Deze handleiding helpt u:**
- Blader door bestaande schema&#39;s.
- Maak een schema en geef dit een naam.
- XDM-mixen toevoegen en definiëren.
- Stel uw schemavelden in als identiteitsvelden.
- Profiel inschakelen voor uw schema.

Voor geleidelijke instructies bij het creëren van een schema dat voor zowel [!DNL Profile] als [!DNL Identity Service] wordt toegelaten, gelieve te verwijzen naar de leerprogramma&#39;s voor [het creëren van een schema gebruikend de Registratie API ](../xdm/tutorials/create-schema-api.md) of [het creëren van een schema gebruikend de Bouwer van het Schema UI](../xdm/tutorials/create-schema-ui.md).

## Een gegevensset configureren voor [!DNL Profile] en [!DNL Identity]

Als u wilt beginnen met het opnemen van gegevens in [!DNL Profile], moet u een gegevensset hebben die correct is geconfigureerd voor gebruik met [!DNL Real-time Customer Profile] en [!DNL Identity Service].

**Deze handleiding helpt u:**
- Maak een gegevensset die is ingeschakeld voor Profiel.
- Vorm bestaande datasets.
- Voeg gegevens in de dataset in.
- Bevestig uw dataset toegelaten Profiel is en het gebruiken van de Dienst van de Identiteit.

Om te beginnen, volg de API leerprogramma&#39;s voor [het vormen van een dataset voor Profiel en Identiteit](../profile/tutorials/dataset-configuration.md).

## Samenvoegingsbeleid configureren

Met Adobe Experience Platform kunt u gegevens uit meerdere bronnen samenvoegen en combineren om een volledig beeld van elk van uw individuele klanten te krijgen. Wanneer het brengen van deze gegevens samen, zijn het fusiebeleid de regels die [!DNL Platform] gebruikt om te bepalen hoe de gegevens aan voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om die verenigde mening tot stand te brengen.

**Deze handleiding helpt u:**
- Nieuw samenvoegbeleid maken.
- Beheren van bestaand samenvoegbeleid.
- Stel een standaardsamenvoegbeleid in voor uw organisatie.
- Begrijp schendingen van het fusiebeleid.

Om met samenvoegbeleid in [!DNL Platform] UI te werken, bezoek [de gids van de gebruiker ](../profile/ui/merge-policies.md) van het samenvoegbeleid. Om met samenvoegbeleid te werken gebruikend Real-time API van het Profiel van de Klant, zie [de gids van de ontwikkelaar van samenvoegingsbeleid](../profile/api/merge-policies.md).

## Edge-projecties configureren

Om gecoördineerde, verenigbare, en gepersonaliseerde ervaringen voor uw klanten over veelvoudige kanalen in real time te drijven, moeten de juiste gegevens gemakkelijk beschikbaar en onophoudelijk bijgewerkt zijn aangezien de veranderingen gebeuren. Met Adobe [!DNL Experience Platform] hebt u in real time toegang tot gegevens via het gebruik van zogenaamde randen. Een rand is een geografisch geplaatste server die gegevens opslaat en deze gemakkelijk toegankelijk maakt voor toepassingen. De gegevens worden verpletterd aan een rand door een projectie, met een projectiebestemming die de rand bepaalt waarnaar de gegevens zullen worden verzonden, en een projectieconfiguratie die de specifieke informatie bepaalt die op de rand beschikbaar zal worden gemaakt.

**Deze handleiding helpt u:**
- Een doel voor randprojectie weergeven, maken, weergeven, bijwerken en verwijderen.
- Maak een lijst met randprojectieconfiguraties en maak deze.
- Inzicht in kiezers.

Raadpleeg de [!DNL Real-time Customer Profile] API [subhandleiding voor randprojecties](../profile/api/edge-projections.md) voor meer informatie en om te gaan werken met randen.

## Aanpassen hoe profielgegevens worden weergegeven in de gebruikersinterface

Binnen de gebruikersinterface van het Experience Platform kunt u gegevens van het Profiel van de Klant in real time bekijken en met elkaar in de vorm van klantenprofielen in wisselwerking staan. De profielgegevens die in de gebruikersinterface worden weergegeven, zijn samengevoegd vanuit meerdere profielfragmenten en vormen één weergave van elke afzonderlijke klant. Dit omvat details zoals basiskenmerken, gekoppelde identiteiten en kanaalvoorkeuren. De standaardvelden in profielen kunnen ook op organisatorisch niveau worden gewijzigd, zodat de voorkeursprofielkenmerken worden weergegeven.

**Deze handleiding helpt u:**
- U kunt kaarten opnieuw rangschikken, vergroten of verkleinen, bewerken en verwijderen.
- Kenmerken toevoegen.
- Voeg een nieuwe kaart toe.
- Standaardinstellingen herstellen.

Meer informatie over het aanpassen van profielgegevens, bezoek [de documentatie van de aanpassing van het Profiel](../profile/ui/profile-customization.md)

## Volgende stappen

Als u [!DNL Real-time Customer Profile] voor uw organisatie hebt geconfigureerd, kunt u beginnen met het toevoegen van gegevens aan individuele klantprofielen en het maken van publiekssegmenten op basis van specifieke klantkenmerken. Raadpleeg de volgende zelfstudies om aan de slag te gaan:

- [Gegevens toevoegen aan realtime klantprofiel](../profile/tutorials/add-profile-data.md)
- [Een segment maken](../segmentation/tutorials/create-a-segment.md)
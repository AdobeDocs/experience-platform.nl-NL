---
keywords: Experience Platform;home;popular topics;Real-time Customer Profile;Identity Service;
solution: Experience Platform
title: Zelfstudies voor realtime klantprofiel
topic: tutorial
type: Tutorial
description: In dit document worden de desbetreffende stappen beschreven en worden koppelingen weergegeven naar zelfstudies voor het voltooien van elke afzonderlijke workflow.
translation-type: tm+mt
source-git-commit: 844ef4a0131e41d3a7a3da319ccf7f8d5cf1f40d
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 0%

---


# Configureren [!DNL Real-time Customer Profile] en [!DNL Identity Service]

Voor de configuratie [!DNL Real-time Customer Profile] voor uw organisatie moet u meerdere afzonderlijke workflows voltooien. In dit document worden de desbetreffende stappen beschreven en worden koppelingen weergegeven naar zelfstudies voor het voltooien van elke afzonderlijke workflow.

Als u meer wilt weten over [!DNL Real-time Customer Profile]het profiel, leest u eerst het [profieloverzicht](../profile/home.md).

## Overzicht gebruikersinterface voor realtime gebruikersprofiel

Het profiel van de Klant in real time leidt tot een holistische mening van elk van uw individuele klanten, die gegevens van veelvoudige kanalen met inbegrip van online, off-line, CRM, en derdegegevens combineren.

**Deze handleiding helpt u:**
- De interface [!UICONTROL Profielen] en beschikbare functies begrijpen.
- De profielgegevens weergeven en beheren.

Voor meer informatie raadpleegt u de gebruikershandleiding van het [realtime klantprofiel](../profile/ui/user-guide.md)

## Real-time API voor klantprofiel

De realtime-API voor klantprofiel bevat meerdere eindpunten. Het profiel staat u toe om verschillende klantengegevens van veelvoudige kanalen, zoals online, off-line, CRM, en derdegegevens, in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt. Lees het API-overzicht [van het profiel van de](../profile/api/overview.md) real-time klant voor meer informatie over elk van de beschikbare eindpunten en de bijbehorende gebruiksgevallen.

**De volgende API-ontwikkelaarshulplijnen zijn beschikbaar:**
- [Berekende kenmerken (alfa) ](../profile/api/computed-attributes.md) - Leer meer over de gebruiksgevallen voor berekende kenmerken en hoe u een berekend kenmerk kunt configureren, openen, bijwerken en verwijderen.
- [Edge-projecties](../profile/api/edge-projections.md) - Leer hoe u projectiedoelen kunt maken, weergeven, bijwerken, verwijderen en weergeven. Bovendien bevat dit document informatie over het maken van een lijst met projectieconfiguraties en voorbeelden voor het gebruik van Kiezers.
- [Entiteiten (toegang tot profiel)](../profile/api/entities.md) - Leer hoe u toegang krijgt tot profielgegevens via identiteit of een lijst met identiteiten. Bovendien, leer hoe te om tot de gebeurtenissen van de tijdreeks voor veelvoudige profielen toegang te hebben gebruikend identiteiten, één enkel profiel door identiteit, en tot veelvoudige schemaentiteiten toegang te hebben.
- [Exporteer taken (Profielexport)](../profile/api/export-jobs.md) - Leer hoe u exporttaken kunt maken, weergeven, controleren en annuleren.
- [Beleid](../profile/api/merge-policies.md) voor samenvoegen - Leer meer over de componenten van het samenvoegbeleid en hoe u een samenvoegbeleid kunt openen, maken, bijwerken en verwijderen.
- [Voorbeeldstatus voorvertonen (voorvertoning van profiel)](../profile/api/preview-sample-status.md) - Leer hoe u de laatste voorbeeldstatus, de verdeling van het lijstprofiel per dataset en de verdeling van het lijstprofiel per naamruimte kunt weergeven.
- [Systeemtaken profiel (aanvragen verwijderen)](../profile/api/profile-system-jobs.md) - Leer hoe u een aanvraag voor een gegevensset of batch in de profielopslag kunt weergeven, maken en verwijderen.

Voor meer informatie en de vereiste waarden voor het uitvoeren van CRUD-bewerkingen met de Real-Time Customer Profile API, raadpleegt u de gids [Aan de slag](../profile/api/getting-started.md).

## Een schema voor [!DNL Profile] en [!DNL Identity] service inschakelen

Voordat gegevens in Adobe Experience Platform kunnen worden ingevoerd en bij het maken van [!DNL Real-time Customer Profiles]het schema kunnen worden gebruikt, moet een schema worden gemaakt dat de structuur bevat voor de gegevens die worden ingevoerd en dat schema moet zijn ingeschakeld voor gebruik in [!DNL Profile] en Adobe Experience Platform [!DNL Identity Service].

**Deze handleiding helpt u:**
- Blader door bestaande schema&#39;s.
- Maak een schema en geef dit een naam.
- XDM-mixen toevoegen en definiëren.
- Stel uw schemavelden in als identiteitsvelden.
- Profiel inschakelen voor uw schema.

Voor geleidelijke instructies bij het creëren van een schema dat voor zowel [!DNL Profile] als [!DNL Identity Service], gelieve te verwijzen naar de leerprogramma&#39;s voor het [creëren van een schema gebruikend de Registratie API](../xdm/tutorials/create-schema-api.md) van het Schema of [het creëren van een schema gebruikend de Bouwer UI](../xdm/tutorials/create-schema-ui.md)van het Schema.

## Een dataset configureren voor [!DNL Profile] en [!DNL Identity]

Beginnen opnemend gegevens in [!DNL Profile], moet u een dataset hebben die behoorlijk voor gebruik met [!DNL Real-time Customer Profile] en [!DNL Identity Service]. is gevormd.

**Deze handleiding helpt u:**
- Maak een gegevensset die is ingeschakeld voor Profiel.
- Vorm bestaande datasets.
- Voeg gegevens in de dataset in.
- Bevestig uw dataset toegelaten Profiel is en het gebruiken van de Dienst van de Identiteit.

Volg de API-zelfstudie om een gegevensset voor profiel en identiteit [te](../profile/tutorials/dataset-configuration.md)configureren om aan de slag te gaan.

## Samenvoegingsbeleid configureren

Met Adobe Experience Platform kunt u gegevens uit meerdere bronnen samenvoegen en combineren om een volledig beeld van elk van uw individuele klanten te krijgen. Wanneer het brengen van deze gegevens samen, zijn het fusiebeleid de regels die [!DNL Platform] gebruiken om te bepalen hoe de gegevens aan voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om die verenigde mening tot stand te brengen.

**Deze handleiding helpt u:**
- Nieuw samenvoegbeleid maken.
- Beheren van bestaand samenvoegbeleid.
- Stel een standaardsamenvoegbeleid in voor uw organisatie.
- Begrijp schendingen van het fusiebeleid.

Om met samenvoegbeleid in [!DNL Platform] UI te werken, bezoek de de gebruikersgids [van het](../profile/ui/merge-policies.md)fusiebeleid. Om met samenvoegbeleid te werken gebruikend Real-time API van het Profiel van de Klant, zie de de ontwikkelaarsgids [van het](../profile/api/merge-policies.md)fusiebeleid.

## Edge-projecties configureren

Om gecoördineerde, verenigbare, en gepersonaliseerde ervaringen voor uw klanten over veelvoudige kanalen in real time te drijven, moeten de juiste gegevens gemakkelijk beschikbaar en onophoudelijk bijgewerkt zijn aangezien de veranderingen gebeuren. Adobe maakt deze realtime toegang tot gegevens mogelijk door gebruik te maken van zogenaamde randen. [!DNL Experience Platform] Een rand is een geografisch geplaatste server die gegevens opslaat en deze gemakkelijk toegankelijk maakt voor toepassingen. De gegevens worden verpletterd aan een rand door een projectie, met een projectiebestemming die de rand bepaalt waarnaar de gegevens zullen worden verzonden, en een projectieconfiguratie die de specifieke informatie bepaalt die op de rand beschikbaar zal worden gemaakt.

**Deze handleiding helpt u:**
- Een doel voor randprojectie weergeven, maken, weergeven, bijwerken en verwijderen.
- Maak een lijst met randprojectieconfiguraties en maak deze.
- Inzicht in kiezers.

Raadpleeg de [!DNL Real-time Customer Profile] API- [subhandleiding voor randprojecties](../profile/api/edge-projections.md)voor meer informatie en om te gaan werken met randen.

## Aanpassen hoe profielgegevens worden weergegeven in de gebruikersinterface

Binnen de gebruikersinterface van het Experience Platform kunt u gegevens van het Profiel van de Klant in real time bekijken en met elkaar in de vorm van klantenprofielen in wisselwerking staan. De profielgegevens die in de gebruikersinterface worden weergegeven, zijn samengevoegd vanuit meerdere profielfragmenten en vormen één weergave van elke afzonderlijke klant. Dit omvat details zoals basiskenmerken, gekoppelde identiteiten en kanaalvoorkeuren. De standaardvelden in profielen kunnen ook op organisatorisch niveau worden gewijzigd, zodat de voorkeursprofielkenmerken worden weergegeven.

**Deze handleiding helpt u:**
- U kunt kaarten opnieuw rangschikken, vergroten of verkleinen, bewerken en verwijderen.
- Kenmerken toevoegen.
- Voeg een nieuwe kaart toe.
- Standaardinstellingen herstellen.

Meer informatie over het aanpassen van profielgegevens, bezoek de documentatie van de aanpassing van het [Profiel](../profile/ui/profile-customization.md)

## Volgende stappen

Zodra u [!DNL Real-time Customer Profile] voor uw organisatie hebt gevormd, kunt u beginnen gegevens aan individuele klantenprofielen toe te voegen en publiekssegmenten te creëren die op specifieke klantenattributen worden gebaseerd. Raadpleeg de volgende zelfstudies om aan de slag te gaan:

- [Gegevens toevoegen aan realtime klantprofiel](../profile/tutorials/add-profile-data.md)
- [Een segment maken](../segmentation/tutorials/create-a-segment.md)
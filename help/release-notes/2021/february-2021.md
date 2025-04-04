---
title: Aanvullende informatie voor Adobe Experience Platform van februari 2021
description: Aanvullende informatie voor Adobe Experience Platform van februari 2021.
doc-type: release notes
last-update: February 24, 2021
author: ens70167
exl-id: 8c3142af-4021-4f7e-acbd-c5277dd188d1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1139'
ht-degree: 20%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum: donderdag 24 februari 2021**

Nieuwe functies in Adobe Experience Platform:

- [(Beta) Dashboards](#dashboards)

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Dataflows]](#dataflows)
- [[!DNL Destinations]](#destinations)
- [[!DNL Experience Data Model (XDM) System]](#xdm)
- [[!DNL Identity Service]](#identity)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## (Beta) Dashboards {#dashboards}

Adobe Experience Platform biedt meerdere dashboards waarmee u belangrijke informatie over de gegevens van uw organisatie kunt bekijken, zoals vastgelegd tijdens dagelijkse momentopnamen.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Profielen, segmenten, doelen en gebruiksdashboards voor licenties (Beta) | **Nota: De functionaliteit van het dashboard is momenteel in bèta en is niet beschikbaar aan alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.**<br/><br/> dashboards verstrekken out-of-the-box rapporterend op de gegevens van uw organisatie en zijn direct gebouwd in het markeringswerkschema binnen Experience Platform. Deze dashboards zijn beschikbaar zonder de behoefte aan extra steun van IT of de tijd en de inspanning het anders zou vergen om gegevens met extra het opslagontwerp en implementatie van gegevens uit te voeren en te verwerken. |

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace maakt gebruik van machinaal leren en kunstmatige intelligentie om inzichten te creëren op basis van uw gegevens. Met Data Science Workspace, dat in Adobe Experience Platform is geïntegreerd, kunt u voorspellingen maken met behulp van uw inhoud en gegevenselementen voor alle Adobe-oplossingen.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| JupyterLab EDA-laptop | De exploratieve gegevensanalyse (EDA) Python-laptop is nu beschikbaar in Jupyterlab. Deze laptop is ontworpen om u te helpen bij het ontdekken van patronen in gegevens, het controleren van de hygiëne van gegevens en het samenvatten van de relevante gegevens voor voorspellende modellen. Zie het leerprogramma op [ het onderzoeken van web-based gegevens voor voorspellende modellen ](../../data-science-workspace/jupyterlab/eda-notebook.md) voor meer informatie. |

Voor meer algemene informatie over de Wetenschap van Gegevens Workspace, verwijs naar het [ overzicht van Workspace van de Wetenschap van Gegevens ](../../data-science-workspace/home.md).

## [!DNL Dataflows] {#dataflows}

In Adobe Experience Platform worden gegevens uit een groot aantal verschillende bronnen ingevoerd, geanalyseerd in Experience Platform en geactiveerd voor een groot aantal verschillende bestemmingen. Experience Platform maakt het proces om deze potentieel niet-lineaire stroom van gegevens te volgen gemakkelijker door transparantie van gegevensstromen te verstrekken.

Dataflows zijn een voorstelling van gegevenstaken die gegevens over Experience Platform verplaatsen. Deze gegevensstromen worden gevormd over verschillende diensten, die gegevens van bronschakelaars aan doeldatasets helpen bewegen, waar het dan door [!DNL Identity Service] en [!DNL Real-Time Customer Profile] wordt gebruikt alvorens uiteindelijk aan [!DNL Destinations] wordt geactiveerd.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Nieuw dashboard voor bewaking | U kunt het controledashboard nu gebruiken voor cross-service transparantie en actionable inzichten voor brongegevensopname. Het nieuwe dashboard voor bewaking biedt een uitgebreide weergave van gegevens die zijn verwerkt van [!DNL Data Lake] naar [!DNL Identity Service] en [!DNL Profile] , terwijl u ook de innamesnelheden, successen en fouten kunt controleren. Zie het leerprogramma op [ controlerende brondataflows in UI ](../../dataflows/ui/monitor-sources.md) voor meer informatie. |

Voor meer algemene informatie over dataflows, verwijs naar het [ dataflows overzicht ](../../dataflows/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe bestemmingen**

| Bestemming | Beschrijving |
| ----------- | ----------- |
| [[!DNL LinkedIn Matched Audiences]](../../destinations/catalog/social/linkedin.md) | Met de [!DNL LinkedIn Matched Audiences] -verbinding kunt u het publiek activeren op het [!DNL LinkedIn] sociale platform. |

Voor meer algemene informatie over bestemmingen raadpleegt u het [overzicht van bestemmingen](../../destinations/home.md).

## [!DNL Experience Data Model (XDM) System] {#xdm}

Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter [!DNL Experience Platform] . [!DNL Experience Data Model] (XDM), aangedreven door Adobe, is een inspanning om de gegevens van de klantenervaring te standaardiseren en schema&#39;s voor het beheer van de klantenervaring te bepalen.

XDM is een openbaar gedocumenteerde specificatie die wordt ontworpen om de macht van digitale ervaringen te verbeteren. Het verstrekt gemeenschappelijke structuren en definities voor om het even welke toepassing om met de diensten op Adobe Experience Platform te communiceren. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen die inzichten op een snellere, meer geïntegreerde manier levert. U kunt waardevolle inzichten verkrijgen uit klantacties, klantdoelgroepen definiëren via segmenten en klantkenmerken gebruiken voor personalisatiedoeleinden.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Bijgewerkte zoekinterface | Verbeterde zoekmogelijkheden zijn nu beschikbaar op het tabblad [!UICONTROL Browse] in de [!UICONTROL Schemas] -werkruimte en in het dialoogvenster voor het selecteren van groepen in schemavelden in het [!DNL Schema Editor] .<br><br> wanneer het zoeken naar een termijn eerder, zouden de resultaten slechts middelen XDM omvatten de waarvan naam de onderzoeksvraag aanpast. Nu, naast middelen de waarvan naam de vraag aanpast, zullen de middelen die individuele attributen bevatten die de termijn aanpassen ook worden omvat. Dit staat u toe om naar middelen te zoeken XDM die op de attributen worden gebaseerd zij eerder dan door middelnaam bevatten.<br><br> zie de documenten op [ het onderzoeken van middelen XDM ](../../xdm/ui/explore.md) en [ het leiden schema&#39;s ](../../xdm/ui/resources/schemas.md) in UI voor meer informatie. |

Voor meer algemene informatie over XDM, verwijs naar het [ XDM overzicht van het Systeem ](../../xdm/home.md).

## [!DNL Identity Service] {#identity}

Voor het aanbieden van relevante digitale ervaringen is een volledig begrip van uw klant vereist. Dit wordt bemoeilijkt wanneer uw klantengegevens over verschillende systemen worden gefragmenteerd, die elke individuele klant ertoe brengen om veelvoudige &quot;identiteiten&quot;te hebben te schijnen.

Met Adobe Experience Platform [!DNL Identity Service] kunt u uw klanten en hun gedrag beter laten zien door identiteiten tussen apparaten en systemen te overbruggen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Naamgrafiekviewer | Met de viewer voor identiteitsgrafieken kunt u identiteiten valideren en visualiseren die in de gebruikersinterface aan elkaar zijn gekoppeld, zodat de foutopsporing en de transparantie kunnen worden verbeterd. Zie het [ document van de de grafiekkijker van de identiteitsgrafiek ](../../identity-service/features/identity-graph-viewer.md) voor meer informatie. |

Voor meer algemene informatie over [!DNL Identity Service], verwijs naar het [ overzicht van de Dienst van de Identiteit ](../../identity-service/home.md).

## Realtime-klantenprofiel {#profile}

Met Adobe Experience Platform kunt u uw klanten gecoördineerde, consistente en relevante ervaringen bieden, ongeacht waar of wanneer ze met uw merk in aanraking komen. Met Real-Time Customer Profile krijgt u een holistisch beeld van elke individuele klant, waarbij gegevens uit meerdere kanalen worden gecombineerd, waaronder online, offline, CRM en gegevens van derden. Met [!DNL Profile] kunt u klantgegevens consolideren in een uniforme weergave die een actionabel, tijdstempelaccount voor elke interactie van de klant biedt.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Berekende kenmerken (Alpha) | ***Nota: Deze functionaliteit is momenteel in alpha en niet beschikbaar aan alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.*** <br/><br/> de Berekende attributen zijn functies die worden gebruikt om gebeurtenis-vlakke gegevens in profiel-vlakke attributen samen te voegen. Vervolgens kunt u de aggregaten in segmentatie, activering en personalisatie gebruiken. Voorbeelden van deze functies zijn count, sum, average, min, max, true/false. Berekende kenmerken zijn momenteel alleen beschikbaar via de API. |

Voor meer informatie over het Profiel van de Klant in real time, met inbegrip van leerprogramma&#39;s en beste praktijken voor het werken met [!DNL Profile] gegevens, gelieve te beginnen door het [ overzicht van het Profiel van de Klant in real time ](../../profile/home.md) te lezen.

## [!DNL Sources] {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens opnemen uit verschillende bronnen, zoals Adobe-toepassingen, cloudgebaseerde opslag, software van derden en uw CRM-systeem.

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Nieuwe bronnen**

| Functie | Beschrijving |
| --- | --- |
| [!DNL Google PubSub] | U kunt nu verbinding maken met [!DNL Google PubSub] via de [!DNL Experience Platform] API of de gebruikersinterface. [!DNL Flow Service] Zie het [[!DNL Google PubSub]  schakelaaroverzicht ](../../sources/connectors/cloud-storage/google-pubsub.md) voor meer informatie. |
| [!DNL Oracle Object Storage] | U kunt nu verbinding maken met [!DNL Oracle Object Storage] via de [!DNL Experience Platform] API of de gebruikersinterface. [!DNL Flow Service] Zie het [[!DNL Oracle Object Storage]  schakelaaroverzicht ](../../sources/connectors/cloud-storage/oracle-object-storage.md) voor meer informatie. |

Voor meer algemene informatie over bronnen, verwijs naar het [ overzicht van bronnen ](../../sources/home.md).

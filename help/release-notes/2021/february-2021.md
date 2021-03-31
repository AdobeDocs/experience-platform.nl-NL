---
title: Opmerkingen bij de release van Adobe Experience Platform
description: Opmerkingen bij de release van Experience Platform voor 24 februari 2021.
doc-type: release notes
last-update: February 24, 2021
author: ens70167
translation-type: tm+mt
source-git-commit: 398e55f442a2c8ecab0c3d9315fbdd5c02946e45
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 2%

---


# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 24 februari 2021**

Nieuwe functies in Adobe Experience Platform:

- [(bèta) dashboards](#dashboards)

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Dataflows]](#dataflows)
- [[!DNL Destinations]](#destinations)
- [[!DNL Experience Data Model (XDM) System]](#xdm)
- [[!DNL Identity Service]](#identity)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## (bèta) Dashboards {#dashboards}

Adobe Experience Platform biedt meerdere dashboards waarmee u belangrijke informatie over de gegevens van uw organisatie kunt bekijken, zoals vastgelegd tijdens dagelijkse momentopnamen.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Profielen, segmenten, doelen en gebruiksdashboards voor licenties (bèta) | **Opmerking: De dashboardfunctionaliteit bevindt zich momenteel in bèta en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.**<br/><br/> De dashboards verstrekken out-of-the-box rapportering over de gegevens van uw organisatie en zijn direct gebouwd in de markeringswerkschema binnen Platform. Deze dashboards zijn beschikbaar zonder de behoefte aan extra steun van IT of de tijd en de inspanning het anders zou vergen om gegevens met extra het opslagontwerp en implementatie van gegevens uit te voeren en te verwerken. |

## [!DNL Data Science Workspace] {#dsw}

De Werkruimte van de Wetenschap van Gegevens gebruikt machine het leren en kunstmatige intelligentie om inzichten van uw gegevens tot stand te brengen. De Data Science Workspace is geïntegreerd in Adobe Experience Platform en helpt u om voorspellingen te maken met behulp van uw inhoud en gegevenselementen voor verschillende Adobe-oplossingen.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| JupyterLab EDA-laptop | De exploratieve gegevensanalyse (EDA) Python-laptop is nu beschikbaar in Jupyterlab. Deze laptop is ontworpen om u te helpen bij het ontdekken van patronen in gegevens, het controleren van de hygiëne van gegevens en het samenvatten van de relevante gegevens voor voorspellende modellen. Zie de zelfstudie over [het verkennen van webgebaseerde gegevens voor voorspellende modellen](../../data-science-workspace/jupyterlab/eda-notebook.md) voor meer informatie. |

Voor meer algemene informatie over de Werkruimte van de Wetenschap van Gegevens, verwijs naar [Overzicht van de Werkruimte van de Wetenschap van Gegevens](../../data-science-workspace/home.md).

## [!DNL Dataflows] {#dataflows}

In Adobe Experience Platform worden gegevens uit een groot aantal verschillende bronnen opgenomen, binnen het Experience Platform geanalyseerd en geactiveerd voor een groot aantal verschillende bestemmingen. Platform maakt het proces om deze potentieel niet-lineaire stroom van gegevens te volgen gemakkelijker door transparantie van gegevensstromen te verstrekken.

Dataflows zijn een voorstelling van gegevenstaken die gegevens over het Platform verplaatsen. Deze gegevensstromen worden gevormd over verschillende diensten, die gegevens van bronschakelaars aan doeldatasets helpen bewegen, waar het dan door [!DNL Identity Service] en [!DNL Real-time Customer Profile] wordt gebruikt alvorens uiteindelijk aan [!DNL Destinations] wordt geactiveerd.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Nieuw dashboard voor bewaking | U kunt het controledashboard nu gebruiken voor cross-service transparantie en actionable inzichten voor brongegevensopname. Het nieuwe controledashboard biedt een uitgebreide weergave van gegevens die zijn verwerkt van [!DNL Data Lake] naar [!DNL Identity Service] en naar [!DNL Profile], terwijl u ook de innamesnelheden, successen en fouten kunt controleren. Zie de zelfstudie over [brongegevens controleren in UI](../../dataflows/ui/monitor-sources.md) voor meer informatie. |

Voor meer algemene informatie over gegevensstromen, verwijs naar [dataflows overzicht](../../dataflows/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe bestemmingen**

| Bestemming | Beschrijving |
| ----------- | ----------- |
| [[!DNL LinkedIn Matched Audiences]](../../destinations/catalog/social/linkedin.md) | Met de verbinding [!DNL LinkedIn Matched Audiences] kunt u het publiek activeren op het sociale platform [!DNL LinkedIn]. |

Voor meer algemene informatie over bestemmingen, verwijs naar [bestemmingen overzicht](../../destinations/home.md).

## [!DNL Experience Data Model (XDM) System] {#xdm}

Standaardisering en interoperabiliteit zijn belangrijke concepten achter [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), gedreven door Adobe, is een inspanning om de gegevens van de klantenervaring te standaardiseren en schema&#39;s voor het beheer van de klantenervaring te bepalen.

XDM is een openbaar gedocumenteerde specificatie die wordt ontworpen om de macht van digitale ervaringen te verbeteren. Het verstrekt gemeenschappelijke structuren en definities voor om het even welke toepassing om met de diensten op Adobe Experience Platform te communiceren. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen die inzichten op een snellere, meer geïntegreerde manier levert. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Bijgewerkte zoekinterface | Verbeterde zoekmogelijkheden zijn nu beschikbaar op het tabblad [!UICONTROL Browse] in de werkruimte [!UICONTROL Schemas] en in het dialoogvenster voor gemengde selectie in [!DNL Schema Editor].<br><br>Wanneer het zoeken naar een termijn eerder, zouden de resultaten slechts XDM middelen omvatten de waarvan naam de onderzoeksvraag aanpast. Nu, naast middelen de waarvan naam de vraag aanpast, zullen de middelen die individuele attributen bevatten die de termijn aanpassen ook worden omvat. Dit staat u toe om naar middelen te zoeken XDM die op de attributen worden gebaseerd zij eerder dan door middelnaam bevatten.<br><br>Zie de documenten over het  [onderzoeken van ](../../xdm/ui/explore.md) middelen XDM en het  [beheren van ](../../xdm/ui/resources/schemas.md) schema&#39;s in UI voor meer informatie. |

Voor meer algemene informatie over XDM, verwijs naar [XDM System overview](../../xdm/home.md).

## [!DNL Identity Service] {#identity}

Voor het aanbieden van relevante digitale ervaringen is een volledig begrip van uw klant vereist. Dit wordt bemoeilijkt wanneer uw klantengegevens over verschillende systemen worden gefragmenteerd, die elke individuele klant ertoe brengen om veelvoudige &quot;identiteiten&quot;te hebben te schijnen.

Met Adobe Experience Platform [!DNL Identity Service] kunt u een beter beeld krijgen van uw klant en zijn gedrag door identiteiten tussen apparaten en systemen te overbruggen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Identiteitsgrafiekviewer | Met de viewer voor identiteitsgrafieken kunt u identiteiten valideren en visualiseren die in de gebruikersinterface aan elkaar zijn gekoppeld, zodat de foutopsporing en de transparantie kunnen worden verbeterd. Zie [identiteitsgrafiekviewerdocument](../../identity-service/ui/identity-graph-viewer.md) voor meer informatie. |

Voor meer algemene informatie over [!DNL Identity Service], verwijs naar [Overzicht van de Dienst van de Identiteit](../../identity-service/home.md).

## Klantprofiel in realtime {#profile}

Met Adobe Experience Platform kunt u zorgen voor gecoördineerde, consistente en relevante ervaringen voor uw klanten, ongeacht waar of wanneer ze met uw merk communiceren. Met het Profiel van de Klant in real time, kunt u een holistische mening van elke individuele klant zien die gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derdegegevens combineert. [!DNL Profile] staat u toe om klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Berekende kenmerken (alfa) | ***Opmerking: Deze functionaliteit bevindt zich momenteel in alfa en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.*** <br/><br/>Berekende kenmerken zijn functies die worden gebruikt om gegevens op gebeurtenisniveau samen te voegen tot kenmerken op profielniveau. Vervolgens kunt u de aggregaten in segmentatie, activering en personalisatie gebruiken. Voorbeelden van deze functies zijn count, sum, average, min, max, true/false. Berekende kenmerken zijn momenteel alleen beschikbaar via de API. Voor meer informatie, zie [gegevens verwerkte attributen overzicht](../../profile/computed-attributes/overview.md). |

Voor meer informatie over het profiel van de Klant in real time, met inbegrip van leerprogramma&#39;s en beste praktijken voor het werken met [!DNL Profile] gegevens, gelieve te beginnen door [Overzicht van het Profiel van de Klant in real time](../../profile/home.md) te lezen.

## [!DNL Sources] {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe bronnen**

| Functie | Beschrijving |
| --- | --- |
| [!DNL Google PubSub] | U kunt [!DNL Google PubSub] nu verbinden met [!DNL Experience Platform] gebruikend [!DNL Flow Service] API of UI. Zie [[!DNL Google PubSub] connectoroverzicht](../../sources/connectors/cloud-storage/google-pubsub.md) voor meer informatie. |
| [!DNL Oracle Object Storage] | U kunt [!DNL Oracle Object Storage] nu verbinden met [!DNL Experience Platform] gebruikend [!DNL Flow Service] API of UI. Zie [[!DNL Oracle Object Storage] connectoroverzicht](../../sources/connectors/cloud-storage/oracle-object-storage.md) voor meer informatie. |

Voor meer algemene informatie over bronnen, verwijs naar [bronnen overzicht](../../sources/home.md).

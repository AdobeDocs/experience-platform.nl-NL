---
title: Opmerkingen bij de release van Adobe Experience Platform
description: Opmerkingen bij de release van Experience Platform voor 24 februari 2021.
doc-type: release notes
last-update: February 24, 2021
author: ens70167
translation-type: tm+mt
source-git-commit: 9f7d7ae9c721d1ce7abf0dc7d3eaff18eed09d6f
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 2%

---


# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 24 februari 2021**

Updates voor bestaande functies in Adobe Experience Platform:

- [Gegevensstromen](#dataflows)
- [XDM-systeem (Experience Data Model)](#xdm)
- [Identiteitsservice](#identity)
- [Bronnen](#sources)

## Gegevensstromen {#dataflows}

In Adobe Experience Platform worden gegevens uit een groot aantal verschillende bronnen opgenomen, binnen het Experience Platform geanalyseerd en geactiveerd voor een groot aantal verschillende bestemmingen. Platform maakt het proces om deze potentieel niet-lineaire stroom van gegevens te volgen gemakkelijker door transparantie van gegevensstromen te verstrekken.

Dataflows zijn een voorstelling van gegevenstaken die gegevens over het Platform verplaatsen. Deze gegevensstromen worden gevormd over verschillende diensten, die gegevens van bronschakelaars aan doeldatasets helpen bewegen, waar het dan door [!DNL Identity Service] en [!DNL Real-time Customer Profile] wordt gebruikt alvorens uiteindelijk aan [!DNL Destinations] wordt geactiveerd.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Nieuw dashboard voor bewaking | U kunt het controledashboard nu gebruiken voor cross-service transparantie en actionable inzichten voor brongegevensopname. Het nieuwe controledashboard biedt een uitgebreide weergave van gegevens die zijn verwerkt van [!DNL Data Lake] naar [!DNL Identity Service] en naar [!DNL Profile], terwijl u ook de innamesnelheden, successen en fouten kunt controleren. Zie de zelfstudie over [brongegevens controleren in UI](../../dataflows/ui/monitor-sources.md) voor meer informatie. |

Voor meer algemene informatie over gegevensstromen, verwijs naar [dataflows overzicht](../../dataflows/home.md).

## Systeem {#xdm} van de Gegevens van de ervaring Model (XDM)

Standaardisering en interoperabiliteit zijn belangrijke concepten achter [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), gedreven door Adobe, is een inspanning om de gegevens van de klantenervaring te standaardiseren en schema&#39;s voor het beheer van de klantenervaring te bepalen.

XDM is een openbaar gedocumenteerde specificatie die wordt ontworpen om de macht van digitale ervaringen te verbeteren. Het verstrekt gemeenschappelijke structuren en definities voor om het even welke toepassing om met de diensten op Adobe Experience Platform te communiceren. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen die inzichten op een snellere, meer geïntegreerde manier levert. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Bijgewerkte zoekinterface | Verbeterde zoekmogelijkheden zijn nu beschikbaar op het tabblad [!UICONTROL Bladeren] in de werkruimte [!UICONTROL Schema&#39;s] en in het dialoogvenster voor gemengde selectie in [!DNL Schema Editor].<br><br>Wanneer het zoeken naar een termijn eerder, zouden de resultaten slechts XDM middelen omvatten de waarvan naam de onderzoeksvraag aanpast. Nu, naast middelen de waarvan naam de vraag aanpast, zullen de middelen die individuele attributen bevatten die de termijn aanpassen ook worden omvat. Dit staat u toe om naar middelen te zoeken XDM die op de attributen worden gebaseerd zij eerder dan door middelnaam bevatten.<br><br>Zie de documenten over het  [onderzoeken van ](../../xdm/ui/explore.md) middelen XDM en het  [beheren van ](../../xdm/ui/resources/schemas.md) schema&#39;s in UI voor meer informatie. |

Voor meer algemene informatie over XDM, verwijs naar [XDM System overview](../../xdm/home.md).

## Identiteitsservice {#identity}

Voor het aanbieden van relevante digitale ervaringen is een volledig begrip van uw klant vereist. Dit wordt bemoeilijkt wanneer uw klantengegevens over verschillende systemen worden gefragmenteerd, die elke individuele klant ertoe brengen om veelvoudige &quot;identiteiten&quot;te hebben te schijnen.

Met Adobe Experience Platform [!DNL Identity Service] kunt u een beter beeld krijgen van uw klanten en hun gedrag door identiteiten over verschillende apparaten en systemen te overbruggen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Identiteitsgrafiekviewer | Met de viewer voor identiteitsgrafieken kunt u identiteiten valideren en visualiseren die in de gebruikersinterface aan elkaar zijn gekoppeld, zodat de foutopsporing en de transparantie kunnen worden verbeterd. Zie [identiteitsgrafiekviewerdocument](../../identity-service/ui/identity-graph-viewer.md) voor meer informatie. |

Voor meer algemene informatie over [!DNL Identity Service], verwijs naar [Overzicht van de Dienst van de Identiteit](../../identity-service/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe bronnen**

| Functie | Beschrijving |
| --- | --- |
| [!DNL Google PubSub] | U kunt [!DNL Google PubSub] nu verbinden met [!DNL Experience Platform] gebruikend [!DNL Flow Service] API of UI. Zie [[!DNL Google PubSub] connectoroverzicht](../../sources/connectors/cloud-storage/google-pubsub.md) voor meer informatie. |
| [!DNL Oracle Object Storage] | U kunt [!DNL Oracle Object Storage] nu verbinden met [!DNL Experience Platform] gebruikend [!DNL Flow Service] API of UI. Zie [[!DNL Oracle Object Storage] connectoroverzicht](../../sources/connectors/cloud-storage/oracle-object-storage.md) voor meer informatie. |

Voor meer algemene informatie over bronnen, verwijs naar [bronnen overzicht](../../sources/home.md).

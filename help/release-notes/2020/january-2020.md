---
title: 'Aanvullende informatie van januari 2020 voor Adobe Experience Platform '
description: Aanvullende informatie van januari 2020 voor Adobe Experience Platform.
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
exl-id: e488a50c-2a87-4649-b3a4-f9d45cb12fcb
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '887'
ht-degree: 22%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum: donderdag 15 januari 2020**

Updates voor bestaande functies in Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)
* [[!DNL Destinations]](#destinations)

## [!DNL Experience Data Model] (XDM)-systeem {#xdm}

Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter [!DNL Experience Platform] . [!DNL Experience Data Model] (XDM), aangedreven door Adobe, is een inspanning om de gegevens van de klantenervaring te standaardiseren en schema&#39;s voor het beheer van de klantenervaring te bepalen.

XDM is een openbaar gedocumenteerde specificatie die wordt ontworpen om de macht van digitale ervaringen te verbeteren. Het verstrekt gemeenschappelijke structuren en definities voor om het even welke toepassing om met de diensten op Adobe Experience Platform te communiceren. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen die inzichten op een snellere, meer geïntegreerde manier levert. U kunt waardevolle inzichten verkrijgen uit klantacties, klantdoelgroepen definiëren via segmenten en klantkenmerken gebruiken voor personalisatiedoeleinden.

**Nieuwe functies**

| Functie | Beschrijving |
|--- | ---|
| Beperkingen van veldtype voor velden met gelijke hiërarchie | Nadat een XDM-veld is gedefinieerd als een bepaald type, moeten andere velden met dezelfde naam en hiërarchie hetzelfde veldtype gebruiken, ongeacht de klassen of groepen schemavelden waarin ze worden gebruikt. Als een veldgroep voor de klasse XDM [!DNL Profile] bijvoorbeeld een `profile.age` veld van het type &quot;integer&quot; bevat, kan een vergelijkbare veldgroep voor XDM [!DNL ExperienceEvent] geen `profile.age` veld van het type &quot;string&quot; hebben. Als u een ander veldtype wilt gebruiken, moet het veld een andere hiërarchie hebben dan het eerder gedefinieerde veld (bijvoorbeeld `profile.person.age` ). Deze functie is bedoeld om conflicten te voorkomen wanneer schema&#39;s in een unie worden samengebracht. Hoewel de beperking geen retroactief effect heeft op bestaande schema&#39;s, wordt sterk geadviseerd dat u uw schema&#39;s voor field-type conflicten herziet en hen zonodig uitgeeft. |
| Hoofdlettergevoelige veldvalidatie | Aangepaste velden op hetzelfde niveau moeten verschillende namen hebben, ongeacht het hoofdlettergebruik. Als u bijvoorbeeld een aangepast veld met de naam &quot;E-mail&quot; toevoegt en hieraan een aangepaste waarde toevoegt, kunt u geen ander aangepast veld op hetzelfde niveau met de naam &quot;e-mail&quot; toevoegen. |

**Bekende kwesties**

* Geen

Om meer over het werken met XDM te leren gebruikend [!DNL Schema Registry] API en [!DNL Schema Editor] gebruikersinterface, te lezen gelieve de [ documentatie van het Systeem XDM ](../../xdm/home.md).

## [!DNL Privacy Service] {#privacy}

De nieuwe wettelijke en organisatorische verordeningen geven gebruikers het recht om tot hun persoonlijke gegevens van uw gegevensopslag toegang te hebben of te schrappen op verzoek. Adobe Experience Platform [!DNL Privacy Service] biedt een RESTful-API en gebruikersinterface waarmee u deze gegevensaanvragen van uw klanten kunt beheren. Met [!DNL Privacy Service] kunt u verzoeken indienen om toegang te krijgen tot privé- of persoonlijke klantgegevens en deze te verwijderen uit Adobe Experience Cloud-toepassingen, waardoor u gemakkelijker kunt voldoen aan wettelijke en organisatorische privacyregels.

**Nieuwe functies**

| Functie | Beschrijving |
|--- | ---|
| [!DNL Privacy Service]-rebranding | De eerdere naam &#39;GDPR-service&#39; is vervangen door [!DNL Privacy Service] omdat de service inmiddels ook andere regels ondersteunt naast GDPR. |
| Nieuwe API-eindpunten | Het basispad voor de [!DNL Privacy Service] API is bijgewerkt van `/data/privacy/gdpr` tot `/data/core/privacy/jobs` . |
| Nieuwe vereiste `regulation`-eigenschap | Wanneer u nieuwe taken maakt in de [!DNL Privacy Service]-API, moet de eigenschap `regulation` in de payload van de aanvraag worden opgegeven om aan te geven onder welke regeling de taak moet worden bijgehouden. Accepteerde waarden zijn `gdpr` en `ccpa` . |
| Ondersteuning voor [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service] accepteert nu toegang-/verwijderaanvragen van Adobe [!DNL Primetime Authentication] en gebruikt `primetimeAuthentication` als de productwaarde. |
| Verbeteringen voor de gebruikersinterface van Privacy Service | Afzonderlijke pagina&#39;s voor het volgen van taken voor GDPR en CCPA verordeningen. Nieuw **Type verordening &#x200B;** dropdown om tussen het volgen gegevens voor GDPR en CCPA te schakelen. |

**Bekende kwesties**

* Geen

Voor meer informatie over [!DNL Privacy Service], gelieve te beginnen door het [ overzicht van Privacy Service ](../../privacy-service/home.md) te lezen.

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met [!DNL Experience Platform] -services. U kunt gegevens opnemen uit verschillende bronnen, zoals Adobe-toepassingen, cloudgebaseerde opslag, software van derden en uw CRM-systeem.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Nieuwe functies**

| Functie | Beschrijving |
|--- | ---|
| Ondersteuning voor kenmerkgegevens van klanten | UI- en API-ondersteuning voor het maken van streaming-connectors om klantkenmerkgegevens in te voeren. |
| Extra ondersteuning voor bestandsindelingen voor cloudopslagsystemen | Bestandsinvoer uit cloudopslagsystemen ondersteunt nu XDM-compatibele Parquet- en JSON-bestandsindelingen. |
| Ondersteuning voor toegangsbeheermachtigingen | Het toegangsbeheerkader in Adobe Experience Platform verstrekt de toestemmingen nodig om toegang tot bronnen in gegevensopname te verlenen. Afhankelijk van hun toestemmingsniveau, kan een gebruiker bronnen bekijken, bronnen beheren, of toegang volledig worden ontzegd. |

**de controletoestemmingen van de Toegang**

| Categorie | Machtiging | Beschrijving |
|--- | --- | ---|
| Gegevensopname | Bronnen beheren | Toegang tot bronnen lezen, maken, bewerken en uitschakelen. |
| Gegevensopname | Bronnen weergeven | Alleen-lezen toegang tot beschikbare bronnen op het tabblad **[!UICONTROL Catalog]** en geverifieerde bronnen op het tabblad **[!UICONTROL Browse]** . |

**Bekende kwesties**

* Geen

Voor meer informatie over bronnen, zie het [ overzicht van bronnen ](../../sources/home.md)

## Bestemmingen {#destinations}

In [ Real-Time CDP ](../../rtcdp/overview.md), zijn de bestemmingen pre-gebouwde integratie met bestemmingsplatforms die gegevens aan die partners op een naadloze manier activeren.

**Nieuwe functies**

| Functie | Beschrijving |
|--- | ---|
| Ondersteuning voor toegangsbeheermachtigingen | De functie Doelen in Real-Time CDP werkt met Adobe Experience Platform-toegangsbeheermachtigingen. Afhankelijk van het machtigingsniveau van uw gebruiker, kunt u bestemmingen bekijken, beheren en activeren. |

**de controletoestemmingen van de Toegang**

| Categorie | Machtiging | Beschrijving |
|--- | --- | ---|
| Bestemmingen | Doelen beheren | Toegang tot het lezen, creëren, uitgeven, en onbruikbaar maken bestemmingen. |
| Bestemmingen | Doelen weergeven | Read-only toegang tot beschikbare bestemmingen in het **[!UICONTROL Catalog]** lusje en voor authentiek verklaarde bestemmingen in **doorbladert** lusje. |
| Bestemmingen | Doelen activeren | Mogelijkheid om gegevens naar doelen te activeren. Voor deze machtiging moet &quot;Doelen beheren&quot; of &quot;Doelen weergeven&quot; worden toegevoegd aan het productprofiel. |

**Bekende kwesties**

* Geen

Zie het [ overzicht van Doelen ](../../destinations/home.md) voor meer informatie.

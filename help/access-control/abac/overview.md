---
keywords: Experience Platform;huis;populaire onderwerpen;toegangsbeheer;op attribuut-gebaseerde toegangscontrole;
title: Kenmerk-Gebaseerd Overzicht van het Toegangsbeheer
description: Dit document bevat informatie over op kenmerken gebaseerd toegangsbeheer in Adobe Experience Platform
exl-id: 5495c55f-b808-40c1-8896-e03eace0ca4d
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1864'
ht-degree: 0%

---

# Overzicht van toegangsbeheer op basis van kenmerken {#attribute-based-access-control-overview}

>[!CONTEXTUALHELP]
>id="platform_accesscontrol_abac_labelusageaccesspolicy"
>title="Toegangsbeleid voor gebruik van label"
>abstract=""

Toegangsbeheer op basis van kenmerken is een mogelijkheid van Adobe Experience Platform waarmee beheerders de toegang tot specifieke objecten en/of mogelijkheden kunnen beheren op basis van kenmerken. Kenmerken kunnen metagegevens zijn die aan een object worden toegevoegd, zoals een label dat aan een schemaveld of -segment wordt toegevoegd. Een beheerder bepaalt toegangsbeleid dat attributen omvat om de toestemmingen van de gebruikerstoegang te beheren.

Gebruik deze functionaliteit om XDM-schemavelden (Experience Data Model) te labelen met labels die bereik voor organisatie- of gegevensgebruik definiëren. Parallel hieraan kunnen beheerders de gebruikers- en rolbeheerinterface gebruiken om toegangsbeleid te definiëren rondom XDM-schemavelden en de toegang die gebruikers of groepen gebruikers (interne, externe of externe gebruikers) krijgen beter te beheren. Bovendien, op attribuut-gebaseerde toegangsbeheer staat beheerders toe om toegang tot specifieke segmenten te beheren.

>[!IMPORTANT]
>
>Op attributen-gebaseerde toegangscontrole moet niet met de mogelijkheden van het gegevensbeheer van het Experience Platform worden verward, die u toestaan om etiketten en beleid te gebruiken om te controleren hoe het gegeven in Platform eerder wordt gebruikt dan welke gebruikers in uw organisatie toegang tot het hebben. Zie het [ overzicht van het gegevensbeheer ](../../data-governance/home.md) voor meer informatie.

Via attribuut-gebaseerde toegangscontrole, kunnen de beheerders van uw organisatie gebruikers&#39; toegang tot gevoelige persoonlijke gegevens (SPD) controleren, persoonlijk identificeerbare informatie (PII) en aangepast type van gegevens over alle werkschema&#39;s en middelen van het Platform. Beheerders kunnen gebruikersrollen definiëren die alleen toegang hebben tot specifieke velden en gegevens die overeenkomen met die velden.

De volgende video is bedoeld om uw begrip van op attribuut-gebaseerde toegangscontrole te steunen, en schetst hoe te om rollen, middelen, en beleid te vormen.

>[!VIDEO](https://video.tv.adobe.com/v/345641?learn=on)

## Op kenmerken gebaseerde terminologie voor toegangsbeheer

Op attributen-gebaseerde toegangsbeheer impliceert de volgende componenten:

| Terminologie | Definitie |
| --- | --- |
| Attributen | Attributen zijn de herkenningstekens die op de correlatie tussen een gebruiker en de middelen van het Platform wijzen die zij hebben toegang tot. Kenmerken kunnen metagegevens zijn die aan een object worden toegevoegd, zoals een label dat aan een schemaveld of -segment wordt toegevoegd. Een beheerder bepaalt toegangsbeleid dat attributen omvat om de toestemmingen van de gebruikerstoegang te beheren. |
| Labels | Met labels kunt u gegevenssets en velden categoriseren op basis van het gebruiksbeleid dat op die gegevens van toepassing is. Labels kunnen op elk gewenst moment worden toegepast, zodat u op flexibele wijze gegevens kunt beheren. De beste praktijken bevorderen etiketteringsgegevens zodra het in Platform wordt opgenomen, of zodra de gegevens voor gebruik in Platform beschikbaar worden. |
| Machtigingen | De toestemmingen omvatten de capaciteit om de eigenschappen van het Platform te bekijken en/of te gebruiken, zoals het creëren van zandbakken, het bepalen van schema&#39;s, en het beheren van datasets. |
| Machtigingssets | Machtigingssets vertegenwoordigen een groep machtigingen die een beheerder op een rol kan toepassen. Een beheerder kan rechtensets toewijzen aan een rol in plaats van individuele machtigingen toe te wijzen. Dit staat u toe om douanerollen van een vooraf bepaalde rol tot stand te brengen die een groep toestemmingen bevat. |
| Beleid | Het beleid is verklaringen die attributen samenbrengen om toegelaten en ontoelaatbare acties te vestigen. Het beleid kan of lokaal of globaal zijn, en kan ander beleid met voeten treden. |
| Bron | Een bron is het element dat of het object dat een onderwerp kan of kan benaderen. Bronnen kunnen segmenten of schemavelden zijn. |
| Rollen | Rollen zijn manieren om de soorten gebruikers te categoriseren die met uw instantie van het Platform in wisselwerking staan en bouwstenen van toegangsbeheerbeleid zijn. In een op rol-gebaseerd milieu van het toegangsbeheer, is de levering van de gebruikerstoegang groepering door gemeenschappelijke verantwoordelijkheden en behoeften. Een rol heeft een bepaalde reeks toestemmingen en de leden van uw organisatie kunnen aan één of meerdere rollen, afhankelijk van het werkingsgebied van mening worden toegewezen of toegang schrijven zij nodig hebben. |
| Onderwerp | Een onderwerp is de gebruiker die toegang tot een bron aanvraagt om een handeling uit te voeren. |
| Gebruikersgroepen | Gebruikersgroepen zijn meerdere gebruikers die zijn gegroepeerd en die toegang hebben om dezelfde functies uit te voeren. |

## Machtigingen

>[!IMPORTANT]
>
>Zodra uw organisatie voor op attributen-gebaseerde toegangsbeheer wordt toegelaten, kunt u beginnen toestemmingen op Adobe Experience Cloud, in plaats van Rollen in Adobe Admin Console te gebruiken, om toestemmingen voor gebruikers, functionaliteit, etiketten, en andere middelen in uw organisatie te beheren.

De toestemmingen zijn het gebied van Experience Cloud waar de beheerders gebruikersrollen en toegangsbeleid kunnen bepalen om toegangstoestemmingen voor eigenschappen en voorwerpen binnen een producttoepassing te beheren.

Door Toestemmingen, kunt u rollen tot stand brengen en beheren, evenals de gewenste middeltoestemmingen voor deze rollen toewijzen. Met machtigingen kunt u ook de labels, sandboxen en gebruikers beheren die aan een specifieke rol zijn gekoppeld. Voor meer informatie, zie de [ gids van Toestemmingen ](ui/browse.md).

## API voor toegangsbeheer op basis van kenmerken

Met de op kenmerken gebaseerde API voor toegangsbeheer kunt u rollen, beleid en producten binnen het platform programmatisch beheren met behulp van API&#39;s. Voor meer informatie zie de gids op [ gebruikend API om op attribuut-gebaseerde configuraties van de toegangscontrole ](api/overview.md) te beheren.

## Toegangsbeheer op basis van kenmerken in Adobe Experience Platform

De volgende secties verstrekken informatie over hoe op attribuut-gebaseerde toegangsbeheer aan andere componenten van Platform wordt geïntegreerd:

### Toegangsbeheer

De hefboomwerkingen van het platform [ Adobe Admin Console ](https://adminconsole.adobe.com) rollen om gebruikers met toestemmingen en zandbakken te verbinden. De toestemmingen controleren toegang tot een verscheidenheid van de mogelijkheden van het Platform, met inbegrip van gegevensmodellering, profielbeheer, en zandbakbeleid. Zodra uw organisatie voor op attributen-gebaseerde toegangsbeheer wordt toegelaten, kunt u beginnen toestemmingen op Adobe Experience Cloud, in plaats van Rollen in Adobe Admin Console te gebruiken, om toestemmingen voor gebruikers, functionaliteit, etiketten, en andere middelen in uw organisatie te beheren.

Er is beperkte beschikbaarheid voor op attribuut-gebaseerde toegangsbeheer voor klanten die Gezondheidszorg en/of de Schilden van de Privacy kopen. De functies van deze functionaliteit zijn onder andere:

* De interface van toestemmingen: Verstrekt een interface voor u om gebruikersrollen, toestemmingen en beleid voor op attribuut-gebaseerde toegangsbeheer te bepalen.

* Etikettering: Voeg toe, geef, verwijder etiketten aan gebruikersrollen, schemagebieden, segmenten, en andere gesteunde voorwerpen uit om het beleid van de toegangscontrole te hefboomwerking. **Nota:** Om het even welk segment dat een geëtiketteerd attribuut gebruikt moet eveneens worden geëtiketteerd als u de zelfde toegangsbeperkingen op het wilt toepassen.

De beleidswerkschema&#39;s voor alle Experience Platform-aangedreven toepassingen van Admin Console aan de nieuwe interface van Toestemmingen worden geschakeld.

>[!IMPORTANT]
>
>Uw rollen worden automatisch gemigreerd aan de interface van Toestemmingen wanneer uw organisatie wordt toegelaten. De rollen in de Admin Console blijven op dit moment ongewijzigd. Gelieve te **wijzigt niet** uw rollen nadat uw organisatie is toegelaten.

Voor meer informatie over toegangsbeheer, zie het [ overzicht van de toegangscontrole ](../home.md).

### Doelen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integratie met bestemmingsplatforms die voor de naadloze activering van gegevens van Platform toestaan. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

Als beheerder, kunt u op attribuut-gebaseerde toegangsbeheerfunctionaliteit gebruiken aan:

* Vorm gebruikerstoegang om specifieke segmenten in het activeringsproces te bekijken, die op rol, toestemmingen, en etiketten wordt gebaseerd;
   * Tijdens het activeringsproces moeten gebruikers mogelijk segmenten selecteren die ze op een bestemming willen activeren. Als beheerder, kunt u gebruikers in uw organisatie voorzien om segmenten slechts te zien die met etiketten worden geëtiketteerd die de gebruikers toegang hebben tot, en segmenten die geen etiketten bevatten.
* Vorm gebruikerstoegang om specifieke gebieden in het activeringsproces te bekijken, die op rol, toestemmingen, en etiketten wordt gebaseerd;
   * Tijdens het activeringsproces moeten gebruikers mogelijk velden selecteren die ze op een bestemming willen activeren. Als beheerder, kunt u gebruikers in uw organisatie verstrekken om gebieden slechts te zien die met etiketten worden geëtiketteerd die de gebruikers toegang hebben tot, en gebieden die geen etiketten bevatten.

>[!IMPORTANT]
>
>Samenvattend, houd in mening de volgende implicaties wanneer het werken met bestemmingen en op attribuut-gebaseerde toegangsbeheer:
>
>* U kunt publiek slechts activeren dat u toestemming hebt om in [ Portaal van het Publiek ](/help/segmentation/ui/audience-portal.md#browse) toegang te hebben en te bekijken en [ segmentstap ](/help/destinations/ui/activate-batch-profile-destinations.md#select-segments) van het activeringswerkschema te selecteren.
>* In de [ afbeeldingsstap van het activeringswerkschema ](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping), kunt u voor activering slechts bekijken en selecteren de gebieden die u toegangstoestemming hebt om te hebben.
>* Wanneer u extra segmenten wilt activeren naar een bestaand doel waar u geen toegang hebt tot alle velden die zijn toegewezen voor export, wordt de activeringsworkflow voor u geblokkeerd.

Voor meer informatie over [!DNL Destinations], verwijs naar het [[!DNL Destinations]  overzicht ](../../destinations/home.md).

### Identiteitsservice

Adobe Experience Platform [!DNL Identity Service] helpt u een beter inzicht te krijgen in uw klanten en hun gedrag door identiteiten te overbruggen tussen apparaten en systemen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

Als deel van op attribuut-gebaseerde toegangscontrole, `view-identity-graph` toestemming staat u toe om te bepalen welke gebruikers in uw organisatie tot de identiteitsgrafiek door de gebruikersinterface of APIs kunnen toegang hebben. Voor meer informatie, zie de gids op [ gebruikend de kijker van de identiteitsgrafiek ](../../identity-service/features/identity-graph-viewer.md).

Voor meer informatie over [!DNL Identity Service], verwijs naar het [[!DNL Identity Service]  overzicht ](../../identity-service/home.md).

### Klantprofiel in realtime

Met Platform kunt u zorgen voor gecoördineerde, consistente en relevante ervaringen voor uw klanten, ongeacht waar of wanneer ze met uw merk communiceren. Met het Profiel van de Klant in real time, kunt u een holistische mening van elke individuele klant zien die gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derdegegevens combineert. Het profiel staat u toe om uw ongelijke klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

Als beheerder, kunt u op attribuut-gebaseerde toegangsbeheerfunctionaliteit gebruiken aan:

* Configureer gebruikerstoegang tot specifieke profielkenmerken op basis van rol, machtigingen en labels.
   * Als beheerder, kunt u gebruikers in uw organisatie verstrekken om profielattributen slechts te zien die met etiketten worden geëtiketteerd die de gebruikers toegang hebben tot, en profielattributen die geen etiket bevatten;
   * Als beheerder, kunt u gebruikers in uw organisatie voorzien om profielattributen slechts te zien die met etiketten worden geëtiketteerd die de gebruikers toegang hebben tot, wanneer het creëren van segmenten;
* Vorm gebruikerstoegang tot gegevensvoorproef door specifieke gegevensgebieden te etiketteren die in het schema XDM van het gegevensmodel worden gebruikt.

Voor meer informatie over Profiel, verwijs naar het [ overzicht van het Profiel ](../../profile/home.md).

### Segmenteringsservice

[!DNL Segmentation Service] definieert een bepaalde subset van profielen door de criteria te beschrijven die een verhandelbare groep personen binnen uw klantenbasis onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

Als beheerder, kunt u op attribuut-gebaseerde toegangsbeheerfunctionaliteit gebruiken aan:

* Vorm gebruikerstoegang om specifieke segmenten te bekijken en te beheren, die op rol, toestemmingen, en etiketten worden gebaseerd;
   * Als beheerder, kunt u gebruikers in uw organisatie voorzien om segmenten slechts te zien die met etiketten worden geëtiketteerd die de gebruikers toegang hebben tot, en segmenten die geen etiketten bevatten, wanneer het gebruiken van de Segmentatie UI.

Voor meer informatie over [!DNL Segmentation Service], verwijs naar het [[!DNL Segmentation Service]  overzicht ](../../segmentation/home.md).

### XDM

Het Model van Gegevens van de ervaring (XDM) is een open-bronspecificatie die wordt ontworpen om de kracht van digitale ervaringen te verbeteren. Het verstrekt gemeenschappelijke structuren en definities voor om het even welke toepassing om met de diensten op Platform te communiceren. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

Met op attribuut-gebaseerde toegangscontrole, kunt u:

* [ pas de etiketten van het gegevensgebruik op gebiedsgroepen en klassen ](../../xdm/tutorials/labels.md) toe. Hierdoor kunnen in meerdere schema&#39;s met dezelfde veldgroepen of klassen velden worden gelabeld met dezelfde kenmerken, afhankelijk van de configuraties op veldniveau of veldniveau.
* Vorm gebruikerstoegang tot specifieke XDM schemagebieden afhankelijk van de toestemmingsreeksen die op rollen worden toegepast die aan gebruikers worden toegewezen.

Voor meer informatie over XDM, verwijs naar het [ XDM overzicht ](../../xdm/home.md).
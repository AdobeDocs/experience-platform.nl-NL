---
keywords: Experience Platform;home;populaire onderwerpen;toegangsbeheer;op kenmerk-gebaseerde toegangscontrole;
title: Kenmerk-Gebaseerd Overzicht van het Toegangsbeheer
description: Dit document bevat informatie over op kenmerken gebaseerd toegangsbeheer in Adobe Experience Platform
exl-id: 5495c55f-b808-40c1-8896-e03eace0ca4d
source-git-commit: 14028928362d8396c30babfc2279135011dd7c6f
workflow-type: tm+mt
source-wordcount: '1929'
ht-degree: 10%

---

# Overzicht van toegangsbeheer op basis van kenmerken {#attribute-based-access-control-overview}

Toegangsbeheer op basis van kenmerken is een mogelijkheid van Adobe Experience Platform waarmee beheerders de toegang tot specifieke objecten en/of mogelijkheden kunnen beheren op basis van kenmerken. Kenmerken kunnen metagegevens zijn die aan een object worden toegevoegd, zoals een label dat aan een schemaveld of -segment wordt toegevoegd. Een beheerder bepaalt toegangsbeleid dat attributen omvat om de toestemmingen van de gebruikerstoegang te beheren.

Gebruik deze functionaliteit om XDM-schemavelden (Experience Data Model) te labelen met labels die bereik voor organisatie- of gegevensgebruik definiëren. Parallel hieraan kunnen beheerders de gebruikers- en rolbeheerinterface gebruiken om toegangsbeleid te definiëren rondom XDM-schemavelden en de toegang die gebruikers of groepen gebruikers (interne, externe of externe gebruikers) krijgen beter te beheren. Bovendien, op attribuut-gebaseerde toegangsbeheer staat beheerders toe om toegang tot specifieke segmenten te beheren.

>[!IMPORTANT]
>
>Toegangsbeheer op basis van kenmerken mag niet worden verward met Experience Platform-mogelijkheden voor gegevensbeheer, waardoor u labels en beleidsregels kunt gebruiken om te bepalen hoe gegevens in Experience Platform worden gebruikt en niet welke gebruikers in uw organisatie er toegang toe hebben. Zie het [ overzicht van het gegevensbeheer ](../../data-governance/home.md) voor meer informatie.

Via attribuut-gebaseerde toegangscontrole, kunnen de beheerders van uw organisatie gebruikers&#39; toegang tot gevoelige persoonlijke gegevens (SPD) controleren, persoonlijk identificeerbare informatie (PII) en aangepast type van gegevens over alle werkschema&#39;s en middelen van Experience Platform. Beheerders kunnen gebruikersrollen definiëren die alleen toegang hebben tot specifieke velden en gegevens die bij die velden horen.

De volgende video is bedoeld om uw begrip van op attribuut-gebaseerde toegangscontrole te steunen, en schetst hoe te om rollen, middelen, en beleid te vormen.

>[!VIDEO](https://video.tv.adobe.com/v/345641?learn=on)

## Op kenmerken gebaseerde terminologie voor toegangsbeheer

Op attributen-gebaseerde toegangsbeheer impliceert de volgende componenten:

| Terminologie | Definitie |
| --- | --- |
| Attributen | Kenmerken zijn de id&#39;s die de correlatie aangeven tussen een gebruiker en de Experience Platform-bronnen waartoe deze toegang heeft. Kenmerken kunnen metagegevens zijn die aan een object worden toegevoegd, zoals een label dat aan een schemaveld of -segment wordt toegevoegd. Een beheerder bepaalt toegangsbeleid dat attributen omvat om de toestemmingen van de gebruikerstoegang te beheren. |
| Labels | Met labels kunt u gegevenssets en velden categoriseren op basis van het gebruiksbeleid dat op die gegevens van toepassing is. Labels kunnen op elk gewenst moment worden toegepast, zodat u op flexibele wijze gegevens kunt beheren. De beste praktijken bevorderen etiketteringsgegevens zodra het in Experience Platform wordt opgenomen, of zodra de gegevens voor gebruik in Experience Platform beschikbaar worden. |
| Machtigingen | De toestemmingen omvatten de capaciteit om de eigenschappen van Experience Platform te bekijken en/of te gebruiken, zoals het creëren van zandbakken, het bepalen van schema&#39;s, en het beheren van datasets. |
| Machtigingssets | Machtigingssets vertegenwoordigen een groep machtigingen die een beheerder op een rol kan toepassen. Een beheerder kan rechtensets toewijzen aan een rol in plaats van individuele machtigingen toe te wijzen. Dit staat u toe om douanerollen van een vooraf bepaalde rol tot stand te brengen die een groep toestemmingen bevat. |
| Beleid | Het beleid is verklaringen die attributen samenbrengen om toegelaten en ontoelaatbare acties te vestigen. Het beleid kan of lokaal of globaal zijn, en kan ander beleid met voeten treden. |
| Bron | Een bron is het element dat of het object dat een onderwerp kan of kan benaderen. Bronnen kunnen segmenten of schemavelden zijn. |
| Rollen | Rollen zijn manieren om de soorten gebruikers te categoriseren die met uw instantie van Experience Platform in wisselwerking staan en bouwstenen van toegangsbeheerbeleid zijn. In een op rol-gebaseerd milieu van het toegangsbeheer, is de levering van de gebruikerstoegang groepering door gemeenschappelijke verantwoordelijkheden en behoeften. Een rol heeft een bepaalde reeks toestemmingen en de leden van uw organisatie kunnen aan één of meerdere rollen, afhankelijk van het werkingsgebied van mening worden toegewezen of toegang schrijven zij nodig hebben. |
| Onderwerp | Een onderwerp is de gebruiker die toegang tot een bron aanvraagt om een handeling uit te voeren. |
| Gebruikersgroepen | Gebruikersgroepen zijn meerdere gebruikers die zijn gegroepeerd en die toegang hebben om dezelfde functies uit te voeren. |

## Machtigingen

>[!IMPORTANT]
>
>Zodra uw organisatie voor op attributen-gebaseerde toegangsbeheer wordt toegelaten, kunt u beginnen toestemmingen op Adobe Experience Cloud, in plaats van Rollen in Adobe Admin Console te gebruiken, om toestemmingen voor gebruikers, functionaliteit, etiketten, en andere middelen in uw organisatie te beheren.

Machtigingen zijn het gebied van Experience Cloud waar beheerders gebruikersrollen en toegangsbeleid kunnen definiëren om toegangsmachtigingen voor functies en objecten binnen een producttoepassing te beheren.

Door Toestemmingen, kunt u rollen tot stand brengen en beheren, evenals de gewenste middeltoestemmingen voor deze rollen toewijzen. Met machtigingen kunt u ook de labels, sandboxen en gebruikers beheren die aan een specifieke rol zijn gekoppeld. Voor meer informatie, zie de [ gids van Toestemmingen ](ui/browse.md).

## API voor toegangsbeheer op basis van kenmerken

Met de op kenmerken gebaseerde API voor toegangsbeheer kunt u rollen, beleid en producten binnen Experience Platform programmatisch beheren met behulp van API&#39;s. Voor meer informatie zie de gids op [ gebruikend API om op attribuut-gebaseerde configuraties van de toegangscontrole ](api/overview.md) te beheren.

## Toegangsbeheer op basis van kenmerken in Adobe Experience Platform

De volgende secties verstrekken informatie over hoe op attribuut-gebaseerde toegangsbeheer aan andere componenten van Experience Platform wordt geïntegreerd:

### Toegangsbeheer

Experience Platform hefboomwerkingen [ Adobe Admin Console ](https://adminconsole.adobe.com) rollen om gebruikers met toestemmingen en zandbakken te verbinden. Machtigingen beheren de toegang tot verschillende Experience Platform-mogelijkheden, waaronder gegevensmodellering, profielbeheer en sandboxbeheer. Zodra uw organisatie voor op attributen-gebaseerde toegangsbeheer wordt toegelaten, kunt u beginnen toestemmingen op Adobe Experience Cloud, in plaats van Rollen in Adobe Admin Console te gebruiken, om toestemmingen voor gebruikers, functionaliteit, etiketten, en andere middelen in uw organisatie te beheren.

Er is beperkte beschikbaarheid voor op attribuut-gebaseerde toegangsbeheer voor klanten die Gezondheidszorg en/of de Schilden van de Privacy kopen. De functies van deze functionaliteit zijn onder andere:

* De interface van toestemmingen: Verstrekt een interface voor u om gebruikersrollen, toestemmingen en beleid voor op attribuut-gebaseerde toegangsbeheer te bepalen.

* Etikettering: Voeg toe, geef, verwijder etiketten aan gebruikersrollen, schemagebieden, segmenten, en andere gesteunde voorwerpen uit om het beleid van de toegangscontrole te hefboomwerking. **Nota:** Om het even welk segment dat een geëtiketteerd attribuut gebruikt moet eveneens worden geëtiketteerd als u de zelfde toegangsbeperkingen op het wilt toepassen.

De beleidswerkstromen voor alle Experience Platform-aangedreven toepassingen van Admin Console aan de nieuwe interface van Toestemmingen worden geschakeld.

>[!IMPORTANT]
>
>Uw rollen worden automatisch gemigreerd aan de interface van Toestemmingen wanneer uw organisatie wordt toegelaten. De rollen in Admin Console blijven voorlopig ongewijzigd. Gelieve te **wijzigt niet** uw rollen nadat uw organisatie is toegelaten.

Voor meer informatie over toegangsbeheer, zie het [ overzicht van de toegangscontrole ](../home.md).

### Bestemmingen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met bestemmingsplatforms waarmee gegevens uit Experience Platform naadloos kunnen worden geactiveerd. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

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

### Real-Time Customer Profile

Met Experience Platform kunt u zorgen voor gecoördineerde, consistente en relevante ervaringen voor uw klanten, ongeacht waar of wanneer ze met uw merk communiceren. Met Real-Time Customer Profile krijgt u een holistisch beeld van elke individuele klant, waarbij gegevens uit meerdere kanalen worden gecombineerd, waaronder online, offline, CRM en gegevens van derden. Het profiel staat u toe om uw ongelijke klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

Als beheerder, kunt u op attribuut-gebaseerde toegangsbeheerfunctionaliteit gebruiken aan:

* Configureer gebruikerstoegang tot specifieke profielkenmerken op basis van rol, machtigingen en labels.
   * Als beheerder, kunt u gebruikers in uw organisatie verstrekken om profielattributen slechts te zien die met etiketten worden geëtiketteerd die de gebruikers toegang hebben tot, en profielattributen die geen etiket bevatten;
   * Als beheerder, kunt u gebruikers in uw organisatie voorzien om profielattributen slechts te zien die met etiketten worden geëtiketteerd die de gebruikers toegang hebben tot, wanneer het creëren van segmenten;
* Vorm gebruikerstoegang tot gegevensvoorproef door specifieke gegevensgebieden te etiketteren die in het schema XDM van het gegevensmodel worden gebruikt.

Voor meer informatie over Profiel, verwijs naar het [ overzicht van het Profiel ](../../profile/home.md).

### Segmentatieservice

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

Als beheerder, kunt u op attribuut-gebaseerde toegangsbeheerfunctionaliteit gebruiken aan:

* Vorm gebruikerstoegang om specifieke segmenten te bekijken en te beheren, die op rol, toestemmingen, en etiketten worden gebaseerd;
   * Als beheerder, kunt u gebruikers in uw organisatie voorzien om segmenten slechts te zien die met etiketten worden geëtiketteerd die de gebruikers toegang hebben tot, en segmenten die geen etiketten bevatten, wanneer het gebruiken van de Segmentatie UI.

Voor meer informatie over [!DNL Segmentation Service], verwijs naar het [[!DNL Segmentation Service]  overzicht ](../../segmentation/home.md).

### XDM

Het Model van Gegevens van de ervaring (XDM) is een open-bronspecificatie die wordt ontworpen om de kracht van digitale ervaringen te verbeteren. Het verstrekt gemeenschappelijke structuren en definities voor om het even welke toepassing om met de diensten op Experience Platform te communiceren. Door de XDM-standaarden te hanteren, kunnen alle gegevens over de klantervaring worden opgenomen in een gemeenschappelijke weergave. Zo worden inzichten sneller en beter geïntegreerd verkregen. U kunt waardevolle inzichten verkrijgen uit klantacties, klantdoelgroepen definiëren via segmenten en klantkenmerken gebruiken voor personalisatiedoeleinden.

Met op attribuut-gebaseerde toegangscontrole, kunt u:

* [ pas de etiketten van het gegevensgebruik op gebiedsgroepen en klassen ](../../xdm/tutorials/labels.md) toe. Hierdoor kunnen in meerdere schema&#39;s met dezelfde veldgroepen of klassen velden worden gelabeld met dezelfde kenmerken, afhankelijk van de configuraties op veldniveau of veldniveau.
* Vorm gebruikerstoegang tot specifieke XDM schemagebieden afhankelijk van de toestemmingsreeksen die op rollen worden toegepast die aan gebruikers worden toegewezen.

Voor meer informatie over XDM, verwijs naar het [ XDM overzicht ](../../xdm/home.md).

### Customer Journey Analytics (CJA)

Customer Journey Analytics (CJA)-toegangsmachtigingen worden beheerd op toepassingsniveau in CJA. CJA gebruikt zijn eigen op attributen-gebaseerde toegangscontroles en erft of past geen op attributen-gebaseerde toegangscontroles toe die in Adobe Experience Platform worden bepaald.

Voor meer informatie over de toegangscontrole van CJA, verwijs naar de [ de toegangsbeheer van CJA ](https://experienceleague.adobe.com/en/docs/analytics-platform/using/technotes/access-control) documentatie.

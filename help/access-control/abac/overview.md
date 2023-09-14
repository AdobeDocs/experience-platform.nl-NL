---
keywords: Experience Platform;huis;populaire onderwerpen;toegangsbeheer;op attribuut-gebaseerde toegangscontrole;
title: Kenmerk-Gebaseerd Overzicht van het Toegangsbeheer
description: Dit document bevat informatie over op kenmerken gebaseerd toegangsbeheer in Adobe Experience Platform
exl-id: 5495c55f-b808-40c1-8896-e03eace0ca4d
source-git-commit: 36e38824963139414f2803ef4127706d1e521d1a
workflow-type: tm+mt
source-wordcount: '1847'
ht-degree: 0%

---

# Overzicht van toegangsbeheer op basis van kenmerken

Toegangsbeheer op basis van kenmerken is een mogelijkheid van Adobe Experience Platform waarmee beheerders de toegang tot specifieke objecten en/of mogelijkheden kunnen beheren op basis van kenmerken. Kenmerken kunnen metagegevens zijn die aan een object worden toegevoegd, zoals een label dat aan een schemaveld of -segment wordt toegevoegd. Een beheerder bepaalt toegangsbeleid dat attributen omvat om de toestemmingen van de gebruikerstoegang te beheren.

Met deze functionaliteit kunt u XDM-schemavelden (Experience Data Model) labelen met labels die bereik voor organisatie of gegevensgebruik definiëren. Parallel hieraan kunnen beheerders de gebruikers- en rolbeheerinterface gebruiken om toegangsbeleid te definiëren rondom XDM-schemavelden en de toegang die gebruikers of groepen gebruikers (interne, externe of externe gebruikers) krijgen beter te beheren. Bovendien, op attribuut-gebaseerde toegangsbeheer staat beheerders toe om toegang tot specifieke segmenten te beheren.

>[!IMPORTANT]
>
>Op attributen-gebaseerde toegangscontrole moet niet met de mogelijkheden van het gegevensbeheer van het Experience Platform worden verward, die u toestaan om etiketten en beleid te gebruiken om te controleren hoe het gegeven in Platform eerder wordt gebruikt dan welke gebruikers in uw organisatie toegang tot het hebben. Zie de [gegevensbeheer - overzicht](../../data-governance/home.md) voor meer informatie .

Via attribuut-gebaseerde toegangscontrole, kunnen de beheerders van uw organisatie gebruikers&#39; toegang tot gevoelige persoonlijke gegevens (SPD) controleren, persoonlijk identificeerbare informatie (PII) en aangepast type van gegevens over alle werkschema&#39;s en middelen van het Platform. Beheerders kunnen gebruikersrollen definiëren die alleen toegang hebben tot specifieke velden en gegevens die overeenkomen met die velden.

De volgende video is bedoeld om uw begrip van op attribuut-gebaseerde toegangscontrole te steunen, en schetst hoe te om rollen, middelen, en beleid te vormen.

>[!VIDEO](https://video.tv.adobe.com/v/345641?learn=on)

## Op kenmerken gebaseerde terminologie voor toegangsbeheer

Op attributen-gebaseerde toegangsbeheer impliceert de volgende componenten:

| Terminologie | Definitie |
| --- | --- |
| Attributen | Attributen zijn de herkenningstekens die op de correlatie tussen een gebruiker en de middelen van het Platform wijzen die zij hebben toegang tot. Kenmerken kunnen metagegevens zijn die aan een object worden toegevoegd, zoals een label dat aan een schemaveld of -segment wordt toegevoegd. Een beheerder bepaalt toegangsbeleid dat attributen omvat om de toestemmingen van de gebruikerstoegang te beheren. |
| Labels | Met labels kunt u gegevenssets en velden categoriseren op basis van het gebruiksbeleid dat op die gegevens van toepassing is. Labels kunnen op elk gewenst moment worden toegepast, zodat u op flexibele wijze gegevens kunt beheren. De beste praktijken bevorderen etiketteringsgegevens zodra het in Platform wordt opgenomen, of zodra de gegevens voor gebruik in Platform beschikbaar worden. |
| Toestemmingen | De toestemmingen omvatten de capaciteit om de eigenschappen van het Platform te bekijken en/of te gebruiken, zoals het creëren van zandbakken, het bepalen van schema&#39;s, en het beheren van datasets. |
| Machtigingssets | Machtigingssets vertegenwoordigen een groep machtigingen die een beheerder op een rol kan toepassen. Een beheerder kan rechtensets toewijzen aan een rol in plaats van individuele machtigingen toe te wijzen. Dit staat u toe om douanerollen van een vooraf bepaalde rol tot stand te brengen die een groep toestemmingen bevat. |
| Beleid | Het beleid is verklaringen die attributen samenbrengen om toegelaten en ontoelaatbare acties te vestigen. Het beleid kan of lokaal of globaal zijn, en kan ander beleid met voeten treden. |
| Bron | Een bron is het element dat of het object dat een onderwerp kan of kan benaderen. Bronnen kunnen segmenten of schemavelden zijn. |
| Rollen | Rollen zijn manieren om de soorten gebruikers te categoriseren die met uw instantie van het Platform in wisselwerking staan en bouwstenen van toegangsbeheerbeleid zijn. In een op rol-gebaseerd milieu van het toegangsbeheer, is de levering van de gebruikerstoegang groepering door gemeenschappelijke verantwoordelijkheden en behoeften. Een rol heeft een bepaalde reeks toestemmingen en de leden van uw organisatie kunnen aan één of meerdere rollen, afhankelijk van het werkingsgebied van mening worden toegewezen of toegang schrijven zij nodig hebben. |
| Onderwerp | Een onderwerp is de gebruiker die toegang tot een bron aanvraagt om een handeling uit te voeren. |
| Gebruikersgroepen | Gebruikersgroepen zijn meerdere gebruikers die zijn gegroepeerd en die toegang hebben om dezelfde functies uit te voeren. |

## Toestemmingen

>[!IMPORTANT]
>
>Zodra uw organisatie voor op attributen-gebaseerde toegangsbeheer wordt toegelaten, kunt u toestemmingen op Adobe Experience Cloud, in plaats van de Profielen van het Product in Adobe Admin Console beginnen te gebruiken, om toestemmingen voor gebruikers, functionaliteit, etiketten, en andere middelen in uw organisatie te beheren.

De toestemmingen zijn het gebied van Experience Cloud waar de beheerders gebruikersrollen en toegangsbeleid kunnen bepalen om toegangstoestemmingen voor eigenschappen en voorwerpen binnen een producttoepassing te beheren.

Door Toestemmingen, kunt u rollen tot stand brengen en beheren, evenals de gewenste middeltoestemmingen voor deze rollen toewijzen. Met machtigingen kunt u ook de labels, sandboxen en gebruikers beheren die aan een specifieke rol zijn gekoppeld. Zie de klasse [Handleiding voor machtigingen](ui/browse.md).

## API voor toegangsbeheer op basis van kenmerken

Met de op kenmerken gebaseerde API voor toegangsbeheer kunt u rollen, beleid en producten binnen het platform programmatisch beheren met behulp van API&#39;s. Zie voor meer informatie de handleiding op [het gebruiken van API om op attributen-gebaseerde configuraties van de toegangscontrole te beheren](api/overview.md).

## Toegangsbeheer op basis van kenmerken in Adobe Experience Platform

De volgende secties verstrekken informatie over hoe op attribuut-gebaseerde toegangsbeheer aan andere componenten van Platform wordt geïntegreerd:

### Toegangsbeheer

Platform hefboomwerkingen [Adobe Admin Console](https://adminconsole.adobe.com) productprofielen om gebruikers te koppelen aan machtigingen en sandboxen. De toestemmingen controleren toegang tot een verscheidenheid van de mogelijkheden van het Platform, met inbegrip van gegevensmodellering, profielbeheer, en zandbakbeleid. Zodra uw organisatie voor op attributen-gebaseerde toegangsbeheer wordt toegelaten, kunt u toestemmingen op Adobe Experience Cloud, in plaats van de Profielen van het Product in Adobe Admin Console beginnen te gebruiken, om toestemmingen voor gebruikers, functionaliteit, etiketten, en andere middelen in uw organisatie te beheren.

Er is beperkte beschikbaarheid voor op attribuut-gebaseerde toegangsbeheer voor klanten die Gezondheidszorg en/of de Schilden van de Privacy kopen. De functies van deze functionaliteit zijn onder andere:

* De interface van toestemmingen: Verstrekt een interface voor u om gebruikersrollen, toestemmingen en beleid voor op attribuut-gebaseerde toegangsbeheer te bepalen.

* Etikettering: Voeg toe, geef, verwijder etiketten aan gebruikersrollen, schemagebieden, segmenten, en andere gesteunde voorwerpen uit om het beleid van de toegangscontrole te hefboomwerking.

De beleidswerkschema&#39;s voor alle Experience Platform-aangedreven toepassingen van Admin Console aan de nieuwe interface van Toestemmingen worden geschakeld.

>[!IMPORTANT]
>
>Uw productprofielen worden automatisch gemigreerd naar de interface voor machtigingen als uw organisatie is ingeschakeld. De productprofielen in Admin Console blijven op dit moment ongewijzigd. Gelieve **niet** pas uw productprofielen aan nadat uw organisatie is toegelaten.

Voor meer informatie over toegangsbeheer, zie [toegangsbeheeroverzicht](../home.md).

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
>* U kunt alleen segmenten activeren die u hebt gemachtigd om te openen en te bekijken in het dialoogvenster [segmentbladerweergave](/help/segmentation/ui/overview.md#browse) en [stap voor segment selecteren](/help/destinations/ui/activate-batch-profile-destinations.md#select-segments) van de activeringsworkflow.
>* In de [toewijzingsstap van de activeringsworkflow](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping), kunt u alleen de velden weergeven en selecteren voor activering waarvoor u toegangsrechten hebt.
>* Wanneer u extra segmenten wilt activeren naar een bestaand doel waar u geen toegang hebt tot alle velden die zijn toegewezen voor export, wordt de activeringsworkflow voor u geblokkeerd.

Voor meer informatie over [!DNL Destinations], verwijst u naar de [[!DNL Destinations] overzicht](../../destinations/home.md).

### Identiteitsservice

Adobe Experience Platform [!DNL Identity Service] helpt u een beter inzicht te krijgen in uw klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen, zodat u in real time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

Als deel van op attribuut-gebaseerde toegangsbeheer, `view-identity-graph` Met deze machtiging kunt u bepalen welke gebruikers in uw organisatie toegang hebben tot de identiteitsgrafiek via de gebruikersinterface of API&#39;s. Zie de handleiding voor meer informatie over [de viewer voor identiteitsgrafieken gebruiken](../../identity-service/ui/identity-graph-viewer.md).

Voor meer informatie over [!DNL Identity Service], verwijst u naar de [[!DNL Identity Service] overzicht](../../identity-service/home.md).

### Klantprofiel in realtime

Met Platform kunt u zorgen voor gecoördineerde, consistente en relevante ervaringen voor uw klanten, ongeacht waar of wanneer ze met uw merk communiceren. Met het Profiel van de Klant in real time, kunt u een holistische mening van elke individuele klant zien die gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derdegegevens combineert. Het profiel staat u toe om uw ongelijke klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

Als beheerder, kunt u op attribuut-gebaseerde toegangsbeheerfunctionaliteit gebruiken aan:

* Configureer gebruikerstoegang tot specifieke profielkenmerken op basis van rol, machtigingen en labels.
   * Als beheerder, kunt u gebruikers in uw organisatie verstrekken om profielattributen slechts te zien die met etiketten worden geëtiketteerd die de gebruikers toegang hebben tot, en profielattributen die geen etiket bevatten;
   * Als beheerder, kunt u gebruikers in uw organisatie voorzien om profielattributen slechts te zien die met etiketten worden geëtiketteerd die de gebruikers toegang hebben tot, wanneer het creëren van segmenten;
* Vorm gebruikerstoegang tot gegevensvoorproef door specifieke gegevensgebieden te etiketteren die in het schema XDM van het gegevensmodel worden gebruikt.

Raadpleeg voor meer informatie over Profiel de [Profieloverzicht](../../profile/home.md).

### Segmenteringsservice

[!DNL Segmentation Service] definieert een bepaalde subset van profielen door de criteria te beschrijven die een verhandelbare groep personen binnen uw klantenbasis onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

Als beheerder, kunt u op attribuut-gebaseerde toegangsbeheerfunctionaliteit gebruiken aan:

* Vorm gebruikerstoegang om specifieke segmenten te bekijken en te beheren, die op rol, toestemmingen, en etiketten worden gebaseerd;
   * Als beheerder, kunt u gebruikers in uw organisatie voorzien om segmenten slechts te zien die met etiketten worden geëtiketteerd die de gebruikers toegang hebben tot, en segmenten die geen etiketten bevatten, wanneer het gebruiken van de Segmentatie UI.

Voor meer informatie over [!DNL Segmentation Service], verwijst u naar de [[!DNL Segmentation Service] overzicht](../../segmentation/home.md).

### XDM

Het Model van Gegevens van de ervaring (XDM) is een open-bronspecificatie die wordt ontworpen om de kracht van digitale ervaringen te verbeteren. Het verstrekt gemeenschappelijke structuren en definities voor om het even welke toepassing om met de diensten op Platform te communiceren. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

Met op attribuut-gebaseerde toegangscontrole, kunt u:

* [Gegevensgebruikslabels toepassen op veldgroepen en -klassen](../../xdm/tutorials/labels.md). Hierdoor kunnen in meerdere schema&#39;s met dezelfde veldgroepen of klassen velden worden gelabeld met dezelfde kenmerken, afhankelijk van de configuraties op veldniveau of veldniveau.
* Vorm gebruikerstoegang tot specifieke XDM schemagebieden afhankelijk van de toestemmingsreeksen die op rollen worden toegepast die aan gebruikers worden toegewezen.

Raadpleeg voor meer informatie over XDM de [XDM-overzicht](../../xdm/home.md).
---
keywords: Experience Platform;thuis;populaire onderwerpen;DULE;module
solution: Experience Platform
title: Overzicht gegevensbeheer
topic: overview
description: Met Adobe Experience Platform Data Governance kunt u klantgegevens beheren en ervoor zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik worden nageleefd. Het speelt een sleutelrol binnen Experience Platform op diverse niveaus, met inbegrip van catalogiseren, gegevenslijn, het etiketteren van het gegevensgebruik, het beleid van het gegevensgebruik, en het controleren van het gebruik van gegevens voor marketing acties
translation-type: tm+mt
source-git-commit: 37c1c98ccba50fa917acc5e93763294f4dde5c36
workflow-type: tm+mt
source-wordcount: '1345'
ht-degree: 0%

---


# Overzicht van gegevensbeheer

Een van de kernmogelijkheden van Adobe Experience Platform is om gegevens van meerdere bedrijfssystemen samen te brengen, zodat marketeers klanten beter kunnen identificeren, begrijpen en betrekken. Deze gegevens zijn mogelijk onderworpen aan gebruiksbeperkingen die zijn gedefinieerd door uw organisatie of wettelijke voorschriften. Daarom is het belangrijk om ervoor te zorgen dat uw gegevensbewerkingen binnen [!DNL Platform] compatibel zijn met het beleid voor gegevensgebruik.

Met Adobe Experience Platform [!DNL Data Governance] kunt u klantgegevens beheren en ervoor zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik worden nageleefd. Het speelt een belangrijke rol binnen [!DNL Experience Platform] op diverse niveaus, met inbegrip van catalogiseren, gegevenslijn, het etiketteren van het gegevensgebruik, het beleid van het gegevensgebruik, en het controleren van het gebruik van gegevens voor marketing acties.

## Functies voor gegevensbeheer

Het gegevensbeheer is niet automatisch en ook niet in een vacuüm. Wat begon als een rol voor één individu, dat doorgaans wordt erkend als een datastrijder, is aanzienlijk gegroeid naarmate het ecosysteem voor gegevensbeheer is uitgebreid. Tegenwoordig vereist gegevensbeheer voortdurend beheer en toezicht om succesvol te zijn en is het afhankelijk van datatransfers die beschikken over instrumenten waarmee gegevens correct kunnen worden gelabeld, het gebruiksbeleid kan worden gecreëerd en de naleving van dat beleid kan worden afgedwongen.

Hoewel het beheer van gegevens de verantwoordelijkheid van elk individu in de organisatie moet zijn, zijn er enkele essentiële functies binnen de cyclus van gegevensbeheer:

![Rollen gegevensbeheer](./images/overview/roles.png)

### Data steward

Gegevensstewards vormen de kern van gegevensbeheer. Deze rol is verantwoordelijk voor het interpreteren van verordeningen, contractuele beperkingen, en beleid, en het toepassen van hen direct op de gegevens. Op basis van hun kennis van deze verordeningen, beperkingen en beleidsvormen, is de rol van gegevensbeheerder onder meer:

* Gegevens, gegevenssets en gegevensvoorbeelden evalueren om labels voor metagegevensgebruik toe te passen en te beheren.
* Het creëren van gegevensbeleid en het toepassen van hen op datasets en gebieden.
* Het communiceren van gegevensbeleid aan de organisatie.

### Marketer

Marktdeelnemers zijn het eindpunt van gegevensbeheer. Ze vragen gegevens van de infrastructuur voor gegevensbeheer die is gemaakt door data stewards, wetenschappers en engineers. Marktdeelnemers omvatten een aantal verschillende specialiteiten onder de marketingparaplu, waaronder:

* De analisten van de marketing verzoeken gegevens om inzicht in klanten, zowel als individuen als in groepen (ook die als segmenten worden bekend) toe te laten.
* De Specialisten van de marketing en Ontwerpers van de Ervaring gebruiken gegevens om nieuwe klantenervaringen te ontwerpen.


## [!DNL Data Governance] kader

Het [!DNL Data Governance]-framework vereenvoudigt en stroomlijnt het proces voor het categoriseren van gegevens en het maken van beleidsregels voor gegevensgebruik. Zodra gegevensetiketten zijn toegepast en het beleid van het gegevensgebruik op zijn plaats is, kunnen de marketing acties worden geëvalueerd om het correcte gebruik van gegevens te verzekeren.

Het [!DNL Data Governance]-framework kent drie hoofdelementen: Labels, Beleid en Handhaving.

1. **Labels:** classificeer gegevens die privacygerelateerde overwegingen en contractuele voorwaarden weerspiegelen, zodat deze in overeenstemming zijn met regelgeving en organisatiebeleid.
1. **Beleid:** Beschrijf welke soort(en) marketingacties al dan niet mogen worden uitgevoerd met betrekking tot specifieke gegevens.
1. **Handhaving:** gebruikt het beleidskader om beleid over verschillende gegevenstoegangspatronen te adviseren en af te dwingen.

## Labels voor gegevensgebruik

[!DNL Data Governance] laat gegevens toe stewards om gebruiksetiketten op de dataset en gebiedsniveau toe toe te passen om gegevens volgens het type van beleid te categoriseren dat van toepassing is.

Het [!DNL Data Governance]-framework bevat vooraf gedefinieerde labels voor gegevensgebruik waarmee gegevens op drie manieren kunnen worden gecategoriseerd:

![Categorieën gegevensgebruikslabels](./images/overview/label-categories.png)

* **Contract &quot;C&quot;de Etiketten van Gegevens:** Etiket en categoriseer gegevens die contractuele verplichtingen hebben of met het beleid van het de gegevensbeheer van de klant verwant zijn.
* **Gegevenslabels identiteit &quot;I&quot;:gegevens** labelen en indelen die een specifieke persoon kunnen identificeren of benaderen.
* **Gevoelige &quot;S&quot;-gegevenslabels:** Gegevens met betrekking tot gevoelige gegevens zoals geografische gegevens labelen en categoriseren.

>[!NOTE]
>
>Zie de handleiding op [ondersteunde labels voor gegevensgebruik](labels/reference.md) voor een volledige lijst met beschikbare labels en definities voor elk labeltype.

Labels kunnen op elk gewenst moment worden toegepast, zodat u op flexibele wijze gegevens kunt beheren. De beste praktijken bevorderen etiketteringsgegevens zodra het in [!DNL Experience Platform] wordt opgenomen, of zodra de gegevens in [!DNL Platform] beschikbaar worden.

Zie het overzicht op [labels voor gegevensgebruik](./labels/overview.md) voor meer informatie.

## Beleid voor gegevensgebruik

Om gegevensgebruikslabels effectief te steunen gegevensnaleving, moet het beleid van het gegevensgebruik worden uitgevoerd. Beleid voor gegevensgebruik is regels die het soort marketingacties beschrijven dat u mag uitvoeren op gegevens binnen [!DNL Experience Platform].

Een voorbeeld van een marketing actie zou de wens kunnen zijn om een dataset naar een derdedienst uit te voeren. Als er een beleid bestaat dat zegt dat specifieke types van gegevens, zoals Persoonlijk Identificeerbare Informatie (PII), niet kunnen worden uitgevoerd en een &quot;I&quot;etiket (de Gegevens van de Identiteit) is toegepast op de dataset, zult u een reactie van [!DNL Policy Service] ontvangen die u vertelt dat een beleid van het gegevensgebruik is geschonden.

Nadat labels voor gegevensgebruik zijn toegepast, kunnen gegevensbeheerders beleid maken met de [!DNL Policy Service]-API of de [!DNL Experience Platform]-gebruikersinterface.

>[!IMPORTANT]
>
>Alle beleidsregels voor gegevensgebruik (inclusief kernbeleid van Adobe) zijn standaard uitgeschakeld. Om een individueel beleid voor handhaving te overwegen, moet u dat beleid manueel toelaten.

Voor meer informatie over het beleid van het gegevensgebruik en marketing acties, zie [beleidsoverzicht](./policies/overview.md).

## Volgende stappen

Dit document biedt een introductie op hoog niveau voor [!DNL Data Governance] en het [!DNL Data Governance]-framework. U kunt nu doorgaan met de [gegevensgebruikslabels in de gebruikershandleiding](labels/user-guide.md) en gebruikslabels toevoegen aan uw ervaringsgegevens.

## Aanhangsel

In de volgende sectie vindt u aanvullende informatie over [!DNL Data Governance].

### [!DNL Data Governance] terminologie

In de volgende tabel worden de belangrijkste termen beschreven die betrekking hebben op [!DNL Data Governance] en het [!DNL Data Governance] framework.

| Term | Definitie |
|---|---|
| **Contractlabels** | De etiketten van het contract &quot;C&quot;worden gebruikt om gegevens te categoriseren die contractuele verplichtingen hebben of met het beleid van het gegevensbeheer van uw organisatie verwant zijn. |
| **Gegevens naar andere sites** | Gegevens die naar andere sites verwijzen, zijn de combinatie van gegevens van verschillende sites, waaronder een combinatie van gegevens ter plaatse en externe gegevens of een combinatie van gegevens van verschillende externe bronnen. |
| **Gegevensbeheer** | Gegevensbeheer omvat de strategieën en technologieën die worden gebruikt om ervoor te zorgen dat gegevens in overeenstemming zijn met de regelgeving en het bedrijfsbeleid met betrekking tot gegevensgebruik. |
| **Data steward** | De gegevensbeheerder is de persoon die verantwoordelijk is voor het beheer, het toezicht en de handhaving van de gegevensactiva van een organisatie. Een gegevensgestuurde functie zorgt er ook voor dat het beleid inzake gegevensbeheer wordt gewaarborgd en gehandhaafd om in overeenstemming te zijn met de overheidsvoorschriften en het organisatiebeleid. |
| **Labels voor gegevensgebruik** | Met labels voor gegevensgebruik kunnen gebruikers gegevens categoriseren die privacygerelateerde overwegingen en contractuele voorwaarden weerspiegelen om te voldoen aan de regels en het bedrijfsbeleid. |
| **Dataset-labels** | De etiketten kunnen aan een dataset worden toegevoegd. Alle gebieden binnen een dataset erven de etiketten van de dataset. |
| **Veldlabels** | Veldlabels zijn labels voor gegevensbeheer die zijn overgeërfd van een gegevensset of die rechtstreeks op een veld zijn toegepast.  Labels voor gegevensbeheer die op een veld worden toegepast, worden niet overgeërfd tot een gegevensset. |
| **Geofence** | Een geofence is een virtuele geografische grens, gedefinieerd door GPS- of RFID-technologie, die software in staat stelt een reactie te activeren wanneer een mobiel apparaat een bepaald gebied binnenkomt of verlaat. |
| **Identiteitslabels** | De etiketten van de identiteit &quot;I&quot;worden gebruikt om gegevens te categoriseren die een specifieke persoon kunnen identificeren of contacteren. |
| **Rentegerichte gerichtheid** | Rentegerichte gericht zijn, ook bekend als verpersoonlijking, komt voor als aan de volgende drie voorwaarden wordt voldaan: gegevens die ter plaatse worden verzameld, worden gebruikt om conclusies te trekken over de belangen van de gebruikers, worden in een andere context gebruikt, bijvoorbeeld op een andere site of een andere app (off-site), en worden gebruikt om te selecteren welke inhoud of advertenties op basis van die conclusies worden aangeboden. |
| **Handeling** | Een marketingactie, in het kader van het gegevensbeheerkader, is een actie die een [!DNL Experience Platform] gegevensconsument onderneemt, waarvoor moet worden gecontroleerd op schendingen van het gegevensgebruiksbeleid |
| **Beleid** | In het kader van gegevensbeheer is een beleid een regel die beschrijft welke marketingacties al dan niet mogen worden ondernomen met betrekking tot specifieke gegevens. |
| **Gevoelige labels** | De gevoelige etiketten &quot;S&quot;worden gebruikt om gegevens te categoriseren die u, en uw organisatie, gevoelig overwegen. |

## Aanvullende bronnen

De volgende video is bedoeld om uw begrip van het [!DNL Data Governance] kader te steunen.

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&enable10seconds=on&speedcontrol=on)

De volgende video biedt een inleiding tot verschillende [!DNL Data Governance]-functies in Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/36653?quality=12&enable10seconds=on&speedcontrol=on)
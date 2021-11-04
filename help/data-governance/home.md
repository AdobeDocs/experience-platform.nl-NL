---
keywords: Experience Platform;thuis;populaire onderwerpen;DULE;module
solution: Experience Platform
title: Overzicht gegevensbeheer
topic-legacy: overview
description: Met Adobe Experience Platform Data Governance kunt u klantgegevens beheren en ervoor zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik worden nageleefd. Het speelt een sleutelrol binnen Experience Platform op diverse niveaus, met inbegrip van catalogiseren, gegevenslijn, het etiketteren van het gegevensgebruik, het beleid van het gegevensgebruik, en het controleren van het gebruik van gegevens voor marketing acties
exl-id: 00ca6bc2-1c58-4ea2-8bb5-30fd3fa5944a
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '1371'
ht-degree: 0%

---

# Overzicht van gegevensbeheer

Een van de kernmogelijkheden van Adobe Experience Platform is om gegevens van meerdere bedrijfssystemen samen te brengen, zodat marketeers klanten beter kunnen identificeren, begrijpen en betrekken. Deze gegevens zijn mogelijk onderworpen aan gebruiksbeperkingen die zijn gedefinieerd door uw organisatie of wettelijke voorschriften. Daarom is het belangrijk ervoor te zorgen dat uw gegevens binnen [!DNL Platform] zijn compatibel met het beleid voor gegevensgebruik.

Met Adobe Experience Platform Data Governance kunt u klantgegevens beheren en ervoor zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik worden nageleefd. Het speelt een sleutelrol binnen [!DNL Experience Platform] op verschillende niveaus, waaronder catalogisering, gegevenskoppeling, etikettering van het gegevensgebruik, beleid inzake gegevensgebruik en controle op het gebruik van gegevens voor marketingacties.

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


## Kader voor gegevensbeheer

Het gegevensbeheerkader vereenvoudigt en stroomlijnt het proces om gegevens te categoriseren en het beleid van het gegevensgebruik te creëren. Zodra gegevensetiketten zijn toegepast en het beleid van het gegevensgebruik op zijn plaats is, kunnen de marketing acties worden geëvalueerd om het correcte gebruik van gegevens te verzekeren.

Het kader voor gegevensbeheer bestaat uit drie hoofdelementen: Labels, Beleid en Handhaving.

1. **Labels:** Gegevens indelen die privacygerelateerde overwegingen en contractuele voorwaarden weerspiegelen, zodat deze in overeenstemming zijn met regelgeving en organisatiebeleid.
1. **Beleid:** Beschrijf welke marketingacties al dan niet zijn toegestaan voor specifieke gegevens.
1. **Handhaving:** Gebruikt het beleidskader om beleid over verschillende patronen van de gegevenstoegang te adviseren en af te dwingen.

## Labels voor gegevensgebruik

Met gegevensbeheer kunnen de gegevens in plaats daarvan worden gebruikt om labels op gegevensset en veldniveau toe te passen om gegevens te categoriseren op basis van het type beleid dat van toepassing is.

Het gegevensbeheerframework bevat vooraf gedefinieerde labels voor gegevensgebruik waarmee gegevens op drie manieren kunnen worden gecategoriseerd:

![Categorieën gegevensgebruikslabels](./images/overview/label-categories.png)

* **Gegevenslabels &quot;C&quot;-contract:** Label en categoriseer gegevens die contractuele verplichtingen hebben of verband houden met het beleid voor het beheer van klantgegevens.
* **Gegevenslabels van identiteit &quot;I&quot;:** Label en categoriseer gegevens die een specifieke persoon kunnen identificeren of contacteren.
* **Gevoelige S-gegevenslabels:** Gegevens met betrekking tot gevoelige gegevens zoals geografische gegevens labelen en indelen.

>[!NOTE]
>
>Zie de handleiding op [ondersteunde labels voor gegevensgebruik](labels/reference.md) voor een volledige lijst van beschikbare etiketten, evenals definities voor elk etikettype.

Labels kunnen op elk gewenst moment worden toegepast, zodat u op flexibele wijze gegevens kunt beheren. De beste praktijken bevorderen etiketteringsgegevens zodra het wordt opgenomen in [!DNL Experience Platform]of zodra gegevens beschikbaar komen in [!DNL Platform].

Zie het overzicht op [gegevensgebruikslabels](./labels/overview.md) voor meer informatie .

## Beleid voor gegevensgebruik

Om gegevensgebruikslabels effectief te steunen gegevensnaleving, moet het beleid van het gegevensgebruik worden uitgevoerd. Het beleid van het gebruik van gegevens is regels die de soorten marketing acties beschrijven die u aan, of beperkt van, op gegevens binnen mag uitvoeren [!DNL Experience Platform].

Een voorbeeld van een marketing actie zou de wens kunnen zijn om een dataset naar een derdedienst uit te voeren. Als er een beleid bestaat dat zegt dat specifieke types van gegevens, zoals Persoonlijk Identificeerbare Informatie (PII), niet kunnen worden uitgevoerd en een &quot;I&quot;etiket (de Gegevens van de Identiteit) is toegepast op de dataset, zult u een antwoord van ontvangen [!DNL Policy Service] u vertellen dat een beleid van het gegevensgebruik is geschonden.

Zodra de etiketten van het gegevensgebruik zijn toegepast, kunnen de gegevens stewards beleid tot stand brengen gebruikend [!DNL Policy Service] API of de [!DNL Experience Platform] gebruikersinterface.

>[!IMPORTANT]
>
>Alle beleidsregels voor gegevensgebruik (inclusief kernbeleid van Adobe) zijn standaard uitgeschakeld. Om een individueel beleid voor handhaving te overwegen, moet u dat beleid manueel toelaten.

Voor meer informatie over het beleid en de marketingacties van het gegevensgebruik, zie [beleidsoverzicht](./policies/overview.md).

## Volgende stappen

Dit document bevatte een inleiding op hoog niveau op het gebied van gegevensbeheer en gegevensbeheer. U kunt nu doorgaan naar het dialoogvenster [gebruikershandleiding voor gegevensgebruikslabels](labels/user-guide.md) en begin gebruiksetiketten aan uw ervaringsgegevens toe te voegen.

## Aanhangsel

In het volgende gedeelte wordt aanvullende informatie gegeven over gegevensbeheer.

### terminologie voor gegevensbeheer

De volgende tabel geeft een overzicht van de belangrijkste termen met betrekking tot gegevensbeheer en het kader voor gegevensbeheer.

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
| **Handeling** | Een marketingactie, in het kader van het kader voor gegevensbeheer, is een actie die [!DNL Experience Platform] gegevens die de consument nodig heeft, waarvoor moet worden nagegaan of het beleid inzake gegevensgebruik wordt geschonden |
| **Beleid** | In het kader van gegevensbeheer is een beleid een regel die beschrijft welke marketingacties al dan niet mogen worden ondernomen met betrekking tot specifieke gegevens. |
| **Gevoelige labels** | De gevoelige etiketten &quot;S&quot;worden gebruikt om gegevens te categoriseren die u, en uw organisatie, gevoelig overwegen. |

## Aanvullende bronnen

De volgende video is bedoeld om uw begrip van het kader van het Beleid van Gegevens te steunen.

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&enable10seconds=on&speedcontrol=on)

In de volgende video wordt een inleiding gegeven op verschillende functies voor gegevensbeheer in Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/36653?quality=12&enable10seconds=on&speedcontrol=on)

---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Beheer van gegevens Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 7f6612f7dd649d68aa7ebe5b971b72d7b433b1e3
workflow-type: tm+mt
source-wordcount: '1434'
ht-degree: 0%

---


# Overzicht van gegevensbeheer

Een van de kernmogelijkheden van Adobe Experience Platform is om gegevens van meerdere bedrijfssystemen samen te brengen, zodat marketeers klanten beter kunnen identificeren, begrijpen en betrekken. Deze gegevens zijn mogelijk onderworpen aan gebruiksbeperkingen die zijn gedefinieerd door uw organisatie of wettelijke voorschriften. Daarom is het belangrijk om ervoor te zorgen dat uw gegevensbewerkingen binnen [!DNL Platform] voldoen aan het beleid voor gegevensgebruik.

Met gegevensbeheer voor Adobe Experience Platforms kunt u klantgegevens beheren en ervoor zorgen dat de voorschriften, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik worden nageleefd. Het speelt een sleutelrol binnen [!DNL Experience Platform] op diverse niveaus, met inbegrip van catalogiseren, gegevenslijn, het etiketteren van het gegevensgebruik, het beleid van het gegevensgebruik, en het controleren van het gebruik van gegevens voor marketing acties.

## Functies voor gegevensbeheer

Het gegevensbeheer is niet automatisch en ook niet in een vacuüm. Wat begon als een rol voor één individu, dat doorgaans wordt erkend als een **datastunt**, is aanzienlijk gegroeid naarmate het ecosysteem voor gegevensbeheer is uitgebreid. Tegenwoordig vereist gegevensbeheer voortdurend beheer en toezicht om succesvol te zijn en is het afhankelijk van datatransfers die beschikken over instrumenten waarmee gegevens correct kunnen worden gelabeld, het gebruiksbeleid kan worden gecreëerd en de naleving van dat beleid kan worden afgedwongen.

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


## DULE-kader

De Etikettering en de Handhaving van het Gebruik van gegevens (DULE) is het belangrijkste kader voor [!DNL Experience Platform] Gegevensbeheer. DULE vereenvoudigt en stroomlijnt het proces om gegevens te categoriseren en het beleid van het gegevensgebruik te creëren. Zodra gegevensetiketten zijn toegepast en het beleid van het gegevensgebruik is op zijn plaats, kunnen de marketing acties worden geëvalueerd om het correcte gebruik van gegevens te verzekeren.

Het DULE-raamwerk bestaat uit drie hoofdelementen: Labels, Beleid en Handhaving.

1. **Labels:** Gegevens indelen die privacygerelateerde overwegingen en contractuele voorwaarden weerspiegelen, zodat deze in overeenstemming zijn met regelgeving en organisatiebeleid.
1. **Beleid:** Beschrijf welke marketingacties al dan niet zijn toegestaan voor specifieke gegevens.
1. **Handhaving:** Gebruikt het beleidskader om beleid over verschillende patronen van de gegevenstoegang te adviseren en af te dwingen.

## Labels voor gegevensgebruik

Met gegevensbeheer kunnen de gegevens in plaats daarvan worden gebruikt om labels op gegevensset en veldniveau toe te passen om gegevens te categoriseren op basis van het type beleid dat van toepassing is.

Het DULE-framework bevat vooraf gedefinieerde labels voor gegevensgebruik waarmee gegevens op drie manieren kunnen worden gecategoriseerd:

![Categorieën gegevensgebruikslabels](./images/overview/label-categories.png)

* **Gegevenslabels &quot;C&quot;-contract:** Label en categoriseer gegevens die contractuele verplichtingen hebben of verband houden met het beleid voor het beheer van klantgegevens.
* **Gegevenslabels van identiteit &quot;I&quot;:** Label en categoriseer gegevens die een specifieke persoon kunnen identificeren of contacteren.
* **Gevoelige S-gegevenslabels:** Gegevens met betrekking tot gevoelige gegevens zoals geografische gegevens labelen en indelen.

>[!NOTE]
>
>Zie de handleiding over [ondersteunde labels](labels/reference.md) voor gegevensgebruik voor een volledige lijst met beschikbare labels en definities voor elk labeltype.

Labels kunnen op elk gewenst moment worden toegepast, zodat u op flexibele wijze gegevens kunt beheren. De beste praktijken bevorderen etiketteringsgegevens zodra het in wordt opgenomen [!DNL Experience Platform], of zodra de gegevens in [!DNL Platform].

Zie het overzicht op de labels [van het](./labels/overview.md) gegevensgebruik voor meer informatie.

## Beleid voor gegevensgebruik

Om gegevensgebruikslabels effectief te steunen gegevensnaleving, moet het beleid van het gegevensgebruik worden uitgevoerd. Het beleid van het gebruik van gegevens is regels die de soorten marketing acties beschrijven die u aan, of beperkt van, het uitvoeren op gegevens binnen wordt toegestaan [!DNL Experience Platform].

Een voorbeeld van een marketing actie zou de wens kunnen zijn om een dataset naar een derdedienst uit te voeren. Als er een beleid is dat zegt dat de specifieke types van gegevens, zoals Persoonlijk Identificeerbare Informatie (PII), niet kunnen worden uitgevoerd en een &quot;I&quot;etiket (de Gegevens van de Identiteit) is toegepast op de dataset, zult u een reactie van de Dienst van het Beleid ontvangen die u vertelt dat een beleid van het gegevensgebruik is geschonden.

Zodra de etiketten van het gegevensgebruik zijn toegepast, kunnen de gegevens stewards beleid tot stand brengen gebruikend de DULE Dienst API van het Beleid of de [!DNL Experience Platform] gebruikersinterface.

>[!IMPORTANT]
>
>Alle beleidsregels voor gegevensgebruik (inclusief kernbeleid van Adobe) zijn standaard uitgeschakeld. Om een individueel beleid voor handhaving te overwegen, moet u dat beleid manueel toelaten.

Zie het [beleidsoverzicht](./policies/overview.md)voor meer informatie over het beleid en de marketingacties voor gegevensgebruik.

## Toekomstige releases

Gegevensbeheer ondersteunt momenteel DULE-etikettering op twee niveaus (dataset en field). Gegevensbeheer ondersteunt ook het maken en beheren van beleid voor gegevensgebruik en marketingacties via de DULE Policy Service API.

De volgende versies zullen de volgende eigenschappen verstrekken:

* Beleidshandhaving: Gebruik het beleidskader om beleid over verschillende patronen van de gegevenstoegang te adviseren en af te dwingen.
* Controle: De activiteiten van de gegevenstoegang van het toezicht en identificeert en rapporteert over nalevingskwesties.

## Volgende stappen

Dit document bevatte een inleiding op hoog niveau op het gebied van gegevensbeheer en het DULE-kader. U kunt nu doorgaan met de gebruikershandleiding [voor labels voor](labels/user-guide.md) gegevensgebruik en gebruikslabels toevoegen aan uw ervaringsgegevens.

## Aanhangsel

In het volgende gedeelte wordt aanvullende informatie gegeven over gegevensbeheer.

### terminologie voor gegevensbeheer

De volgende tabel geeft een overzicht van de belangrijkste termen met betrekking tot gegevensbeheer en het DULE-kader.

| Term | Definitie |
|---|---|
| **Contractlabels** | De etiketten van het contract &quot;C&quot;worden gebruikt om gegevens te categoriseren die contractuele verplichtingen hebben of met het beleid van het gegevensbeheer van uw organisatie verwant zijn. |
| **Gegevens naar andere sites** | Gegevens die naar andere sites verwijzen, zijn de combinatie van gegevens van verschillende sites, waaronder een combinatie van gegevens ter plaatse en externe gegevens of een combinatie van gegevens van verschillende externe bronnen. |
| **Gegevensbeheer** | Gegevensbeheer omvat de strategieën en technologieën die worden gebruikt om ervoor te zorgen dat gegevens in overeenstemming zijn met de regelgeving en het bedrijfsbeleid met betrekking tot gegevensgebruik. |
| **Data steward** | De gegevensbeheerder is de persoon die verantwoordelijk is voor het beheer, het toezicht en de handhaving van de gegevensactiva van een organisatie. Een gegevensgestuurde functie zorgt er ook voor dat het beleid inzake gegevensbeheer wordt gewaarborgd en gehandhaafd om in overeenstemming te zijn met de overheidsvoorschriften en het organisatiebeleid. |
| **Labels voor gegevensgebruik** | Met labels voor gegevensgebruik kunnen gebruikers gegevens categoriseren die privacygerelateerde overwegingen en contractuele voorwaarden weerspiegelen om te voldoen aan de regels en het bedrijfsbeleid. |
| **Dataset-labels** | De etiketten kunnen aan een dataset worden toegevoegd. Alle gebieden binnen een dataset erven de etiketten van de dataset. |
| **DULE** | DULE is een acroniem voor &quot;de Etikettering en de Handhaving van het Gebruik van Gegevens.&quot; Een belangrijk onderdeel van gegevensbeheer, DULE, is een inzameling van eigenschappen die voor het etiketteren van het gegevensgebruik en het toepassen van het beleid van de gegevenstoegang voor bestuursbehoeften binnen een organisatie toestaan. |
| **Veldlabels** | Veldlabels zijn labels voor gegevensbeheer die zijn overgeërfd van een gegevensset of die rechtstreeks op een veld zijn toegepast.  Labels voor gegevensbeheer die op een veld worden toegepast, worden niet overgeërfd tot een gegevensset. |
| **Geofence** | Een geofence is een virtuele geografische grens, gedefinieerd door GPS- of RFID-technologie, die software in staat stelt een reactie te activeren wanneer een mobiel apparaat een bepaald gebied binnenkomt of verlaat. |
| **Identiteitslabels** | De etiketten van de identiteit &quot;I&quot;worden gebruikt om gegevens te categoriseren die een specifieke persoon kunnen identificeren of contacteren. |
| **Rentegerichte gerichtheid** | Rentegerichte gericht zijn, ook bekend als verpersoonlijking, komt voor als aan de volgende drie voorwaarden wordt voldaan: gegevens die ter plaatse worden verzameld, worden gebruikt om conclusies te trekken over de belangen van de gebruikers, worden in een andere context gebruikt, bijvoorbeeld op een andere site of een andere app (off-site), en worden gebruikt om te selecteren welke inhoud of advertenties op basis van die conclusies worden aangeboden. |
| **Handeling** | Een marketingactie in het kader van het gegevensbeheerkader is een actie die een [!DNL Experience Platform] gegevensconsument onderneemt en waarvoor moet worden gecontroleerd op overtredingen van het gegevensgebruiksbeleid |
| **Beleid** | In het kader van gegevensbeheer is een beleid een regel die beschrijft welke marketingacties al dan niet mogen worden ondernomen met betrekking tot specifieke gegevens. |
| **Gevoelige labels** | De gevoelige etiketten &quot;S&quot;worden gebruikt om gegevens te categoriseren die u, en uw organisatie, gevoelig overwegen. |

## Aanvullende bronnen

De volgende video is bedoeld om uw begrip van Gegevensbeheer te steunen, en schetst de belangrijkste aspecten van het Kader van de Etikettering en van de Handhaving van het Gebruik van Gegevens (DULE).

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&enable10seconds=on&speedcontrol=on)

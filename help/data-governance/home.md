---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Data Governance Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 42efd7295dd8002869694a146ea166ad21bd14bb

---


# Overzicht van gegevensbeheer

Een van de kernmogelijkheden van het Adobe Experience Platform is om gegevens van meerdere bedrijfssystemen samen te brengen, zodat marketers hun klanten beter kunnen identificeren, begrijpen en betrekken. Deze gegevens zijn mogelijk onderworpen aan gebruiksbeperkingen die zijn gedefinieerd door uw organisatie of wettelijke voorschriften. Daarom is het belangrijk om ervoor te zorgen dat uw gegevensbewerkingen binnen Platform in overeenstemming zijn met het beleid voor gegevensgebruik.

Met de gegevensbeheer van het Adobe Experience Platform kunt u klantgegevens beheren en ervoor zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik worden nageleefd. Het speelt een sleutelrol binnen het ervaringsplatform op verschillende niveaus, zoals catalogisering, datalayage, etikettering van het gegevensgebruik, het beleid voor gegevensgebruik en het controleren van het gebruik van gegevens voor marketingacties.

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

De Etikettering en de Handhaving van het Gebruik van gegevens (DULE) is het kernkader voor het Beleid van de Gegevens van het Platform van de Ervaring. DULE vereenvoudigt en stroomlijnt het proces om gegevens te categoriseren en het beleid van het gegevensgebruik te creëren. Zodra gegevensetiketten zijn toegepast en het beleid van het gegevensgebruik is op zijn plaats, kunnen de marketing acties worden geëvalueerd om het correcte gebruik van gegevens te verzekeren.

Het DULE-raamwerk bestaat uit drie hoofdelementen: Labels, Beleid en Handhaving.

1. **Labels:** Gegevens indelen die privacygerelateerde overwegingen en contractuele voorwaarden weerspiegelen, zodat deze in overeenstemming zijn met regelgeving en organisatiebeleid.
1. **Beleid:** Beschrijf welke marketingacties al dan niet zijn toegestaan voor specifieke gegevens.
1. **Handhaving:** Gebruikt het beleidskader om beleid over verschillende patronen van de gegevenstoegang te adviseren en af te dwingen.

## Labels voor gegevensgebruik

Met gegevensbeheer kunnen de gegevens in plaats daarvan worden gebruikt om labels op gegevensset en veldniveau toe te passen om gegevens te categoriseren op basis van het type beleid dat van toepassing is.

Het DULE-framework bevat vooraf gedefinieerde labels voor gegevensgebruik waarmee gegevens op vier manieren kunnen worden gecategoriseerd:

![Categorieën gegevensgebruikslabels](./images/overview/label-categories.png)

* **Gegevenslabels &quot;C&quot;-contract:** Label en categoriseer gegevens die contractuele verplichtingen hebben of verband houden met het beleid voor het beheer van klantgegevens.
* **Gegevenslabels van identiteit &quot;I&quot;:** Label en categoriseer gegevens die een specifieke persoon kunnen identificeren of contacteren.
* **Gevoelige S-gegevenslabels:** Gegevens met betrekking tot gevoelige gegevens zoals geografische gegevens labelen en indelen.
* **GDPR-gegevenslabels:** Gegevens labelen en categoriseren die persoonlijke id&#39;s kunnen bevatten voor gebruik in GDPR-toegang en/of verzoeken verwijderen.

>[!NOTE] Zie de handleiding over [ondersteunde labels](labels/reference.md) voor gegevensgebruik voor een volledige lijst met beschikbare labels en definities voor elk labeltype.

Labels kunnen op elk gewenst moment worden toegepast, zodat u op flexibele wijze gegevens kunt beheren. De beste praktijken bevorderen etiketteringsgegevens zodra het in het Platform van de Ervaring wordt opgenomen, of zodra de gegevens in Platform beschikbaar worden.

Zie het overzicht op de etiketten [van het](./labels/overview.md) gegevensgebruik voor geleidelijke instructies op hoe te om etiketten op datasets en gebieden toe te passen gebruikend UI.

## Beleid voor gegevensgebruik

Om gegevensgebruikslabels effectief te steunen gegevensnaleving, moet het beleid van het gegevensgebruik worden uitgevoerd. Het beleid van het gebruik van gegevens is regels die de soorten marketing acties beschrijven die u aan, of beperkt van, op gegevens binnen het Platform van de Ervaring mag uitvoeren.

Een voorbeeld van een marketing actie zou de wens kunnen zijn om een dataset naar een derdedienst uit te voeren. Als er een beleid is dat zegt dat de specifieke types van gegevens, zoals Persoonlijk Identificeerbare Informatie (PII), niet kunnen worden uitgevoerd en een &quot;I&quot;etiket (de Gegevens van de Identiteit) is toegepast op de dataset, zult u een reactie van de Dienst van het Beleid ontvangen die u vertelt dat een beleid van het gegevensgebruik is geschonden.

Zodra de etiketten van het gegevensgebruik zijn toegepast, kunnen de gegevensstewards beleid tot stand brengen gebruikend de DULE Dienst API van het Beleid of de gebruikersinterface van het Platform van de Ervaring.

Voor meer informatie bij het uitvoeren van de belangrijkste verrichtingen die door de DULE Dienst API van het Beleid worden verstrekt, zie de de ontwikkelaarsgids [van de Dienst van het](api/getting-started.md)Beleid. Voor geleidelijke instructies over het werken met DULE beleid, zie de zelfstudie over het [creëren van en het evalueren van DULE beleid gebruikend API](policies/create.md).

Voor informatie over hoe te om beleid in de UI van het Platform van de Ervaring te beheren, zie de gids [van de](policies/user-guide.md)beleidsgebruiker.

## Toekomstige releases

Gegevensbeheer ondersteunt momenteel DULE-etikettering op twee niveaus (dataset en field). Gegevensbeheer ondersteunt ook het maken en beheren van beleid voor gegevensgebruik en marketingacties via de DULE Policy Service API.

De volgende versies zullen de volgende eigenschappen verstrekken:

* Labels voor aangepast gegevensgebruik: Maak nieuwe labels en definities op basis van de behoeften van uw organisatie.
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
| **Handeling** | Een marketingactie in het kader van het gegevensbeheerkader is een actie die een gebruiker van het ervaringsplatform onderneemt en waarvoor moet worden gecontroleerd op schendingen van het gegevensgebruiksbeleid |
| **Beleid** | In het kader van gegevensbeheer is een beleid een regel die beschrijft welke marketingacties al dan niet mogen worden ondernomen met betrekking tot specifieke gegevens. |
| **Gevoelige labels** | De gevoelige etiketten &quot;S&quot;worden gebruikt om gegevens te categoriseren die u, en uw organisatie, gevoelig overwegen. |

## Aanvullende bronnen

De volgende video is bedoeld om uw begrip van Gegevensbeheer te steunen, en schetst de belangrijkste aspecten van het Kader van de Etikettering en van de Handhaving van het Gebruik van Gegevens (DULE).

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&enable10seconds=on&speedcontrol=on)

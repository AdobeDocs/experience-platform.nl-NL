---
keywords: Experience Platform;home;populaire onderwerpen;DULE;module
solution: Experience Platform
title: Overzicht gegevensbeheer
description: Met Adobe Experience Platform Data Governance kunt u klantgegevens beheren en ervoor zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op het gebruik van gegevens worden nageleefd. Het speelt binnen Experience Platform een sleutelrol op verschillende niveaus, zoals catalogisering, gegevenskoppeling, etikettering van het gegevensgebruik, het beleid voor gegevensgebruik en het controleren van het gebruik van gegevens voor marketingacties.
exl-id: 00ca6bc2-1c58-4ea2-8bb5-30fd3fa5944a
source-git-commit: 9b1630a4876c0bcd7331f8da264e4f19ce00b59a
workflow-type: tm+mt
source-wordcount: '1656'
ht-degree: 0%

---

# Overzicht van gegevensbeheer {#data-governance-overview}

>[!CONTEXTUALHELP]
>id="platform_datagovernance_framework"
>title="Verplichting tot gegevensbeheer"
>abstract="Vergeet niet dat u als enige verantwoordelijk bent voor het naleven van het beleid voor gegevensbeheer van uw organisatie en voor het voldoen aan uw wettelijke vereisten. Experience Platform biedt tools voor gegevensbeheer waarmee u uw gegevensgebruiksverplichtingen kunt beheren. Pas de juiste labels voor gegevensgebruik toe voordat u gegevens opvraagt of verwerkt. Raadpleeg de documentatie voor meer informatie over de tools en best practices voor gegevensbeheer."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html" text="Overzicht van gegevensbeheer"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html" text="Overzicht van labels voor gegevensbeheer"

Een van de kernmogelijkheden van Adobe Experience Platform is om gegevens van meerdere bedrijfssystemen samen te brengen, zodat marketeers klanten beter kunnen identificeren, begrijpen en betrekken. Deze gegevens zijn mogelijk onderworpen aan gebruiksbeperkingen die zijn gedefinieerd door uw organisatie of wettelijke voorschriften. Daarom is het belangrijk dat u ervoor zorgt dat uw gegevensbewerkingen in [!DNL Experience Platform] voldoen aan het beleid voor gegevensgebruik.

Beheer klantgegevens en zorg ervoor dat u zich houdt aan de voorschriften, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik met Adobe Experience Platform Data Governance. Het beheer van gegevens speelt binnen Experience Platform op verschillende niveaus een sleutelrol, zoals catalogisering, datalayage, etikettering van het gegevensgebruik, het beleid voor gegevensgebruik en het controleren van het gebruik van gegevens voor marketingacties.

>[!NOTE]
>
>In Experience Platform gaat het gegevensbeheer alleen over de manier waarop gegevens worden gebruikt of geactiveerd, ongeacht de gebruiker die de handeling uitvoert. Voor informatie over hoe te om toegang tot specifieke gegevensgebieden voor bepaalde gebruikers van Experience Platform binnen uw organisatie te controleren, zie in plaats daarvan de documentatie op [&#x200B; op attribuut-gebaseerde toegangsbeheer &#x200B;](../access-control/abac/overview.md).

## Functies voor gegevensbeheer {#data-governance-roles}

Het gegevensbeheer is niet automatisch en ook niet in een vacuüm. Wat begon als een rol voor één individu, dat doorgaans wordt erkend als een datastrijder, is aanzienlijk gegroeid naarmate het ecosysteem voor gegevensbeheer is uitgebreid. Het beheer van gegevens vereist voortdurend beheer en toezicht om succesvol te zijn. Effectief gegevensbeheer is afhankelijk van datateuzes die beschikken over instrumenten waarmee gegevens correct kunnen worden gelabeld, het gebruiksbeleid kan worden gecreëerd en de naleving van dat beleid kan worden afgedwongen.

Hoewel het beheer van gegevens de verantwoordelijkheid van elk individu in de organisatie moet zijn, zijn er enkele essentiële functies binnen de cyclus van gegevensbeheer:

![&#x200B; Grafisch om de vier rollen van het gegevensbeheer, met citaten over de taken van elke rol over te brengen.](./images/overview/roles.png)

### Data steward {#data-steward}

Gegevensstewards vormen de kern van gegevensbeheer. Deze rol is verantwoordelijk voor het interpreteren van verordeningen, contractuele beperkingen, en beleid, en het toepassen van hen direct op de gegevens. Op basis van hun kennis van deze verordeningen, beperkingen en beleidsvormen, is de rol van gegevensbeheerder onder meer:

* Gegevens, gegevenssets en gegevensvoorbeelden evalueren om labels voor metagegevensgebruik toe te passen en te beheren.
* Het creëren van gegevensbeleid en het toepassen van hen op datasets en gebieden.
* Het communiceren van gegevensbeleid aan de organisatie.

### Marketer {#marketer}

Marktdeelnemers zijn het eindpunt van gegevensbeheer. Ze vragen gegevens van de infrastructuur voor gegevensbeheer die is gemaakt door data stewards, wetenschappers en engineers. Marktdeelnemers omvatten een aantal verschillende specialiteiten onder de marketingparaplu, waaronder:

* De analisten van de marketing verzoeken gegevens om begrip van klanten, zowel als individuen als in groepen (ook die als segmenten worden bekend) toe te laten.
* De Specialisten van de marketing en Ontwerpers van de Ervaring gebruiken gegevens om nieuwe klantenervaringen te ontwerpen.

## Kader voor gegevensbeheer {#data-governance-framework}

Het gegevensbeheerkader vereenvoudigt en stroomlijnt het proces om gegevens te categoriseren en het beleid van het gegevensgebruik te creëren. Zodra gegevensetiketten zijn toegepast en het beleid van het gegevensgebruik is op zijn plaats, kunnen de marketing acties worden geëvalueerd om het correcte gebruik van gegevens te verzekeren.

Het kader voor gegevensbeheer bestaat uit drie hoofdelementen: labels, beleid en handhaving.

1. **Etiketten:** classificeer gegevens die op privacy betrekking hebbende overwegingen en contractuele voorwaarden wijzen om met verordeningen en organisatiebeleid te voldoen.
1. **Beleid:** beschrijf welke soorten marketing acties worden toegestaan of niet om op specifieke gegevens mogen worden genomen.
1. **Handhaving:** gebruikt het beleidskader om beleid over verschillende patronen van de gegevenstoegang te adviseren en af te dwingen.

## Labels voor gegevensgebruik {#data-usage-labels}

Het Beleid van gegevens laat gegevens toe stewards om gebruiksetiketten op het niveau van het schemagebied toe toe te passen om gegevens volgens het type van beleid te categoriseren dat van toepassing is.

Het gegevensbeheerframework bevat vooraf gedefinieerde labels voor gegevensgebruik waarmee gegevens op drie manieren kunnen worden gecategoriseerd:

![&#x200B; de drie categorieën van het gegevensgebruik etiketteren.](./images/overview/label-categories.png)

* **Etiketten van Gegevens &quot;C&quot;van het Contract:** Etiket en categoriseer gegevens die contractuele verplichtingen hebben of met het beleid van het de gegevensbeheer van de klant verwant zijn.
* **Etiketten van Gegevens &quot;I&quot;van de Identiteit:** Etiket en categoriseer gegevens die een specifieke persoon kunnen identificeren of contacteren.
* **Gevoelige Etiketten van Gegevens &quot;S&quot;:** Etiket en categoriseer gegevens met betrekking tot gevoelige gegevens zoals geografische gegevens.

>[!NOTE]
>
>Zie de gids op [&#x200B; gesteunde etiketten van het gegevensgebruik &#x200B;](labels/reference.md) voor een volledige lijst van beschikbare etiketten, en definities voor elk etikettype.

Labels kunnen op elk gewenst moment worden toegepast, zodat u op flexibele wijze gegevens kunt beheren. De beste praktijken bevorderen etiketteringsgegevens wanneer het in Experience Platform wordt opgenomen, of zodra de gegevens in [!DNL Experience Platform] beschikbaar worden.

Zie het overzicht op [&#x200B; de etiketten van het gegevensgebruik &#x200B;](./labels/overview.md) voor meer informatie over hoe de etiketten van het gegevensgebruik worden gebruikt helpen naleving van het gegevensbeheer afdwingen.

## Beleid voor gegevensgebruik {#data-usage-policies}

Voor gegevensgebruiksetiketten om gegevensnaleving effectief te steunen, moet het beleid van het gegevensgebruik worden uitgevoerd. Beleid voor gegevensgebruik is regels die het soort marketingacties beschrijven dat u mag uitvoeren op gegevens in Experience Platform of waarvan u een beperking hebt ingesteld.

Een voorbeeld van een marketing actie zou de wens kunnen zijn om een dataset naar een derdedienst uit te voeren. Als er een beleid bestaat waarin wordt verklaard dat Persoonlijk Identificeerbare Informatie (PII) niet kan worden uitgevoerd, en een etiket &quot;I&quot;(identiteitsgegevens) is toegepast op het gebiedsniveau van zijn schema. De Dienst van het beleid verhindert dan om het even welke actie die deze dataset naar een derdebestemming zou uitvoeren. Als één van deze actiepogingen voorkomt, verzendt de Dienst van het Beleid een bericht die u vertelt dat een beleid van het gegevensgebruik is geschonden.


Er zijn twee soorten beleid beschikbaar:

* **[!UICONTROL Data governance policy]**: de activering van gegevens beperken op basis van de marketingactie die wordt uitgevoerd en de labels voor gegevensgebruik die door de gegevens in kwestie worden meegevoerd.
* **[!UICONTROL Consent policy]**: Filter de profielen die aan [&#x200B; bestemmingen &#x200B;](../destinations/home.md) kunnen worden geactiveerd die op de toestemming of de voorkeur van uw klanten worden gebaseerd.

Zodra de etiketten van het gegevensgebruik zijn toegepast, kunnen de gegevensstewards beleid tot stand brengen gebruikend de Dienst API van het Beleid of de gebruikersinterface van Experience Platform. Voor meer informatie over het beleid van het gegevensgebruik en marketing acties, zie het [&#x200B; beleidsoverzicht &#x200B;](./policies/overview.md).

>[!IMPORTANT]
>
>Alle beleidsregels voor gegevensgebruik (inclusief basisbeleid van Adobe) zijn standaard uitgeschakeld. Om een individueel beleid voor handhaving te overwegen, moet u dat beleid manueel toelaten.

## Volgende stappen

Dit document bevatte een inleiding op hoog niveau op het gebied van gegevensbeheer en gegevensbeheer. U kunt nu aan de [&#x200B; gebruikersgids van de gebruiksetiketten van het gegevensgebruik &#x200B;](labels/user-guide.md) verdergaan en beginnen gebruiksetiketten aan uw ervaringsgegevens toe te voegen.

## Bijlage

In het volgende gedeelte wordt aanvullende informatie gegeven over gegevensbeheer.

### terminologie voor gegevensbeheer {#data-governance-terminology}

De volgende tabel geeft een overzicht van de belangrijkste termen met betrekking tot gegevensbeheer en het kader voor gegevensbeheer.

| Term | Definitie |
|---|---|
| **de etiketten van het Contract** | De etiketten van het contract &quot;C&quot;worden gebruikt om gegevens te categoriseren die contractuele verplichtingen hebben of met het beleid van het gegevensbeheer van uw organisatie verwant zijn. |
| **gegevens van de dwars-plaats** | Gegevens die naar andere sites verwijzen, vormen de combinatie van gegevens van verschillende sites. Gegevens die naar andere sites verwijzen, omvatten zowel onsite als externe gegevens, of een combinatie van gegevens van verschillende externe bronnen. |
| **het bestuur van Gegevens** | Gegevensbeheer omvat de strategieën en technologieën die worden gebruikt om ervoor te zorgen dat gegevens in overeenstemming zijn met de regelgeving en het bedrijfsbeleid met betrekking tot gegevensgebruik. |
| **Beweging van Gegevens** | De gegevensbeheerder is de persoon die verantwoordelijk is voor het beheer, het toezicht en de handhaving van de gegevensactiva van een organisatie. Een gegevensgestuurde benadering zorgt er ook voor dat het beleid inzake gegevensbeheer wordt gewaarborgd en gehandhaafd om in overeenstemming te zijn met de overheidsvoorschriften en het organisatiebeleid. |
| **de gebruiksetiketten van Gegevens** | Met labels voor gegevensgebruik kunnen gebruikers gegevens categoriseren die privacygerelateerde overwegingen en contractuele voorwaarden weerspiegelen om te voldoen aan de regels en het bedrijfsbeleid. |
| **de etiketten van de Dataset** | U kunt labels toevoegen aan een schema. Alle gebieden binnen een dataset erven de etiketten van het schema. |
| **de etiketten van het Gebied** | Veldlabels zijn labels voor gegevensbeheer die zijn overgeërfd van een schema of rechtstreeks zijn toegepast op een veld. Labels voor gegevensbeheer die op een veld worden toegepast, worden niet tot het schemaniveau overgeërfd. |
| **Geofence** | Een geofence is een virtuele geografische grens, gedefinieerd door GPS- of RFID-technologie, die software in staat stelt een reactie te activeren wanneer een mobiel apparaat een bepaald gebied binnenkomt of verlaat. |
| **de etiketten van de Identiteit** | De etiketten van de identiteit &quot;I&quot;worden gebruikt om gegevens te categoriseren die een specifieke persoon kunnen identificeren of contacteren. |
| **Op rente-Gebaseerd richtend** | Op rente-gebaseerd richten, die ook als verpersoonlijking wordt bekend, komt voor als de volgende drie voorwaarden worden voldaan:<br> Gegevens die op-plaats worden verzameld is, <br><ul><li>Gebruikt om conclusies te trekken over het belang van de gebruikers,</li><li>Wordt gebruikt in een andere context, zoals op een andere site of in een app (externe site)</li><li>Wordt gebruikt om te selecteren welke inhoud of advertenties worden aangeboden op basis van die conclusies.</li></ul> |
| **de Marketing actie** | Een marketingactie in het kader van het gegevensbeheerkader is een actie die een Experience Platform-gegevensconsument onderneemt en waarvoor moet worden gecontroleerd op overtredingen van het gegevensgebruiksbeleid |
| **Beleid** | In het kader van gegevensbeheer is een beleid een regel die beschrijft welke soorten marketingacties al dan niet mogen worden ondernomen met betrekking tot specifieke gegevens. |
| **Etiketten van het Schema** | Beheer de etiketten voor gegevensbeheer, toestemming, en toegangsbeheer op het schemaniveau. Dit verspreidt de etiketten aan elke dataset die dat schema gebruikt. |
| **Gevoelige Etiketten** | De gevoelige etiketten &quot;S&quot;worden gebruikt om gegevens te categoriseren die u, en uw organisatie, gevoelig overwegen. |

## Aanvullende bronnen

De volgende video is bedoeld om uw begrip van het kader van het Beheer van Gegevens te steunen.

>[!IMPORTANT]
>
>De videoverwijzingen die etiketten op individuele datasetgebieden toepassen. Deze workflow is vervangen. [&#x200B; de Etiketten moeten nu op het niveau van het schemagebied &#x200B;](./e2e.md#labels) worden toegepast. De concepten in de video blijven accuraat, maar de labelworkflow is gewijzigd.

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&enable10seconds=on&speedcontrol=on)

De volgende video biedt richtlijnen voor het toepassen van labels voor gegevensgebruik op uw schema&#39;s of op de volledige dataset in Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29709/?learn=on)

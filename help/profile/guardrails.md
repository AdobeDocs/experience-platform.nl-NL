---
keywords: Experience Platform;profiel;real-time klantprofiel;het oplossen van problemen;gidsen;richtlijnen;grens;entiteit;primaire entiteit;dimensie entiteit;
title: Experience Platform-instructies voor realtime klantprofielgegevens
solution: Experience Platform
product: experience platform
topic: guide
type: Documentation
description: 'Adobe Experience Platform biedt een reeks instructies om u te helpen te voorkomen dat u gegevensmodellen maakt die niet kunnen worden ondersteund door het Real-Time Klantprofiel. In dit document worden aanbevolen procedures en beperkingen beschreven waarmee u rekening kunt houden bij het modelleren van profielgegevens. '
translation-type: tm+mt
source-git-commit: e6ecc5dac1d09c7906aa7c7e01139aa194ed662b
workflow-type: tm+mt
source-wordcount: '1457'
ht-degree: 1%

---


# [!DNL Platform] guardrails voor  [!DNL Real-time Customer Profile]

[!DNL Real-time Customer Profile] verstrekt individuele profielen die u toelaten om gepersonaliseerde dwars-kanaalervaringen te leveren die op gedragsinzichten en klantenattributen worden gebaseerd. Om dit doel te bereiken, gebruiken [!DNL Profile] en de segmenteringsmotor binnen Adobe Experience Platform een hoogst gedenormaliseerd hybride gegevensmodel dat een nieuwe benadering van het ontwikkelen van klantenprofielen aanbiedt. Het gebruik van dit hybride gegevensmodel maakt het uiterst belangrijk dat de gegevens die worden verzameld correct worden gemodelleerd. Hoewel de [!DNL Profile] gegevensopslag het handhaven van profielgegevens geen relationele opslag is, [!DNL Profile] staat integratie met kleine afmetingsentiteiten toe om segmenten op een vereenvoudigde en intuïtieve manier tot stand te brengen. Deze integratie staat bekend als segmentatie van meerdere entiteiten.

Adobe Experience Platform biedt een aantal instructies om te voorkomen dat u gegevensmodellen maakt die [!DNL Real-time Customer Profile] niet kan ondersteunen. In dit document worden deze instructies en aanbevolen procedures en beperkingen beschreven wanneer u profielgegevens gebruikt voor segmentatie.

>[!NOTE]
>
>De in dit document geschetste voorzorgsmaatregelen en limieten worden voortdurend verbeterd. Kom regelmatig terug voor updates.

## Aan de slag

Het wordt aanbevolen de volgende documentatie van de services van het Experience Platform te lezen voordat u gegevensmodellen gaat maken voor gebruik in [!DNL Real-time Customer Profile]. Als u werkt met gegevensmodellen en de instructies in dit document, hebt u inzicht nodig in de verschillende services van het Experience Platform die betrokken zijn bij het beheer van [!DNL Real-time Customer Profile]-entiteiten:

* [[!DNL Real-time Customer Profile]](home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [Adobe Experience Platform Identity Service](../identity-service/home.md): Steunt de verwezenlijking van een &quot;enige mening van de klant&quot;door identiteiten van verschillende gegevensbronnen te overbruggen aangezien zij in worden opgenomen  [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Het gestandaardiseerde kader waardoor het Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../xdm/schema/composition.md): Een inleiding tot schema&#39;s en gegevensmodellering binnen Experience Platform.
* [Adobe Experience Platform Segmentation Service](../segmentation/home.md): De segmenteringsmotor binnen  [!DNL Platform] die wordt gebruikt om publiekssegmenten van uw klantenprofielen tot stand te brengen op klantengedrag en attributen worden gebaseerd.
   * [Segmentatie](../segmentation/multi-entity-segmentation.md) van meerdere entiteiten: Een handleiding voor het maken van segmenten waarin entiteiten met dimensies worden geïntegreerd met profielgegevens.

## Typen entiteiten

Het gegevensmodel van de [!DNL Profile] opslaggegevens bestaat uit twee kerneenheidstypes:

* **Primaire entiteit:** Een primaire entiteit, of profielentiteit, voegt gegevens samen om een &quot;enige bron van waarheid&quot; voor een individu te vormen. Deze verenigde gegevens worden vertegenwoordigd gebruikend wat als &quot;verenigingsmening&quot;wordt bekend is. Een verenigingsmening voegt de gebieden van alle schema&#39;s samen die de zelfde klasse in één enkel samenvoegingsschema uitvoeren. Het samenvoegingsschema voor [!DNL Real-time Customer Profile] is een gedenormaliseerd hybride gegevensmodel dat als container voor alle profielattributen en gedragsgebeurtenissen dienst doet.

   Tijdonafhankelijke kenmerken, ook wel &quot;recordgegevens&quot; genoemd, worden gemodelleerd met behulp van [!DNL XDM Individual Profile], terwijl tijdreeksgegevens, ook wel &quot;gebeurtenisgegevens&quot; genoemd, worden gemodelleerd met behulp van [!DNL XDM ExperienceEvent]. Aangezien verslag en tijd-reeksgegevens in Adobe Experience Platform worden opgenomen, brengt het [!DNL Real-time Customer Profile] aan begin het opnemen van gegevens die voor zijn gebruik zijn toegelaten. Hoe meer interacties en details worden opgenomen, hoe robuuster de afzonderlijke profielen worden.

   ![](images/guardrails/profile-entity.png)

* **Dimension entiteit:** Uw organisatie kan ook klassen XDM bepalen om dingen buiten individuen, zoals opslag, producten, of eigenschappen te beschrijven. Deze niet-[!DNL XDM Individual Profile] schema&#39;s zijn gekend als &quot;dimensie entiteiten&quot;en bevatten geen tijd-reeksgegevens. Dimension-entiteiten bieden opzoekgegevens die de segmentatieprogramma&#39;s van meerdere entiteiten ondersteunen en vereenvoudigen. Deze moeten zo klein zijn dat de gehele gegevensset door de segmenteringsengine in het geheugen kan worden geladen voor optimale verwerking (snelle puntzoekopdracht).

   ![](images/guardrails/profile-and-dimension-entities.png)

## Limiettypen

Bij het definiëren van uw gegevensmodel is het raadzaam om binnen de beschikbare instructies te blijven, zodat u over de juiste prestaties beschikt en systeemfouten kunt voorkomen. De instructies in dit document omvatten twee typen beperkingen:

* **Zachte limiet:** een zachte limiet biedt een aanbevolen maximum voor optimale systeemprestaties. Het is mogelijk om verder te gaan dan een zachte grens zonder het systeem te breken of foutenmeldingen te ontvangen, nochtans zal het gaan voorbij een zachte grens in prestatiesdegradatie resulteren. Aanbevolen wordt om binnen de zachte limiet te blijven om een vermindering van de algehele prestaties te voorkomen.

* **Harde limiet:** een harde limiet biedt een absoluut maximum voor het systeem. Het overschrijden van een harde limiet leidt tot breuken en fouten, waardoor het systeem niet naar behoren functioneert.

## Handleidingen gegevensmodel

Aanbevolen wordt de volgende instructies te gebruiken bij het maken van een gegevensmodel voor gebruik met [!DNL Real-time Customer Profile].

### Primaire entiteitsinstructies

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Aantal gegevenssets aanbevolen om bij te dragen aan het [!DNL Profile]-samenvoegingsschema | 20 | Zacht | **Een maximum van 20  [!DNL Profile]-Toegelaten datasets wordt geadviseerd.** Om een andere dataset voor toe te laten  [!DNL Profile], zou een bestaande dataset eerst moeten worden verwijderd of worden onbruikbaar gemaakt. |
| Aantal aanbevolen relaties met meerdere entiteiten | 5 | Zacht | **Er worden maximaal vijf relaties tussen primaire entiteiten en dimensie-entiteiten aanbevolen.** Aanvullende relatietoewijzingen moeten pas worden gemaakt wanneer een bestaande relatie is verwijderd of uitgeschakeld. |
| Maximale JSON-diepte voor id-veld dat wordt gebruikt in een relatie met meerdere entiteiten | 4 | Zacht | **De aanbevolen maximale JSON-diepte voor een id-veld in relaties met meerdere entiteiten is 4.** Dit betekent dat in een hoogst-genest schema, gebieden die meer dan 4 niveaus diep worden genesteld niet als gebied van identiteitskaart in een verhouding zouden moeten worden gebruikt. |
| Arraycardinaliteit in een profielfragment | &lt;> | Zacht | **De optimale arraycardinaliteit in een profielfragment (tijdonafhankelijke gegevens) is  &lt;>** |
| Array-kardinaliteit in ExperienceEvent | &lt;> | Zacht | **De optimale arraycardinaliteit in een ExperienceEvent (tijdreeksgegevens) is  &lt;>** |

### Dimension-entiteitsgeleidingen

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Geen gegevens uit tijdreeksen toegestaan voor niet-[!DNL XDM Individual Profile] entiteiten | 0 | Hard | **Gegevens uit tijdreeksen zijn niet toegestaan voor niet-[!DNL XDM Individual Profile] entiteiten in de profielservice.** Als een reeks dataset met een niet-[!DNL XDM Individual Profile] identiteitskaart wordt geassocieerd, zou de dataset niet voor  [!DNL Profile]moeten worden toegelaten. |
| Geen geneste relaties | 0 | Zacht | **U zou geen verband tussen twee niet-[!DNL XDM Individual Profile] schema&#39;s moeten tot stand brengen.** De capaciteit om verhoudingen tot stand te brengen wordt niet geadviseerd voor om het even welke schema&#39;s die geen deel van het  [!DNL Profile] verenigingsschema uitmaken. |
| Maximale JSON-diepte voor veld primaire id | 4 | Zacht | **De aanbevolen maximale JSON-diepte voor het veld primaire id is 4.** Dit betekent dat in een hoogst-genest schema, u geen gebied als primaire identiteitskaart zou moeten selecteren als het meer dan 4 niveaus diep wordt genesteld. Een veld op het vierde geneste niveau kan als primaire id worden gebruikt. |

## Gegevensgroottehulplijnen

De volgende instructies verwijzen naar de gegevensgrootte en worden aanbevolen om ervoor te zorgen dat gegevens kunnen worden ingevoerd, opgeslagen en opgevraagd zoals bedoeld.

>[!NOTE]
>
>De gegevensgrootte wordt gemeten als ongecomprimeerde gegevens in JSON op het moment van inname.

### Primaire entiteitsinstructies

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Maximale grootte per profielfragment | 10 KB | Zacht | **De aanbevolen maximale grootte van een profielfragment is 10 kB.** Het gebruik van grotere profielfragmenten heeft invloed op de systeemprestaties. Bijvoorbeeld, zal het laden van een zware dataset van CRM waar sommige profielfragmenten 50kB in grootte zijn in degraded systeemprestaties resulteren. |
| Absolute maximumgrootte per profielfragment | 1 MB | Hard | **De absolute maximumgrootte van een profielfragment is 1 MB.** De congestie zal ontbreken wanneer het proberen om een profielfragment te uploaden dat groter is dan 1 MB. |

### Dimension-entiteitsgeleidingen

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Maximale totale grootte voor alle dimensionale entiteiten | 5 GB | Zacht | **De maximale aanbevolen totale grootte voor alle dimensionale entiteiten is 5 GB.** Het inzetten van entiteiten met een grote dimensie zal leiden tot verminderde systeemprestaties. Het wordt bijvoorbeeld niet aanbevolen een productcatalogus van 10 GB als een dimensie-entiteit te laden. |
| Datasets per dimensionaal eenheidschema | 5 | Zacht | **Het wordt aanbevolen maximaal vijf datasets toe te voegen aan elk dimensionaal eenheidschema.** Bijvoorbeeld, als u een schema voor &quot;producten&quot;creeert en vijf bijdragende datasets toevoegt, zou u geen zesde dataset moeten creëren verbonden aan het productschema. |

## Segmenteringsgeleiding

De instructies in deze sectie verwijzen naar het aantal en de aard van de segmenten die een organisatie binnen het Experience Platform kan maken, en naar het toewijzen en activeren van segmenten aan bestemmingen.

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Maximumaantal segmenten per sandbox | 10 kB | Zacht | **Het maximumaantal segmenten dat een organisatie kan maken, is 10 kB per sandbox.** Een organisatie kan in totaal meer dan 10K segmenten hebben, zolang er minder dan 10.000 segmenten in elke individuele zandbak zijn. Het proberen om extra segmenten tot stand te brengen zal in verminderde systeemprestaties resulteren. |
| Maximumaantal streamingsegmenten per sandbox | 500 | Zacht | **Het maximumaantal streamingsegmenten dat een organisatie kan maken, is 500 per sandbox.** Een organisatie kan in totaal meer dan 500 streaming segmenten hebben, zolang er zich in elke sandbox minder dan 500 streaming segmenten bevinden. Als u probeert extra streamingsegmenten te maken, neemt de systeemprestaties af. |
| Maximum aantal batchsegmenten per sandbox | 10 kB | Zacht | **Het maximumaantal batchsegmenten dat een organisatie kan maken, is 10 kB per sandbox.** Een organisatie kan in totaal meer dan 10.000 batchsegmenten hebben, zolang er in elke sandbox minder dan 10.000 batchsegmenten zijn. Het proberen om extra partijsegmenten tot stand te brengen zal in verminderde systeemprestaties resulteren. |
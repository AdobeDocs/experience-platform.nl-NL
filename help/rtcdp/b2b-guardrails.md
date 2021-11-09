---
keywords: profiel;real-time profiel van de klant;het oplossen van problemen;gidsen;grens;entiteit;primaire entiteit;dimensie-entiteit;RTCDP;CDP;B2B Edition;Real-time Customer Data Platform;real-time platform van de klantengegevens;real-time cdp;b2b;cdp;
title: Standaardhulplijnen voor Real-time Customer Data Platform B2B Edition
type: Documentation
description: 'Adobe Experience Platform gebruikt een sterk gedenormaliseerd hybride gegevensmodel dat van het traditionele relationele gegevensmodel verschilt. Dit document biedt standaardgebruiks- en tarieflimieten om u te helpen uw gegevens te modelleren voor optimale systeemprestaties met Real-time Customer Data Platform B2B Edition. '
source-git-commit: 7b9b01657ab2a682b900a8c55a201f9864e4428b
workflow-type: tm+mt
source-wordcount: '1601'
ht-degree: 0%

---


# Standaardhulplijnen voor Real-time Customer Data Platform B2B Edition

>[!NOTE]
>
>De limieten die in dit document worden beschreven, vertegenwoordigen de wijzigingen die door Real-time Customer Data Platform B2B Edition worden ingeschakeld. Voor een volledige lijst met standaardlimieten voor Real-time CDP B2B Edition, combineert u deze limieten met de algemene Adobe Experience Platform-limieten die in de [handleidingen voor de gegevensdocumentatie van het Profiel van de Klant in real time](../profile/guardrails.md).

Met Real-time Customer Data Platform B2B Edition kunt u persoonlijke kanaalervaringen op basis van gedragsinzichten en klantkenmerken aanbieden in de vorm van realtime-klantprofielen en accountprofielen. Om deze nieuwe benadering van profielen te steunen, gebruikt Experience Platform een hoogst gedenormaliseerd hybride gegevensmodel dat van het traditionele relationele gegevensmodel verschilt.

Dit document biedt standaardgebruiks- en tarieflimieten om u te helpen uw gegevens te modelleren voor optimale systeemprestaties. Bij het bekijken van de volgende instructies wordt aangenomen dat u de gegevens correct hebt gemodelleerd. Als u vragen hebt over het modelleren van uw gegevens, neemt u contact op met uw medewerker van de klantenservice.

>[!INFO]
>
>De meeste klanten overschrijden deze standaardgrenzen niet. Neem contact op met uw medewerker van de klantenservice als u meer wilt weten over aangepaste limieten.

## Limiettypen

Dit document bevat twee typen standaardlimieten:

* **Zachte limiet:** Het is mogelijk om verder te gaan dan een zachte limiet, maar zachte limieten bieden een aanbevolen richtlijn voor systeemprestaties.

* **Harde limiet:** Een harde grens verstrekt een absoluut maximum.

>[!INFO]
>
>De limieten die in dit document worden uiteengezet, worden voortdurend verbeterd. Kom regelmatig terug voor updates. Neem contact op met uw vertegenwoordiger van de klantenservice als u meer wilt weten over aangepaste limieten.

## Gegevensmodellimieten

De volgende instructies bieden aanbevolen limieten bij het modelleren van gegevens in realtime-klantprofiel. Zie de sectie over primaire entiteiten en dimensie-entiteiten voor meer informatie over primaire entiteiten en dimensie-entiteiten [entiteitstypen](#entity-types) in het aanhangsel.

### Primaire entiteitsinstructies

>[!NOTE]
>
>De limieten van het gegevensmodel die in deze sectie worden beschreven, vertegenwoordigen de wijzigingen die door Real-time Customer Data Platform B2B Edition worden ingeschakeld. Voor een volledige lijst met standaardlimieten voor Real-time CDP B2B Edition, combineert u deze limieten met de algemene Adobe Experience Platform-limieten die in de [handleidingen voor de gegevensdocumentatie van het Profiel van de Klant in real time](../profile/guardrails.md).

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| CDP B2B Edition-standaard XDM-klassegegevenssets in realtime | 60 | Zacht | Een maximum van 60 datasets die hefboomwerking de standaard klassen van de Gegevens van de Ervaring (XDM) door CDP B2B Uitgave in real time wordt verstrekt wordt geadviseerd. Voor een volledige lijst van standaardXDM klassen voor B2B gebruiksgevallen, verwijs naar [schema&#39;s in Real-time CDP B2B Edition-documentatie](schemas/b2b.md). <br/><br/>*Opmerking: Vanwege de aard van het gedenormaliseerde hybride gegevensmodel van Experience Platform overschrijden de meeste klanten deze limiet niet. Voor vragen over het modelleren van uw gegevens of als u meer wilt weten over aangepaste limieten, neemt u contact op met uw medewerker van de klantenservice.* |
| Verouderde relaties met meerdere entiteiten | 20 | Zacht | Er wordt aanbevolen maximaal 20 relaties tussen primaire entiteiten en dimensie-entiteiten te definiëren. Aanvullende relatietoewijzingen moeten pas worden gemaakt wanneer een bestaande relatie is verwijderd of uitgeschakeld. |
| Veel-op-één relaties per XDM-klasse | 2 | Zacht | Het wordt aanbevolen maximaal twee vele-op-één relaties te definiëren per XDM-klasse. Er dient geen aanvullende relatie te worden gelegd totdat een bestaande relatie is verwijderd of uitgeschakeld. Voor stappen op hoe te om een verhouding tussen twee schema&#39;s tot stand te brengen, verwijs naar het leerprogramma op [B2B-schemarelaties definiëren](../xdm/tutorials/relationship-b2b.md). |

### Dimension-entiteitsgeleidingen

>[!NOTE]
>
>De limieten van het gegevensmodel die in deze sectie worden beschreven, vertegenwoordigen de wijzigingen die door Real-time Customer Data Platform B2B Edition worden ingeschakeld. Voor een volledige lijst met standaardlimieten voor Real-time CDP B2B Edition, combineert u deze limieten met de algemene Adobe Experience Platform-limieten die in de [handleidingen voor de gegevensdocumentatie van het Profiel van de Klant in real time](../profile/guardrails.md).

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Geen geneste verouderde relaties | 0 | Zacht | U moet geen relatie maken tussen twee niet-[!DNL XDM Individual Profile] schema&#39;s. De capaciteit om verhoudingen tot stand te brengen wordt niet geadviseerd voor om het even welke schema&#39;s die geen deel van zijn [!DNL Profile] samenvoegingsschema. |
| Alleen B2B-objecten kunnen deelnemen aan een vele-op-één relatie | 0 | Hard | Het systeem ondersteunt alleen vele-op-één relaties tussen B2B-objecten. Raadpleeg de zelfstudie voor meer informatie over veel-op-één relaties [B2B-schemarelaties definiëren](../xdm/tutorials/relationship-b2b.md). |
| Maximale diepte van geneste relaties tussen B2B-objecten | 3 | Hard | De maximale diepte van geneste relaties tussen B2B-objecten is 3. Dit betekent dat in een hoogst genest schema, u geen verhouding tussen B2B voorwerpen zou moeten hebben die meer dan 3 niveaus diep worden genest. |

## Limieten voor gegevensgrootte

De volgende instructies verwijzen naar de gegevensgrootte en bieden aanbevolen limieten voor gegevens die kunnen worden ingevoerd, opgeslagen en opgevraagd, zoals bedoeld. Zie de sectie over primaire entiteiten en dimensie-entiteiten voor meer informatie over primaire entiteiten en dimensie-entiteiten [entiteitstypen](#entity-types) in het aanhangsel.

>[!INFO]
>
>De gegevensgrootte wordt gemeten als ongecomprimeerde gegevens in JSON op het moment van inname.

### Primaire entiteitsinstructies

>[!NOTE]
>
>De limieten voor gegevensgrootte die in deze sectie worden beschreven, vertegenwoordigen de wijzigingen die door Real-time Customer Data Platform B2B Edition worden ingeschakeld. Voor een volledige lijst met standaardlimieten voor Real-time CDP B2B Edition, combineert u deze limieten met de algemene Adobe Experience Platform-limieten die in de [handleidingen voor de gegevensdocumentatie van het Profiel van de Klant in real time](../profile/guardrails.md).

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Batches die per XDM-klasse per dag worden ingevoerd | 45 | Zacht | Het totale aantal batches dat elke dag per XDM-klasse wordt ingevoerd, mag niet groter zijn dan 45. Door extra batches in te zetten, kunnen optimale prestaties worden voorkomen. |

### Dimension-entiteitsgeleidingen

>[!NOTE]
>
>De limieten voor gegevensgrootte die in deze sectie worden beschreven, vertegenwoordigen de wijzigingen die door Real-time Customer Data Platform B2B Edition worden ingeschakeld. Voor een volledige lijst met standaardlimieten voor Real-time CDP B2B Edition, combineert u deze limieten met de algemene Adobe Experience Platform-limieten die in de [handleidingen voor de gegevensdocumentatie van het Profiel van de Klant in real time](../profile/guardrails.md).

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Totale grootte voor alle dimensionale entiteiten | 5 GB | Zacht | De aanbevolen totale grootte voor alle dimensionale entiteiten is 5 GB. Het inzetten van entiteiten met een grote dimensie kan van invloed zijn op de systeemprestaties. Het wordt bijvoorbeeld niet aanbevolen een productcatalogus van 10 GB als een dimensie-entiteit te laden. |
| Datasets per dimensionaal eenheidschema | 5 | Zacht | Het wordt aanbevolen maximaal vijf datasets toe te voegen aan elk dimensionaal eenheidschema. Bijvoorbeeld, als u een schema voor &quot;producten&quot;creeert en vijf bijdragende datasets toevoegt, zou u geen zesde dataset moeten creëren verbonden aan het productschema. |
| Per dag ingenomen partijen van Dimension-entiteit | 4 per entiteit | Zacht | Het aanbevolen maximumaantal per dag ingeslikte batches voor dimensieentiteiten is 4 per entiteit. U kunt bijvoorbeeld updates van een productcatalogus tot vier keer per dag invoeren. Het invoeren van extra dimensieentiteitsbatches voor dezelfde entiteit kan de systeemprestaties beïnvloeden. |

## Segmenteringsgeleiding

De instructies in deze sectie verwijzen naar het aantal en de aard van de segmenten die een organisatie binnen het Experience Platform kan maken, en naar het toewijzen en activeren van segmenten aan bestemmingen.

>[!NOTE]
>
>De segmentatielimieten die in deze sectie worden beschreven, vertegenwoordigen de wijzigingen die door Real-time Customer Data Platform B2B Edition worden ingeschakeld. Voor een volledige lijst met standaardlimieten voor Real-time CDP B2B Edition, combineert u deze limieten met de algemene Adobe Experience Platform-limieten die in de [handleidingen voor de gegevensdocumentatie van het Profiel van de Klant in real time](../profile/guardrails.md).

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Segmenten per B2B-sandbox | 400 | Zacht | Een organisatie kan in totaal meer dan 400 segmenten hebben, zolang er minder dan 400 segmenten in elke afzonderlijke B2B-sandbox zijn. Het maken van extra segmenten kan van invloed zijn op de systeemprestaties. |

## Volgende stappen

De limieten die in dit document worden beschreven, vertegenwoordigen de wijzigingen die door Real-time Customer Data Platform B2B Edition worden ingeschakeld. Voor een volledige lijst met standaardlimieten voor Real-time CDP B2B Edition, combineert u deze limieten met de algemene Adobe Experience Platform-limieten die in de [handleidingen voor de gegevensdocumentatie van het Profiel van de Klant in real time](../profile/guardrails.md).

## Aanhangsel

Deze sectie bevat aanvullende details voor de limieten in dit document.

### Typen entiteiten

De [!DNL Profile] opslaggegevensmodel bestaat uit twee kerneenheidstypen:

* **Primaire entiteit:** Een primaire entiteit, of profielentiteit, voegt gegevens samen om een &quot;enige bron van waarheid&quot;voor een individu te vormen. Deze verenigde gegevens worden vertegenwoordigd gebruikend wat als &quot;verenigingsmening&quot;wordt bekend is. Een verenigingsmening voegt de gebieden van alle schema&#39;s samen die de zelfde klasse in één enkel samenvoegingsschema uitvoeren. Het samenvoegingsschema voor [!DNL Real-time Customer Profile] is een gedenormaliseerd hybride gegevensmodel dat als container voor alle profielattributen en gedragsgebeurtenissen dienst doet.

   Tijdonafhankelijke kenmerken, ook bekend als &quot;recordgegevens&quot;, worden gemodelleerd met behulp van [!DNL XDM Individual Profile], terwijl tijdreeksgegevens, ook wel &quot;gebeurtenisgegevens&quot; genoemd, worden gemodelleerd met [!DNL XDM ExperienceEvent]. Als in Adobe Experience Platform record- en tijdreeksgegevens worden ingevoerd, wordt dit geactiveerd [!DNL Real-time Customer Profile] beginnen gegevens in te voeren die voor het gebruik ervan zijn ingeschakeld. Hoe meer interacties en details worden opgenomen, hoe robuuster de afzonderlijke profielen worden.

   ![](../profile/images/guardrails/profile-entity.png)

* **Dimension-entiteit:** Hoewel de profielgegevensopslag het handhaven van profielgegevens geen relationele opslag is, staat het Profiel integratie met kleine afmetingsentiteiten toe om segmenten op een vereenvoudigde en intuïtieve manier tot stand te brengen. Deze integratie wordt bekend als [segmentatie van meerdere entiteiten](../segmentation/multi-entity-segmentation.md). Uw organisatie kan ook klassen XDM bepalen om dingen buiten individuen, zoals opslag, producten, of eigenschappen te beschrijven. Deze[!DNL XDM Individual Profile] schema&#39;s worden &quot;dimensie-entiteiten&quot; genoemd en bevatten geen tijdreeksgegevens. Dimension-entiteiten bieden opzoekgegevens die de segmentatieprogramma&#39;s van meerdere entiteiten ondersteunen en vereenvoudigen. Deze moeten zo klein zijn dat de gehele gegevensset door de segmenteringsengine in het geheugen kan worden geladen voor optimale verwerking (snelle puntzoekopdracht).

   ![](../profile/images/guardrails/profile-and-dimension-entities.png)

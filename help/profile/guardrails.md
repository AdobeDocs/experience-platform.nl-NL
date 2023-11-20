---
title: Standaardhulplijnen voor realtime gegevens en segmentatie van klantprofiel
solution: Experience Platform
product: experience platform
type: Documentation
description: Leer over prestaties en systeem-gedwongen gidsen voor profielgegevens en segmentatie om een optimaal gebruik van de functionaliteit van Real-Time CDP te verzekeren.
exl-id: 33ff0db2-6a75-4097-a9c6-c8b7a9d8b78c
source-git-commit: 554763cc444da0d1459b22f3f37d22b528b290e1
workflow-type: tm+mt
source-wordcount: '2200'
ht-degree: 2%

---

# Standaardhulplijnen voor [!DNL Real-Time Customer Profile] gegevens en segmentatie

Met Adobe Experience Platform kunt u persoonlijke interkanaalervaringen bieden op basis van gedragsinzichten en klantkenmerken in de vorm van realtime klantprofielen. Om deze nieuwe benadering van profielen te steunen, gebruikt Experience Platform een hoogst gedenormaliseerd hybride gegevensmodel dat van het traditionele relationele gegevensmodel verschilt.

Dit document bevat standaard gebruiks- en snelheidslimieten om u te helpen uw profielgegevens te modelleren voor optimale systeemprestaties. Bij het bekijken van de volgende instructies wordt aangenomen dat u de gegevens correct hebt gemodelleerd. Als u vragen hebt over het modelleren van uw gegevens, neemt u contact op met uw medewerker van de klantenservice.

>[!NOTE]
>
>De meeste klanten overschrijden deze standaardgrenzen niet. Neem contact op met uw medewerker van de klantenservice als u meer wilt weten over aangepaste limieten.

## Aan de slag

De volgende services van het Experience Platform zijn betrokken bij het modelleren van realtime gegevens van het klantprofiel:

* [[!DNL Real-Time Customer Profile]](home.md): Maak geharmoniseerde consumentenprofielen met behulp van gegevens uit meerdere bronnen.
* [Identiteiten](../identity-service/home.md): Bridge-id&#39;s van verschillende gegevensbronnen worden opgenomen in Platform.
* [Schemas](../xdm/home.md): De schema&#39;s van het Model van Gegevens van de ervaring (XDM) zijn het gestandaardiseerde kader waardoor het Platform gegevens van de klantenervaring organiseert.
* [Soorten publiek](../segmentation/home.md): De segmenteringsengine in Platform wordt gebruikt om een publiek te maken op basis van uw klantgedragingen en -kenmerken.

## Limiettypen

Dit document bevat twee typen standaardlimieten:

| Het type Guardrail | Beschrijving |
|----------|---------|
| **Prestatiegarantie (Zachte limiet)** | Prestatiegaranties zijn gebruikslimieten die betrekking hebben op het bereik van uw gebruiksgevallen. Als u de prestatiegaranties overschrijdt, kan de prestaties achteruitgaan en de latentie vertragen. Adobe is niet verantwoordelijk voor een dergelijke verslechtering van de prestaties. Klanten die een prestatiegarantie consequent overschrijden, kunnen ervoor kiezen om extra capaciteit te licentiëren om prestatievermindering te voorkomen. |
| **Door het systeem afgedwongen geleiding (harde limiet)** | De door het systeem afgedwongen instructies worden afgedwongen door de gebruikersinterface of API van Real-Time CDP. Dit zijn grenzen die u niet kunt overschrijden aangezien UI en API u zal tegenhouden dit te doen of een fout zal terugkeren. |

{style="table-layout:auto"}

>[!NOTE]
>
>De limieten die in dit document worden uiteengezet, worden voortdurend verbeterd. Kom regelmatig terug voor updates. Als u meer wilt weten over aangepaste limieten, neemt u contact op met uw medewerker van de klantenservice.

## Gegevensmodellimieten

De volgende instructies bieden aanbevolen limieten bij het modelleren van gegevens in realtime-klantprofiel. Zie de sectie over primaire entiteiten en dimensie-entiteiten voor meer informatie over primaire entiteiten en dimensie-entiteiten [entiteitstypen](#entity-types) in het aanhangsel.

![Een diagram met de verschillende geleidingen voor profielgegevens in Adobe Experience Platform.](./images/guardrails/profile-guardrails.png)

### Primaire entiteitsinstructies

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Gegevenssets voor de klasse XDM Individueel profiel | 20 | Prestatiegerichting | Een maximum van 20 datasets die hefboomwerking de individuele klasse van het Profiel XDM wordt geadviseerd. |
| Gegevenssets voor de klasse XDM ExperienceEvent | 20 | Prestatiegerichting | Een maximum van 20 datasets die hefboomwerking de klasse XDM ExperienceEvent wordt geadviseerd. |
| Gegevenssets van Adobe Analytics-rapportsuite ingeschakeld voor profiel | 1 | Prestatiegerichting | Een maximum van één (1) dataset van de het rapportreeks van Analytics zou voor Profiel moeten worden toegelaten. Het proberen om veelvoudige datasets van de het rapportreeks van Analytics voor Profiel toe te laten kan onbedoelde gevolgen voor gegevenskwaliteit hebben. Zie de sectie over [Adobe Analytics-gegevenssets](#aa-datasets) in het aanhangsel. |
| Relaties met meerdere entiteiten | 5 | Prestatiegerichting | Er worden maximaal vijf relaties tussen primaire entiteiten en dimensie-entiteiten aanbevolen. Aanvullende relatietoewijzingen moeten pas worden gemaakt wanneer een bestaande relatie is verwijderd of uitgeschakeld. |
| JSON-diepte voor id-veld gebruikt in relatie met meerdere entiteiten | 4 | Prestatiegerichting | De aanbevolen maximale JSON-diepte voor een id-veld in relaties met meerdere entiteiten is 4. Dit betekent dat in een hoogst genest schema, gebieden die meer dan 4 niveaus diep worden genesteld niet als gebied van identiteitskaart in een verhouding zouden moeten worden gebruikt. |
| Arraycardinaliteit in een profielfragment | &lt;=500 | Prestatiegerichting | De optimale arraycardinaliteit in een profielfragment (tijdonafhankelijke gegevens) is &lt;=500. |
| Array-kardinaliteit in ExperienceEvent | &lt;=10 | Prestatiegerichting | De optimale arraycardinaliteit in een ExperienceEvent (tijdreeksgegevens) is &lt;=10. |
| Identiteitstelling voor individueel profiel Identiteitsgrafiek | 50 | Door het systeem afgedwongen geleiding | **Het maximumaantal identiteiten in een identiteitsgrafiek voor een individueel profiel is 50.** Profielen met meer dan 50 identiteiten worden uitgesloten van segmentatie, export en lookups. |

{style="table-layout:auto"}

### Garanties voor entiteiten van Dimension

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Geen gegevens uit tijdreeksen toegestaan voor niet-[!DNL XDM Individual Profile] entiteiten | 0 | Door het systeem afgedwongen geleiding | **Gegevens uit tijdreeksen zijn niet toegestaan voor niet-tijdreeksen[!DNL XDM Individual Profile] entiteiten in de profielservice.** Als een reeks gegevensreeksen met een niet-reeks wordt geassocieerd[!DNL XDM Individual Profile] ID, de dataset zou niet moeten worden toegelaten voor [!DNL Profile]. |
| Geen geneste relaties | 0 | Prestatiegerichting | U moet geen relatie maken tussen twee niet-[!DNL XDM Individual Profile] schema&#39;s. De mogelijkheid om relaties te maken wordt niet aanbevolen voor schema&#39;s die geen deel uitmaken van de [!DNL Profile] samenvoegingsschema. |
| JSON-diepte voor veld primaire id | 4 | Prestatiegerichting | De aanbevolen maximale JSON-diepte voor het veld primaire id is 4. Dit betekent dat in een hoogst genest schema, u geen gebied als primaire identiteitskaart zou moeten selecteren als het meer dan 4 niveaus diep wordt genesteld. Een veld op het vierde geneste niveau kan als primaire id worden gebruikt. |

{style="table-layout:auto"}

## Limieten voor gegevensgrootte

De volgende instructies verwijzen naar de gegevensgrootte en bieden aanbevolen limieten voor gegevens die kunnen worden ingevoerd, opgeslagen en opgevraagd, zoals bedoeld. Zie de sectie over primaire entiteiten en dimensie-entiteiten voor meer informatie over primaire entiteiten en dimensie-entiteiten [entiteitstypen](#entity-types) in het aanhangsel.

>[!NOTE]
>
>De gegevensgrootte wordt gemeten als ongecomprimeerde gegevens in JSON op het moment van inname.

### Primaire entiteitsinstructies

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Maximale grootte van ExperienceEvent | 10KB | Door het systeem afgedwongen geleiding | **De maximale grootte van een gebeurtenis is 10 kB.** De inname gaat door, maar alle gebeurtenissen die groter zijn dan 10 kB gaan verloren. |
| Maximale recordgrootte profiel | 100KB | Door het systeem afgedwongen geleiding | **De maximale grootte van een profielrecord is 100 kB.** De inname gaat door, maar profielrecords die groter zijn dan 100 kB worden verwijderd. |
| Maximale framegrootte profiel | 50MB | Door het systeem afgedwongen geleiding | **De maximale grootte van één profielfragment is 50 MB.** De segmentatie, de uitvoer, en de raadplegingen kunnen voor om het even welke ontbreken [profielfragment](#profile-fragments) dat groter is dan 50 MB. |
| Maximale grootte voor profielopslag | 50MB | Prestatiegerichting | **De maximale grootte van een opgeslagen profiel is 50 MB.** Nieuw toevoegen [profielfragmenten](#profile-fragments) in een profiel dat groter is dan 50 MB, de systeemprestaties beïnvloeden. Een profiel kan bijvoorbeeld één fragment bevatten dat 50 MB is of meerdere fragmenten kan bevatten voor meerdere datasets met een gecombineerde totale grootte van 50 MB. Het opslaan van een profiel met één fragment dat groter is dan 50 MB of meerdere fragmenten die samen meer dan 50 MB groot zijn, heeft invloed op de systeemprestaties. |
| Aantal per dag ingenomen Profile- of ExperienceEvent-batches | 90 | Prestatiegerichting | **Het maximumaantal per dag ingenomen Profile of ExperienceEvent-batches is 90.** Dit houdt in dat het gecombineerde totaal van de elke dag ingeslikte Profile en ExperienceEvent batches niet meer dan 90 mag bedragen. Door extra batches in te voeren worden de systeemprestaties beïnvloed. |
| Aantal ExperienceEvents per profielrecord | 5000 | Prestatiegerichting | **Het maximumaantal ExperienceEvents per profielrecord is 5000.** Profielen met meer dan 5000 ervaringGebeurtenissen zullen **niet** voor segmentatie in aanmerking worden genomen. |

{style="table-layout:auto"}

### Garanties voor entiteiten van Dimension

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Totale grootte voor alle dimensionale entiteiten | 5GB | Prestatiegerichting | De aanbevolen totale grootte voor alle dimensionale entiteiten is 5 GB. Het inzetten van entiteiten met een grote dimensie kan van invloed zijn op de systeemprestaties. Het wordt bijvoorbeeld niet aanbevolen een productcatalogus van 10 GB als een dimensie-entiteit te laden. |
| Datasets per dimensionaal eenheidschema | 5 | Prestatiegerichting | Het wordt aanbevolen maximaal vijf datasets toe te voegen aan elk dimensionaal eenheidschema. Bijvoorbeeld, als u een schema voor &quot;producten&quot;creeert en vijf bijdragende datasets toevoegt, zou u geen zesde dataset moeten creëren verbonden aan het productschema. |
| Per dag ingenomen partijen van een Dimension-entiteit | 4 per entiteit | Prestatiegerichting | Het aanbevolen maximumaantal per dag ingeslikte batches voor dimensieentiteiten is 4 per entiteit. U kunt bijvoorbeeld updates van een productcatalogus tot vier keer per dag invoeren. Het invoeren van extra dimensieentiteitsbatches voor dezelfde entiteit kan de systeemprestaties beïnvloeden. |

{style="table-layout:auto"}

## Segmenteringsgeleiding {#segmentation-guardrails}

De instructies in deze sectie hebben betrekking op het aantal en de aard van de soorten publiek die een organisatie binnen Experience Platform kan maken, alsmede op het in kaart brengen en activeren van het publiek naar bestemmingen.

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Soorten publiek per sandbox | 4000 | Prestatiegerichting | Een organisatie kan in totaal meer dan 4000 soorten publiek hebben, zolang er in elke sandbox minder dan 4000 soorten publiek aanwezig zijn. Pogingen om extra publiek te creëren kunnen systeemprestaties beïnvloeden. Meer informatie over [publiek maken](/help/segmentation/ui/segment-builder.md) door de segmentbouwer. |
| Publiek randen per sandbox | 150 | Prestatiegerichting | Een organisatie kan in totaal meer dan 150 randsoorten publiek hebben, zolang er in elke afzonderlijke sandbox minder dan 150 randsoorten publiek zijn. Poging om extra randpubliek te maken kan van invloed zijn op de systeemprestaties. Meer informatie over [randpubliek](/help/segmentation/ui/edge-segmentation.md). |
| Streaming publiek per sandbox | 500 | Prestatiegerichting | Een organisatie kan in totaal meer dan 500 streamingdeelnemers hebben, zolang er in elke sandbox minder dan 500 streamingdeelnemers zijn. Het maken van extra streaming publiek kan van invloed zijn op de systeemprestaties. Meer informatie over [streaming publiek](/help/segmentation/ui/streaming-segmentation.md). |
| Batchpubliek per sandbox | 4000 | Prestatiegerichting | Een organisatie kan in totaal meer dan 4000 batchdoelgroepen hebben, zolang er in elke sandbox minder dan 4000 doelgroepen aanwezig zijn. Het maken van extra batchdoelgroepen kan van invloed zijn op de systeemprestaties. |
| Accountsoorten per sandbox | 50 | Door het systeem afgedwongen geleiding | U kunt niet meer dan 50 accountsoorten maken in een sandbox. Nadat u 50 publiek in een zandbak bereikt, **[!UICONTROL Create audience]** besturingselement is uitgeschakeld wanneer u een nieuw publiek voor een account probeert te maken. Meer informatie over [accountpubliek](/help/segmentation/ui/account-audiences.md). |

{style="table-layout:auto"}

## Bijlage

Deze sectie bevat aanvullende details voor de limieten in dit document.

### Typen entiteiten

De [!DNL Profile] opslaggegevensmodel bestaat uit twee kerneenheidstypen: [primaire entiteiten](#primary-entity) en [dimensie-entiteiten](#dimension-entity).

#### Primaire entiteit

Een primaire entiteit, of profielentiteit, voegt gegevens samen om een &quot;enige bron van waarheid&quot;voor een individu te vormen. Deze verenigde gegevens worden vertegenwoordigd gebruikend wat als &quot;verenigingsmening&quot;wordt bekend is. Een verenigingsmening voegt de gebieden van alle schema&#39;s samen die de zelfde klasse in één enkel samenvoegingsschema uitvoeren. Het samenvoegingsschema voor [!DNL Real-Time Customer Profile] is een gedenormaliseerd hybride gegevensmodel dat als container voor alle profielattributen en gedragsgebeurtenissen dienst doet.

Tijdonafhankelijke kenmerken, ook bekend als &quot;recordgegevens&quot;, worden gemodelleerd met behulp van [!DNL XDM Individual Profile], terwijl tijdreeksgegevens, ook wel &quot;gebeurtenisgegevens&quot; genoemd, worden gemodelleerd met [!DNL XDM ExperienceEvent]. Als in Adobe Experience Platform record- en tijdreeksgegevens worden ingevoerd, wordt dit geactiveerd [!DNL Real-Time Customer Profile] beginnen gegevens in te voeren die voor het gebruik ervan zijn ingeschakeld. Hoe meer interacties en details worden opgenomen, hoe robuuster de afzonderlijke profielen worden.

![Een infografisch waarin de verschillen tussen recordgegevens en tijdreeksgegevens worden beschreven.](images/guardrails/profile-entity.png)

#### Dimension-entiteit

Hoewel de profielgegevensopslag het handhaven van profielgegevens geen relationele opslag is, staat het Profiel integratie met kleine afmetingsentiteiten toe om publiek op een vereenvoudigde en intuïtieve manier tot stand te brengen. Deze integratie wordt bekend als [segmentatie van meerdere entiteiten](../segmentation/multi-entity-segmentation.md).

Uw organisatie kan ook klassen XDM bepalen om dingen buiten individuen, zoals opslag, producten, of eigenschappen te beschrijven. Deze[!DNL XDM Individual Profile] schema&#39;s worden &quot;dimensie-entiteiten&quot;genoemd (ook genoemd geworden &quot;raadplegingsentiteiten&quot;) en bevatten geen tijd-reeksgegevens. Schema&#39;s die dimensie-entiteiten vertegenwoordigen, zijn via het gebruik van [schema-relaties](../xdm/tutorials/relationship-ui.md).

De entiteiten van het Dimension verstrekken raadplegingsgegevens die helpen en multi-entiteitsegmentdefinities vereenvoudigen en moeten zo klein zijn dat de segmenteringsmotor de volledige gegevensreeks in geheugen voor optimale verwerking (snelle puntraadpleging) kan laden.

![An infographic that shows that a profile entity is eruit of dimensie entities.](images/guardrails/profile-and-dimension-entities.png)

### Profielfragmenten

In dit document zijn er verschillende hulplijnen die naar &quot;profielfragmenten&quot; verwijzen. In Experience Platform worden meerdere profielfragmenten samengevoegd tot het realtime klantprofiel. Elk fragment vertegenwoordigt een unieke primaire identiteit en de corresponderende record of volledige set gebeurtenisgegevens voor die id binnen een bepaalde gegevensset. Raadpleeg voor meer informatie over profielfragmenten de [Profieloverzicht](home.md#profile-fragments-vs-merged-profiles).

### Beleid samenvoegen {#merge-policies}

Wanneer het samenbrengen van gegevens uit veelvoudige bronnen, is het fusiebeleid de regels die het Platform gebruikt om te bepalen hoe de gegevens aan voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om die verenigde mening tot stand te brengen. Bijvoorbeeld, als een klant met uw merk over verscheidene kanalen in wisselwerking staat, zal uw organisatie veelvoudige profielfragmenten met betrekking tot die enige klant hebben die in veelvoudige datasets verschijnen. Wanneer deze fragmenten in Platform worden opgenomen, worden ze samengevoegd om één profiel voor die klant te maken. Wanneer de gegevens uit meerdere bronnen conflicteren, bepaalt het samenvoegbeleid welke informatie moet worden opgenomen in het profiel voor de persoon. Een maximum van vijf (5) samenvoegbeleid wordt toegestaan per organisatie. Voor meer informatie over samenvoegingsbeleid leest u de [overzicht van samenvoegbeleid](merge-policies/overview.md).

### Gegevenssets van de Adobe Analytics-rapportsuite in Platform {#aa-datasets}

De veelvoudige rapportsuites kunnen voor Profiel worden toegelaten zolang alle gegevensconflicten worden opgelost. U kunt de functie Gegevensvoorbeeld gebruiken om gegevensconflicten op te lossen over eVars, Lijsten, en Props. Lees voor meer informatie over het gebruik van de functie Data Prep de [UI-hulplijn Adobe Analytics-connector](../sources/tutorials/ui/create/adobe-applications/analytics.md).

## Volgende stappen

Raadpleeg de volgende documentatie voor meer informatie over andere Experience Platforms services guardrails, over end-to-end latentie-informatie en licentiegegevens uit Real-Time CDP Product Description-documenten:

* [Real-Time CDP guardrails](/help/rtcdp/guardrails/overview.md)
* [Diagrammen met latentie van begin tot eind](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) voor verschillende diensten van de Experience Platform.
* [Real-time Customer Data Platform (B2C Edition - Premiere en Ultimate Packages)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2P - Premiere en Ultimate Packages)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2B - Premiere en Ultimate Packages)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)

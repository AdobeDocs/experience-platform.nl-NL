---
title: Standaardhulplijnen voor realtime gegevens en segmentatie van klantprofiel
solution: Experience Platform
product: experience platform
type: Documentation
description: Leer over prestaties en door systemen afgedwongen richtlijnen voor profielgegevens en segmentatie. Zo zorgt u voor optimaal gebruik van de functie Real-Time CDP.
exl-id: 33ff0db2-6a75-4097-a9c6-c8b7a9d8b78c
source-git-commit: 56bf7ae20c33b013a1710fba8c04d9edc23baf89
workflow-type: tm+mt
source-wordcount: '2647'
ht-degree: 1%

---

# Standaardgeleiding voor gegevens en segmentatie van [!DNL Real-Time Customer Profile]

Met Adobe Experience Platform kunt u persoonlijke interkanaalervaringen bieden op basis van gedragsinzichten en klantkenmerken in de vorm van realtime klantprofielen. Om deze nieuwe benadering van profielen te steunen, gebruikt Experience Platform een hoogst gedenormaliseerd hybride gegevensmodel dat van het traditionele relationele gegevensmodel verschilt.

>[!IMPORTANT]
>
>Controleer uw vergunningsrechten in uw Orde van de Verkoop en de overeenkomstige [ Beschrijving van het Product ](https://helpx.adobe.com/nl/legal/product-descriptions.html) op daadwerkelijke gebruiksgrenzen naast deze guardrails pagina.

Dit document biedt standaardgebruiks- en tarieflimieten om u te helpen uw profielgegevens te modelleren voor optimale systeemprestaties. Bij het bekijken van de volgende instructies wordt aangenomen dat u de gegevens correct hebt gemodelleerd. Als u vragen hebt over het modelleren van uw gegevens, neemt u contact op met uw medewerker van de klantenservice.

>[!NOTE]
>
>De meeste klanten overschrijden deze standaardgrenzen niet. Neem contact op met uw medewerker van de klantenservice als u meer wilt weten over aangepaste limieten.

## Aan de slag

De volgende Experience Platform-services zijn betrokken bij het modelleren van realtime-klantprofielgegevens:

* [[!DNL Real-Time Customer Profile]](home.md): Maak uniforme consumentenprofielen met behulp van gegevens uit meerdere bronnen.
* [ Identiteiten ](../identity-service/home.md): De identiteiten van Bridge van verschillende gegevensbronnen aangezien zij in Experience Platform worden opgenomen.
* [ Schema&#39;s ](../xdm/home.md): De schema&#39;s van de Gegevens van de ervaring van het Model (XDM) zijn het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
* [ Soorten publiek ](../segmentation/home.md): De segmenteringsmotor binnen Experience Platform wordt gebruikt om publiek van uw klantenprofielen tot stand te brengen die op klantengedrag en attributen worden gebaseerd.

## Limiettypen

Dit document bevat twee typen standaardlimieten:

| Het type Guardrail | Beschrijving |
| -------------- | ----------- |
| **Gegarandeerde van Prestaties (Zachte grens)** | Prestatiegaranties zijn gebruikslimieten die betrekking hebben op het bereik van uw gebruiksgevallen. Als u de prestatiegaranties overschrijdt, kan de prestaties achteruitgaan en de latentie vertragen. Adobe is niet verantwoordelijk voor deze verslechtering van de prestaties. Klanten die een prestatiegarantie consequent overschrijden, kunnen ervoor kiezen om extra capaciteit te licentiëren om prestatievermindering te voorkomen. |
| **systeem-afgedwongen grails (Harde grens)** | De door het systeem afgedwongen instructies worden afgedwongen door de gebruikersinterface of API van Real-Time CDP. Dit zijn grenzen die u niet kunt overschrijden aangezien UI en API u zal tegenhouden dit te doen of een fout zal terugkeren. |

{style="table-layout:auto"}

>[!NOTE]
>
>De limieten die in dit document worden uiteengezet, worden voortdurend verbeterd. Kom regelmatig terug voor updates. Als u meer wilt weten over aangepaste limieten, neemt u contact op met uw medewerker van de klantenservice.

## Gegevensmodellimieten

De volgende instructies bieden aanbevolen limieten bij het modelleren van gegevens in realtime-klantprofiel. Meer over primaire entiteiten en afmetingsentiteiten leren, zie de sectie over [ entiteittypes ](#entity-types) in de Bijlage.

![ een diagram dat de verschillende gidsen voor de gegevens van het Profiel in Adobe Experience Platform toont.](./images/guardrails/profile-guardrails.png)

### Primaire entiteitsinstructies

| Guardrail | Limiet | Limiettype | Beschrijving |
| --------- | ----- | ---------- | ----------- |
| Gegevenssets voor de klasse XDM Individueel profiel | 20 | Prestatiegerichting | Een maximum van 20 datasets die hefboomwerking de individuele klasse van het Profiel XDM wordt geadviseerd. |
| Gegevenssets voor de klasse XDM ExperienceEvent | 20 | Prestatiegerichting | Een maximum van 20 datasets die hefboomwerking de klasse XDM ExperienceEvent wordt geadviseerd. |
| Gegevenssets van Adobe Analytics-rapportsuite ingeschakeld voor profiel | 1 | Prestatiegerichting | Een maximum van één (1) dataset van de het rapportreeks van Analytics zou voor Profiel moeten worden toegelaten. Het proberen om veelvoudige datasets van de het rapportreeks van Analytics voor Profiel toe te laten kan onbedoelde gevolgen voor gegevenskwaliteit hebben. Voor meer informatie, zie de sectie over [ datasets van Adobe Analytics ](#aa-datasets) in de Bijlage. |
| Relaties met meerdere entiteiten | 5 | Prestatiegerichting | Er worden maximaal vijf relaties tussen primaire entiteiten en dimensie-entiteiten aanbevolen. Aanvullende relatietoewijzingen moeten pas worden gemaakt wanneer een bestaande relatie is verwijderd of uitgeschakeld. |
| JSON-diepte voor id-veld gebruikt in relatie met meerdere entiteiten | 4 | Prestatiegerichting | De aanbevolen maximale JSON-diepte voor een id-veld in relaties met meerdere entiteiten is 4. Dit betekent dat in een hoogst genest schema, gebieden die meer dan 4 niveaus diep worden genesteld niet als gebied van identiteitskaart in een verhouding zouden moeten worden gebruikt. |
| Arraycardinaliteit in een profielfragment | &lt;=500 | Prestatiegerichting | De optimale arraycardinaliteit in een profielfragment (tijdonafhankelijke gegevens) is &lt;=500. |
| Array-kardinaliteit in ExperienceEvent | &lt;=10 | Prestatiegerichting | De optimale arraycardinaliteit in een ExperienceEvent (tijdreeksgegevens) is &lt;=10. |
| Identiteitstelling voor individueel profiel Identiteitsgrafiek | 50 | Door het systeem afgedwongen geleiding | **het maximumaantal identiteiten in een Grafiek van de Identiteit voor een individueel profiel is 50.** Profielen met meer dan 50 identiteiten zijn uitgesloten van segmentatie, export en zoekopdrachten. Voor meer informatie, lees de gids over [ het begrip logica van de identiteitsschrapping ](../identity-service/guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated). |

{style="table-layout:auto"}

### Garanties van Dimension-entiteiten

| Guardrail | Limiet | Limiettype | Beschrijving |
| --------- | ----- | ---------- | ----------- |
| Geen gegevens uit tijdreeksen toegestaan voor niet- [!DNL XDM Individual Profile] entiteiten | 0 | Door het systeem afgedwongen geleiding | **tijd-reeksen gegevens worden niet toegelaten voor niet [!DNL XDM Individual Profile] entiteiten in de Dienst van het Profiel.** Als een reeks dataset met een niet - [!DNL XDM Individual Profile] identiteitskaart wordt geassocieerd, zou de dataset niet voor [!DNL Profile] moeten worden toegelaten. |
| Geen geneste relaties | 0 | Prestatiegerichting | U zou geen verband tussen twee niet [!DNL XDM Individual Profile] schema&#39;s moeten tot stand brengen. De mogelijkheid om relaties te maken wordt niet aanbevolen voor schema&#39;s die geen deel uitmaken van het samenvoegingsschema van [!DNL Profile] . |
| JSON-diepte voor veld primaire id | 4 | Prestatiegerichting | De aanbevolen maximale JSON-diepte voor het veld primaire id is 4. Dit betekent dat in een hoogst genest schema, u geen gebied als primaire identiteitskaart zou moeten selecteren als het meer dan 4 niveaus diep wordt genesteld. Een veld op het vierde geneste niveau kan als primaire id worden gebruikt. |

{style="table-layout:auto"}

## Limieten voor gegevensgrootte

De volgende instructies verwijzen naar de gegevensgrootte en bieden aanbevolen limieten voor gegevens die kunnen worden ingevoerd, opgeslagen en opgevraagd, zoals bedoeld. Meer over primaire entiteiten en afmetingsentiteiten leren, zie de sectie over [ entiteittypes ](#entity-types) in de Bijlage.

>[!NOTE]
>
>De gegevensgrootte wordt gemeten als ongecomprimeerde gegevens in JSON op het moment van inname.

### Primaire entiteitsinstructies

| Guardrail | Limiet | Limiettype | Beschrijving |
| --------- | ----- | ---------- | ----------- |
| Maximale grootte van ExperienceEvent | 10 KB | Door het systeem afgedwongen geleiding | **de maximumgrootte van een gebeurtenis is 10KB.** De inname gaat door, maar gebeurtenissen die groter zijn dan 10 kB worden verwijderd. |
| Maximale recordgrootte profiel | 100 kB | Door het systeem afgedwongen geleiding | **de maximumgrootte van een profielverslag is 100KB.** De inname gaat door, maar profielrecords die groter zijn dan 100 kB worden verwijderd. |
| Maximale framegrootte profiel | 50 MB | Door het systeem afgedwongen geleiding | **de maximumgrootte van één enkel profielfragment is 50MB.** de segmentatie, de uitvoer, en de raadplegingen kunnen voor om het even welk [ profielfragment ](#profile-fragments) ontbreken dat groter is dan 50MB. |
| Maximale grootte voor profielopslag | 50 MB | Prestatiegerichting | **de maximumgrootte van een opgeslagen profiel is 50MB.** Toevoegend nieuwe [ profielfragmenten ](#profile-fragments) in een profiel dat groter is dan 50MB zal systeemprestaties beïnvloeden. Een profiel kan bijvoorbeeld één fragment bevatten dat 50 MB is of meerdere fragmenten kan bevatten voor meerdere datasets met een gecombineerde totale grootte van 50 MB. Het opslaan van een profiel met één fragment dat groter is dan 50 MB of meerdere fragmenten die samen meer dan 50 MB groot zijn, heeft invloed op de systeemprestaties. |
| Aantal per dag ingenomen Profile- of ExperienceEvent-batches | 90 | Prestatiegerichting | **het maximumaantal per dag ingebedde partijen van het Profiel of van de ExperienceEvent is 90.** Dit betekent dat het gecombineerde totaal van de elke dag ingeslikte profielen Profile en ExperienceEvent niet meer dan 90 mag zijn. Door extra batches in te voeren worden de systeemprestaties beïnvloed. |
| Aantal ExperienceEvents per profielrecord | 5000 | Prestatiegerichting | **het maximumaantal ExperienceEvents per profielverslag is 5000.** Profielen met meer dan 5000 ExperienceEvents zullen slechts **recentste** 5000 ExperienceEvents wanneer gebruikt met segmentatie gebruiken. |

{style="table-layout:auto"}

### Garanties van Dimension-entiteiten

| Guardrail | Limiet | Limiettype | Beschrijving |
| --------- | ----- | ---------- | ----------- |
| Totale grootte voor alle dimensionale entiteiten | 5 GB | Prestatiegerichting | De aanbevolen totale grootte voor alle dimensionale entiteiten is 5 GB. Het inzetten van entiteiten met een grote dimensie kan van invloed zijn op de systeemprestaties. Het wordt bijvoorbeeld niet aanbevolen een productcatalogus van 10 GB als een dimensie-entiteit te laden. |
| Datasets per dimensionaal eenheidschema | 5 | Prestatiegerichting | Het wordt aanbevolen maximaal vijf datasets toe te voegen aan elk dimensionaal eenheidschema. Bijvoorbeeld, als u een schema voor &quot;producten&quot;creeert en vijf bijdragende datasets toevoegt, zou u geen zesde dataset moeten creëren verbonden aan het productschema. |
| Per dag ingenomen partijen van Dimension-entiteit | 4 per entiteit | Prestatiegerichting | Het aanbevolen maximumaantal per dag ingeslikte batches voor dimensieentiteiten is 4 per entiteit. U kunt bijvoorbeeld updates van een productcatalogus tot vier keer per dag invoeren. Het invoeren van extra dimensieentiteitsbatches voor dezelfde entiteit kan de systeemprestaties beïnvloeden. |

{style="table-layout:auto"}

## Segmenteringsgeleiding {#segmentation-guardrails}

De instructies in deze sectie hebben betrekking op het aantal en de aard van de soorten publiek die een organisatie binnen Experience Platform kan maken, alsmede op het in kaart brengen en activeren van het publiek naar bestemmingen.

| Guardrail | Limiet | Limiettype | Beschrijving |
| --------- | ----- | ---------- | ----------- |
| Soorten publiek per sandbox | 4000 | Prestatiegerichting | U kunt tot 4000 **actieve** publiek per zandbak hebben. U kunt meer dan 4000 soorten publiek per organisatie hebben, zolang er minder dan 4000 soorten publiek in elke **individuele** zandbak zijn. Dit is inclusief publiek in batch, streaming en edge. Pogingen om extra publiek te creëren kunnen systeemprestaties beïnvloeden. Lees meer over [ creërend publiek ](/help/segmentation/ui/segment-builder.md) door de segmentbouwer. |
| Edge-publiek per sandbox | 150 | Prestatiegerichting | U kunt tot 150 **actieve** randpubliek per zandbak hebben. U kunt meer dan 150 randpubliek per organisatie hebben, zolang er minder dan 150 randpubliek in elke **individuele** zandbak zijn. Poging om extra randpubliek te maken kan van invloed zijn op de systeemprestaties. Lees meer over [ randpubliek ](/help/segmentation/methods/edge-segmentation.md). |
| Edge-doorvoer door alle sandboxen | 1500 RPS | Prestatiegerichting | De segmentatie van Edge steunt een gecombineerde piekwaarde van 1500 binnenkomende gebeurtenissen per seconde die Adobe Experience Platform Edge Network over uw productie en ontwikkelingszandbakken ingaan. Edge-segmentatie kan tot 350 milliseconden duren om een binnenkomende gebeurtenis te verwerken nadat deze de Adobe Experience Platform Edge Network is binnengekomen. Lees meer over [ randpubliek ](/help/segmentation/methods/edge-segmentation.md). |
| Streaming publiek per sandbox | 500 | Prestatiegerichting | U kunt tot 500 **actieve** het stromen publiek per zandbak hebben. U kunt meer dan 500 het stromen publiek per organisatie hebben, zolang er minder dan 500 het stromen publiek in elke **individuele** zandbak zijn. Dit geldt zowel voor streaming als voor randpubliek. Het maken van extra streaming publiek kan van invloed zijn op de systeemprestaties. Lees meer over [ het stromen publiek ](/help/segmentation/methods/streaming-segmentation.md). |
| Doorvoer streamen voor alle sandboxen | 1500 RPS | Prestatiegerichting | Streaming segmentatie ondersteunt een gecombineerde piekwaarde van 1500 inkomende gebeurtenissen per seconde voor uw productie- en ontwikkelingssandboxen. Het kan tot 5 minuten duren voordat streamingsegmentatie in aanmerking komt voor een profiel voor segmentlidmaatschap. Lees meer over [ het stromen publiek ](/help/segmentation/methods/streaming-segmentation.md). |
| Batchpubliek per sandbox | 4000 | Prestatiegerichting | U kunt tot 4000 **actieve** partijpubliek per zandbak hebben. U kunt meer dan 4000 partijpubliek per organisatie hebben, zolang er minder dan 4000 partijpubliek in elke **individuele** zandbak zijn. Het maken van extra batchdoelgroepen kan van invloed zijn op de systeemprestaties. |
| Accountsoorten per sandbox | 50 | Door het systeem afgedwongen geleiding | U kunt maximaal 50 accountsoorten gebruiken in een sandbox. Wanneer u 50 soorten publiek bereikt in een sandbox, wordt het besturingselement **[!UICONTROL Create audience]** uitgeschakeld wanneer u een nieuw publiek voor een account probeert te maken. Lees meer over [ rekeningspubliek ](/help/segmentation/types/account-audiences.md). |
| Gepubliceerde composities per sandbox | 10 | Prestatiegerichting | U kunt maximaal 10 gepubliceerde composities in een sandbox hebben. Lees meer over [ publiekssamenstelling in de gids UI ](/help/segmentation/ui/audience-composition.md). **Nota**: De samenstellingen die met de Federatieve Samenstelling van het Publiek worden gecreeerd worden **niet** geteld met deze guardrail. |
| Maximale doelgrootte | 30% | Prestatiegerichting | Het geadviseerde maximum lidmaatschap van een publiek is 30 percent van het totale aantal profielen in het systeem. Het is mogelijk een publiek te maken met meer dan 30% van de profielen als leden of met meerdere grote doelgroepen, maar dit heeft gevolgen voor de systeemprestaties. |
| Flexibele evaluatietests voor het publiek | 50 per jaar (productie zandbak) <br/> 100 per jaar (ontwikkelingszandbak) | Door het systeem afgedwongen geleiding | U hebt een maximum van 50 flexibele de looppas van de publieksevaluatie per jaar per **productie** zandbak. U hebt een maximum van 100 flexibele de looppas van de publieksevaluatie per jaar per **zandbak van de ontwikkelings**. |
| Flexibele evaluatietests voor het publiek | 2 per dag | Door het systeem afgedwongen geleiding | U hebt maximaal 2 regels per dag per sandbox. |
| Soorten publiek per flexibele evaluatieronde voor publiek | 20 | Door het systeem afgedwongen geleiding | U kunt maximaal 20 publiek per flexibele uitvoering van de publieksevaluatie hebben. |

{style="table-layout:auto"}

## Verwachte beschikbaarheid

De volgende sectie schetst de **verwachte** beschikbaarheid voor publiek en voegt beleid in stroomafwaartse diensten zoals de bestemmingen van Real-Time CDP samen:

| Het type Sandbox | Tijd |
| ------------ | ---- |
| Bestaande sandboxen | 1 uur |
| Nieuwe sandboxen | 2 uur |
| Nieuwe sandboxen opnieuw instellen | 2 uur |

{style="table-layout:auto"}

## Bijlage

Deze sectie bevat aanvullende details voor de limieten in dit document.

### Typen entiteiten

Het [!DNL Profile] model van opslaggegevens bestaat uit twee types van kernentiteit: [ primaire entiteiten ](#primary-entity) en [ afmetingsentiteiten ](#dimension-entity).

#### Primaire entiteit

Een primaire entiteit, of profielentiteit, voegt gegevens samen om een &quot;enige bron van waarheid&quot;voor een individu te vormen. Deze verenigde gegevens worden vertegenwoordigd gebruikend wat als &quot;verenigingsmening&quot;wordt bekend is. Een verenigingsmening voegt de gebieden van alle schema&#39;s samen die de zelfde klasse in één enkel samenvoegingsschema uitvoeren. Het samenvoegingsschema voor [!DNL Real-Time Customer Profile] is een gedenormaliseerd hybride gegevensmodel dat als container voor alle profielattributen en gedragsgebeurtenissen dienst doet.

Tijdonafhankelijke kenmerken, ook wel &#39;recordgegevens&#39; genoemd, worden gemodelleerd met [!DNL XDM Individual Profile] , terwijl tijdreeksgegevens, ook wel &#39;gebeurtenisgegevens&#39; genoemd, worden gemodelleerd met [!DNL XDM ExperienceEvent] . Wanneer in Adobe Experience Platform record- en tijdreeksgegevens worden opgenomen, wordt [!DNL Real-Time Customer Profile] geactiveerd om te beginnen met het opnemen van gegevens die voor het gebruik ervan zijn ingeschakeld. Hoe meer interacties en details worden opgenomen, hoe robuuster de afzonderlijke profielen worden.

![ Infographic die de verschillen tussen verslaggegevens en tijd-reeksen gegevens schetsen.](images/guardrails/profile-entity.png)

#### Dimension

Hoewel de profielgegevensopslag het handhaven van profielgegevens geen relationele opslag is, staat het Profiel integratie met kleine afmetingsentiteiten toe om publiek op een vereenvoudigde en intuïtieve manier tot stand te brengen. Deze integratie is gekend als [ multi-entiteitsegmentatie ](../segmentation/tutorials/multi-entity-segmentation.md).

Uw organisatie kan ook klassen XDM bepalen om dingen buiten individuen, zoals opslag, producten, of eigenschappen te beschrijven. Deze schema&#39;s, die gebruikend klassen XDM buiten de individuele klasse van het Profiel XDM worden gemodelleerd, worden genoemd &quot;afmetingsentiteiten&quot;(die ook als &quot;raadplegingsentiteiten&quot;worden bekend) en bevatten geen tijd-reeksgegevens. De schema&#39;s die afmetingsentiteiten vertegenwoordigen zijn verbonden met profielentiteiten door het gebruik van [ schemaverhoudingen ](../xdm/tutorials/relationship-ui.md).

Dimension-entiteiten bieden opzoekgegevens die de definities van segmenten met meerdere entiteiten ondersteunen en vereenvoudigen. Deze moeten zo klein zijn dat de segmenteringsengine de volledige gegevensset in het geheugen kan laden voor optimale verwerking (snelle puntzoekopdracht).

![ Infographic die toont dat een profielentiteit uit afmetingsentiteiten bestaat.](images/guardrails/profile-and-dimension-entities.png)

### Profielfragmenten

In dit document zijn er verschillende hulplijnen die naar &quot;profielfragmenten&quot; verwijzen. In Experience Platform worden meerdere profielfragmenten samengevoegd tot het realtime klantprofiel. Elk fragment vertegenwoordigt een unieke primaire identiteit en de corresponderende record of volledige set gebeurtenisgegevens voor die id binnen een bepaalde gegevensset. Meer over profielfragmenten leren, verwijs naar het [ overzicht van het Profiel ](home.md#profile-fragments-vs-merged-profiles).

### Beleid samenvoegen {#merge-policies}

Wanneer het samenbrengen van gegevens uit veelvoudige bronnen, is het fusiebeleid de regels die Experience Platform gebruikt om te bepalen hoe de gegevens aan voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om die verenigde mening tot stand te brengen. Bijvoorbeeld, als een klant met uw merk over verscheidene kanalen in wisselwerking staat, zal uw organisatie veelvoudige profielfragmenten met betrekking tot die enige klant hebben die in veelvoudige datasets verschijnen. Wanneer deze fragmenten in Experience Platform worden opgenomen, worden ze samengevoegd om één profiel voor die klant te maken. Wanneer de gegevens uit meerdere bronnen conflicteren, bepaalt het samenvoegbeleid welke informatie moet worden opgenomen in het profiel voor de persoon. Per sandbox zijn maximaal vijf (5) samenvoegbeleidsregels die het `_xdm.context.profile` -schema gebruiken, toegestaan. Om meer over fusiebeleid te leren, te lezen gelieve het [ overzicht van het samenvoegbeleid ](merge-policies/overview.md).

### Adobe Analytics-rapportenpakket, gegevenssets in Experience Platform {#aa-datasets}

De veelvoudige rapportsuites kunnen voor Profiel worden toegelaten zolang alle gegevensconflicten worden opgelost. U kunt de functie Gegevensvoorbeeld gebruiken om gegevensconflicten op te lossen over eVars, Lijsten, en Props. Om meer over te leren hoe te om de functionaliteit van Prep van Gegevens te gebruiken, te lezen gelieve de [ de schakelaargids UI van Adobe Analytics ](../sources/tutorials/ui/create/adobe-applications/analytics.md).

## Volgende stappen

Raadpleeg de volgende documentatie voor meer informatie over andere Experience Platform Services-instructies, informatie over end-to-end latentie en licentiegegevens uit Real-Time CDP Product Description-documenten:

* [Real-Time CDP guardrails](/help/rtcdp/guardrails/overview.md)
* [ de diagrammen van de de latentie van begin tot eind ](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=nl-NL#end-to-end-latency-diagrams) voor diverse diensten van Experience Platform.
* [ Real-Time Customer Data Platform (B2C Edition - Prime en de Pakketten van Ultimate) ](https://helpx.adobe.com/nl/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [ Real-Time Customer Data Platform (B2P - de Pakketten van Prime en van Ultimate) ](https://helpx.adobe.com/nl/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [ Real-Time Customer Data Platform (B2B - de Pakketten van Prime en van Ultimate) ](https://helpx.adobe.com/nl/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)

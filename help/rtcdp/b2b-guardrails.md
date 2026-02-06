---
keywords: profiel;real-time profiel van de klant;het oplossen van problemen;gidsen;grens;entiteit;primaire entiteit;dimensie entiteit;RTCDP;CDP;B2B edition;Real-Time Customer Data Platform;real-time platform van de klantengegevens;real-time cdp;b2b;cdp;
title: Standaardhulplijnen voor Real-Time Customer Data Platform B2B edition
type: Documentation
description: Adobe Experience Platform gebruikt een sterk gedenormaliseerd hybride gegevensmodel dat verschilt van het traditionele relationele gegevensmodel. Dit document biedt standaardgebruiks- en tarieflimieten om u te helpen uw gegevens te modelleren voor optimale systeemprestaties met Adobe Real-Time Customer Data Platform B2B edition.
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html#rtcdp-editions" newtab=true
feature: Guardrails, B2B
exl-id: 8eff8c3f-a250-4aec-92a1-719ce4281272
source-git-commit: 5998adf98aa7250864983d7e4e629921633e1a1c
workflow-type: tm+mt
source-wordcount: '1815'
ht-degree: 1%

---

# Standaardhulplijnen voor Real-Time Customer Data Platform B2B edition

>[!NOTE]
>
>De limieten die in dit document worden beschreven, vertegenwoordigen de wijzigingen die door Real-Time Customer Data Platform B2B edition zijn ingeschakeld. Voor een volledige lijst van standaardgrenzen voor Real-Time CDP B2B edition, combineer deze grenzen met de algemene grenzen van Adobe Experience Platform die in de [ garanties voor de gegevensdocumentatie van het Profiel van de Klant in real time ](../profile/guardrails.md) worden geschetst.

Met Real-Time Customer Data Platform B2B edition kunt u persoonlijke kanaalervaringen bieden op basis van gedragsinzichten en klantkenmerken in de vorm van realtime-klantprofielen en accountprofielen. Om deze nieuwe benadering van profielen te steunen, gebruikt Experience Platform een hoogst gedenormaliseerd hybride gegevensmodel dat van het traditionele relationele gegevensmodel verschilt.

>[!IMPORTANT]
>
>Controleer uw vergunningsrechten in uw Orde van de Verkoop en de overeenkomstige [ Beschrijving van het Product ](https://helpx.adobe.com/legal/product-descriptions.html) op daadwerkelijke gebruiksgrenzen naast deze guardrails pagina.

Dit document biedt standaardgebruiks- en tarieflimieten om u te helpen uw gegevens te modelleren voor optimale systeemprestaties. Bij het bekijken van de volgende instructies wordt aangenomen dat u de gegevens correct hebt gemodelleerd. Als u vragen hebt over het modelleren van uw gegevens, neemt u contact op met uw medewerker van de klantenservice.

>[!INFO]
>
>De meeste klanten overschrijden deze standaardgrenzen niet. Neem contact op met uw medewerker van de klantenservice als u meer wilt weten over aangepaste limieten.

## Limiettypen

Dit document bevat twee typen standaardlimieten:

| Het type Guardrail | Beschrijving |
| -------------- | ----------- |
| **Gegarandeerde van Prestaties (Zachte grens)** | Prestatiegaranties zijn gebruikslimieten die betrekking hebben op het bereik van uw gebruiksgevallen. Als u de prestatiegaranties overschrijdt, kan de prestaties achteruitgaan en de latentie vertragen. Adobe is niet verantwoordelijk voor deze verslechtering van de prestaties. Klanten die een prestatiegarantie consequent overschrijden, kunnen ervoor kiezen om extra capaciteit te licentiëren om prestatievermindering te voorkomen. |
| **systeem-afgedwongen grails (Harde grens)** | De door het systeem afgedwongen instructies worden afgedwongen door de gebruikersinterface of API van Real-Time CDP. Dit zijn grenzen die u niet kunt overschrijden aangezien UI en API u zal tegenhouden dit te doen of een fout zal terugkeren. |

>[!INFO]
>
>De limieten die in dit document worden uiteengezet, worden voortdurend verbeterd. Kom regelmatig terug voor updates. Als u meer wilt weten over aangepaste limieten, neemt u contact op met uw medewerker van de klantenservice.

## Gegevensmodellimieten

De volgende instructies bieden aanbevolen limieten bij het modelleren van gegevens in realtime-klantprofiel. Meer over primaire entiteiten en afmetingsentiteiten leren, zie de sectie over [ entiteittypes ](#entity-types) in de Bijlage.

### Primaire entiteitsinstructies

>[!NOTE]
>
>De limieten van het gegevensmodel die in deze sectie worden beschreven, vertegenwoordigen de wijzigingen die door Real-Time Customer Data Platform B2B edition zijn ingeschakeld. Voor een volledige lijst van standaardgrenzen voor Real-Time CDP B2B edition, combineer deze grenzen met de algemene grenzen van Adobe Experience Platform die in de [ garanties voor de gegevensdocumentatie van het Profiel van de Klant in real time ](../profile/guardrails.md) worden geschetst.

| Guardrail | Limiet | Limiettype | Beschrijving |
| --------- | ----- | ---------- | ----------- |
| Real-Time CDP B2B edition standaard XDM-klassegegevenssets | 60 | Prestatiegerichting | Een maximum van 60 datasets die hefboomwerking de klassen standaard van de Gegevens van de Ervaring (XDM) door Real-Time CDP B2B edition worden verstrekt wordt geadviseerd. Voor een volledige lijst van standaardXDM klassen voor B2B gebruiksgevallen, verwijs naar de [ schema&#39;s in de documentatie van Real-Time CDP B2B edition ](schemas/b2b.md). <br/><br/>*Nota: Wegens de aard van Experience Platform gedenormaliseerde hybride gegevensmodel, overschrijden de meeste klanten deze grens niet. Voor vragen over hoe te om uw gegevens te modelleren, of als u meer over douanelimieten zou willen leren, gelieve uw vertegenwoordiger van de klantenzorg te contacteren.* |
| Identiteitstelling voor individuele account in een identiteitsgrafiek | 50 | Prestatiegerichting | Het maximumaantal identiteiten in een identiteitsgrafiek voor een individuele rekening is 50. Profielen met meer dan 50 identiteiten worden uitgesloten van segmentatie, export en lookups. |
| Verouderde relaties met meerdere entiteiten | 20 | Prestatiegerichting | Er wordt aanbevolen maximaal 20 relaties tussen primaire entiteiten en dimensie-entiteiten te definiëren. Aanvullende relatietoewijzingen moeten pas worden gemaakt wanneer een bestaande relatie is verwijderd of uitgeschakeld. |
| Veel-op-één relaties per XDM-klasse | 2 | Prestatiegerichting | Het wordt aanbevolen maximaal twee vele-op-één relaties te definiëren per XDM-klasse. Er dient geen aanvullende relatie te worden gelegd totdat een bestaande relatie is verwijderd of uitgeschakeld. Voor stappen op hoe te om een verband tussen twee schema&#39;s tot stand te brengen, verwijs naar het leerprogramma op [ bepalend B2B schemaverhoudingen ](../xdm/tutorials/relationship-b2b.md). |

### Garanties van Dimension-entiteiten

>[!NOTE]
>
>De limieten van het gegevensmodel die in deze sectie worden beschreven, vertegenwoordigen de wijzigingen die door Real-Time Customer Data Platform B2B edition zijn ingeschakeld. Voor een volledige lijst van standaardgrenzen voor Real-Time CDP B2B edition, combineer deze grenzen met de algemene grenzen van Adobe Experience Platform die in de [ garanties voor de gegevensdocumentatie van het Profiel van de Klant in real time ](../profile/guardrails.md) worden geschetst.

| Guardrail | Limiet | Limiettype | Beschrijving |
| --------- | ----- | ---------- | ----------- |
| Geen geneste verouderde relaties | 0 | Prestatiegerichting | U zou geen verband tussen twee niet [!DNL XDM Individual Profile] schema&#39;s moeten tot stand brengen. Het creëren van verhoudingen wordt **niet** geadviseerd voor om het even welke schema&#39;s die geen deel van het [!DNL Profile] verenigingsschema uitmaken. |
| Alleen B2B-objecten kunnen deelnemen aan een vele-op-één relatie | 0 | Door het systeem afgedwongen geleiding | Het systeem ondersteunt alleen vele-op-één relaties tussen B2B-objecten. Voor meer informatie over vele-aan-één verhoudingen, verwijs naar het leerprogramma op [ bepalend B2B schemaverhoudingen ](../xdm/tutorials/relationship-b2b.md). |
| Maximale diepte van geneste relaties tussen B2B-objecten | 3 | Door het systeem afgedwongen geleiding | De maximale diepte van geneste relaties tussen B2B-objecten is 3. Dit betekent dat in een hoogst genest schema, u geen verhouding tussen B2B voorwerpen zou moeten hebben die meer dan 3 niveaus diep worden genest. |
| Eén schema voor elke dimensie-entiteit | 1 | Door het systeem afgedwongen geleiding | Elke dimensie-entiteit moet één schema hebben. Het proberen om dimensie-entiteiten te gebruiken die van meer dan één schema worden gecreeerd kan segmentatieresultaten beïnvloeden. Van verschillende dimensie-entiteiten wordt verwacht dat ze afzonderlijke schema&#39;s hebben. |

## Limieten voor gegevensgrootte

De volgende instructies verwijzen naar de gegevensgrootte en bieden aanbevolen limieten voor gegevens die kunnen worden ingevoerd, opgeslagen en opgevraagd, zoals bedoeld. Meer over primaire entiteiten en afmetingsentiteiten leren, zie de sectie over [ entiteittypes ](#entity-types) in de Bijlage.

>[!INFO]
>
>De gegevensgrootte wordt gemeten als ongecomprimeerde gegevens in JSON op het moment van inname.

### Primaire entiteitsinstructies

>[!NOTE]
>
>De limieten voor gegevensgrootte die in deze sectie worden beschreven, vertegenwoordigen de wijzigingen die door Real-Time Customer Data Platform B2B edition zijn ingeschakeld. Voor een volledige lijst van standaardgrenzen voor Real-Time CDP B2B edition, combineer deze grenzen met de algemene grenzen van Adobe Experience Platform die in de [ garanties voor de gegevensdocumentatie van het Profiel van de Klant in real time ](../profile/guardrails.md) worden geschetst.

| Guardrail | Limiet | Limiettype | Beschrijving |
| --------- | ----- | ---------- | ----------- |
| Batches die per XDM-klasse per dag worden ingevoerd | 45 | Prestatiegerichting | Het totale aantal batches dat elke dag per XDM-klasse wordt ingevoerd, mag niet groter zijn dan 45. Door extra batches in te zetten, kunnen optimale prestaties worden voorkomen. |

### Garanties van Dimension-entiteiten

>[!NOTE]
>
>De limieten voor gegevensgrootte die in deze sectie worden beschreven, vertegenwoordigen de wijzigingen die door Real-Time Customer Data Platform B2B edition zijn ingeschakeld. Voor een volledige lijst van standaardgrenzen voor Real-Time CDP B2B edition, combineer deze grenzen met de algemene grenzen van Adobe Experience Platform die in de [ garanties voor de gegevensdocumentatie van het Profiel van de Klant in real time ](../profile/guardrails.md) worden geschetst.

| Guardrail | Limiet | Limiettype | Beschrijving |
| --------- | ----- | ---------- | ----------- |
| Totale grootte voor alle dimensionale entiteiten | 5 GB | Prestatiegerichting | De aanbevolen totale grootte voor alle dimensionale entiteiten is 5 GB. Het inzetten van entiteiten met een grote dimensie kan van invloed zijn op de systeemprestaties. Het wordt bijvoorbeeld niet aanbevolen een productcatalogus van 10 GB als een dimensie-entiteit te laden. |
| Datasets per dimensionaal eenheidschema | 5 | Prestatiegerichting | Het wordt aanbevolen maximaal vijf datasets toe te voegen aan elk dimensionaal eenheidschema. Bijvoorbeeld, als u een schema voor &quot;producten&quot;creeert en vijf bijdragende datasets toevoegt, zou u geen zesde dataset moeten creëren verbonden aan het productschema. |
| Per dag ingenomen partijen van Dimension-entiteit | 4 per entiteit | Prestatiegerichting | Het aanbevolen maximumaantal per dag ingeslikte batches voor dimensieentiteiten is 4 per entiteit. U kunt bijvoorbeeld updates van een productcatalogus tot vier keer per dag invoeren. Het invoeren van extra dimensieentiteitsbatches voor dezelfde entiteit kan de systeemprestaties beïnvloeden. |

## Segmenteringsgeleiding

De instructies in deze sectie hebben betrekking op het aantal en de aard van de soorten publiek die een organisatie binnen Experience Platform kan maken, alsmede op het in kaart brengen en activeren van het publiek naar bestemmingen.

>[!NOTE]
>
>De segmentatielimieten die in deze sectie worden beschreven, vertegenwoordigen de wijzigingen die door Real-Time Customer Data Platform B2B edition zijn ingeschakeld. Voor een volledige lijst van standaardgrenzen voor Real-Time CDP B2B edition, combineer deze grenzen met de algemene grenzen van Adobe Experience Platform die in de [ garanties voor de gegevensdocumentatie van het Profiel van de Klant in real time ](../profile/guardrails.md) worden geschetst.

| Guardrail | Limiet | Limiettype | Beschrijving |
| --------- | ----- | ---------- | ----------- |
| Segmentdefinities per B2B-sandbox | 400 | Prestatiegerichting | Een organisatie kan in totaal meer dan 400 segmentdefinities hebben, zolang er minder dan 400 segmentdefinities in elke individuele B2B-sandbox zijn. Het proberen om extra segmentdefinities tot stand te brengen kan systeemprestaties beïnvloeden. |

## Volgende stappen

De limieten die in dit document worden beschreven, vertegenwoordigen de wijzigingen die door Real-Time Customer Data Platform B2B edition zijn ingeschakeld. Voor een volledige lijst van standaardgrenzen voor Real-Time CDP B2B edition, combineer deze grenzen met de algemene grenzen van Adobe Experience Platform die in de [ garanties voor de gegevensdocumentatie van het Profiel van de Klant in real time ](../profile/guardrails.md) worden geschetst.

## Bijlage

Deze sectie bevat aanvullende details voor de limieten in dit document.

### Typen entiteiten

Het [!DNL Profile] model van opslaggegevens bestaat uit twee types van kernentiteit: [ primaire entiteiten ](#primary-entity) en [ afmetingsentiteiten ](#dimension-entity).

#### Primaire entiteit

Een primaire entiteit, of profielentiteit, voegt gegevens samen om een &quot;enige bron van waarheid&quot;voor een individu te vormen. Deze verenigde gegevens worden vertegenwoordigd gebruikend wat als &quot;verenigingsmening&quot;wordt bekend is. Een verenigingsmening voegt de gebieden van alle schema&#39;s samen die de zelfde klasse in één enkel samenvoegingsschema uitvoeren. Het samenvoegingsschema voor [!DNL Real-Time Customer Profile] is een gedenormaliseerd hybride gegevensmodel dat als container voor alle profielattributen en gedragsgebeurtenissen dienst doet.

Tijdonafhankelijke kenmerken, ook wel &#39;recordgegevens&#39; genoemd, worden gemodelleerd met [!DNL XDM Individual Profile] , terwijl tijdreeksgegevens, ook wel &#39;gebeurtenisgegevens&#39; genoemd, worden gemodelleerd met [!DNL XDM ExperienceEvent] . Wanneer in Adobe Experience Platform record- en tijdreeksgegevens worden opgenomen, wordt [!DNL Real-Time Customer Profile] geactiveerd om te beginnen met het opnemen van gegevens die voor het gebruik ervan zijn ingeschakeld. Hoe meer interacties en details worden opgenomen, hoe robuuster de afzonderlijke profielen worden.

![ Infographic die de verschillen tussen verslaggegevens en tijd-reeksen gegevens schetsen.](../profile/images/guardrails/profile-entity.png)

#### Dimension

Hoewel de profielgegevensopslag het handhaven van profielgegevens geen relationele opslag is, staat het Profiel integratie met kleine afmetingsentiteiten toe om publiek op een vereenvoudigde en intuïtieve manier tot stand te brengen. Deze integratie is gekend als [ multi-entiteitsegmentatie ](../segmentation/tutorials/multi-entity-segmentation.md).

Uw organisatie kan ook klassen XDM bepalen om dingen buiten individuen, zoals opslag, producten, of eigenschappen te beschrijven. Deze niet- [!DNL XDM Individual Profile] schema&#39;s worden genoemd &quot;afmetingsentiteiten&quot;(die ook als &quot;raadplegingsentiteiten&quot;worden bekend) en bevatten geen tijd-reeksgegevens. De schema&#39;s die afmetingsentiteiten vertegenwoordigen zijn verbonden met profielentiteiten door het gebruik van [ schemaverhoudingen ](../xdm/tutorials/relationship-ui.md).

Dimension-entiteiten bieden opzoekgegevens die de definities van segmenten met meerdere entiteiten ondersteunen en vereenvoudigen. Deze moeten zo klein zijn dat de segmenteringsengine de volledige gegevensset in het geheugen kan laden voor optimale verwerking (snelle puntzoekopdracht).

![ Infographic die toont dat een profielentiteit uit afmetingsentiteiten bestaat.](../profile/images/guardrails/profile-and-dimension-entities.png)

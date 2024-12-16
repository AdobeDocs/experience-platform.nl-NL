---
keywords: RTCDP;CDP;B2B edition;Real-time Customer Data Platform;real-time platform voor klantgegevens;real-time cdp;b2b;cdp
solution: Experience Platform
title: Aan de slag met Real-time Customer Data Platform B2B edition
description: Gebruik dit voorbeeldscenario als voorbeeld bij het instellen van uw implementatie van Adobe Real-time Customer Data Platform B2B edition.
feature: Get Started, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: ad9ace46-9915-4b8f-913a-42e735859edf
source-git-commit: 90323c32833b0d8a2b4feb88b8eb851bc767c2f8
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 0%

---

# Aan de slag met Real-time Customer Data Platform B2B edition

Dit document biedt een end-to-end workflow op hoog niveau om aan de slag te gaan met Real-time Customer Data Platform (CDP) B2B edition, waarbij een voorbeeld wordt gebruikt voor het illustreren van belangrijke concepten.

Het technologiebedrijf Bodea wil persoon en rekeningsgegevens van verschillende gesiloed gegevensbronnen combineren om klanten effectief met een e-mail en een de advertentiecampagne van LinkedIn voor zijn nieuw product te richten. Bodea gebruikt Marketo Engage als zijn platform van de marketing automatisering en moet een B2B-specifiek publiek van veelvoudige CRMs segmenteren die klantengegevens bevatten.

## Aan de slag

Deze zelfstudie is gebaseerd op verschillende Adobe Experience Platform-services als onderdeel van de demonstratie. Als u wilt volgen wordt het geadviseerd om een goed inzicht in de volgende diensten te hebben:

- [Experience-datamodel (XDM)](../xdm/home.md)
- [Bronnen](../sources/home.md)
- [Segmentatie](../segmentation/home.md)
- [Bestemmingen](../destinations/home.md)

## Schema&#39;s maken voor uw gegevens

Als deel van de aanvankelijke opstelling, moet de afdeling van IT van Bodea een XDM schema tot stand brengen om ervoor te zorgen dat hun gegevens een standaardformaat wanneer wordt gebracht in Platform, volgen en voor de verschillende diensten van het Platform en de producten van Adobe Experience Cloud (zoals Adobe Analytics en Adobe Target) handelend is.

>[!WARNING]
>
>U moet de innamepatronen volgen, zoals beschreven in de documentatie bij relevante bronnen waarnaar u in deze zelfstudie verwijst. Andere kaartmethoden in het veld werken niet gegarandeerd.

Met Adobe Experience Platform kunt u automatisch de schema&#39;s en naamruimten genereren die vereist zijn voor B2B-gegevensbronnen. Dit hulpmiddel zorgt ervoor dat de gecreeerde schema&#39;s de gegevens op een gestructureerde herbruikbare manier beschrijven. Volg [ B2B namespaces en schema auto-generatie hulpdocumentatie ](../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) voor een volledige verwijzing naar het opstellingsproces.

In de gebruikersinterface van Adobe Experience Platform selecteert de Bodea-markering **[!UICONTROL Schemas]** in de linkertrack, gevolgd door de tab **[!UICONTROL Browse]** . Aangezien zij het Marketo Engage auto-generatienut gebruikten, verschijnen de nieuwe lege schema&#39;s in de lijst en allen hebben een prefix van &quot;B2B&quot;.

![ de werkruimte van het Schema doorbladert lusje ](./assets/b2b-tutorial/empty-b2b-schemas.png)

Het auto-generatienut bepaalde de structuur van het gegevensmodel voor de schema&#39;s gebruikend standaard klassen XDM B2B (zoals [ XDM BedrijfsRekening ](../xdm/classes/b2b/business-account.md) en [ XDM BedrijfsKans ](../xdm/classes/b2b/business-opportunity.md)) die fundamentele B2B gegevensentiteiten vangen. Bovendien hebben de automatisch gegenereerde B2B-schema&#39;s die op deze klassen zijn gebaseerd, vooraf ingestelde relaties die geavanceerde gevallen van segmentatiegebruik mogelijk maken. Eventuele extra veldgroepen die voor de gegevensstructuur nodig zijn, kunt u hier eenvoudig via de gebruikersinterface maken. Zie de [ gids XDM UI, die gebiedsgroepen aan een schemacgedeelte ](../xdm/ui/resources/schemas.md#add-field-groups) voor meer informatie toevoegt.

>[!NOTE]
> 
>Als u niet het auto-generatornut gebruikt of een nieuwe verhouding zou moeten worden gecreeerd, zie het leerprogramma op [ creërend verhoudingen tussen schema&#39;s B2B ](../xdm/tutorials/relationship-b2b.md).

In realtime klantprofiel worden gegevens uit verschillende bronnen samengevoegd om geconsolideerde profielen van belangrijke B2B-entiteiten te maken. Aangezien de profielen worden geproduceerd gebaseerd op één enkele klasse, plaatst het auto-generatienut omhoog verhoudingen tussen schema&#39;s die op gemeenschappelijke bedrijfsgebruikscenario&#39;s worden gebaseerd. Dientengevolge, is het team van Bodea nu bereid om gegevens in te voeren die op hun B2B schema&#39;s worden gebaseerd.

>[!NOTE]
> 
>Standaard identiteitsnaamruimten, primaire sleutels, en verhoudingen die voor de schema&#39;s door het auto-generatienut worden gecreeerd zijn gemakkelijk te ontdekken binnen de werkruimte van het Schema.
>
>![ standaardschemaidentiteit en verhoudingUI vertoning ](./assets/b2b-tutorial/schema-identity-relationship.png)

## Gegevens in Experience Platform plaatsen

Daarna, gebruikt de telleraar Bodea de [ schakelaar van het Marketo Engage ](../sources/connectors/adobe-applications/marketo/marketo.md) om gegevens in Platform voor gebruik in stroomafwaartse diensten in te voeren. U kunt ook gegevens invoeren met een van de goedgekeurde bronnen voor Real-Time CDP B2B edition.

>[!NOTE]
> 
>Om te leren welke bronschakelaars aan uw organisatie beschikbaar zijn, kunt u de broncatalogus in Platform UI bekijken. Om tot de catalogus toegang te hebben, selecteer **Bronnen** in de linkernavigatie, dan uitgezochte **Catalogus**.

Als u een verbinding wilt maken tussen een Marketo-account en Platform, moet u verificatiegegevens aanschaffen. Zie de [ gids bij het bereiken van de geloofsbrieven van de de bronschakelaarauthentificatie van Marketo ](../sources/connectors/adobe-applications/marketo/marketo-auth.md) voor gedetailleerde instructies.

Nadat de Bodea-markering de verificatiegegevens heeft opgehaald, maakt deze een verbinding tussen de Marketo-account en de organisatie Platform. Zie de documentatie voor instructies op [ hoe te om een Rekening van Marketo te verbinden gebruikend Platform UI ](../sources/tutorials/ui/create/adobe-applications/marketo.md).

De bronschakelaar van het Marketo Engage verstrekt een auto-toewijzingseigenschap om het proces te maken om al uw gegevensgebieden aan die van nieuw tot stand gebrachte schema&#39;s in kaart te brengen veel gemakkelijker.

>[!NOTE]
> 
>Als u aangepaste veldgroepen hebt gemaakt in uw XDM-schema&#39;s, hebt u mogelijk niet-verbonden velden in deze fase van het proces. Controleer alle waarden die uw aangepaste veldgroepen vullen.

De telleraar Bodea controleert dat alle gebiedsgroepen geschikt in kaart worden gebracht en vervolgt het proces van de bronopstelling door een dataflow te initialiseren. Door een gegevensstroom te creëren om de gegevens van Marketo in te brengen, kunnen de inkomende gegevens door de stroomafwaartse diensten van het Platform worden gebruikt. Tijdens de eerste inname worden gegevens als batch in het Experience Platform gebracht. Hierna worden de volgende opgenomen gegevens gestreamd naar Profiel met vrijwel realtime updates.

## Een publiek maken om uw gegevens te evalueren

De volgende taak is om een publiek voor de nieuwe e-mailmarketing campagne van Bodea te creëren die op specifieke attributen van verwante entiteiten in de brongegevens wordt gebaseerd. In de interface van het Platform selecteert de Bodea-markeerteken eerst **[!UICONTROL Segments]** in de linkernavigatie en vervolgens **[!UICONTROL Create segment]** .

In dit voorbeeld vindt het publiek alle mensen die in de verkoopafdeling werken en zijn verwant aan om het even welke rekening die minstens één open kans heeft. Voor dit soort publiek is een koppeling vereist tussen de XDM-klasse Individual Profile, de XDM-klasse Business Account en de XDM-klasse Business Opportunity.

![ gevalsegment van het Gebruik ](./assets/b2b-tutorial/use-case-segment.png)

>[!NOTE]
> 
>Voor instructies op hoe te om publiek tot stand te brengen om uw gegevens te evalueren zie de [ gids UI van de Bouwer van het Segment ](../segmentation/ui/segment-builder.md). Voor specifiekere B2B het gebruiksgevallen van de segmentatie, verwijs naar het [ segmentatieoverzicht voor Real-Time CDP B2B edition ](./segmentation/b2b.md).

De Bouwer van het Segment staat u toe om een verhandelbaar publiek van de gegevens van het Profiel van de Klant in real time tot stand te brengen en ramingen van uw prospectief publiek te bekijken die op de combinatie attributen, gebeurtenissen, en bestaand publiek worden gebaseerd u bepaalde.

## Uw geëvalueerde gegevens naar een doel activeren

Nadat het publiek is gemaakt, wordt een samenvatting weergegeven in de sectie [!UICONTROL Details] van de werkruimte. Aangezien geen bestemmingen momenteel voor de segmentdefinitie worden geactiveerd, moet de prijsmeter Bodea het publiek naar een dataset uitvoeren waar het kan worden betreden en worden gehandeld.

In de [!UICONTROL Segments] -werkruimte van de gebruikersinterface van het platform selecteert de Bodea-markeerteken **[!UICONTROL Activate to destination]** .

![ activeer het publiek aan een bestemming ](./assets/b2b-tutorial/activate-to-destination.png)

>[!NOTE]
> 
>Zie het leerprogramma op [ activerend een publiek aan een bestemming ](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html) voor uitvoerige stappen op hoe te om dit te verwezenlijken.

De Bodea-markeerteken activeert het publiek naar de Marketo-bestemming, zodat het publiek gegevens van Platform naar Marketo Engage kan verzenden in de vorm van een statische lijst. Zie de gids op de [ bestemming van Marketo ](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/adobe/marketo-engage.html) voor meer informatie.

## Volgende stappen

Door deze zelfstudie te volgen, hebt u de verschillende Adobe Experience Platform-services die Real-Time CDP B2B edition gebruikt, met succes benut. Dientengevolge, hebt u geleerd om uw B2B gegevens in te voeren, te segmenteren, te evalueren en uit te voeren als actionable publiek dat over verschillende kanalen kan worden betrokken.

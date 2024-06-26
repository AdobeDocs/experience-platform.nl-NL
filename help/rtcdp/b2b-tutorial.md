---
keywords: RTCDP;CDP;B2B Edition;Real-time Customer Data Platform;real-time platform voor klantgegevens;real-time cdp;b2b;cdp
solution: Experience Platform
title: Aan de slag met Real-time Customer Data Platform B2B Edition
description: Gebruik dit voorbeeldscenario als voorbeeld bij het instellen van uw implementatie van Adobe Real-time Customer Data Platform B2B Edition.
feature: Get Started, B2B
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: ad9ace46-9915-4b8f-913a-42e735859edf
source-git-commit: 8a487d948d2eb7db167298b61045ef8dd2099da6
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 0%

---

# Aan de slag met Real-time Customer Data Platform B2B Edition

Dit document biedt een end-to-end workflow op hoog niveau om aan de slag te gaan met Real-time Customer Data Platform (CDP) B2B Edition, waarbij een voorbeeld wordt gebruikt voor het illustreren van belangrijke concepten.

Het technologiebedrijf Bodea wil persoon en rekeningsgegevens van verschillende gesiloed gegevensbronnen combineren om klanten effectief met een e-mail en een de advertentiecampagne van LinkedIn voor zijn nieuw product te richten. Bodea gebruikt Marketo Engage als zijn platform van de marketing automatisering en moet een B2B-specifiek publiek van veelvoudige CRMs segmenteren die klantengegevens bevatten.

## Aan de slag

Deze zelfstudie is gebaseerd op verschillende Adobe Experience Platform-services als onderdeel van de demonstratie. Als u wilt volgen wordt het geadviseerd om een goed inzicht in de volgende diensten te hebben:

- [Experience Data Modal (XDM)](../xdm/home.md)
- [Bronnen](../sources/home.md)
- [Segmentatie](../segmentation/home.md)
- [Doelen](../destinations/home.md)

## Schema&#39;s maken voor uw gegevens

Als deel van de aanvankelijke opstelling, moet de afdeling van IT van Bodea een XDM schema tot stand brengen om ervoor te zorgen dat hun gegevens een standaardformaat wanneer wordt gebracht in Platform, volgen en voor de verschillende diensten van het Platform en de producten van Adobe Experience Cloud (zoals Adobe Analytics en Adobe Target) handelend is.

>[!WARNING]
>
>U moet de innamepatronen volgen, zoals beschreven in de documentatie bij relevante bronnen waarnaar u in deze zelfstudie verwijst. Andere kaartmethoden in het veld werken niet gegarandeerd.

Met Adobe Experience Platform kunt u automatisch de schema&#39;s en naamruimten genereren die vereist zijn voor B2B-gegevensbronnen. Dit hulpmiddel zorgt ervoor dat de gecreeerde schema&#39;s de gegevens op een gestructureerde herbruikbare manier beschrijven. Volg de [B2B-naamruimten en documentatie van het hulpprogramma voor automatisch genereren van schema](../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) voor een volledige verwijzing naar het installatieproces.

In de gebruikersinterface van Adobe Experience Platform selecteert de Bodea-markeerteken **[!UICONTROL Schemas]** in het linkerspoor, gevolgd door **[!UICONTROL Browse]** tab. Aangezien zij het Marketo Engage auto-generatienut gebruikten, verschijnen de nieuwe lege schema&#39;s in de lijst en allen hebben een prefix van &quot;B2B&quot;.

![Tabblad Bladeren in werkruimte Schema](./assets/b2b-tutorial/empty-b2b-schemas.png)

Het nut van de auto-generatie bepaalde de structuur van het gegevensmodel voor de schema&#39;s gebruikend standaard klassen XDM B2B (zoals [XDM Business Account](../xdm/classes/b2b/business-account.md) en [XDM Business Opportunity](../xdm/classes/b2b/business-opportunity.md)) die fundamentele B2B-gegevensentiteiten vastleggen. Bovendien hebben de automatisch gegenereerde B2B-schema&#39;s die op deze klassen zijn gebaseerd, vooraf ingestelde relaties die geavanceerde gevallen van segmentatiegebruik mogelijk maken. Eventuele extra veldgroepen die voor de gegevensstructuur nodig zijn, kunt u hier eenvoudig via de gebruikersinterface maken. Zie de [XDM UI-hulplijn: veldgroepen toevoegen aan een schemasectie](../xdm/ui/resources/schemas.md#add-field-groups) voor meer informatie .

>[!NOTE]
> 
>Als u niet het auto-generatornut gebruikt of een nieuwe verhouding zou moeten tot stand worden gebracht, zie het leerprogramma op [relaties creëren tussen B2B-schema&#39;s](../xdm/tutorials/relationship-b2b.md).

In realtime klantprofiel worden gegevens uit verschillende bronnen samengevoegd om geconsolideerde profielen van belangrijke B2B-entiteiten te maken. Aangezien de profielen worden geproduceerd gebaseerd op één enkele klasse, plaatst het auto-generatienut omhoog verhoudingen tussen schema&#39;s die op gemeenschappelijke bedrijfsgebruikscenario&#39;s worden gebaseerd. Dientengevolge, is het team van Bodea nu bereid om gegevens in te voeren die op hun B2B schema&#39;s worden gebaseerd.

>[!NOTE]
> 
>Standaard identiteitsnaamruimten, primaire sleutels, en verhoudingen die voor de schema&#39;s door het auto-generatienut worden gecreeerd zijn gemakkelijk te ontdekken binnen de werkruimte van het Schema.
>
>![standaardschema-id en -relatie, UI-weergave](./assets/b2b-tutorial/schema-identity-relationship.png)

## Gegevens in Experience Platform plaatsen

Vervolgens gebruikt de Bodea-markering de [Marketo Engage-aansluiting](../sources/connectors/adobe-applications/marketo/marketo.md) gegevens in Platform in te voeren voor gebruik in downstreamdiensten. U kunt ook gegevens invoeren door een van de goedgekeurde bronnen voor Real-Time CDP B2B Edition te gebruiken.

>[!NOTE]
> 
>Om te leren welke bronschakelaars aan uw organisatie beschikbaar zijn, kunt u de broncatalogus in Platform UI bekijken. Als u de catalogus wilt openen, selecteert u **Bronnen** in de linkernavigatie selecteert u vervolgens **Catalogus**.

Als u een verbinding wilt maken tussen een Marketo-account en Platform, moet u verificatiegegevens aanschaffen. Zie de [handleiding voor het verkrijgen van verificatiereferenties van Marketo-bronconnector](../sources/connectors/adobe-applications/marketo/marketo-auth.md) voor gedetailleerde instructies.

Nadat de Bodea-markering de verificatiegegevens heeft opgehaald, maakt deze een verbinding tussen de Marketo-account en de organisatie Platform. Zie de documentatie voor instructies op [hoe u verbinding maakt met een Marketo-account via de gebruikersinterface van het platform](../sources/tutorials/ui/create/adobe-applications/marketo.md).

De bronschakelaar van het Marketo Engage verstrekt een auto-toewijzingseigenschap om het proces te maken om al uw gegevensgebieden aan die van nieuw tot stand gebrachte schema&#39;s in kaart te brengen veel gemakkelijker.

>[!NOTE]
> 
>Als u aangepaste veldgroepen hebt gemaakt in uw XDM-schema&#39;s, hebt u mogelijk niet-verbonden velden in deze fase van het proces. Controleer alle waarden die uw aangepaste veldgroepen vullen.

De telleraar Bodea controleert dat alle gebiedsgroepen geschikt in kaart worden gebracht en vervolgt het proces van de bronopstelling door een dataflow te initialiseren. Door een gegevensstroom te creëren om de gegevens van Marketo in te brengen, kunnen de inkomende gegevens door de stroomafwaartse diensten van het Platform worden gebruikt. Tijdens de eerste inname worden gegevens als batch in het Experience Platform gebracht. Hierna worden de volgende opgenomen gegevens gestreamd naar Profiel met vrijwel realtime updates.

## Een publiek maken om uw gegevens te evalueren

De volgende taak is om een publiek voor de nieuwe e-mailmarketing campagne van Bodea te creëren die op specifieke attributen van verwante entiteiten in de brongegevens wordt gebaseerd. Binnen Platform UI, selecteert de telleraar Bodea eerst **[!UICONTROL Segments]** in de linkernavigatie, dan **[!UICONTROL Create segment]**.

In dit voorbeeld vindt het publiek alle mensen die in de verkoopafdeling werken en zijn verwant aan om het even welke rekening die minstens één open kans heeft. Voor dit soort publiek is een koppeling vereist tussen de XDM-klasse Individual Profile, de XDM-klasse Business Account en de XDM-klasse Business Opportunity.

![Hoofdlettersegment gebruiken](./assets/b2b-tutorial/use-case-segment.png)

>[!NOTE]
> 
>Voor instructies over hoe u een publiek kunt maken om uw gegevens te evalueren raadpleegt u de [Handleiding voor de gebruikersinterface van Segment Builder](../segmentation/ui/segment-builder.md). Raadpleeg voor specifiekere gevallen van B2B-segmentatiegebruik de [segmentatieoverzicht voor Real-Time CDP B2B Edition](./segmentation/b2b.md).

De Bouwer van het Segment staat u toe om een verhandelbaar publiek van de gegevens van het Profiel van de Klant in real time tot stand te brengen en ramingen van uw prospectief publiek te bekijken die op de combinatie attributen, gebeurtenissen, en bestaand publiek worden gebaseerd u bepaalde.

## Uw geëvalueerde gegevens naar een doel activeren

Nadat het publiek is gemaakt, wordt een samenvatting weergegeven in het dialoogvenster [!UICONTROL Details] van de werkruimte. Aangezien geen bestemmingen momenteel voor de segmentdefinitie worden geactiveerd, moet de prijsmeter Bodea het publiek naar een dataset uitvoeren waar het kan worden betreden en worden gehandeld.

Binnen de [!UICONTROL Segments] in de werkruimte van de interface van het platform selecteert de Bodea-markering **[!UICONTROL Activate to destination]**.

![Het publiek naar een doel activeren](./assets/b2b-tutorial/activate-to-destination.png)

>[!NOTE]
> 
>Zie de zelfstudie aan [het activeren van een publiek aan een bestemming](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html) voor uitvoerige stappen over hoe te om dit te verwezenlijken.

De Bodea-markeerteken activeert het publiek naar de Marketo-bestemming, zodat het publiek gegevens van Platform naar Marketo Engage kan verzenden in de vorm van een statische lijst. Zie de handleiding op de [Marketo-bestemming](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/adobe/marketo-engage.html) voor meer informatie .

## Volgende stappen

Door deze zelfstudie te volgen, hebt u de verschillende Adobe Experience Platform-services benut die door Real-Time CDP B2B Edition worden gebruikt. Dientengevolge, hebt u geleerd om uw B2B gegevens in te voeren, te segmenteren, te evalueren en uit te voeren als actionable publiek dat over verschillende kanalen kan worden betrokken.

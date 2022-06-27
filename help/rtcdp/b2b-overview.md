---
keywords: RTCDP;CDP;B2B Edition;Real-time Customer Data Platform;real-time platform voor klantgegevens;real-time cdp;b2b;cdp;Customer AI
title: Real-time CDP B2B Edition - Overzicht
description: Overzicht van Real-time Customer Data Platform B2B Edition-account
exl-id: 9b45bba4-fc46-4d69-b36a-5cb91f316612
source-git-commit: ad0d38cbd249642d582a807c5679065827f57717
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 0%

---

# Overzicht van Real-time Customer Data Platform B2B Edition

Gebaseerd op Real-time Customer Data Platform (Real-Time CDP), is de Echte - tijdCDP B2B Uitgave speciaal-gebouwd voor marketers die in een zaken-aan-zaken de dienstmodel werken. Het verenigt gegevens uit veelvoudige bronnen en combineert het in één enkele mening van mensen en rekeningsprofielen. Deze verenigde gegevens staan marketers toe om specifiek publiek nauwkeurig te richten en dat publiek over alle beschikbare kanalen te betrekken.

Er zijn verbeteringen aan een verscheidenheid van de mogelijkheden van Adobe Experience Platform die Real-time CDP B2B Uitgave van zijn B2C tegenhanger onderscheiden. Zij omvatten verbeteringen aan het Model van de Gegevens van de Ervaring (XDM) voor B2B gebruiksgevallen, verbeteringen aan identiteitsresolutie en profielsegmentatie, evenals een douane-gebouwde schakelaar en bestemming voor [!DNL Marketo Engage]. De [!DNL Marketo] Dankzij de aansluiting kunnen B2B-merken hun toonaangevende B2B-betrokkenheidsgegevens verbinden met gedragsinformatie om de leads te voeden en de marketingactiviteiten op basis van account te verbeteren.

Met CDP B2B Edition in realtime kunt u:

* Combineer gegevens die uit meerdere bronnen zijn verzameld in één weergave om holistische personen en accountprofielen te maken.
* Verrijk, segmenteer en exporteer al uw gegevens over meerdere bronnen vanuit een gecentraliseerde opslagruimte van uniforme accountprofielen.
* Beheer uw gegevens met behulp van de tools voor gegevensbeheer die beschikbaar zijn in elke stap van het centralisatieproces om ervoor te zorgen dat uw gegevens in overeenstemming zijn met de wettelijke voorschriften en het bedrijfsbeleid.

Meer gedetailleerde informatie over de verbeteringen die in real time CDP B2B Edition zijn aangebracht, wordt in de volgende secties verdeeld.

## XDM

CDP B2B Edition in real time biedt verschillende nieuwe XDM-schemaklassen, veldgroepen en relatietypen om uw gegevens specifiek voor B2B-doeleinden vast te leggen en te structureren. Zie het overzicht op [XDM in Real-time CDP B2B-editie](./schemas/b2b.md) voor een uitsplitsing van elk van deze verbeteringen.

Door vooraf geconfigureerde B2B-schema&#39;s te gebruiken, kunt u gegevens in een gestandaardiseerde, activeerbare structuur inbrengen. Veel van de nieuwe schemaklassen wijzen bijna direct aan die in mainstream CRMs zoals aan [!DNL Salesforce], [!DNL Microsoft Dynamics], [!DNL Marketo]en andere B2B-gegevensbronnen. Met CDP B2B Uitgave in real time, kunt u gegevens van B2B bronnen in Platform op een ongecompliceerde manier en met resultaten brengen die gemakkelijk zijn te controleren.

Deze verbeteringen XDM staan u toe om gegevens via B2B-centric bronnen en bestemmingen beter in te voeren en te activeren, die gegevenssamenvoeging en presentatie voor meer diverse en flexibele gebruiksgevallen verbeteren.

## Identiteitsresolutie

Nadat de schema&#39;s worden bepaald en de gegevens zijn opgenomen die aan die schema&#39;s in overeenstemming zijn, identificeert de Echte - tijdCDP B2B Uitgave bronverslagen die mensen en ondernemingen door een krachtig, in real time systeem van de identiteitsresolutie vertegenwoordigen.

Het systeem van de identiteitsresolutie verstrekt de volgende eigenschappen:

* Gecombineerde B2B- en B2C-personenrecords
* Een accounthiërarchie op meerdere niveaus
* Vele-aan-vele, mensen-aan-rekening verbindingen
* Personen en accountidentiteiten worden in real-time opgelost

Het systeem voor identiteitsafwikkeling is uitgebreid om een meer veelzijdige classificatie van personen te ondersteunen. Het systeem staat voor mensen toe om als lood in bedrijfskansen evenals klanten worden geïdentificeerd.

De verslagen van de rekening die door bronCRM worden gesynchroniseerd en via veelvoudige wegen binnen het systeem worden verbonden worden samengevoegd door Platform. Het systeem brengt die mensen samen verbonden aan bedrijfskansen en die geregistreerd als klanten, maar kan ook het onderscheid tussen hen als attribuut bewaren als zij identificeerbaar zijn.

Overeenkomende id&#39;s worden gebruikt om accountrecords van meerdere systemen te koppelen en samen te voegen. Accounthiërarchieën blijven gedurende dit proces behouden. De differentiators worden gebruikt onderzoeken of een persoon met een rekening verbonden is of niet, en verstrekken de capaciteit om hen van de rekening te scheiden indien nodig.

## Profielen en segmentatie

Zodra de Uitgave In real time CDP B2B gegevens en opgeloste identiteiten met betrekking tot mensen, bedrijven, attributen, en gedrag heeft ingegeten, dat gegeven wordt gebruikt om profielen te construeren. Deze profielen kunnen vervolgens worden gesegmenteerd in een browserbaar publiek dat vervolgens kan worden geactiveerd voor verschillende doelen.

Als het systeem correct is geïmplementeerd, worden mensen bijgehouden die unieke primaire id&#39;s gebruiken in plaats van kenmerken die kunnen worden gewijzigd, zoals e-mailadressen. Dit betekent dat als iemand van baan verandert, het systeem hen nog steeds volgt. De persoon is nog steeds dezelfde entiteit, maar in plaats daarvan zijn ze aan een nieuwe rekening gekoppeld. Deze native functionaliteit biedt een grote vector voor uitbreiding naar nieuwe accounts, aangezien het systeem deze personen volgt als individuen, inclusief alle kenmerken en gedragingen.

## B2B-bronnen

Platform staat gegevens toe om van externe bronnen worden opgenomen terwijl het voorzien u van de capaciteit om inkomende gegevens te structureren, te etiketteren en te verbeteren gebruikend de diensten van het Platform. De [!DNL Marketo] bron staat u toe om B2B gegevens in Platform te stromen en deze gegevens bijgewerkt te houden gebruikend Platform-verbonden toepassingen. Het ondersteunt een willekeurig aantal [!DNL Marketo] (wat gunstig is voor grote bedrijven met meerdere instanties) en wordt opgenomen in één IMS-organisatie waar de gegevens worden samengevoegd.

>[!NOTE]
>
>De [!DNL Marketo] bron is **niet** vereist om Real-time CDP B2B Edition te gebruiken.

Zie de [bronnen in Real-time CDP B2B Edition](./sources/b2b.md) documentatie voor meer informatie over Marketo en het in Platform brengen van B2B-gegevens.

## B2B-bestemmingen

De bestemmingen van het Experience Platform zoals de Klant van Google, Facebook, LinkedIn, Marketo Engage, Amazon S3, de Vertoning van Google &amp; Video 360, Google Ads, en de Manager van Google Ad zijn beschikbaar en volledig gesteund door CDP B2B Uitgave in real time. De bestemming van de Marketo Engage stroomt ook de gegevens van het segmentlidmaatschap uit Platform en stelt het als lijsten in Marketo beschikbaar.

Zie het overzicht op de [Marketo Engage-bestemming](../destinations/catalog/adobe/marketo-engage.md) voor meer informatie .

Voor bedrijven met meer dan één CRM, verstrekt de Echte - tijdCDP B2B Uitgave de optie om bestemmingsschakelaars aan afzonderlijke instanties van Marketo of CRM te vormen. Indien vereist, kunt u bestemmingsschakelaars aan elke instantie vormen en publiek naar elk van de instanties van CRM onafhankelijk verzenden.

## Volgende stappen

Nu u beter de voordelen voor marketers begrijpt die door Echte - tijd CDP B2B Uitgave, en verschillen tussen het en Echte - tijd CDP worden aangeboden, kunt u leren hoe te om deze eigenschappen op uw eigen IMS Organisatie toe te passen.

Om te begrijpen hoe de Echte - tijdCDP B2B Uitgave uw zaken-aan-zaken de dienstmodel kan voordeel halen, zie de volgende documentatie om u te helpen begonnen worden:

* [Een voorbeeld gebruikt geval voor Echte - tijdCDP B2B Uitgave](./b2b-use-case.md)
* [Een end-to-end zelfstudie voor Real-time Customer Data Platform B2B Edition](./b2b-tutorial.md)
* [Hoe kan ik gegevens invoeren](./sources/b2b.md)
* [Profielen openen](./profile/profile-overview.md)
* [Schemas in Real-time Customer Data Platform B2B Edition](./schemas/b2b.md)
* [Hoe te om segmenten te bouwen](./segmentation/b2b.md)
* [Hoe te om segmenten aan bestemmingen te activeren](./destinations/b2b.md)
* [Beleid voor gegevensbeheer definiëren en afdwingen](./privacy/data-governance-overview.md)

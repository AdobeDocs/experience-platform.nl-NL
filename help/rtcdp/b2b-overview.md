---
keywords: RTCDP;CDP;B2B edition;Real-Time Customer Data Platform;real-time platform voor klantgegevens;real-time cdp;b2b;cdp;Customer AI
title: Real-Time CDP B2B edition - Overzicht
description: Overzicht van Real-time Customer Data Platform B2B Edition-account
feature: Get Started, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html#rtcdp-editions" newtab=true
exl-id: 9b45bba4-fc46-4d69-b36a-5cb91f316612
source-git-commit: 5998adf98aa7250864983d7e4e629921633e1a1c
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 0%

---

# Real-Time Customer Data Platform B2B edition - overzicht

Real-Time CDP B2B edition is gebaseerd op Adobe Real-Time Customer Data Platform (Real-Time CDP) en is speciaal ontworpen voor marketers die werken in een servicemodel voor bedrijven. Het verenigt gegevens uit veelvoudige bronnen en combineert het in één enkele mening van mensen en rekeningsprofielen. Deze verenigde gegevens staan marketers toe om specifiek publiek nauwkeurig te richten en dat publiek over alle beschikbare kanalen in dienst te nemen.

Er zijn verbeteringen aangebracht in verschillende Adobe Experience Platform-mogelijkheden die Real-Time CDP B2B edition onderscheiden van zijn B2C-tegenhanger. Deze omvatten verbeteringen aan het Model van de Gegevens van de Ervaring (XDM) voor B2B gebruiksgevallen, verbeteringen aan identiteitsresolutie en profielsegmentatie, evenals een douane-gebouwde schakelaar en bestemming voor [!DNL Marketo Engage]. Met de [!DNL Marketo] -connector kunnen B2B-merken hun toonaangevende B2B-betrokkenheidsgegevens verbinden met gedragsinformatie om leads te koesteren en marketingactiviteiten op basis van account te verbeteren.

Met Real-Time CDP B2B edition kunt u:

* Combineer gegevens die uit meerdere bronnen zijn verzameld in één weergave om holistische personen en accountprofielen te maken.
* Verrijk, segmenteer en exporteer al uw gegevens over meerdere bronnen vanuit een gecentraliseerde opslagruimte van uniforme accountprofielen.
* Beheer uw gegevens met behulp van de tools voor gegevensbeheer die beschikbaar zijn in elke stap van het centralisatieproces om ervoor te zorgen dat uw gegevens in overeenstemming zijn met de wettelijke voorschriften en het bedrijfsbeleid.

Meer details over de verbeteringen die voor Real-Time CDP B2B edition zijn aangebracht, zijn onderverdeeld in de volgende secties.

## XDM

Real-Time CDP B2B edition biedt verschillende nieuwe XDM-schemaklassen, veldgroepen en relatietypen om uw gegevens specifiek voor B2B-doeleinden vast te leggen en te structureren. Zie het overzicht op [ XDM in Real-Time CDP B2B edition ](./schemas/b2b.md) voor een uitsplitsing van elk van deze verhogingen.

Door vooraf geconfigureerde B2B-schema&#39;s te gebruiken, kunt u gegevens in een gestandaardiseerde, activeerbare structuur inbrengen. Veel van de nieuwe schemaklassen wijzen bijna direct aan die in mainstream CRMs zoals [!DNL Salesforce], [!DNL Microsoft Dynamics], [!DNL Marketo], en andere B2B gegevensbronnen aan. Met Real-Time CDP B2B edition kunt u gegevens van B2B-bronnen op een eenvoudige manier naar Experience Platform overbrengen, met resultaten die eenvoudig te controleren zijn.

Deze verbeteringen XDM staan u toe om gegevens via B2B-centric bronnen en bestemmingen beter in te voeren en te activeren, die gegevenssamenvoeging en presentatie voor meer diverse en flexibele gebruiksgevallen verbeteren.

## Identiteitsresolutie

Nadat de schema&#39;s worden bepaald en de gegevens zijn opgenomen volgend aan die schema&#39;s, identificeert Real-Time CDP B2B edition bronverslagen die mensen en ondernemingen in de praktijk door een krachtig, real-time systeem van de identiteitsresolutie vertegenwoordigen.

Het systeem van de identiteitsresolutie verstrekt de volgende eigenschappen:

* Gecombineerde B2B- en B2C-personenrecords
* Een accounthiërarchie op meerdere niveaus
* Vele-aan-vele, mensen-aan-rekening verbindingen
* Personen en accountidentiteiten worden in real-time opgelost

Het systeem voor identiteitsafwikkeling is uitgebreid om een meer veelzijdige classificatie van personen te ondersteunen. Het systeem staat voor mensen toe om als lood in bedrijfskansen evenals klanten worden geïdentificeerd.

Accountrecords die door de bron-CRM zijn gesynchroniseerd en via meerdere paden in het systeem zijn verbonden, worden door Experience Platform samengevoegd. Het systeem verenigt die mensen verbonden aan bedrijfskansen en die geregistreerd als klanten, maar kan ook het onderscheid tussen hen als attribuut bewaren als zij identificeerbaar zijn.

Overeenkomende id&#39;s worden gebruikt om accountrecords van meerdere systemen te koppelen en samen te voegen. Accounthiërarchieën blijven gedurende dit proces behouden. De differentiators worden gebruikt onderzoeken of een persoon met een rekening verbonden is of niet, en verstrekken de capaciteit om hen van de rekening te scheiden indien nodig.

## Profielen en segmentatie

Zodra Real-Time CDP B2B edition gegevens heeft opgenomen en identiteiten heeft opgelost die betrekking hebben op personen, bedrijven, kenmerken en gedragingen, worden die gegevens gebruikt om profielen samen te stellen. Deze profielen kunnen vervolgens worden gesegmenteerd in een browserbaar publiek dat vervolgens kan worden geactiveerd voor verschillende doelen.

Als het systeem correct is geïmplementeerd, worden mensen bijgehouden die unieke primaire id&#39;s gebruiken in plaats van kenmerken die kunnen worden gewijzigd, zoals e-mailadressen. Dit betekent dat als iemand van baan verandert, het systeem hen nog steeds volgt. De persoon is nog steeds dezelfde entiteit, maar in plaats daarvan zijn ze aan een nieuwe rekening gekoppeld. Deze native functionaliteit biedt een grote vector voor uitbreiding naar nieuwe accounts, aangezien het systeem deze personen volgt als individuen, inclusief al hun kenmerken en gedrag.

## B2B-bronnen

Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen en biedt u de mogelijkheid om inkomende gegevens te structureren, labelen en verbeteren met behulp van Experience Platform-services. Met de [!DNL Marketo] -bron kunt u B2B-gegevens streamen naar Experience Platform en deze gegevens up-to-date houden met Experience Platform-toepassingen. De klasse ondersteunt een willekeurig aantal instanties van [!DNL Marketo] (hetgeen gunstig is voor grote bedrijven met meerdere instanties) en voegt zich toe aan één organisatie waar de gegevens worden samengevoegd.

>[!NOTE]
>
>De [!DNL Marketo] bron is **niet** wordt vereist om Real-Time CDP B2B edition te gebruiken.

Zie de [ bronnen in Real-Time CDP B2B edition ](./sources/b2b.md) documentatie voor meer informatie over Marketo en het brengen van B2B gegevens in Experience Platform.

## B2B-bestemmingen

Experience Platform-bestemmingen zoals Google Customer Match, Facebook, LinkedIn, Marketo Engage, Amazon S3, Google Display &amp; Video 360, Google Ads en Google Ad Manager zijn beschikbaar en volledig ondersteund door Real-Time CDP B2B edition. De Marketo Engage-bestemming streamt ook segmentlidmaatschapsgegevens uit Experience Platform en maakt deze beschikbaar als lijsten in Marketo.

Zie het overzicht op de [ Bestemming van Marketo Engage ](../destinations/catalog/adobe/marketo-engage.md) voor meer informatie.

Voor bedrijven met meer dan één CRM biedt Real-Time CDP B2B edition de optie om bestemmingsschakelaars aan afzonderlijke instanties van Marketo of CRM te vormen. Indien vereist, kunt u bestemmingsschakelaars aan elke instantie vormen en publiek naar elk van de instanties van CRM onafhankelijk verzenden.

## Volgende stappen

Nu u beter begrijpt welke voordelen Real-Time CDP B2B edition biedt voor marketers, en welke verschillen er zijn tussen en Real-Time CDP, kunt u leren hoe u deze functies kunt toepassen op uw eigen organisatie.

Raadpleeg de volgende documentatie voor meer informatie over hoe Real-Time CDP B2B edition uw business-to-business servicemodel kan bevoordelen:

* [Een voorbeeld van een gebruiksgeval voor Real-Time CDP B2B edition](./b2b-use-case.md)
* [Een complete zelfstudie voor Real-Time Customer Data Platform B2B edition](./b2b-tutorial.md)
* [Hoe kan ik gegevens invoeren](./sources/b2b.md)
* [Profielen openen](./profile/profile-overview.md)
* [Schemas in Real-Time Customer Data Platform B2B edition](./schemas/b2b.md)
* [Hoe te om publiek te bouwen](./segmentation/b2b.md)
* [Het publiek naar bestemmingen activeren](./destinations/b2b.md)
* [Beleid voor gegevensbeheer definiëren en afdwingen](./privacy/data-governance-overview.md)

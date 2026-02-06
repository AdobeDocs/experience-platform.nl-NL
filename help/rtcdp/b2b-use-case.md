---
keywords: RTCDP;CDP;Real-Time Customer Data Platform;real-time platform voor klantgegevens;real-time cdp;cdp;rtcdp
title: Voorbeeld van gebruik van hoofdletters/kleine letters voor Real-Time Customer Data Platform B2B edition
description: Dit voorbeeldscenario biedt een voorbeeld voor de configuratie van uw implementatie van Adobe Real-Time Customer Data Platform B2B Edition.
feature: Get Started, Use Cases, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html#rtcdp-editions" newtab=true
exl-id: 15505980-ac33-44b2-8989-c08cbabd212b
source-git-commit: 5998adf98aa7250864983d7e4e629921633e1a1c
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 1%

---

# Voorbeeld van gebruik van hoofdletters/kleine letters voor Real-Time Customer Data Platform B2B edition

Real-Time Customer Data Platform B2B edition breidt het bestaande aanbod van Real-Time CDP en Adobe Experience Platform uit om B2B-gegevens en -workflows te ondersteunen. In dit document vindt u een voorbeeld van een gebruiksgeval waarin de extra voordelen van de B2B edition worden getoond. Deze omvatten:

- Combineer persoon- en accountgegevens uit verschillende gegevensbronnen op dezelfde locatie om een uitgebreide weergave te maken die een beter inzicht in de klanten en een nauwkeuriger segmentering mogelijk maakt. Zie de documentatie bij [&#x200B; het creëren van XDM schemaverhoudingen &#x200B;](./schemas/b2b.md) voor gebruik met gevarieerde B2B bronnen voor meer informatie.
- Segmenteer een publiek op basis van kenmerken van verwante entiteiten. Dit omvat Rekeningen, Kansen, Campagnes, en de Lijst van de Marketing. Het publiek is niet meer beperkt tot alleen Personen-kenmerken en Experience Events. Zie de [&#x200B; B2B segmentatiedocumentatie &#x200B;](./segmentation/b2b.md) voor meer voorbeelden van het creëren van B2B-Specifiek publiek.
- Native ondersteuning bieden voor het gebruik van één persoon met betrekking tot meerdere rekeningen.

## Gebruiksscenario

Bodea, een technologiebedrijf, heeft een nieuw product en wil klanten met een e-mail en een LinkedIn reclamecampagne gelijktijdig richten. Om de doeltreffendheid van hun marketingcampagne te maximaliseren, wil Bodea zich ook richten op de mensen die met die bestaande rekening verbonden zijn en die meer dan een miljoen dollar hebben uitgegeven aan hun producten eerder, EN de nieuwe productpagina in de afgelopen maand hebben bezocht.

Bodea heeft echter twee verschillende bedrijfsonderdelen. Bodea&#39;s eerste business line 1 creëert software voor de automobielindustrie. De tweede branche, &quot;Line 2&quot;, verkoopt 3D-printers die auto-onderdelen maken. Als gevolg van de twee bedrijfsonderdelen van Bodea zijn de inkomstengegevens die uit de klantenrekeningen van Bodea worden gegenereerd, niet in één enkele weergave verenigd.

Elke branche heeft haar eigen verkoopsysteem: &quot;CRM 1&quot; en &quot;CRM 2&quot;. Beide CRM-verkoopsystemen zijn verbonden met hun eigen marketingautomatiseringsplatform &quot;Marketo 1&quot; en &quot;Marketo 2&quot;. Gegevens van CRM 1 worden alleen gesynchroniseerd naar Marketo 1 en gegevens van CRM2 worden alleen gesynchroniseerd naar Marketo 2. Uiteindelijk worden hun gegevens bewaard in verschillende informatiesilo&#39;s van bedrijven.

## Huidige gegevenssituatie

Aangezien beide bedrijfsonderdelen van Bodea aan de Townsend-onderneming verkopen, worden de bedrijfsgegevens van Townsend in elk verkoopsysteem als twee afzonderlijke rekeningen geregistreerd.

In Marketo 1 wordt Townsend opgenomen als Account 1. Het heeft twee verwante mensen (p1@townsend.com en p2@townsend.com) en één gesloten-won kans van $200k (&quot;Opportunity 1&quot;) in CRM 1. Deze gegevens worden gesynchroniseerd van CRM 1 naar Marketo 1.

In Marketo 2 wordt Townsend opgenomen als Account 2. Account 2 heeft ook twee verwante personen (p2@townsend.com en p3@townsend.com) en één &#39;closed-won&#39; kans van $900k (&#39;Opportunity 2&#39;) in CRM 2. Deze gegevens worden gesynchroniseerd van CRM 2 naar Marketo 2.

Voor integratie en aanvullende bedrijfscontroledoeleinden beschikt Bodea ook over een MDM-systeem (Master Data Management), waarbij een record wordt bijgehouden waarin wordt aangegeven dat Account 1 in Marketo 1 (en CRM 1) en Account 2 in Marketo 2 (en CRM 2) dezelfde onderneming zijn.

In de laatste maand bezocht `p2@townsend.com` de nieuwe productpagina en werd het webbezoek opgenomen door Marketo 1.

![&#x200B; diagram van rekeninginfo &#x200B;](./assets/account-info.png)

## Het probleem

Lijn 1 heeft zojuist een nieuw softwareproduct uitgebracht en wil het naar de bestaande top-tier klantenbasis van Bodea upsell. Bodea lanceert een marketing campagne met dat specifieke doelpubliek in mening.

Aangezien de relevante informatie over de stad wordt geregistreerd als account 1 in Marketo 1 en account 2 in Marketo 2, kan het marketingteam van Bodea de opgeslagen informatie niet efficiënt gebruiken.

Dit verbiedt het marketingteam van Bodea om op efficiënte wijze specifieke zakelijke contacten met deze nieuwe kans aan te knopen bij deze bedrijven.

Tot op heden heeft Townsend meer dan een miljoen dollar cumulatief uitgegeven aan Bodea producten over al hun rekeningen. Een publiek dat met behulp van zijn oude systeem is gemaakt, zou echter niemand van Townsend omvatten, tenzij het totaal dat binnen één verkoopsysteem is uitgegeven meer dan 1 miljoen dollar bedroeg. Dit komt doordat de inkomstengegevens in rekeningen onder verschillende verkoopsystemen worden opgeslagen.

Aangezien de uitgaven van Townsend over verschillende verkoopsystemen worden verdeeld en individueel niet meer dan één miljoen bedragen, zou de segmentdefinitie niemand in Marketo 1 of Marketo 2 kwalificeren.

### Hoe Real-Time CDP B2B edition het probleem oplost

Met Real-Time CDP B2B edition kan het marketingteam van Bodea:

- Combineer de gegevens van alle verschillende bronnen (meerdere Marketo- en CRM-instanties en het hoofdgegevensbeheer) in Real-Time CDP B2B edition.

Met RT-CDP B2B edition kan Bodea de Marketo Engage Source Connector gebruiken om B2B gegevens van Marketo 1 en Marketo 2 naar Experience Platform te brengen en deze gegevens actueel te houden gebruikend Experience Platform verbonden toepassingen. Zie de [&#x200B; documentatie van de 0&rbrace; de bronschakelaar van Marketo &lbrace;voor meer informatie.](../sources/connectors/adobe-applications/marketo/marketo.md)

B2B-gegevens (Mensen, Accounts, Opportunity, and activity ) van CRM1 worden gesynchroniseerd in Marketo 1. Evenzo worden alle B2B-gegevens van CRM 2 gesynchroniseerd in Marketo 2. Ze worden gesynchroniseerd in Adobe Experience Platform via de Marketo-bronconnector. Nochtans, als Bodea extra gegevens van CRM in Experience Platform wil brengen, kunnen zij bestaande Verbindingen van CRM gebruiken.

In het belang van de eenvoud en het doel van dit voorbeeld worden mensen geïdentificeerd door hun e-mails. De gecombineerde accountgegevens voor dit voorbeeld zien er als volgt uit:

| Mensen |
|---|
| p1@townsend.com |
| p2@townsend.com (die de laatste maand de nieuwe productpagina heeft bezocht) |
| p3@townsend.com |

| Kansen (gesloten-won) |
|---|
| Opportunity 1, $200 k |
| Opportunity 2, $900 k |

- Maak een uniek publiek met deze geaggregeerde gegevens voor verschillende marketinginitiatieven. In dit voorbeeld vindt de segmentdefinitie alle mensen die:

   - Heb bijbehorende kansen (over ALLE rekeningen) $1 miljoen in waarde overschrijden
   - EN
   - De productpagina in de afgelopen maand hebben bezocht

- Creëer een publiek dat de meest efficiënte ontvangers van de nieuwe marketingcampagne van Bodea is. In dit voorbeeld, RT-CDP, zal B2B edition de teler helpen `p2@townsend.com` identificeren als het juiste doel voor deze marketing campagne.

Door Marketo Engage en LinkedIn bestemmingen te gebruiken, heeft Bodea een oplossing van de klantenervaring van begin tot eind voor zijn marketing team. Het publiek dat in Experience Platform is gemaakt, wordt naar de Marketo-bestemming geduwd, waar het als een statische lijst wordt weergegeven. Dit publiek wordt vervolgens automatisch toegevoegd aan een Marketo-marketingcampagne. Tegelijkertijd kan het publiek ook naar een LinkedIn marketing campagne door RT-CDP B2B edition worden verzonden.

## Volgende stappen

Door dit document te lezen, bent u nu op de hoogte gebracht van de soorten doelstellingen en problemen die met Real-Time CDP B2B edition kunnen worden opgelost.

De volgende documentatie wordt aanbevolen om meer inzicht te krijgen in B2B-specifieke functies:

- [Real-Time Customer Data Platform B2B edition - end-to-end zelfstudie](./b2b-tutorial.md)
- [Bronnen in Real-Time Customer Data Platform B2B edition](./sources/b2b.md)
- [Schemas in Real-Time Customer Data Platform B2B edition](./schemas/b2b.md)
- [B2B-segmenteringsvoorbeelden](./segmentation/b2b.md)
- [Overzicht van accountprofielen](./accounts/account-profile-overview.md)
- [Doelen in Real-Time Customer Data Platform B2B edition](./destinations/b2b.md)
- [Vorm een bestemming LinkedIn Gelijke Publiek](../destinations/catalog/social/linkedin.md)

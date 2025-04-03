---
keywords: Experience Platform;home;populaire onderwerpen;segmentatie;Segmentering;Segmentovereenkomst;segmentovereenkomst
solution: Experience Platform
title: Veelgestelde vragen over segmentovereenkomst
description: Segment Match is een segment-delende dienst in Adobe Experience Platform die voor twee of meer gebruikers van Experience Platform toestaat om segmentgegevens op een veilige, beheerde, en privacy-vriendelijke manier uit te wisselen.
exl-id: cfa9db16-0bc3-4d25-914d-0d923eccb5a3
source-git-commit: 0a9028beca36b46d6228c0038366bbac5d32603c
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# [!DNL Segment Match] vaak gestelde vragen

Deze handleiding bevat antwoorden op privacy- en juridische vragen die vaak worden gesteld over Adobe Experience Platform Segment Match.

## Welke gegevens worden gedeeld tijdens de schatting en hoe kan Adobe ervoor zorgen dat deze cijfers veilig worden verkregen?

![ overlapping-report.png ](./images/overlap-report.png)

Er worden geen klant- of segmentgegevens over sandboxen verplaatst om deze schattingsgegevens voor overlappingen te verkrijgen. De door de klant geselecteerde, vooraf gehakte toepasselijke identiteiten in een bepaalde sandbox worden toegevoegd aan een probabilistische gegevensstructuur waarin de id&#39;s zelf in een gehakt formaat worden vertegenwoordigd.

Dit is een eenrichtingsproces, dat betekent de originele pre-haastige herkenningstekens niet worden blootgesteld en kunnen niet worden omgekeerd-gebouwd.

Deze gegevensstructuren hebben unieke eigenschappen die engineering toestaan om unie en doorsnedeverrichtingen tussen hen uit te voeren, zelfs als de gecodeerde informatie ernstig wordt gecomprimeerd of gehakt. Met deze bewerkingen kan [!DNL Segment Match] de geschatte doorsnede verkrijgen van twee gegevensstructuren die bestaan uit id&#39;s van twee verschillende sandboxen, zonder dat de werkelijke waarden moeten worden vergeleken. Aangezien [!DNL Segment Match] alleen de gegevensstructuren gebruikt, laten de id&#39;s nooit de profielopslagruimten van hun respectievelijke organisaties achter voor schattingsdoeleinden. Op deze manier kan Adobe voldoen aan de privacy- en beveiligingsvereisten van klanten en beschikt het over uiterst nauwkeurige schattingsprogramma&#39;s om samenwerkingsovereenkomsten voor gegevens te begeleiden.

## Wat is het proces achter het aanwijzen van welke identiteiten gedeelde segment IDs ontvangen?

[!DNL Segment Match] biedt klanten een optie om te configureren welke naamruimten moeten worden gebruikt in de service. Deze selectie wordt toegepast op zowel het ramingsproces dat in de vorige vraag wordt beschreven als het proces van de gegevensoverdracht, als de klant besluit om het voer aan een partnerzandbak te publiceren.

Het gegevensoverdrachtproces tussen de gecodeerde identiteiten van twee verschillende organisaties wordt uitgevoerd in een neutrale compute omgeving. De gegevensoverdrachtstaak is eigendom van Adobe en de organisaties die bij het partnerschap betrokken zijn, hebben geen toegang tot deze omgeving en krijgen ook geen toegang tot logboeken die het resultaat kunnen zijn van de gegevensoverdrachtstaak.

Slechts wordt het segmentlidmaatschap opgenomen in de overlappende fragmenten van het Profiel van een ontvangende organisatie en geen extra identiteit wordt overgebracht van de afzenderorganisatie naar de ontvangende organisatie. Er wordt geen platte tekst met persoonlijk identificeerbare informatie (PII) gelezen door de gegevensoverdrachtstaak omdat [!DNL Segment Match] alleen overlap toestaat op met SHA256 gecodeerde naamruimten (e-mail/telefoon) wanneer gegevens PII zijn. Resultaten worden nooit opgeslagen in de computeromgeving.

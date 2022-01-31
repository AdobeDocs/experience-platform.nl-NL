---
keywords: Experience Platform;huis;populaire onderwerpen;segmentatie;Segmentatie;Segmentovereenkomst;segmentovereenkomst
solution: Experience Platform
title: Veelgestelde vragen over segmentovereenkomst
description: Segmentovereenkomst is een segmentdelende service in Adobe Experience Platform waarmee twee of meer gebruikers in het Platform segmentgegevens kunnen uitwisselen op een veilige, beheerde en privacyvriendelijke manier.
exl-id: cfa9db16-0bc3-4d25-914d-0d923eccb5a3
source-git-commit: 823eb549e5514a3201ba68ed395c69e202cb747f
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# [!DNL Segment Match] vaak gestelde vragen

Deze handleiding bevat antwoorden op privacy- en juridische vragen die vaak worden gesteld over Adobe Experience Platform Segment Match.

## Welke gegevens worden tijdens de schatting gedeeld en hoe kan Adobe me verzekeren dat deze cijfers veilig worden verkregen?

![overlap-rapport.png](./images/overlap-report.png)

Er worden geen klant- of segmentgegevens over sandboxen verplaatst om deze schattingsgegevens voor overlappingen te verkrijgen. De door de klant geselecteerde, vooraf gehakte toepasselijke identiteiten in een bepaalde sandbox worden toegevoegd aan een probabilistische gegevensstructuur waarin de id&#39;s zelf in een gehakt formaat worden vertegenwoordigd.

This is a one-way process, meaning the original pre-hashed identifiers are not exposed and cannot be reverse-engineered.

Deze gegevensstructuren hebben unieke eigenschappen die engineering toestaan om unie en doorsnedeverrichtingen tussen hen uit te voeren, zelfs als de gecodeerde informatie ernstig wordt gecomprimeerd of gehakt. Deze bewerkingen staan [!DNL Segment Match] om de geschatte doorsnede te krijgen van twee gegevensstructuren die bestaan uit id&#39;s van twee verschillende sandboxen zonder dat de werkelijke waarden moeten worden vergeleken. Since [!DNL Segment Match] only uses the data structures, the IDs never leave their respective IMS Organizations&#39; Profile storages for estimation purposes. Hierdoor kan Adobe voldoen aan de privacy- en beveiligingsvereisten van klanten en tegelijkertijd uiterst nauwkeurige schattingsgereedschappen bieden om samenwerkingsovereenkomsten op het gebied van gegevens te begeleiden.

## Wat is het proces achter het aanwijzen van welke identiteiten gedeelde segment IDs ontvangen?

[!DNL Segment Match] voorziet klanten van een optie om te vormen welke namespaces in de dienst te gebruiken. This selection is applied to both the estimation process described in the previous question and the data transfer process, should the customer decide to publish the feed to a partner sandbox.

The data transfer process between the encrypted identities of two different organizations is performed in a neutral compute environment. De gegevensoverdrachtstaak is in het bezit van Adobe en de organisaties die bij het partnerschap zijn betrokken, hebben geen toegang tot deze omgeving en krijgen ook geen toegang tot logboeken die het resultaat kunnen zijn van de gegevensoverdrachtstaak.

Alleen segmentlidmaatschap wordt opgenomen in de overlappende profielfragmenten van een IMS-organisatie van een ontvanger en er wordt geen extra identiteit overgedragen van de IMS-organisatie van de afzender naar de IMS-organisatie van de ontvanger. Geen platte tekst persoonlijk identificeerbare informatie (PII) wordt gelezen door de gegevensoverdrachtbaan omdat [!DNL Segment Match] staat overlappingen alleen toe op met SHA256 gecodeerde naamruimten (e-mail/telefoon) wanneer gegevens PII zijn. Resultaten worden nooit opgeslagen in de computeromgeving.

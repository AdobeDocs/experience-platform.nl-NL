---
keywords: Experience Platform;thuis;populaire onderwerpen;Marketo Engage;marketo engageren;marketo
solution: Experience Platform
title: Marketo Engage-aansluiting
description: Dit document biedt een overzicht van de bronconnector van het Marketo Engage, inclusief informatie over verificatie, toewijzing en gegevenslatentie.
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: 50b97ebb8496636a0fccd64d57d7829b1342f87c
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 0%

---

# [!DNL Marketo Engage] connector

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de platformservices. U kunt gegevens uit diverse bronnen invoeren, zoals toepassingen voor Adobe, opslag in de cloud, databases en vele andere.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) is een volledige oplossing voor het beheer van leads en B2B-marketers die de ervaringen van klanten willen transformeren door in elke fase van complexe inkoopritten te gaan werken.

Met de [!DNL Marketo Engage] bronaansluiting, kunt u B2B-gegevens van [!DNL Marketo Engage] om deze gegevens up-to-date te houden met behulp van platformaangesloten toepassingen.

>[!IMPORTANT]
>
>U moet toegang hebben tot [Adobe Real-time Customer Data Platform B2B Edition](../../../../rtcdp/b2b-overview.md) om alle Marketo datasets voor segmentatie met te gebruiken [Klantprofiel in realtime](../../../../profile/home.md). Zonder Real-Time CDP B2B Edition kunt u nog steeds de Marketo-bron gebruiken om gegevens van de personen- en activiteitengegevenssets naar Real-Time klantprofiel te verzenden voor segmentatie.

Dit document biedt een overzicht van de [!DNL Marketo Engage] bronschakelaar, met inbegrip van informatie over hoe te om de schakelaar voor authentiek te verklaren, hoe te om in kaart te brengen [!DNL Marketo Engage] velden naar Experience Data Model (XDM) en de gegevenslatentie van de connector.

## Toewijzing organisatie Adobe instellen

Voordat u toewijzingssets kunt maken voor [!DNL Marketo Engage], moet u eerst Organisatie-toewijzing voor Adoben instellen. Zie de handleiding voor gedetailleerde stappen over het voltooien van deze taak [Organisatietoewijzing voor Adobe instellen voor [!DNL Marketo Engage]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html).

## Verifieer uw [!DNL Marketo Engage] connector

Om verbinding te maken [!DNL Marketo Engage] aan Platform, moet u waarden voor uw `munchkinId`, `clientId`, en `clientSecret`.

Zie de stappen in het dialoogvenster [Verifieer uw Marketo-bronconnector](./marketo-auth.md) document om uw referenties op te halen.

## B2B-naamruimten instellen en hulpprogramma voor automatisch genereren van schema&#39;s

Gebruik vervolgens de B2B-naamruimte en het schema auto-generation hulpprogramma om uw Platform Developer Console en Postman-omgeving in te stellen. Hierdoor kunt u uw B2B-naamruimten en -schema&#39;s automatisch vullen. Zie de handleiding voor gedetailleerde instructies op [B2B-naamruimten instellen en hulpprogramma voor automatisch genereren van schema&#39;s](./marketo-namespaces.md)

## Experience Data Model (XDM)

XDM is een openbaar gedocumenteerde specificatie die gemeenschappelijke structuren en definities verstrekt die u toestaan om gegevens van derdebronnen voor gebruik in de stroomafwaartse diensten van het Platform in te voeren.

Door te voldoen aan XDM-standaarden kunnen gegevens op uniforme wijze worden opgenomen in het ecosysteem van het platform, waardoor het eenvoudiger wordt om gegevens te leveren en informatie te verzamelen.

Voor meer informatie over XDM en zijn rol in Platform, gelieve te zien [XDM System, overzicht](../../../../xdm/home.md).

## Veldtoewijzing van [!DNL Marketo Engage] naar XDM

Een bronverbinding tot stand brengen tussen [!DNL Marketo Engage] en Platform, moeten de de brongegevensgebieden van Marketo aan hun aangewezen doelXDM gebieden worden in kaart gebracht alvorens in Platform wordt opgenomen.

Zie het volgende voor gedetailleerde informatie over de regels voor het in kaart brengen van velden tussen [!DNL Marketo Engage] Gegevensbestanden en platform:

* [Activiteiten](../mapping/marketo.md#activities)
* [Programma&#39;s](../mapping/marketo.md#programs)
* [Lidmaatschap van programma](../mapping/marketo.md#program-memberships)
* [Bedrijven](../mapping/marketo.md#companies)
* [Statische lijsten](../mapping/marketo.md#static-lists)
* [Statische lijstlidmaatschappen](../mapping/marketo.md#static-list-memberships)
* [Benoemde accounts](../mapping/marketo.md#named-accounts)
* [Kansen](../mapping/marketo.md#opportunities)
* [Contactrollen opportunity](../mapping/marketo.md#opportunity-contact-roles)
* [Personen](../mapping/marketo.md#persons)

## Verwachte vertraging van [!DNL Marketo Engage] gegevens op platform

In de volgende tabel wordt de verwachte vertraging voor het overbrengen van [!DNL Marketo Engage] gegevens in Platform, die op de aard van opname en de gewenste bestemming worden gebaseerd:

| Bestemming | Verwachte vertraging |
| ----------- | ---------------- |
| [!DNL Real-Time Customer Profile] | &lt; 10 minuten |
| Gegevensmeer | &lt; 60 minuten |

>[!NOTE]
>
>Bovenstaande latentiecijfers vertegenwoordigen verwachtingen met een betrouwbaarheid van 95%. De werkelijke latentie zal variëren en kan in zeldzame gevallen 50% groter zijn dan deze cijfers.

## Volgende stappen en extra bronnen

In de volgende documentatie vindt u meer informatie over het maken van een [!DNL Marketo Engage] bronverbinding:

* Voor informatie over hoe u verbinding kunt maken met uw [!DNL Marketo Engage] gegevens naar platform, lees de zelfstudie op [een [!DNL Marketo Engage] bronverbinding in de gebruikersinterface](../../../tutorials/ui/create/adobe-applications/marketo.md).
   * Lees de zelfstudie voor informatie over hoe u schema&#39;s kunt instellen en aangepaste activiteitgegevens kunt invoeren [een bronverbinding en gegevensstroom maken voor [!DNL Marketo Engage] aangepaste activiteitsgegevens](../../../tutorials/ui/create/adobe-applications/marketo-custom-activities.md)
* Voor informatie over de onderliggende opstelling voor B2B namespaces en schema&#39;s die met worden gebruikt [!DNL Marketo Engage], lees de documentatie voor [B2B-naamruimten en -schema&#39;s](./marketo-namespaces.md).
* Voor informatie over het zoeken naar uw [!DNL Marketo Engage] munchkin-id en het genereren van uw referenties lezen de [[!DNL Marketo Engage] verificatiehandleiding](./marketo-auth.md).
* Voor informatie over de specifieke toewijzingsregels die gelden voor [!DNL Marketo Engage] datasets, lees de documentatie over [[!DNL Marketo Engage] veldtoewijzingen](../mapping/marketo.md).
* Voor algemene informatie over [!DNL Real-Time Customer Data Platform B2B Edition] en de bijbehorende functies, leest u de documentatie op [[!DNL Real-Time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).

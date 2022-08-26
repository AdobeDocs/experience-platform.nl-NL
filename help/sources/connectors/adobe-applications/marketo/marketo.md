---
keywords: Experience Platform;thuis;populaire onderwerpen;Marketo Engage;marketo engageren;marketo
solution: Experience Platform
title: Marketo Engage-aansluiting
topic-legacy: overview
description: Dit document verstrekt een overzicht van de Marketo Engage bronschakelaar, met inbegrip van informatie over zijn authentificatie, afbeelding, en gegevenslatentie.
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: efa6891024cacd383f4cd958162a7a4f8ead0624
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---

# [!DNL Marketo Engage] connector

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de services van het Platform. U kunt gegevens van diverse bronnen, zoals Adobe-toepassingen, cloudopslag, databases en vele andere, invoeren.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) (hierna &quot;[!DNL Marketo]&quot;) is een volledige oplossing voor het beheer van leads en B2B-marketers die de ervaringen van klanten willen transformeren door in elke fase van complexe inkoopritten te gaan werken.

Met de [!DNL Marketo] bronaansluiting, kunt u B2B-gegevens van [!DNL Marketo] om deze gegevens te Platforms en up-to-date te houden gebruikend Platform-Verbonden toepassingen.

>[!IMPORTANT]
>
>U moet toegang hebben tot [Real-time Customer Data Platform B2B Edition](../../../../rtcdp/b2b-overview.md) om alle Marketo datasets voor segmentatie met te gebruiken [Klantprofiel in realtime](../../../../profile/home.md). Zonder CDP B2B Uitgave in real time, kunt u de bron van Marketo nog gebruiken om gegevens van de mensen en activiteitendatasets aan het Profiel van de Klant in real time voor segmentatie te brengen.

Dit document biedt een overzicht van de [!DNL Marketo] bronschakelaar, met inbegrip van informatie over hoe te om de schakelaar voor authentiek te verklaren, hoe te om in kaart te brengen [!DNL Marketo] velden naar Experience Data Model (XDM) en de gegevenslatentie van de connector.

## Verifieer uw [!DNL Marketo] connector

Om verbinding te maken [!DNL Marketo] aan Platform, moet u waarden voor uw `munchkinId`, `clientId`, en `clientSecret`.

Zie de stappen in het dialoogvenster [Verifieer uw Marketo-bronconnector](./marketo-auth.md) document om uw referenties op te halen.

## Adobe-organisatietoewijzing instellen

Voordat u toewijzingssets kunt maken voor [!DNL Marketo], moet u eerst Adobe Organisatie-toewijzing instellen. Zie de handleiding voor gedetailleerde stappen over het voltooien van deze taak [Adobe Organisatie-toewijzing instellen voor [!DNL Marketo]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html).

## B2B-naamruimten instellen en hulpprogramma voor automatisch genereren van schema&#39;s

Gebruik vervolgens de B2B-naamruimte en het schema auto-generation hulpprogramma om de Platform-ontwikkelaarsconsole en de Postman-omgeving in te stellen. Hierdoor kunt u uw B2B-naamruimten en -schema&#39;s automatisch vullen. Voor gedetailleerde instructies raadpleegt u de handleiding op [B2B-naamruimten instellen en hulpprogramma voor automatisch genereren van schema&#39;s](./marketo-namespaces.md)

## Experience Data Model (XDM)

XDM is een openbaar gedocumenteerde specificatie die gemeenschappelijke structuren en definities verstrekt die u toestaan om gegevens van derdebronnen voor gebruik in de stroomafwaartse diensten van het Platform in te voeren.

Door te voldoen aan XDM-standaarden kunnen gegevens op uniforme wijze worden opgenomen in het ecosysteem van het Platform, waardoor het eenvoudiger wordt om gegevens te leveren en informatie te verzamelen.

Voor meer informatie over XDM en zijn rol in Platform, gelieve te zien [XDM System, overzicht](../../../../xdm/home.md).

## Veldtoewijzing van [!DNL Marketo] naar XDM

Een bronverbinding tot stand brengen tussen [!DNL Marketo] en Platform, moeten de de brongegevensgebieden van Marketo aan hun aangewezen doelXDM gebieden worden in kaart gebracht alvorens in Platform wordt opgenomen.

Zie het volgende voor gedetailleerde informatie over de regels voor het in kaart brengen van velden tussen [!DNL Marketo] gegevenssets en Platform:

* [Activiteiten](../mapping/marketo.md#activities)
* [Programma&#39;s](../mapping/marketo.md#programs)
* [Lidmaatschap van programma](../mapping/marketo.md#program-memberships)
* [Bedrijven](../mapping/marketo.md#companies)
* [Statische lijsten](../mapping/marketo.md#static-lists)
* [Statische lijstlidmaatschap](../mapping/marketo.md#static-list-memberships)
* [Benoemde accounts](../mapping/marketo.md#named-accounts)
* [Kansen](../mapping/marketo.md#opportunities)
* [Contactrollen opportunity](../mapping/marketo.md#opportunity-contact-roles)
* [Personen](../mapping/marketo.md#persons)

## Verwachte vertraging van [!DNL Marketo] gegevens over Platform

In de volgende tabel wordt de verwachte vertraging voor het introduceren weergegeven [!DNL Marketo] gegevens in Platform, gebaseerd op de aard van de inname en de gewenste bestemming:

| Bestemming | Verwachte vertraging |
| ----------- | ---------------- |
| [!DNL Real-time Customer Profile] | &lt; 1 minuut |
| Data Lake | &lt; 60 minuten |

## Volgende stappen en extra bronnen

In de volgende documentatie vindt u meer informatie over het maken van een [!DNL Marketo] bronverbinding:

* Voor informatie over hoe u verbinding kunt maken met uw [!DNL Marketo] gegevens aan Platform, zie de zelfstudie over [Marketo-bronaansluiting maken in de gebruikersinterface](../../../tutorials/ui/create/adobe-applications/marketo.md).
* Voor informatie over de onderliggende opstelling voor B2B namespaces en schema&#39;s die met worden gebruikt [!DNL Marketo], zie de documentatie voor [B2B-naamruimten en -schema&#39;s](./marketo-namespaces.md).
* Voor informatie over het zoeken naar uw [!DNL Marketo] munchkin-id en het genereren van uw referenties raadpleegt u de [[!DNL Marketo] verificatiegids](./marketo-auth.md).
* Voor informatie over de specifieke toewijzingsregels die van toepassing zijn op [!DNL Marketo] datasets, zie de documentatie over [[!DNL Marketo] veldtoewijzingen](../mapping/marketo.md).
* Voor algemene informatie over [!DNL Real-time Customer Data Platform B2B Edition] en de bijbehorende functies, raadpleegt u de documentatie over [[!DNL Real-time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).

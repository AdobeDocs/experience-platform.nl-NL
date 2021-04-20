---
keywords: Experience Platform;thuis;populaire onderwerpen;Marketo Engage;marketo engageren;marketo
solution: Experience Platform
title: Marketo Engage-aansluiting
topic: overzicht
description: Dit document verstrekt een overzicht van de Marketo Engage bronschakelaar, met inbegrip van informatie over zijn authentificatie, afbeelding, en gegevenslatentie.
translation-type: tm+mt
source-git-commit: 2563b413ec35cb4c5f05a54bce6f7271917e51f3
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---


# (Bèta) [!DNL Marketo Engage]-connector

>[!IMPORTANT]
>
>De bron [!DNL Marketo Engage] bevindt zich momenteel in bèta. De kenmerken en de documentatie van het programma kunnen worden gewijzigd.

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de services van het Platform. U kunt gegevens van diverse bronnen, zoals Adobe-toepassingen, cloudopslag, databases en vele andere, invoeren.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) (hierna &quot;[!DNL Marketo]&quot; genoemd) is een volledige oplossing voor het beheer van lood en B2B-marketers die de ervaringen van klanten willen transformeren door zich in elke fase van complexe koopreizen te engageren.

Met de [!DNL Marketo] bronschakelaar, kunt u B2B gegevens van [!DNL Marketo] brengen aan Platform en deze gegevens bijgewerkt houden gebruikend Platform-verbonden toepassingen.

Dit document verstrekt een overzicht van de [!DNL Marketo] bronschakelaar, met inbegrip van informatie over hoe te om de schakelaar voor authentiek te verklaren, hoe te om [!DNL Marketo] gebieden aan het Model van Gegevens van de Ervaring (XDM) in kaart te brengen, en de gegevenslatentie van de schakelaar.

## Verifieer uw [!DNL Marketo] schakelaar

Als u [!DNL Marketo] wilt verbinden met een Platform, moet u eerst waarden ophalen voor `munchkinId`, `clientId` en `clientSecret`.

Zie de stappen die worden beschreven in het [Marketo-bronconnector](./marketo-auth.md)-document verifiëren om uw referenties op te halen.

## Experience Data Model (XDM)

XDM is een openbaar gedocumenteerde specificatie die gemeenschappelijke structuren en definities verstrekt die u toestaan om gegevens van derdebronnen voor gebruik in de stroomafwaartse diensten van het Platform in te voeren.

Door te voldoen aan XDM-standaarden kunnen gegevens op uniforme wijze worden opgenomen in het ecosysteem van het Platform, waardoor het eenvoudiger wordt om gegevens te leveren en informatie te verzamelen.

Voor meer informatie over XDM en zijn rol in Platform, gelieve te zien [XDM systeemoverzicht](../../../../xdm/home.md).

## Veldtoewijzing van [!DNL Marketo] naar XDM

Om een bronverbinding tussen [!DNL Marketo] en Platform te vestigen, moeten de de brongegevensgebieden van Marketo aan hun aangewezen doelXDM gebieden worden in kaart gebracht alvorens in Platform wordt opgenomen.

Zie het volgende voor gedetailleerde informatie over de regels van de gebiedstoewijzing tussen [!DNL Marketo] datasets en Platform:

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

## Verwachte vertraging van [!DNL Marketo] gegevens op Platform

In de volgende tabel wordt de verwachte vertraging voor het plaatsen van [!DNL Marketo]-gegevens in het Platform weergegeven op basis van de aard van de opname en het gewenste doel:

| Bestemming | Verwachte vertraging |
| ----------- | ---------------- |
| [!DNL Real-time Customer Profile] | &lt; 1=&quot;&quot; minute=&quot;&quot;> |
| Data Lake | &lt; 60=&quot;&quot; minutes=&quot;&quot;> |

## Volgende stappen en extra bronnen

In de volgende documentatie vindt u meer informatie over het maken van een [!DNL Marketo]-bronverbinding:

* Voor informatie over hoe te om uw [!DNL Marketo] gegevens aan Platform aan te sluiten, zie de zelfstudie over [het creëren van een bron van Marketo schakelaar in UI](../../../tutorials/ui/create/adobe-applications/marketo.md).
* Voor informatie over de onderliggende opstelling voor B2B namespaces en schema&#39;s die met [!DNL Marketo] worden gebruikt, zie de documentatie voor [B2B namespaces en schema&#39;s](./marketo-namespaces.md).
* Raadpleeg de [[!DNL Marketo] verificatiegids](./marketo-auth.md) voor informatie over het zoeken naar uw [!DNL Marketo]-insteekmodule en het genereren van uw referenties.
* Voor informatie over de specifieke toewijzingsregels die op [!DNL Marketo] datasets van toepassing zijn, zie de documentatie over [[!DNL Marketo] gebiedsafbeeldingen](../mapping/marketo.md).
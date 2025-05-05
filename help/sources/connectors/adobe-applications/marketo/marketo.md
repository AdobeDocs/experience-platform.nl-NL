---
keywords: Experience Platform;home;populaire onderwerpen;Marketo Engage;Marketo engageren;Marketo
solution: Experience Platform
title: Marketo Engage-connector
description: Dit document biedt een overzicht van de Marketo Engage-bronconnector, inclusief informatie over verificatie, toewijzing en gegevenslatentie.
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 0%

---

# [!DNL Marketo Engage] -connector

>[!IMPORTANT]
>
>U kunt nu de [!DNL Marketo Engage] -bron gebruiken wanneer u Adobe Experience Platform uitvoert op Amazon Web Services (AWS). Experience Platform die op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Meer over de gesteunde infrastructuur van Experience Platform leren, zie het [ multi-wolkenoverzicht van Experience Platform ](../../../../landing/multi-cloud.md).

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen en biedt u de mogelijkheid om inkomende gegevens te structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, opslag in de cloud, databases en vele andere.

[[!DNL Marketo Engage] ](https://www.marketo.com/software/) is een volledige oplossing voor loodbeheer en B2B marketers die klantenervaringen willen omzetten door over elke fase van complexe het kopen reizen in dienst te nemen.

Met de [!DNL Marketo Engage] bronconnector kunt u B2B-gegevens van [!DNL Marketo Engage] naar Experience Platform overbrengen en deze gegevens up-to-date houden met Experience Platform-aangesloten toepassingen.

>[!IMPORTANT]
>
>U moet toegang tot [ Adobe Real-Time Customer Data Platform B2B edition ](../../../../rtcdp/b2b-overview.md) hebben om alle datasets van Marketo voor segmentatie met het [ Real-Time Profiel van de Klant ](../../../../profile/home.md) te gebruiken. Zonder Real-Time CDP B2B edition kunt u nog steeds de Marketo-bron gebruiken om gegevens van de personen- en activiteitengegevenssets over te brengen naar het realtime-klantprofiel voor segmentatie.

Dit document verstrekt een overzicht van de [!DNL Marketo Engage] bronschakelaar, met inbegrip van informatie over hoe te om de schakelaar voor authentiek te verklaren, hoe te om [!DNL Marketo Engage] gebieden aan het Model van de Gegevens van de Ervaring (XDM) in kaart te brengen, en de gegevenslatentie van de schakelaar.

## Toewijzing Adobe-organisatie instellen

Voordat u toewijzingssets kunt maken voor [!DNL Marketo Engage] , moet u eerst Adobe Organisatie Mapping instellen. Voor gedetailleerde stappen op hoe te om dit te voltooien, zie de gids bij [ vestiging de Toewijzing van de Organisatie van Adobe voor  [!DNL Marketo Engage] ](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html?lang=nl-NL).

## Verifieer uw [!DNL Marketo Engage] -connector

Als u [!DNL Marketo Engage] wilt verbinden met Experience Platform, moet u eerst waarden voor de `munchkinId` , `clientId` en `clientSecret` ophalen.

Zie de stappen die in [ worden geschetst verifieer uw van de bron Marketo schakelaar ](./marketo-auth.md) document om uw geloofsbrieven terug te winnen.

## B2B-naamruimten instellen en hulpprogramma voor automatisch genereren van schema&#39;s

Gebruik vervolgens de B2B-naamruimte en het schema auto-generation hulpprogramma om de Experience Platform-ontwikkelaarsconsole en de Postman-omgeving in te stellen. Hierdoor kunt u uw B2B-naamruimten en -schema&#39;s automatisch vullen. Voor gedetailleerde instructies, zie de gids bij [ vestiging uw B2B namespaces en schema auto-generatienut ](./marketo-namespaces.md)

## Experience-datamodel (XDM)

XDM is een openbaar gedocumenteerde specificatie die gemeenschappelijke structuren en definities verstrekt die u toestaan om gegevens van derdebronnen voor gebruik in de stroomafwaartse diensten van Experience Platform in te voeren.

Door te voldoen aan XDM-standaarden kunnen gegevens op uniforme wijze worden opgenomen in het ecosysteem van Experience Platform, waardoor het eenvoudiger wordt om gegevens te leveren en informatie te verzamelen.

Meer over XDM en zijn rol in Experience Platform leren, gelieve te zien het [ XDM overzicht van het Systeem ](../../../../xdm/home.md).

## Veldtoewijzing van [!DNL Marketo Engage] naar XDM

Om een bronverbinding tussen [!DNL Marketo Engage] en Experience Platform tot stand te brengen, moeten de de brongegevensgebieden van Marketo aan hun aangewezen doelXDM gebieden worden in kaart gebracht alvorens in Experience Platform wordt opgenomen.

Zie het volgende voor meer informatie over de regels voor veldmapping tussen [!DNL Marketo Engage] datasets en Experience Platform:

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

## Verwachte vertraging van [!DNL Marketo Engage] gegevens op Experience Platform

In de volgende tabel wordt de verwachte vertraging voor het plaatsen van [!DNL Marketo Engage] -gegevens naar Experience Platform weergegeven, op basis van de aard van de opname en het gewenste doel:

| Bestemming | Verwachte vertraging |
| ----------- | ---------------- |
| [!DNL Real-Time Customer Profile] | &lt; 10 minuten |
| Gegevensmeer | &lt; 60 minuten |

>[!NOTE]
>
>Bovenstaande latentiecijfers vertegenwoordigen verwachtingen met een betrouwbaarheid van 95%. De werkelijke latentie zal variëren en kan in zeldzame gevallen 50% groter zijn dan deze cijfers.

## Volgende stappen en extra bronnen

In de volgende documentatie vindt u meer informatie over het maken van een [!DNL Marketo Engage] bronverbinding:

* Voor informatie over hoe te om uw [!DNL Marketo Engage] gegevens met Experience Platform te verbinden, leest het leerprogramma op [ het creëren van a  [!DNL Marketo Engage]  bronverbinding in UI ](../../../tutorials/ui/create/adobe-applications/marketo.md).
   * Voor informatie over hoe te opstelling uw schema&#39;s en de gegevens van de douaneactiviteit in te voeren, leest het leerprogramma op [ creërend een bronverbinding en dataflow voor  [!DNL Marketo Engage]  gegevens van de douaneactiviteit ](../../../tutorials/ui/create/adobe-applications/marketo-custom-activities.md)
   * Voor informatie over hoe te om uw afbeelding ECID van de [!DNL Person] dataset aan de [!DNL Activity] dataset te migreren, lees de [ ECID de Gids van de kaartmigratie ](./migration.md).
* Voor informatie over de onderliggende opstelling voor B2B namespaces en schema&#39;s die met [!DNL Marketo Engage] worden gebruikt, lees de documentatie voor [ B2B namespaces en schema&#39;s ](./marketo-namespaces.md).
* Voor informatie bij het vinden van uw [!DNL Marketo Engage] munchkin identiteitskaart en het produceren van uw geloofsbrieven, lees de [[!DNL Marketo Engage]  authentificatiegids ](./marketo-auth.md).
* Voor informatie over de specifieke kaartregels die op [!DNL Marketo Engage] datasets van toepassing zijn, lees de documentatie over [[!DNL Marketo Engage]  gebiedsafbeeldingen ](../mapping/marketo.md).
* Lees de documentatie bij [[!DNL Real-Time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md) voor algemene informatie over [!DNL Real-Time Customer Data Platform B2B Edition] en de bijbehorende functies.

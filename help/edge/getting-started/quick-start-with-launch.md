---
title: Snel starten met starten
seo-title: Adobe Experience Platform Web SDK snel aan de slag met Starten
description: Snelle startgids voor het gebruiken van de uitbreiding van SDK van het Platform van de Ervaring om gegevens te verzamelen
seo-description: Snelle startgids voor het gebruiken van de uitbreiding van SDK van het Platform van de Ervaring om gegevens te verzamelen
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---


# Welkom

In deze handleiding wordt uitgelegd hoe u de Adobe Experience Platform Web SDK in Launch instelt. Als u deze functie wilt gebruiken, moet u een whitelist hebben. Als u op de wachtlijst wilt krijgen gelieve uw CSM te bereiken.

- Heb een [1st-partijdomein (CNAME)](https://docs.adobe.com/content/help/en/core-services/interface/ec-cookies/cookies-first-party.html) toegelaten. Als u al een CNAME voor Analytics hebt, zou u dat moeten gebruiken. Testen in ontwikkeling werkt zonder CNAME, maar u hebt er een nodig voordat u naar productie gaat
- U kunt gebruikmaken van het Adobe Experience Platform Data Platform. Als u geen platform hebt gekocht, zullen wij u van de Stichting van de Diensten van de Gegevens van het Platform van de Ervaring voor gebruik met SDK voorzien.
- Gebruik de nieuwste versie van de service Bezoeker-id

## Een configuratie-id maken

U kunt een configuratie-id maken met het gereedschap [](../fundamentals/edge-configuration.md) Edge-configuratie tijdens het opstarten. Hierdoor kunt u het Edge-netwerk inschakelen om gegevens naar de verschillende oplossingen te verzenden. Nadere informatie over het vinden van elke optie vindt u in de pagina [Edge Configuration Tool](../fundamentals/edge-configuration.md) .

>Opmerking: Uw organisatie moet voor de eigenschap worden gewhitelisteerd. Neem contact op met uw CSM om op de lijst te komen voor eventuele whitelisting.

## Een schema voorbereiden

Het Edge Network van het Platform van de Ervaring neemt gegevens als XDM. XDM is een gegevensformaat dat u schema&#39;s laat bepalen. Het schema bepaalt hoe het Netwerk van de Rand verwacht dat de gegevens worden geformatteerd. Om gegevens te verzenden zult u uw schema moeten bepalen.

- [Een schema maken](../../xdm/tutorials/create-schema-ui.md)
- Voeg de Adobe Experience Platform Web SDK-mix toe aan het schema dat u hebt gemaakt

## SDK installeren in Launch

Meld u aan bij Starten en installeren van de `AEP Web SDK` extensie. Als onderdeel van de installatie van de SDK wordt u gevraagd om de extensie te configureren. Voer de configuratie-id in die u hierboven hebt aangevraagd. De extensie vult automatisch uw organisatie-id in.

Voor meer details over verschillende configuratieopties, zie het [Vormen SDK](../fundamentals/configuring-the-sdk.md).

## Een gegevenselement maken op basis van uw schema

In lancering creeer een Element van Gegevens dat verwijzingen het schema door de uitbreiding in het Web SDK van AEP te veranderen en het type aan Object XDM te plaatsen. Hierdoor wordt uw schema geladen en kunt u gegevenselementen toewijzen in verschillende delen van het schema.

![Date-element in Launch](../../assets/edge_data_element.png)

## Een gebeurtenis verzenden

Nadat de extensie is geïnstalleerd, begint u gebeurtenissen te verzenden door een actie &quot;sendEvent&quot; van de SDK-extensie van AEP Web toe te voegen aan een regel. Vergeet niet het gegevenselement dat u net als de XDM-gegevens aan de gebeurtenis hebt gemaakt, toe te voegen. We raden u aan ten minste één gebeurtenis te verzenden telkens wanneer een pagina wordt geladen.

Zie Gebeurtenissen [bijhouden voor meer informatie over het bijhouden van gebeurtenissen](../fundamentals/tracking-events.md).

## Volgende stappen

Zodra u gegevens hebt die stromen kunt u het volgende doen.

- [Uw schema samenstellen](https://docs.adobe.com/content/help/en/experience-platform/xdm/schema/composition.html)
- Leer hoe u de ervaring kunt [aanpassen](../fundamentals/rendering-personalization-content.md)
- Meer informatie over het verzenden van gegevens naar meerdere oplossingen
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe-doel](../solution-specific/target/target-overview.md)

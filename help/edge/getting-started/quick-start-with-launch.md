---
title: Snel starten met starten
seo-title: Snelle start met Adobe Experience Platform Web SDK bij starten
description: Snelle startgids voor het gebruiken van de uitbreiding van SDK van het Platform van de Ervaring om gegevens te verzamelen
seo-description: Snelle startgids voor het gebruiken van de uitbreiding van SDK van het Platform van de Ervaring om gegevens te verzamelen
translation-type: tm+mt
source-git-commit: dc5ee796ca390d06fc8e08bd6c30e88a0d96dd53
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---


# Welkom

Deze gids zal u door de verschillende stappen op hoe te opstelling de SDK van het Web van Adobe Experience Platform in Lancering nemen. Als u deze functie wilt kunnen gebruiken, moet u beschikken over machtigingen en in de lijst Toestaan staan. Als u op de wachtlijst wilt krijgen gelieve uw CSM te bereiken.

- Heb een [1st-partijdomein (CNAME)](https://docs.adobe.com/content/help/en/core-services/interface/ec-cookies/cookies-first-party.html) toegelaten. Als u al een CNAME voor Analytics hebt, zou u dat moeten gebruiken. Testen in ontwikkeling werkt zonder CNAME, maar u hebt er een nodig voordat u naar productie gaat
- recht hebben op het Adobe Experience Platform-gegevensplatform. Als u Platform niet hebt aangeschaft, zullen wij u van de Stichting van de Diensten van de Gegevens van het Platform van de Ervaring voor gebruik op een beperkte manier met SDK zonder extra kosten voorzien.
- Gebruik de nieuwste versie van de service Bezoeker-id

## Een configuratie-id maken

U kunt een configuratie-id maken met het gereedschap [](../fundamentals/edge-configuration.md) Edge-configuratie tijdens het opstarten. Hierdoor kunt u het Edge-netwerk inschakelen om gegevens naar de verschillende oplossingen te verzenden. Nadere informatie over het vinden van elke optie vindt u in de pagina [Edge Configuration Tool](../fundamentals/edge-configuration.md) .

>[!NOTE]
>
>Uw organisatie moet in de lijst met toegestane items staan voor de functie. Neem contact op met uw CSM om de lijst voor toestaan weer te geven.

## Een schema voorbereiden

Het Edge Network van het Platform van de Ervaring neemt gegevens als XDM. XDM is een gegevensformaat dat u schema&#39;s laat bepalen. Het schema bepaalt hoe het Netwerk van de Rand verwacht dat de gegevens worden geformatteerd. Om gegevens te verzenden zult u uw schema moeten bepalen.

- [Een schema maken](../../xdm/tutorials/create-schema-ui.md)
- Voeg de mix van de SDK van Adobe Experience Platform Web toe aan het schema dat u hebt gemaakt

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
- [Meer informatie over foutopsporing](../fundamentals/debugging.md)
- Leer hoe u de ervaring kunt [aanpassen](../fundamentals/rendering-personalization-content.md)
- Meer informatie over het verzenden van gegevens naar meerdere oplossingen
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)

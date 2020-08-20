---
title: Snel starten met starten
seo-title: Snelle start met Adobe Experience Platform Web SDK bij starten
description: Snelle startgids voor het gebruiken van de uitbreiding van SDK van het Web van het Experience Platform om gegevens te verzamelen
seo-description: Snelle startgids voor het gebruiken van de uitbreiding van SDK van het Web van het Experience Platform om gegevens te verzamelen
keywords: 1st-party domain;CNAME;schema;create schema;launch;aep web sdk extension;extension;configuration id;configuration tool;data element;create data element;XDM Object;sendEvent;send Event;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 1%

---


# Welkom

Deze handleiding leidt u door de verschillende manieren om de Adobe Experience Platform Web SDK in te stellen bij Starten. Als u deze functie wilt gebruiken, moet u een whitelist hebben. Neem contact op met uw CSM als u op de wachtlijst wilt staan.

- Heb een [1st-partijdomein (CNAME)](https://docs.adobe.com/content/help/en/core-services/interface/ec-cookies/cookies-first-party.html) toegelaten. Als u al een CNAME voor Analytics hebt, zou u dat moeten gebruiken. Het testen in ontwikkeling werkt zonder CNAME, maar u hebt er een nodig voordat u naar productie gaat.
- Mag Adobe Experience Platform gebruiken. Als u geen Platform hebt gekocht, zal Adobe u van de Stichting van de Diensten van de Gegevens van het Experience Platform voor gebruik op een beperkte manier met SDK zonder extra kosten voorzien.
- Gebruik de nieuwste versie van de service Bezoeker-id.

## Een schema voorbereiden

Het Netwerk van de Rand van het Experience Platform neemt gegevens als XDM. XDM is een gegevensformaat dat u schema&#39;s laat bepalen. Het schema bepaalt hoe het Netwerk van de Rand verwacht dat de gegevens worden geformatteerd. Als u gegevens wilt verzenden, moet u het schema definiëren.

1. [Een schema maken](../../xdm/tutorials/create-schema-ui.md)
2. Voeg de AEP- [!DNL Web SDK ExperienceEvent] mix toe aan het schema dat u hebt gemaakt.
3. Creeer een Dataset van het schema u creeerde.

De volgende video is bedoeld om u in het creëren van een schema, dataset, en het stromen bronschakelaar voor uw [!DNL Web SDK] gegevens te steunen.


>[!VIDEO](https://video.tv.adobe.com/v/35395?quality=12&learn=on)

Meld u aan bij Starten en installeren van de `AEP Web SDK` extensie. Wanneer u de SDK installeert, wordt u gevraagd om de extensie te configureren. Voer de configuratie-id in die u hierboven hebt aangevraagd. De extensie vult automatisch uw organisatie-id in.


Voor meer details over verschillende configuratieopties, zie het [Vormen SDK](../fundamentals/configuring-the-sdk.md).

## Een configuratie-id maken

U kunt een configuratie-id maken met het gereedschap [](../fundamentals/edge-configuration.md) Edge-configuratie in Launch. Dit staat u toe om het Netwerk van de Rand toe te laten om gegevens naar de diverse oplossingen te verzenden. Nadere informatie over het vinden van elke optie vindt u in de pagina [Edge Configuration Tool](../fundamentals/edge-configuration.md) .

>[!NOTE]
>
>Voor deze functie moet een whitelist zijn voor uw organisatie. Neem contact op met uw CSM om op de lijst te komen voor eventuele whitelisting.

## Een gegevenselement maken op basis van uw schema

In Lancering, creeer een Element van Gegevens dat verwijzingen het schema door de uitbreiding in het Web SDK van AEP te veranderen en het type te plaatsen aan `XDM Object`. Dit laadt uw schema en staat u toe om gegevenselementen in verschillende delen van het schema in kaart te brengen.

![Date-element in Launch](../../assets/edge_data_element.png)

## Een gebeurtenis verzenden

Nadat de uitbreiding wordt geïnstalleerd, begin gebeurtenissen te verzenden door een `sendEvent` actie van de uitbreiding van SDK van het Web van AEP aan een regel toe te voegen. Voeg het gegevenselement toe u enkel aan de gebeurtenis als XDM gegevens creeerde. Adobe raadt u aan ten minste één gebeurtenis te verzenden telkens wanneer een pagina wordt geladen.

Zie Gebeurtenissen [bijhouden voor meer informatie over het bijhouden van gebeurtenissen](../fundamentals/tracking-events.md).

## Volgende stappen

Nadat u gegevens hebt laten stromen, kunt u het volgende doen.

- [Uw schema samenstellen](https://docs.adobe.com/content/help/en/experience-platform/xdm/schema/composition.html)
- [Meer informatie over foutopsporing](../fundamentals/debugging.md)
- Leer hoe u de ervaring kunt [aanpassen](../fundamentals/rendering-personalization-content.md)
- Meer informatie over het verzenden van gegevens naar meerdere oplossingen
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)

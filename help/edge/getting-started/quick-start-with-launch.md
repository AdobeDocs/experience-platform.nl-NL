---
title: Snel starten met starten
seo-title: Adobe Experience Platform Web SDK snel starten met starten
description: Snelle startgids voor het gebruiken van de uitbreiding van SDK van het Web van het Experience Platform om gegevens te verzamelen
seo-description: Snelle startgids voor het gebruiken van de uitbreiding van SDK van het Web van het Experience Platform om gegevens te verzamelen
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 1%

---


# Welkom

In deze handleiding worden de verschillende stappen beschreven voor het instellen van het Adobe Experience Platform [!DNL Web SDK] in Adobe Launch. U moet over toestemmingen beschikken en op de lijst van gewenste personen zijn om deze eigenschap te gebruiken. Neem contact op met uw CSM als u op de wachtlijst wilt staan. Als u deze functie wilt gebruiken, moet u bovendien:

- Heb een [1st-partijdomein (CNAME)](https://docs.adobe.com/content/help/en/core-services/interface/ec-cookies/cookies-first-party.html) toegelaten. Als u al een CNAME voor Adobe Analytics hebt, moet u die gebruiken. Testen in ontwikkeling werkt zonder CNAME, maar u hebt er een nodig voordat u naar productie gaat
- Gebruik de nieuwste versie van de service Bezoeker-id

## Een configuratie-id maken

U kunt een configuratie-id maken met het gereedschap [](../fundamentals/edge-configuration.md) Edge-configuratie in Adobe Launch. Hierdoor kunt u het Edge-netwerk inschakelen om gegevens naar de verschillende oplossingen te verzenden. Zie de pagina van het Hulpmiddel [van de Configuratie van de](../fundamentals/edge-configuration.md) Rand voor details op hoe te om elke optie te vinden.

>[!NOTE]
>
>Uw organisatie moet op de lijst van gewenste personen voor de eigenschap zijn. Neem contact op met uw CSM om aan de lijst van gewenste personen te worden toegevoegd.

## Een schema voorbereiden

De [!DNL Experience Platform Edge Network] gegevens worden als XDM gebruikt. XDM is een gegevensformaat dat u schema&#39;s laat bepalen. Het schema bepaalt hoe de gegevens [!DNL Edge Network] verwacht worden geformatteerd. Om gegevens te verzenden zult u uw schema moeten bepalen. Controleer of u het volgende hebt voltooid:

1. [Een schema maken](../../xdm/tutorials/create-schema-ui.md)
2. Voeg de AEP- [!DNL Web SDK ExperienceEvent] mix toe aan het schema dat u hebt gemaakt.
3. Creeer een Dataset van het schema u creeerde.

De volgende video is bedoeld om u in het creëren van een schema, dataset, en het stromen bronschakelaar voor uw [!DNL Web SDK] gegevens te steunen.

>[!VIDEO](https://video.tv.adobe.com/v/35395?quality=12&learn=on)

## SDK installeren in Adobe Launch

Meld u aan bij Adobe Launch en installeer de `AEP Web SDK` extensie. Als onderdeel van de installatie van de SDK wordt u gevraagd om de extensie te configureren. Voer de configuratie-id in die u hierboven hebt aangevraagd. De extensie vult automatisch uw organisatie-id in.

Voor meer details over verschillende configuratieopties, zie het [Vormen SDK](../fundamentals/configuring-the-sdk.md).

## Een gegevenselement maken op basis van uw schema

Maak in Adobe Launch een gegevenselement dat naar het schema verwijst door de extensie te wijzigen in AEP [!DNL Web SDK] en het type in te stellen op XDM Object. Hierdoor wordt uw schema geladen en kunt u gegevenselementen toewijzen in verschillende delen van het schema.

![Date-element in Launch](../../assets/edge_data_element.png)

## Een gebeurtenis verzenden

Nadat de extensie is geïnstalleerd, begint u met het verzenden van gebeurtenissen door een actie &quot;sendEvent&quot; van de AEP- [!DNL Web SDK] extensie toe te voegen aan een regel. Vergeet niet het gegevenselement dat u net als de XDM-gegevens aan de gebeurtenis hebt gemaakt, toe te voegen. We raden u aan ten minste één gebeurtenis te verzenden telkens wanneer een pagina wordt geladen.

Zie Gebeurtenissen [bijhouden voor meer informatie over het bijhouden van gebeurtenissen](../fundamentals/tracking-events.md).

## Volgende stappen

Zodra u gegevens hebt die stromen kunt u het volgende doen:

- [Uw schema samenstellen](https://docs.adobe.com/content/help/en/experience-platform/xdm/schema/composition.html)
- [Meer informatie over foutopsporing](../fundamentals/debugging.md)
- Leer hoe u de ervaring kunt [aanpassen](../fundamentals/rendering-personalization-content.md)
- Meer informatie over het verzenden van gegevens naar meerdere oplossingen
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)

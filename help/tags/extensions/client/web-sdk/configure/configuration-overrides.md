---
title: Instellingen voor gegevensstroomconfiguratie overschrijven
description: Wijzig configuratie-instellingen wanneer aan bepaalde voorwaarden wordt voldaan.
exl-id: 68227148-3d74-4807-836c-14acd8a9c1dc
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 2%

---

# Instellingen voor gegevensstroomconfiguratie overschrijven {#config-overrides}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_overrides"
>title="DataStream-configuratieoverschrijvingen"
>abstract="U kunt voorwaardelijk verschillende gegevensstroomgedragingen activeren zonder een aparte gegevensstroom te vereisen. Het plaatsen van om het even welke cliënt-zijgegevensstroomconfiguratie treedt voor een milieu in deze sectie met voeten om het even welke server-zijdynamische gegevensstroomconfiguratie en regels voor dat milieu."

Met DataStream-overschrijvingen kunt u aanvullende configuraties voor uw gegevensstreams definiëren. Deze configuraties worden via de Web SDK aan de Edge Network doorgegeven. Met deze functie kunt u voorwaardelijk verschillende gegevensstroomgedragingen activeren zonder een nieuwe gegevensstroom te maken of uw bestaande instellingen te wijzigen.

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Ga naar **[!UICONTROL Extensions]** en selecteer vervolgens **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.
1. Schuif omlaag naar de sectie **[!UICONTROL Datastream configuration overrides]** .

De configuratieopheffing van gegevensstroom is een proces in twee stappen:

1. Eerst, moet u uw de configuratieopheffing van de gegevensstroom bepalen wanneer [ vormend een datastream ](/help/datastreams/configure.md) in de UI van Gegevensstromen. Zie [ de configuratie DataStream met voeten treedt ](/help/datastreams/overrides.md) in de documentatie van gegevensstromen voor instructies op hoe te om met voeten te treden.
1. Nadat u de gegevensstroomoverschrijving in de gegevensstreams UI hebt gevormd, kunt u de markeringsuitbreiding vormen.

DataStream-overschrijvingen moeten per omgeving worden geconfigureerd. De ontwikkelings-, staging- en productieomgevingen hebben allemaal verschillende overschrijvingen. U kunt de overschrijvingsinstellingen kopiëren naar elke gewenste omgeving:

![ Beeld dat de configuratie van de gegevensstroom toont treedt het gebruiken van de de markeringsuitbreidingspagina van SDK van het Web met voeten.](../assets/datastream-overrides.png)

Standaard zijn overschrijvingen van gegevensstroomconfiguraties uitgeschakeld. De optie **[!UICONTROL Match datastream configuration]** is standaard geselecteerd.

![ SDK van het Web de gebruikersinterface van de markeringsuitbreiding die de configuratie van de gegevensstroom toont treedt gebrek het plaatsen met voeten.](../assets/datastream-override-default.png)

Als u gegevensstroomoverschrijvingen wilt inschakelen in de tagextensie, selecteert u **[!UICONTROL Enabled]** in het keuzemenu.

![ SDK van het Web de gebruikersinterface van de markeringsuitbreiding die de configuratie van de gegevensstroom toont treedt Toegelaten het plaatsen met voeten.](../assets/datastream-override-enabled.png)

Nadat u de gegevensstroomconfiguratie met voeten treedt, kunt u de overschrijvingen voor elke hieronder beschreven dienst vormen. Deze gegevensstroom treedt montages met voeten om het even welke server-zijgegevensstroomconfiguraties en regels voor het geselecteerde milieu.

## Adobe Analytics

De gegevens met voeten treden die aan de dienst van Adobe Analytics verpletteren.

{het beeld van de de marktextensie UI van SDK van het 0} Web die de montages van de de gegevensstroom van Adobe Analytics met voeten treedt.![](../assets/datastream-override-analytics.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]** : schakel gegevensroutering naar Adobe Analytics in of uit.
* **[!UICONTROL Report suites]**: De id&#39;s voor de bestemmingsrapportsuites in Adobe Analytics. De waarde moet een vooraf geconfigureerde rapportsuite (of een door komma&#39;s gescheiden lijst met rapportsuites) van uw gegevensstroomconfiguratie zijn. Deze instelling overschrijft de primaire rapportsuites.
* **[!UICONTROL Add Report Suite]**: selecteer deze optie om extra rapportsuites toe te voegen.

## Adobe Audience Manager

Overschrijf gegevens die naar Adobe Audience Manager worden verzonden.

{het beeld van de de marktextensie UI van SDK van het 0} Web die de montages van de de gegevensstroom van Adobe Audience Manager met voeten treedt.![](../assets/datastream-override-audience-manager.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]** : schakel gegevensroutering naar Adobe Audience Manager in of uit.
* **[!UICONTROL Third-party ID sync container]**: De id voor de synchronisatiecontainer van de doel-id van derden in Audience Manager. De waarde moet een preconfigured secundaire container van uw gegevensstroomconfiguratie zijn en treedt de primaire container met voeten.

## Adobe Experience Platform

Overschrijf gegevens die naar Adobe Experience Platform worden verzonden.

{het beeld van de de marktextensie UI van SDK van het 0} Web die de montages van de de gegevensstroom van Adobe Experience Platform met voeten treedt.![](../assets/datastream-override-experience-platform.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]** : schakel gegevensroutering naar Adobe Experience Platform in of uit.
* **[!UICONTROL Event dataset]**: De id voor de gegevensset met doelgebeurtenissen in de Adobe Experience Platform. De waarde moet een preconfigured secundaire dataset van uw configuratie van de gegevensstroom zijn.
* **[!UICONTROL Offer Decisioning]**: schakel gegevensroutering naar de [!DNL Offer Decisioning] -service in of uit.
* **[!UICONTROL Edge Segmentation]**: schakel gegevensroutering naar de [!DNL Edge Segmentation] -service in of uit.
* **[!UICONTROL Personalization Destinations]**: laat of maak gegevens toe onbruikbaar verpletterend aan verpersoonlijkingsbestemmingen.
* **[!UICONTROL Adobe Journey Optimizer]**: schakel gegevensroutering naar [!DNL Adobe Journey Optimizer] in of uit.

## Adobe Server-Side Event Forwarding

Overschrijf gegevens die naar de Adobe Server-Side Event Forwarding service routeren.

{het beeld van de de markeringsuitbreiding UI van SDK van het 0} Web die de Server-zij Gebeurtenis toont die van Adobe gegevensstroom met voeten treedt montages.![](../assets/datastream-override-ssf.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]**: schakel gegevensroutering naar de Adobe Server-Side Event Forwarding-service in of uit.

## Adobe Target {#target}

Overschrijf gegevens die naar Adobe Target worden verzonden.

{het beeld van de de marktextensie UI van SDK van het 0} Web die de montages van de de gegevensstroom van Adobe Target met voeten treedt.![](../assets/datastream-override-target.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]** : schakel gegevensroutering naar Adobe Target in of uit.

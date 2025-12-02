---
title: Aan de slag met de webextensie SDK
description: Verzend gebeurtenisgegevens naar de Adobe Experience Platform Edge Network met de Web SDK-tagextensie.
exl-id: 01ddbb19-40bb-4cb5-bfca-b272b88008b3
source-git-commit: 8dd658c46fc92ae6d450213ab79f2766f4211c53
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 3%

---

# Aan de slag met de webextensie SDK

Het gebruik Adobe Experience Platform **markeringen** (vroeger Lancering) om gebeurtenisgegevens van uw website naar Edge Network en stroomafwaartse oplossingen van Adobe te verzenden.

Alvorens deze stappen te volgen, zorg ervoor dat u tot de volgende [ bezitsrechten ](/help/tags/ui/administration/user-permissions.md) kunt toegang hebben:

* [!UICONTROL Develop]
* [!UICONTROL Manage extensions]

Bovendien zorg ervoor dat u alle [ toestemmingen ](/help/access-control/home.md#permissions) onder de volgende categorieën hebt:

* Gegevensmodellering
* Identiteiten

## Een XDM-schema maken {#schema}

Het [ Model van de Gegevens van de Ervaring (XDM) ](/help/xdm/home.md) is een open-bronspecificatie die gemeenschappelijke structuren en definities voor gegevens in de vorm van schema&#39;s verstrekt. Het is aan te raden een schema te configureren wanneer u gegevens naar de Edge Network verzendt.

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Schemas]**.
1. Selecteer **[!UICONTROL Create schema]**.
1. Selecteer **[!UICONTROL Experience Event]** en selecteer vervolgens **[!UICONTROL Next]** .
1. Geef het schema een gewenste naam en selecteer vervolgens **[!UICONTROL Finish]** .
1. (Facultatief) kunt u meer gebieden of [ gebiedsgroepen ](/help/xdm/ui/resources/field-groups.md) voor om het even welke extra gegevens toevoegen die u wilt verzamelen.

![ het canvas van het Schema ](assets/getting-started/schema-structure.png)

>[!NOTE]\
>Zodra bewaard, staan de schema&#39;s slechts *additieve* veranderingen toe. Zie [ schemaevolutie ](/help/xdm/schema/composition.md#evolution) voor meer informatie.

## Een gegevensstroom maken {#datastream}

A [ Datastream ](/help/datastreams/overview.md) is een configuratie die Edge Network vertelt hoe te om de gegevens te behandelen die u het verzendt. Wanneer u een gegevensstroom vormt om gegevens naar een bepaald product te verzenden, gaat de gegevensstroom automatisch relevante gegevens over aan elk respectieve product op een manier die het specifieke product begrijpt.

1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Datastreams]**.
1. Selecteer **[!UICONTROL New datastream]**.
1. Geef de gegevensstroom een gewenste naam en selecteer het onlangs gemaakte schema onder **[!UICONTROL Mapping schema]** .
1. Selecteer **[!UICONTROL Save]**.

![ Lijst van Gegevensstromen ](assets/getting-started/datastreams.png)

## Een tag-eigenschap maken

Nadat u een schema en een gegevensstroom hebt gemaakt, kunt u een eigenschap voor tags maken en configureren.

1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer **[!UICONTROL New property]**.
1. Geef de eigenschap tag een gewenste naam en domein en selecteer vervolgens **[!UICONTROL Save]** .

## De extensie van de tag installeren

De Web SDK-tagextensie is geïnstalleerd op een bepaalde tag-eigenschap.

1. Navigeer naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]** > **[!UICONTROL Extensions]** .
1. Selecteer het tabblad **[!UICONTROL Catalog]**. 
1. Gebruik de zoekopdracht om de extensie **[!UICONTROL Adobe Experience Platform Web SDK]** te zoeken.
1. Selecteer de extensiekaart en selecteer vervolgens **[!UICONTROL Install]** aan de rechterkant.

![ installeer SDK ](assets/getting-started/install-sdk.png)

## De tagextensie configureren

Wanneer u de de markeringsuitbreiding van SDK van het Web installeert, wordt u automatisch genomen aan de [ pagina van de Configuratie ](configure/config-overview.md).

1. Onder de [ sectie van Gegevensstromen ](configure/datastreams.md), selecteer de gewenste gegevensstroom voor elk milieu.

Alle andere configuratie-instellingen worden voor u ingevuld of optioneel. Stel de gewenste configuratie-instellingen in en selecteer vervolgens **[!UICONTROL Save]** .

## Een gegevenselement met variabele maken

Adobe adviseert gebruikend [ Veranderlijke ](data-element-types.md#variable) gegevenselementen om de nuttige lading op te slaan die u naar Adobe wilt verzenden. XDM-objecten zijn ook beschikbare gegevenselementen, maar zijn ouder en beperkter in toepasselijke gebruiksgevallen.

1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Selecteer **[!UICONTROL Data elements]** > **[!UICONTROL Create new data element]** .
1. Geef het gegevenselement de volgende eigenschappen op de linkerzijde:
   * **[!UICONTROL Name]**: Elke gewenste naam
   * **[!UICONTROL Extension]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Data element type]**: [!UICONTROL Variable]
1. Stel de volgende eigenschappen in aan de rechterkant:
   **Variabel type**: XDM
   **[!UICONTROL Sandbox]**: De sandbox waarin u het schema hebt gemaakt
   **[!UICONTROL Schema]**: Het gewenste schema
1. Selecteer **[!UICONTROL Save]**.

## Een regel maken

Regels bepalen wanneer u iets wilt activeren of variabelen wilt instellen. Als u een regel maakt die wordt uitgevoerd wanneer de bibliotheek wordt geladen, kunt u gemakkelijk variabelen vullen die u op elke pagina een waarde wilt bevatten.

1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Selecteer **[!UICONTROL Rules]** > **[!UICONTROL Add rule]** .
1. Geef de regel een gewenste naam.
1. Selecteer het pictogram &#39;`+`&#39; naast **[!UICONTROL Events]** .
1. Geef de gebeurtenis de volgende instellingen:
   * **[!UICONTROL Extension]**: [!UICONTROL Core]
   * **[!UICONTROL Event type]**: [!UICONTROL Library loaded (page top)]
1. Selecteer **[!UICONTROL Keep changes]**.

In de bovenstaande stappen wordt het criterium onderdeel van de regel vastgelegd, dat moet worden geactiveerd zodra de bibliotheek is geladen. In de volgende stappen wordt aangegeven welke maatregelen moeten worden genomen wanneer aan die criteria wordt voldaan.

1. Selecteer het pictogram &#39;`+`&#39; naast **[!UICONTROL Actions]** .
1. Geef de actie de volgende montages op de linkerzijde:
   * **[!UICONTROL Extension]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Action type]**: [!UICONTROL Send event]
1. Stel de volgende velden rechts in:
   * **[!UICONTROL XDM]**: Het XDM-gegevenselement voor variabelen
1. Selecteer **[!UICONTROL Keep changes]**.

![ config van de Actie ](assets/getting-started/action-config.png)

## Publiceren

De eigenschap tag bevat alle componenten die nodig zijn om gegevens naar de Edge Network te verzenden.

1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Publishing flow]**.
1. Selecteer **[!UICONTROL Add library]**.
1. Geef de bibliotheek een gewenste naam. Denk aan deze naam gelijkaardig aan a commit name wanneer het werken in de software van de versiecontrole.
1. Stel het vervolgkeuzemenu voor de omgeving in op **[!UICONTROL Development]** .
1. Selecteer **[!UICONTROL Add all changed resources]**.
1. Selecteer **[!UICONTROL Save & build to Development]**.

Uw wijzigingen worden nu geïmplementeerd in uw ontwikkelomgeving.

1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Environments]**.
1. Selecteer het installatiepictogram naast de ontwikkelomgeving
1. Installeer de insluitcode in een testwebpagina op uw site.

Nadat u hebt gecontroleerd of de tag werkt in uw ontwikkelomgeving, kunt u de interface van [!UICONTROL Publishing flow] gebruiken om de bibliotheek te publiceren naar &#39;staging&#39; en uiteindelijk naar productie.

1. Voeg de uitbreiding en de regel aan a **Bibliotheek** toe, bouw het aan een **Milieu**, en installeer de ingebedde code op uw plaats.
2. Valideer met **Adobe Experience Platform Debugger**.

U hebt nu een slanke opstelling die gebeurtenissen vangt en hen naar Edge Network verzendt. U kunt uw implementatie nu verder opbouwen door velden toe te voegen aan uw schema, producten toe te voegen aan een gegevensstroom of gegevenselementen toe te voegen aan uw markeringseigenschap.

---
title: Het publiek activeren op gekrulde doelen op basis van LiveRamp-id's
type: Tutorial
description: Leer hoe u het publiek activeert van Adobe Experience Platform naar verbonden tv- en audiodoelen en andere integraties met de LiveRamp RampID.
exl-id: 37e5bab9-588f-40b3-b65b-68f1a4b868f1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 0%

---

# Het publiek activeren op gekrulde doelen op basis van LiveRamp-id&#39;s

Gebruik de Adobe Real-Time CDP-integratie met [!DNL LiveRamp] om het publiek te activeren naar een gekrulde lijst met doelen die [!DNL [LiveRamp RampID]](https://docs.liveramp.com/connect/en/interpreting-rampid,-liveramp-s-people-based-identifier.html) gebruiken voor activering, waaronder aangesloten tv- en audiodoelen, zoals de hieronder vermelde doelen.

>[!IMPORTANT]
>
>U hoeft geen LiveRamp RampID&#39;s in de Experience Platform-interface in te voeren of op welke manier dan ook te gebruiken.
>
> U kunt identiteiten van Real-Time CDP, zoals op PII-Gebaseerde herkenningstekens, bekende herkenningstekens, en douane IDs uitvoeren, zoals die in de officiële [ documentatie LiveRamp ](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers) wordt beschreven. Deze identiteiten worden dan gevolgd door [!DNL LiveRamp RampIDs] verderop in het activeringsproces.


* [[!DNL 4C Insights]](#insights)
* [[!DNL Acast]](#acast)
* [[!DNL Ampersand.tv]](#ampersand-tv)
* [[!DNL Captify]](#captify)
* [[!DNL Cardlytics]](#cardlytics)
* [[!DNL Disney (Hulu/ESPN/ABC)]](#disney)
* [[!DNL iHeartMedia]](#iheartmedia)
* [[!DNL Index Exchange]](#index-exchange)
* [[!DNL Magnite CTV Platform]](#magnite)
* [[!DNL Magnite DV+ (Rubicon Project)]](#magnite-dv)
* [[!DNL Nexxen]](#nexxen)
* [[!DNL One Fox]](#fox)
* [[!DNL Pandora]](#pandora)
* [[!DNL Reddit]](#reddit)
* [[!DNL Roku]](#roku)
* [[!DNL Spotify]](#spotify)
* [[!DNL Taboola]](#taboola)
* [[!DNL TargetSpot]](#targetspot)
* [[!DNL Teads]](#teads)
* [[!DNL WB Discovery]](#wb-discovery)

In dit artikel wordt uitgelegd welke workflow nodig is om het publiek vanuit Real-Time CDP rechtstreeks vanuit de gebruikersinterface van Real-Time CDP naar de hierboven vermelde doelen te activeren.

## Workflow voor activering {#workflow}

U activeert publiek aan verbonden TV en audiobestemmingen door een proces in twee stappen te gaan, en door [ LiveRamp - Onboarding ](../catalog/advertising/liveramp-onboarding.md) en [ LiveRamp te gebruiken - Distributie ](../catalog/advertising/liveramp-distribution.md) bestemmingen, zoals aangetoond in het beeld hieronder.

![ Diagram die het werkschema tonen voor het activeren van publiek van Real-Time CDP aan gekrulde bestemmingen, door LiveRamp.](../assets/ui/activate-curated-destinations-liveramp/workflow-diagram.png){width="1920" zoomable="yes"}

Eerst exporteert u uw publiek van Real-Time CDP naar de [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) -bestemming, als CSV-bestanden.

Nadat u het publiek hebt geëxporteerd, activeert u het publiek met de bestemming [[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md) .

>[!TIP]
>
>Met dit proces kunt u uw publiek rechtstreeks vanuit de gebruikersinterface van Real-Time CDP activeren naar doelen als [[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku) , [[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney) en meer, zonder dat u zich hoeft aan te melden bij uw [!DNL LiveRamp] -account voor activering.

### Videotutorial {#video}

Bekijk de onderstaande video voor een end-to-end uitleg van de workflow die in deze pagina wordt beschreven.

>[!VIDEO](https://video.tv.adobe.com/v/3425367)

### Stap 1: verzend uw publiek van Experience Platform naar LiveRamp, via de [!DNL LiveRamp - Onboarding] -bestemming {#onboarding}

Het eerste wat u moet doen om uw publiek aan gekromde bestemmingen te activeren die op LiveRampIDs worden gebaseerd is uw publiek van Experience Platform naar **uit te voeren.[!DNL LiveRamp]**

Dit doet u met het doel **[!DNL LiveRamp - Onboarding]** .

![ het beeld van Experience Platform UI die LiveRamp - Onboarding bestemmingskaart toont ](../assets/ui/activate-curated-destinations-liveramp/liveramp-onboarding-catalog.png)

Lees de [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) -doeldocumentatie voor meer informatie over het configureren van de [!DNL LiveRamp - Onboarding] -bestemming en het exporteren van uw publiek vanuit Experience Platform.

>[!IMPORTANT]
>
>Wanneer het uitvoeren van dossiers aan de [!DNL LiveRamp - Onboarding] bestemming, produceert Experience Platform één Csv- dossier voor elke [ identiteitskaart van het fusiebeleid ](../../profile/merge-policies/overview.md). Zie de doeldocumentatie van [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) voor gedetailleerde informatie over hoe u de gegevensexport naar LiveRamp kunt valideren.


Nadat u met succes uw publiek naar LiveRamp hebt uitgevoerd, ga aan [ stap 2 ](#distribution) verder.

>[!TIP]
>
>Alvorens aan [ stap 2 ](#distribution) te bewegen, [ bevestigt ](../catalog/advertising/liveramp-onboarding.md#exported-data) dat uw publiek met succes naar LiveRamp is uitgevoerd. Zie de documentatie bij [ controlerende bestemmingsdataflows ](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) en lees over de specifieke controledetails voor [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data).

### Stap 2: Activeer het publiek aan boord naar aangesloten tv- en audiodoelen, via de [!DNL LiveRamp - Distribution] -bestemming {#distribution}

Nadat u [ ](../catalog/advertising/liveramp-onboarding.md#exported-data) hebt bevestigd dat uw publiek met succes naar LiveRamp is uitgevoerd, is het tijd om het publiek aan uw aangewezen bestemmingen, zoals [[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku), [[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney), en meer te activeren.

U activeert het publiek (die in [ wordt uitgevoerd stap 1 ](#onboarding)) door de **[!DNL LiveRamp - Distribution]** bestemming te gebruiken.

![ het beeld van Experience Platform UI die LiveRamp toont - de bestemmingskaart van de Distributie ](../assets/ui/activate-curated-destinations-liveramp/liveramp-distribution-catalog.png)

Leren hoe te om de **[!DNL LiveRamp - Distribution]** bestemming te vormen en het publiek te activeren dat u in [ stap 1 ](#onboarding) uitvoerde, de [[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md) bestemmingsdocumentatie lezen.

>[!IMPORTANT]
>
>In de **stap van de 0} publieksselectie {van de **[!DNL LiveRamp - Distribution]**bestemming, moet u het *nauwkeurige zelfde publiek* selecteren dat u naar [ LiveRamp - Onboarding ](../catalog/advertising/liveramp-onboarding.md) bestemming in [ stap 1 ](#onboarding) hebt uitgevoerd.**

Wanneer u de **[!DNL LiveRamp - Distribution]** bestemming vormt, moet u een specifieke verbinding voor elke stroomafwaartse bestemming tot stand brengen die u (Roku, Disney, etc.) wilt gebruiken.

>[!TIP]
>
>Adobe raadt u aan de volgende notatie te gebruiken als u uw bestemming een naam geeft. `LiveRamp - Downstream Destination Name` Dit het noemen patroon helpt u snel uw bestemmingen in [ identificeren doorbladert ](../ui/destinations-workspace.md#browse) lusje van de bestemmingswerkruimte.
><br>
>Voorbeeld: `LiveRamp - Roku` .

{het schermschot van 0} Experience Platform UI die veelvoudige bestemmingen LiveRamp toont.](../assets/ui/activate-curated-destinations-liveramp/liveramp-naming.png)![

## Geëxporteerde gegevens/Gegevens valideren bij exporteren {#exported-data}

Om de succesvolle uitvoer van uw publiek naar de [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) bestemming te bevestigen, zie de documentatie over [ controlerende bestemmingsdataflows ](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) en lees over de specifieke controledetails voor [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data).

Als u wilt controleren of uw publiek correct is geactiveerd voor uw favoriete advertentieplatform (zoals Roku, Disney en anderen), meldt u zich aan bij uw account voor het doelplatform en controleert u de activeringswaarden.

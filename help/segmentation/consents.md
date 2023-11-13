---
solution: Experience Platform
title: Constante waarderen in segmenten
description: Leer hoe u de voorkeursinstellingen voor toestemming van klanten voor het verzamelen van persoonlijke gegevens en het delen van gegevens in gesegmenteerde bewerkingen naleeft.
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# Naleving van toestemming in segmenten

>[!NOTE]
>
>In deze handleiding wordt uitgelegd hoe u de inhoud van de inhoud kunt respecteren **segmentdefinities**.

Wettelijke privacyvoorschriften zoals [!DNL California Consumer Privacy Act] (CCPA) de consument het recht te geven zich te onthouden van het verzamelen of delen van persoonsgegevens met derden. Adobe Experience Platform biedt standaard XDM-componenten (Experience Data Model) die bedoeld zijn om deze voorkeuren voor toestemming van klanten vast te leggen in realtime gegevens van het klantprofiel.

Als een klant zijn toestemming voor het delen van persoonlijke gegevens heeft ingetrokken of geweigerd, is het belangrijk dat uw organisatie deze voorkeur respecteert bij het genereren van een publiek voor marketingactiviteiten. Dit document beschrijft hoe te om de waarden van de klantentoestemming in uw segmentdefinities te integreren gebruikend het gebruikersinterface van het Experience Platform.

## Aan de slag

Het naleven van de waarden voor instemming van klanten vereist inzicht in de verschillende [!DNL Adobe Experience Platform] betrokken diensten. Voordat u met deze zelfstudie begint, moet u de volgende services gebruiken:

* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Het gestandaardiseerde kader waardoor Platform gegevens van de klantenervaring organiseert.
* [[!DNL Real-Time Customer Profile]](../profile/home.md): Verstrekt een verenigd, klantenprofiel in echt - tijd die op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Hiermee kunt u een publiek opbouwen op [!DNL Real-Time Customer Profile] gegevens.

## Goedgekeurde schemavelden

Om de instemming en voorkeuren van de klant te respecteren, maakt een van de schema&#39;s deel uit van uw [!UICONTROL XDM Individual Profile] samenvoegingsschema moet de standaardveldgroep bevatten **[!UICONTROL Consents and Preferences]**.

Zie voor meer informatie over de structuur en het beoogde gebruik van elk van de kenmerken die door de veldgroep worden verschaft de [handleiding voor toestemmingen en voorkeuren](../xdm/field-groups/profile/consents.md). Voor geleidelijke instructies op hoe te om een gebiedsgroep aan een schema toe te voegen, verwijs naar [XDM UI-hulplijn](../xdm/ui/resources/schemas.md#add-field-groups).

Nadat de veldgroep is toegevoegd aan een [Schema met profiel ingeschakeld](../xdm/ui/resources/schemas.md#profile) en zijn gebieden zijn gebruikt om toestemmingsgegevens van uw ervaringstoepassing in te voeren, kunt u de verzamelde toestemmingsattributen in uw segmentregels gebruiken.

## Verwerking van toestemming in segmentatie

Om ervoor te zorgen dat opted-out-profielen niet in segmentdefinities worden opgenomen, moeten speciale velden worden toegevoegd aan bestaande segmentdefinities en worden opgenomen wanneer nieuwe segmentdefinities worden gemaakt.

In de onderstaande stappen wordt getoond hoe u de juiste velden kunt toevoegen voor twee soorten optievlaggen:

1. [!UICONTROL Data Collection]
1. [!UICONTROL Share Data]

>[!NOTE]
>
>Terwijl deze gids zich op de twee hierboven opt-out vlaggen concentreert, kunt u uw segmentdefinities vormen om extra toestemmingssignalen eveneens op te nemen. De [handleiding voor toestemmingen en voorkeuren](../xdm/field-groups/profile/consents.md) geeft meer informatie over elk van deze opties en het beoogde gebruik ervan.

Wanneer het bouwen van een segmentdefinitie in UI, onder **[!UICONTROL Attributes]**, navigeer naar **[!UICONTROL XDM Individual Profile]** selecteert u vervolgens **[!UICONTROL Consents and Preferences]**. Hier ziet u de opties voor **[!UICONTROL Data Collection]** en **[!UICONTROL Share Data]**.

![](./images/opt-outs/consents.png)

Begin door te selecteren **[!UICONTROL Data Collection]** categorie, en sleep vervolgens **[!UICONTROL Choice Value]** in de segmentbouwer. Wanneer u het kenmerk aan de segmentdefinitie toevoegt, kunt u de optie [toestemmingswaarden](../xdm/field-groups/profile/consents.md#choice-values) die moeten worden opgenomen of uitgesloten.

![](./images/opt-outs/consent-values.png)

Eén methode is om klanten uit te sluiten die ervoor hebben gekozen hun gegevens niet te laten verzamelen. Om dit te doen, plaats de exploitant aan **[!UICONTROL does not equal]** en kies de volgende waarden:

* **[!UICONTROL No (opt-out)]**
* **[!UICONTROL Default of No (opt-out)]**
* **[!UICONTROL Unknown]** (indien wordt aangenomen dat de toestemming wordt geweigerd indien anderszins onbekend)

![](./images/opt-outs/collect.png)

Onder **[!UICONTROL Attributes]** navigeer in het linkerspoor naar de **[!UICONTROL Consents and Preferences]** sectie selecteert u vervolgens **[!UICONTROL Share Data]**. De bijbehorende slepen **[!UICONTROL Choice Value]** in het canvas en selecteert u dezelfde waarden als voor de [!UICONTROL Data Collection] keuzevrijheid. Zorg ervoor dat een **[!UICONTROL Or]** Er wordt een relatie tussen de twee eigenschappen tot stand gebracht.

![](./images/opt-outs/share.png)

Met beide **[!UICONTROL Data Collection]** en **[!UICONTROL Share Data]** aan de segmentdefinitie toegevoegde toestemmingswaarden, klanten die ervoor gekozen hebben hun gegevens niet te gebruiken, zullen van het resulterende publiek worden uitgesloten. Vanaf hier kunt u de segmentdefinitie blijven aanpassen voordat u **[!UICONTROL Save]** om het proces te voltooien.

## Volgende stappen

Door deze zelfstudie te volgen, zou u een beter inzicht in moeten hebben hoe te om klantentoestemmingen en voorkeur te respecteren wanneer het bouwen van segmentdefinities in Experience Platform.

Raadpleeg de volgende documentatie voor meer informatie over het beheer van toestemming in Platform:

* [Goedkeuring met behulp van de Adobe-standaard](../landing/governance-privacy-security/consent/adobe/overview.md)
* [Goedkeuring verwerking gebruikend IAB TCF 2.0 norm](../landing/governance-privacy-security/consent/iab/overview.md)
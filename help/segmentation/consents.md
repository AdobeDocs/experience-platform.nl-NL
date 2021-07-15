---
keywords: Experience Platform;home;populaire onderwerpen;opt-out;Segmentatie;Segmenteringsservice;segmenteringsservice;eeroptie-outs;opt-out;opt-out;opt-outs;agreement;share;collection;
solution: Experience Platform
title: Constante waarderen in segmenten
topic-legacy: overview
description: Leer hoe u de voorkeursinstellingen voor toestemming van klanten voor het verzamelen van persoonlijke gegevens en het delen van gegevens in gesegmenteerde bewerkingen naleeft.
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
source-git-commit: bd312024a1a3fb6da840a38d6e9d19fcbd6eab5a
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---

# Naleving van toestemming in segmenten

Wettelijke privacyregels zoals de [!DNL California Consumer Privacy Act] (CCPA) bieden consumenten het recht om te weigeren dat hun persoonsgegevens worden verzameld of gedeeld met derden. Adobe Experience Platform biedt standaard XDM-componenten (Experience Data Model) die bedoeld zijn om deze voorkeuren voor toestemming van klanten vast te leggen in gegevens van het klantprofiel in real time.

Als een klant zijn toestemming voor het delen van persoonlijke gegevens heeft ingetrokken of geweigerd, is het belangrijk dat uw organisatie deze voorkeur respecteert bij het genereren van een publiek voor marketingactiviteiten. Dit document beschrijft hoe te om de waarden van de klantentoestemming in uw segmentdefinities te integreren gebruikend het gebruikersinterface van het Experience Platform.

## Aan de slag

Voor het respecteren van de waarden voor instemming van de klant is een goed begrip van de verschillende [!DNL Adobe Experience Platform] services vereist. Voordat u met deze zelfstudie begint, moet u de volgende services gebruiken:

* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Het gestandaardiseerde kader waardoor het Platform gegevens van de klantenervaring organiseert.
* [[!DNL Real-time Customer Profile]](../profile/home.md): Verstrekt een verenigd, klantenprofiel in real time die op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Staat u toe om publiekssegmenten van  [!DNL Real-time Customer Profile] gegevens te bouwen.

## Goedgekeurde schemavelden

Om de instemming en voorkeuren van de klant te respecteren, moet een van de schema&#39;s die deel uitmaken van uw [!UICONTROL XDM Individual Profile]-samenvoegingsschema de standaardveldgroep **[!UICONTROL Consents and Preferences]** bevatten.

Zie de [handleiding voor toestemmingen en voorkeuren](../xdm/field-groups/profile/consents.md) voor meer informatie over de structuur en het beoogde gebruik van alle kenmerken die door de veldgroep worden geleverd. Voor geleidelijke instructies op hoe te om een gebiedsgroep aan een schema toe te voegen, verwijs naar [XDM UI gids](../xdm/ui/resources/schemas.md#add-field-groups).

Zodra de gebiedsgroep aan een [profiel-Toegelaten schema](../xdm/ui/resources/schemas.md#profile) is toegevoegd en zijn gebieden zijn gebruikt om toestemmingsgegevens van uw ervaringstoepassing in te voeren, kunt u de verzamelde toestemmingsattributen in uw segmentregels gebruiken.

## Verwerking van toestemming in segmentatie

Om ervoor te zorgen dat opted-out-profielen niet in segmenten worden opgenomen, moeten speciale velden worden toegevoegd aan bestaande segmenten en worden opgenomen bij het maken van nieuwe segmenten.

In de onderstaande stappen wordt getoond hoe u de juiste velden kunt toevoegen voor twee soorten optievlaggen:

1. [!UICONTROL Data Collection]
1. [!UICONTROL Share Data]

>[!NOTE]
>
>Terwijl deze gids zich op de twee hierboven opt-out vlaggen concentreert, kunt u uw segmenten vormen om extra toestemmingssignalen eveneens op te nemen. In de [handleiding voor toestemmingen en voorkeuren](../xdm/field-groups/profile/consents.md) vindt u meer informatie over elk van deze opties en de gevallen waarin u deze wilt gebruiken.

Wanneer het bouwen van een segment in UI, onder **[!UICONTROL Attributes]**, navigeer aan **[!UICONTROL XDM Individual Profile]**, dan selecteer **[!UICONTROL Consents and Preferences]**. Vanaf hier ziet u de opties voor **[!UICONTROL Data Collection]** en **[!UICONTROL Share Data]**.

![](./images/opt-outs/consents.png)

Begin door **[!UICONTROL Data Collection]** categorie te selecteren, dan belemmering **[!UICONTROL Choice Value]** in de segmentbouwer. Wanneer u het kenmerk toevoegt aan het segment, kunt u de [toestemmingswaarden](../xdm/field-groups/profile/consents.md#choice-values) opgeven die moeten worden opgenomen of uitgesloten.

![](./images/opt-outs/consent-values.png)

Eén methode is om klanten uit te sluiten die ervoor hebben gekozen hun gegevens niet te laten verzamelen. U doet dit door de operator in te stellen op **[!UICONTROL does not equal]** en de volgende waarden te kiezen:

* **[!UICONTROL No (opt-out)]**
* **[!UICONTROL Default of No (opt-out)]**
* **[!UICONTROL Unknown]** (indien wordt aangenomen dat de toestemming wordt geweigerd indien anderszins onbekend)

![](./images/opt-outs/collect.png)

Navigeer onder **[!UICONTROL Attributes]** in de linkertrack naar de sectie **[!UICONTROL Consents and Preferences]** en selecteer **[!UICONTROL Share Data]**. Sleep de corresponderende **[!UICONTROL Choice Value]** naar het canvas en selecteer dezelfde waarden als die voor de gekozen waarde [!UICONTROL Data Collection]. Zorg ervoor dat een **[!UICONTROL Or]** verhouding tussen de twee attributen wordt gevestigd.

![](./images/opt-outs/share.png)

Als zowel de toestemmingswaarden **[!UICONTROL Data Collection]** als **[!UICONTROL Share Data]** aan het segment worden toegevoegd, zullen om het even welke klanten die uit het hebben van hun gegevens hebben verkozen worden uitgesloten van het resulterende publiek. Van hier, kunt u de segmentdefinitie blijven aanpassen alvorens **[!UICONTROL Save]** te selecteren om het proces te beëindigen.

## Volgende stappen

Door deze zelfstudie te volgen, zou u nu een beter inzicht in moeten hebben hoe te om klantentoestemmingen en voorkeur te respecteren wanneer het bouwen van segmenten in Experience Platform.

Raadpleeg de volgende documentatie voor meer informatie over het beheer van de toestemming in Platform:

* [Goedkeuring met gebruik van de Adobe-standaard](../landing/governance-privacy-security/consent/adobe/overview.md)
* [Goedkeuring verwerking gebruikend IAB TCF 2.0 norm](../landing/governance-privacy-security/consent/iab/overview.md)
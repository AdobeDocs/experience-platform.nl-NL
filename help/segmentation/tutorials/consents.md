---
solution: Experience Platform
title: Constante in segmentdefinities
description: Leer hoe te om de voorkeur van de klantengoedkeuring voor het verzamelen van persoonlijke gegevens en het delen in segmenteringsverrichtingen na te leven.
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 0%

---

# Erkenning van de toestemming in segmentdefinities

>[!NOTE]
>
>Deze gids verklaart hoe te om toestemmingen binnen **segmentdefinities** te respecteren.

Wettelijke privacyregels zoals de [!DNL California Consumer Privacy Act] (CCPA) bieden consumenten het recht om te weigeren dat hun persoonsgegevens worden verzameld of gedeeld met derden. Adobe Experience Platform biedt standaard XDM-componenten (Experience Data Model) die bedoeld zijn om deze voorkeuren voor toestemming van klanten vast te leggen in realtime gegevens van het klantprofiel.

Als een klant zijn toestemming voor het delen van persoonlijke gegevens heeft ingetrokken of geweigerd, is het belangrijk dat uw organisatie deze voorkeur respecteert bij het genereren van een publiek voor marketingactiviteiten. In dit document wordt beschreven hoe u de waarden voor klantmachtigingen in uw segmentdefinities kunt integreren met de gebruikersinterface van Experience Platform.

## Aan de slag

Voor het respecteren van de waarden voor toestemming van klanten is een goed begrip van de verschillende services van [!DNL Adobe Experience Platform] vereist. Voordat u met deze zelfstudie begint, moet u de volgende services gebruiken:

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde raamwerk waarmee Experience Platform gegevens over de ervaring van klanten organiseert.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): biedt een uniform, klantprofiel in real-time op basis van geaggregeerde gegevens van meerdere bronnen.
* [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): hiermee kunt u soorten publiek maken op basis van [!DNL Real-Time Customer Profile] -gegevens.

## Goedgekeurde schemavelden

Om de instemming en voorkeuren van klanten te respecteren, moet een van de schema&#39;s die deel uitmaken van uw [!UICONTROL XDM Individual Profile] -samenvoegingsschema de standaardveldgroep **[!UICONTROL Consents and Preferences]** bevatten.

Voor details op de structuur en het voorgenomen gebruiksgeval van elk van de attributen die door de gebiedsgroep worden verstrekt, zie de [ handleiding van de toestemmingen en van de voorkeursverwijzing ](../../xdm/field-groups/profile/consents.md). Voor geleidelijke instructies op hoe te om een gebiedsgroep aan een schema toe te voegen, verwijs naar de [ gids XDM UI ](../../xdm/ui/resources/schemas.md#add-field-groups).

Zodra de gebiedsgroep aan a [ profiel-Toegelaten schema ](../../xdm/ui/resources/schemas.md#profile) is toegevoegd en zijn gebieden zijn gebruikt om toestemmingsgegevens van uw ervaringstoepassing in te voeren, kunt u de verzamelde toestemmingsattributen in uw segmentregels gebruiken.

## Verwerking van toestemming in segmentatie

Om ervoor te zorgen dat opted-out-profielen niet in segmentdefinities worden opgenomen, moeten speciale velden worden toegevoegd aan bestaande segmentdefinities en worden opgenomen wanneer nieuwe segmentdefinities worden gemaakt.

In de onderstaande stappen wordt getoond hoe u de juiste velden kunt toevoegen voor twee soorten optievlaggen:

1. [!UICONTROL Data Collection]
1. [!UICONTROL Share Data]

>[!NOTE]
>
>Terwijl deze gids zich op de twee hierboven opt-out vlaggen concentreert, kunt u uw segmentdefinities vormen om extra toestemmingssignalen eveneens op te nemen. De [ toestemmingen en voorkeurenverwijzingsgids ](../../xdm/field-groups/profile/consents.md) verstrekt meer informatie over elk van deze opties en hun voorgenomen gebruiksgevallen.

Navigeer bij het maken van een segmentdefinitie in de gebruikersinterface onder **[!UICONTROL Attributes]** naar **[!UICONTROL XDM Individual Profile]** en selecteer vervolgens **[!UICONTROL Consents and Preferences]** , gevolgd door **[!UICONTROL Id Specific]** . Hier ziet u de opties voor **[!UICONTROL Data Collection]** en **[!UICONTROL Share Data]** .

![](../images/tutorials/opt-outs/consents.png)

Selecteer eerst de categorie **[!UICONTROL Data Collection]** en sleep vervolgens **[!UICONTROL Choice Value]** naar de gesegmenteerde ontwikkelaar. Wanneer het toevoegen van de attributen aan de segmentdefinitie, kunt u de [ toestemmingswaarden ](../../xdm/field-groups/profile/consents.md#choice-values) specificeren die moeten worden omvat of worden uitgesloten.

![](../images/tutorials/opt-outs/consent-values.png)

Eén methode is om klanten uit te sluiten die ervoor hebben gekozen hun gegevens niet te laten verzamelen. U doet dit door de operator in te stellen op **[!UICONTROL does not equal]** en de volgende waarden te kiezen:

* **[!UICONTROL No (opt-out)]**
* **[!UICONTROL Default of No (opt-out)]**
* **[!UICONTROL Unknown]** (als wordt aangenomen dat de toestemming wordt geweigerd indien anderszins onbekend)

![](../images/tutorials/opt-outs/collect.png)

Navigeer onder **[!UICONTROL Attributes]** in de linkertrack naar de sectie **[!UICONTROL Consents and Preferences]** en selecteer vervolgens **[!UICONTROL Share Data]** . Sleep de corresponderende **[!UICONTROL Choice Value]** ervan naar het canvas en selecteer dezelfde waarden als die voor de [!UICONTROL Data Collection] -keuzevrijheid. Zorg ervoor dat een **[!UICONTROL Or]** -relatie tot stand is gebracht tussen de twee kenmerken.

![](../images/tutorials/opt-outs/share.png)

Als zowel de toestemmingswaarden **[!UICONTROL Data Collection]** als **[!UICONTROL Share Data]** aan de segmentdefinitie worden toegevoegd, zullen om het even welke klanten die uit het hebben van hun gegevens hebben verkozen worden uitgesloten van het resulterende publiek. Vanaf hier kunt u de segmentdefinitie blijven aanpassen voordat u **[!UICONTROL Save]** selecteert om het proces te voltooien.

## Volgende stappen

Door deze zelfstudie te volgen, zou u nu een beter inzicht in moeten hebben hoe te om klantentoestemmingen en voorkeur te respecteren wanneer het bouwen van segmentdefinities in Experience Platform.

Raadpleeg de volgende documentatie voor meer informatie over het beheer van de toestemming in Experience Platform:

* [Goedkeuring met gebruik van de Adobe-standaard](../../landing/governance-privacy-security/consent/adobe/overview.md)
* [Goedkeuring verwerking gebruikend IAB TCF 2.0 norm](../../landing/governance-privacy-security/consent/iab/overview.md)
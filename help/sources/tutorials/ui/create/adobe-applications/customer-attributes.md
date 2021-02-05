---
keywords: Experience Platform;home;populaire onderwerpen;klantkenmerken
solution: Experience Platform
title: Creeer een BronVerbinding van de Attributen van de Klant in UI
topic: overview
type: Tutorial
description: Leer hoe u een bronverbinding maakt in de gebruikersinterface voor het verzamelen van klantkenmerkprofielgegevens naar Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 1%

---


# Een bronverbinding voor klantkenmerken maken in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een bronverbinding in de gebruikersinterface voor het verzamelen van klantkenmerkprofielgegevens naar Adobe Experience Platform. Voor meer informatie over de Attributen van de Klant, zie [overzichtsdocument](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html).

## Een bronverbinding maken

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer **[!UICONTROL Bronnen]** in de linkernavigatiebalk om de werkruimte Bronnen te openen. In het scherm **[!UICONTROL Catalog]** worden beschikbare bronnen weergegeven om binnenkomende verbindingen met te maken. Elke bron toont het aantal bestaande verbindingen dat aan deze verbindingen is gekoppeld. Selecteer de optie voor **[!UICONTROL Klantkenmerken]** en selecteer **[!UICONTROL Gegevens toevoegen]**. Toestaan dat de verbinding enige tijd kan duren, wordt u omgeleid als een verbinding tot stand is gebracht.

>[!NOTE]
>
>Als u reeds een bronschakelaar voor de profielgegevens van klantenattributen hebt gevestigd, zal de optie om met de bron te verbinden gehandicapt zijn.

![](../../../../images/tutorials/create/customer-attributes/catalog.png)

In het scherm **Bronactiviteit** worden alle eerder ingestelde verbindingen voor profielgegevens van klantkenmerken weergegeven. U kunt een nieuwe verbinding maken door op **Gegevens selecteren** te klikken.

>[!NOTE]
>
>De veelvoudige binnenkomende verbindingen aan een bron kunnen voor het brengen van verschillende gegevens worden gemaakt.

![](../../../../images/tutorials/create/customer-attributes/source_activity.png)

Selecteer in de lijst met beschikbare klantkenmerkprofielgegevenssets de gegevensset die u wilt opnemen in [!DNL Platform] en klik op **Volgende**.

>[!NOTE]
>
>Slechts één dataset kan per de bronverbinding van klantenattributen worden geselecteerd.

![](../../../../images/tutorials/create/customer-attributes/select_data.png)

De stap **Review** verschijnt, toestaand u om uw nieuwe binnenkomende verbinding te herzien alvorens het wordt gecreeerd. De details van de verbinding worden gegroepeerd per categorieën, die omvatten:

* **Brongegevens**: Hiermee geeft u het type van de bronverbinding en de geselecteerde brongegevens weer.
* **Doelgegevens**: Wanneer het creëren van andere bronschakelaars, toont deze container welke dataset de brongegevens opnemen in, met inbegrip van het schema de dataset zich aan houdt. Klantkenmerkprofielgegevens worden automatisch toegewezen en opgenomen in realtime profielen van klanten.

![](../../../../images/tutorials/create/customer-attributes/review.png)

## Volgende stappen

Zodra de verbinding wordt gecreeerd, wordt een doelschema en een dataset automatisch gecreeerd om de inkomende gegevens te bevatten. Wanneer de eerste opname is voltooid, kunnen de profielgegevens van klantkenmerken worden gebruikt door downstreamservices [!DNL Platform] zoals [!DNL Real-time Customer Profile] en [!DNL Segmentation Service]. Raadpleeg de volgende documenten voor meer informatie:

* [[!DNL Real-time Customer Profile]  - overzicht](../../../../../profile/home.md)
* [[!DNL Segmentation Service]  - overzicht](../../../../../segmentation/home.md)
